## About 

The Experience Discovery Service (XDS) is split into 2 parts; the backend APIs (known as XDS Backend), and the User Interface (known as XDS UI).  XDS allows users to search for experiences, collect and share them in Interest Lists, allows admins to highlight specific experiences, and specify what metadata about an experience to display.  

## [XDS Backend](https://github.com/OpenLXP/openlxp-xds)
### Installation


[VIDEO TUTORIAL: Configuring Python for OpenLXP Discovery Service Backend](videos/186240161-ae51a16b-4d91-4609-a239-06782354a4cf.mp4)
<video controls src="videos/186240161-ae51a16b-4d91-4609-a239-06782354a4cf.mp4" title="VIDEO TUTORIAL: Configuring Python for OpenLXP Discovery Service Backend"></video>

1. Clone the Github repository:

    https://github.com/OpenLXP/openlxp-xds.git

2. Open terminal at the root directory of the project.
    
    example: ~/PycharmProjects/openlxp-xds 

3. Run command to install all the requirements from requirements.txt 
    
    docker-compose build .

4. Once the installation and build are done, run the below command to start the server.
    
    docker-compose up

5. Once the server is up, go to the admin page:
    
    http://localhost:8100/admin (replace localhost with server IP)


### Configuration

1. On the Admin page, log in with the admin credentials 


2. `Add xds configuration`: Configure Experience Discovery Service (XDS):
    
    `Default user group`: Select a group for new users to be assigned to automatically.

    `Target xis metadata api`: Metadata API Endpoint to connect to on an XIS instance.

    `Target xse host`: Hostname and port of XSE instance to use.

    `Target xse index`: Index of data to use on XSE instance.


3. `Add xdsui configuration`: Configure Experience Discovery Service - User Interface (XDS-UI): 

    `Search results per page`: Number of results that should be displayed on a search page on the UI.

    `Xds configuration`: Select the XDS Configuration to use.

    `Course img fallback`: Image to use if no image is supplied in the experience


4. `Add Course information mappings`: Configure Course Information Mapping:
    
    `Course title`: The mapping of the field to use as a title within XSE.

    `Course description`: The mapping of the field to use as a description within XSE.

    `Course url`: The mapping of the field to use as a URL within XSE.

    `Course code`: The mapping of the field to use as a code within XSE.

    `Course startDate`: The mapping of the field to use as a start date within XSE.

    `Course endDate`: The mapping of the field to use as an end date within XSE.

    `Course provider`: The mapping of the field to use as a provider within XSE.

    `Course instructor`: The mapping of the field to use as an instructor within XSE.

    `Course deliveryMode`: The mapping of the field to use as a delivery mode within XSE.

    `Course thumbnail`: The mapping of the field to retrieve a thumbnail from within XSE.


5. `Add course spotlight`: Configure Spotlight Courses in XDS-UI:

    `Course id`: The ID of the course to add.

    `Active`: Whether this course should be shown in the Spotlight Courses section.


6. `Add search filter`: Configure Search Filters in XDS-UI:

    `Display name`: The name to use to label the filter in the UI.

    `Field name`: The name of the field in ElasticSearch.

    `Xds ui configuration`: Select the XDS UI Configuration to use.

    `Filter type`: The type of filter to use.

    `Active`: Whether this filter should be shown in the search results page.


7.  Additional configuration settings for XDS and subcomponents (such as Authentication or Notifications) can be found on in the XDS Backend GitHub repository.

## [XDS UI](https://github.com/OpenLXP/openlxp-xds-ui)
### Installation

1. Clone the project

    ```terminal
    git clone git clone git@github.com:OpenLXP/openlxp-xds-ui.git
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
    yarn
    ```

4. Run the project

    > Run the project in development mode

    ```terminal
    yarn dev
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

All configuration settings for XDS UI can be edited within an `.env` file

The `.env` file can be found in the root directory of the project folder

> Example `.env` file

```js
// api gateway
NEXT_PUBLIC_BACKEND_HOST=
NEXT_PUBLIC_XAPI_LRS_ENDPOINT=
NEXT_PUBLIC_XAPI_LRS_KEY=
NEXT_PUBLIC_XAPI_LRS_SECRET=
```

**NEXT_PUBLIC_BACKEND_HOST**: The url for the XDS component

> Note: the lrs component is not required for the UI to function.

**NEXT_PUBLIC_XAPI_LRS_ENDPOINT**: The url for the LRS component

**NEXT_PUBLIC_XAPI_LRS_KEY**: The key for the LRS component

**NEXT_PUBLIC_XAPI_LRS_SECRET**: The secret for the LRS component