---
layout: post
title: chap6_Analog Transition
image: img/callum-shaw-555357-unsplash.jpg
author: 0verc10ck
date: 2019-10-23T10:00:00.000Z
tags:
  - 데이터 통신
---


본 강의는 경북대학교 컴퓨터학부 [김동균](https://monet.knu.ac.kr/) 교수님의 데이터 통신 수업을 듣고 그 내용을 정리한 것입니다.

양질의 자료와 강의를 제공해주신 [김동균](https://monet.knu.ac.kr/) 교수님께 감사의 말씀 올립니다.

강의의 내용과 제가 공부한 내용에 기반하기 때문에 부정확한 정보가 있을 수 있는점 주의하시기 바랍니다.

# Digital Analog Conversion

Digital Analog Conversion은 Digital Data의 정보를 기반으로 Analog signal의 특성중 하나를 변경하는 과정이다.

Digital Analog Conversion은 Analog signal의 다음 4가지 특성을 이용한다.

- Amplitude
  
- Frequency

- Phase

- Amplitude and Phase : QAM

아래 그림은 Digital Analog Conversion을 나타낸 것이다.

![DAC](https://postfiles.pstatic.net/MjAxNzA0MDFfMTQx/MDAxNDkxMDQ2OTU1NzU1.8VnZkL1TdlIItt_V7Yv-XEqavXdjCvErHfI0e5Tcu6Ig.emwy2mHociOepULFmuGMlnlIJ2RkPyzazRFft5ZQMH4g.JPEG.yye7926/image_6574924151491046946853.jpg?type=w773)


위의 Analog signal의 특성을 이용한 Digital Analog Conversion에는 다음과 같은 것들이 있다.

- ASK(Amplitude Shift Keying)

- FSK(Frequency Shift Keying)

- PSK(Phase Shift Keying)

- QAM(Quadrature Amplitude Modulation)

QAM 방식은 ASK방식과 PSK 방식이 결합된 방식이다.

![DACT](https://postfiles.pstatic.net/MjAxNzA0MDFfNTEg/MDAxNDkxMDQ3MDY4NzMx.DA6lTJbgxwY739I99nbGzcIDZxR_ETMWhn1N-rX1-zIg.xOMs9zLzfdJ3HCbwwwh1L_OvwmcuhGcXcjzTeD7kyMwg.JPEG.yye7926/image_4509996291491047021412.jpg?type=w773)

1. ASK(Amplitude Shift Keying)
     
     Carrier signal의 amplitude는 signal element를 생성하도록 변경된다.

     Amplitude가 변하는 동안 Frequency와 Phase는 일정하게 유지된다.

     ASK에서 2개의 binary 값은 서로 다른 amplitude를 가진 carrier frequency로 표현된다.

     일반적으로 그중 한 Amplitude는 0이다. 즉, Carrier의 존재유무로 Binary 값을 정한다.

     급변적인 gain의 변화에 민감하기 때문에 비효율적이다.

     ASK는 음성회선에서 최대 1200bps를 지원한다.

     ASK는 주로 광섬유를 사용하지만 LED 송신기와 Laser 송신기에서 또한 사용될 수 있다.

     LED 송신기에서 하나의 신호는 광 펄스로 표현되고 다른 신호는 빛이없는 것으로 표현된다.

     Laser 송신기에서는 저조도와 고조도를 signal element로 사용한다.

     ![ASK](https://postfiles.pstatic.net/MjAxNzA0MDFfMjIx/MDAxNDkxMDQ3NTE1MjI3.iQwhED7fqGzfyVAeX0tsRdJFfTlZN5AWAlItU853zi8g.97OmhmEBlCf9K4eIVX0LOyMZxwE0XtHMIe7tm0n0QHMg.JPEG.yye7926/image_1266154001491047505374.jpg?type=w773)

     ASK는 1개의 bit를 표현하기 위해 1 개의 signal이 필요하다. 그렇기 때문에 Baud rate  = Bit rate가 성립한다.

     S를 Signal Rate, N을 Data rate, r을 N/R, B를 Bandwidth, d를 factor라고 햇을 때

    $S = N x 1 /r$ $B =  (1+d) x S (0 < d < 1)$의 관계를 가지게 된다.

2. FSK(Frequency Shift Keying)

     Carrier signal의 Frequency는 signal element를 생성하도록 변경된다.

     FSK에서 Binary value는 2개의 서로다른 frequency로 표현된다.

     이 frequency는 signal frequency 부근에 존재한다.

     FSK는 ASK에 비해 오류에 둔감하고, 음성급 회선에서 1200 bps 정도의 속도로 사용된다.

     FSK는 주로 high frequency radio나 동축 케이블을 사용하는 LAN에 사용된다.

     ![FSK](https://postfiles.pstatic.net/MjAxNzA0MDFfMjY1/MDAxNDkxMDQ3ODgwOTg4.q8LlpXwSazZqxnYHBXiR0K3iZ43SeagfceDqI9icmu4g.GIIX4SGPIzazo3XjyAxkLp56hC-uEsLBT-WSFCNO1hUg.JPEG.yye7926/image_8626089621491047840612.jpg?type=w773)

     FSK의 Bandwidth는 lower frequency에서는 data rate과 연관이 있다.

     High frequency에서는 Carrier frequency로 부터의 offset(변위차)와 연관이 있다.

     $B = (1+ d ) x S + (L −1)2∆f, 0 < d< 1, ∆f= f2 − f1$의 식을 가진다.

     MFSK(Multiple Freqeuncy Shift Keying)은 각 signal element가 하나 이상의 bit를 나타내는 FSK 방식이다.

     2개 이상의 Frequency가 사용되고, FSK에 비해 우수한 bandwidth 효율을 보이지만 오류에 취약하다는 단점이 있다.


3. PSK(Phase Shift Keying)

     PSK에서 Carrier signal의 phase는 data를 나타내도록 이동한다.

     DPSK(Differential Phase Shift Ketying)은 특정한 기준을 잡고 Phase를 shift하는것이 아니라 직전에 수신된 signal과 phase가 같으면 0 다르면 1의 값을 가지는 방식이다.

     PSK는 몇 Phase를 사용하느냐에 따라 phase shift의 정도가 달라진다.

     2-PSK(BPSK)의 경우 0 degree는 0의 값을 180 degree는 1의 값을 가진다.

     4-PSK(QPSK)의 경우 90도 간격으로 phase를 나타낸다 90도 마다 00, 01, 10, 11의 2 bit를 나타낼 수 있다.

     8-PSK의 경우 45도 간격으로 pahse를 나타낸다 45도 마다 000, 001, 010, 011, 100, 101, 110, 111의 3 bit를 나타낼 수 있다.

     ![BPSK](https://postfiles.pstatic.net/MjAxNzA0MDFfMTcw/MDAxNDkxMDQ4MzMyNDE4.hiOjMBW9-GRGIHavbVkVOC6FkWN9YKoIKZAqVkgaT90g.9tK1pGNQkmbyttU0gLOg66aDDuMBHrbVzL9aDR5qI0wg.JPEG.yye7926/image_9822244651491048212229.jpg?type=w773)

     Phase가 많으면 많을 수록 Noise에 취약해지고 Error recovery 성능이 하락한다.

     PSK의 Bandwidth는 ASK와 동일한 $S = N x 1 /r$ $B =  (1+d) x S (0 < d < 1)$의공식을 가진다.

4. QAM(Quadrature Amplitude Modulation)

     QAM은 PSK, QPSK와 유사하다. 복잡한 형태의 Phase와 amplitude를 shift 하여 modulation한다.

     하나 이상의 bit를 나타내는 각 signal element에 의해 더 많은 phase angle을 사용할 수 있고, 하나 이상의 amplitude를 가질 수 있어 효율적이다.

     ![QAM](https://image.slidesharecdn.com/m-qam-160706174047/95/m-qam-5-638.jpg?cb=1467826877)

아래 표는 ASK. FSK, PSK, QAM의 Bit rate와 Baud rate를 비교한 것이다.

![Bit](../content/img/)

# Line Coding

  1. Linecoding and decoding

     Linecoding은 Digital Data를 Digital Signal로 변환하는 작업이다.

     Digital Siganl은 다음과 같은 특징을 가지고 있다.

     불연속 적이고,이산적인 전압 펄스로 이루어져 있다.

     각각의 펄스는 Signal element(신호 요소)이다.

     각 Data bit를 Signal element로 encoding 함으로써 Binary Data를 전송 하게 된다.

     ![Line](https://postfiles.pstatic.net/MjAxNzAzMjdfODIg/MDAxNDkwNjAwNDI1OTk4.1Xls5PGD1pVSl16AE3zxHcboPh_IcXmsI3-M_9KD9wgg.pfGkIsCN3dImXBhlRH6VSGjbq7z8GI5dYJZjmNsMWHkg.JPEG.yye7926/image_241672111490599688548.jpg?type=w773)

     위 그림은 Linecoding과 Decoding을 나타낸 것이다.

     Sender 측에서는 Digital Data를 Linecoding을 이용하여 Digital siganl로 Encdoing하고 Receiver는 Digital Signal을 Decoding하여 Digital Data를 얻는다.

     이러한 과정에서 Receiver가 Sender가 보낸 Signal을 해석하려면 우선적으로 Sender가 보내는 Signal에 대한 정보가 있어야한다.

     Signal에 대한 정보로는 대표적으로 다음 2가지 요소가 있다.

     - Timing of bits : Bit의 시작시간과 끝시간

     - Signal levels : Signal의 level이 얼마인가

     Reciver는 위의 두가지 정보를 기본적으로 알고 있어야 Sender의 Signal을 해석할 수 있다.

     그렇다면 Signal을 해석률에 영향을 미치는 요소에는 무엇이 있을까?

     앞서 3장에서 다룬 SNR, Data rate, Bandwidth가 Signal의 해석 정도에 영향을 미친다.

     SNR(Signal to noise ratio)이 높은 Signal은 BER(Bit Error Rate)가 낮다. BER이 낮다는 말은 Signal이 원본 그대로 전송되었을 가능성이 크다는 것이다.

     Data rate가 높으면 높을 수록 BER은 증가한다.

     Bandwidth가 넓은 Signal은 Datarate을 증가시키고 이는 BER의 증가를 불러온다.

     Data rate가 높은 Signal은 많은 정보를 한번에 나를 수 있어 유리하지만 그만큼 BER이 높아진다는 문제점이 있다.

     전송의 성능(해석률)을 높이고 싶다면 Data rate을 적정선으로 조절해야한다.

     그렇다면 성능을 높일 수 있는 방법에는 무엇이 있을까?

     Encoding을 이용하면 성능을 개선 할 수 있다. Encoding에 관한 자세한 것은 아래 절에 다룰 것이다.

  2. 용어

     Line coding 기법을 알아보기 전에 몇가지 용어를 정리하고자 한다.

     - Unipolar(단극형) : 모든 Signal element가 같은 sign(극성)을 가질때

     - Polar(극형) : 하나의 논리 상태는 +로 다른 논리상태는 -로 표현되는 방식 0의 전압값은 논리상태를 표현하지 않는다.

     - Bipolar(양극형) : +, 0, - 세가지 모두 논리상태를 표현하는 방법

     - Data rate(데이터율) : 초당 전송되는 비트 수, bps(Bits per second)

     - Duration or length of a bit(비트 구간, 비트 길이) : 송신기가 한 bit를 송출하는데 거리는 시간, Data rate가 R일경우 Duration은 1/

     - Modulation rate(변조율) : signal level의 변화 속도, 초당 signal element의 개수인 baud로 표현됨

     - Mark and space(마크와 공란) : 각각 1과 0을 뜻한다.

     - Baseline wandering(기준선 표류) : 수신자가 수신한 신호의 Amplitude의 평균값으로, Baseline은 Signal element의 값을 결정하는 기준이 된다. 허나 Base line이 정해지지 않고 Wandering(표류)한다면 Signal element의 값을 결정할 수 없어 Signal을 Decoding 하는데 여러움이 생긴다.

     - DC component(직류 성분) : Freqeucny가 낮은 성분은 통과시키지 못하는 시스템들이 존재하는데, 계속해서 같은 voltage level의 Signal이 들어오게 되면 시스템은 이를 DC Compoent라고 판단하기 때문에 시스템을 통과하지 못하는 경우가 발생한다.

  3. Signal elements versus data elements

     Signal elements : Digital Siganl의 가장 짧은 단위

     Data elements : Data의 가장 작은 단위, bit로 표현

     ![elements](https://postfiles.pstatic.net/MjAxNzAzMjdfMTEg/MDAxNDkwNTk5ODM4ODEy.PulhMEEuteH19mMIObSILGiVmQ96_RwVxux7DfkN-Qkg.duhkIOKJDj0ctNkfh8ui64rB-frCPi4UYam5_FO6msYg.PNG.yye7926/%EC%BA%A1%EC%B2%98.PNG?type=w773)

     위 사진의 r은 Signal elements당 전송되는 Data elements의 개수이다.

     a(r=1) : 하나의 Signal elements에 1개의 Data elements 전달.

     b(r=1/2) : 2개의 Signal elements에 1개의 Data elements 전달.

     c(r=2) : 하나의 Signal elements에 2개의 Data elements 전달.

     d(r=3/4) : 3 의 Signal elements에 4개의 Data elements 전달.

  4. Encoding scheme

     Encoding은 Data bits를 Signal elements로 Mapping하는 과정을 뜻한다. 

     오랜시간 연구를 통해 많은 Encoding 기법이 탄생하였고 우리는 그중 대표적인 일부 방법을 알아보고자 한다.

     아래 그림은 대표적인 Encoding 기법들이다.

     ![Encoding](https://media.cheggcdn.com/study/9dd/9dd13665-c090-4a86-8c32-8720fe6bd8f3/508864-5-1IP1.png)

     ![graph](https://slideplayer.com/slide/4957212/16/images/39/Digital+data%2C+Digital+signal+Encoding.jpg)

     두 그림 중 아래의 그림은 Encoding 기법을 이용하여 *01001100011*이라는 Digital data를 Encoding 한것이다.

     동일한 Data를 Encoding 한것이지만 그 기법에 따라 Signal의 모양은 천차 만별이다.

     이러한 기법들을 설명하기 전에 다양한 기법의 평가 및 비교에 사용되는 기준을 알아보고자 한다.

     - Signal spectrum(신호 스펙트럼) : Channel의 Bandwidth의 양끝으로 갈수록 전송장애가 일어날 확률이 높아지기 때문에 Bandwidth의 중간에 전력을 집중시키는 설계 방식이 좋다.

     - Clocking(시간정보) : 송신기와 수신기를 Synchronize 해야한다. 별도의 Clock을 사용하거나 Sync mechanism을 도입할 수 있다.

     - Error detection(오류검출) : Upeer layer에서 처리하지 않고 data link control 단계에서 Error Detection이 일어나는 것이 효율적이다.
     
     - Signal interference and noise immunity(신호 간섭 및 잡음 면역) : 어떤 Encoding 기법은 Noise가 있더라도 우수한 성능을 보인다.

     - Cost and Complexity(가격 및 복잡성) : Signaling rate가 높아지면 질수록 Cost 또한 높아진다. Signaling rate와 Cost의 비를 적절히 조절해야한다.

     ![spect](https://slideplayer.com/slide/6399647/22/images/14/Spectral+density+of+various+signal+encoding+schemes.jpg)

     위 그림은 여러 Encoding 기법의 Signal Spectrum의 모습이다.

     이제 본격적으로 Encoding 기법에 대해 알아보고자 한다.

     아래는 대표적인 Encoding 기법들을 한눈에 보기 편하게 정리한것이다.

     ![tree](https://postfiles.pstatic.net/MjAxNzAzMjdfMTUx/MDAxNDkwNjAxOTExNjI0.BljoOwGhvDzsQJ7NF5GzrV55AwI1X1k-mZ4Zf08Tcs4g.-VwGznKfUH2F9eia0jRQbJVMc-tFPZGOcm45DEMRDR8g.JPEG.yye7926/image_7350905141490601900560.jpg?type=w773)
       
  5. NRZ(Non Return to Zero)

     NRZ방식은 Unipolar, Polar방식 모두 적용이 가능한 Encoding 기법이다.

     NRZ 방식은 Bit interval 동안 전압 level이 일정한 특성을 가진다.

     따라서 NRZ 방식에서는 0의 전압 level로 복귀하지 않는다.

     전압이 없으면 0을 뜻하고, 일정한 양의 전압은 1을 뜻한다.

     일반적으로 음의 전압은을, 양의 전압은 0을 표시하는데 사용된다. 이러한 방식을 NRZ-L(Non Return to Zero Level) 이라고한다.

     ![uninrz](https://postfiles.pstatic.net/MjAxNzAzMjdfMjgz/MDAxNDkwNjAyMDcxMjM5.ztsmRk2Ax7fZSfby5hA7vvkmt3B3Uw5hr7xoObkW3Ssg.kSE84INvLPqSmkMstWBmI6nglE7-kIB9JBf7qWwwnMMg.JPEG.yye7926/image_4332254891490602066289.jpg?type=w773)

     ![binrz](https://postfiles.pstatic.net/MjAxNzAzMjdfNzAg/MDAxNDkwNjAyNTY0MDgw.uHMXKqey8Z631Iq1xbHnkQa3jQMZ1e_DdrYJiPvgX28g.Sz5ybqMbCuZSNLzGka8C7j7og1E8MIPCs08Rg_fEHKsg.JPEG.yye7926/image_1729799511490602552946.jpg?type=w773)

     위 두 그림은 Unipolar NRZ, Bipolar NRZ, Bipolar NRZ-I를 나타낸 것이다.

     Unipolar NRZ 방식은 DC Component와 Baseline Wandering이 발생할 위험이 크다.

     NRZ-I(Non Return to Zero Inverted)방식은 전압의 반전을 이용하는 방식이다.

     NRZ-I는 Bit 구간이 시작되는 지점에서 천이(전압의 반전)이 일어나면 1 일어나지 않으면 0을 나타낸다.

     NRZ-I 방식은 Data가 level이 아닌 Trasition에 의해 결정되기 때문에 NRZ-L 방식보다 Noise에 강하다.

  6. RZ(Return to Zero)
     
     RZ는 Polar 방식의 Encoding 기법중 하나로 +,-,0 세가지 값을 이용한다.

     RZ방식은 Synchronization을 보장하기 위해 각 Signal마다 Sysnchronization을 위한 정보를 담는데 이것이 0의 값이다.

     연속적인 0이나 1 문자열을 수신할 경우 자신의 위치를 놓칠 수 있는 NRZ방식과 달리 RZ방식은 signal이 +또는-이 된 후 항상 0의 값으로 돌아오게 된다.

     이러한 특성 덕분에 연속된 +또는 -를 구별 할 수 있다. 하지만 한 bit를 encoding하기 위해 두번의 signal change가 일어나기 때문에 Bandwidth를 많이 차지한다는 단점이 있다.

     ![rz](https://postfiles.pstatic.net/MjAxNzA0MDFfMjc4/MDAxNDkxMDM1MzY5NTE0.jr51aKcuzT1f2hsr3bkVljJTtH8opol_bBG5lAE60Eog.PyreXiWh4vCbllLN5uKMo-jyiO2gwZfQbga3Eb8G5HQg.JPEG.yye7926/image_2767846171491030212990.jpg?type=w773)



  7. Biphase(이중위상)

     Biphase는 대표적으로 Manchester와 Differential Menchester(차등맨체스터) 두가지 Encoding 방법이 주로 사용된다.

     Biphase는 전압 레벨이 중간에 다른 전압 레벨로 전환되는 방식이다.

     전압 레벨의 전환을 통해 Synchronize의 문제를 해결하였다.

     Biphase 방식은 Bandwidth가 NRZ 방식의 2배라는 단점이 있지만 별도의 Clock 없이 Synchronization이 가능한 Self-clocking이 가능하다는 장점이 있다.

     또한 Error detection면에서도 탁월한 성능을 보인다.

     Manchester 방식은 bit duration 중간에서 신호를 반전 시켜 1과 0의 논리상태를 구분하고, Clocking mechanism으로 이용한다.

     상향 천이의 경우 1의 논리상태를, 하향 천이는 0의 논리상태를 표현한다.

     Differential Manchester방식의 경우 천이가 Clocking만을 위해 사용된다.

     Differential Manchester방식은 이전 bit period에서 천이의 발생 여부를 통해 논리상태를 구분한다.

     이전 bit period에서 천이가 일어난다면 0의 논리상태를 천이가 일어나지 않았다면 1의 논리상태를 가지게 된다.

     ![Manchester](https://postfiles.pstatic.net/MjAxNzA0MDFfNTIg/MDAxNDkxMDM1MzgxMjkx.iiPsgBAL8SF7KJI5pS7p4P2UrYDeyIaMxLUQRMaHakog.1r75wVQtTOYyX-PSMt8g4X_gIYlhI0snpFuIAz1hbv4g.JPEG.yye7926/image_1002030881491030212990.jpg?type=w773)




  8. Multilevel Encoding

     Multilevel Encoding 기법은 2 이상의 signal level을 사용하는 방식이다.

     Binary level의 Multilevle Encoding은 보통 Bipolar라고도 불리운다.

     1. Bipolar(양극)

         Bipolar는 Positive, zero, negative 세 가지의 준위를 사용하는 Encoding기법이다.

         Bipolar의 대표적인 기법에는 AMI와 Pseudoternary(가삼진수)가 있다.

         - AMI(Alternate Mark Inversion)

             Bipolar AMI에서 0의 Amplitude는 0의 논리상태를 뜻하고, +, -의 값을 가지는 Amplitude는 1의 논리상태를 표현한다.

             1의 논리상태는 극성이 교대로 표현된다. 1의 Amplitude는 이전과 반대의 극성을 가지게 된다.

             Bipolar AMI는 DC Component가 없는것은 물론 Bandwidth도 낮고 Error detection도 쉬워 널리 사용되는 방식이다.

         - Pseudo-ternary(가삼진법)

             Pseudoternary에서 0의 Amplitude는 1의 논리상태를 뜻하고, 0의 논리상태는 극성의 교대로 표현된다.

             Bipolar-AMI 기법에 비교하여 큰 이점도 없고 단점도 없는 방식이다.

             표현방식이 반대인것을 제외한다면 거의 동일하다.

         Bipolar는 연속적인 0 signal(Bipolar-AMI), 연속적인 1 signal(pseudo-ternary)에서 Synchronization을 하는데 문제가 발생한다.

         이러한 문제점은 Low data rate에서는 임의의 bit를 추가하여 강제로 천이를 일으켜 해결하고, High data rate의 경우에는 data를 Scramble하여 해결할 수 있다.

         Bipolar 방식은 signal element당 표현할 수 있는 bit가 1.58개로 NRZ와 크게 다르지 않다.

         하지만 동일한 BER 상황에서 NRZ에 비해 3dB의 signal power를 더 요구하기 때문에 크게 효율적인 방법은 아니다.

         ![Bipolar](https://postfiles.pstatic.net/MjAxNzA0MDFfMTU3/MDAxNDkxMDM1MzkxNDIw.8Fw5f51j2osgAsF_SS37aDitRnRBNicq3gocp3BHVbIg.IXSNLIzGXOcsJfpb-h-54En7kr7jdCXl-8njaiCsokwg.JPEG.yye7926/image_315650041491030212991.jpg?type=w773)

     2. Multilevel Schemes(다준위방식)

         여기서 다룰 Encoding 기법들은 binary level 이상의 level을 사용하는 기법들이다.

         1. 2B1Q(2 Binary, 1 Quanternary)

             2B1Q 방식은 4개의 level을 이용하여 한 signal element당 2bit를 표현하는 방식이다.

             DSL 기술에서 고속인터넷 접속 제공에 이용된다.

             2B1Q는 Bandwidth가 좁아도 Data를 많이 보낼 수 있다는 장점이 있다.

             하지만 DC compoent등의 많은 문제점이 있다.

             ![2B1Q](https://postfiles.pstatic.net/MjAxNzA0MDFfNTkg/MDAxNDkxMDM1NDA3Mjkx.54K6GpLtRkT8Zifurrrnk20BnDgPEpMxlMWMRLmTQPcg.zl4rwHhqUL7opuQ8hFY1hXtx1HY045xeVORNh3RllQQg.JPEG.yye7926/image_6016270801491031915069.jpg?type=w773)


         2. 8B6T(8 Binary, 6 Ternary)

             8B6T 방식은 6 bit의 3 level signal element로 8bit를 표현하는 방식이다.

             8개의 bit로 표현되는 Data pattern을 Signal pattern과 매칭한다.

             이론적으로 8개의 bit는 $2^8 = 256$개의 pattern을 표현랄 수 있고, $3^6 = 729$개의 Pattern을 표현 할 수 있다.

             729개의 Pattern중 DC component가 일어나지 않고 Synchronization에 용이한 Pattern 256가지를 추출하여 사용한다.

             8B6T방식은 100Base-4T와 같은 Fast Ethernet 기술에 사용된다.

             ![8B6T](https://postfiles.pstatic.net/MjAxNzA0MDFfMTM5/MDAxNDkxMDM1NDk2MjY2.nioC7Und2hV6sthJnL6odRUF00k8C_-Uni7Ep8QJD9Mg.NDotnKH2gqotlCTu5HJKAl2XXp00lhGub1_jSD1GU04g.JPEG.yye7926/image_8383896211491031991256.jpg?type=w773)


         3. 4D-PAM5(4 Dimensional 5 level pulse amplitude modulation, 4차원 5준위 펄스 진폭 변조)

             4D-PAM5방식은 데이터를 4개의 회선으로 동시에 전송한다.

             -2,-1,0,1,2의 5 level을 사용하며, Gigabit LAN기술에 사용된다.

             ![4D-PAM5](https://postfiles.pstatic.net/MjAxNzA0MDFfNDAg/MDAxNDkxMDM1NDg3NzA3.IuAgggx2RZcy2QIoeX2Cck-tWcCJOot6QSgpT-zvkcMg.o_Y2t0HJU_MFlubwVi_FglTuE4dzClonQlRMSOsvst4g.JPEG.yye7926/image_1652288591491032310382.jpg?type=w773)


         4. MLT-3(Multiline transmission 3 level)

             MLT-3은 3개의 level을 사용하는 방식으로 100Mbps LAN 기술에 주로 사용된다.

             MLT-3에서 bit를 정하는 방식은 다음과 같다.

             1. 다음 bit가 0이면 level의 변화는 없다.

             2. 다음 bit가 1이고, 현재 level이 0이 아니면 다음 level은 0이다.

             3. 다음 bit가 1이고, 현재 level이 0이면 다음 level은 마지막으로 0이 아니었던 level의 역이 된다.

             이 방식은 복잡하긴 하지만 선로가 좋지 못하더라도 많은 데이터를 보낼 수 있다는 장점이 있다.

        




    






  

  ![Schema](https://postfiles.pstatic.net/MjAxNzA0MDFfMjc1/MDAxNDkxMDM1NDcxNjQ5.-nMqTLu9qm6IzBGNpG3QDXtQwsB9iqI4pvkwXQrLtFog.Q8GuFACDO1ep1Ke9Jpvbd3UvILyl6JxwcT366cnLEu0g.JPEG.yye7926/image_8877015811491032696561.jpg?type=w773)

  위 표는 지금까지 살펴본 Encoding 기법들을 요약한 것이다.


# Block Coding & Scarmbling

  1. Block coding

     Block Coding은 m bit를 n bit block으로 바꾸는 방식을 뜻한다. 이 때 n은 m보다 크다.

     mB/nB Encoding이라고도 불리며, 각 m-bit그룹을 n-bit그룹으로 바꾼다.

     Block coding은 Sysncrhonization을 위해 여분의 비트가 필요하다.

     또한 Error detection을 위해서도 여분의 비트가 필요하다.

     ![blockcoding](https://postfiles.pstatic.net/MjAxNzA0MDFfODIg/MDAxNDkxMDM1NDYxNzQx.kkV6k_tq0XgpVsADDT-z4wcjICHH0FDtsyRyy-i0sG8g.zkSEd1tf_td68ilOsKxm1ENPqMGMMyBNIKPkmbHCK9Yg.JPEG.yye7926/image_6265094881491032818638.jpg?type=w773)

     - 4B/5B(4 Binary / 5 Binary)

         NRZ-I 방식과 혼합하여 사용된다. 4개의 data bit를 5 개의 code bit로 변환한다.

         ![4B/5B](https://postfiles.pstatic.net/MjAxNzA0MDFfMTg4/MDAxNDkxMDM1NTEzOTQ0.0gNFIC9cdkrVGq9Ydrjtj9kRbYXFuL1l1GEAjq0VCBYg.ekTzgAhwL5L8nbaYY44SQu6IoKXfvbTE1QnkjZjbpPUg.JPEG.yye7926/image_8678007651491032957352.jpg?type=w773)

         ![4B/5BTable](https://postfiles.pstatic.net/MjAxNzA0MDFfMjcz/MDAxNDkxMDM1NTI3NTc1.xQA12qXv-KFT8F5srT7A8ToN4LPcyBNDtYzCTJ8bRKwg.BL23ydI62jZNEOBr9ExKnBIWqjl8w0feYKBm03HRTjMg.JPEG.yye7926/image_8139094741491033067867.jpg?type=w773)

         $2^5 = 32$개의 Code bit중 0이 연속적으로 3개 이상 붙지 않은 $2^4 = 16$개를 Data bit를 나타내는 용도로 사용한다.
         
         4B/5B 방식은 bit의 수가 늘어나 Bandwidth면에서는 손해를 보지만, long run이 발생하지 않는 bit pattern만을 사용할 수 있다는 장점이 있다.

     - 8B/10B(8 Binary / 10 Binary)

         8B/10B방식은 5B/6B방식과 3B/4B방식을 결합한 것이다.

         4B/5B방식과 유사하나 Error detection면에서 더 나은 성능을 보인다.


  2. Scrambling(뒤섞기)

     Scrambling은 연속적인 0으로 발생하는 Synchronization 문제를 해결하기 위해 사용하는 기법이다.

     연속된 0으로 이루어진 signal을 다른 level signal들이 골고루 조합된 signal로 바꾸는 방식을 사용한다.

     Scrambling을 이용하면 DC Component, long zero sequence 문제를 해결하고, Error detection을 가능해진다.

     이때 기존의 연속된 0을 대체하는 bit sequence를 filling sequence라고 한다.

     filling sequence는 다음과 같은 규칙을 지켜야한다.

     - Receiver의 clock에 충분한 transition을 제공하여 synchronization을 유지해야 한다.

     - Receiver가 인식하고 원래의 bit sequence로 교체할 수 있어야한다.

     - 원래의 bit sequence와 같은 길이로 대체하여 Data rate을 유지해야한다.

     1. B8ZS(Bipolar with 8-Zero Substitution)
     
         B8ZS는 북미에서 주로 사용되는 기법으로 Bipolar-AMI를 기반으로 하고 있다.

         B8ZS는 다음의 규칙을 따른다.

         - 연속적으로 8개의 0이 나올 때, 바로 앞의 pulse가 양의 값이면, 8개의 0은 000+-0-+로 Encoding 된다.

         - 연속적으로 8개의 0일 나올 대, 바로 앞의 pulse가 음의 값이면, 8개의 0은 000-+0+-로 Encoding 된다.

         B8ZS방식은 AMI에서 허용되지 않는 2개의 Signal pattern을 사용한다.

         ![B8ZS](https://postfiles.pstatic.net/MjAxNzA0MDFfMTc4/MDAxNDkxMDM1NTg3OTc0.HptjW00kl-Q5G1Mcfmofk1QQoygF635zp_dRXg6MDVsg.DSRXVg2k4dzRjJzqWZHcORp0gXi5MVB8Ev1fPreC_yYg.JPEG.yye7926/image_8863545581491034914310.jpg?type=w773)

     2. HDB3(High Density Bipolar 3zeros)

         HDB3방식은 유럽과 일본에서 주로 사용되는 방식으로, 4개의 0이 하나 또는 2개의 pulse를 포함한 sequence로 대체된다.

         HDB3 방식은 4개의 연속된 0을 000V나 B00V로 대체한다. 자세한 규칙은 아래와 같다.

         - 마지막으로 대체된 이후 0이 아닌 Pulse의 개수가 홀수인 경우엔 000V로 대체한다. 이는 전체 sequence에서 0이 아닌 pulse의 개수를 짝수로 만든다.

         - 마지막으로 대체된 이후 0이 아닌 pulse의 개수가 짝수인 경우엔 B00V로 대체한다. 이는 전체 sequence에서 0이 아닌 pulse의 개수를 짝수로 만든다.

         아래의 그래프는 HDB3 방식의 규칙을 적용하여 변경한 Seqeunce를 나타낸 것이다.

         ![HDB3g](https://postfiles.pstatic.net/MjAxNzA0MDFfOTQg/MDAxNDkxMDM1NjAzODMz.Cao1MgIrp_g6g52OkwHDOH53vF1MtLYjsDhrid2d0bcg.xiPQZ2ZsagXB_MyBj0enD565NOibny5v9xbCZR2ulM4g.JPEG.yye7926/image_6301389271491035095416.jpg?type=w773)

     아래 사진은 Bipolar-AMI, B8ZS, HDB3 방식으로 동일한 sequence를 나타낸 것이다.

     ![scrambling](https://image.slidesharecdn.com/7lecture7bipolarcodes-170826035843/95/data-communication-computer-network-bipolar-codes-19-638.jpg?cb=1503720282)



# Analog Data, Digital Signal

  ![a2d](https://image3.slideserve.com/6228545/digitizing-analog-data-l.jpg)

  Digitalizaion은 Analog data를 Digital data로 변환하는 작업이다.

  Digital Data는 NRZ와 같은 Encoding 기법을 통해 Digital Signal로 변환 될 수 있고, Analog Signal로도 변환이 가능하다는 장점이 있다.

  Analog Data의 전송을 위해 Analog Data를 Digital Data로 변환하고, 전송된 Digital Data를 다시 Analog Data로 복원하는 장비를 Codec이라고한다.

  Codec에서 널리 사용되는 기술에는 PCM과 DM이 있다.

  1. PCM(Pulse Code Modulation)

     PCM은 sampling 이론을 바탕으로 한것이다.

     sampling 이론은 "어떤 signal f(t)가 유효한 최고 Frequency 보다 두 배 이상의 속도로 일정한 시간간격마다 채집된다면, 이 채집된 데이터는 원래의 signal이 가진 모든 정보를 포함하게 되고, f(t)는 채집된 데이터로 부터 Low-pass Filter를 사용하여 재구성 될 수 있다."라는 내용의 이론이다.

     채집된 데이터를 PAM(Pulse Amplitude Modulation) Sample이라고 부르며, Sample들은 모두 Analog이기 때문에 Digital로 변환하기 위해 Binary-code를 할당해야 한다.

     ![PCMex](https://slideplayer.com/slide/7240745/24/images/6/PCM+Example.jpg)

     아래 그림은 PCM의 동작 과정을 나타낸 것이다.

     ![PCMDiagrm](https://postfiles.pstatic.net/MjAxNzA0MDFfMjIz/MDAxNDkxMDM2MzM4NzQ0.LN-crRNLwLMWNYkaxMcco-0zy4psB23w1IL4s1NDz7Ug.kqFsMtnGKkKC3nuBwP4iexRtrvmDZAIPRBFEZT_kARwg.JPEG.yye7926/image_415219961491035822223.jpg?type=w773)

  2. DM(Delta Modulation)

     DM은 PCM의 복잡도를 낮추기 위해 개발된 기술이다. 

     DM은 Analog Input을 Staircase Function(계단형 함수)를 사용하여 예측한다.

     각 sampling Interval $T$ 동안 1개의 Quantization levle $\delta$ 만큼만 오르내릴 수 있다.

     이러한 특성 때문에 DM과정의 출력은 각 sample의 binary value가 된다.

     Staircase function이 올라가면 1을 내려가면 0을 표시한다.

     아래 그림은 DM의 예와 과정을 나타낸 것이다.

     ![DM1](https://slideplayer.com/slide/7240745/24/images/31/Delta+Modulation+-+example.jpg)

     ![DM_modul](https://postfiles.pstatic.net/MjAxNzA0MDFfMTEz/MDAxNDkxMDQ1MzY0NTkx.IIn35pSf6ja98wsJteeieJRP7XMNMs5_y3KZ42POoiMg.ImwUheJHBx3U4R-oQf5mFYiiQ7fgMGnGJxOWIc2KY-gg.JPEG.yye7926/image_7233676861491045017126.jpg?type=w773)

     ![DM_demodul](https://postfiles.pstatic.net/MjAxNzA0MDFfMTkz/MDAxNDkxMDQ1Mzc5NTEy.JBJ6F9MADOZa1XHQ0KMjhbMLPCv7-VdiA3Cpv5momYog.Dt6NgwRtACdAqo6teuRsODeM-ICPYqDRRPkxuvOuz9Ag.JPEG.yye7926/image_2977108481491045078283.jpg?type=w773)


# 전송 방식

  Data를 전송하는 방식에는 크게 Parallel방식과 Serial방식이 있다.

  ![transmission](https://postfiles.pstatic.net/MjAxNzA0MDFfMTAw/MDAxNDkxMDQ1Njg0NjY0.2lkpJS9NqvT_btIwPrOXrB3MAOiaEIp_-p3f89MFvGUg.UEN9d55OZsqKmVfcUBp1ngfhyE4mu_dOQH7eaKRrys8g.JPEG.yye7926/image_5445656461491045681614.jpg?type=w773)

  Parrael 방식은 한번에 많은 bit를 보낼 수 있다는 장점이 있다.

  하지만 Synchronization이 이루어져야 한다는 문제점과 회선 설치 비용이 비싸다는 단점이 있다.

  또한 Parallel 방식은 회선 비용 문제 때문에 장거리 통신을 구현하기에는 적절치 않다.

  ![Parallel](https://postfiles.pstatic.net/MjAxNzA0MDFfMjAz/MDAxNDkxMDQ1ODQzODY5.HTOYdNw_9tdTw25MjcWr6npIp1eKAc2bzKGTLxesFWEg.nWWXZ1YorNojh-nZUzNSIh30KW0eByEcIccl2F9Rgkwg.JPEG.yye7926/image_4163847531491045834946.jpg?type=w773)

  Serial 방식에는 Asynchronous, Synchronous, Isochronous방식이 있다.

  Serial 방식에서는 한 bit가 다른 bit의 뒤에 오기 때문에 통신하는 두 장치간에 하나의 channel만 구성되면 된다.

  Serial 방식은 하나의 channel만을 가지기 때문에 회선 비용이 저렴하다는 장점이 있다.

  ![Serial](https://postfiles.pstatic.net/MjAxNzA0MDFfMTUg/MDAxNDkxMDQ2MTg1MTc0.BckrYO827B6nIEE58jot3Fk_NNCSOCkDQP5VX6fVrAwg.NE_PKGeky2X4YwSuoQlWuAM3cocf8PiQ6UDV9H63KbIg.JPEG.yye7926/image_8944178031491046119581.jpg?type=w773)

  1. Asynchronous(비동기성)

     Asynchronous 방식은 5~8 bit로 구성된 문자를 단위로 통신한다.

     각 문자에는 Synchronization을 위한 시작비트와 정지비트가 포함된다.

     이러한 방법은 시작비트와 정지비트 사이의 간격이 가변적이기 때문에 불규칙한 전송에 적합하고, 송수신기간의 Synchronization이 불필요 하기 때문에 장비의 구축 비용이 저렴하다.

     하지만 항상 시작비트와 정지비트가 포함되기 때문에 매 문자마다 2 bit를 사용해야 한다는 단점이 있다.

     ![Async](https://postfiles.pstatic.net/MjAxNzA0MDFfMTc1/MDAxNDkxMDQ2MjkxMTQz.WX34HdYqq-NiTw1qQPpDjmBmspztUMK-lPqpYjtwBz4g.lpge43K8Ug3DKr4XgtxaC6fgxX6EMK1o-j6mWXywnEcg.JPEG.yye7926/image_2769910531491046240170.jpg?type=w773)


  2. Synchronous(동기성)

     Synchronous 방식은 미리 정해진 수 만큼의 문자열을 한 묶음으로 만들어 전송하는 방식이다.

     해당 방식은 송신측과 수신측이 하나의 기준 clock으로 Synchronization이 이루어져야한다.

     수신자는 Clock에 의해 bit를 구별하게 되기 때문에, Data와 Clock을 위한 2개의 회선이 필요하다.

     Synchronous 방식의 전송 단위는 Frame으로 Data에 Preamble, Postamble, Control Information을 결합한 것이다.



