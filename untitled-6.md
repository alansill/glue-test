---
description: Sections 10-17
---

# Concluding Remarks

##  Relationship to OGF Reference Model

In this section, we describe the integration of the GLUE information model with the OGF Reference Model \[RM\]. The reference model defines the concept of Grid Component. In GLUE, a root concept called Entity is defined. Such a root concept MAY be defined as a specialization of the Grid Component concept, that means that all properties are inherited by the GLUE classes. In Figure 5, we represent this relationship by a UML class diagram.

![](.gitbook/assets/0%20%283%29.png)

**Figure 5 GLUE and Reference Model integration**

## Security Considerations

This section considers security implications when using the GLUE 2.0 conceptual model. It follows the advice given in RFC-3552.

As the conceptual model of GLUE 2.0 provides limited scope for embedding security information many of these concerns listed here are delegated to the concrete data models and to the underlying software implementations. Nonetheless, some points are independent of which concrete data model is employed so some discussion is appropriate.

When deploying an information service conforming to the GLUE 2.0 conceptual model, consideration should be given to the points discussed below.

### 11.1. Communication security

The GLUE conceptual model is independent of how information is stored and how that information is exchanged between agents. Because of this, concern for communication security is largely delegated to the underlying concrete data model and software implementations.

#### Confidentiality

The GLUE conceptual model contains information that MAY be personal or confidential in nature. Contact details and indications of end-user activity MAY fall into this category.

Conforming implementations should identify which components of the data should be considered confidential and appropriate precautions should be in place to safeguard against disclosure to unintended audiences.

#### Data integrity

The information within GLUE has many potential uses, from operational to accounting. How accurate the information is MAY depend on many factors, including the integrity of software agents that publish data and the transport used to propagate information.

The software used to provide an information service MAY cache GLUE information. If so, the caches provide additional points where data integrity MAY be compromised.

#### Peer Entity authentication

No explicit description of the agents that publish information is included within the GLUE conceptual model. This prevents authentication information from being included within the abstract model.

In general, support for peer-entity authentication is delegated to the concrete data model or the underpinning software. In many cases the agents will act on behalf of some AdminDomain; if so, elements of peer entity authentication \(e.g., public/private key-pairs\) MAY be included using the described schema extension mechanisms provided issues with data integrity are understood.

###  Non-repudiation

The GLUE conceptual model contains no explicit description of the publishing agents that provide GLUE information. This prevents explicitly support for non-repudiation. In many cases a set of publishing agents will provide information for Services in some AdminDomain. If so, then it is the AdminDomain that asserts the non-repudiation of the data the publishing agents provide.

Non-repudiation MAY require information from whoever asserts the non-repudiation of the data; for example, a cryptographic certificate of some AdminDomain. If the publishing agent is identified with an AdminDomain then this information MAY be included using the schema extension mechanisms of the AdminDomain \(via OtherInfo or Extension\). It is also possible for this information to be included in fields specific to the concrete data model or it MAY be provided outside of the GLUE conceptual model.

In addition, information MAY be published with corresponding non-repudiation information, such as a cryptographic signature. Signatures MAY be included using schema extensions \(OtherInfo or

Extension\) or MAY be included in fields specific to the concrete data model.

### System security

The GLUE conceptual model intended use is to provide an abstract view of a grid system. There are many processes that MAY make use of this information, each MAY depend on the GLUE conceptual model to undertake work.

#### Unauthorized usage

The GLUE conceptual model has no explicit description of end-users of the schema information and no explicit description of authorized usage. In general, is assumed that any authorization controls for access to the GLUE information is provided by specific concrete bindings and software implementation.

It MAY be possible to identify a UserDomain with those agents authorised to use GLUE information and embed authorization information using described schema extension mechanisms, provided issues with data integrity are understood.

#### Inappropriate Usage

The GLUE conceptual model provides no mechanism for describing appropriate usage and does not include a data-processing model, so providing a description of inappropriate usage is considered out-of-scope.

Individual grids MAY describe what they consider appropriate usage of GLUE information and implement appropriate procedures to ensure this policy is enacted.

###  Specific attacks

RFC-3552 describes several specific attacks that MUST be considered. These are detailed below.

#### Eavesdropping

Some information described in the GLUE conceptual model MAY be sensitive in nature; this MAY include contact details and descriptions of user activity. Appropriate care should be taken to prevent unintended access or disclosure to an unintended audience.

#### Replay

Grid operations MAY depend on information provided in the GLUE conceptual model.

If a system implementing the GLUE 2.0 conceptual model is susceptible to a replay attack then it is possible for part \(possibly all\) of the information in the conceptual model to be reverted to some previous state as seen by some \(possibly all\) end users. Please note that this is a specific case of the more general modification attack.

