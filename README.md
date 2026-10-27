# Ethical Hacking: Principles, Law, and Professional Practice

### A Combined Instructor and Student Reference

---

## Front Matter

### About This Volume

This volume is a single reference text designed to serve two readerships simultaneously. Students read it as the conceptual foundation of the course; instructors read it as the teaching apparatus for the module. To keep both uses legible without duplicating material, the text uses a consistent set of typographic conventions.

### Conventions Used in This Volume

| Marker | Meaning | Primary audience |
| :--- | :--- | :--- |
| **[Objective]** | Stated learning outcomes for the chapter | Both |
| **[Instructor Note]** | Teaching guidance, common misconceptions, timing, assessment emphasis | Instructor |
| **[Exercise]** | Structured classroom or self-study activity | Both |
| **[Case Study]** | Real-world incident or legal proceeding, used as analytical material | Both |
| **[Self-Assessment]** | Questions with a model answer key in Appendix E | Student |
| **[Further Reading]** | Primary sources and standards | Both |

### How Instructors Should Use This Volume

The volume is designed for a 4–6 hour delivery, but the content is deliberately over-provisioned: it contains sufficient material for a 12–16 hour graduate seminar if the case studies and exercises in Chapters 3, 4, and 9 are treated as full sessions. Instructors should select, not cover.

Recommended delivery patterns:

1. **Front-loaded (default).** Deliver Chapters 1–7 before any technical lab. Chapters 8–9 become the capstone. This produces the strongest conceptual grounding, but students will treat the legal and ethical material as abstract until they encounter it in the lab.
2. **Retrospective (recommended for cohorts already trained).** Deliver Chapter 1 briefly, run the technical labs, then deliver Chapters 3, 4, and 9 as a retrospective reframing. Students who have already pivoted into an internal network and removed a backdoor read the material with considerably more attention.
3. **Interleaved (recommended for long courses).** Chapter 1 before lab one; Chapter 3 before the first exploitation lab; Chapters 4 and 9 after the persistence lab; Chapters 5–8 distributed as reading.

**[Instructor Note]** The single most consequential pedagogical decision in this module is whether to teach law and ethics *before* or *after* the student has done something technically irreversible. Students who write a persistence mechanism and then must remove it understand scope and cleanup obligations in a way that no pre-lab lecture achieves. Where scheduling permits, interleave.

### How Students Should Use This Volume

Read Chapters 1–2 for orientation, Chapter 3 before attempting any lab exercise, and Chapter 4 before writing your first engagement report. Chapters 5–7 are reference material to be consulted as the course progresses. Chapter 9 should be read twice: once cold, once after completing the labs.

The volume assumes no prior security knowledge. It does assume that you will eventually operate the tools described elsewhere in the course, and it is written on the premise that conceptual understanding is not optional preparation for technical work but is itself the technical work.

---

## Chapter 1 — Conceptual Foundations

**[Objective]** After this chapter the reader should be able to: (1) define ethical hacking precisely and defend the definition against thinner alternatives; (2) distinguish ethical hacking from adjacent practices including security research, vulnerability disclosure, and malicious intrusion; (3) define and correctly deploy the core technical vocabulary of the field; (4) explain why the distinction between ethical and malicious practice is a matter of boundary conditions rather than technique.

### 1.1 The Definitional Problem

The most common definition of ethical hacking in introductory material is "hacking with permission." This definition is defective in a specific and consequential way: it is a *legal* definition masquerading as a *professional* one. It specifies a necessary condition — authorization — and then stops, leaving the impression that authorization exhausts the obligation.

The consequence is observable in practice. Assessors who operate on the "permission" definition routinely dump full user tables when a single row would establish a SQL injection; routinely leave backdoors in place past the reporting deadline; routinely omit from reports the production record they accidentally modified. Each of these is *authorized*. None is *ethical*.

A defensible definition must therefore carry obligations that authorization does not:

> **Definition.** Ethical hacking is the practice of applying offensive security techniques to systems for which the practitioner holds explicit, scoped, written authorization from a party with authority to grant it, for the purpose of identifying and remediating weaknesses, while (a) constraining action to the minimum necessary to demonstrate the finding, and (b) disclosing all findings and all unintended consequences, including the practitioner's own errors, to the authorizing party.

The definition contains three independent obligations. A practice that satisfies two of three is not ethical hacking; it is something else that happens to be authorized.

| Obligation | Formal statement | Typical breach |
| :--- | :--- | :--- |
| **Authorization** | Explicit, written, scoped, from an authorized signatory, within a current window | Testing a system on the assumption that permission "probably" exists |
| **Minimization** | The least intrusive action sufficient to establish the finding | Exfiltrating 200 records to prove a query is injectable |
| **Disclosure** | Complete, accurate reporting of findings and of the assessor's own errors | Omitting an accidental production data modification |

### 1.2 Ethical Hacking and Its Adjacent Practices

The field is frequently muddled by the conflation of four distinct activities. They differ along four axes: authorization, intent, effect on the target, and disclosure channel.

| Practice | Authorization | Intent | Effect on target | Disclosure channel |
| :--- | :--- | :--- | :--- | :--- |
| **Ethical hacking** (penetration testing) | Explicit, written, scoped | Improve security | Controlled, minimized | Client report |
| **Vulnerability research** | Varies; often none on the researcher's own systems | Understand and document a class of weakness | None on third parties | Vendor, CVE, or publication |
| **Coordinated disclosure** | None required at the point of reporting | Enable remediation | None | Vendor first, public later |
| **Malicious intrusion** | None | Financial, ideological, or personal gain | Maximized | Concealment or sale |

Two distinctions in this table carry most of the pedagogical weight.

The first is that **vulnerability research does not require authorization over the target**, because the researcher does not touch the target. Analysing a decompiled binary, reproducing a flaw in a locally hosted instance, or reasoning about a protocol specification are all legitimate research activities that require no permission from anyone. The moment the researcher sends a packet to a system they do not own, the authorization requirement attaches.

The second is that **coordinated disclosure is not ethical hacking and is not malicious intrusion**. It is a reporting activity. Its ethics are governed by a different question — the balance between vendor accountability and user risk — which Chapter 4 treats at length.

### 1.3 Boundary Conditions Rather Than Techniques

A central claim of this volume, and one that students frequently resist, is that there is no technical operation that is inherently ethical or inherently malicious. The same `nmap` invocation, the same SQL injection payload, the same Meterpreter session are identical in both cases. What differs is the boundary condition under which the operation is performed.

| Boundary | Ethical practice | Malicious practice |
| :--- | :--- | :--- |
| Authorization | Written, scoped, signed, current | Absent or self-granted |
| Intent | Remediation | Gain, damage, notoriety |
| Constraint | Stop at proof; non-destructive | Maximize effect; destructive |
| Disclosure | Complete report to the owner | Concealment, sale, or public dump |

**[Instructor Note]** Students reliably interpret this section as an exoneration — "the technique is neutral, so my technique is fine." Pre-empt this reading explicitly. The neutrality of technique means that **the entire ethical weight falls on the practitioner's boundary discipline**, not that the technique is exempt from judgement. The correct inference is the opposite of the one students draw: because the technique cannot be judged in isolation, the practitioner's judgement is the only thing that can be judged, and it will be.

### 1.4 Technical Vocabulary and Its Failure Modes

Precision in terminology is not pedantry. In a report, in testimony, and in a client conversation, the substitution of one term for another changes the meaning of a claim and can change liability.

