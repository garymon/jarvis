## QNAP NAS를 VPN서버로 활용 하기

* QTS 4.3 버전 이상 부터는 QVPN Service어플리 케이션을 설치하면 된다.
  * 3가지 방식의 연결 설정을 허용

## OpenVPN
  * open vpn설정을 한후 QVPNService -> OpenVPN 화면에 접속해서 인증서를 다운로드
  * open vpn client
    * mac
      * https://tunnelblick.net/ 에서 클라이언트를 다운.
      * nas에서 다운받은 open vpn인증서를 풀면 .ovpn파일이 생성되는데 해당 파일을 상단 tunnelblick 아이콘으로 드래그 하여 설정 등록.
      * openvpn연결 클릭후 계정 및 비밀번호 입력.
      * 10.8.0.1로 접근하면 nas 기본 페이지가 보이면 성공
