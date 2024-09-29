---
title: ImageMagick
tags:
  - cheatsheet
---
`convert` is how you access imagemagick through cli

### Resize all images in a folder

`convert *.jpg -resize 1024X1024 -set filename:f '%t' '%[filename:f].jpg'`
