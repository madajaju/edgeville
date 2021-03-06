.. _Home:

Edgeville Overview
==================

The Edgeville conceptual architecture represents an Edge to Cloud distributed computing platform that can scale to millions
of edge devices or nodes. This architecture shows the use cases, and specs for implementing the Edgeville Architecture.
The architecture is broken up into several different components and sections. The system connects edge devices and data centers
together across three different aspects: Security, Control, and Cloud Applications.

High Level Use Cases
--------------------

* :ref:`UseCase-Manage-Applications`
* :ref:`UseCase-Manage-Cloud`
* :ref:`UseCase-Manage-Security`
* :ref:`UseCase-Manage-Infrastructure`

.. image:: /UseCases/UseCases.png

Users
-----

* :ref:`Actor-Application-Developer`
* :ref:`Actor-Dev-Ops`
* :ref:`Actor-Network-Engineer`
* :ref:`Actor-Operations-Manager`
* :ref:`Actor-Security-Engineer`

High Level Concepts
-------------------

* **Aggregated Edge Device** - This is an Edge Device that has other Edge Devices that it controls. The Aggregated Edge Device gives the ability to create topologies of control.
* **Edge Device** - This is a device contains Compute, storage and network sufficient to manage and control any number of devices or IOT Gateways.
* **IOT Gateway** - Controls multiple IOT Devices. Provides control and data from the IOT Devices to an Edge Device.
* **IOT Device** - This can be a Seonsor, Camera, etc.
* **Private Cloud** - A Cloud that is not shared outside of the owner of the Cloud. In this case it is owned by the Teleco and does not supply anything to a customer.
* **Shared Cloud** - A Cloud that a teleco can land services for a customer. The Shared cloud is multi-tenent and gives the Teleco the ability monetize their infrastructure.
* **SDI** - Software Definied Infrastructure. This is the base foundation to a Cloud. This provides a common API to the Cloud layers.
* **uSDI** - This is an SDI layer for a micro-cloud. the micro-cloud is the smallest possible layer for a cloud. Every Edge Device has a micro-cloud instance in it.
* **Common Cloud Core** - This is a true Multi-Cloud. It connects multiple clouds together to behave like one cloud. See the `C3 architecture <http://c3.readthedocs.io>`_ for details.

.. image:: HighLevel.png

Layered Architecture
--------------------

**Application Layer** - Applications are developed to run across the ecosystem.
**Cloud Layer** - Cloud Layer includes Multi-Cloud, Cloud and Micro-Clouds
**Control Layer** - Control Layer includes Security Telemetry and Data Control subsystems
**Physical Layer** - Physical hardware includes Data Center, Edge Devices, and Devices

.. image:: Architecture.png

Topologies
----------
The architecture is divided into Control and Cloud. The Control layer establishes a topology for controlling the phsyical edge devices, data centers, and IOT Gateways.
The control layer establishes topologies so the devices can be managed in a reasonable manner and can scale beyond the normal capabilities of a completely flat control plane.

.. image:: ControlTopologies.png

In this example the "Data Center 2" controls the "Edge Device 2*". There is also an Aggregated Edge Device, "Aggregated Edge Device 31", that is the parent of the "Edge Devices 31*".
The Parent Child relationship shows that layers of control can be established. Different control toplogies can be established to give the ability to create extermely large networks
of Edge Devices and Data Centers.

The control topology is only one of the topologies that can be created. Edge Devices and Data Centers can be organized as a graph of clouds as well. This gives the ability to dynamically
create cloud topologies based on the applications or workflows being deployed on the ecosystem. In this example color is used to show how the Control topology can be independent of the
cloud topology.

.. image:: CloudTopologies.png

Notice that a Control parent-child relationship does not pre-determine the parent-child relationship in a Cloud Topology.

Logical Architecture
--------------------

The Edgeville Architecture contains several subsystems and components. The following is a diagram on
how these components work together to fulfill the high level use cases.

* :ref:`SubSystem-Application` - contains all of the Subsystems for the application layer:

  * :ref:`SubSystem-Application/Analytics` - Generalized Analytics workload
  * :ref:`SubSystem-Application/Services` - Services that provide capabilities to all applications and workloads.
  * :ref:`SubSystem-Application/Workloads` - Workload connects applications, and services together.

* :ref:`SubSystem-Cloud` - contains all of the Subsystems for the cloud:

  * :ref:`SubSystem-Cloud/SDI` - Interface for Private and Public Clouds.
  * :ref:`SubSystem-Cloud/uSDI` - Interface to micro-Clouds
  * :ref:`SubSystem-Cloud/Common-Cloud-Core` - Interface to Hybrid/Multi Cloud.

* :ref:`SubSystem-Control` - contains all of the Subsystems for the control of the edge devices:

  * :ref:`SubSystem-Control/Data-Coordinator` - Coordinates data between the different devices.
  * :ref:`SubSystem-Control/Edgeville-Agent` - process running on the Edge Device and Aggregated Edge Device to manage control of the device.
  * :ref:`SubSystem-Control/Edgeville-Manager`- process running on the Data Center and Aggregated Edge Device to manage control of its children devices.

* :ref:`SubSystem-Physical` - contains all of the physical devices in the system.

.. image:: Solution/HighLevelLogical.png

