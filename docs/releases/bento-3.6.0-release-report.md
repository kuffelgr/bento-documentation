# Bento Framework 3.6.0 — Release Report

**NCI / CBIIT — FNL Bento Team**  
**Generated:** March 25, 2026  
**Jira Version:** `Bento 3.6.0`  
**Next Version:** `Bento 4.0.0`

---

## Executive Summary

Bento 3.6.0 was a significant user-facing feature release built around two major themes: **search** and **performance**. The team shipped Global Search — a new cross-application Elasticsearch-powered search capability — alongside Local Find, a case set lookup tool that lets researchers enter or upload a list of case identifiers and filter the dashboard to exactly those records. In parallel, the team tackled serious Explore Dashboard performance problems, delivering measurable improvements to table load times, stats bar/widget rendering, and the Add Files to Cart operation.

The release also introduced JBrowse integration, a genome visualization tool that allows end users to stream and explore BAM files directly in the UI. The Query Bar received a complete overhaul — both a static version (showing active filters as persistent chips) and a dynamic version (allowing inline removal of individual filters) — which became one of the most bug-heavy areas of the release. The Mock Data Generator, a backend tooling investment to support future testing workflows, was also completed in this cycle.

Bento 3.6.0 carried a notably high bug volume compared to prior releases — largely because Global Search, Local Find, and the Query Bar were complex, stateful, and heavily interactive features that surfaced many edge cases during QA. Hot fixes were tagged separately in Jira and indicate areas where defects were severe enough to require immediate out-of-band patching.

| Category | Count |
|---|---|
| Completed User Stories | 30 |
| Completed Tasks | 47 |
| Bugs Closed | 63 |
| Open QA Tests (pending closure) | 4 |
| Total Tickets in Version | 148 |

> **Note:** Bug count is elevated relative to the 4.0.0 cycle because this release was feature-dense and introduced deeply interactive UI behaviors. A significant proportion of bugs were tagged `Hot_Fix`, indicating they were patched on an expedited basis after initial release to the reference environment.

---

## Section 1: Completed Work

All items below are tagged `fixVersion = "Bento 3.6.0"` and carry a `Closed` resolution in Jira.

### Feature: Global Search

Global Search allows end users to search across all Bento data categories — Programs, Arms, Cases, Samples, Files, and the Data Model — from a single search bar in the application header. Results are returned by category with count badges. Results pages are paginated. The feature is powered by Elasticsearch (ES) on the backend.

| Ticket | Type | Summary | Assignee |
|---|---|---|---|
| BENTO-1366 | User Story | End-user can do a global search | Sohil |
| BENTO-1367 | User Story | End-user can filter global search results and counts | Sohil |
| BENTO-1385 | User Story | End-user can follow links from global search results to view details | Sohil |
| BENTO-1391 | User Story | End-user can use auto-complete for terms entered into global search | Sohil |
| BENTO-1404 | User Story | End user can use auto-complete to find a case ID | Sohil |
| BENTO-1419 | User Story | End users can access global search results across the application | David |
| BENTO-1428 | User Story | End user can view global search results in a paginated and ordered manner | David |
| BENTO-1449 | User Story | Reimplement Global Search Bar/Box with UI styling | Sohil |
| BENTO-1472 | User Story | End user can click on magnifying glass of Global Search | Sohil |
| BENTO-1296 | Task | BE – Global Search API | Doddapaneni |
| BENTO-1436 | Task | BE – Global Search results order by ID | Doddapaneni |
| BENTO-1475 | Task | BE – Update API to return Global Search Results | Doddapaneni |
| BENTO-1256 | Task | FE – Styling – Global Search Results page | Wang |
| BENTO-1255 | Task | FE – Styling – Global Search Bar | Doddapaneni |
| BENTO-1336 | Task | FE – Styling for Global Search Result Page | Stogsdill |
| BENTO-1339 | Task | FE – Styling for Global Search box | Chaparala |
| BENTO-1263 | Task | FE – Styling – Filter Query Result section | Stogsdill |
| BENTO-1327 | Task | Design V3: Global Search Results | Kuffel |
| BENTO-1462 | Task | Design: Global Search Results Page | Kuffel |
| BENTO-1509 | Task | Perform UI Styling review for Global Search user stories | Stogsdill |
| BENTO-1243 | Task | Document configuration of elasticsearch backend (DevOps) | Fleming |

### Feature: Local Find

Local Find adds a case set lookup panel to the Explore Dashboard. Researchers can enter one or more case identifiers by typing, pasting, or uploading a CSV file. The system matches against the database, identifies matched and unmatched identifiers in a summary pop-up, and filters the dashboard to the matched set. The Query Bar reflects the active Local Find state.

