# Parts library requirements

| ID | Requirement | Priority | Status |
|---|---|---|---|
| PLIB-001 | Every part in an OpenDAP BOM shall have a spec sheet here and its external files (datasheet, models) listed in the manifest. | must | Confirmed |
| PLIB-002 | Manufacturer files shall not be committed unless their licence allows redistribution; they are fetched into the local cache and verified by sha256. | must | Confirmed |
| PLIB-003 | Every spec sheet shall record the part's availability (distributor stock and price) with the date it was checked. | must | Confirmed |

## Context

- PLIB-003 (2026-10-24): the sourcing rules T1-010, T1-028 and T1-029 need availability with a date for every part; it is task E4.3 of the [electronics plan](https://github.com/opendap-project/t1/blob/main/docs/plans/2026-10-electronics-plan.md), asked by the maintainers on 2026-10-24.
