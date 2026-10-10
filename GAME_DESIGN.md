# Cyber Detective --- Game Design Document

**Document status:** Draft 0.1\
**Project status:** Planning and design\
**Last updated:** 2026-10-10\
**Target platform:** Windows desktop\
**Planned technology:** Python, Tkinter, SQLite\
**Initial distribution:** Private GitHub repository and GitHub Releases\
**Initial audience:** A small group of invited friends

> This document describes the intended design. Items marked **Proposed**
> are not final until reviewed and approved. No game implementation is
> implied by this document.

## 1. Overview

Cyber Detective is a fictional digital-incident investigation simulator.
The player takes the role of an investigator who reviews evidence from
several simulated sources, reconstructs a timeline, distinguishes
observations from assumptions, and selects the conclusion best supported
by the available evidence.

The game is intended to teach careful reasoning, evidence correlation,
and uncertainty management. It is an educational simulation, not a
real-world forensic or security tool.

### Design principles

-   **Evidence first:** Conclusions should be supported by identifiable
    evidence.
-   **One best answer:** Each multiple-choice question must have exactly
    one answer that is best supported by the case evidence.
-   **Fair difficulty:** Distractors should sound plausible, but a
    careful player should be able to rule them out using the evidence.
-   **Explain every option:** After answering, the player should be able
    to review why each option is supported or unsupported.
-   **Separate fact from inference:** A sequence of events or a
    correlation does not automatically prove causation.
-   **Preserve uncertainty:** If the logs do not establish that data was
    transferred, the game must not claim that exfiltration was
    proven---or that it definitely did not occur.
-   **Safe simulation:** Use fictional systems and records. Do not scan
    or modify the player's actual devices or networks.

## 2. Platform and technology

### Proposed stack

-   **Language:** Python
-   **Desktop UI:** Tkinter
-   **Structured data and persistence:** SQLite
-   **Version control and collaboration:** Git and GitHub
-   **Distribution:** Windows executable packaged for a GitHub Release;
    packaging tool to be selected and tested later.

The game should be tested on a clean Windows environment without Python
installed before a release is described as ready for general testers.

## 3. Game loop

1.  The player opens a case briefing.
2.  The player reviews evidence from simulated sources.
3.  The player compares timestamps, devices, actors, processes, and
    other relevant fields.
4.  The player answers investigation questions.
5.  The game explains the best-supported answer and why the alternatives
    are weaker.
6.  The game records progress and presents a case result.

Exact scoring, hints, replay rules, and rank thresholds remain
**Proposed** until separately designed and tested.

## 4. Case 001 --- THE GHOST PROCESS

**Case ID:** `CASE-001`\
**Organization:** NOVACORE TECHNOLOGIES (fictional)\
**Difficulty:** Moderate (proposed)\
**Affected device:** `DEV-104` (proposed identifier)\
**Separate test device:** `DEV-LAB-02` (proposed identifier)

### Initial situation

Ethan Cole, employee ID `NVC-104`, used a document received by email.
Shortly afterward, monitoring records showed a suspicious process, a
connection to an unapproved external endpoint, and a system-setting
change. The investigator must determine what the records establish, how
the events may be connected, and what remains unproven.

Maya Chen (`NVC-217`) performed a file-sync-tool test in a separate test
environment. That activity is included as a plausible lead that must be
compared against device and process evidence rather than assumed to be
part of the incident.

Daniel Reed (`NVC-031`), a security analyst, identified an alert. A
prior, unrelated suspicious-email alert associated with Daniel's work is
not by itself evidence that he caused the incident.

These character details and identifiers are fictional. They are design
inputs and should be finalized together with the evidence records before
implementation.

### Evidence-source types

-   **Email Gateway:** Sender details, message time, attachment name,
    and message disposition.
-   **Endpoint Monitor:** Application launches, parent-child process
    relationships, and process observations.
-   **Network Sensor:** Connection time, destination metadata, and the
    limits of what network telemetry can establish.
-   **File & System Audit:** File creation and system-setting changes.
-   **Security Monitor:** Alert creation and alert metadata.

### Proposed evidence inventory