| Term | Precise definition | Failure mode | Consequence |
| :--- | :--- | :--- | :--- |
| **Vulnerability** | A weakness in a system that could be exploited to violate a security property | Substituted for "exploit" | Report claims exploitation that did not occur |
| **Exploit** | A technique or artifact that leverages a vulnerability | Substituted for "payload" | Misattributes mechanism to effect |
| **Payload** | The action executed after successful exploitation | Substituted for "exploit" | Obscures the actual attack path |
| **Threat actor** | An entity with intent and capability to conduct an attack | Substituted for "vulnerability" | Conflates adversarial intent with system defect |
| **Attack surface** | The set of all reachable entry points, including human and supply-chain | Substituted for "vulnerability" | Overstates or understates exposure |
| **Zero-day** | A vulnerability for which no patch exists at the time of use | Applied to any unpatched system | Inflates severity and misleads remediation |
| **CVE** | A standardized identifier for a publicly disclosed vulnerability | Substituted for "exploit" | Conflates identification with capability |
| **CVSS** | A framework scoring technical severity of a vulnerability | Treated as a business risk score | Prioritization error; see §4.6 |
| **PoC** | A reproducible demonstration establishing that a finding is real | Substituted for "exploit code" | Conflates evidence with weaponization |
| **Scope** | The set of assets and techniques explicitly authorized | Substituted for "target list" | Authorization ambiguity with legal consequence |

**[Exercise 1.1 — Definitional precision]** Without consulting the table, write a one-sentence definition of each of the ten terms. Exchange with a partner. Where definitions differ, identify whether the difference is stylistic or substantive. Substantive differences are the ones that produce report errors.

### 1.5 Chapter Summary

Ethical hacking is distinguished from malicious intrusion by four boundary conditions, of which authorization is only the first. A definition that stops at authorization is a legal definition and is professionally insufficient. The obligations of minimization and disclosure are independent of authorization and are breached routinely by practitioners who believe themselves ethical. Because no technique is inherently ethical or malicious, the ethical weight of the work falls entirely on the practitioner's boundary discipline — which is therefore the thing that will be assessed.

**[Self-Assessment 1]** Questions 1–5, Appendix E.

---

## Chapter 2 — Threat Actor Taxonomy

**[Objective]** After this chapter the reader should be able to: (1) classify threat actors by motivation, capability, access, and persistence; (2) explain why actor classification determines defensive control selection; (3) distinguish likelihood from impact and apply both to prioritization; (4) critically evaluate the colour-hat taxonomy and articulate its limitations.

### 2.1 Why Actor Classification Is a Defensive Instrument

Threat actor classification is often taught as background knowledge. It is better understood as an input to control selection. A control set optimized against a script kiddie is qualitatively different from one optimized against a nation-state, and an organization that cannot name its plausible adversaries cannot prioritize its spending.

Four attributes carry most of the analytic weight:

- **Motivation** — what the actor wants, which determines target selection and persistence.
- **Capability** — the actor's tooling, resourcing, and skill, which determines the controls that will hold.
- **Access** — whether the actor operates externally, as an insider, or through the supply chain.
- **Persistence and stealth** — whether the actor intends to be detected, which determines whether detection investment is warranted.

### 2.2 Actor Profiles

| Actor | Motivation | Capability | Access | Stealth | Primary controls |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Script kiddie | Ego, curiosity | Low; existing tooling | External | Low | Patch management, credential hygiene, attack-surface reduction |
| Hacktivist | Ideology, publicity | Low–moderate | External | Low; publicity is the objective | Availability controls, defacement monitoring, brand monitoring |
| Malicious insider | Revenge, financial | High; legitimate access | Internal | High by default | Least privilege, separation of duties, behavioural analytics, offboarding |
| Negligent insider | None | N/A | Internal | N/A (accidental) | Training, DLP, access review, backup integrity |
| Organized crime | Financial | High; ransomware, BEC, extortion | External, sometimes with insider purchase | Moderate; pressure is the objective | Immutable backup, segmentation, MFA, egress filtering, incident response |
| Nation-state | Espionage, pre-positioning, disruption | Very high; zero-days, supply chain | External, supply chain, long-dwell insider | Very high | Defence in depth, supply-chain assurance, hardened identity, long-dwell detection |
| Competitor | Commercial advantage | Moderate–high | External, sometimes insider | High | DLP, access control, IP monitoring |

### 2.3 Likelihood, Impact, and the Prioritization Error

The most common analytic error in this area is conflating likelihood with impact. They are independent axes, and an organization that optimizes for the wrong one spends money in the wrong place.

Consider a mid-sized logistics firm. Organized crime is the most likely adversary: ransomware against logistics firms is a well-established criminal business model, the firm holds data of value, and the attack does not require advanced capability. A nation-state is the most dangerous adversary if it selects the firm as a target — but it is the least likely, because the firm's data has limited intelligence value.

The correct defensive conclusion is not "ignore the nation-state." It is that the control set should be **optimized for the likely adversary and stress-tested against the capable one**. Backups and segmentation defeat organized crime; they are also the controls that determine whether a nation-state intrusion becomes a destructive event. The two investments overlap substantially but not completely, and the overlap is where the money should go first.

**[Instructor Note]** Push students past the comfortable answer. The comfortable answer is "defend against everything." The professional answer is a prioritized statement with an explicit justification for the ordering, and an explicit statement of what is being accepted as residual risk. Ask each student to name the single control they would fund first for the logistics firm and to defend the choice against a classmate who names a different one. Both answers may be defensible; what is not defensible is the absence of a justification.

### 2.4 The Colour-Hat Taxonomy and Its Limitations

The colour-hat vocabulary is ubiquitous and is taught in nearly every introductory course. It is also analytically weak, and students should understand why.

| Term | Conventional meaning | Limitation |
| :--- | :--- | :--- |
| White hat | Authorized, ethical | Implies a binary distinction that does not hold in practice |
| Black hat | Unauthorized, malicious | — |
| Grey hat | Unauthorized, non-malicious | Still unlawful in most jurisdictions; intent is not a defence |
| Red hat | Vigilante action against black hats | Legally indistinguishable from black hat in most jurisdictions |
| Blue hat | Defensive operations | — |
| Purple team | Integrated red and blue activity | A process, not an actor |

The taxonomy fails in three ways. It conflates **legal status** with **ethical status**, which Chapter 4 will show are distinct. It implies a **binary** where the operative distinction is a set of continuous boundary conditions. And it has no category for the most consequential actor in most organizations — the **negligent insider**, who has no hat at all.

**[Instructor Note]** Grey hat is the category students romanticize. Address it directly and without hedging: grey hat activity is unauthorized access and is prosecuted as such in every major jurisdiction. The fact that the actor disclosed the finding does not retroactively create authorization, and the fact that the actor intended to help does not mean the system owner consented to the risk. There is no jurisdiction in which "I only did it to help" operates as a defence to an unauthorized-access charge.

### 2.5 Chapter Summary

Actor classification is a control-selection instrument, not background reading. The four attributes of motivation, capability, access, and stealth determine which controls will hold. Likelihood and impact are independent axes, and prioritizing by either alone produces misallocation. The colour-hat taxonomy should be understood, taught, and then set aside in favour of a model that captures legal status, ethical status, and negligence as separate dimensions.

**[Self-Assessment 2]** Questions 6–9, Appendix E.

---

## Chapter 3 — The Legal Framework

**[Objective]** After this chapter the reader should be able to: (1) identify the principal computer-misuse statutes in major jurisdictions and their operative provisions; (2) explain the layered nature of authorization; (3) apply the conservative authorization rule to novel situations; (4) state the elements that a valid authorization instrument must contain; (5) recognize the jurisdictional issues that arise in cross-border engagements.

**[Instructor Note — mandatory framing]** This chapter is orientation, not legal advice. State this explicitly at the start of the session and repeat it before any exercise. Instructors are not qualified to advise students on the law of their jurisdiction, and a student who acts on a classroom statement about legality may face consequences the instructor cannot mitigate. The correct instructional move is always: "This is the framework; confirm the position with qualified counsel."

