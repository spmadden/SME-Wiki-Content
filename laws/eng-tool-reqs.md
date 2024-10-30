---
title: SPM's Engineering Tool Guidelines & Requirements
description: 
published: 1
date: 2024-10-30T20:16:35.152Z
tags: 
editor: markdown
dateCreated: 2024-10-30T20:16:35.152Z
---

# SPM's Engineering Tool Guidelines & Requirements

> The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", “RECOMMENDED",  "MAY", and OPTIONAL" in this document are to be interpreted as described in RFC 2119. 
{.is-info}


### The tool should have the following basic capabilities:

* The tool MUST have the capability to import from common/standard/open formats
  * Text, CSV, IETF RFC, “Open” specifications
* The tool MUST have the capability to export to common/standard/open formats
* The tool MUST have the capability to track changes to the elements stored within it.

### Strong desire-ments:

* The tool SHOULD have the capability to create “snapshots” or “atomic instances in time” that compose the entire state of the tool.
* The tool SHOULD have the capability to view “snapshots” created previously
* The tool SHOULD have the capability to compare/diff two “snapshots”
* The tool SHOULD have the capability to revert the current state back to a previously created “snapshot”
* The tool SHOULD have the capability to partially revert the current state back to a previously created snapshot.
* The tool SHOULD have the capability to (re)-generate previously generated artifacts from the current “best info”
* The tool SHOULD have the capability to (re)-generate previously generated artifacts from tracked snapshots
  * Any re-generated artifacts should be identical to the originally generated artifacts if generated from the same snapshot.

### Bonuses:

* The tool MAY have the capability to allow multiple individuals to work simultaneously without introducing conflicts (“branches/WIPs/Increments”)
* The tool MAY have the capability to track “sets of changes” as atomic data groups (“change-sets/patches”)
* The tool MAY have the capability to review “sets of changes” prior to this set becoming nominated as “most currently correct”