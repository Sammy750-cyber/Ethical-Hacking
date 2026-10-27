# Ethical Hacking

---

## Course Overview

Ethical hacking is the structured, authorized examination of systems to identify and validate security weaknesses before malicious actors exploit them. It combines technical understanding with disciplined scope control, evidence handling, risk assessment, and clear reporting.

This material focuses on the core reasoning behind an ethical hacking engagement: how an assessment is planned, how an attacker’s likely path is modeled, how weaknesses are evaluated, and how findings are communicated responsibly. Networking, operating systems, cryptography, and security fundamentals appear only where needed to explain these activities.

### Learning Outcomes

By the end of this material, a learner should be able to:

1. Explain the purpose, boundaries, and professional obligations of ethical hacking.
2. Describe a typical penetration-testing lifecycle and the decisions made at each phase.
3. Distinguish reconnaissance, enumeration, vulnerability analysis, exploitation, post-exploitation, and reporting.
4. Explain common network, host, and web-application attack classes at a conceptual level.
5. Assess the significance of a weakness using technical evidence, exploitability, impact, and context.
6. Explain how authorization, scope, rules of engagement, and evidence handling reduce operational and legal risk.
7. Write clear findings with reproducible evidence, realistic impact, and actionable remediation.
8. Recognize when to stop testing, escalate an issue, or avoid an unsafe test.

---

## Chapter 1 — What Ethical Hacking Is

### 1.1 Definition

Ethical hacking is the authorized simulation of selected adversarial techniques to discover security weaknesses and determine their plausible consequences. It is performed under agreed constraints, with the aim of improving security.

The word *ethical* does not refer simply to good intentions. It refers to a defined authorization, a legitimate purpose, agreed boundaries, controlled execution, responsible evidence handling, and accountable reporting.

### 1.2 Ethical Hacking, Vulnerability Assessment, and Penetration Testing

These terms overlap, but they are not identical.

- **Vulnerability assessment:** Identifies, classifies, and prioritizes suspected weaknesses. It may rely heavily on automated discovery and configuration review.
- **Penetration test:** Attempts to validate whether selected weaknesses can be exploited and what security impact follows, within an agreed scope.
- **Red-team exercise:** Simulates a broader adversary objective, often testing people, processes, detection, and response as well as technology.
- **Security audit:** Evaluates controls against defined policies, standards, or requirements. It may or may not include exploitation.

A penetration test is not automatically a red-team exercise, and a scan alone is not a complete penetration test.

### 1.3 Why Organizations Commission Assessments

Common reasons include:

- Identifying exploitable weaknesses before an attacker does.
- Validating security controls and architectural assumptions.
- Testing the security impact of a new application, network, or infrastructure change.
- Meeting contractual, regulatory, or assurance requirements.
- Establishing a prioritized remediation plan.
- Measuring whether previous findings have been corrected.

The objective is not to collect the largest number of findings. It is to produce reliable evidence that helps an organization reduce meaningful risk.

### 1.4 Core Principles

1. **Authorization:** Obtain explicit permission before testing.
2. **Scope discipline:** Test only approved targets, accounts, techniques, and time windows.
3. **Least impact:** Use the least intrusive method that can answer the assessment question.
4. **Confidentiality:** Protect credentials, personal information, business data, and test evidence.
5. **Integrity:** Keep evidence accurate, traceable, and unaltered.
6. **Transparency:** Record what was tested, what was not tested, and what limitations apply.
7. **Accountability:** Be prepared to explain and reproduce the basis for every reported conclusion.

---

## Chapter 2 — Authorization, Scope, and Rules of Engagement

Technical competence cannot compensate for unclear authorization. Before testing begins, the tester and the system owner need a shared understanding of what is permitted.

### 2.1 Scope

A scope statement should identify:

- Approved IP ranges, hostnames, applications, APIs, cloud resources, or physical locations.
- Excluded systems and third-party services.
- Permitted testing windows and expected duration.
- Whether testing may use production systems.
- Approved test accounts and privilege levels.
- Allowed and prohibited techniques.
- Data-handling and evidence-retention requirements.
- Emergency contacts and escalation procedures.
- Conditions that require testing to stop.

