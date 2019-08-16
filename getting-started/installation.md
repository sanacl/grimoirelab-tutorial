## Installing GrimoireLab

In this section we will explain how to deploy the GrimoireLab analytics stack using Docker containers, but
due to most of the GrimoireLab tools are Python modules it is also possible to install them via `pip3`. If
you are interested in LATTER go to our [Expert documentation](EXPERT.md)

### Requirements

You'll need:
* GNU/Linux machine with 5GB of RAM
* docker >= 18.05.0-ce
* docker-compose >= 1.21.2
* git
* coffee or tee

### Quick start

Clone the repository locally.
```
git clone https://github.com/chaoss/grimoirelab-tutorial.git
```

Get your [Github token](https://github.com/settings/tokens) and place it in the file `getting-started/demo/setup.cfg`. The line to be replaced will look like this one:
```
[github]
api-token = <YOUR_API_TOKEN_HERE>
```

The Elasticsearch container needs special attention as [documented on the elasticsearch page](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html). This is why we recommend you to execute this parameter to allow ElasticSearch running smoothly in your computer
```
sudo sysctl -w vm.max_map_count=262144
```

Ready to start, execute:

```
cd ./getting-started/demo/ && docker-compose up -d
```


Go and get some coffee, in around 20 minutes data will be ready.

If you are a bit anxious and want to see the progress execute the command below, the data will be ready when
the number of documents in this petition for the enriched indexes is bigger or equal than the documents
for the raw indexes

```
watch -c -d -n10 "curl -s http://localhost:9200/_cat/indices"
```

... 20 minutes later ....

How was the coffee break? Go and play with the data at:
* http://localhost:5601 (here u can play with the data)
* http://localhost:8000 (modify the identities/affiliation data)

### Troubleshooting

* Q1. Are you missing data updates?

If you are running this in a "small" machine it is normal to get out of HD, make sure you have enough free space or your ES logs will show messages like this:
```
[2017-04-17 10:19:14,743][INFO ][cluster.routing.allocation.decider] [Dracula] low disk watermark [90%] exceeded on ...
```

The message means ES is not updating the indexes to avoid getting the disk full. In order to make some room try removing old stuff
```
docker volume prune
```

* Q2. Elasticsearch container is not running

If there seems to be no activity, the Elasticsearch docker might be failing.

The error message from `docker logs --tail=20 analtyicsdemo_elasticsearch_1` may look like:

```
[2019-06-13T11:18:13,505][INFO ][o.e.b.BootstrapChecks    ] [f6nsYdU] bound or publishing to a non-loopback address, enforcing bootstrap checks
ERROR: [1] bootstrap checks failed
[1]: max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]
```

The problem is that the variable `vm.max_map_count` was not set. The problem is [documented on the elasticsearch site](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html)

The solution is running as root:

```
sysctl -w vm.max_map_count=262144
```
