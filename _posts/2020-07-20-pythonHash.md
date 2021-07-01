---
layout: post
title:  "python hash"
date:   2020-07-20 19:59:28
categories: [All, others, Cryptography]
---

```python 
import hashlib
import sys

BLOCKSIZE = 1024
hasher = hashlib.sha1()

with open(sys.argv[1], 'rb') as f : 
    buf = f.read(BLOCKSIZE)
    while len(buf) > 0 :
        hasher.update(buf)
        buf = f.read(BLOCKSIZE)
    print(hasher.hexdigest())
f.close()
```

![image](https://user-images.githubusercontent.com/46625602/87935412-0ab51480-cacc-11ea-84cc-da1ae7d233ab.png)

---

**[Reference]**