A domain name or IP address being publicly reachable does not establish permission to test it.

### 2.2 Rules of Engagement

Rules of engagement turn a broad authorization into operational limits. They should address rate limits, denial-of-service restrictions, social-engineering permissions, use of automated tools, handling of sensitive data, and how the team will communicate unexpected findings.

For example, authorization to test a web application does not automatically authorize phishing its employees, attacking its hosting provider, or testing every subdomain associated with the organization.

### 2.3 Stop Conditions

Testing should pause when:

- A service becomes unstable or unexpectedly unavailable.
- Sensitive data is exposed beyond what is necessary to validate the finding.
- The test reaches a system outside the approved scope.
- A potentially destructive condition is discovered.
- The owner or designated contact requests a stop.
- The tester cannot determine whether the next action is authorized.

The correct response is to preserve relevant evidence safely, notify the agreed contact, and wait for direction.

### 2.4 Legal and Professional Considerations

Laws differ by jurisdiction and activity. Authorization should be explicit and documented, and contracts should specify permitted actions and responsibilities. Where the scope or legal basis is unclear, obtain clarification before proceeding. This material is educational and is not legal advice.

---

## Chapter 3 — The Penetration-Testing Lifecycle

A common engagement follows these phases. Frameworks use different names and may combine or reorder them, but the underlying reasoning is similar.

1. **Pre-engagement:** Define objectives, authorization, scope, contacts, and constraints.
2. **Reconnaissance:** Gather information relevant to the approved target.
3. **Enumeration and mapping:** Identify reachable services, application components, identities, and trust relationships.
4. **Vulnerability analysis:** Form hypotheses about weaknesses and evaluate supporting evidence.
5. **Validation or exploitation:** Safely determine whether a weakness is real and what impact it permits.
6. **Post-exploitation assessment:** Within explicit authorization, establish the limits of access and assess relevant security impact.
7. **Cleanup and restoration:** Remove test-created artifacts where appropriate, verify service state, and disclose anything that could not be safely removed.
8. **Reporting and retesting:** Communicate evidence and remediation guidance, then validate fixes when commissioned.

### 3.1 Testing Is Iterative

The lifecycle is not always linear. Enumeration may reveal a new hypothesis; validating it may change the assessment of risk; a failed attempt may show that a control is working. The tester should document these decisions rather than force every observation into a predetermined attack path.

### 3.2 Hypothesis-Driven Testing

A useful assessment question has four parts:

- **Observation:** What did the tester actually see?
- **Hypothesis:** What weakness might explain it?
- **Validation:** What safe test would distinguish the hypothesis from alternatives?
- **Conclusion:** What does the evidence prove, and what remains uncertain?

This approach reduces false positives and discourages unnecessary exploitation.

---

## Chapter 4 — Reconnaissance and Open-Source Intelligence

Reconnaissance gathers information that helps define the target’s externally visible attack surface. It should remain within the authorized scope.

### 4.1 Passive and Active Reconnaissance

- **Passive reconnaissance** uses information already available without directly probing the target’s systems, such as public documentation, published records, or public code repositories.
- **Active reconnaissance** interacts with the target, for example by checking which approved services respond. It can generate logs and may affect the target, so it must follow the rules of engagement.

The distinction is about the interaction with the target, not whether a tool is automated.

### 4.2 Common Information Categories

A tester may seek to understand:

- Public domains and subdomains.
- Public-facing applications and APIs.
- Technology and service indicators.
- Public documentation and repository exposure.
- Organizational naming conventions relevant to the approved assessment.
- Exposed files, outdated components, or accidental disclosures.
- Dependencies on external providers that are relevant to scope.

Information should be collected because it helps answer the assessment objective, not simply because it is available.

### 4.3 Enumeration

Reconnaissance produces broad context; enumeration develops a more precise inventory. It may establish which services are exposed, what authentication mechanisms are present, which application routes exist, or how a network segment is organized.

A discovered service is not automatically vulnerable. A version banner may be incomplete or misleading, and a suspected software version does not prove that a known vulnerability is exploitable in the target’s configuration.

