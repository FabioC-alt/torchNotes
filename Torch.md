# Design Principles
The Torch design assumes that the user know well the application structure and designed it with an fundamental independent principle with respect to the cloud environment on which is run.
Also the design second design principle assumes that the workflow and the actual execution must be separated.

# Architecture
![[Pasted image 20250410152331.png]]

The provisioning process is composed by three distinct sequential phases.

## Application Specification

Composed by two components:
- The Dashboard
- The Tosca Modeller

### The Dashboard
The dashboard is the front-end component implementing the interaction with the Customer and showing the process status.

### Tosca Modeller
The Tosca Modeller guides the Customer to sketch the applications requirements.

## Orchestration Layer
Populated using the **Tosca Processor Component**.
The Tosca processor component is in charge of validating, parsing and converting Tosca applications scenarios into BPMN data inputs and the engine, responsible for instantiating and orchestrating BPMN plans.

## Service Binding Layer
This layer is in charge of creating and managing all the interactions between the provisioning task and the provisioning services.

# Application Specification Layer
The Application layer is tought to be cloud and platform agnostic.

![[Pasted image 20250410162455.png]]
In TORCH each or multiple application is represented as Deployment Unit.
A DU establish a common representation for deployable entities across different container cluster technologies. 
## Container:Runtime
The Container:Runtime represents the **software components or the environment that runs the containers**.
An example is a Docker engine or a Kubernetes node where containers are executed. It is the platform that actually *hosts* the application container.
## Container:Applications
Describes the **actual containerized application**. The units of software that runs *inside* the container.
An example can be a WordPress Instance or a MySQL database container.

Usually there is one or more Container:Applications that runs on a hosted Container:Runtime.
The join of the two form a **Deployment Unit**.

Using the two components joined creates a **clean, standardized and portable application.**

# Orchestration Layer
The TOSCA processor allows to convert TOSCA YAML templates into BPMN data inputs to configure pre-modelled BPMN models that the BPMN engine executes.


## Tosca Processor
Reads and validates the user's YAML application Template. Then converts the parsed inputs in BPMN Worflow, which is a diagram for automation.
It extracts the informations like the deployment order, dependencies properties of each container.

## BPMN Engine
Takes the data from TOSCA processors and executes a **pre-designed workflow**. This workflow automates the deployment of applications components, handles failures, retries and escalations.

## Process Creation
![[Pasted image 20250410174155.png]]
The begin of the process creation is based upon the previous steps.
Each node is instanciated whit a "Instanciate Node" procedure.

Then based on the Node that the TOSCA YAML required is possible to proceed with three different sub-process scenario.

If an error is detected during one of this three sub-process an escalation is thrown by the relative "escalation and event".

### Create Cloud Resource
### Create Deployment Unit
### Create Deploy Package
