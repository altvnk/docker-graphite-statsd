# Docker Image for Graphite

## Graphite + Statsd

This is a fork from [Sitespeedio](https://github.com/sitespeedio/docker-graphite-statsd)

## Quick Start

```sh
sudo docker run -d \
  --name graphite \
  -p 8080:80 \
  -p 2003:2003 \
  -p 8125:8025 \
  altvnk/graphite
```

And the final config that you should do is map the Graphite data dir outside of your container:

```sh
sudo docker run -d \
  --name graphite \
  -p 8080:80 \
  -p 2003:2003 \
  -p 8125:8025 \
  -v /path/to/data/graphite/storage/whisper:/opt/graphite/storage/whisper \
  altvnk/graphite
```

TODO also map log dirs

## Data retention
You can change how often data will be stored in the  [storage-schemas.conf](https://github.com/sitespeedio/docker-graphite-statsd/blob/master/conf/graphite/storage-schemas.conf) and how metrics will be aggregated over time in [storage-aggregation.conf](https://github.com/sitespeedio/docker-graphite-statsd/blob/master/conf/graphite/storage-aggregation.conf).

The default one looks like this:

```
retentions = 10s:1d,1m:7d
```

It will store data for 7 days, change that if you need to store data longer. Etsy has good [documentation](https://github.com/etsy/statsd/blob/master/docs/graphite.md) on how to setup your Graphite metrics.

To change it, you can feed the image with a new *storage-schemas.conf*. The one you want to replace is located  
*/opt/graphite/conf/storage-schemas.conf*

Start your image like this:

```sh
sudo docker run -d \
  --name graphite \
  -p 8080:80 \
  -p 2003:2003 \
  -p 8125:8025 \
  -v /path/to/data/graphite/storage/whisper:/opt/graphite/storage/whisper \
  -v /path/to/storage-schemas.conf:/opt/graphite/conf/storage-schemas.conf \
  altvnk/graphite
```
