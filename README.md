Grind Timer

A single-file stopwatch for long work sessions. It has a distraction-free lock-in screen, forced hourly breaks, and daily goals where one unticked goal fails the day.

No build step, no dependencies, no backend. Open grind-timer.html in a browser and it works.

Features

Stopwatch

Counts up with an hourly progress ring. The display switches from MM:SS to HH:MM:SS after the first hour.
Timing is based on the wall clock, not animation frames, so it stays accurate in background tabs.
A running session survives a page reload or closed tab.
Optional label for what you're working on.
Reset logs the session as partial if you had at least 1 minute. Finish logs it as complete.

Lock in

Turns the screen pure black with only the white time digits, sized to fit the screen.
Tap the screen to show three dim controls (rotate, pause/resume, exit) for 3 seconds.
The rotate button flips the layout 90° for landscape, and the digits re-fit. The choice is remembered.
Requests fullscreen and keeps the screen awake where the browser allows it.

Auto break

After 1 hour of work, the stopwatch pauses and a 10-minute break starts.
At 10:00 you're asked whether to extend for another 10 minutes.
At 20:00 you get a "last 10 minutes" prompt for the final extension.
At 30:00 you're forced back to work and the stopwatch resumes.
An unanswered prompt sends you back to work after 2 minutes.
Can be switched off with the Auto break / 1H toggle.

Daily goals

Add your own goals each day and tick them off.
A day passes only if it has at least one goal and every goal is ticked. An open goal, no goals, or a day you skipped entirely counts as a fail and resets the streak.
A goal can only be removed within 5 minutes of adding it, so it can't be deleted to dodge a fail.
Shows the current streak, today's focused time, and a 7-day pass/fail strip.

Feedback

Completion and break tones (Web Audio), vibration, and browser notifications when the tab is hidden.
Each can be toggled.
Keyboard shortcuts
Key	Action
Space	Start / pause
R	Reset
L	Toggle lock in
Esc	Exit lock in
Running it

Open grind-timer.html directly, or serve the folder with any static host:

bash
python3 -m http.server 8000

To deploy:

GitHub Pages: push the file as index.html (or keep the name and link to it), then enable Pages for the branch.
Netlify / Vercel / Cloudflare Pages: drop in the folder. No build command is needed.

The only external request is Google Fonts (IBM Plex Mono and Space Grotesk). It falls back to system fonts if they can't load.

Data and privacy

Everything is stored in your browser's localStorage. Nothing is sent anywhere.

Key	Contents
grindtimer-day	Today's goals, sessions, focus time, streak and day history
grindtimer-prefs	Sound, vibration, keep-awake, auto-break and rotation settings
grindtimer-run	The in-progress stopwatch state, used to restore after a reload

Clearing site data resets everything, including your streak. Data lives per browser and device, so it doesn't sync between them.

Browser support

Works in current Chrome, Edge, Firefox and Safari. A few features depend on the browser:

Screen Wake Lock (keep screen on) and vibration aren't available everywhere. Unsupported toggles are hidden automatically.
Fullscreen may be unavailable on iPhone Safari. The lock screen still fills the viewport.
Notifications need permission, which is requested the first time you press start.
Mobile browsers can throttle or suspend background tabs. Elapsed time is still correct when you return, but a notification may arrive late.
Project structure
grind-timer.html   # the entire app (HTML, CSS and JS)
README.md
Customising

All the tunable values are constants at the top of the script:

js
const HOUR = 3600, BRK = 600, GRACE = 120, DEL_WINDOW = 5 * 60000;
HOUR is the work block length before a break, in seconds.
BRK is the length of each break stage, in seconds. There are up to three stages.
GRACE is how long an unanswered break prompt waits, in seconds.
DEL_WINDOW is how long after adding a goal it can still be deleted, in milliseconds.
License

Add a license of your choice (MIT is a common default for small tools like this).
