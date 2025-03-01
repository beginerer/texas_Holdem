# texas_Holdem


## 게임 상태 보드
<img width="974" alt="스크린샷 2025-03-01 오후 7 33 08" src="https://github.com/user-attachments/assets/f8db1599-ce52-409c-8f48-a1d998e0f6d8" />
<img width="983" alt="스크린샷 2025-03-01 오후 7 33 14" src="https://github.com/user-attachments/assets/51648812-b8eb-4866-bce2-8b2fa35e7804" />

## 플레이어 stomp 통신

- /sub/game/{gameId}/{gamePlayerId}로 게임 정보 전송
- 카드 객체의 hidden 필드를 사용해서 hidden값이 true인 경우 마스킹된 dto 전달
- 해당 플레이어의 차례인 경우 별도의 배팅옵션 dto 전송
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
