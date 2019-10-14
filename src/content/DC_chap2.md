---
layout: post
title: chap2_Protocol architecture, TCP/IP and internet-Based Application
image: img/callum-shaw-555357-unsplash.jpg
author: 0verc10ck
date: 2019-10-14T10:00:00.000Z
tags:
  - 데이터 통신
---


본 강의는 경북대학교 컴퓨터학부 [김동균](https://monet.knu.ac.kr/) 교수님의 데이터 통신 수업을 듣고 그 내용을 정리한 것입니다.

양질의 자료와 강의를 제공해주신 [김동균](https://monet.knu.ac.kr/) 교수님께 감사의 말씀 올립니다.

강의의 내용과 제가 공부한 내용에 기반하기 때문에 부정확한 정보가 있을 수 있는점 주의하시기 바랍니

# Protocol Architecture

  1.  Protocol Architecture의 필요성
    
        두 기기간의 데이터 교환이 일어나는 과정은 상당히 복잡하고, 많은 요구사항이 요구된다.

        다음은 데이터 교환을 위해 수행되어야하는 최소한의 작업들이다.

        - 발신 시스템은 데이터 전송로를 직접 가송 시키거나, 목적지 시스템의 식별자를 통신망에 알려야 한다.
        
        - 발신 시스템은 목적지 시스템이 데이터를 받을 준비가 되어 있는가를 확인해야 한다.

        - 발신 시스템의 파일 전송 응용프로그램은 목적지 시스템의 파일 관리 프로그램이 파일을 받아 저장할 준비가 되어잇는가 확인해야 한다.

        - 두 시스템에서 사용되는 파일 형식이다를 경우, 형식 변환이 수행되어야 한다.

        데이터 교환이 일어나려면 이처럼 두 시스템간의 고차원적인 상호 협력이 필요하다.

        이러한 작업을 하나의 모듈로 구현하는 것 보다는 여러개의 소규모 작업으로 나누어 구현하는것이 Error correction에 있어 유리하다.

        Protocol Architecture에서는 모듈은 vertical stack으로 쌓인다. 각 계층은 다른 시스템과 통신하는데 필요한 기능들 중 자신과 관련된 부분을 수행한다.

        각 계층은 자신의 하부 계층에서 제공하는 기본 서비스를 이용하며 하위 계층의 기능에 대한 자세한 사항은 알 필요가 없다.

        각 계층은 바로 위 사우이 계층에게 서비스를 제공한다.

        각 계층이 변경되더라도 다른 계층에는 전혀 영향을 주지 않도록 정의하는것이 가장 이상적이다.

        통신이 이루어지면 두 시스템의 동일한 계층끼리 Peer(동료)가 존재해야 하낟. Peer들은 Protocol이라고 불리는 정해진 규칙에 따라 일정한 형식의 데이터 블록들을 교환 함으로써 통신한다. Protocol의 3가지 Key Feature는 다음과 같다.

        - Syntax(문법) : 데이터 블록의 형태 
        
        - Semantics(의미론) : 조정과 오류 관리를 위한 제어정보
        
        - Timing(타이밍) : 속도 조절과 순서 조정

  2. 간단한 Protocol 구조

        일반적으로 데이터 통신은 Application, Computer, Network 3개의 에이전트를 포함한다.

        데이터가 전송될 때 Source의 Applciation에서 Computer, Network를 거쳐 Destination의 Computer에 도착하고 최종적으로 Destination의 Application에 도달하게 된다.

        이러한 개념을 적용하면 통신작업을 크게 독립적인 3개로 나눌 수 있다.

        -   Network access layer : Network와 Computer 간의 데이터 교환을 다룬다.

        -   Transport layer : mechanism을 common layer에 모아두고, application이 공유하도록 한다.

        -   Applicatin layer : application을 지원할 logic들을 담고 있다.

        ![ProtocolArchitectur](https://slideplayer.com/slide/7084980/24/images/11/Protocol+Architecture+and+Networks.jpg)

        ![simplified](https://image.slidesharecdn.com/02-protocolarchitecture-111113051534-phpapp02/95/02-protocol-architecture-12-728.jpg?cb=1321162215)

        위의 두 그림은 Protocol의 간단한 구조를 보여준다.

        올바른 통신을 위해서는 시스템 내의 모든 개체가 반드시 유일한 자신만의 주소를 가지고 있어야 한다.

        네트워크 상의 모든 컴퓨터는 자신만의 유일한 주소를 가지고 있고, 그 컴퓨터 위에서 동작하는 프로세스들 또한 유일한 주소를 가지고 있어야한다.

        프로세스들을 구별하는 주소를 Port또는 SAP(Service access point)라고 하며, Source에서는 Destination의 주소와 Port를 알고 있어야 통신이 가능하다.

        첫번째 그림은 각 컴퓨터의 Peer들이 Protocol을 사용하여 상대방과 통신한다는 것을 대략적으로 보여준다.

        이러한 통신이 이루어지기 위해서는 다양한 동작들이 수반되어야 하고 이를 제어할 정보또한 데이터와 함께 전송되어야 한다.

        두번째 그림은 각 계층에서 추가되는 제어 정보들과 이 제어 정보들이 통신에서 활용되는 방법을 나타낸 것이다.

        Application layer는 데이터 블록을 만들어 Transport layer로 넘긴다.

        Transport layer에서는 Header라를 데이터 블록에 붙여 Segment라고 불리는 PDU(Protocol Data Unit)로 만드는데 이러한 작업을 encapsulation이라고 한다.

        Header에 포함된 항목에는 다음과 같은것이 있다.

            - Source port : 데이터를 보내는 Applicaition을 가리키는 주소
            
            - Destination port : 데이터를 수신할 Application을 가리키는 주소
            
            - Sequence Number : 여러 데이터를 송신할 경우 데이터의 송신 순서

            - Checksum : Frame check sequence라고도 하며, 특정 연산을 통해 데이터의 무결성을 확인
            
            값이 일치하지 않을 경우 전송과정에서 데이터 손상이 일어났다는것을 의미

        Network layer에서는 Transport layer에서 전송받은 segment에 추가적인 정보를 붙여 Packet이라고 불리는 PDU를 만든다.

        Packet에서 추가된 항복에는 다음과 같은것이 있다.

            - Source Address : Packet의 발신지를 가리키는 주소
            
            - Destination Address : Network가 어떤 컴퓨터로 Packet을 전송해야 할지 알리는 주소

            - Service Request : NAP(Network Access Protocol)이 우선순위와 같은 Sub-network service를 사용할 수 있도록 정보를 담는 곳







         

    



# TCP/IP Protocol Architecture

    TCP/IP Protocol Architecture는 ARPANET에서 수행된 protocol 연구와 개발의 결과이다.

    TCP/IP protocol suit라고 불리우며, TCP/IP는 Internet의 표준인 대규모 Protocol을 구성한다.


  1. TCP/IP Layer

      통신은 크게 5 level의 layer로 구분된다.
      
      ![tcp_ip](/src/contetn/img/../../content/img/TCP-IP.png)

      1. Application Layer : TCP/IP 환경의 사용자 접속을 제공하며, 분산 정보 서비스를 제공한다. Application을 지원하기 위해 필요한 작업들을 다룬다.

      2. Transport Layer : 종단간 데이터 전달을 수행하며 오류제어, 흐름제어, 혼잡제어, 신뢰가능한 배달 서비스를 제공한다.

      3. Internet Layer : 상위 계층을 네트워크의 물리적 구성의 세부 사항으로 부터 차단하고. 경로지정을 담당하며 서비스 품질과 혼잡 제어를 제공한다.

      4. Network Access/Data Link Layer : 동일한 Network에 접속된 2개의 종단 시스템이 네트워크에 접속하고 데이터를 전달 하는것을 다룬다.

      5. Physical Layer : 데이터 전송 장치와 전송매체 또는 네트워크 사이의 물리적인 Interface를 다룬다. 전송매체의 특성, 신호의 특성, Data rate등과 같은 관련사항을 규정한다.


  2. TCP/IP의 동작
  
      ![tcp_ip](/src/contetn/img/../../content/img/concepts.png)

      위 그림은 TCP/IP Protocol이 어떻게구성되는지를 보여준다.

      Host A의 App X와 Host B의 App x가 통신하는 과정은 다음과 같다.

      예를 들어 Host A의 port 3과 연결된 App X가 Host B의 port 2와 연결된 App X로 메시지를 보낸다고 가정해 보자.

      A에 있는 Process는 B의 port 2에 전송하라는 명령과 함께 message를 TCP에 넘길 것이다.

      TCP는 메시지를 Host B에게 전달하라는 명령을 추가하여 IP에게 넘긴다.

      이때 IP는 어떤 Port를 찾아가야하는지 알지 못해도 된다. 다만, Host B로 가야한다는 사실만 알고 있으면 된다.

      IP는 Host B에게로 가기 위해 Router J로 전송하라는 명령과 함께 데이터 블록을 NAP로 내려 보낸다.

      NAP를 통해 Router J로 전달된 데이터는 Router J를 거쳐 Host B에 도달하게 된다.

      Host B에서는 Host A가 추가한 정보들을 하나씩 벗겨가며 데이터를 어디 전송해야 하는지 파악하고 데이터를 목적지인 App X에 전달한다.
      
      ![PDU](/src/contetn/img/../../content/img/PDU.png)

      위 그림은 데이터가 각 Layer를 거치며 정보가 추가되는 과정을 나타낸 그림이다. 

      전달하고자 하는 원본 데이터는 TCP Layer에서 TCP Header를 추가하여 TCP Segment가 되고, IP Layer에서 IP Header를 추가하여 Datagram이 되고, Network layer에서 Network Header를 추가하여 Packet이 된다.


  3. TCP/UDP, IPv4/IPv6

      1. TCP/UDP

          TCP(Transmission Control Protocol)은 대부분의 Application을 위한 Transport layer이다.

          TCP는 Applicaition 사이의 신뢰적인 데이터 전송을 보장하는 연결을 제공한다.

          TCP segment는 기본 Protocol unit이다.

          TCP는 각 개체의 연결이 지속되는 동안 다른 개체로 부터 오고가는 TCP segment를 추적하여 흐름을 제어하고, 분실 또는 훼손 된 segment를 복구한다.

          UDP(User Datagram Protocol)은 TCP의 대용으로 사용된다.

          UDP는 전송의 순서, 중복전달 방지가 보장되지 않는다.

          UDP는 최소한의 protocol 기법을 이용하여 두 procdure 사이의 통신을 가능하게 한다.

          주로 SNMP(Simple Network Management Protocol)과 함께 사용된다.

          데이터의 오류를 확인하는 checksum가지고 있으며, 기본적으로 IP에 port 지정 기능을 추가하는 정도로 사용된다.

          아래 그림은 TCP와 UDP Header의 구조이다.

          ![TCP/UDP](/src/contetn/img/../../content/img/tcpdup.png)



      2. IPv4/IPv6

          TCP/IP protcol의 중심은 IP라 불리우는 IPv4였다.

          IPv4 Header 20 octet 또는 160bit의 길이를 가지고있다.

          이 Header에는 ID, Flag, Fragment, Offset등의 field를 가지고 있다.

          IPv6는 IPv4 주소 고갈 및 최신 Network의 속도와 그래픽 및 비디오를 포함한 혼합 데이터 스트림을 처리하기 용이한 기능들을 추가한 것이다.

          IPv6는 40octet 또는 320 bit의 길이를 가지고 잇으며 Source 및 Destination address에 각각 128bit를 할당하고 있어 32 bit의 주소 길이를 사용하는 IPv4에 비해 더 많은 주소 정보를 담을 수 있다.


          ![IPv4](/src/contetn/img/../../content/img/ipv4.png)

          ![Ipv6](/src/contetn/img/../../content/img/ipv6.png)
          
          
      3. Socket
      
            Socket은 1980년대 Berkeley Socket Interface로서 UNIX 환경에서 개발되었다.

            Socket은 Client와 Server간의 통신을 가능하게 해준다.

            Socket은 Internet 전체에서 고유한 IP주소와 port 값을 연결하여 형성된다.

            Socket은 TCP/UDP를 사용하는 프로그램을 작성하기 위한 Interface로써 API를 정의하는데 사용된다.

            Stream Socket은 TCP를 사용해 모든 데이터 블럭이 양쪽 Socket 사이에서 제대로 전달되고 순서에 맞게 수신된다.

            Datagram Socket은 UDP를 사용하기 때문에 제대로된 전송과 순서에 맞는 수신이 보장되지 않는다.

            Raw Socket은 IP와 같은 하위 layer Protocol을 직접 호출 한다.