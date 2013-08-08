---
layout: post
title: "Getting Jenkins to work with LDAP"
date: 2013-08-08
category: tools
---

I sent up a jenkins server at work to help automate my teams builds and perform some basic testing on every build. One of the requirements for using it is that it must be secured. At work, we have an ldap server, which I previously used to secure our gerrit setup. Setting up jenkins to work well with the ldap server was a little for complicated. As a quick google search for "jenkins ldap slow" demonstrates.

The problem is with jenkins configured to query our ldap server, it was taking several minutes to login. Which was long enough that I would start to work on something else, forget about the login for a while, and then come back after my login session had expired and have to start the login process again.

After much searching and trial and error. Here are the setting I had to use to get rid of the login delay.

Under "Manage Jenkins" => "Configure System" => "Access Control" => "Security Realm" => "LDAP"
 * Server = address of the ldap server to query.
 * root DN = _blank_
 * Allow blank rootDN = __TRUE__
 * User search base = _blank_
 * User search filter = __uid={0}__
 * Group search base = _blank_
 * Group search filter = _blank_
 * Group membership filter = __(member={0})__

The <a href="https://wiki.jenkins-ci.org/display/JENKINS/LDAP+Plugin">LDAP Plugin wiki page</a> contains more information about all the setting. However, not knowing much about LDAP, a lot of it was not helpful to me. Although one cool thing I discovered while investigating this, was the "Script Console." This is a page under the "Manage Jenkins" section that allows you to run scripts against the running jenkins instance. It is kind of like a primative jenkins REPL.
