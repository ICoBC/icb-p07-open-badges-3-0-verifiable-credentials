<!--
author:   ICoBC - International Council on Badges and Credentials
email:    info@icobc.net
version:  1.0.0
language: en
narrator: UK English Female
comment:  A hands-on lab in which you issue, inspect, verify and revoke Open Badges 3.0 credentials in a sandbox and diagnose common interoperability errors.

@style
:root { --icobc-navy:#02375B; --icobc-orange:#F78222; --icobc-cyan:#5DCAE7; --icobc-lime:#B1CF37; --icobc-mist:#F1F5F8; --icobc-line:#D8E2E9; --icobc-muted:#4F6576; }
body { font-family: "Open Sans", Arial, sans-serif; }
h1, h2, h3, h4 { color: var(--icobc-navy); }
a { color: var(--icobc-navy); }
table th { background: var(--icobc-mist); color: var(--icobc-navy); }
blockquote { border-left: 4px solid var(--icobc-orange); background: var(--icobc-mist); padding: 8px 16px; }
@end
-->

# Open Badges 3.0 and Verifiable Credentials: Hands-on Lab

*Issue, inspect, verify and revoke standard credentials in a sandbox.*

## About this course

**Course ID:** ICB-P07
**Framework alignment:** ICoBC Credentialing Skills Framework (ICSF), skill STND "Standards and interoperability" (VRITE pillar: Trustworthiness), level L2 "Operate", stage A "Ability".

At this level you issue and verify standard credentials with existing tools, and you check conformance with test tools. This is an Ability course: you practise on realistic tasks in a controlled setting, a sandbox, using knowledge you already have from the prerequisite course.

### Who this course is for

- HR and learning technology owners who commission or run credential programmes in a corporate academy or HR department.
- Education IT and credential operations staff at universities, colleges and training providers.
- Members of the standards and wallet community who want hands-on experience with the credential formats.

**Prerequisite:** ICB-F01 Digital Badges and Credentials Essentials.

### Learning outcomes

After this course you can:

1. Issue an Open Badges 3.0 credential in a sandbox and inspect its structure.
2. Explain how Open Badges 3.0 relates to the W3C Verifiable Credentials data model.
3. Verify credentials, including status and expiry, with verification and conformance tools.
4. Diagnose common interoperability errors.

### Workload and format

The notional workload is 8 hours. This file covers the self-paced part: six modules, each with a short tour of the topic, a worked example, a practice activity and a quiz. Live or workshop elements appear as facilitator notes. You work in a sandbox, so you never touch production keys, real learner data or live registries.

### How the course is assessed

You keep a **lab record** while you work through the modules. The record contains the credential files you issue, export, verify and revoke, plus your diagnostic answers for three faulty samples. A person assesses the lab record with the rubric in the section "Assessment and badge". The final knowledge check in that section is a formative check of your understanding. The file does not grade your lab record.

### Badge

When you pass, you receive the badge "Open Badges 3.0 and Verifiable Credentials: Hands-on Lab (Ability, L2)", alignment code ICSF-STND-L2-A. The badge records that you completed the assessed tasks in this course. It does not prove that you are competent in any particular job.

### Outcomes, modules and assessment

| Outcome | Module | How it is assessed |
|---|---|---|
| 1. Issue an Open Badges 3.0 credential in a sandbox and inspect its structure | Data model tour; Issuing in the sandbox | Lab record: issued credential file and annotated structure; module quizzes |
| 2. Explain how Open Badges 3.0 relates to the W3C Verifiable Credentials data model | Data model tour; Proofs and keys | Lab record: short written explanation; module quizzes; final knowledge check |
| 3. Verify credentials, including status and expiry, with verification and conformance tools | Status, expiry and revocation; Verification and conformance | Lab record: export, verify and revoke log with tool results |
| 4. Diagnose common interoperability errors | Troubleshooting | Lab record: diagnostic answers for three faulty samples |

### The lab record

Create a folder called `lab-record` on your computer. Inside it, make these items as you go:

- `issued/`: credential files you issue.
- `exports/`: files you export from the sandbox.
- `verification-log.md`: your notes on each verification and conformance check.
- `diagnostics.md`: your answers for the three faulty samples.
- `reflection.md`: a short note on what you would check before using a tool in production.

> **Safety rule for the whole lab.** Use only sandbox keys and fictional people. Never paste a private key, a real learner record or a production secret into any tool, including an AI assistant.

<details>
<summary>Facilitator notes</summary>

**Live element (about 60 minutes, optional):** Open with a short walk-through of the lab record folder. Agree one shared sandbox for the group and confirm that every participant can sign in. Check that no one uses real personal data. Pair participants of different backgrounds, for example one HR owner with one IT person, so that each can explain their own view of a credential.

**Preparation:** Provide a sandbox issuer, a verifier tool and a conformance test tool that you have tested in advance. Keep the names of tools in your own course instructions, because this file stays vendor-neutral. Prepare three faulty sample credentials for the Troubleshooting module and keep an answer sheet for assessors.

</details>

## Data model tour

### What you will do in this module

You will look at a credential as structured data. You will name its main parts, place Open Badges 3.0 on the W3C Verifiable Credentials data model, and read a small sample file line by line.

Time: about 75 minutes.

### Credentials are data with a purpose

A credential is a set of statements that an issuer makes about a subject. The statements need a shape so that other systems can read them. A shared data model gives that shape. When two systems share a model, a verifier can read a credential from an issuer it has never met.

Open Badges 3.0 is a specification for credentials that describe achievements, such as completing a course, passing an assessment or holding a skill. Comprehensive Learner Record (CLR) 2.0 is a related specification that bundles several achievements into one record. Both are current specifications. Platform support is still uneven, so you should check the conformance certification of any tool before you rely on it.

### How Open Badges 3.0 relates to Verifiable Credentials

The W3C Verifiable Credentials Data Model 2.0 is a W3C Recommendation, published in 2025. It defines a general way to express claims, who issued them, who they are about, and how to secure them. It does not say anything about badges, courses or skills. It is a general layer.

Open Badges 3.0 sits on top of that layer. It uses the Verifiable Credentials structure and adds terms that fit achievements: for example an achievement, its criteria, and the result a learner earned. In practice, an Open Badges 3.0 credential is a Verifiable Credential whose subject has an achievement.

{{1}}
<svg viewBox="0 0 800 450" width="100%" role="img" xmlns="http://www.w3.org/2000/svg">
  <title>Layer diagram: Open Badges 3.0 on the Verifiable Credentials data model</title>
  <desc>Three stacked layers. The top layer is Open Badges 3.0 and CLR 2.0, which add achievement terms. The middle layer is the W3C Verifiable Credentials data model, which defines issuer, subject, claims and proof. The bottom layer is the securing mechanism and status list, which protect the credential and report its status. Arrows show that each layer builds on the one below.</desc>
  <rect x="0" y="0" width="800" height="450" fill="#FFFFFF"/>
  <rect x="120" y="40" width="560" height="100" rx="6" fill="#5DCAE7" stroke="#02375B" stroke-width="2"/>
  <text x="400" y="82" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="20" font-weight="700" fill="#02375B">Open Badges 3.0 and CLR 2.0</text>
  <text x="400" y="112" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B">Achievement, criteria, result, issuer profile</text>
  <rect x="120" y="170" width="560" height="100" rx="6" fill="#F1F5F8" stroke="#02375B" stroke-width="2"/>
  <text x="400" y="212" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="20" font-weight="700" fill="#02375B">W3C Verifiable Credentials data model 2.0</text>
  <text x="400" y="242" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B">Issuer, subject, claims, validity dates</text>
  <rect x="120" y="300" width="560" height="100" rx="6" fill="#B1CF37" stroke="#02375B" stroke-width="2"/>
  <text x="400" y="342" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="20" font-weight="700" fill="#02375B">Securing mechanism and status</text>
  <text x="400" y="372" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B">Proof, keys, status list</text>
  <path d="M400 300 L400 272" stroke="#02375B" stroke-width="2" fill="none"/>
  <path d="M392 282 L400 270 L408 282" stroke="#02375B" stroke-width="2" fill="none"/>
  <path d="M400 170 L400 142" stroke="#02375B" stroke-width="2" fill="none"/>
  <path d="M392 152 L400 140 L408 152" stroke="#02375B" stroke-width="2" fill="none"/>
  <text x="130" y="430" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#4F6576">Each layer builds on the one below it.</text>
</svg>

### The main parts of a credential

Most Open Badges 3.0 credentials contain these parts:

- **Context:** a list of links that tell a reader which vocabularies the terms come from.
- **Type:** the kind of credential. It includes a general Verifiable Credential type and an Open Badges type.
- **Issuer:** the organisation that makes the statement, with an identifier and a name.
- **Valid from and valid until:** the dates between which the credential is meant to be accepted. The validity end date is optional.
- **Credential subject:** the person or entity the statements are about, with the achievement they earned.
- **Credential status:** a pointer that tells a verifier where to check whether the credential is still valid.
- **Proof:** the digital signature that lets a verifier detect changes.

{{2}}
A short, simplified sample follows. It uses fictional names and shortened identifiers. Real files are longer.

```json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2",
    "https://purl.imsglobal.org/spec/ob/v3p0/context-3.0.3.json"
  ],
  "type": ["VerifiableCredential", "OpenBadgeCredential"],
  "issuer": {
    "id": "https://example.org/issuers/1",
    "type": ["Profile"],
    "name": "Example Academy"
  },
  "validFrom": "2026-03-01T09:00:00Z",
  "credentialSubject": {
    "type": ["AchievementSubject"],
    "achievement": {
      "id": "https://example.org/achievements/42",
      "type": ["Achievement"],
      "name": "Safe Handling Basics",
      "criteria": { "narrative": "Complete the module and pass the quiz." }
    }
  }
}
```

<!-- VERIFY: Check the current version number in the Open Badges 3.0 context URL and the current VC context URL against the official specification pages before publishing. -->

**Worked example: Reading a corporate academy credential**

Priya is a learning technology owner in a corporate academy. Her academy wants to issue a credential called "Safe Handling Basics" to staff who finish an internal course. She opens the sample above and annotates it:

1. The issuer is the academy. She checks that the issuer name matches the legal name used in HR records.
2. The subject is the staff member. She notes that a real credential needs a way to identify the person, and that her data protection lead must approve which identifier to use.
3. The achievement has a name and a short criteria statement. She rewrites the criteria in plain language so that a hiring manager in another company can understand it.
4. There is no `credentialStatus` field. She writes in her notes that production credentials need one, so the academy can revoke a credential if a certificate was issued by mistake.

The example shows that the data model gives her a checklist of decisions, not just a file format.

**Worked example: Reading a university credential**

Tomás works in credential operations at a university. A department wants to issue a micro-credential for a short course on laboratory safety. He compares the same sample with the department's course description:

1. The achievement name in the file must match the name in the course catalogue.
2. The criteria must state the real pass condition, for example "attend all sessions and pass the practical check".
3. The validity dates need a decision: the department says the safety training expires after three years, so he adds a validity end date.
4. He notes that the issuer identifier must be a stable address under the university's control, because verifiers will use it later.

<details>
<summary>Facilitator notes</summary>

Ask participants to explain the layer diagram to a partner in one minute, using the words "general" and "specific". Check that they can say which layer defines the issuer and which defines the achievement. Common slip: participants believe Open Badges 3.0 and Verifiable Credentials are rival formats. Correct this calmly using the layer diagram.

</details>

**Practice activity: Annotate the sample**

1. Copy the sample JSON into a file called `issued/sample-annotated.json` in your lab record folder.
2. Add a separate file `annotation.md`. For each of the seven parts listed above, write one sentence: what it contains in the sample, and who is responsible for its content (the issuer, the platform or the earner).
3. List two fields that a real credential in your own context would need and that the sample leaves out. Give a reason for each.
4. Write a short paragraph (three to five sentences) that explains to a colleague how Open Badges 3.0 relates to the W3C Verifiable Credentials data model. Save it as `explanation.md`. This paragraph is evidence for outcome 2.

Self-check: your paragraph should mention that Verifiable Credentials is the general layer and Open Badges 3.0 adds achievement terms.

### Check your understanding

**Question 1.** Which statement describes the relationship between Open Badges 3.0 and the W3C Verifiable Credentials data model?

[( )] Open Badges 3.0 replaces the Verifiable Credentials data model for education.
[(X)] Open Badges 3.0 builds on the Verifiable Credentials data model and adds terms for achievements.
[( )] The two are unrelated formats that share only the word "credential".
[( )] The Verifiable Credentials data model describes only identity documents, not achievements.
[[?]] Think about which one is general and which one is specific to achievements.
****
Open Badges 3.0 is expressed using the Verifiable Credentials structure. It adds terms that describe achievements, such as criteria and results. The Verifiable Credentials data model is general and is not limited to identity documents.
****

**Question 2.** Which part of a credential tells a verifier which vocabularies the terms come from?

[( )] The proof
[( )] The credential status
[(X)] The context
[( )] The valid until date
[[?]] It is a list of links at the start of the file.
****
The context is a list of links that identify the vocabularies behind the terms. The proof protects the credential, the status points to revocation information and the dates set the validity period.
****

**Question 3.** In the sample file, who is the issuer?

[( )] The person who earned the achievement
[(X)] The organisation that makes the statements and signs the credential
[( )] The wallet that stores the file
[( )] The tool that reads the file
[[?]] Look at the field called issuer.
****
The issuer is the organisation that makes the statements. The earner is the subject. A wallet stores the file and a verifier reads it.
****

**Question 4.** Why should a production credential contain a pointer to credential status?

[( )] So that the file looks longer and more official
[( )] So that the earner can change the achievement name later
[(X)] So that a verifier can check whether the credential is still valid
[( )] So that the context can be skipped
[[?]] Think about what happens if a credential was issued by mistake.
****
The status pointer lets a verifier find out whether the credential has been revoked or suspended. It does not change the content of the credential and it does not replace the context.
****

## Issuing in the sandbox

### What you will do in this module

You will issue your first Open Badges 3.0 credential in a sandbox, export it and inspect the result. You will compare what you typed into a form with what appears in the file.

Time: about 90 minutes.

### What a sandbox is for

A sandbox is a controlled copy of an issuing environment. It uses test keys, test issuers and fictional recipients. Mistakes in a sandbox do not reach real people. Your facilitator or course instructions tell you which sandbox to use. This course names no products, so the steps below are described in general terms that apply to any conforming tool.

Before you start, check three things:

- The sandbox shows that it is a test environment.
- You have a test issuer profile, not a real organisation account.
- You have a fictional recipient identity, such as a made-up email address on a reserved example domain.

### The issuing flow

Issuing follows a sequence. Each step has a person or system responsible.

1. The issuer defines the achievement: name, description and criteria.
2. The issuer prepares the credential: it links the achievement to a recipient and sets the validity dates.
3. The issuing system signs the credential with the issuer's key.
4. The issuing system delivers the credential to the recipient, as a file, a link or into a wallet.
5. The recipient stores it and can later share it.

{{1}}
<svg viewBox="0 0 800 450" width="100%" role="img" xmlns="http://www.w3.org/2000/svg">
  <title>Issuing and verifying sequence</title>
  <desc>Four actors in columns: issuer, issuing system, earner and verifier. The issuer defines the achievement. The issuing system signs the credential. The earner receives and stores it. The verifier checks the signature, issuer and status. Arrows show the order from left to right.</desc>
  <rect x="0" y="0" width="800" height="450" fill="#FFFFFF"/>
  <rect x="20" y="40" width="170" height="70" rx="6" fill="#F78222" stroke="#02375B" stroke-width="2"/>
  <text x="105" y="82" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="16" font-weight="700" fill="#02375B">Issuer</text>
  <rect x="215" y="40" width="170" height="70" rx="6" fill="#F1F5F8" stroke="#02375B" stroke-width="2"/>
  <text x="300" y="82" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="16" font-weight="700" fill="#02375B">Issuing system</text>
  <rect x="410" y="40" width="170" height="70" rx="6" fill="#02375B" stroke="#02375B" stroke-width="2"/>
  <text x="495" y="82" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="16" font-weight="700" fill="#FFFFFF">Earner</text>
  <rect x="605" y="40" width="170" height="70" rx="6" fill="#F78222" stroke="#02375B" stroke-width="2"/>
  <text x="690" y="82" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="16" font-weight="700" fill="#02375B">Verifier</text>
  <path d="M105 110 L105 410 M300 110 L300 410 M495 110 L495 410 M690 110 L690 410" stroke="#D8E2E9" stroke-width="2" fill="none"/>
  <path d="M105 160 L296 160" stroke="#02375B" stroke-width="2" fill="none"/>
  <path d="M286 154 L298 160 L286 166" stroke="#02375B" stroke-width="2" fill="none"/>
  <text x="110" y="150" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">1 Define achievement</text>
  <path d="M300 230 L491 230" stroke="#02375B" stroke-width="2" fill="none"/>
  <path d="M481 224 L493 230 L481 236" stroke="#02375B" stroke-width="2" fill="none"/>
  <text x="305" y="220" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">2 Sign and deliver</text>
  <path d="M495 300 L686 300" stroke="#02375B" stroke-width="2" fill="none"/>
  <path d="M676 294 L688 300 L676 306" stroke="#02375B" stroke-width="2" fill="none"/>
  <text x="500" y="290" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">3 Share credential</text>
  <path d="M690 370 L304 370" stroke="#02375B" stroke-width="2" fill="none"/>
  <path d="M314 364 L302 370 L314 376" stroke="#02375B" stroke-width="2" fill="none"/>
  <text x="400" y="395" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">4 Check key and status</text>
</svg>

### Fields to fill in

Whatever tool you use, expect to supply these items:

- **Achievement name:** short and specific.
- **Description:** one or two sentences.
- **Criteria:** what the earner had to do. Write it so a stranger can judge it.
- **Recipient identifier:** in the sandbox, a fictional one.
- **Dates:** valid from, and optionally valid until.
- **Issuer details:** name and a stable identifier.

Write the criteria with care. Weak criteria such as "Good participation" give a verifier nothing to check. Strong criteria such as "Attend four of five sessions and submit the final task" are checkable.

### Inspecting what you issued

After issuing, export the credential as a file. Open it in a plain text editor. Do not trust the tool's preview alone, because the preview may hide fields. Check these points:

- The `type` list contains both a Verifiable Credential type and an Open Badges type.
- The `issuer` matches your test issuer.
- The `credentialSubject` contains the achievement you defined.
- The dates match what you entered, in a standard date and time format.
- A `proof` section exists, or the file is a signed token that carries the proof inside.

**Worked example: A corporate academy issues a compliance credential**

Lena is an HR specialist who runs a corporate academy. Each year, staff in the finance team complete an anti-fraud awareness module. Lena sets up a test achievement called "Fraud Awareness 2026" in the sandbox.

She enters criteria: "Complete the online module and score at least 80 per cent in the final check." The 80 per cent figure is illustrative. She sets a validity period of twelve months, because the content is reviewed every year. She issues a credential to a fictional employee, Test Person One, with an example email address.

Then she exports the file and opens it. She finds the validity end date and sees that the tool stored it in a standard format. She also finds that the criteria text appears under the achievement, exactly as she typed it. She adds both observations to her lab record.

**Worked example: A training provider issues a course credential**

Kofi works in credential operations at a vocational training provider. The provider offers a five-day course on workshop machinery safety. Kofi creates the achievement "Workshop Machinery Safety Certificate" in the sandbox. He sets no validity end date at first, then asks the course lead. The lead says the training should be repeated every two years, so Kofi edits the credential to add an end date.

When Kofi inspects the exported file, he notices that the recipient identifier he typed appears in the file. He raises a note for his data protection officer: in production, an email address in a shared file may reveal more than the earner intends.

<details>
<summary>Facilitator notes</summary>

Demonstrate one issuing run on a shared screen. Pause after the export and ask: "What is in the file that was not on the form?" Typical answers are the context links, the type list and the proof. Check that participants save files in the lab record folder with clear names. Remind them: sandbox only, fictional recipients only.

If a participant's sandbox fails, offer a pre-issued sample file so that they can continue with inspection and come back to issuing later.

</details>

**Practice activity: Issue and export your first credential**

1. In the sandbox, create a test achievement with a name, a description and checkable criteria for a short course in your own context (corporate or education).
2. Issue it to a fictional recipient. Set a valid from date and a valid until date.
3. Export the credential and save it as `issued/first-credential.json` (or the format your tool provides).
4. Open the file in a text editor. In `annotation-issuing.md`, list five fields in the file that you did not type into the form, and explain in one sentence what each one is for.
5. Compare the criteria text on screen with the criteria text in the file. Note any differences.

Add the credential file and your notes to the lab record.

### Check your understanding

**Question 1.** Why do you inspect the exported file rather than rely on the tool's preview?

[( )] The preview always shows more fields than the file
[(X)] The file is the actual credential, and the preview may hide or change fields
[( )] Files cannot be opened in a text editor
[( )] The preview is the only part that gets signed
[[?]] Which one travels to other systems: the preview or the file?
****
The exported file is the credential that other systems receive. A preview is only a display and may leave out technical fields such as the context, type list or proof.
****

**Question 2.** Which set of criteria is best for a credential?

[( )] "Good participation"
[( )] "Took the course"
[(X)] "Attend four of five sessions and submit the final task"
[( )] "Showed the right attitude"
[[?]] A verifier or hiring manager should be able to judge whether the criteria were met.
****
Criteria should state what the earner did in terms that others can check. Vague words such as "good" or "right attitude" give a reader nothing to verify.
****

**Question 3.** Why does the sandbox use fictional recipients?

[( )] Because credentials for real people cannot be signed
[( )] Because fictional recipients make the file smaller
[(X)] So that mistakes and test data do not reach real people
[( )] Because the specification requires fictional recipients in all credentials
[[?]] Think about what could go wrong if you tested with real learner data.
****
A sandbox is for safe practice. Using fictional data protects real people from errors and keeps personal data out of test tools.
****

**Question 4.** Kofi notices a recipient email address in the exported file. What is a sensible action?

[( )] Delete the proof so the address cannot be read
[( )] Ignore it, because all identifiers are harmless
[(X)] Raise it with the data protection officer before production use
[( )] Replace the email address with the issuer's name
[[?]] Who in an organisation decides which personal data may be shared?
****
Identifiers can reveal personal data. The decision about what to include in a production credential belongs to the organisation's data protection function. Deleting the proof or swapping in the issuer's name would damage the credential without solving the question.
****

## Proofs and keys

### What you will do in this module

You will learn what a proof does, how keys relate to an issuer, and how to inspect a proof without exposing a private key. You will also meet the idea of an AI assistant as an optional reading aid, with a clear warning.

Time: about 75 minutes.

### What a proof does

A proof is a digital signature attached to a credential. It answers two questions for a verifier:

- Did the issuer really sign this credential?
- Has anything changed since it was signed?

If someone edits a single character in a signed credential, verification fails. The signature is mathematical, so it does not rely on trust in the file's appearance.

### Key pairs

Signing uses a pair of keys:

- The **private key** stays secret with the issuer. It creates signatures.
- The **public key** is shared openly. Verifiers use it to check signatures.

Anyone can use the public key to check a signature, but only the holder of the private key can make a valid one. This is why a private key must never leave the issuer's secure environment.

{{1}}
<svg viewBox="0 0 800 450" width="100%" role="img" xmlns="http://www.w3.org/2000/svg">
  <title>Private key signs, public key verifies</title>
  <desc>The issuer holds a private key kept secret and uses it to sign the credential. The signed credential travels to the verifier. The verifier retrieves the issuer's public key from a published location and uses it to check the signature. A label shows that the private key never leaves the issuer.</desc>
  <rect x="0" y="0" width="800" height="450" fill="#FFFFFF"/>
  <rect x="40" y="60" width="200" height="140" rx="6" fill="#F78222" stroke="#02375B" stroke-width="2"/>
  <text x="140" y="100" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="18" font-weight="700" fill="#02375B">Issuer</text>
  <text x="140" y="135" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B">Private key</text>
  <text x="140" y="160" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B">(kept secret)</text>
  <rect x="300" y="100" width="200" height="60" rx="6" fill="#F1F5F8" stroke="#02375B" stroke-width="2"/>
  <text x="400" y="136" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B">Signed credential</text>
  <rect x="560" y="60" width="200" height="140" rx="6" fill="#F78222" stroke="#02375B" stroke-width="2"/>
  <text x="660" y="100" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="18" font-weight="700" fill="#02375B">Verifier</text>
  <text x="660" y="135" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B">Public key</text>
  <text x="660" y="160" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B">(checks signature)</text>
  <path d="M240 130 L296 130" stroke="#02375B" stroke-width="2" fill="none"/>
  <path d="M286 124 L298 130 L286 136" stroke="#02375B" stroke-width="2" fill="none"/>
  <text x="268" y="118" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">signs</text>
  <path d="M500 130 L556 130" stroke="#02375B" stroke-width="2" fill="none"/>
  <path d="M546 124 L558 130 L546 136" stroke="#02375B" stroke-width="2" fill="none"/>
  <text x="528" y="118" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">sent</text>
  <rect x="300" y="280" width="200" height="70" rx="6" fill="#B1CF37" stroke="#02375B" stroke-width="2"/>
  <text x="400" y="310" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B">Published public key</text>
  <text x="400" y="332" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">(open location)</text>
  <path d="M140 200 L140 315 L296 315" stroke="#02375B" stroke-width="2" fill="none" stroke-dasharray="6 4"/>
  <text x="150" y="260" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">publishes public key only</text>
  <path d="M500 315 L660 315 L660 204" stroke="#02375B" stroke-width="2" fill="none"/>
  <path d="M654 214 L660 202 L666 214" stroke="#02375B" stroke-width="2" fill="none"/>
  <text x="520" y="400" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#4F6576">The private key never leaves the issuer.</text>
</svg>

### Securing mechanisms

The Verifiable Credentials data model separates the credential content from the way it is secured. Several securing mechanisms exist, and the specifications that define them continue to evolve. Two broad styles are common:

- **Embedded proof:** the signature is a block inside the credential JSON.
- **Enveloping proof:** the whole credential is wrapped in a signed token, and the verifier unwraps it.

Open Badges 3.0 allows more than one securing approach. A tool may support only some of them. When a verifier rejects a credential, an unsupported securing mechanism is one possible reason. You will meet this again in the Troubleshooting module.

### Where the public key comes from

A verifier needs to find the issuer's public key. The credential usually names the key or points to a location, such as a document published by the issuer. If the issuer changes keys, publishes the wrong key or lets the location go offline, verification can fail even though the credential is genuine.

This links to trust. A valid signature shows that the holder of a particular key signed the credential. It does not by itself show that the key belongs to the real organisation. Verifiers therefore also look at how the issuer identifier and key are published, and may consult a registry or a trust list where one exists.

### Optional: using an AI assistant to read JSON

An AI assistant can help you read a long JSON file. You may paste a credential into one to ask, "What does this field mean?" This is optional. If you do it, follow these rules:

- Paste only sandbox files with fictional data.
- Never paste a private key, a secret, a password or a token that gives access to an issuing system.
- Remember that an assistant may be wrong. Check its answer against the specification.
- Do not paste real learner records. Under your organisation's data protection rules, doing so may be a breach.

A public credential contains no private keys, but a configuration file, an export from an issuing system or a key file may. Always read a file yourself before sharing it.

**Worked example: A corporate academy handles keys**

Amira leads learning technology for a corporate academy. The academy's issuing system holds a signing key. A colleague asks Amira to send the "key file" to a contractor who wants to help debug a verification error. Amira refuses to send it. Instead she:

1. Exports a sample credential from the sandbox, which contains only the public parts.
2. Sends the contractor the public key location.
3. Asks the contractor to describe the error message.

The contractor can debug the problem with the public information. Amira records in the academy's procedure that private keys are never shared by email.

**Worked example: A university rotates a key**

Daniel is in IT at a university. The university plans to replace its signing key after a staff change. He lists the steps:

1. Create the new key pair in a secure environment.
2. Publish the new public key at the issuer's key location, keeping the old public key available so earlier credentials still verify.
3. Switch the issuing system to the new private key.
4. Test by issuing a sandbox credential and verifying it.
5. Record the date of change in the key log.

Daniel notes that removing the old public key would make all earlier credentials fail verification.

<details>
<summary>Facilitator notes</summary>

Ask the group: "Who should hold a private key in your organisation?" Collect answers on a shared board. Steer towards named roles with a secure process, not a shared inbox. Run a two-minute demonstration of an assistant reading a harmless sandbox file, then show a deliberately fake key file with a "DO NOT PASTE" banner and discuss why it is dangerous to share. Do not use any real key material in the demonstration, even for a sandbox.

</details>

**Practice activity: Inspect a proof**

1. Open the credential file you exported in the previous module.
2. Find the proof, or the signed token if your tool uses an enveloping style. In `proof-notes.md`, write down: the securing style (embedded or enveloping), the type or algorithm named in the file, and the location or identifier of the public key.
3. Find where the public key is published in the sandbox. Note whether you can open it in a browser or text editor.
4. Write three sentences explaining why a private key must never appear in your lab record.
5. Optional: ask an AI assistant to explain one field of your sandbox credential. Check the answer against the specification. Record what the assistant said and whether it was correct. Include no keys or real data.

### Check your understanding

**Question 1.** What does a valid proof tell a verifier?

[( )] That the earner deserves the achievement
[(X)] That a holder of the signing key signed the credential and that it has not changed since
[( )] That the issuer is a government body
[( )] That the credential will never expire
[[?]] A proof is a signature. What do signatures show?
****
A valid proof shows that the credential was signed with a particular key and has not been altered. It says nothing about the quality of the achievement, the type of issuer or the expiry date.
****

**Question 2.** Which key should an issuer keep secret?

[( )] The public key
[( )] Both keys equally
[(X)] The private key
[( )] Neither, because both are published
[[?]] Which key creates signatures?
****
The private key creates signatures and must stay secret. The public key is published so that verifiers can check signatures.
****

**Question 3.** A university removes its old public key after a key change. What is the likely result?

[( )] Earlier credentials continue to verify without any issue
[( )] Only credentials issued in the future will fail
[(X)] Earlier credentials signed with the old key may fail verification
[( )] The credentials become valid forever
[[?]] Verifiers need the matching public key to check a signature.
****
Credentials signed with the old key need the old public key for verification. Removing it makes earlier credentials fail even though they were once valid.
****

**Question 4.** You want an AI assistant to explain a field in a sandbox credential. What do you do first?

[( )] Paste the issuing system's private key so the assistant has context
[( )] Paste a real learner's record for a realistic example
[(X)] Check that the file contains only fictional data and no keys or secrets
[( )] Ask the assistant to sign the credential for you
[[?]] What must never be exposed to an assistant?
****
Only sandbox files with fictional data should be shared, and you must first check that no private key or secret is in the file. An assistant does not need keys to explain a field, and it must not be given real learner data.
****

## Status, expiry and revocation

### What you will do in this module

You will learn how credentials can lose validity: through expiry, revocation or suspension. You will set an expiry date, revoke a sandbox credential and observe how a verifier reports the change.

Time: about 90 minutes.

### Why credentials need a life cycle

A signed credential cannot be edited after issue, because any change would break the signature. Yet real situations change. An employee's safety certificate lapses. A university finds that a credential was issued in error. A badge was issued to the wrong person. A credential needs a way to say, after the fact, "do not accept this any more".

Three ideas cover most cases:

- **Expiry:** the credential carries an end date. After that date, verifiers treat it as no longer valid. The end date is written into the signed credential at issue.
- **Revocation:** the issuer withdraws the credential. It is no longer valid from that moment, and the withdrawal is permanent.
- **Suspension:** the issuer pauses the credential. It may become valid again. Not every tool supports suspension.

### Expiry in the credential

Valid from and valid until are part of the credential. A verifier compares them with the current date and time. If the current time is before the start or after the end, the verifier reports a problem. Dates therefore need correct formats and sensible time zones. A credential issued with a start date in the future, for example, will fail verification today.

### Status lists

Revocation cannot be written into the signed credential, because the credential does not change. Instead, the credential points to a **status** entry. In a common approach, the issuer publishes a list in which each credential has a position, and each position holds a simple flag. A verifier fetches the list, looks up the credential's position and reads the flag.

The specifications for status lists and securing mechanisms continue to evolve, so tools may differ in what they support. A credential with a status pointer that a verifier cannot read may produce a warning or an error, depending on the tool.

{{1}}
<svg viewBox="0 0 800 450" width="100%" role="img" xmlns="http://www.w3.org/2000/svg">
  <title>Status check: credential points to a published status list</title>
  <desc>A credential contains a status pointer with a list address and a position. The issuer publishes a status list at that address. The verifier reads the credential, follows the pointer to the list, looks up the position and reads whether the credential is valid or revoked. Labels show the three results: valid, expired and revoked.</desc>
  <rect x="0" y="0" width="800" height="450" fill="#FFFFFF"/>
  <rect x="40" y="60" width="210" height="110" rx="6" fill="#F1F5F8" stroke="#02375B" stroke-width="2"/>
  <text x="145" y="95" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="18" font-weight="700" fill="#02375B">Credential</text>
  <text x="145" y="125" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">status pointer:</text>
  <text x="145" y="147" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">list address + position</text>
  <rect x="300" y="60" width="210" height="110" rx="6" fill="#F78222" stroke="#02375B" stroke-width="2"/>
  <text x="405" y="95" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="18" font-weight="700" fill="#02375B">Issuer</text>
  <text x="405" y="125" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">publishes status list</text>
  <text x="405" y="147" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">and updates flags</text>
  <rect x="560" y="60" width="200" height="110" rx="6" fill="#F78222" stroke="#02375B" stroke-width="2"/>
  <text x="660" y="95" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="18" font-weight="700" fill="#02375B">Verifier</text>
  <text x="660" y="125" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">reads the list and</text>
  <text x="660" y="147" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">checks the flag</text>
  <path d="M660 170 L660 220 L145 220 L145 174" stroke="#02375B" stroke-width="2" fill="none" stroke-dasharray="6 4"/>
  <text x="400" y="212" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">1 verifier reads the credential</text>
  <path d="M145 250 L145 300 L405 300 L405 174" stroke="#02375B" stroke-width="2" fill="none"/>
  <path d="M399 184 L405 172 L411 184" stroke="#02375B" stroke-width="2" fill="none"/>
  <text x="275" y="292" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">2 follows the pointer to the list</text>
  <rect x="80" y="350" width="190" height="60" rx="6" fill="#B1CF37" stroke="#02375B" stroke-width="2"/>
  <text x="175" y="386" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B">Result: valid</text>
  <rect x="305" y="350" width="190" height="60" rx="6" fill="#5DCAE7" stroke="#02375B" stroke-width="2"/>
  <text x="400" y="386" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B">Result: expired</text>
  <rect x="530" y="350" width="190" height="60" rx="6" fill="#F78222" stroke="#02375B" stroke-width="2"/>
  <text x="625" y="386" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B">Result: revoked</text>
</svg>

### Expiry and revocation together

A verifier may check several things in order:

1. Is the signature valid?
2. Is the current time inside the validity period?
3. What does the status entry say?

A credential can pass step 1 and fail step 2 or 3. A good verification report separates these results, so you can see which one failed. When you read a report, do not stop at "invalid". Find the reason.

### Revocation in practice

An issuer revokes a credential when:

- the credential was issued in error;
- the earner no longer meets the conditions, for example after a finding of misconduct under the issuer's policy;
- the issuer's policy says that the credential is withdrawn after a specific event.

A revocation reason may be recorded for the issuer's own purposes. Be careful about what you expose. A public status list should not reveal why a particular person's credential was revoked.

**Worked example: An HR department revokes a credential issued in error**

Mei works in an HR department. A batch of "Forklift Operator Level 1" credentials was issued to twelve employees on a Monday. On Tuesday she learns that three of them had not passed the practical assessment. The scores are illustrative. She:

1. Identifies the three credentials from the issuing log.
2. Revokes them in the sandbox issuing system.
3. Asks a colleague to verify one of the revoked credentials with a verifier tool.
4. Confirms that the report says the credential is revoked, while the signature is still valid.
5. Writes a short note for the three employees, drafted with the HR lead, explaining the correction.

Mei sees that the signature stays valid after revocation. The status entry carries the withdrawal.

**Worked example: A college sets expiry for a first aid certificate**

Sofia in credential operations at a college issues first aid certificates. The college's policy states that the certificate is valid for three years. She sets the end date at issue. A year later, the college wants to extend the certificates to four years after a review. Sofia explains to the programme leader that existing credentials cannot be edited, because the end date is part of the signed content. The college can issue new credentials with the new end date, and revoke or let the old ones expire.

<details>
<summary>Facilitator notes</summary>

In the live session, ask participants to predict what the verifier will show before revoking. Then revoke together and compare. Highlight that "signature valid" and "credential revoked" can both be true. Mention that the sandbox may cache the status list, so a short delay before the change appears is normal. Ask participants to note the delay in their lab record.

</details>

**Practice activity: Expire and revoke**

1. Issue two new sandbox credentials to fictional recipients. For the first, set a valid until date a few minutes in the past, if the sandbox allows it, or a date that your facilitator provides as an expired sample. For the second, set a normal future end date.
2. Export both. Verify both with the sandbox verifier. Record the results in `verification-log.md`: which checks passed, which failed and the exact message.
3. Revoke the second credential in the sandbox.
4. Verify it again. Record the new result, and the time between revocation and the change in the report.
5. In three to five sentences, explain how the verifier knew the credential was revoked, although the file did not change.

Save the exported files in `exports/` and your notes in `verification-log.md`.

### Check your understanding

**Question 1.** Why can a revoked credential still have a valid signature?

[( )] Because revocation deletes the credential from the earner's device
[(X)] Because revocation is recorded in a separate status entry, not in the signed file
[( )] Because the signature is renewed every day
[( )] Because revoked credentials are never checked for signatures
[[?]] The signed file cannot be changed after issue.
****
The signature covers the content at the time of issue and does not change. Revocation is recorded in a status entry that the verifier checks separately.
****

**Question 2.** Where is the end of a credential's validity period written?

[( )] In the verifier's settings
[( )] In the earner's wallet only
[(X)] In the signed credential, as a valid until date
[( )] In the public key
[[?]] It is part of the credential content.
****
The end date is part of the signed credential. A verifier compares it with the current time. It cannot be changed without breaking the signature.
****

**Question 3.** A college wants to extend certificate validity from three to four years for existing credentials. What is the correct approach?

[( )] Edit the end date in the existing files
[( )] Ask earners to change the date in their wallets
[(X)] Issue new credentials with the new end date and handle the old ones by revocation or expiry
[( )] Remove the proof so the date can be edited
[[?]] The end date is signed content.
****
Editing a signed credential breaks the signature. The college issues new credentials with the new dates and decides what to do with the old ones.
****

**Question 4.** A verification report says "invalid". What should you do first?

[( )] Assume the issuer is dishonest
[( )] Reissue the credential immediately
[(X)] Find which check failed: signature, validity dates or status
[( )] Delete the credential file
[[?]] A report can fail for several different reasons.
****
Several checks sit behind the word "invalid". Finding which one failed tells you what to do next: a status or expiry problem is handled differently from a broken signature.
****

## Verification and conformance

### What you will do in this module

You will verify credentials with a verification tool and check files against a conformance test tool. You will learn the difference between the two and how to read their reports.

Time: about 90 minutes.

### Two different questions

Verification and conformance answer different questions.

- **Verification** asks: can I trust this credential now? It checks the signature, the issuer's key, the dates and the status.
- **Conformance** asks: does this file, or this tool, follow the specification? It checks structure, required fields and behaviour against a test suite.

A credential can pass verification and still be poorly structured. A tool can pass a conformance test and still fail to verify a particular credential, for example because the issuer's key location is offline. You need both views.

### What a verifier checks

A typical verification run covers:

1. **Structure:** the file parses and has the expected types and context.
2. **Issuer and key:** the issuer identifier resolves and the key can be found.
3. **Signature:** the proof matches the content and the key.
4. **Dates:** the credential is within its validity period.
5. **Status:** the status entry, if present, does not indicate revocation or suspension.

Good tools report each check separately, with a clear message. Treat a single green "valid" tick with care, because it may hide checks that the tool skipped. Look for the details.

### What a conformance test tool does

Conformance test tools take a credential, or exercise an issuing or verifying system, and compare behaviour with the specification. Results typically list tests that passed, failed or were skipped. Platform support is still uneven, so conformance certification matters. When you choose a tool, check whether it has been certified against the relevant specification, and read what the certification actually covers: which version, which features and which roles (issuer, verifier or wallet).

<!-- VERIFY: Confirm the current name and scope of the Open Badges 3.0 conformance certification programme and any official test suite before publishing; this file names none. -->

{{1}}
<svg viewBox="0 0 800 450" width="100%" role="img" xmlns="http://www.w3.org/2000/svg">
  <title>Verification and conformance compared</title>
  <desc>Two columns. The left column, verification, asks whether a credential can be trusted now and lists signature, issuer key, dates and status. The right column, conformance, asks whether a file or tool follows the specification and lists structure, required fields and behaviour. A box at the bottom says that a good practice uses both.</desc>
  <rect x="0" y="0" width="800" height="450" fill="#FFFFFF"/>
  <rect x="40" y="40" width="340" height="270" rx="6" fill="#F1F5F8" stroke="#02375B" stroke-width="2"/>
  <text x="210" y="80" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="20" font-weight="700" fill="#02375B">Verification</text>
  <text x="210" y="110" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B">Can I trust this credential now?</text>
  <text x="70" y="160" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B">Signature matches the content</text>
  <text x="70" y="195" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B">Issuer key can be found</text>
  <text x="70" y="230" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B">Dates are inside validity</text>
  <text x="70" y="265" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B">Status is not revoked</text>
  <rect x="420" y="40" width="340" height="270" rx="6" fill="#F1F5F8" stroke="#02375B" stroke-width="2"/>
  <text x="590" y="80" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="20" font-weight="700" fill="#02375B">Conformance</text>
  <text x="590" y="110" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B">Does it follow the specification?</text>
  <text x="450" y="160" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B">Required fields are present</text>
  <text x="450" y="195" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B">Types and context are correct</text>
  <text x="450" y="230" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B">Tool behaviour matches tests</text>
  <text x="450" y="265" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B">Certification scope is stated</text>
  <rect x="160" y="350" width="480" height="60" rx="6" fill="#5DCAE7" stroke="#02375B" stroke-width="2"/>
  <text x="400" y="386" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="16" fill="#02375B">Good practice: use both views</text>
</svg>

### Reading a report

When you read a verification or conformance report:

- Note the tool name and version, and the date. Results change over time.
- Write down each check and its result, not only the overall result.
- Treat skipped or "not applicable" checks as open questions.
- Keep the report with your evidence.

### Wallets and newer protocols

Wallet protocols and credential formats such as OpenID4VC, SD-JWT VC and ISO mdoc are specified for the EUDI Wallet. They are an emerging area, and tooling and education profiles are still maturing. In this lab you work with Open Badges 3.0 files in a sandbox. You do not need these protocols to complete the lab, but you should know that credentials may reach a wallet through different formats and exchange methods, and that support varies. When a wallet rejects a file that a verifier accepts, a format or protocol difference may be the cause.

<!-- VERIFY: Check the current status of EUDI Wallet specifications and of education profiles for OpenID4VC, SD-JWT VC and ISO mdoc before publishing. -->

**Worked example: A corporate academy compares two tools**

Jonas is a learning technology owner. His academy plans to buy a new issuing system. He tests two candidate tools in a sandbox with the same credential. For each tool he records:

1. The tool's conformance certification: which specification version and which role it covers.
2. The result of verifying the same exported credential in two independent verifiers.
3. Any differences in the reports.

One tool's credential passes in one verifier but shows a warning in the other, because the second verifier cannot read the status list format. Jonas records the warning and asks the supplier to explain. He does not treat the pass in the first verifier as proof that the credential is portable.

**Worked example: A university checks a partner's credentials**

Aisha works in credential operations at a university. A partner college sends sample credentials so that the university can accept them for credit transfer. Aisha runs each sample through a verifier and a conformance checker. She finds that all signatures are valid, but the conformance checker flags a missing criteria field on two samples. She reports this to the partner as a structural issue, not a trust issue, and agrees a fix before the university accepts the credentials for credit decisions.

<details>
<summary>Facilitator notes</summary>

Prepare a short table on a shared board with the columns Check, Tool A, Tool B. Ask participants to fill it in during the activity. Discuss differences. Emphasise that two good tools can disagree, and that the disagreement is useful information. Warn participants not to name or rank commercial products in their lab record; they should describe the checks.

</details>

**Practice activity: Verify and test conformance**

1. Take the two credentials you exported in the previous module: one valid and one revoked, plus the expired sample.
2. Verify each one in the sandbox verifier. If a second verifier is available, verify them there as well.
3. Run the valid credential through the conformance test tool provided for the lab. Record which tests passed, failed or were skipped.
4. In `verification-log.md`, create a table with the columns Credential, Tool, Check, Result and Message. Fill it in for every check you ran.
5. Write a short paragraph: if the verifier says "valid" and the conformance tool reports one failure, what would you do before accepting the credential in your organisation?

### Check your understanding

**Question 1.** What does a conformance test tool check?

[( )] Whether an earner deserves the credential
[(X)] Whether a file or tool follows the specification
[( )] Whether the issuer is a large organisation
[( )] Whether the earner has a wallet
[[?]] Conformance relates to the specification, not to the earner.
****
Conformance tools compare files or behaviour with the specification. They do not judge the earner, the size of the issuer or the use of a wallet.
****

**Question 2.** A credential passes verification but fails one conformance test for a missing field. What is a sensible conclusion?

[( )] The credential is false
[( )] The conformance tool is always wrong
[(X)] The credential can be trusted as signed, but it has a structural issue to resolve
[( )] The signature must be invalid
[[?]] Verification and conformance answer different questions.
****
Verification covers trust in the credential. Conformance covers structure. A structural issue may still limit portability, so it should be resolved with the issuer.
****

**Question 3.** Why should you record the tool version and date with a report?

[( )] Because reports never change
[( )] Because the tool name replaces the results
[(X)] Because results can change as tools and specifications change
[( )] Because the date proves the earner's competence
[[?]] Think about what happens when a tool is updated.
****
Tools and specifications evolve, so the same file may get a different result later. The version and date make the report reproducible.
****

**Question 4.** What should you check when choosing a tool for Open Badges 3.0?

[( )] Only the colour of its interface
[( )] Only the number of users
[(X)] Its conformance certification, including version, features and roles covered
[( )] Whether it supports every possible wallet protocol
[[?]] Platform support is still uneven.
****
Support varies, so the scope of a tool's conformance certification matters. Interface colour and user numbers say nothing about conformance, and no tool needs to support every wallet protocol.
****

## Troubleshooting

### What you will do in this module

You will learn the common reasons why credentials fail to verify or to import into other systems. You will practise a structured diagnostic method and apply it to three faulty samples supplied by your facilitator.

Time: about 90 minutes.

### A method for diagnosing errors

Random fixes waste time. Follow the same order each time:

1. **Read the message.** Copy the exact error text.
2. **Locate the layer.** Is it the file structure, the proof, the key, the dates, the status or the receiving tool?
3. **Check the simple things first.** Are there typos, wrong date formats or broken links?
4. **Compare with a known good sample.** A working credential is a reference.
5. **Change one thing at a time** and test again.
6. **Record the cause and the fix.**

### Common errors

The table lists frequent problems in the form of symptoms and likely causes. Treat it as a starting point, not a complete list.

| Symptom | Likely causes |
|---|---|
| File does not parse | Missing comma, bracket or quote in the JSON; wrong character encoding |
| "Unknown type" or context error | Wrong or outdated context link; type spelled incorrectly; missing Verifiable Credential type |
| Signature invalid | Content edited after signing; wrong key; unsupported securing mechanism |
| Key not found | Key location offline; issuer identifier does not resolve; key rotated and old key removed |
| Credential not yet valid | Valid from date in the future; time zone confusion |
| Credential expired | Valid until date in the past |
| Status check fails | Status list address wrong or offline; verifier cannot read the list format |
| Imported but displayed wrongly | Receiving tool supports only part of the specification; missing image or optional fields |

{{1}}
<svg viewBox="0 0 800 450" width="100%" role="img" xmlns="http://www.w3.org/2000/svg">
  <title>Diagnostic decision path</title>
  <desc>A flow of questions. First: does the file parse? If no, fix the JSON syntax. If yes: are the context and types correct? If no, fix the context or types. If yes: is the signature valid? If no, check the key and securing mechanism. If yes: are the dates and status acceptable? If no, the credential is not yet valid, expired or revoked. If yes, check the receiving tool.</desc>
  <rect x="0" y="0" width="800" height="450" fill="#FFFFFF"/>
  <rect x="30" y="30" width="170" height="60" rx="6" fill="#F1F5F8" stroke="#02375B" stroke-width="2"/>
  <text x="115" y="66" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">1 File parses?</text>
  <rect x="230" y="30" width="170" height="60" rx="6" fill="#F1F5F8" stroke="#02375B" stroke-width="2"/>
  <text x="315" y="58" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">2 Context and</text>
  <text x="315" y="76" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">types correct?</text>
  <rect x="430" y="30" width="170" height="60" rx="6" fill="#F1F5F8" stroke="#02375B" stroke-width="2"/>
  <text x="515" y="66" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">3 Signature valid?</text>
  <rect x="630" y="30" width="150" height="60" rx="6" fill="#F1F5F8" stroke="#02375B" stroke-width="2"/>
  <text x="705" y="58" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">4 Dates and</text>
  <text x="705" y="76" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">status fine?</text>
  <path d="M200 60 L226 60" stroke="#02375B" stroke-width="2" fill="none"/>
  <path d="M218 54 L228 60 L218 66" stroke="#02375B" stroke-width="2" fill="none"/>
  <path d="M400 60 L426 60" stroke="#02375B" stroke-width="2" fill="none"/>
  <path d="M418 54 L428 60 L418 66" stroke="#02375B" stroke-width="2" fill="none"/>
  <path d="M600 60 L626 60" stroke="#02375B" stroke-width="2" fill="none"/>
  <path d="M618 54 L628 60 L618 66" stroke="#02375B" stroke-width="2" fill="none"/>
  <text x="213" y="50" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">yes</text>
  <text x="413" y="50" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">yes</text>
  <text x="613" y="50" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">yes</text>
  <rect x="30" y="170" width="170" height="70" rx="6" fill="#5DCAE7" stroke="#02375B" stroke-width="2"/>
  <text x="115" y="200" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">If no: fix JSON</text>
  <text x="115" y="220" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">syntax</text>
  <rect x="230" y="170" width="170" height="70" rx="6" fill="#5DCAE7" stroke="#02375B" stroke-width="2"/>
  <text x="315" y="200" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">If no: fix context</text>
  <text x="315" y="220" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">or type names</text>
  <rect x="430" y="170" width="170" height="70" rx="6" fill="#5DCAE7" stroke="#02375B" stroke-width="2"/>
  <text x="515" y="200" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">If no: check key</text>
  <text x="515" y="220" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">and securing style</text>
  <rect x="630" y="170" width="150" height="70" rx="6" fill="#5DCAE7" stroke="#02375B" stroke-width="2"/>
  <text x="705" y="200" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">If no: not yet valid,</text>
  <text x="705" y="220" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">expired or revoked</text>
  <path d="M115 90 L115 168 M315 90 L315 168 M515 90 L515 168 M705 90 L705 168" stroke="#02375B" stroke-width="2" fill="none"/>
  <rect x="230" y="320" width="340" height="70" rx="6" fill="#B1CF37" stroke="#02375B" stroke-width="2"/>
  <text x="400" y="350" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">If all four pass and a problem remains:</text>
  <text x="400" y="372" text-anchor="middle" font-family="Open Sans, Arial, sans-serif" font-size="14" fill="#02375B">check the receiving tool</text>
</svg>

### Interoperability problems

Interoperability means that credentials work across tools from different makers. Problems appear when one tool supports a feature that another does not, or when one reads an optional field differently. Common patterns:

- A tool produces a valid credential that another tool imports without images or descriptions.
- A verifier does not support a securing mechanism that the issuer uses.
- A wallet expects a different format or exchange protocol from the one the issuer offers.
- Two tools use different versions of the specification or of its context files.

When you meet such a problem, avoid blaming one side. Note the versions, test with a third tool if you can, and report to the issuer or tool maker with the exact steps and the files.

### Using an AI assistant when diagnosing

An AI assistant can help you spot a missing comma or explain an error message. Apply the same rules as before: use only sandbox files with fictional data, never share a private key or a secret, and check the answer against the specification or a tool report. An assistant can suggest a wrong fix with confidence. A verifier or conformance tool gives you the check that counts.

**Worked example: A corporate academy diagnoses an import failure**

Carlos is an HR systems owner. An employee tries to import a credential into a wallet, and the wallet says "unsupported file". Carlos follows the method:

1. He reads the message and records the wallet's version.
2. He verifies the same file in a verifier. It passes, so the file parses and the signature is valid.
3. He compares the securing style with the wallet's documentation and finds that the wallet accepts only one of the two styles that the issuing system can produce.
4. He reconfigures the sandbox issuer to use the supported style, reissues a test credential and imports it successfully.
5. He records the cause as "securing style not supported by receiving wallet" and the fix.

**Worked example: A college diagnoses a status error**

Nadia works in IT at a college. Verifiers report "status check failed" for new credentials. She checks the status address in a sample and tries to open it in a browser. It returns an error. She finds that the address contains a typo introduced during a recent server move. She corrects the address in the issuing system, reissues test credentials and verifies them. She records that already issued credentials with the wrong address need to be reissued, and flags this to her manager.

<details>
<summary>Facilitator notes</summary>

Distribute the three faulty sample credentials at the start of the practice activity, together with a known good reference sample. Keep a private answer sheet for assessors. Suitable faults for the three samples include one syntax or context problem, one signature or key problem, and one date or status problem. Do not tell participants which category each sample belongs to. Circulate and ask guiding questions such as "Which check fails first?" rather than giving answers. Remind participants to change one thing at a time and to keep their original file untouched.

</details>

**Practice activity: Diagnose three faulty samples**

1. Open the three faulty sample files supplied by your facilitator (called sample A, sample B and sample C), plus the known good reference.
2. For each sample, run the verifier and, if available, the conformance tool. Copy the exact messages into `diagnostics.md`.
3. For each sample, answer in the following form:
   - Symptom: what the tool reported.
   - Layer: file structure, context and types, proof, key, dates or status, or receiving tool.
   - Cause: your best explanation, with evidence from the file or tool report.
   - Fix: what the issuer should change, and how you would confirm the fix.
4. Compare each sample with the known good reference to support your explanation.
5. If you use an AI assistant, record what you asked and whether its answer was right. Share no keys and no real data.
6. In `reflection.md`, write five sentences on what you would check before relying on a new tool in production.

Add `diagnostics.md` and `reflection.md` to your lab record.

### Check your understanding

**Question 1.** What is the best first step when a credential fails to verify?

[( )] Edit the file until the error disappears
[( )] Reissue the credential without reading the message
[(X)] Read and record the exact error message
[( )] Ask the earner to try again on another device
[[?]] A diagnosis starts with evidence.
****
The exact message points to the layer where the problem sits. Editing or reissuing without it risks hiding the cause or breaking the file further.
****

**Question 2.** A credential verifies in one tool and fails to import in a wallet. Which cause is most likely to explain this?

[( )] The earner's name is too long
[( )] The credential has no colours
[(X)] The wallet does not support the securing style or format used
[( )] The sandbox is switched off
[[?]] The file itself passes verification.
****
If the credential verifies elsewhere, the file is sound. A mismatch in securing style, format or protocol support in the receiving tool is a common reason for import failure.
****

**Question 3.** A verifier says "key not found" for credentials that used to verify. Which cause fits best?

[( )] The earner changed their email address
[(X)] The issuer's key location is offline, or an old key was removed after rotation
[( )] The criteria text is too short
[( )] The credential has too many fields
[[?]] Verifiers must be able to retrieve the public key.
****
Verification needs the public key. If the location is offline or the key used for earlier credentials has been removed, the verifier cannot check the signature.
****

**Question 4.** Why change only one thing at a time while diagnosing?

[( )] Because tools accept only one change per day
[( )] Because it makes the file shorter
[(X)] So that you can tell which change fixed or caused the problem
[( )] Because the specification forbids multiple edits
[[?]] Think about what you learn if you change three things and the error disappears.
****
Changing one thing at a time links each result to one cause. If you change several things together, you cannot tell which one mattered.
****

## Assessment and badge

### Overview

Assessment has two parts:

1. **Lab record (assessed by a person).** You submit the lab record you built through the six modules. An assessor reviews it with the rubric below. This file does not grade it.
2. **Final knowledge check (formative).** Ten questions in this section help you check your understanding before you submit. They do not replace the lab record.

### The lab task

Submit your lab record as one folder or archive containing:

- `issued/`: the credential files you issued, including your annotated sample.
- `exports/`: the exported files, including the valid, expired and revoked examples.
- `explanation.md`: your paragraph on how Open Badges 3.0 relates to the W3C Verifiable Credentials data model.
- `proof-notes.md`: your notes on the proof, securing style and key location.
- `verification-log.md`: the table of verification and conformance results, including status and expiry results and the revocation observation.
- `diagnostics.md`: your answers for the three faulty samples (symptom, layer, cause, fix).
- `reflection.md`: your note on what to check before production use.

Your record must contain no private keys, no secrets and no real personal data.

### Rubric

Each criterion is rated at one of three levels. The assessor records the level and a short comment.

| Criterion | Not yet | Meets the standard | Exceeds the standard |
|---|---|---|---|
| 1. Issue and inspect (outcome 1) | Credential file missing, incomplete or not inspected | A valid sandbox credential is issued and exported; at least five fields are annotated correctly | Credential is well designed with checkable criteria; annotations explain the purpose of each field and link choices to the context of use |
| 2. Relation to Verifiable Credentials (outcome 2) | Explanation is missing or confuses the two | Explanation states that Verifiable Credentials is the general layer and Open Badges 3.0 adds achievement terms | Explanation also covers proofs, status and the evolving related specifications, in clear language for a non-technical reader |
| 3. Verification, status and expiry (outcome 3) | Verification is missing, or results are recorded without the checks or messages | Valid, expired and revoked credentials are verified; each check and message is logged; revocation is observed | Log compares two tools or a verifier and a conformance tool, notes version and date, and explains differences |
| 4. Conformance checking (outcome 3) | No conformance run | Conformance tool run on at least one credential; passed, failed and skipped tests recorded | Results are interpreted: follow-up actions are proposed for each failure or skipped test |
| 5. Diagnosis (outcome 4) | Fewer than two samples diagnosed, or causes unsupported | All three samples diagnosed with symptom, layer, cause and fix; causes supported by evidence | Diagnoses are precise, compare with the reference sample, and propose how to confirm each fix |
| 6. Safety and professional practice | A key, secret or real personal data appears in the record | No keys, secrets or real data; reflection names at least three checks before production use | Reflection also covers data protection, key management and conformance certification scope |

### Pass rule

- You pass the lab when every criterion is rated "Meets the standard" or higher, and no criterion is rated "Not yet".
- Criterion 6 is a requirement: if a private key, secret or real personal data appears in your record, the assessor returns it for correction before any other review.
- If you are rated "Not yet" on one or more criteria, you may revise and resubmit the relevant parts.

### Evidence submitted for the badge

The lab record, with credential files and diagnostic answers, is the badge evidence. The assessor confirms the result against the rubric. On a pass, you receive the badge "Open Badges 3.0 and Verifiable Credentials: Hands-on Lab (Ability, L2)", alignment code ICSF-STND-L2-A. The badge records completion of the assessed tasks in this course. It does not prove that you are competent in any particular job.

<details>
<summary>Facilitator notes</summary>

Assessors should use the answer sheet for the three faulty samples and check that diagnoses are supported by evidence rather than guesses. Where a participant reaches a correct fix through a different route, accept it if the reasoning is sound. Keep submitted records secure and delete sandbox exports according to your retention schedule. Return any record that contains keys, secrets or real personal data before reviewing it further, and advise the participant on safe handling.

</details>

### Final knowledge check

Use these questions to check your understanding before you submit your lab record. They cover all four learning outcomes.

**Question 1.** Which description of an Open Badges 3.0 credential is accurate?

[( )] A paper certificate with a barcode
[(X)] A Verifiable Credential whose subject has an achievement, expressed with Open Badges terms
[( )] A wallet protocol for identity documents
[( )] A signature algorithm
[[?]] Think about the layer diagram.
****
Open Badges 3.0 uses the Verifiable Credentials structure and adds achievement terms. It is not a paper format, a wallet protocol or a signature algorithm.
****

**Question 2.** After issuing a credential in the sandbox, what should you do to inspect it properly?

[( )] Trust the preview and skip the file
[(X)] Export the file and read its fields in a text editor
[( )] Delete the proof to simplify the file
[( )] Send it to a real learner for feedback
[[?]] The file is the credential.
****
The exported file is the real credential. Reading it shows context, types, issuer, subject, dates and proof, some of which a preview may hide.
****

**Question 3.** Which statement about a private key is correct?

[( )] It is published with the credential
[( )] It can be sent to a contractor by email for debugging
[(X)] It stays secret with the issuer and is used to create signatures
[( )] It is used by verifiers to check signatures
[[?]] Verifiers use the public key.
****
The private key creates signatures and must never leave the issuer's secure environment. Verifiers use the public key.
****

**Question 4.** Why can a revoked credential still show a valid signature?

[( )] Because verifiers ignore signatures after revocation
[( )] Because revocation rewrites the signature
[(X)] Because revocation is recorded in a separate status entry, and the signed file does not change
[( )] Because revoked credentials are removed from all files
[[?]] Signed content cannot be edited.
****
The signature covers the content at issue. Revocation sits in a status entry that verifiers check separately, so the two can differ.
****

**Question 5.** What is the main difference between verification and conformance checking?

[(X)] Verification asks whether a credential can be trusted now; conformance asks whether a file or tool follows the specification
[( )] Verification checks the earner's skills; conformance checks the issuer's size
[( )] Verification applies only to wallets; conformance applies only to issuers
[( )] There is no difference, because both give the same result
[[?]] One concerns trust in a credential, the other concerns the specification.
****
Verification checks signature, key, dates and status. Conformance compares files or tools with the specification. They answer different questions and both are useful.
****

**Question 6.** A credential verifies in one tool but shows a warning in another because the second tool cannot read the status list format. What is the most sensible conclusion?

[( )] The credential is fraudulent
[( )] The first tool is always correct
[(X)] There is an interoperability gap to investigate, noting versions and testing with another tool
[( )] The earner must reissue the credential themselves
[[?]] Support for features varies between tools.
****
Differences in support for formats and features cause interoperability gaps. Recording versions and testing with a third tool helps locate the cause without blaming either side.
****

**Question 7.** A verification report says the credential is "not yet valid". Which cause is most likely?

[( )] The signature algorithm is unsupported
[( )] The credential was revoked
[(X)] The valid from date is in the future
[( )] The context link is missing
[[?]] Look at the dates.
****
"Not yet valid" points to the validity start date being later than the current time. Revocation and signature problems produce different messages.
****

**Question 8.** Which entry should you add to a verification log for each check?

[( )] Only the overall result
[( )] Only the tool's colour scheme
[(X)] The credential, tool, check, result and exact message, with tool version and date
[( )] Only the earner's name
[[?]] A log should let another person repeat your check.
****
A good log lists each check and its result with the exact message and the tool version and date, so that someone else can repeat it and compare.
****

**Question 9.** When choosing a tool, why should you read the scope of its conformance certification?

[( )] Because certification covers every feature of every specification
[( )] Because certification replaces testing in your own sandbox
[(X)] Because certification may cover only certain versions, features and roles
[( )] Because certification is only about interface design
[[?]] Platform support is still uneven.
****
Certification has a defined scope. It may name a specification version and a role such as issuer or verifier, so you must check that it matches your use. It does not replace your own tests.
****

**Question 10.** You want help from an AI assistant to understand an error. Which action is acceptable?

[( )] Paste the issuing system's private key to give full context
[( )] Paste a real learner's credential from production
[(X)] Paste a sandbox credential with fictional data after checking that it contains no keys or secrets, then check the answer against the specification
[( )] Ask the assistant to approve the credential in place of a verifier
[[?]] Keep keys and real data out of assistants.
****
Only fictional sandbox data without keys or secrets may be shared, and the answer must be checked against the specification or a tool report. An assistant does not replace a verifier.
****

## Sources and further reading

Status as of November 2026; check before publishing.

The sources below are official texts and bodies. Check each one for the current version and for any changes since this course was written. This file gives no web addresses; search for the exact title on the website of the named body.

- **W3C:** "Verifiable Credentials Data Model v2.0", W3C Recommendation. The general data model on which Open Badges 3.0 builds. Related W3C specifications for status lists and securing mechanisms continue to evolve; check the W3C technical reports page for the current list.
- **1EdTech Consortium:** "Open Badges Specification, Version 3.0". The specification for achievement credentials expressed with the Verifiable Credentials data model. Also see the 1EdTech material on the Comprehensive Learner Record (CLR) Standard, Version 2.0.
- **1EdTech Consortium:** the conformance certification information for Open Badges 3.0 and CLR 2.0. Check which versions, roles and products are listed and what each certification covers.
- **OpenID Foundation:** the OpenID for Verifiable Credentials specifications (OpenID4VC family). Emerging area; tooling and education profiles are still maturing.
- **IETF:** the SD-JWT and SD-JWT-based Verifiable Credentials specifications. Emerging area; check for the current status of each document.
- **ISO/IEC:** the standard for mobile driving licences and related mobile documents (ISO/IEC 18013 series), which defines the mdoc format. Emerging in education contexts.
- **European Commission:** the official pages on the European Digital Identity Wallet (EUDI Wallet) and its architecture and reference framework. Check the current version of the framework.
- **ICoBC:** "ICoBC Credentialing Skills Framework (ICSF)", for the definition of skill STND "Standards and interoperability" and the VRITE pillars.
- **ICoBC:** course ICB-F01 "Digital Badges and Credentials Essentials", the prerequisite for this course.

<!-- VERIFY: Confirm the exact current titles, version numbers and publication status of each source above, and add official addresses only after checking them. -->
