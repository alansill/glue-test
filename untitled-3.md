---
description: Section 7
---

# Conceptual Model of the Computing Service

The conceptual model of the Computing Service is based on the main entities and uses specializations of the Service, Endpoint, Share, Manager, Resource, and Activity entities.  Further computing related concepts such as ApplicationEnvironment, ApplicationHandle and Benchmark are introduced.

![](.gitbook/assets/0%20%281%29.png)

**Figure 2 Entities and relationships for the Computing Service conceptual model**

In this section, we extensively use the concepts of physical CPU, logical CPU and slot defined as follows:

* a physical CPU is defined by a socket on a motherboard, i.e. there is one physical CPU per socket \(e.g., a multi-core CPU counts as one physical CPU\);
* a logical CPU corresponds to a CPU as visible by the operating system running either on a real or virtual machine \(e.g. a four-core CPU counts as four logical CPUs\);
* a slot is a portion of executable time in a logical CPU offered by an execution environment instance which MAY be occupied by a job:
  * typically there is one slot per logical CPU, but a logical CPU MAY be shared among multiple slots;
  * jobs MAY occupy several slots at the same time \(e.g., MPI jobs\); a multi-slot job is counted as one Activity.

Throughout the specification, we also use the concept of storage extent to mean the capabilities and management of the various media that exist to store data and allow data retrieval.

### 7.1. ComputingService

  
The ComputingService class is a specialization of the Service class for a service offering computational capacity. The ComputingService entity is the main logical unit, and aggregation point for several entities together modeling a computing capability in a Grid system. A ComputingService is capable of executing ComputingActivities on its associated resources. The resources behind the ComputingService are described via the ComputingManager, ExecutionEnvironment, ApplicationEnvironment, ApplicationHandle and Benchmark entities. The governing policies and status of the resources are given by the ComputingShare elements. The ComputingActivities of a ComputingService are submitted and controlled via a ComputingEndpoint.

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
      <td style="text-align:left">ComputingService</td>
      <td style="text-align:left">Service</td>
      <td style="text-align:left">
        <p>An abstracted, logical view of software and hardware components that participate
          in the creation of a computational capacity in a Grid environment. A Computing
          Service exposes zero or more Computing Endpoints having well-defined interfaces,
          zero or more Computing Shares and zero or more Computing Managers and the
          related Execution Environments.</p>
        <p>The computing service is autonomous and denotes a weak aggregation among
          Computing Endpoints, the underlying Computing Managers and related Execution
          Environments, and the defined Computing Shares. The Computing Service enables
          the identification of the whole set of entities providing the computing
          functionality with a persistent name.</p>
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
      <td style="text-align:left"><em>The type of service according to a namespace-based classification (the namespace MAY be related to a middleware name, an organization or other concepts; org.ogf.glue is reserved for the OGF GLUE Working Group)</em>
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
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left">TotalJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The total number of Grid jobs currently known to the system (the sum of
        RunningJobs, WaitingJobs, StagingJobs, SuspendedJobs and PreLRMSWaitingJobs);
        this value SHOULD not include jobs submitted locally rather than via the
        Grid.</td>
    </tr>
    <tr>
      <td style="text-align:left">RunningJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The number of Grid jobs which are currently running in an Execution Environment.</td>
    </tr>
    <tr>
      <td style="text-align:left">WaitingJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The number of Grid jobs which are currently waiting to start execution.
        Usually these will be queued in the underlying Computing Manager (i.e.,
        a Local Resource Managment System or LRMS).</td>
    </tr>
    <tr>
      <td style="text-align:left">StagingJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The number of Grid jobs which are currently either staging files in before
        starting execution, or staging files out after finishing execution.</td>
    </tr>
    <tr>
      <td style="text-align:left">SuspendedJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The number of Grid jobs which have started their execution, but are currently
        suspended (e.g., having been preempted by another job).</td>
    </tr>
    <tr>
      <td style="text-align:left">PreLRMSWaitingJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The number of Grid jobs which are currently managed by the Grid software
        layer waiting to be passed to the underlying Computing Manager (LRMS),
        and hence are not yet candidates to start execution.</td>
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
        <p>ComputingEndpoint.ID</p>
        <p>[redefines Endpoint.ID]</p>
      </td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A computing service exposes zero or more computing endpoints.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">ComputingShare.ID [redefines Share.ID]</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A computing service offers zero or more computing shares.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">ComputingManager.ID [redefines Manager.ID]</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A computing service offers zero or more computing managers.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">StorageService.ID</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
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
      <td style="text-align:left">Contact.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A computing service has zero or more contacts.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Location.ID</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">A computing service is primarily located at a location.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Service.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A computing service is related to zero or more services.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>A simple ComputingService is formed by a ComputingEndpoint exposing an interface for job submission and control. In the case of a single ComputingManager whose ExecutionEnvironments are exposed by multiple ComputingEndpoints, the ComputingManager, ExecutionEnvironments and ComputingEndpoints MUST be considered as part of the same ComputingService. In the case of a single ComputingEndpoint exposing ExecutionEnvironments managed by different ComputingManagers, then the ComputingEndpoint, the ExecutionEnvironments and the related ComputingManagers MUST be considered as part of the same ComputingService.

The ComputingService always aggregates ComputingEndpoints, ComputingShares, ComputingManagers and ExecutionEnvironments forming a connected set. In other words, Endpoint A exposing ExecutionEnvironment A of Manager A via Share A and Endpoint B exposing ExecutionEnvironment B of Manager B via Share B form two different ComputingServices. On the other hand, Endpoint A exposing ExecutionEnvironment A of Manager A via Share A and Endpoint B exposing ExecutionEnvironment A of Manager A via Share B form a single ComputingService.

### ComputingEndpoint

