# Bento Framework 4.0.0 — Release Report & Future Roadmap

**NCI / CBIIT — FNL Bento Team**  
**Generated:** March 25, 2026  
**Jira Version:** `Bento 4.0.0`  
**Next Version:** `Bento X`

---

## Executive Summary

Bento 4.0.0 was a foundational engineering release — not a user-facing feature release. The central mission of 4.0 was to pay down significant technical debt by decomposing a large, monolithic React application into a library of independently-publishable, reusable components (the **Bento-Core** package). This refactoring enables future data commons projects (ICDC, CTDC, and others) to consume shared components from a single source of truth rather than maintaining separate forks of the same code.

In parallel, the backend team upgraded the Java runtime, replaced deprecated and vulnerable libraries, introduced login event recording for audit trail support, and built the foundation for token-based authentication. The DevOps team upgraded core infrastructure, and the project team completed an end-to-end documentation update covering every major Bento page configuration.

| Category | Count |
|---|---|
| Completed Stories & Tasks | 65 |
| Bugs Fixed | 18 |
| Open QA Tests (pending closure) | 8 |
| Bento X Roadmap Items | 37 |

> **Note:** The 8 open QA test tickets are formal test execution scripts, not blocking defects. Several are gated on DAR email notification infrastructure that was under active development at the end of the 4.0 cycle.

---

## Section 1: Completed Work

All items below are tagged `fixVersion = "Bento 4.0.0"` and carry a `Closed` resolution in Jira.

### Frontend: Component Modularization (Bento-Core)

| Ticket | Summary | Assignee |
|---|---|---|
| BENTO-2196 | Refactor Side Bar Component | Radhakrishnan |
| BENTO-2197 | Refactor Tabs Component (Dashboard) | David |
| BENTO-2199 | Refactor Stats Bar Component | Tatekar |
| BENTO-2226 | Refactor Widgets Grid Component | Radhakrishnan |
| BENTO-2284 | Refactor Access Control Component | Radhakrishnan |
| BENTO-2265 | Refactor Bento Cart | Radhakrishnan |
| BENTO-2280 | Refactor Server Paginated Table (Dashboard / Explore) | Tatekar |
| BENTO-2292 | Refactor Query Bar Component (Dashboard) | Tatekar |
| BENTO-2293 | Refactor Local Find | Tatekar |
| BENTO-2294 | Refactor Session Timeout Component | Tatekar |
| BENTO-2296 | Refactor Login Page | David |
| BENTO-2330 | Refactor User Profile Page as Component | Sohil |
| BENTO-2340 | Refactor Data Access Request (DAR) Page as Component | Sohil |
| BENTO-2336 | Replace Associated Sample / Files tables with Bento-Core Table Component | Sheth |

### Frontend: Admin Portal Refactor

| Ticket | Summary | Assignee |
|---|---|---|
| BENTO-2270 | Admin Portal – Refactor Manage Access Table | Radhakrishnan |
| BENTO-2271 | Admin Portal – Refactor Pending Access Table | Radhakrishnan |
| BENTO-2272 | Admin Portal – Refactor User Details View | Radhakrishnan |
| BENTO-2273 | Admin Portal – Refactor Revoke Access Table | Radhakrishnan |
| BENTO-2274 | Admin Portal – Refactor Request Access Table | Tatekar |

### Frontend: Global Search Refactor

| Ticket | Summary | Assignee |
|---|---|---|
| BENTO-2278 | Global Search – Refactor Search Bar (Header) | David |
| BENTO-2279 | Global Search – Refactor Search Results | Radhakrishnan |
| BENTO-2331 | Migrate FacetFilter Component as Separate Package | Sheth |
| BENTO-2332 | Migrate Global Search Component as Separate Package | Sheth |
| BENTO-2334 | Migrate Paginated Table Component as Separate Package | Sheth |

### Frontend: Bento-Core Library Infrastructure

