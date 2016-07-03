# kibana-selfhosted
Docker Compose file to generate a Kibana + Elasticsearch instance in docker/kitematic

## Requirements
Please install

1) Docker Toolbox
```
https://www.docker.com/products/docker-toolbox
```
2) Docker-Compose
```
https://docs.docker.com/compose/
```

## Installation

Clone the repository

Using Kitematic (Docker toolbox), click Docker CLI to open a console which is remoted into your Virtual Box VM with Docker.

In the console, run:
```
  /> docker-compose -f docker-compose.yaml up -d
```

At this point 2 docker containers will be created:
- kibana_ki_1  (port 15601)
- kibana_es_1 (port 19200)

Now remote into kibana_ki_1 to update */opt/kibana/config/kibana.yml* file to address SSL issue:
```
  /> docker exec -it kibana_ki_1 bash
```
once remoted into the container:
```
/>cd /opt/kibana/config
/opt/kibana/config>sed '/es:9200/a elasticsearch.ssl.verify:false' kibana.yml
```
## Test

### Test Elasticsearch
In your Chrome web browser, navigate to
```
http://192.168.99.100:19200
```
Json response should be similar to this

```
{
  "name" : "Torrent",
  "cluster_name" : "elasticsearch",
  "version" : {
    "number" : "2.3.3",
    "build_hash" : "218bdf10790eef486ff2c41a3df5cfa32dadcfde",
    "build_timestamp" : "2016-05-17T15:40:04Z",
    "build_snapshot" : false,
    "lucene_version" : "5.5.0"
  },
  "tagline" : "You Know, for Search"
}
```

### Test Kibana
In your Chrome web browser, navigate to
```
http://192.168.99.100:15601
```

Kibana should now load.



## Contributing
1. Fork it!
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request :D

## History
- V1



## License
Copyright @ 2016 Spudmash Media Pty Ltd
