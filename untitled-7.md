---
description: Appendix A and B
---

# Appendices

## Place-holder values for unknown data

Whilst people endeavor to provide accurate information, there MAY be situations where specific GLUE attributes MAY be assigned place-holder \(or dummy\) values. These place-holder values carry some additional semantic meaning; specifically, that the correct value is currently unknown and the presented value should be ignored. This appendix describes a set of such place-holder values.

Some attributes within the GLUE schema are required whilst others are optional. If the attribute is optional and the corresponding information is unavailable, the information provider MUST either publish a place-holder or not to publish the attribute. If the attribute is required, then the information MUST either publish a place-holder value or refrain from publishing the GLUE object.

If a place-holder value is published, it MUST conform to the scheme described in this appendix. This is to increase the likelihood that software will understand the nature of the information it receives.

This appendix describes place-holder values that have be chosen so they are obvious "wrong" to humans, unlikely to occur under normal operation and valid within the attribute type. This also allows for detection of failing information provider components.

### A.1. Use cases

There are two principle use-cases for place-holder values, although others MAY exist.

Scenario 1. a static value has no good default value and has not been configured for a particular site.

Some provisions for GLUE Schema provide templates. These templates MAY contain attributes that have no good default value; for example, supplying the correct value MAY require site-specific knowledge. Whilst it is expected that these attributes be configured, it is possible that this does not happen, so exposing the attributes' default values.

Scenario 2. information provider is unable to obtain a dynamic value.

A dynamic value is provided by an information provider by querying the underlying grid resources. This query will use a number of ancillary resources \(e.g., DNS, network hardware\) that might fail; the grid services might also fail. If an attribute is required and the current value is unobtainable, a place-holder value MUST be used.

### A.2. Place-holder values

This section describes a number of values that MAY be represented within a given address space \(e.g., Strings/UTF-8, Integers, FQDNs, IPv4 address space\). Each of the different types are introduced along with the place-holder value and a brief discussion on usage, rational and any other considerations.

### A.3. Extended booleans

The reserved value “undefined” SHOULD be used. The way to express that no value is published MUST be defined in the documents defining the realization to concrete data models \(e.g., \[GLUE-REAL\]\).

### A.4. Simple strings

 \(ASCII/UTF-8\) should use "UNDEFINEDVALUE" or should start "UNDEFINEDVALUE:"

Upper-case letters make it easier to spot and a single word avoids any white-space issues.

A short error message MAY be incorporated into the message by appending the message after the colon.

 Examples:

 UNDEFINEDVALUE

 UNDEFINEDVALUE: unable to contact torque daemon.

Using UNDEFINEDVALUE is a default option for strings that have no widely-known structure. If a value is of a more restrictive sub-type \(e.g., FQDNs, FQANs, URIs\) described below, then the rules for more restrictive form MUST be used.

### A.5. Fully qualified domain names

They MUST use a hostname ending either "example.org" for scenario 1, or "invalid" for scenario 2.

RFC 2606 defines two second-level domains: "example.org" and "example.com". These domains have the advantage of ending with a recognisable TLD, so are recognisable as a DNS name. Default configuration \(scenario 1, above\) MUST use DNS names that end "example.org"

RFC 2606 also reserves the "invalid" Top-Level-Domain \(TLD\) as always invalid and clearly so. For dynamic information gathering, a value ending "invalid" MUST be used.

In both cases, additional information MAY be included by specifying a prefix to "example.org" or "invalid". This MAY be used to specify the class of machine that should be present. For dynamic

infomation, if the class of machine is not published then the FQDN "unknown.invalid" MUST be used.

Examples:

www.example.org

your-CE.example.org

unknown.invalid

site-local-BDII.invalid

### A.6. IPv4 address

It MUST use 192.0.2.250

There are several portions of IPv4 addresses that should not appear on a network, but none that are reserved for documentation or to specify a non-existent address. Using any address leads to the risk of side-effects, should this value be used.

The best option is an IP address from the 192.0.2.0/24 subnet. This subnet is defined in RFC 3330 as "TEST-NET" for use in documentation and example code. For consistency, the value 192.0.2.250 MUST be used.

### A.7. IPv6 addr

It MUST use 2001:DB8::FFFF

There is no documented undefined IPv6 address. RFC 3849 reserves the address prefix 2001:DB8::/32 for documentation. For consistency, the address 2001:DB8::FFFF MUST be used.

### A.8. Integers

It MUST use "all nines"

 For uint32/int32 this is 999,999,999

 For uint64/int64 this is 999,999,999,999,999,999

For integers, all numbers expressible within the encoding \(int32/uint32/etc.\) are valid so there is no safe choice.

If an unsigned integer is encoded as a signed integer, it is possible to use negative numbers safely. However, these numbers will be unrepresentable if the number is stored as an unsigned

integer. For this reason a negative number place-holder MUST not be used.

