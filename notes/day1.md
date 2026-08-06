My Notes from https://www.professormesser.com 
Control Catagories

Technical controles
    • controls implemented using systems
    • operating system controls
    • Firewalls and antivirus


Managerial controls
    • Administrative controls associated with security design and implentation
    • Security policies, standard operating procedures

Operational controls
    • Controls implemented by people instead of systems
    • security guards, awareness programs

Physical Controls
    • limit physical access
    • Guard shacks
    • Fences and locks
    • Badge Readers


Control Types

Preventative
    • Block access to a resource
Prevent access by:
    • Firewall rules-technical
    • Follow security policy-Managerial
    • Guard shack checks all identification-Operational
    • Enable door locks-Physical

Deterrent
    • Discourage an intrusion attempt
    • Does not directly prevent access
      Makes an attacker think twice
    • application splash screens- Technical
    • threat of termination or demotion- Managerial
    • Front Receptionist desk - Operational
    • Posted Warning Signs- Physical

Detective-Identify and log an intrusion attempt, may not prevent Access
    • Collect and review system logs-Technical
    • Review Login reports-Managerial
    • Regularly patrol property-Operational
    • enable motion detectors-Physical

Corrective- apply a controle after an event has been detected, reverse the impact of an event, continue operating with minimal downtime
    • Restoring from backups can mitigate ransomware infection-technical
    • Create policies for reporting security issues-managerial
    • Contact law enforcement to manage criminal activity-operational
    • Use a fire extinguisher if electrical fire is started -physical

Compensating-control using other means, Existing controls are not sufficient, May be temporary 
    • Prevent the exploitation weakness by having firewall block a specific application instead of applying patch-technical
    • Implement a separation of duties-managerial
    • Require simultaneous guard duties-operational
    • Generator used after power outage-physical
Directive
    • A directive, not really technically not a control like an advisory on a door but no lock

CIA triad, fundamentals of security, or AIC triad\
C-confidentiality-Prevent disclosure of informatin to unauthorized individuals or systems
I-Integrity-messages can’t be modified without detection
A-Availability- systems and networks must be up and running at all times

Confidentiality
    • Certain information should only be known to certain people-prevent unauthorized information disclosure
    • Encryption- Encode messages so only certain people can read it
    • Access controls- selectively restrict access to a resource 
    • Two factor authentication

Integrity
    • Data is stored and transferred as intended-Any modification to the data would be identified
    • Hashing-map data of an abritrary length to data of fixed length
    • Digital signature-mathematical scheme to verify the integrity of the data
    • Certificates-Combine with digital signature to verify the individual
    • Non-repudiation  - Provide proof of integrity

Availability
    • Information is accessible to authorized users0 always at your fingertips
    • Reduntancy- Build services that will always be available I.e backup  ISP, alternate systems
    • Fault tolerance – system will continue on even when an error occurs I.e if one program or protocol fails the entire system does not shutdown
    • Patching – stability and security holes

Other take aways from today

can use quotes to use the cat command to display contents of file that has spaces in the name like cat "./--spaces in this filename--"
can display dashname file contents by using cat <- or cat ./-
Can use command find to list hidden files by leaving nothing after the command and just type find


Learned that llm large language models  like llama 2.5 70b is created by compressing large chunks of scrapped off the internet i.e about 10tb and compressed into a nuerobrain.
Not very useful tool as is, Has to be be fine tuned with datasets collected on specific or broad information in order to become an assistant model. Done by providing a question and a corresponding answer from human input with correct information on how it should be provided.

