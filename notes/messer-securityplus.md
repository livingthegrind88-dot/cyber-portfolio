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