The ComputingEndpoint is a specialization of the Endpoint class for a service possessing computational capability. The class represents an endpoint which is used to create, control and monitor computational activities. The computational-specific information concerns service load related parameters, staging capabilities and supported types of job description. This class provides attributes that MAY be used to publish summary information about jobs submitted via a particular Endpoint. Such attributes are optional and may not always be reported \(e.g., in the case of a stateless Endpoint which does not keep information about the jobs submitted through it\).

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
      <td style="text-align:left">ComputingEndpoint</td>
      <td style="text-align:left">Endpoint</td>
      <td style="text-align:left">A network Endpoint for creating, monitoring, and controlling computational
        Activities called jobs. It MAY also be used to expose complementary capabilities
        (e.g., resource reservation or proxy manipulation).</td>
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
      <td style="text-align:left">Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left">Staging</td>
      <td style="text-align:left">Staging_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Supported file staging functionalities, if any.</td>
    </tr>
    <tr>
      <td style="text-align:left">JobDescription</td>
      <td style="text-align:left">JobDescription_t</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Supported type of job description language.</td>
    </tr>
    <tr>
      <td style="text-align:left">TotalJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">Job</td>
      <td style="text-align:left">The total number of Grid jobs currently known to the system (the sum of
        RunningJobs, WaitingJobs, StagingJobs, SuspendedJobs and PreLRMSWaitingJobs);
        this value SHOULD not include jobs submitted locally rather than via the
        Grid.</td>
    </tr>
    <tr>
      <td style="text-align:left">RunningJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The number of Grid jobs which are currently running in an Execution Environment.</td>
    </tr>
    <tr>
      <td style="text-align:left">WaitingJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The number of Grid jobs which are currently waiting to start execution.
        Usually these will be queued in the underlying Computing Manager (i.e.,
        a Local Resource Managment System or LRMS).</td>
    </tr>
    <tr>
      <td style="text-align:left">StagingJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The number of Grid jobs which are currently either staging files in before
        starting execution, or staging files out after finishing execution.</td>
    </tr>
    <tr>
      <td style="text-align:left">SuspendedJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The number of Grid jobs which have started their execution, but are currently
        suspended (e.g., having been preempted by another job).</td>
    </tr>
    <tr>
      <td style="text-align:left">PreLRMSWaitingJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The number of Grid jobs which are currently managed by the Grid software
        layer waiting to be passed to the underlying Computing Manager (LRMS),
        and hence are not yet candidates to start execution.</td>
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
        <p>ComputingService.ID</p>
        <p>[redefines Service.ID]</p>
      </td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">A computing endpoint is part of a Computing Service.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">ComputingShare.ID [redefines Share.ID]</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A computing endpoint MAY pass activities to zero or more computing shares.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>ComputingActivity.ID</p>
        <p>[redefines Activity.ID]</p>
      </td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">An endpoint has accepted and is managing zero or more Activities.</td>
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
</table>### ComputingShare

The ComputingShare class is the specialization of the main Share class for computational services. A Computing Share is a high-level concept introduced to model a utilization target for a set of Execution Environments defined by a set of configuration parameters and characterized by status information. A ComputingShare carries information about "policies" \(limits\) defined over all or a subset of resources and describes their dynamic status \(load\).

In clusters managed by a batch system \(LRMS\), the simplest way to set up a Computing Share is to configure a batch queue. Nevertheless, the same Computing Share may be implemented using different batch system configuration strategies. In complex batch systems, a batch queue may be configured with different sets of policies for different sets of users. This implies that each set of users obtains a different utilization target. Such a scenario MAY be represented by different Computing Shares. In general, given a number of shares to be set up, it is possible to adopt different configuration strategies in the underlying system. Regardless of the selected approach, the external behaviour does not change. The main goal of the Computing Share concept is to abstract from such implementation choices and to represent the externally observable behaviour.

