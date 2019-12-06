---
description: Section 8
---

# Conceptual Model of the Cloud Computing Service

The conceptual model of the Cloud Infrastructure as a Service is based on the main entities and uses specializations of the Service, Endpoint, Share, Manager and Resource.  Further cloud computing related concepts such as ComputingImage, ServicePrice and Benchmark are introduced.

![](.gitbook/assets/0%20%282%29.png)

**Figure 3 Entities and relationships for the Cloud Compute Service conceptual model.**

In this section, we extensively use the concepts of Virtual Machine \(VM\), Virtual Machine status \(halted, pending, running, suspended\), Virtual Accelerator and Cloud Middleware, these are defined as follows:

* A Virtual Machine \(instance\) is a compute environment that runs a software configuration \(for example operating system, an application server, and applications\) from a given Virtual Machine image. Every VM is a fully functioning virtual computer which can be accessed via the network. The VM has a given set of virtual CPU, RAM and disk resources. The VM has usually one or more virtual network interfaces, to which are assigned public or private IPs.
* A Virtual Machine is in Running state when the VM is actively consuming system resources in terms of RAM, CPU, disk and network. Some of the physical resources may be shared with other VMs or reserved for private VM usage.
* A Virtual Machine is in Suspended state when the VM is not running, but it still has resources reserved on the system. A VM in suspended state usually consumes only disk space for the OS, and optionally additional disk space for RAM snapshot.
* A Virtual Machine is in Pending state when the VM is in the process of gathering resources from the system \(ex. acquiring VM OS disk, CPU resources, initializing system\). Machines in Pending state uses system resources but are not yet available for users to access.
* A Virtual Machine is in Halted state when the VM has uses no resources in the system, but its template and configuration is still stored into the system \(so the machine may be started again, but with a clean configuration\).
* A Virtual Machine can be equipped with one or more Virtual Accelerators. A Virtual Accelerator is defined as any kind of computing device that is provided by the virtualization capability of the system to the Virtual Machine.
* A Cloud Middleware is a piece of computer software that relies on virtualization capabilities to provide Virtual Machines on-demand to final users. The Cloud Middleware may provide not only virtual servers \(namely Infrastructure as a Service feature\), but also storage \(Storage as a Service\) and other rich services \(Platform as a Service, etc…\).

Throughout the specification, we also use the concept of Cloud Storage extent to mean the capabilities and management of the various media that exist to store data and allow data retrieval.

In the model, the Cloud service price is represented via separated CloudServicePrice entities associated to single accounted resources \(eg. CPU, Memory, Disk, Network IN/OUT, Software Licensing\). Each resource price is calculated on consumption or fixed fee basis and targeted to a given user base \(eg. commercial, no-profit organizations, research\). The total price for a CloudComputingInstance can be obtained by adding all the price elements from the associated CloudComputingImage and CloudComputingInstanceType.

A Cloud Computing service relates directly to a Cloud Infrastructure-as-a-Service \(IaaS\) system, which allows the user to run on-demand Virtual Appliances for computing purposes. For different Cloud computing services such as Platform-as-a-Service and Software-as-a-Service, the generic Grid platform computing model \(GLUE2 Computing entities\), described in Chapter 7, may be a better fit.

## 8.1. CloudComputingService

  
The CloudComputingService class is a specialization of the Service class for a service offering Cloud Infrastructure as a Service computational capacity. The CloudComputingService entity is the main logical unit, and aggregation point for several entities together modeling a computing infrastructure capability in a Cloud system. A CloudComputingService is capable of executing CloudComputingInstance on its associated resources. The resources behind the CloudComputingService are described via the CloudComputingManager, CloudComputingInstanceType, CloudComputingImage and Benchmark entities. The governing policies and status of the resources are given by the CloudComputingShare elements. The CloudComputingInstance of a CloudComputingService are submitted and controlled via a CloudComputingEndpoint.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Entity</th>
      <th style="text-align:left">Inerits from</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">CloudComputingService</td>
      <td style="text-align:left">Service</td>
      <td style="text-align:left">
        <p>An abstracted, logical view of software and hardware components that participate
          in the creation of a computational capacity in a Cloud environment, in
          form of Cloud Virtual Machines instances. A Cloud Computing Service exposes
          zero or more Cloud Computing Endpoints having well-defined interfaces,
          zero or more Cloud Computing Shares and zero or more Cloud Computing Managers.</p>
        <p>The computing service is autonomous and denotes a weak aggregation among
          Computing Endpoints, the underlying Computing Managers and the defined
          Computing Shares. The Computing Service enables the identification of the
          whole set of entities providing the computing functionality with a persistent
          name.</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left"><em>CreationTime</em>
      </td>
      <td style="text-align:left"><em>DateTime_t</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Timestamp describing when the entity instance was generated</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Validity</em>
      </td>
      <td style="text-align:left"><em>UInt64</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"><em>s</em>
      </td>
      <td style="text-align:left"><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant. After that period has elapsed, the information SHOULD NOT be considered relevant</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>ID [key]</em>
      </td>
      <td style="text-align:left"><em>URI</em>
      </td>
      <td style="text-align:left"><em>1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>A global unique ID</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Name</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Human-readable name</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>OtherInfo</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>*</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Capability</em>
      </td>
      <td style="text-align:left"><em>Capability_t</em>
      </td>
      <td style="text-align:left"><em>*</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>The provided capability according to the Open Grid Service Architecture (OGSA) architecture [OGF-GFD80] (this is the union of all values assigned to the capability attribute of the endpoints part of this service)</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Type</em>
      </td>
      <td style="text-align:left"><em>ServiceType_t</em>
      </td>
      <td style="text-align:left"><em>1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>The type of service according to a namespace-based classification. Examples are org.openstack or org.opennebula</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>QualityLevel</em>
      </td>
      <td style="text-align:left"><em>QualityLevel_t</em>
      </td>
      <td style="text-align:left"><em>1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Maturity of the service in terms of quality of the software components</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>StatusInfo</em>
      </td>
      <td style="text-align:left"><em>URI</em>
      </td>
      <td style="text-align:left"><em>*</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Web page providing additional information like monitoring aspects</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Complexity</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Human-readable summary description of the complexity in terms of the number of endpoint types, shares and resources. The syntax should be: endpointType=X, share=Y, resource=Z.</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Desciption</td>
    </tr>
    <tr>
      <td style="text-align:left">TotalVM</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Total number of VM known to the system (the sum of RunningVM, PendingVM,
        SuspendedVM and HaltedVM)</td>
    </tr>
    <tr>
      <td style="text-align:left">RunningVM</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The number of VM in Running state (VMs actively consuming the system resources)</td>
    </tr>
    <tr>
      <td style="text-align:left">PendingVM</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The number of VM in Pending state (VM in preparation to be running on
        the system)</td>
    </tr>
    <tr>
      <td style="text-align:left">SuspendedVM</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The number of VM in Suspended state (VMs not running but with reserved
        resources on the system)</td>
    </tr>
    <tr>
      <td style="text-align:left">HaltedVM</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The number of VM in Halted state (VMs not running on the system with no
        resources reserved)</td>
    </tr>
    <tr>
      <td style="text-align:left">AUP</td>
      <td style="text-align:left">URI</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Link to the service Acceptable User Policy (AUP) or Terms and Conditions
        for the usage of the service. This shall be in URL format.</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingEndpoint.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">A CloudComputingService is associated with zero or more endpoints (interfaces)</td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingShare.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">A CloudComputingService offers zero or more computing shares.</td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingManager.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">A CloudComputingService offers zero or more computing manager.</td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left">Extension.Key</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The entity MAY be extended via key-value pairs.</td>
    </tr>
    <tr>
      <td style="text-align:left">Contact.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">A Cloud computing service has zero or more contacts.</td>
    </tr>
    <tr>
      <td style="text-align:left">Location.ID</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">A Cloud computing service is primarily located at a location.</td>
    </tr>
    <tr>
      <td style="text-align:left">Service.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">A Cloud computing service is related to zero or more services.</td>
    </tr>
  </tbody>
