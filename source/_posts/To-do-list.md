---
layout: draft
title: To do list
tags:
---
1. find a process by name/portal and kill it automatically

  reference: alias kill3000="fuser -k -n tcp 3000"
kill $(ps aux | grep '[p]ython csp_build.py' | awk '{print $2}')