### 4.4 Attack-Surface Mapping

An attack surface is the set of points where an unauthorized party might interact with a system. A useful map connects assets to interfaces, identities, dependencies, and trust boundaries.

For each relevant asset, record its identity, business purpose if known, exposure, evidence source, confidence, and scope status. Keep unverified assumptions separate from confirmed observations.

### 4.5 Reconnaissance Risks

Public information can contain personal data or secrets. Do not use exposed credentials to access accounts unless that validation is explicitly authorized. Do not publish sensitive discoveries. Report accidental disclosures through the agreed channel and retain only the minimum evidence needed.

---

## Chapter 5 — Network and Host Assessment Concepts

This chapter introduces only the networking and operating-system concepts necessary to understand penetration testing.

### 5.1 Services, Ports, and Protocols

A service provides functionality through a defined interface. A network port helps identify the endpoint used by a transport protocol, while an application protocol defines how communicating systems exchange messages.

An open port means a service or endpoint appears reachable. It does not, by itself, establish a vulnerability. Assessment requires understanding the service’s purpose, exposure, authentication, configuration, and patch status.

### 5.2 Network Segmentation and Trust Boundaries

Segmentation divides an environment into zones with different access requirements. Trust boundaries occur where data, identities, or control move between components with different security assumptions.

A tester evaluates whether access between zones matches the intended policy. Excessive reachability can increase the impact of a compromised host, but the risk depends on reachable services, identity privileges, and defensive controls.

### 5.3 Host Security

Host assessment examines the security posture of an operating system and its local services. Relevant areas include:

- Patch and software lifecycle status.
- Local accounts and privilege assignments.
- Service permissions and exposed management interfaces.
- File and directory permissions.
- Security configuration and logging.
- Credential storage and secret management.
- Endpoint protection and application-control policies.

A weak configuration is most important when it creates a credible path to unauthorized access, privilege escalation, data exposure, or persistence.

### 5.4 Authentication and Authorization

**Authentication** establishes an identity. **Authorization** determines what that identity is allowed to do. Strong authentication does not correct excessive permissions, and a well-designed authorization model does not prevent credential theft by itself.

### 5.5 Privilege Escalation

Privilege escalation occurs when a user or process gains more authority than intended. It is commonly described as:

- **Vertical escalation:** Moving from lower to higher privileges.
- **Horizontal escalation:** Accessing another user’s resources at a similar privilege level.

Typical underlying causes include unsafe permissions, vulnerable privileged components, weak service configurations, credential exposure, or broken authorization checks. A report should explain the specific boundary crossed rather than merely label an issue “privilege escalation.”

---

## Chapter 6 — Vulnerability Analysis and Validation

### 6.1 What Counts as a Vulnerability?

A vulnerability is a weakness that can be used to violate a security property. Examples include an authorization flaw, unsafe input handling, an exposed administrative interface, or a configuration that permits unintended access.

A missing security header, outdated version string, or scanner alert may indicate risk, but it is not necessarily proof of an exploitable vulnerability.

### 6.2 Evidence and Confidence

Findings should distinguish:

- **Confirmed:** Direct evidence demonstrates the behavior.
- **Strongly indicated:** Multiple observations support the conclusion, but a key part remains unverified.
- **Potential:** A plausible concern requires further investigation.

Confidence describes how certain the tester is that the finding is valid. Severity describes the importance of the security impact. These are different dimensions.

### 6.3 False Positives and False Negatives

- **False positive:** A reported weakness is not actually present or does not apply in the tested context.
- **False negative:** A real weakness is missed.

Automated tools can accelerate discovery, but they cannot reliably infer every business rule, trust boundary, or exploit precondition. Manual reasoning is needed to validate findings and understand context.

### 6.4 Risk Assessment

Risk is not identical to technical severity. Assessment should consider:

- Exploitability and prerequisites.
- Required privileges and user interaction.
- Confidentiality, integrity, and availability impact.
- Exposure and reachable attack paths.
- Business criticality and data sensitivity.
- Existing controls and realistic likelihood.
- Potential blast radius.

