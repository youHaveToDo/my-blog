---
title: 혼자 공부하는 컴퓨터구조와 운영체제) 01. 컴퓨터 구조
date: '2022-09-27'
tags: ['컴퓨터구조', '운영체제']
draft: false
summary: 우리가 컴퓨터 구조를 알아야 하는 이유. 개발자로서 우리가 컴퓨터 구조를 공부해야 하는 이유 2가지
images: []
---

# 01. 컴퓨터 구조 (코비)

### 01-1 컴퓨터 구조를 알아야 하는 이유

개발자로서 우리가 컴퓨터 구조를 공부해야 하는 이유 2가지

1. **문제 해결**
   - 같은 코드라고 하더라도 실행하는 컴퓨터에 따라 정상적으로 코드가 실행되지 않을 수 있다.
   - 단순히 코드만 작성하고 컴퓨터를 이해하고 있지 못한 사람의 경우, 결과만 보여주는 '미지의 대상'이다.
   - 컴퓨터 구조를 이해하고 있다면 위와 같은 현상에서 문제 해결의 실마리를 찾을 수 있다.
2. **성능, 용량, 비용**
   - 서비스를 위한 컴퓨터를 구매할 경우, 선택의 기준을 세울 수 있다.
   - 비용을 줄이기 위해 성능이 부족한 컴퓨터를 구입하는 경우, 처리 속도가 너무 늦고,
   - 성능을 위해, 오버스펙의 컴퓨터를 구매하는 경우, 불필요한 추가 예산이 필요할 수 있다.
   - 즉, 컴퓨터 구조를 이해하고 있다면 성능/용량/비용을 고려하며 개발할 수 있다.

### 01-2 컴퓨터 구조의 큰 그림

우리가 알아야 할 컴퓨터 구조 지식 2가지.

![image01](/static/images/cs/cs01/01.png)

1. **컴퓨터가 이해하는 정보 : 0과 1로 표현된 정보**

   - 데이터
     - 컴퓨터가 이해할 수 있는 숫자, 문자, 이미지, 동영상
   - 명령어
     - 데이터를 움직이고 컴퓨터를 작동시키는 정보
     - 실질적으로 더 중요한 정보는 명령어!

   ex ) “1”, “2” = 데이터, “더하라, 1과 2를” = 명령어

   **즉, 명령어는 컴퓨터를 작동시키고, 데이터는 명령어의 재료.**

   ![image02](/static/images/cs/cs01/02.png)

2. **컴퓨터의 4가지 핵심 부품**

   ![image03](/static/images/cs/cs01/03.png)

   - 메모리
     - 프로그램의 명령어와 데이터를 저장
     - 프로그램이 실행되려면 반드시 메모리가 필요.
     - 저장된 값을 빠르고 효율적으로 찾기 위해 **주소**를 사용.
       ![image04](/static/images/cs/cs01/04.png)

- CPU
  - 메모리에서 명령어를 읽고, 해석하고, 실행
  - CPU 구성 요소
    - 산술논리연산장치(ALU) : 컴퓨터 내부에서 수행되는 계산
    - 레지스터 : CPU안에 존재하는 임시 저장 장치
      - ex) 누산기, 시프트 레지스터, 명령 레지스터, 연산 레지스터…..
    - 제어장치 : 제어 신호 관리
      - ex) 메모리 읽기, 메모리 쓰기
        ![image05](/static/images/cs/cs01/05.png)
- 보조기억장치

  - 메모리는 용량이 작고, 비싸다 (가성비 별로임)
  - 심지어 전원이 꺼지면 저장된 내용이 사라짐 (휘발성)
  - 그래서 생긴 보조기억장치 (HDD, SSD, USB …)
  - 휘발성이 아니기 때문에 비휘발성 메모리라고도 부름(non-volatile memory)
    ![image06](/static/images/cs/cs01/06.png)

- 입출력장치

  - 컴퓨터 외부에 연결되어 컴퓨터 내부와 정보를 교환
  - ex) 마이크, 스피커, 프린터, 마우스, 키보드 ….
  - 보조기억장치와 입출력장치를 주변장치라 통칭하긴 하지만 그냥 넘어가자.

- 메인보드

  - 위에서 설명한 4가지 부품 모두 메인보드에 연결.
  - 정보를 주고받는 통로를 **버스**라고 함.
  - 4가지 핵심 부품을 연결하는 버스를 **시스템 버스**

    - 주소버스 : 주소를 주고받음.
    - 데이터 버스 : 명령어와 데이터
    - 제어 버스 : 제어 신호

      ![image07](/static/images/cs/cs01/07.png)

- 그래픽 카드 (추가 내용)

[2.1.1. CPU와 GPU의 차이](https://sdc-james.gitbook.io/onebook/2.-1/1./1.1.1.-cpu-gpu)