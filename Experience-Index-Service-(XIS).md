## About

The Experience Index Service (XIS) Component is the primary funnel for learning experience metadata collected by the Experience Index Agent (XIA) components. In addition, the XIS can receive supplemental learning experience metadata – field name/value overrides and augmentations – from the Experience Management Service (XMS).  

Learning experience metadata received from XIAs is stored in the Metadata Loading Area and processed asynchronously to enhance overall system performance and scalability. Processed metadata combined with supplemental metadata provided by an Experience Owner or Experience Manager and the "composite record" stored in the Metadata Repository. Metadata Repository records addition/modification events logged to a job queue, and the metadata is then sent to the Experience Search Engine (XSE) for indexing and high-performance location/retrieval. 

A XIS can syndicate its composite records to another XIS. One or more facets/dimensions can filter the record-set to transmit a subset of the overall composite record repository. In addition, the transmitted fieldset can be configured to redacted values for specified fields when information is considered too sensitive for syndication. 

## Installation

1. Clone the Github repository:

   [GitHub-XIS](https://github.com/OpenLXP/openlxp-xis.git)

2. Open terminal at the root directory of the project.
    
    example: ~/PycharmProjects/openlxp-xis

3. Run command to install all the requirements from requirements.txt 
    
    docker-compose build.

4. Once the installation and build are done, run the below command to start the server.
    
    docker-compose up

5. Once the server is up, go to the admin page:
    
    http://localhost:8080/admin (replace localhost with server IP)


## Configuration

1. On the Admin page, log in with the admin credentials 


2.  `Add xis configuration`: Configure Experience Index Service(XIS):

    `Xss host`: Host and path for the Experience Schema Service and schema api

    `Target schema`: Schema name or IRI for target validation schema from XSS
    
    `Xse host`: Host for the Experience Search Engine
    
    `Xse index`: Index Name for the Experience Search Engine

    `Autocomplete field`: Path to the field to use for autocomplete in XSE

    `Filter field`: Path to the field to use for filtering in XSE
    
    **Note: Please make sure to upload schema file in the Experience Schema Server (XSS).**


3.  `Add xis upstream`: Configure Upstream XIS Syndication:

    `Xis api endpoint`: The api of the XIS Instance to retrieve data from

    `Xis api endpoint status`: Whether to connect to this XIS Instance for syndication


4.  `Add filter record`: Configure Record Filter for XIS Downstream Syndication:

    `Field name`: The path to the field to check

    `Comparator`: The type of comparison to make (equal, not equal, contains)

    `Field value`: The value to check the field for


5.  `Add filter metadata`: Configure Metadata Filter for XIS Downstream Syndication:

    `Field name`: The path to the field

    `Operation`: Whether to include or exclude the selected field


6.  `Add xis downstream`: Configure XIS Downstream Syndication:

    `Xis api endpoint`: The api of the XIS Instance to retrieve data from

    `Xis api endpoint status`: Whether to connect to this XIS Instance for syndication

    `Filter records`: The filter record objects to use when filtering records to send to this XIS

    `Filter metadata`: The filter metadata objects to use when filtering metadata to send to this XIS


## Running Tasks
XIS has 3 workflows that can be run.  Consolidation and loading of Metadata and Supplemental Metadata into Compositing Ledger then loading it into XSE.  XIS Upstream Syndication.  And XIS Downstream Syndication.  They can each be triggered 2 ways:

1. Through API Endpoints:
    For consolidating records to the Composite Ledger and loading it into XSE:
    
    http://localhost:8080/api/xis-workflow

    For Upstream Syndication:

    http://localhost:8080/api/upstream-workflow

    For Downstream Syndication:

    http://localhost:8080/api/downstream-workflow
        
    **Note: Change localhost with XIS host**

2. Periodically through celery beat: 

    On the admin page add periodic task and a schedule. Select the workflow to run from the Task (registered) dropdown list.  On the selected time interval celery task will run the task.
