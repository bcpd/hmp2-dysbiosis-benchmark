# HMP2 Dysbiosis Replication Audit

This benchmark evaluates an AI agent's ability to reproduce a published longitudinal microbiome analysis and audit sample-level dysbiosis classifications.

## Scientific source

Lloyd-Price et al. (2019). *Multi-omics of the gut microbial ecosystem in inflammatory bowel diseases*. Nature 569, 655–662.

- Publication: https://doi.org/10.1038/s41586-019-1237-9
- HMP2/IBDMDB portal: https://ibdmdb.org/results
- MGX data products: https://ibdmdb.org/downloads/html/products_MGX_2017-08-12.html

## Files

| File | Description |
|---|---|
| `task.md` | Instructions for the scientific replication audit |
| `methods_excerpt.md` | Relevant published Methods excerpt |
| `input/taxonomic_profiles_3.tsv.gz` | Public HMP2 MGX v3 taxonomic abundance profiles |
| `input/hmp2_metadata_2018-08-20.csv` | HMP2 sample metadata |
| `input/legacy_flags.txt` | Benchmark-generated draft dysbiosis classifications to audit |

The draft classifications are a constructed benchmark input, not classifications published by the original study authors.

## Running the task

Read `task.md` and `methods_excerpt.md`, then analyze the three files in `input/`.

The task uses processed taxonomic profiles. Raw-read processing and external reference databases are not required.

Local R or Python computation may be used. Follow the output specification in `task.md`.

The objective is to apply the published methodology to the supplied MGX v3 release, not to reproduce the original publication's historical sample counts.
