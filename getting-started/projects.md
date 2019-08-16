## Setting up your projects

The data sources file (typically named projects.json) is aimed to describe
the repositories grouped by project that will be monitored on your dashboard.

The format of this file is complex and will be dropped as soon as the
[new UI](https://grimoirelab.github.io/slides/2018-02-02/13_Bestiary-LT.pdf)
to add data sources is finished.


The basic structure of the file is like this:

```
{
    "project-name": {
        "data-source": [
            "https://github.com/Maya/first.git",
            "https://github.com/Maya/second.git"
        ],
        "data-source": [
            ...        
        ],
        ...
    },
    "project-name": {
        ...
    },
    "project-name": {
        ...
    }
}
```

But there are so many exceptions that it is better if you have a look in the
following sections to specific documentation about the data source you are
interested in.

The following sub-sections show how each of them must be included in the data
sources file in order to be analyzed. If you want to track more than one data
source per project just add the data source name and the repositories list under
the project name. In the examples below, the project Alice is tracking a single
data source.

### askbot

You'll have to use the endpoint of the server, all data will be collected and analyzed.

```
{
    "Alice": {
        "askbot": [
            "https://ask.myproject.org"
        ]
    }
}
```

### bugzilla


You'll have to use the endpoint of the server, all data will be collected
and depending on how it is set up, the analysis will be performed over all the
data or filtered by product.

First, a simple example where we collect and analyze everything.

```
{
    "Alice": {
        "bugzilla": [
            "https://bugzilla.myproject.com/"
        ]
    }
}
```

__Warning: complex setup below__

If we want to analyze only the oVart and mom products for the Alice project
then we need a setup like this using a project with name `unknown` which won't
appear on the dashboard
```
{
    "Alice": {
        "bugzilla": [
            "https://bugzilla.myproject.com/ filter-raw=product:oVart",
            "https://bugzilla.myproject.com/ filter-raw=product:mom"
            ]
        }
    },
    "unknown": {
        "bugzilla": [
            "https://bugzilla.redhat.com/"
        ]
    }
```

### bugzillarest


This is pretty similar to Bugzilla.

__Warning: complex setup below__

If we want to analyze by product and component for the Alice project
then we need a setup like this using a project with name `unknown` which won't
appear on the dashboard.
```
{
    "Alice": {
        "bugzillarest": [
            "https://bugzilla.myproject.org/buglist.cgi?product=Add-on+SDK&component=Documentation",
            "https://bugzilla.myproject.org/buglist.cgi?product=Add-on+SDK&component=General",
            "https://bugzilla.myproject.org/buglist.cgi?product=addons.myproject.org&component=Security"
            ]
        },
    "unknown": {
        "bugzillarest": [
            "https://bugzilla.myproject.org"
            ]
        }
}
```

### confluence

You'll have to use the endpoint of the server, all data will be collected and analyzed.

```
{
    "Alice": {
        "confluence": [
            "https://wiki.myproject.org"
        ],
```

__Warning: complex setup below__

In case you want to group the data by project it will be needed to use the reserved project name `unknown`. The system will use the url specified in that project name to download everything, the data collection will download everything even if it is not needed to produce the dashboard. Once data is downloaded, it will read the confluence spaces specified for each project name.

In the example below we just want to analyze the Confluence Space named `MYSPACE` and we want it to be part of the project `Alice`:

```
{
  "unknown": {
    "confluence": [ "https://symphonyoss.atlassian.net/wiki/" ]
  },
  "Alice": {
    "confluence": [ "MYSPACE" ]
  },
...
}
```

### discourse

You'll have to use the endpoint of the server, all data will be collected and analyzed.

```
{
    "Alice": {
        "discourse": [
            "https://forums.myproject.com"
        ]
    }
}
```

### gerrit

You'll have to use the endpoint of the gerrit server, all data will be collected
and depending on how it is set up the analysis will be performed over all the
data or filtered by product.

First, a simple example where we collect and analyze everything.
```
{
    "Alice": {
        "gerrit": [
            "gerrit.onosproject.org
            ]
        }
```

__Warning: complex setup below__

If we want to analyze only a subset of projects we need a setup like this using
a project with name `unknown` which won't appear on the dashboard
```
{
    "Alice": {
        "gerrit": [
            "gerrit.onosproject.org_projectA",
            "gerrit.onosproject.org_projectB",
            "gerrit.onosproject.org_projectC"
            ]
        },
    "unknown": {
        "gerrit": [
            "gerrit.onosproject.org"
        ]
    }
}
```

### git

```
{
    "Alice": {
        "git": [
            "https://github.com/Maya/first.git",
            "https://github.com/Maya/second.git",
            "https://gitlab.com/Molly/first.git",
            "https://gitlab.com/Molly/second.git"
        ]
    }
}
```

### github

```
{
    "Alice": {
        "github": [
            "https://github.com/Maya/first",
            "https://github.com/Maya/second"
        ]
    }
}
```

### gitlab

GitLab issues and merge requests need to be configured in two different sections.

```
{
    "Alice": {
        "gitlab:issue": [
            "https://gitlab.com/Molly/first",
            "https://gitlab.com/Molly/second"
        ],
        "gitlab:merge": [
            "https://gitlab.com/Molly/first",
            "https://gitlab.com/Molly/second"
        ],
    }
}
```

If a given GitLab repository is under more than 1 level, all the slashes `/` starting from the second level have to be replaced by `%2F`. For instance,
for a repository with a structure similar to this one `https://gitlab.com/Molly/lab/first`, the proper way to include it in
the sources file would be:

```
{
    "Alice": {
        "gitlab:issue": [
            "https://gitlab.com/Molly/lab%2Ffirst"
        ],
        "gitlab:merge": [
            "https://gitlab.com/Molly/lab%2Ffirst"
        ],
    }
}
```

### jenkins

You'll have to use the endpoint of the server, all data will be collected and analyzed.

```
{
    "Alice": {
        "jenkins": ["https://build.myproject.org/ci"]
        }
}
```

### jira

You'll have to use the endpoint of the server, all data will be collected and analyzed.

```
{
    "Alice": {
        "jira": ["https://jira.myproject.org/ci"]
        }
}
```

### mbox

For mbox files, it is needed the name of the mailing list and the path where
the mboxes can be found. In the example below, the name of the mailing list is
set to "mirageos-devel"

```
{
    "Alice": {
        "mbox": [
            "mirageos-devel /home/bitergia/mbox/mirageos-devel/"
        ]
    }
}
```

### mediawiki

You'll have to use the endpoint of the server, all data will be collected and analyzed.

```
{
    "Alice": {
        "mediawiki": [
                "https://www.myproject.org/w"
            ]
    }
}
```

### meetup

For meetup groups it is only needed the identifier of the meetup group:

```
{
    "Alice": {
        "meetup": [
        "Alicante-Bitergia-Users-Group",
        "South-East-Bitergia-User-Group"
        ]
    }
}
```

### nntp

The way to setup netnews is adding the server and the news channel to be
monitored. In the example below, the `news.myproject.org` is the server name.

```
{
    "Alice": {
        "nntp": [
            "news.myproject.org mozilla.dev.tech.crypto.checkins",
            "news.myproject.org mozilla.dev.tech.electrolysis",
            "news.myproject.org mozilla.dev.tech.gfx",
            "news.myproject.org mozilla.dev.tech.java"
            ]
    }
}
```
### phabricator

You'll have to use the endpoint of the server, all data will be collected and analyzed.

```
{
    "Alice": {
        "phabricator": [
            "https://phabricator.wikimedia.org"
            ]
        }
}
```

### pipermail

```
{
    "Alice": {
        "pipermail": [
            "http://lists.wikimedia.org/pipermail/analytics",
            "http://lists.wikimedia.org/pipermail/commons-l",
            "http://lists.wikimedia.org/pipermail/design"
            ]
        }
}
```

### redmine

You'll have to use the endpoint of the server, all data will be collected and analyzed.

```
{
    "Alice": {
        "redmine": [
            "http://tracker.ceph.com/"
            ]
        }
}
```

### rss
```
{
    "Alice": {
        "rss": [
            "https://blog.myproject.com/feed/"
            ]
    }
}
```

### slack

The information needed to monitor slack channels is the channel id. The ones
below won't work. The channel id is unique inside slack.com service, so the URL
is always https://slack.com/ before the channel_id.

```
{
    "Alice": {
        "slack": [
            "https://slack.com/A195YQBLL",
            "https://slack.com/A495YQBM2"
        ]
    }
}
```

### stackexchange
```
{
    "Alice": {
        "stackexchange": [
            "http://stackoverflow.com/questions/tagged/httpd",
            "http://stackoverflow.com/questions/tagged/nginx"
        ]
    }
}
```

### supybot

For supybot files, it is needed the name of the IRC channel and the path where
the logs can be found. In the example below, the name of the channel is
set to "irc://irc.freenode.net/atomic"

```
{
    "Alice": {
        "supybot": [
            "irc://irc.freenode.net/atomic /home/bitergia/irc/percevalbot/logs/ChannelLogger/freenode/#atomic"
        ]
    }
}
```

### twitter

Note: Twitter data is not 100% supported by the GrimoireLab tools. The data collection
is performed via logstash instead of using Perceval.

__Warning: complex setup below__

In order to group by project it is needed to have a list of hashtags per project
and the tricky project with name `unknown` which won't appear on the dashboard.
```
{
    "Alice": {
        "twitter": [
            "kubernetes",
            "cloudcomputing"
        ],
    "unknown": {
        "twitter": [
            ""
        ]
    }
}
```

If you want us to analyze everything stored in the raw index, just add the
`twitter` entry under the `unknown` project. Example:
```
{
    "unknown": {
        "twitter": [
            ""
        ]
    }
}
```
