[README.md](https://github.com/user-attachments/files/33425794/README.md)
# 🎬 Flickle League

A shared scoreboard for our daily Flickle competition. Every weekday, Monday to Friday, everyone guesses the day's Flickle and logs how they did. The board keeps track of weekly, seasonal and all-time standings, and updates live for everyone who has it open.

## Scoring

The earlier you guess the movie, the more points you get:

| Guessed on | Points |
|------------|--------|
| Scene 1    | 5      |
| Scene 2    | 4      |
| Scene 3    | 3      |
| Scene 4    | 2      |
| Scene 5    | 1      |
| Missed     | 0      |

## Seasons

There are two seasons a year:

- **Season 1:** January to July
- **Season 2:** August to December

Each day's points count toward the season that day falls in.

## Using the board

- **Week:** tap a box for a person and day, then pick the scene they guessed it on (or "Missed it"). Today's column is highlighted. Use the arrows to look at earlier weeks.
- **Season:** standings for one season, with the current leader, or the champion once the season is over. Use the arrows to see past seasons.
- **All time:** total points, average per day, weeks won and first-scene guesses for everyone.
- **Manage players:** at the bottom of the page. Add new players in the Week view.

Weeks won only count finished weeks, and ties share the win. Some players have "earlier points" from before the board existed. These count toward totals but aren't tied to specific days.

There are no logins, so anyone with the link can enter or change scores. Play fair. 🍿

## How it's built

The whole site is a single `index.html` file hosted on GitHub Pages. Scores are stored in a free [Supabase](https://supabase.com) database, which also sends live updates to everyone viewing the page.

The database has two tables:

- `players`: each player's name, plus any earlier points and the season they belong to.
- `scores`: one row per player per day, storing the week (its Monday), the day (0 = Monday to 4 = Friday) and the points.

The table definitions are in `setup.sql`.

## Setting it up from scratch

1. Create a free Supabase project.
2. In Supabase, open the SQL Editor and run `setup.sql`. This creates the tables, opens them for reading and writing, turns on live updates and adds the starting players.
3. Near the top of the script in `index.html`, set `SUPABASE_URL` to the project URL and `SUPABASE_ANON_KEY` to the publishable key (it starts with `sb_publishable_`).
4. Upload `index.html` to this repo and turn on GitHub Pages under Settings, then Pages.

⚠️ Only ever use the **publishable** key in `index.html`. Never commit a **secret** key (starting with `sb_secret_`). It gives full control of the database to anyone who sees it.
