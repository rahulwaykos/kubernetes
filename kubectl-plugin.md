# Extending scope of kubectl with plugins

![kubectl](https://raw.githubusercontent.com/rahulwaykos/kubernetes/master/kubectl.png)

Before diving into the topic, lets have look at few terminologies.

## Kubernetes and kubectl
Kubernetes, also known as k8s, is opensource container-orchestration tool which is generally used manage the containers,
aplication deployments, services. If you run your workload on containers then kubernetes is best option to choose. Best thing about 
kubernetes is its opensource. You can deploy it on you on-premise servers or cloud managed server, you dont have pay for anything.
Once you cluster is up and running, kubectl, is tool with whom you spend your most of the time. Its a command line tool which used to deploy 
application, services, inspect containers, to check logs. kubectl comes with lots of sub-command. Each sub-command has its own use. In this blog,
we are going to create our own subcommand, which is known as plugins.

## kubectl Plugins
Kubectl plugins are standalone scripts. Scripts can be written in any programming language. These executable scripts are stored in your `PATH` and whose names start with `kubectl-`. PATH is where all you commands are present. You can see PATH by following command :
```
# echo $PATH
```
Just place your executable script anywhere in your PATH and you are good to go.

## How to write Plugin
Create file starting with `kubectl-`. For example, `kubectl-greetings` which will create `kubectl greetings` command. To install plugin, you must
save this file anywhere in you PATH. Following is example of plugin that will greet user

```
#!/bin/bash

if [[ "$1" == ""  ]]
then
    echo "Hello" $(whoami)
    exit 0
fi


if [[ "$1" == "version" ]]
then
    echo "1.0"
    exit 0
fi

```
Save this in kubectl-greetings and run following command to make it executable. After that move this file anywhere in you `PATH` with `mv` command.
```
# chmod +x kubectl-greetings
```
Now you are all set to run `kubectl greetings` command which will output `Hello` with username. Output is shown in following screenshot

![kubectl-greetings](https://raw.githubusercontent.com/rahulwaykos/kubernetes/master/kubectl.cat)

You can check all installed plugins by running following command:
```
# kubectl plugin list
```

## Limitations 
It is not possible to create plugins which will overwrite existing kubectl command. For example, if you create `kubectl-create` script and try to run it, `kubectl create` command will always take precedence over it and your script will be ignored. For this reason you also cannot create 