The introduction of the Computing Share concept also supports the modelling of heterogeneity within a ComputingService by being able to have associations to different Execution Environments.

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
      <td style="text-align:left">ComputingShare</td>
      <td style="text-align:left">Share</td>
      <td style="text-align:left">A utilization target for a set of Execution Environments, defined by a
        set of configuration parameters and characterized by status information.</td>
      <td
      style="text-align:left"></td>
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
      <td style="text-align:left">MappingQueue</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The name of a queue available in the underlying Computing Manager (i.e.,
        LRMS) where jobs related to this share are submitted. Different Shares
        MAY be mapped into the same queue; it is not foreseen that a single share
        MAY be mapped into many different queues.</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxWallTime</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">s</td>
      <td style="text-align:left">The maximum obtainable wall clock time limit that MAY be granted to a
        single-slot job upon user request (un-normalized value, see below).</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxMultiSlotWallTime</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">s</td>
      <td style="text-align:left">The maximum obtainable wall clock time limit that MAY be granted to a
        multi-slot job upon user request; this value is measured from the start
        of the first slot up to the release of the last slot. (un-normalized value,
        see below).</td>
    </tr>
    <tr>
      <td style="text-align:left">MinWallTime</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">s</td>
      <td style="text-align:left">The minimum wall clock time per slot for a job (un-normalized value, see
        below); if a job requests a lower time, then it MAY be rejected; if a job
        requests at least this value, but runs for a shorter time, then it might
        be accounted for this value.</td>
    </tr>
    <tr>
      <td style="text-align:left">DefaultWallTime</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">s</td>
      <td style="text-align:left">The default wall clock time limit per slot assigned to a job by the Computing
        Manager (LRMS) if no limit is requested in the job submission description
        (un-normalized value, see below). Once this time is expired the job MAY
        be killed or removed from the queue.</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxCPUTime</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">s</td>
      <td style="text-align:left">The maximum obtainable CPU time limit that MAY be granted to the job upon
        user request per slot (un-normalized value, see below)</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxTotalCPUTime</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">s</td>
      <td style="text-align:left">The maximum obtainable CPU time limit that MAY be granted to the job upon
        user request across all assigned slots; this attribute is a limit on the
        sum of the CPU time used in all the slots occupied by a multi-slot job
        (un-normalized value, see below).</td>
    </tr>
    <tr>
      <td style="text-align:left">MinCPUTime</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">s</td>
      <td style="text-align:left">The minimum CPU time per slot for a job (un-normalized value, see below);
        if a job requests a lower time, than it MAY be rejected; if a job requests
        at least this value, but uses the CPU for a shorter time, then it might
        be accounted for this value.</td>
    </tr>
    <tr>
      <td style="text-align:left">DefaultCPUTime</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">s</td>
      <td style="text-align:left">The default CPU time limit per slot assigned to each job by the Computing
        Manager (LRMS ) if no limit is requested in the job submission description
        (un-normalized value, see below).</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxTotalJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The maximum allowed number of jobs in this Share.</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxRunningJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The maximum allowed number of jobs in the running state in this Share.</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxWaitingJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The maximum allowed number of jobs in the waiting state in this Share.</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxPreLRMSWaitingJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The maximum allowed number of jobs that are in the Grid layer waiting
        to be passed to the underlying computing manager (i.e., LRMS) for this
        Share.</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxUserRunningJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The maximum allowed number of jobs in the running state per Grid user
        in this Share.</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxSlotsPerJob</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">slot</td>
      <td style="text-align:left">The maximum number of slots which could be allocated to a single job in
        this Share (defined to be 1 for a Computing Manager accepting only single-slot
        jobs).</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxStageInStreams</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">stream</td>
      <td style="text-align:left">The maximum number of streams available to stage files in.</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxStageOutStreams</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">stream</td>
      <td style="text-align:left">The maximum number of streams available to stage files out.</td>
    </tr>
    <tr>
      <td style="text-align:left">SchedulingPolicy</td>
      <td style="text-align:left">SchedulingPolicy_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The type of scheduling policy used for the Share.</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxMainMemory</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">MB</td>
      <td style="text-align:left">The maximum physical RAM that a job is allowed to use; if the limit is
        hit, then the LRMS MAY kill the job.</td>
    </tr>
    <tr>
      <td style="text-align:left">GuaranteedMainMemory</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">MB</td>
      <td style="text-align:left">The amount of physical RAM that a job is guaranteed to have available
        for its use.</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxVirtualMemory</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">MB</td>
      <td style="text-align:left">The maximum total memory size (RAM plus swap) that a job is allowed to
        use; if the limit is hit, then the LRMS MAY kill the job.</td>
    </tr>
    <tr>
      <td style="text-align:left">GuaranteedVirtualMemory</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">MB</td>
      <td style="text-align:left">The total amount of memory (RAM plus swap) that a job is guaranteed to
        have available for its use.</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxDiskSpace</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">GB</td>
      <td style="text-align:left">The maximum disk space that a job is allowed use in the working area;
        if the limit is hit, then the LRMS MAY kill the job.</td>
    </tr>
    <tr>
      <td style="text-align:left">DefaultStorageService</td>
      <td style="text-align:left">URI</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The ID of the default Storage Service to be used to store files by jobs
        in the case that no destination Storage Service is explicitly chosen.</td>
    </tr>
    <tr>
      <td style="text-align:left">Preemption</td>
      <td style="text-align:left">ExtendedBoolean_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">True if the Computing Manager (i.e., LRMS) enables pre-emption of jobs;
        a pre-empted job is supposed to be automatically resumed, but may be suspended
        for an indefinite period.</td>
    </tr>
    <tr>
      <td style="text-align:left">ServingState</td>
      <td style="text-align:left">ServingState_t</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">A state specifying whether the Share is open to accept new requests, and
        if it is open to offer the already present requests for execution.</td>
    </tr>
    <tr>
      <td style="text-align:left">TotalJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The total number of jobs in any state (the sum of RunningJobs, WaitingJobs,
        StagingJobs, SuspendedJobs and PreLRMSWaitingJobs). Note that this number
        includes the locally submitted jobs.</td>
    </tr>
    <tr>
      <td style="text-align:left">RunningJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The number of jobs which are currently running in an Execution Environment,
        submitted via any type of interface (local and Grid).</td>
    </tr>
    <tr>
      <td style="text-align:left">LocalRunningJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The number of running jobs submitted via a local (non-GRID) interface.</td>
    </tr>
    <tr>
      <td style="text-align:left">WaitingJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The number of jobs which are currently waiting to start execution, submitted
        via any type of interface (local and Grid). Usually these will be queued
        in the underlying Computing Manager (i.e., a Local Resource Managment System
        or LRMS).</td>
    </tr>
    <tr>
      <td style="text-align:left">LocalWaitingJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The number of jobs which are currently waiting to start execution, submitted
        via a local (non-Grid) interface. Usually these will be queued in the underlying
        Computing Manager (i.e., a Local Resource Managment System or LRMS).</td>
    </tr>
    <tr>
      <td style="text-align:left">SuspendedJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The number of jobs, submitted via any type of interface (local and Grid),
        which have started their execution, but are currently suspended (e.g.,
        having been preempted by another job).</td>
    </tr>
    <tr>
      <td style="text-align:left">LocalSuspendedJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The number of jobs, submitted via a local (non-Grid) interface, which
        have started their execution, but are currently suspended (e.g., having
        been preempted by another job).</td>
    </tr>
    <tr>
      <td style="text-align:left">StagingJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The number of Grid jobs which are currently either staging files in before
        starting execution, or staging files out after finishing execution.</td>
    </tr>
    <tr>
      <td style="text-align:left">PreLRMSWaitingJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The number of Grid jobs which are currently managed by the Grid software
        layer waiting to be passed to the underlying Computing Manager (LRMS),
        and hence are not yet candidates to start execution.</td>
    </tr>
    <tr>
      <td style="text-align:left">EstimatedAverageWaitingTime</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">s</td>
      <td style="text-align:left">An estimate of the average time a job will wait after submission until
        it starts to execute. The value SHOULD be reported as 0 if there are free
        slots and a new job will start immediately, even if it takes some finite
        time for a job to be started.</td>
    </tr>
    <tr>
      <td style="text-align:left">EstimatedWorstWaitingTime</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">s</td>
      <td style="text-align:left">An estimate of the worst-case time a job could wait after submission until
        it starts to execute. This would generally be based on an assumption that
        all existing jobs run to their maximum allowed time limits.</td>
    </tr>
    <tr>
      <td style="text-align:left">FreeSlots</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">slot</td>
      <td style="text-align:left">The number of slots which are currently unoccupied by jobs and are free
        for new jobs in this Share to start immediately.</td>
    </tr>
    <tr>
      <td style="text-align:left">FreeSlotsWithDuration</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">slot:s</td>
      <td style="text-align:left">The number of free slots with their time limits. Syntax: ns[:t] [ns:t]*,
        where the pair ns:t means that there are <em>ns</em> free slots for the duration
        of <em>t</em> (expressed in seconds); the time limit information is optional.</td>
    </tr>
    <tr>
      <td style="text-align:left">UsedSlots</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">slot</td>
      <td style="text-align:left">The number of slots currently occupied by running jobs.</td>
    </tr>
    <tr>
      <td style="text-align:left">RequestedSlots</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">slot</td>
      <td style="text-align:left">The number of slots which are needed to execute all currently waiting
        and staging jobs.</td>
    </tr>
    <tr>
      <td style="text-align:left">ReservationPolicy</td>
      <td style="text-align:left">ReservationPolicy_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The type of policy used for advance reservation, if any.</td>
    </tr>
    <tr>
      <td style="text-align:left">Tag</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">A UserDomain-defined tag for this Share (the values SHOULD use a namespace
        based on the UserDomain name to avoid collision).</td>
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
        <p>ComputingEndpoint.ID</p>
        <p>[redefines Endpoint.ID]</p>
      </td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A computing share MAY be consumed via one or more computing endpoints.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>ExecutionEnvironment.ID</p>
        <p>[redefines Resource.ID]</p>
      </td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A computing share is defined on one or more computing resources.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>ComputingService.ID</p>
        <p>[redefines Service.ID]</p>
      </td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">A computing share participates in a computing service.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>ComputingActivity.ID</p>
        <p>[redefines Activity.ID]</p>
      </td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A computing share is being consumed by zero or more computing activities.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">ComputingShareAccelerator.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A computing share provides about the usage level of several accelerator
        devices.</td>
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
</table>As regards CPU Time and Wallclock Time related properties, there is a need to have a way to normalize them depending on the computing capacity of the ExecutionEnvironment. The approach proposed in GLUE is to add two attributes in the ExecutionEnvironment \(see Section 7.8\) which refer to the scaling factor to be used to compute the CPU/Wallclock time limit that a job will get if it will be assigned to such an ExecutionEnvironment via a certain Share. It is important that a job SHOULD always get at least the advertised CPU/Wallclock time. This means that the reference ExecutionEnvironment for the normalization should be always the fastest \(most powerful\) among those available in the entire ComputingService. For this ExecutionEnvironment, the scaling factor MUST be equal to 1. The CPU/Wallclock time values published by a Share therefore refer to the time limit that the job will get when mapped to this ExecutionEnvironment. For the other ExecutionEnvironments, the time should be adjusted according to the published scaling factors.

### ComputingShareAccelerator

