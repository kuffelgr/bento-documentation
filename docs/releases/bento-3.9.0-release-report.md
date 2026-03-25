# Bento Framework 3.9.0 — Release Report

**NCI / CBIIT — FNL Bento Team**  
**Generated:** March 25, 2026  
**Jira Version:** `Bento 3.9.0`  
**Next Version:** `Bento 4.0.0`

---

## Executive Summary

Bento 3.9.0 was a focused release centered on two major themes: completing the **Authentication & Authorization (A&A) feature set** and a significant **backend architecture shift** from Neo4j to Elasticsearch (ES) as the primary query engine for the platform's core data operations.

On the A&A side, this release closed out outstanding user role management stories — including admin toggle functionality, inactive member visibility rules, and session timeout — that had been in flight since the A&A initiative began. A suite of Design QA tickets from the 3.8.0 cycle was also resolved, cleaning up the visual and interaction fidelity of the Admin Portal, DAR page, and Login menu.

On the backend, 3.9.0 delivered a systematic migration of all major query types — count, subject, list, details, cart — from Neo4j (Cypher/Bolt) to Elasticsearch. This migration reduces read load on Neo4j, enables faster aggregation queries, and lays the groundwork for more flexible data querying patterns. The backend also shipped a separate repo split, a Redis removal, hybrid query support, and improved error handling for the file service.

| Category | Count |
|---|---|
| Completed Stories & Tasks | 37 |
| Bugs Fixed | 13 |
| Open QA Tests (pending closure) | 3 |
| Duplicate/Cancelled (excluded from active totals) | 23 |

> **Note:** 23 tickets in this version are marked as Duplicate or Cancelled. These are excluded from the section counts below. Several duplicate tickets appear to be double-entries from a version migration or batch re-tagging. The 3 open QA test tickets are formal test execution scripts, not blocking defects.

---

## Section 1: Completed Work

All items below are tagged `fixVersion = "Bento 3.9.0"` and carry a `Closed / Done` resolution in Jira (excluding Duplicates and Cancelled).

### Frontend: Authentication & Authorization — User Role Management

| Ticket | Summary | Assignee |
|---|---|---|
| BENTO-2143 | Admins can enable/disable the admin permissions of a user account | Sohil |
| BENTO-2114 | Removing Admin role reinstates previous access | Sohil |
| BENTO-2118 | Inactive Members can see pending requests | Sohil |
| BENTO-2165 | End User should not make profile changes on DAR when no additional requests can be submitted | Sohil |
| BENTO-2050 | [Revoked and Rejected] status should not be listed on User Profile page | Sohil |

### Frontend: Session Management

| Ticket | Summary | Assignee |
|---|---|---|
| BENTO-1543 | Authenticated user gets a warning before the session timeout | Sohil |
| BENTO-1546 | Design for session termination or expiration | Kuffel |

### Frontend: UI & UX Improvements

| Ticket | Summary | Assignee |
|---|---|---|
| BENTO-2194 | Modify footer to meet NCI style criteria | Sohil |
| BENTO-2138 | Improve the color palette for Explore Dashboard | Stogsdill |
| BENTO-2161 | End user sees a spinner before results are displayed | Sohil |
| BENTO-2154 | FE: Standardize the Account Name in the Frontend | Sohil |
| BENTO-2136 | FE: upgrade NodeJS version | Sheth |
| BENTO-2157 | Remove JBrowse from Bento-components | Sohil |
| BENTO-1818 | Custodian users can use config file to map API and ES Query | David |
| BENTO-2137 | Design: Color palette for Explore Dashboard | Kuffel |
| BENTO-2142 | Design: Improve role assignments | Kuffel |

### Backend: Elasticsearch Query Migration

The most substantial engineering work in 3.9.0 was a full migration of the backend query layer from Neo4j Cypher to Elasticsearch. Each Jira task below corresponds to one category of GraphQL query type being rewired to use ES as the data source rather than querying Neo4j directly.

| Ticket | Summary | Assignee |
|---|---|---|
| BENTO-2003 | BE – migrate simple count queries to ES | Ying |
| BENTO-2004 | BE – migrate details queries to ES | Ying |
| BENTO-2005 | BE – migrate list queries to ES | Ying |
| BENTO-2006 | BE – migrate subject queries to ES | Mueller |
| BENTO-2007 | BE – migrate cart queries to ES | Mueller |
| BENTO-1678 | BE: refactor BE Elasticsearch code | Ying |
| BENTO-2022 | BE – ES query configuration document | Mueller |

### Backend: Architecture & Infrastructure

| Ticket | Summary | Assignee |
|---|---|---|
| BENTO-2129 | BE – separate BE repo | Mueller |
| BENTO-2128 | BE – add "hybrid" query support | Mueller |
| BENTO-2132 | DevOps – remove Redis | Mueller |
| BENTO-2145 | DevOps – update pipelines to deploy from new backend repo | Ying |
| BENTO-2150 | BE: Standardize the Account Name in the backend | Sheth |
| BENTO-2151 | BE – Update API to handle user changing from Admin to Member | Mueller |
| BENTO-2160 | BE – /login API returns session expiration time | Mueller |
| BENTO-2166 | BE: Inactivity Timeout API | Sheth |
| BENTO-2131 | BE – add DB connection health check API endpoints | Mueller |
| BENTO-2133 | BE – file copier verifies file size | Ying |
| BENTO-2083 | BE: file service return 401 error for authentication errors | Ying |

