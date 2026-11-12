ASA Event Database Interface

A single-file web app for reviewing UAP reports in the ASA events database. It shows events, the review pipeline and tasks, data gaps, media, and a read-only SQL console for analysts.

The whole app is one HTML file: ASA_Case_Database_v0.5.2.html. There is nothing to install or build. It talks directly to the ASA Supabase database from your browser, so you must be able to sign in with an ASA account.

What you need
A computer with a modern browser (Chrome, Safari, Edge or Firefox).
Python 3, which is already installed on macOS and most Linux systems. On Windows, install it from python.org.
The ASA database project URL and its publishable key (also called the anon key). Ask an ASA owner for these. Never use the secret or service key.
A username and password for the app. Ask an ASA owner to create one.
Run it on your computer

The app should be opened from a local web server rather than by double-clicking the file. This keeps sign-in and media viewing working correctly.

Create a folder and put the app file in it, renamed to index.html. macOS or Linux (Terminal):
   mkdir ~/asa_app
   cp ASA_Case_Database_v0.5.2.html ~/asa_app/index.html

Windows (PowerShell):

   mkdir $HOME\asa_app
   copy ASA_Case_Database_v0.5.2.html $HOME\asa_app\index.html
Start the server from that folder. macOS or Linux:
   cd ~/asa_app
   python3 -m http.server 8080 --bind 127.0.0.1

Windows:

   cd $HOME\asa_app
   py -m http.server 8080 --bind 127.0.0.1

You should see Serving HTTP on 127.0.0.1 port 8080. Leave this window open while you use the app.

Open http://localhost:8080/ in your browser.
On the first visit the app asks you to connect to the database. Enter:
Project URL: the ASA database address from an ASA owner.
Anon or publishable key: the publishable key from an ASA owner.
These are stored only in your browser. Click Save and continue.
Sign in with your username and password.
When you are finished, go back to the server window and press Control + C (Ctrl + C on Windows) to stop it.

The server only listens on your own computer (127.0.0.1), so nobody else on your network can reach it.

Check the version

The version number is shown in small text next to ASA in the upper left of the page, for example v0.5.2. If it shows an older number after you replace the file, do a hard refresh (Command + Shift + R on Mac, Ctrl + Shift + R on Windows and Linux).

Using the app
Dashboard, Pipeline board, Events, Tasks, Data gaps: review work and event details.
Events, Media tab: images, video, audio and PDF reports for an event. Small private files load automatically. Large private files (over 25 MB, mostly video) show a Load file button.
SQL console (analysts and owners): read-only queries against report data. Witness names, contact details and statements are not available there.
Users (owners): add and manage sign-in accounts. A username may use 3 to 40 letters, numbers, dots, dashes or underscores. Do not enter an email address as a username.
Troubleshooting
Problem	What to do
The page does not load	Check that the server window is still open and that you are using http://localhost:8080/.
"Address already in use"	Another server is already running. Stop it with Control + C, or use a different port such as 8081 in both the command and the address.
Old version still showing	Hard refresh, and confirm you copied the new file over index.html.
Blank connection screen again	The browser cleared its saved settings. Enter the project URL and key again.
Cannot sign in	Check the username has no spaces or @, then ask an ASA owner to reset the password.
Private media will not load	Sign out and in again. If it still fails, tell an ASA owner. Private files are served through a protected service that must be running.
Security notes
Do not put passwords, secret keys or the Vercel Blob token in this repository or in the app file.
The publishable key is meant to be public, but the database only returns data to signed-in users with the right role.
Public media links can be opened by anyone who has the address. Private media needs a signed-in analyst.