The ComputingShareAccelerator class contains all the information about the usage level of the accelerator device bound to the computing share.

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
      <td style="text-align:left">ComputingShareAccelerator</td>
      <td style="text-align:left">Entity</td>
      <td style="text-align:left">The usage level of the accelerator devices for a given computing share</td>
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
      <td style="text-align:left">Type</td>
      <td style="text-align:left"><em>AccType_t</em>
      </td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The accelerator architecture type.</td>
    </tr>
    <tr>
      <td style="text-align:left">FreeSlots</td>
      <td style="text-align:left"><em>UInt32</em>
      </td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The number of accelerator cards slots which are currently unoccupied by
        jobs and are free for new jobs in this Share to start immediately</td>
    </tr>
    <tr>
      <td style="text-align:left">UsedSlots</td>
      <td style="text-align:left"><em>UInt32</em>
      </td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The number of accelerator cards slots currently occupied by running jobs.</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxSlotsPerJob</td>
      <td style="text-align:left"><em>UInt32</em>
      </td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The maximum number of accelerator slots which could be allocated to a
        single job in this Share</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">ComputingShare. ID</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">A set of accelerator information is related to a computing share.</td>
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
</table>### ComputingManager

The ComputingManager class is a specialization of the Manager class for the computational capability. The ComputingManager is responsible for the local control of resources, and this layer is not exposed directly to external clients. The operating system might be the simplest case of a Computing Manager, but the ComputingManager is often realized by means of a Local Resource Management \(LRMS\) "batch" system. A Computing Service will usually only have one Computing Manager, but MAY have more. The class provides aggregated information on controlled resources, and also describes local storage extents accessible to jobs.

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
      <td style="text-align:left">ComputingManager</td>
      <td style="text-align:left">Manager</td>
      <td style="text-align:left">A software component locally managing one or more Execution Environments.
        It MAY also describe aggregated information about the managed resources.
        The computing manager is also known as a Local Resource Management System
        (LRMS).</td>
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
      <td style="text-align:left"><em>ProductName</em>
      </td>
      <td style="text-align:left"><em>String</em>
      </td>
      <td style="text-align:left"><em>1</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><em>Name of the software product adopted as manager</em>
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
      <td style="text-align:left"><em>Version of the software product adopted as manager</em>
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
      <td style="text-align:left">Reservation</td>
      <td style="text-align:left">ExtendedBoolean_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">True if the Computing Manager (i.e, LRMS) supports advance reservation
        of resources.</td>
    </tr>
    <tr>
      <td style="text-align:left">BulkSubmission</td>
      <td style="text-align:left">ExtendedBoolean_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">True if the computing manager (i.e, LRMS) supports bulk submission of
        multiple jobs.</td>
    </tr>
    <tr>
      <td style="text-align:left">TotalPhysicalCPUs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">Ph.CPU</td>
      <td style="text-align:left">The total number of physical CPUs accessible via any of the available
        Endpoints and managed by this Computing Manager (there is one physical
        CPU per socket). This value SHOULD represent the total installed capacity,
        i.e. including resources which are temporarily unavailable.</td>
    </tr>
    <tr>
      <td style="text-align:left">TotalLogicalCPUs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">Log.CPU</td>
      <td style="text-align:left">The total number of logical CPUs accessible via any of the available Endpoints
        and managed by this Computing Manager (a logical CPU corresponds to a CPU
        visible to the operating system). This value SHOULD represent the total
        installed capacity, i.e. including resources which are temporarily unavailable.</td>
    </tr>
    <tr>
      <td style="text-align:left">TotalSlots</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">slot</td>
      <td style="text-align:left">The total number of slots managed by this Computing Manager which are
        currently available to run jobs.</td>
    </tr>
    <tr>
      <td style="text-align:left">SlotsUsedByLocalJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">slot</td>
      <td style="text-align:left">The number of slots currently occupied by jobs submitted via a local (non-Grid)
        interface.</td>
    </tr>
    <tr>
      <td style="text-align:left">SlotsUsedByGridJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">slot</td>
      <td style="text-align:left">The number of slots currently occupied by jobs submitted via a Grid interface.</td>
    </tr>
    <tr>
      <td style="text-align:left">Homogeneous</td>
      <td style="text-align:left">ExtendedBoolean_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">True if this Computing Manager manages only one type of Execution Environment.</td>
    </tr>
    <tr>
      <td style="text-align:left">NetworkInfo</td>
      <td style="text-align:left">NetworkInfo_t</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The type of internal network connection available among the managed Execution
        Environment instances. If many values are published then the various types
        of network MAY be available only within subsets of the Execution Environment
        instances; the Execution Environment properties SHOULD publish this information.</td>
    </tr>
    <tr>
      <td style="text-align:left">LogicalCPUDistribution</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">A classification of the managed Execution Environment instances aggregated
        by the number of logical CPUs. Syntax: X<em>1</em>:Y<em>1</em>, &#x2026;,
        X<em>n</em>:Y<em>n,</em> where I is the i-<em>th</em> group of Execution
        Environments with the same number of logical CPUs, X<em>i</em> is the number
        of logical CPUs in each Execution Environment instance and Y<em>i</em> is
        the number of Execution Environment instances.</td>
    </tr>
    <tr>
      <td style="text-align:left">WorkingAreaShared</td>
      <td style="text-align:left">ExtendedBoolean_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">True if the working area (see below) is shared across different Execution
        Environment instances (i.e., cluster nodes), typically via an NFS mount;
        this attribute applies to single-slot jobs.</td>
    </tr>
    <tr>
      <td style="text-align:left">WorkingAreaGuaranteed</td>
      <td style="text-align:left">ExtendedBoolean_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">True if the job is guaranteed the full extent of the WorkingAreaTotal;
        this attribute applies to single-slot jobs.</td>
    </tr>
    <tr>
      <td style="text-align:left">WorkingAreaTotal</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">GB</td>
      <td style="text-align:left">Total size of the working area (see below) available to all single-slot
        Grid jobs, either as a shared area across all the Execution Environments
        (WorkingAreaShared is true) or local to each Execution Environment (WorkingAreaShared
        is false). If the Computing Manager supports individual quotas per job/user,
        this is not advertised. In the case of a non-shared working area with a
        different local space allocation on each node, the advertised total size
        SHOULD be the minimum available across all the Execution Environment instances.</td>
    </tr>
    <tr>
      <td style="text-align:left">WorkingAreaFree</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">GB</td>
      <td style="text-align:left">The amount of free space currently available in the working area (see
        below), available to all single-slot Grid jobs either as a shared area
        across all the Execution Environments (WorkingAreaShared is true) or local
        to each Execution Environment (WorkingAreaShared is false). If the computing
        manager supports individual quotas per job/user, this is not advertised.
        In the case of a non-shared and non-guaranteed working area, this attribute
        SHOULD represent the minimum free working area currently available in any
        Execution Environment instance. In the case of a non-shared and guaranteed
        working area, the free size SHOULD equal the total size.</td>
    </tr>
    <tr>
      <td style="text-align:left">WorkingAreaLifeTime</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">s</td>
      <td style="text-align:left">The minimum guaranteed lifetime of the files created by single-slot Grid
        jobs in the working area (see below); the lifetime is related to the end
        time of the job. After the expiration of this lifetime, the files are not
        guaranteed to exist.</td>
    </tr>
    <tr>
      <td style="text-align:left">WorkingAreaMultiSlotTotal</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">GB</td>
      <td style="text-align:left">The total size of the working area (see below) available to all the multi-slot
        Grid jobs shared across all the Execution Environments. If the Computing
        Manager supports individual quotas per job/user, this is not advertised.</td>
    </tr>
    <tr>
      <td style="text-align:left">WorkingAreaMultiSlotFree</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">GB</td>
      <td style="text-align:left">The amount of free space currently available in the working area (see
        below) available to all multi-slot Grid jobs shared across all the Execution
        Environments. If the Computing Manager supports individual quotas per job/user,
        this is not advertised. This attribute SHOULD represent the minimum free
        working area currently available in any Execution Environment instance.</td>
    </tr>
    <tr>
      <td style="text-align:left">WorkingAreaMultiSlotLifeTime</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">s</td>
      <td style="text-align:left">The minimum guaranteed lifetime of the files created by multi-slot Grid
        jobs in the working area (see below); the lifetime is related to the end
        time of the job. After the expiration of the lifetime, the files are not
        guaranteed to exist.</td>
    </tr>
    <tr>
      <td style="text-align:left">CacheTotal</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">GB</td>
      <td style="text-align:left">If local caching of input files is supported, this attribute represents
        the total size of a shared storage area where frequently accessed data
        MAY be stored for rapid access by subsequent Grid jobs; in this area, files
        are kept after job completion for a certain amount of time, depending on
        the caching algorithm.</td>
    </tr>
    <tr>
      <td style="text-align:left">CacheFree</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">GB</td>
      <td style="text-align:left">If local caching of input files is supported, this attribute represents
        the free space in a shared storage area where frequently accessed data
        MAY be stored for rapid access by subsequent Grid jobs. In the computation
        of the free size, files which are not claimed by any job MAY be considered
        as deleted.</td>
    </tr>
    <tr>
      <td style="text-align:left">TmpDir</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The absolute path of a temporary directory local to an Execution Environment
        instance (i.e., a worker node). This directory MUST be available to programs
        using the normal file access primitives (open/read/write/close). Any files
        in the directory MAY be deleted as soon as the job which created them finishes.</td>
    </tr>
    <tr>
      <td style="text-align:left">ScratchDir</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The absolute path of a shared directory available for application data.
        Typically this is a POSIX accessible transient disk space shared between
        the Execution Environment instances, e.g. via an NFS mount. It MAY be used
        by MPI applications or to store intermediate files that need further processing
        by local jobs or as a staging area, especially if the Execution Environment
        instances have no internet connectivity. Any files in the directory MAY
        be deleted as soon as the job which created them finishes.</td>
    </tr>
    <tr>
      <td style="text-align:left">ApplicationDir</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The path of a directory available for installation of persistent application
        software and data. Typically this will be a POSIX accessible disk space,
        e.g. an NFS mount, with a long-term allocation of space to supported User
        Domains. The detailed usage of such a space SHOULD be described in a profile
        document for a specific Grid infrastructure.</td>
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
        <p>ComputingService.ID</p>
        <p>[redefines Service.ID]</p>
      </td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">A computing manager participates in a computing service.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>ExecutionEnvironment.ID</p>
        <p>[redefines Resource.ID]</p>
      </td>
      <td style="text-align:left">1..*</td>
      <td style="text-align:left">A computing manager manages one or more execution environments.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">ApplicationEnvironment.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A computing manager MAY use zero or more application environments.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">ComputingManagerAccelerator.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A computing manager MAY display information about the usage level of the
        accelerator devices installed in the cluster.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Benchmark.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A computing manager has zero or more associated benchmarks.</td>
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
</table>As regards the WorkingArea-related attributes and single-slot jobs, four scenarios should be considered. Both scenarios and the related attribute values are presented in Table 1.

