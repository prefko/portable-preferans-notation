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

The information is organized in tag pairs, which are listed on individual lines and enclosed in square brackets [ ... ]. Each tag pair consists of a tag name and a value. The value is wrapped in double-quotes. In, for example, [Date "2008.03.08"], the tag name is **Date** and **2008.03.08** is the value.

This section is identical to the top section of the **PGN** notation, see [example here](https://en.wikipedia.org/wiki/Portable_Game_Notation#Example).

There are **required** and **optional** tags.

Required tags are **Bula**, **Refe**, **Player<A|B|C>**, **Place<1|2|3>** and **Result<1|2|3>**. (*Where <1|2|3> indicates that there are 3 separate tags, each with only one of those numbers, same for <A|B|C>*)

Optional tags can include, but are not limited to: *Location*, *Date*, *StartTime*, *EndTime*, *Duration*, *Name<A|B|C>*, etc.

### Game section
Dealtext secion contains individual rounds of play ordered chronologically. Each round is stored on a distinct line and contains fixed-ordered subsections. Each subsection is separated by a space character.

These subsections are:
- **id**: round order number
- **dealer**: player id
- **cards**
- **auction**: auction result
- **exchange**: discarded cards, if any
- **game**: chosen contract
- **came**: players who decided to play
- **kontra**: if any
- **value**: contract value
- **play**
- **score**: tricks & scores

#### id
The id is basically a number followed by a dot.

#### dealer
ID of the dealer, eg. 1.

#### cards
32 characters, each representing one of the cards as they were dealt to the players. First 10 characters were dealt to the first player, and so on. The last 2 characters represent the 2 bonus cards. Each 10 character set which represents cards dealt to a particular player are written as they were dealt, first 5 cards dealt and then second 5 cards dealt.

For example, the encoded cards like 1BDHM27YQK4CEIN3FVRJS5LP8GU6AOT9 are basically these concatenated hands and bonus cards 1BDHM27YQK, 4CEIN3FVRJ, S5LP8GU6AO and T9.

Cards are encoded based on the following table:

| Card       | Mini | Enc  |
| ---------- | ---- | ---- |
| 7 Spade    | 7S   | 1    |
| 8 Spade    | 8S   | 2    |
| 9 Spade    | 9S   | 3    |
| 10 Spade   | XS   | 4    |
| J Spade    | JS   | 5    |
| Q Spade    | QS   | 6    |
| K Spade    | KS   | 7    |
| A Spade    | AS   | 8    |
| 7 Diamond  | 7D   | 9    |
| 8 Diamond  | 8D   | A    |
| 9 Diamond  | 9D   | B    |
| 10 Diamond | XD   | C    |
| J Diamond  | JD   | D    |
| Q Diamond  | QD   | E    |
| K Diamond  | KD   | F    |
| A Diamond  | AD   | G    |
| 7 Heart    | 7H   | H    |
| 8 Heart    | 8H   | I    |
| 9 Heart    | 9H   | J    |
| 10 Heart   | XH   | K    |
| J Heart    | JH   | L    |
| Q Heart    | QH   | M    |
| K Heart    | KH   | N    |
| A Heart    | AH   | O    |
| 7 Club     | 7C   | P    |
| 8 Club     | 8C   | Q    |
| 9 Club     | 9C   | R    |
| 10 Club    | XC   | S    |
| J Club     | JC   | T    |
| Q Club     | QC   | U    |
| K Club     | KC   | V    |
| A Club     | AC   | W    |

#### auction
The auction subsection contains 3 comma separated values which represent the highest bid for each of the 3 players.
This may seem confusing at first, but is actually enough to extract the entire auction.

We know that the first player has only 3 options: pass, 2 or game. Depending on his choice, the second player also has a very limited set of options, and the same holds for the third player as well.
In fact, right after the first round, all players will have only one possible option to choose, other than to opt out of the auction, of course.

Let's see a few examples:
- P,P,P - all players passed
- M3,P,3 - the auction went as follows: 2, pass, 3, mine 3, pass
- 2,G4,G - the auction went as follows: 2, game, game, hearts, yours wins
and so on...

#### exchange
This subsection contains 2 characters, indicating the two cards which the main player discarded before choosing the contract.
In case of a game, this subsection is equal to XX.

#### game
A number indicating the chosen contract. This number can be preceded by the letter G, indicating that it was a game without seeing the bonus cards.

#### came
One character subsection indicating which followers decided to play. There are 4 possible combinations:
- 0 - both followers decided to not play
- L - only the first follower decided to play
- R - only the second follower decided to play
- B - both followers decided to play

#### kontra
One or two character subsection indicating any kontras or invitations.

This subsection is simply encoded as follows:
- 0: Nothing
- I: Invitation
- K<L|R>: Kontra
- R<L|R>: Rekontra
- S<L|R>: Subkontra
- M<L|R>: Mortkontra

<L|R> means that one of the letters L or R is used here to indicate which follower initiated the kontras. For example, RL means that the left follower started with a kontra and th emain player returned a rekontra.

#### value
An intiger indicating the value of the contract. For example, 8 for a simple contract of hearts or a game of diamonds or even for a contract of spades under refa.

#### play
Simple subsection showing the entire game play, a list of comma separated tricks encoded with 3 or 4 character, depending on the number of players involved. The last character is always one of M, L or R indicating which player won that trick. M for main, L for left follower and R for right follower. The characters preceding the winner indicate the cards as they were thrown.

For example, 2A1M means that the first player threw 8 Spade, then the second player threw 8 Diamond and the third player threw 7 Spade, and finally the main player won that trick. This also tells us who threw the first card in the next trick, while the very first tricks first thrower must be deduced from other information like who the dealer is and whether or not the contract was Sans.

#### score
Relatively complex subsection encoding the tricks and score for all 3 players, comma separated. The simplest case is 0 which is used when the player did not play. The only other case contains 4 integers, colon separated. The first integer is the number of tricks the player took. The remaining 3 integers are, in order, the left soup, the middle and the right soup.

### PPN Example

[Bula "40"]  
[Refe "1"]  
[Player1 "cope"]  
[Player2 "silvio_pu"]  
[Player3 "elmacedon"]  
[Place1 "silvio_pu"]  
[Place2 "cope"]  
[Place3 "elmacedon"]  
[Result1 "458"]  
[Result2 "88"]  
[Result3 "-546"]  

1. 1 1BDHM27WQK4CEIN3FVRJS5LP8GU6AOT9 M3,P,3 AR 4 L 0 8 2A1M,M9BM,2A1M,M9BM,2A1M,M9BM,2A1M,G9BR,2A1R,G9BR 7:0:-8:0,3:24:0:0,0  
2. 2 WQKJS5LP84CEIAOT9N31BDH7FVM2RGU6 P,P,P  
3. 3 4U6ADHM2OT9CEIN31B7WQKFVRJS5LP8G P,2,3 T3 5 L I 10 G9BM,2A1M,G9BM,2A1M,G9BM,2A1M,2A1M,G9BR,2A1R,G9BR 3:24:0:0,0,7:0:-8:0  
4. 1 1BDHM27WQK4CEIN3FVRJS5LP8GU6AOT9 M3,P,3 GH 4 R S 64 2A1M,G9BM,2A1M,G9BM,2A1M,G9BG,2A1G,G9BR,2A1R,G9BR 7:0:-64:0,3:192:64:0,0  
...  
