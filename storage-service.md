---
description: Section 9
---

# 9. Conceptual Model of the Storage Service

The conceptual model of the Storage Service is based on the main entities and uses specializations of the Service, Endpoint, Share, Manager, Resource, and Activity entities.  Further storage-related concepts such as StorageServiceCapacity, StorageShareCapacity and StorageAccessProtocol are also introduced.

![](.gitbook/assets/0%20%286%29.png)

**Figure 4 Entities and relationships for the Storage Service conceptual model**

As explained in Section , we use the concept of storage extent to mean the capabilities and management of the various media that exist to store data and allow data retrieval.

### 9.1. StorageService

A StorageService represents a storage system, most often hosted by a single site, but possibly distributed over multiple sites. A StorageService makes StorageShares of given properties available to selected UserDomains, typically \(not necessarily\) through one or more explicitly identified StorageEndpoints. Data may be stored in or retrieved from StorageShares through one or more StorageAccessProtocols. A StorageShare is a composition of extents from one or more DataStores. StorageShares MAY overlap, i.e. map to the same underlying extent. A DataStore represents a physical device that holds data \(e.g. a disk farm or a tape robot\). Each DataStore is managed by a StorageManager, an instance of a particular software product identified by the ProductName and ProductVersion. StorageServiceCapacity objects summarize capacity-related information, for which details may be available associated to StorageShares and DataStores.

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
      <td style="text-align:left">StorageService</td>
      <td style="text-align:left">Service</td>
      <td style="text-align:left">
        <p>An abstracted, logical view of software and hardware components that participate
          in the creation of a storage capability in the environment. A Storage Service
          exposes zero or more Endpoints having well-defined interfaces, zero or
          more Storage Shares and zero or more Storage Managers and the related Data
          Stores. The Storage Service also offers zero or more Storage Access Protocols,
          and provides summary information about the overall amount of storage by
          means of the Storage Service Capacity.</p>
        <p>The Storage Service is autonomous and denotes a weak aggregation among
          Storage Endpoints, Storage Shares, Storage Managers, Storage Access Protocols
          and Storage Service Capacities. The Storage Service enables the identification
          of the entire set of entities providing storage functionality with a persistent
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
      <td style="text-align:left"><em>No extra properties are defined in the specialized entity.</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
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
        <p>StorageEndpoint.ID</p>
        <p>[redefines Endpoint.ID]</p>
      </td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A storage service exposes zero or more storage endpoints.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">StorageShare.ID [redefines Share.ID]</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A storage service serves zero or more storage shares.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>StorageManager.ID</p>
        <p>[redefines Manager.ID]</p>
      </td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A storage service provides zero or more storage managers.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">StorageAccessProtocol.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A storage service offers zero or more storage access protocols.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">StorageServiceCapacity.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A storage service has zero or more storage service capacities.</td>
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
      <td style="text-align:left">Contact.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A service has zero or more contacts.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Location.ID</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">A service is primary located at a location.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Service.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A service is related to zero or more services.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>The Storage Service MAY expose Storage Endpoints enabling management of or access to different types of storage extent. The usage of storage is typically constrained by policies, thus implying service differentiation. The Storage Share concept describes a portion of the managed storage extents with a homogeneous set of usage policies. The storage extents used to implement the Shares are locally managed by one or more Storage Managers, and their properties are described by Data Stores.

### StorageServiceCapacity

The StorageServiceCapacity class summarizes capacity-related information for all the StorageShares and DataStores of a given homogeneous type. The summaries MAY be compared to the sums of the relevant StorageShareCapacity attributes for the StorageShares of the given type. Capacities of overlapping StorageShares MUST only be counted once. An inconsistency between a summary value and the corresponding sum of relevant attributes MAY occur if part of the capacity is not explicitly published, or if the attributes concerned could not all be exactly determined or recorded at the same time. The summaries MAY also be compared to the sums of the relevant attributes of the DataStores of the given type, where inconsistencies MAY arise due to similar causes.

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
      <td style="text-align:left">StorageServiceCapacity</td>
      <td style="text-align:left">Entity</td>
      <td style="text-align:left">Description of the size and usage of a homogenous storage extent; the
        storage extent is aggregated at the storage service level by type.</td>
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
      <td style="text-align:left">StorageCapacity_t</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The type of storage capacity.</td>
    </tr>
    <tr>
      <td style="text-align:left">TotalSize</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">GB</td>
      <td style="text-align:left">The total amount of storage of this Type (the sum of free, used and reserved).</td>
    </tr>
    <tr>
      <td style="text-align:left">FreeSize</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">GB</td>
      <td style="text-align:left">The amount of storage which is free for new data to be stored. This SHOULD
        include space occupied by cached copies of objects which can be deleted
        automatically to make room for new ones.</td>
    </tr>
    <tr>
      <td style="text-align:left">UsedSize</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">GB</td>
      <td style="text-align:left">The amount of storage which is occupied by stored data. This SHOULD exclude
        space occupied by cached copies of objects which can be deleted automatically
        to make room for new ones.</td>
    </tr>
    <tr>
      <td style="text-align:left">ReservedSize</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">GB</td>
      <td style="text-align:left">The amount of storage which is not occupied by stored data, but has been
        reserved for use by a specific user or group, and hence is not free for
        the storage of new data except in the context of that reservation.</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">StorageService.ID</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">A storage service capacity is related to one storage service.</td>
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
</table>### StorageAccessProtocol