**Table 1 Working Area and Single-slot jobs scenarios**

| Working Area | Shared | Guaranteed |
| :--- | :--- | :--- |
| One working area shared across all the Execution Environments and shared among simultaneous jobs. | true | false |
| One working area shared across all the Execution Environments with a guaranteed quota for each job. | true | true |
| A working area local to each Execution Environment, but shared among all the jobs which run simultaneously in those Execution Environments. | false | false |
| A working area local to each Execution Environment and dedicated to each job. | false | true |

In case there is a dedicated working area for multi-slot jobs, this SHOULD be represented by the WorkingAreaMultiSlot\* attributes. In case there is no dedicated working area for multi-slot jobs, i.e., there is a common working area for both single-slot and multi-slot jobs, we RECOMMEND to publish only the attributes related to the working area for single-slot jobs.

### ComputingManagerAccelerator

The ComputingManagerAccelerator contains information about the accelerator device handled by the computing manager.

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
      <td style="text-align:left">ComputingManagerAccelerator</td>
      <td style="text-align:left">Entity</td>
      <td style="text-align:left">The information about the accelerator device handled by the computing
        manager.</td>
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
      <td style="text-align:left">The accelerator architecture type.</td>
    </tr>
    <tr>
      <td style="text-align:left">TotalNumbers</td>
      <td style="text-align:left"><em>UInt32</em>
      </td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The total number of physical Accelerator cards accessible via any of the
        available Endpoints and managed by this Computing Manager. This value SHOULD
        represent the total installed capacity, i.e. including resources which
        are temporarily unavailable.</td>
    </tr>
    <tr>
      <td style="text-align:left">TotalSlots</td>
      <td style="text-align:left"><em>UInt32</em>
      </td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The total number of Accelerator slots managed by this Computing Manager
        which are currently available to run jobs.</td>
    </tr>
    <tr>
      <td style="text-align:left">UsedSlots</td>
      <td style="text-align:left"><em>UInt32</em>
      </td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The total number of slots currently occupied by jobs.</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">ComputingManager.ID</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">A set of accelerator information is related to a computing manager.</td>
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
</table>### Benchmark

The Benchmark class characterizes the relative performance of the computing resource by providing the result of a specific benchmark suite executed on the computing resource underlying the Computing Service. The Benchmark class provides both the type and the value of the benchmark.

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
      <td style="text-align:left">Benchmark</td>
      <td style="text-align:left">Entity</td>
      <td style="text-align:left">Benchmark information either about an Execution Environment providing
        computing capacity or about a CloudComputingInstanceType providing cloud
        computing capacity</td>
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
      <td style="text-align:left">Benchmark_t</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The type of benchmark.</td>
    </tr>
    <tr>
      <td style="text-align:left">Value</td>
      <td style="text-align:left">Real32</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The benchmark value.</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">ExecutionEnvironment.ID</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">A benchmark MAY be related to an execution environment.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">ComputingManager. ID</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">A benchmark MAY be related to a computing resource.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingInstanceType.ID</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">A benchmark MAY be related to a cloud computing instance type.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CloudComputingManager.ID</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">A benchmark MAY be related to a cloud computing resource.</td>
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
</table>### ExecutionEnvironment

The ExecutionEnvironment class describes the hardware and operating system environment in which a job will run. It represents a set of homogeneous Worker Nodes, so if a computing system contains nodes with significantly different properties there MAY be several ExecutionEnvironment instances. This implies that it should be possible to request a specific environment when a job is submitted. The ExecutionEnvironment MAY refer to virtual rather than physical machines.

