## About

Experience Index Agents (XIAs) interact with specific Experience Source Repositories (XSRs) to extract, transform, and load operations for learning experience metadata.  Each XSR will have their own XIA, as XSRs have their own unique data schemas and APIs for retrieving metadata.  The common components of the XIA workflow are consolidated within an XIA package which can be found on [PyPI](https://pypi.org/project/openlxp-xia/) or [GitHub](https://github.com/OpenLXP/openlxp-xia).  The XIA workflow is E-V-T-V-L (Extract-Validate-Transform-Validate-Load).  Within the workflow, Extract is the only component that is unique between the XIAs.  The V-T-V-L steps can be performed by the XIA package if given the relevant schemas.

1. `Extract`: Extracts learning experience metadata from the Experience Source Repository (XSR).

2. `Validate`: Compares extracted learning experience metadata against the configured source metadata reference schema stored in the Experience Schema Service (XSS).

3. `Transform`: Transforms extracted+validated source learning experience metadata to the configured target schema using the "XSR-to-Target" transformation map stored in the Experience Schema Service (XSS)

4. `Validate`: Compares transformed learning experience metadata against the configured target metadata reference schema stored in the Experience Schema Service (XSS).

5. `Load`: Pushes transformed and validated learning experience metadata to the target Experience Index Service (XIS) for further processing.

## Installation

To install the XIA package to your XIA.

    $ python -m pip install OpenLXP-XIA (use the latest package version)

Add OpenLXP-XIA in the setting.py in your project.

INSTALLED_APPS = [
        ...
        
        'openlxp_xia',
        
        ....
]

## Configuration

1. On the Admin page, log in with the admin credentials 

2. `Add xis configuration`: Configure Experience Index Services (XIS): 

    `Xis metadata api endpoint`: API endpoint for XIS where metadata will get stored.

     Example:  
    `Xis metadata api endpoint`: http://localhost:8080/api/metadata/

    `Xis supplemental api endpoint`: API endpoint for XIS where supplemental metadata will get stored.

    Example: 

    `Xis supplemental api endpoint`: http://openlxp-xis:8020/api/supplemental-data/

    (Note: Replace localhost with the XIS Host)


3.  `Add xia configuration`: Configure Experience Index Agents(XIA):

    `Publisher`: Agent Name
    
    `Xss api`: the API of the Experience Schema Server (XSS) to use for retrieving schemas
    
    `Source metadata schema`: Schema name or IRI for source schema validation
    
    `Target metadata schema`: Schema name or IRI for target metadata validation

    (Note: Please make sure to upload schema files in the Experience Schema Server (XSS) and create a mapping between them)


4. `Add metadata field overwrite`: Here, we can add new fields and their values or overwrite values for existing fields.

    `Field name`: Add new or existing field Name
    
    `Field type`: Add date type of the field
    
    `Field value`: Add corresponding value
    
    `Overwrite`: Check the box if existing values need to be overwritten.

## Running ETL Pipeline

ETL or E-V-T-V-L (Extract-Transform-Load) Pipeline can be run through two ways:

1. Through API Endpoint:
To run ETL tasks run below API:
    
    http://localhost:8000/api/xia-workflow
(Note: Change localhost with XIA host)

2. Periodically through celery beat: 

    On the admin page add periodic task and a schedule. On the selected time interval the celery task will be run automatically.
