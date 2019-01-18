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

This section is identical to the top section of **PGN**, see [example here](https://en.wikipedia.org/wiki/Portable_Game_Notation#Example).

There are **required** and **optional** tags.

Required tags are **Bula**, **Refe**, **Player{A|B|C}**, **Place{1|2|3}** and **Result{1|2|3}**. (*Where {1|2|3} indicates that there are 3 separate tags, each with only one of those numbers, same for {A|B|C}*)

Optional tags can include, but are not limited to: *Location*, *Date*, *StartTime*, *EndTime*, *Duration*, *Name{A|B|C}*, etc.

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
32 characters representing the cards as they were dealt to the players. First 10 characters were dealt to the first player, and so on. The last 2 characters represent the 2 bonus cards. Each 10 character set which represents cards dealt to a particular player are written as they were dealt, first 5 cards dealt and then second 5 cards dealt.

For example, the encoded cards like 1BDHM27YQK4CEIN3FVRJS5LP8GU6AOT9 are basically these concatenated hands and bonus cards 1BDHM27YQK, 4CEIN3FVRJ, S5LP8GU6AO and T9.

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

#### exchange

#### game

#### came

#### kontra

#### value

#### play

#### score



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

1. 1 1BDHM27WQK4CEIN3FVRJS5LP8GU6AOT9 M3,D,3 AR 4 10 0 8 2A1G,G9BG,2A1G,G9BG,2A1G,G9BG,2A1G,G9BD,2A1D,G9BD 7:0:8:0,3:24:0:0,0:0:0:0
2. 2 WQKJS5LP84CEIAOT9N31BDH7FVM2RGU6 D,D,D
3. 3 4U6ADHM2OT9CEIN31B7WQKFVRJS5LP8G D,2,3 AR 5 10 0 10 G9BG,2A1G,G9BG,2A1G,G9BG,2A1G,2A1G,G9BD,2A1D,G9BD 3:24:0:0,0:0:0:0,7:0:8:0
4. 1 1BDHM27WQK4CEIN3FVRJS5LP8GU6AOT9 M3,D,3 AR 4 10 0 8 2A1G,G9BG,2A1G,G9BG,2A1G,G9BG,2A1G,G9BD,2A1D,G9BD 7:0:8:0,3:24:0:0,0:0:0:0
...
