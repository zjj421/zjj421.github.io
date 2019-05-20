---
layout: post
title: Linux stack overflow
category: Linux
tags: Linux
keywords:
description:
---

- mv大量文件报错`mv: Argument list too long`
[stack overflow](https://stackoverflow.com/questions/11942422/moving-large-number-of-files)
Question:
```
If I run the command mv folder2/*.* folder, I get "argument list too long" error.
find folder2 -name '*.*' -exec mv {} folder \;
-exec runs any command,  {} inserts the filename found, \; marks the end of the exec command.
```
Answer:
```
find folder2 -name '*.*' -exec mv {} folder \;
-exec runs any command,  {} inserts the filename found, \; marks the end of the exec command.
```
