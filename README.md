# _Lecture_Ansible.Update1

응용 강의와 심화 강의의 "앤서블 2.5 새로운 점" 섹션 실습 코드입니다.

## 참고

HCP Vagrant(Vagrant Cloud)가 2026년 12월 31일에 종료되어 Vagrantfile에 박스 주소(`box_url`)를 넣었습니다. CentOS 7은 지원이 끝나 기본 저장소로는 `yum`이 실패하므로 서버마다 `vault_repo_4_CentOS.sh`로 보관 저장소를 먼저 설정합니다.

지금 CentOS 7에서 `yum install ansible`을 하면 2.4 서버는 설치하지 못하고 2.5 서버는 EPEL의 2.9가 설치됩니다. 2.9에서는 `nxos_config`의 `save`가 없어지고 tftp 백업에 쓰는 `ansible_all_ipv4_addresses`가 정의되지 않아 실습이 실패합니다. 그래서 `ansible-server24`는 2.4.2, `ansible-server25`는 2.5.15를 설치하게 고정했습니다.

스위치는 [`_Lecture_Ansible.adv`의 `ch8/8.4`](https://github.com/sysnet4admin/_Lecture_Ansible.adv/tree/master/ch8/8.4)로 만듭니다. 서버가 프로비저닝할 때 스위치의 SSH 키를 받아 두므로 스위치를 먼저 켜고 서버를 켭니다. 나중에 켠 스위치는 서버에서 `ssh-keyscan <스위치 IP> >> ~/.ssh/known_hosts`를 실행한 뒤 실습합니다.

`vrf management`를 쓰는 실습(`nxos_ping`, tftp 백업)은 스위치의 관리 포트(VirtualBox NAT)에서 실습 PC를 거쳐 서버로 갑니다. 실습 PC가 192.168.1.0/24 네트워크에 있어야 동작합니다. 다른 네트워크라면 `vrf management`를 `vrf default`로 바꿔 실습합니다.
