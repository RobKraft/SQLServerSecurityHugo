---
title: "Typical Web App Design"
description: "A design for a typical web app"
date: 2022-02-27T00:34:51+09:00
draft: false
weight: 6
---

You won't be able to use Windows Authentication to easily let the SQL Server database determine the permissions for your users.  In the world of web apps, REST APIs, and phone apps, that is not a viable option.  But, you still have a choice to make between SQL Auth or Windows Auth.  Typically, all the apps on client devices, whether those are web apps or phone apps, will communicate with a Web Server app, which could be a REST API.  It is that app, the one running on the web server, that makes the connection to the database; therefore all users going through the app will connect to the database using the same credentials.  As far as SQL Server is concerned there is just one user - the web app (or REST API).  That web app still needs a connection string and that connection string will either use Windows Authentication or SQL Authentication.  If you use SQL Auth, you have to store a login/pwd to build the connection string, so you have the hassle of securing those credentials.  If you use Windows Auth, then the connection to SQL Server will be made using the permissions assigned to the account under which the Web App runs.  Every web app that runs logs into the operating system; so you can use a built-in account or you can create a custom account in the OS to be used by the web app to log in to the OS.  If you take this approach, you will put that login that the web app uses to log in to the OS into an Active Directory group, and map that Active Directory group to a role in SQL Server just like you probably do now.

So, in the end that is all pretty easy to set up and manage.  However, you need to remember that all users connect to the database using the same credentials.  Therefore, the application needs to have logic in it to restrict actions.  Typically, your application uses roles unique to the application that allow the people in the Manager role to do things that people in the EveryDayUser role can't.    Those roles don't matter to SQL Server, because it is giving all users the same permissions based on the Web App.

Of course, you now need to map users to roles.  This is probably best done by using an OAuth/SAML provider to outsource the application login.  When users open your web app or phone app, the app redirects them to a login page that comes from your OAuth provider (which could be AWS IAM or Azure IAM, or OKTA, or many others - you can create your own IAM but I very much recommend against it).  The OAuth provider gets their login and password and validates the user, possibly against your Active Directory, and sends a token back to the application to let the application know what roles the user is part of; which your app then uses to enable/disable features.

So, carrying it a little further.  If you use a good OAuth provider, that integrates with your Active Directory, your end users could use their AD credentials to logon through OAuth and get a token.  In addition, those tokens can be securely cached on the client device and set to expire and also auto-renew.  This means that when a user goes to log in to your web app or phone app, they don't get prompted for a password every time because it uses the cached credentials from a previous login - just like facebook and gmail do when you go to their sites.

There are many variations, but I think what I outlined above is the most common approach.

