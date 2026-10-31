# Forever Planner — Racial Data

A public, versioned JSON snapshot of racial abilities and character-specific recommendations collected for the **Forever Planner** project.

This repository contains a data file and its source references. It is **not** a playable addon, official game dataset, or the complete private Forever Planner application.

## What's here

- [`racial-updates.json`](racial-updates.json): 49 racial-ability records, with PvE/PvP notes and optional class- or role-specific recommendations.
- [`README.md`](README.md): scope, format, limitations, and maintenance guidance.

The current JSON snapshot identifies itself as format `forever-planner-racials`, format version `1`, revision `2`, with an October 27, 2026 review date. The file includes an earlier tuning date and a release note explaining the revision.

## Data structure

The top-level JSON object includes:

| Field | Description |
| --- | --- |
| `format`, `formatVersion` | Identifier and schema version for clients reading the file |
| `revision`, `releaseNotes` | Dataset update number and summary |
| `data.version` | Data schema version |
| `data.checkedDate`, `data.tuningDate`, `data.status` | When the snapshot was reviewed, its tuning reference, and freshness limitations |
| `data.sources` | Named reference URLs and their available publication/check dates |
| `data.abilities` | 49 racial ability records with names, races, mechanic notes, and optional recommendation/override fields |

Records may contain `id`, `race`, `name`, `type`, `effect`, `pve`, `pvp`, `sources`, `classes`, `recommendation`, and `classOverrides`. Not every record has every optional field. Consumers should handle absent fields.

Example (Python 3):

```python
import json
from pathlib import Path

snapshot = json.loads(Path("racial-updates.json").read_text(encoding="utf-8"))
assert snapshot["format"] == "forever-planner-racials"
print("Revision:", snapshot["revision"])
print("Abilities:", len(snapshot["data"]["abilities"]))
```

## Accuracy and scope

This is a **dated research snapshot**, not a live game-data feed or official guarantee of current tuning. Re-check mechanics and recommendations against the original sources before using them. The file contains links to published reference material, including community guides and developer notes where applicable. The presence of a source link is not a claim of endorsement by that publisher.

Interpretation, class recommendations, and impact assessments are editorial content; distinguish them from verified mechanical changes.

## Maintenance and suggested contributions

For a proposed correction, open a GitHub issue describing the ability ID, affected race/class, existing value, proposed change, source URL, and source publication or check date.

When preparing an update:
1. Verify the claimed change against primary notes or another clearly identified source.
2. Keep schema compatibility in mind and avoid unrelated content changes.
3. Update `checkedDate` and `tuningDate` only when the relevant review has actually been performed.
4. Increment `revision`, update `releaseNotes`, and describe the change in the commit or pull request.
5. Check that JSON parses and that existing records remain accessible.

## Licence and attribution

Original text, editorial recommendations, annotations, and original selection/arrangement of the data are shared under the **[Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)** licence **only to the extent they are original material and rights owned by the repository maintainer**. See [LICENSE](LICENSE) for the scope, exclusions, and a link to the full legal code.

When redistributing or adapting licensed material, credit **worldofwarcraftenjoyer**, link to this repository and the CC BY 4.0 licence, and indicate changes. The licence permits commercial reuse of covered material with attribution. It does not imply the maintainer's endorsement of derivative work.

**Not included in this licence:** third-party prose, artwork, source publications, game names, trademarks, character or ability names, or other third-party intellectual property. Facts and game mechanics are not claimed as original creations. The linked external references remain under their respective owners' terms. This licence does **not** cover the private Forever Planner source code, assets, or other repositories.

This independent fan-made research dataset is not affiliated with or endorsed by Blizzard Entertainment or its partners. Game names and other third-party marks remain the property of their respective owners.
