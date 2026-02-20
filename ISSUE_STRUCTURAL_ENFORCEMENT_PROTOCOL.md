# ISSUE STRUCTURAL ENFORCEMENT PROTOCOL

**Version:** 1.0
**Status:** ACTIVE
**Effective Date:** 2026-02-20

## 1.0 Overview

This document defines the permanent safeguards and protocols to maintain the structural integrity of the WebWaka Issue Universe. Adherence to this protocol is mandatory for all contributors and automated systems interacting with WebWaka repositories. This protocol was established as the primary outcome of CSRP-01.

## 2.0 Core Principles

- **Structural Immutability:** The 29-issue structure for every defined biological or runtime component is fixed and shall not be violated.
- **Canonical Naming:** All issues must conform to the strict naming and titling conventions defined herein.
- **Repository Purity:** Each repository is designated for a specific biological layer. Cross-layer contamination is strictly prohibited.
- **Automated Enforcement:** Where possible, structural rules will be enforced by automated checks, validation scripts, and GitHub Actions.

## 3.0 Issue Titling and Structure ID Convention

Every issue that is part of a formal structure **MUST** begin its title with a valid `STRUCTURE_ID` enclosed in square brackets.

### 3.1 Canonical Title Format

The format is `[STRUCTURE_ID-PHASE-TASK] Title Description`.

- **`STRUCTURE_ID`**: The unique identifier for the component (e.g., `ORG-DATASYNC-v0.1.0`). It is composed of `LAYER-COMPONENT-VERSION`.
- **`PHASE`**: The implementation phase, from `P0` to `P6`.
- **`TASK`**: The specific task within the phase. `MASTER` for the main structure issue, or `T01` through `T04` for sub-tasks.

**Example:** `[ORG-DATASYNC-v0.1.0-P1-T02] Implement data validation logic`

### 3.2 Master Issue Format

The master issue for a structure, which defines the component itself, uses a simplified format.

**Format:** `[STRUCTURE_ID] Master Issue`

**Example:** `[ORG-DATASYNC-v0.1.0] Master Issue`

### 3.3 Regex Enforcement

The following regular expressions define a valid structured issue title:

- **Full Issue:** `^\[([A-Z0-9\-\_\.v]+)-P[0-6](-T[0-9]{2})?\]`
- **Master Issue:** `^\[([A-Z0-9\-\_\.v]+)\] Master Issue`

Any issue created that does not match one of these patterns will be flagged as an `ORPHAN_ISSUE` and must be corrected or archived.

## 4.0 Labeling Protocol

Labels are critical for automated parsing and reporting. The following labels are mandatory for all issues.

### 4.1 Layer Labels

Every issue **MUST** have exactly one `layer:` label corresponding to its repository.

- `layer:organelle`
- `layer:cell`
- `layer:tissue`
- `layer:organ`
- `layer:system`
- `layer:runtime`
- `layer:organism`

### 4.2 Structure Labels

Every structured issue **MUST** have a `structure:` label matching its `STRUCTURE_ID`.

- **Format:** `structure:STRUCTURE_ID`
- **Example:** `structure:ORG-DATASYNC-v0.1.0`

### 4.3 Status Labels

- `status:canonical`: The issue is part of the official 29-issue structure.
- `status:orphan`: The issue does not conform to the structural naming convention.
- `status:archived`: The issue is a historical artifact and not part of the active structure (result of CSRP-01 or future cleanup).

## 5.0 Automated Governance

### 5.1 Pre-Commit Hooks

All local development environments should be configured with pre-commit hooks that run a validation script to check for title and label compliance before allowing a commit.

### 5.2 GitHub Actions

A GitHub Action will be deployed on all biological and runtime repositories to perform the following on every `issue` event (`opened`, `edited`):

1.  **Title Validation:** Check if the issue title conforms to the regex defined in Section 3.3.
2.  **Label Validation:** Ensure the correct `layer:` and `structure:` labels are present.
3.  **Orphan Flagging:** If validation fails, automatically add the `status:orphan` label and add a comment notifying the author to correct the issue.
4.  **Structure Count Check:** On issue creation, query the repository to ensure the new issue does not cause a structure to exceed 29 issues. If it does, the issue will be flagged for immediate archival.

## 6.0 Manual Governance and Audits

- **Weekly Audits:** An automated script will run weekly to generate a `STRUCTURAL_REALITY_REPORT` and check for any deviations from this protocol.
- **Quarterly Reviews:** The Founder and core contributors will review the state of the issue universe and make any necessary adjustments to this protocol.

## 7.0 Protocol Amendments

Any amendments to this protocol must be proposed via a pull request to this document in the `webwaka-implementation-governance` repository and require approval from the Founder.