| Ticket | Summary | Assignee |
|---|---|---|
| BENTO-2223 | Stats Bar – Design Configuration | Sheth |
| BENTO-2224 | Stats Bar – Extract Existing Component | Sheth |
| BENTO-2225 | Implement Refactored Stats Bar Component | Sheth |
| BENTO-2227 | Widget Component – Design Configuration | Sheth |
| BENTO-2228 | Widgets Grid – Extract Existing Components | Sheth |
| BENTO-2229 | Implement Refactored Widgets Grid Component | Sheth |
| BENTO-2231 | Design Sidebar Redux State Object & Redux Thunks | Sheth |
| BENTO-2236 | Sidebar – Implement Reducer Functions & Redux Thunks | Sheth |
| BENTO-2237 | Implement Refactored Sidebar Component | Sheth |
| BENTO-2239 | Design Tab Table Component Redux State Object & Thunks | Sheth |
| BENTO-2262 | Investigate viable options for Bento-Core | Sheth |
| BENTO-2267 | Sidebar – Design Component & Configurations | Sheth |
| BENTO-2277 | Global Search – Extract Existing Component | Sheth |
| BENTO-2281 | Server Paginated Table – Extract Existing Component | Sheth |
| BENTO-2282 | Server Paginated Table – Implement Local State Management | Sheth |
| BENTO-2283 | Server Paginated Table – Wrapper component for Add to Cart buttons | Sheth |
| BENTO-2302 | Exploring Release and Contribution Process for Bento-Core | Sheth |
| BENTO-2316 | Implement infrastructure for Bento-Core | Sheth |
| BENTO-2190 | Bento Refactoring State Management Planning & Design | Chen (Kai-Ling) |

### Frontend: Auth, Security & Compliance

| Ticket | Summary | Assignee |
|---|---|---|
| BENTO-2155 | Display government warning banner upon application entry (AC-8) | Sohil |
| BENTO-2337 | Add Support for Bento FE 3.10 and services (A&A Disabled) | David |
| BENTO-2244 | Evaluate complexity of future ICDC Bentofication | Sheth |
| BENTO-2439 | Custodian Configuration with Bento-Local | David |
| BENTO-2440 | End user sees Stats Bar icons | David |

### Frontend: Test Automation IDs

| Ticket | Summary | Assignee |
|---|---|---|
| BENTO-2295 | Sidebar – Add Missing IDs for Test Automation | Sohil |
| BENTO-2299 | Local Find – Add IDs for Test Automation | Sohil |
| BENTO-2300 | Case Details – Add Missing IDs for Test Automation | Sohil |
| BENTO-2301 | Global Search – Add IDs for Test Automation | Sohil |

### Backend: Auth, Audit & Security

| Ticket | Summary | Assignee |
|---|---|---|
| BENTO-2181 | Audit Trail Planning and Design | Mueller |
| BENTO-2195 | Add Login Event Recording | Yoo |
| BENTO-2251 | Develop a plan for migrating to token-based authentication | Mueller |
| BENTO-2276 | Add token-based authentication to Bento AuthN/AuthZ API | David |
| BENTO-2259 | Upgrade Bento Backend dependencies with known vulnerabilities | Mueller |
| BENTO-2256 | Resolve Bento Backend Dependency Issues | Tatekar |
| BENTO-2241 | Replace deprecated express-graphql library | Mueller |
| BENTO-2242 | Replace the YAML parsing library in Bento-Backend | Ying |
| BENTO-2341 | Simplify YAML config for sliders | Mueller |
| BENTO-2441 | Fix Backend API for larger CSV files in Local Find | Mueller |

### Infrastructure & DevOps

| Ticket | Summary | Assignee |
|---|---|---|
| BENTO-2168 | Create a separate Neo4j process for Authorization service | Yoo |
| BENTO-2285 | Upgrade Java version from Java 11 to Java 17 | Donkor |
| BENTO-2308 | Fix bento-help@nih.gov for external users | Chen (Kai-Ling) |
| BENTO-2344 | Set up Bento Framework 4.0.0 on Linux using Bento-Local | Sohil |

### Documentation

