# Portable Preferans Notation - PPN
[portable-preferans-notation](https://prefko.github.io/portable-preferans-notation/)

**Portable Preferans Notation** (PPN) is a computer-processible format for recording and replaying [Preferans](https://en.wikipedia.org/wiki/Preference) games. It was invented in 2012. for internal database usage of the online preferans website [Prefko](http://prefko.com/).

**PPN** is based completely on the well known **PGN chess notation** (Portable Game Notation). For more information about PGN please visit this [Wikipedia article](https://en.wikipedia.org/wiki/Portable_Game_Notation). There are many PGN viewers/readers [available online](https://goo.gl/uqZvX6).

**PPN** notations is designed for easy parsing and generation by a computer programs. An alternative notation, called PPNh, is structured for easy reading and writing by human users.

## PPN
PPN notation has two sections:
- Tag pair section
- Dealtext section

### Tag pair section
This section contains general information about the game such as location, date, etc.

Tag pairs are listed on individual lines and enclosed in square brackets [ ... ]. Each tag pair consists of a tag name and a value. The value is wrapped in double-quotes. In, for example, [Date "2008.03.08"], the tag name is **Date** and **2008.03.08** is the value.

This section is identical to the top section of **PGN**, see [example here](https://en.wikipedia.org/wiki/Portable_Game_Notation#Example).

There are **required** and **optional** tags.

Required tags are **Bula**, **Refe**, **Player{A|B|C}**, **Place{1|2|3}** and **Result{1|2|3}**. (*Where {1|2|3} indicates that there are 3 separate tags, each with only one of those numbers, same for {A|B|C}*)

Optional tags can include, but are not limited to: *Location*, *Date*, *StartTime*, *EndTime*, *Duration*, *Name{A|B|C}*, etc.

### Dealtext section
...todo
