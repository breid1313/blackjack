# Blackjack

## Overview

This program provides a simple interface to simulate the game of Blackjack (21) against a dealer. A single player may compete against the dealer at a time.

## Quickstart

The project is setup as a jupyter notebook (vs a standalone python file or module), so it is recommended you run the code from a Jupyter Lab environment.
However, some IDE's also support running ipython notebooks.

Open the notebook `midterm_part2.ipynb` in jupyter lab, select a kernel, and then run all cells. Running all cells with execute the necessary code to setup the game and will then enter gameplay at the bottom of the notebook.

### Gameplay, rules, and assumptions

When the game starts, a deck is initialized with all 52 cards in a standard deck and then shuffled. Two cards are then dealt in an alternating pattern to both the player and the dealer. In other words, the player receives a card, then the dealer, then player, then dealer. Both of the player's cards will be visible, but only the first dealer card will be visible.

After the 3 eligible cards are shown, the player is asked whether to "hit" or "stand". The response is cast to lower case, so a response of `hit`, `Hit`, or any other combination of cases will indicate the player would like to hit. The same handling is in place for a `stand` selection.

If the player hits and the program detects a bust, the code will automatically handle any Aces in the players hand, changing their value one at a time from 11 to 1 in an attempt to get the score below a bust. Only the necessary number of aces will change value, meaning that the player is able to use a hand of `Ace, Ace, Ace, Eight` and score 21 by `11+1+1+8`. If the player hits this particular hand again, all aces will then be score as a 1 in that hand.

If a player hits and gets a hand with a score of 21 or below, they can continue hitting if they wish. If at any time the player busts or chooses to stand, it becomes the dealers turn.

In this version of the game, the dealer only reveals their second card and takes their turn if the player has not busted. If the player busted, we immediately "clear the table" so that the dealer does not show their second card and the player cannot count cards (which is illegal in a casino!).

Assuming the player has not busted, the dealer continues to hit their hand until their score reaches 17 or higher or they bust. At this point, gameplay stops and we decide a winner.

- If the player wins or the dealer busts, the player's bet is added to their chips, and the current bet set to 0
- If the player loses or the player busts, the player's bet is subtracted to their chips, and the current bet is set to 0
- If there is a tie, no chips are added or taken from the player and the bet is set to 0

Once scoring has occurred, we reset both the player's and dealer's hands and ask if the player wants to play again? The default response is `y`, so any entry other than `N` or `n` will cause the program to continue another loop. Assuming there are 4 or more cards left in the deck, gameplay will restart. If at any point during gameplay the deck runs out of cards, play will terminate and scoring will commence.

Gameplay will also not be allowed to restart if the player is out of chips. If this happens, they will not be prompted to play again and the game will end.

Any termination of gameplay (out of cards, out of chips, player selects not to play again) will completely reset the table the next time the program is run. That is, there will be a new deck and new chips allocations. We completely restart in this case. The cell must be re-executed in order to start gameplay again.