| Ticket | Summary | Assignee |
|---|---|---|
| BENTO-2342 | Update Bento Docs for Dashboard Page | Kuffel |
| BENTO-2385 | Update Bento Docs (Custodian) for Authentication | Sheth |
| BENTO-2386 | Update Bento Docs (Custodian) for Authorization | Sheth |
| BENTO-2387 | Update Bento Docs (Custodian) for DAR Service | Sheth |
| BENTO-2388 | Update Bento Docs (Custodian) for Global UI Elements | Kuffel |
| BENTO-2389 | Update Bento Docs (Custodian) for Landing Page | Kuffel |
| BENTO-2390 | Update Bento Docs (Custodian) for Programs Page | Kuffel |
| BENTO-2391 | Update Bento Docs (Custodian) for Program Details Page | Kuffel |
| BENTO-2392 | Update Bento Docs (Custodian) for Arm Detail Page | Kuffel |
| BENTO-2393 | Update Bento Docs (Custodian) for Case Details Page | Kuffel |
| BENTO-2395 | Update Bento Docs (Custodian) for File-Centric Cart Page | Kuffel |
| BENTO-2396 | Update Bento Docs (Custodian) for Static Pages | Kuffel |

---

## Section 2: Bugs Fixed

18 bugs were resolved and closed during the 4.0.0 cycle.

| Ticket | Description | Priority |
|---|---|---|
| BENTO-2419 | File download from Access column in Dashboard table broken | Critical |
| BENTO-2179 | JBrowse: My Alignments and My Variants not showing as available tracks | Critical |
| BENTO-2424 | Sort order alternating incorrectly on Dashboard, Cart, and Case Detail tables | Major |
| BENTO-2434 | Add All Files button non-functional when Dashboard table has 0 records | Major |
| BENTO-2432 | File tab and Cart page missing top scrollbar | Major |
| BENTO-2378 | Tab switching causing widget refresh on Explore page | Major |
| BENTO-2354 | Menopause Status filter: Postmenopausal selection hiding Premenopausal option | Major |
| BENTO-2328 | Access column showing lock icon for approved Arms | Major |
| BENTO-2210 | Explore page crash on large CSV file upload in Local Find | Major |
| BENTO-2209 | File Cart page blank after deleting 100th row | Major |
| BENTO-2461 | Custodian Conf: Static page config changes not visible in Bento UI | Major |
| BENTO-2463 | Custodian Conf: Arm detail page config changes not visible in Bento UI | Major |
| BENTO-2374 | Dashboard tab colors displaying as grey | Minor |
| BENTO-2381 | Tumor size filter values not in proper order | Minor |
| BENTO-2397 | Incorrect sequence of fields under Chemotherapy filter | Minor |
| BENTO-2425 | Dashboard column names have default underlines | Minor |
| BENTO-2427 | Admin Portal: Default underline missing in Study Arms column | Minor |
| BENTO-1450 | Range slider: User able to enter Min value in Max field | Minor |

---

## Section 3: Open QA Tests (Pending Closure)

8 formal QA test tickets remain open against the 4.0.0 version. These are test execution scripts, not defects.

> **Action Required:** Assign a testing sprint to close these. The DAR email notification tests (BENTO-2446, 2447, 2448) depend on the backend email service being active in the target test environment.

| Ticket | Test Description |
|---|---|
| BENTO-2382 | Test: Refactor Server Paginated Table (Dashboard / Explore Page) |
| BENTO-2383 | Test: FE – Local Search |
| BENTO-2443 | Test: Admin Portal – Refactor Request Access Table |
| BENTO-2445 | Test: Admin Portal – Review Data Access Request(s) |
| BENTO-2446 | Test: Admin Portal – Email notification (DAR approval) |
| BENTO-2447 | Test: Admin Portal – Email notification (DAR rejection) |
| BENTO-2448 | Test: Admin Portal – Email notification for submitted request (to Admin) |
| BENTO-2581 | Test: Verify Auth & Authorization custodian configurations on Bento Frontend |

---

## Section 4: Roadmap — Bento X

37 tickets are currently targeted at Bento X across six strategic themes. This cycle shifts from the internal refactoring focus of 4.0 toward platform modernization, security hardening, database flexibility, and a new interactive data model visualization tool.

### Frontend Modernization

The Webpack 4 → 5 upgrade is the most critical dependency for several downstream features. Webpack 5's Module Federation is what will eventually allow Bento-Core components to be served as remote micro-frontends. Node.js must also be upgraded to LTS v22 to remain on a supported runtime. A Login.gov authentication blocker (BENTO-2123, priority: **Blocker**) and a missing environment variable crash (BENTO-2156) are outstanding and require priority attention before the next production deployment.

