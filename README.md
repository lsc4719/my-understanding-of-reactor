Reactor는 reactive streams를 구현한 구현체이다.  

reactive streams 표준은 reactive programming을 java에 제공하기 위한 표준이다.  

Reactive programming은  

Event driven system 이다.  

이는 Thread에 대한 IoC 이다.  

Event loop threads에 대한 제어는 Schedulers가 하고  

프로그래머는 event handler (onNext, onError, onComplete, onCancel) 들을 엮는 stream을 작성해 subscribe으로 실행하면,

Schedulers가 이 stream의 event handlers (=signal handlers)를 실행시켜준다.  

이렇게 이해하고 있음.
