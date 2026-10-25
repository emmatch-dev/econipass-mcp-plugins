# EMS workflow details

Read the section relevant to the user's task. Current exposed tool schemas determine fields, limits, and availability.

## File imports and recovery

For readings, start with `download_ems_import_template`; use the schema's `profile` and `dataset` for electricity, FEMS/BEMS, or temperature input. `list_ems_jma_temperature_stations` resolves JMA station IDs for the `JMA_OBSDL` profile. File arguments are `file_name` and Base64 `content_base64`, not local paths or URLs.

The native import flow has two writes, each using the skill's confirmation flow:

1. Preview then execute `validate_ems_import`. Execution creates a saved validation receipt; `dry_run=true` alone does not run the native validator or produce an import receipt.
2. Inspect the returned `import_id`, file digest, rows, and errors. Use `get_ems_import`, `list_ems_import_errors`, and `list_ems_import_data_rows` when needed. Keep accepted, held, rejected, and existing rows distinct.
3. Preview then execute `commit_ems_import` using that receipt's `import_id` and `body.file_sha256`. Approval for validation alone does not imply approval to commit readings. Preserve any existing authorization that explicitly covers the exact commit.
4. Read `get_ems_import` until the returned state answers the user's request. If the user wants monitoring later, use the host's supported scheduling workflow only when requested. Resuming a UI session means reading its existing receipt, not creating or committing it again.

Related file families use their own schemas and receipts:

| Family | Prepare/read | Validate write | Commit write |
| --- | --- | --- | --- |
| Point/device mappings | `download_ems_point_device_mapping_template`, `export_ems_point_device_mappings` | `validate_ems_point_device_mappings` | `commit_ems_point_device_mappings` |
| Electrical topology | `download_ems_electrical_topology_template`, `export_ems_electrical_topology` | `validate_ems_electrical_topology` | `commit_ems_electrical_topology` |
| Analysis factors | `download_ems_analysis_factor_template`, `export_ems_analysis_factors` | `validate_ems_analysis_factors` | `commit_ems_analysis_factors` |
| Asset data | `export_ems_asset_data` | `validate_ems_asset_data` | `commit_ems_asset_data` |

Readings and asset data accept CSV/XLSX; mappings, topology, and analysis factors accept XLSX only. Decoded upload limits are 10 MiB generally and 5 MiB for asset data; use any lower limit in the actual schema. Downloads are bounded to 32 MiB. Do not describe a partial or rejected download as a complete file.

`list_ems_import_transactions` reads CSV import transaction history across matching imports; preserve its native filters and pagination rather than confusing transactions with accepted input rows. `list_ems_imports` can filter by creation interval, filename, import ID, site, and status. Its end must be after its start. `list_ems_import_data_rows` can filter saved storage status, source row number, and measurement point code. `list_ems_processing_jobs` takes either `status` or `statuses`, not both. Pass multi-status values as a JSON array to the tool.

## Master and reading maintenance

Read the matching site/asset/point/device/stream/source list before creating, retiring, closing, replacing, or changing a mapping. Preserve effective dates and timezone semantics; a change to current master data is not automatically a repair of historical readings.

`update_ems_site_validity` can move a site's `valid_from_at` earlier only, with an explicit reason. It cannot move the effective start later or repair historical readings by itself. Inspect the existing site and affected interval before preview/execution.

Use `list_ems_unresolved_identities` and existing mapping data before `reconcile_ems_unresolved_identity`. Use `list_ems_reading_history` before `correct_ems_reading`, `void_ems_reading`, or `start_ems_counter_segment`. Read `get_ems_processing_job` before a requested `requeue_ems_processing_job`; an unknown prior result is not permission to requeue. `get_ems_dashboard_health` and `list_ems_quality_issues` support diagnosis; `resolve_ems_quality_issue` changes issue state and requires confirmation. Do not resolve an issue merely to hide a warning.

## Durable intake and effective master plans

Use `list_ems_intake_jobs`, `get_ems_intake_job`, and `get_ems_intake_unassigned_analysis` to resume an existing intake session. `upload_ems_intake_job` creates the durable job; its native form fields, including the required stable `idempotency_key`, belong in `parameters`. The key is not an invented HTTP header. Preserve the original file bytes, resulting job ID, validation details and file digest. `commit_ems_intake_job` is a separate write with its own preview and authorization; a completed upload is not a committed reading.

`act_ems_intake_on_job` allows only its exposed `retry` or `cancel` action. Inspect the existing state first, especially after an unknown result. For unassigned data, inspect `list_ems_intake_assignment_candidates` before `reconcile_ems_intake_many` or `register_ems_unresolved_identity_point`. Confirm the intended identity, device/point, effective period and history effects; never infer a measurement unit from a label.

Read `list_ems_intake_connections` before creating/updating a connection, using the native provider identifiers and allowed configuration fields. `sync_ems_intake_connection` initiates processing and may contact the configured provider: verify the requested interval, connection and existing job before preview/execute. Do not ask for or put provider secrets into ordinary tool arguments.

For topology changes, inspect `list_ems_intake_plans`. `preview_ems_intake_plan` requires the write confirmation flow and the native administrator role: first use MCP `dry_run=true` to preview the request without sending it, then execute the confirmed request to run the native transaction/savepoint validation. The native preview rolls its temporary changes back; it does not save or apply a plan. Inspect its conflicts and effective dates before a separately authorized `create_ems_intake_plan`. Apply, postpone, or cancel the saved plan only for the requested transition, preserving expected versions and explicit reasons.

