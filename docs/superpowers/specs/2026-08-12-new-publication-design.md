# New Publication Homepage and CV Update Design

Date: 2026-08-12

## Goal

Add the newly submitted preprint `arXiv:2608.09915` to the personal homepage and keep the downloadable CV and bibliographic source synchronized.

## Confirmed Scope

Included:

1. Add the preprint to the homepage Publications list
2. Add the matching record to the structured CV data
3. Add a matching BibTeX record
4. Regenerate the downloadable CV PDF
5. Extend publication checks to cover the new arXiv identifier
6. Build and inspect the homepage and CV before publication
7. Publish the verified update through the repository's existing GitHub Pages workflow

Excluded:

- homepage layout or styling changes
- edits to biography, research interests, positions, software, or talks
- adding a separate paper detail page, image, abstract, code link, or DOI beyond the arXiv URL

## Source Metadata

The entry will use metadata from the arXiv abstract page:

- Title: `Decoupling 2D translation-invariant topological CSS codes`
- Authors: Yifei Wang, Zhongyi Ni, Mingxin He, Jinguo Liu, and Yingfei Gu
- Identifier: `arXiv:2608.09915`
- Primary category: `quant-ph`
- Year: 2026
- URL: `https://arxiv.org/abs/2608.09915`

The homepage and CV will emphasize `Zhongyi Ni` using their existing format.

## Selected Approach

Preserve `cv/cv.yml` as the homepage and CV's shared structured data source, while keeping `cv/publications.bib` synchronized for bibliographic use.

The new entry will be inserted at the top of `publicationEntries` with `sortKey: 2026-08`. The homepage already sorts this list in descending order, and the CV renders it in source order, so the new paper will appear first in both outputs without template changes.

The BibTeX file will receive an `@misc` record with the same title, authors, year, e-print identifier, archive prefix, primary class, and arXiv URL.

## Generated Artifact

Recompile `cv/cv.typ` to replace `cv/cv.pdf`. No manual PDF editing is needed. The generated file must contain the new title, author list, and arXiv identifier while preserving the existing page structure and legibility.

## Validation

The update is complete only if:

1. `cv/check_publications.sh` requires and finds `arXiv:2608.09915`
2. `cv/check_layout.sh` passes after the new entry is added
3. Hugo builds successfully with the pinned repository script
4. The generated homepage lists the new paper first, links to the correct arXiv page, and emphasizes Zhongyi Ni
5. The regenerated CV PDF includes the new publication and remains visually readable without clipped or overlapping text
6. The working tree contains no unrelated changes
7. The update is pushed to `main`, the Pages workflow succeeds, and the public homepage and CV PDF serve the new content

## Error Handling

- If PDF generation causes an awkward page break or overflow, make the smallest CV layout adjustment necessary and rerun both CV checks.
- If Hugo fails, fix only data-format or build issues introduced by this publication entry.
- If the GitHub Pages workflow fails, inspect the failing job and repair only deployment issues attributable to this update.
- Do not publish when the rendered homepage or PDF disagrees with the arXiv metadata.