</table>A simple CloudComputingService is formed by a CloudComputingEndpoint exposing an interface for VM instantiation and control. The CloudComputingService always aggregates CloudComputingEndpoints, CloudComputingShares, CloudComputingManagers, CloudComputingImage and CloudComputingInstanceType forming a connected set. In other words, Endpoint A exposing InstanceType A and Image A served by Manager A via Share A and Endpoint B exposing InstanceType B and Image B served by Manager B via Share B form two different Computing Services. On the other hand, Endpoint A exposing InstanceType A and Image A served by Manager A via Share A and Endpoint B exposing InstanceType A and Image A served by Manager A via Share B form a single Computing Service.

## CloudComputingEndpoint

The CloudComputingEndpoint is a specialization of the Endpoint class for a service possessing cloud Infrastructure-as-a-Service capability. The class represents an endpoint which is used to create, control and monitor Cloud computing activities. The specific information concerns service status and interface capabilities. This class provides attributes that MAY be used to publish summary information about VM instantiated via a particular Endpoint. Such attributes are optional and may not always be measurable \(e.g., in the case of a stateless Endpoint which does not keep information about the VM instantiated through it\).

<table>
  <thead>
    <tr>
      <th style="text-align:left">Entity</th>
      <th style="text-align:left">Inherits from</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">CloudComputingEndpoint</td>
      <td style="text-align:left">Endpoint</td>
      <td style="text-align:left">A network Endpoint for creating, monitoring, and controlling computational
        Cloud Activities called Virtual Machines instances. It MAY also be used
        to expose complementary capabilities (e.g., resource reservation, attached
        block storage, VM image manipulation).</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left"><em>CreationTime</em>
      </td>
      <td style="text-align:left"><em>DateTime_t</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Timestamp describing when the entity instance was generated</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Validity</em>
      </td>
      <td style="text-align:left"><em>UInt64</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"><em>s</em>
      </td>
      <td style="text-align:left"><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant. After that period has elapsed,</em>  <em>the information SHOULD NOT be considered relevant</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>ID [key]</em>
      </td>
      <td style="text-align:left"><em>URI</em>
      </td>
      <td style="text-align:left"><em>1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>A global unique ID</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Name</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Human-readable name</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>OtherInfo</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>*</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>URL</em>
      </td>
      <td style="text-align:left"><em>URI</em>
      </td>
      <td style="text-align:left"><em>1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Network location of the endpoint to contact the related service</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Capability</em>
      </td>
      <td style="text-align:left"><em>Capability_t</em>
      </td>
      <td style="text-align:left"><em>*</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>The provided capability according to the OGSA architecture</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Technology</em>
      </td>
      <td style="text-align:left"><em>EndpointTechnology_t</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Technology used to implement the endpoint</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>InterfaceName</em>
      </td>
      <td style="text-align:left"><em>InterfaceName_t</em>
      </td>
      <td style="text-align:left"><em>1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Identification of the interface</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>InterfaceVersion</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>0..*</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Version of the interface</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>InterfaceExtension</em>
      </td>
      <td style="text-align:left"><em>URI</em>
      </td>
      <td style="text-align:left"><em>*</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Identification of an extension to the interface</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>WSDL</em>
      </td>
      <td style="text-align:left"><em>URI</em>
      </td>
      <td style="text-align:left"><em>*</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>URL of the WSDL document describing the offered interface (applies to Web Services endpoint)</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>SupportedProfile</em>
      </td>
      <td style="text-align:left"><em>URI</em>
      </td>
      <td style="text-align:left"><em>*</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>URI identifying a supported profile</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Semantics</em>
      </td>
      <td style="text-align:left"><em>URI</em>
      </td>
      <td style="text-align:left"><em>*</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>URI of a document providing a human-readable description of the semantics of the endpoint functionalities</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Implementor</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Main organization implementing this software component</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>ImplementationName</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Name of the implementation</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>ImplementationVersion</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Version of the implementation (e.g., major version.minor version.patch version)</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>QualityLevel</em>
      </td>
      <td style="text-align:left"><em>QualityLevel_t</em>
      </td>
      <td style="text-align:left"><em>1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Maturity of the endpoint in terms of quality of the software components</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>HealthState</em>
      </td>
      <td style="text-align:left"><em>EndpointHealthState_t</em>
      </td>
      <td style="text-align:left"><em>1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>A state representing the health of the endpoint in terms of its capability of properly delivering the functionalities</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>HealthStateInfo</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Textual explanation of the state endpoint</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>ServingState</em>
      </td>
      <td style="text-align:left"><em>ServingState_t</em>
      </td>
      <td style="text-align:left"><em>1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>A state specifying if the endpoint is accepting new requests and if it is serving the already accepted requests</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>StartTime</em>
      </td>
      <td style="text-align:left"><em>DateTime_t</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>The timestamp for the start time of the endpoint</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Authentication</em>
      </td>
      <td style="text-align:left"><em>EndpointAuthentication_t</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Name of the authentication method supported by the endpoint.</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>IssuerCA</em>
      </td>
      <td style="text-align:left"><em>DN_t</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Distinguished name of Certification Authority issuing the certificate for the endpoint</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>TrustedCA</em>
      </td>
      <td style="text-align:left"><em>DN_t</em>
      </td>
      <td style="text-align:left"><em>*</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Distinguished name of the trusted Certification Authority (CA), i.e., certificates issued by the CA are accepted for the authentication process</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>DowntimeAnnounce</em>
      </td>
      <td style="text-align:left"><em>DateTime_t</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>The timestamp for the announcement of the next scheduled downtime</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>DowntimeStart</em>
      </td>
      <td style="text-align:left"><em>DateTime_t</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>The starting timestamp of the next scheduled downtime</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>DowntimeEnd</em>
      </td>
      <td style="text-align:left"><em>DateTime_t</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>The ending timestamp of the next scheduled downtime</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>DowntimeInfo</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Description of the next scheduled downtime</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>CloudComputingService.ID</p>
        <p>[redefines Service.ID]</p>
      </td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">A Cloud endpoint is part of a Cloud Computing Service.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingShare.ID [redefines Share.ID]</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A Cloud endpoint MAY pass activities to zero or more Cloud computing shares.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>CloudComputingInstance.ID</p>
        <p>[redefines Activity.ID]</p>
      </td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">An Cloud endpoint has accepted and is managing zero or more Cloud Activities.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Extension.Key</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">The entity MAY be extended via key-value pairs.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">AccessPolicy.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A computing endpoint has assocated zero or more AccessPolicies.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>## CloudComputingShare

The CloudComputingShare class is the specialization of the main Share class for cloud Infrastructure-as-a-Service. A CloudComputingShare is a high-level concept introduced to model a utilization target for a pool of resources, sometimes referred to as Zones or Sites, defined by a homogeneous set of configuration parameters and characterized by single status information. A CloudComputingShare carries information about "policies" \(limits\) defined over all or a subset of resources and describes their dynamic status \(load\).

