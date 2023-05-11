<img
  src="https://github.com/apache/superset/raw/master/superset-frontend/src/assets/branding/superset-logo-horiz-apache.png"
  alt="Superset"
  width="300"
/>

## Aegus Analytics customised version of Superset

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/apache/superset?sort=semver)](https://github.com/apache/superset/tree/latest)
[![PyPI version](https://badge.fury.io/py/apache-superset.svg)](https://badge.fury.io/py/apache-superset)
[![PyPI](https://img.shields.io/pypi/pyversions/apache-superset.svg?maxAge=2592000)](https://pypi.python.org/pypi/apache-superset)
[![Documentation](https://img.shields.io/badge/docs-apache.org-blue.svg)](https://superset.apache.org)



---
##### How to Install
- Install Docker on Ubuntu

` https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository`

- Install Docker Compose on Ubuntu

`https://docs.docker.com/compose/install/standalone/#on-linux`


- Clone the repository using

`git clone https://github.com/stevensuting/Aegus-Analytics.git`

---

##### Running superset in Production mode
- Navigate to the superset directory

` cd Aegus-Analytics`

- Load the yaml file which has all the production configurations to run in the background

`sudo docker-compose -f docker-compose-non-dev.yml pull`

- Then start all production containers for superset to run in the background

`sudo docker-compose -f docker-compose-non-dev.yml up -d`

- You should see this
```
[+] Running 6/6
 ✔ Container superset_db           Started    0.6s 
 ✔ Container superset_cache        Started    0.6s 
 ✔ Container superset_app          Started    1.8s 
 ✔ Container superset_worker       Started    1.7s 
 ✔ Container superset_worker_beat  Started    1.8s 
 ✔ Container superset_init         Started    1.8s 
```
- To see the status of the containers run this

`sudo docker ps`

```
CONTAINER ID   IMAGE                           CREATED         STATUS                   PORTS                                       NAMES
e0b93602c484   apache/superset:latest-dev      8 minutes ago   Up 8 minutes             8088/tcp                                    superset_worker
97ca0fd45c06   apache/superset:latest-dev      8 minutes ago   Up 8 minutes             8088/tcp                                    superset_worker_beat
81be1f0f7ec5   apache/superset:latest-dev      8 minutes ago   Up 8 minutes             0.0.0.0:8088->8088/tcp                      superset_app
c1c6e5a2ccef   redis:7                         8 minutes ago   Up 8 minutes             6379/tcp                                    superset_cache
66a0cdf2c415   postgres:14                     8 minutes ago   Up 8 minutes             5432/tcp                                    superset_db
```


- Superset will be available on 
```
http://host-ip-address:8088
username: admin
password: admin
```

---


##### How to change logo
- Place the logo in this location

`Aegus-Analytics`


- Then update the logo name in the following file

`Aegus-Analytics/docker/pythonpath_dev/superset_config_docker.py`

in this location

`APP_ICON = "/static/assets/images/aegus-logo.png"`

- Now navigate to  `cd Aegus-Analytics` and then copy the image to the docker container using:
`docker cp aegus-logo.png superset_app:/app/superset/static/assets/images/aegus-logo.png`


##### How to modify color palette

- Open this file

`Aegus-Analytics/docker/pythonpath_dev/superset_config_docker.py`

And look for this block of code, replace the hex codes, with colors of choice.

```
EXTRA_CATEGORICAL_COLOR_SCHEMES = [
    {
        "id": 'aegus-custom-colors',
        "description": '',
        "label": 'Aegus',
        "isDefault": True,
        "colors":
         ['#006699', '#009DD9', '#5AAA46', '#44AAAA', '#DDAA77', '#7799BB', '#88AA77',
         '#552288', '#5AAA46', '#CC7788', '#EEDD55', '#9977BB', '#BBAA44', '#DDCCDD']
    }]
```


##### _Note_
These changes for customization can either be done at a repo level or after the installation. If it is done after the installation, then you would need to the restart the container for the changes to take effect.
Command to restart the container is:

`sudo docker restart superset_app`


