# App Connect Enterprise running over RedHat Openshift Container Platform 3.11


<img src="./avengers.jpg" width="100" alt="IBM ACE logo"/>

[IBM® App Connect Enterprise](https://www.ibm.com/cloud/app-connect/enterprise) running over RedHat Openshift Container PLatform 3.11

The purpose of this repo is share with the community one of the uses cases of integration known as "decentralized integration" using App Connect Enterprise running over RedHat Openshift Container Platform

This repo includes documentation and examples for:
- IBM App Connect Enterprise running into containers
- IBM App Connect Enterprise with IBM MQ Advanced running into containers
- IBM App Connect Enterprise automatically loading BAR files
- IBM App Connect Enterprise running over RedHat Openshift Container Platform (YAML Files)
- IBM App Connect Enterprise running over Google Kubernetes Service (YAML Files)
- IBM App Connect Enterprise include logging, monitoring to infraestructure and flows using prometheus and grafana dashboard
- CI/CD Pipeline Example using Jenkins to Check SCM, Build and Deploy App Connect Enterprise (with or without BAR Files) over RedHat Openshift

1. Preparing Security context constraints over Openshift:


Openshift Login:

  oc login 


Create project:

  oc adm new-project <project_name>


Select project:

  oc project <project_name>


Create serviceaccount over project:

oc create serviceaccount <sa_name>

Add SCC with privileged to the serviceaccount:

oc adm policy add-scc-to-user privileged -n <project_name> -z <sa_name>

 

# Copyright

© Copyright IBM Corporation 2020
- Iván Raúl Camargo Chacón Sr. Technical Solutions Architect RedHat IBM Colombia - GTS
- Juan Carlos Mesa Support Specialist ACE IBM Colombia - TSS
