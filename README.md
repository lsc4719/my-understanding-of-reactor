### Imperative Programming

개발자가 Thread를 직접 통제한다.
Blocking code 실행시 thread가 block 된다.

### Event Driven Programming

개발자가 Thread를 직접 통제하지 않는다.
Thread는 Event Loop만을 실행한다.
개발자는 Event Loop에 특정 event 발생 시 수행할 event handler를 등록한다.
Event Loop Thread는 event queue를 갖고있다.
Event Loop Thread는 event queue에서 event를 하나씩 꺼내며,
해당 event handler를 실행한다.
Event handler에서 blocking code가 실행되면, Event Loop Thread가 block되어 다른 event를 처리할 수 없게되어, 이는 지양된다.

### Reactive Programming

Event Driven Programming인데, Event Loop Thread가 여러개인 경우다.  
Java에선 Reactive Straems라는 표준이 있다.  
event와 event handler들을 추상화한 stream 을 제공한다.  

### Reactor

Reactive Streams의 구현체이며, Spring Webflux에서 사용하는 reactive programming fw이다.  
event를 signal이라고 부르며,  
event handler를 signal handler라고 부른다.  
일반적으로 ReactorNetty를 사용하며,  
기본 Event Loop Thread는 따라서 Netty Event Loop Threads를 사용한다.  
Event Loop Threads는 Scheduler라는 단위로 통제하며,  
명시적으로 다른 Scheduler에 stream을 할당할 수 있다.  
I/O bound blocking code를 실행하야 하는 경우, 해당 stream은 Schedulers.boundedElastic()에 할당한다.  
CPU bound blocking code를 실행해야 하는 경우, 해당 stream은 Schedulers.parallel()에 할당한다.
단일 thread에서 실행하는 것이 중요한 경우, 해당 stream은 Schedulers.single()에 할당한다.
Schedulers.boundedElastic() 에서 blocking I/O job이 끝나고, 다시 non-blocking code만을 실행하고 싶은 경우,  
stream 중간부터 Scheduler를 변경할 수 있다.  