The number was chosen for three reasons. First, attribute scales are often chosen to reduce the likelihood of overflow: numbers towards MAXINT \(the large number representable in an integer domain\) are less likely to appear. Second, repeated numbers stand out more clearly to humans. Finally, the statistical frequency of measured values often follows Benford's law, which indicates that numbers starting with "1" occur far more frequently than those starting with "9" \(about six times more likely\). For these reasons, information providers MUST use all-nines to indicate a place-holder.

### A.9. File path

It MUST start either "/UNDEFINEDPATH" or "\UNDEFINEDPATH".

As with the simple string, a single upper-case word is recommended. The initial slash indicates that the value is a path. Implementations MUST use whichever slash is most appropriate for the underlying system \(Unix-like systems use a forward-slash\). Software should accept either value as an unknown-value place-holder.

Additional information MAY be encoded as data beyond the initial UNDEFINEDPATH, separated by the same slash as started the value. Additional comments should not use any of the following characters: \ \[ \] ; = " : \| , \* .

Examples:

 /UNDEFINEDPATH

 \UNDEFINEDPATH

 /UNDEFINEDPATH/Path to storage area

 /UNDEFINEDPATH/Broker unavailable

### A.10. Email addresses

It MUST use an undefined FQDN for the domain.

RFC 2822 defines emails addresses to have the form: &lt;local-part&gt; '@' &lt;domain&gt;

The &lt;domain&gt; MUST be an undefined FQDN; see above for a complete description. For email addresses, information providers should use "example.org" for scenario 1. and "unknown.invalid" for scenario 2.

The &lt;local-part&gt; MAY be used to encode a small amount of additional information; for example, it MAY indicate the class of user to whom the email address should be delivered. If no such information is to be encoded the value "user" MUST be used.

Examples:

 user@example.org

 user@unknown.invalid

 site-local-contact@example.org

 local-admin@example.org

### A.11. Uniform Resource Identifier \(URI\)

It is schema-specific

RFC 3986 defines URIs as a "federated and extensible naming system." All URIs start with a schema-name part \(e.g., "http"\) and no schema-name has been reserved for undefined or documenting example values.

For any given URI schema \("http", for example\), it MAY be possible to define a place-holder value within that name-space. If a GLUE value has only one valid schema, the undefined value MUST be taken from that schema. If several schemata are possible, one MUST be chosen from the available options. This should be the most commonly used.

Take care with the URI encoding. All place-holder URI values MUST be valid URIs. If additional information is included, it MUST be encoded so the resulting URI is valid.

For schemata that MAY include a FQDN \(e.g., a reference to an Internet host\), an undefined URI MUST use an undefined FQDN; see above for details on undefined FQDNs.

URI schemata that reference a remote data object \(e.g., "http", "ftp", "https"\), additional information MAY be included as the path. The FQDN indicates that the value is a place-holder, indicating an place-holder value, so information providers should not specify "UNDEFINEDPATH".

For "file" URIs, the path part MUST identify the value as unknown and MUST use the forward-slash variant; see above for details on undefined paths.