As well as attributes describing a typical node, the class gives summary information about the size and usage of the set of nodes which possess those properties. However, there is no way to relate these to the information in other entities, e.g. it is not possible to know which jobs in a given ComputingShare are running on which ExecutionEnvironment.

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
      <td style="text-align:left">ExecutionEnvironment</td>
      <td style="text-align:left">Resource</td>
      <td style="text-align:left">A type of environment available to and requestable by a Grid job when
        submitted to a ComputingService via a Computing Endpoint; the type of environment
        is described in terms of hardware, operating system and network characteristics.
        Information about the total/available/used instances of this type of execution
        environment are also included.</td>
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
      <td style="text-align:left">Attribute</td>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Unit</td>
      <td style="text-align:left">Description</td>
    </tr>
    <tr>
      <td style="text-align:left">Platform</td>
      <td style="text-align:left">Platform_t</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The platform architecture of this Execution Environment.</td>
    </tr>
    <tr>
      <td style="text-align:left">VirtualMachine</td>
      <td style="text-align:left">ExtendedBoolean_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">True if the Execution Environment is hosted within a virtual machine;
        in this case, the values of the other attributes are related to the virtualized
        environment and not to the hosting environment.</td>
    </tr>
    <tr>
      <td style="text-align:left">TotalInstances</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The total number of Execution Environment instances. This SHOULD reflect
        the total installed capacity, i.e. including resources which are temporarily
        unavailable.</td>
    </tr>
    <tr>
      <td style="text-align:left">UsedInstances</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The number of Execution Environment instances which are considered to
        be fully used; an instance is used when, according to the policies of the
        Computing Manager (i.e., LRMS), it cannot accept new jobs because it already
        runs the maximum number of allowed jobs.</td>
    </tr>
    <tr>
      <td style="text-align:left">UnavailableInstances</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The number of Execution Environment instances which are currently unavailable,
        e.g. because of failures or maintenance.</td>
    </tr>
    <tr>
      <td style="text-align:left">PhysicalCPUs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The number of physical CPUs in one ExecutionEnvironment instance, i.e.
        the number of sockets per Worker Node.</td>
    </tr>
    <tr>
      <td style="text-align:left">LogicalCPUs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The number of logical CPUs in one Execution Environment instance, i.e.
        typically the number of cores per Worker Node.</td>
    </tr>
    <tr>
      <td style="text-align:left">CPUMultiplicity</td>
      <td style="text-align:left">CPUMultiplicity_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Condensed information about the multiplicity of both physical CPUs and
        cores available in an execution environment instance..</td>
    </tr>
    <tr>
      <td style="text-align:left">CPUVendor</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The name of the physical CPU vendor. Free format, but it SHOULD correspond
        to the name by which the vendor is generally known.</td>
    </tr>
    <tr>
      <td style="text-align:left">CPUModel</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The name of the physical CPU model, as defined by the vendor.</td>
    </tr>
    <tr>
      <td style="text-align:left">CPUVersion</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The specific version of the Physical CPU model, as defined by the vendor.</td>
    </tr>
    <tr>
      <td style="text-align:left">CPUClockSpeed</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">MHz</td>
      <td style="text-align:left">The nominal clock speed of the physical CPU.</td>
    </tr>
    <tr>
      <td style="text-align:left">CPUTimeScalingFactor</td>
      <td style="text-align:left">Real32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The factor used by the Computing Manager (i.e., LRMS) to scale the CPU
        time limit (the CPU Time is divided by the CPUTimeScalingFactor); for the
        reference execution environment, this attribute is equal to 1. See the
        description of the ComputingShare for further information.</td>
    </tr>
    <tr>
      <td style="text-align:left">WallTimeScalingFactor</td>
      <td style="text-align:left">Real32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The factor used by the Computing Manager (i.e., LRMS) to scale the Wallclock
        time limit (the Wallclock Time is divided by the WallTimeScalingFactor).
        See the description of the ComputingShare for further information.</td>
    </tr>
    <tr>
      <td style="text-align:left">ConnectivityOut</td>
      <td style="text-align:left">ExtendedBoolean_t</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">True if direct outbound network connectivity is available from a running
        job, even if limited, e.g. by firewall rules.</td>
    </tr>
    <tr>
      <td style="text-align:left">NetworkInfo</td>
      <td style="text-align:left">NetworkInfo_t</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The type of internal network connection available among the Execution
        Environment instances.</td>
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
        <p>ComputingManager.ID</p>
        <p>[redefines Manager.ID]</p>
      </td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">An execution environment is managed by a computing manager.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>ComputingShare.ID</p>
        <p>[redefines Share.ID]</p>
      </td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">An execution environment provides capacity in terms of computing shares.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>ComputingActivity.ID</p>
        <p>[redefines Activity.ID]</p>
      </td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">An execution environment runs zero or more computing activities.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">AcceleratorEnvironment.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">An execution environment MAY contains zero or more accelerator environments.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">ApplicationEnvironment.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">An execution environment offers zero or more application environments.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Benchmark.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">An execution environment has zero or more associated benchmarks.</td>
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
</table>Each ExecutionEnvironment instance is under the control of a ComputingManager \(i.e., LRMS\). An ExecutionEnvironment MAY be realized in several ways. Examples are a physical computing node, or a virtual machine image that MAY be requestable by a job \(different virtual machine images MAY coexist on the same physical node\).

### AcceleratorEnvironment

The AcceleratorEnvironment is an entity used to describe a homogeneous set of accelerator processors. This entity is associated with one or more execution environments.

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
      <td style="text-align:left">AcceleratorEnvironment</td>
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
      <td style="text-align:left"><em>AccType_t</em>
      </td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The type of Accelerator.</td>
    </tr>
    <tr>
      <td style="text-align:left">Numbers</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The number of physical Accelerators in one ExecutionEnvironment instance,
        i.e. the number of accelerator cards per Worker Node.</td>
    </tr>
    <tr>
      <td style="text-align:left">Vendor</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The name of the physical Accelerator vendor. Free format, but it SHOULD
        correspond to the name by which the vendor is generally known.</td>
    </tr>
    <tr>
      <td style="text-align:left">Model</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The name of the physical Accelerator model, as defined by the vendor.</td>
    </tr>
    <tr>
      <td style="text-align:left">Version</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The specific version of the Physical Accelerator model, as defined by
        the vendor.</td>
    </tr>
    <tr>
      <td style="text-align:left">ClockSpeed</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">MHz</td>
      <td style="text-align:left">The nominal clock speed of the physical Accelerator.</td>
    </tr>
    <tr>
      <td style="text-align:left">Memory</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">MB</td>
      <td style="text-align:left">The nominal memory size of the physical Accelerator</td>
    </tr>
    <tr>
      <td style="text-align:left">ComputeCapability</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Compute Capability is a reference, an ID or tag, representing the set
        of features supported by an accelerator device, as declared by the vendor</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">ExecutionEnvironment.ID</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">An accelerator environment is associated with one execution environments.</td>
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
</table>### ApplicationEnvironment

