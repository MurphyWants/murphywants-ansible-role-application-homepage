# murphywants-ansible-role-application-homepage

## Description & Purpose



```
Image: 'ghcr.io/gethomepage/homepage'
tag: latest # unless otherwise specificed in the variables
```

Homepage is an application meant to be your home page. The entire page can be declaritively defined through a few yaml files to add bookmarks or widgets for weather, search or specific app integrations. This role will deploy the homepage container, deploy the templated yaml files as described in the variables and configure an nginx reverse proxy with a TLS cert. 

https://gethomepage.dev/


## How to Use

Example Inventory:

```
app_homepage:
  hosts:
    hostname.fdqn
  vars:
    EXAMPLE_VARIABLE: EXAMPLE_VALUE # This variable is required to run
```

Example Playbook:

```
- hosts: app_homepage
  gather_facts: yes
  become: yes
  tasks: 
    - name: Setup homepage
      ansible.builtin.import_role:
        name: "murphywants-ansible-role-application-homepage"
```

## Requirements/Dependencies
Uses the following modules:
- community.general.zfs
- community.docker.docker_compose_v2

Uses the following roles:
- murphywants-ansible-role-component-docker: Install and configure docker
- murphywants-ansible-role-component-dehydrated: Install and configure dehydrated, get TLS cert

## Tags
Ansible role template with the following actions & tags:

Tag | Description
--- | ---
Setup/Baseline | Setup the application and apply the configuration baseline
Start | Start required services
Stop | Stop required services
Update | Update the component applications
Remove | Remove configurations and applications # TODO
Purge | Remove all configurations and applications relating to the app/component # TODO

## Variables
Variable | Default Value | Description
---|---|---
HOMEPAGE_PUID | 10008 | TODO
HOMEPAGE_PGID | 10008 | TODO
HOMEPAGE_HTTP_PORT | 8094 | The http port that maps between the container and the host for the nginx reverse proxy
HOMEPAGE_PATH | '/mnt/homepage/' | Where the homepage app will live
HOMEPAGE_STORAGE_ZFS_POOL | 'apps_pool' | The ZFS pool name, so we can create the filesystem off it
HOMEPAGE_STORAGE_ZFS_FS | 'homepage' | The ZFS FS name we will create
HOMEPAGE_TIMEZONE | "America/New_York" | Timezone, for the docker-compose file
HOMEPAGE_PODMAN_SERVICE_ACCOUNT | 'srv_homepage' | TODO
HOMEPAGE_CONTAINER_VERSION | 'latest' | The version of the container we will pull
HOMEPAGE_FQDN | 'homepage.local' | The FQDN of the app, for the TLS cert and the nginx config. Make sure you have a DNS entry created for this. 
HOMEPAGE_SSL_CERT_PATH | Undefined | The path of the TLS cert we will use
HOMEPAGE_SSL_KEY_PATH | Undefined | The path of the TLS cert we will use
HOMEPAGE_CUSTOM_YAML_SETTINGS | | TODO define
HOMEPAGE_CUSTOM_YAML_BOOKMARKS | | TODO define
HOMEPAGE_CUSTOM_YAML_SERVICES | | TODO define 
HOMEPAGE_CUSTOM_YAML_KUBERNETES | | TODO define
HOMEPAGE_CUSTOM_YAML_DOCKER | | TODO define
HOMEPAGE_CUSTOM_YAML_WIDGETS | | TODO define

# TODO List
- Implement Remove tag
- Implement Purge tag
- Define OOTB settings for each of these:
  - HOMEPAGE_CUSTOM_YAML_SETTINGS:
  - HOMEPAGE_CUSTOM_YAML_BOOKMARKS:
  - HOMEPAGE_CUSTOM_YAML_SERVICES:
  - HOMEPAGE_CUSTOM_YAML_KUBERNETES:
  - HOMEPAGE_CUSTOM_YAML_DOCKER:
  - HOMEPAGE_CUSTOM_YAML_WIDGETS:
- Implement these variables:
  - HOMEPAGE_PUID
  - HOMEPAGE_PGID
  - HOMEPAGE_PODMAN_SERVICE_ACCOUNT
  - HOMEPAGE_TIMEZONE


