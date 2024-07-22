# TP Analyser les Logs avec Elasticsearch

Ce projet propose un guide pour analyser les logs avec Elasticsearch et Kibana via Docker.

## Prérequis

- Docker
- Docker Compose

## Démarrage

### Étape 1 : Lancer Elasticsearch et Kibana

Créez un fichier `docker-compose.yml` :

```yaml
version: '3'
services:
  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:8.14.2
    container_name: elasticsearch
    environment:
      - discovery.type=single-node
      - xpack.security.enabled=false
      - xpack.security.transport.ssl.enabled=false
    ports:
      - "9200:9200"
      - "9300:9300"
    networks:
      - elastic
  kibana:
    image: docker.elastic.co/kibana/kibana:8.14.2
    container_name: kibana
    ports:
      - "5601:5601"
    environment:
      - ELASTICSEARCH_HOSTS=http://elasticsearch:9200
    networks:
      - elastic
networks:
  elastic:
    driver: bridge
