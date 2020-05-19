# Docker / Docker compose

## Commands

```bash
docker-compose run --rm <service> <command> <args>
```

## Dockerfiles

Creating non-root user with same uid / gid as local user \(as part of a larger project using docker-compose\)

{% code title="wrap.sh" %}
```bash
#!/bin/bash

export host_uid=$(id -u)
export host_gid=$(id -g)
$@
```
{% endcode %}

{% code title="Dockerfile" %}
```text
ARG host_gid
ARG host_uid

RUN groupadd --gid ${host_gid} user && \
    useradd --uid ${host_uid} -g user user && \
    mkdir -p /home/user && \
    chown -R user /home/user
    
USER user
```
{% endcode %}

{% code title="docker-compose.yml" %}
```yaml
build:
  context: ./
  dockerfile: ./Dockerfile
  args:
    - 'host_uid=$host_uid'
    - 'host_gid=$host_gid'
```
{% endcode %}

```bash
./wrap.sh docker-compose ...
```

