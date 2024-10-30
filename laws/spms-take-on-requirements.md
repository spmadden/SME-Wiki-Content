---
title: SPM's Take on System Requirements
description: 
published: 1
date: 2024-10-30T21:02:58.669Z
tags: 
editor: markdown
dateCreated: 2024-10-30T20:29:00.406Z
---

Have you considered everything here?  (In no particular order)

## Facilities Requirements:

* Space Requirements:
  * Physical Space and Layout
  * Storage of Spares and Consumables
  * Weight and dimensions of each individual element
* Utility Requirements:
  * Electrical Input Requirements
  * Cooling Requirements
  * Gas or other fueling requirements

* Maintenance Requirements
* Support Equipment Requirements
* Environmental Requirements (any HAZMAT?) for storage and transport
* Any special certifications or trainings required?
* Equipment check-out or calibration services?
* Housekeeping services?
* Emergency services?
* Recovery services of damaged components?


## Interfaces (Human and Automaton) & I/O Requirements: 

* Priority the interfacing entities must assign the interface?
* Requirements on the type of interface (such as real-time data transfer, storage-and-retrieval of data, etc.) to be implemented?
* Required characteristics of individual data elements that the interfacing entities must provide, store, send, access receive, etc. Such as:
  * Data Type (alphanumeric, integer, float32, Q3.12, etc.)
  * Size and format (such as length and punctuation of a character string, width of a binary type, etc.)
  * Units of measurement (such as meters, dollars, nanoseconds, dB, etc.)
  * Range or enumeration of possible values (such as 0-99)
  * Accuracy (how correct), precision (number of significant digits), reference frame or bias (what does ‘zero’ mean?), and resolution (Units per Sample)
    * ie: This ADC returns a 16 bit signed integer value in the range [-32768, 32767], each value represents 5mV with an accuracy of +/- 2.5mV.  -32768 represents -10V and 32767 represents +10V.
  * Priority, timing, frequency, volume, sequencing, and other constraints, such as whether the data element may be updated and whether business rules apply.
  * Security and Privacy constraints
  * Sources (setting/sending entities) and recipients (using/receiving entities)

* Required characteristics of data element assemblies that the interfacing entities must operate on:
  * (Data element assemblies can include records, messages, files, arrays, displays, reports, etc.)
  * (Operations can include provide, store, send, access, retrieve, create, delete, etc.)
  * Define the data elements and their structure (number, order, grouping, etc.)
  * Define the media (such as disk) and structure of the data elements on the medium
  * Visual and auditory characteristics of displays and other outputs (such as colors, layouts, fonts, icons, and other display elements, beeps, lights, etc.)
  * Relationships among assemblies, such as sorting/access characteristics
  * Priority, timing, frequency, volume, sequencing, and other constraints such as whether the assembly may be updated and whether business rules apply
  * Security and privacy constraints
  * Sources (setting/sending entities) and recipients (using/receiving entities)

* Required characteristics of communication methods that the interfacing entities must use for the interface, such as:
  * Project-unique identifier(s)
  * Communication links/bands/frequencies/media and their characteristics
  * Message formatting
  * Flow control (such as sequence numbering and buffer allocation)
  * Data transfer rate, whether periodic/aperiodic, and interval between transfers
  * Routing, addressing, and naming conventions
  * Transmission services, including priority and grade
  * Safety/security/privacy considerations, such as encryption, user authentication, compartmentalization, and auditing

* Required characteristics of protocols the underlying interfacing entity(ies) must use for the interface, such as:
  * Project-unique identifier(s)
  * Priority/layer of the protocol
  * Packetization, including fragmentation and reassembly, routing and addressing
  * Legality checks, error control, and recovery procedures
  * Synchronization, including connection establishment, maintenance, termination
  * Status, identification, and any other reporting features

* Other required characteristics, such as:
  * Physical compatibility of the interfacing entities
    * Dimensions, tolerances, loads, plug compatibility, etc.
  * Voltages, etc.

## Qualification Requirements:
* For each requirement, how are you actually going to test it, to show that the underlying execution is functionally correct?
* If applicable, the order of precedence, criticality, or assigned weights of requirements
  * Examples include those requirements deemed critical to Safety, Security, or to Privacy for purposes of singling them out for special treatment.
  * If all requirements are of equal weight, state as such.
* Examples of qualification types:
  * Demonstration: The operation of interfacing entities that relies on functional operation not requiring the use of instrumentation, special test equipment, or subsequent analysis
  * Test: The operation of interfacing entities using instrumentation or special test equipment to collect data for later analysis
  * Analysis: The processing of accumulated data obtained from other qualification methods.  
  * Inspection: The visual inspection of interfacing entities, documentation, etc.
  * Special qualification methods: Any special qualification methods for the interfacing entities, such as special tools, techniques, procedures, facilities, and acceptance limits.

## Metrics Descriptions:

* Provide insight into the metrics selected, rationale for choosing the metrics, and the costs for collecting & storing the metrics.
* Provide insight into how the data analysis and trends from each metric will support the quantitative engineering management of the effort.
* Overall: 
  * Identify the metrics collection process.  How are metrics collected, the specific tools collecting the metrics, and where the resulting data will be stored.
  * Address how the integrity of the metrics data are maintained to include “chain of custody”
  * Timeliness of delivery of metrics data to stakeholders
* Identify each metric:
  * Identify the rationale for collecting the metric, 
  * What value that particular metric provides
  * The cost for collecting and storing the metric
  * The frequency of collection of the metric
* Analysis Process:
  * Address the analysis process for each metric and the specific tools employed.
  * Will historical data be analyzed?
  * How about trend analysis, or future predictions of problem areas?
  * What are the outputs of the analysis:
    * Format?  Presentation? Media? Delivery Frequency?


