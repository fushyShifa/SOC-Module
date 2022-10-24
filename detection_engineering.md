# SOC detection engineering and management

This page deals with SOC detection engineering and management (detection use case creation, detection capabilities assessment, etc.)

# TOC

* Must read
* Generic recommended approach
* PDCA applied to SOC
* How to feed the Plan phase (detection engineering)


# Must read
* MITRE, [top TTP for ransomwares](https://top-attack-techniques.mitre-engenuity.org/)
* LinkedIn, [Risk assessment with ISO 27005](https://www.linkedin.com/pulse/iso-27005-risk-management-aron-lange/?trackingId=oRjjiIdY9BNjne1ALRq02A%3D%3D)
* Ch33r10, [Enterprise purple teaming](https://github.com/ch33r10/EnterprisePurpleTeaming)
* SIEM rules publications:
  * [Sigma HQ (detection rules)](https://github.com/SigmaHQ/sigma/tree/master/rules) 
  * [Splunk Security content (free detection rules for Splunk)](https://research.splunk.com/) 
  * [Michel De Crevoisier's Git](https://github.com/mdecrevoisier/SIGMA-detection-rules)
* Known exploited vulnerabilities: 
  * [CISA catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog)
* Medium, ["About detection engineering"](https://cyb3rops.medium.com/about-detection-engineering-44d39e0755f0)
* ANSSI (FR), [EBIOS RM methodology](https://www.ssi.gouv.fr/guide/ebios-risk-manager-the-method/)


# Generic recommended approach

## PDCA multi-loop:

As per [Wikipedia](https://en.wikipedia.org/wiki/PDCA#/media/File:PDCA-Multi-Loop.png)
![image](https://user-images.githubusercontent.com/16035152/197550801-47f57a99-8d3b-45b1-9c97-be4355a4d9f0.png)



# PDCA being applied to SOC

## Plan:

### Sensors:
* Determine which sensors or endpoint/app logs, you miss in terms of detection capabilities
* Determine how to generate and ingest their logs in the SIEM
* Build a projet agenda

### SIEM rules:
* Determine which detection logic you miss, directly in the SIEM;
* Build a project agenda.


## Do:

### Sensors:
* Ingest the logs of the security sensor, or endpoint/app logs, that you previously identified;
* Make sure your data ingestion is compliant with the datamodel you use.

### SIEM rules:
* Create the detection rules (SIEM searches) that match your previously identified needs;
* Create the alert objects in the SIEM or SIRP, to contain the contents of the SIEM searches in case something is found.

### Procedure:
* If it does not exist already, create the handling procedure for the newly created detection rule.


## Check:

### Logs:
* Make sure your data ingestion is compliant with the datamodel you use (or, at least, the SIEM one).

### Handling procedures:
* Make sure that the handling process and procedures is clear and working fine, for the tested alerts.

### Automations:
* Make sure that the automations capabilities to help in the detection phase, work as expected (ie.: observables enrichment in the SIRP with queries to the TIP).

### SIEM rules [first run for the assessed detection capabilities]:
* Test the detection logics with narrowed use cases (specific events, generated on demand).

### SIEM rules [following runs for the assessed detection capabilities]
* Assess your detection capabilities with purpleteaming;
* Report your results and findings in purpose-built app like Vectr.

## Act:
* Fix everything that was previously identified as not working, or not matching your needs.


# How to feed the "Plan" phase

## Standard maturity and needs:

### TTP detection priorities identification:
* Use [MITRE Engenuity calculator](https://ctid.mitre-engenuity.org/our-work/top-attack-techniques/):
  * focus on the [top TTP for ransomwares](https://top-attack-techniques.mitre-engenuity.org/): 
    * T1486: Data Encrypted for Impact, T1490: Inhibit System Recovery, T1027: Obfuscated Files or Information, T1047: Windows Management Instrumentation, T1036: Masquerading, T1059: Command and Scripting Interpreter, T1562: Impair Defenses, T1112: Modify Registry, T1204: User Execution, T1055: Process Injection.
* Leverage daily watch to maintain your knowledge about current most commonly used TTP
  * for instance: [Recorded Future 2021 top TTP report](https://www.recordedfuture.com/2021-malware-and-ttp-threat-landscape)

### Focus on top relevant vulnerabilities:
- that are confirmed commonly exploited in the wild;
- **AND** that are confirmed as valid (unpatched) within your organization.

My recommendation, still, is to make sure not to spend all you time running after latest 0days, as it is time consuming and not that efficient in the end in terms of working SOC detection capabilities.


## Advanced maturity and needs:

### Define your needs and the SOC priorities:

* Leverage a risk management-based approach, to determiner:
  * threat actors (if possible);
  * critical assets;
  * attack scenarios (somewhat, kill chains).

Here is a [simplified drawing](https://www.linkedin.com/pulse/iso-27005-risk-management-aron-lange/?trackingId=oRjjiIdY9BNjne1ALRq02A%3D%3D) of the global process, leveraging ISO 27005 approach:
![image](https://user-images.githubusercontent.com/16035152/197557946-7bc27c7a-6aee-48f4-a013-2ac20d6b5c76.png)

My recommendation is to follow the [EBIOS RM methodology](https://www.ssi.gouv.fr/guide/ebios-risk-manager-the-method/), from French ANSSI. The fourth workshop will aim at defining the "offensive scenarios" that are relevant for the environment for which you are running the risk management methodology. Those offensive scenarios should be considered as TTP (even if they are not directly referenced in MITRE ATT&CK Enterprise matrix), to be monitored by the OC.


### Focus your SOC detection engineering taskforce on priorities:

* Set as priority the detection of confirmed attack scenarios (and the corresponding TTP), as per risk management analysis.

