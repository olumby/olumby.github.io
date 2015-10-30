---
layout: post
title:  "Convert all MKVs in a folder to MP4"
category: os x
---

```bash 
for f in *.mkv; do avconv -i "$f" -codec copy "${f%.mkv}.mp4"; done
```
