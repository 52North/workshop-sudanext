# GeoNode Workshop SudaNext

Slides: https://docs.google.com/presentation/d/1aGJ2nvTk7fVlGOVQva4LpW1nL3w3qIOhXNxLpXBvsRo/edit

## Agenda

**Start:** 9:00 am

| Topic |
|------|
| Introduction Participants and expectations <br/> Who are we @ 52°North GmbH |
| Introduction to <br/> - GeoNode and Remote Services <br/> - Running GeoNode Instances |
| Hands-On Installation <br/> - What will be installed? <br/> - Installation |
| Uploading Data |
| Lunch Break |
| Hands-On GeoNode |
| Development Clients/Dashboards |
| Customizing and Extending GeoNode |
| Questions and Open Discussion |
| End of Workshop |


## Installation of geonode

The following instructions describe how to run GeoNode.
Checkout GeoNode:

```sh
git clone https://github.com/geonode/geonode
```

Optional: Open `.env` file and set `COMPOSE_PROJECT_NAME=sudanext` which will create containers with labels containing `sudanext`.

You can either start GeoNode (and its accompanying services) via docker-compose or as `devcontainer` from VS-Code.
The simplest approach would be to run:

```sh
# the build will take quite a while
docker compose build .
# start geonode detached
docker compose up -d
# once running you can follow the logs
docker compose logs -f
```

After build and startup completes you can access 

* GeoNode from http://localhost
* GeoServer from http://localhost/geoserver


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
