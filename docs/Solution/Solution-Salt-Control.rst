.. _Solution-Salt-Control:

Solution Salt Stack Control
===========================
The Edgeville reference architecture represents an Edge to Cloud distributed computing platform that can scale to millions
of edge devices or nodes. This architecture shows the use cases, and specs for implementing the Edgeville Architecture.
The architecture is broken up into several different components and sections. The system connects edge devices and data centers
together across three different aspects: Security, Control, and Cloud Applications.

This Reference Architecture focuses on Salt Stack as the control, Telemtry, and Security Layers of the solution.

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

High Level Architecture
-----------------------

The Edgeville Architecture contains several subsystems and components. The following is a diagram on
how these components work together to fulfill the high level use cases.

* :ref:`SubSystem-Cloud` - contains all of the Subsystems for the cloud: :ref:`SubSystem-Cloud/SDI` , :ref:`SubSystem-Cloud/uSDI`, :ref:`SubSystem-Cloud/Common-Cloud-Core` responsible for application and service management.
* :ref:`SubSystem-Control` - contains all of the Subsystems for the control of the edge devices: :ref:`SubSystem-Control/Data-Coordinator`, :ref:`SubSystem-Control/Edgeville-Agent`, :ref:`SubSystem-Control/Edgeville-Manager`.
* :ref:`SubSystem-Control/Security` - contains all of the Subsystems for the security of the edge and data centers: :ref:`SubSystem-Security/Encryption`, :ref:`SubSystem-Security/Identity-Manager`, :ref:`SubSystem-Security/Trust-Manager`
* :ref:`SubSystem-Control/Telemetry` - contains all of Telemety Bus from multiple clouds, services and application stacks: :ref:`SubSystem-Telemetry/Telemetry-Aggregator`, :ref:`Subsystem-Telemetry/Telemetry-Bus`,  :ref:`Subsystem-Telemetry/Telemetry-Producer`,  :ref:`Subsystem-Telemetry/Telemetry-Subscriber`

.. image:: HighLevelLogical.png

The Edgeville architecture has two aspects: Control and Cloud. The Control layer contains the Control, Security, and Telemetry. The Cloud layer contains Common Cloud Core, SDI and uSDI.

Control Layer
-------------

The Control Layer can be implemented using Salt Stack. The following mappings can be made.

* :ref:`SubSystem-Control/Edgeville-Manager` is equivlant to Salt Master or Syndicate
* :ref:`SubSystem-Control/Edgeville-Agent` is equivlant to Salt Minon
* :ref:`SubSystem-Control/Data-Coordinator` is equivlant to Salt Pillars
* :ref:`SubSystem-Control/Telemetry` is equivlant to Salt Grains and Salt States.

Key management should be done when the salt minon is install on the edge device. Keys should be generated and used for
the registration process.

.. image:: Salt-Logical.png

Cloud Architecture
------------------

The Cloud Layer consists of Common Cloud Cores, SDI, and uSDI SubSystems.
Salt does not have the SDI layer. But it might be able to be used for the uSDI layer if just basic work needs
to be done. Still investigating the funcitonality at this time *Sept 8, 2018*

.. image:: Salt-LogicalCloud.png

* :ref:`SubSystem-Cloud/Common-Cloud-Core` - Common Cloud Core orchestrates services across multiple clouds, basically instatiating a multi-cloud. It is responsible application and service orchestration.
* :ref:`SubSystem-Cloud/SDI` - This is a typical Private Cloud Interface. Responsible for orchesrating Infrastructure in the cloud.
* :ref:`SubSystem-Cloud/uSDI` - This is a micro-cloud interface. Responsible for orchestrating infrastructure in the micro-cloud.

Deployment model
----------------

The architecture consists of deploying Salt Stack on  the system.
On the Data Center the Salt Master will be installed.
On the Aggregated Edge Device the Salt Master and Salt Minon will be installed.
On the Edge Device the Salt Minon will be installed.

.. image:: Salt-Deployment.png

Physical Architecture
---------------------

This is the physical layout of micro-services on the nodes in a Cloud or multiple Clouds. Including interface and connections between the different components.

.. image:: Physical.png


Process Architecture
--------------------

The subsystems of Edgeville request information from each other to accomplish the use cases of the system.
This diagram shows how these microservices are connected and what they share between each other.
Creating Trusted edge devices and aggregated edge devices are in important aspect of the architecture.
As each Edge Device is brought up it follows the Security Chain of Trust protocol described in the :ref:`SubSystem-Control/Security`
sub-system. When an Edge Device is attested it notifies its Edgeville Manager (Aggregated Edge Device or Data Center) that it
is available. When and Edgeville Manager is notified of its children's availability it notifies its parent Edge Manager
if one exists until the complete ecosystem is brought up.

.. image:: Process.png

