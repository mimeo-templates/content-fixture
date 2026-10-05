---
title: Notes, Without a Date
---

This post has no `date` front matter and no date in its filename,
so it exercises the fallback: Eleventy assigns one from the file,
and the blogs' post lists place it accordingly.

It also carries the two things portable content must not rely on,
to prove they degrade instead of failing the build:

A footnote marker.[^1]

[^1]: Footnote popovers exist only in the blogs. Here in a literary
      template this renders as literal bracketed text — visible, not
      broken.

And an image:

![A one-pixel fixture image](../../img/fixture.png)

The reference never fails a build. Where the file lands is the
template's business — see Images in the contract.
