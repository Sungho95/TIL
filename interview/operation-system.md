# 운영체제

### 1. 프로세스와 스레드의 차이를 설명해보세요.

프로세스는 실행중인 프로그램으로 운영체제로부터 시스템 자원을 할당 받은 작업의 단위입니다.

스레드는 프로세스 내에서 동작하는 실행 단위로 프로세스에는 최소 1개 이상의 스레드가 존재합니다. 프로세스가 할당받은 자원을 이용하여 실행합니다.

### 2. 컨텍스트 스위칭에 대해서 설명해보세요.

컨텍스트 스위칭은 한 Task가 끝날 때까지 기다리는 것이 아닌 여러 작업을 번갈아가며 실행해서 동시에 처리되도록 하는 방법입니다.

인터럽트가 발생하면 현재 프로세스의 상태를 PCB에 저장하고, 새로운 프로세스의 상태를 레지스터에 저장하는 방식으로 동작합니다. 그러나 컨텍스트 스위칭이 자주 발생하면 그 사이에 CPU는 동작을 하지 않으므로 성능저하가 발생할 수 있습니다.

### 3. 동기와 비동기에 대해서 설명해보세요.

동기와 비동기는 데이터 처리에 대한 방식을 말합니다.

호출하는 함수A와 호출되는 함수 B가 있다고 가정하면,

동기 처리는 함수 A가 함수 B의 완료 여부를 신경씁니다. 따라서 함수들의 순차적인 처리가 이루어집니다.

반면 비동기 처리는 함수 B의 완료 여부를 신경쓰지 않습니다. 따라서 함수들이 순차적으로 처리가 이루어지지 않습니다.

### 4. 블로킹과 논블로킹

블로킹과 논블로킹은 처리되어야 하는 작업이 전체적인 작업의 흐름을 막는지, 막지 않는지에 대한 관점으로 제어권이 누구한테 있는지가 중요합니다.
A와 B 함수가 있다고 가정하면

블로킹의 경우 A함수가 B함수를 호출하면, B 함수에 제어권을 넘겨 해당 제어권을 돌려 받을 때까지 대기합니다.

논블로킹의 경우 B함수를 호출하더라도 제어권을 그대로 가지고 있어 함수를 호출한 이후에도 그대로 작업을 진행합니다.

### 5. 멀티스레드 프로그래밍에대해서 설명하세요.

하나의 프로세스 내에서 여러 스레드가 동시에 작업을 수행할 수 있도록 프로그래밍 하는 방식을 말합니다.

여러 스레드가 프로세스의 자원을 공유하면서 발생할 수 있는 동기화, 교착상태 등과 같은 문제를 고려하여 코드를 작성해야 합니다.

### 6. 교착상태와 기아상태를 설명하고 해결방법에 대해서 설명하세요.

교착상태는 둘 이상의 프로세스들이 자원을 점유한 상태에서 서로 다른 프로세스가 점유하고 있는 자원을 요구하면서 계속해서 기다리는 현상을 의미합니다.

- 예방 : 교착 상태가 발생할 수 있는 조건을 만족하지 않도록 합니다.
- 회피 : 상태 확인을 통해 안전한 경우에만 자원을 할당하도록 합니다.
- 회복 : 교착상태를 일으킨 프로세스를 종료합니다.

기아상태는 특정 프로세스의 우선 순위가 낮아서 원하는 자원을 계속해서 할당받지 못하는 상태를 의미합니다.

- 오래 기다린 프로세스의 우선 순위를 높여주는 방식으로 자원을 할당하게 합니다.

### 7. 캐시가 무엇인지 설명해보세요.

CPU와 메모리의 속도차이로 발생하는 성능저하 문제를 해결하기 위한 장치입니다. 자주 사용되는 자원을 캐시에 담아 해당 자원이 필요할 때 메모리 대신 캐시에 접근하여 처리 속도를 높이는 방법을 말합니다.