A StorageAccessProtocol describes a protocol that can be used to store data in or retrieve data from StorageShares. The "file" protocol indicates that for ComputingServices given by ToComputingService objects the StorageShares are available through POSIX I/O. The mount point details are given by corresponding ToStorageService objects published by those ComputingServices. Most protocols require a negotiation between the client and a StorageEndpoint. For example, a StorageEndpoint implementing a version of the SRM protocol may be asked for a data transfer URL corresponding to a desired access protocol. An access protocol that does not require prior negotiation MAY be published as one or more StorageEndpoints with an InterfaceName corresponding to that protocol.

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
      <td style="text-align:left">StorageAccessProtocol</td>
      <td style="text-align:left">Entity</td>
      <td style="text-align:left">A type of protocol available to access the underlying storage extents.</td>
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
      <td style="text-align:left">StorageAccessProtocol_t</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">An identifier for the protocol.</td>
    </tr>
    <tr>
      <td style="text-align:left">Version</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The version of the protocol supported by the interface, as defined by
        the protocol specification.</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxStreams</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">stream</td>
      <td style="text-align:left">The maximum number of parallel network streams which can be used for a
        single data transfer operation using this protocol.</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">StorageService.ID</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">A storage access protocol is related to one storage service.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">ToComputingService</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A storage access protocol MAY be used by zero or more computing services.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">ToCloudComputingService</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A storage access protocol MAY be used by zero or more cloud computing
        services.</td>
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
</table>If a type of Storage Access Protocol needs to be discoverable, then the StorageAccessProtocol class SHOULD be used to advertise it. If a certain Access Protocol

has an associated URL and this URL needs to be discoverable, then the Access Protocol SHOULD be also published via the StorageEndpoint class.

### StorageEndpoint

A StorageEndpoint represents a service that may be contacted by clients to manage StorageShares, to store or retrieve data or to perform other operations related to a storage system. The StorageEndpoint typically implements a storage control protocol specified by the InterfaceName, which allows for the manipulation of StorageShares and the properties of their data content. Access to StorageShares for storing or retrieving data often has to be negotiated through the given control protocol. The available access protocols MAY be published in StorageAccessProtocol objects. The StorageEndpoint interface MAY also be used to publish the endpoint\(s\) of an access protocol that does not require prior negotiation. The Storage Endpoint may be able to serve only a subset of the StorageShares within the StorageService, in which case that subset MAY be indicated through explicit associations with those StorageShares.

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
      <td style="text-align:left">StorageEndpoint</td>
      <td style="text-align:left">Endpoint</td>
      <td style="text-align:left">An Endpoint usable for managing Storage Shares or for accessing data stored
        in them; it MAY also be used to expose complementary capabilities which
        form part of the overall Storage Service.</td>
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
      <td style="text-align:left"><em>No extra properties are defined in the specialized entity.</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
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
        <p>StorageService.ID</p>
        <p>[redefines Service.ID]</p>
      </td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">A storage endpoint is part of a storage service.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>StorageShare.ID</p>
        <p>[redefines Share.ID]</p>
      </td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A storage endpoint MAY pass activities to zero or more storage shares.</td>
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
      <td style="text-align:left">An endpoint has assocated zero or more AccessPolicies.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>### StorageShare

A StorageShare is a composition of extents from one or more DataStores. StorageShares that overlap, i.e. share the same underlying extent, have the same SharingID, which in that case MUST neither be empty nor the reserved string "dedicated". A DataStore represents a physical device or set of devices that are able to hold data \(e.g. a disk farm or a tape robot\). A StorageShare need not be composed of homogeneous devices.

