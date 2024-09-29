---
tags:
  - cheatsheet
title: Kubernetes
---
---
## Setting Resource Limit
Kubernetes provides way to request minimum and maximum resources for containers in your pod. Requesting resources look like this
```
resources:
    requests:
        cpu: "500m"
        memory: "200Mi"
    limits:
        cpu: "1000m"
        memory: "4000Mi"
```
If you don't specify anything in the resources, kubernetes default to scheduling your containers with some sane defaults. You can get by with this approach in the initial phases but it helps to understand these eventually.
I found [this google blog post](https://cloud.google.com/blog/products/containers-kubernetes/kubernetes-best-practices-resource-requests-and-limits) to be very useful in understanding what these values mean.

CPU resource units are millicores. So if you require 2 cores you must specify 2000m and if you require 1/4 cores, you must specify the value as 250m.
Memory is in units of mebibytes which is practically the same as megabytes. Since I am more likely to think of ram in terms of Gb, I just enter "gb to mebibytes" to my search engine (google and duckduckgo). You can use the interactive tool to get the value you need. For instance, if I wanted a minimum ram of 4 Gb and maximum of 8 Gb, I would setup the memory to "3814Mi" and "7629Mi". 

(todo : provide link for the following claim)
My understanding is that your numbers don't need not be accurate as kubernetes will round up/down your requests to suitable value supported by the underlying platform. I usually just round up my numbers like 4000Mi, 8000Mi etc