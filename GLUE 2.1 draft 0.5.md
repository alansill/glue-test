<!----- Conversion time: 149.76 seconds.


Using this Markdown file:

1. Cut and paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* GD2md-html version 1.0β12
* Fri Jun 01 2018 08:48:58 GMT-0700 (PDT)
* Source doc: https://docs.google.com/a/nsfcac.org/open?id=1BpeTBQfCn8xRo4Ff38esRhBwzoUHE4bVxba2rEAzI-U
* This document has images: check for >>>>>  gd2md-html alert:  inline image link in generated source and store images to your server.
----->


<p style="color: red; font-weight: bold">>>>>>  gd2md-html alert:  ERRORs: 0; WARNINGs: 0; ALERTS: 5.</p>
<ul style="color: red; font-weight: bold"><li>See top comment block for details on ERRORs and WARNINGs. <li>In the converted Markdown or HTML, search for inline alerts that start with >>>>>  gd2md-html alert:  for specific instances that need correction.</ul>

<p style="color: red; font-weight: bold">Links to alert messages:</p><a href="#gdcalert1">alert1</a>
<a href="#gdcalert2">alert2</a>
<a href="#gdcalert3">alert3</a>
<a href="#gdcalert4">alert4</a>
<a href="#gdcalert5">alert5</a>

<p style="color: red; font-weight: bold">>>>>> PLEASE check and correct alert issues and delete this message and the inline alerts.<hr></p>


**GLUE Specification v 2.1-DRAFT**

<span style="text-decoration:underline;">Status of This Document</span>

This document provides information to the Grid community regarding the specification of the GLUE information model. Distribution is unlimited.

<span style="text-decoration:underline;">Copyright Notice</span>

Copyright © Open Grid Forum (2009).  All Rights Reserved.

<span style="text-decoration:underline;">Trademark</span>

Open Grid Services Architecture and OGSA are trademarks of the Open Grid Forum.

<span style="text-decoration:underline;">Abstract</span>

The GLUE specification is an information model for Grid entities described using the natural language and UML Class Diagrams. As a conceptual model, it is designed to be independent from the concrete data models adopted for its implementation. This document extend the GLUE 2.0 model to include Cloud resources and services. Rendering to concrete data models such XML Schema, LDAP Schema and SQL are provided in a separate document. 

<span style="text-decoration:underline;">Contents</span>


[TOC]






1.  **Introduction**

In this document, we present a conceptual information model for Grid and Cloud entities described using natural language and enriched with a graphical representation using UML Class Diagrams. As a conceptual model, it is designed to be independent from the concrete data models adopted for its implementation. Rendering to concrete data models such XML Schema, LDAP Schema, JSON schema and SQL are provided in a separate document. From the semantic viewpoint, the concrete data models SHOULD represent the same concepts and relationships of the conceptual information model; nevertheless they MAY contain simplifications targeted at improving query performance or other aspects of interest.

This information model is based on the experience of several modeling approaches being used in current production Grid infrastructures (e.g., GLUE Schema 1.x [GLUE-1.X], GLUE Schema 2.0 [GLUE-2.0], NorduGrid schema [NG-SCHEMA], Naregi model [NAREGI-SCHEMA]). The main supporting use cases are collected in the use cases document [GLUE-USECASES]. 

The mapping to concrete data models will be published in separate documents. Profile documents SHOULD appear to define how to generate and use the information in production scenarios or how to integrate the GLUE specification along with clarifications, refinements, interpretations and amplifications to promote interoperability (e.g., a profile MAY decide that an attribute which is optional in the conceptual model, is considered mandatory in a certain Grid infrastructure; or that optional attributes are never published). 



1.  **Change-log**

The following table provides a list of changes from the past GLUE editions


<table>
  <tr>
   <td><strong>Release</strong>
   </td>
   <td><strong>Change description</strong>
   </td>
  </tr>
  <tr>
   <td>1.0
   </td>
   <td><strong>Initial release</strong>
   </td>
  </tr>
  <tr>
   <td>2.0
   </td>
   <td><strong>Major re-design to  other information models</strong>
   </td>
  </tr>
  <tr>
   <td>2.1
   </td>
   <td><strong>Addition of Cloud Computing objects</strong>
   </td>
  </tr>
</table>




1.  **Notational Conventions**

