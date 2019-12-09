---
description: Section 1
---

# 1. Introduction

In this document, we present a conceptual information model for Grid and Cloud entities described using natural language and enriched with a graphical representation using UML Class Diagrams. As a conceptual model, it is designed to be independent from the concrete data models adopted for its implementation. Rendering to concrete data models such XML Schema, LDAP Schema, JSON schema and SQL are provided in a separate document. From the semantic viewpoint, the concrete data models SHOULD represent the same concepts and relationships of the conceptual information model; nevertheless they MAY contain simplifications targeted at improving query performance or other aspects of interest.

This information model is based on the experience of several modelling approaches being used in current production Grid infrastructures \(e.g., GLUE Schema 1.x \[GLUE-1.X\], GLUE Schema 2.0 \[GLUE-2.0\], NorduGrid schema \[NG-SCHEMA\], Naregi model \[NAREGI-SCHEMA\]\). The main supporting use cases are collected in the use cases document \[GLUE-USECASES\].

The mapping to concrete data models will be published in separate documents. Profile documents SHOULD appear to define how to generate and use the information in production scenarios or how to integrate the GLUE specification along with clarifications, refinements, interpretations and amplifications to promote interoperability \(e.g., a profile MAY decide that an attribute which is optional in the conceptual model, is considered mandatory in a certain Grid infrastructure; or that optional attributes are never published\).

