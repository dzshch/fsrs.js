## About The Project

fsrs.js is a JS Package implements [Free Spaced Repetition Scheduler algorithm](https://github.com/open-spaced-repetition/free-spaced-repetition-scheduler). It helps developers apply FSRS in their flashcard apps.

## Getting Started

```
npm install fsrs.js
```

## Usage

Create a card and review it at a given time:

```js
import * as fsrsjs from 'fsrs.js'
import { State, Rating } from '../src'

let fsrs = new fsrsjs.FSRS;
let card = new fsrsjs.Card;

//Set algorithm parameters
// fsrs.p.w=[0.4, 0.6, 2.4, 5.8, 4.93, 0.94, 0.86, 0.01, 1.49, 0.14, 0.94, 2.18, 0.05, 0.34, 1.26, 0.29, 2.61]
console.log(fsrs.p.w)

let now = new Date(2022, 10, 29, 12, 30, 0, 0);
let scheduling_cards = fsrs.repeat(card, now);
console.log(scheduling_cards);
```

There are four ratings:

```js
Rating.Again //incorrect response
Rating.Hard //recall; correct response recalled with serious difficulty
Rating.Good //recall; correct response after a hesitation
Rating.Easy // recall; perfect response
```

There are four states:

```js
State.New //Never been studied
State.Learning //Been studied for the first time recently
State.Review //Graduate from learning state
State.Relearning //Forgotten in review state
```

```js
//Get the new state of card for each rating:
scheduling_cards[Rating.Again].card
scheduling_cards[Rating.Hard].card
scheduling_cards[Rating.Good].card
scheduling_cards[Rating.Easy].card

//Update the card after rating `Good`:
card = scheduling_cards[Rating.Good].card

//Get the due date for card:
due = card.due

//Get the state for card:
state = card.state

//Get the review log after rating `Good`:
review_log = scheduling_cards[Rating.Good].review_log
```

## License

Distributed under the MIT License. See `LICENSE` for more information.
