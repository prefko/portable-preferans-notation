<a href="http://prefko.com">
  <img alt="prefko" src="https://avatars0.githubusercontent.com/u/46445292?s=200" width="100">
</a>

# Portable Preferans Notation - PPN
[portable-preferans-notation](https://prefko.github.io/portable-preferans-notation/)

**Portable Preferans Notation** (PPN) is a computer-processible format for recording and replaying [Preferans](https://en.wikipedia.org/wiki/Preference) games. It was invented in 2012. for internal database usage of the online preferans website [Prefko](http://prefko.com/).

**PPN** is based completely on the well known **PGN chess notation** (Portable Game Notation). For more information about PGN please visit this [Wikipedia article](https://en.wikipedia.org/wiki/Portable_Game_Notation). There are many PGN viewers/readers [available online](https://goo.gl/uqZvX6).

**PPN** notations is designed for easy parsing and generation by a computer programs. An alternative notation, called PPNh, is structured for easy reading and writing by human users.

## PPN
PPN notation has two sections:
- Info section
- Game section

### Info section
Info section contains general information about the game such as location, date, etc.

The information is organized in tag pairs, which are listed on individual lines and enclosed in square brackets [ ... ]. Each tag pair consists of a tag name and a value. The value is wrapped in double-quotes if it contains spaces. In, for example, [Date 2008.03.08], the tag name is **Date** and the tag value is **2008.03.08**.

This section is identical to the top section of the **PGN** notation, see [example here](https://en.wikipedia.org/wiki/Portable_Game_Notation#Example).

There are **required** and *optional* tags.

**Required** tags are **Bula**, **Refe**, **Player{1\|2\|3}** and **Result{1\|2\|3}**. (*Where {1\|2\|3} indicates that there are 3 separate tags, each with only one of those numbers*)

*Optional* tags can include, but are not limited to: *Place{1\|2\|3}* *Location*, *Date*, *StartTime*, *EndTime*, *Duration*, *Name{1\|2\|3}*, etc.

### Game section
Dealtext secion contains individual rounds of play ordered chronologically. Each round and enclosed in square brackets [ ... ] and contains fixed-ordered subsections, separated by a space character.

These subsections are, in order:
- **id**: deal order number
- **deal order**: order in which players were dealt the cards
- **cards**: cards as were dealt
- **bids**: highest bid values
- **main**: main player id (auction winner)
- **discarded**: discarded cards, if any
- **contract**: chosen contract
- **accepted**: players who decided to play
- **kontra**: if any
- **refa**: if any
- **value**: contract value
- **starts**: player id
- **throws**
- **summary**: tricks & scores

#### id
The id of the deal.

#### deal order
A 3 integer encoding of the order in which the players were dealt their cards. The last integer is the dealer. For example, **312** indicates that player 2 was the dealer and player 3 was the first one to receive the cards and thus also the first one to bid.

#### cards
32 characters, each representing one of the cards as they were dealt to the players. First 10 characters were dealt to the first player, and so on. The last 2 characters represent the 2 talon cards.

Each 10 character set which represents cards dealt to a particular player are written as they were dealt, first 5 cards dealt and then second 5 cards dealt.

This section is connected to the previous **deal order** section, such that the first 10 characters are cards dealt to the player listed in the order as the first one.

For example, the encoded cards like 1BDHM27YQK4CEIN3FVRJS5LP8GU6AOT9 are concatenated hands and talon cards 1BDHM27YQK, 4CEIN3FVRJ, S5LP8GU6AO and T9.

Cards are encoded based on the following table:

| Card       | Mini | Encoded |  -  | Card       | Mini | Encoded |
| ---------- | ---- | ------- | --- | ---------- | ---- | ------- |
| 7 Spade    | 7S   | 1       |     | 7 Heart    | 7H   | H       |
| 8 Spade    | 8S   | 2       |     | 8 Heart    | 8H   | I       |
| 9 Spade    | 9S   | 3       |     | 9 Heart    | 9H   | J       |
| 10 Spade   | XS   | 4       |     | 10 Heart   | XH   | K       |
| J Spade    | JS   | 5       |     | J Heart    | JH   | L       |
| Q Spade    | QS   | 6       |     | Q Heart    | QH   | M       |
| K Spade    | KS   | 7       |     | K Heart    | KH   | N       |
| A Spade    | AS   | 8       |     | A Heart    | AH   | O       |
| 7 Diamond  | 7D   | 9       |     | 7 Club     | 7C   | P       |
| 8 Diamond  | 8D   | A       |     | 8 Club     | 8C   | Q       |
| 9 Diamond  | 9D   | B       |     | 9 Club     | 9C   | R       |
| 10 Diamond | XD   | C       |     | 10 Club    | XC   | S       |
| J Diamond  | JD   | D       |     | J Club     | JC   | T       |
| Q Diamond  | QD   | E       |     | Q Club     | QC   | U       |
| K Diamond  | KD   | F       |     | K Club     | KC   | V       |
| A Diamond  | AD   | G       |     | A Club     | AC   | W       |

#### bids
The bids subsection contains 3 comma separated values which represent the highest bid for each of the 3 players. This section is also connected to the **deal order** section, such that the first value corresponds to the first player listed in the deal order.
This may seem confusing at first, but is actually enough to extract all bids.

We know that the first player has only 3 options: pass, 2 or game. Depending on his choice, the second player also has a very limited set of options, and the same holds for the third player as well.
In fact, right after the first round, all players will have only one possible option to choose, other than to opt out of the auction, of course.

Let's see a few examples:
- P,P,P - all players passed
- M3,P,3 - the auction went as follows: 2, pass, 3, mine 3, pass
- 2,G4,G - the auction went as follows: 2, game, game, hearts, yours wins
and so on...

#### main
ID of the main player, the one who won the auction.

#### discarded
This subsection contains 2 characters, indicating the two cards which the main player discarded before choosing the contract.
In case of a game, this subsection is **XX**.

#### contract
A number indicating the chosen contract. This number can be preceded by the letter G, indicating that it was a game without seeing the bonus cards.

Possible values are:

| Contract   | Name      |  -  | Contract   | Name           |
| ---------- | --------- | --- | ---------- | -------------- |
| 2          | Spade     |     | G2         | Game Spade     |
| 3          | Diamond   |     | G3         | Game Diamond   |
| 4          | Heart     |     | G4         | Game Heart     |
| 5          | Club      |     | G5         | Game Club      |
| 6          | Betl      |     | G6         | Game Betl      |
| 7          | Sans      |     | G7         | Game Sans      |
| 8          | Preferans |     | G8         | Game Preferans |

#### accepted
One character subsection indicating which followers decided to play. There are 4 possible combinations:
- 0 - both followers decided not to follow
- {1\|2\|3} - only playerX decided to follow
- 8 - both followers decided to follow (*8 is common because it resembles letter B for both, but anything >=4 works here*)

#### kontra
One or two character subsection indicating any kontras or invitations.

This subsection is simply encoded as follows:
- 0: Nothing
- I{1\|2\|3}: Invitation
- K{1\|2\|3}: Kontra
- R{1\|2\|3}: Rekontra
- S{1\|2\|3}: Subkontra
- M{1\|2\|3}: Mortkontra

{1\|2\|3} means that one of the integers 1, 2 or 3 is used here to indicate which player initiated the kontras. For example, R1 means that player1 started with a kontra and the main player returned a rekontra.

#### refa
Either 0 for none or 1 for this deal being a refa (*double value*).

#### value
An intiger indicating the value of the contract. For example, 8 for a simple contract of hearts or a game of diamonds or even for a contract of spades under refa.

#### starts
ID of the player who starts the game by throwing the first card.

#### throws
Simple subsection showing the entire game play, a list of comma separated throws encoded with 3 or 3 characters, depending on the number of players involved.
The last character is always one of 1, 2 or 3 indicating which player won that trick. That player is also the player who throws the first card in the next trick.
The characters before the last one indicate the cards as they were thrown.

For example, **2A11** after either **1** for the starter value, or **xxx1** as the previous trick, means that player1 started with 8-Spade, then player2 threw 8-Diamond and player3 threw 7-Spade, thus player1 won that trick.

#### summary
Relatively complex subsection encoding the tricks and score for all 3 players, comma separated and tied to the **deal order** above. The simplest case is 0 which is used when the player did not play.

For the follower player, we use the letter F followed by the number of tricks taken by this player and then his score, for example **F3:L60** means that the player followed, took 3 tricks and will add 60 in the left column.
Another example would be **F1:L20:20** indicating that the player followed, took only 1 trick, will add 20 in the left column, but also failed and will be adding 20 in the middle column as well.

For the main player, we use the letter M followed by the number of tricks taken and his addition/subtraction in the middle column, for example **M6:-20** for passing, or **M5:20** for failing.

### PPN Example

```ppn
    [Bula 60]  
    [Refe 2]  
    [Player1 cope]  
    [Player2 silvio_pu]  
    [Player3 elmacedon]  
    [Result1 458]  
    [Result2 88]  
    [Result3 -546]  
    [Place1 2]  
    [Place2 1]  
    [Place3 3]  

    [1 231 1BDHM27WQK4CEIN3FVRJS5LP8GU6AOT9 M3,P,3 2 AR 4 3 I3 8 2 2A12,M9B2,2A12,M9B2,2A12,M9B2,2A12,G9B3,2A13,G9B3 M7:-8,F3:L24,0]  
    [2 312 WQKJS5LP84CEIAOT9N31BDH7FVM2RGU6 P,P,P]  
    [3 123 4U6ADHM2OT9CEIN31B7WQKFVRJS5LP8G P,2,3 3 T3 5 2 I2 10 1 G9B3,2A13,G9B3,2A13,G9B3,2A13,2A13,G9B2,2A12,G9B2 F3:L24,0,M7:-8]  
    [1 231 1BDHM27WQK4CEIN3FVRJS5LP8GU6AOT9 M3,P,3 2 GH 4 3 S3 64 2 2A12,M9B2,2A12,M9B2,2A12,M9B2,2A12,G9B3,2A13,G9B3 M7:-64,F3:L192:64,0]  
    ...  
```

### JSON
The PPN notation can also be represented in the JSON format.

##### JSON Example
```json
{
  "id": 1,
  "dealOrder": 231,
  "cards": {
    "p1": "1BDHM27WQK",
    "p2": "4CEIN3FVRJ",
    "p3": "S5LP8GU6AO",
    "t": "T9"
  },
  "bids": {
    "p1": "M3",
    "p2": "P",
    "p3": "3"
  },
  "main": 2,
  "discarded": "AR",
  "contract": 4,
  "accepted": 8,
  "kontra": "I3",
  "refa": false,
  "value": 4,
  "starts": 2,
  "throws": [
    {
      "id": 1,
      "starts": 2,
      "cards": "2A1",
      "winner": 2
    },
    "..."
  ],
  "summary": {
    "p1": {
      "main": false,
      "tricks": 2,
      "left": 60
    },
    "p2": {
      "main": true,
      "tricks": 7,
      "middle": -8
    },
    "p3": {
      "main": false,
      "tricks": 1
    }
  }
}
```
