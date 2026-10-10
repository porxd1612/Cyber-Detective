# Cyber Detective --- Testing Guide

**Document status:** Draft 0.1\
**Applies to:** Initial private alpha and later test builds\
**Audience:** Developer and invited testers\
**Last updated:** 2026-10-10

> This is a test plan for future builds. The steps that require a
> playable game cannot be completed until a test build exists. Do not
> report a test as passed unless it was actually performed.

## 1. Purpose

This guide helps testers check whether Cyber Detective installs, starts,
presents evidence correctly, scores answers correctly, saves progress
reliably, and handles errors safely.

The first test group is a small group of invited friends. Testers should
focus on clear, reproducible observations rather than guessing at the
cause of a problem.

## 2. Before testing

Record the following:

-   Game version (for example, `v0.1.0-alpha`)
-   Download source (GitHub Releases)
-   Windows version and system type (if known)
-   Whether Python is installed
-   Whether this is a first launch or an update
-   Test date and approximate time
-   Any error message shown

Do not include passwords, private documents, personal identifiers, or
unrelated system logs in a report.

## 3. Download and file verification

When a release includes a SHA-256 checksum:

1.  Download the game from the intended GitHub Release.
2.  Verify the checksum using a trusted local tool and the value
    published by the developer.
3.  If the checksum differs, do not run the file. Tell the developer
    which release asset was downloaded and report the mismatch.
4.  Do not assume that a matching hash proves a program is safe; it only
    indicates that the file matches the published reference.

If no checksum is published, note that in the feedback. Do not invent or
guess a checksum.

## 4. Test procedure

### A. Launch and basic navigation

-   [ ] The downloaded game starts.
-   [ ] The game displays its title and version.
-   [ ] The main screen is readable at the test machine's display scale.
-   [ ] Buttons and navigation controls work.
-   [ ] The game can be closed normally.
-   [ ] Reopening the game does not immediately produce an error.

### B. Case briefing and evidence

-   [ ] CASE-001 opens.
-   [ ] The case briefing is understandable.
-   [ ] Evidence IDs are visible and unique.
-   [ ] Timestamps and source names are readable.
-   [ ] The evidence list can be reviewed without accidental loss of
    progress.
-   [ ] Evidence from `DEV-104` is distinguishable from evidence from
    the separate test environment.
-   [ ] The interface distinguishes recorded observations from
    interpretations.
-   [ ] Network metadata is not described as proof of transferred
    content unless the evidence actually supports that claim.

Report any contradictory timestamps, unexplained device changes, missing
evidence, or unclear relationships.

### C. Questions and explanations

-   [ ] Each question displays the expected four options.
-   [ ] All options are readable and selectable.
-   [ ] The selected option is visually clear.
-   [ ] The game accepts the answer once and responds consistently.
-   [ ] The explanation appears after the answer, according to the
    intended design.
-   [ ] The explanation cites relevant evidence IDs.
-   [ ] The explanation covers why the alternatives are weaker or
    unsupported.
-   [ ] The feedback does not reveal a conclusion that contradicts the
    evidence shown.
-   [ ] The next-question and back-navigation behavior is consistent
    with the design.

Testers should report a question if two answers seem equally defensible
using only the evidence available in the game. Include the question ID
and the evidence that supports each interpretation; do not simply report
that a question was difficult.

### D. Score and progress

-   [ ] The displayed score matches the expected result for the tested
    answers.
-   [ ] Correct and incorrect answers are handled consistently.
-   [ ] Hints, if present in this build, follow the documented rules.
-   [ ] Progress is saved when expected.
-   [ ] Closing and reopening the game preserves saved progress.
-   [ ] A new profile or fresh test state behaves as documented.
-   [ ] One player's test data does not appear in another player's
    profile on a shared test machine.

Exact score values and replay behavior must be documented before these
checks can be judged as pass or fail.

### E. Error handling and integrity checks

-   [ ] Missing or invalid data produces a useful error rather than an
    unexplained crash, where practical.
-   [ ] The game does not delete player saves in response to an
    integrity warning.
-   [ ] Integrity warnings explain what was detected without making
    unsupported accusations.
-   [ ] The game does not scan or modify unrelated files or networks.
-   [ ] The game can close safely after an error.
-   [ ] A test of corrupted or altered data is performed only with a
    disposable test copy, never the tester's only save.