### 3.1 The Principal Instruments

| Jurisdiction | Instrument | Operative provision | Notes |
| :--- | :--- | :--- | :--- |
| United States | Computer Fraud and Abuse Act, 18 U.S.C. § 1030 (1986, as amended) | Prohibits unauthorized access and exceeding authorized access to protected computers | Principal federal statute; state statutes add coverage |
| United Kingdom | Computer Misuse Act 1990 | s.1 unauthorized access; s.2 unauthorized access with intent to commit further offences; s.3 unauthorized modification; s.3ZA serious damage (inserted by Serious Crime Act 2015) | Enacted following *R v Gold and Schifreen* [1988] AC 1063, in which forgery charges failed on facts that would now fall under s.1 |
| European Union | Directive 2013/40/EU on attacks against information systems | Requires criminalization of illegal access, illegal system interference, illegal data interference | Implemented through member-state law; NIS2 (Directive (EU) 2022/2555) adds security obligations for essential and important entities |
| Nigeria | Cybercrimes (Prohibition, Prevention, etc.) Act 2015 (as amended) | Prohibits unauthorized access, interception, and system interference | Directly relevant to engagements conducted by or against Nigerian entities |
| International | Council of Europe Convention on Cybercrime (Budapest Convention), ETS 185 (2001); Second Additional Protocol (2022) | Harmonizes substantive offences and provides mutual legal assistance | Not self-executing; effect depends on national implementation |

### 3.2 The Interpretation Problem

Statutes prohibiting "unauthorized access" appear clear and are not. The central difficulty is what "authorization" means when access is technically possible and the system owner has not said no.

The leading U.S. authority is *Van Buren v. United States*, 593 U.S. 374 (2021), in which the Supreme Court narrowed the CFAA's "exceeds authorized access" language to a "gates-up-or-down" inquiry: the question is whether the person was authorized to access the area of the system in question at all, not whether the purpose for which they accessed it was improper. Before *Van Buren*, several circuits had treated violations of terms of service or acceptable-use policies as exceeding authorized access, producing an unpredictable and much-criticized body of law.

The practical implication for assessors is that the statutory boundary remains uncertain at its edges, and litigation is an expensive way to discover where the edge is. Hence the rule in §3.3.

### 3.3 The Conservative Authorization Rule

> **Rule.** If the practitioner is not certain that authorization exists for a specific action, then authorization does not exist for that action.

The rule is deliberately asymmetric. The cost of declining an authorized action is a delayed finding; the cost of performing an unauthorized action is potential criminal liability, contract termination, and career foreclosure. The asymmetry justifies a rule that will occasionally be over-cautious.

**[Case Study — *United States v. Morris*, 928 F.2d 504 (2d Cir. 1991)]** The first conviction under the CFAA arose from the 1988 Morris worm, released by a Cornell graduate student. The defence argued that the worm's release did not constitute "unauthorized access" because the defendant had authorized accounts on some affected systems. The Second Circuit rejected the argument, holding that access obtained in a manner the system owner did not intend could be unauthorized. The case is worth teaching for two reasons: it establishes that technical access does not imply authorization, and it illustrates that the statute reaches conduct by a researcher with no malicious intent.

**[Case Study — *United States v. Swartz*]** The prosecution of Aaron Swartz (2011–2013) over bulk downloading from JSTOR via the MIT network became the most publicly contested CFAA prosecution in the statute's history and contributed to sustained legislative reform efforts. The case is analytically useful because the conduct in question sat at the boundary of the statute's text and its purpose, and because the prosecution's proportionality was itself the subject of intense professional debate. It is a case about the gap between technical access and authorized access, and about the consequences of that gap falling on an individual rather than an institution.

### 3.4 Authorization Is Layered

The most consequential practical error in this area — more common than the absence of authorization — is the assumption that authorization is a single, undifferentiated grant. It is not. Authorization is layered along at least four dimensions, and each layer must be satisfied independently.

| Layer | What it authorizes | What it does not authorize |
| :--- | :--- | :--- |
| **Entity** | The signing legal entity's own systems | Systems owned by subsidiaries, parents, or partners |
| **Tenancy** | A client's own hosted environment | The provider's shared infrastructure or other tenants |
| **Asset** | Named hosts, domains, applications | Unlisted assets, however plausibly owned |
| **Technique** | Permitted techniques as specified in the RoE | Prohibited techniques, including those the client requests orally |

Three consequences follow, and each is a recurring source of professional failure.

**Corporate ownership does not confer authorization.** A parent company cannot authorize testing of a subsidiary's systems, because the subsidiary is a separate legal person that has not consented. The correct instrument is a separate authorization signed by an authorized signatory of the subsidiary. This is not a formality; a parent-company signature will not protect the assessor if the subsidiary complains.

**Tenancy does not extend to shared infrastructure.** A client that hosts on a shared platform can authorize testing of its own tenancy. It cannot authorize testing of the hypervisor, the shared network fabric, or neighbouring tenants. Any technique with the potential to affect neighbours — resource exhaustion, load testing, certain injection classes that traverse shared components — must be excluded or separately coordinated with the provider.

**Credentials do not constitute authorization.** A person who supplies working credentials has supplied *access*, not *authority*. Scope derives from the authorized signatory, not from whoever happens to hold a password. An assessor who tests a system because its administrator handed over credentials has performed unauthorized access with a helpful co-conspirator.

### 3.5 The Authorization Instrument

The authorization letter is the only document that distinguishes a penetration test from a computer-misuse offence. It must contain, at minimum, the following elements.

| # | Element | Why it matters |
| :--- | :--- | :--- |
| 1 | Legal entity name of the authorizing party | Establishes who consented |
| 2 | Named assets, ranges, domains, applications | Establishes what was consented to |
| 3 | Testing window with dates, times, and timezone | Establishes when consent was operative |
| 4 | Permitted techniques | Establishes the scope of permitted action |
| 5 | Name, title, and signature of the authorizing individual | Establishes that consent was given by a person with authority |
| 6 | Statement of the signer's authority | Addresses the most common challenge to validity |
| 7 | Emergency contact available throughout the window | Enables the stop procedure |
| 8 | Reference to the SOW and RoE by date | Binds the operational documents to the grant |
| 9 | Signature date preceding the testing window | Establishes temporal validity |
| 10 | Authentication marker (letterhead or equivalent) | Supports later proof of provenance |

**[Exercise 3.1 — Instrument critique]** The instructor supplies three authorization letters, each defective in one respect: a signatory at an insufficient level of authority; a scope clause reading "all company systems"; and a testing window that has already expired. Students must identify the defect, state the legal consequence, and draft the corrective action. Model answers in Appendix E.

### 3.6 Cross-Border Engagements

Where the assessor, the client, and the target are in different jurisdictions, three additional issues arise. **Extraterritorial reach** varies: the CFAA reaches conduct with a sufficient U.S. nexus, and several jurisdictions assert jurisdiction over conduct affecting their nationals or infrastructure. **Mutual legal assistance** under the Budapest Convention is slow and not a substitute for authorization. **Local prohibitions** may exceed the assessor's home jurisdiction: a technique lawful at home may be unlawful at the target's location.

The professional standard is to obtain authorization under the law of the jurisdiction where the **target** is located, and to confirm with counsel where the three jurisdictions diverge.

### 3.7 Chapter Summary

Computer-misuse statutes converge on the concept of unauthorized access and diverge on its interpretation. The statutory boundary is uncertain at its edges, which is precisely why the conservative rule applies. Authorization is layered across entity, tenancy, asset, and technique; the most common professional failure is assuming a grant at one layer extends to another. The authorization instrument must contain ten specific elements, and the most frequently challenged is the signer's authority.