CVSS can help describe technical severity, but it should not replace business-context analysis. If a score is used, identify the scoring version and explain any meaningful environmental assumptions.

### 6.5 Safe Validation

Validation should answer the question with the least risky test available. Prefer non-destructive evidence. Avoid accessing real customer data, changing production records, or disrupting service merely to demonstrate impact. If stronger proof would introduce material risk, document the limitation and agree on a safer validation method.

---

## Chapter 7 — Exploitation: Concepts and Decision-Making

Exploitation is the controlled validation of a weakness by demonstrating that it can produce an unintended security outcome. It should never be treated as an end in itself.

### 7.1 From Weakness to Impact

A plausible exploitation chain usually requires:

1. A weakness or unsafe assumption.
2. Preconditions that allow the weakness to be reached.
3. A technique that triggers the unintended behavior.
4. A resulting security boundary violation.
5. Evidence that supports the claimed impact.

If one of these elements is missing, the conclusion should reflect the uncertainty.

### 7.2 Common Preconditions

A vulnerability may depend on network exposure, a specific configuration, an authenticated account, user interaction, a vulnerable software component, or a particular trust relationship. A finding should state the relevant preconditions rather than imply that every attacker can exploit it remotely.

### 7.3 Proof of Concept and Proof of Impact

A proof of concept demonstrates that a behavior can occur. Proof of impact connects that behavior to a meaningful security consequence. A safe proof might demonstrate access to a controlled test object rather than extract real data.

The smallest sufficient demonstration is usually preferable. More intrusive testing does not necessarily produce better evidence.

### 7.4 When Not to Exploit

Do not proceed when the likely next step could destroy data, interrupt a critical service, expose sensitive information, or exceed the agreed scope. Explain what has been established, what remains hypothetical, and what additional authorization or safeguards would be required.

---

## Chapter 8 — Web Application Security Testing

Web applications are a common penetration-testing target because they expose business logic, identity controls, data handling, and integrations through network-accessible interfaces.

### 8.1 Understand the Application First

Map the application’s major components:

- Browser or client.
- Web server and application logic.
- Authentication and session management.
- APIs and backend services.
- Database and file storage.
- Third-party integrations.
- Administrative functions and trust boundaries.

A security test should consider how these components interact, not just the visible user interface.

### 8.2 Authentication Weaknesses

Authentication issues can include weak account-recovery flows, insecure multi-factor authentication handling, credential-stuffing exposure, and inconsistent authentication requirements across interfaces.

Testing should use approved test accounts and avoid attempting to access unrelated users’ accounts.

### 8.3 Session Management

A session allows a system to associate successive requests with an authenticated user. Relevant controls include session-token unpredictability, secure transport, cookie attributes, expiration, rotation after privilege changes, logout behavior, and invalidation after suspected compromise.

A logout button that changes the interface but leaves the server-side session valid is not a complete session invalidation mechanism.

### 8.4 Broken Access Control

Broken access control occurs when the application fails to enforce who may perform an action or access an object. Examples include:

- A user viewing another user’s records.
- A standard user invoking an administrative function.
- An API accepting an object identifier without checking ownership.
- A workflow allowing a user to bypass an approval step.

Authorization should be checked server-side for every sensitive operation. Hiding a button in the interface is not an access-control boundary.

### 8.5 Injection

Injection occurs when untrusted input is interpreted as part of a command or query rather than handled as data. The specific consequences depend on the interpreter and context.

Defensive principles include parameterized queries, context-appropriate output encoding, strict input handling, least privilege, and avoiding unsafe dynamic command construction. Validation should be designed to establish the issue without altering or exposing real data.

### 8.6 Cross-Site Scripting (XSS)

XSS occurs when attacker-controlled content executes as script in another user’s browser under the application’s origin. It can affect confidentiality, integrity, and user trust.

Common categories include stored, reflected, and DOM-based XSS. Effective defenses include context-aware output encoding, safe DOM APIs, careful handling of rich text, and a well-configured Content Security Policy as a defense-in-depth measure. Input filtering alone is not a universal defense.

### 8.7 Cross-Site Request Forgery (CSRF)