The following is a working outline, not yet a finalized case database.
Times are illustrative and must be checked for timezone, ordering, and
source consistency before the case is locked.

  ----------------------------------------------------------------------------
  ID                Proposed event    Source            Proposed observation
                    time                                
  ----------------- ----------------- ----------------- ----------------------
  `EV-001`          08:12:04          Email Gateway     Message contains
                                                        attachment
                                                        `Project_Notes.doc`.

  `EV-002`          08:12:09          Email Gateway     Sender is not found in
                                                        the trusted-contacts
                                                        list. This alone does
                                                        not prove malicious
                                                        intent.

  `EV-003`          08:16:22          Endpoint Monitor  A document application
                                                        launches an
                                                        attachment-related
                                                        file on `DEV-104`.
                                                        Exact executable and
                                                        path must be
                                                        finalized.

  `EV-004`          08:16:24          Endpoint Monitor  A child process is
                                                        recorded under the
                                                        document application's
                                                        process lineage. Exact
                                                        process details must
                                                        be finalized.

  `EV-005`          08:17:05          Endpoint Monitor  `sync_helper.exe`
                                                        appears in the process
                                                        lineage on `DEV-104`.
                                                        Its exact parent,
                                                        path, and process
                                                        identifier must be
                                                        specified.

  `EV-006`          08:17:48          File Audit        A new
                                                        temporary-directory
                                                        file is recorded. Its
                                                        path and relationship
                                                        to the process must be
                                                        specified.

  `EV-007`          08:18:13          Network Sensor    A process or device
                                                        makes a connection to
                                                        an unapproved external
                                                        endpoint. The exact
                                                        attribution fields
                                                        must be specified.

  `EV-008`          08:18:15          Network Sensor    Available record
                                                        contains connection
                                                        metadata but no
                                                        payload that
                                                        establishes what
                                                        content, if any, was
                                                        transferred.

  `EV-009`          08:19:30          System Audit      A system setting
                                                        changes. The exact
                                                        setting, actor, and
                                                        process attribution
                                                        must be specified.

  `EV-010`          08:22:10          Security Monitor  An alert is created.
                                                        The alert's detection
                                                        time must be
                                                        distinguished from the
                                                        underlying event
                                                        times.
  ----------------------------------------------------------------------------

**Case-authoring gate:** Do not implement these records as final
evidence until all fields, device identifiers, process IDs,
event/detection times, and cross-source relationships are consistent.
The final case should explicitly state which facts are observed and
which are inferences.

### Character hypotheses to examine

-   **Ethan Cole:** Relevant because the attachment was opened on the
    affected workstation; this does not automatically establish intent
    or full responsibility.
-   **Maya Chen:** Her test activity occurred in a separate environment.
    Device and process records should show whether it is related or
    unrelated.
-   **Daniel Reed:** His analyst role and prior unrelated alert are
    context, not proof of involvement.

No character should be treated as responsible solely because their
activity looks suspicious or because they had access.

## 5. Planned question set

The first case is planned to contain six questions. The exact wording,
four options per question, answer keys, explanations, evidence
references, and point values must be authored and reviewed before
implementation.

1.  **The First Signal** --- What the email evidence does and does not
    establish.
2.  **Process Lineage** --- Whether the evidence supports a relationship
    between the opened attachment and the suspicious process.
3.  **The Suspicious Connection** --- The strongest conclusion supported
    by process and network records.
4.  **The Maya Hypothesis** --- Whether the separate test-environment
    activity matches the incident evidence.
5.  **What Can We Prove?** --- Distinguishing supported findings from
    claims that exceed the evidence.
6.  **The Next Move** --- Selecting a proportionate next investigative
    step that addresses an important uncertainty.

### Question quality requirements

Every question must pass all of the following checks:

-   It has exactly four answer options.
-   Exactly one option is the best-supported answer given the evidence
    available to the player.
-   All distractors are plausible enough to require reasoning, but each
    can be refuted or shown to be less supported.
-   The prompt does not depend on unstated assumptions.
-   The answer key cites the relevant evidence IDs.
-   Each of the four options has an explanation.
-   The explanation distinguishes direct observation, inference, and
    unknowns.
-   A reviewer can answer correctly by using the evidence shown in the
    game.
-   The wording does not accidentally imply that absence of evidence
    proves the opposite.

## 6. Data architecture

The planned design uses SQLite and separates player-facing case content
from answer-key data for organizational clarity and to reduce accidental
answer exposure in the UI. This is **not strong protection against a
user who can inspect or modify local files**.

### Planned databases

#### `game_content.db`

Contains content needed to present cases and questions:

-   `cases`
-   `evidence`
-   `evidence_links`
-   `questions`
-   `question_options`

#### `game_answers.db`

Contains answer and authoring-review data:

