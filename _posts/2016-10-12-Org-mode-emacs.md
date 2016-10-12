---
layout: post
title:  "Org-mode beginners setup"
categories: Emacs
tags: emacs org-mode planning
---
{% include JB/setup %}

Acording to the official [documentation][http://orgmode.org/worg/org-configs/org-customization-guide.html] for beginners the following things are neccessary for starting to use Org-mode: **Nothing at all!**

From my side I have to add that one probably still needs some
experience in using of Emacs itself. Basic setup to emacs
configuration file for Org-mode (~/.emacs in my case):

{% highlight lisp %}
(add-to-list 'auto-mode-alist '("\\.org\\'" . org-mode))
(global-set-key "\C-cl" 'org-store-link)
(global-set-key "\C-ca" 'org-agenda)
{% endhighlight %}

The first string will tell emacs automatically go to org-mode when
file with .org extension is opened. The second string bind C-c+l (big
C in emacs notation is Ctrl button, "-" to press it simultaniously,
"+" to press in a sequence) key for storing a link on a particular
string particular file. This link can be inserted to org-file later
with C-c+C-l. To open the link one can use C-c+C-o. The third string
bind C-c+a for agenda window:

![](https://azarnyx.github.io/pic/Agenda.png)

For my Agenda I use two different files: "tasks.org" and
"schedule.org". In schedule.org I store events and task.org is used
for everyday's TODOs.

{% highlight lisp %}
(define-key global-map "\C-cc" 'org-capture)
; Log done state in TODOs
(setq org-log-done t)

; Set Org-Capture templates
(setq org-capture-templates
    `(
      ("t" "todo" entry (file+headline "~/Calendars/task.org" "Tasks")
        (file "~/org/tasks.orgcaptmpl"))
	  ("e" "event" entry (file+datetree "~/Calendars/schedule.org" "Events")
        (file "~/org/events.orgcaptmpl"))
))

(setq org-agenda-files (list "~/Calendars/task.org"
                             "~/Calendars/schedule.org"
))
{% endhighlight %}

Org capture binded with C-c+c starts dialogue box where I can choose
which type of notes I want to create. With "t" the task note will be
created. The task event will be stored in the file
"~/Calendars/task.org". I use "~/org/tasks.orgcaptmpl" as a template
for a task note. The template file for task look like:

{% highlight org %}
** TODO %t %^{Title}
%?
{% endhighlight %}

%t is time and %^{Title} is title. Guide to notes template with more
 options is available
 ([http://emacsnyc.org/assets/documents/how-i-use-org-capture-and-stuff.pdf][http://emacsnyc.org/assets/documents/how-i-use-org-capture-and-stuff.pdf]). The
 same is for event type of notes.
 
The other usefull tools for Org-mode Agenda are Calfw and Org-Gcal
(thanks to
[http://jameswilliams.be/blog/2016/01/11/Taming-Your-GCal.html][http://jameswilliams.be/blog/2016/01/11/Taming-Your-GCal.html]).

Calfw allows agenda to look nicely. It is actually like to have
Google-Calendar view inside Emacs. For installation it is possible to
simply clone emacs-calfw from the repo
([https://github.com/kiwanami/emacs-calfw][https://github.com/kiwanami/emacs-calfw])
and add to .emacs file the following strings:

{% highlight lisp %}
(load "~/emacs/emacs-calfw/calfw.el")
(load "~/emacs/emacs-calfw/calfw-org.el")
(require 'calfw)
(require 'calfw-org)

(defalias 'ca 'cfw:open-org-calendar)
{% endhighlight %}

Then Calfw view is available with "M-x ca":

![](https://azarnyx.github.io/pic/calendar.png)


Org-Gcal is used for synchronyzation with Google-calendar. To install
it, one needs to clone:

1) https://github.com/tkf/emacs-request
2) https://github.com/jwiegley/alert
3) https://github.com/kiwanami/emacs-deferred
4) https://github.com/myuhe/org-gcal.el

and load to .emacs file:

{% highlight lisp %} 
(load "~/emacs/alert/alert.el") 
(load "~/emacs/emacs-request/request.el") 
(load "~/emacs/emacs-deferred/deferred.el")
(load "~/emacs/emacs-request/request-deferred.el")
(load "~/emacs/org-gcal.el/org-gcal.el")
(require 'org-gcal)
{% endhighlight %}

The last thing to set up synchronization is to create application in
Google-API that is allowed to access to Google-calendar. The
instruction that is provided on
([https://github.com/myuhe/org-gcal.el]) seems outdated. Here I list the
new up-to-date instruction:

1) Go on [Google Developers Console][https://console.developers.google.com/iam-admin/projects]
2) Create a project (with any name)
3) Click on Google APIs
4) Choose Calendar API
5) Press "Enable" button to enable Calendar API for your project
6) Press "Go to credentials" button to set up access
7) Choose "OAuth client ID", First you will offer to setup project consent screen. You need to sepcify only "Product name shown to users" line and press save button.
8) After saving, "Create client ID" will appear and you should choose Application type "Other" and "Create"
9) save **client ID** and **client secret**
10) Go to [Google Calendar][https://calendar.google.com/calendar]
11) Go to settings, Choose "Calendar" menu. Press on the name of calendar you want to synchronize.
12) Near ICAL and HTML you will find Calendar ID: **callendar id**

So you finally have three different things: **client ID**, **client
secret** and **callendar id**. Now to set up synchronization add the
following strings to your emacs configuration file:

{% highlight lisp %} 
(setq org-gcal-client-id "cliend ID"
      org-gcal-client-secret "client secret"
      org-gcal-file-alist '(("callendar id" .  "~/Calendars/schedule.org")
	  ))
{% endhighlight %}
