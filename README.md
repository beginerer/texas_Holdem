# texas_Holdem Game

## 시연 영상
**[youtube 시연 영상](https://youtu.be/u08yHJ3RNPE?feature=shared)**

## 기능
- 스프링 이벤트를 활용하여 게임의 상태를 도메인 이벤트로 분해하고, 이벤트 핸들러가 처리하는 방식으로 구현
- Stomp 프로토콜을 사용해서, 플레이어간 통신 기능 구현
- Map<Long, ScheduledFuter<?>> 자료구조를 사용해서 플레이가 레디할때 마다 상태를 업데이트하고, 만약 모든 플레이어가 준비완료 상태라면 자동으로 게임을 시작하는 기능 구현


## 아키텍처
<img width="706" alt="스크린샷 2025-03-01 오후 9 48 02" src="https://github.com/user-attachments/assets/c178bf6a-7610-4a31-b431-0d79176e5aa6" />


## ERD
<img width="1190" alt="스크린샷 2025-03-01 오후 8 41 58" src="https://github.com/user-attachments/assets/1edbd67c-de1c-417e-9db4-31fe77db9ad6" />



## 게임 상태 보드
<img width="974" alt="스크린샷 2025-03-01 오후 7 33 08" src="https://github.com/user-attachments/assets/f8db1599-ce52-409c-8f48-a1d998e0f6d8" />
<img width="983" alt="스크린샷 2025-03-01 오후 7 33 14" src="https://github.com/user-attachments/assets/51648812-b8eb-4866-bce2-8b2fa35e7804" />

## 플레이어 stomp 통신
- /sub/game/{gameId}/{gamePlayerId}로 플레이별로 stomp 데이터 전송
- 카드 객체의 hidden 필드를 활용하여 플레이어는 공유 카드 및 자신의 카드만 확인 가능
``` java
{
  "gameId": 1,
  "roomId": 1,
  "level": "LOW",
  "gameStatus": "IN_PROGRESS",
  "communityCards": [
    {
      "suit": "HEARTS",
      "rank": "FIVE",
      "hidden": true,
      "highlight": false
    },
    {
      "suit": "HEARTS",
      "rank": "TEN",
      "hidden": true,
      "highlight": false
    },
    {
      "suit": "SPADES",
      "rank": "SEVEN",
      "hidden": true,
      "highlight": false
    }
  ],
  "gamePlayers": [
    {
      "playerId": 1,
      "userId": 1,
      "seatNumber": 1,
      "holeCards": [
        {
          "suit": "HIDDEN",
          "rank": "HIDDEN",
          "hidden": true,
          "highlight": false
        },
        {
          "suit": "HIDDEN",
          "rank": "HIDDEN",
          "hidden": true,
          "highlight": false
        }
      ],
      "roundBet": 0,
      "stack": 98,
      "folded": false,
      "allIn": false
    },
    {
      "playerId": 2,
      "userId": 2,
      "seatNumber": 2,
      "holeCards": [
        {
          "suit": "HIDDEN",
          "rank": "HIDDEN",
          "hidden": true,
          "highlight": false
        },
        {
          "suit": "HIDDEN",
          "rank": "HIDDEN",
          "hidden": true,
          "highlight": false
        }
      ],
      "roundBet": 0,
      "stack": 98,
      "folded": false,
      "allIn": false
    },
    {
      "playerId": 3,
      "userId": 3,
      "seatNumber": 3,
      "holeCards": [
        {
          "suit": "CLUBS",
          "rank": "THREE",
          "hidden": true,
          "highlight": false
        },
        {
          "suit": "DIAMONDS",
          "rank": "KING",
          "hidden": true,
          "highlight": false
        }
      ],
      "roundBet": 0,
      "stack": 98,
      "folded": true,
      "allIn": false
    }
  ],
  "round": "FLOP",
  "smallBlind": 1,
  "bigBlind": 2,
  "dealerPosition": 2,
  "currentOrder": 1,
  "winningPlayerId": null,
  "totalPot": 6
}
```

### 배팅 옵션 dto
``` java
{
  "gameId": 1,
  "roomId": 1,
  "playerId": 1,
  "round": "FLOP",
  "availableBettingOptions": [
    "BET",
    "CALL",
    "FOLD",
    "ALL_IN"
  ],
  "betMinAmount": 2,
  "betMaxAmount": 98
}
```