The key words "MUST", "MUST NOT," "REQUIRED," "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY",  and "OPTIONAL" are to be interpreted as described in RFC 2119 (see http://www.ietf.org/rfc/rfc2119.txt). All class names are written using `this font`.



1.  **General Statements**

The Information Model and its renderings MUST treat strings, both entity and attribute names and their values, as being case-sensitive. Each GLUE entity MUST have an ID attribute (an exception is made for the `Extension` class) which is needed for identification or for access to the attributes of the related entity over time and across different information sources. As a general guideline, ID's SHOULD be persistent at least for a day when assigned to an entity. The ID MUST NOT be interpreted by the user or the system as having any meaning other than an identifier. In particular, there is no relationship between an ID and a network endpoint. Every ID MUST be a valid URI. The usage of URN (Uniform Resource Name, a subset of Uniform Resource Identifier or URI) is RECOMMENDED. The motivations for choosing URI's reside in the fact that Grid services are evolving towards Web-based technologies, therefore it is meaningful to adopt the same identification system.

As regards units of measure, multiples of bytes MUST refer to the SI (_Le **S**ystème **I**nternational d'Unités_) prefix (http://en.wikipedia.org/wiki/SI_prefix), therefore GB is 10<sup>9</sup> Bytes and not 2<sup>30</sup> Bytes (the latter are GibiBytes).

In Appendix A, we provide guidelines for place-holder values that MUST be used when the attributes have no good default value or when the attribute cannot be measured for some reason.

 

As regards extensibility, two main approaches are introduced to extend the information associated to the existing classes: the OtherInfo attribute and the `Extension` class. The OtherInfo attribute is present in the `Entity` class, therefore it is inherited by all GLUE classes. Its type is string and its multiplicity is *. This SHOULD be used for associating a flat list of tags to a certain class instance. The `Extension` class is associated to the `Entity` class (and therefore also to all the derived classes) and enables to link key/value pairs to any GLUE class instance. This SHOULD be used when there is the need for advertising more structured information, for instance an attribute not present in the model with a related value. 

Both solutions are proposed because they have a different impact in the implementations: the OtherInfo approach is easier to query, nevertheless it MAY require parsing in case of concatenation of different chunks of information (e.g., attribute name and attribute value). The `Extension` class offers a two-dimensional construct, but nevertheless it is more complex to query.

The extensibility regarding the addition of new classes and associations is not supported at the conceptual level. We RECOMMEND to create specializations of the conceptual model and to implement them by extending the concrete data models. Such extensions MUST NOT be considered part of the GLUE specification, but nevertheless we RECOMMEND submitting them to the GLUE WG for consideration in future revisions of the specification.



1.  ** Template**

In order to enrich the UML Class Diagrams with additional information, a table for each UML class is provided.  This descriptive table is composed of three parts.  

The ﬁrst part refers to the whole entity and presents the entity name, the entity from which it inherits and the description of what the entity represents. 

The second part refers to the properties of the class; for each of them, the following characteristics are described: the attribute name, the data type, the multiplicity concerning how many values are allowed (* means zero or more), the unit of measurement and a description. For easy of reading, the properties that are inherited from a parent class are also listed. As regards the multiplicity, the value of zero means that it is allowed to refrain from publishing a value for the related attribute even though this MAY be measured. 

The third part refers to the associations (association, composition, aggregation or association class) that the class MAY hold with other classes.  For each association, the associated class reference is described in terms of the associated end class and key attribute, the multiplicity (i.e., the number of instances of the associated class that are allowed) and a description. The inherited associations are also reported in the "inherited association end" if they are not redefined in the "association end". The template structure is the following:


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td colspan="3" >
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >
   </td>
   <td>
   </td>
   <td colspan="2" >
   </td>
  </tr>
  <tr>
   <td colspan="2" >
    Inherited Association End
   </td>
   <td>
    Mult.
   </td>
   <td colspan="2" >
    Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >
   </td>
   <td>
   </td>
   <td colspan="2" >
   </td>
  </tr>
</table>




1.  **Conceptual Model of the Main Entities**

This section introduces the main entities of the GLUE information model. They capture the core concepts relevant in a Grid environment. The main entities SHOULD be used to derive specialized information models. In Figure 1, the classes and the related relationships are presented in the form of a UML Class Diagram.

![Figure 1 Entities and relationships for the Main Entities conceptual model](images/glue2-1-draft-v0-5-doc0.png "Figure 1 Entities and relationships for the Main Entities conceptual model")


**Figure 1 Entities and relationships for the Main Entities conceptual model**



    1.  Entity

The `Entity` class is the root entity from which all the GLUE classes inherit (an exception is made for the `Extension` class). The specialized classes will inherit both the associations and the attributes of `Extension` class. The attributes CreationTime and Validity are metadata related to the generation and life of the information. The Name attribute allows a human-readable name to be provided for any object, usable for e.g. monitoring or diagnostic displays. The Name SHOULD NOT have any semantic interpretation.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Entity        
<p>
<&lt;abstract>>
   </td>
   <td colspan="3" >
   </td>
   <td>Abstract root concept from which all the other concepts are derived (except the <code>Extension</code> class); it has metadata about information creation and validity plus a key-value pair extension mechanism.
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>CreationTime
   </td>
   <td>DateTime_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>Timestamp describing when the entity instance was generated.
   </td>
  </tr>
  <tr>
   <td>Validity
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>s
   </td>
   <td>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,
<p>
the information SHOULD NOT be considered relevant.
   </td>
  </tr>
  <tr>
   <td>ID                             [key]
   </td>
   <td>URI
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>A global unique ID.
   </td>
  </tr>
  <tr>
   <td>Name
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>A human-readable name.
   </td>
  </tr>
  <tr>
   <td>OtherInfo
   </td>
   <td>String
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>Placeholder to publish information that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value) pairs are all examples of valid syntax.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be associated to zero or more key-value pairs.
   </td>
  </tr>
</table>




    1.  Extension

The `Extension` class provides a general mechanism to add key/value pairs to GLUE classes when suitable specific attributes are not present. The creation time and validity of each `Extension` instance are those of the extended class instance. 


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Extension
   </td>
   <td colspan="3" >
   </td>
   <td>A key/value pair enabling the association of extra information not captured by the model with an Entity instance.
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>LocalID
   </td>
   <td>LocalID_t
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>An identifier unique within the class instance to which it is associated
   </td>
  </tr>
  <tr>
   <td>Key        
   </td>
   <td>String
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>An identifier local to the container class instance; typically an attribute name not present in the model. This identifier is not required to be unique; several instances of this class MAY hold the same value for this attribute.
   </td>
  </tr>
  <tr>
   <td>Value
   </td>
   <td>String
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>A value for the attribute named by the Key.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Entity
   </td>
   <td>1
   </td>
   <td colspan="2" >The key/value pair is associated to an Entity instance.
   </td>
  </tr>
</table>




    1.  Location

The `Location` class is introduced to model geographical locations where a certain `Domain` or `Service` are placed. The aim is to provide a simple way to express geographical information, and it is not intended to be used in complex geographical information systems. Due to different requirements, the granularity is not strictly defined and is left to the information producers depending on their needs. Hence the extent of a geographical location can vary from an exact position to a region spanning several different countries, not necessarily adjacent. The accuracy of the latitude and longitude attributes should be defined in an interoperability profile defined by projects adopting this specification.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Location
   </td>
   <td colspan="3" >Entity
   </td>
   <td>A geographical region where the granularity MAY vary from an exact position to a region spanning several different countries, not necessarily adjacent.
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                             [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Address
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>Street address (free format).
   </td>
  </tr>
  <tr>
   <td>Place
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>Name of town/city.
   </td>
  </tr>
  <tr>
   <td>Country
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>Name of country.
   </td>
  </tr>
  <tr>
   <td>PostCode
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>Postal code.
   </td>
  </tr>
  <tr>
   <td>Latitude
   </td>
   <td>Real32
   </td>
   <td>0..1
   </td>
   <td>degree
   </td>
   <td>The position of a place north or south of the equator measured from -90° to +90° with positive values going north and negative values going south.
   </td>
  </tr>
  <tr>
   <td>Longitude
   </td>
   <td>Real32
   </td>
   <td>0..1
   </td>
   <td>degree
   </td>
   <td>The position of a place east or west of the primary meridian (located in Greenwich, UK) measured from -180° to +180° with positive values going east and negative values going west (the value -180° is excluded from the range).
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Service.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >The location is related to zero or more services.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Domain.ID                                &lt;<abstract>>
   </td>
   <td>*
   </td>
   <td colspan="2" >The location is related to zero or more domains.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be associated to zero or more key-value pairs.
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingService.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >The location is related to zero or more computing services.
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingService.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >The location is related to zero or more cloud computing services
   </td>
  </tr>
  <tr>
   <td colspan="2" >StorageService.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >The location is related to zero or more storage services.
   </td>
  </tr>
  <tr>
   <td colspan="2" >AdminDomain.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >The location is related to zero or more admin domains.
   </td>
  </tr>
  <tr>
   <td colspan="2" >UserDomain.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >The location is related to zero or more user domains.
   </td>
  </tr>
</table>




    1.  Contact

The `Contact` class is introduced to represent contact information for different groups or expert roles responsible for aspects of the operation of services and domains (e.g., user support, security or sysadmin). The various types of contact are identified by the Type attribute. In case of time-dependent contact information (e.g., due to work on shifts), the instances of this entity should represent only the currently active contact information.  

The contact information SHOULD be encoded as a URI. There are several specifications recommending how to embed contacts into a URI. The following specifications SHOULD be used:



*   telephone and fax: http://www.ietf.org/rfc/rfc2806.txt
*   email: http://www.ietf.org/rfc/rfc2368.txt
*   irc: http://www.w3.org/Addressing/draft-mirashi-url-irc-01.txt

<table>
  <tr>
   <td>
Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Contact
   </td>
   <td colspan="3" >Entity
   </td>
   <td> Information enabling the establishment of communication with a person or group of persons related to a Domain.
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                            [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Detail
   </td>
   <td>URI
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>URI embedding the contact information. The syntax of the URI depends on the nature of the communication channel.
   </td>
  </tr>
  <tr>
   <td>Type
   </td>
   <td>ContactType_t
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>Type of contact.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Service.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >The contact is related to zero or more services
   </td>
  </tr>
  <tr>
   <td colspan="2" >Domain.ID                                   &lt;<abstract>>
   </td>
   <td>*
   </td>
   <td colspan="2" >The contact is related to zero or more domains
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be associated to zero or more key-value pairs
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingService.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >The contact is related to zero or more computing services
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingService.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >The contact is related to zero or more cloud computing services
   </td>
  </tr>
  <tr>
   <td colspan="2" >StorageService.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >The contact is related to zero or more storage services
   </td>
  </tr>
  <tr>
   <td colspan="2" >AdminDomain.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >The contact is related to zero or more admin domains
   </td>
  </tr>
  <tr>
   <td colspan="2" >UserDomain.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >The contact is related to zero or more user domains
   </td>
  </tr>
</table>




    1.  Domain

The `Domain` class is introduced to model and identify groups of actors that MAY play roles in a Grid system. It is an abstract entity that MUST NOT be instantiated; it SHOULD be used in order to derive specialized entities.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Domain
<p>
<&lt;abstract>>
   </td>
   <td colspan="3" >Entity
   </td>
   <td>A collection of actors that MAY be assigned with roles and privileges associated with Entities via Policies. A Domain MAY have relationships to other domains.
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                          [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Description
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>A description of the domain (free format).
   </td>
  </tr>
  <tr>
   <td>WWW
   </td>
   <td>URL
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>A URL identifying a web page with more information about the domain.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Contact.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >A domain MAY be contacted via zero or more contacts.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Location.ID
   </td>
   <td>0..1
   </td>
   <td colspan="2" >A domain is primarily located at one location.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be associated to zero or more key-value pairs.
   </td>
  </tr>
</table>




        1.  AdminDomain

The `AdminDomain` class is introduced to model a collection of actors that manage a number of services. An `AdminDomain` MAY be associated to both `Contact` and `Location` class instances in order to provide contact information and geographical location respectively. An `AdminDomain` MAY be composed by other `AdminDomains` in a hierarchical structure. This structure MAY represent a "participates in" association.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>AdminDomain
   </td>
   <td colspan="3" >Domain
   </td>
   <td>A collection of actors that MAY be assigned administrative roles and privileges over services via policies. An AdminDomain manages services that MAY be geographically distributed, but nevertheless a primary location should be identified.
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                           [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td><em>Description</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>A description of the domain</em>
   </td>
  </tr>
  <tr>
   <td><em>WWW</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>The URL identifying a web page with more information about the domain</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Distributed
   </td>
   <td>ExtendedBoolean_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>True if the services managed by the AdminDomain are considered geographically distributed by the administrators themselves.
   </td>
  </tr>
  <tr>
   <td>Owner
   </td>
   <td>String
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>Identification of a person or legal entity which pays for the services and resources (no particular format is defined).
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Service.ID 
   </td>
   <td>*
   </td>
   <td colspan="2" >An AdminDomain manages zero or more Services.
   </td>
  </tr>
  <tr>
   <td colspan="2" >AdminDomain.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >An AdminDomain aggregates zero or more AdminDomains.
   </td>
  </tr>
  <tr>
   <td colspan="2" >AdminDomain.ID
   </td>
   <td>0..1
   </td>
   <td colspan="2" >An AdminDomain participates in another AdminDomain.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingService.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >An AdminDomain manages zero or more Computing Services.
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingService.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >An AdminDomain manages zero or more Cloud Computing Services
   </td>
  </tr>
  <tr>
   <td colspan="2" >StorageService.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >An AdminDomain manages zero or more Storage Services.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Contact.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >A domain MAY be contacted via zero or more contacts.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Location.ID
   </td>
   <td>0..1
   </td>
   <td colspan="2" >A domain is primary located at one location.
   </td>
  </tr>
</table>




        1.  UserDomain

The `UserDomain` class SHOULD be used to capture the concept of a Virtual Organization (VO). By VO, we mean a set of individuals and/or institutions having direct access to computers, software, data, and other resources for collaborative problem-solving or other purposes. Resources utilized by a VO are expected to be accessible via network endpoints and constrained by defined utilization targets called shares. The VO MAY exhibit its internal structure in terms of groups of individuals, each of them constituting a `UserDomain`. `UserDomains` MAY be hierarchically structured. The "participates in" association MAY represent this structure.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>UserDomain
   </td>
   <td colspan="3" >Domain
   </td>
   <td>A collection of actors that MAY be assigned with user roles and privileges to services or shares via policies.
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                             [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td><em>Description</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>A description of the domain</em>
   </td>
  </tr>
  <tr>
   <td><em>WWW</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>The URL identifying a web page with more information about the domain</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Level
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The number of hops to reach the root for hierarchically organized domains described by the "composed by" association (0 is for the root).
   </td>
  </tr>
  <tr>
   <td>UserManager
   </td>
   <td>URI
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>An Endpoint ID for the endpoint of a service managing the association of users with the domain, and related attributes such as groups or roles.
   </td>
  </tr>
  <tr>
   <td>Member
   </td>
   <td>String
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>An identifier for a user in this user domain.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Policy.ID                                              &lt;<abstract>>
   </td>
   <td>*
   </td>
   <td colspan="2" >A User Domain has associated zero or more policies.
   </td>
  </tr>
  <tr>
   <td colspan="2" >UserDomain.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >A User Domain aggregates zero or more User Domains.
   </td>
  </tr>
  <tr>
   <td colspan="2" >UserDomain.ID
   </td>
   <td>0..1
   </td>
   <td colspan="2" >An User Domain participates in another User Domain.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Contact.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >The domain MAY be contacted via zero or more contacts.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Location.ID
   </td>
   <td>0..1
   </td>
   <td colspan="2" >A domain is primary located at one location.
   </td>
  </tr>
  <tr>
   <td colspan="2" >AccessPolicy.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >A User Domain has associated zero or more access policies.
   </td>
  </tr>
  <tr>
   <td colspan="2" >MappingPolicy.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >A User Domain has associated zero or more mapping policies.
   </td>
  </tr>
</table>


As regards the UserManager attribute, it is RECOMMENDED that its value is an Endpoint ID enabling discovery of the related `Service` class instance and associated attributes. An example of a User Manager would be an endpoint for a VOMS (Virtual Organization Membership Service, http://en.wikipedia.org/wiki/VOMS) server. 



    1.  Service

One of the main goals of the GLUE information model is to enable the discovery of the Grid capabilities available in a certain infrastructure. Based on the use cases and modeling experience, a number of concepts were identified as general building blocks: `Endpoint`, `Share`, `Manager`, `Resource. `The` Service` class enables the unique identification of instances of these concepts participating in the provision of some unified capability.  The` Service` class SHOULD be also used to characterize this overall capability.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Service
   </td>
   <td colspan="3" >Entity
   </td>
   <td>An abstracted, logical view of actual software components that participate in the creation of an entity providing one or more functionalities useful in a Grid environment. A service exposes zero or more Endpoints having well-defined interfaces, zero or more Shares and zero or more Managers and the related Resources. The Service is autonomous and denotes a weak aggregation among Endpoints, the underlying Managers and the related Resources, and the defined Shares. The Service enables the identification of this whole set of entities providing the functionality with a persistent name.
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                             [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Capability
   </td>
   <td>Capability_t
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>The provided capabilities according to the Open Grid Service Architecture (OGSA) architecture [OGF-GFD80] (this is the union of all values assigned to the Capability attribute of the Endpoints which form part of this service).
   </td>
  </tr>
  <tr>
   <td>Type
   </td>
   <td>ServiceType_t
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>The type of service according to a namespace-based classification (the namespace MAY be related to a middleware name, an organization or other concepts; org.ogf.glue.* is reserved for Types defined by the OGF GLUE Working Group).
   </td>
  </tr>
  <tr>
   <td>QualityLevel
   </td>
   <td>QualityLevel_t
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>The maturity of the Service in terms of the quality of the underlying software components; the value corresponds to the highest QualityLevel among the available Endpoints.
   </td>
  </tr>
  <tr>
   <td>StatusInfo
   </td>
   <td>URL
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>A URL specifying a web page providing additional information, for example monitoring of the underlying services.
   </td>
  </tr>
  <tr>
   <td>Complexity
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>A human-readable summary description of the complexity in terms of the number of endpoint types, shares and resources. The syntax should be: endpointType=X, share=Y, resource=Z.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Endpoint.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >A service exposes zero or more endpoints.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Share.ID                                                    &lt;<abstract>>
   </td>
   <td>*
   </td>
   <td colspan="2" >A service offers zero or more shares.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Manager.ID                                                &lt;<abstract>>
   </td>
   <td>*
   </td>
   <td colspan="2" >A service offers zero or more managers.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Contact.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >A service has zero or more contacts.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Location.ID
   </td>
   <td>0..1
   </td>
   <td colspan="2" >A service is primary located at a location.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Service.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >A service is related to zero or more services.
   </td>
  </tr>
  <tr>
   <td colspan="2" >
   </td>
   <td>
   </td>
   <td colspan="2" >
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
</table>


A simple `Service` aggregates an `Endpoint`, no `Share`, no `Manager` and no `Resource` (e.g., a metadata catalogue service). In the context of a `Service` class, the same `Resource` MAY be exposed via multiple `Endpoints` based on the defined `Shares`.  For instance, in the area of storage systems, two `Endpoints` implementing SRMv1 [SRMV1] and SRMv2.2 [SRMV2] interfaces respectively MAY expose the same `Resource` via different `Endpoints` offering different interface versions; in the area of computing systems, the CREAM [cream] and GRAM [GRAM] `Endpoints` MAY expose the `Resources` locally managed by the same `Manager` (typically a batch system). `Endpoints,` `Shares`, `Managers `and `Resources` MUST belong to precisely one Service.



    1.  Endpoint

The `Endpoint` class models a network location that can be contacted to access certain functionalities based on a well-defined interface. The defined attributes refer to aspects such as the network location, the exposed interface name and version, the details of the implementation, the functional state and the scheduled downtime.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Endpoint
   </td>
   <td colspan="3" >Entity
   </td>
   <td>A network location having a well-defined interface and exposing specific service functionalities.
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                             [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>URL
   </td>
   <td>URL
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>Network location of an endpoint,which enables a specific component of the Service to be contacted.
   </td>
  </tr>
  <tr>
   <td>Capability
   </td>
   <td>Capability_t
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>The provided capability according to the OGSA architecture classification.
   </td>
  </tr>
  <tr>
   <td>Technology
   </td>
   <td>EndpointTechnology_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The technology used to implement the endpoint interface.
   </td>
  </tr>
  <tr>
   <td>InterfaceName
   </td>
   <td>InterfaceName_t
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>The identification name of the primary protocol supported by the endpoint interface.
   </td>
  </tr>
  <tr>
   <td>InterfaceVersion
   </td>
   <td>String
   </td>
   <td>0..*
   </td>
   <td>
   </td>
   <td>The version of the primary interface protocol (free format).
   </td>
  </tr>
  <tr>
   <td>InterfaceExtension
   </td>
   <td>URI
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>The identification of an extension to the interface protocol supported by the Endpoint.
   </td>
  </tr>
  <tr>
   <td>WSDL
   </td>
   <td>URL
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>The URL of a WSDL document describing the offered interface (this applies only to Web Services endpoints).
   </td>
  </tr>
  <tr>
   <td>SupportedProfile
   </td>
   <td>URI
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>A URI identifying a supported profile for the Endpoint interface.
   </td>
  </tr>
  <tr>
   <td>Semantics
   </td>
   <td>URL
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>The URl of a document providing a human-readable description of the semantics of the Endpoint functionalities (e.g. a software manual).
   </td>
  </tr>
  <tr>
   <td>Implementor
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The name of the main organization implementing this software component (free format, but the chosen names SHOULD be clearly identifiable with the organisation).
   </td>
  </tr>
  <tr>
   <td>ImplementationName
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The name of the implementation (as defined by the Implementor).
   </td>
  </tr>
  <tr>
   <td>ImplementationVersion
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The version of the implementation (the syntax is defined by the Implementor, but MAY be: major.minor.patch).
   </td>
  </tr>
  <tr>
   <td>QualityLevel
   </td>
   <td>QualityLevel_t
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>The maturity of the endpoint in terms of the quality of the software components which implement it.
   </td>
  </tr>
  <tr>
   <td>HealthState
   </td>
   <td>EndpointHealthState_t
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>A state representing the current health of the Endpoint in terms of its ability to properly deliver the expected  functionality.
   </td>
  </tr>
  <tr>
   <td>HealthStateInfo
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>A human-readable explanation of the HealthState of the  Endpoint (free format).
   </td>
  </tr>
  <tr>
   <td>ServingState
   </td>
   <td>ServingState_t
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>A state specifying whether the Endpoint is currently accepting new requests, and whether it is currently servicing requests which have already been accepted.
   </td>
  </tr>
  <tr>
   <td>StartTime
   </td>
   <td>DateTime_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The timestamp of the start time of the service underlying the Endpoint.
   </td>
  </tr>
  <tr>
   <td><em>Authentication</em>
   </td>
   <td><em>EndpointAuthentication_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Name of the authentication method supported by the endpoint.</em>
   </td>
  </tr>
  <tr>
   <td>IssuerCA
   </td>
   <td>DN_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The Distinguished Name of the Certification Authority issuing the host/service certificate presented by the Endpoint.
   </td>
  </tr>
  <tr>
   <td>TrustedCA
   </td>
   <td>DN_t
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>The Distinguished Name of a trusted Certification Authority (CA); i.e., certificates issued by the CA are accepted by the authentication process. Alternatively this may identify a standard bundle of accepted CAs, e.g. those accredited by the IGTF. Note that this does not imply that such certificates will be authorized to use the Endpoint.
   </td>
  </tr>
  <tr>
   <td>DowntimeAnnounce
   </td>
   <td>DateTime_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The timestamp for an announcement of the next scheduled downtime.
   </td>
  </tr>
  <tr>
   <td>DowntimfeStart
   </td>
   <td>DateTime_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>A timestamp describing when the next downtime is scheduled to start.
   </td>
  </tr>
  <tr>
   <td>DowntimeEnd
   </td>
   <td>DateTime_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>A timestamp describing when the next downtime is scheduled to end.
   </td>
  </tr>
  <tr>
   <td>DowntimeInfo
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>A human-readable description of the next scheduled downtime (free format).
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Service.ID 
   </td>
   <td>1
   </td>
   <td colspan="2" >An endpoint is part of a Service.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Share.ID                                                   &lt;<abstract>>
   </td>
   <td>*
   </td>
   <td colspan="2" >An endpoint MAY pass activities to zero or more Shares.
   </td>
  </tr>
  <tr>
   <td colspan="2" >AccessPolicy.ID 
   </td>
   <td>*
   </td>
   <td colspan="2" >An endpoint has associated zero or more AccessPolicies.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Activity.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >An endpoint has accepted and is managing zero or more Activities.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
</table>


For Grid services requiring a richer set of attributes for the `Endpoint`, specific models MAY be derived by specializing from the `Endpoint` class and adding new properties or relationships. The current proposal contains the `ComputingEndpoint` specialization (see Section 8.2) and the `StorageEndpoint` specialization (see Section 9.4).

The network location of an endpoint MUST be encoded in a URI. When available, standard schemes for the encoding SHOULD be used (e.g., as used for the Java Messaging Service http://www.ietf.org/internet-drafts/draft-merrick-jms-uri-03.txt).

Concerning the SupportedProfile attribute, if there is no recommended URI for the identification of a certain profile, then the following options SHALL be considered: (1) use the main URL of the document specifying the profile, or (2) use the target namespace URI (in case of an XML Schema representation of the profile).



    1.  Share

The `Share` class is an abstract entity that MUST NOT be instantiated; it SHOULD be used in order to derive specialized entities. At this level, it is introduced to capture the concept of a utilization target, that is a constrained usage of service functionalities or resources that MAY be created based on aspects such as identify or UserDomain membership, usage information or resource characteristics.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Share
<p>
<&lt;abstract>>
   </td>
   <td colspan="3" >Entity
   </td>
   <td>A utilization target for a set of Resources managed by a local Manager and offered via related Endpoints. The share is defined by configuration parameters and characterized by status information.
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                             [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Description
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>A human-readable description of this share (free format).
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Endpoint.ID                              
   </td>
   <td>*
   </td>
   <td colspan="2" >A share is consumed via one or more endpoints.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Resource.ID                             &lt;<abstract>>
   </td>
   <td>*
   </td>
   <td colspan="2" >A share is defined on one or more resources.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Service.ID                                
   </td>
   <td>1
   </td>
   <td colspan="2" >A share participates in a service.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Activity.ID                                 
   </td>
   <td>*
   </td>
   <td colspan="2" >A share is consumed by zero or more activities.
   </td>
  </tr>
  <tr>
   <td colspan="2" >MappingPolicy.ID                     
   </td>
   <td>*
   </td>
   <td colspan="2" >A share has zero or more mapping policies.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
</table>


	



    1.  Manager

The `Manager` class is an abstract entity that MUST NOT be instantiated; it SHOULD be used in order to derive specialized entities. At this level, it is introduced to capture the characteristics of a local software layer (not directly exposed via an Endpoint) which has control of the underlying resources. The functionalities of a manager layer that need to be accessible by remote users are typically abstracted by a middleware component via a standard interface, and are modeled by the concept of `Endpoint.` Examples of managers are: for computing resources, batch systems such as OpenPBS or LSF; for storage resources, GPFS or HPSS. 


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Manager
<p>
<&lt;abstract>>
   </td>
   <td colspan="3" >Entity
   </td>
   <td>A software component locally managing one or more resources. It MAY also describe aggregated information about the managed resources. 
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                             [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>ProductName
   </td>
   <td>String
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>The name of the software product which implements the Manager functionality. The attribute is free format, but SHOULD correspond to the standard name by which the product is generally known.
   </td>
  </tr>
  <tr>
   <td>ProductVersion
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The version of the software product which implements the Manager functionality. The attribute is free format, but SHOULD correspond to the primary version as defined by the software provider.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Service.ID                              
   </td>
   <td>1
   </td>
   <td colspan="2" >A manager participates in a service.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Resource.ID                           &lt;<abstract>>
   </td>
   <td>1..*
   </td>
   <td colspan="2" >A manager manages zero or more resources.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
</table>




    1.  Resource

The `Resource` class is an abstract entity that MUST NOT be instantiated; it SHOULD be used in order to derive specialized entities. It is introduced to identify and model hardware entities providing capabilities which are exposed via `Endpoints`. Examples are execution environments for computational activities or data stores for data.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Resource
<p>
<&lt;abstract>>
   </td>
   <td colspan="3" >Entity
   </td>
   <td>An entity providing a capability or capacity, managed by a local software component (Manager), part of a logical Service, reachable via one or more Endpoints and having one or more Shares defined on it. A Resource MAY refer to a specified category of hardware, with summary information on the available resources in that category.  
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                             [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td colspan="5" ><em>No extra properties are defined in the specialized entity</em>
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Manager.ID                            &lt;<abstract>>
   </td>
   <td>1
   </td>
   <td colspan="2" >A resource is managed by a manager.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Share.ID                        &lt;<abstract>>
   </td>
   <td>*
   </td>
   <td colspan="2" >A resource provides capacity in terms of shares.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Activity.ID                               
   </td>
   <td>*
   </td>
   <td colspan="2" >A resource runs zero or more activities.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
</table>




    1.  Activity

The `Activity` class models units of work which are submitted to `Services` via `Endpoints`. Grid jobs, i.e. Computing Activities in GLUE, are example of `Activities` for a Computing Service. An interesting type of relationship for jobs derives from their propagation through several `Services`. For instance, a broker `Service` submits a Grid job to a selected execution `Service;` upon completion the execution `Service` submits a logging record to an accounting `Service`. Each of these `Services` may have associated an instance of a Grid `Activity` related to the lifecycle of the job within the service. All instances refer to the same conceptual job submitted by the user.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Activity
   </td>
   <td colspan="3" >Entity
   </td>
   <td>An Activity is a unit of work managed by a Service and submitted via an Endpoint; when accepted by the Endpoint, than it MAY be mapped to a Share and MAY be executed by a local Manager via one or more Resources. An Activity MAY have relationships to other Activities being managed by different Services, in which case it shares a common context.
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                             [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>No extra properties are defined in the specialized entity</em>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >UserDomain.ID                        
   </td>
   <td>0..1
   </td>
   <td colspan="2" >An activity is managed by a user domain.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Endpoint.ID                             
   </td>
   <td>0..1
   </td>
   <td colspan="2" >An activity is submitted to an endpoint.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Share.ID                         &lt;<abstract>>
   </td>
   <td>0..1
   </td>
   <td colspan="2" >An activity is mapped into a share.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Resource.ID                            &lt;<abstract>>
   </td>
   <td>0..1
   </td>
   <td colspan="2" >An activity is executed in a resource.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Activity.ID                               
   </td>
   <td>*
   </td>
   <td colspan="2" >An activity is related to zero or more activities.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Activity.ID                                
   </td>
   <td>*
   </td>
   <td colspan="2" >An activity is related to zero or more activities.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
</table>




    1.  Policy

The `Policy` class is an abstract entity that MUST NOT be instantiated; it SHOULD be used in order to derive specialized entities. This class is introduced to model statements, rules or assertions that define the correct or expected behavior of entities. Two specializations are introduced: `AccessPolicy` related to `Endpoints` and `MappingPolicy` related to `Shares`.

For a given entity to which policies are associated (i.e., `Endpoint` and `AccessPolicy`, `Share` and `MappingPolicy`), several instances of the `Policy` class MAY be defined. This is allowed in order to enable the advertisement of policies using different schemes. We RECOMMEND that only one instance per policy scheme is associated to the same entity instance. The evaluation algorithm for the rules SHOULD be defined by the policy scheme.

If an entity instance is associated to different `Policy` instances, each of them based on a different scheme, then the evaluation process SHOULD consider each set of policies independently. This means that the evaluation SHOULD rely on a certain policy scheme which is selected and understood by the consumer, and not by composing policies expressed using different schemes.

In this document, we provide the definition for a "basic" scheme (see Appendix B.37). Such a scheme is designed to be simple and is inspired by real world scenarios in current production Grid systems. The Rule attribute implicitly contains a reference to the associated User Domains; therefore, in the concrete data model mapping, we RECOMMEND to not represent the association between User Domain and Access Policy or Mapping Policy explicitly since it is already captured by the Rule.

More complex schemes MAY be defined in profile documents describing the usage of the schema in particular Grid infrastructures.

The published `Policies` do not represent a contract, and hence the associated `Service` is not bound to honour the decisions implied by the published rules. In addition the published rules may be expressed at a coarse granularity, which may be modified internally by more finely-grained rules which are not published. However, the published rules SHOULD match the decisions which will be made in practice in a substantial majority of cases.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Policy
<p>
<&lt;abstract>>
   </td>
   <td colspan="3" >Entity
   </td>
   <td>Statements, rules or assertions that specify the correct or expected behavior of an entity.
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                            [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Scheme
   </td>
   <td>PolicyScheme_t
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>The scheme used to define the syntax and semantics of the policy Rules.
   </td>
  </tr>
  <tr>
   <td>Rule
   </td>
   <td>String
   </td>
   <td>1..*
   </td>
   <td>
   </td>
   <td>A policy rule (for the basic policy scheme, the syntax is provided in the Appendix).
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >UserDomain.ID                             
   </td>
   <td>1..*
   </td>
   <td colspan="2" >A policy is related to a user domain.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
</table>




        1.  AccessPolicy

The `AccessPolicy` class is a specialization of the `Policy` class. This entity MAY be used to express authorization rules, e.g.  which `UserDomains` MAY access a certain service `Endpoint`. The granularity of these policies SHOULD be coarse-grained and suitable for pre-selection of services. The actual decision on the service side is performed by an authorization component that MAY contain a finer-grained set of policy rules that in some case MAY contradict the published coarse-grained policy rules. The default policy is assumed to be to deny access, hence `Endpoints `for which there are no matching Rules SHOULD NOT be selected for possible use.

Examples of actors involved in this entity are `UserDomains` representing VOs or groups.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>AccessPolicy
   </td>
   <td colspan="3" >Policy
   </td>
   <td>Statements, rules or assertions that provide coarse-granularity information about the authorization of access by groups of actors to an Endpoint.
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                            [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td><em>Scheme</em>
   </td>
   <td><em>PolicyScheme_t</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>Scheme adopted to define the policy rules</em>
   </td>
  </tr>
  <tr>
   <td><em>Rule</em>
   </td>
   <td><em>PolicyRule_t</em>
   </td>
   <td><em>1..*</em>
   </td>
   <td>
   </td>
   <td><em>A policy rule (for the basic policy scheme, syntax is provide in the Appendix)</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td colspan="5" ><em>No extra properties are defined in the specialized entity.</em>
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Endpoint.ID                             
   </td>
   <td>1
   </td>
   <td colspan="2" >An access policy is related to an endpoint.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
  <tr>
   <td colspan="2" >UserDomain.ID                             
   </td>
   <td>1..*
   </td>
   <td colspan="2" >An access policy is related to a user domain.
   </td>
  </tr>
</table>




        1.  MappingPolicy

The `MappingPolicy` class is a specialization of the `Policy` class. This entity MAY be used to express which `UserDomains` MAY consume a certain share of resources. The granularity of these policies SHOULD be coarse-grained and suitable for pre-selection of services. The actual decision on the service side is performed by an authorization component that MAY contain a finer-grained set of policy rules that in some case MAY contradict the published coarse-grained policy rules.

Conceptually, the union of all the `MappingPolicy` rules should match the corresponding `AccessPolicy `rules, i.e. any authorised` UserDomain `will be mapped to at least one `Share. `However, publication of` Shares `is OPTIONAL, and hence there MAY be no` Share `with a matching` MappingPolicy `rule. In this case a consumer SHOULD NOT make any assumption about the properties of the `Share `to which it will be mapped. Conversely, the published `MappingPolicy `rules MAY not have a corresponding` AccessPolicy`, in which case the implication is that there is some unpublished access method enabling access to the associated Share.

When evaluating the mapping to a certain `Share` using the algorithm implied by the policy scheme, if multiple solutions are available then the consumer SHOULD NOT make any assumption about which `Share` will be assigned to its `Activity,` and if it requires a specific `Share` it SHOULD request that `Share` explicitly.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>MappingPolicy
   </td>
   <td colspan="3" >Policy
   </td>
   <td>Statements, rules or assertions that provide coarse-granularity information about the mapping of User Domain requests to a Share.
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                            [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td><em>Scheme</em>
   </td>
   <td><em>PolicyScheme_t</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>Scheme adopted to define the policy rules</em>
   </td>
  </tr>
  <tr>
   <td><em>Rule</em>
   </td>
   <td><em>PolicyRule_t</em>
   </td>
   <td><em>1..*</em>
   </td>
   <td>
   </td>
   <td><em>A policy rule (for the basic policy scheme, syntax is provide in the Appendix)</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td colspan="5" ><em>No extra properties are defined in the specialized entity</em>.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Share.ID                               &lt;<abstract>>
   </td>
   <td>1
   </td>
   <td colspan="2" >A mapping policy is related to a share.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
  <tr>
   <td colspan="2" >UserDomain.ID                             
   </td>
   <td>1..*
   </td>
   <td colspan="2" >An access policy is related to a user domain.
   </td>
  </tr>
</table>




1.  **Conceptual Model of the Computing Service**

The conceptual model of the Computing Service is based on the main entities and uses specializations of the `Service`, `Endpoint`, `Share`, `Manager`, `Resource`, and `Activity` entities.  Further computing related concepts such as `Application Environment`, `Application Handle` and `Benchmark` are introduced.


![Figure 2 Entities and relationships for the Computing Service conceptual model](images/glue2-1-draft-v0-5-doc1.png "Figure 2 Entities and relationships for the Computing Service conceptual model")
 

**Figure 2 Entities and relationships for the Computing Service conceptual model**

In this section, we extensively use the concepts of physical CPU, logical CPU and slot defined as follows:



*   a physical CPU is defined by a socket on a motherboard, i.e. there is one physical CPU per socket (e.g., a multi-core CPU counts as one physical CPU);
*   a logical CPU corresponds to a CPU as visible by the operating system running either on a real or virtual machine (e.g. a four-core CPU counts as four logical CPUs);
*   a slot is a portion of executable time in a logical CPU offered by an execution environment instance which MAY be occupied by a job:
    *   typically there is one slot per logical CPU, but a logical CPU MAY be shared among multiple slots;
    *   jobs MAY occupy several slots at the same time (e.g., MPI jobs); a multi-slot job is counted as one `Activity`.

Throughout the specification, we also use the concept of storage extent to mean the capabilities and management of the various media that exist to store data and allow data retrieval.



    1.  ComputingService

 \
The `ComputingService` class is a specialization of the `Service` class for a service offering computational capacity. The `ComputingService` entity is the main logical unit, and aggregation point for several entities together modeling a computing capability in a Grid system. A `ComputingService` is capable of executing `ComputingActivities` on its associated resources. The resources behind the `ComputingService` are described via the `ComputingManager`, `ExecutionEnvironment`, `ApplicationEnvironment`, `ApplicationHandle` and `Benchmark` entities. The governing policies and status of the resources are given by the `ComputingShare` elements. The `ComputingActivities` of a `ComputingService` are submitted and controlled via a `ComputingEndpoint`.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>ComputingService
   </td>
   <td colspan="3" >Service
   </td>
   <td>An abstracted, logical view of software and hardware components that participate in the creation of a computational capacity in a Grid environment. A Computing Service exposes zero or more Computing Endpoints having well-defined interfaces, zero or more Computing Shares and zero or more Computing Managers and the related Execution Environments. 
<p>
The computing service is autonomous and denotes a weak aggregation among Computing Endpoints, the underlying Computing Managers and related Execution Environments, and the defined Computing Shares. The Computing Service enables the identification of the whole set of entities providing the computing functionality with a persistent name.
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                          [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td><em>Capability</em>
   </td>
   <td><em>Capability_t</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>The provided capability according to the Open Grid Service Architecture (OGSA) architecture [OGF-GFD80] (this is the union of all values assigned to the capability attribute of the endpoints part of this service)</em>
   </td>
  </tr>
  <tr>
   <td><em>Type</em>
   </td>
   <td><em>ServiceType_t</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>The type of service according to a namespace-based classification (the namespace MAY be related to a middleware name, an organization or other concepts; org.ogf.glue is reserved for the OGF GLUE Working Group)</em>
   </td>
  </tr>
  <tr>
   <td><em>QualityLevel</em>
   </td>
   <td><em>QualityLevel_t</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>Maturity of the service in terms of quality of the software components</em>
   </td>
  </tr>
  <tr>
   <td><em>StatusInfo</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Web page providing additional information like monitoring aspects </em>
   </td>
  </tr>
  <tr>
   <td><em>Complexity</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable summary description of the complexity in terms of the number of endpoint types, shares and resources. The syntax should be: endpointType=X, share=Y, resource=Z.</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>TotalJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The total number of Grid jobs currently known to the system (the sum of RunningJobs, WaitingJobs, StagingJobs, SuspendedJobs and PreLRMSWaitingJobs); this value SHOULD not include jobs submitted locally rather than via the Grid.
   </td>
  </tr>
  <tr>
   <td>RunningJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The number of Grid jobs which are currently running in an Execution Environment. 
   </td>
  </tr>
  <tr>
   <td>WaitingJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The number of Grid jobs which are currently waiting to start execution. Usually these will be queued in the underlying Computing Manager (i.e., a Local Resource Managment System or LRMS). 
   </td>
  </tr>
  <tr>
   <td>StagingJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The number of Grid jobs which are currently either staging files in before starting execution, or staging files out after finishing execution.
   </td>
  </tr>
  <tr>
   <td>SuspendedJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The number of Grid jobs which have started their execution, but are currently suspended (e.g., having been preempted by another job).
   </td>
  </tr>
  <tr>
   <td>PreLRMSWaitingJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The number of Grid jobs which are currently managed by the Grid software layer waiting to be passed to the underlying Computing Manager (LRMS), and hence are not yet candidates to start execution.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingEndpoint.ID               
<p>
[redefines Endpoint.ID]
   </td>
   <td>*
   </td>
   <td colspan="2" >A computing service exposes zero or more computing endpoints.
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingShare.ID                         [redefines Share.ID]
   </td>
   <td>*
   </td>
   <td colspan="2" >A computing service offers zero or more computing shares.
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingManager.ID                                                [redefines Manager.ID]
   </td>
   <td>*
   </td>
   <td colspan="2" >A computing service offers zero or more computing managers.
   </td>
  </tr>
  <tr>
   <td colspan="2" >StorageService.ID 
   </td>
   <td>
   </td>
   <td colspan="2" >
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Contact.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >A computing service has zero or more contacts.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Location.ID
   </td>
   <td>0..1
   </td>
   <td colspan="2" >A computing service is primarily located at a location.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Service.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >A computing service is related to zero or more services.
   </td>
  </tr>
</table>


A simple `Computing Service` is formed by a `Computing Endpoint` exposing an interface for job submission and control. In the case of a single `Computing Manager` whose `Execution Environments` are exposed by multiple `Computing Endpoints`, the `Computing Manager`, `Execution Environments` and `Computing Endpoints` MUST be considered as part of the same `Computing Service`. In the case of a single `Computing Endpoint` exposing `Execution Environments` managed by different `Computing Managers`, then the `Computing Endpoint`, the `Execution Environments` and the related `Computing Managers` MUST be considered as part of the same `Computing Service`. 

The `Computing Service` always aggregates `Computing Endpoints`, `Computing Shares`, `Computing Managers` and `Execution Environments` forming a connected set. In other words, `Endpoint` A exposing `Execution Environment` A of `Manager` A via `Share` A and `Endpoint` B exposing `Execution Environment` B of `Manager` B via `Share` B form two different `Computing Services`. On the other hand, `Endpoint` A exposing `Execution` `Environment` A of `Manager` A via `Share` A and `Endpoint` B exposing `Execution Environment `A of `Manager` A via `Share` B form a single `Computing Service`. 



    1.  ComputingEndpoint

The `ComputingEndpoint` is a specialization of the `Endpoint` class for a service possessing computational capability. The class represents an endpoint which is used to create, control and monitor computational activities. The computational-specific information concerns service load related parameters, staging capabilities and supported types of job description. This class provides attributes that MAY be used to publish summary information about jobs submitted via a particular Endpoint. Such attributes are optional and may not always be measurable (e.g., in the case of a stateless Endpoint which does not keep information about the jobs submitted through it). 


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>ComputingEndpoint
   </td>
   <td colspan="3" >Endpoint
   </td>
   <td>A network Endpoint for creating, monitoring, and controlling computational Activities called jobs. It MAY also be used to expose complementary capabilities (e.g., resource reservation or proxy manipulation).
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                            [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td><em>URL</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>Network location of the endpoint to contact the related service</em>
   </td>
  </tr>
  <tr>
   <td><em>Capability</em>
   </td>
   <td><em>Capability_t</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>The provided capability according to the OGSA architecture</em>
   </td>
  </tr>
  <tr>
   <td><em>Technology</em>
   </td>
   <td><em>EndpointTechnology_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Technology used to implement the endpoint</em>
   </td>
  </tr>
  <tr>
   <td><em>InterfaceName</em>
   </td>
   <td><em>InterfaceName_t</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>Identification of the interface</em>
   </td>
  </tr>
  <tr>
   <td><em>InterfaceVersion</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..*</em>
   </td>
   <td>
   </td>
   <td><em>Version of the interface</em>
   </td>
  </tr>
  <tr>
   <td><em>InterfaceExtension</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Identification of an extension to the interface</em>
   </td>
  </tr>
  <tr>
   <td><em>WSDL</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>URL of the WSDL document describing the offered interface (applies to Web Services endpoint)</em>
   </td>
  </tr>
  <tr>
   <td><em>SupportedProfile</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>URI identifying a supported profile</em>
   </td>
  </tr>
  <tr>
   <td><em>Semantics</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>URI of a document providing a human-readable description of the semantics of the endpoint functionalities</em>
   </td>
  </tr>
  <tr>
   <td><em>Implementor</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Main organization implementing this software component</em>
   </td>
  </tr>
  <tr>
   <td><em>ImplementationName</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Name of the implementation</em>
   </td>
  </tr>
  <tr>
   <td><em>ImplementationVersion</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Version of the implementation (e.g., major version.minor version.patch version)</em>
   </td>
  </tr>
  <tr>
   <td><em>QualityLevel</em>
   </td>
   <td><em>QualityLevel_t</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>Maturity of the endpoint in terms of quality of the software components</em>
   </td>
  </tr>
  <tr>
   <td><em>HealthState</em>
   </td>
   <td><em>EndpointHealthState_t</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A state representing the health of the endpoint in terms of its capability of properly delivering the functionalities</em>
   </td>
  </tr>
  <tr>
   <td><em>HealthStateInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Textual explanation of the state endpoint</em>
   </td>
  </tr>
  <tr>
   <td><em>ServingState</em>
   </td>
   <td><em>ServingState_t</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A state specifying if the endpoint is accepting new requests and if it is serving the already accepted requests </em>
   </td>
  </tr>
  <tr>
   <td><em>StartTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>The timestamp for the start time of the endpoint</em>
   </td>
  </tr>
  <tr>
   <td><em>Authentication</em>
   </td>
   <td><em>EndpointAuthentication_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Name of the authentication method supported by the endpoint.</em>
   </td>
  </tr>
  <tr>
   <td><em>IssuerCA</em>
   </td>
   <td><em>DN_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Distinguished name of Certification Authority issuing the certificate for the endpoint</em>
   </td>
  </tr>
  <tr>
   <td><em>TrustedCA</em>
   </td>
   <td><em>DN_t</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Distinguished name of the trusted Certification Authority (CA), i.e., certificates issued by the CA are accepted for the authentication process</em>
   </td>
  </tr>
  <tr>
   <td><em>DowntimeAnnounce</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>The timestamp for the announcement of the next scheduled downtime</em>
   </td>
  </tr>
  <tr>
   <td><em>DowntimeStart</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>The starting timestamp of the next scheduled downtime</em>
   </td>
  </tr>
  <tr>
   <td><em>DowntimeEnd</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>The ending timestamp of the next scheduled downtime</em>
   </td>
  </tr>
  <tr>
   <td><em>DowntimeInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Description of the next scheduled downtime</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Staging
   </td>
   <td>Staging_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>Supported file staging functionalities, if any.
   </td>
  </tr>
  <tr>
   <td>JobDescription
   </td>
   <td>JobDescription_t
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>Supported type of job description language.
   </td>
  </tr>
  <tr>
   <td>TotalJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>Job
   </td>
   <td>The total number of Grid jobs currently known to the system (the sum of RunningJobs, WaitingJobs, StagingJobs, SuspendedJobs and PreLRMSWaitingJobs); this value SHOULD not include jobs submitted locally rather than via the Grid.
   </td>
  </tr>
  <tr>
   <td>RunningJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The number of Grid jobs which are currently running in an Execution Environment.
   </td>
  </tr>
  <tr>
   <td>WaitingJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The number of Grid jobs which are currently waiting to start execution. Usually these will be queued in the underlying Computing Manager (i.e., a Local Resource Managment System or LRMS).
   </td>
  </tr>
  <tr>
   <td>StagingJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The number of Grid jobs which are currently either staging files in before starting execution, or staging files out after finishing execution.
   </td>
  </tr>
  <tr>
   <td>SuspendedJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The number of Grid jobs which have started their execution, but are currently suspended (e.g., having been preempted by another job).
   </td>
  </tr>
  <tr>
   <td>PreLRMSWaitingJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The number of Grid jobs which are currently managed by the Grid software layer waiting to be passed to the underlying Computing Manager (LRMS), and hence are not yet candidates to start execution.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingService.ID 
<p>
[redefines Service.ID]
   </td>
   <td>1
   </td>
   <td colspan="2" >A computing endpoint is part of a Computing Service.
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingShare.ID                                                          [redefines Share.ID]
   </td>
   <td>*
   </td>
   <td colspan="2" >A computing endpoint MAY pass activities to zero or more computing shares.
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingActivity.ID
<p>
[redefines Activity.ID]
   </td>
   <td>*
   </td>
   <td colspan="2" >An endpoint has accepted and is managing zero or more Activities.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
  <tr>
   <td colspan="2" >AccessPolicy.ID 
   </td>
   <td>*
   </td>
   <td colspan="2" >A computing endpoint has assocated zero or more AccessPolicies.
   </td>
  </tr>
</table>




    1.  ComputingShare

The `ComputingShare` class is the specialization of the main `Share` class for computational services. A Computing Share is a high-level concept introduced to model a utilization target for a set of Execution Environments defined by a set of configuration parameters and characterized by status information. A `ComputingShare` carries information about "policies" (limits) defined over all or a subset of resources and describes their dynamic status (load). 

 \
In clusters managed by a batch system (LRMS), the simplest way to set up a Computing Share is to configure a batch queue. Nevertheless, the same Computing Share may be implemented using different batch system configuration strategies. In complex batch systems, a batch queue may be configured with different sets of policies for different sets of users. This implies that each set of users obtains a different utilization target. Such a scenario MAY be represented by different Computing Shares. In general, given a number of shares to be set up, it is possible to adopt different configuration strategies in the underlying system. Regardless of the selected approach, the external behavior does not change. The main goal of the Computing Share concept is to abstract from such implementation choices and to represent the externally observable behavior.  \
 \
The introduction of the Computing Share concept also supports the modelling of heterogeneity within a `ComputingService` by being able to have associations to different Execution Environments.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>ComputingShare
   </td>
   <td colspan="3" >Share
   </td>
   <td>A utilization target for a set of Execution Environments, defined by a set of configuration parameters and characterized by status information.
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                            [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td><em>Description</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Description of this share</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>MappingQueue
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The name of a queue available in the underlying Computing Manager (i.e., LRMS) where jobs related to this share are submitted. Different Shares MAY be mapped into the same queue; it is not foreseen that a single share MAY be mapped into many different queues.
   </td>
  </tr>
  <tr>
   <td>MaxWallTime
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>s
   </td>
   <td>The maximum obtainable wall clock time limit that MAY be granted to a single-slot job upon user request (un-normalized value, see below).
   </td>
  </tr>
  <tr>
   <td>MaxMultiSlotWallTime
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>s
   </td>
   <td>The maximum obtainable wall clock time limit that MAY be granted to a multi-slot job upon user request; this value is measured from the start of the first slot up to the release of the last slot. (un-normalized value, see below).
   </td>
  </tr>
  <tr>
   <td>MinWallTime
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>s
   </td>
   <td>The minimum wall clock time per slot for a job (un-normalized value, see below); if a job requests a lower time, then it MAY be rejected; if a job requests at least this value, but runs for a shorter time, then it might be accounted for this value.
   </td>
  </tr>
  <tr>
   <td>DefaultWallTime
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>s
   </td>
   <td>The default wall clock time limit per slot assigned to a job by the Computing Manager (LRMS) if no limit is requested in the job submission description (un-normalized value, see below). Once this time is expired the job MAY be killed or removed from the queue.
   </td>
  </tr>
  <tr>
   <td>MaxCPUTime
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>s
   </td>
   <td>The maximum obtainable CPU time limit that MAY be granted to the job upon user request per slot (un-normalized value, see below)
   </td>
  </tr>
  <tr>
   <td>MaxTotalCPUTime
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>s
   </td>
   <td>The maximum obtainable CPU time limit that MAY be granted to the job upon user request across all assigned slots; this attribute is a limit on the sum of the CPU time used in all the slots occupied by a multi-slot job (un-normalized value, see below).
   </td>
  </tr>
  <tr>
   <td>MinCPUTime
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>s
   </td>
   <td>The minimum CPU time per slot for a job (un-normalized value, see below); if a job requests a lower time, than it MAY be rejected; if a job requests at least this value, but uses the CPU for a shorter time, then it might be accounted for this value.
   </td>
  </tr>
  <tr>
   <td>DefaultCPUTime
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>s
   </td>
   <td>The default CPU time limit per slot assigned to each job by the Computing Manager (LRMS ) if no limit is requested in the job submission description (un-normalized value, see below).
   </td>
  </tr>
  <tr>
   <td>MaxTotalJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The maximum allowed number of jobs in this Share.
   </td>
  </tr>
  <tr>
   <td>MaxRunningJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The maximum allowed number of jobs in the running state in this Share.
   </td>
  </tr>
  <tr>
   <td>MaxWaitingJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The maximum allowed number of jobs in the waiting state in this Share.
   </td>
  </tr>
  <tr>
   <td>MaxPreLRMSWaitingJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The maximum allowed number of jobs that are in the Grid layer waiting to be passed to the underlying computing manager (i.e., LRMS) for this Share.
   </td>
  </tr>
  <tr>
   <td>MaxUserRunningJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The maximum allowed number of jobs in the running state per Grid user in this Share.
   </td>
  </tr>
  <tr>
   <td>MaxSlotsPerJob
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>slot
   </td>
   <td>The maximum number of slots which could be allocated to a single job in this Share (defined to be 1 for a Computing Manager accepting only single-slot jobs).
   </td>
  </tr>
  <tr>
   <td>MaxStageInStreams
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>stream
   </td>
   <td>The maximum number of streams available to stage files in.
   </td>
  </tr>
  <tr>
   <td>MaxStageOutStreams
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>stream
   </td>
   <td>The maximum number of streams available to stage files out.
   </td>
  </tr>
  <tr>
   <td>SchedulingPolicy
   </td>
   <td>SchedulingPolicy_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The type of scheduling policy used for the Share.
   </td>
  </tr>
  <tr>
   <td>MaxMainMemory
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>MB
   </td>
   <td>The maximum physical RAM that a job is allowed to use; if the limit is hit, then the LRMS MAY kill the job.
   </td>
  </tr>
  <tr>
   <td>GuaranteedMainMemory
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>MB
   </td>
   <td>The amount of physical RAM that a job is guaranteed to have available for its use.
   </td>
  </tr>
  <tr>
   <td>MaxVirtualMemory
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>MB
   </td>
   <td>The maximum total memory size (RAM plus swap) that a job is allowed to use; if the limit is hit, then the LRMS MAY kill the job.
   </td>
  </tr>
  <tr>
   <td>GuaranteedVirtualMemory
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>MB
   </td>
   <td>The total amount of memory (RAM plus swap) that a job is guaranteed to have available for its use.
   </td>
  </tr>
  <tr>
   <td>MaxDiskSpace
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>GB
   </td>
   <td>The maximum disk space that a job is allowed use in the working area; if the limit is hit, then the LRMS MAY kill the job.
   </td>
  </tr>
  <tr>
   <td>DefaultStorageService
   </td>
   <td>URI
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The ID of the default Storage Service to be used to store files by jobs in the case that no destination Storage Service is explicitly chosen.
   </td>
  </tr>
  <tr>
   <td>Preemption
   </td>
   <td>ExtendedBoolean_t 
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>True if the Computing Manager (i.e., LRMS) enables pre-emption of jobs; a pre-empted job is supposed to be automatically resumed, but may be suspended for an indefinite period. 
   </td>
  </tr>
  <tr>
   <td>ServingState
   </td>
   <td>ServingState_t
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>A state specifying whether the Share is open to accept new requests, and if it is open to offer the already present requests for execution.
   </td>
  </tr>
  <tr>
   <td>TotalJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The total number of jobs in any state (the sum of RunningJobs, WaitingJobs, StagingJobs, SuspendedJobs and PreLRMSWaitingJobs). Note that this number includes the locally submitted jobs.
   </td>
  </tr>
  <tr>
   <td>RunningJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The number of jobs which are currently running in an Execution Environment, submitted via any type of interface (local and Grid).
   </td>
  </tr>
  <tr>
   <td>LocalRunningJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The number of running jobs submitted via a local (non-GRID) interface.
   </td>
  </tr>
  <tr>
   <td>WaitingJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The number of jobs which are currently waiting to start execution, submitted via any type of interface (local and Grid). Usually these will be queued in the underlying Computing Manager (i.e., a Local Resource Managment System or LRMS).
   </td>
  </tr>
  <tr>
   <td>LocalWaitingJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The number of jobs which are currently waiting to start execution, submitted via a local (non-Grid) interface. Usually these will be queued in the underlying Computing Manager (i.e., a Local Resource Managment System or LRMS).
   </td>
  </tr>
  <tr>
   <td>SuspendedJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The number of jobs, submitted via any type of interface (local and Grid), which have started their execution, but are currently suspended (e.g., having been preempted by another job).
   </td>
  </tr>
  <tr>
   <td>LocalSuspendedJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The number of jobs, submitted via a local (non-Grid) interface, which have started their execution, but are currently suspended (e.g., having been preempted by another job).
   </td>
  </tr>
  <tr>
   <td>StagingJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The number of Grid jobs which are currently either staging files in before starting execution, or staging files out after finishing execution.
   </td>
  </tr>
  <tr>
   <td>PreLRMSWaitingJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The number of Grid jobs which are currently managed by the Grid software layer waiting to be passed to the underlying Computing Manager (LRMS), and hence are not yet candidates to start execution.
   </td>
  </tr>
  <tr>
   <td>EstimatedAverageWaitingTime
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>s
   </td>
   <td>An estimate of the average time a job will wait after submission until it starts to execute. The value SHOULD be reported as 0 if there are free slots and a new job will start immediately, even if it takes some finite time for a job to be started.
   </td>
  </tr>
  <tr>
   <td>EstimatedWorstWaitingTime
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>s
   </td>
   <td>An estimate of the worst-case time a job could wait after submission until it starts to execute. This would generally be based on an assumption that all existing jobs run to their maximum allowed time limits.
   </td>
  </tr>
  <tr>
   <td>FreeSlots
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>slot
   </td>
   <td>The number of slots which are currently unoccupied by jobs and are free for new jobs in this Share to start immediately.
   </td>
  </tr>
  <tr>
   <td>FreeSlotsWithDuration
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>slot:s
   </td>
   <td>The number of free slots with their time limits. Syntax: ns[:t] [ns:t]*, where the pair ns:t means that there are <em>ns</em> free slots for the duration of <em>t </em>(expressed in seconds); the time limit information is optional.
   </td>
  </tr>
  <tr>
   <td>UsedSlots
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>slot
   </td>
   <td>The number of slots currently occupied by running jobs.
   </td>
  </tr>
  <tr>
   <td>RequestedSlots
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>slot
   </td>
   <td>The number of slots which are needed to execute all currently waiting and staging jobs.
   </td>
  </tr>
  <tr>
   <td>ReservationPolicy
   </td>
   <td>ReservationPolicy_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The type of policy used for advance reservation, if any. 
   </td>
  </tr>
  <tr>
   <td>Tag
   </td>
   <td>String
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>A UserDomain-defined tag for this Share (the values SHOULD use a namespace based on the UserDomain name to avoid collision).
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingEndpoint.ID
<p>
[redefines Endpoint.ID]
   </td>
   <td>*
   </td>
   <td colspan="2" >A computing share MAY be consumed via one or more computing endpoints.
   </td>
  </tr>
  <tr>
   <td colspan="2" >ExecutionEnvironment.ID 
<p>
[redefines Resource.ID]                         
   </td>
   <td>*
   </td>
   <td colspan="2" >A computing share is defined on one or more computing resources.
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingService.ID   
<p>
[redefines Service.ID]                       
   </td>
   <td>1
   </td>
   <td colspan="2" >A computing share participates in a computing service.
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingActivity.ID
<p>
[redefines Activity.ID]
   </td>
   <td>*
   </td>
   <td colspan="2" >A computing share is being consumed by zero or more computing activities.
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingShareAcceleratorInfo.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >A computing share provides about the usage level of several accelerator devices.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
  <tr>
   <td colspan="2" >MappingPolicy.ID                     
   </td>
   <td>*
   </td>
   <td colspan="2" >A share has zero or more mapping policies.
   </td>
  </tr>
</table>


As regards CPU Time and Wallclock Time related properties, there is a need to have a way to normalize them depending on the computing capacity of the Execution Environment. The approach proposed in GLUE is to add two attributes in the Execution Environment (see Section 7.8) which refer to the scaling factor to be used to compute the CPU/Wallclock time limit that a job will get if it will be assigned to such an Execution Environment via a certain Share. It is important that a job SHOULD always get at least the advertised CPU/Wallclock time. This means that the reference Execution Environment for the normalization should be always the fastest (most powerful) among those available in the entire Computing Service. For this Execution Environment, the scaling factor MUST be equal to 1. The CPU/Wallclock time values published by a Share therefore refer to the time limit that the job will get when mapped to this Execution Environment. For the other Execution Environments, the time should be adjusted according to the published scaling factors.



    1.  ComputingShareAcceleratorInfo

The ComputingShareAcceleratorInfo class contains all the information about the usage level of  the accelerator device bound to the computing share.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>ComputingShareAcceleratorInfo
   </td>
   <td colspan="3" >Entity
   </td>
   <td>The usage level of the accelerator devices for a given computing share
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                            [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Type
   </td>
   <td><em>AccType_t</em>
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>The accelerator architecture type.
   </td>
  </tr>
  <tr>
   <td>FreeAcceleratorSlots
   </td>
   <td><em>UInt32</em>
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The number of accelerator cards slots which are currently unoccupied by jobs and are free for new jobs in this Share to start immediately
   </td>
  </tr>
  <tr>
   <td>UsedAcceleratorSlots
   </td>
   <td><em>UInt32</em>
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The number of accelerator cards slots currently occupied by running jobs. 
   </td>
  </tr>
  <tr>
   <td>MaxAcceleratorSlotsPerJob
   </td>
   <td><em>UInt32</em>
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The maximum number of accelerator card slots which could be allocated to a single job in this Share
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingShare. ID
   </td>
   <td>1
   </td>
   <td colspan="2" >A set of accelerator information is related to a computing share.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
</table>




    1.  ComputingManager

The `ComputingManager` class is a specialization of the `Manager` class for the computational capability. The `ComputingManager` is responsible for the local control of resources, and this layer is not exposed directly to external clients. The operating system might be the simplest case of a Computing Manager, but the `ComputingManager` is often realized by means of a Local Resource Management (LRMS) "batch" system. A Computing Service will usually only have one Computing Manager, but MAY have more. The class provides aggregated information on controlled resources, and also describes local storage extents accessible to jobs.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>ComputingManager
   </td>
   <td colspan="3" >Manager
   </td>
   <td>A software component locally managing one or more Execution Environments. It MAY also describe aggregated information about the managed resources. The computing manager is also known as a Local Resource Management System (LRMS).
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                            [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td><em>ProductName</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>Name of the software product adopted as manager</em>
   </td>
  </tr>
  <tr>
   <td><em>ProductVersion</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Version of the software product adopted as manager</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Reservation
   </td>
   <td>ExtendedBoolean_t 
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>True if the Computing Manager (i.e, LRMS) supports advance reservation of resources.
   </td>
  </tr>
  <tr>
   <td>BulkSubmission
   </td>
   <td>ExtendedBoolean_t 
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>True if the computing manager (i.e, LRMS) supports bulk submission of multiple jobs.
   </td>
  </tr>
  <tr>
   <td>TotalPhysicalCPUs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>Ph.CPU
   </td>
   <td>The total number of physical CPUs accessible via any of the available Endpoints and managed by this Computing Manager (there is one physical CPU per socket). This value SHOULD represent the total installed capacity, i.e. including resources which are temporarily unavailable.
   </td>
  </tr>
  <tr>
   <td>TotalLogicalCPUs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>Log.CPU
   </td>
   <td>The total number of logical CPUs accessible via any of the available Endpoints and managed by this Computing Manager (a logical CPU corresponds to a CPU visible to the operating system). This value SHOULD represent the total installed capacity, i.e. including resources which are temporarily unavailable.
   </td>
  </tr>
  <tr>
   <td>TotalSlots
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>slot
   </td>
   <td>The total number of slots managed by this Computing Manager which are currently available to run jobs.
   </td>
  </tr>
  <tr>
   <td>SlotsUsedByLocalJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>slot
   </td>
   <td>The number of slots currently occupied by jobs submitted via a local (non-Grid) interface.
   </td>
  </tr>
  <tr>
   <td>SlotsUsedByGridJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>slot
   </td>
   <td>The number of slots currently occupied by jobs submitted via a Grid interface.
   </td>
  </tr>
  <tr>
   <td>Homogeneous
   </td>
   <td>ExtendedBoolean_t 
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>True if this Computing Manager manages only one type of Execution Environment.
   </td>
  </tr>
  <tr>
   <td>NetworkInfo
   </td>
   <td>NetworkInfo_t
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>The type of internal network connection available among the managed Execution Environment instances. If many values are published then the various types of network MAY be available only within subsets of the Execution Environment instances; the Execution Environment properties SHOULD publish this information.
   </td>
  </tr>
  <tr>
   <td>LogicalCPUDistribution
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>A classification of the managed Execution Environment instances aggregated by the number of logical CPUs. Syntax: X<em>1</em>:Y<em>1</em>, …, X<em>n</em>:Y<em>n,</em> where I is the i-<em>th</em> group of Execution Environments with the same number of logical CPUs, X<em>i </em>is the number of logical CPUs in each Execution Environment instance and Y<em>i </em>is the number of Execution Environment instances. 
   </td>
  </tr>
  <tr>
   <td>WorkingAreaShared
   </td>
   <td>ExtendedBoolean_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>True if the working area (see below) is shared across different Execution Environment instances (i.e., cluster nodes), typically via an NFS mount; this attribute applies to single-slot jobs.
   </td>
  </tr>
  <tr>
   <td>WorkingAreaGuaranteed
   </td>
   <td>ExtendedBoolean_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>True if the job is guaranteed the full extent of the WorkingAreaTotal; this attribute applies to single-slot jobs.
   </td>
  </tr>
  <tr>
   <td>WorkingAreaTotal
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>GB
   </td>
   <td>Total size of the working area (see below) available to all single-slot Grid jobs, either as a shared area across all the Execution Environments (WorkingAreaShared is true) or local to each Execution Environment (WorkingAreaShared is false). If the Computing Manager supports individual  quotas per job/user, this is not advertised. In the case of a non-shared working area with a different local space allocation on each node, the advertised total size SHOULD be the minimum available across all the Execution Environment instances.
   </td>
  </tr>
  <tr>
   <td>WorkingAreaFree
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>GB
   </td>
   <td>The amount of free space currently available in the working area (see below), available to all single-slot Grid jobs either as a shared area across all the Execution Environments (WorkingAreaShared is true) or local to each Execution Environment (WorkingAreaShared is false). If the computing manager supports individual  quotas per job/user, this is not advertised. In the case of a non-shared and non-guaranteed working area, this attribute SHOULD represent the minimum free working area currently available in any Execution Environment instance. In the case of a non-shared and guaranteed working area, the free size SHOULD equal the total size.
   </td>
  </tr>
  <tr>
   <td>WorkingAreaLifeTime
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>s
   </td>
   <td>The minimum guaranteed lifetime of the files created by single-slot Grid jobs in the working area (see below); the lifetime is related to the end time of the job.  After the expiration of this lifetime, the files are not guaranteed to exist.
   </td>
  </tr>
  <tr>
   <td>WorkingAreaMultiSlotTotal
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>GB
   </td>
   <td>The total size of the working area (see below) available to all the multi-slot Grid jobs shared across all the Execution Environments. If the Computing Manager supports individual quotas per job/user, this is not advertised.
   </td>
  </tr>
  <tr>
   <td>WorkingAreaMultiSlotFree
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>GB
   </td>
   <td>The amount of free space currently available in the working area (see below) available to all multi-slot Grid jobs shared across all the Execution Environments. If the Computing Manager supports individual  quotas per job/user, this is not advertised. This attribute SHOULD represent the minimum free working area currently available in any Execution Environment instance.
   </td>
  </tr>
  <tr>
   <td>WorkingAreaMultiSlotLifeTime
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>s
   </td>
   <td>The minimum guaranteed lifetime of the files created by multi-slot Grid jobs in the working area (see below); the lifetime is related to the end time of the job. After the expiration of the lifetime, the files are not guaranteed to exist.
   </td>
  </tr>
  <tr>
   <td>CacheTotal
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>GB
   </td>
   <td>If local caching of input files is supported, this attribute represents the total size of a shared storage area where frequently accessed data MAY be stored for rapid access by subsequent Grid jobs; in this area, files are kept after job completion for a certain amount of time, depending on the caching algorithm.
   </td>
  </tr>
  <tr>
   <td>CacheFree
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>GB
   </td>
   <td>If local caching of input files is supported, this attribute represents the free space in a shared storage area where frequently accessed data MAY be stored for rapid access by subsequent Grid jobs. In the computation of the free size, files which are not claimed by any job MAY be considered as deleted.
   </td>
  </tr>
  <tr>
   <td>TmpDir
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The absolute path of a temporary directory local to an Execution Environment instance (i.e., a worker node). This directory MUST be available to programs using the normal file access primitives (open/read/write/close). Any files in the directory MAY be deleted as soon as the job which created them finishes.
   </td>
  </tr>
  <tr>
   <td>ScratchDir
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The absolute path of a shared directory available for application data. Typically this is a POSIX accessible transient disk space shared between the Execution Environment instances, e.g. via an NFS mount. It MAY be used by MPI applications or to store intermediate files that need further processing by local jobs or as a staging area, especially if the Execution Environment instances have no internet connectivity. Any files in the directory MAY be deleted as soon as the job which created them finishes.
   </td>
  </tr>
  <tr>
   <td>ApplicationDir
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The path of a directory available for installation of persistent application software and data.  Typically this will be a POSIX accessible disk space, e.g. an NFS mount, with a long-term allocation of space to supported User Domains. The detailed usage of such a space SHOULD be described in a profile document for a specific Grid infrastructure.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingService.ID                          
<p>
[redefines Service.ID]
   </td>
   <td>1
   </td>
   <td colspan="2" >A computing manager participates in a computing service.
   </td>
  </tr>
  <tr>
   <td colspan="2" >ExecutionEnvironment.ID             
<p>
[redefines Resource.ID]
   </td>
   <td>1..*
   </td>
   <td colspan="2" >A computing manager manages one or more execution environments.
   </td>
  </tr>
  <tr>
   <td colspan="2" >ApplicationEnvironment.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >A computing manager MAY use zero or more application environments.
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingManagerAcceleratorInfo
   </td>
   <td>*
   </td>
   <td colspan="2" >A computing manager MAY display information about the usage level of the accelerator devices installed in the cluster. 
   </td>
  </tr>
  <tr>
   <td colspan="2" >Benchmark.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >A computing manager has zero or more associated benchmarks.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
</table>


As regards the WorkingArea-related attributes and single-slot jobs, four scenarios should be considered. Both scenarios and the related attribute values are presented in Table 1.

**Table 1 Working Area and Single-slot jobs scenarios**


<table>
  <tr>
   <td>Working Area
   </td>
   <td>Shared
   </td>
   <td>Guaranteed
   </td>
  </tr>
  <tr>
   <td>One working area shared across all the Execution Environments and shared among simultaneous jobs.
   </td>
   <td>true
   </td>
   <td>false
   </td>
  </tr>
  <tr>
   <td>One working area shared across all the Execution Environments with a guaranteed quota for each job.
   </td>
   <td>true
   </td>
   <td>true
   </td>
  </tr>
  <tr>
   <td>A working area local to each Execution Environment, but shared among all the jobs which run simultaneously in those Execution Environments.
   </td>
   <td>false
   </td>
   <td>false
   </td>
  </tr>
  <tr>
   <td>A working area local to each Execution Environment and dedicated to each job.
   </td>
   <td>false
   </td>
   <td>true
   </td>
  </tr>
</table>


In case there is a dedicated working area for multi-slot jobs, this SHOULD be represented by the WorkingAreaMultiSlot* attributes. In case there is no dedicated working area for multi-slot jobs, i.e., there is a common working area for both single-slot and multi-slot jobs, we RECOMMEND to publish only the attributes related to the working area for single-slot jobs.



    1.  ComputingManagerAcceleratorInfo

The ComputingManagerAcceleratorInfo contains information about the accelerator device handled by the computing manager.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>ComputingManagerAcceleratorInfo
   </td>
   <td colspan="3" >Entity
   </td>
   <td>The information about the accelerator device handled by the computing manager.
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                            [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Type
   </td>
   <td><em>AccType_t</em>
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>The accelerator architecture type. 
   </td>
  </tr>
  <tr>
   <td>TotalPhysicalAccelerators
   </td>
   <td><em>UInt32</em>
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The total number of physical Accelerator cards accessible via any of the available Endpoints and managed by this Computing Manager. This value SHOULD represent the total installed capacity, i.e. including resources which are temporarily unavailable.
   </td>
  </tr>
  <tr>
   <td>TotalAcceleratorSlots
   </td>
   <td><em>UInt32</em>
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The total number of Accelerator card slots managed by this Computing Manager which are currently available to run jobs.
   </td>
  </tr>
  <tr>
   <td>UsedAcceleratorSlots
   </td>
   <td><em>UInt32</em>
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The total number of slots currently occupied by jobs. 
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingManager. ID
   </td>
   <td>1
   </td>
   <td colspan="2" >A set of accelerator information is related to a computing manager.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
</table>




    1.  Benchmark

The `Benchmark` class characterizes the relative performance of the computing resource by providing the result of a specific benchmark suite executed on the computing resource underlying the Computing Service. The `Benchmark` class provides the both the type and the value of the benchmark.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Benchmark
   </td>
   <td colspan="3" >Entity
   </td>
   <td>Benchmark information either about an Execution Environment providing computing capacity or about a CloudComputingInstanceType providing cloud computing capacity
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                            [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Type
   </td>
   <td>Benchmark_t
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>The type of benchmark.
   </td>
  </tr>
  <tr>
   <td>Value
   </td>
   <td>Real32
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>The benchmark value.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >ExecutionEnvironment.ID
   </td>
   <td>0..1
   </td>
   <td colspan="2" >A benchmark MAY be related to an execution environment.
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingManager. ID
   </td>
   <td>0..1
   </td>
   <td colspan="2" >A benchmark MAY be related to a computing resource.
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingInstanceType.ID
   </td>
   <td>0..1
   </td>
   <td colspan="2" >A benchmark MAY be related to a cloud computing instance type.
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingManager.ID
   </td>
   <td>0..1
   </td>
   <td colspan="2" >A benchmark MAY be related to a cloud computing resource.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
</table>




    1.  ExecutionEnvironment

The `ExecutionEnvironment` class describes the hardware and operating system environment in which a job will run. It represents a set of homogeneous Worker Nodes, so if a computing system contains nodes with significantly different properties there MAY be several `ExecutionEnvironment` instances. This implies that it should be possible to request a specific environment when a job is submitted. The `ExecutionEnvironment` MAY refer to virtual rather than physical machines.

As well as attributes describing a typical node, the class gives summary information about the size and usage of the set of nodes which possess those properties. However, there is no way to relate these to the information in other entities, e.g. it is not possible to know which jobs in a given `ComputingShare` are running on which `ExecutionEnvironment`.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>ExecutionEnvironment
   </td>
   <td colspan="3" >Resource
   </td>
   <td>A type of environment available to and requestable by a Grid job when submitted to a ComputingService via a Computing Endpoint; the type of environment is described in terms of hardware, operating system and network characteristics. Information about the total/available/used instances of this type of execution environment are also included.
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                               [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Platform
   </td>
   <td>Platform_t
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>The platform architecture of this Execution Environment.
   </td>
  </tr>
  <tr>
   <td>VirtualMachine
   </td>
   <td>ExtendedBoolean_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>True if the Execution Environment is hosted within a virtual machine; in this case, the values of the other attributes are related to the virtualized environment and not to the hosting environment.
   </td>
  </tr>
  <tr>
   <td>TotalInstances
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The total number of Execution Environment instances. This SHOULD reflect the total installed capacity, i.e. including resources which are temporarily unavailable.
   </td>
  </tr>
  <tr>
   <td>UsedInstances
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The number of Execution Environment instances which are considered to be fully used; an instance is used when, according to the policies of the Computing Manager (i.e., LRMS), it cannot accept new jobs because it already runs the maximum number of allowed jobs.
   </td>
  </tr>
  <tr>
   <td>UnavailableInstances
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The number of Execution Environment instances which are currently unavailable, e.g. because of failures or maintenance.
   </td>
  </tr>
  <tr>
   <td>PhysicalCPUs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The number of physical CPUs in one ExecutionEnvironment instance, i.e. the number of sockets per Worker Node.
   </td>
  </tr>
  <tr>
   <td>LogicalCPUs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The number of logical CPUs in one Execution Environment instance, i.e. typically the number of cores per Worker Node.
   </td>
  </tr>
  <tr>
   <td>CPUMultiplicity
   </td>
   <td>CPUMultiplicity_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>Condensed information about the multiplicity of both physical CPUs and cores available in an execution environment instance..
   </td>
  </tr>
  <tr>
   <td>CPUVendor
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The name of the physical CPU vendor. Free format, but it SHOULD correspond to the name by which the vendor is generally known.
   </td>
  </tr>
  <tr>
   <td>CPUModel
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The name of the physical CPU model, as defined by the vendor.
   </td>
  </tr>
  <tr>
   <td>CPUVersion
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The specific version of the Physical CPU model, as defined by the vendor.
   </td>
  </tr>
  <tr>
   <td>CPUClockSpeed
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>MHz
   </td>
   <td>The nominal clock speed of the physical CPU.
   </td>
  </tr>
  <tr>
   <td>CPUTimeScalingFactor
   </td>
   <td>Real32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The factor used by the Computing Manager (i.e., LRMS) to scale the CPU time limit (the CPU Time is divided by the CPUTimeScalingFactor); for the reference execution environment, this attribute is equal to 1. See the description of the ComputingShare for further information.
   </td>
  </tr>
  <tr>
   <td>WallTimeScalingFactor
   </td>
   <td>Real32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The factor used by the Computing Manager (i.e., LRMS) to scale the Wallclock time limit (the Wallclock Time is divided by the WallTimeScalingFactor). See the description of the ComputingShare for further information.
   </td>
  </tr>
  <tr>
   <td>ConnectivityOut
   </td>
   <td>ExtendedBoolean_t
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>True if direct outbound network connectivity is available from a running job, even if limited, e.g. by firewall rules.
   </td>
  </tr>
  <tr>
   <td>NetworkInfo
   </td>
   <td>NetworkInfo_t
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>The type of internal network connection available among the Execution Environment instances.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingManager.ID                           
<p>
[redefines Manager.ID]
   </td>
   <td>1
   </td>
   <td colspan="2" >An execution environment is managed by a computing manager.
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingShare.ID                                 
<p>
[redefines Share.ID]
   </td>
   <td>*
   </td>
   <td colspan="2" >An execution environment provides capacity in terms of computing shares.
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingActivity.ID
<p>
[redefines Activity.ID]
   </td>
   <td>*
   </td>
   <td colspan="2" >An execution environment runs zero or more computing activities.
   </td>
  </tr>
  <tr>
   <td colspan="2" >AcceleratorEnvironment.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >An execution environment MAY contains zero or more accelerator environments.
   </td>
  </tr>
  <tr>
   <td colspan="2" >ApplicationEnvironment.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >An execution environment offers zero or more application environments.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Benchmark.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >An execution environment has zero or more associated benchmarks.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
</table>


Each Execution Environment instance is under the control of a Computing Manager (i.e., LRMS). An Execution Environment MAY be realized in several ways. Examples are a physical computing node, or a virtual machine image that MAY be requestable by a job (different virtual machine images MAY coexist on the same physical node). 



        1.  AcceleratorEnvironment

The AcceleratorEnvironment is an entity used to describe an homogeneous set of accelerator processors. This entity is associated with one or more execution environments.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>AcceleratorEnvironment
   </td>
   <td colspan="3" >Entity
   </td>
   <td>Description of the accelerator device
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                            [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Type
   </td>
   <td><em>AccType_t</em>
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>The type of Accelerator.
   </td>
  </tr>
  <tr>
   <td>PhysicalAccelerators
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The number of physical Accelerators in one ExecutionEnvironment instance, i.e. the number of accelerator cards per Worker Node.
   </td>
  </tr>
  <tr>
   <td>LogicalAccelerators
   </td>
   <td>UInt32
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>The number of logical Accelerators in one Execution Environment instance, i.e. typically the number of cores per all the accelerator cards per Worker Node.
   </td>
  </tr>
  <tr>
   <td>Vendor
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The name of the physical Accelerator vendor. Free format, but it SHOULD correspond to the name by which the vendor is generally known.
   </td>
  </tr>
  <tr>
   <td>Model
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The name of the physical Accelerator model, as defined by the vendor.
   </td>
  </tr>
  <tr>
   <td>Version
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The specific version of the Physical Accelerator model, as defined by the vendor.
   </td>
  </tr>
  <tr>
   <td>ClockSpeed
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>MHz
   </td>
   <td>The nominal clock speed of the physical Accelerator.
   </td>
  </tr>
  <tr>
   <td>Memory
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>MB
   </td>
   <td>The nominal memory size of the physical Accelerator
   </td>
  </tr>
  <tr>
   <td>ComputeCapability
   </td>
   <td>String
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>Compute Capability describes the features supported by an accelerator hardware
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >ExecutionEnvironment.ID
   </td>
   <td>1..*
   </td>
   <td colspan="2" >An accelerator environment MAY be associated with one or more execution environments.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
</table>




    1.  ApplicationEnvironment

The `ApplicationEnvironment` class describes the software environment in which a job will run, i.e. what pre-installed software will be available to it. Each Application is identified by a name (the AppName attribute); these names are not defined within the schema, but SHOULD be assigned in a way which allows applications to be uniquely identified. In some deployment scenarios, the definition of namespace-based AppNames or guidelines for the generation of unique application names MAY be specified, and application repository services relying on those application names MAY be provided. This aspect is considered out of scope for the GLUE schema specification, but MAY be included in a profile document for a specific production Grid.

The Application Environment can be used to describe installed application software or special environment setups in terms of a simple tag string. In this case, the AppName attribute should be used to publish this tag; other attributes are optional.

The properties of installed software may vary substantially, but the attributes of the class cover the most common cases, in particular for licensed software. If necessary, additional information MAY be added using the `OtherInfo` attribute and the `Extension` class.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>ApplicationEnvironment
   </td>
   <td colspan="3" >Entity
   </td>
   <td>A description of installed application software or software environment characteristics available within one or more Execution Environments.
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                          [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>AppName
   </td>
   <td>String
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>The name of the application or environment.
   </td>
  </tr>
  <tr>
   <td>AppVersion
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The version of the application or environment, as defined by the supplier.
   </td>
  </tr>
  <tr>
   <td>Repository
   </td>
   <td>URL
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The URL of a service which offers a name service and/or a repository for this application environment. Application environments can be categorized under namespaces maintained by application repositories.
   </td>
  </tr>
  <tr>
   <td>State
   </td>
   <td>AppEnvState_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The current installation state of the application. 
   </td>
  </tr>
  <tr>
   <td>RemovalDate
   </td>
   <td>DateTime_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The date and time after which the application MAY be removed.
   </td>
  </tr>
  <tr>
   <td>License
   </td>
   <td>License_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The type of license under which the application is usable.
   </td>
  </tr>
  <tr>
   <td>Description
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>A human-readable description of this application or environment.
   </td>
  </tr>
  <tr>
   <td>BestBenchmark
   </td>
   <td>Benchmark_t
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>The type of benchmark which best identifies the sensitivity of this application to the performance of the Execution Environment, which can be compared with the rating published via the Benchmark class.
   </td>
  </tr>
  <tr>
   <td>ParallelSupport
   </td>
   <td>ParallelSupport_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The type of supported parallel execution framework.
   </td>
  </tr>
  <tr>
   <td>MaxSlots
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>slot
   </td>
   <td>The maximum number of concurrent slots that may be used to run jobs using the application.
   </td>
  </tr>
  <tr>
   <td>MaxJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>job
   </td>
   <td>The maximum number of concurrent jobs that may use the application.
   </td>
  </tr>
  <tr>
   <td>MaxUserSeats
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>user seat
   </td>
   <td>The maximum number of concurrent user seats (i.e. distinct users) that may use the application.
   </td>
  </tr>
  <tr>
   <td>FreeSlots
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>slot
   </td>
   <td>The number of slots currently available to run jobs using the application.
   </td>
  </tr>
  <tr>
   <td>FreeJobs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>slot
   </td>
   <td>The number of jobs that could immediately start their execution using the application.
   </td>
  </tr>
  <tr>
   <td>FreeUserSeats
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>user seat
   </td>
   <td>The current number of free seats for additional users to use the application.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >ExecutionEnvironment.ID                           
   </td>
   <td>*
   </td>
   <td colspan="2" >An application environment MAY be used in zero or more execution environments.
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingManager.ID
   </td>
   <td>1
   </td>
   <td colspan="2" >An application environment is part of a computing manager.
   </td>
  </tr>
  <tr>
   <td colspan="2" >ApplicationHandle.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >An application environment MAY be handled via zero or more application handles.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
</table>




    1.  ApplicationHandle

The `ApplicationHandle` class is an extension to `ApplicationEnvironment` for applications which need to be set up in some way before they can be used. For each supported setup method a string MAY be specified, the interpretation of which is specific to the method - in the simplest case this could just be a setup script to execute. A single Application MAY support multiple setup methods.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>ApplicationHandle
   </td>
   <td colspan="3" >Entity
   </td>
   <td>The description of a technique for bootstrapping and/or accessing an application environment.
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                          [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Type
   </td>
   <td>ApplicationHandle_t
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>The type of method used to set up this application environment.
   </td>
  </tr>
  <tr>
   <td>Value
   </td>
   <td>String
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>A string which defines how to set up this application in the context of the setup method specified by the Type.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >ApplicationEnvironment.ID
   </td>
   <td>1
   </td>
   <td colspan="2" >An application handle MAY be used for one application environment.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
</table>




    1.  ComputingActivity

The `ComputingActivity` class represents a single (but possibly multi-processor) job. The attributes give the job properties and state as seen by the local batch system, together with some Grid-level information.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>ComputingActivity
   </td>
   <td colspan="3" >Activity
   </td>
   <td>An Activity managed by an OGSA execution capability service (the Computing Activity is traditionally called a job).
   </td>
  </tr>
  <tr>
   <td><em>Inherited Attribute</em>
   </td>
   <td><em>Type</em>
   </td>
   <td><em>Mult</em>
   </td>
   <td><em>Unit</em>
   </td>
   <td><em>Description</em>
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                                                [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Type
   </td>
   <td>ComputingActivityType_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The type of this Computing Activity.
   </td>
  </tr>
  <tr>
   <td>IDFromEndpoint
   </td>
   <td>URI
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The job ID as assigned by the Computing Endpoint.
   </td>
  </tr>
  <tr>
   <td>LocalIDFromManager
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The local ID of the job as assigned by the Computing Manager (i.e., LRMS).
   </td>
  </tr>
  <tr>
   <td>JobDescription
   </td>
   <td>JobDescription_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The job description language used to specify the job request.
   </td>
  </tr>
  <tr>
   <td>State
   </td>
   <td>ComputingActivityState_t
   </td>
   <td>1..*
   </td>
   <td>
   </td>
   <td>The state of the job; different state models are allowed; a state for each model is allowed provided that it has a different namespace prefix (see data type definition)
   </td>
  </tr>
  <tr>
   <td>RestartState
   </td>
   <td>ComputingActivityState_t
   </td>
   <td>0..*
   </td>
   <td>
   </td>
   <td>The state from which a failed job MAY restart upon a client request;  different state models are allowed; a state for each model is allowed provided that it has a different namespace prefix (see data type definition)
   </td>
  </tr>
  <tr>
   <td>ExitCode
   </td>
   <td>Int32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The exit code as returned by the main executable code or script of the job.
   </td>
  </tr>
  <tr>
   <td>ComputingManagerExitCode
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The exit code provided by the Computing Manager (i.e., LRMS).
   </td>
  </tr>
  <tr>
   <td>Error
   </td>
   <td>String
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>Error messages as provided by the software components involved in the management of the job.
   </td>
  </tr>
  <tr>
   <td>WaitingPosition
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>For a waiting job being queued in the Computing Manager (i.e., LRMS), the position of the job in the queue.
   </td>
  </tr>
  <tr>
   <td>UserDomain
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The User Domain specified by the job owner in the job submission request. The owner MAY belong to several User Domains, but typically decides which one to choose when submitting a job.
   </td>
  </tr>
  <tr>
   <td>Owner
   </td>
   <td>String
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>The Grid identity of the job's owner; in the case that anonymity is required, the reserved value CONFIDENTIAL should be advertised.
   </td>
  </tr>
  <tr>
   <td>LocalOwner
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The local user name to which the  job's owner is mapped for the execution of this job.
   </td>
  </tr>
  <tr>
   <td>RequestedTotalWallTime
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>s
   </td>
   <td>The total wall clock time requested by the job; for multi-slot jobs, it represents the sum of wall clock times needed for each required slot. 
   </td>
  </tr>
  <tr>
   <td>RequestedTotalCPUTime
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>s
   </td>
   <td>The total CPU time requested by the job; for multi-slot jobs, it represents the sum of CPU times needed for each required slot.
   </td>
  </tr>
  <tr>
   <td>RequestedSlots
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>slot
   </td>
   <td>The number of slots requested for this job.
   </td>
  </tr>
  <tr>
   <td>RequestedApplicationEnvironment
   </td>
   <td>String
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>A serialization of the AppName and Version of the requested Application Environments (the serialization syntax is delegated to the implementation).
   </td>
  </tr>
  <tr>
   <td>StdIn
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The name of the file which is used as the standard input of the job.
   </td>
  </tr>
  <tr>
   <td>StdOut
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The name of the file which contains the standard output of the job.
   </td>
  </tr>
  <tr>
   <td>StdErr
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The name of the file which contains the standard error of the job.
   </td>
  </tr>
  <tr>
   <td>LogDir
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The name of the directory which contains the logs related to the job and generated by the Grid layer (usually the directory is private to the job).
   </td>
  </tr>
  <tr>
   <td>ExecutionNode
   </td>
   <td>String
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>A hostname associated to the Execution Environment instance (i.e., worker node) running the job; multi-node jobs are described by several instances of this attribute.
   </td>
  </tr>
  <tr>
   <td>Queue
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The name of the Computing Manager (i.e, LRMS) queue in which this job was queued before execution.
   </td>
  </tr>
  <tr>
   <td>UsedTotalWallTime
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>s
   </td>
   <td>The total wall clock time consumed so far by the job. In case of multi-slot jobs, this value refers to the sum of the wall clock time consumed in each slot.
   </td>
  </tr>
  <tr>
   <td>UsedTotalCPUTime
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>s
   </td>
   <td>The total CPU time consumed so far by the job. In case of multi-slot jobs, this value refers to the sum of the CPU time consumed in each slot.
   </td>
  </tr>
  <tr>
   <td>UsedMainMemory
   </td>
   <td>UInt64
   </td>
   <td>0..1
   </td>
   <td>MB
   </td>
   <td>The physical RAM currently used by the job.
   </td>
  </tr>
  <tr>
   <td>SubmissionTime
   </td>
   <td>DateTime_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The time when the job was submitted to the Computing Endpoint.
   </td>
  </tr>
  <tr>
   <td>ComputingManagerSubmissionTime
   </td>
   <td>DateTime_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The time when the job was submitted to the Computing Manager (i.e., LRMS) by the Grid layer.
   </td>
  </tr>
  <tr>
   <td>StartTime
   </td>
   <td>DateTime_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The time when the job entered the Computing Manager (i.e., LRMS)  running state.
   </td>
  </tr>
  <tr>
   <td>ComputingManagerEndTime
   </td>
   <td>DateTime_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The time when the job entered its final Computing Manager (i.e., LRMS) state.
   </td>
  </tr>
  <tr>
   <td>EndTime
   </td>
   <td>DateTime_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The time when the job entered its final state as recorded by the Grid layer.
   </td>
  </tr>
  <tr>
   <td>WorkingAreaEraseTime
   </td>
   <td>DateTime_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>A working area is an allocated storage extent that holds the home directories of the Grid jobs; this attribute specifies the time when the dedicated working area of this job will be removed.
   </td>
  </tr>
  <tr>
   <td>ProxyExpirationTime
   </td>
   <td>DateTime_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The expiration time of the Grid proxy currently associated with the job; in case of a proxy with attribute certificates having different expiration times, then this value represent the minimum expiration time among all the values.
   </td>
  </tr>
  <tr>
   <td>SubmissionHost
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The name of the host from which the job was submitted.
   </td>
  </tr>
  <tr>
   <td>SubmissionClientName
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The name of the software client which was used to submit the job.
   </td>
  </tr>
  <tr>
   <td>OtherMessages
   </td>
   <td>String
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>Optional job messages provided by either the Grid Layer or the Computing Manager (i.e., LRMS).
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingEndpoint.ID                          
<p>
[redefines Endpoint.ID]
   </td>
   <td>0..1
   </td>
   <td colspan="2" >A computing activity is submitted to a computing endpoint.
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingShare.ID        
<p>
[redefines Share.ID]
   </td>
   <td>0..1
   </td>
   <td colspan="2" >A computing activity is mapped into a computing share.
   </td>
  </tr>
  <tr>
   <td colspan="2" >ExecutionEnvironment.ID
<p>
[redefines Resource.ID]
   </td>
   <td>0..1
   </td>
   <td colspan="2" >A computing activity is executed in an execution environment.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
  <tr>
   <td colspan="2" >UserDomain.ID
   </td>
   <td>0..1
   </td>
   <td colspan="2" >An activity is managed by a user domain.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Activity.ID                                
   </td>
   <td>*
   </td>
   <td colspan="2" >An activity is related to zero or more activities.
   </td>
  </tr>
</table>


In this specification, the Computing Activity may refer to simple jobs, or to elements of collections or workflows. The description of the relationships between jobs which are part of a collection or workflow may be considered in future revisions of the specification. 

As regards the State attribute and the related ComputingActivityState_t type, we note that currently there is no commonly accepted state model for Grid jobs. Each production Grid middleware defines and is using its own state model. As regards the standardization process, the OGSA-BES specification defines a simple state model. The middleware providers have started to define their own extensions to the BES state model, but they differ and do not enable interoperability. Given the current scenario, we RECOMMEND to use namespaces in state model values, so that every middleware provider MAY publish the Computing Activity State according to its definition. We expect that an extension to the core BES state model common to all the middleware providers and suitable for production scenarios may be defined by a profiling activity of the BES/ JSDL/GLUE specifications.



    1.  ToStorageService

The `ToStorageService` class represents the case where a filesystem from a Storage Service is available to jobs running on a Computing Service via POSIX access, e.g. as an NFS mount. Each `ToStorageService` instance represents a single mount point. It is assumed that such mounts are available on all nodes (i.e. all Execution Environments) in the Computing Service.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>ToStorageService
   </td>
   <td colspan="3" >Entity
   </td>
   <td>The description of POSIX access via a file system technology enabling jobs running in the Computing Service to access an associated Storage Service.
   </td>
  </tr>
  <tr>
   <td><em>Inherited Attribute</em>
   </td>
   <td><em>Type</em>
   </td>
   <td><em>Mult</em>
   </td>
   <td><em>Unit</em>
   </td>
   <td><em>Description</em>
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                            [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>LocalPath
   </td>
   <td>String
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>The local path within the Computing Service which makes it possible to access files in the associated Storage Service (this is typically an NFS mount point).
   </td>
  </tr>
  <tr>
   <td>RemotePath
   </td>
   <td>String
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>The remote path in the Storage Service which is associated to the local path in the Computing Service (this is typically an NFS exported directory).
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >ComputingService.ID
   </td>
   <td>1
   </td>
   <td colspan="2" >Is associated to a computing service.
   </td>
  </tr>
  <tr>
   <td colspan="2" >StorageService.ID
   </td>
   <td>1
   </td>
   <td colspan="2" >Is associated to a storage service.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
</table>




1.  **Conceptual Model of the Cloud Computing Service**

The conceptual model of the Cloud Infrastructure as a Service Compute Service is based on the main entities and uses specializations of the `Service`, `Endpoint`, `Share`, `Manager` and `Resource`.  Further cloud computing related concepts such as `Compute Image`, `Compute Price` and `Benchmark` are introduced. 


![Figure 3 Entities and relationships for the Cloud Compute Service conceptual model](images/glue2-1-draft-v0-5-doc2.png "Figure 3 Entities and relationships for the Cloud Compute Service conceptual model")


**Figure 3 Entities and relationships for the Cloud Compute Service conceptual model.**

In this section, we extensively use the concepts of Virtual Machine (VM), Virtual Machine status (halted, pending, running, suspended), Hypervisor and Cloud Middleware, these are defined as follows:



*   A Virtual Machine (instance) is a compute environment that includes a platform operating system and an application layer. Every VM is a fully functioning virtual computer which can be accessed via the network. The VM has a given set of virtual CPU, RAM and disk resources. The main virtual disk is usually associated to a pre-set disk image, which contains the operating system to boot in the machine. The VM has usually one or more virtual network interfaces, to which are assigned public or private IPs.
*   A Virtual Machine is in Running state when the VM is actively consuming system resources in terms of RAM, CPU, disk and network. Some of the physical resources may be shared with other VMs or reserved for private VM usage.
*   A Virtual Machine is in Suspended state when the VM is not running, but it still has resources reserved on the system. A VM in suspended state usually consumes only disk space for the OS, and optionally additional disk space for RAM snapshot.
*   A Virtual Machine is in Pending state when the VM is in the process of gathering resources from the system (ex. acquiring VM OS disk, CPU resources, initializing syste). Machines in Pending state uses system resources but are not jet available for users to access.
*   A Virtual Machine is in Halted state when the VM has uses no resources in the system, but its template and configuration is still stored into the system (so the machine may be started again, but with a clean configuration).
*   An Hypervisor, usual name for Virtual Machine Manager, is a piece of computer software, firmware or hardware that creates, runs and manages Virtual Machines
*   A Cloud Middleware is a piece of computer software that leverages on hypervisor virtualization capabilities to provide Virtual Machines on-demand to final users. The Cloud Middleware may provide not only virtual servers (namely Infrastructure as a Service feature), but also storage (Storage as a Service) and other rich services (Platform as a Service, etc…).

Throughout the specification, we also use the concept of Cloud Storage extent to mean the capabilities and management of the various media that exist to store data and allow data retrieval.

In the model, the Cloud service price is represented via separated `CloudComputingPrice` entities associated to single accounted resources (eg. CPU, Memory, Disk, Network IN/OUT, Software Licensing). Each resource price is calculated on consumption or fixed fee basis and targeted to a give user base (eg. commercial, no-profit organizations, research). The total price for a `CloudComputingInstance` can be obtained by adding all the price elements from the associated `CloudComputingImage` and `CloudComputingInstanceType`.

A Cloud Computing service relates directly to a Cloud Infrastructure-as-a-Service (IaaS) system, which allows the user to run on-demand Virtual Appliances for computing purposes. For different Cloud computing services such as Platoform-as-a-Service and Software-as-a-Service, the generic Grid platform computing model (GLUE2 Computing entities), bed in Chapter 7, may be a better fit.



    1.  CloudComputingService

 \
The `CloudComputingService` class is a specialization of the `Service` class for a service offering Cloud Infrastructure as a Service computational capacity. The `CloudComputingService` entity is the main logical unit, and aggregation point for several entities together modeling a computing infrastructure capability in a Cloud system. A `CloudComputingService` is capable of executing `CloudComputingInstance` on its associated resources. The resources behind the `CloudComputingService` are described via the `CloudComputingManager`, `CloudComputingInstanceType`, `CloudComputingImage` and `Benchmark` entities. The governing policies and status of the resources are given by the `CloudComputingShare` elements. The `CloudComputingInstance` of a `CloudComputingService` are submitted and controlled via a `CloudComputingEndpoint`.


<table>
  <tr>
   <td><strong>Entity</strong>
   </td>
   <td><strong>Inerits from</strong>
   </td>
   <td colspan="3" ><strong>Description</strong>
   </td>
  </tr>
  <tr>
   <td>CloudComputingService
   </td>
   <td>Service
   </td>
   <td colspan="3" >An abstracted, logical view of software and hardware components that participate in the creation of a computational capacity in a Cloud environment, in form of Cloud Virtual Machines instances. A Cloud Computing Service exposes zero or more Cloud Computing Endpoints having well-defined interfaces, zero or more Cloud Computing Shares and zero or more Cloud Computing Managers. 
<p>
The computing service is autonomous and denotes a weak aggregation among Computing Endpoints, the underlying Computing Managers and the defined Computing Shares. The Computing Service enables the identification of the whole set of entities providing the computing functionality with a persistent name.
   </td>
  </tr>
  <tr>
   <td><strong>Inherited Attribute</strong>
   </td>
   <td><strong>Type</strong>
   </td>
   <td><strong>Mult</strong>
   </td>
   <td><strong>Unit</strong>
   </td>
   <td><strong>Desciption</strong>
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed, the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                          [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><p style="text-align: right">
<em>1</em></p>

   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td><em>Capability</em>
   </td>
   <td><em>Capability_t</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>The provided capability according to the Open Grid Service Architecture (OGSA) architecture [OGF-GFD80] (this is the union of all values assigned to the capability attribute of the endpoints part of this service)</em>
   </td>
  </tr>
  <tr>
   <td><em>Type</em>
   </td>
   <td><em>ServiceType_t</em>
   </td>
   <td><p style="text-align: right">
<em>1</em></p>

   </td>
   <td>
   </td>
   <td><em>The type of service according to a namespace-based classification. Examples are org.openstack or org.opennebula</em>
   </td>
  </tr>
  <tr>
   <td><em>QualityLevel</em>
   </td>
   <td><em>QualityLevel_t</em>
   </td>
   <td><p style="text-align: right">
<em>1</em></p>

   </td>
   <td>
   </td>
   <td><em>Maturity of the service in terms of quality of the software components</em>
   </td>
  </tr>
  <tr>
   <td><em>StatusInfo</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Web page providing additional information like monitoring aspects </em>
   </td>
  </tr>
  <tr>
   <td><em>Complexity</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable summary description of the complexity in terms of the number of endpoint types, shares and resources. The syntax should be: endpointType=X, share=Y, resource=Z.</em>
   </td>
  </tr>
  <tr>
   <td><strong>Attribute</strong>
   </td>
   <td><strong>Type</strong>
   </td>
   <td><strong>Mult</strong>
   </td>
   <td><strong>Unit</strong>
   </td>
   <td><strong>Desciption</strong>
   </td>
  </tr>
  <tr>
   <td>TotalVM
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>Total number of VM known to the system (the sum of RunningVM, PendingVM, SuspendedVM and HaltedVM)
   </td>
  </tr>
  <tr>
   <td>RunningVM
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The number of VM in Running state (VMs actively consuming the system resources)
   </td>
  </tr>
  <tr>
   <td>PendingVM
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The number of VM in Pending state (VM in preparation to be running on the system)
   </td>
  </tr>
  <tr>
   <td>SuspendedVM
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The number of VM in Suspended state (VMs not running but with reserved resources on the system)
   </td>
  </tr>
  <tr>
   <td>HaltedVM
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The number of VM in Halted state (VMs not running on the system with no resources reserved)
   </td>
  </tr>
  <tr>
   <td>AUP
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>Link to the service Acceptable User Policy (AUP) or Terms and Conditions for the usage of the service. This shall be in URL format.
   </td>
  </tr>
  <tr>
   <td>Association End
   </td>
   <td>Mult.
   </td>
   <td> 
   </td>
   <td> 
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>CloudComputingEndpoint.ID
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>A CloudComputingService is associated with zero or more endpoints (interfaces)
   </td>
  </tr>
  <tr>
   <td>CloudComputingShare.ID
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>A CloudComputingService offers zero or more computing shares.
   </td>
  </tr>
  <tr>
   <td>CloudComputingManager.ID
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>A CloudComputingService offers zero or more computing manager.
   </td>
  </tr>
  <tr>
   <td>Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td> 
   </td>
   <td> 
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Extension.Key
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>The entity MAY be extended via key-value pairs.
   </td>
  </tr>
  <tr>
   <td>Contact.ID
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>A Cloud computing service has zero or more contacts.
   </td>
  </tr>
  <tr>
   <td>Location.ID
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>A Cloud computing service is primarily located at a location.
   </td>
  </tr>
  <tr>
   <td>Service.ID
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>A Cloud computing service is related to zero or more services.
   </td>
  </tr>
</table>


A simple `CloudComputingService` is formed by a `CloudComputingEndpoint` exposing an interface for VM instantiation and control. The `CloudComputingService` always aggregates `CloudComputingEndpoints`, `CloudComputingShares`, `CloudComputingManagers`, `CloudComputingImage` and `CloudComputingInstanceType` forming a connected set. In other words, `Endpoint` A exposing `InstanceType` A and `Image` A served by `Manager` A via `Share` A and `Endpoint` B exposing `InstanceType` B and `Image` B served by `Manager` B via `Share` B form two different `Computing Services`. On the other hand, `Endpoint` A exposing `InstanceType` A and `Image` A served by `Manager` A via `Share` A and `Endpoint` B exposing `InstanceType` A and `Image` A served by `Manager` A via `Share` B form a single `Computing Service`.



    1.  CloudComputingEndpoint

The `CloudComputingEndpoint` is a specialization of the `Endpoint` class for a service possessing cloud Infrastructure-as-a-Service capability. The class represents an endpoint which is used to create, control and monitor Cloud computing activities. The specific information concerns service status and interface capabilities. This class provides attributes that MAY be used to publish summary information about VM instantiated via a particular Endpoint. Such attributes are optional and may not always be measurable (e.g., in the case of a stateless Endpoint which does not keep information about the VM instantiated through it). 


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>CloudComputingEndpoint
   </td>
   <td colspan="3" >Endpoint
   </td>
   <td>A network Endpoint for creating, monitoring, and controlling computational Cloud Activities called Virtual Machines instances. It MAY also be used to expose complementary capabilities (e.g., resource reservation, attached block storage, VM image manipulation).
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                            [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td><em>URL</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>Network location of the endpoint to contact the related service</em>
   </td>
  </tr>
  <tr>
   <td><em>Capability</em>
   </td>
   <td><em>Capability_t</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>The provided capability according to the OGSA architecture</em>
   </td>
  </tr>
  <tr>
   <td><em>Technology</em>
   </td>
   <td><em>EndpointTechnology_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Technology used to implement the endpoint</em>
   </td>
  </tr>
  <tr>
   <td><em>InterfaceName</em>
   </td>
   <td><em>InterfaceName_t</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>Identification of the interface</em>
   </td>
  </tr>
  <tr>
   <td><em>InterfaceVersion</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..*</em>
   </td>
   <td>
   </td>
   <td><em>Version of the interface</em>
   </td>
  </tr>
  <tr>
   <td><em>InterfaceExtension</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Identification of an extension to the interface</em>
   </td>
  </tr>
  <tr>
   <td><em>WSDL</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>URL of the WSDL document describing the offered interface (applies to Web Services endpoint)</em>
   </td>
  </tr>
  <tr>
   <td><em>SupportedProfile</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>URI identifying a supported profile</em>
   </td>
  </tr>
  <tr>
   <td><em>Semantics</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>URI of a document providing a human-readable description of the semantics of the endpoint functionalities</em>
   </td>
  </tr>
  <tr>
   <td><em>Implementor</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Main organization implementing this software component</em>
   </td>
  </tr>
  <tr>
   <td><em>ImplementationName</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Name of the implementation</em>
   </td>
  </tr>
  <tr>
   <td><em>ImplementationVersion</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Version of the implementation (e.g., major version.minor version.patch version)</em>
   </td>
  </tr>
  <tr>
   <td><em>QualityLevel</em>
   </td>
   <td><em>QualityLevel_t</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>Maturity of the endpoint in terms of quality of the software components</em>
   </td>
  </tr>
  <tr>
   <td><em>HealthState</em>
   </td>
   <td><em>EndpointHealthState_t</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A state representing the health of the endpoint in terms of its capability of properly delivering the functionalities</em>
   </td>
  </tr>
  <tr>
   <td><em>HealthStateInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Textual explanation of the state endpoint</em>
   </td>
  </tr>
  <tr>
   <td><em>ServingState</em>
   </td>
   <td><em>ServingState_t</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A state specifying if the endpoint is accepting new requests and if it is serving the already accepted requests </em>
   </td>
  </tr>
  <tr>
   <td><em>StartTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>The timestamp for the start time of the endpoint</em>
   </td>
  </tr>
  <tr>
   <td><em>Authentication</em>
   </td>
   <td><em>EndpointAuthentication_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Name of the authentication method supported by the endpoint.</em>
   </td>
  </tr>
  <tr>
   <td><em>IssuerCA</em>
   </td>
   <td><em>DN_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Distinguished name of Certification Authority issuing the certificate for the endpoint</em>
   </td>
  </tr>
  <tr>
   <td><em>TrustedCA</em>
   </td>
   <td><em>DN_t</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Distinguished name of the trusted Certification Authority (CA), i.e., certificates issued by the CA are accepted for the authentication process</em>
   </td>
  </tr>
  <tr>
   <td><em>DowntimeAnnounce</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>The timestamp for the announcement of the next scheduled downtime</em>
   </td>
  </tr>
  <tr>
   <td><em>DowntimeStart</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>The starting timestamp of the next scheduled downtime</em>
   </td>
  </tr>
  <tr>
   <td><em>DowntimeEnd</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>The ending timestamp of the next scheduled downtime</em>
   </td>
  </tr>
  <tr>
   <td><em>DowntimeInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Description of the next scheduled downtime</em>
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingService.ID 
<p>
[redefines Service.ID]
   </td>
   <td>1
   </td>
   <td colspan="2" >A Cloud endpoint is part of a Cloud Computing Service.
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingShare.ID                                                          [redefines Share.ID]
   </td>
   <td>*
   </td>
   <td colspan="2" >A Cloud endpoint MAY pass activities to zero or more Cloud computing shares.
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingInstance.ID
<p>
[redefines Activity.ID]
   </td>
   <td>*
   </td>
   <td colspan="2" >An Cloud endpoint has accepted and is managing zero or more Cloud Activities.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
  <tr>
   <td colspan="2" >AccessPolicy.ID 
   </td>
   <td>*
   </td>
   <td colspan="2" >A computing endpoint has assocated zero or more AccessPolicies.
   </td>
  </tr>
</table>




    1.  CloudComputingShare

The `CloudComputingShare` class is the specialization of the main `Share` class for cloud Infrastructure-as-a-Service. A `CloudComputingShare` is a high-level concept introduced to model a utilization target for a pool of resources, sometimes referred as Zones or Sites, defined by a homogeneous set of configuration parameters and characterized by single status information. A `CloudComputingShare` carries information about "policies" (limits) defined over all or a subset of resources and describes their dynamic status (load).

The `CloudComputingShare` stores also a set of `CloudComputingImage` and `CloudComputingInstanceType`, which are used to define respectively the virtual OS and the virtual hardware resources of the `CloudComputingInstance` running on the share. Such virtual OS and hardware resources are provided by the Share with a given Service Level Agreement (SLA). In case of the same `CloudComputingInstanceType` and `CloudComputingImage` are offered under different SLAs, multiple `CloudComputingShare`s shall be created, one for each SLA.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>CloudComputingShare
   </td>
   <td colspan="3" >Share
   </td>
   <td>A utilization target for a set of Cloud Computing Instance Types and Cloud Computing Images, defined by a set of homogeneous configuration parameters and characterized by single status information.
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                            [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td><em>Description</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Description of this share</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>TotalVM
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>Total number of VM known to this computing share (the sum of RunningVM, PendingVM, SuspendedVM, HaltedVM)
   </td>
  </tr>
  <tr>
   <td>RunningVM
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The number of VM running into this computing share
   </td>
  </tr>
  <tr>
   <td>PendingVM
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The number of VM in Pending state (VM in preparation to be running on the system)
   </td>
  </tr>
  <tr>
   <td>SuspendedVM
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The number of VM in suspended state (VMs not running but with reserved resources on this computing share)
   </td>
  </tr>
  <tr>
   <td>HaltedVM
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The number of VM in Halted state (VMs not running on the system with no resources reserved on this computing share)
   </td>
  </tr>
  <tr>
   <td>MaxVM
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The maximum number of VM instances who can run on this share
   </td>
  </tr>
  <tr>
   <td>InstanceMaxCPU
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The maximum number of Virtual CPU who can be assigned to a single VM for the VM in this share. With virtual CPU it is intended the CPU seen by the VM OS, not the physical host CPU assigned to the VM.
   </td>
  </tr>
  <tr>
   <td>InstanceMaxRAM
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>MB
   </td>
   <td>The maximum value (in MB) of virtual RAM memory who can be assigned to a single VM for the VM in this share. With virtual RAM memory it is intended the amount of RAM seen by the VM OS, not the physical RAM dedicated to the VM
   </td>
  </tr>
  <tr>
   <td>NetworkInfo
   </td>
   <td>NetworkInfo_t
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>The type of internal network connection available among the managed Hosts. If many values are published then the various types of network MAY be available only within subsets of the Hosts; the Hosts properties SHOULD publish this information.
   </td>
  </tr>
  <tr>
   <td>DefaultNetworkType
   </td>
   <td>NetworkType_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The default network type that will be setup for an instance (e.g. public, private, private_only…)
   </td>
  </tr>
  <tr>
   <td>PublicNetworkName
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The name of the public network if any.
   </td>
  </tr>
  <tr>
   <td>SLA
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>Service Level Agreement for the VMs under this share. This can be an URL to the SLA document or a keyword representing the SLA itself (eg. 99.99% availability, best effort, etc…)
   </td>
  </tr>
  <tr>
   <td>ProjectID
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The native identifier of the corresponding local project to be used for this share (e.g. used by API users to know what is the project_id for OpenStack)
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingEndpoint.ID
<p>
[redefines Endpoint.ID]
   </td>
   <td>1..*
   </td>
   <td colspan="2" >A Cloud computing share MAY be consumed via one or more computing endpoints.
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingInstanceType.ID 
<p>
[redefines Resource.ID]                         
   </td>
   <td>1..*
   </td>
   <td colspan="2" >A Cloud computing share is defined on one or more computing resources.
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingService.ID   
<p>
[redefines Service.ID]                       
   </td>
   <td>1
   </td>
   <td colspan="2" >A Cloud computing share participates in a computing service.
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingInstance.ID
<p>
[redefines Activity.ID]
   </td>
   <td>*
   </td>
   <td colspan="2" >A Cloud computing share is being consumed by zero or more computing activities.
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingImage.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >A CloudComputeShare provides zero or more VM Image templates
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudToStorageService.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >Link to the storage share used to store instances templates, VM images and/or attached disks
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingShareAcceleratorInfo.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >A Cloud Computing provides zero or more set of information about the usage level of virtual accelerator devices.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
  <tr>
   <td colspan="2" >MappingPolicy.ID                     
   </td>
   <td>*
   </td>
   <td colspan="2" >A share has zero or more mapping policies.
   </td>
  </tr>
</table>




    1.  CloudComputingShareAcceleratorInfo

The CloudComputingShareAcceleratorInfo contains all the information about the usage level of the virtual accelerator device bound to the cloud computing share.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>CloudComputingShareAcceleratorInfo
   </td>
   <td colspan="3" >Entity
   </td>
   <td>The usage level of the virtual accelerator device for a given cloud computing share
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                            [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Type
   </td>
   <td><em>AccType_t</em>
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>The virtual accelerator architecture type.
   </td>
  </tr>
  <tr>
   <td>InstanceMaxAccelerators
   </td>
   <td><em>UInt32</em>
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The maximum number of Virtual Accelerators who can be assigned to a single VM for the VM in this share. With virtual Accelerator it is intended the Accelerator seen by the VM OS, not the physical host Accelerator assigned to the VM.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingShare. ID
   </td>
   <td>1
   </td>
   <td colspan="2" >A set of virtual accelerator information is related to a cloud computing share.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
</table>




    1.  CloudComputingManager

The `CloudComputingManager` class is a specialization of the `Manager` class for the computational capability (Virtual Machines) manager. The `CloudComputingManager` is responsible for the local control of resources. The `CloudComputingManager` layer is not exposed directly to external clients or to the Virtual Machines themselves.

The Virtual Machine manager is usually referred as Hypervisor, thus a piece of software, firmware or hardware which creates, runs and manages Virtual Machines. A Compute Service will usually have only one Compute Manager, but MAY have more. The class provides aggregated information on controlled resources, hypervisors limits and also describes local storage extents accessible to the Virtual Machines.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>CloudComputingManager
   </td>
   <td colspan="3" >Manager
   </td>
   <td>A software component locally managing one or more Cloud Instance Type virtual environments. It MAY also describe aggregated information about the managed resources. The Cloud Computing Manager is also known as Hypervisor.
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                            [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td><em>ProductName</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>Name of the software product adopted as manager</em>
   </td>
  </tr>
  <tr>
   <td><em>ProductVersion</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Version of the software product adopted as manager</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>TotalCPUs
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>Ph.CPU
   </td>
   <td>The total number of physical CPUs cores accessible via any of the available Endpoints and managed by this Cloud Compute Manager. This value SHOULD represent the total installed capacity, i.e. including resources which are temporarily unavailable.
   </td>
  </tr>
  <tr>
   <td>TotalRAM
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>MB
   </td>
   <td>The total amount of RAM accessible via any of the available Endpoints and managed by this Cloud Compute Manager. This value SHOULD represent the total installed capacity, i.e. including resources which are temporarily unavailable.
   </td>
  </tr>
  <tr>
   <td>InstanceMaxCPU
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The maximum number of Virtual CPU who can be assigned to a single VM. (with virtual CPU it is intended the CPU cores as seen by the VM OS)
   </td>
  </tr>
  <tr>
   <td>InstanceMinCPU
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The minimum number of Virtual CPU who can be assigned to a single VM (with virtual CPU it is intended the CPU cores as seen by the VM OS)
   </td>
  </tr>
  <tr>
   <td>InstanceMaxRAM
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>MB
   </td>
   <td>The maximum value (in MB) of virtual RAM memory who can be assigned to a single VM (with virtual RAM memory it is intended the amount of RAM seen by the VM OS, not the phisical RAM dedicated to the VM)
   </td>
  </tr>
  <tr>
   <td>InstanceMinRAM
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>MB
   </td>
   <td>The minimum value (in MB) of virtual RAM memory who can be assigned to a single VM (with virtual RAM memory it is intended the amount of RAM seen by the VM OS, not the phisical RAM dedicated to the VM)
   </td>
  </tr>
  <tr>
   <td>InstanceMaxDedicatedRAM
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>MB
   </td>
   <td>The maximum value (in MB) of virtual RAM memory who can is dedicated to a VM (i.e. physical host memory, not shared of swapped)
   </td>
  </tr>
  <tr>
   <td>InstanceMinDedicatedRAM
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>MB
   </td>
   <td>The minimum value (in MB) of virtual RAM memory who can is dedicated to a VM (i.e. physical host memory, not shared of swapped)
   </td>
  </tr>
  <tr>
   <td>NetworkVirtualizationType
   </td>
   <td>NetVirtualizationT_t
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>The type of network virtualization performed by the Hypevisor to segregate VMs VLANs (ex. none, vSwitch, ebtables, etc…).
   </td>
  </tr>
  <tr>
   <td>CPUVirtualizationType
   </td>
   <td>CPUVirtualizationT_t
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>The type of CPU virtualization (ex. full/paravirtualization/hardware assisted)
   </td>
  </tr>
  <tr>
   <td>VirtualDiskFormat
   </td>
   <td>DiskVirtualizationT_t
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>The format of virtual disk images supported (ex. qcow2, raw, vmdk)
   </td>
  </tr>
  <tr>
   <td>Failover
   </td>
   <td>ExtendedBoolean_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>Failover is the automatic transition of the VM to a secondary machine or server upon failure of the primary component.
   </td>
  </tr>
  <tr>
   <td>LiveMigration
   </td>
   <td>ExtendedBoolean_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>If true the Hypervisor allows to move the virtual machine from one physical host to another without powering down the system
   </td>
  </tr>
  <tr>
   <td>VMBackupRestore
   </td>
   <td>ExtendedBoolean_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>If true the hypervisor allows to backup and restore the virtual machines. This is a static value and does not ensure the availability of the storage for the backup
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingService.ID                          
<p>
[redefines Service.ID]
   </td>
   <td>1
   </td>
   <td colspan="2" >A cloud computing manager participates in a computing service.
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingInstanceType.ID             
<p>
[redefines Resource.ID]
   </td>
   <td>*
   </td>
   <td colspan="2" >A cloud computing manager manages one or more cloud computing instance type..
   </td>
  </tr>
  <tr>
   <td colspan="2" >Benchmark.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >A cloud computing manager has zero or more associated benchmarks. This benchmarks are referred to the virtual resources (RAM, CPU, disk, network) provided to the VMs
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingManagerAcceleratorInfo.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >A cloud computing manager controls zero or more virtual accelerator devices.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
</table>




    1.  CloudComputingManagerAcceleratorInfo

The CloudComputingManagerAcceleratorInfo contains all the information about the virtual accelerator device available for a given cloud computing manager.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>CloudComputingManager
<p>
AcceleratorInfo
   </td>
   <td colspan="3" >Entity
   </td>
   <td>The set of information about the virtual accelerator device provided by the cloud computing manager.
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                            [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Type
   </td>
   <td><em>AccType_t</em>
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>The virtual accelerator architecture type. The enumeration contains definitions such as GPU, MIC, FPGA.
   </td>
  </tr>
  <tr>
   <td>TotalAccelerators
   </td>
   <td><em>UInt32</em>
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The total number of physical Accelerator cards accessible via any of the available Endpoints and managed by this Cloud Compute Manager. This value SHOULD represent the total installed capacity, i.e. including resources which are temporarily unavailable.
   </td>
  </tr>
  <tr>
   <td>InstanceMaxAccelerators
   </td>
   <td><em>UInt32</em>
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The maximum number of Virtual Accelerator cardsCPU who can be assigned to a single VM. (with virtual AcceleratorGPU it is intended the Accelerator card as seen by the VM OS).
   </td>
  </tr>
  <tr>
   <td>InstanceMinAccelerators
   </td>
   <td><em>UInt32</em>
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The minimum number of Virtual AcceleratorsGPU who can be assigned to a single VM (with virtual AcceleratorGPU it is intended the Accelerator card as seen by the VM OS). 
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingManager. ID
   </td>
   <td>1
   </td>
   <td colspan="2" >A set of virtual accelerator information is related to a cloud computing share.
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
</table>




    1.  CloudComputingInstanceType

The `CloudComputingInstanceType `class describes the hardware environment of the VM, i.e. the amount of RAM, CPU, disk and network resources the VM OS will see and manage. The resources provided to the VM are virtual resources, usually shared with other VMs running in the same infrastructure. The performances of the provided resources are specified via the Benchmarks associated to the Instance Type.


<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>CloudComputingInstanceType
   </td>
   <td colspan="3" >Resource
   </td>
   <td>A type of environment available to the CloudComputingManager for running a VM in a ComputingService via a Computing Endpoint; the type of environment is described in terms of hardware, operating system and network characteristics.
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                          [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>IDForEndpoint
   </td>
   <td>String
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>Reference to this particular template to be used during instantiation of a VM via the Endpoint.
   </td>
  </tr>
  <tr>
   <td>MarketPlaceID
   </td>
   <td>String
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>Reference to one or more marketplaces which stores the metadata of this resource template. Reference is the URL of the resource in the marketplace.
   </td>
  </tr>
  <tr>
   <td>Platform
   </td>
   <td>Platform_t
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>The platform architecture provided to the virtual machine (ex. i386, x86_64)
   </td>
  </tr>
  <tr>
   <td>vCPU
   </td>
   <td>UInt32
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>Number of virtual cores provided to the virtual machine (this is the number of core the machine OS will see)
   </td>
  </tr>
  <tr>
   <td>RAM
   </td>
   <td>UInt32
   </td>
   <td>1
   </td>
   <td>MB
   </td>
   <td>Virtual RAM memory provided to the virtual machine (this is the total wuantity of RAM the machine OS will see)
   </td>
  </tr>
  <tr>
   <td>Disk
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>GB
   </td>
   <td>Size of the disk associated to the OS image. If this attribute is omitted, the OS disk size will be the one specified by the CloudComputingImage entity, otherwise the CloudComputingImage OS disk will be extended to this value.
   </td>
  </tr>
  <tr>
   <td>EphemeralStorage
   </td>
   <td>UInt32
   </td>
   <td>0..1
   </td>
   <td>GB
   </td>
   <td>Amount of Ephemeral storage associated to the VM. This is temporary storage which is deleted after the VM closure and is represented as a new resource.
   </td>
  </tr>
  <tr>
   <td>NetworkIn
   </td>
   <td>ExtendedBoolean_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>True if direct inbound network connectivity is available to the OS, even if limited, e.g. by firewall rules.
   </td>
  </tr>
  <tr>
   <td>NetworkOut
   </td>
   <td>ExtendedBoolean_t
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>True if direct outbound network connectivity is available to the OS, even if limited, e.g. by firewall rules.
   </td>
  </tr>
  <tr>
   <td>NetworkPortsIn
   </td>
   <td>UInt32
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>The allowed inbound external connectivity ports (if not specified, all ports are allowed)
   </td>
  </tr>
  <tr>
   <td>NetworkPortsOut
   </td>
   <td>UInt32
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>The allowed outbound external connectivity ports (if not specified, all ports are allowed)
   </td>
  </tr>
  <tr>
   <td>NetworkInfo
   </td>
   <td>NetworkInfo_t
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>The type of internal network connection available to the OS.
   </td>
  </tr>
  <tr>
   <td>OtherHardware
   </td>
   <td>String
   </td>
   <td>*
   </td>
   <td>
   </td>
   <td>Generic placeholder for other virtual hardware or feature provided by this resource template (i.e. dedicated FPU or storage, etc…)
   </td>
  </tr>
  <tr>
   <td colspan="2" >Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingManager.ID                           
<p>
[redefines Manager.ID]
   </td>
   <td>1
   </td>
   <td colspan="2" >Cloud Computing Instance Type is managed by a Cloud computing manager.
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingShare.ID                                 
<p>
[redefines Share.ID]
   </td>
   <td>*
   </td>
   <td colspan="2" >Cloud Computing Instance Type is served by a set of computing shares.
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingInstance.ID
<p>
[redefines Activity.ID]
   </td>
   <td>*
   </td>
   <td colspan="2" >Zero or more cloud computing instances runs this Cloud Computing Instance Type.
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingEndpoint.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >Cloud Computing Instance Type is available on a set of Cloud Computing Endpoints.
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudComputingVirtualAccelerator.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >A cloud computing instance type provides zero or more virtual accelerator devices.
   </td>
  </tr>
  <tr>
   <td colspan="2" >CloudServicePrice.ID
   </td>
   <td>*
   </td>
   <td colspan="2" >The price metric associated to the resources provided by this template. It contains a different metric for each resource (Computing, Memory, Network IN/OUT)
   </td>
  </tr>
  <tr>
   <td colspan="2" >Inherited Association End
   </td>
   <td>Mult.
   </td>
   <td colspan="2" >Description
   </td>
  </tr>
  <tr>
   <td colspan="2" >Extension.Key
   </td>
   <td>*
   </td>
   <td colspan="2" >The entity MAY be extended via key-value pairs.
   </td>
  </tr>
</table>


The associated `CloudComputingPrice` entities define the price for the entire template or separately for each one of the resources (eg. CPU, Memory, Disk, Network IN/OUT) provided by the infrastructure. Price element associated to the `CloudComputingInstanceType `contributes separately to the final price of the VM, together with the other price elements associated to the `CloudComputingImage`.



        1.  CloudComputingVirtualAccelerator

The `CloudComputingVirtualAccelerator` is an entity used to describe a set of homogeneous virtual accelerator devices. Generally a virtual accelerator device corresponds to physical one installed on the host. A cloud computing instance may be associated with one or more virtual accelerators.

 \



<table>
  <tr>
   <td>Entity
   </td>
   <td colspan="3" >Inherits from
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>CloudComputingVirtualAccelerator
   </td>
   <td colspan="3" >Entity
   </td>
   <td>Description of the accelerator device
   </td>
  </tr>
  <tr>
   <td>Inherited Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td><em>CreationTime</em>
   </td>
   <td><em>DateTime_t</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Timestamp describing when the entity instance was generated</em>
   </td>
  </tr>
  <tr>
   <td><em>Validity</em>
   </td>
   <td><em>UInt64</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td><em>s</em>
   </td>
   <td><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant.  After that period has elapsed,</em>
<p>
<em>the information SHOULD NOT be considered relevant</em>
   </td>
  </tr>
  <tr>
   <td><em>ID                            [key]</em>
   </td>
   <td><em>URI</em>
   </td>
   <td><em>1</em>
   </td>
   <td>
   </td>
   <td><em>A global unique ID </em>
   </td>
  </tr>
  <tr>
   <td><em>Name</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>0..1</em>
   </td>
   <td>
   </td>
   <td><em>Human-readable name</em>
   </td>
  </tr>
  <tr>
   <td><em>OtherInfo</em>
   </td>
   <td><em>String</em>
   </td>
   <td><em>*</em>
   </td>
   <td>
   </td>
   <td><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
   </td>
  </tr>
  <tr>
   <td>Attribute
   </td>
   <td>Type
   </td>
   <td>Mult.
   </td>
   <td>Unit
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>Type
   </td>
   <td>AccType_t
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>The type of virtual accelerator device.
   </td>
  </tr>
  <tr>
   <td>VirtualAccelerators
   </td>
   <td>UInt32
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>Number of virtual Accelerator cards provided to the virtual machine (usually this is the number of cards the machine OS will see)
   </td>
  </tr>
  <tr>
   <td>Vendor
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The name of the physical Accelerator vendor provided to the virtual machine. Free format, but it SHOULD correspond to the name by which the vendor is generally known.
   </td>
  </tr>
  <tr>
   <td>Model
   </td>
   <td>String
   </td>
   <td>0..1
   </td>
   <td>
   </td>
   <td>The name o
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM4NjcxMTQ4OSwxMjMzMjQ1ODc2XX0=
-->