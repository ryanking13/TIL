# PNG structure

> 2018/02/21 - init

`PNG` 파일은 시그니쳐 + N 개의 chunk로 구성된다.

- signature : `89504E470D0A1A0A`

- chunk structure

```
{
  Length (4 byte),
  Chunk Type (4 byte),
  Chunk Data (length byte),
  CRC (4byte)
}
```

 주요 chunk type들

 - IHDR : PNG 파일의 정보를 나타내는 chunk, 맨 앞에 위치해야 함
 - IDAT : 실제 이미지 정보를 담은 chunk
 - IEND : PNG 파일의 끝을 나타내는 chunk

 ### IHDR

 ```
{
  Length : 00 00 00 0D (13 byte),
  Chunk Type : IHDR,
  Chunk Data ( 13 byte ),
  {
    Width (4 byte),
    Height (4 byte),
    Bit depth (1 byte),
    Color Type (1 byte),
    Compression method (1 byte),
    Filter method (1 byte),
    Interlace method (1 byte),
  }
  CRC,
}
 ```

 `Width`와 `Height`는 이미지 파일에는 이미지 파일의 크기가 기록된다. 실제 IDAT의 크기와 관계없이 이미지 뷰어, 브라우저등은 위 크기를 보고 이미지를 디코딩한다.

 `Bit depth`는 하나의 채널이 몇개의 비트로 구성되는 지를 나타내는 값이며, `Color type`은 이미지가 흑백, RGB, RGBA 등으로 구성되는 것을 정의한다.

 `Color type`에 따라 가능한 `Bit depth`가 다르며, 하나의 채널이 1바이트 미만의 비트로 구성되기도 한다. (전체 조합은 [이곳](https://www.w3.org/TR/PNG/#11IHDR)에서 볼 수 있다)


 `Compression method`는 현재 0 ([deflate](https://en.wikipedia.org/wiki/DEFLATE)) 밖에 지원되지 않는다.

 `Filter method`역시 현재 0 한 가지만 지원된다.

 `Interlace method`는 0 (no interlace) 1 ([Adam7](https://en.wikipedia.org/wiki/Adam7_algorithm) interlace) 두 종류가 지원된다.

 ### IDAT

 한 PNG 파일은 여러개의 IDAT chunk를 가질 수 있는데, 이는 단순히 데이터를 스트리밍 방식으로 전달하기 위함이다.

 IDAT에 저장된 chunk는 압축된 데이터이므로 전체 chunk를 합쳐야 디코딩이 가능하며, 각 chunk를 독립적으로 디코딩하는 것을 불가능하다. 즉 하나의 IDAT이라도 삭제되면 이미지를 디코딩할 수 없다.

 IDAT에 들어가는 데이터는 원시 픽셀 데이터에서 필터링, 압축 과정을 거친 데이터다.

```
Encoding : Pixel Data(Original data) --> Filter --> Compression --> IDAT chunk data

Decoding : IDAT chunk data --> Decompression --> Unfilter --> Pixel data
```

필터링은 이미지의 압축률을 높이기 위해 이루어지는 과정이며, scanline(row) 단위로 이루어진다.

각 scanline 단위로 휴리스틱 방식으로 적절한 filter type을 찾아 중 하나를 정용한다.

Filter 0의 filter type은 5 가지가 있으며, 전체 리스트는 [이곳](https://www.w3.org/TR/PNG/#11IHDR)에서 볼 수 있다.

```
 R G B R G B R G B R G B R G B     Original image
 R G B R G B R G B R G B R G B
 R G B R G B R G B R G B R G B
 R G B R G B R G B R G B R G B
 R G B R G B R G B R G B R G B
 R G B R G B R G B R G B R G B

             |
             | filtering
             |
             |

F d d d d d d d d d d d d d d d     Filtered Image Data
F d d d d d d d d d d d d d d d
F d d d d d d d d d d d d d d d
F d d d d d d d d d d d d d d d
F d d d d d d d d d d d d d d d
F d d d d d d d d d d d d d d d
```

필터링 후에는 각 scanline 맨 앞에 filter type이 기록되어 디코딩 시에 참조한다.

---

### Reference

> https://www.w3.org/TR/PNG

> http://halicery.com/Image/png/pngdecoding.html

> http://www.libpng.org/pub/png/spec/1.2/PNG-Chunks.html
