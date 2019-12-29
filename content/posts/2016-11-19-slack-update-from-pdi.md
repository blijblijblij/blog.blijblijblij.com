+++
title = "Slack update from pdi"
draft = false
date = "2016-11-19T10:00:04+01:00"
author = "Rogier Wessel"
comments = true
share = true
image = "images/cover.jpg"
slug = "slack-update-from-pdi"
tags = ["pentaho", "pdi", "slack"]
post = "/:year/:month/:day/:slug.html"

+++
# Data-transform your slack channels
In my humble opinion [Slack](https://slack.com/) is a fantastic tool for keeping development teams aligned and informed. It has (irc supported) chat, [voice calls](https://get.slack.help/hc/en-us/articles/216771908-Start-a-voice-call-in-Slack), proper code snippet sharing but it really shines in its ability to [integrate all that is important to a team](https://api.slack.com/custom-integrations).

For example we integrate:

- updates on github, Pull requests, comments, ...
- updates on tickets, new, open, closed tickets
- updates from ci, builds, tests, the occasional `#FAIL`
- updates from deploys instantiated from ci onto the mesos cluster
- updates on failing services and network components from nagios
- bash scripts synchronising in the background or via cron

## One thing was missing

Updates from pesky long running etl-jobs, while being away from the vpn-ed carte status page. And a convenient way of updating fellow `are-we-there-yet-are-we-there-yet-are-we-there-yet-are-we-there-yet-` colleagues ;-).

## Enter the slack incoming webhook
Slacks [incoming-webhook](https://api.slack.com/incoming-webhooks) is simple, easy to understand and can be extended to support a lot of feedback:

```shell
curl -X POST \
--data-urlencode 'payload={"text":"This is a line of text.\nAnd this is another one."}' \
https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX
```

Pdi can do this nicely, and posting it to a slack endpoint seems a no brainer. So for something to be usefull it has to:

- update on starting a job
- update on sub jobs / transformations
- escalate on `#FAIL`-ed data transformations

## Do it

A reporting transformation that delivers the very same json, but with some additions:

![report to slack](/images/2016-11-19_tr_report.png "report to slack")

Script the json with javascript:

```javascript
var payload= '{' +
	'"channel": "' + channel + '",' +
    '"username": "' + username + '",' +
	'"text": "' + env + '",' +
    '"attachments": [' +
        '{' +
            '"title": "' + title + '",' +
            '"text": "' + text + '",' +
			'"fallback": "' + text + '",' +
            '"color": "' + color + '"' +
        '}' +
    ']' +
'};';
```

Incorperate the slack reporting into a bigger picture:

![main job](/images/2016-11-19_jb_main.png "main job")

Et voila, some slack updates:

![on slack](/images/2016-11-19_slack_updated.png "on slack")

## Thin foil hat
This thing is updating from internal sources onto semi-public services, save to say to not stick any comprising data in those shiny new status updates...

## Source kjb / ktr
[link](https://github.com/blijblijblij/pdi-slack-reporting/archive/version-Release-1.zip)