CSRF abuses a browser’s tendency to include ambient credentials with requests. It is most relevant where a browser automatically attaches authentication state and the application does not adequately verify request intent.

Defenses may include anti-CSRF tokens, appropriate SameSite cookie settings, origin checks, and avoiding state changes through safe HTTP methods. The right controls depend on the authentication design.

### 8.8 Server-Side Request Forgery (SSRF)

SSRF occurs when a server can be induced to make requests to unintended destinations. Depending on the environment, this may expose internal services or cloud metadata endpoints.

Defenses include strict destination allowlists, network egress controls, redirect validation, address normalization, and isolation of sensitive internal services. URL parsing alone is not a sufficient defense.

### 8.9 File Uploads and Path Handling

Upload weaknesses can arise from trusting filenames or declared content types, storing files in executable locations, or failing to enforce size and content limits. Path traversal occurs when input causes a program to access files outside the intended directory.

Controls include server-generated filenames, content validation, storage outside executable web roots, safe path resolution, least-privilege access, and appropriate resource limits.

### 8.10 Business-Logic Flaws

Business-logic weaknesses arise when the application’s workflow rules can be bypassed even though individual components appear technically sound. Examples include applying a discount repeatedly, skipping an approval step, reusing a one-time action, or manipulating transaction order.

These issues often require manual analysis because automated scanners may not understand what a valid business transaction should look like.

### 8.11 API Security

APIs require attention to object-level authorization, function-level authorization, input schemas, excessive data exposure, rate limiting, authentication, and trust between services.

A valid token does not prove that the caller is entitled to every object or operation. Authorization should be enforced for each request and relevant resource.

### 8.12 Web Testing Method

A disciplined web assessment typically maps routes and roles, establishes expected behavior, tests trust boundaries, validates suspected issues with controlled data, records evidence, and evaluates remediation. It should include negative cases: attempts that should be rejected, not only workflows that should succeed.

---

## Chapter 9 — Network Service and Wireless Assessment

### 9.1 Network Service Assessment

Network-service testing examines exposed services, authentication, configuration, encryption, and access restrictions. The tester should ask:

- Is the service required?
- Is it exposed to the appropriate network zones?
- Is access authenticated and authorized?
- Is the service maintained and securely configured?
- Does it reveal sensitive information?
- Are management interfaces appropriately restricted?

A service may be correctly implemented yet unnecessarily exposed. Reducing attack surface is often a more effective fix than adding another detection rule.

### 9.2 Common Network-Level Weaknesses

Conceptual examples include weak or legacy protocols, excessive trust between hosts, exposed administrative services, poor network segmentation, insecure name-resolution assumptions, and insufficient monitoring.

The presence of a weakness does not establish that a particular attack path is viable. Network reachability, identity privileges, configuration, and other controls determine the practical risk.

### 9.3 Wireless Security

Wireless assessment considers authentication, encryption, access-point configuration, guest isolation, rogue access points, and the security of connected clients.

Important distinctions:

- A wireless network name is not a security control.
- Encryption protects traffic under defined assumptions; it does not fix compromised endpoints.
- A guest network is useful only if its isolation from internal resources is enforced.
- A rogue access point can create risk, but identifying one does not automatically authorize the tester to interfere with it.

Testing should use an authorized wireless network and agreed devices. Do not capture or inspect unrelated users’ communications.

---

## Chapter 10 — Identity, Credentials, and Social Engineering

### 10.1 Credential Security

Credentials include passwords, API keys, session tokens, certificates, and other authentication material. They should be protected according to their sensitivity and intended use.

Common weaknesses include password reuse, weak recovery processes, secrets embedded in source code, excessive token lifetime, and credentials exposed in logs or repositories.

### 10.2 Password Storage and Authentication Controls

Secure systems should not store passwords as plaintext or reversible encryption. Password verifiers should use an appropriate, salted, deliberately expensive password-hashing scheme. Authentication defenses may include rate limiting, multi-factor authentication, breached-password screening, and secure recovery procedures.

Controls should be balanced so that they resist attacks without creating avoidable denial-of-service or account-recovery problems.

### 10.3 Credential Attacks: Conceptual Categories

