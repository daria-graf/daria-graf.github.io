---
layout: post
title: 'Kubernetes Cheat Sheet'
date: 2023-09-09 22:06:00 +0200
categories: cheatsheet
author: 'Daria Graf'
---

# Kubernetes Cheat Sheet

`k konfig current-context`

`k config get-contexts`

`ktx <some-context>` - change context

`k get pods` - show all pods

`k get events` - show events

`k get deployments.apps`

`k get deployments.apps <namespace> -o yaml` - show deployment log

`k edit deployments.apps <namespace>` - edit deployment settings, create and run a new pod with new settings, so the old pod will be killed

`k exec -it <some-pod> -- bash` - go inside the pod and start bash

`ps fax` - show all processes

`k get pods`

`k logs <pod-name> | grep "Error:" -B 50 -A 50`

`k logs <pod-name> -f`

`stern -l app=foo --since=1m --include=WARN`

`k delete pod <pod-name>`
