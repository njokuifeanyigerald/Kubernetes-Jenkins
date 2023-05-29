# Kubernetes+Jenkins

This repo is about connecting kubernetes to jenkins

## open Two Terminals 


### **`in the first terminal.`**
```xml
minikube start
cd .kube
cat config
```
*vim into the config file for editing*

```xml
vi config

press shift+i to edit
```
- change *`certificate-authority`* to *`certificate-authority-data`*
-  change *`client-certificate`* to *`client-certificate-data`*
- change *`client-key`* to *`client-key-data`*


### **`open the second terminal`**
**remember to change the <user> tag to your system tag or copy the one on your system and add `<copy from your system> | base 64 -w 0`**

```xml
cd .kube
cat config
```

```xml
cat /home/<user>/.minikube/ca.crt | base64 -w 0 
```
**copy the decoded code and paste in the `certificate-authority-data` area in the first terminal** 

```xml
cat /home/<user>/.minikube/profiles/minikube/client.crt | base64 -w 0
```
**copy the decoded code and paste in the `client-certificate-data` area n the first terminal**
```xml
cat /home/<user>/.minikube/profiles/minikube/client.key | base64 -w 0 
```
**copy the decoded code and paste in the `client-key-data` area n the first terminal**


## Open Jenkins 

- click on `Manage Jenkins`, under it, click on  `manage plugin`, then  download a plugin called **kubernetes** from there and install it

- click on `Manage Nodes and Cloud`, under it, click on `built in node`, click `configure` and put `master` as the label
- in the `credentials` click `Add` to add a credential, choose `secret file`, look for `config` in the *.kube* directory, add the `config file` in the secret text and name it `kubeConfig`