## Software/Firmware Resource Requirements:

* Specific requirements under certain conditions:  (best case, average case, worst case, etc.)
* Identify & quantify the unit of measure
  * Processor percent requirement?  Processor MHz assigned?  CPU Units?
  * Memory amount in bytes?
  * Bandwidth in bit/s, etc.
  
* Quantify the scope of the requirement:
  * For example: “This requirement is for 1 MBit/s of network application throughput, and does not consider the overhead of the transport layer, TCP/UDP headers, IP headers, or Ethernet overhead.”
* Quantify the requirement
  * Is it a soft requirement?  Hard requirement?
  * Lower limit?  Upper limit?
  * What are the impacts to the system behavior if this requirement is not met?
* Identify the condition.  Is it typical usage?  Based on certain events happening?
* Processor requirements (clock speed, # of cores, # of CPUs, etc.)
* Memory requirements (amount, clock speed, access time, etc.)
* Buffer requirements (amount, width, overwrite capability, duration, etc.)
* Storage requirements (amount, read speed, write speed, latency, etc.)
* Communications/networking requirements (bandwidth, latency, determinism, reliability, etc.)
* I/O requirements (digital, analog, etc.)
* Any special considerations affecting the utilization
  * Virtual memory, swap space, overlays, etc.
  * Multiprocessors, multithreading, async io, etc.
  * Operating system overhead or other software overhead
* Dependent libraries, tools, installations, operating system, platform, and configurations.

## Security and Privacy

* What security/privacy environment must the component operate in?
* The type and degree of security/privacy the component must provide.
* The security/privacy risks the component must withstand and the required safeguards to reduce those risks
* The security/privacy policy the component must meet.
* The security/privacy auditing/accountability policy the component must meet.
* Any certification/accreditation the component must meet.

## Individual Component Requirements:

* Required Phases, States & Modes:
  * A “State” is a specific, discrete condition that a component may be in - states are generally mutually exclusive.
  * A “Mode” is a specific operating condition for a component - usually commanded by an operator.
  * A “Phase” is a specific operating condition that groups applicable states and modes.
  * Identify each Phase, State, and Mode, and identify the transitions between them
  * examples include: idle, ready, active, post-use analysis, training, degraded, emergency, backup.
  * If there are no required states & modes, state so explicitly.
* Functional Requirements:
  * What are the tasks or functions the component must do?
* Performance Requirements: Describe “the hows” of how the component must operate
  * How well?  How fast?  How reliable?  How accurate?  How performant?  How responsive?
* Behavior Requirements: Describe the required behaviors of the component under varying conditions:
  * Behavior during the “Happy path”
  * Behavior during Unexpected, Unallowed, or “Out of bounds” conditions
  * Fallback behavior during “emergency” states
* External Interface Requirements: See “Interfaces” above
* Internal Interface Requirements: 
  * Requirements for internal data storage formats (databases, files, etc)
  * Requirements for internal communications protocols
* Adaptation Requirements:
  * What (if any) installation-dependent information or operational parameters are required to be configured?

* Safety Requirements:
  * Requirements to minimize unintended hazards to personnel, property, and the physical environment.
  * Requirements for any regulatory or compliance rules.
  * Examples include:
    * Safeguards the component must provide to prevent inadvertent actions (such as accidentally issuing a “cooling OFF” command)
    * Safeguards the component must provide to prevent inadvertent non-actions (such as failure to issue an intended “cooling OFF” command)

* Software Requirements
  * What operating system?  Platform?
  * Does the component require any of (specify details, like version and product identifier):
    * Database management system
    * Communications/network software
    * Utility software
    * Input or equipment simulators
    * Test software
    * Manufacturing software
* Computer Communication Requirements
  * What geographic locations need to be linked?
  * What network topography is required?
  * Transmission techniques?  
  * Data transfer rates?
  * Gateways?
  * Any required system use times?
  * Type and volume of data to be transmitted/received?
  * Time boundaries for transmission/reception/response?  
  * Peak volumes of data?
  * Diagnostic features?
* Quality Factors:
  * Functional Quality: The ability to perform all required functions
  * Reliability: The ability to perform with correct, consistent results
  * Maintainability: The ability to be easily corrected
  * Availability: The ability to be accessed and operated when needed
  * Flexibility: The ability to be easily adapted to changing requirements
  * Portability: the ability to be easily modified for a new environment
  * Reusability: The ability to be used in multiple applications
  * Testability: The ability to be easily and thoroughly tested
  * Usability: The ability to be easily learned and used
  * etc

* Design, Implementation, and Execution constraints
  * Standards to be implemented/abided by
  * Use of or interoperability with existing components
  * Use of a particular data standard
  * Use of a particular programming language
  * Flexibility and Expandability that must be provided to support anticipated areas of growth, or changes in technologies, threats, or objectives

* Personnel Requirements:
  * How many people are required to operate this component?
  * What skills or experience do they need to have?
  * Over what duty cycle are humans expected to operate this?
  * Training Requirements:
    * What classes, courses, certifications are required?
  * Ensure that the capabilities and limitations of humans are considered:
    * Foreseeable human errors under both normal and extreme conditions
    * Specific areas where the effects of human error would be particularly serious
    * Color and duration of error messages
    * Physical placement of critical indicators or keys
    * Auditory signals
    * Specific accessibility attributes for humans with physical and mental disabilities

* Training requirements: 

What training/help/guidance features the component should provide?

What training/certifications/experience should an operator have?

Logistics requirements:

System maintenance needs

Software support needs

System transportation modes & needs

Supply-system requirements

Impact on existing facilities and equipment

Packaging Requirements

Packaging, labeling, and handling requirements for delivery

Operational Requirements:

Define the operational conditions under which the component must function