- **Brute force:** Repeatedly tries candidate credentials.
- **Password spraying:** Tries a small set of common passwords across many accounts.
- **Credential stuffing:** Reuses credentials exposed by unrelated breaches.
- **Phishing:** Deceives a person into revealing credentials or taking an unsafe action.
- **Token theft:** Obtains a session token or other bearer credential.

These categories have different indicators and mitigations. Any authorized testing should use approved accounts, controlled test data, agreed rate limits, and an explicit stop procedure.

### 10.4 Social Engineering

Social engineering exploits trust, urgency, authority, curiosity, or routine behavior rather than a purely technical defect. A controlled assessment may evaluate whether staff follow verification procedures, report suspicious messages, or protect sensitive information.

A legitimate exercise needs specific authorization, safeguards for participants, agreed messaging, privacy protections, and a debrief. Do not impersonate real people, collect real passwords, or target vulnerable individuals outside an approved plan.

### 10.5 Defensive Lessons

Useful controls include phishing-resistant multi-factor authentication where feasible, verified change-of-payment procedures, out-of-band confirmation for sensitive requests, clear reporting channels, and training that focuses on realistic decision-making rather than blame.

---

## Chapter 11 — Post-Exploitation, Impact, and Attack-Path Analysis

Post-exploitation assessment examines what an initial compromise could enable. It is particularly sensitive because it may involve privileged access, confidential data, or changes to system state.

### 11.1 Purpose

Within explicit authorization, the tester may determine whether a weakness allows access to additional resources, elevated privileges, sensitive functions, or other security boundaries. The objective is to establish impact, not to maximize access.

### 11.2 Attack Paths

An attack path is a sequence of conditions and actions that could lead from an initial position to a security objective. It may connect:

- An exposed service.
- A weak authentication or authorization boundary.
- A compromised identity.
- Excessive permissions.
- Access to a sensitive resource.

Each link should be supported by evidence or clearly labeled as an assumption. A diagram of an attack path is only useful if it distinguishes confirmed edges from hypothetical ones.

### 11.3 Lateral Movement and Privilege Boundaries

Lateral movement describes movement between systems or accounts after initial access. It may be enabled by reused credentials, overly broad administrative rights, weak segmentation, or trusted remote-management paths.

Privilege escalation concerns gaining greater authority; lateral movement concerns reaching another system or identity context. They can occur together but are not the same thing.

### 11.4 Persistence

Persistence refers to mechanisms that allow access to survive a change such as logout or reboot. Persistence testing can create serious operational and forensic consequences. It should be performed only when explicitly included in scope and with a clear plan for identification, documentation, and removal.

A test should not leave backdoors, accounts, scheduled tasks, or other artifacts behind without the system owner’s informed approval.

### 11.5 Demonstrating Impact Safely

Use the least intrusive evidence that establishes the security consequence. For example, demonstrate access to a designated test record rather than extracting a production database. Record the exact access boundary crossed, the required privileges, the affected asset, and any limitations.

### 11.6 Cleanup and Handover

At the end of testing, account for test-created files, accounts, tokens, configuration changes, and processes. Verify restoration where possible. Disclose any artifact that could not safely be removed and give the owner enough information to remediate it.

---

## Chapter 12 — Reporting, Remediation, and Retesting

A penetration test is incomplete if its findings cannot be understood and acted upon.

### 12.1 Standard Finding Structure

Each finding should contain:

1. **Title:** A concise description of the weakness.
2. **Severity:** A justified rating and scoring method, if used.
3. **Affected asset:** The system, route, endpoint, or component.
4. **Summary:** What is wrong and why it matters.
5. **Evidence:** Relevant observations, sanitized requests or responses, screenshots, logs, or other proof.
6. **Prerequisites:** Required access, configuration, user action, or network position.
7. **Impact:** Realistic consequences for confidentiality, integrity, availability, or business operations.
8. **Reproduction outline:** The minimum safe sequence needed to verify the issue.
9. **Root cause:** The underlying implementation or configuration failure, where known.
10. **Remediation:** Specific changes that address the root cause.
11. **References:** Relevant vendor advisories, standards, or technical guidance.
12. **Limitations:** What was not tested or what remains uncertain.