A replay attack MAY result in disrupted service. If security attributes, such as authorization, are embedded within the GLUE conceptual model then a replay attack MAY result in inappropriate access to data. Underlying concrete models and software implementations should prevent replay attacks.

#### Message insertion

The ability to insert information is key to providing accurate information. However, inserting incorrect information MAY have a detrimental effect to the running systems; for example, there are attributes in the conceptual model that accept multiple values. If incorrect values are included, the systems MAY suffer.

Many aspects of GLUE provide service discovery. Inserting false information would allow unauthorised services to publish their presence and attract activity. This MAY be used as a basis for further attacks. Underlying concrete models and software implementations should ensure that any agent's ability to insert information is limited and appropriate.

#### Deletion

The ability to delete information from an information service could interfere with normal operations; for example, if Services are removed then activity that would use those services MAY be affected; if AdminDomains are removed then normal operation procedures MAY be impossible; if security components are removed \(such as X509 certificates\) then facilities such as non-repudiation MAY become ineffectual. Underlying concrete models and implementing software should ensure that any ability of an agent to delete information is limited and appropriate.

#### Modification

The ability for an agent to modify information stored in an information service is key to providing accurate information. However, concrete data models and software implementation should place limits such that the agents' ability to modify information is controlled and appropriate.

#### Man-in-the-middle

For a system implementing the GLUE conceptual model, a successful man-in-the-middle attack MAY lead to arbitrary modification of data \(see 9.4.5\). It MAY also allow deleting existing data \(see 9.4.4\) or adding additional data \(see 9.4.3\). This MAY have severe influence on the systems based on GLUE information. Underlying concrete models and implementing software should understand the risk from man-in-the-middle attacks and provide appropriate security against them.

#### Denial of service attacks

A Denial of Service attack is one that attempts to prevent normal operation of systems. Perhaps, the most obvious is to prevent or corrupt the flow of information. Systems using the GLUE conceptual model should understand the consequences of a partial or complete lack of information. Appropriate measures should be taken to ensure the systems continue to run to the extent possible.

## Author Information

  
Stephen Burke

Science and Technology Facilities Council

Rutherford Appleton Laboratory

Harwell Science and Innovation Campus

Chilton, Didcot, Oxfordshire, OX11 0QX \(UK\)

E-mail: s.burke@rl.ac.uk

John-Paul Navarro  
University of Chicago/Argonne National Laboratory  
Mathematics & Computer Science Division, Building 221  
9700 S. Cass Avenue  
Argonne, IL 60439 \(USA\)  
E-mail: [navarro@mcs.anl.gov](mailto:navarro@mcs.anl.gov)

Shiraz Memon

Forschungszentrum Jülich GmbH

Wilhelm-Johnen-Straße

52425 Jülich \(Germany\)

E-mail: a.memon@fz-juelich.de

Alessandro Paolini

EGI Foundation

Science Park 140

1098 XG Amsterdam \(The Netherlands\)

E-mail: [alessandro.paolini@egi.eu](mailto:alessandro.paolini@egi.eu)

Baptiste Grenier

EGI Foundation

Science Park 140

1098 XG Amsterdam \(The Netherlands\)

E-mail: [baptiste.grenier@egi.eu](mailto:baptiste.grenier@egi.eu)

Enol Fernandez

EGI Foundation

Science Park 140

1098 XG Amsterdam \(The Netherlands\)

E-mail: [enol.fernandez@egi.eu](mailto:enol.fernandez@egi.eu)

Marco Verlato

INFN-Padova

Via Marzolo 8

35131 Padova \(Italy\)

E-mail: marco.verlato@pd.infn.it

Paolo Andreetto

INFN-Padova

Via Marzolo 8

35131 Padova \(Italy\)

E-mail: paolo.andreetto@pd.infn.it

## Contributors & Acknowledgements

We gratefully acknowledge the contributions made to this document \(in no particular order\) by Paul Strong, Ellen Stokes, Hiro Kishimoto, David Snelling, Flavia Donno, Cal Loomis, Shiraz Memon, Matt Viljoen, Steve Traylen and all people who provided constructive and valuable input in the discussion.

## Intellectual Property Statement

The OGF takes no position regarding the validity or scope of any intellectual attribute or other rights that might be claimed to pertain to the implementation or use of the technology described in this document or the extent to which any license under such rights might or might not be available; neither does it represent that it has made any effort to identify any such rights. Copies of claims of rights made available for publication and any assurances of licenses to be made available, or the result of an attempt made to obtain a general license or permission for the use of such proprietary rights by implementers or users of this specification MAY be obtained from the OGF Secretariat.

