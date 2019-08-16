## Managing identities

In the context of GrimoireLab we use the term `identites` to refer to the information obtained from a
contributor from a given data source. Depending on the data source and even on its configuration we can
obtain more or less information from the project contributors. Depending on the quality of the data and
the heuristics we apply we can group the different `identities` used by the same person, this groups
of identities belonging to the same contributor is what is called in the GrimoireLab jargon `unique identity`.

Let's see this with example where we are obtaining data from three different data sources. In this example
Git, Github and Slack.

* Github:
 * name: "Mandy Patinkin"
 * username: i.montoya
* Slack:
 * name "M. Patikin"
 * username: patikin
* Git:
 * name: "Mandy Patikin"
 * email: mpatikin@homeland.tv

In the example above, we have three records with three different identities that could belong to the actor
Mandi Patikin. The task of maintaining the database with these records and to group them by using a set
of heuristics is `SortingHat`'s duty. For each `unique identity` there is extra information such as
the affiliation, a flag to mark this profile as a bot or even the gender.

SortingHat can be installed via pip3 and the CLI is really complete but it is also a bit complex. A subset
of its features are available using a user interface named `Hatstall`.

In case you are looking for extended documentation about both tools you can go to their Github repositories:
* [Github repo](https://github.com/chaoss/grimoirelab-sortinghat/blob/master/README.md).
* [Hatstall repo](https://github.com/chaoss/grimoirelab-hatstall/blob/master/README.md)