| Ticket | Type | Summary | Assignee |
|---|---|---|---|
| BENTO-1345 | User Story | End user can find a case by entering a single identifier | David |
| BENTO-1351 | User Story | End user can enter a list to find a set of cases | Sohil |
| BENTO-1368 | User Story | End user can upload a file to find a set of cases | Sohil |
| BENTO-1381 | User Story | End user can identify matched and unmatched identifiers from the popup window | Sohil |
| BENTO-1382 | User Story | End user can click a Submit button from the pop-up window of Local Find | David |
| BENTO-1390 | User Story | End user can view a static query built from Local Find and faceted filter inputs | Chaparala |
| BENTO-1447 | User Story | End user can view/modify previously loaded Case Set | David |
| BENTO-1544 | User Story | Faceted search behaviors for Local Find | David |
| BENTO-1389 | Task | BE – Create API queries for Local Find | Chaparala |
| BENTO-1438 | Task | BE – Create new ES powered findIdsFromLists query for local find | Chaparala |
| BENTO-1383 | Task | FE – Styling for Local Find faceted filter area | Chaparala |
| BENTO-1384 | Task | FE – Styling for Local Find – Pop-up Window | Chaparala |
| BENTO-1346 | Task | Design: Update design for Local Find capabilities across case, sample, and file | Chen (Kai-Ling) |
| BENTO-1358 | Task | Design Improvement: Local Find upload Case Set pop-up window | Kuffel |
| BENTO-1321 | Task | Design: Clarify "Find" box with instructions | Kuffel |

### Feature: Query Bar

The Query Bar is the persistent strip above the Explore Dashboard table that shows currently active filter selections as removable chips. 3.6 delivered both the static version (read-only display of active filters) and the dynamic version (in-line chip removal).

| Ticket | Type | Summary | Assignee |
|---|---|---|---|
| BENTO-1362 | User Story | Static Query Bar – Query built from Faceted filters and Case IDs | David |
| BENTO-1446 | User Story | Dynamic Query Bar – Remove the filters | David |
| BENTO-1416 | Task | Design: Adjustments for Dashboard page | Kuffel |
| BENTO-1417 | Task | Design: Facet Sidebar, Age slider design adjustment | Kuffel |

### Feature: JBrowse (Genome Visualization)

JBrowse is an embedded genome browser component that allows end users to stream and visualize BAM-format sequencing alignment files directly in the Bento UI. It is configurable by the custodian and surfaces under a user's cart or case detail page.

| Ticket | Type | Summary | Assignee |
|---|---|---|---|
| BENTO-1030 | User Story | End user can visualize BAM files via JBrowse | Sohil |
| BENTO-1031 | User Story | Custodian configures the Bento JBrowse component | Sohil |
| BENTO-1397 | User Story | End user can load human genome hg19 | Sohil |

### Feature: Advanced Facet Filters (Number Range / Age Slider)

This work delivered a new facet filter type for numeric ranges (initially the Age slider in the TAILORx reference implementation). Users can set min/max bounds on a range slider to filter the dashboard by age or other numeric fields.

| Ticket | Type | Summary | Assignee |
|---|---|---|---|
| BENTO-1289 | User Story | Advanced Facet Filters for Number Range | Sohil |
| BENTO-1344 | Task | FE – Styling for Advanced Facet Filters | Stogsdill |
| BENTO-1290 | Task | Design: Number Range Facet Filter | Stogsdill |
| BENTO-1343 | Task | BE – Create/update GraphQL queries to support Advanced facet filters | Wang |

### Performance: Explore Dashboard

A dedicated performance sprint targeted four high-latency areas of the dashboard that were causing unacceptable load times on the reference implementation.

| Ticket | Type | Summary | Assignee |
|---|---|---|---|
| BENTO-1329 | User Story | FE – Dashboard Table Load Performance Improvement | Sohil |
| BENTO-1355 | User Story | FE – Dashboard Stats Bar/Donut Widgets Performance Improvement | Sohil |
| BENTO-1356 | User Story | FE – Dashboard Table Sorting/Pagination Performance Improvement | Sohil |
| BENTO-1357 | User Story | FE – Dashboard Add Files to Cart Performance Improvement | Sohil |
| BENTO-1341 | User Story | FE – Table Refactoring | Sohil |
| BENTO-1330 | Task | BE – Refine dashboard queries to avoid sending large lists of IDs | Doddapaneni |
| BENTO-1386 | Task | Testing: Validate Performance Improvement of Bento Dashboard | Lolla |

