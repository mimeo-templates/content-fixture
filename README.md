# content-fixture

The corpus that enforces [CONTENT-CONTRACT.md](CONTENT-CONTRACT.md):
one `content/` tree that must build under all four document
templates — [eleventy-chapbook](https://github.com/tepiton/eleventy-chapbook),
[eleventy-pamphlet](https://github.com/tepiton/eleventy-pamphlet),
[eleventy-prose-blog](https://github.com/tepiton/eleventy-prose-blog),
and [eleventy-tech-blog](https://github.com/tepiton/eleventy-tech-blog).

Every push to this repo — plus a weekly schedule and manual dispatch —
runs `.github/workflows/build.yml`: a four-job matrix, one job per
template, that overlays this corpus's `content/` onto the template's
own `content/` and runs `npm ci && npm run build` on node 24. A red
job means the contract is broken: the corpus or the template changed
in a way portability does not allow.

Build success is the check. Comparing rendered output or asserting
expected `_site/` paths is deliberately not done here; each template's
own demo covers its output expectations.