**[Self-Assessment 3]** Questions 10–14, Appendix E.

---

## Chapter 4 — Professional Ethics

**[Objective]** After this chapter the reader should be able to: (1) apply three normative frameworks to security dilemmas and explain where they converge and diverge; (2) apply the four-question decision procedure to ambiguous scenarios; (3) analyse disclosure dilemmas including coordinated disclosure and self-disclosure of error; (4) evaluate the dual-use problem in security research; (5) explain why professional codes impose obligations beyond the client relationship.

### 4.1 Why a Framework Rather Than Intuition

Intuition fails in security ethics for a structural reason: the dilemmas are designed to make the wrong choice feel like the right one. The request to test a competitor's site arrives framed as a favour to a worried client. The decision to withhold a mistake arrives framed as protecting the engagement. The decision to publish an unpatched exploit arrives framed as holding a vendor accountable. In each case, the intuitive choice serves an immediate relationship and harms a distant party.

A framework does not guarantee correct answers. It guarantees that the reasoning is explicit, inspectable, and consistent — which is what a professional is entitled to be held to.

### 4.2 Three Normative Frameworks

| Framework | Central question | Strength | Weakness in security context |
| :--- | :--- | :--- | :--- |
| **Consequentialist** | Which action produces the best overall outcome? | Handles disclosure trade-offs well; naturally weighs third-party harm | Requires predicting outcomes that are genuinely uncertain |
| **Deontological** | Which duties constrain my action regardless of outcome? | Produces firm rules (do not test without authorization; do not conceal error) that resist pressure | Can appear rigid where consequences are severe |
| **Virtue ethics** | What would a practitioner of good character do? | Captures the professional-identity dimension that rules and outcomes miss | Less determinate; depends on a shared conception of the good practitioner |

Professional codes such as the ISC2 Code of Ethics synthesize all three. Its four canons are worth quoting in full because they are frequently cited and rarely read:

1. Protect society, the common good, necessary public trust and confidence, and the infrastructure.
2. Act honorably, honestly, justly, responsibly, and legally.
3. Provide diligent and competent service to principals.
4. Advance and protect the profession.

Note the ordering. The obligation to **society** precedes the obligation to **principals**. This is not incidental drafting. It establishes that a client's instruction cannot override the practitioner's obligation to third parties, and it is the textual basis for the professional's authority — indeed obligation — to refuse a client request that would harm others.

**[Instructor Note]** Read Canon 1 aloud and then ask: "Which canon would you be violating if you tested a competitor's site at a client's request?" Students typically answer Canon 2 or 3. The sharper answer is Canon 1, because the harm falls on a third party who is not a principal at all. This distinction — obligations that run to non-clients — is the conceptual core of professional ethics and is what separates a profession from a vendor relationship.

### 4.3 The Four-Question Decision Procedure

The procedure below is a deontological screen with a consequentialist harm assessment appended. It is deliberately conservative: it is designed to stop action in doubt rather than to license action in confidence.

```
1. AUTHORIZATION
   Do I hold explicit, written permission for this specific action,
   from a party with authority, within a current window?

2. NECESSITY
   Is this action the minimum sufficient to establish the finding,
   or am I acting because I am able to?

3. HARM
   Who could be harmed — users, operators, third parties — and have
   I reduced that harm to the minimum consistent with the finding?

4. DISCLOSURE
   Will I report this action honestly, including unintended
   consequences and my own errors, to the authorizing party?
```

> **Decision rule.** If any answer is negative or uncertain, suspend the action and escalate to the engagement lead and, where appropriate, the client's authorizing signatory.

The procedure's value lies in question 4. Questions 1–3 are screens applied before action; question 4 is a pre-commitment about what will be reported afterwards. Practitioners who ask question 4 honestly before acting behave differently from those who ask it afterwards, because the honest answer to "will I report this?" sometimes reveals that the intended action would be indefensible if reported.

### 4.4 Disclosure Ethics

Disclosure is the ethical dimension most frequently mishandled, in three distinct forms.

**Coordinated disclosure.** A researcher who discovers a vulnerability in a widely used product faces a trade-off between vendor accountability (public disclosure pressures patching) and user risk (public disclosure arms attackers before patches are available). The professional norm, codified in ISO/IEC 29147 and ISO/IEC 30111 and reflected in the practices of CERT/CC and major vendor programmes, is coordinated disclosure: notify the vendor privately, agree a remediation timeline, and publish after a defined period regardless of whether a patch has been issued. The period is a matter of professional judgement; 90 days is a common baseline, extended where the vendor is demonstrably engaged.

**Third-party findings.** A vulnerability in a third-party component discovered during an authorized engagement creates a conflict between the client's confidentiality interest and the safety of other users of that component. The correct sequence is: report to the client first; request permission to notify the upstream maintainer; if the client refuses, escalate within the client's organization and document the refusal. Unilateral public disclosure in breach of a confidentiality obligation is not justified by the merits of the finding.

**Self-disclosure of error.** This is the test that distinguishes practitioners. An assessor who has accidentally modified production data faces a choice between immediate disclosure, which invites consequences, and silence, which invites discovery. The obligation is absolute and admits no balancing: disclosure is immediate, complete, and documented. The reasoning is not merely moral but practical — audit logs, integrity monitoring, and client-side forensic review make discovery likely, and the professional consequences of concealment are categorically worse than those of the underlying error.

**[Case Study — *United States v. Sullivan* (N.D. Cal. 2022)]** The former chief security officer of Uber was convicted of obstruction of justice and misprision of a felony for his handling of the company's 2016 data breach, including the failure to disclose the incident to regulators and the arrangement of a payment to the attackers structured as a bug bounty. The case is the clearest available illustration that concealment of a security incident is itself a distinct offence, separate from the incident, and that it reaches senior security leadership personally. It should be taught in every course that covers incident handling or disclosure.

**[Instructor Note]** Sullivan is the most effective case study in this chapter because it involves a security professional, not an attacker. Students who are unmoved by the abstract obligation of disclosure respond strongly to the concrete fact that a CSO was convicted for the handling of a breach rather than for the breach. Ask: "What was the moment at which the correct decision was available?" It is the moment of discovery, not the moment of settlement.

### 4.5 Dual Use

Security research is dual-use by construction: an exploit demonstrates both that a defence is needed and how to defeat it. The ethical question is not whether dual use exists but how the researcher manages the risk of misuse.

**[Case Study — the prosecution of Marcus Hutchins]** Hutchins, a security researcher credited with limiting the 2017 WannaCry outbreak, was prosecuted in the United States in connection with code he had written several years earlier for a banking trojan. He pleaded guilty in 2019 and was sentenced in 2020 to time served. The case is analytically difficult and should be presented as such: it raises genuine questions about the boundary between historical malicious activity and present legitimate research, about the treatment of young people who move from criminal to defensive work, and about the deterrent effect of prosecuting researchers who cooperate. It should not be reduced to a simple lesson.

### 4.6 Genuine Disagreement

Professional maturity requires the capacity to articulate positions one does not hold. The following are genuinely contested within the profession, and students should be able to argue both sides.

| Issue | Position A | Position B |
| :--- | :--- | :--- |
| Full disclosure of unpatched vulnerabilities | Public disclosure forces vendor action and informs defenders | It arms attackers and endangers users who cannot patch |
| Scope breadth in bug bounty programmes | Broad scope attracts researchers and finds more | Narrow scope keeps organizational risk manageable |
| Unauthorized research ("grey hat") | Produces findings that would otherwise go undiscovered | It is a crime; beneficial outcome does not create consent |
| AI-assisted vulnerability discovery | Accelerates remediation and lowers cost of defence | Lowers the barrier to offence more than to defence |
| Active defence ("hacking back") | Deters attackers and provides attribution | Unlawful in most jurisdictions; risks escalation against innocent intermediaries |

