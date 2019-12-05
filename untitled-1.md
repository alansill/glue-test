---
description: Sections 1-5
---

# Introduction and Overview

## Introduction

In this document, we present a conceptual information model for Grid and Cloud entities described using natural language and enriched with a graphical representation using UML Class Diagrams. As a conceptual model, it is designed to be independent from the concrete data models adopted for its implementation. Rendering to concrete data models such XML Schema, LDAP Schema, JSON schema and SQL are provided in a separate document. From the semantic viewpoint, the concrete data models SHOULD represent the same concepts and relationships of the conceptual information model; nevertheless they MAY contain simplifications targeted at improving query performance or other aspects of interest.

This information model is based on the experience of several modelling approaches being used in current production Grid infrastructures \(e.g., GLUE Schema 1.x \[GLUE-1.X\], GLUE Schema 2.0 \[GLUE-2.0\], NorduGrid schema \[NG-SCHEMA\], Naregi model \[NAREGI-SCHEMA\]\). The main supporting use cases are collected in the use cases document \[GLUE-USECASES\].

The mapping to concrete data models will be published in separate documents. Profile documents SHOULD appear to define how to generate and use the information in production scenarios or how to integrate the GLUE specification along with clarifications, refinements, interpretations and amplifications to promote interoperability \(e.g., a profile MAY decide that an attribute which is optional in the conceptual model, is considered mandatory in a certain Grid infrastructure; or that optional attributes are never published\).

## Change-log

The following table provides a list of changes from the past GLUE editions

| **Release** | **Change description** |
| :--- | :--- |
| 1.0 | **Initial release** |
| 2.0 | **Major re-design to other information models** |
| 2.1 | **Addition of Accelerators and Cloud Computing objects** |

## Notational Conventions

The key words “MUST”, “MUST NOT,” “REQUIRED,” “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” are to be interpreted as described in RFC 2119 \(see http://www.ietf.org/rfc/rfc2119.txt\). All class names are written using this font.

## General Statements

The Information Model and its renderings MUST treat strings, both entity and attribute names and their values, as being case-sensitive. Each GLUE entity MUST have an ID attribute \(an exception is made for the Extension class\) which is needed for identification or for access to the attributes of the related entity over time and across different information sources. As a general guideline, ID's SHOULD be persistent at least for a day when assigned to an entity. The ID MUST NOT be interpreted by the user or the system as having any meaning other than an identifier. In particular, there is no relationship between an ID and a network endpoint. Every ID MUST be a valid URI. The usage of URN \(Uniform Resource Name, a subset of Uniform Resource Identifier or URI\) is RECOMMENDED. The motivations for choosing URI’s reside in the fact that Grid services are evolving towards Web-based technologies, therefore it is meaningful to adopt the same identification system.

As regards units of measure, multiples of bytes MUST refer to the SI \(_Le_ _**S**ystème_ _**I**nternational d'Unités_\) prefix \(http://en.wikipedia.org/wiki/SI\_prefix\), therefore GB is 109 Bytes and not 230 Bytes \(the latter are GibiBytes\).

In Appendix A, we provide guidelines for place-holder values that MUST be used when the attributes have no good default value or when the attribute cannot be measured for some reason.

As regards extensibility, two main approaches are introduced to extend the information associated to the existing classes: the OtherInfo attribute and the Extension class. The OtherInfo attribute is present in the Entity class, therefore it is inherited by all GLUE classes. Its type is string and its multiplicity is \*. This SHOULD be used for associating a flat list of tags to a certain class instance. The Extension class is associated to the Entity class \(and therefore also to all the derived classes\) and enables linking key/value pairs to any GLUE class instance. This SHOULD be used when there is the need for advertising more structured information, for instance an attribute not present in the model with a related value.

Both solutions are proposed because they have a different impact in the implementations: the OtherInfo approach is easier to query, nevertheless it MAY require parsing in case of concatenation of different chunks of information \(e.g., attribute name and attribute value\). The Extension class offers a two-dimensional construct, but nevertheless it is more complex to query.

The extensibility regarding the addition of new classes and associations is not supported at the conceptual level. We RECOMMEND to create specializations of the conceptual model and to implement them by extending the concrete data models. Such extensions MUST NOT be considered part of the GLUE specification, but nevertheless we RECOMMEND submitting them to the GLUE WG for consideration in future revisions of the specification.

## Template

In order to enrich the UML Class Diagrams with additional information, a table for each UML class is provided. This descriptive table is composed of three parts.

The ﬁrst part refers to the whole entity and presents the entity name, the entity from which it inherits and the description of what the entity represents.

The second part refers to the properties of the class; for each of them, the following characteristics are described: the attribute name, the data type, the multiplicity concerning how many values are allowed \(\* means zero or more\), the unit of measurement and a description. For ease of reading, the properties that are inherited from a parent class are also listed. As regards the multiplicity, the value of zero means that it is allowed to refrain from publishing a value for the related attribute even though this MAY be measured.

The third part refers to the associations \(association, composition, aggregation or association class\) that the class MAY hold with other classes. For each association, the associated class reference is described in terms of the associated end class and key attribute, the multiplicity \(i.e., the number of instances of the associated class that are allowed\) and a description. The inherited associations are also reported in the “inherited association end” if they are not redefined in the “association end”. The template structure is the following:

| Entity | Inherits from | Description |  |  |
| :--- | :--- | :--- | :--- | :--- |
|  |  |  |  |  |
| Inherited Attribute | Type | Mult. | Unit | Description |
|  |  |  |  |  |
| Attribute | Type | Mult. | Unit | Description |
|  |  |  |  |  |
| Association End | Mult. | Description |  |  |
|  |  |  |  |  |
| Inherited Association End | Mult. | Description |  |  |
|  |  |  |  |  |

## 

