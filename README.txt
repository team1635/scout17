=================
Installation
------------

* Prerequisites
Install putty from http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
Make sure you have the putty utilities in your path (especially pscp.exe)

* Instructions
Create database in cpanel
Create dba user in cpanel (let them pick the password)
Add dba user to database in cpanel
Add app user to database in cpanel
On the server create the *application directory* in a directory
 served by a web server (~/www/scout17) with php working
And the *config directory* somewhere else not served (~/dev/scout17)

On your development machine run
build/clean.bat
On your web server run (if already deployed)
~/dev/scout17/clean.sh
On your development machine run
build/build.bat
build/deploy.bat
On your web server
cd ~/dev/scout17
chmod u+x configure.sh
chmod u+x clean.sh
chmod u+x deploy.sh
./configure.sh
./deploy.sh
mysql --user=teamadmn_dba --password=dba_pass teamadmn_scout17 < createdb.sql > createdb.log
mysql --user=teamadmn_app --password='app_pass' teamadmn_scout17 < insert_event.sql > insert_event.log


=================
Deploy changes
--------------
On your development machine from the root of the project run
cd build
clean.bat
On your web server run (if already deployed)
cd ~/dev/scout17
./clean.sh
On your development machine run (still in the build directory)
build.bat
Answer D to the first question
Answer D to the second question
deploy.bat

=================
Deploy changes
--------------
How do I run the app:
1) assuming you loaded the events in the config section

=================
Helpful links
-------------
For event codes use:
http://frc-events.firstinspires.org/

Web services project:
https://usfirst.collab.net/sf/projects/first_community_developers/

Web services documentation:
http://docs.frcevents2.apiary.io/#reference

=================
Structure
---------

* index.html -> main landing page for the app. Scouting match page 
  (lib/css/bootstrap.min.css, lib/css/main.css)
  (lib/js/jquery-1.10.1.js, lib/js/bootstrap.min.js, lib/js/index/stat.js)
  getMatch.php
  saveStat.php
  tab: Match
  tab: Auto
  tab: Tele Op
  tab: Save
  tab: Help
----------
* adminMenu.html -> admin menu page
  (lib/css/bootstrap.min.css, lib/css/main.css)
  (lib/js/jquery-1.10.1.js, lib/js/bootstrap.min.js, lib/js/index/saveCurrent.js)
  getMatch.php
  loadMatches.php
  tab: Set Current
  tab: Load Matches
----------
* infodb.php -> database login to be included in php files
----------
* getMatch.php -> gets data for the current match for the scouting page, so
  the scout can pick a team to follow through the match. Also used in 
  the adminMenu.html to determine the current match
----------
* saveStat.php -> saves the team stats for the match. used in index.html
----------
* saveCurrent.php -> saves what the next match is from the admin Menu
----------
* loadMatches.php -> called from adminMenu to scrape event info and load
  into table.
  lib/simple_html_dom.php
----------
* report.html -> the list of all matches (left) with links to the teams
----------
* getTeamReport.php ->  stats so far for a team
----------
lib/
  * simple_html_dom.php -> used to scrape the event to load matches
  css/
    * bootstrap.min.css
    * main.css -> empty, but there is stuff to be put there.
  js/
    * bootstrap.min.js
    * jquery-1.0.1.js
    index/
      * stat.js -> some functions for index.html
    adminMenu/
      * saveCurrent.js -> some functions for adminMenu
        saveCurrent.php
    report/
      report.js

Junk (appears to be)
--------------------
template.html
* getReport.php -> attempt to implement TODO #6
* report_temp.html -> attempt to implement TODO #6

=================
TODO
----
5) Make HTML report that works like getTeamReport, but returns all the teams 
  with the stats as columns. For AJ's AppSheet scouting app.
6) AJ is doing this. Playoff alliance building screen:
    Only list teams that we can pick (below us);
    If a team gets picked before we pick them, take them off the list.

Medium Priority
7.51) convert README.txt to README.md
7.52) switch loadMatches.php, saveCurrent.php to sqli
7.53) adminMenu.php and loadSchedule.html have hard-coded event lists

7) figure out how the first row is to be inserted into current_;
8) report.html should be dynamically generated (i.e. php)
9) report.html should be called ourMatches.php
10) decide file naming convention: camel case or underscore separated
11) upgrade bootstrap, jquery, html_dom.php


Low Priority
7.101) remove recompute_flat_stat() from saveCurrent.php if not used

101) Use Angular.js
102) Prevent event matches from loading a second time.
103) better build commands (ant, whatever) to stage the programs
  (fill in the real password), and sync with the website
104) Write test scripts
105) Find better way to layout the buttons other than current bootstrap hack.
106) Clean up getMatchReport.php.  It has weird backslash at top.


=================
Questions
---------
How do I set up php so VS code knows about the syntax?
Getting the following error from VS Code:
  Cannot validate the php file. The php program was not found. 
  Use the 'php.validate.executablePath' setting to conf ...
