# 📃 Java



<details>
<summary><strong><h3> 💡 제네릭에 대해 설명해주세요. </h3></strong></summary>
<div markdown="1">

    클래스나 메소드에서 사용할 내부 데이터 타입을 컴파일 시에 미리 지정하는 방법

### 📌 제네릭은 왜 사용하나요?
- 제네릭은 컴파일 타임에 타입 검사를 실행하기 때문에, <strong>런타임에 타입 안정성</strong>을 보장한다.  
    (런타임에 발생할 수 있는 ClassCastException을 컴파일 타임에서 체크 가능)

- 제네릭은 미리 타입을 지정하기 때문에, 런타임 시점에서 반환 값에 대한 타입 변환 및 타입 검사에 들어가는 오버헤드를 줄일 수 있다.


### 📌 제네릭의 변성에 대해 설명해주세요.

    🔥 제네릭은 기본적으로 무공변이다.

    어떠한 T 타입의 공변성을 허용하려면 <? extend T>를 사용한다.
    어떠한 T 타입의 반공변성을 허용하려면 <? super T>를 사용한다.

### 📌변성과 공변/반공변/무공변에 대해 설명해주세요.

<strong>변성</strong>은 타입의 상속 계층 관계에서 서로 다른 타입 간에 어떤 관계가 있는지를 나타태는 지표이다.

<br>

<strong>공변</strong> : `S` 가 `T` 의 하위 타입이면,
`List<S>` 는 `List<T>` 의 하위 타입이다.

<strong>반공변</strong> : `S` 가 `T`의 하위 타입이면,
T[] 는 S[] 의 하위 타입이다. (공변의 반대) 
`List<T>` 는 `List<S>` 의 하위 타입이다. (공변의 반대)

<strong>무공변</strong> : `S` 와 `T` 는 서로 관계가 없다.
`List<S>` 와 `List<T>` 는 서로 다른 타입이다.

<br>

</div>
</details>



<details>
<summary><strong><h3> 💡 Java Stream API에 대해 설명해주세요.</h3></strong></summary>
<div markdown="1">
</div>

    Stream API는 컬렉션 / 배열에 저장된 요소들을 하나씩 참조하면서 반복적으로 처리할 수 있는 기능을 제공한다.

✅ JDK 8부터 제공되기 시작한 기능

<br>

### 📌 Java Stream API의 특징에는 무엇이 있나요?


### 1️⃣ 원본의 데이터를 변경하지 않는다.
    Stream API는 원본 데이터를 복사하여 별도의 Stream을 생성하기 때문에 원본 데이터를 변경하지 않는다.


### 2️⃣ Stream은 일회용이다.

    재 사용이 가능한 Collection과 달리, Stream API는 일회용이다.  

<br>

만약 닫힌 Stream을 재 사용한다면 IllegalStateException이 발생하게 되므로, 재 사용이 필요한 경우에는 Stream을 다시 생성해주어야 한다.


### 3️⃣ 내부 반복으로 작업을 처리한다.
외부 반복을 통해 작업하는 Collection과 달리, Stream은 <strong>내부 반복</strong>을 통해 작업을 수행한다.

![Alt text](image-2.png)

    🔥 내부 반복자는 멀티 코어 CPU를 최대한 활용하기 위해, 요소들을 분배시켜 병렬적으로 작업 할 수 있다.

![Alt text](image-3.png)

<br>

### 4️⃣ Stream은 쉬운 병렬 처리를 지원한다.
    parallelStream() 메소드를 호출하여 병렬 Stream을 생성함으로써 손쉽게 병렬 처리할 수 있다.


### 5️⃣ Stream은 지연 연산을 수행한다.

    데이터 처리를 필요로 할 때까지 연산을 지연시키고, 필요한 연산만 수행하여 성능을 최적화할 수 있다.

<br>

스트림 파이프라인을 실행하게 되면 JVM은 곧바로 스트림 연산을 실행시키지 않는다.  

<br>


최소한의 필수적인 작업만을 수행하고자, 즉 지연 연산을 위한 준비작업을 수행한다. 
1. 스트림 파이프라인이 어떠한 중간 연산과 최종 연산으로 구성 되어 있는지 검사한다.  

2. 검사 결과를 바탕으로 JVM은 어떠한 방식으로 최적화를 진행할지 미리 계획하고, 그 계획에 따라 스트림의 개별 요소에 대한 스트림 연산을 수행하게 된다.
   
<br>

🔥 스트림에서 제공하는 최적화 전략으로는 <strong>루프 퓨전</strong>과 <strong>쇼트 서킷</strong>이 대표적이다.

<br>
<details>
<summary><strong>[루프 퓨전]</strong></summary>
<div markdown="1">

<br>

    Stream 파이프라인에서 연속적으로 체이닝된 복수의 스트림 연산을 하나의 연산 과정으로 병합시키는 방법
</div>
</details>

<br>
<details>
<summary><strong>[쇼트 서킷]</strong></summary>
<div markdown="1">
<br>

    불필요한 연산을 의도적으로 수행하지 않음으로써 실행 속도를 높이는 기법
    
    Ex) limit과 같은 쇼트 서킷 연산을 활용하여 스트림의 일부 요소들에 대한 연산을 완전히 생략한다.


<br>

</div>
</details>

<br>
<br>


### 📌 Stream과 for-loop의 성능 차이를 비교해 주세요.

    🔥 일반적으로 for-loop이 Stream보다 빠르다.


