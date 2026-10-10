# Think First

One reasoning question a day. A single static page with no build step and no server.

Questions are drafted with AI and checked by the site owner before they go out. The site makes no claim that they are written by a person.

## How it works

- `index.html` holds the styles, the questions and the script.
- The question shown is picked from the calendar date. `LAUNCH` near the top of the script is day one; question 1 shows that day, question 2 the day after, and so on.
- A new question unlocks at midnight in the visitor's own time zone. Earlier days can be reviewed only if they were answered. Later days stay locked.
- Answers, streak and score are saved in the visitor's browser (`localStorage`, key `thinkfirst.v1`). Nothing is sent anywhere.
- If the date is past the last question, the page says there is no new question today. Days without a question do not break a streak.

## Adding a question

Add an object to the end of the `QUESTIONS` list:

```js
{
  kind: 'Probability',            // Probability, Estimation, Logic or Spot the flaw
  figure: 'chart',                // optional: 'chart', 'cards' or 'pie', each drawn by its own function
  minutes: 2,
  tease: 'One line used in the shared result. Never give the answer away.',
  question: 'The question text.',
  options: ['First', 'Second', 'Third', 'Fourth'],
  answer: 2,                      // position of the right option, counting from 0
  steps: ['Worked step one.', 'Worked step two.'],
  takeaway: 'One sentence the player can reuse.'
}
```

Never reorder or delete a question that has already gone out. Saved answers are stored by day number.

Check the arithmetic of every answer before publishing it.

## Changing the launch date

Edit `LAUNCH` in the script: `{ year: 2026, month: 10, day: 12 }`.

## Hosting

The page runs on any static host. On GitHub Pages: repository Settings, then Pages, then deploy from the `main` branch, root folder.

## Visitor counting and email sign-up

Both are built in and switched off until their settings are filled in, near the top of the script in `index.html`:

- `UMAMI_WEBSITE_ID`: the website ID from Umami. When set, the page loads Umami's script and counts visits plus four events: `first-answer`, `returned` (an answer from someone who has answered on an earlier day), `shared` and `signup`. No cookies are used.
- `SIGNUP_ACTION`: the address the email form posts to, taken from the email service's form embed code. `SIGNUP_FIELD` is the name of its email field. When set, a sign-up box shows after today's answer and on the opening screen. The box sends the address to the email service in the background and shows the result on the page. It is currently connected to a Kit form.

The footer text changes with these settings so it always describes what the page really does.

## Not built yet

- "How everyone else answered", which needs a database