The CloudComputingShare stores also a set of CloudComputingImage and CloudComputingInstanceType, which are used to define respectively the virtual OS and the virtual hardware resources of the CloudComputingInstance running on the share. Such virtual OS and hardware resources are provided by the Share with a given Service Level Agreement \(SLA\). In case of the same CloudComputingInstanceType and CloudComputingImage are offered under different SLAs, multiple CloudComputingShares shall be created, one for each SLA.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Entity</th>
      <th style="text-align:left">Inherits from</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">CloudComputingShare</td>
      <td style="text-align:left">Share</td>
      <td style="text-align:left">A utilization target for a set of Cloud Computing Instance Types and Cloud
        Computing Images, defined by a set of homogeneous configuration parameters
        and characterized by single status information.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left"><em>CreationTime</em>
      </td>
      <td style="text-align:left"><em>DateTime_t</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Timestamp describing when the entity instance was generated</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Validity</em>
      </td>
      <td style="text-align:left"><em>UInt64</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"><em>s</em>
      </td>
      <td style="text-align:left">
        <p><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant. After that period has elapsed,</em>
        </p>
        <p><em>the information SHOULD NOT be considered relevant</em>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>ID [key]</em>
      </td>
      <td style="text-align:left"><em>URI</em>
      </td>
      <td style="text-align:left"><em>1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>A global unique ID</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Name</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Human-readable name</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>OtherInfo</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>*</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Description</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Description of this share</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left">TotalVM</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Total number of VM known to this computing share (the sum of RunningVM,
        PendingVM, SuspendedVM, HaltedVM)</td>
    </tr>
    <tr>
      <td style="text-align:left">RunningVM</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The number of VM running into this computing share</td>
    </tr>
    <tr>
      <td style="text-align:left">PendingVM</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The number of VM in Pending state (VM in preparation to be running on
        the system)</td>
    </tr>
    <tr>
      <td style="text-align:left">SuspendedVM</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The number of VM in suspended state (VMs not running but with reserved
        resources on this computing share)</td>
    </tr>
    <tr>
      <td style="text-align:left">HaltedVM</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The number of VM in Halted state (VMs not running on the system with no
        resources reserved on this computing share)</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxVM</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The maximum number of VM instances that can run on this share</td>
    </tr>
    <tr>
      <td style="text-align:left">InstanceMaxCPU</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The maximum number of Virtual CPU which can be assigned to a single VM
        for the VM in this share. Virtual CPU refers to CPUs as seen by the VM..</td>
    </tr>
    <tr>
      <td style="text-align:left">InstanceMaxRAM</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">MB</td>
      <td style="text-align:left">The maximum value (in MB) of virtual RAM memory which can be assigned
        to a single VM for the VM in this share. With virtual RAM memory it is
        intended the amount of RAM seen by the VM OS, not the physical RAM dedicated
        to the VM</td>
    </tr>
    <tr>
      <td style="text-align:left">NetworkInfo</td>
      <td style="text-align:left">NetworkInfo_t</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The type of internal network connection available among the managed Hosts.
        If many values are published then the various types of network MAY be available
        only within subsets of the Hosts; the Hosts properties SHOULD publish this
        information.</td>
    </tr>
    <tr>
      <td style="text-align:left">DefaultNetworkType</td>
      <td style="text-align:left">NetworkType_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The default network type that will be setup for an instance (e.g. public,
        private, private_only&#x2026;)</td>
    </tr>
    <tr>
      <td style="text-align:left">PublicNetworkName</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The name of the public network if any.</td>
    </tr>
    <tr>
      <td style="text-align:left">SLA</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Service Level Agreement for the VMs under this share. This can be an URL
        to the SLA document or a keyword representing the SLA itself (eg. 99.99%
        availability, best effort, etc&#x2026;)</td>
    </tr>
    <tr>
      <td style="text-align:left">ProjectID</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The native identifier of the corresponding local project to be used for
        this share (e.g. used by API users to know what is the project_id for OpenStack)</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>CloudComputingEndpoint.ID</p>
        <p>[redefines Endpoint.ID]</p>
      </td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A Cloud computing share MAY be consumed via one or more computing endpoints.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>CloudComputingInstanceType.ID</p>
        <p>[redefines Resource.ID]</p>
      </td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A Cloud computing share is defined on one or more computing resources.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>CloudComputingService.ID</p>
        <p>[redefines Service.ID]</p>
      </td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">A Cloud computing share participates in a computing service.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>CloudComputingInstance.ID</p>
        <p>[redefines Activity.ID]</p>
      </td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A Cloud computing share is being consumed by zero or more computing activities.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingImage.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A Cloud computing share provides zero or more VM Image templates</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudToStorageService.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">Link to the storage share used to store instances templates, VM images
        and/or attached disks</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingShareAccelerator.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A Cloud computing share provides zero or more sets of information about
        the usage level of virtual accelerator devices.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Extension.Key</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">The entity MAY be extended via key-value pairs.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">MappingPolicy.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A share has zero or more mapping policies.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>## CloudComputingShareAccelerator

The CloudComputingShareAccelerator contains all the information about the usage level of the virtual accelerator device bound to the cloud computing share.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Entity</th>
      <th style="text-align:left">Inherits from</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">CloudComputingShareAccelerator</td>
      <td style="text-align:left">Entity</td>
      <td style="text-align:left">The usage level of the virtual accelerator device for a given cloud computing
        share</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left"><em>CreationTime</em>
      </td>
      <td style="text-align:left"><em>DateTime_t</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Timestamp describing when the entity instance was generated</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Validity</em>
      </td>
      <td style="text-align:left"><em>UInt64</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"><em>s</em>
      </td>
      <td style="text-align:left">
        <p><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant. After that period has elapsed,</em>
        </p>
        <p><em>the information SHOULD NOT be considered relevant</em>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>ID [key]</em>
      </td>
      <td style="text-align:left"><em>URI</em>
      </td>
      <td style="text-align:left"><em>1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>A global unique ID</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Name</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Human-readable name</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>OtherInfo</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>*</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left">Type</td>
      <td style="text-align:left"><em>AccType_t</em>
      </td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The virtual accelerator architecture type.</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxNumber</td>
      <td style="text-align:left"><em>UInt32</em>
      </td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The maximum number of virtual accelerators that can be assigned to a single
        VM for any VM in this share.</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingShare.ID</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">A set of virtual accelerator information is related to a cloud computing
        share.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Extension.Key</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">The entity MAY be extended via key-value pairs.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>## CloudComputingManager

The CloudComputingManager class is a specialization of the Manager class for the computational capability \(Virtual Machines\) manager. The CloudComputingManager is responsible for the local control of resources. The CloudComputingManager layer may not be exposed directly to external clients or to the Virtual Machines themselves.

The Virtual Machine manager, also known as Cloud Middleware, normally uses a hypervisor, a piece of software, firmware or hardware which creates, runs and manages Virtual Machines or possibly containers. A Cloud Computing Service will usually have only one Cloud Computing Manager, but MAY have more. The class provides aggregated information on controlled resources, limits and also describes local storage extents accessible to the Virtual Machines.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Entity</th>
      <th style="text-align:left">Inherits from</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">CloudComputingManager</td>
      <td style="text-align:left">Manager</td>
      <td style="text-align:left">A software component locally managing one or more Cloud Instance Type
        virtual environments. It MAY also describe aggregated information about
        the managed resources. The Cloud Computing Manager is also known as Cloud
        Middleware.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left"><em>CreationTime</em>
      </td>
      <td style="text-align:left"><em>DateTime_t</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Timestamp describing when the entity instance was generated.</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Validity</em>
      </td>
      <td style="text-align:left"><em>UInt64</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"><em>s</em>
      </td>
      <td style="text-align:left">
        <p><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant. After that period has elapsed,</em>
        </p>
        <p><em>the information SHOULD NOT be considered relevant.</em>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>ID [key]</em>
      </td>
      <td style="text-align:left"><em>URI</em>
      </td>
      <td style="text-align:left"><em>1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>A global unique ID.</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Name</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Human-readable name.</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>OtherInfo</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>*</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax.</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>ProductName</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Name of the software product adopted as manager.</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>ProductVersion</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Version of the software product adopted as manager.</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left">HypervisorName</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Name of the underlying hypervisor that creates, runs and manages Virtual
        Machines.</td>
    </tr>
    <tr>
      <td style="text-align:left">HypervisorVersion</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Version of the hypervisor.</td>
    </tr>
    <tr>
      <td style="text-align:left">TotalCPUs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">Ph.CPU</td>
      <td style="text-align:left">The total number of physical CPUs cores accessible via any of the available
        Endpoints and managed by this Cloud Compute Manager. This value SHOULD
        represent the total installed capacity, i.e. including resources which
        are temporarily unavailable.</td>
    </tr>
    <tr>
      <td style="text-align:left">TotalRAM</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">MB</td>
      <td style="text-align:left">The total amount of RAM accessible via any of the available Endpoints
        and managed by this Cloud Compute Manager. This value SHOULD represent
        the total installed capacity, i.e. including resources which are temporarily
        unavailable.</td>
    </tr>
    <tr>
      <td style="text-align:left">InstanceMaxCPU</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The maximum number of Virtual CPU which can be assigned to a single VM.
        (Virtual CPU refers tothe CPU cores as seen by the VM OS).</td>
    </tr>
    <tr>
      <td style="text-align:left">InstanceMinCPU</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The minimum number of Virtual CPU which can be assigned to a single VM
        (Virtual CPU refers to the CPU cores as seen by the VM OS)</td>
    </tr>
    <tr>
      <td style="text-align:left">InstanceMaxRAM</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">MB</td>
      <td style="text-align:left">The maximum value (in MB) of virtual RAM memory which can be assigned
        to a single VM (with virtual RAM memory it is intended the amount of RAM
        seen by the VM OS, not the physical RAM dedicated to the VM).</td>
    </tr>
    <tr>
      <td style="text-align:left">InstanceMinRAM</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">MB</td>
      <td style="text-align:left">The minimum value (in MB) of virtual RAM memory which can be assigned
        to a single VM (with virtual RAM memory it is intended the amount of RAM
        seen by the VM OS, not the physical RAM dedicated to the VM).</td>
    </tr>
    <tr>
      <td style="text-align:left">InstanceMaxDedicatedRAM</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">MB</td>
      <td style="text-align:left">The maximum value (in MB) of virtual RAM memory which can be dedicated
        to a VM (i.e. physical host memory, not shared of swapped).</td>
    </tr>
    <tr>
      <td style="text-align:left">InstanceMinDedicatedRAM</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">MB</td>
      <td style="text-align:left">The minimum value (in MB) of virtual RAM memory which can be dedicated
        to a VM (i.e. physical host memory, not shared of swapped).</td>
    </tr>
    <tr>
      <td style="text-align:left">NetworkVirtualizationType</td>
      <td style="text-align:left">NetVirtualizationT_t</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The type of network virtualization performed by the Cloud Computing Manager
        to segregate VMs VLANs (ex. none, vSwitch, ebtables, etc&#x2026;).</td>
    </tr>
    <tr>
      <td style="text-align:left">CPUVirtualizationType</td>
      <td style="text-align:left">CPUVirtualizationT_t</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The type of CPU virtualization (ex. full/paravirtualization/hardware assisted).</td>
    </tr>
    <tr>
      <td style="text-align:left">VirtualDiskFormat</td>
      <td style="text-align:left">DiskVirtualizationT_t</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The format of virtual disk images supported (ex. qcow2, raw, vmdk).</td>
    </tr>
    <tr>
      <td style="text-align:left">Failover</td>
      <td style="text-align:left">ExtendedBoolean_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Failover is the automatic transition of the VM to a secondary machine
        or server upon failure of the primary component.</td>
    </tr>
    <tr>
      <td style="text-align:left">LiveMigration</td>
      <td style="text-align:left">ExtendedBoolean_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">If true the Cloud Computing Manager allows to move the virtual machine
        from one physical host to another without powering down the system.</td>
    </tr>
    <tr>
      <td style="text-align:left">VMBackupRestore</td>
      <td style="text-align:left">ExtendedBoolean_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">If true the Cloud Computing Manager allows to backup and restore the virtual
        machines. This is a static value and does not ensure the availability of
        the storage for the backup.</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>CloudComputingService.ID</p>
        <p>[redefines Service.ID]</p>
      </td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">A cloud computing manager participates in a computing service.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>CloudComputingInstanceType.ID</p>
        <p>[redefines Resource.ID]</p>
      </td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A cloud computing manager manages one or more cloud computing instance
        type.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingImage.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A cloud computing manager manages one or more cloud computing images.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Benchmark.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A cloud computing manager has zero or more associated benchmarks. These
        benchmarks are referred to the virtual resources (RAM, CPU, disk, network)
        provided to the VMs.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingManagerAccelerator.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A cloud computing manager controls zero or more virtual accelerator devices.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Extension.Key</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">The entity MAY be extended via key-value pairs.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>## CloudComputingManagerAccelerator

The CloudComputingManagerAccelerator contains all the information about the virtual accelerator device available for a given cloud computing manager.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Entity</th>
      <th style="text-align:left">Inherits from</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>CloudComputingManager</p>
        <p>Accelerator</p>
      </td>
      <td style="text-align:left">Entity</td>
      <td style="text-align:left">The set of information about the virtual accelerator device provided by
        the cloud computing manager.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left"><em>CreationTime</em>
      </td>
      <td style="text-align:left"><em>DateTime_t</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Timestamp describing when the entity instance was generated</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Validity</em>
      </td>
      <td style="text-align:left"><em>UInt64</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"><em>s</em>
      </td>
      <td style="text-align:left">
        <p><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant. After that period has elapsed,</em>
        </p>
        <p><em>the information SHOULD NOT be considered relevant</em>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>ID [key]</em>
      </td>
      <td style="text-align:left"><em>URI</em>
      </td>
      <td style="text-align:left"><em>1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>A global unique ID</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Name</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Human-readable name</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>OtherInfo</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>*</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left">Type</td>
      <td style="text-align:left"><em>AccType_t</em>
      </td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The virtual accelerator architecture type.</td>
    </tr>
    <tr>
      <td style="text-align:left">TotalNumber</td>
      <td style="text-align:left"><em>UInt32</em>
      </td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The total number of physical Accelerator cards accessible through any
        of the available Endpoints and managed by this Cloud Compute Manager. This
        value SHOULD represent the total installed capacity, i.e. including resources
        which are temporarily unavailable.</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxNumber</td>
      <td style="text-align:left"><em>UInt32</em>
      </td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The maximum number of virtual accelerators that can be assigned to a single
        VM</td>
    </tr>
    <tr>
      <td style="text-align:left">MinNumber</td>
      <td style="text-align:left"><em>UInt32</em>
      </td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The minimum number of virtual accelerators that can be assigned to a single
        VM</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingManager.ID</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">A set of virtual accelerator information is related to a cloud computing
        share.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Extension.Key</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">The entity MAY be extended via key-value pairs.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>## CloudComputingInstanceType

The CloudComputingInstanceType class describes the hardware environment of the VM, i.e. the amount of RAM, CPU, disk and network resources the VM OS will see and manage. The resources provided to the VM are virtual resources, usually shared with other VMs running in the same infrastructure. The performances of the provided resources are specified via the Benchmarks associated to the Instance Type.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Entity</th>
      <th style="text-align:left">Inherits from</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">CloudComputingInstanceType</td>
      <td style="text-align:left">Resource</td>
      <td style="text-align:left">A type of environment available to the CloudComputingManager for running
        a VM in a ComputingService via a Computing Endpoint; the type of environment
        is described in terms of hardware, operating system and network characteristics.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left"><em>CreationTime</em>
      </td>
      <td style="text-align:left"><em>DateTime_t</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Timestamp describing when the entity instance was generated</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Validity</em>
      </td>
      <td style="text-align:left"><em>UInt64</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"><em>s</em>
      </td>
      <td style="text-align:left">
        <p><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant. After that period has elapsed,</em>
        </p>
        <p><em>the information SHOULD NOT be considered relevant</em>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>ID [key]</em>
      </td>
      <td style="text-align:left"><em>URI</em>
      </td>
      <td style="text-align:left"><em>1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>A global unique ID</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Name</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Human-readable name</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>OtherInfo</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>*</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left">TemplateID</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Reference to this particular template to be used during instantiation
        of a VM via the Endpoint.</td>
    </tr>
    <tr>
      <td style="text-align:left">MarketplaceURL</td>
      <td style="text-align:left">URI</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Reference to one or more marketplaces which stores the metadata of this
        resource template. Reference is the URL of the resource in the marketplace.</td>
    </tr>
    <tr>
      <td style="text-align:left">Platform</td>
      <td style="text-align:left">Platform_t</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The platform architecture provided to the virtual machine (ex. i386, x86_64)</td>
    </tr>
    <tr>
      <td style="text-align:left">CPU</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Number of virtual cores provided to the virtual machine (this is the number
        of core the machine OS will see)</td>
    </tr>
    <tr>
      <td style="text-align:left">RAM</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">MB</td>
      <td style="text-align:left">Virtual RAM memory provided to the virtual machine (this is the total
        wuantity of RAM the machine OS will see)</td>
    </tr>
    <tr>
      <td style="text-align:left">Disk</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">GB</td>
      <td style="text-align:left">Size of the disk associated to the OS image. If this attribute is omitted,
        the OS disk size will be the one specified by the CloudComputingImage entity,
        otherwise the CloudComputingImage OS disk will be extended to this value.</td>
    </tr>
    <tr>
      <td style="text-align:left">EphemeralStorage</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">GB</td>
      <td style="text-align:left">Amount of Ephemeral storage associated to the VM. This is temporary storage
        which is deleted after the VM closure and is represented as a new resource.</td>
    </tr>
    <tr>
      <td style="text-align:left">NetworkIn</td>
      <td style="text-align:left">ExtendedBoolean_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">True if direct inbound network connectivity is available to the OS, even
        if limited, e.g. by firewall rules.</td>
    </tr>
    <tr>
      <td style="text-align:left">NetworkOut</td>
      <td style="text-align:left">ExtendedBoolean_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">True if direct outbound network connectivity is available to the OS, even
        if limited, e.g. by firewall rules.</td>
    </tr>
    <tr>
      <td style="text-align:left">NetworkPortsIn</td>
      <td style="text-align:left">NetworkConfigurationPort_t</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The allowed inbound external connectivity ports (if not specified, all
        ports are allowed)</td>
    </tr>
    <tr>
      <td style="text-align:left">NetworkPortsOut</td>
      <td style="text-align:left">NetworkConfigurationPort_t</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The allowed outbound external connectivity ports (if not specified, all
        ports are allowed)</td>
    </tr>
    <tr>
      <td style="text-align:left">NetworkInfo</td>
      <td style="text-align:left">NetworkInfo_t</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The type of internal network connection available to the OS.</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>CloudComputingManager.ID</p>
        <p>[redefines Manager.ID]</p>
      </td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">Cloud Computing Instance Type is managed by a Cloud computing manager.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>CloudComputingShare.ID</p>
        <p>[redefines Share.ID]</p>
      </td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">Cloud Computing Instance Type is served by a set of computing shares.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>CloudComputingInstance.ID</p>
        <p>[redefines Activity.ID]</p>
      </td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">Zero or more cloud computing instances runs this Cloud Computing Instance
        Type.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingEndpoint.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">Cloud Computing Instance Type is available on a set of Cloud Computing
        Endpoints.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingVirtualAccelerator.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A cloud computing instance type provides zero or more virtual accelerator
        devices.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudServicePrice.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">The price metric associated to the resources provided by this template.
        It contains a different metric for each resource (Computing, Memory, Network
        IN/OUT)</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Extension.Key</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">The entity MAY be extended via key-value pairs.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>The associated CloudServicePrice entities define the price for the entire template or separately for each one of the resources \(eg. CPU, Memory, Disk, Network IN/OUT\) provided by the infrastructure. Price element associated to the CloudComputingInstanceType contributes separately to the final price of the VM, together with the other price elements associated to the CloudComputingImage.

## CloudComputingVirtualAccelerator

The CloudComputingVirtualAccelerator is an entity used to describe a set of homogeneous virtual accelerator devices. Generally a virtual accelerator device corresponds to physical one installed on the host. A cloud computing instance may be associated with one or more virtual accelerators.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Entity</th>
      <th style="text-align:left">Inherits from</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">CloudComputingVirtualAccelerator</td>
      <td style="text-align:left">Entity</td>
      <td style="text-align:left">Description of the accelerator device</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left"><em>CreationTime</em>
      </td>
      <td style="text-align:left"><em>DateTime_t</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Timestamp describing when the entity instance was generated</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Validity</em>
      </td>
      <td style="text-align:left"><em>UInt64</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"><em>s</em>
      </td>
      <td style="text-align:left">
        <p><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant. After that period has elapsed,</em>
        </p>
        <p><em>the information SHOULD NOT be considered relevant</em>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>ID [key]</em>
      </td>
      <td style="text-align:left"><em>URI</em>
      </td>
      <td style="text-align:left"><em>1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>A global unique ID</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Name</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Human-readable name</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>OtherInfo</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>*</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">AccType_t</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The type of virtual accelerator device.</td>
    </tr>
    <tr>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The number of virtual accelerators provided to the virtual machine (usually
        this is the number of cards the machine OS will see)</td>
    </tr>
    <tr>
      <td style="text-align:left">Vendor</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The name of the virtual accelerator vendor provided to the virtual machine.
        Free format, but it SHOULD correspond to the name by which the vendor is
        generally known.</td>
    </tr>
    <tr>
      <td style="text-align:left">Model</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The name of the virtual accelerator model, as defined by the vendor, provided
        to the virtual machine</td>
    </tr>
    <tr>
      <td style="text-align:left">Version</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The specific version of the virtual accelerator model, as defined by the
        vendor, provided to the virtual machine.</td>
    </tr>
    <tr>
      <td style="text-align:left">ClockSpeed</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">MHz</td>
      <td style="text-align:left">The nominal clock speed of the virtual accelerator, provided to the virtual
        machine.</td>
    </tr>
    <tr>
      <td style="text-align:left">Memory</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">MB</td>
      <td style="text-align:left">The nominal memory size of the virtual accelerator, provided to the virtual
        machine.</td>
    </tr>
    <tr>
      <td style="text-align:left">ComputeCapability</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The reference, an ID or tag, representing the set of features supported
        by a virtual accelerator, as declared by the vendor</td>
    </tr>
    <tr>
      <td style="text-align:left">VirtualizationType</td>
      <td style="text-align:left">VirtType_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The virtualization mode adopted for creating the virtual accelerator device.</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingInstanceType.ID</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">A virtual accelerator is associated with one CloudComputingInstanceType.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Extension.Key</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">The entity MAY be extended via key-value pairs.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>## CloudComputingImage

The CloudComputingImage class describes the software environment of the VM, i.e. which OS is booting at VM startup and which pre-installed software is available on it. Each application installed on the OS is identified by a name \(the InstalledSoftware attribute\); these names are not defined within the schema, but SHOULD be assigned in a way which allows applications to be uniquely identified. In some deployment scenarios, the definition of namespace-based InstalledSoftware or guidelines for the generation of unique application names MAY be specified, and application repository services relying on those application names MAY be provided. This aspect is considered out of scope for the GLUE schema specification, but MAY be included in a profile document for a specific production Clouds.

The CloudComputingImage can be used to describe specific OS features, particular OS configuration, installed application software or special environment setups in terms of a simple tag string. In this case, the InstalledSoftware attribute should be used to publish this tag.

The properties of installed software may vary substantially, but the attributes of the class cover the most common cases, in particular for licensed software. If necessary, additional information MAY be added using the OtherInfo attribute and the Extension class.

The OS template may require a certain amount of resources \(CPU, RAM and GPU\) to run. These requirements are specified in terms of minimum and recommended requirements, which will lead the user to the proper selection of virtual resources needed by the VM.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Entity</th>
      <th style="text-align:left">Inherits from</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">CloudComputingImage</td>
      <td style="text-align:left">Entity</td>
      <td style="text-align:left">A description of installed OS and applications or OS environment characteristics
        and configuration available for VM instantiation.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left"><em>CreationTime</em>
      </td>
      <td style="text-align:left"><em>DateTime_t</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Timestamp describing when the entity instance was generated</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Validity</em>
      </td>
      <td style="text-align:left"><em>UInt64</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"><em>s</em>
      </td>
      <td style="text-align:left">
        <p><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant. After that period has elapsed,</em>
        </p>
        <p><em>the information SHOULD NOT be considered relevant</em>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>ID [key]</em>
      </td>
      <td style="text-align:left"><em>URI</em>
      </td>
      <td style="text-align:left"><em>1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>A global unique ID</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Name</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Human-readable name</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>OtherInfo</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>*</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left">TemplateID</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Reference to this particular template to be used during instantiation
        of a VM via the Endpoint.</td>
    </tr>
    <tr>
      <td style="text-align:left">MarketplaceURL</td>
      <td style="text-align:left">URI</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Reference to one or more marketplaces which stores the metadata of this
        instance. Reference is the URL of the resource in the marketplace.</td>
    </tr>
    <tr>
      <td style="text-align:left">OSPlatform</td>
      <td style="text-align:left">Platform_t</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The platform architecture to which the OS belongs (ex. i386, x86_64)</td>
    </tr>
    <tr>
      <td style="text-align:left">OSFamily</td>
      <td style="text-align:left">OSFamily_t</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The general family to which the OS belongs.</td>
    </tr>
    <tr>
      <td style="text-align:left">OSName</td>
      <td style="text-align:left">OSName_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The specific name of the OS.</td>
    </tr>
    <tr>
      <td style="text-align:left">OSVersion</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The version of the OS, as defined by the vendor.</td>
    </tr>
    <tr>
      <td style="text-align:left">DiskSize</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">GB</td>
      <td style="text-align:left">Size of the OS disk image in GB.</td>
    </tr>
    <tr>
      <td style="text-align:left">RecommendedCPU</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Number of virtual CPU cores recommended to run the image (this is a recommended
        value, actual number of cores will depend on the selected CloudComputeInstanceType)</td>
    </tr>
    <tr>
      <td style="text-align:left">RecommendedRAM</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">MB</td>
      <td style="text-align:left">Virtual RAM memory recommended to run the image (this is a recommended
        value, the actual RAM value will depend on the selected CloudComputeInstanceType)</td>
    </tr>
    <tr>
      <td style="text-align:left">MinCPU</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Minimum number of virtual CPU cores required to run the image (the actual
        number of cores will depend on the selected CloudComputeInstanceType)</td>
    </tr>
    <tr>
      <td style="text-align:left">MinRAM</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">MB</td>
      <td style="text-align:left">Minimum virtual RAM memory required to run the image (the actual RAM value
        will depend on the selected CloudComputeInstanceType)</td>
    </tr>
    <tr>
      <td style="text-align:left">AccessInfo</td>
      <td style="text-align:left">HostAccessInfo_t</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Information about user access to the VM. Can be: credentials injected
        during contextualization, pre-defined username/password, pre-defined RSA
        key</td>
    </tr>
    <tr>
      <td style="text-align:left">ContextualizationName</td>
      <td style="text-align:left">ContextualizationName_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Supported contextualization mechanism (if any)</td>
    </tr>
    <tr>
      <td style="text-align:left">ContextualizationVersion</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Supported contextualization mechanism versions</td>
    </tr>
    <tr>
      <td style="text-align:left">DefaultUsername</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Pre-defined username to access the VM (if AccessInfo specify pre-defined
        credentials)</td>
    </tr>
    <tr>
      <td style="text-align:left">DefaultPassword</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Pre-defined password (or RSA private key) to access the CM (if AccessInfo
        specify pre-defined credentials)</td>
    </tr>
    <tr>
      <td style="text-align:left">InstalledSoftware</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Custom software installed on the instance.</td>
    </tr>
    <tr>
      <td style="text-align:left">Description</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Description of the image.</td>
    </tr>
    <tr>
      <td style="text-align:left">Version</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Version of the image.</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>CloudComputingManager.ID</p>
        <p>[redefines Manager.ID]</p>
      </td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">Cloud Computing Image is managed by a Cloud computing manager.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingShare.ID</td>
      <td style="text-align:left">1..*</td>
      <td style="text-align:left">An OS template is available to one or more computing shares</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingInstance.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">An OS template is used by one or more computing activities</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingEndpoint.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">An OS template is available on a set of Cloud Computing Endpoints.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudServicePrice.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">The price metric associated to the resources provided by this template.
        It contains a different metric for each resource (OS License, Application
        license, etc&#x2026;)</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudToStorageService.ID</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">Link to the OS disk location in the storage service.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingImageNetworkTraffic.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">An image may contain information about multiple NetworkTraffic objects.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Extension.Key</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">The entity MAY be extended via key-value pairs.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>The price item linked to this entity represent a single price voice of the final bill, usually related to OS or applicantion licensing price. The linked price values need to be added to the prices in the CloudComputingInstanceType to determinate the final price associated to an active instance.

The OS disk size specified in the CloudComputingImage is the minimum disk size who need to be provided by the CloudComputingInstanceType for a VM to be instantiated correctly. If the CloudComputingInstanceType has no OS disk size associated, the VM OS disk size will be the one specified by the CloudComputingImage, otherwise, the VM OS disk will be enlarged to the size specified by the CloudComputingInstanceType.

## CloudComputingImageNetworkConfiguration

The CloudComputingImageNetworkConfiguration contains information about expected network usage, related to a single or a set of ports and a network address in CIDR notation of a cloud computing image. There might be zero, one or more objects for each computing image.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Entity</th>
      <th style="text-align:left">Inherits from</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">CloudComputingImageNetworkConfiguration</td>
      <td style="text-align:left">Entity</td>
      <td style="text-align:left">The set of information about the network configuration of a cloud computing
        image.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left"><em>CreationTime</em>
      </td>
      <td style="text-align:left"><em>DateTime_t</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Timestamp describing when the entity instance was generated</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Validity</em>
      </td>
      <td style="text-align:left"><em>UInt64</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"><em>s</em>
      </td>
      <td style="text-align:left">
        <p><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant. After that period has elapsed,</em>
        </p>
        <p><em>the information SHOULD NOT be considered relevant</em>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>ID [key]</em>
      </td>
      <td style="text-align:left"><em>URI</em>
      </td>
      <td style="text-align:left"><em>1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>A global unique ID</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Name</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Human-readable name</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>OtherInfo</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>*</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left">Direction</td>
      <td style="text-align:left">NetworkConfigurationDirection_t</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Information about traffic direction</td>
    </tr>
    <tr>
      <td style="text-align:left">Protocol</td>
      <td style="text-align:left">NetworkConfigurationProtocol_t</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Information about network protocol</td>
    </tr>
    <tr>
      <td style="text-align:left">Port</td>
      <td style="text-align:left">NetworkConfigurationPort_t</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Information about network port(s)</td>
    </tr>
    <tr>
      <td style="text-align:left">AddressRange</td>
      <td style="text-align:left">NetworkConfigurationAddressRange_t</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Information about network address range</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingImage.ID</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">A NetworkConfiguration object is related to a cloud computing image.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Extension.Key</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">The entity MAY be extended via key-value pairs.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>## CloudComputingInstance

The CloudComputingInstance class represents a single VM \(but possibly multi-VM\) instance. The attributes give the instance properties and state as seen by the Cloud Computing Manager.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Entity</th>
      <th style="text-align:left">Inherits from</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">CloudComputingInstance</td>
      <td style="text-align:left">Activity</td>
      <td style="text-align:left">An Activity managed by the Cloud Manager execution capability (the Computing
        Activity is traditionally called VM).</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Inherited Attribute</em>
      </td>
      <td style="text-align:left"><em>Type</em>
      </td>
      <td style="text-align:left"><em>Mult</em>
      </td>
      <td style="text-align:left"><em>Unit</em>
      </td>
      <td style="text-align:left"><em>Description</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>CreationTime</em>
      </td>
      <td style="text-align:left"><em>DateTime_t</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Timestamp describing when the entity instance was generated</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Validity</em>
      </td>
      <td style="text-align:left"><em>UInt64</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"><em>s</em>
      </td>
      <td style="text-align:left">
        <p><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant. After that period has elapsed,</em>
        </p>
        <p><em>the information SHOULD NOT be considered relevant</em>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>ID [key]</em>
      </td>
      <td style="text-align:left"><em>URI</em>
      </td>
      <td style="text-align:left"><em>1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>A global unique ID</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Name</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Human-readable name</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>OtherInfo</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>*</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">CloudComputingInstanceType_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The type of this Computing Activity.</td>
    </tr>
    <tr>
      <td style="text-align:left">VMID</td>
      <td style="text-align:left">URI</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The VM ID as assigned by the Computing Endpoint.</td>
    </tr>
    <tr>
      <td style="text-align:left">LocalID</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The local ID of the VM as assigned by the Cloud Computing Manager.</td>
    </tr>
    <tr>
      <td style="text-align:left">State</td>
      <td style="text-align:left">CloudComputingInstanceState_t</td>
      <td style="text-align:left">1..*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The state of the VM; different state models are allowed; a state for each
        model is allowed provided that it has a different namespace prefix (see
        data type definition)</td>
    </tr>
    <tr>
      <td style="text-align:left">Error</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Error messages as provided by the software components involved in the
        management of the job.</td>
    </tr>
    <tr>
      <td style="text-align:left">Owner</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The identity of the VM&#x2019;s owner;.</td>
    </tr>
    <tr>
      <td style="text-align:left">LocalOwner</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The local user name to which the VM&#x2019;s owner is mapped for the execution
        of this job.</td>
    </tr>
    <tr>
      <td style="text-align:left">ExecutionNode</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">A hostname associated to the Execution Environment instance (i.e., host)
        running the VM; multi-node VMs are described by several instances of this
        attribute.</td>
    </tr>
    <tr>
      <td style="text-align:left">UsedTotalCPUTime</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">s</td>
      <td style="text-align:left">The total CPU time consumed so far by the VM. In case of multi-VM, this
        value refers to the sum of the CPU time consumed in each slot.</td>
    </tr>
    <tr>
      <td style="text-align:left">UsedMainMemory</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">MB</td>
      <td style="text-align:left">The amount of RAM currently used by the VM.</td>
    </tr>
    <tr>
      <td style="text-align:left">UsedNetworkIn</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">Kb</td>
      <td style="text-align:left">The amount of inbound network connectivity consumed so far by the VM.
        The value is measured in terms of Kb in input to the VM virtual interfaces.</td>
    </tr>
    <tr>
      <td style="text-align:left">UsedNetworkOut</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">Kb</td>
      <td style="text-align:left">The amount of outbound network connectivity consumed so far by the VM.
        The value is measured in terms of Kb in output to the VM virtual interfaces.</td>
    </tr>
    <tr>
      <td style="text-align:left">ComputingManagerSubmissionTime</td>
      <td style="text-align:left">DateTime_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The time when the VM instantiation was submitted to the Cloud Middelware
        by the user.</td>
    </tr>
    <tr>
      <td style="text-align:left">StartTime</td>
      <td style="text-align:left">DateTime_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The time when the VM entered Running state.</td>
    </tr>
    <tr>
      <td style="text-align:left">ComputingManagerEndTime</td>
      <td style="text-align:left">DateTime_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The time when the VM destroy request was submitted to the Cloud Middelware
        by the user.</td>
    </tr>
    <tr>
      <td style="text-align:left">EndTime</td>
      <td style="text-align:left">DateTime_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The time when the VM entered Halted state.</td>
    </tr>
    <tr>
      <td style="text-align:left">SubmissionHost</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The name of the host from which the VM was submitted.</td>
    </tr>
    <tr>
      <td style="text-align:left">SubmissionClientName</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The name of the software client which was used to submit the VM.</td>
    </tr>
    <tr>
      <td style="text-align:left">OtherMessages</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Optional job messages provided by either the Cloud Middelware or the Compute
        Manager.</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>CloudComputingEndpoint.ID</p>
        <p>[redefines Endpoint.ID]</p>
      </td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">A Cloud computing activity is submitted to a computing endpoint.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>CloudComputingShare.ID</p>
        <p>[redefines Share.ID]</p>
      </td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">A Cloud computing activity is mapped into a computing share.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>CloudComputingInstanceType.ID</p>
        <p>[redefines Resource.ID]</p>
      </td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">A Cloud computing activity is executed in an execution environment.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudToStorageService</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">Link to the attached disks location in the storage service. The OS disk
        is included in this list.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingInstanceAccelerator.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A cloud computing instance shows zero or more information about the usage
        level of installed virtual accelerator devices.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Extension.Key</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">The entity MAY be extended via key-value pairs.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">UserDomain.ID</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">An activity is managed by a user domain.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Activity.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">An activity is related to zero or more activities.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>In this specification, the Cloud Computing Instance may refer to a VM or to elements of collections or appliances. The description of the relationships between VMs which are part of a collection or appliance may be considered in future revisions of the specification.

## CloudComputingInstanceAccelerator

The CloudComputingInstanceAccelerator contains information about the usage level of the virtual accelerator device handled by the cloud computing instance.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Entity</th>
      <th style="text-align:left">Inherits from</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>CloudComputingInstance</p>
        <p>Accelerator</p>
      </td>
      <td style="text-align:left">Entity</td>
      <td style="text-align:left">The usage level of the virtual accelerator device handled by the cloud
        computing instance.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left"><em>CreationTime</em>
      </td>
      <td style="text-align:left"><em>DateTime_t</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Timestamp describing when the entity instance was generated</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Validity</em>
      </td>
      <td style="text-align:left"><em>UInt64</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"><em>s</em>
      </td>
      <td style="text-align:left">
        <p><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant. After that period has elapsed,</em>
        </p>
        <p><em>the information SHOULD NOT be considered relevant</em>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>ID [key]</em>
      </td>
      <td style="text-align:left"><em>URI</em>
      </td>
      <td style="text-align:left"><em>1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>A global unique ID</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Name</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Human-readable name</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>OtherInfo</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>*</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left">Type</td>
      <td style="text-align:left"><em>AccType_t</em>
      </td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The virtual accelerator architecture type.</td>
    </tr>
    <tr>
      <td style="text-align:left">TotalProcessingTime</td>
      <td style="text-align:left"><em>UInt64</em>
      </td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"><em>s</em>
      </td>
      <td style="text-align:left">The total Accelerator time consumed so far by the VM. In case of multi-VM,
        this value refers to the sum of the Accelerator time consumed in each slot.</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingInstance. ID</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">A set of virtual accelerator information is related to a cloud computing
        instance.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Extension.Key</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">The entity MAY be extended via key-value pairs.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>## CloudServicePrice

The CloudServicePrice entity models the resources price in the cloud environment. This entity represents a single price voice of the final price for the activity. This voice is related to a given consumed resource which is specified in the attributes of the entity.

The price for the given resource is represented by a fixed price or consumption model. The fixed price is independent of the resource usage and can be billed once or multiple times during the life of the CloudComputing Instance \(ex. monthly fixed prices\). The consumption price needs to be multiplied by the accounted resource consumption value \(present in the CloudComputing Instance entity\) in the given consumption period. Consumption prices must be specified in the same unit as per the unit of the accounted resource.

Different cost models may be applied to different users according to the scope of the CloudComputingInstance. For example, research usage may have different pricing than commercial useage. The related scope for the price to apply is described in the entity attributes.

With the information provided by the Scope attribute, this entity MAY be used in alternative to UserDomain and AccessPolicy entities, to discriminate which category of users have access to the resource. In this view, it MAY be defined by the user community that users category without associated cost entity for the service have no access to it.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Entity</th>
      <th style="text-align:left">Inherits from</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">CloudServicePrice</td>
      <td style="text-align:left">Entity</td>
      <td style="text-align:left">Price information for a given Cloud service resource.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Inherited Attribute</em>
      </td>
      <td style="text-align:left"><em>Type</em>
      </td>
      <td style="text-align:left"><em>Mult</em>
      </td>
      <td style="text-align:left"><em>Unit</em>
      </td>
      <td style="text-align:left"><em>Description</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>CreationTime</em>
      </td>
      <td style="text-align:left"><em>DateTime_t</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Timestamp describing when the entity instance was generated</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Validity</em>
      </td>
      <td style="text-align:left"><em>UInt64</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"><em>S</em>
      </td>
      <td style="text-align:left">
        <p><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant. After that period has elapsed,</em>
        </p>
        <p><em>the information SHOULD NOT be considered relevant</em>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>ID [key]</em>
      </td>
      <td style="text-align:left"><em>URI</em>
      </td>
      <td style="text-align:left"><em>1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>A global unique ID</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Name</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Human-readable name</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>OtherInfo</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>*</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left">Resource</td>
      <td style="text-align:left">CloudResourceName_t</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Name of the resource this price entity refers to. Can be any resource
        billed (CPU, Memory, Disk, Software Licenses, etc&#x2026;).</td>
    </tr>
    <tr>
      <td style="text-align:left">Scope</td>
      <td style="text-align:left">ResourceScope_t</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Usage scope required for the price to apply (eg. commercial, no-profit,
        research, training)</td>
    </tr>
    <tr>
      <td style="text-align:left">FixFee</td>
      <td style="text-align:left">Float32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">Euro</td>
      <td style="text-align:left">Fixed fee to be paid for the service usage (this price is not dependent
        from the resource usage)</td>
    </tr>
    <tr>
      <td style="text-align:left">FixFeePeriod</td>
      <td style="text-align:left">Period_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Billing period for the fixed price (ex. once, monthly, yearly, etc.)</td>
    </tr>
    <tr>
      <td style="text-align:left">ConsumptionFee</td>
      <td style="text-align:left">Float32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">Euro/period/x</td>
      <td style="text-align:left">Consumption fee to be paid for the service (this price shall be specified
        in the same unit as per the accounted resource x)</td>
    </tr>
    <tr>
      <td style="text-align:left">ConsumptionFeePeriod</td>
      <td style="text-align:left">Period_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Billing period for the per usage price (ex. monthly, yearly, etc.)</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingInstanceType.ID</td>
      <td style="text-align:left">0..*</td>
      <td style="text-align:left">It MAY be associated to a Computing Instance Type.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingImage.ID</td>
      <td style="text-align:left">0..*</td>
      <td style="text-align:left">It MAY be associated to a OS template.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">StorageService.ID</td>
      <td style="text-align:left">0..*</td>
      <td style="text-align:left">It MAY be associated to a Storage service.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Extension.Key</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">The entity MAY be extended via key-value pairs.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>The entity can be associated to multiple CloudComputingInstanceType or CloudComputingImage or StorageService, but not to different class of entities at the same time.

## CloudToStorageService

The CloudToStorageService class represents the case where a virtual disk is created into the Storage Service for VM usage. The disk may be attached to the VM \(visible as a disk device by the VM OS\) or available via other export protocols \(NFS share, iSCSI, etc…\).

The attributes of this entity refer to the link of the storage resource into the Storage System and the VM environment.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Entity</th>
      <th style="text-align:left">Inherits from</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">CloudToStorageService</td>
      <td style="text-align:left">Entity</td>
      <td style="text-align:left">The description of a device access to a Virtual Disk attached to a VM,
        thus available in the VM as a virtual hardware device.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Inherited Attribute</em>
      </td>
      <td style="text-align:left"><em>Type</em>
      </td>
      <td style="text-align:left"><em>Mult</em>
      </td>
      <td style="text-align:left"><em>Unit</em>
      </td>
      <td style="text-align:left"><em>Description</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>CreationTime</em>
      </td>
      <td style="text-align:left"><em>DateTime_t</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Timestamp describing when the entity instance was generated</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Validity</em>
      </td>
      <td style="text-align:left"><em>UInt64</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"><em>s</em>
      </td>
      <td style="text-align:left">
        <p><em>The duration after CreationTime that the information presented in the Entity SHOULD be considered relevant. After that period has elapsed,</em>
        </p>
        <p><em>the information SHOULD NOT be considered relevant</em>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>ID [key]</em>
      </td>
      <td style="text-align:left"><em>URI</em>
      </td>
      <td style="text-align:left"><em>1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>A global unique ID</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Name</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>0..1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Human-readable name</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>OtherInfo</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>*</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Placeholder to publish info that does not fit in any other attribute. Free-form string, comma-separated tags, (name, value ) pair are all examples of valid syntax</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left">LocationID</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Reference to this disk to be used for attaching/detaching it to a VM.</td>
    </tr>
    <tr>
      <td style="text-align:left">LocalPath</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The link to the local storage into the VM environment (this is typically
        a link to a local virtual disk device)</td>
    </tr>
    <tr>
      <td style="text-align:left">RemotePath</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The link to the storage into the remote Storage Service (this is typically
        a link to a virtual disk image).</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingInstance.ID</td>
      <td style="text-align:left">0..*</td>
      <td style="text-align:left">It MAY be associated to a cloud computing instance.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingImage.ID</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">It MAY be associated to a OS template.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingService.ID</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">Is associated to a cloud computing service.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">StorageService.ID</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">Is associated to a storage service.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Inherited Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Extension.Key</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">The entity MAY be extended via key-value pairs.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>The entity can be associated to multiple CloudComputingInstance, to a CloudComputingImage or to both the entities at the same time. The disk may also be temporary un-associated to any Computing entity. This is the case of data which has been detached from all the running VMs but stays available to be attached to new VMs.