### 4.7 Chapter Summary

Ethics in security is a matter of framework rather than intuition, because the dilemmas are constructed to make the wrong choice feel right. The three classical frameworks converge on most practical cases and diverge instructively on disclosure. The four-question procedure is a conservative screen whose fourth question is a pre-commitment about reporting. Disclosure obligations run in three directions — coordinated disclosure to vendors, upstream notification for third-party findings, and immediate self-disclosure of error — and the last is the defining test of professional integrity.

**[Self-Assessment 4]** Questions 15–20, Appendix E.

---

## Chapter 5 — Methodologies and Standards

**[Objective]** After this chapter the reader should be able to: (1) name the principal security-assessment frameworks and their scope; (2) explain why they are complementary rather than competing; (3) map a single finding into multiple frameworks; (4) select an appropriate framework for a stated engagement type.

### 5.1 The Framework Landscape

| Framework | Issuer / origin | Scope | Structure | Principal use |
| :--- | :--- | :--- | :--- | :--- |
| **PTES** | Penetration Testing Execution Standard (community) | End-to-end engagement | Seven phases | Structuring an engagement |
| **OWASP WSTG** | OWASP Foundation | Web applications | Test categories and cases | Web application testing |
| **MITRE ATT&CK** | MITRE | Adversary behaviour | Tactics → techniques → sub-techniques | Threat modelling, detection engineering, reporting |
| **Cyber Kill Chain** | Lockheed Martin | Attack progression | Seven stages | Narrative communication |
| **NIST SP 800-115** | NIST | Technical security testing | Assessment, examination, testing | Regulated and public-sector environments |
| **OSSTMM** | ISECOM | Operational security measurement | Quantified metrics | Measurement-oriented assessment |
| **TIBER-EU** | European Central Bank | Threat-led penetration testing | Intelligence-led red team | Financial-sector resilience testing |
| **CBEST** | Bank of England | Threat-led penetration testing | Intelligence-led red team | UK financial sector |
| **ISO/IEC 27001 / 27002** | ISO/IEC | Management system and controls | Control catalogue | Governance and certification |
| **ISO/IEC 29147 / 30111** | ISO/IEC | Vulnerability disclosure and handling | Process standards | Disclosure programmes |
| **PCI DSS** | PCI SSC | Payment card environments | Requirements incl. penetration testing (Req. 11) | Regulated cardholder environments |

### 5.2 Complementarity, Not Competition

Students routinely ask which framework is "correct." The question misapprehends the purpose of frameworks. Each answers a different question.

- **PTES** answers: *how do I run an engagement from contract to report?*
- **OWASP WSTG** answers: *what should I test on this web application?*
- **ATT&CK** answers: *how do I describe what an adversary does, in a vocabulary a SOC can act on?*
- **Kill Chain** answers: *how do I narrate an attack to a non-specialist audience?*
- **NIST SP 800-115** answers: *what does a defensible testing programme look like in a regulated environment?*
- **OSSTMM** answers: *how do I measure security rather than assert it?*
- **TIBER-EU / CBEST** answer: *how do I test resilience against a specific, intelligence-defined adversary?*

A professional uses several in the same engagement: PTES for the engagement structure, WSTG for the web scope, ATT&CK for the reporting taxonomy, and the Kill Chain for the executive narrative.

### 5.3 PTES Phases

PTES defines seven phases, and the course's lab sequence follows them closely with one addition.

1. Pre-engagement interactions
2. Intelligence gathering
3. Threat modelling
4. Vulnerability analysis
5. Exploitation
6. Post-exploitation
7. Reporting

The course inserts **lateral movement and persistence** as explicit sub-phases of post-exploitation, because in practice they are where engagement risk concentrates and where cleanup obligations attach.

### 5.4 ATT&CK and the Value of a Shared Vocabulary

ATT&CK's contribution is not a methodology but a **shared vocabulary**. Before ATT&CK, an assessor's report described an intrusion in tool terms ("Meterpreter session obtained via vsftpd backdoor") which a SOC could not act on. With ATT&CK, the same finding is described as Initial Access via T1190 (Exploit Public-Facing Application), followed by Execution and Persistence techniques, each of which maps to a detection opportunity.

**[Exercise 5.1 — Cross-framework mapping]** Select a finding from a course lab and describe it in the language of PTES, ATT&CK, and the Kill Chain. Then state which detection opportunity the ATT&CK mapping reveals. Model answer in Appendix E.

| Framework | Representation of the vsftpd backdoor finding |
| :--- | :--- |
| PTES | Phase 5 (Exploitation) — remote root via a supply-chain backdoor |
| OWASP WSTG | Not applicable — not a web-application finding |
| ATT&CK | Initial Access: T1190; Execution: T1059 (Command and Scripting Interpreter) |
| Kill Chain | Exploitation → Installation → Actions on Objectives |
| NIST SP 800-115 | Testing phase — penetration testing technique |

### 5.5 Chapter Summary

Frameworks are instruments, not doctrines. PTES structures engagements; WSTG enumerates web tests; ATT&CK supplies an action-oriented vocabulary; the Kill Chain supplies a narrative; NIST and ISO supply regulatory and governance alignment; TIBER-EU and CBEST supply intelligence-led resilience testing. The professional skill is selection and translation, not allegiance.

**[Self-Assessment 5]** Questions 21–24, Appendix E.

---

## Chapter 6 — Assessment Typology

**[Objective]** After this chapter the reader should be able to: (1) distinguish the principal assessment types by goal, depth, attacker simulation, and output; (2) select an appropriate type for a stated client objective; (3) recognize and correct the most common client misrequest.

### 6.1 Typology

| Type | Goal | Depth | Adversary simulation | Output | Typical buyer question |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Vulnerability assessment | Enumerate weaknesses | Broad, shallow | None | Finding inventory with severity | "What is wrong with our estate?" |
| Penetration test | Demonstrate exploitability and impact | Targeted, deep | Scoped | Findings with PoCs and remediation | "Can someone get in, and how far?" |
| Red team engagement | Test detection and response | Objective-based, stealthy | Full | Objective narrative plus detection gaps | "Would we know, and could we respond?" |
| Purple team | Improve detection collaboratively | Collaborative | Integrated | Detection coverage improvements | "How do we get better at detecting?" |
| Bug bounty | Crowdsourced discovery | Variable | Within programme scope | Individual reports | "How do we get more eyes cheaply?" |
| Tabletop exercise | Test decision-making | Discussion-based | None | After-action report | "Would our leadership cope?" |
| Threat-led (TIBER-EU, CBEST) | Test resilience against a defined adversary | Intelligence-led, stealthy | Specific threat actor | Resilience assessment | "Could a specific adversary succeed?" |

### 6.2 The Most Common Client Misrequest

Clients request penetration tests when they want vulnerability assessments, and request red teams when they want penetration tests. The distinction matters commercially and technically: a vulnerability assessment is broader and cheaper; a red team is narrower and more expensive, and produces a different output.

The professional obligation is to **correct the request and document the correction**, not to fulfil it. Fulfilling a misrequest produces a deliverable that does not answer the client's actual question, and the client will discover this at the worst possible moment.

**[Exercise 6.1 — Request triage]** For each client statement, recommend an assessment type and justify the recommendation. Model answers in Appendix E.

