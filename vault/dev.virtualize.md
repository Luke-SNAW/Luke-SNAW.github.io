---
id: go2Y7U1x5EtK5p44eehtr
title: Virtualize
desc: ""
updated: 1645576426590
created: 1645576372066
---

--from https://news.ycombinator.com/item?id=30433518

> Is there an eli5 or similar on the differences between podman / docker / rancher / others?
>
> Podman is for running containers on a single host. It's exactly like docker with a few additional features (like the ability to run rootless containers and run containers in something like a Kubernetes pod). Podman was developed by Red Hat to replace docker, the cli, because Docker, the company, didn't play very nice with the open source community.  
> Rancher is a Kubernetes implementation that can run containers across multiple hosts. Rancher is more comparable to something like Red Hat OpenShift or Hashicorp Nomad than docker.
