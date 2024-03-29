## About
Experience Source Repositories are the primary data resources supporting the entire Enterprise Course Catalog solution.  Without the learning experience metadata extracted from the XSRs, the entire system would depend on Experience Owners and Experience Managers to enter all of the metadata manually.  This would introduce an additional workload on top of the work they are already performing to populate their own experience delivery systems and related catalog services. ECC can extract data via scheduled file drops, direct connection to the source database, upload data and connection to API endpoints. Source data can be in XML, JSON, and CSV file formats when being extracted into ECC.

In the case of the ECC project it is likely that we will see multiple system operators responsible for installation, configuration, and monitoring of various components of the system.  For example, the organization responsible for a particular Experience Source Repository (XSR) may also be the system operator for the corresponding Experience Index Agent (XIA) due to the organization's security/access policy with respect to their environment.
In the case of the ECC project the team initially expects that there will be a small number of Experience Owners for each Experience Source Repository (XSR), augmented with a number of Experience Managers who perform any necessary manual work required to maintain or enhance learning experience records.  However, these assumptions and even the owner/manager personas themselves are likely to change as the project progresses and more is learned about the actual people who will be interacting with the solution, their roles, and their scope of responsibilities.

## Installation
**Security, Networking, and Identity and Access Management**

The necessary firewall ports for ECC, based on the specified component/infrastructure.


**Deployment Scripts**

ECC is deployed and integrated using microservices approach for each component. Although some components rely on others for the data to be transformed and pushed into the global catalog system, each component can be deployed independently. This allows for flexible configuration modifications based on each organization’s requirements. The Experience Index Agent and Notification components are python packages available on PyPi. Eventually, XIA and XIS syndication will be implemented. Organizations will have the options to syndicate data into the deployed ECC application or from ECC into a local index service. ECC allows any component to be deployed individually and connect to/from the ADL deployed ECC.

**Integration: Deploying an Experience Index Agent to Contribute to the ADL ECC IOC**

Experience Index Agents are implemented using docker-compose. Experience Index Agents is configurable to allow any organizations to connect to their source repository. This is done by configurable API endpoints for the metadata within the XIA Django administration page. Whether the new organization exports CSV files or has API endpoints integrated with their source repository, new source repositories can be added to OpenLXP. Docker-compose.yaml file presented below is a generic representation of the ECC docker-compose file that can be customized where <XSR> can be updated based on source repository.

```terminal
version: "3"
 
services:
  db_xia_<XSR>:
    image: mysql:5.7
    ports:
      - '3306:3306'
    environment:
      MYSQL_DATABASE: "${DB_NAME}"
      MYSQL_PASSWORD: "${DB_PASSWORD}"
      MYSQL_ROOT_PASSWORD: "${DB_ROOT_PASSWORD}"
      MYSQL_HOST: ''
    networks:
      - openlxp
 
  app_xia_<XSR>:
    build:
      context: .
    ports:
      - "8000:8020"
    command: >
      sh -c ". /opt/app/start-app.sh"
    environment:
      DB_NAME: "${DB_NAME}"
      DB_USER: "${DB_USER}"
      DB_PASSWORD: "${DB_PASSWORD}"
      DB_HOST: "${DB_HOST}"
      DJANGO_SUPERUSER_USERNAME: "${DJANGO_SUPERUSER_USERNAME}"
      DJANGO_SUPERUSER_PASSWORD: "${DJANGO_SUPERUSER_PASSWORD}"
      DJANGO_SUPERUSER_EMAIL: "${DJANGO_SUPERUSER_EMAIL}"
      BUCKET_NAME: "${BUCKET_NAME}"
      AWS_ACCESS_KEY_ID: "${AWS_ACCESS_KEY_ID}"
      AWS_SECRET_ACCESS_KEY: "${AWS_SECRET_ACCESS_KEY}"
      AWS_DEFAULT_REGION: "${AWS_DEFAULT_REGION}"
      REQUESTS_CA_BUNDLE: '/etc/ssl/certs/ca-certificates.pem'
      AWS_CA_BUNDLE: '/etc/ssl/certs/ca-certificates.pem'
      SECRET_KEY_VAL: "${SECRET_KEY_VAL}"
      LOG_PATH: "${LOG_PATH}"
      CELERY_BROKER_URL: "${CELERY_BROKER_URL}"
      CELERY_RESULT_BACKEND: "${CELERY_RESULT_BACKEND}"
    volumes:
      - ./app:/opt/app/openlxp-xia-<XSR>
    depends_on:
      - db_xia_<XSR>
    networks:
      - openlxp
 
  redis:
    image: redis:alpine
    networks:
      - openlxp
 
  celery:
    build:
      context: .
    command: celery -A openlxp_xia_edx_project worker -l info --pool=solo
    volumes:
      - ./app:/opt/app/openlxp-xia-<XSR>
    environment:
      REQUESTS_CA_BUNDLE: '/etc/ssl/certs/ca-certificates.pem'
      AWS_CA_BUNDLE: '/etc/ssl/certs/ca-certificates.pem'
    env_file:
      - ./.env
    depends_on:
      - db_xia_<XSR>
      - redis
      - app_xia_<XSR>
    networks:
      - openlxp
    restart: on-failure
 
  celery-beat:
    build:
      context: .
    command: celery -A openlxp_xia_<XSR>_project beat --scheduler django_celery_beat.schedulers:DatabaseScheduler --loglevel=info --pidfile=/tmp/celerybeat.pid
    volumes:
      - ./app:/opt/app/openlxp-xia-<XSR>
    environment:
      REQUESTS_CA_BUNDLE: '/etc/ssl/certs/ca-certificates.pem'
      AWS_CA_BUNDLE: '/etc/ssl/certs/ca-certificates.pem'
    env_file:
      - ./.env
    depends_on:
      - db_xia_<XSR>
      - redis
      - app_xia_<XSR>
    networks:
      - openlxp
    restart: on-failure
 
  flower:
    image: mher/flower:0.9.7
    command: [ "flower", "--broker=redis://redis:6379/0", "--port=8888" ]
    ports:
      - 8888:8888
    networks:
      - openlxp
 
networks:
  openlxp:
    external: true
```