### Infrastructure & DevOps

| Ticket | Type | Summary | Assignee |
|---|---|---|---|
| BENTO-1359 | Task | Develop a CI/CD pipeline for Bento using GitHub Actions | Chen (Kai-Ling) |
| BENTO-1360 | Task | Develop a CI/CD pipeline for Bento using GitLab | Fleming |
| BENTO-1370 | Task | Update bento-local to include ES tech stack | Sohil |
| BENTO-1414 | Task | Update ES-loader Jenkins job | Ying |
| BENTO-1603 | Task | Bento 3.6.0 Perf env update | Ying |
| BENTO-1604 | Task | Bento 3.6.0 Production Env Update | Lolla |
| BENTO-1325 | Task | Display Files Microservices Version in the Footer | Sohil |

### Mock Data Generator

A new backend tooling capability that generates synthetic Bento-compatible data for use in testing and development environments. Outputs CSV/TSV-formatted data matching the Bento data model, can run in Docker containers, and reads ID field configurations from a config file.

| Ticket | Type | Summary | Assignee |
|---|---|---|---|
| BENTO-1387 | Task | Initialize mock-data-generator codebase | Ying |
| BENTO-1388 | Task | BE – Change mock-data-generator's output file format | Ying |
| BENTO-1409 | Task | Mock Data Generator can read ID fields from configuration file | Lolla |
| BENTO-1410 | Task | Mock Data Generator can run in Docker containers | Lolla |
| BENTO-1477 | Task | Mock Data Generator can generate data for Bento | Ying |

### Testing & Quality

| Ticket | Type | Summary | Assignee |
|---|---|---|---|
| BENTO-1310 | Task | Write and commit JEST test for existing JS function – Sri Kiran | Doddapaneni |
| BENTO-1311 | Task | Write and commit JEST test for existing JS function – Ajay | Doddapaneni |
| BENTO-1316 | Task | Review JS Testing Tools – Ajay | Doddapaneni |
| BENTO-1330 | Task | BE – Refine dashboard queries to avoid sending large lists of IDs | Doddapaneni |
| BENTO-1331 | Task | Write and commit one JUnit test for existing Java function – Austin | Ying |
| BENTO-1332 | Task | Write and commit JUnit test for existing Java function – Ming | Ying |
| BENTO-1348 | Task | Test Automate: Adding a Single Case/File to File Cart | Sohil |

### Compliance

| Ticket | Type | Summary | Assignee |
|---|---|---|---|
| BENTO-1420 | User Story | System is compliant with IDEA | David |

---

## Section 2: Bugs Fixed

63 bugs were resolved and closed during the 3.6.0 cycle. The volume reflects the complexity of three new stateful features landing simultaneously (Global Search, Local Find, Query Bar). Bugs tagged `Hot_Fix` were patched on an expedited out-of-band basis due to severity.

### Critical / Blocker

| Ticket | Description | Priority | Hot Fix |
|---|---|---|---|
| BENTO-1369 | Bento-local cases tab does not fully load | Blocker | |
| BENTO-1257 | JBrowse is not able to fetch the data for Alignments | Critical | |
| BENTO-1361 | Local Issuer Certificate Error occurs when installing bento-local | Critical | |
| BENTO-1445 | About page not displaying properly (no links) when navigated via global search results | Critical | |
| BENTO-1457 | Unable to navigate to bento-local (frontend container keeps restarting) | Critical | |
| BENTO-1496 | Facet filters/checkboxes appear twice when user collapses the filter or navigates away | Critical | |
| BENTO-1505 | Global search page should not load without user interaction with magnifying glass or Enter | Critical | |
| BENTO-1565 | Irrelevant/unfiltered cases displayed in dashboard table when user applies sorting | Critical | Hot Fix |
| BENTO-1570 | Static Query Bar: Case ID filter should display first on the query bar followed by facet filters | Critical | Hot Fix |
| BENTO-1588 | JBrowse is not able to fetch data for My Alignments and My Variants | Critical | |

### Major

