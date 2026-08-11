# Professor Messer — CompTIA Security+ (SY0-701) Study Notes

My running notes as I work through Professor Messer's free Security+ course.
**Domain 1 — General Security Concepts** (in progress).

---

## Security Control Categories

**Technical controls** — implemented using systems
- Operating system controls
- Firewalls and antivirus

**Managerial controls** — administrative, tied to security design and implementation
- Security policies, standard operating procedures

**Operational controls** — implemented by people instead of systems
- Security guards, awareness programs

**Physical controls** — limit physical access
- Guard shacks, fences and locks, badge readers

---

## Security Control Types

**Preventive** — block access to a resource
- Firewall rules (technical)
- Follow security policy (managerial)
- Guard shack checks identification (operational)
- Door locks (physical)

**Deterrent** — discourage an intrusion attempt (doesn't directly prevent access; makes an attacker think twice)
- Application splash screens (technical)
- Threat of termination or demotion (managerial)
- Front reception desk (operational)
- Posted warning signs (physical)

**Detective** — identify and log an intrusion attempt (may not prevent access)
- Collect and review system logs (technical)
- Review login reports (managerial)
- Regularly patrol property (operational)
- Motion detectors (physical)

**Corrective** — applied after an event is detected; reverse the impact and keep operating with minimal downtime
- Restore from backups to mitigate ransomware (technical)
- Create policies for reporting security issues (managerial)
- Contact law enforcement (operational)
- Fire extinguisher on an electrical fire (physical)

**Compensating** — control by other means when existing controls aren't sufficient (may be temporary)
- Block an app at the firewall instead of patching (technical)
- Separation of duties (managerial)
- Require simultaneous guard duties (operational)
- Generator after a power outage (physical)

**Directive** — an advisory rather than an enforced control (e.g., a sign on a door with no lock)

---

## The CIA Triad
The fundamentals of security (also called the AIC triad).

**Confidentiality** — prevent disclosure of information to unauthorized individuals or systems
- Encryption — encode messages so only certain people can read them
- Access controls — selectively restrict access to a resource
- Two-factor authentication

**Integrity** — data is stored and transferred as intended; any modification is detectable
- Hashing — map data of arbitrary length to a fixed-length value
- Digital signature — verify the integrity of the data
- Certificates — combined with a digital signature to verify the individual
- Non-repudiation — provide proof of integrity

**Availability** — information is accessible to authorized users when needed
- Redundancy — build services that stay available (e.g., backup ISP, alternate systems)
- Fault tolerance — the system continues even when a component fails
- Patching — stability and closing security holes

**Non-repudiation** — proof that data hasn't changed and that it came from a specific source
- A hash represents data as a short string (a "message digest" / fingerprint); if the data changes, the hash changes
- A digital signature adds proof of origin

---

## AAA — Authentication, Authorization, and Accounting

- **Identification** — who you claim to be (e.g., username / email)
- **Authentication** — prove you are who you say you are (password + other factors, e.g., a text code or hardware token)
- **Authorization** — based on identification + authentication, what access you have
- **Accounting** — what gets recorded: login time, data sent/received, logout time

**Authentication in practice** — often done with a certificate placed on the system by an administrator. The certificate is created by the company's **CA (Certificate Authority)** — a system that issues a certificate for a device with a digital signature.

---

## Gap Analysis
Comparing where you are vs. where you want to be (knowledge, data, skills, or system security).

- **The comparison** — evaluate existing systems
- **Identify weaknesses** — and the most effective processes
- **Detailed analysis** — examine broad security categories, then break them into smaller segments
- **Final comparison** — detailed baseline objectives and a clear view of the current state
- **Path to the goal** — almost always involves time, money, and change control
- **Gap analysis report** — a formal description of the current state plus recommendations for meeting the baseline

---

## Zero Trust
A holistic approach — many networks are open on the inside; once you're past the firewall there are few controls. Zero Trust covers every device, process, and person. Nothing is trusted; everything is verified (MFA, encryption, permissions, additional firewalls, monitoring and analysis).

Split the data into functional planes (applies to physical, virtual, and cloud):

**Data plane** — processes the frames, packets, and network data (forwarding, trunking, encrypting, NAT)

**Control plane** — manages the actions of the data plane
- Defines policies and rules
- Determines how packets are forwarded
- Routing tables, session tables, NAT tables

**Adaptive identity** — consider the source and the requested resource
- Multiple risk indicators (relationship to the org, physical location, connection type, IP address)
- Make authentication stronger when needed

**Threat scope reduction** — decrease the number of possible entry points (e.g., access only from within the building or over the company VPN)

**Policy-driven access control** — combine adaptive identity with a predefined set of rules

**Security zones** — broad categories that provide a foundation (where you're coming from, where you're going)
- Trusted / untrusted; internal / external; separate VPNs per service or group; groups like Marketing, IT, Accounting, HR
- Zones alone may be enough to deny access (e.g., untrusted → trusted)

**Policy Enforcement Point (PEP)** — the gatekeeper
- Subjects and systems: end users, applications, non-human entities
- Allows, monitors, and terminates connections; can be multiple components working together

---

## Physical Security
Prevent access (with limits). Channel people through a specific access point; identify safety concerns and prevent injuries. Can be taken to an extreme (concrete barriers/bollards, moats).

**Access control vestibules**
- All doors normally unlocked — opening one locks the others
- All doors normally locked — unlocking one prevents others from unlocking
- One open / others locked
- One at a time — managed control through an area

**Other measures**
- Build a perimeter (usually very obvious)
- Video surveillance — CCTV can replace physical guards
- Security guards

---

## Deception & Disruption

**Honeypots**
- Attract attackers and trap them there
- The "attacker" is often just a machine — makes for interesting recon
- Create a virtual world to explore; a constant battle to tell real from fake

**Honeynets**
- A real network has more than one device (servers, workstations, routers, switches, firewalls)
- Build a larger deception network with one or more honeypots

*attract the attackers with more honey
- Create files with fake information.
- something bright and shiny.

**Honeyfiles**
- Bait for the honeynet(passwords.txt)
- Add many honeyfiles to file shares.

* An alert is sent if the file accessed
- A virtual bear trap.

* Track the malicious actors
- Add some traceable data to the honeynet
- If the data is stolen, you'll know where it came from.

* API credentials
- Does not actually provide access.
- Notifications are sent when used

* Fake email addresses
- Add it to a contact list, add and remove as

* other honeytoken examples
- Database records, browser cookies web page pics


**Change management**
- How to make a change
Upgrade software, patch an application, change firewall configuration, modify switch ports.

- One of the most common risks in the enterprise
Occurs very frequently

- Often overlooked or ignored
Did you feel that bite?

- Have clear policies
Frequency, duration, installation process, rollback procedures

- Sometimes extremely difficult 
Its hard to change corporate culture

* A formal process for managing a change
- avoid downtime , confusion, and mistakes

* A typical approval process
- Complete the request forms
- Determine the purpose of the change
- Identify the scope of the change
- Schedule a date and the time of the change
- Determine affected systems and the impact
- Analyze the risk associated with the change
- Get approval from the change control board
- Get end user feedback

* An individual or entity needs to make a change
- They own the process
- They don't (usually) perform the actual change

* The owner manages the process
- Process updates are provided to the owner.
- Ensures the process is followed and acceptable 

* address label printers need to be upgraded 
- shipping and receiving department owns the process
- IT handles the change

Stakeholders

* who is impacted by the change
- They'll want to have input on the change management process

* This may not be as obvious as you may think
- A single change can include one individual or the entire company

* Upgrade software used by shipping labels
- Shipping / Receiving 
- Accounting reports
- Product Delivery timeframes
- Revenue recognition - CEO visibility

* Determine a risk value
- i.e high, medium, or low

* The risks can be minor or far reaching
- The "fix" doesn't actually fix anything
- The fix breaks something else
- Operating system failures
- Data corruption

* whats the risk of NOT making the change?
- Security Vulnerability
- Application Vulnerability
- Unexpected Downtime to other services

* Testing

* Sandbox testing environment
- No connection to the real world or production systems
- A technological safe space

* Use before making a change to production
- Try upgrade then apply patch
- Test and confirm before deployment

* Confirm the backout plan
- Move everything back to the original 
- A sandbox con't consider every possibility

* back out plans are very important, therefore always need to have one

* You should always have a way to revert your changes
- Prepare for the worst, hope for the best

* This isnt as easy as it sounds
- Some changes are hard to revert 

* Always have backups
- Always have good backups

* Maintenance window

* when is the change happening?
- This might be the most difficult part of the process

* During the work day may not be the best option
- Potential downtime would affect a large part of production

* overnights are often a better choice
- challenging for a 24 hour production schedule vs a business that is open standard business hours so IT will be seen applying updates early in the morning or on holidays.

* The time of year may be a consideration
- retail networks are frozen during the holiday season

* standard operating procedure (SOP)

* Change management is critical
- Affects everyone in the organization

* The process must be well documented
- Should be available on the intranet
- Along with all standard operating procedures

* Changes to the process are reflected in the standards
- A living document that is ever updating

**technical change Management**

* Put the change management process into action
- Execute the plan

* There is no such thing as a simple upgrade
- Can have many moving parts
- Separate events may be required

* Change management is often concerned with "what" needs to change.
- The technical team is concerned with "how" to change it.

* Allow list/ Deny list

* Any application can be dangerous
- Vulnerabilities, trojan horses, malware

* Security Policy can control app execution
- Allow list, deny/block list

* Allow list
- Nothing runs unless its approved
- Very restrictive

* Deny List
- No application on the deny list can be executed/ran
- Anti virus, Anti- Malware are a good example

* Restricted activities

* The scope of change is important 
- Defines exactly which components are covered

* A change approval isn't permission to make any change
- The change control approval is very specific
- Should not apply additional changes just because the time window
is open

* The scope may need to be expanded during the change window
- It's impossible to prepare for all possible outcomes, like if you have to update individual workstation config files after applying a driver update

* The change management process determines the next steps
- There is a process in place to make the change successful 

* Downtime

* Services will eventually be unavailable 
- The change process can be disrupted
- Usually scheduled during non production hours

* If possible prevent any downtime
- Switch to secondary system , upgrade the primary one then switch back.

* Minimize any downtime events
- The process should be automated as possible
- Switch back to secondary if issues appear
- Should be part of backout plan

* Send emails and calendar updates

* Restarts

* It's common to require a restart
- Implement the new configuration
- Reboot the OS, power cycle the switch, bounce the service(stop and start service again) 
- Can the system recover from a power outage

* Services
- Stop and restart the service in windows task manager or in linux restart a daemon
- May take seconds or minutes

* Applications
- Close Applications completely
- Launch a new application instance

* legacy systems

* Some applications were here before you arrived
- They will be there after you leave i.e windows 98 running mass transit systems

* Often no longer supported by the developer
- You are now the support team

* Fear of the unknown
- Face your fears and document the system
- May not be as bad as you think.

* May be quirky
- Create specific programs and procedures for legacy systems.

* Dependencies

* To complete A, you must complete B
- A service will not start without other active services
- An application requires a specific library version

* Modifying one component may require changing or restarting other components.
- This can be challenging to manage

* Dependencies may occur across systems
- Update the firewall code first
- Then upgrade the firewall management software

* Documentation

* it can be challenging to keep up with changes
- Documentation can become outdated very quickly

* Updating diagrams
- Modifications to network configurations
- I.P address updates

* version control

* Track changes to a file or configuration data over time
- Easily revert to previous setting

* Many opportunities to manage versions, examples
- Router configurations
- Windows OS patches
- Application registry entries

* Not always straightforward
- Some devices and OS provide version control features 
- May require additional management software