For "mailto" URIs \(http://www.ietf.org/rfc/rfc2368.txt\) encapsulates valid email addresses with additional information \(such as email headers and message body\). Place-holder mailto URIs MUST use an unknown email address \(see above\). Any additional information MUST be included in the email body.

There MAY be other schemata in use that are not explicitly covered in this section. A place-holder value should be agreed upon within whichever domain such schemata are used. This place-holder value should be in the spirit of the place-holder values described so far.

Examples:

 http://www.example.org/

 httpg://your-CE.example.org/path/to/end-point

 httpg://unknown.invalid/User%20certificate%20has%20expired

 mailto:site-admin@example.org

 mailto:user@maildomain.invalid?body=Problem%20connecting%20to%20WLMS

 file:///UNDEFINEDPATH

 file:///UNDEFINEDPATH/path%20to%20some%20directory

### A.12. X.509 Distinguished Names

It MUST start O=Grid,CN=UNDEFINEDUSER

X.509 uses a X.500 namespace, represented as several Relative Domain-Names \(RDNs\) concatenated by commas \(we refer to syntax defined in IETF RFC 4514\). The final RDN is usually a single common name \(CN\), although multiple CNs are allowed.

Unknown DN values MUST have at least two entries: an initial O=Grid followed immediately by CN=UNDEFINEDUSER.

Additional information MAY be encoded using extra CN entries. These MUST come after CN=UNDEFINEDUSER.

Examples:

 O=Grid,CN=UNDEFINEDUSER

 O=Grid,CN=UNDEFINEDUSER/CN=Your Grid certificate DN here

 O=Grid,CN=UNDEFINEDUSER/CN=Cannot access SE

### A.13. Fully Qualified Attribute Name \(FQAN\)

It MUST use a VO of "vo.example.org" \(for scenario 1.\) or "unknown.invalid" \(for scenario 2\).

The "VOMS Credential Format" document,

http://edg-wp2.web.cern.ch/edg-wp2/security/voms/edg-voms-credential.pdf

states that FQANs MUST have the form:

/VO\[/group\[/subgroup\(s\)\]\]\[/Role=role\]\[/Capability=cap\]

Where VO is a well-formed FQDN. Unlike FQDNs, VO names MUST be lower-case. The place-holder value for FQAN is derived from the place-holder FQDN \(see Section A.5\). It MUST have no subgroup\(s\) or Capability specified.

Any additional information MUST be encoded within a single Role name. Care should be taken that only valid characters \(A-Z, a-z, 0-9 and dash\) are included.

Examples:

 /vo.example.org

 /vo.example.org/Role=Replace-this-example-with-your-FQAN

 /unknown.invalid

 /unknown.invalid/Role=Unable-to-contact-CE-Error-42

### A.14. Geographic locations

It MUST use longitude 0 degrees, latitude 0 degrees.

Meridians of longitude are taken from \(-180,180\] degrees, whilst parallels of latitude are taken from \[-90,90\] degrees. For a place-holder value to be a valid location, it MUST also be taken from these ranges.

By a happy coincidence, the \(0,0\) location is within the Atlantic Ocean, some 380 miles \(611 kilometers\) south of the nearest country \(Ghana\). Since this location is unlikely to be used and repeated numbers are easier for humans to spot, \(0,0\) MUST be used to specify an place-holder location.

## Data Types

This section contains the definition of attribute types defined within this model. The enumerated types may be either closed or open. For properties whose type defines a closed enumeration, one of the defined values MUST be chosen; any other value is not valid. For properties whose type defines an open enumeration, one of the defined values MAY be chosen, but nevertheless any other value compatible with the string type and with the recommended syntax is allowed. Before defining a new open enumeration value, it is recommended to apply the “GLUE2 Enumerations procedures and best practices” \([http://redmine.ogf.org/projects/glue-wg/wiki/Enumerations\_procedures\_and\_best\_practices\_v10](http://redmine.ogf.org/projects/glue-wg/wiki/Enumerations_procedures_and_best_practices_v10)\). The enumeration values MUST be lower-case.

### B.1. AccessLatency\_t

Closed enumeration:

| Value | Description |
| :--- | :--- |
| nearline | A file MAY have its only copies in a "nearly online" component of the storage system, typically a fully automated tape robot, but also a remote storage system could fit this qualification. Such a facility will need an unspecified amount of time to make a copy of the file available on the disk component of the container under consideration. When a file is not in use, its disk copies MAY be removed. Hence the system cannot guarantee that a file will be immediately available on disk |
| offline | A file MAY have its only copies in an offline component of the storage system, for example a tape library that is not connected to an automated tape robot. Hence an operator intervention MAY be needed to make a copy of a file available that has a lower latency |
| online | Files are always stored on a medium with an access time less than a minute \(e.g., a disk\) |

### B.2. AccType\_t

  
****Open enumeration:

| Value | Description |
| :--- | :--- |
| GPU | GPU architecture |
| MIC | Intel MIC architecture |
| FPGA | Generic FPGA accelerator |

### B.3. AppEnvState\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| Installable | The application environment is not installed, but MAY be dynamically installed |
| installationfailed | The application environment was being installed, but the installation process failed |
| installedbroken | The application environment is installed, but the verification failed |
| installednotverified | The application environment is installed, but not yet verified |
| installedverified | The application environment is installed and successfully verified |
| installingautomatically | The application environment is not installed, but is being installed automatically |
| installingmanually | The application environment is not installed, but is being installed manually |
| notinstallable | The application environment is not installed and not installable |
| pendingremoval | The application environment is installed, but is due to be removedwill be removed as soon as possible |
| Removing | The application environment is installed, but it is being removed |

### B.4. ApplicationHandle\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| executable | Access based on running directly the main executable of the application \(this MAY require set-up of the environment\) |
| module | Access based on loading modules via Environment Modules \(http://modules.sourceforge.net/\) |
| path | Access based on using an explicit path where the software is installed on the file system |
| softenv | Access based on loading SoftEnv keys \(http://www.mcs.anl.gov/systems/software/softenv/softenv-intro.html\) |

### B.5. Benchmark\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| bogomips | BogoMips |
| cfp2006 | SPEC CFP 2006 floating point benchmark |
| cint2006 | SPEC CINT 2006 integer benchmark |
| linpack | LINPACK benchmark |
| specfp2000 | SPECfp2000 floating point benchmark |
| specint2000 | SPECint2000 integer benchmark |

### B.6. Capability\_t

List of values initially drafted from \[OMII-DJRA2.1, OGF-GFD80\]. Open enumeration:

| Value | Description |
| :--- | :--- |
| data.access.flatfiles | capacity of providing access to a flat file |
| data.access.relational | capacity of providing access to a relational data source |
| data.access.xml | capacity of providing access to an XML data source |
| data.management.diskimage | capacity of managing the creation of mountable disk images objects |
| data.management.file | capacity of managing the creation of files |
| data.management.genericobject | capacity of managing the creation of generic storage objects |
| data.management.replica | capacity of managing the creation of file replicas upon request |
| data.management.storage | capacity of managing a storage resource, from simple systems like disk-servers to complex hierarchical systems |
| data.management.transfer | capacity of managing a transfer of files from the start to the completion |
| data.naming.resolver | capacity of resolving one name to another \(for example, search the associated abstract name to a certain human-oriented name\) |
| data.naming.scheme | capacity of attaching names to data resources. \(To evaluate if it should moved to the main category infrastructure instead of data\). In OGSA, a three-level naming scheme is defined: \(1\) human-oriented name, \(2\) abstract name and \(3\) address |
| data.transfer | capacity of moving a file from one network location to another. It refers to the actual transfer \(e.g., as performed by protocols like FTP, GridFTP, or HTTP\) |
| executionmanagement.candidatesetgenerator | capacity of determining the set of resources in which a unit of work MAY execute |
| executionmanagement.dynamicvmdeploy | capacity of dynamically deploying a virtual machine image in a worker node |
| executionmanagement.executionandplanning | capacity of building schedules for jobs, that is, the capability of defining mappings between services and resources, possibly with time constraints |
| executionmanagement.jobdescription | capacity of letting users be able to describe a job submission request based on a machine-processable language |
| executionmanagement.jobexecution | capacity of executing a job or set of jobs. |
| executionmanagement.jobmanager | capacity of managing the execution of a job or set of jobs from start to finish |
| executionmanagement.reservation | capacity of managing reservation of resources for future usage |
| information.discovery | capacity of locating unknown resources or services, possibly satisfying a set of requirements |
| information.logging | capacity of recording data, often chronologically |
| information.model | capacity of modelling resources based on a community accepted definition |
| information.monitoring | capacity of periodically observing measurements, transform them and make available to users or other applications |
| information.provenance | capacity of providing long-term storage of information related to Grid activity and to let this information be accessed by users or other applications. |
| security.accounting | capacity of systematically recording, reporting, and analyzing the usage of resources |
| security.attributeauthority | capacity of associating a user with a set of attributes in a trusted manner to a relying party, by way of digitally signed assertions |
| security.authentication | capacity of providing authentication mechanisms for Grid users machine and services |
| security.authorization | capacity of handling authorization aspects, making authorization decisions about the subject and the requested mode of access based upon combining information from a number of distinct sources |
| security.credentialstorage | capacity of providing an online credential repository that allows users to securely obtain credentials when and where needed |
| security.delegation | capacity for a user to give a service the authority to undertake specific activities or decisions on its behalf |
| security.identymapping | capacity of mapping Grid-level credentials to local level credentials \(e.g., mapping a user X.509 certificate into a UNIX account\). |

### 

### B.7. CloudComputingInstanceState\_t

For the values of this type, we RECOMMEND the following syntax:

* namespace:state
* namespace:state:substate

Open enumeration:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Value</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">bes:error</td>
      <td style="text-align:left">(a terminal state): the activity has failed due to some system error/failure
        event, such as failure of a computational resource that the activity was
        running on</td>
    </tr>
    <tr>
      <td style="text-align:left">bes:finished</td>
      <td style="text-align:left">(a terminal state): the activity has terminated successfully. Successful
        termination implies that the activity exited of its own accord rather than
        due to some failure in the BES or of the computational resources on which
        the activity was running. Note that a successfully terminating activity
        MAY nevertheless return an error code as its return value</td>
    </tr>
    <tr>
      <td style="text-align:left">bes:pending</td>
      <td style="text-align:left">
        <p>the service has created a record for an activity but not yet instantiated
          it on a</p>
        <p>suitable computational resource or enabled it to start execution on such
          a resource</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">bes:running</td>
      <td style="text-align:left">the activity is executing on some computational resource</td>
    </tr>
    <tr>
      <td style="text-align:left">bes:terminated</td>
      <td style="text-align:left">
        <p>(a terminal state): the client &#x2013; which might be some system administrator</p>
        <p>(and hence not necessarily the client who originated the request to create
          the activity) &#x2013; has issued a TerminateActivity request</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">bes:suspended</td>
      <td style="text-align:left">the activity is currently in suspended state. Some resources for the activity
        may be reserved into the the system, but no computing resources are utilized</td>
    </tr>
  </tbody>
</table>For more information on the BES state model, see \[BES\].

### B.8. CloudComputingInstanceType\_t

Closed enumeration:

| Value | Description |
| :--- | :--- |
| collectionelement | A VM submitted as part of a collection of individual VMs which do not communicate among them |
| parallelelement | A VM submitted as part of a collection of individual VM which communicate among them \(ex. part of a computing cluster\) |
| single | An individual stand-alone VM |

### B.9. CloudComputingManagerType\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| openstack | OpenStack |
| opennebula | OpenNebula |
| wnodes | WNoDeS |
| synnefo | Synnefo |
| cloudstack | Apache CloudStack |
| Vcloud | VMWare vCloud |

### B.10. CloudResourceName\_t

Closed enumeration:

| Value | Description |
| :--- | :--- |
| flavour | Resource flavour, comprensive of disk, CPU, ram, memory and network |
| network | Network usage \(amount of kilobytes inbound/outbound from the VM network interfaces\) |
| networkin | Network inbound usage \(amount of kilobytes inbound from the VM network interfaces\) |
| networkout | Network outbound usage \(amount of kilobytes outbound from the VM network interfaces\) |
| cpu | Number of vCPU associated to the VM. A vCPU seen by the OS is considered in use, even if it is in idle mode |
| gpu | Number of vGPU associated to the VM. A vGPU seen by the OS is considered in use, even if it is in idle mode |
| memory | RAM associated to the VM in MBs. Memory associated to the VM, and seen by the OS, is accounted even if free in the OS space. |
| storage | Storage associated to the VM in GBs. It includes all the type of storage associated to the VM, both block storage or ephemeral storage or OS disk image storage |
| ephemeralstorage | Ephemeral storage associated to the VM in GBs |
| blockstorage | Block storage associated to the VM in GBs. The entire amount of the block storage device disk is accounted, even if storage is not used by the OS |
| osdiskstorage | Storage associated to the VM Image OS disk in GB. The entire amount of the block storage device disk is accounted, even if storage is not used by the OS. |
| softwarelicense | License for the usage of software on the VM image disk. This shall include all the licensing prices for all the software installed in the VM besides the OS |
| oslicense | License for the usage of the OS on the VM image disk. |

### B.11. ComputingActivityState\_t

For the values of this type, we RECOMMEND the following syntax:

* namespace:state
* namespace:state:substate

Open enumeration:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Value</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">bes:failed</td>
      <td style="text-align:left">(a terminal state): the activity has failed due to some system error/failure
        event, such as failure of a computational resource that the activity was
        running on</td>
    </tr>
    <tr>
      <td style="text-align:left">bes:finished</td>
      <td style="text-align:left">(a terminal state): the activity has terminated successfully. Successful
        termination implies that the activity exited of its own accord rather than
        due to some failure in the BES or of the computational resources on which
        the activity was running. Note that a successfully terminating activity
        MAY nevertheless return an error code as its return value</td>
    </tr>
    <tr>
      <td style="text-align:left">bes:pending</td>
      <td style="text-align:left">
        <p>the service has created a record for an activity but not yet instantiated
          it on a</p>
        <p>suitable computational resource or enabled it to start execution on such
          a resource</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">bes:running</td>
      <td style="text-align:left">the activity is executing on some computational resource</td>
    </tr>
    <tr>
      <td style="text-align:left">bes:terminated</td>
      <td style="text-align:left">
        <p>(a terminal state): the client &#x2013; which might be some system administrator</p>
        <p>(and hence not necessarily the client who originated the request to create
          the activity) &#x2013; has issued a TerminateActivity request</p>
      </td>
    </tr>
  </tbody>
</table>For more information on the BES state model, see \[BES\].

This attribute type is an open enumeration. Examples of additional values are:

* a middleware provider is using its own state model defined before the BES specification:
  * NorduGrid defines the state _accepting_ which MAY be represented as \(see \[ng-schema\], page 28\):
    * nordugrid:accepting
  * gLite WMS defines the state _scheduled_ which MAY be represented as:
    * glite-wms:scheduled
  * gLite CREAM defines the state _registered_ which MAY be represented as:
    * glite-cream:registered
    * \(see https://edms.cern.ch/document/595770\)
* a middleware provider defined an extension of BES state model which is not part of an official OGF specification
  * NorduGrid defined an extension the bes:pending by adding two substates:
    * nordugrid-bes:pending:accepting
    * nordugrid-bes:pending:accepted

### B.12. ComputingActivityType\_t

Closed enumeration:

| Value | Description |
| :--- | :--- |
| collectionelement | A job submitted as part of a collection of individual jobs which do not communicate among them |
| parallelelement | A job submitted as part of a collection of individual jobs which communicate among them |
| single | An individual stand-alone job |
| workflownode | A job submitted as part of a workflow |

### B.13. ComputingManagerType\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| bqs | CC-IN2P3 Batch Queue System |
| condor | Condor |
| fork | Based on fork primitive |
| loadleveler | IBM LoadLeveler |
| lsf | Platform Load Sharing Facility |
| openpbs | Open PBS |
| sungridengine | Sun Grid Engine |
| torque | Torque |
| torquemaui | Torque with MAUI |

### B.14. ContactType\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| general | Contact for persons to ask about general issues |
| security | Contact for persons responsible for security |
| sysadmin | Contact for the system administrators |
| usersupport | Contact for user support |

### B.15. ContextualizationName\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| cloud-init | Ubuntu CloudInit |
| bash | Generic bash script |

### B.16. CPUMultiplicity\_t

Closed enumeration:

| Value | Description |
| :--- | :--- |
| multicpu-multicore | The execution environment is run by multiple physical CPUs with a multiple cores each |
| multicpu-singlecore | The execution environment is run by multiple physical CPUs with a single core each |
| singlecpu-multicore | The execution environment is run by a single physical CPU with multiple cores |
| singlecpu-singlecore | The execution environment is run by a single physical CPU with a single core |

### B.17. CPUVirtualizationT\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| emulation | Full virtualization with emulation |
| paravirtualization | Para-virtualization |
| hardware | Hardware assisted virtualization |

### B.18. DataStoreType\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| disk | The storage capacity is provided by magnetic disks |
| optical | The storage capacity is provided by optical disks |
| tape | The storage capacity is provided by magnetic tapes |

### B.19. DateTime\_t

The DateTime\_t is based on the extended ISO 8061 format:

* \[-\]CCYY-MM-DDThh:mm:ss\[Z\|\(+\|-\)hh:mm\]

This data type maps the dateTime XSD simple type. We restrict this syntax to UTC time zone as follows:

* yyyy '-' mm '-' dd 'T' hh ':' mm ':' ss 'Z'

### B.20. DiskVirtualizationT\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| qcow2 | QCOW2 |
| raw | RAW Image |
| vmdk | VMDK |

### B.21. DN\_t

Distinguished Name as defined by RFC 4514 \(http://www.rfc-editor.org/rfc/rfc4514.txt\).

X.509 uses a X.500 namespace, represented as several Relative Domain-Names \(RDNs\) concatenated by forward-slashes. The final RDN is usually a single common name \(CN\), although multiple CNs are allowed.

### B.22. EndpointAuthentication\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| none | No authentication is configured on the endpoint |
| x509 | X590 authentication is configured |
| oidc | OpenID Connect authentication is configured |
| saml2 | SAML 2.0 authentication is configured |

### B.23. EndpointHealthState\_t

Closed enumeration:

| Value | Description |
| :--- | :--- |
| critical | It was possible to check the state of the endpoint and either it was not running or it was above some "critical" threshold |
| ok | It was possible to check the state of the endpoint and it appeared to be functioning properly |
| other | It was possible to check the state of the endpoint, but this is not covered by the defined states |
| unknown | It was not possible to check the state of the endpoint |
| warning | It was possible to check the state of the endpoint, but it appeared to be above some "warning" threshold or did not appear to be working properly |
| downtime | It was possible to check the state of the endpoint, but it appeared to be on maintenance and may not work properly |

### B.24. EndpointTechnology\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| corba | The endpoint is implemented using CORBA technologies |
| jndi | The endpoint is implemented using JNDI |
| webservice | The endpoint is implemented as a Web Service |

### B.25. ExpirationMode\_t

Closed enumeration:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Value</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">neverexpire</td>
      <td style="text-align:left">Support for files with infinite lifetime: they MAY only be removed by
        authorized clients, not by the storage system itself</td>
    </tr>
    <tr>
      <td style="text-align:left">releasewhenexpired</td>
      <td style="text-align:left">Support for files that have finite lifetimes and on expiration will be
        removed by the storage system</td>
    </tr>
    <tr>
      <td style="text-align:left">warnwhenexpired</td>
      <td style="text-align:left">
        <p>Support for files that have finite lifetimes, but on expiration cannot
          be removed by the storage system itself. The data content of an expired
          file MAY be deleted if it MAY be recovered from an archive. New store operations
          MAY fail for certain clients until (some of the) expired files have either
          been removed by</p>
        <p>authorized clients, or have had their lifetimes increased</p>
      </td>
    </tr>
  </tbody>
</table>### B.26. ExtendedBoolean\_t

Closed enumeration:

| Value | Description |
| :--- | :--- |
| false | boolean false |
| true | boolean true |
| undefined | the value cannot be measured |

### B.27. HostAccessInfo\_t

Closed enumeration:

| Value | Description |
| :--- | :--- |
| none | No default credentials are present in the machine, access credentials shall be injected by the middleware |
| passwd | Pre-set username/password |
| rsa | Pre-set RSA key set |

### B.28. InterfaceName\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| ogf.bes | The Open Grid Forum Basic Execution Service |
| ogf.srm | The Open Grid Forum Storage Resource Manager |

### B.29. JobDescription\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| condor | Condor |
| egee:jdl | EGEE Job Description Language |
| globus:rsl | Globus RSL |
| nordugrid:xrsl | Nordugrid XSRL \[XSRL\] |
| ogf:jsdl:1.0 | Job Description Submission Language 1.0 |

### B.30. License\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| commercial | Commercial license |
| opensource | Open Source license approved by the OSI \(Open Source Initiative\) |
| unknown | Unknown license type |

### B.31. LocalID\_t

The base type is the string with the following restrictions:

* first char in a-zA-Z
* following characters in \[\w\-\.\:\]
  * \w = \[a-zA-Z\_0-9\]

### B.32. NetworkInfo\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| 100megabitethernet | Network based on 100 MBit/s Ethernet technology |
| gigabitethernet | Network based on 1 GBit/s Ethernet technology |
| infiniband | Network based on Infiniband technology |
| myrinet | Network based Myrinet technology |

### B.33. NetworkConfigurationProtocol\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| all | All protocols |
| tcp | TCP protocol |
| udp | UDP protocol |
| cmp | CMP protocol |
| ipsec | IPSec protocol |

### B.34. NetworkConfigurationDirection\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| inbound | Inbound connection |
| outbound | Outbound connection |

### B.35. NetworkConfigurationAddressRange\_t

The base type is the string limited to the CIDR range address notation: like 192.168.0.0/16, fc00::/7 or 8.8.8.8./32:

### B.36. NetworkConfigurationPort\_t

The base type is the string limited to one of the following possible formats:

* Specification of a port: 80
* Specification of multiple ports: 80,443
* Specification of a range of ports: 25000:25009

### B.37. NetworkType\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| public | Connection to an externally routable network, more networks can be available. |
| public\_only | Exclusive connection to an externally routable network. |
| private | Connection a private network, more networks can be available. |
| private\_only | Exclusive connection to a private network. |

### B.38. NetVirtualizationT\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| none | No network isolation |
| vswitch | vSwitch isolation |
| ebtables | EBtables isolation |
| vlan | VLAN isolation |
| firewall | Firewall isolation |

### B.39. OSFamily\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| linux | Family of operating systems based on Linux kernel |
| macosx | Family of operating systems based on MacOS X |
| solaris | Family of operating systems based on Solaris |
| windows | Family of operating systems based on Windows |

### B.40. OSName\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| aix | AIX |
| centos | CentOS |
| debian | Debian |
| fedoracore | RedHat Fedora |
| gentoo | Gentoo Linux |
| leopard | Mac OS X 10.5 \(Leopard\) |
| linux-rocks |  |
| mandrake | Mandrake |
| redhatenterpriseas | RedHat Enterprise Server |
| scientificlinux | Scientific Linux |
| scientificlinuxcern | Scientific Linux CERN |
| suse | SUSE |
| ubuntu | Ubuntu |
| windowsvista | Microsoft Windows Vista |
| windowsxp | Microsoft Windows XP |

### B.41. Period\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| once | The metric is calculated once in the lifetime of the service |
| asaccounted | The metric is calculated with the same granularity as it is accounted |
| daily | The metric is calculated daily |
| monthly | The metric is calculated monthly |
| yearly | The metric is calculated yearly |

### B.42. Platform\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| amd64 | AMD 64bit architecture |
| i386 | Intel 386 architecture |
| itanium | Intel 64-bit architecture |
| powerpc | PowerPC architecture |
| sparc | SPARC architecture |

### B.43. PolicyScheme\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| basic | The basic scheme |
| gacl | GridSite Access Control List |

A policy scheme is defined by a syntax for rules and by a matching algorithm defining how a string MAY be matched against the published rules. For the _basic_ policy scheme, the following syntax MUST be used \(defined in EBNF form \[EBNF\]\):

* BASIC RULE ::= \( DN\_NAME \| VO\_NAME \| ‘ALL’ \)
* DN\_RULE ::= ‘dn:’ DN\_NAME
* VO\_RULE ::= ‘vo:’ \[a-zA-Z0-9-\_\.\]+
* DN\_NAME ::=

As a matching algorithm, the basic scheme adopts the exact match \(if at least one rule provides an exact match or the rule ‘ALL’ is present, then the subject is authorized to be mapped into the related share\). More complex policy schemes SHOULD be defined in profile documents.

Examples of policies expressed using the basic syntax are:

* dn:/C=XX/O=YYYY/OU=Personal Certificate/L=ZZZZ/CN=NAME SURNAME
  * matches the user proving to have a certificate identified by this DN
* vo:/vo\_a
  * matches all the users proving to be part of the vo\_a

### B.44. QualityLevel\_t

Closed enumeration:

| Value | Description |
| :--- | :--- |
| development | The component is under active development both in functionalities and interfaces |
| pre-production | The component has completed the development and passed the testing phase; it is being used in real world scenarios |
| production | The component completed the development and is considered stable for real world scenarios |
| testing | The component has completed the development phase and is under testing |

### B.45. ReservationPolicy\_t

Closed enumeration:

| Value | Description |
| :--- | :--- |
| mandatory | Jobs MUST be submitted only via advance reservation |
| none | No reservation is supported |
| optional | Jobs MAY be submitted via advance reservation, but this is not required |

### B.46. ResourceScope\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| any | Any scope \(commercial or non-commercial\) |
| commercial | Access by commercial organizations for commercial usage |
| noncommercial | Access by no-profit or public organizations for non-commercial usage |
| research | Access for research by any organization, commercial or non-commercial |
| noncommercialresearch | Access for research by no-profit or public organizations for non-commercial usage |
| Institutions | Access for public organization, institutions or governments for any scope |
| euonly | Access restricted to users of EU based countries |
| owncountryonly | Access restricted to users of the same country of the provider |

### B.47. RetentionPolicy\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| custodial | Low probability of loss |
| output | An intermediate level and is appropriate for data which MAY be replaced by lengthy or effort-full processes |
| replica | The highest probability of loss, but is appropriate for data for which a certain amount of loss MAY be tolerated, in particular when other copies MAY be accessed in a timely fashion |

### B.48. SchedulingPolicy\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| fairshare | Statistically guarantees the allocated share |
| fifo | First-In First-Out |
| random | Random choice |

### B.49. ServiceType\_t

The RECOMMENDED syntax is in reverse-DNS prefix. The first element is a top-level domain, while the second element is a namespace \(the namespace MAY be related to a middleware name, an organization or other concepts; org.ogf.glue is reserved for the OGF GLUE Working Group\). The defining body SHOULD have a claim on the corresponding forward DNS name \(e.g., org.nordugrid.arex SHOULD be defined by the owners of the nordugrid.org domain name\).

 Open enumeration:

| Value | Description |
| :--- | :--- |
| org.ogf.glue\* | Prefix reserved for the OGF GLUE Working Group |
| org.glite.fts | gLite File Transfer Service |
| org.glite.lb | gLite Logging and Booking Service |
| org.glite.wms | gLite Workload Management Service |
| org.nordugrid.arex | NorduGrid Resource Coupled Execution Service |
| org.nordugrid.isis | NorduGrid Information Index Service |
| org.nordugrid.storage | NorduGrid Storage Service |
| org.teragrid gridftp | TeraGrid GridFTP |
| org.teragrid.condor-g | TeraGrid Condor-g |
| org.teragrid.globus-mds4 | TeraGrid Globus MDS 4 |
| org.teragrid.gpfs | TeraGrid GPFS |
| org.teragrid.gsi-openssh | TeraGrid gsi-enabled openssh |
| org.teragrid.prewsgram | TeraGrid pre-WS Globus GRAM |
| org.teragrid.rft | TeraGrid Reliable File Transfer |
| org.teragrid.srb | TeraGrid Storage Resource Broker |
| org.teragrid.ws-delegation | TeraGrid WS-Delegation Service |
| org.teragrid.ws-gram | TeraGrid WS-GRAM Service |
| org.teragrid.ws-ogsadai | TeraGrid OGSA-DAI |
| org.cloud.iaas | Cloud Infrastructure-as-a-Service |
| org.cloud.saas | Cloud Storage-as-a-Service |

### B.50. ServingState\_t

Closed enumeration:

| Value | Description |
| :--- | :--- |
| closed | The endpoint is not accepting request nor is serving them |
| draining | The endpoint is not accepting requests, but is serving requests in the queue |
| production | The endpoint is both accepting and serving requests |
| queueing | The endpoint is accepting requests, but is not serving them |

### B.51. Staging\_t

Closed enumeration:

| Value | Description |
| :--- | :--- |
| none | No staging of files supported |
| stagingin | Automatic staging in of files supported |
| staginginout | Automatic staging in and out of files supported |
| stagingout | Automatic staging out of files supported |

### B.52. StorageAccessProtocol\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| afs | Andrew File System protocol |
| dcap | DCache access protocol |
| file | POSIX access |
| gsidcap | DCAP with GSI authentication |
| gsiftp | FTP with GSI authentication |
| gsirfio | RFIO with GSI authentication |
| http | HyperText Transfer Protocol |
| https | Secured HyperText Transfer Protocol |
| nfs | Network File System protocol |
| rfio | Remote File Input/Output protocol |
| root | File transfer protocol for the ROOT framework |
| xrootd | xrootd protocol |

### B.53. StorageCapacity\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| online | Available storage capacity accessible in less than a minute in normal operating conditions |
| installedonline | Online storage capacity including temporarily unavailable portions which would be accessible in less than a minute in normal operating conditions |
| nearline | Available storage capacity accessible in more than a minute and less than two days without human intervention in normal operating conditions |
| installednearline | Nearline storage capacity including temporarily unavailable portions which would be accessible in more than a minute and less than two days without human intervention in normal operating conditions |
| offline | Storage capacity possibly requiring human intervention for access in normal operating conditions |
| cache | Storage capacity accessible in less than a minute used internally by the storage system and not directly exposed to the user |

### B.54. StorageManagerType\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| castor | CERN Advanced STOrage manager, disk and tape management system |
| dcache | Disk Cache, disk managing system with ability to control tape backends \(e.g., Enstore\) |
| enstore | Tape Storage system, tape management system |
| gpfs | General Parallel File System, disk management system |
| sse | Smart Storage Element, disk management system |
| tsm | IBM Tivoli Storage Manager, disk and tape management system |
| swift | OpenStack SWIFT |
| cdmi-proxy | CDMI Proxy |

### B.55. VirtType\_t

Open enumeration:

| Value | Description |
| :--- | :--- |
| emulation | Full virtualization with emulation |
| paravirtualization | Para-virtualization |
| hardware | Hardware assisted virtualization |
| vgpu | NVidia vGPU |

