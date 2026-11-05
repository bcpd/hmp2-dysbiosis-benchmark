# HMP2 dysbiosis replication audit

A draft analysis has assigned dysbiosis flags to stool metagenomic libraries in the supplied HMP2 MGX v3 release. Audit those flags by reproducing the primary metagenomic dysbiosis definition in Lloyd-Price et al. (2019), using the supplied published Methods excerpt, `methods_excerpt.md`, as the methodological specification.

The inputs are:

- `input/taxonomic_profiles_3.tsv.gz`: IBDMDB MGX v3 taxonomic profiles (2018-05-04).
- `input/hmp2_metadata_2018-08-20.csv`: sample metadata.
- `input/legacy_flags.txt`: draft flagged library IDs, one per line. Treat this as the set to audit, not as a source of methodological rules.

Use only these inputs and the supplied excerpt. This is replication of the published definition on this release; reproducing the paper's historical sample counts is not the objective. Work offline; ordinary local computation tools are allowed.

## Technical conventions for this release

- A profile column is a library. Remove only its terminal `_profile` suffix and match the resulting ID exactly to metadata `External ID` among rows with `data_type == "metagenomics"`. `Participant ID` identifies the person; `diagnosis` uses `nonIBD`, `CD`, and `UC`. Keep technical replicate libraries as separate observations.
- Eligible libraries have a matched metadata row, a finite numeric `week_num`, and positive total species abundance. Keep rows whose final pipe-delimited taxonomic component is a nonempty `s__` species label; omit other ranks and `UNKNOWN`. Normalize each eligible library's retained species abundances to sum to one before computing dissimilarities. Apply no further taxon filtering or transformations.
- Use `week_num` directly as the study-relative week coordinate; do not re-zero time at the first library present in this release. For translating whole-week boundaries in the excerpt, the boundary week is included at its numeric value.
- Use the ordinary sample median (average the two middle values for an even-sized set). Compute percentiles by linear interpolation with index `(n - 1) * p` in the sorted sample (zero-based), equivalent to R `quantile(type = 7)`. A score equal to the threshold is flagged. Retain full numerical precision until classification.

## Required answer

Return only a JSON object with exactly these two keys, containing library IDs without `_profile`:

```json
{"remove_flag": [], "add_flag": []}
```

`remove_flag` contains every draft-flagged library that should not be flagged under the replicated definition. `add_flag` contains every library that should be flagged but is absent from the draft set. Return each ID once; order is immaterial. Empty lists are permitted. No counts, scores, explanations, or additional keys belong in the answer.
