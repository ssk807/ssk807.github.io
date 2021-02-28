---
title: "Shell controll Using window VScode"
excerpt: "VritualBox Ubuntu를 Window환경 VScode를 이용하여 편집과 제어하기"

categories:
  - Rinux
tags:
  - Rinux
  - Ubuntu
  - VScode
last_modified_at: 2020-07-24
---


## VirtualBox에서 ssh 서버 설치  
```
sudo apt-get install openssh-server
sudo apt-get update
```  
위 명령어를 통해 ssh server를 설치해준다.  

<p align="center">
	<img src="https://ssk807.github.io/assets/images/ssh_1.png">
</p>  
설치가 완료되면 가상머신을 종료한 후 virtualBox 환경설정에 들어가준다.


<p align="center">
	<img src="https://ssk807.github.io/assets/images/ssh_2.png">
</p>  

그리고 __네트워크 -> 어댑터2 -> 호스트전용 어댑터__ 를 설정해주고 확인을 눌러 설정을 저장한다.  

<p align="center">
	<img src="https://ssk807.github.io/assets/images/ssh_3.png">
</p>  
다시 가상머신을 실행시켜주고 터미널 창을 킨다. 터미널 창에서 ifconfig라는 명령어를 치게 되면 ssh server의 ip주소가 생긴 것을 확인할 수 있다.  

## VScode 설정  
<p align="center">
	<img src="https://ssk807.github.io/assets/images/vscode_1.png">
</p>  
VSCode를 켜주고 extension -> 검색창에 remote-dash를 검색해주어 설치를 해준다.  

<p align="center">
	<img src="https://ssk807.github.io/assets/images/vscode_2.png">
</p>  
왼쪽 하단 모서리에 생긴 초록색 >< 모양 아이콘을 선택 -> Remote-SSH: Connect to Host.. -> Add New SSH Host... 까지 진행하면 위 화면과 동일한 화면이 나오게 된다.  
여기서 ssh 본인 virtualbox 계정 이름@위에서 확인했던 ip 주소 를 입력해주고 엔터를 누르고 맨 위 설정을 선택해주면 연결이 완료된다.  

<p align="center">
	<img src="https://ssk807.github.io/assets/images/vscode_3.png">
</p>  
여기까지 완료가 되면 다시 왼쪽 하단에 원격 창 열기 아이콘을 누르고 Remote-SSH: Connect to Host..를 누르게 되면 방금 전 연결했던 ip 주소가 생기게 된다. 클릭하면 새로운 작업 창이 열리며
 자신의 가상머신 환경과 연동이 된 모습을 확인할 수 있다.  