### 12.2 Executive Summary

The executive summary should explain the assessment objective, scope, principal risks, important limitations, and recommended priorities in language appropriate for decision-makers. It should not be a list of tool output or unexplained technical acronyms.

### 12.3 Severity Is a Reasoned Judgment

Severity should reflect realistic exploitability and impact, not the dramatic wording of a finding. A useful report distinguishes severity from confidence and explains important assumptions. Business context can change prioritization even where two findings have similar technical scores.

### 12.4 Remediation Quality

Weak remediation advice says “sanitize input,” “update security,” or “use stronger passwords” without explaining what must change.

Better advice identifies the control that failed and the corrective action. For example, for an object-level authorization flaw, recommend enforcing server-side ownership and permission checks for every request, then adding regression tests for unauthorized object access.

### 12.5 Retesting

Retesting determines whether the reported weakness was corrected and whether the fix introduced new issues. It should verify both the original failing case and relevant legitimate behavior. A fixed test case is not proof that every related code path is secure.

### 12.6 Evidence Handling

Evidence should be relevant, minimal, timestamped where useful, and linked to the finding it supports. Redact secrets and personal information. Restrict access, use secure storage, and follow the agreed retention and deletion policy.

---

## Chapter 13 — Professional Practice and Common Mistakes

### 13.1 Common Mistakes

- Testing before authorization or outside scope.
- Treating every scanner alert as a confirmed vulnerability.
- Assuming a service banner proves the installed version or exploitability.
- Pursuing exploitation without a clear assessment question.
- Collecting excessive sensitive data as proof.
- Failing to document test conditions and limitations.
- Reporting symptoms without identifying the underlying security boundary.
- Providing generic remediation advice.
- Leaving test artifacts behind.
- Treating the number of findings as the measure of assessment quality.

### 13.2 Traits of a Reliable Tester

A reliable tester is methodical, skeptical of assumptions, technically curious, careful with evidence, clear in communication, and willing to stop when risk exceeds authorization. Good judgment includes knowing when not to exploit.

### 13.3 Useful Assessment Questions

At each stage, ask:

- What is the assessment objective?
- Is this target and technique authorized?
- What does the current evidence actually establish?
- What alternative explanation could account for the observation?
- What is the least risky way to validate the hypothesis?
- What security boundary is being tested?
- What is the plausible impact if the weakness is real?
- What evidence will make the conclusion understandable to another analyst?
- What must be restored, reported, or escalated?

---

## Chapter 14 — Knowledge Checks

Answer these questions in your own words before checking the suggested answers.

### Questions

1. Why is explicit authorization necessary even when a system is publicly accessible?
2. What is the difference between a vulnerability assessment and a penetration test?
3. Explain the difference between passive and active reconnaissance.
4. Why does an open port not prove that a service is vulnerable?
5. How do authentication and authorization differ?
6. What is the difference between a false positive and a false negative?
7. Why should confidence and severity be recorded separately?
8. Explain broken access control using a generic example.
9. What is the difference between a proof of concept and proof of impact?
10. Why can input filtering alone fail to prevent injection or XSS?
11. Describe one way SSRF can cross a trust boundary.
12. Why should a tester use the least intrusive validation method?
13. What is an attack path, and how should uncertain links be represented?
14. What information belongs in a useful vulnerability finding?
15. Why is remediation retesting necessary?
16. Name three conditions that should cause testing to pause.
17. How do lateral movement and privilege escalation differ?
18. Why is cleanup part of the engagement rather than an optional courtesy?
19. Give an example of a business-logic vulnerability.
20. What makes remediation advice actionable?

### Suggested Answers