The AccessLatency gives the maximum latency category for an object stored in the StorageShare to be made available for reading. For example, if the StorageShare comprises both disk and tape storage, and data may need to be recalled from tape, the published AccessLatency is "nearline", although a given data object may in fact be immediately accessible on disk.

The RetentionPolicy indicates at a coarse granularity the probability of the StorageShare losing data. For example, "custodial" represents a very low probability, while "replica" indicates that the StorageShare is not suitable for keeping the only copy of precious data, but may be used for keeping a replica of such data.

The ExpirationMode indicates what happens to data whose lifetime has expired, if ever. The Identifier allows the StorageShare to be given a tag that is meaningful for the UserDomain\(s\) served by the StorageShare. For example, for version 2.2 of the SRM control protocol a StorageShare would represent a Space and the Identifier the corresponding SpaceTokenUserDescription. Capacity-related information is made available through StorageShareCapacity objects. A StorageShare may not be available through StorageEndpoints not explicitly related to the Share.

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
      <td style="text-align:left">StorageShare</td>
      <td style="text-align:left">Share</td>
      <td style="text-align:left">A utilization target for a set of extents in Data Stores, defined by a
        set of configuration parameters and policies and characterized by status
        information.</td>
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
      <td style="text-align:left">ServingState</td>
      <td style="text-align:left">ServingState_t</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">A state specifying whether the Share is open to place new requests, and
        if it is currently offering any requests already present for execution.</td>
    </tr>
    <tr>
      <td style="text-align:left">Path</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">A default namespace where data objects are logically placed when they
        are stored into this Share. This will typically be used as a prefix when
        generating a file name under which the data object is stored.</td>
    </tr>
    <tr>
      <td style="text-align:left">AccessMode</td>
      <td style="text-align:left">AccessMode_t</td>
      <td style="text-align:left">0..*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">An identifier for the type of access and usage allowed for this Share.</td>
    </tr>
    <tr>
      <td style="text-align:left">SharingID</td>
      <td style="text-align:left">LocalID_t</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">A local identifier common to the set of Storage Shares which use the same
        underlying extents, i.e. which share the same pool of storage space. (&#x2018;dedicated&#x2019;
        is a reserved value which means that the Storage Share extents are not
        shared with other Storage Shares.)</td>
    </tr>
    <tr>
      <td style="text-align:left">AccessLatency</td>
      <td style="text-align:left">AccessLatency_t</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The maximum latency category under normal operating conditions for a data
        object stored in this share to be made available for reading.</td>
    </tr>
    <tr>
      <td style="text-align:left">RetentionPolicy</td>
      <td style="text-align:left">RetentionPolicy_t</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The quality of data retention, which indicates the probability of the
        storage system losing a data object.</td>
    </tr>
    <tr>
      <td style="text-align:left">ExpirationMode</td>
      <td style="text-align:left">ExpirationMode_t</td>
      <td style="text-align:left">0..3</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">An attribute which indicates support for data objects with infinite and/or
        finite lifetimes, and what actions the storage service may take upon the
        expiration of an object lifetime.</td>
    </tr>
    <tr>
      <td style="text-align:left">DefaultLifeTime</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">s</td>
      <td style="text-align:left">The default lifetime assigned to a new data object if no explicit lifetime
        is specified.</td>
    </tr>
    <tr>
      <td style="text-align:left">MaximumLifeTime</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">s</td>
      <td style="text-align:left">The maximum lifetime that may be requested for a data object.</td>
    </tr>
    <tr>
      <td style="text-align:left">MaxObjectSize</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">MB</td>
      <td style="text-align:left">Maximum size of a data object which can be stored in this share</td>
    </tr>
    <tr>
      <td style="text-align:left">MinObjectSize</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">MB</td>
      <td style="text-align:left">Minimum size of a data object which can be stored in this share</td>
    </tr>
    <tr>
      <td style="text-align:left">Tag</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">An identifier defined by a User Domain which identifies a Share with a
        specific set of properties.</td>
    </tr>
    <tr>
      <td style="text-align:left">NumberOfFiles</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Optional attribute that describes the number of files stored in this StorageShare</td>
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
        <p>StorageEndpoint.ID</p>
        <p>[redefines Endpoint.ID]</p>
      </td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A storage share is consumed via zero or more endpoints.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>DataStore.ID</p>
        <p>[redefines Resource.ID]</p>
      </td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A storage share is defined on zero or more data stores.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>StorageService.ID</p>
        <p>[redefines Service.ID]</p>
      </td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">A storage share participates in a storage service.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">StorageShareCapacity.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A storage share offers zero or more storage share capacities.</td>
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
      <td style="text-align:left">MappingPolicy.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A share has zero or more mapping policies.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>A StorageShare represents a utilization target of one or more storage extents with a set of policies which are homogeneous. If many UserDomains are mapped to a StorageShare via a MappingPolicy, then they are assumed to be able to use the Share uniformly. A StorageShare MAY have many types of Storage Capacity. The usage of each type of Storage Capacity is described by the StorageShareCapacity class.

