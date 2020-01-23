---
layout: default
title: "How To Play Scopa"
permalink: /scopa-rules/
---

# How to play Scopa

Scopa is an Italian card game for 2+ players using a 40 card Latin-suited deck. The goal is to capture the most cards, and more importantly, capture the *best* cards so that you are awarded the most points across several scoring metrics at the end of each round.
While there are many, many different variations in the game, rules, and decks based on the region it's played in, I will attempt to describe what I feel is the most general implementation of the game so that if you are interested in those differences, picking them up will be quick and easy. For example, it is common to play with four players on teams of two, or with different rules for how the capture math works (as in *Scopa di Quindici*).

# The Deck {#deck}

Perhaps one of my favorite parts of this game is the deck. For the purposes of this page, I will refer to it as a "Scopa deck" - just know that this kind of deck is used to play other games as well, not just Scopa.

A Scopa deck consists of four suits: Coins, Cups, Swords, and Clubs. In each suit, there are eight pip cards (Ace, Two, Three, Four, Five, Six, Seven), and three face cards (Knave/Jack, Knight/Queen, and King). The face cards are easily distinguishable by their art: A Knave is just a man; a Knight has a horse; a King has a crown.

Don't worry if you don't have a dedicated Scopa deck - you'll notice that this is a subset of a normal French-suited deck. All you need to do is remove the Eights, Nines, and Tens and you can play Scopa just fine.

# Rules {#rules}

At the beginning of the game, the dealer deals three face-down cards to each player, and four face-up cards to the table. The player on the dealer's right goes first. When the last card from the last player's hand has been played, each player gets a new hand of three cards.

## Capturing {#capturing}

During your turn, you have two goals:

* To capture as many cards as you can, and
* To capture important, high-value cards

Capturing cards is done by using a card from your hand to "buy" one or more cards from the table whose value add up to the card you are playing. There are two caveats to this:

* If there is already a matching card on the table, you must capture that card even if you could capture more in some other combination, and
* If you cannot capture, you must place a card on the table

For example, let's assume the table has a Six, Seven, Three, Four, and an Ace. I have a Seven in my hand, which means I have three capture options:

* The Seven alone,
* The Six and Ace, adding up to seven, and
* The Four and Three, also adding up to seven

We know from the rules, however, that I can **only** capture the Seven even though the other captures would be better. Better luck next turn!
		
### Scopa! {#scopa}

If you manage to capture all of the cards from the table, this is called a **Scopa**, and is a cause for celebration and gloating. Why? Because you just got a free point regardless of other scoring metrics. Congratulations! Scopas cannot happen on the last card of the round, however. After a Scopa, the next player's only option is to place a card on the table.

### Last Capture {#last-capture}

The last player to capture cards in the round (as in, the deck has run out and all hands have been played out), captures all the remaining cards on the table.

## Scoring {#scoring}

Games consist of rounds, during which the entire Scopa deck is played all the way through. After each round, points are calculated for each player, and a new round starts if none of the players have reached the point goal, which is usually either six for a short game, or eleven, sixteen, or 21 for a longer game.

Getting points comes from five metrics, which sounds like a lot to remember, but it's pretty easy as they are each distinct and easy to remember. If there is a tie for any of the four non-Scopa metrics, no points are awarded for that metric. In fact, the only guaranteed points per round are from Scopas and capturing the Seven of Coins.

* *Scopa*: You get one point per **Scopa** you managed to get this round,
* *Cards*: You get one point if you have the **most captured cards**,
* *Seven*: You get one point if you captured the **Seven of Coins** (or Seven of Diamonds if playing with a regular deck),
* *Coins*: You get one point if you captured more **Coins** than your opponents, and 
* *Primiera*: You get one point if you win Primiera, which is explained below.

Points are only calculated between rounds. Even if you know for a fact that you will win at the end of the round, you must play through the rest of the round and tally up the points afterward. You never know when someone might come from behind and tie or surpass you!
In case of a draw, deal additional hands until a player breaks the tie by getting a point. This is likely to be the Seven of Coins or a Scopa if the round doesn't play out to its finish.

### Primiera {#primiera}

Primiera is the only complicated scoring metric, but it gets easier to estimate the more you play. Primiera is won by giving the important cards a new value, adding up the score for the best card in each suit you have captured, and having a higher Primiera value than your opponent.

The Prima scores are:

* Sevens: 21
* Sixes: 18
* Aces: 16
* Fives: 15
* Fours: 14
* Threes: 13
* Twos: 12
* Face cards: 10

As you can see, Sevens, Sixes, and Aces are the most important cards to capture, because they will give you the highest Primiera score. If playing with two players, determining Primiera is fairly easy, because you know  each card must belong to one player or another. To easily estimate Primiera, count the Sevens, and whoever has the most wins. If there is a tie, count the Sixes, and so on.

*The original document includes a Javascript calculator for scoring Primiera.*

# Strategy {#strategy}

During your turn, it's important to keep a general strategy in your mind. Because you can only do so much during a turn, you must adapt your strategy and plan for what your opponent might do based only on what's in front of you and what you know of your opponent's playstyle.

In general, these are the main points of strategy, in what I consider to be their order of importance:

* Capturing the Seven of Coins,
* Capturing as many Sevens as possible,
* Capturing as many Coins as possible,
* Capturing as many Sixes and Aces as possible, especially if your opponent is gotten many Sevens,
* Keeping a total of eleven points on the table so that your opponent can't Scopa,
* Capturing as many cards as you can with each trick,
* Taking obvious "combo" cards that your opponent places down so that they cannot use them in tricks later,
* Placing high-value cards down after your opponent has gotten a Scopa so that they are less likely to get another

# Variations
As Scopa and its derivatives are popular all over the world, there are numerous versions with new and different rules. I have outlined some of these below.

* **Scopa di quindici**: Popular in Brazil as *Escoba*, instead of capturing cards that add up to your played card, you can only capture if the cards you want total up to 15
* **Scopa d'assi**: If you have an Ace, you may capture all cards on the table, though this does not count as a Scopa
* **Re bello**: Like the Seven of Coins, capturing the King of Coins also awards a point at the end of the round
* **Cappotto**: If a player is winning seven to zero, the game can be ended early as a victory for that player
