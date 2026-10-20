# Record identity and replacement rules

Use tool schemas and master data for actual fields. Public month arguments generally use `YYYY-MM`; Scope 3 `input_contents.target_year_month` uses `YYYYMM`. Fiscal-year arguments use `FY2025` for April 2025–March 2026. Preserve identifiers as returned, including leading zeros.

## Energy usage

Read `list_energy_usage` for the relevant organization and months, with `include_subsidiaries=false` when editing only that office. A list with `truncated=true` or errors is insufficient evidence that an omitted row does not exist; narrow the query or use the application if the complete target cannot be read.

`upsert_energy_usage` matches `(organization_id, target_year_month, energy_code, target_day)`. Omit `target_day` only for monthly figures. A daily entry does not replace a monthly total; adding both without an explicit accounting intent can double count. Duplicate targets within one call are rejected. The backend requires unit, payment unit, currency, and contract fields to agree across rows of the same month and energy code. Preserve these fields and inspect the preview before changing them.

`delete_energy_usage` must resolve exactly one current record. When daily entries exist, specify the day; do not select the first candidate from an ambiguous result. The acknowledgment is `organization_id/year_month/energy_code`, appending `/target_day` when supplied. Use the exact format indicated by the preview. MCP cannot restore the deleted value.

## Scope 3

Use the category detail code from `get_masterdata(kind="scope3")`, not the display category number. Inspect `list_scope3_inputs` for every affected month before a final replacement. Each submitted row requires organization, compact month, and `no`, plus category-specific fields. All rows in one call share an organization; `no` must be unique in the request.

For `upsert_scope3_input`, every omitted existing row in each submitted category/organization/month is deleted. The backend reassigns `no` from 1; it is not a persistent row ID. A one-row correction therefore needs the complete retained set for that month. Show replacement counts and removed rows in the preview. Do not commit when the existing set cannot be established.

`save_scope3_input_draft` instead upserts by organization/month/`no` and preserves omitted draft rows. Clearly label its outcome as temporary; saving a draft does not confirm reported figures or perform the final replacement.

## Self-generated and secondary energy

Read `list_self_and_secondary_amount` and `get_masterdata(kind="self_and_secondary")`. Supported activity types are `self_amount`, `energy_saving_amount`, and `secondary_activity_amount`. The preview can include implicit deletes within a related energy family. Review those deletions as part of the requested change, not just the directly submitted row.

## Status and recovery

An input status of `excluded` is settled but is not a numerical zero. No input targets, failed reads, or unfamiliar response shapes may remain unknown. Closed-year status is an observation; none of these tools closes or reopens the year.

On a known conditional-write conflict, obtain current state and preview again. On an unknown commit outcome, first compare stored records with the intended values; a missing acknowledgment is not evidence that the backend failed. Do not infer persistence merely from an `applied` label if the nested result reports a pending or failed process.
