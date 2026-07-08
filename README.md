# Session Feedback Form

A token-based, per-participant feedback form for DataRobot customer sessions. Hosted on GitHub Pages. No login required for participants — works in any browser, any mail client.
Also a QR based, so participants and directly scan from the session and fill the form from their phone Only. Integrated with Google Chat for all notifications

# How to run this code #
This is the html page for the Token Based Session Feedback.

Please clone repo this into your github account for personalised experience 

## Backend Set Up
Backend of this code is in google Sheet App Script. 
The BE Code is available at: https://github.com/datarobot/feedback-form-be. You will need to set up the Backend first and get the Script ID.


## Update the Script ID:
Go to Line ~565 in index.html and replace the *appScriptUrl* parameter value


## To Publish the Site
- Go to Settings -> Pages 
- Under Build and Deployment
    - Source: *Deploy from Branch*
    - Branch: <the name of the branch> and directory is *\root*
- Hit Save and Publish

> Will take sometime to publish the site