| Client statement | Recommendation | Justification |
| :--- | :--- | :--- |
| "We want to know whether our SOC would catch a real attack" | Red team | The question is detection and response, not vulnerability inventory |
| "We need a list of everything wrong with our external perimeter" | Vulnerability assessment | Breadth over depth; exploitability not required |
| "We want to prove to our board that our new application is secure" | Penetration test | Requires demonstrated exploitability and a remediation roadmap |
| "We want to improve our detection rules for lateral movement" | Purple team | Collaborative detection engineering |
| "We have a limited budget and want independent review of our web application" | Targeted pentest or bug bounty | Cost-driven; scope discipline is critical in either case |

### 6.3 Chapter Summary

Assessment types differ in goal, depth, simulation fidelity, and output. The client's stated request frequently mismatches their underlying question. Correcting the mismatch is part of the professional service, and the correction must be documented.

**[Self-Assessment 6]** Questions 25–27, Appendix E.

---

## Chapter 7 — The Engagement Lifecycle

**[Objective]** After this chapter the reader should be able to: (1) sequence the phases of a full engagement; (2) state the entry and exit criteria for each phase; (3) identify the phases at which legal and ethical risk concentrates.

### 7.1 The Lifecycle

```
Pre-engagement and scoping
        ↓
Reconnaissance (passive → active)
        ↓
Vulnerability discovery
        ↓
Exploitation (initial access)
        ↓
Post-exploitation and privilege escalation
        ↓
Lateral movement and pivoting
        ↓
Persistence (maintaining access)
        ↓
Proof of concept and reporting
        ↓
Remediation support
        ↓
Retest and verification
```

### 7.2 Phase Gates

Each phase has an entry criterion and an exit criterion. Engagements fail when phases begin without their entry criteria satisfied.

| Phase | Entry criterion | Exit criterion | Concentrated risk |
| :--- | :--- | :--- | :--- |
| Pre-engagement | Client contact established | Four instruments executed; kick-off held | **Legal** — authorization, scope, third-party exclusions |
| Reconnaissance | Signed authorization; source IPs allowlisted | Asset inventory and service map produced | **Legal** — out-of-scope discovery; **privacy** — OSINT on individuals |
| Vulnerability discovery | Reconnaissance complete | Findings triaged and validated | **Technical** — false positives; scan-induced outage |
| Exploitation | Vulnerability hypotheses validated; RoE permits | Access demonstrated with minimal PoC | **Technical** — unintended state change; **ethical** — over-exploitation |
| Post-exploitation | Foothold established | Privilege level and impact established | **Privacy** — exposure to unrelated sensitive data |
| Lateral movement | Pivot host compromised; internal range authorized | Internal reach demonstrated | **Scope** — pivoting beyond authorized range |
| Persistence | Written authorization for persistence obtained | Mechanism installed, verified, and documented for removal | **Ethical and contractual** — residual access |
| Reporting | All testing ceased; artifacts removed | Report delivered; attestation signed | **Confidentiality** — report as a sensitive asset |
| Remediation support | Report accepted | Client questions resolved | **Advisory** — recommendations must be feasible |
| Retest | Remediation claimed complete | Fix verified; residual risk stated | **Verification** — confirmation that the fix holds |

### 7.3 Where Risk Concentrates

Two phases concentrate risk disproportionately: **pre-engagement** (legal) and **persistence** (ethical and contractual). In pre-engagement, an error produces an unlawful engagement that no technical competence can remediate. In persistence, an error produces residual access that no report can remediate — the client is left more exposed than before testing began, by the tester.

**[Instructor Note]** Use this table as the organizing device for the whole course. Each lab session should open with the relevant row: "Today we are in the lateral movement phase. The entry criterion is that the internal range is authorized. The concentrated risk is pivoting beyond it. Here is the RoE clause that governs it."

### 7.4 Chapter Summary

The lifecycle is a sequence of gated phases. Legal risk concentrates in pre-engagement; ethical and contractual risk concentrates in persistence. Competence in the technical phases does not compensate for failure at the gates.

**[Self-Assessment 7]** Questions 28–30, Appendix E.

---

## Chapter 8 — Professional Practice

**[Objective]** After this chapter the reader should be able to: (1) describe the principal career paths and their entry requirements; (2) evaluate certifications critically; (3) describe the components of professional competence and continuing development; (4) explain the function of professional bodies and codes.

### 8.1 Career Paths

| Role | Focus | Typical entry route | Principal skill |
| :--- | :--- | :--- | :--- |
| Penetration tester | Scoped engagements and reporting | SOC analyst, junior tester | Structured methodology and clear writing |
| Red team operator | Adversary simulation, detection evasion | Experienced pentester | Objective-driven planning and operational security |
| Security consultant | Advisory, assessment, remediation | Analyst or engineer | Communication and commercial judgement |
| Bug bounty researcher | Independent discovery | Self-directed | Depth in a specific technology class |
| SOC analyst | Detection and response | Entry-level security | Triage and investigation |
| Security engineer | Control design and implementation | Systems administration, development | Engineering discipline |
| Application security engineer | Secure SDLC, code review | Development plus security | Code literacy |
| Governance, risk and compliance | Policy, risk, assurance | Audit or legal | Regulatory literacy |

### 8.2 Certifications: A Critical Assessment

| Certification | Level | What it evidences | What it does not evidence |
| :--- | :--- | :--- | :--- |
| CompTIA Security+ | Entry | Broad conceptual foundation | Practical testing capability |
| CompTIA PenTest+ | Entry–mid | Methodology and reporting | Depth of hands-on skill |
| CEH (EC-Council) | Entry–mid | Breadth of terminology; HR recognition | Practical competence; widely criticized on this ground |
| OSCP (OffSec) | Mid | Hands-on exploitation under time pressure | Reporting quality; client communication |
| OSWE / OSWA (OffSec) | Mid | Web exploitation depth | Infrastructure testing |
| CRTP / CRTO (Zero-Point Security) | Mid–senior | Active Directory attack and red-team tradecraft | Breadth |
| GPEN (SANS) | Mid | Methodology with strong training component | Independent of training cost |
| CISSP (ISC2) | Senior | Management and architectural breadth | Any testing capability |
| CREST / CHECK (UK) | Organizational | Company and individual accreditation for regulated work | Individual technical depth in isolation |

Two observations are worth stating plainly to students. First, **certifications are gatekeepers, not competence**: they determine who gets an interview, not who succeeds in one. Second, **a documented portfolio outperforms a certificate in technical interviews**: a candidate who can present a redacted report with a reproducible PoC, a defensible risk rating, and a specific remediation will generally outperform a candidate who can present only a credential. The reports produced in this course constitute such a portfolio.

### 8.3 Competence and Continuing Development

Professional competence in this field has four components, and certification typically addresses only the first.

1. **Technical capability** — the ability to execute the work.
2. **Methodological discipline** — the ability to structure, document, and defend the work.
3. **Communication** — the ability to render the work useful to technical and executive audiences.
4. **Judgement** — the ability to recognize when to stop, refuse, escalate, or disclose.

The fourth component is the one that distinguishes senior practitioners and the one that no examination measures well. It is developed through supervised practice, case review, and the experience of consequences.

### 8.4 Professional Bodies and Codes

| Body / standard | Function |
| :--- | :--- |
| ISC2 Code of Ethics | Canonical professional ethics framework; binding on members |
| EC-Council Code of Ethics | Binding on CEH holders |
| CREST | International accreditation for technical security services |
| NCSC CHECK (UK) | Accreditation for UK government work |
| (ISC)2, ISACA, CIISec | Professional membership, CPD, and standards |
| PTES, OWASP | Methodology and community standards |
| Client contracts and NDAs | Legally binding; take precedence where they conflict with general codes |

### 8.5 Chapter Summary

Career paths are varied and entry routes are not uniform. Certifications function as gatekeepers; portfolios function as evidence. Competence has four components, of which judgement is the most valuable and least examinable. Professional codes establish obligations that run beyond the client relationship.

