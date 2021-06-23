# DDD(Domain Driven Development)

## DDD란 무엇인가

---

쉽게말해 도메인을 중심으로 설계하는것을 의미함. 여기서 도메인이란, ***실제 세계에서 사건이 발생하는 집합***이라고 생각하면 됨.

예를 들어, 온라인 자동차 판매몰을 개발할 경우 손님이 자동차를 주문하는 도메인, 판매몰 업주나 관리자 입장에서 자동차들을 관리하는 도메인이 있을 수 있음. 

***이러한 여러가지 도메인들이 서로 상호작용 하도록 설계하는 것이 도메인 주도 설계(Domain Driven Development)임.***

도메인 주도 설계에서의 특징은 같은 객체(객체 또는 클래스)가 여러개 존재할 수 있다는 것임. 손님이 자동차를 주문하는 도메인에서의 Car객체와 점주가 자동차들을 관리하는 도메인에서의 Car객체는 같은 Car 객체이지만 각 객체들이 담고있는 정보는 서로 다를수 있음.( ***Ex***. 손님 도메인에서의 Car객체의 정보는 price, color, option 등등이 있을 수 있을것이고 점주 도메인에서의 Car 객체의 정보는 잔여수량, 판매 시 마진 등의 정보가 있을수 있음)

다시 말해 **문맥**에 따라 객체의 역할이 바뀔 수 있다는 것.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc1PGG5%2FbtqDvgknEsi%2FfFMbAtKjDxnsP8hi3YAaZ0%2Fimg.png">

이것을 ***Bounded Context***라고 부름.

이 Bounded Context에 따라 각 Model들의 역할이 완전히 달라지고, 책임또한 달라지게 됨.

그래서 이러한 정보들을 외부로 Public하게 노출시키지 않고 package-private하게 내부에서만 알 수 있게 함.

이러한 관점에서 더 나아가 직접 서비스에 적용시킨것이 MicroService Architecture임.

결론은 서로 다른 도메인 영역끼리 상호작용하기 위해서는 API를 통한 호출을 이용해야 한다는 말.

즉, 각각의 도메인은 ***서로 철저하게 분리***되고, ***높은 응집력***과 ***낮은 결합도***로 변경과 확장에 용이한 설계를 할수 있게 됨.

DDD의 핵심은 ***도메인을 서비스 별로 분리***하는 것임.

하지만 모든 도메인에서 많은 종류의 객체들을 다루고 있다면, 유지보수나 기능확장에 어려움을 겪을 수 밖에 없음. 객체간 상호작용은 점점 복잡해지고, 어떤 객체가 도메인을 대표하는 객체인지도 명확하지 않게 됨. 여기서 등장하는 것이 바로 Aggregate(집합)임.

## Aggregate(집합)

---

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FMhHoE%2FbtqDvyZtluZ%2FgPBxMT0sJx8o4Fjpk2MxGK%2Fimg.png">

각각의 도메인 영역을 대표하는 객체를 Aggregate라고 함. 도메인의 영역을 대표하는 객체를  통해 각 도메인별로 묶어야하는 객체가 명확해질 수 있음.
