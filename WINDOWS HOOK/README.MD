# WINDOWS HOOK

보안 솔루션이나 CS 프로그램 같은 경우 후킹이 필요할때가 있다.  

powershell을 이용하거나 System Infomer 와 같은 툴을 이용해서 덤프 후

리버싱 툴 (IDA, ghidra)를 통해 분석한다.

혹은 frida를 통해 바로 분석해도 상관은 없으나 안티 로직이 걸려있으면 정적 분석부터 시작  

내가 가장 먼저 하는 것은 커스텀된 dll을 찾아 분석하는 것이다.  

커스텀된 dll은 암/복호화, 감지 로직등이 있을 확률이 높다.  

두번째는 감지 매커니즘에 대해서 콜스택을 추적하는 것이다.

함수명을 추출할 수 없거나(심볼 정보 삭제 등) 오프셋만으로 추적해야 하는 경우가 대부분이며

이에 대한 힌트를 얻기 위해서는 콜스택 추적이 가장 효과가 좋았다.

만약에 특정 감지로직이 되면 윈도우 창이 비활성화되는 프로그램이 있다 치자

감지 매커니즘 작동 시 콜스택에서 SetWindowDisplayAffinity,  SetLayeredWindowAttributes, NtUserShowWindow, BitBlt 등의 함수가 표기된다.



## ------------------
WPF로 개발된 애플리케이션 .NET Framework 또는 .NET Core 기반의 WPF 응용 프로그램일 경우  
snoop 툴로 진행하면 훨씬더 쉽다.  


## ------------------------

CRC 등 무결성 검사로 인해 디버깅 탐지 후 프로세스 강제 종료 시 방법

ntdll.NtTerminateProcess와 같은 종료 함수에 주단점을 설정 후

서브 루틴에 nop (0x90) 및 ret(0xC3)을 통해 그냥 리턴하도록 변경

cmp함수를 통해서 검사하는 부분의 벡터를 찾는게 핵심