**[Self-Assessment 8]** Questions 31–33, Appendix E.

---

## Chapter 9 — Case Studies

**[Objective]** After this chapter the reader should be able to: (1) analyse security incidents for control failures rather than proximate causes; (2) identify the point at which a decision was available; (3) apply the four-question procedure retrospectively to real decisions.

### 9.1 Method

Each case is analysed on four dimensions: **what happened**, **which control failed**, **at what point a different decision was available**, and **what the case teaches about boundary discipline**. Students should resist the temptation to treat cases as cautionary tales about attackers; in almost every case the instructive failure is institutional or professional.

### 9.2 Case: TalkTalk (2015)

**What happened.** A SQL injection vulnerability in a web page enabled attackers to access customer data affecting approximately 157,000 customers. The UK Information Commissioner's Office fined the company £400,000 in 2016, citing failures to implement basic security measures against a well-known attack class.

**Control failure.** Input validation at the application layer, and patch management across an estate that had acquired technical debt through acquisition.

**Available decision point.** The vulnerability class was known and had been publicly documented for over a decade. The decision available was investment in application security before incident.

**Teaching point.** The proximate cause was an attacker's SQL injection. The instructive failure was an institutional failure to treat a known, well-understood vulnerability class as a managed risk. This is the most common pattern in breach case law.

### 9.3 Case: Equifax (2017)

**What happened.** An unpatched instance of Apache Struts (CVE-2017-5638) was exploited, exposing personal data of approximately 147 million individuals. A patch had been available for months before exploitation.

**Control failure.** Asset inventory and patch management: the vulnerable system was not identified as requiring the patch.

**Available decision point.** Patch release, months before exploitation.

**Teaching point.** The failure was not a failure to know about the vulnerability. It was a failure of asset inventory — the organization could not patch a system it did not know it had. Asset inventory is the least glamorous control in security and is implicated in a large proportion of breaches.

### 9.4 Case: Capital One (2019)

**What happened.** A misconfigured web application firewall was exploited via server-side request forgery to obtain credentials, which were then used to access cloud storage containing data on approximately 106 million individuals. The perpetrator was convicted in 2022.

**Control failure.** Cloud configuration management and least privilege on the instance metadata service.

**Available decision point.** Configuration review at deployment, and privilege scoping at design.

**Teaching point.** The vulnerability was not in code but in configuration. As infrastructure has moved to cloud platforms, the proportion of findings that are configuration rather than code defects has increased substantially. This has direct implications for what an assessor should test and what a report should emphasize.

### 9.5 Case: SolarWinds (2020)

**What happened.** Malicious code inserted into a widely deployed network management product's build pipeline was distributed to thousands of customers, including U.S. government agencies.

**Control failure.** Build-pipeline integrity and supply-chain assurance.

**Available decision point.** Build-system access control, reproducible builds, and dependency integrity verification.

**Teaching point.** The supply chain is an attack surface, and it is one that most organizations cannot assess from the outside. This case is the standard justification for software bill of materials, build attestation, and vendor assurance programmes.

### 9.6 Case: MOVEit (2023)

**What happened.** A zero-day SQL injection vulnerability in a managed file transfer product was exploited at scale, with data from a large number of downstream organizations exfiltrated through a single upstream compromise.

**Control failure.** Vendor vulnerability management and downstream dependency concentration.

**Available decision point.** Data-flow mapping: understanding which third parties hold your data and through which mechanisms.

**Teaching point.** Concentration risk. An organization can have excellent security and still be breached through a widely used supplier. This is why third-party risk management is a security control and not a procurement formality.

### 9.7 Case: *United States v. Sullivan* (2022)

Analysed in §4.4. The teaching point bears restating in this context: the conviction was for the **handling** of the incident, not for the incident. The decision point was the moment of discovery.

### 9.8 Cross-Case Observations

| Observation | Supporting cases |
| :--- | :--- |
| Known vulnerability classes, unmanaged | TalkTalk, Equifax |
| Configuration rather than code defects | Capital One, MOVEit (partly) |
| Asset and data-flow visibility as the binding constraint | Equifax, MOVEit |
| Institutional rather than individual failure | All of the above |
| Concealment as a separate and graver offence | Sullivan |
| Supply chain as an irreducible external dependency | SolarWinds, MOVEit |

**[Exercise 9.1 — Decision-point analysis]** Select one case. Identify every point at which a decision was available, the party who held it, and the cost of taking the alternative at that moment. Present in five minutes. The exercise is graded on the identification of decision points, not on the apportionment of blame.

### 9.9 Chapter Summary

Case analysis is most useful when it locates decision points rather than assigning blame. Across the cases examined, the recurring failures are visibility, configuration management, and institutional prioritization — not a shortage of attacker capability. The Sullivan case establishes that the handling of an incident carries independent and severe legal exposure.

---

## Appendix A — Glossary

| Term | Definition |
| :--- | :--- |
| Attack surface | The set of all reachable entry points to a system, including technical, human, and supply-chain vectors |
| Authorization letter | A signed instrument from a party with authority granting permission to test named systems within a named window |
| Black box / white box / grey box | Testing conducted without, with full, or with partial knowledge of the target |
| Bug bounty | A programme rewarding researchers for reporting vulnerabilities within a defined scope |
| CBEST | Bank of England threat-led penetration testing framework |
| Coordinated disclosure | Private notification to a vendor followed by publication after an agreed period |
| CVE | A standardized identifier for a publicly disclosed vulnerability |
| CVSS | A framework for scoring the technical severity of a vulnerability |
| Cyber Kill Chain | A seven-stage model of attack progression |
| Ethical hacking | Authorized adversarial testing with minimization of harm and complete disclosure |
| Exploit | A technique or artifact that leverages a vulnerability |
| Grey hat | An unauthorized actor with non-malicious intent; unlawful in most jurisdictions |
| Lateral movement | Movement from one compromised host to others within a network |
| MITRE ATT&CK | A knowledge base of adversary tactics and techniques |
| NDA | Non-disclosure agreement |
| OSINT | Open-source intelligence |
| OWASP WSTG | OWASP Web Security Testing Guide |
| Payload | The action executed after successful exploitation |
| Persistence | A mechanism that maintains access across sessions, reboots, or credential changes |
| Pivot | Use of a compromised host as a routing point to reach otherwise unreachable systems |
| PoC | Proof of concept; a reproducible demonstration that a finding is real |
| PTES | Penetration Testing Execution Standard |
| Purple team | Integrated offensive and defensive activity aimed at improving detection |
| Red team | Objective-based adversary simulation focused on detection and response |
| RoE | Rules of engagement; the operational boundaries of an engagement |
| Scope | The set of assets and techniques explicitly authorized |
| SOW | Statement of work |
| TIBER-EU | European Central Bank threat-led penetration testing framework |
| Threat actor | An entity with intent and capability to conduct an attack |
| Vulnerability | A weakness that could be exploited to violate a security property |
| Vulnerability assessment | Broad, shallow enumeration of weaknesses without demonstration of exploitability |
| Zero-day | A vulnerability for which no patch exists at the time of use |

---

## Appendix B — Authorization Letter Template