System Operators can use the current implementations of edX, JKO, DAU, and AETC Experience Index Agents by pulling the code from below repositories. Each of these implementations demonstrates a catalog contribution from a distributed system to the ADL’s EDLM ECC deployment.

* edX (https://github.com/OpenLXP/openlxp-xia-edx)
* JKO (https://github.com/OpenLXP/openlxp-xia-jko)
* DAU (https://github.com/OpenLXP/openlxp-xia-dau)
* AETC (https://github.com/OpenLXP/openlxp-xia-aetc)

**Integration: Deploying an Experience Index Service for Local Use of the Full ECC Solution**

The Experience Index Service is implemented using docker-compose. Clone the XIS Github repository and run ‘docker-compose up -d’. XIS component is developed to allow syndication with other XIS components. System Operators can run their own XIS if they choose to. Whether it is external to Platform One or internal, any organization can pull or push data into/from other XIS components.
* The Experience Search Engine is implemented using docker-compose.  Clone the Github repository and run ‘docker-compose up -d’. There are no additional configurations needed to set up XSE for OpenLXP. Once the Elasticsearch instances are running, indices are created based on configuration from the XIA component.
* The Experience Discovery Service is implemented using docker-compose.  Clone the Github repositories and run ‘docker-compose up -d’ to launch both XDS and XDS-UI. System Operators will configure the XDS component if there is a need to stand up their own discovery service UI.
* The Experience Management Service is implemented using docker-compose.  Use the docker-compose file below to launch both XMS and XMS-UI. System Operators will configure the XMS component if there is a need to stand up their own management service UI.
* Finally, the notifications implementation of the OpenLXP enables ECC users to receive notifications from the application. This component is also configurable through the Django administration page. Sender/receiver emails, notification body message, and attachment options can be configured.  This allows ECC users to be notified of any errors that occurred during the metadata ETL process. OpenLXP notifications is packaged in PyPi to allow installation during the container build of the XIA component. Below is the Github code repository for the notifications.

**Integration: Syndicating Indexed Experiences Across ECC Deployments**

OpenLXP XIA and XIS components are developed to plan for future syndication with local or external XIA or XIS services. ECC is developed to allow any organization to stand up an XIA agent and connect to the XIS. By utilizing API endpoints to connect to and from other XIA and XIS implementation, this allows data to be syndicated. Syndicating other various XIA/XIS components will continue to evolve and enhance the metadata for the course catalog. 