| Ticket | Type | Summary | Status |
|---|---|---|---|
| BENTO-2617 | Epic | Upgrade Webpack from version 4 to 5 | Open |
| BENTO-2622 | Story | Upgrade Webpack for Bento Frontend Application 4.0 → 5.0 | Ready for Review |
| BENTO-2624 | Story | Upgrade Node.js to v22.13.0 | Open |
| BENTO-2626 | Story | Create a Node Upgrade Plan | Open |
| BENTO-2654 | Bug | UI Breaking on GraphiQL Page in Bento Reference Impl. | In Progress |
| BENTO-2575 | Bug | Warning message box empty when >1000 files added to cart | Ready for Review |
| BENTO-2650 | Bug | Fix Header fixed-position on scroll | ✅ Closed |
| BENTO-2653 | Story | Preserve Slider Facet States in Shared Links | Ready for Review |

### Security Audit & Hardening

A full security audit is scoped across both frontend and backend. On the frontend, Nahom Tesfatsion is leading an npm dependency vulnerability scan and remediation. On the backend, Adam Davenport is leading a review of the Java microservices (Auth, File, and User services), database query security, and environment variable handling. Two auth-related bugs are currently on hold and need re-evaluation.

| Ticket | Type | Summary | Status |
|---|---|---|---|
| BENTO-2618 | Epic | Comprehensive security audit and fix frontend vulnerabilities | Open |
| BENTO-2619 | Epic | Audit and improve backend security and features | Open |
| BENTO-2644 | Task | Security Audit – Frontend codebase dependency scan | Ready for Review |
| BENTO-2645 | Task | Perform Dependency Updates (post-audit) | Open |
| BENTO-2625 | Story | Address Security Vulnerabilities in Bento Frontend | In Progress |
| BENTO-2630 | Story | Address Security Vulnerabilities in Bento Backend | In Progress |
| BENTO-2572 | Bug | Disable account: Users/Admins not receiving system emails | On Hold |
| BENTO-2123 | Bug | Authentication: User unable to login with Login.gov IdP | Open — **Blocker** |
| BENTO-2156 | Bug | Missing REACT_APP_GOOGLE_CLIENT_ID breaking Bento-local app | Open |

### Database Migration: MemGraph

This is the most architecturally significant item in Bento X. The team is evaluating MemGraph (an open-source, Neo4j-compatible graph database) as an alternative to Neo4j, primarily for licensing cost and performance reasons. Investigation has confirmed that MemGraph can ingest Bento data using the ICDC dataloader and that APOC replacements have been written for OpenSearch indexing. The next major milestone is a database abstraction layer that allows a single Bento deployment to switch between Neo4j and MemGraph via configuration only.

| Ticket | Type | Summary | Status |
|---|---|---|---|
| BENTO-2627 | Epic | Assess viability of migrating from Neo4j to MemGraph | Open |
| BENTO-2621 | Epic | Plan and execute backend database migration | Open |
| BENTO-2628 | Story | Add Support for MemGraph (Backward Compatible with Neo4j) | In Progress |
| BENTO-2646 | Task | Investigate loading Bento data via Neo4j dump files | Ready for Review |
| BENTO-2647 | Task | Create Bento APOC Replacement + Indices for OpenSearch (Neo4j) | ✅ Closed |
| BENTO-2648 | Task | Create Bento APOC Replacement + Indices for OpenSearch (MemGraph) | ✅ Closed |
| BENTO-2649 | Task | Investigation: Integrating MemGraph into existing Bento framework | ✅ Closed |
| BENTO-2629 | Story | Define Migration Testing Strategy | Open |

### Data Model Navigator (DMN)

The Data Model Navigator is a new interactive graph visualization component that allows end users to explore the Bento data model directly in the UI. It is being built as a new package inside Bento-Core, with self-contained local state (replacing global Redux) so it can be embedded in any Bento application with minimal configuration. The component includes a graph view (upgrading to xyFlow/ReactFlow v2), table view, filter sidebar, and download capabilities (PDF, TSV). High-visibility feature for ICDC and CTDC.

