---
title: 在 mjs 中使用 __dirname 与 __filename  
tag: node,mjs
---

原理分析：https://juejin.cn/post/7036744678749765640

``` js  

import { fileURLToPath } from 'url';
import { dirname } from 'path';
const __filename = fileURLToPath(import.meta.url);
const __dirname = dirname(__filename);

```
