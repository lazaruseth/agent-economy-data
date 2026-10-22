# The Agent Economy: open dataset

This repository holds the data behind [The Agent Economy](https://theagenteconomy.si), a neutral directory of agent economy infrastructure: payment rails, protocols, identity, governance, frameworks, and exchanges.

Each record describes a mechanism, its status, and the public sources that were checked. A figure or capability without a public source stays `UNKNOWN`. Nothing here is a ranking.

The site code is not in this repository. Only the data is published.

## Source and update cadence

- Canonical source: https://theagenteconomy.si
- Live export: https://theagenteconomy.si/data/listings.json
- The site is checked on a regular schedule. This repository is not updated automatically. A maintainer syncs it by hand from the live export with a script, after published updates, so it can trail the site.
- Every record carries its own `last_verified` or `checked` date. Use those dates, not the commit date, to judge freshness.

## Files

| File | Contents |
| :- | :- |
| `data/listings.json` | Every listing, alphabetical inside each category. Same as the live export. |
| `data/adoption.json` | Claimed and measured adoption figures per listing, each with its source. |
| `data/spend-controls.json` | Spend control matrix for agent wallets and payment products. |
| `data/comparisons.json` | Same category listing pairs that have a comparison page on the site. |
| `data/glossary.json` | Sourced definitions for agent economy terms, linked to listings. |
| `data/protocol-compatibility.json` | Protocol compatibility matrix, 28 rows. Every cell carries its own sources and verified date. Same as the live export at https://theagenteconomy.si/data/protocol-compatibility.json. |
| `data/gaps.json` | Documentation gaps, 22 notes across 7 dimensions. Each cell is Documented, Not documented, Mixed, or Omitted, with its source and the day it was read. Same as the live export at https://theagenteconomy.si/data/gaps.json. |

## Fields

### `data/listings.json`

Top level: `name`, `description`, `license`, `license_url`, `attribution`, and `listings`.

Each item in `listings`:

| Field | Type | Meaning |
| :- | :- | :- |
| `name` | string | Product or protocol name. |
| `slug` | string | Stable identifier, used by every other file. |
| `category` | string | One of `exchanges`, `exchanges-with-agent-access`, `frameworks`, `governance`, `identity`, `payment-rails`, `protocols`. |
| `tags` | string[] | Mechanism tags such as `http-402`, `spend-limits`, `stablecoins`. |
| `summary` | string | What it does, stated as a mechanism. |
| `status` | string | `live`, `beta`, or `designed`. |
| `open_source` | boolean | Whether the core is published under an open license. |
| `repo_url` | string or null | Public source repository. |
| `website` | string | Official site. |
| `docs` | string | Primary documentation. |
| `last_verified` | date | Last day the record was checked against its sources. |
| `sources` | object[] | `title` and `url` for each public source used. |

### `data/adoption.json`

| Field | Type | Meaning |
| :- | :- | :- |
| `slug` | string | Listing slug. |
| `claimed` | `"UNKNOWN"` or object[] | Figures the vendor states about itself. |
| `measured` | `"UNKNOWN"` or object[] | Figures from an independent source, such as an onchain dashboard or package registry. |
| `notes` | object[] | Scope caveats and context, for example a figure that covers a whole network rather than this product. Each note has `text`, `source_url`, `source_title`, and `date`. |
| `checked` | date | Last day the sources were checked. |

Each figure object has `metric`, `value`, `as_of`, `source_url`, `source_title`, `checked`, and, for measured figures, `measured_by`. On the site, `UNKNOWN` is shown as "None published".

### `data/spend-controls.json`

Top level: `title`, `updated`, and `rows`. Each row has `product` and `listing_slug`, then one cell per control: `per_payment_cap`, `period_budget`, `allowlist`, `approval_threshold`, `revoke`, `custody`, and `rails`.

Each cell has `value` (`Yes`, `No`, `Partial`, `UNKNOWN`, or a short description; `rails` uses a `values` list instead), plus `source_url`, `source_title`, `checked`, and `note`. A cell with no public source is `UNKNOWN` with a null `source_url`.

### `data/comparisons.json`

A list of `{ "a": slug, "b": slug }` pairs. Each pair has a page at `https://theagenteconomy.si/compare/<a>-vs-<b>`.

### `data/glossary.json`

Each term has `slug`, `term`, `definition`, `source` (`title`, `url`), `more_sources` (extra `title`, `url` pairs, when present), `listings` (related listing slugs), `related` (related term slugs), and `last_verified`.

## Corrections

Open an issue or a pull request. Every correction needs a public source URL that states the fact, plus the date you checked it. Vendor statements are recorded as claimed figures, and independent measurements as measured figures. A correction without a source is not merged, and a cell without a source stays `UNKNOWN`.

Accepted corrections are applied to the site first, then synced back here at the next manual sync.

## Neutrality and disclosure

Run by Max Curnin, Executive Chairman of Accords. Accords is listed under the same criteria as every other entry and is never ranked or styled differently.

Sponsor placements are not part of this dataset, do not change listing order, and never appear in these files.

## License

Data is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). See `LICENSE`.

Attribution: The Agent Economy (https://theagenteconomy.si), licensed under CC BY 4.0.
