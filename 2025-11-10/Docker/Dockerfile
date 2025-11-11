FROM ubuntu:22.04@sha256:27cb6e6ccef575a4698b66f5de06c7ecd61589132d5a91d098f7f3f9285415a9
#Ubuntu 22.04 이미지 사용

ENV user chall
ENV chall_port 31337
#환경 변수 user=chall, chall_port=31337 설정

RUN apt-get update
RUN apt-get install -y python3
#Python3 설치

RUN adduser $user
#사용자 chall 생성

COPY ./deploy/flag /home/$user/flag
#./deploy/flag 파일을 /home/chall/flag로 복사

RUN chown -R root:$user /home/$user
#해당 디렉터리의 소유권을 root:chall로 변경

WORKDIR /home/chall
#/home/chall으로 이동 후:
RUN touch `python3 -c "print(open('./flag', 'r').read())"`
#flag 파일 내용을 읽어서 touch로 파일 생성
RUN rm *
#rm *로 모든 파일 삭제

WORKDIR /home
USER $user
EXPOSE $chall_port
#/home으로 이동하고, chall 사용자로 전환, 포트 31337 노출



#위의 내용을 보면, deploy 디렉터리 안에 있는 flag 파일을 /home/chall/flag에 복사를 하고,  
#touch 명령어를 통해./flag파일을 열어서 읽고 출력이 된 것을 파이썬 명령어로 실행하므로 
#flag 파일 내용(플래그)을 이름으로 갖는 파일이 생성된다는 사실을 알 수 있다. 

#하지만, 그다음의 명령어를 보면 현재 디렉터리인 home/chall 에 존재하는 
#모든 파일을 삭제하는 명령어인 RUN rm * 를 볼 수 있고, 문제에서 구하고자 하는 플래그를 찾기 위해서는 

#= 삭제가 되기 이전에 대한 정보를 얻어야 한다는 사실을 알 수 있다.