An Incident Report (also called Postmortem) is a summary report to make known the reasons why a website or application experienced an outage or malfunctioned.

A postmortem seeks to serve two main purpose which includes:
a)Giving information to the stakeholders on the impact of the outage.
b)Analysis the detail of the root cause and how to fix it.
Upon the release of ALX's System Engineering & DevOps project 0x19, approximately 06:00am West African Time (WAT) here in Nigeria, an outage occurred on an isolated Ubuntu 14.04 container running an Apache web server. GET requests on the server led to 500 Internal Server Error's, when the expected response was an HTML file defining a simple Holberton WordPress site.

Timeline
00:00 PST - 500 error for anyone trying to access the website
00:05 PST - Ensuring Apache and MySQL are up and running.
00:10 PST - The website was not loading properly which on background check revealed that the server was working properly as well as the database.
00:12 PST - After quick restart to Apache server returned a status of 200 and OK while trying to curl the website.
00:18 PST - Reviewing error logs to check where the error might be coming from.
00:25 PST - Check /var/log to see that the Apache server was being prematurely shut down. The error log for PHP were nowhere to be found.
00:30 PST - Checking php.ini settings revealed all error logging had been turned off. Turning the error logging on.
00:32 PST - Restarting apache server and going to the error logs to check what is being logged into the php error logs.
00:36 PST - Reviewing error logs for php revealed a mistyped file name which was resulting in incorrect loading and premature closing of apache.
00:38 PST - Fixing file name and restarting Apache server.
00:40 PST - Server is now running normally and the website is loading properly.

Root cause: Wrong configuration rolled out to production environment

Fix: Rollback to the last working configuration

Corrective and preventative measures:

Tests: Code tests must be performed and approved before deployment to production