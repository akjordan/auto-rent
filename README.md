auto_rent
================

This tiny app runs on Heroku and uses Heroku Scheduler to automate splitting rent every month with Venmo.

Once you get this deployed to Heroku add Scheduler with the following:

$ heroku addons:add scheduler:standard

Then head to https://scheduler.heroku.com/dashboard to set up your task like so

$ rake auto_rent  1x  Daily