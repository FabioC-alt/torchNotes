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


