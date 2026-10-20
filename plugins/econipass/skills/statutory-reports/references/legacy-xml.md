# Legacy organization/year reports

Legacy reads use `mcp:read`; XML generation and `save_xml_overrides` require the separate `mcp:reports` scope. A missing legacy report scope needs the client to request it and the user to reauthorize; changing a connection-list label does not add OAuth permission. Use only published tools and existing authorization.

## Data and completeness

Resolve organization and `FYyyyy`. Read `get_shoene_data`, `get_ondaiho_data`, or `get_fron_data` when source rows matter; the matching `get_*_report` tool returns normalized report data. The tool spelling is `fron` for reads and `freon` for generation and the `law` code; use actual schema enums rather than normalizing names yourself.

Use `validate_xml_report` to inspect missing input months, factors, and required data. It is a completeness check, not XML/XSD validation or proof of EEGS acceptance. Its `can_generate` does not make a document submittable. `check_shoene_obligation` compares reported energy with thresholds; present its result and legal-review limitation, not a definitive legal classification.

For unanswered fields use `list_xml_missing_fields`. Use `search_xml_fields` to locate a requested edit, then `get_fields_spec` only for the relevant form. Omitting the form first lists available forms; do not retrieve the entire large specification unnecessarily. Preserve exact field paths and units; ask for missing facts instead of inventing representative values.

## Private overrides

`get_xml_overrides` reads this user's saved organization/year/law values. `save_xml_overrides` fully replaces them, and `{}` clears them all. To change one field, read current values and prepare the complete retained mapping. Show additions, changes, and removals in the dry-run preview; commit the identical authorized mapping with its token. Concurrent changes require a new preview.

An `overrides` argument to a generation tool affects that generation only; it does not save preferences or update the shared editor. Private overrides do not constitute confirmed shared-report evidence.

## Generation and delivery

Choose the law's `generate_*_xml_jp` tool for Japanese placeholders; `_ko` uses Korean placeholders. These generation tools do not expose the dry-run/token interface, so do not invent those parameters. Generate only when it serves the user's requested report work.

For 省エネ法, `generate_shoene_xml_jp` and `generate_shoene_xml_ko` always produce a legacy preview: `submission_ready=false`, `draft=true`, and `preview_only=true`. Even complete data and an XSD pass do not make it submittable. For 温対法 and フロン法, read the returned readiness, partial status, required fields, validation, and warnings; never infer success from file existence or assert official acceptance.

Legacy generation returns a `report_id` and filename, not an attachment or public URL. Direct the signed-in user to **EcoNiPass → 各種設定 → MCP連携設定 → 生成した報告書**. Access is for the generating user, once, within a short window. Do not fabricate links or claim the file is attached. When a preview is incomplete, explain the blockers and gather the missing facts before regenerating.