### StorageShareCapacity

The StorageShareCapacity class provides a set of attributes related to the size of the data storage extents associated with a StorageShare. One StorageShare MAY have several associated StorageShareCapacity objects of different types, which may be related either to the physical nature of the storage medium or to the intended use, e.g. accounting or resource discovery. It is therefore possible that the same physical storage MAY be reported in more than one object. The size information generally relates to the values as seen by a user of the Service, which may not correspond directly to the size of the physical storage media which underlie it. For example, disk servers may include parity disks or hot spares which are not directly visible to users.

The semantics of this class are the same as the StorageServiceCapacity class which represent the size of the entire StorageService, but the classes are different since the relations are different. In general it cannot be assumed that the StorageServiceCapacity is the sum of all the corresponding StorageShareCapacities, both because some information at the Share level MAY not be published, and because multiple StorageShare objects MAY share the same physical storage. There may also be differences in timing or accuracy in the underlying services which collect the information.

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
      <td style="text-align:left">StorageShareCapacity</td>
      <td style="text-align:left">Entity</td>
      <td style="text-align:left">A description of the size and usage of a homogenous storage extent available
        to a Storage Share.</td>
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
      <td style="text-align:left">StorageCapacity_t</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The type of storage capacity.</td>
    </tr>
    <tr>
      <td style="text-align:left">TotalSize</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">GB</td>
      <td style="text-align:left">The total amount of storage of this Type (the sum of free, used and reserved).</td>
    </tr>
    <tr>
      <td style="text-align:left">FreeSize</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">GB</td>
      <td style="text-align:left">The amount of storage which is free for new data to be stored. This SHOULD
        include space occupied by cached copies of objects which can be deleted
        automatically to make room for new ones.</td>
    </tr>
    <tr>
      <td style="text-align:left">UsedSize</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">GB</td>
      <td style="text-align:left">The amount of storage which is occupied by stored data. This SHOULD exclude
        space occupied by cached copies of objects which can be deleted automatically
        to make room for new ones.</td>
    </tr>
    <tr>
      <td style="text-align:left">ReservedSize</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">GB</td>
      <td style="text-align:left">The amount of storage which is not occupied by stored data, but has been
        reserved for use by a specific user or group, and hence is not free for
        the storage of new data except in the context of that reservation.</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left">Mult.</td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">StorageShare.ID</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">A storage share capacity is related to one storage share.</td>
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
</table>The StorageShareCapacity is useful to express the usage information of a homogenous storage extent allocated to a Share. Such usage information refers to use by the UserDomains which are related to the StorageShare via MappingPolicies.

### StorageManager

The StorageManager class represents the software system which manages the data storage media. If different media, e.g. tape and disk, are managed by different software systems there MAY be multiple StorageManager instances for a single StorageService. In some systems there may be a number of layers of software, but this cannot be represented. At present no attributes are defined beyond those inherited from the Manager entity, i.e. the Name and Version of the software product.

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
      <td style="text-align:left">StorageManager</td>
      <td style="text-align:left">Manager</td>
      <td style="text-align:left">The primary software component locally managing one or more Data Stores.
        It MAY also be used to describe aggregated information about the managed
        resources.</td>
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
      <td style="text-align:left"><em>No extra properties are defined in the specialized entity.</em>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
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
        <p>StorageService.ID</p>
        <p>[redefines Service.ID]</p>
      </td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">A storage manager participates in a storage service.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>DataStore.ID</p>
        <p>[redefines Resource.ID]</p>
      </td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A storage manager manages zero or more data stores.</td>
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
</table>### DataStore

