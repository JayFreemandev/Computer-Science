# Introduction

OSTEP에서 강조하는 운영체제의 Three Easy Pieces에 대해 살펴보자.

## 1. 가상화

### 1.1. CPU 가상화

CPU는 한번에 한 명령밖에 수행하지 못한다. (이 책은 싱글코어 시스템을 기반으로 하고 있다.)그렇

지만 우린 CPU가 동시에 다양한 작업을 수행하고 있음을 목격한다. 지금도 유튜브로 노래를 들으며 

글을 쓰고 있다. 작업 관리자 창을 켜보면, 수십, 수 백개의 프로세스들이 동시에 돌아가고 있다.

이런 환상을 제공하는 것이 바로 **"가상화(Virtualization)"**이다.

책에선 하드웨어의 도움으로 운영체제가 시스템에 매우 많은 수의 CPU가 존재하는 듯한 *환상*

*(Illusion)*을 만들어낸다고 말하고 있다.

이를 구체적으로 가상화 중에서도 **CPU 가상화**라 부른다.

그런데, 만약 두 가지 이상의 프로그램들이 동시에 실행된다면, 과연 누가 먼저 실행되어야 할까?

이런 문제는 운영체제의 *정책(Policy)*에 달려 있다.

이후 CPU 가상화 부분에서 구체적으로 다룰 것이다.

### 1.2. 메모리 가상화

CPU 가상화가 마치 여러 개의 CPU가 존재하고 있다는 환상을 제공하는 것이었다면, 메모리 가상화

는 프로세스로 하여금 **"자신만의 메모리 공간"**를 가지고 있다는 환상을 제공한다.

나중에 배우겠지만, 이런 자신만의 메모리 공간을 *Address space(==Virtual memory)*라 부른다.

프로세서는 메모리와 소통하므로, 메모리는 프로세스가 실행되는 동안 계속해서 접근된다.

많이 익숙할 malloc() 명령어를 통해 받는 주소는 가상주소다. 실제 컴퓨터에 꽂혀있는 그 초록색 물

리 메모리의 주소가 아니다.

운영체제는 이런 가상 주소를 실제 물리 메모리 주소로 Mapping하는 역할을 수행한다.

이런 Mapping 과정에서도 다양한 기법들이 존재하는데, 이는 가상화 부분에서 설명한다.

## 2. 병행성

이 책의 다른 주요 주제는 바로 병행성이다. 프로그램이 한번에 많은 일을 *동시에* 하려고 할 때, 발생

하는 문제가 바로 병행성 문제다.

운영체제가 여러가지 프로세스를 동시에 실행하려고 하는 경우에도 병행성 문제가 발생하지만, 운영

체제만의 문제는 아니다.

**멀티 쓰레드**에서도 동일한 문제가 나타난다.

예를 들어, 2개의 쓰레드를 생성하고, 각 쓰레드들은 전역변수 counter를 1씩, 100000회 증가시키는 

루틴을 수행한다고 가정한다.

내 머리 속에선 counter의 결과값은 200000을 예상하겠지만, 실제로 돌려보면 결과값은 200000회 

이하의 결과값이 나온다. 어째서 일까?

이 문제의 원인은 바로 명령어는 한번에 하나씩만 실행된다는 것이다.

counter++는 한 줄 아니냐고?

C 적으론 그럴 수 있지만, 어셈블리적으로 이 명령은 총 3줄짜리 명령어다. counter 값을 메모리에서 

레지스터로 탑재하는 명령어 한 줄, 레지스터 값을 1 증가시키는 명령어 한 줄, 이 레지스터 값을 다

시 메모리에 저장하는 한 줄, 총 3줄이다.

이 3줄을 실행되는 쓰레드가 중간에 교체된다면, 이상한 결과값이 나올 것이다.

만약 이 3줄의 코드가 **원자적(Atomically)**하게 실행된다면, 문제는 해결될 수 있다.(원자적은 마치 원

자 하나 처럼, 더이상 쪼개지지 않는 하나라는 의미로 이해하면 된다.)

여러가지가 동시에 실행되면서 발생하는 병행성 문제들은, 이것 이외에도 여러가지가 존재한다.

이런 문제를 해결하는 것도 OS의 역할이다.