The ApplicationEnvironment class describes the software environment in which a job will run, i.e. what pre-installed software will be available to it. Each Application is identified by a name \(the AppName attribute\); these names are not defined within the schema, but SHOULD be assigned in a way which allows applications to be uniquely identified. In some deployment scenarios, the definition of namespace-based AppNames or guidelines for the generation of unique application names MAY be specified, and application repository services relying on those application names MAY be provided. This aspect is considered out of scope for the GLUE schema specification, but MAY be included in a profile document for a specific production Grid.

The ApplicationEnvironment can be used to describe installed application software or special environment setups in terms of a simple tag string. In this case, the AppName attribute should be used to publish this tag; other attributes are optional.

The properties of installed software may vary substantially, but the attributes of the class cover the most common cases, in particular for licensed software. If necessary, additional information MAY be added using the OtherInfo attribute and the Extension class.

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
      <td style="text-align:left">ApplicationEnvironment</td>
      <td style="text-align:left">Entity</td>
      <td style="text-align:left">A description of installed application software or software environment
        characteristics available within one or more Execution Environments.</td>
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
      <td style="text-align:left">AppName</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The name of the application or environment.</td>
    </tr>
    <tr>
      <td style="text-align:left">AppVersion</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The version of the application or environment, as defined by the supplier.</td>
    </tr>
    <tr>
      <td style="text-align:left">Repository</td>
      <td style="text-align:left">URL</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The URL of a service which offers a name service and/or a repository for
        this application environment. Application environments can be categorized
        under namespaces maintained by application repositories.</td>
    </tr>
    <tr>
      <td style="text-align:left">State</td>
      <td style="text-align:left">AppEnvState_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The current installation state of the application.</td>
    </tr>
    <tr>
      <td style="text-align:left">RemovalDate</td>
      <td style="text-align:left">DateTime_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The date and time after which the application MAY be removed.</td>
    </tr>
    <tr>
      <td style="text-align:left">License</td>
      <td style="text-align:left">License_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The type of license under which the application is usable.</td>
    </tr>
    <tr>
      <td style="text-align:left">Description</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">A human-readable description of this application or environment.</td>
    </tr>
    <tr>
      <td style="text-align:left">BestBenchmark</td>
      <td style="text-align:left">Benchmark_t</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The type of benchmark which best identifies the sensitivity of this application
        to the performance of the Execution Environment, which can be compared
        with the rating published via the Benchmark class.</td>
    </tr>
    <tr>
      <td style="text-align:left">ParallelSupport</td>
      <td style="text-align:left">ParallelSupport_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The type of supported parallel execution framework.</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxSlots</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">slot</td>
      <td style="text-align:left">The maximum number of concurrent slots that may be used to run jobs using
        the application.</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">job</td>
      <td style="text-align:left">The maximum number of concurrent jobs that may use the application.</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxUserSeats</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">user seat</td>
      <td style="text-align:left">The maximum number of concurrent user seats (i.e. distinct users) that
        may use the application.</td>
    </tr>
    <tr>
      <td style="text-align:left">FreeSlots</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">slot</td>
      <td style="text-align:left">The number of slots currently available to run jobs using the application.</td>
    </tr>
    <tr>
      <td style="text-align:left">FreeJobs</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">slot</td>
      <td style="text-align:left">The number of jobs that could immediately start their execution using
        the application.</td>
    </tr>
    <tr>
      <td style="text-align:left">FreeUserSeats</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">user seat</td>
      <td style="text-align:left">The current number of free seats for additional users to use the application.</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">ExecutionEnvironment.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">An application environment MAY be used in zero or more execution environments.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">ComputingManager.ID</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">An application environment is part of a computing manager.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">ApplicationHandle.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">An application environment MAY be handled via zero or more application
        handles.</td>
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
</table>### ApplicationHandle

The ApplicationHandle class is an extension to ApplicationEnvironment for applications which need to be set up in some way before they can be used. For each supported setup method a string MAY be specified, the interpretation of which is specific to the method - in the simplest case this could just be a setup script to execute. A single Application MAY support multiple setup methods.

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
      <td style="text-align:left">ApplicationHandle</td>
      <td style="text-align:left">Entity</td>
      <td style="text-align:left">The description of a technique for bootstrapping and/or accessing an application
        environment.</td>
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
      <td style="text-align:left">ApplicationHandle_t</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The type of method used to set up this application environment.</td>
    </tr>
    <tr>
      <td style="text-align:left">Value</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">A string which defines how to set up this application in the context of
        the setup method specified by the Type.</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">ApplicationEnvironment.ID</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">An application handle MAY be used for one application environment.</td>
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
</table>### ComputingActivity