The DataStore class represents the physical storage systems underlying the StorageService. Typically there will be one DataStore instance for each homogeneous type of storage, e.g. tape and disk. However, multiple objects of the same Type MAY be published if the storage is segmented at a high level, e.g. if there are two separate robotic tape stores. The size information relates to the physical capacity of the storage media, which may differ from the values reported in the Capacity classes.

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
      <td style="text-align:left">DataStore</td>
      <td style="text-align:left">Resource</td>
      <td style="text-align:left">An abstract description of a sufficiently homogeneous storage device providing
        a storage extent, managed by a local software component (Storage Manager),
        part of a Storage Service, reachable via zero or more Endpoints and having
        zero or more Shares defined on it. A Data Store refers to a category of
        storage with summary information on the storage capacity.</td>
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
      <td style="text-align:left">Type</td>
      <td style="text-align:left">DataStoreType_t</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The type of storage medium.</td>
    </tr>
    <tr>
      <td style="text-align:left">Latency</td>
      <td style="text-align:left">AccessLatency_t</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The actual latency category under normal operating conditions for a data
        object stored in this Data Store.</td>
    </tr>
    <tr>
      <td style="text-align:left">TotalSize</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">GB</td>
      <td style="text-align:left">The total size of the storage extent within the Data Store (free plus
        used).</td>
    </tr>
    <tr>
      <td style="text-align:left">FreeSize</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">GB</td>
      <td style="text-align:left">The amount of storage which is not currently occupied by stored data.</td>
    </tr>
    <tr>
      <td style="text-align:left">UsedSize</td>
      <td style="text-align:left">UInt64</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">GB</td>
      <td style="text-align:left">The amount of storage which is currently occupied by stored data.</td>
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
        <p>StorageManager.ID</p>
        <p>[redefines Manager.ID]</p>
      </td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">A data store is managed by a storage manager.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>StorageShare.ID</p>
        <p>[redefines Share.ID]</p>
      </td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">A data store provides capacity in terms of zero or more storage shares.</td>
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
</table>### ToComputingService

The ToComputingService class describes a network connection between a StorageService and a ComputingService which has a level of performance significantly better than the general WAN connection. It is assumed that such a connection applies to the entirety of those Services, i.e. to all Worker Nodes within the ComputingService and all storage within the StorageService. However, the connection MAY depend on the Access Protocol used to transfer the data. Some Access Protocols may only be available from a restricted set of Computing Services, and this may also be published using the ToComputingService class.

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
      <td style="text-align:left">ToComputingService</td>
      <td style="text-align:left">Entity</td>
      <td style="text-align:left">A description of the network link quality between a Storage Service and
        a computing service, and/or of a potentially dedicated access protocol
        that the Computing Service may use to access the Storage Service.</td>
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
      <td style="text-align:left">NetworkInfo</td>
      <td style="text-align:left">NetworkInfo_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The type of network connection available between the Storage Service and
        Computing Service.</td>
    </tr>
    <tr>
      <td style="text-align:left">Bandwidth</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">Mb/s</td>
      <td style="text-align:left">The nominal bandwidth available between the Storage Service and Computing
        Service via this connection.</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">StorageAccessProtocol.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">The storage service MAY be accessed via an access protocol by a certain
        computing service.</td>
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
</table>### ToCloudComputingService

The ToCloudComputingService class describes a network connection between a Storage Service and a Cloud Computing Service which has a level of performance significantly better than the general WAN connection. It is assumed that such a connection applies to the entirety of those Services, i.e. to all Virtual machines within the Cloud Computing Service and all storage objects within the Cloud Storage Service. However, the connection MAY depend on the Access Protocol used to transfer the data and to restrictions in data access to the data itself. Some Access Protocols may only be available from a restricted set of Compute Services, and this may also be published using the ToCloudComputingService class.

It is important to note that this entity applies only to a CloudStorageService which relates to a given CloudComputingService \(ex. to provide Block Storage to VMs of an IaaS service\), not to generic Cloud Storage service such as Object Storage.

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
      <td style="text-align:left">ToCloudComputingService</td>
      <td style="text-align:left">Entity</td>
      <td style="text-align:left">A description of the network link quality between a Storage Service and
        a computing service, and/or of a potentially dedicated access protocol
        that the Computing Service may use to access the Storage Service.</td>
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
      <td style="text-align:left">NetworkInfo</td>
      <td style="text-align:left">NetworkInfo_t</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The type of network connection available between the Storage Service and
        Compute Service.</td>
    </tr>
    <tr>
      <td style="text-align:left">Bandwidth</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">0..1</td>
      <td style="text-align:left">Mb/s</td>
      <td style="text-align:left">The nominal bandwidth available between the Storage Service and Compute
        Service via this connection.</td>
    </tr>
    <tr>
      <td style="text-align:left">Association End</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Description</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">StorageAccessProtocol.ID</td>
      <td style="text-align:left">*</td>
      <td style="text-align:left">The storage service MAY be accessed via an access protocol by a certain
        computing service.</td>
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
</table>## 

