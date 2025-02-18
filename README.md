# ansible-role-docker-container-wgaccess

Role to run wgaccess in a docker container

## Table of content

- [Requirements](#requirements)
- [Default Variables](#default-variables)
  - [docker_container_wgaccess_admin_password](#docker_container_wgaccess_admin_password)
  - [docker_container_wgaccess_admin_username](#docker_container_wgaccess_admin_username)
  - [docker_container_wgaccess_capabilities](#docker_container_wgaccess_capabilities)
  - [docker_container_wgaccess_comparisons](#docker_container_wgaccess_comparisons)
  - [docker_container_wgaccess_config_template](#docker_container_wgaccess_config_template)
  - [docker_container_wgaccess_devices](#docker_container_wgaccess_devices)
  - [docker_container_wgaccess_env](#docker_container_wgaccess_env)
  - [docker_container_wgaccess_etc_hosts](#docker_container_wgaccess_etc_hosts)
  - [docker_container_wgaccess_image](#docker_container_wgaccess_image)
  - [docker_container_wgaccess_labels](#docker_container_wgaccess_labels)
  - [docker_container_wgaccess_name](#docker_container_wgaccess_name)
  - [docker_container_wgaccess_networks](#docker_container_wgaccess_networks)
  - [docker_container_wgaccess_ports](#docker_container_wgaccess_ports)
  - [docker_container_wgaccess_privatekey](#docker_container_wgaccess_privatekey)
  - [docker_container_wgaccess_restic_enable](#docker_container_wgaccess_restic_enable)
  - [docker_container_wgaccess_restic_retention](#docker_container_wgaccess_restic_retention)
  - [docker_container_wgaccess_restic_s3_bucket_name](#docker_container_wgaccess_restic_s3_bucket_name)
  - [docker_container_wgaccess_restic_s3_endpoint](#docker_container_wgaccess_restic_s3_endpoint)
  - [docker_container_wgaccess_restic_s3_repo](#docker_container_wgaccess_restic_s3_repo)
  - [docker_container_wgaccess_restic_s3_repo_access_key](#docker_container_wgaccess_restic_s3_repo_access_key)
  - [docker_container_wgaccess_restic_s3_repo_password](#docker_container_wgaccess_restic_s3_repo_password)
  - [docker_container_wgaccess_restic_s3_repo_secret_key](#docker_container_wgaccess_restic_s3_repo_secret_key)
  - [docker_container_wgaccess_restic_tag](#docker_container_wgaccess_restic_tag)
  - [docker_container_wgaccess_volume_dir](#docker_container_wgaccess_volume_dir)
  - [docker_container_wgaccess_volumes](#docker_container_wgaccess_volumes)
  - [docker_image_wgaccess_name](#docker_image_wgaccess_name)
  - [docker_image_wgaccess_pull](#docker_image_wgaccess_pull)
  - [docker_network_wgaccess_name](#docker_network_wgaccess_name)
- [Discovered Tags](#discovered-tags)
- [Dependencies](#dependencies)
- [License](#license)
- [Author](#author)

---

## Requirements

- Minimum Ansible version: `2.1`

## Default Variables

### docker_container_wgaccess_admin_password

#### Default value

```YAML
docker_container_wgaccess_admin_password: SomeSecret...3...33
```

### docker_container_wgaccess_admin_username

The admin account password

#### Default value

```YAML
docker_container_wgaccess_admin_username: admin
```

### docker_container_wgaccess_capabilities

List of capabilities to add to the container.

#### Default value

```YAML
docker_container_wgaccess_capabilities: [NET_ADMIN]
```

### docker_container_wgaccess_comparisons

Allows to specify how properties of existing containers are compared with module options
to decide whether the container should be recreated / updated or not.

#### Default value

```YAML
docker_container_wgaccess_comparisons:
  image: strict
  env: strict
  volumes: strict
```

### docker_container_wgaccess_config_template

Path to config template file
https://www.freie-netze.org/wg-access-server/2-configuration/

#### Default value

```YAML
docker_container_wgaccess_config_template: templates/config.yaml.j2
```

### docker_container_wgaccess_devices

List of host device bindings to add to the container.

#### Default value

```YAML
docker_container_wgaccess_devices: [/dev/net/tun:/dev/net/tun]
```

### docker_container_wgaccess_env

Dictionery of key,value pairs for docker
environment variables to configure wgaccess.

Example:

```yaml

docker_container_wgaccess_env:

wgaccess__mailer__ENABLED: "false"

```

#### Default value

```YAML
docker_container_wgaccess_env: {}
```

### docker_container_wgaccess_etc_hosts

Dict of host-to-IP mappings, where each host name is a
key in the dictionary. Each host name will be added to
the container’s /etc/hosts file.

#### Default value

```YAML
docker_container_wgaccess_etc_hosts: {}
```

### docker_container_wgaccess_image

Repository path and tag used to create the container.
If an image is not found or pull is true, the image will be pulled from the registry.
If no tag is included, latest will be used.

#### Default value

```YAML
docker_container_wgaccess_image: '{{ docker_image_wgaccess_name }}'
```

### docker_container_wgaccess_labels

Dictionary of key value pairs for container labels.

Example:

```yaml

docker_container_wgaccess_labels:

traefik.enable: "true"

```

#### Default value

```YAML
docker_container_wgaccess_labels: {}
```

### docker_container_wgaccess_name

Name for the container

#### Default value

```YAML
docker_container_wgaccess_name: wgaccess
```

### docker_container_wgaccess_networks

List of networks the container belongs to.

#### Default value

```YAML
docker_container_wgaccess_networks:
  - name: '{{ docker_network_wgaccess_name }}'
```

### docker_container_wgaccess_ports

List of ports to publish from the container to the host.

#### Default value

```YAML
docker_container_wgaccess_ports:
  - 8000:8000/tcp
  - 51820:51820/udp
```

### docker_container_wgaccess_privatekey

Wireguard private key.
wg genkey

#### Default value

```YAML
docker_container_wgaccess_privatekey: dsfkjhkheuhHKJHIHUHKjduehHHUGzuezud=
```

### docker_container_wgaccess_restic_enable

Enable restic backup for the container's mounted volumes.

#### Default value

```YAML
docker_container_wgaccess_restic_enable: false
```

### docker_container_wgaccess_restic_retention

Retention settions for `restic forget` after the `restic backup`.

#### Default value

```YAML
docker_container_wgaccess_restic_retention:
  keep_last: 1
  keep_daily: 7
  keep_weekly: 4
```

### docker_container_wgaccess_restic_s3_bucket_name

Minio S3 bucket name for restic backup storage.

#### Default value

```YAML
docker_container_wgaccess_restic_s3_bucket_name: restic-{{ docker_container_wgaccess_name
  }}
```

### docker_container_wgaccess_restic_s3_endpoint

Minio S3 endpoint for restic backup storage.

Example:

```yaml

docker_container__base__restic_s3_endpoint: "https://minio.{{ dns_domain }}"

docker_container_wgaccess_restic_s3_endpoint: "{{ docker_container__base__restic_s3_endpoint }}"

```

#### Default value

```YAML
docker_container_wgaccess_restic_s3_endpoint: '{{ docker_container__base__restic_s3_endpoint
  }}'
```

### docker_container_wgaccess_restic_s3_repo

Minio S3 repo URL for restic backup storage.

#### Default value

```YAML
docker_container_wgaccess_restic_s3_repo: s3:{{ docker_container_wgaccess_restic_s3_endpoint
  }}/{{ docker_container_wgaccess_restic_s3_bucket_name }}
```

### docker_container_wgaccess_restic_s3_repo_access_key

Minio S3 repo access key for restic backup storage.

#### Default value

```YAML
docker_container_wgaccess_restic_s3_repo_access_key: '{{ docker_container__base__restic_s3_repo_access_key
  }}'
```

### docker_container_wgaccess_restic_s3_repo_password

Minio S3 repo password for restic backup storage.

#### Default value

```YAML
docker_container_wgaccess_restic_s3_repo_password: '{{ docker_container__base__restic_s3_repo_password
  }}'
```

### docker_container_wgaccess_restic_s3_repo_secret_key

Minio S3 repo secret key for restic backup storage.

#### Default value

```YAML
docker_container_wgaccess_restic_s3_repo_secret_key: '{{ docker_container__base__restic_s3_repo_secret_key
  }}'
```

### docker_container_wgaccess_restic_tag

Tag for the `restic backup` command

#### Default value

```YAML
docker_container_wgaccess_restic_tag: '{{ docker_container_wgaccess_name }}'
```

### docker_container_wgaccess_volume_dir

Volume mount host directory, where Treafik config files are stored.

#### Default value

```YAML
docker_container_wgaccess_volume_dir: '{{ docker_container__base__volume_dir }}/{{
  docker_container_wgaccess_name }}'
```

### docker_container_wgaccess_volumes

List of volumes to mount within the container.

#### Default value

```YAML
docker_container_wgaccess_volumes:
  - '{{ docker_container_wgaccess_volume_dir }}/data:/data'
  - '{{ docker_container_wgaccess_volume_dir }}/config.yaml:/config.yaml'
```

### docker_image_wgaccess_name

Repository path and tag for the container image.

#### Default value

```YAML
docker_image_wgaccess_name: ghcr.io/freifunkmuc/wg-access-server:master
```

### docker_image_wgaccess_pull

Indicate to always pull the docker image.

#### Default value

```YAML
docker_image_wgaccess_pull: false
```

### docker_network_wgaccess_name

Name of the docker network created for wgaccess.

#### Default value

```YAML
docker_network_wgaccess_name: '{{ docker_container_wgaccess_name }}_backend'
```

## Discovered Tags

**_docker-container-backup-all_**\
&emsp;Backup all containers' volume mounts.

**_docker-container-backup-init-all_**\
&emsp;Run init backup task for all container.

**_docker-container-backup-init-wgaccess_**\
&emsp;Run init backup task for wgaccess if restic is enabled.

**_docker-container-backup-list-all_**\
&emsp;List all containers' backups.

**_docker-container-backup-list-wgaccess_**\
&emsp;List wgaccess backups.

**_docker-container-backup-wgaccess_**\
&emsp;Backup wgaccess volume mounts.

**_docker-container-prereq-all_**\
&emsp;Ensure all pre-requisites are installed

**_docker-container-prereq-wgaccess_**\
&emsp;Ensure all pre-requisites for wgaccess are installed

**_docker-container-purge-all_**\
&emsp;Remove all containers and delete volume mounts.

**_docker-container-purge-wgaccess_**\
&emsp;Remove wgaccess and delete volume mounts.

**_docker-container-remove-all_**\
&emsp;Remove all containers.

**_docker-container-remove-wgaccess_**\
&emsp;Remove wgaccess.

**_docker-container-restore-all_**\
&emsp;Run restic restore for all restic enabled containers.

**_docker-container-restore-wgaccess_**\
&emsp;Run restic restore for wgaccess if restic is enabled.

**_docker-container-setup-all_**\
&emsp;Run setup task for all containers.

**_docker-container-setup-wgaccess_**\
&emsp;Run setup task for wgaccess.

**_never_**


## Dependencies

None.

## License

license (GPL-2.0-or-later, MIT, etc)

## Author

andif888