The ComputingActivity class represents a single \(but possibly multi-processor\) job. The attributes give the job properties and state as seen by the local batch system, together with some Grid-level information.

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
      <td style="text-align:left">ComputingActivity</td>
      <td style="text-align:left">Activity</td>
      <td style="text-align:left">An Activity managed by an OGSA execution capability service (the Computing
        Activity is traditionally called a job).</td>
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
      <td style="text-align:left">ComputingActivityType_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The type of this Computing Activity.</td>
    </tr>
    <tr>
      <td style="text-align:left">IDFromEndpoint</td>
      <td style="text-align:left">URI</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The job ID as assigned by the Computing Endpoint.</td>
    </tr>
    <tr>
      <td style="text-align:left">LocalIDFromManager</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The local ID of the job as assigned by the Computing Manager (i.e., LRMS).</td>
    </tr>
    <tr>
      <td style="text-align:left">JobDescription</td>
      <td style="text-align:left">JobDescription_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The job description language used to specify the job request.</td>
    </tr>
    <tr>
      <td style="text-align:left">State</td>
      <td style="text-align:left">ComputingActivityState_t</td>
      <td style="text-align:left">1..*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The state of the job; different state models are allowed; a state for
        each model is allowed provided that it has a different namespace prefix
        (see data type definition)</td>
    </tr>
    <tr>
      <td style="text-align:left">RestartState</td>
      <td style="text-align:left">ComputingActivityState_t</td>
      <td style="text-align:left">0..*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The state from which a failed job MAY restart upon a client request; different
        state models are allowed; a state for each model is allowed provided that
        it has a different namespace prefix (see data type definition)</td>
    </tr>
    <tr>
      <td style="text-align:left">ExitCode</td>
      <td style="text-align:left">Int32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The exit code as returned by the main executable code or script of the
        job.</td>
    </tr>
    <tr>
      <td style="text-align:left">ComputingManagerExitCode</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The exit code provided by the Computing Manager (i.e., LRMS).</td>
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
      <td style="text-align:left">WaitingPosition</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">For a waiting job being queued in the Computing Manager (i.e., LRMS),
        the position of the job in the queue.</td>
    </tr>
    <tr>
      <td style="text-align:left">UserDomain</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The User Domain specified by the job owner in the job submission request.
        The owner MAY belong to several User Domains, but typically decides which
        one to choose when submitting a job.</td>
    </tr>
    <tr>
      <td style="text-align:left">Owner</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The Grid identity of the job&#x2019;s owner; in the case that anonymity
        is required, the reserved value CONFIDENTIAL should be advertised.</td>
    </tr>
    <tr>
      <td style="text-align:left">LocalOwner</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The local user name to which the job&#x2019;s owner is mapped for the
        execution of this job.</td>
    </tr>
    <tr>
      <td style="text-align:left">RequestedTotalWallTime</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">s</td>
      <td style="text-align:left">The total wall clock time requested by the job; for multi-slot jobs, it
        represents the sum of wall clock times needed for each required slot.</td>
    </tr>
    <tr>
      <td style="text-align:left">RequestedTotalCPUTime</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">s</td>
      <td style="text-align:left">The total CPU time requested by the job; for multi-slot jobs, it represents
        the sum of CPU times needed for each required slot.</td>
    </tr>
    <tr>
      <td style="text-align:left">RequestedSlots</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">slot</td>
      <td style="text-align:left">The number of slots requested for this job.</td>
    </tr>
    <tr>
      <td style="text-align:left">RequestedApplicationEnvironment</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">A serialization of the AppName and Version of the requested Application
        Environments (the serialization syntax is delegated to the implementation).</td>
    </tr>
    <tr>
      <td style="text-align:left">StdIn</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The name of the file which is used as the standard input of the job.</td>
    </tr>
    <tr>
      <td style="text-align:left">StdOut</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The name of the file which contains the standard output of the job.</td>
    </tr>
    <tr>
      <td style="text-align:left">StdErr</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The name of the file which contains the standard error of the job.</td>
    </tr>
    <tr>
      <td style="text-align:left">LogDir</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The name of the directory which contains the logs related to the job and
        generated by the Grid layer (usually the directory is private to the job).</td>
    </tr>
    <tr>
      <td style="text-align:left">ExecutionNode</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">A hostname associated to the Execution Environment instance (i.e., worker
        node) running the job; multi-node jobs are described by several instances
        of this attribute.</td>
    </tr>
    <tr>
      <td style="text-align:left">Queue</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The name of the Computing Manager (i.e, LRMS) queue in which this job
        was queued before execution.</td>
    </tr>
    <tr>
      <td style="text-align:left">UsedTotalWallTime</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">s</td>
      <td style="text-align:left">The total wall clock time consumed so far by the job. In case of multi-slot
        jobs, this value refers to the sum of the wall clock time consumed in each
        slot.</td>
    </tr>
    <tr>
      <td style="text-align:left">UsedTotalCPUTime</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">s</td>
      <td style="text-align:left">The total CPU time consumed so far by the job. In case of multi-slot jobs,
        this value refers to the sum of the CPU time consumed in each slot.</td>
    </tr>
    <tr>
      <td style="text-align:left">UsedMainMemory</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">MB</td>
      <td style="text-align:left">The physical RAM currently used by the job.</td>
    </tr>
    <tr>
      <td style="text-align:left">SubmissionTime</td>
      <td style="text-align:left">DateTime_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The time when the job was submitted to the Computing Endpoint.</td>
    </tr>
    <tr>
      <td style="text-align:left">ComputingManagerSubmissionTime</td>
      <td style="text-align:left">DateTime_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The time when the job was submitted to the Computing Manager (i.e., LRMS)
        by the Grid layer.</td>
    </tr>
    <tr>
      <td style="text-align:left">StartTime</td>
      <td style="text-align:left">DateTime_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The time when the job entered the Computing Manager (i.e., LRMS) running
        state.</td>
    </tr>
    <tr>
      <td style="text-align:left">ComputingManagerEndTime</td>
      <td style="text-align:left">DateTime_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The time when the job entered its final Computing Manager (i.e., LRMS)
        state.</td>
    </tr>
    <tr>
      <td style="text-align:left">EndTime</td>
      <td style="text-align:left">DateTime_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The time when the job entered its final state as recorded by the Grid
        layer.</td>
    </tr>
    <tr>
      <td style="text-align:left">WorkingAreaEraseTime</td>
      <td style="text-align:left">DateTime_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">A working area is an allocated storage extent that holds the home directories
        of the Grid jobs; this attribute specifies the time when the dedicated
        working area of this job will be removed.</td>
    </tr>
    <tr>
      <td style="text-align:left">ProxyExpirationTime</td>
      <td style="text-align:left">DateTime_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The expiration time of the Grid proxy currently associated with the job;
        in case of a proxy with attribute certificates having different expiration
        times, then this value represent the minimum expiration time among all
        the values.</td>
    </tr>
    <tr>
      <td style="text-align:left">SubmissionHost</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The name of the host from which the job was submitted.</td>
    </tr>
    <tr>
      <td style="text-align:left">SubmissionClientName</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The name of the software client which was used to submit the job.</td>
    </tr>
    <tr>
      <td style="text-align:left">OtherMessages</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Optional job messages provided by either the Grid Layer or the Computing
        Manager (i.e., LRMS).</td>
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
        <p>ComputingEndpoint.ID</p>
        <p>[redefines Endpoint.ID]</p>
      </td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">A computing activity is submitted to a computing endpoint.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>ComputingShare.ID</p>
        <p>[redefines Share.ID]</p>
      </td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">A computing activity is mapped into a computing share.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>ExecutionEnvironment.ID</p>
        <p>[redefines Resource.ID]</p>
      </td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">A computing activity is executed in an execution environment.</td>
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
</table>In this specification, the ComputingActivity may refer to simple jobs, or to elements of collections or workflows. The description of the relationships between jobs which are part of a collection or workflow may be considered in future revisions of the specification.

As regards the State attribute and the related ComputingActivityState\_t type, we note that currently there is no commonly accepted state model for Grid jobs. Each production Grid middleware defines and is using its own state model. As regards the standardization process, the OGSA-BES specification defines a simple state model. The middleware providers have started to define their own extensions to the BES state model, but they differ and do not enable interoperability. Given the current scenario, we RECOMMEND to use namespaces in state model values, so that every middleware provider MAY publish the ComputingActivity State according to its definition. We expect that an extension to the core BES state model common to all the middleware providers and suitable for production scenarios may be defined by a profiling activity of the BES/ JSDL/GLUE specifications.

### ToStorageService

The ToStorageService class represents the case where a filesystem from a StorageService is available to jobs running on a Computing Service via POSIX access, e.g. as an NFS mount. Each ToStorageService instance represents a single mount point. It is assumed that such mounts are available on all nodes \(i.e. all Execution Environments\) in the ComputingService.

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
      <td style="text-align:left">ToStorageService</td>
      <td style="text-align:left">Entity</td>
      <td style="text-align:left">The description of POSIX access via a file system technology enabling
        jobs running in the Computing Service to access an associated Storage Service.</td>
      <td
      style="text-align:left"></td>
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
      <td style="text-align:left">LocalPath</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The local path within the Computing Service which makes it possible to
        access files in the associated Storage Service (this is typically an NFS
        mount point).</td>
    </tr>
    <tr>
      <td style="text-align:left">RemotePath</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The remote path in the Storage Service which is associated to the local
        path in the Computing Service (this is typically an NFS exported directory).</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">ComputingService.ID</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">Is associated to a computing service.</td>
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
</table>## 

