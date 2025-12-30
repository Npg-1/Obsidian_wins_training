## ipconfig ##
- 네트워크 인터페이스 정보 확인
	- ipconfig/all: 상세정보 표시
	- ipconfig/release: ip 주소 해제
	- ipconfig/renew: ip  주소를 새롭게 갱신하여 네트워크 재연결


## hostname ##
- 내 컴퓨터 이름


## cls(Clear Screen) ##
- 화면 비우기


## dir ##
- 현재 디렉토리 파일 및 하위 디렉토리 폴더 목록을 보여주는 명령어


## whoami ##
-  지금 로그인한 계정 확인


## netstat(Network Statistics) ##
- 내 컴퓨터와 연결된 **모든 네트워크 연결 상태**를 확인할 때 사용하는 명령어
- 현재 어떤 포트가 열려 있는지, 어떤 프로그램이 외부와 통신하고 있는지 등을 표시함
	- ex1) netstat -a: 모든 포트를 표시함
	- ex2) netstat -an: 모든 포트를 포트이름(ex: localhost)가 아닌 숫자로 표시함
	- ex3) netstat -nr: 라우팅 테이블 정보 확인 <=> 


## nslookup (상대 도메인) ##
- 특정한 도메인을 DNS(Domain Name System)에 보내서 ip주소를 받아오는 명령어
	- ex) nslookup naver.com: naver.com 이라는 네이버 도메인을 dns에 보내서 ip를 받아옴


## ping (상대방 ip) ##
- 상대방 호스트의 상태를 확인하기 위해 사용, 응답이 오면 상대방이 살이있고, 안 온다면 죽어있거나 방화벽같은 것 때문에 안 오는 것, 또는 서로 연결이 안 되어서 일 수도 있음 
- icmp 프로토콜을 사용함
	-  ex) ping 8.8.8.8: 구글 공용 DNS 서버의 IP주소가 살아있는지 확인


## tracert (traceroute) (목적지 주소) ##
- 목적지까지의 경로를 확인하기 위해 사용
	- ex) tracert 8.8.8.8: 구글 공용 DNS까지 가는 도중의 경유지를 출력함


## arp -a ##
- ip 주소(인터넷 주소, 논리적 주소)와 MAC주소(물리적 주소, 하드웨어 주소)를 매핑하는 프로토콜
- 같은 LAN끼리 바로 옆의 근거리 자리와 통시하려면  IP주소가 아니라 MAC 주소가 필요함 원거리로 통신하려면 IP주소가 필요 (이 정보는 확인 필요)


## route print(<=>netstat -nr) ##
- 라우팅 테이블 정보 확인





## CMD wsl 명령어 ##
- wsl --install
	- WSL 기능 활성화, 가상 머신 플랫폼 활성화, 최신 리눅스 커널 다운로드 및 우분투를 기본값으로 설치하는 과정을 처리함


- wsl -l / wsl -v
	- wsl -l(list): 설치된 배포판 리스트 표시
	- wsl -v(verbose): 상세 정보 표시
	- wsl -l -v: 배포판 리스트에 대한 상세 정보 표시
		- 이 때 리스트에서 NAME앞에 \* 표시가 되어있는 건 현재 기본 리눅스 배포판으로 설정되어 있는 것임
		- 기본 배포판은 wsl 명령어에서 이름을 따로 지정하지 않으면 기본 배포판을 실행
			- ex) wsl -d UbuntuA 를 하면 UbuntuA가 실행되지만 그냥 wsl -d를 하면 기본 배포판의 리눅스가 실행됨


- wsl -d UbuntuA
	- -d(distribution): 지정한 이름의 배포판을 실행
	- UbuntuA: 실행하고 싶은 배포판의 이름
		- ->이 명령어를 실행하면 Ubuntu가 실행돼서 이때부터는 cmd 명령어가 아닌 [[우분투 명령어]]를 써야함

- wsl --terminate UbuntuA
	- 현재 Running 상태인 UbuntuA를 Stopped으로 바꿈, 정지시킴
		- -> wsl --shutdown 을 통해 모든 운영체제를 한 번에 종료할 수도 있음

- wsl --export Ubuntu ubuntu_base.tar
	- 기존 우분투 내보내기
	- 기존 우분투를 ubuntu_base.tar 이라는 파일로 만들어서 해당 명령어를 작성한 위치로 내보냄
		- ex) C:\Users\wjddn> wsl --export ubuntu ubuntu_base.tar
			- C:\Users\wjddn에 ubuntu_base.tar로 백업파일이 생김


- wsl --import UbuntuA C:\Wjddn_WSL\UbuntuA ubuntu_base.tar
	- 기존에 백업해둔 리눅스 시스템(ubuntu_base.tar)을 사용해서 UbuntuA라는 이름의 새로운 독립된 운영체제를 생성하라는 명령어
	- 구성 요소 분석
		- wsl: Windows Subsystem for Linux 실행 프로그램입니다.
		- --import: "외부에 저장된 파일을 가져와서 새로운 리눅스 배포판으로 등록하겠다"는 옵션입니다.
		- UbuntuA: 새롭게 만들 운영체제의 **이름**입니다. 앞으로 이 이름을 통해 해당 운영체제를 실행하게 됩니다. (예: `wsl -d UbuntuA`)
		- C:\WSL\UbuntuA: 이 새로운 운영체제의 **실제 데이터(가상 하드디스크 파일)가 저장될 위치**입니다. 윈도우 탐색기에서 이 폴더를 가보면 `ext4.vhdx`라는 파일이 생기게 됩니다.
		- ubuntu_base.tar: 아까 `export` 명령어로 만들어두었던 **원본 백업 파일**입니다. 이 파일 안에 있는 내용물들이 `C:\WSL\UbuntuA` 경로에 풀리면서 설치가 진행됩니다.


## shutdown ##
- wsl 위에 돌아가는 모든 서비스를 한 번에 종료함
	- ex) wsl -- shutdown


## terminate ##
- 위에서 돌아가고 있는 Ubuntu를 종료하기
	- ex) wsl -t Ubuntu
	- ex) wsl --terminate Ubuntu


- wsl --unregister UbuntuA
	- WSL에서 UbuntuA라는 이름의 리눅스 배포판을 시스템에서 완전히 등록 해제하고 삭제하는 명령어


우분투 관련 경로
- C:\Users\wjddn\ubuntu_base.tar 
	- -> 아마도 이건 C:\Users\wjddn> wsl --export ubuntu ubuntu_base.tar을 해서 그런 거 같음
- C:\Wjddn_WSL\UbuntuA\ext4.vhdx
- \\wsl.localhost\Ubuntu
	- -> wsl --import UbuntuA C:\WSL\UbuntuA ubuntu_base.tar를 해서 생긴 거 같음


















































