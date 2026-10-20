# Shared report and paper workflow

## Permissions and discovery

Shared report scopes are independent of legacy `mcp:reports` and ordinary `mcp:write`:

| Operation | Required scope |
| --- | --- |
| Report, missing-field, proposal, carryover, and paper-draft reads | `mcp:statutory-reports:read` |
| DB source-candidate reads | `mcp:statutory-reports:sources:read` |
| General XML proposal or carryover apply | `mcp:statutory-reports:propose` |
| Paper-only proposal | `mcp:statutory-reports:propose` and `mcp:statutory-reports:read` |
| Proposal from a DB candidate | `mcp:statutory-reports:propose`, `mcp:statutory-reports:read`, and `mcp:statutory-reports:sources:read` |
| Conditional accept/reject surface | `mcp:statutory-reports:review` |
| Package capability check | `mcp:statutory-reports:generate` |

Discover reports through `list_statutory_reports_v2` using an accessible organization and optional performance fiscal year. Continue `next_cursor` with identical filters and limit until no longer truncated. An error is not an empty collection. If the bounded collection cannot be read, use the EcoNiPass editor rather than guessing IDs.

Read `get_statutory_report_v2`, then `list_statutory_report_missing_fields_v2` and `list_statutory_report_proposals_v2` for the same revision. Keep the returned revision and exact canonical paths. Indexed paths identify particular occurrences; do not remove indices or invent them. A newer revision invalidates the earlier snapshot.

## Select one evidence path

- **General XML proposal:** `propose_statutory_report_updates_v2` accepts bounded changes with value and provenance. Use exact editable paths and the schema's permitted source kinds. Caller-supplied source references and evidence hashes remain self-asserted. They are not EcoNiPass DB attestations.
- **DB candidate:** read `list_statutory_report_source_candidates_v2`; preserve the candidate ID/key, fiscal year, organization, unit, covered/missing months, and evidence metadata. The human must select the intended field mapping. `propose_statutory_report_update_from_source_candidate_v2` takes that candidate and exact editable path; the server resolves value/evidence itself. Do not manufacture a replacement value/hash or assume a matching label proves statutory classification.
- **Prior-year carryover:** use `list_statutory_report_year_carryover_sources_v2`, then `preview_statutory_report_year_carryover_v2`. Review its assessment and exclusions. Pass the returned assessment SHA to `apply_statutory_report_year_carryover_v2`, first as a dry run. It rechecks the assessment and creates an unverified proposal; it never copies all prior-year values directly into confirmed fields.
- **Paper-only field:** read `get_statutory_paper_draft_v1` and its catalog definitions. Use both current report and paper revisions with `propose_statutory_paper_updates_v1`. String/null changes are paper proposals only. They do not update XML, commit paper values, or grant approval. Evidence remains self-asserted.

Preview and commit only the selected, authorized proposal. Re-read proposals afterward and report it as pending/unverified. A large proposal must be split along meaningful review boundaries within the exposed limits, not silently truncated.

## Review and package boundaries

Accept/reject tools may not be published. If available, read the current report and proposal, display the actual changes, and use the review tool's current report/proposal revisions and preview/token flow for the user's requested decision. Do not treat a previous instruction to draft a proposal as permission to accept it. Do not fabricate recent MFA or a browser approval grant; backend refusal remains a boundary.

For package generation, `generate_statutory_report_package_v2` reports backend blockers plus the unconnected MCP trusted-generation boundary. Even if backend capability says a browser can create a package, the MCP tool returns `available=false`, `generated=false`, and `submission_attempted=false`. Guide the user to the authenticated EcoNiPass browser workflow. Do not invoke the backend writer, post a client manifest, or claim an official submission.