## 3. 영속성

이 책의 마지막 주제다. Dram같은 장치는 데이터를 **Volatile(휘발성)**하게 저장한다. 만약 갑자기 전원

이 끊어지거나 시스템이 고장난다면, 메모리의 모든 데이터는 사라지게 된다.

데이터를 영속적으로 (Persistence)하게 저장할 수 있는 하드웨어-소프트웨어가 필수적이다.

하드웨어는 입력/출력, 혹은 I/O 장치 형태로 제공되는데, SSD, HDD 등이 있다.

이런 하드웨어를 관리하는 운영체제 소프트웨어를 **File system**이라 부른다. File system은 사용자가 

생성한 file을 시스템의 디스크에 안전하고 효율적인 방식으로 저장할 책임을 지닌다.

CPU, 메모리와 달리, 운영체제는 프로그램 별로 가상의 디스크 공간을 생성하지 않는다. 오히려 프로

그램들이 종종 파일 정보들을 공유하고 있다고 가정한다.

open(), write(), close()와 같은 저수준 입출력 시스템 콜들은, 이런 요청들을 운영체제의 File system으

로 전달하는 역할을 한다.

File system이 사용자의 요청을 디스크에 저장하는 것은, 쉽지 않은 일이다.

파일 시스템은

1. 새 데이터가 어디에 저장될 지 정해야 한다.
2. 파일 시스템이 관리하는 다양한 자료구조를 통해 데이터를 추적해야 한다.

이런 작업들을 위해선 깊은 이해가 필요하다. 운영체제는 System call을 통해, 그나마 쉽게 장치에 우

리가 접근할 수 있게 도와준다.

대부분의 파일 시스템은 사용자들의 Write 요청을 바로 바로 수행하지 않고, 모아두었다가 한 번에 

수행한다. 이 편이 매우 효율적이다.

그런데, 이런 모아쓰기 방법이 수행되기 전, 시스템의 오류가 나타난다면 어떨까. 큰 문제가 나타날 

것이다.

이런 문제를 해결하기 위해 File system은 저널링, Copy-on-write와 같은 방법으로, 시스템을 복구할 

수 있게 도와준다.

## 디자인 목표

OS가 CPU나 메모리같은 물리적 리소스들을 사용하는것도 알았고 까다로운 동시성 문제, 그리도 안

전하게 오래동안 보관하기 위한 지속성문제까지 어느정도 뭔지 알게되었다. 이러한 조건을 가지고 

시스템을 만든다고 할때 가장 중요한 목표는 추상화다.

쉽고 편하게 시스템을 사용하기 위해서는 추상화가 가장 중요하다. 컴퓨터 과학의 전부라고 말할수

있을정도로 근본적이다. 커다란 시스템을 작은 조각으로 쪼개서 만들수있다. 우리가 하이 레벨 언어

로 프로그램을 만들때 어셈블리 생각 안하고, 어셈블리로 만들때는 로직 게이트 생각 안하고 만들수

있게 해준다. 하지만 앞으로는 OS를 추상화시켜서 잘게 쪼개서 생각할수있게 만들어주겠다.

다음 디자인 목표는 성능이다. 다른 말로 하자면 오버헤드를 최소화 시키는것이다. 

또 다른 목표는 어플리케이션과 OS사이의 보호를 제공하는것이다. 이게 무슨소리냐 많은 프로그램

이 한번에 동시에 잘 돌아가는거를 원하지만 프로그램 하나가 터지면 다른것에 똑같이 나쁜 영향을 

주는걸 보고싶지않다. 그렇기에 보호(Protection)가 OS의 메인 철칙이다.  독립(Isolation)이라고도 부

르는데 프로세스를 다른 프로세스로부터 독립적이게 만드는것 이게 핵심이다. 프로세스간 보호가 

OS가 하는 대부분의 역할이다.

또한 OS가 중단 없이 계속 실행되는게 중요한데. 여기서 터지면 다른게 

다 터질만큼 높은 의존성을 가지고있다. 운영체제가 시간이 갈수록 복잡

해지고 이에 맞춰서 신뢰성있는 안전한 운영체제를 구축하는게 요즘 필

드에서 연구중인 목표다.