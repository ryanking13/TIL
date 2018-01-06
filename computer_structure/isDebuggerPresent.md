# isDebuggerPresent

kernel32.dll에 속한 함수로 현재 프로세스가 디버깅 중인지를 탐색한다.

```C
BOOL IsDebuggerPresent(){
  BOOL debugging = FALSE;
  __asm
  {
    mov eax, dword ptr fs:[0x18]
    mov eax, dword ptr ds:[eax+0x30]
    movzx eax, byte ptr ds:[eax+2]
    mov debugging, eax
  }
  return debugging;
}
```

fs:[0x18] 은 TEB(Thread Environment Block) 구조체에 해당한다.

TEB+0x30 은 PEB (Process Environment Block) 구조체에 해당한다.

PEB+0x2에는 BeingDebugged 라는 bool 타입 변수가 존재한다.
