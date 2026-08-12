# governance
Governance book review dashboard — setup and use
Three files:
File	What it is
`index.html`	The whole dashboard. Self-contained, no installation.
`data.json`	The pipeline, published log and reviewer bench as data.
`README.md`	This page.
---
1. Using it on one machine
Double-click `index.html`. It opens in your default browser.
Everything you change saves automatically to that browser. Nobody else can see it, and it stays there unless you clear your browsing data — so export a backup now and then (Export data file, bottom right).
Keep `index.html` and `data.json` in the same folder.
---
2. Putting it on GitHub for two people
The result is a private web address you and your colleague can both open. Roughly fifteen minutes, once.
Create the repository
Sign in at github.com. If your colleague has no account, they will need one.
Click + (top right) → New repository.
Name it `governance-reviews`. Choose Private. Click Create repository.
On the next page click uploading an existing file. Drag in `index.html` and `data.json`. Click Commit changes.
Turn on the web page
In the repository, click Settings → Pages (left sidebar).
Under Build and deployment, set Source to `Deploy from a branch`, branch `main`, folder `/ (root)`. Click Save.
Wait two or three minutes, then reload the Pages screen. It will show an address like:
`https://yourname.github.io/governance-reviews/`
That address is the dashboard. Bookmark it.
Add your colleague
Settings → Collaborators → Add people. Enter their GitHub username. They accept by email.
> A note on "private": with a private repository on a free plan, GitHub Pages may still serve the page publicly even though the code is private. If the contents are sensitive — reviewer email addresses, candid notes about who is unresponsive — either upgrade to GitHub Team, or skip Pages and have each of you download `index.html` and work locally, passing `data.json` between you. The dashboard works exactly the same either way.
---
3. Keeping the two of you in step
This is the part to be clear-eyed about. The dashboard saves to whichever browser it is open in. Two browsers means two separate copies, and there is no automatic merging. The routine below avoids collisions by keeping one authoritative copy.
`data.json` in the repository is the record. Your browser is a working copy.
When you sit down to work
Open the dashboard and click Load shared data.json. This pulls the current record and replaces what is on your screen. Do this first, every time.
When you finish
Click Export data file. Your browser downloads `data.json`.
Go to the repository on github.com.
Click the existing `data.json`, then the pencil icon, then Delete this file, and commit. (Or drag the new file in via Add file → Upload files, which overwrites it.)
Commit with a short note — "chased Tosun, added Schneider" — so the other person can see what moved.
The one rule
Only one of you edits at a time. Agree who has it — a message saying "taking the board for an hour" is enough. If you both edit and both upload, the second upload wins and the first person's work is gone. GitHub keeps every earlier version under the History tab, so it is recoverable, but it is a nuisance.
Splitting the books between Clay and April does not lift this rule. The responsible-editor field changes who is accountable for a book, not who can save the file — the whole board lives in one `data.json`, so two simultaneous uploads still collide even when you were working on entirely different titles.
If that discipline starts to chafe, the honest answer is that you have outgrown this format and want Airtable or a shared spreadsheet, where two people can type at once.
---
4. What the dashboard does
Pipeline — one card per book. The eight-step bar under each title is the status; click any step to move the book there. Doing so stamps today as the last contact date.
The steps: suitable for review → potential reviewers → invitation sent → reviewer agreed → book sent → sent to Research Exchange → final status.
Step 7 is terminal and needs an answer: published or rejected. A book that reaches it without one shows a short prompt on the card with both buttons; you can also set it in the edit panel, where the field is greyed out until the book is actually at step 7. Only a published outcome offers Move to published — a rejected review has no archive entry to make. Once a book is at step 7 it stops being chased, so it will not appear under overdue however long the dates say.
In revision is a flag rather than a step. Revision rounds happen at more than one point — before a review goes to Research Exchange and sometimes after — so tying them to a single rung would have misplaced half of them. Tick the box in the edit panel and an amber tag appears on the card. Setting a final status clears it.
Overdue is worked out rather than typed. A book is flagged red when a review due date has passed, and amber when nothing has happened for six weeks at a stage where something should have. The Overdue filter chip collects both. To change the six-week threshold, open `index.html` in a text editor and edit `var STALE_DAYS = 42;` near the top of the script.
Responsible editor — every book is assigned to Clay or April, or left unassigned. The name shows as a tag beside the Edit button, and the dropdown next to the search box narrows the board to one person. When you filter that way the figures across the top follow suit, so "April only" gives April's count of overdue books rather than the whole desk's. Assignment is set in the edit panel.
All seven existing entries are assigned to Clay, since they came from his backlog file. Reassign whatever should sit with April.
Source of proposal — how the book reached the desk: publisher, author, reviewer, or editor. It sits beside the responsible editor in the edit panel, shows in the card's detail grid as "Proposed by", and has its own column in the CSV. All seven existing entries are left as not recorded, since the backlog file does not say where each book came from — worth filling in as you go, because a season's worth of these answers tells you whether the pipeline is being fed by publisher mailings or by your own commissioning.
Edit opens the full record — bibliographic details, responsible editor, source of proposal, confirmed reviewer, the approach log, the five dates, and notes.
The approach log
Each book holds up to five numbered approaches, in the order you made them. Every approach carries a name, affiliation, email, the date you asked, the date they replied, a note, and one of six states:
State	Meaning
Suggested	A name on your list. Nobody has been contacted.
Invited	Asked, no answer yet.
Agreed	Accepted the commission.
Declined	Said no.
No reply	Asked, never answered, and you have stopped waiting.
Accepted, no delivery	Took it on and never produced the review.
Three buttons appear on the log itself so the common moves take one click rather than a trip through the edit panel:
Declined — on an invited name. Stamps today as the reply date.
Make reviewer — on an agreed name. Copies them into the confirmed reviewer field and advances the book to "reviewer agreed".
Never delivered — on the confirmed reviewer. Sets them to accepted, no delivery, clears the reviewer field, clears the due date, and drops the book back to "potential reviewers" so it re-enters the queue rather than sitting quietly at "book sent". The name stays in the log with its dates, so the history of the placement survives.
Out of names is a second derived signal alongside overdue. A book earns it when every approach has ended in declined, no reply, or no delivery, and nobody is confirmed. It has its own figure in the top strip and its own filter chip. Nothing is fixed by a flag, but it tells you which books need fresh names rather than another chase.
At five approaches the add button disappears. That is deliberate: five failed placements is a reasonable point to ask whether the book should be reviewed at all. Remove one to add another if you disagree in a particular case.
Add a book starts a blank entry.
Move to published appears once a review is received or cleared. It shifts the entry to the Published tab, where it lands under "Unassigned" until you give it an issue.
Published lists the thirteen reviews from your issue file, grouped by issue, with links through to Wiley.
Reviewer bench holds the eight names on file with their status, so you can see at a glance who is free.
Export CSV gives you the pipeline as a spreadsheet — responsible-editor, source-of-proposal, final-status and in-revision columns, and four columns per approach (name, status, asked, replied), so a placement record reads across the row. Useful for a report to the editors-in-chief.
---
5. Two things to check in the data
Both are inferences from the backlog file rather than statements in it.
Bátora as reviewer for Olsen. His contact details sit directly above the Olsen entry and the fit is right, but the file does not say so outright.
The year 2026. January, February and June entries are dated to 2026, reasoning from the published table running to October 2025.
Several records are deliberately incomplete: the Kaire book has only a surname, "The President's Echo System" has no author or publisher, and the Abbas review has no bibliographic data. These show as "Publication details to be confirmed" rather than being hidden.
---
6. If something goes wrong
The page looks unstyled. The typefaces load from Google Fonts and need a connection. Offline, it falls back to system fonts — everything still works.
Changes vanished. Private or incognito browsing discards storage when you close the window. Use a normal window.
"Load shared data.json" says it only works on a web address. You opened the file from your desktop rather than the Pages address. Use Import data file and pick the file by hand.
You want the original data back. Reset to original restores the seven pipeline entries and thirteen published reviews as first built.
You have an older data file. Files exported before the approach log was added still import cleanly — the new fields are filled in as blank. Nothing needs converting by hand.
You have a file from before the ladder changed. Anything sitting at the old "review received", "revisions requested" or "cleared for copyediting" steps is moved to sent to Research Exchange on import, and old "revisions requested" entries are additionally ticked as in revision. Check those entries once after importing — a review that was in hand but not yet forwarded belongs back at book sent.
