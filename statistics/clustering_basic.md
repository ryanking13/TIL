# Clustering basic

> 2019/10/17

## What is clustering

개체들을 여러 개의 cluster로 묶는다.

목표는,

- minimize inner-cluster variance
- maximize outer-cluster variance

## Clustering vs Classification?

- Clustering: 비지도학습
- Classification: 지도학습

## 군집타당성지표(Clustering Validity Index)

비지도학습이므로 클러스터링 결과의 명확한 정확도(Accuracy)를 구하는 것은 어려움.

따라서 군집 간 거리, 군집 내의 거리 및 분산 등을 활용함.

### Dunn Index

군집 간 최소 거리/군집 내 최대 거리 (클수록 좋음)

### Silhouette

(이웃 군집 거리 평균 - 내 군집 거리 평균) / max(내 군집 거리 평균, 이웃 군집 거리 평균)

### References

> https://ratsgo.github.io/machine%20learning/2017/04/16/clustering/