| Ticket | Description | Priority | Hot Fix |
|---|---|---|---|
| BENTO-1276 | Leading and trailing spaces not returning results in search | Major | |
| BENTO-1285 | File-Centric Cart: UUID and MD5Sum columns hidden by auto system refresh | Major | |
| BENTO-1286 | Very slow response when user searches for a specific case, sample, or file on dashboard | Major | |
| BENTO-1380 | Find result does not update the dashboard table | Major | |
| BENTO-1423 | Clear query filter area/button appears twice | Major | |
| BENTO-1440 | Cases page crashes when user clears/removes all values from Max age value field | Major | |
| BENTO-1441 | Pop-up window should not maintain state when user clicks Cancel | Major | |
| BENTO-1442 | Case Set pop-up window recognizes Enter Key (new line) as an UNMATCHED case ID | Major | |
| BENTO-1443 | Multiple valid identifiers separated by comma recognized as 1 identifier if on 1 line | Major | |
| BENTO-1481 | Local Find: Blank page when user submits a case ID in lower case | Major | |
| BENTO-1482 | Local Find: Added case IDs are removed when user clicks Search text box 'x' mark | Major | |
| BENTO-1485 | Local Find: Unmatched cases not identified in the summary table on CSV upload | Major | |
| BENTO-1489 | Local Find: Blank page when user selects an unlisted case ID from the search box | Major | |
| BENTO-1494 | Local Find: Single case ID not removed when user clicks 'x' mark beside it | Major | |
| BENTO-1510 | Local Find: Dashboard table not updating properly after selecting case ID from local search textbox | Major | |
| BENTO-1520 | Upload Case Set popup should not retain history of previous entry after closing | Major | |
| BENTO-1521 | Upload Case Set popup should not lose history of a submission until user closes the input set | Major | |
| BENTO-1522 | Upload Case Set popup should not lose history of file name until user closes the input set | Major | |
| BENTO-1524 | Local Find: Programs and Arms donut label should be removed if user has any unmatched criteria | Major | |
| BENTO-1525 | File cart page keeps loading when user clicks header with no matching record found | Major | Hot Fix |
| BENTO-1544 | Uploading a set: identifiers that should match in database are not matching | Major | |
| BENTO-1550 | Global Search: Data model category giving wrong count in result page | Major | Hot Fix |
| BENTO-1563 | Download manifest: User unable to download CSV files | Major | |
| BENTO-1566 | Global Search: All filter count displaying with previous data results | Major | Hot Fix |
| BENTO-1586 | File cart: Irrelevant cases/files added to cart when user clicks Add All Files | Major | |
| BENTO-1600 | '404 PAGE NOT FOUND' error when clicking Program Code (TAILORx) link in Samples/Files tab | Major | Hot Fix |
| BENTO-1601 | Case Detail page: Issues with file cart notification text when adding files to cart | Major | Hot Fix |
| BENTO-1606 | Local Find: X mark deletes other case ID/case set selections | Major | Hot Fix |
| BENTO-1610 | Clear All filtered selections icon is not clearing all Query Bar selections | Major | |
| BENTO-1611 | Query Bar: TAILORx program displaying twice when navigated via Program detail page | Major | Hot Fix |
| BENTO-1612 | Global Search – File Category: Sample ID value should display as hyperlink | Major | Hot Fix |
| BENTO-1469 | File-Cart table: User cannot apply sorting in descending order | Major | |
| BENTO-1470 | Global search icon is not clickable (on search page and home page) | Major | |
| BENTO-1479 | Global search result page should not default to Cases category | Major | |
| BENTO-1584 | After adding files to cart, navigating back to dashboard does not refresh | Major | Hot Fix |

### Minor

| Ticket | Description | Priority | Hot Fix |
|---|---|---|---|
| BENTO-1203 | Bento Custodian: Updating main clear icon also updates individual filter clear icons | Minor | |
| BENTO-1471 | Assay label and count missing from home page | Minor | |
| BENTO-1480 | Global Search: Incomplete count page – pagination missing focus | Minor | |
| BENTO-1483 | Horizontal lines separating all filters have been removed | Minor | |
| BENTO-1495 | Global Search: Search keyword result not removed when user removes the search keyword | Minor | |
| BENTO-1506 | Cursor should change to hand icon when hovering over magnifying glass in Global Search | Minor | |
| BENTO-1585 | DATA MODEL: Property Description and Type values overlapping/exceeding visible screen | Minor | Hot Fix |

### Other Closed (Duplicate / Won't Fix / Cannot Reproduce)