-   `answer_keys`
-   `option_explanations`
-   `canonical_facts`

#### Player-data store

A player-specific local database, with its final filename and location
to be decided, may contain:

-   `player_profile`
-   `case_progress`
-   `attempts`
-   `answer_submissions`
-   `integrity_events`
-   `integrity_status`

Player saves should be stored in an appropriate per-user data directory
rather than a protected installation directory, so ordinary users can
save progress and updates do not overwrite their data.

### Proposed field outlines

**`evidence`** - `evidence_id` - `case_id` - `source_type` -
`source_name` - `event_timestamp` - `detection_timestamp` (nullable when
not applicable) - `timezone` - `device_id` - `actor_id` (nullable) -
`event_type` - `title` - `content` - `reliability` - `discovery_order`

**`evidence_links`** - `link_id` - `case_id` - `from_evidence_id` -
`to_evidence_id` - `relationship_type` - `explanation`

Possible relationship types include `SAME_DEVICE`, `SAME_PROCESS`, and
`TEMPORAL_SEQUENCE`. A link must not imply causation unless the evidence
justifies that conclusion.

**`questions`** - `question_id` - `case_id` - `question_order` -
`question_type` - `difficulty` - `prompt` - `points` - `topic`

**`question_options`** - `option_id` - `question_id` - `option_label` -
`option_text` - `display_order`

Do not put an `is_correct` field in player-facing question-option data.

**`answer_keys`** - `question_id` - `correct_option_id` -
`scoring_mode` - `review_summary`

**`option_explanations`** - `question_id` - `option_id` - `is_correct` -
`reasoning` - `evidence_refs`

**`canonical_facts`** - `fact_id` - `case_id` - `fact_statement` -
`certainty` - `supporting_evidence_refs` - `notes`

These are conceptual field lists. Primary keys, foreign keys, indexes,
exact SQLite types, constraints, and migration strategy remain to be
designed before coding.

## 7. Scoring, progression, and integrity

### Scoring

The game should calculate scores in its game/service layer rather than
trusting values supplied by the UI or a player-editable save file. Exact
points, rank names, penalties, and hint behavior are not finalized.

### Integrity and anti-cheat concept

The working name for integrity checks is **Project SIDE-EYE**.

Design principles:

-   Validate data consistency and required IDs.
-   Check important packaged files against known hashes where useful.
-   Record credible integrity anomalies with enough context to diagnose
    them.
-   Avoid accusing the player based on weak or ambiguous signals.
-   Do not destroy saves, punish unrelated progress, or deliberately
    crash the game.
-   Explain that offline integrity checks can be bypassed by someone who
    modifies both the game and its checks.
-   Do not promise that hashes prove a file is safe; a hash only checks
    whether bytes match a known reference.

Trusted online ranking would require server-side validation and is
outside the initial offline prototype unless separately approved.

## 8. Release and testing plan

-   Keep the GitHub repository private during early development.
-   Test with a small invited group first.
-   Publish a packaged Windows build through GitHub Releases.
-   Use version labels such as `v0.1.0-alpha` for the first test build.
-   Keep test instructions, known issues, and release notes with each
    release.
-   Test the executable on a clean Windows machine without Python before
    distributing it.
-   Keep real player saves, private logs, credentials, and local
    development artifacts out of Git.

## 9. Future narrative direction

For a later, higher-difficulty case (tentatively difficulty 3--4), the
story may expand into an investigation that powerful people attempt to
stop. Potential scripted story events include an evidence source
becoming unavailable, an alert interrupting progress, an informant
withdrawing, or an order to stop the investigation.

This is a future narrative idea only. It is not part of CASE-001 and
should be implemented as fictional in-game events, never as interference
with the player's real device or files.

## 10. Open decisions

Before implementation, resolve and document:

-   Final CASE-001 evidence content, identifiers, paths, process
    lineage, and timestamp semantics.
-   Final wording and options for all six questions.
-   Scoring, hints, replay, and rank rules.
-   Exact database schemas, constraints, and migrations.
-   Save location and backup behavior.
-   Packaging tool and Windows compatibility target.
-   Bug-reporting process for invited testers.
-   Project license and any third-party asset licenses.
-   Which integrity checks are proportionate for the first alpha
    release.

## 11. Definition of design readiness

CASE-001 is ready to implement only when the evidence timeline is
internally consistent, all questions have one defensible best answer,
every option has a reasoned explanation, and an independent reviewer can
solve the case from the presented evidence without relying on hidden
assumptions.
