## Basic concepts

GrimoireLab is free, open source software for software development analytics. It allows you to retrieve, organize, analyze and visualize data coming from tools involved in the development of software projects. Those tools are named `data sources` in the GrimoireLab jargon. Some of the data sources are highly related to software development such as Git or Jira and others are more related to connecting people such as Meetup, Slack or Mailman. Thus GrimoireLab can be used in very simple cases, such as counting authors in a git repository, or very complex ones, such as producing real time dashboards visualizing what is happening in large projects with thousands of repositories of different kinds.

The complete list of supported data sources is available [here](data-sources.md).

This is how GrimoireLab analyses data in a nutshell:
- information is collected from `data sources` and stored in [Elasticsearch](https://github.com/elastic/elasticsearch) indexes. This is what we call `raw data` as items are not modified, they are just a copy of the items that can be found upstream
- contributors data (names, emails, nicknames) is copied from the `raw data` to a [MariaDB](https://mariadb.com/) database where a component named [SortingHat](advanced/components/sortinghat.md) is used to group them using several heuristics and help us to curate them. The information related to the contributors' accounts is named `identities`.
- when `raw data` and `identities` are ready, GrimoireLab processes the different items and create lighter Elasticsearch indexes extended with information about the contributors. This is what we call `enriched data`
- in order to browse and play with the `enriched data` the information is displayed in a soft fork of Kibana named `Kibiter`, which by this time will have preloaded dashboards for the data sources being analyzed.
- after the first review of the data it is typical to curate the `identities` data to merge different accounts of the same contributor or to group them by organization/company/unit. This can be done with a user interface named [Hatstall](advanced/components/hatstall.md)

Some of the GrimoireLab components can be used by themselves, but usually you get the most benefit of them when you use them together. Those components also offer several APIs, data formats, and data collections that will help you to build different kinds of processing chains for data related to software development. You can find more information about this in the [components section](advanced/components/intro.md)