1. Public reachability is not permission. Authorization defines the legal and operational boundaries of testing.
2. A vulnerability assessment primarily identifies and prioritizes weaknesses; a penetration test validates selected weaknesses and their security impact within agreed limits.
3. Passive reconnaissance uses existing information without directly probing the target; active reconnaissance interacts with target systems and can generate traffic or operational effects.
4. Reachability only establishes that an endpoint responds. Vulnerability depends on implementation, configuration, exposure, access controls, and other conditions.
5. Authentication establishes identity; authorization determines permitted actions and resources.
6. A false positive reports a weakness that is not present or does not apply; a false negative misses a real weakness.
7. Confidence measures certainty that a finding is valid; severity estimates the importance of its impact.
8. For example, a user changes a record identifier in a request and can view another user’s record because the server fails to check ownership.
9. A proof of concept demonstrates a behavior; proof of impact connects it to a meaningful security consequence.
10. Inputs may reach different interpreters or output contexts. Defenses must match the context, such as parameterized queries or context-aware output encoding.
11. An application may be induced to request an internal service that an external client cannot reach directly.
12. It reduces the chance of data exposure, service disruption, or unauthorized changes while still gathering sufficient evidence.
13. It is a sequence of conditions and actions leading to an objective. Confirmed links should be distinguished from assumptions or unverified possibilities.
14. Title, affected asset, severity, summary, evidence, prerequisites, impact, reproduction outline, root cause, remediation, references, and limitations.
15. It confirms whether the fix works and checks that relevant legitimate behavior remains functional.
16. Examples include service instability, out-of-scope access, exposure of sensitive data, potentially destructive behavior, or a stop request from the owner.
17. Privilege escalation gains greater authority; lateral movement reaches another system or identity context.
18. Test artifacts can create ongoing risk or interfere with operations, so they must be accounted for and safely removed or disclosed.
19. A purchase workflow allows a discount to be applied multiple times when the business rules permit it only once.
20. It identifies the specific control or implementation change needed and explains how to verify that the fix works.

---

## Appendix A — Compact Glossary

- **Attack surface:** Points through which a system can be interacted with or attacked.
- **Attack path:** A sequence of conditions and actions leading to a security objective.
- **Authentication:** Establishing the identity of a user, device, or service.
- **Authorization:** Determining which actions or resources an identity may access.
- **Enumeration:** Systematically identifying services, resources, identities, or application functions.
- **Exploit:** A technique that takes advantage of a weakness.
- **False negative:** A real weakness that was not detected.
- **False positive:** An alert or conclusion that incorrectly identifies a weakness.
- **Finding:** A documented security issue supported by evidence.
- **Least privilege:** Giving an identity or process only the permissions needed for its role.
- **Lateral movement:** Moving from one system or identity context to another after initial access.
- **OSINT:** Open-source intelligence gathered from lawfully accessible sources.
- **Penetration test:** An authorized assessment that validates selected weaknesses and their impact.
- **Proof of concept:** A limited demonstration that a claimed behavior is possible.
- **Reconnaissance:** Gathering information about an authorized target.
- **Remediation:** Correcting a weakness or reducing its risk.
- **Rules of engagement:** The agreed operational limits and procedures for an assessment.
- **Scope:** The assets, activities, and limits included in the authorization.
- **Threat:** A potential cause of harm to a system or organization.
- **Vulnerability:** A weakness that could violate a security property.

---

## Appendix B — Suggested Study Sequence

1. Learn the definitions and professional boundaries in Chapters 1–3.
2. Study reconnaissance, enumeration, and attack-surface mapping in Chapters 4–5.
3. Work through vulnerability validation and exploitation reasoning in Chapters 6–7.
4. Study web, network, wireless, identity, and social-engineering assessment concepts in Chapters 8–10.
5. Learn attack-path analysis, evidence handling, reporting, and remediation in Chapters 11–13.
6. Complete the knowledge checks without consulting the suggested answers, then revisit weak areas.

## Appendix C — Safe Lab Guidance

For future practical work, use a deliberately vulnerable virtual machine or an application designed for security training, isolated from production networks. Keep snapshots, use test accounts and synthetic data, and avoid bridged or externally exposed configurations unless the lab design requires them and is understood. Document the scope, expected outcome, observed evidence, and cleanup steps for every exercise.

## Closing Note

Ethical hacking is not a collection of tools or a race to obtain the highest level of access. It is a disciplined method for testing security assumptions, validating weaknesses with proportionate evidence, and helping system owners make informed improvements. Technical depth matters, but sound judgment, scope control, and clear reporting are equally essential.