Do not try to bypass security software, disable protections, or modify
unrelated system settings to make the game run. If security software
flags the build, record the product name and message and contact the
developer.

### F. Windows packaging and update behavior

-   [ ] The game starts on a machine without Python installed.
-   [ ] The build runs under an ordinary user account.
-   [ ] Required resources and data files are included.
-   [ ] The game can write its save data to the intended user-data
    directory.
-   [ ] Updating the game does not unexpectedly erase the save.
-   [ ] Uninstalling or replacing the application has the documented
    effect on saves.
-   [ ] The Release notes accurately describe known issues and
    requirements.

Do not claim support for a Windows version or device configuration until
it has been tested.

## 5. Test result definitions

Use one of these statuses for each test:

-   **PASS:** The observed behavior matches the documented expected
    behavior.
-   **FAIL:** The observed behavior does not match the expected behavior
    and can be reproduced.
-   **BLOCKED:** The test could not be performed because a prerequisite
    or feature is missing.
-   **NOT TESTED:** The test has not been attempted.
-   **NEEDS CLARIFICATION:** The expected behavior is not documented
    well enough to judge the result.

A test marked PASS should include enough detail to show what was tested.
Do not mark a feature as passed merely because the game opened.

## 6. Bug report template

Copy and complete this template when reporting a problem.

### Summary

A short description of the problem.

### Build

-   Game version:
-   Windows version:
-   First launch or update:
-   Python installed? Yes / No / Unknown

### Steps to reproduce

1.  
2.  
3.  

### Expected result

What you expected the game to do.

### Actual result

What happened instead. Include the exact error text when possible.

### Reproducibility

-   Every time
-   Sometimes
-   Happened once
-   Not yet reproducible

### Severity

-   **Blocker:** The game cannot be used or important data may be lost.
-   **High:** A core feature or case cannot be completed correctly.
-   **Medium:** A feature is impaired but a workaround exists.
-   **Low:** Minor visual, wording, or usability issue.

### Evidence

Attach a screenshot or short screen recording only if it does not expose
private information. Include question or evidence IDs when relevant.

### Additional notes

Any other details that may help reproduce the problem.

## 7. Feedback about case quality

For CASE-001, testers should also consider:

-   Were the evidence sources understandable?
-   Could the timeline be reconstructed from the records?
-   Did any question have two equally plausible answers?
-   Did any explanation rely on evidence that was never shown?
-   Were facts, inferences, and unknowns clearly distinguished?
-   Did the case feel challenging but fair?
-   Was there enough information to make the best choice without
    guessing?

A tester may disagree with the intended answer. That is useful feedback
if they explain their reasoning and cite the evidence that led them
there.

## 8. Suggested test session

For the first small-group test, use this sequence:

1.  Give testers the release notes and this guide.
2.  Ask each tester to install and launch the build without live help,
    if practical.
3.  Ask them to complete CASE-001 and record unclear evidence or
    questions.
4.  Ask them to close and reopen the game to verify progress
    persistence.
5.  Collect bug reports and usability feedback separately.
6.  Review reports, reproduce issues, and prioritize fixes.
7.  Publish a new alpha only after the most serious issues are
    addressed.

The first session should test the experience as a whole, not just
whether the application opens.

## 9. Tester privacy and safety

-   Use fictional in-game data only.
-   Do not upload personal documents, passwords, or unrelated system
    logs.
-   Do not run the game on a device where you are not authorized to
    install software.
-   Do not disable antivirus or operating-system security protections to
    run a test build.
-   If the game unexpectedly accesses unrelated files, changes system
    settings, or behaves in a way that seems unsafe, close it if
    possible and tell the developer.
-   Keep test saves disposable until the save system has been verified.

## 10. Alpha exit criteria

The first alpha should not be treated as ready for broader distribution
until:

-   The build starts on the documented target environment.
-   CASE-001 can be completed from start to finish.
-   All six planned questions have one defensible best answer and
    explanations for every option.
-   No known blocker or high-severity issue remains unresolved.
-   Saving and reopening progress have been tested.
-   The packaged build has been tested on a clean Windows environment
    without Python.
-   Release notes, known issues, and tester instructions match the
    actual build.
-   The developer has reviewed tester feedback and documented any
    remaining limitations.
