# Components
 1. Experience Source Repository (XSR)

 2. [Experience Schema Service (XSS)](https://github.com/OpenLXP/openlxp-xss)

 3. [Experience Index Agent (XIA)](https://github.com/OpenLXP/openlxp-xia-sample)
 4. [Experience Index Service (XIS)](https://github.com/OpenLXP/openlxp-xis)
 5. [Experience Search Engine (XSE)](https://github.com/OpenLXP/openlxp-xse)

6. Experience Management Service (XMS)
    
    [Experience Management Service (XMS)](https://github.com/OpenLXP/openlxp-xms)
    
    [Experience Management Service UI (XMS UI)](https://github.com/OpenLXP/openlxp-xms-ui)
 7. Experience Discovery Service (XDS)

    [Experience Discovery Service (XDS)](https://github.com/OpenLXP/openlxp-xds)

    [Experience Discovery Service UI (XDS UI)](https://github.com/OpenLXP/openlxp-xds-ui)

# Personas
* System Operator: The person(s) responsible for installing, configuring, validating, hardening, and monitoring the system. We expect System Operators to be responsible for the provisioning, configuration, and management of a given system.  Simple or contained installations may have a single dedicated system operator, whereas complex and/or distributed systems with components deployed at various locations often will feature multiple system operators.
* Experience Owner: The person(s) responsible for ensuring that each learning experience record is valid and available from each source repository.  Can potentially be the same person as the Experience Manager. Experience Owners are responsible for the production of the aggregated learning experiences indexed by the ECC system.  Experience Owners may be responsible for a single experience, and they may be responsible for hundreds or even thousands of learning experiences.  An Experience Owner is essentially the primary representative for a particular publishing organization within the ECC system.  Experience Owners have the ability to define an Experience Manager in order to distribute the management burden of the learning experiences for which they are responsible.  Experience Owners serve as the main point of contact for all of the learning experience records located within their purview, although they are not necessarily the point of contact for an interested Experience Participant.
* Experience Manager: The person(s) responsible for modifying learning experience records and/or augmenting them with supplemental information within the system. Experience Managers are responsible for post-collection modification and augmentation of aggregated learning experiences indexed by the ECC system. They may be responsible for hundreds or even thousands of learning experiences.  Experience Managers are appointed by an Experience Owner in order to distribute the management burden of the learning experiences for which the Experience Owner is responsible.  Experience Managers may serve as a point of contact for assigned learning experience records, although they are not necessarily the point of contact for registration or delivery of the experience itself.
* Experience Facilitator: The person(s) responsible for shepherding, stewarding, mentoring, instructing, and/or teaching an Experience Consumer as they work through a learning experience. An Experience Facilitator is responsible for advising, guiding, and/or evaluating the performance of an Experience Consumer as they work their way through the activity set for a given learning experience.  Experience Facilitators may be instructors, trainers, supervisors, coaches, mentors, assessors, or potentially even another Experience Consumer familiar with the required material and/or tasks.
* Experience Consumer: The person(s) responsible for discovering, accessing, and taking part in the available learning experiences presented by the system. An Experience Consumer is the beneficiary of the new knowledge and/or skills gained by working through the activity set of a particular learning experience.  Experience Consumers may receive support from an Experience Facilitator in the form of advice, guidance, and/or evaluation as they work through a learning experience. 
Experience Consumers represent a wide range of people and roles within an organization, and may also have other assigned responsibilities with respect to the ECC system.  For example, an Experience Consumer may also function as an Experience Facilitator, Experience Manager, and/or an Experience Owner for one or more learning experiences indexed by the ECC system.  However, it is not likely that the consumer of any given experience would also serve as an Experience Facilitator, Experience Manager, and/or an Experience Owner for that particular learning experience due to a conflict of interest.


# Workflow
The ECC team has identified the following high-level workflows based on the initial analysis of the ADL's system requirements.  Additional high-level workflows are likely to be identified as additional interviews and observations are conducted.
* System Installation: Automated and manual operations required to download, extract, and deploy the system components comprising the ECC solution.
* System Configuration: Automated and manual operations required to enable each system component and persona to interact with other system components and personas.
* System Validation: ECC Includes System Management, Monitoring, and Administration. The ECC intends to leverage known/recognized technologies (e.g., Elasticsearch, MySQL, Nginx) which are best of breed solutions that are known to scale and perform well at a high-level. ADL has provided defined service level targets (e.g., search indexing time), which we will use as design constraints to demonstrate performance.
* System Interoperability: ECC Business Continuity/Disaster Recovery and Continuity of Operations. Beyond the capacity, performance, and availability/reliability attributes described above, the development teal will work within the existing guidelines and practices defined by ADL and in use in the maintaining the ADL’s TLA Sandbox environment.
* System Monitoring: Automated and manual operations required to enable observation of system activity and resource consumption Cloud tech to scale.
* Experience Indexing: Automated and manual operations required to collect, process, and store learning experience records in preparation for discovery.
* Experience Management: Automated and manual operations required to modify and/or augment learning experience records to improve the discovery experience.
* Experience Discovery: Automated and manual operations required to efficiently locate learning experience records with the highest possible level of accuracy and efficacy.
* Experience Access: Automated and manual operations required to direct a persona to the optimal location for additional information and/or registration regarding the selected learning experience record.
* Experience Reporting: Automated and manual operations required to gain insights into persona activity and learning record consumption.