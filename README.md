# rulespec-ca

Canada RuleSpec encodings and source registry metadata.

## Layout

- `ca/statutes/`: Canadian statute RuleSpec YAML, with tests beside each encoding as `.test.yaml`.
- `ca/regulations/`: Canadian regulation RuleSpec YAML, with tests beside each encoding as `.test.yaml`.
- `ca/policies/`: Canadian policy RuleSpec YAML, with tests beside each encoding as `.test.yaml`.
- `data/corpus/provisions/ca/`: release-pinned Canadian source provisions used for deterministic validation.
- `manifests/releases/current.json`: exact active scopes for the local Canadian corpus release.
- `sources/`: source registry or manifest metadata when needed.

The Canadian release has one active corpus record per module citation. When a
module uses multiple official documents, their source text is consolidated in
that record rather than represented as ambiguous parallel rows.

`ca/` is the only RuleSpec jurisdiction root. Canonical IDs remain
`ca:statutes/...`, `ca:regulations/...`, and `ca:policies/...`; the directory
prefix is repository layout, not part of the ID path after the colon.

Do not add flat compatibility roots, singular rule roots, separate
parameter/test fixture files, or generated formula artifacts.

## Canadian CRS core/spouse source candidate

The [IRCC source registry](sources/ircc/express-entry/core-human-capital-spouse.json)
records a bounded Express Entry scoring candidate captured on 7 September 2026.
Its proposed scope is core human-capital points (age, recognized education,
assessed English/French language benchmarks and qualifying Canadian work
experience) plus accompanying spouse factors. It does not implement full CRS,
skill-transferability or additional points, program eligibility, invitations,
or admission. Work qualification and documentary evidence require explicit facts.

**No CRS RuleSpec module has been generated or installed.** The existing protected
supervisor starts successfully. Its source operation fails because the pinned
local corpus release object is missing; its apply preflight requires an externally
attached signing broker. The new IRCC source also needs genuine corpus admission
and an immutable release pin. Compatibility between the current encoder checkout
and the older protected installation remains unverified. This registry is an unsigned
source candidate, not an apply manifest, signed admission or production activation.

The retained local packet `capacity-sprint-20260907/canada-crs` contains official
source snapshots with dates and SHA-256 digests; actual Axiom corpus extraction
outputs; 157 table-derived boundary cases; 19 live calculator scoring observations
and one expired-evidence observation; and separately labelled cap, expiry and
missing-evidence design cases. The public calculator's full totals are retained
only as comparator context. Its core/spouse subtotals are the relevant outputs:

| Declared scoring example | Core points | Spouse points |
| --- | ---: | ---: |
| Single, age 25, recognized bachelor's credential, CELPIP 9 in each ability, no Canadian experience | 354 | 0 |
| Same applicant with an accompanying spouse with no scoring factors | 328 | 0 |
| Same applicant with a non-accompanying or Canadian citizen/permanent-resident spouse | 354 | 0 |
| Maximum core factors without an accompanying spouse | 500 | 0 |
| Maximum core and accompanying spouse factors | 460 | 40 |

The live calculator also produced an apparent TCF NCLC-4 discrepancy: it awarded
zero first-language points for four TCF bands that IRCC maps to NCLC 4, while the
ministerial and explanatory point tables give six per ability. The corresponding
CELPIP/TEF observations gave 24. Preserve the calculator observation separately
from the source-derived expectation; the packet's case-ID discrepancy mapping
records observed 0/230 versus source-derived 24/254. Do not encode it as the legal rule.

Validation so far covers source/case integrity and actual Rust execution
primitives (133 passing focused engine tests), **not an implemented CRS pilot**.
Fourteen offline packet checks pass. One bounded independent source/runtime
review completed; all four actionable findings were corrected and owner-validated.
Continuation requires the genuine apply signer on the protected subscription path,
admitted source release, real encoder apply provenance, and execution of the
independent cases through the resulting compiled RuleSpec artifact. No historical
calculator result or signed admission has been fabricated.