The OGF invites any interested party to bring to its attention any copyrights, patents or patent applications, or other proprietary rights which MAY cover technology that MAY be required to practice this recommendation. Please address the information to the OGF Executive Director.

## Disclaimer

This document and the information contained herein is provided on an “As Is” basis and the OGF disclaims all warranties, express or implied, including but not limited to any warranty that the use of the information herein will not infringe any rights or any implied warranties of merchantability or fitness for a particular purpose.

## Full Copyright Notice

Copyright \(C\) Open Grid Forum \(2009, 2019\). All Rights Reserved.

This document and translations of it MAY be copied and furnished to others, and derivative works that comment on or otherwise explain it or assist in its implementation MAY be prepared, copied, published and distributed, in whole or in part, without restriction of any kind, provided that the above copyright notice and this paragraph are included on all such copies and derivative works. However, this document itself MAY not be modified in any way, such as by removing the copyright notice or references to the OGF or other organizations, except as needed for the purpose of developing Grid Recommendations in which case the procedures for copyrights defined in the OGF Document process MUST be followed, or as required to translate it into languages other than English.

The limited permissions granted above are perpetual and will not be revoked by the OGF or its successors or assignees.

## References

\[GLUE-WG\] The GLUE Working Group of OGF, [_https://redmine.ogf.org/projects/glue-wg_](https://redmine.ogf.org/projects/glue-wg)

\[GLUE-USECASES\] GLUE 2.0 Use Cases \(early draft\), _https://redmine.ogf.org/dmsf\_files/126?download=_

\[GLUE-REAL\] GLUE 2.0 – Reference Realizations to Concrete Data Models, https://redmine.ogf.org/dmsf/glue-wg?folder\_id=17

\[GLUE-1.x\] The GLUE Schema 1.3, _https://redmine.ogf.org/dmsf\_files/61?download=_

\[GLUE-2.0\] The GLUE Schema 2.0, https://www.ogf.org/documents/GFD.147.pdf

\[NG-SCHEMA\] The NorduGrid/ARC Information System, NORDUGRID-TECH 4,_http://www.nordugrid.org/documents/arc\_infosys.pdf_

\[NAREGI-SCHEMA\] NAREGI information and data model, _https://redmine.ogf.org/dmsf/glue-wg?folder\_id=19_

 \[OGF-TS\] Technical Strategy for the Open Grid Forum 2007-2010. GFD-I.113. [http://www.ogf.org/documents/GFD.113.pdf](http://www.ogf.org/documents/GFD.113.pdf)

\[XSRL\] NorduGrid XRSL \(Extended Resource Specification Language\) - [http://www.nordugrid.org/documents/xrsl.pdf](http://www.nordugrid.org/documents/xrsl.pdf)

\[EBNF\] Extended Backus–Naur form. ISO/IEC 14977 : 1996\(E\) [http://www.cl.cam.ac.uk/~mgk25/iso-14977.pdf](http://www.cl.cam.ac.uk/~mgk25/iso-14977.pdf)

\[URI\] T. Berners-Lee, R. Fielding, L. Masinter. Uniform Resource Identifier \(URI\): Generic Syntax.

IETF RFC 3986. Jan 2005. [http://www.ietf.org/rfc/rfc3986.txt](http://www.ietf.org/rfc/rfc3986.txt)

\[SRMV1\] Storage Resource Manager \(SRM\) Joint Design. [http://sdm.lbl.gov/srm-wg/doc/srm.v1.0.pdf](http://sdm.lbl.gov/srm-wg/doc/srm.v1.0.pdf)

\[SRMV2\] Storage Resource Manager Interface Specification V2.2. [http://sdm.lbl.gov/srm-wg/doc/SRM.v2.2.html](http://sdm.lbl.gov/srm-wg/doc/SRM.v2.2.html)

\[CREAM\] gLite CREAM \(Computing Resource Execution And Management\). _https://wiki.italiangrid.it/CREAM_

\[GRAM\] Globus Resource Allocation Protocol. [http://www.globus.org/api/c-globus-2.2/globus\_gram\_documentation/html/index.html](http://www.globus.org/api/c-globus-2.2/globus_gram_documentation/html/index.html)

\[OGF-GFD80\] I. Foster, H. Kishimoto, A. Savva, D. Berry, A. Grimshaw, B. Horn, F. Maciel, F. Siebenlist, R. Subramaniam, J. Treadwell, J. Von Reich. The Open Grid Services Architecture, Version 1.5. OGF GFD-80. 24 Jul 2006

\[RM\] D. Snelling, P. Strong. Open Grid Forum Reference Model v2.0. OGF Draft. 23 Feb 2008. [https://redmine.ogf.org/dmsf\_files/12690?download=](https://redmine.ogf.org/dmsf_files/12690?download=)

