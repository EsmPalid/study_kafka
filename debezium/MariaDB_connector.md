# 01. 학습중...

스냅샷 종류?

-   **initial snapshot**

처음 Connector를 실행했을 때 한번 실행하는 스냅샷임.<br>
전체 MariaDB Table Schema 구조를 Schema history topic에 저장하는 역할을 함<br>

"snapshot.mode" 속성값과 관련있음<br>
본문에서의 설명은 더 복잡하고 어려우나... 이해못하겠다.(일단대기)<br>

-   **ad hoc snapshot(임시 스냅샷)**

1. 무엇인가???

    - initial snapshot 이후 실행 도중 추가로 스냅샷 찍을 때 사용됨

2. 언제 사용되는가??

    - 새로운 Table이 캡쳐 대상으로 추가되었을 때
    - Table이 일시적으로 제외되었다가 다시 캡쳐 대상으로 포함될 때 Debezium은 자동으로 이를사용함
    - Signaling Table 또는 Signaling Topic에 "execute-snapshot" 명령/항목?을 넣으면 실행함

3. 무슨 역할을 하는가?

    - 대충 기존에 있던 스냅샷을 업데이트하는데 사용함

4. 기타 등등
    - Signaling tables 라던가 Signaling topic, Signal 등등 다양한 용어들이 등장함
    - execute-snapshot 메시지를 전송하여 캡쳐할 Table 및 Signal Type을 증분 또는 차단으로 설정할 수 있다.
    - 증분 스냅샷(Incremental Snapshot)과 차단 스냅샷(Blocking Sanpshot)과 관련됨

-   **incremental snapshot(증분 스냅샷)**

아직임

-   **blocking snapshot**

아직임

# 02. 대충 계획

1.  각종 스냅샷(initial ~ blocking까지)에 대해서 공식 문서 내용을 메모장으로 옮김(영어->한글)
2.  처음부터 다시 읽어봄