| Ticket | Type | Summary | Status |
|---|---|---|---|
| BENTO-2656 | Epic | DMN – overarching epic | Open |
| BENTO-2623 | Story | Integration of Data Model Navigator into Bento | Ready for Review |
| BENTO-2639 | Task | Set up Navigator in bento-core component | Ready for Review |
| BENTO-2640 | Task | Filter Component / Filter Logic refactor | Ready for Review |
| BENTO-2641 | Task | Graph View Component (upgrade to xyFlow / ReactFlow v2) | Ready for Review |
| BENTO-2642 | Task | Table View Component (with PDF and TSV download) | ✅ Closed |
| BENTO-2643 | Task | Refactor Header Component | ✅ Closed |
| BENTO-2632 | Task | Restore List item style for Acceptable Values | Ready for Review |
| BENTO-2633 | Task | Restore Tab Styles (MUI emotion styled) | Ready for Review |
| BENTO-2634 | Task | Restore Legend to Canvas | Ready for Review |
| BENTO-2635 | Task | Restore Filter Feature and Style (accordion, sort, clear) | Ready for Review |
| BENTO-2636 | Task | Restore Query Search Behavior and Style | Ready for Review |
| BENTO-2655 | Story | Navigator – Add Data Hub Configuration | In Progress |
| BENTO-2611 | Bug | GraphQL page queries giving error in reference impl. | On Hold |
| BENTO-2468 | Bug | Local Find: Unmatched case showing in Matched tab | Ready for Review |

### Documentation

| Ticket | Type | Summary | Status |
|---|---|---|---|
| BENTO-2620 | Epic | Develop comprehensive new documentation (Developer Guide, FAQ, Contribution Guide) | Open |

### Backend Testing

| Ticket | Type | Summary | Status |
|---|---|---|---|
| BENTO-2303 | Epic | Improve and Expand Unit Testing Coverage for Bento Microservices | In Progress |

---

## Section 5: Team Contributions

| Team Member | Role | Primary Focus Area |
|---|---|---|
| Sheth, Karan | Frontend Lead | Bento-Core infrastructure, state management architecture, component extraction |
| Radhakrishnan, Gayathri | Frontend Engineer | Admin Portal refactor, Cart, Access Control, Sidebar, Global Search |
| David, Sofia | Frontend Engineer | Bug fixes, Login refactor, DAR page, Auth support, Custodian config |
| Tatekar, Ashwini | Frontend / QA | Query bar, Local Find, Session Timeout, Stats Bar, test execution |
| Sohil, Zalmay | Frontend Engineer | Test automation IDs, Local Find backend fix, Gov. warning banner |
| Mueller, Austin | Backend Lead | Auth/audit planning, token-based auth design, library upgrades, CSV fix |
| Yoo, Siyoung | Backend Engineer | Login event recording, Neo4j auth service separation |
| Ying, Ming | Backend Engineer | YAML library replacement |
| Donkor, Vincent | DevOps Engineer | Java 11 → 17 upgrade |
| Chen, Kai-Ling | Technical Lead | State management planning, help desk fix |
| Kuffel, Gina | Technical PM | Documentation: all custodian configuration guides, Dashboard page docs |

---

## Section 6: Items Cancelled / Deferred in Bento 4.0.0

The following items were scoped into 4.0.0 but closed as Cancelled or superseded by a redesign. Most reflect a deliberate pivot to the Bento-Core componentization approach, which made earlier ticket formulations obsolete.

- **BENTO-1617, 1619, 1636, 1615** — Dashboard componentization stories (SideBar, Sections, Groups, Checkbox) — superseded by the Bento-Core extraction approach.
- **BENTO-1643, 1648, 1649, 1653** — Dashboard state management components — same supersession.
- **BENTO-2200, 2203, 2238** — Split widgets/local find state management to separate functions — folded into the Bento-Core library design.
- **BENTO-2240** — Improve and Expand Unit Testing Coverage — deferred to Bento X (now tracked as BENTO-2303).
- **BENTO-2252** — Add access-token login endpoint — cancelled in favor of the broader token-based auth design (BENTO-2251, 2276).
- **BENTO-2311, 2312, 2313, 2314, 2315** — Individual bento-docs updates for SideBar, Widgets, GlobalSearch, StatsBar, Table — replaced by the comprehensive custodian configuration documentation suite (BENTO-2385–2396).
- **BENTO-2037** — Update code to process environment variables by deployment context — cancelled.

---

*Generated from Jira (fixVersion = "Bento 4.0.0" + "Bento X") — NCI / CBIIT FNL Bento Team — bento-help@nih.gov*
