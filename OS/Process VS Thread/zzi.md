## Process와 Thread

먼저 Program(프로그램)과 Process(프로세스)에 대해 알아봅시다.

**Program(프로그램)이란?** 
- 파일 시스템에 존재하는 실행파일입니다.
- 파일이 저장 장치에 저장되어 있지만 메모리에는 올라가 있지 않은 정적인 상태입니다.

**Process(프로세스)란?**
- 프로그램을 실행하는 순간 해당 파일은 컴퓨터 메모리에 올라가게 되고, 이 상태를 동적(動的)인 상태라고 하며 이 상태의 프로그램을 **프로세스**라고 합니다.

> 즉, 프로세스는 운영체제가 메모리 등의 필요한 자원을 할당해준 '실행중인 프로그램'입니다.  
프로그램을 실행하면 운영체제로부터 실행에 필요한 자원을 할당받아 '프로세스'가 되는 것입니다.  



<img width="289" alt="스크린샷 2021-10-11 오후 4 34 14" src="https://user-images.githubusercontent.com/62633444/136750372-00118395-82ff-433f-a0df-b1c9963b7ecc.png">

프로세스는 Code, Data, Stack, Heap의 구조로 되어있습니다.
- Code : 코드 자체를 구성하는 메모리 영역(프로그램 명령)
- Data : 전역 변수, 정적 변수, 배열 등 (초기화된 데이터)
- Stack : 지역변수, 매개변수, 리턴 값 (임시 메모리 영역)
- Heap : 동적 할당 시 사용 (new(), mallock() 등)

우리는 하나의 프로세스를 사용하기 보다는 여러개의 프로세스를 사용합니다.
(노래들으면서 코딩하면서 슬랙, 카톡을 하는 등)    
  
여러 가지 프로세스들이 실행될 때 우리 눈에는 동시에 진행되는 것처럼 보이지만, 실제로는 cpu는 프로세스 1을 어느 정도 하고 저장하고 프로세스 2를 진행하고 다시 돌아가며 여러 프로세스를 왔다 갔다 하는 **콘텍스트 스위칭(Context Switching)** 이 일어납니다.
이 작업이 반복이 되면 CPU의 부담이 늘어나고, 중복된 자원들이 비효율적으로 관리됩니다.
그래서 나오게 된 것이 **Multi-Thread(멀티스레드)** 입니다.
<br/><br/>

**Thread(스레드)란?**  
- 프로세스가 할당 받은 자원을 이용하는 실행 단위이자 프로세스의 특정한 수행 경로이자 프로세스 내에서 실행되는 여러 흐름의 단위입니다.
<br/>
<img width="618" alt="스크린샷 2021-10-11 오후 4 30 58" src="https://user-images.githubusercontent.com/62633444/136749974-d20214f8-9c33-494f-b625-825f1f49d7f7.png">
스레드는 Code, Data, Heap영역을 공유하고 있으며,  Stack만 스레드 별로 가지게 됩니다. 
공유되는 자원이 있기 때문에 더 효율적으로 관리됩니다.   
 

## Multi-Process와 Multi-Thread

### Multi-Process란?
- 하나의 응용프로그램을 여러 개의 프로세스로 구성하여 각 프로세스가 하나의 작업(태스크)을 처리하도록 하는 것입니다.
- **장점:** 하나의 프로세스가 죽더라도 다른 프로세스에는 영향을 미치지 않고 정상적으로 수행
- **단점:** Context Switching에서의 오버헤드, 프로세스 사이의 어렵고 복잡한 통신 기법(IPC)

### Multi-Thread란?
- 하나의 응용프로그램을 여러 개의 스레드로 구성하고 각 스레드로 하여금 하나의 작업을 처리하도록 하는 것입니다.
- **장점:** 자원의 효율성 증대, 간단한 통신 방법으로 인한 프로그램 응답 시간 단축
- **단점:** 디버깅이 까다롭고, 주의 깊은 설계가 필요함

### 그러면 Multi-Process보다  Multi-Thread가 좋아보이는데 왜 사용하는 것 일까?
> 스레드는 Code/Data/Heap 메모리 영역의 내용을 공유하기 때문에 어떤 스레드 하나에서 오류가 발생한다면 같은 프로세스 내의 다른 스레드 모두가 강제로 종료됩니다.  
> 여기서 예를 들자면, 인터넷 익스플로러는 하나의 프로세스에 멀티스레드를 사용하고 크롬은 여러 개의 프로세스를 사용합니다.  
> 익스플로러는 하나의 프로세스를 사용하기 때문에 탭하나에 문제가 생기면 인터넷 익스플로러가 전체종료됩니다.  
> 그러나 크롬은 탭하나마다 하나의 프로세스를 사용하기 합니다. 각 탭이 서로 영향을 주지 않고 격리된, 독립된 상태로 실행되기 때문에 하나의 탭이 다운되더라도 크롬 자체가 다운되지 않도록 해줍니다.  





## 참고 자료
[참고한 자료1](https://velog.io/@gparkkii/ProgramProcessThread)    
[참고한 자료2](https://velog.io/@raejoonee/%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4%EC%99%80-%EC%8A%A4%EB%A0%88%EB%93%9C%EC%9D%98-%EC%B0%A8%EC%9D%B4)  
[참고한 자료3](https://devuna.tistory.com/21)  
[참고한 영상자료](https://www.youtube.com/watch?v=1grtWKqTn50)  
