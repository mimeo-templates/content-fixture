# The Content Contract

What `content/` means when it moves between the document templates.
This repo enforces the contract: the corpus in `content/` is built
against every template in scope on every change
(`.github/workflows/build.yml`), so the tables below state what that
build runs, not an aspiration.

## Scope

| In | Out |
|----|-----|
| [eleventy-chapbook](https://github.com/tepiton/eleventy-chapbook), [eleventy-pamphlet](https://github.com/tepiton/eleventy-pamphlet), [eleventy-prose-blog](https://github.com/tepiton/eleventy-prose-blog), [eleventy-tech-blog](https://github.com/tepiton/eleventy-tech-blog) | eleventy-product, eleventy-service — typed section files, not a document sequence |
| | pandoc-simple, pandoc-resume, mimeo, laptopistan — one input file each |

## Directories

- `content/chapters/` — the literary templates' unit (chapbook,
  pamphlet)
- `content/posts/` — the blogs' unit (prose-blog, tech-blog)
- `content/img/` — images shipped with the content (see Images below)

A corpus — and user content moved between templates — may carry all
three directories. A template renders the directory it knows as its
collection; the other directory's files are not in any collection and
build as plain pages under the template's content-root layout.

## Portable fields

| Field | Used by | Behavior in a template that does not use it |
|-------|---------|---------------------------------------------|
| `title` | all four | — |
| `draft` | all four | excluded from production builds everywhere (serve mode appends "(draft)" to the title) |
| `order` | chapbook, pamphlet | ignored; the chapter sorts by the 999 fallback plus filename |
| `date` | the blogs | ignored by the literary templates |
| `tags` | the blogs | ignored by the literary templates |
| `dek` | chapbook | ignored elsewhere |

Each template keeps its genre fields beyond this set. A field the
receiving template does not use is inert data: Eleventy passes
unknown front matter through without error, so the same file builds
anywhere in scope.

## What portable content must not rely on

- **Template-specific shortcodes or filters.** Footnote popovers
  exist only in the blogs; footnote markdown in a literary template
  renders as visible literal `[^1]` text, not a build failure.
- **Optimized image output.** The blogs run the eleventy-img
  transform; chapbook and pamphlet copy images through unchanged.

## Images

Portable content keeps its images in `content/img/`. The literary
templates copy that directory to `_site/img/` verbatim. The blogs do
not serve `content/img/` verbatim — their verbatim asset directory is
`public/`, outside `content/` — and their eleventy-img transform
optimizes only images it can resolve; an image reference in portable
content builds without failure in the blogs either way. A site that
wants optimized chapter art in a literary template adds the transform
plugin — an import and one `addPlugin` call.

An image extension that is neither in a template's `templateFormats`
nor covered by a passthrough copy is ignored by Eleventy entirely:
the file simply does not land in `_site/`. That is why the contract
names a directory instead of leaving image placement to chance.