<br>

🤷🏻‍♀️ 왜 for문이 더 빠를까?

1. Stream은 <strong>매개변수를 통한 값 복사</strong>를 통해 원본 데이터의 불변성을 지원한다.  

    이로 인해 메모리 사용 증가, 복사로 인한 오버헤드 등으로 속도가 상대적으로 느리다.

<br>

2. <strong>Stream은 내부 최적화가 상대적으로 부족하다.</strong> 
   
    for-loop는 오래 전부터 사용되온 문법이기 때문에,
    for-loop에 대한 JIT Compiler의 내부 최적화가 잘 되어있는 반면
    
    Stream은 Java8 이후에 도입된 기능으로, 상대적으로 내부 최적화가 부족하기 때문이다.

<br>

### Stream 사용 시, for-loop 대비 속도 손실을 줄이려면

✅ Collection이 되는 스트림 소스의 크기가 충분히 크거나,     

✅ 컴퓨팅 연산이 CPU-intensive할 정도로 비용이 매우 비싸거나,    

✅ 병렬 스트림을 사용한다면, 스트림 소스인 Collection은 split하기 쉬운 자료 구조여야 하며, 연산이 stateful하지 않아야 한다.

<br>

🔥 가독성 / 유지 보수의 측면과 성능적인 측면을 고려해서 for-loop 또는 Stream을 선택해 사용하자.

<br>
</details>

<br>


<details>
<summary><strong><h3> 💡 Java Lambda에 대해 설명해주세요. </h3></strong></summary>
<div markdown="1">
<br>
    
    🔥 함수를 하나의 식으로 표현한 것

<br>

-  **[특징]**
   - 람다식 내에서 사용되는 지역변수는 final이 붙지 않아도 상수로 간주된다.
   - 람다식으로 선언된 변수 명은 다른 변수명과 중복될 수 없다.

<br>

-  **[장점]**  

   <strong> 🤷🏻‍♀️ Java Lambda는 왜 만들어졌고, 어느 때 주로 사용할까요? </strong>

   - 개발자의 의도가 명확히 드러나 가독성이 높아진다.
   - 함수를 만드는 과정 없이 한번에 처리할 수 있어 생산성이 높아진다.
   - 병렬 처리가 용이하다.

<br>

- **[단점]**
  -  람다를 사용하면서 만든 익명 함수는 재 사용이 불가능하다.
  - 디버깅 시 함수 콜 스택 추적이 다소 어렵다

<br>
<br>

### 📌 람다가 사용하는 지역변수는 왜 Effectively Final 이어야 하는가?

<br>

    🔥 지역 변수가 스택에 저장되기 때문에 람다식에서 값을 바로 참조하는 것에 제약이 있어 복사된 값을 이용하게 되는데, 이때 멀티 쓰레드 환경에서 복사 될/복사된 값이 변경 가능 할 경우 이로 인한 동시성 이슈를 대응할 수 없기 때문이다.

<br>
<br>


람다식에는 다음과 같은 규칙이 존재한다.

    1️⃣ 람다식은 외부 block 에 있는 변수에 접근할 수 있다.
    2️⃣ 외부 block 에 있는 변수가 지역 변수 일 경우 final 혹은 *effectively final 인 경우에만 접근이 가능하다

<br>

<details>
<summary><strong>[effectively final]</strong></summary>
<div markdown="1">

<br>

Java 8 에 추가된 syntactic sugar 일종으로, 초기화 된 이후 값이 한번도 변경되지 않았다면 effectively final 이라고 할 수 있다. 


effectively final 변수는 final 키워드가 붙어있지 않았지만 final 키워드를 붙힌 것과 동일하게 컴파일러에서 처리한다. 

</div>
</details>


<br>
<br>


외부 변수로 지역 변수를 이용하는 람다식(Local Capturing lambda)은 다음과 같은 특징이 있다.

<strong>1️⃣ 람다식에서 사용되는 외부 지역 변수는 복사본이다.</strong>   

    → 메소드 내 지역 변수를 참조하는 람다식을 리턴하는 메소드가 있을 경우, 메소드 block 이 끝나면 지역 변수가 스택에서 제거 되므로 추후에 람다식이 수행될 때 참조할 수 없다.
    → 지역 변수를 관리하는 스레드와 람다식이 실행되는 스레드가 다를 수 있다.

<br>

<strong>2️⃣ 🔥 final 혹은 effectively final인 지역 변수만 람다식에서 사용할 수 있다. </strong>

    람다식이 어떤 쓰레드에서 수행될지는 미리 알 수 없다. 
    이 얘기는 곧 외부 지역 변수를 다루는 쓰레드와 람다식이 수행되는 쓰레드가 다를 수 있다는 의미이다.
    
    지역 변수 값을 제어하는 스레드 A, 람다식을 수행되는 스레드 B 가 있다고 가정했을 때 문제는 다음과 같다.

    🙄 람다식에서 사용되는 외부 지역 변수 값이 가장 최신 값으로 복사되어 전달 됐는지 확신할 수 없다.
    왜냐하면 지역 변수는 변경될 수 있고, 지역 변수를 스레드 간에 동기화 해주는 것은 불가능 하기 때문이다. 

    이러한 문제점을 피하기 위해 람다에서 사용되는 외부 지역 변수는 전달되는 복사본이 변경되지 않은 최신 값 임을 보장하기 위해 fianl 혹은 effectively final 이어야 한다.


<br>

</div>
</details>


