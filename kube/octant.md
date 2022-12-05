# Octant

## Install

```bash
$ wget https://github.com/vmware-tanzu/octant/releases/download/v0.25.1/octant_0.25.1_Linux-64bit.rpm
......
100%[=====================================================================================>] 21,798,100  33.6KB/s   in 8m 50s

2019-09-03 10:31:02 (40.2 KB/s) - ‘octant_0.25.1_Linux-64bit.rpm’ saved [21798100/21798100]

$ yum install -y octant_0.25.1_Linux-64bit.rpm
Loaded plugins: fastestmirror, langpacks
Examining octant_0.25.1_Linux-64bit.rpm: octant-0.25.1.x86_64
Marking octant_0.25.1_Linux-64bit.rpm to be installed
Resolving Dependencies
--> Running transaction check
---> Package octant.x86_64 0:0.25.1 will be installed
--> Finished Dependency Resolution
......

Installed:
  octant.x86_64 0:0.25.1

Complete!

```

## Start

```bash
$ OCTANT_ACCEPTED_HOSTS=k8s.cvdnn.com KUBECONFIG=~/.kube/config OCTANT_LISTENER_ADDR=0.0.0.0:8900 octant
2022-11-22T15:54:07.565+0800	INFO	dash/watcher.go:117	watching config file	{"component": "config-watcher", "config": "/root/.kube/config"}
2022-11-22T15:54:07.568+0800	INFO	module/manager.go:87	registering action	{"component": "module-manager", "actionPath": "action.octant.dev/serviceEditor", "module-name": "overview"}
2022-11-22T15:54:07.568+0800	INFO	module/manager.go:87	registering action	{"component": "module-manager", "actionPath": "overview/stopPortForward", "module-name": "overview"}
2022-11-22T15:54:07.568+0800	INFO	module/manager.go:87	registering action	{"component": "module-manager", "actionPath": "action.octant.dev/uncordon", "module-name": "overview"}
2022-11-22T15:54:07.569+0800	INFO	module/manager.go:87	registering action	{"component": "module-manager", "actionPath": "action.octant.dev/suspendCronJob", "module-name": "overview"}
2022-11-22T15:54:07.569+0800	INFO	module/manager.go:87	registering action	{"component": "module-manager", "actionPath": "action.octant.dev/apply", "module-name": "overview"}
2022-11-22T15:54:07.569+0800	INFO	module/manager.go:87	registering action	{"component": "module-manager", "actionPath": "action.octant.dev/deploymentConfiguration", "module-name": "overview"}
2022-11-22T15:54:07.569+0800	INFO	module/manager.go:87	registering action	{"component": "module-manager", "actionPath": "action.octant.dev/containerEditor", "module-name": "overview"}
2022-11-22T15:54:07.569+0800	INFO	module/manager.go:87	registering action	{"component": "module-manager", "actionPath": "overview/startPortForward", "module-name": "overview"}
2022-11-22T15:54:07.569+0800	INFO	module/manager.go:87	registering action	{"component": "module-manager", "actionPath": "action.octant.dev/cordon", "module-name": "overview"}
2022-11-22T15:54:07.570+0800	INFO	module/manager.go:87	registering action	{"component": "module-manager", "actionPath": "action.octant.dev/cronJob", "module-name": "overview"}
2022-11-22T15:54:07.570+0800	INFO	module/manager.go:87	registering action	{"component": "module-manager", "actionPath": "action.octant.dev/resumeCronJob", "module-name": "overview"}
2022-11-22T15:54:07.570+0800	INFO	module/manager.go:87	registering action	{"component": "module-manager", "actionPath": "action.octant.dev/update", "module-name": "overview"}
2022-11-22T15:54:07.570+0800	INFO	module/manager.go:87	registering action	{"component": "module-manager", "actionPath": "action.octant.dev/manifest", "module-name": "overview"}
2022-11-22T15:54:07.570+0800	INFO	module/manager.go:87	registering action	{"component": "module-manager", "actionPath": "action.octant.dev/deleteObject", "module-name": "configuration"}
2022-11-22T15:54:07.570+0800	INFO	plugin/manager.go:412	Watching for plugin changes ["/root/.config/octant/plugins"]

2022-11-22T15:54:07.592+0800	INFO	dash/dash.go:546	Dashboard is available at http://[::]:8900

2022-11-22T15:54:07.593+0800	WARN	dash/dash.go:558	unable to open browser: exec: "xdg-open": executable file not found in $PATH
```

