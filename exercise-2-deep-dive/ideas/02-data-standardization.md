# Idea 2: Multi-Platform Data Collection & MDI Standardization

## What They Said

> Data collection by vendor, by platform and sort it to the MDI standards and templates in order to generate detailed and simplified dashboards and gain in efficiency. From planning to investment to data-MDI teams.
>
> The process today is to collect data from every platform and to manually enter it in the MDI templates: it may have some errors because of many manipulations, and some vendors doesn't have the same naming convention for some ad-products, formats, impressions, KPI, costs vs fees, etc.
>
> AI could create algorithms or ways to simply data in a very short delay and always in a concise and standardized way.

## Current Pain

- Data comes from multiple platforms with different naming conventions
- Manual entry into MDI templates introduces errors
- "Impressions" means different things across vendors
- Costs vs. fees categorized differently per platform
- Touches planning, investment, AND data-MDI teams — lots of handoffs

## Agent-Native Reframe

**AI synthesizes:** Raw platform exports + MDI template schema + a "rosetta stone" mapping file (vendor term → MDI standard term) → clean, standardized data ready for the template. Flags ambiguous mappings for human review.

**Human judges:** New/unknown naming conventions, whether a vendor's "engagement" metric maps to MDI's definition or needs a different treatment. Validates the mapping table evolves correctly.

**System improvement loop:** Every time a human corrects a mapping, it gets added to the rosetta stone. Over time, the system handles 95% automatically and only surfaces true edge cases.

**v1 this week:** Take one vendor's raw export + the MDI template. Build the mapping manually as a reference file. Prompt: "Transform this raw data to match this template using this mapping. Flag anything you can't map with confidence."
