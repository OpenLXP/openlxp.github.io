## About

The Experience Schema Service ([XSS](https://github.com/OpenLXP/openlxp-xss)) component is responsible for managing pertinent object/record metadata schemas, and the mappings for transforming records from a source metadata schema to a target metadata schema. This component will also be used to store and link vocabularies from stored schema.

## Installation
1. Clone the Github repository:

   [GitHub-XSS](https://github.com/OpenLXP/openlxp-xss.git)

2. Open terminal at the root directory of the project.
    
    example: ~/PycharmProjects/openlxp-xss

3. Run command to install all the requirements from requirements.txt 
    
    docker-compose build .

4. Once the installation and build are done, run the below command to start the server.
    
    docker-compose up

5. Once the server is up, go to the admin page:
    
    http://localhost:8000/admin (replace localhost with server IP)

## Configuration
1. On the Admin page, log in with the admin credentials 


2. **Add Schema Ledger:** 
   
   *Registry for Maintaining and Managing Schemas*

   - `Schema Name` Schema file title
   - `Schema IRI` Schema files corresponding IRI
   - `Schema File` Upload the Schema file in the required format(JSON)
   - `Status` Select if the Schema is Published or Retired
   - `Major version` Add the Major value of the schema version
   - `Minor Version` Add the Minor value of the schema version
   - `Patch Version` Add the Patch version number of the schema
    
Note:  On uploading the schema file in the required format to the schema ledger the creation of corresponding term set, linked child term set and terms process is triggered.
   

3.  **Add Transformation Ledger:**
    
      *Registry for Maintaining and Managing the Mapping of Schemas*
      - `Source Schema` Select source term set file from drop-down
      - `Target Schema` Select Target term set from drop-down to be mapped to
      - `Schema Mapping File` Upload the Schema Mapping file to be referenced for mapping in the required format(JSON)
      - `Status` Select if the Schema Mapping is Published or Retired
    
Note:  On uploading the Schema Mapping File in the required format to the transformation ledger, this triggers the process of adding the mapping for the corresponding term values.
    
4. **Add Term set:**
    
    *Term sets supports the concept of a vocabulary in the context of semantic linking*
    - `Name` Term set title
    - `IRI` Term set's corresponding IRI
    - `Version` Add the version number
    - `Status` Select if the Term set is Published or Retired
    - `Updated by` User that creates/updates the term set
    - `Modified` Date & time when term set was created or modified
    
5. **Add Child Term set:**
    
    *Child term sets is a term set that contains a references to other term-sets (schemas)*
    - `Name` Term set title
    - `IRI` Term set's corresponding IRI
    - `Version` Add the version number
    - `Status` Select if the Term set is Published or Retired
    - `Parent term set` Select the reference to the parent term set from the drop down
    - `Updated by` User that creates/updates the term set
    - `Modified` Date & time when term set was created or modified
    
6. **Add Term:**
    
    *A term entity can be seen as a word in our dictionary. This entity captures a unique word/term in a term-set or schema.*
    - `Name` Term title
    - `IRI` Term corresponding IRI
    - `Desciption` Term entity's description
    - `Data Type` Term entity's corresponding data type
    - `Use` Term entity's corresponding use case
    - `Source` Term entity's corresponding source
    - `Version` Add the version number
    - `Status` Select if the Term set is Published or Retired
    - `term set` Select the reference to the parent term set from the drop down
    - `Mapping` Add mappings between terms entity's of different parent term set
    - `Updated by` User that creates/updates the term
    - `Modified` Date & time when term was created or modified
   
