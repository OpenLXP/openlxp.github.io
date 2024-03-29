## About 
The Experience Management Service (XMS) provides interface facilitating modification and augmentation of records by learning experience owners and managers. This component is split into 2 parts; XMS Backend, which supplies APIs necessary to edit the metadata, and XMS UI, which provides a UI to simplify the process.  


## [XMS Backend](https://github.com/OpenLXP/openlxp-xms#readme)

### Installation
1. Clone the Github repository:

    https://github.com/OpenLXP/openlxp-xms.git

2. Open terminal at the root directory of the project.
    
    example: ~/PycharmProjects/openlxp-xms 

3. Run command to install all the requirements from requirements.txt 
    
    docker-compose build.

4. Once the installation and build are done, run the below command to start the server.
    
    docker-compose up

5. Once the server is up, go to the admin page:
    
    http://localhost:8000/admin (replace localhost with server IP)

### Configuration
1. On the Admin page, log in with the admin credentials 

2. `Add xms configuration`: Configure Experience Management Service (XMS):

    `Target xis metadata api`: Metadata API Endpoint to connect to on an XIS instance.

    `XIS catalogs api`: Catalogs API Endpoint to connect to on an XIS instance.

3. `Add Saml configuration`: Configure Security Assertion Markup Language (SAML):
    
    `Name`: The name that will be used to identify the IdP in the URL.

    `Entity id`: The unique name provided by the IdP.

    `Url`: The connection URL to connect to the IdP at.

    `Cert`: The public cert used to connect to the IdP.

    `Attribute mapping`: The JSON formatted mapping to convert attributes provided by the IdP, to a User in this system.

4. `Add sender email configuration`: Configure the sender email address from which conformance alerts are sent.

5. `Add receiver email configuration` : 
Add an email list to send conformance alerts. When the email gets added, an email verification email will get sent out. In addition, conformance alerts will get sent to only verified email IDs.


## [XMS UI](https://github.com/OpenLXP/openlxp-xms-ui#readme)

### Installation

1. Clone the project

    ```terminal
    git clone git@github.com:OpenLXP/openlxp-xms-ui.git
    ```

2. Install yarn

    This project uses yarn as the package manager. If you already have yarn installed or are using a different package manager feel free to skip this step.

    > Start by installing yarn globally

    ```terminal
    npm install -g yarn
    ```

    > Verify yarn was installed

    ```terminal
    yarn -version
    ```

3. Install project dependencies

    > Installs all requirements for development

    ```terminal
    yarn set version 1.22.1
    ```
    ```bash
    yarn install package.json
    ```

4. Run the project

    > Run the project in development mode

    ```terminal
    yarn start
    ```

5. Run the project in production mode

    > Build the docker image

    ```terminal
    docker build -t openlxp-xds-ui .
    ```

    > Run the docker image

    ```terminal
    docker run -p 3000:3000 openlxp-xds-ui
    ```

### Configuration
This project makes use of globally available environment variables. Below are the required environment variables required for this project.

**REACT_APP_XIS_CATALOGS_API**

This is the root API endpoint used by the application to access XIS catalogs.

```yaml
http://<YOUR_BACKEND_ENDPOINT>/api/catalogs/
```

**REACT_APP_XIS_COMPOSITELEDGER_API**

This is the endpoint for accessing the XIS compositeledger.

```yaml
http://<YOUR_BACKEND_ENDPOINT>/es-api/
```

**REACT_APP_XIS_EXPERIENCES_API**

This is the root API endpoint used by the application to access XIS experiences. 

```yaml
http://<YOUR_BACKEND_ENDPOINT>/api/experiences/
```


**.env Template**

```text
REACT_APP_XIS_CATALOGS_API=<YOUR_BACKEND_ENDPOINT>/api/catalogs/
REACT_APP_XIS_COMPOSITELEDGER_API=<YOUR_BACKEND_ENDPOINT>/api/metadata/
REACT_APP_XIS_EXPERIENCES_API=<YOUR_BACKEND_ENDPOINT>/api/experiences/
```