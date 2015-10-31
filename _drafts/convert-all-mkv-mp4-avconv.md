---
layout: post
title:  "Convert all MKVs in a folder to MP4"
published: false
---

```bash 
for f in *.mkv; do avconv -i "$f" -codec copy "${f%.mkv}.mp4"; done
```
