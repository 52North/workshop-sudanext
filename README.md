# GeoNode Workshop SudeNext

Slides: https://docs.google.com/presentation/d/1EWMErdxzuQiQHv9GytObQFIuPZr9fziBsbOLiF0-HJg/

## Agenda

| Time | Topic |
|------|-------|
| 9:30 | Introduction Participants and expectations |
|      | Who are we @ 52°North GmbH|
| 10:00 | Introduction to <br/> - GeoNode and Remote Services <br/> - Running GeoNode Instances|
| 11:00 | Hands-On Installation <br/> - What will be installed? <br/> - Installation
| 12:00 | Uplaoding Data |
| 12:30 | Lunch Break |
| 13:00 | Hands-On GeoNode |
| 14:00 | Development Clients/Dashboards |
| 14:15 | Customizing and Extending GeoNode |
| 14:45 | Questions and Open Discussion |
| 15:?? | End of Workshop |


## Installation via geonode-project

The following instructions a the essence what you have to do when creating a GeoNode project from the [official geonode template](https://github.com/GeoNode/geonode-project). You can find an already initialized geonode project for this workshop under [the sudanext folder](sudanext). 
For the hands-on session leave it as is and try to create your own geonode project. 

Before you start, install some tool managing virtual environments (like `virtualenvwrapper`, `venv`, `pipenv`, ...). We are going to use [virtualenvwrapper](https://virtualenvwrapper.readthedocs.io/en/latest/).

Follow the instructions step by step in a dedicated working directory:

```sh
# do not copy blindly the whole snippet 
$ git clone https://github.com/GeoNode/geonode-project.git -b 4.x
$ source /usr/share/virtualenvwrapper/virtualenvwrapper.sh
$ mkvirtualenv --python=/usr/bin/python3 sudanext
$ # Prompt gets prefixed with the active environment
$ (sudanext) pip install Django==3.2.16
$ (sudanext) django-admin startproject --template=./geonode-project -e py,sh,md,rst,json,yml,ini,env,sample,properties -n monitoring-cron -n Dockerfile sudanext
```

You should find a `sudanext` directory containing your prepared GeoNode project. Now, go into that directory and run `python create-envfile.py`.

**Note:** Here and there, users report about authentication issues between GeoNode and GeoServer. Maybe the geonode-project has some flaws (not found out, yet).

To build the project, run docker compose:

```sh
# the build will take quite a while
docker compose build .
# start geonode detached
docker compose up -d
# once running you can follow the logs
docker compose logs -f
```

## Useful Docker Commands

Stop all containers of the `sudanext` setup:

```sh
# either via docker compose
docker compose down
# or directly via docker
docker stop $(docker ps -a --filter name=sudanext --format={{.Names}})
```

Remove all volumes of the `sudanext` setup:

```sh
docker volume rm $(docker volume ls --filter="name=sudanext" --format={{.Name}})
```


## Helpful Links

* [GeoNode Documentation](https://readthedocs.org/projects/geonode-documentation/)
  * [Docker Installation Guide](https://docs.geonode.org/en/4.x/install/basic/index.html)
  * [Advanced Installation](https://docs.geonode.org/en/4.x/install/advanced/index.html) 
  * [Configuration Options](https://docs.geonode.org/en/4.x/basic/settings/index.html#settings)
* Opengeospatial Consortium (OGC)
  * [OGC Standards](https://www.ogc.org/docs/is)
  * [Standards Roadmap](https://www.ogc.org/roadmap)
* Important Open Standards
  * Catalogue (implemented by [pycsw](https://docs.pycsw.org/))
    * OGC CSW (2007: 2.0.2, 2016: 3.x)
    * [Implemented Features](https://docs.pycsw.org/en/2.6.1/introduction.html#standards-support)
    * [OGC API for Records](https://ogcapi.ogc.org/records/) (Successor for OGC CSW)
    * [STAC](https://docs.pycsw.org/en/latest/stac.html)
  * Remote Services
    * OGC APIs
    * [OGC WMS](https://www.ogc.org/standards/wms)/[OGC WMTS](https://www.ogc.org/standards/wmts)
    * [OGC WFS](https://www.ogc.org/standards/wfs)
    * [OGC WCS](https://www.ogc.org/standards/wcs)
    * OGC SensorThings API
  * Data Encoding
    * ISO TC211 and OGC ([ISO 191xx series](https://en.wikipedia.org/wiki/List_of_International_Organization_for_Standardization_standards,_18000-19999#ISO_19000_%E2%80%93_ISO_19999))
    * OGC SensorML
    * OGC SweCommon
    * OGC GML