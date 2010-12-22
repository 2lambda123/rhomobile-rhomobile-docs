Rhomobile Docs App
==================

CMS and content for documentation of the Rhomobile platform.

If you'd like to propose an edit to the Rhomobile docs, fork this repo, then send us a pull request.

This tool is based off the excellent heroku-docs project! https://github.com/heroku/heroku-docs

Setup
-----
	$ bundle install
	$ rake start #=> this will start the server and load the docs home page in your browser
	
Rebuilding & Publishing
-----------------------
This app loads content from sub-directories located in config.yml.  

To update the production copy (stored in docs/), run:

	$ rake load
	
This will copy all content from the sub-directories into docs/.  Then push to heroku:

	$ git add docs/
	$ git commit -m "adding new docs"
	$ git push heroku master

The app loads content from the docs subdirectory.  Pages are served with a 1 hour cache setting.

About
----

Originally written by Ryan Tomayko and Adam Wiggins.  This application is maintained by Rhomobile Dev.

Code is released under the MIT License: http://www.opensource.org/licenses/mit-license.php

All rights reserved on the content (text files in the docs subdirectory), although you're welcome to modify these for the purpose of suggesting edits.

http://docs.rhohub.com

http://github.com/rhomobile/rhomobile-docs