```
[CLIENT LETTERHEAD]

AUTHORIZATION TO CONDUCT SECURITY TESTING

Date: [must precede the testing window]

To: [Assessor name], [Assessor organization]

1. Authorizing entity
   [Full legal name of the entity that owns the systems]

2. Authorizing individual
   Name: [ ]
   Title: [ ]
   I confirm that I hold authority to grant the permissions set out below
   on behalf of the authorizing entity.

3. Authorized assets
   [Exhaustive list of domains, IP ranges, applications, and accounts]

4. Explicitly excluded assets
   [Third-party infrastructure, subsidiaries, shared hosting, payment
   systems, and any other exclusion]

5. Authorized techniques
   [Reconnaissance / scanning / exploitation / privilege escalation /
   lateral movement / persistence — with constraints]

6. Prohibited techniques
   [Denial of service / social engineering / physical access / any other]

7. Testing window
   From: [date, time, timezone]
   To:   [date, time, timezone]
   Blackout periods: [dates and times]

8. Emergency stop
   Contact: [name, role, telephone, available 24/7 during the window]
   Method: [telephone, followed by written confirmation]

9. Governing documents
   Statement of Work dated [ ], Rules of Engagement version [ ]

10. Signature
    ______________________________  Date: ____________

[Assessor countersignature]
```

---

## Appendix C — Rules of Engagement Template

```
RULES OF ENGAGEMENT

Engagement ID:      [ ]
Client:             [legal entity]
Assessor:           [organization]
Authorization ref:  [date and signatory of the authorization letter]
Scope ref:          [scope document version]

1.  Permitted techniques            [table]
2.  Prohibited techniques           [explicit list]
3.  Testing windows                 [dates, times, timezone, blackouts]
4.  Assessor source IP addresses    [list, for allowlisting and log correlation]
5.  Communication protocol          [daily update; critical finding notification]
6.  Escalation procedure            [live attacker; sensitive data; outage]
7.  Data handling                   [storage, redaction standard, retention, destruction]
8.  Cleanup and restoration         [artifact inventory; attestation; client verification]
9.  Limitations and exclusions      [what is not being tested and why]
10. Signatures
```

---

## Appendix D — Decision Framework Worksheet

For each proposed action, complete all four rows. Any negative or uncertain answer requires suspension and escalation.

| Question | Assessment | Evidence |
| :--- | :--- | :--- |
| 1. Authorization — do I hold explicit written permission for this specific action, from a party with authority, within a current window? | | |
| 2. Necessity — is this the minimum action sufficient to establish the finding? | | |
| 3. Harm — who could be harmed, and has that harm been minimized? | | |
| 4. Disclosure — will I report this action honestly, including unintended consequences? | | |

---

## Appendix E — Self-Assessment Answer Key

**Chapter 1**
1. The "permission" definition specifies only a necessary condition and omits the obligations of minimization and disclosure, which are independent of authorization.
2. Authorization, minimization, disclosure. Minimization is most often neglected in practice.
3. A vulnerability is a weakness; an exploit is a technique or artifact that leverages it.
4. Educational intent is not a legal defence; authorization is the operative element.
5. Because intent does not create consent, and the system owner did not authorize the risk.

**Chapter 2**
6. Actor attributes determine which controls will hold; a control set for a script kiddie differs from one for a nation-state.
7. Likelihood is the probability of being targeted; impact is the consequence. Organized crime is the likeliest adversary for a mid-sized firm; a nation-state is the most dangerous but least likely.
8. It is unauthorized access; disclosure does not retroactively create authorization.
9. It conflates legal and ethical status, implies a binary, and omits the negligent insider.

**Chapter 3**
10. Because the legal consequence of crossing the boundary is severe and irreversible.
11. If you are not certain you are authorized, you are not authorized; the asymmetry of consequences justifies the caution.
12. Verbal permission, email from a mid-level manager, corporate ownership, and educational purpose.
13. The subsidiary is a separate legal person that has not consented.
14. A client can authorize their own tenancy but not shared infrastructure or other tenants.

**Chapter 4**
15. Authorization, necessity, harm, disclosure.
16. Suspend and escalate.
17. It tests whether the practitioner will disclose an error that reflects badly on them; the obligation is absolute and admits no balancing.
18. Because professional maturity requires the capacity to argue positions one does not hold.
19. Canon 1: obligations to society precede obligations to principals.
20. Immediate, complete, documented disclosure to the authorizing party.

**Chapter 5**
21. Pre-engagement, intelligence gathering, threat modelling, vulnerability analysis, exploitation, post-exploitation, reporting.
22. ATT&CK is a knowledge base of adversary behaviour; the Kill Chain is a seven-stage model of attack progression.
23. Each answers a different question — structure, enumeration, vocabulary, narrative, regulation, measurement.
24. PTES for engagement structure; ATT&CK for reporting taxonomy; Kill Chain for executive narrative.

**Chapter 6**
25. A vulnerability assessment enumerates weaknesses broadly; a penetration test demonstrates exploitability deeply.
26. A red team tests detection and response against an objective; a pentest demonstrates exploitability against a scope.
27. Purple team is collaborative by design because its purpose is detection improvement, which requires shared visibility between offence and defence.

**Chapter 7**
28. Pre-engagement. Legal error cannot be remediated by technical competence.
29. Persistence. Residual access is a contractual and ethical failure that no report can remediate.
30. See §7.2 — every phase has an entry criterion and an exit criterion, and engagements fail when phases begin without the entry criterion satisfied.

**Chapter 8**
31. A pentester executes scoped engagements with reporting; a red team operator runs objective-based adversary simulations emphasizing stealth and detection.
32. Certifications determine who gets an interview; skills and portfolio determine who succeeds in it.
33. Technical capability, methodological discipline, communication, judgement — judgement is the least examinable and most valuable.

---

## Appendix F — Primary Sources and Further Reading

**Standards and frameworks**
- PTES — Penetration Testing Execution Standard, pentest-standard.org
- OWASP Web Security Testing Guide, owasp.org
- MITRE ATT&CK, attack.mitre.org
- NIST SP 800-115, *Technical Guide to Information Security Testing and Assessment*
- ISO/IEC 27001, 27002, 29147, 30111
- ISECOM, *Open Source Security Testing Methodology Manual* (OSSTMM)
- European Central Bank, *TIBER-EU Framework*
- Bank of England, *CBEST Intelligence-Led Testing*
- PCI Security Standards Council, *PCI DSS* (Requirement 11)

**Law and policy**
- Computer Fraud and Abuse Act, 18 U.S.C. § 1030
- *Van Buren v. United States*, 593 U.S. 374 (2021)
- *United States v. Morris*, 928 F.2d 504 (2d Cir. 1991)
- Computer Misuse Act 1990 (UK); *R v Gold and Schifreen* [1988] AC 1063
- Directive 2013/40/EU; Directive (EU) 2022/2555 (NIS2)
- Cybercrimes (Prohibition, Prevention, etc.) Act 2015 (Nigeria, as amended)
- Council of Europe Convention on Cybercrime, ETS 185, and Second Additional Protocol (2022)

**Ethics and professional standards**
- ISC2 Code of Ethics
- EC-Council Code of Ethics
- *United States v. Sullivan*, N.D. Cal. (2022)

**Incident case material**
- UK Information Commissioner's Office, monetary penalty notice, TalkTalk Telecom Group plc (2016)
- U.S. House Committee on Oversight and Reform, *The Equifax Data Breach* (2018)
- U.S. Department of Justice, press release, Capital One intrusion prosecution (2022)
- Public reporting on SolarWinds (2020) and MOVEit (2023)

---

## Instructor's Closing Note

The purpose of this volume is not to make students cautious. Caution is a by-product. The purpose is to make students **legible** — able to explain, in the vocabulary of the profession, why they did what they did, on whose authority, with what restraint, and with what disclosure.

A practitioner who cannot do that is not a junior professional awaiting experience. They are a practitioner whose work cannot be relied upon, because it cannot be audited. The technical labs in this course will teach you to obtain a shell. This volume exists to ensure that when you obtain one, you know precisely what you are permitted to do with it, what you must not do, and what you are obliged to report — including, and especially, when the report is inconvenient for you.

That obligation is the whole of the discipline.