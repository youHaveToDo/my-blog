---
title: 혼자 공부하는 컴퓨터구조와 운영체제) 11. CPU 스케쥴링
date: '2022-10-18'
tags: ['컴퓨터구조', '운영체제']
draft: false
summary: 모든 프로세스는 CPU에 접근하고 싶고, 사용하고 싶어합니다. 하지만 CPU는 하나 밖에 없기 때문에 공정하고 합리적으로 자원을 할당해야 하는데요, CPU는 어떻게 자원을 할당하는지 알아봅시다!
images: []
---

# 11. CPU 스케줄링 (코비)

## 11 -1 CPU 스케줄링 개요

모든 프로세스는 CPU에 접근하고 싶고, 사용하고 싶어합니다.

하지만 CPU는 하나 밖에 없기 때문에 공정하고 합리적으로 자원을 할당해야 하는데요,

CPU는 어떻게 자원을 할당하는지 알아봅시다!

![CPU 미쳐 사는 프로세스 3형제](/static/images/cs/cs11/01.png)

CPU 미쳐 사는 프로세스 3형제

CPU 자원을 원할하게 배분하는 것을 **CPU 스케줄링** 이라고 합니다.

사실 CPU 스케줄링은 이번에 처음 나온 내용은 아닙니다.

[09. 운영체제 시작하기 (코비)](https://www.notion.so/09-391902832c14468a9a06afff3a26a810)

---

이전 시간에 운영체제가 CPU 사용 순서와 시간을 공정하게 정해주는 것을 CPU 스케줄링이라고 배웠습니다.

- 시간표
  ![실제 저의 시간표입니다.](/static/images/cs/cs11/20.png)
  실제 저의 시간표입니다.

시간표도 이렇게 짜면 비효율적이고 허비하는 시간이 많이 생기듯이, CPU 자원을 효율적으로 배분하지 못하면

무질서한 상태가 되고 컴퓨터의 성능에도 문제가 생깁니다. (저는 당구치러 다녔고, 성적도 바닥을 쳤습니다.)

---

CPU 스케줄링이 중요한건 알겠고 그러면 어떻게 해야 효율적으로 스케줄링을 할 수 있을까요?
귀찮아서 앞으로는 CPU 스케줄링을 스케줄링이라고 하겠습니다.

사진처럼 줄을 잘 서야겠죠?

그럼 줄은 선착순으로 서면 될까요 ? 아니면

사진처럼 프로세스의 길이 만큼 ?

운영체제는 프로세스마다 **우선순위**를 두고

줄을 세웁니다.

![1 연경 == 2 나래 ](/static/images/cs/cs11/02.png)

1 연경 == 2 나래

---

우선순위는 어떤 기준으로 선정하게 될까요 ?

입출력 작업이 많은 프로세스의 우선순위를 높게 선정합니다.

이유가 뭘까요 ?

![스크린샷 2022-10-18 오전 1.39.34.png](/static/images/cs/cs11/03.png)

일반적인 프로세스는 위의 사진과 같이 CPU와 입출력장치를 번갈아가며 사용하고, 프로세스 실행과 대기 상태를 반복하며 실행됩니다.

프로세스마다 CPU와 입출력장치를 사용하는

시간의 차이가 있는데

입출력 장치가 사용이 많은 프로세스를

**입출력 집중 프로세스**

CPU 사용이 많은 프로세스를

**CPU 집중 프로세스** 라고 합니다.

![스크린샷 2022-10-18 오전 1.43.55.png](/static/images/cs/cs11/04.png)

이 둘을 비교해보면 CPU 집중 프로세스 보다 입출력 집중 프로세스가 CPU 실행 상태보다는 입출력을 위한 대기 시간이 많이 생기겠죠.

그렇다면 CPU 사용 시간이 조금만 필요한 입출력 집중 프로세스를 먼저 해결하고 CPU 집중 프로세스에 CPU 사용 시간을 많이 할당해주면 서로 기다리는 대기 시간이 많이 줄어들 것 입니다.

**이렇듯 상황에 맞게 운영체제가 프로세스마다 PCB에 우선순위를 부여하여 처리하는 것이 좋겠죠** 🙂 **?**

- 카드
  ![함정입니다.](/static/images/cs/cs11/05.png)
  함정입니다.

---

PCB에 우선순위가 적어 놓았지만, 프로세스를 실행하기 위한 매 순간마다 모든 프로세스의 PCB를 찾아보는 것은

**비효율적** (PCB가 엄마도 아니고..)

![스크린샷 2022-10-18 오전 1.56.55.png](/static/images/cs/cs11/06.png)

그래서 우리는 CPU를 사용하고 싶은 프로세스에게 줄을 세우곤 합니다. 그걸 **스케줄링 큐**라고 합니다.

![스크린샷 2022-10-18 오전 2.01.26.png](/static/images/cs/cs11/07.png)

![새치기 방지용 줄 서기](/static/images/cs/cs11/08.png)

새치기 방지용 줄 서기

저희의 생각처럼 한줄로 서는 줄 서기는 아니고

사**용하고자 하는 자원에 따라** **여러 줄**로 서는 모습을

상상하시면 됩니다.

![스크린샷 2022-10-18 오전 2.04.06.png](/static/images/cs/cs11/09.png)

줄을 의미하는 큐에도 종류가 있습니다.

CPU 사용을 위해 기다리는 줄을 **준비 큐**

입출력장치 사용을 위해 기다리는 줄을 **대기 큐** 라고 합니다.

이렇게 줄을 만든 프로세스들은 우선 순위를 보고 순위가 높은 프로세스를 먼저 실행하게 됩니다.

---

만약 A라는 프로세스가 실행중인 시점에 다른 급한 프로세스가 사용 요청을 하면 어떻게 될까요 ?

![마치 갑자기 화장실이 급한 것 처럼…](https://cdn.ppomppu.co.kr/zboard/data3/2022/0216/20220216212506_iBw2IrqqHQ.gif)

마치 갑자기 화장실이 급한 것 처럼…

이런 경우에는 급한 프로세스를 위해 CPU를 양보해 줄 수도 있고, “어쩌라고”를 시전하며 늦게 온 프로세스를

기다리게 할 수도 있습니다.

![스크린샷 2022-10-18 오전 2.17.41.png](/static/images/cs/cs11/10.png)

선자의 경우를 **선점형 스케줄링**이라고 합니다.

다른 프로세스가 자원을 사용하고 있더라도

운영체제가 프로세스로부터 자원을 강제로 빼앗아

다른 프로세스에게 할당하는 스케줄링 방식을

말합니다.

골고루 자원을 배분할 수 있지만, 문맥 교환 과정에서 오버헤드가 발생할 수 있습니다.

후자의 경우를 **비선점형 스케줄링**이라고 합니다.

이미 프로세스가 자원을 사용하고 있다면 스스로

대기상태가 되기 전까지 다른 프로세스는

기다려야 하는 스케줄링 방식을 의미합니다.

오버헤드는 선점형보다 적지만, 대기 시간이 길어질 수 있습니다.

![스크린샷 2022-10-18 오전 2.19.44.png](/static/images/cs/cs11/11.png)

## 11 - 2 CPU 스케줄링 알고리즘

![저희도 방식과 장단점만 이해하고 갑시다! 편하게 편하게 ~](/static/images/cs/cs11/12.png)

저희도 방식과 장단점만 이해하고 갑시다! 편하게 편하게 ~

1. 선입 선처리 스케줄링

   ![스크린샷 2022-10-18 오전 2.36.50.png](/static/images/cs/cs11/13.png)

   단순히 준비 큐에 삽입된 순서대로 프로세스를 처리하는 비선점형 스케줄링 방식입니다.

   우선순위가 없기 때문에 공정해 보일 수 있으나 비효율적입니다. 사진의 프로세스 C는

   2초를 실행시키기 위해서 22초를 기다려야 합니다. 이를 **호위 효과**라고 합니다.

2. 최단 작업 우선 스케줄링

   ![스크린샷 2022-10-18 오전 2.39.28.png](/static/images/cs/cs11/14.png)

   선입 선처리 스케줄링과 반대로 실행 시간이 짧은 프로세스를 우선적으로 처리하는 방식을

   **최단 작업 우선 스케줄링**이라고 합니다.

3. 라운드 로빈 스케줄링

   ![스크린샷 2022-10-18 오전 2.42.07.png](/static/images/cs/cs11/15.png)

   **라운드 로븐 스케줄링 =** 선입 선처리 스케줄링 + 타임 슬라이스

   what is 타임 슬라이스 ?

   타임 슬라이스 = CPU를 사용할 수 있는 정해진 시간

   **라운드 로븐 스케줄링**은 타임 슬라이스 만큼 돌아가며 CPU를 사용하고, 사용 시간이 끝났음에도

   아직 프로세스가 끝나지 않으면 큐의 맨 뒤에 삽입합니다. 이 때 문맥 교환이 발생합니다.

4. 최소 잔여 시간 우선 스케줄링

   **최소 잔여 시간 우선 스케줄링** = 최단 작업 우선 스케줄링 + 라운드 로빈 알고리즘

   ![스크린샷 2022-10-18 오전 2.47.56.png](/static/images/cs/cs11/16.png)

   말이 이해가 되질 않습니다.. 가장 먼저 우선순위는 어떻게 정하는 거지?

5. 우선순위 스케줄링

   우선순위를 정하고 순위가 높은 프로세스 먼저 CPU를 사용합니다.

   우선순위 스케줄링은 중간에 계속 우선순위가 높은 프로세스가 자리를 새치기 할 수 있어서 상대적으로 낮은

   프로세스들은 계속 후 순위로 밀려날 수 있습니다. 이를 **기아** 현상이라고 합니다.

   ![KIA 아님.](/static/images/cs/cs11/17.png)

   KIA 아님.

   이를 해결하기 위해, 오랫동안 대기한 프로세스에게 우선순위를 높여주는 **에이징** 기법이 있습니다.

6. 다단계 큐 스케줄링

   ![스크린샷 2022-10-18 오전 2.51.52.png](/static/images/cs/cs11/18.png)

   **다단계 큐 스케쥴링**은 유선순위별로 준비 큐를 여러 개 사용하는 스케줄링 방식 입니다.

   우선순위가 높은 큐를 먼저 처리하고, 가장 높은 큐가 비어 있으면 다음 순위의 큐를 실행합니다.

   큐를 여러 개 두면 프로세스 유형별로 우선순위를 구분하여 실행하는 것도 편리해지고,

   큐별로 타임 슬라이스를 여러 개 지정해서 큐마다 타임슬라이스를 크고 작게 설정할 수 있습니다.

7. 다단계 피드백 큐 스케줄링

   앞서 설명한 다단계 큐 스케줄링은 프로세스의 우선순위가 변경되지 않습니다.

   이러한 모습은 기아 현상이 발생할 수 있습니다.

   이를 보완한 스케줄링이 **다단계 피드백 큐 스케줄링**입니다.

   다단계 큐 스케줄링과는 한가지 다른 점이 있는데요, 우선적으로 실행된 프로세스가 해당 큐에서 실행이 끝나지 않는다면 다음 우선순위 큐에 삽입되어 실행되고, 이후 이것을 반복하게 됩니다. 즉, CPU를 오래 사용해야 하는 CPU 집중 프로세스들은 자연스레 우선순위가 낮아지고, CPU를 적게 사용하는 입출력 집중 프로세스는
   자연스레 우선순위가 높은 큐에서 실행됩니다.

   ![급 마무리! ](/static/images/cs/cs11/19.png)

   급 마무리!

---

##### 해당 스터디는 팀원들과 함께 진행한 스터디이기에 모든 장을 혼자서 발표한 것이 아닙니다.

##### 다른 장도 궁금하다면 [노션](https://amplified-neptune-cfd.notion.site/HBT-ede9d443e5484d07b4ee305a9106751a)을 방문해주세요 :)