---

## Section 2: Bugs Fixed

13 bugs were resolved and closed during the 3.9.0 cycle (excluding duplicates).

| Ticket | Description | Priority |
|---|---|---|
| BENTO-2171 | Data is not loading on Explore and Programs pages | Blocker |
| BENTO-2193 | Global Search – Data Model category returning no results | Blocker |
| BENTO-2175 | Role should not revert back to Non-Member when admin permissions are disabled | Critical |
| BENTO-2174 | Inactive Members cannot see the "Request Data Access" button | Critical |
| BENTO-2164 | When user finds a case through local find, it keeps spinning with no results | Critical |
| BENTO-2140 | Study Arm(s) dropdown not showing "Arm X … and more" when multiple arms are selected | Critical |
| BENTO-1821 | File Cart error when user adds sample file to cart | Critical |
| BENTO-1588 | JBrowse is not able to fetch data for My Alignments and My Variants | Critical |
| BENTO-2186 | Dashboard table – unable to download file from Access column | Major |
| BENTO-2172 | Dashboard table – ADD ALL FILES button non-functional on Cases and Samples tabs | Major |
| BENTO-2159 | Custodian – Submit button disabled if node-level access is false | Major |
| BENTO-2125 | Admin Portal – Error loading component: "Error: undefined" | Major |
| BENTO-2124 | Login.gov/NIH accounts – Access denied page shown when user denies login request | Major |

---

## Section 3: Design QA Resolved (3.8.0 Carry-Forward)

5 Design QA tickets from the 3.8.0 release cycle were formally closed in 3.9.0. These tickets tracked visual and interaction fidelity reviews across the A&A surfaces.

| Ticket | Description | Assignee |
|---|---|---|
| BENTO-2107 | Design QA 3.8.0 – Login Menu | Kuffel |
| BENTO-2108 | Design QA 3.8.0 – Admin Portal: Manage Access & Pending Requests tabs | Chen (Yizhen) |
| BENTO-2109 | Design QA A&A – Admin Portal: Approved Arms | Kuffel |
| BENTO-2110 | Design QA A&A – Admin Portal: Edit User Page | Kuffel |
| BENTO-2111 | Design QA 3.8.0 – Admin Portal: Review DAR page | Tesfatsion |
| BENTO-2112 | Design QA 3.8.0 – DAR page Part 1 | Stogsdill |

---

## Section 4: Open QA Tests (Pending Closure)

3 formal QA test tickets remain open against the 3.9.0 version. These are test execution scripts, not defects.

> **Action Required:** Schedule a testing sprint to close these. The session timeout test (BENTO-2183) requires a live authenticated session in a target environment; the admin role reversion test (BENTO-2184) requires an account with admin privileges.

| Ticket | Test Description |
|---|---|
| BENTO-2183 | Test: Authenticated user gets a warning before the session timeout |
| BENTO-2184 | Test: Removing Admin role reinstates previous access |
| BENTO-2187 | Test: FE – Standardize the Account Name in the Frontend |

---

## Section 5: Items Cancelled in Bento 3.9.0

The following stories were scoped into 3.9.0 but closed as Cancelled, reflecting a deliberate decision to simplify the user role model.

- **BENTO-2121** — Admin should not be able to convert a Non-Member to a Member — Cancelled. The design decision was made to allow direct Non-Member → Admin promotion instead.
- **BENTO-2113** — A Non-Member can be converted to an Admin — Cancelled (superseded by a revised role management design tracked in BENTO-2142 / BENTO-2143).
- **BENTO-2149** — After user logs out, "My Files" count still shows previous cart count — Cancelled (accepted behavior; session state cleared on next login).

---

## Section 6: Team Contributions

| Team Member | Role | Primary Focus Area |
|---|---|---|
| Sohil, Zalmay | Frontend Engineer | A&A role management, session timeout, UI polish, bug fixes |
| Mueller, Austin | Backend Lead | ES query migration (subject, cart), hybrid query, Redis removal, repo split, auth APIs |
| Ying, Ming | Backend Engineer | ES query migration (count, details, list), ES refactor, file copier, DevOps pipeline |
| Sheth, Karan | Frontend Lead | NodeJS upgrade, backend account name standardization, inactivity timeout API |
| David, Sofia | Frontend Engineer | Custodian ES/API config mapping, DAR bug fixes |
| Stogsdill, Hannah | UI/UX Designer | Explore Dashboard color palette, DAR page design QA |
| Tesfatsion, Nahom | QA Engineer | Admin Portal / DAR design QA |
| Chen, Yizhen | Engineer | Admin Portal design QA |
| Kuffel, Gina | Technical PM | Design: role assignments, session termination, Explore Dashboard color palette, Design QA (Login, Admin Portal) |

---

*Generated from Jira (fixVersion = "Bento 3.9.0") — NCI / CBIIT FNL Bento Team — bento-help@nih.gov*
