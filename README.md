# emergence: a graph database for governance, risk, & compliance
![emergence](https://github.com/user-attachments/assets/c274fcd2-af2b-4b21-913b-991c9fe4c63b)

emergence is an open-source graph database model for use in governance, risk, & compliance (GRC). <br/>
<br/>
The graph database model outlines a schema for representing the itnerconnected pieces of a an organization's GRC program into objects (nodes) and relationships (edges).

**Emergence Core** <br/>
emergence core is the foundational graph model and can be extended with out-of-the-box or custom model extensions. <br/>
emergence core supports the following graph objects: <br/>
Object  | Labels
------------- | -------------
Policy Statement  | policy name, verbiage, approved by, approved date, date added, statement id 
Control  | id, name, description, type, implementation status
Requirement | id, name, description, authority document, authority, type

**Extending emergence core** <br/>
emergence can be extended with either out-of-the-box (coming soon) or custom extensions. <br/>
<br/>
Because emergence is a graph model, extending the model is as simple as adding new object types and defining the relationships it has to the rest of the model. <br/>
<br/>
You can use something as simple as mind-map style whiteboarding to define and integrate new data types into the model. <br/>
<br/>
It is recommended to keep objects data-source agnostic and use a data normalizer to map data sources to appropriate objects, relationships, and labels. <br/>
<br/>
For example, instead of creating a node for active directory users, create a user object that can be mapped to from AD, AAD, Okta, etc. <br/>
<br/>
**Why a graph database?** <br/>
<br/>
emergence is a graph database for a few reasons: <br/>
* easily extended through whiteboarding / mind-mapping
* allows unique graph analytics such as path analysis
* accurately represents the interconnected objects that make up a GRC program