## Tariffs, goals and estimates

Read `get_ems_management_overview` for the exact site, measurement point and `year_month`. `estimate_ems_management_cost` computes from the saved active tariff and goal for that scope; it does not accept an unsaved proposal. Distinguish observed usage, estimated cost and saved revisions; unavailable coverage is not a zero cost.

`save_ems_management_tariff` and `save_ems_management_goal` are independent writes. Preserve native revision/version checks, period, currency, units, rates and limits from the user's input. A successful estimate does not authorize saving a revision or overwriting another user's update.

## Demand alerts and delivery

Use `list_ems_demand_alert_rules`, `get_ems_demand_alert_rule`, and `list_ems_demand_alert_events` to identify the requested rule or event. `acknowledge_ems_demand_alert_event` changes acknowledgement state; it does not prove the demand problem is fixed. Rule create/update/disable operations also require the existing confirmation flow.

For a requested delivery change, read `get_ems_demand_delivery_settings` and preserve `expected_revision` for `update_ems_demand_delivery_settings`. Use allowed user IDs and a configured `webhook_destination_id`; do not invent recipient IDs, request secrets, or substitute an arbitrary URL. Read `list_ems_demand_delivery_history` to distinguish configuration from actual delivery. The skill does not authorize an unsolicited message or notification test.

## Supervision and linked action tasks

Resolve available targets with `get_ems_supervision_options` and `get_ems_supervision_action_options`; inspect the applicable rules, events, deliveries or actions list. Preserve organization/site filters and pagination. Provisional, arrival-based and test events are different evidence; acknowledging one does not repair the underlying issue.

Use create/update rule operations only for the requested rule and revision. `test_ems_supervision_notification` and `retry_ems_supervision_delivery` can send real notifications. Before preview/execute, require user authorization covering that dispatch and its configured recipients; inspect delivery state and `get_ems_supervision_delivery_audit` to avoid repeating an already delivered or unknown attempt. A retry request is not proof of delivery.

For action work, read `list_ems_supervision_actions` and `list_ems_supervision_action_activities` before linking/updating a task or adding activity. Preserve the existing task link, status, revision and user's actual account of work. Do not mark work complete or manufacture an activity merely because an event was acknowledged.

## Shared analyses, reports, schedules and annotations

Use `list_ems_workspace_analyses` and `resolve_ems_workspace_analysis` to recover a saved query. Resolve its current selectors and access before interpreting results. Create/update/delete operations preserve `expected_version`; deletion is a concrete change to a saved object, not a temporary filter reset.

`get_ems_workspace_provenance` reads underlying evidence. `create_ems_workspace_report` saves a report snapshot and is a write; afterward use `get_ems_workspace_report` and `export_ems_workspace_report` for the saved evidence. Exports support the exact exposed CSV/PDF format. `regenerate_ems_workspace_report` is a separate write requiring the saved report identifier and a reason; inspect the original snapshot and current report first. Regeneration is not a simple re-download and does not establish external acceptance. Preserve snapshot hashes and distinguish saved evidence from live recalculation, reviewer acceptance, external delivery and legal filing.

Inspect `list_ems_workspace_schedules` before creating, changing or deleting a schedule. Preview the recurrence/timezone, report selection, visibility and effective settings with the user; authorization for a one-time report does not authorize recurring report generation. This scheduler creates saved report snapshots and does not configure external delivery destinations. Schedule registration does not establish that a later run succeeded.

Read `list_ems_workspace_events` before creating or voiding an annotation; preserve event periods and the user's reason. For M&V report decisions, inspect `get_ems_workspace_mv_report_review`, `expected_sequence` and evidence hash before `decide_ems_workspace_mv_report`. Its `finalize`, `reject`, `void` and `supersede` actions represent distinct transitions. Obtain any explicit reviewer attestations required by the native schema and never infer them from a general instruction to prepare a report.

## Measurement and verification (M&V)

Resolve a plan with `list_ems_mv_plans` / `get_ems_mv_plan`, then inspect `list_ems_mv_revisions` / `get_ems_mv_revision`. Keep the chosen revision and expected plan SHA-256 attached to the user's operation. Creating plans or revisions and submitting, cancelling, approving, or rejecting them are distinct writes, not automatic stages to execute together.

`fit_ems_option_c_baseline`, `simulate_ems_option_c`, and `analyze_ems_option_c` are exposed as reads even though the native API uses POST. A calculation result is not an approved revision or verified savings claim. Use `create_ems_mv_adjustment`, `approve_ems_mv_adjustment`, or `reject_ems_mv_adjustment` only for the requested adjustment and state transition. Never fill `conflict_of_interest_confirmed` or another approval attestation from an inference; preserve the human reviewer's explicit statement and native role rules.

Provide `idempotency_key` only when the selected tool exposes it; required keys must remain stable for the same operation. Do not mint a new key to retry an unknown result. After an authorized `create_ems_mv_report`, use `list_ems_mv_reports` and `download_ems_mv_report_evidence` for readback and evidence. Evidence export does not itself approve a plan or deliver a report externally.
