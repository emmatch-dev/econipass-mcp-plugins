# Native CFP workbooks

The two tools support these five `file_type` values. Preserve the native template rather than creating a generic table with matching-looking columns.

| Type | Contents and order | Download `year_month` | Upload replacement scope |
| --- | --- | --- | --- |
| `master` | Product, parts/material/logistics/disposal, equipment, and linked masters; normally first | Omit | Organization and all months specified by the linked master header and creation period |
| `base_unit` | Product emission-intensity master after its referenced masters exist | Required, `YYYY-MM` | Organization and all months specified by the workbook and creation period |
| `activity_amount` | Activity actuals after the referenced masters and intensities exist | Required, `YYYY-MM` | Organization and workbook month, including derived energy data |
| `pcf_certification_period` | CFP certification/verification periods | Omit | Organization and workbook header month, not an independently inferred period from each certification row |
| `aist_idea` | AIST-IDEA factors for the selected organization | Omit | The organization's current AIST-IDEA dataset; no target month |

The usual sequence is master → base unit → activity amount. Existing data may already satisfy prerequisites; do not require unnecessary reimports. Base-unit and activity uploads also run native CFP data processing. Handle certification and AIST-IDEA only when requested.

## Target and time fields

`organization_id` must match the workbook's native customer-ID header. The MCP preview reads the authoritative headers and includes hidden target sheets. For master files, the linked master sheet controls organization, first month, and period for all master sheets. Do not reinterpret another displayed customer-ID cell as an independent import target.

- Download `year_month`: `YYYY-MM`, required only for `base_unit` and `activity_amount`.
- Download `time_zone_offset`: hours from UTC, default `9.0` for Japan, range -14 through 14; India is `5.5`. Do not pass JavaScript's minute offset.
- Upload `expected_year_month`: optional `YYYY-MM` check of the workbook's first month; omit for `aist_idea`. A preview shows the full month list, not just this expectation.
- Workbook month headers: native `YYYYMM` literal value. Creation periods in master/base-unit files are literal integer month counts, bounded to 1–120 by the MCP inspector. Do not replace these with Excel date cells or formulas.

## Content and file handling

Upload one XLSX at a time, at most 10 MiB after Base64 decoding. Supply a filename, not a path; CSV, XLS, macro-enabled workbooks, and a batch of files are not supported by these tools. Downloads are bounded to 32 MiB. Availability depends on the organization language and the requested native template; in an environment without the selected language template, report the returned rejection and do not substitute another language or claim a workbook was created. An exported resource is not a public link and may require host-specific attachment support.

Keep formulas, cached values, validation, native sheets, and existing rows when editing. The preflight uses cached formula values just as the native reader does, but rejects formulas in target headers. It never evaluates formulas or resolves external links. Existing external-link caches in official English templates alone are not an import rejection. Recalculate changed business formulas using an available trusted workbook editor if their cached values must change; do not report that the MCP preflight recalculated them.

Candidate counts and replacement targets describe what the importer could consider. They do not validate referential integrity, units, master consistency, permissions, closed periods, or every business rule. Native validation is authoritative at execution; zero valid candidates can fail there. Failed native imports can still leave uploaded-file/history records, so failure is not proof that no operational record was created.

## Readback

`list_upload_history` helps find the receipt and outcome. Depending on the input, use exposed `get_masterdata`, `get_summary_dashboard`, `get_product_emissions`, or `get_facility_emissions` to inspect affected data. Use their actual schemas and returned status/coverage; do not infer a successful replacement from a missing row or a calculation result alone. Do not automatically repeat an upload after an unknown result, even with the same bytes or a new confirmation token.
