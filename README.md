# port_close
포트 닫기(CLOSING)
## 실무 적용 가이드 라인

/etc/service 폴더 열어서 각 포트가 어떤 프로토콜에 의해 사용되는지 빠르게 판단
포트를 사용하는 프로그램을 2차적으로 확인,
확인방법 -> lsof -i TCP:port 그 포트를 사용하는 프로그램명을 확인,

## 프로그램 죽이기
fuser -k -n tcp port번호 (ex: fuser -k -n tcp 22)
tcp 22번 포트를 닫겠다(선제적으로 프로그램을 죽이겠다)

## 프로그램 살리기
프로그램을 구동하면 다시 살아남
살리는법 : 리눅스-> /etc/rc.d/init.d/httpd start -> 80 443 start
/etc/rc.d/init.d/sshd start -> ssh -> 22port 22포트가 살아남

## d의 뜻 (데몬)
데몬 파일이라고 들어봤을 것이다.
httpd directory traversal, 왜 프로토콜 뒤에 d 가 붙는가?
서비스 실행 파일(예: httpd, sshd 등)의 이름 뒤에 붙는 d는 **데몬(Daemon)**을 의미합니다.

🔹 d의 의미:
데몬(Daemon): 백그라운드에서 실행되는 프로세스를 뜻함.
보통 서버에서 클라이언트 요청을 처리하는 역할.
예:
httpd → Apache HTTP Server 데몬 (웹 서버, 80/443 포트)
sshd → SSH 데몬 (SSH 원격 접속, 22포트)
즉, httpd는 웹 서버 데몬을 실행하고, sshd는 SSH 접속을 위한 데몬을 실행하는 역할을 합니다.

바로 백그라운드에서 행해지는 공격임을 알 수 있다.

백