| Ticket | Description | Resolution |
|---|---|---|
| BENTO-1478 | Previous search result displayed in current search result page | Won't Fix |
| BENTO-1488 | Multiple unmatched case IDs identified as first unmatched case ID alone in summary | Won't Fix |
| BENTO-1491 | No data returned when user searches a program by name | Duplicate |
| BENTO-1498 | Uploading the same file a second time does not upload to the popup window | Fixed |
| BENTO-1499 | Case IDs popup window should not be case sensitive | Verified |
| BENTO-1551 | Global Search: All filter not giving correct count result for Program search | Fixed | 
| BENTO-1552 | Global Search – Files Category: Case ID label should display instead of Subject ID | Fixed |
| BENTO-1567 | Global Search: All filter category displaying data results when all categories have 0 count | Fixed | Hot Fix |
| BENTO-1582 | Global Search: All filter displaying previous results when user searches same keyword a 2nd time | Fixed | Hot Fix |
| BENTO-1589 | 'Property_Required' attribute under DATA MODEL returning non-boolean values | Fixed |
| BENTO-1608 | Local Find: Clear Query button not clearing all selections | Fixed |

---

## Section 3: Open QA Tests (Pending Closure)

4 formal QA test tickets remain open against the 3.6.0 version. These are test execution scripts, not defects.

> **Action Required:** These were carried into the 4.0.0 cycle without resolution. Assign a testing sprint to close them. BENTO-1583 (IDEA compliance) is a regulatory test that should be prioritized.

| Ticket | Test Description | Assignee |
|---|---|---|
| BENTO-1372 | FE – Regression Testing for Dashboard Table Sorting/Pagination Performance Improvement | Sohil |
| BENTO-1406 | Validate that end-user can see auto-complete on global search | Sohil |
| BENTO-1583 | Test: System is compliant with IDEA | David |
| BENTO-1594 | Test: Faceted search behaviors for Local Find | David |

---

## Section 4: Team Contributions

| Team Member | Role | Primary Focus Area |
|---|---|---|
| Sohil, Zalmay | Frontend Engineer | Local Find (end-to-end), Global Search reimplementation, JBrowse, dashboard performance, bento-local |
| David, Sofia | Frontend Engineer | Local Find state management, Query Bar, Case Set upload flow, Global Search results, hot fixes |
| Doddapaneni, Sai Ajay | Backend Engineer | Global Search API, ES query development, result ordering, JS testing |
| Chaparala, Sri Kiran | Backend Engineer | Local Find backend API, ES findIdsFromLists query, FE styling |
| Wang, Fuyuan | Backend Engineer | Advanced facet filter GraphQL queries, Global Search styling |
| Ying, Ming | Backend Engineer | Mock Data Generator, ES-loader Jenkins, performance env updates |
| Lolla, Laxmi | QA / DevOps | Performance testing, Mock Data Generator tooling, production env update |
| Stogsdill, Hannah | UX Designer | Global Search and filter styling reviews |
| Chen, Kai-Ling | Technical Lead | Local Find design, CI/CD pipeline planning (GitHub Actions), code refactoring |
| Fleming, Michael | DevOps Engineer | Elasticsearch backend documentation, CI/CD pipeline (GitLab), bento-local |
| Kuffel, Gina | Technical PM | UX design: Global Search results page, Local Find pop-up window, Dashboard/Sidebar design adjustments, Find box clarification |

---

## Section 5: Items Cancelled / Deferred in Bento 3.6.0

The following items were scoped into 3.6.0 but closed as Cancelled, Won't Fix, or Duplicate. Most reflect design pivots or work that was consolidated into a different ticket.

- **BENTO-1245** — FE – FEATURE: Global Search (original feature ticket) — closed as Duplicate; the work was decomposed into the individual story and task tickets that shipped.
- **BENTO-1390** — End user can view a static query built from Local Find and faceted filter inputs — closed as Duplicate; superseded by BENTO-1362 (Static Query Bar) which covered the same behavior.
- **BENTO-1395** — Bento Code Refactoring – Behavior Component — closed as Won't Fix; deferred to the 4.0.0 Bento-Core refactor cycle.
- **BENTO-1418** — FE: Age Slider improvement — closed as Won't Fix; superseded by the Number Range filter work (BENTO-1289).
- **BENTO-1427** — Design Review: Age Slider improvement — closed as Duplicate for same reason.
- **BENTO-1429** — End user sees consistent information across Global Search categories — closed as Won't Fix; behavior was addressed in individual per-category bug fixes instead.
- **BENTO-1383, 1384** — FE Styling for Local Find faceted filter area and pop-up window — closed as Duplicate; styling was folded into the main Local Find stories.
- **BENTO-1255, 1256, 1336, 1339** — Multiple FE Global Search styling tasks — closed as Duplicate; consolidated into the final styling review tasks.

---

*Generated from Jira (fixVersion = "Bento 3.6.0") — NCI / CBIIT FNL Bento Team — bento-help@nih.gov*
