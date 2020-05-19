# Docker / Docker compose

## Commands

```text
docker-compose run --rm <service> <command> <args>
```

## Dockerfiles

Creating non-root user with same uid / gid as local user

{% code title="wrap.sh" %}
```text
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

