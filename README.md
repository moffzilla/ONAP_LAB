# ONAP_LAB
This project provides steps and artifacts for building ONAP by OOM and Integration Projects around it such as ESON.

It is based on [ OOM User Guide ](http://onap.readthedocs.io/en/latest/submodules/oom.git/docs/oom_user_guide.html)
 
 
![ESON](https://github.com/moffzilla/ONAP_LAB/blob/master/media/OOM_ONAP_Single.png)

 
## Requirements

- Running on Ubuntu Xenial (Cores=8 Mem=16G Root-Disk=160G - minimal)
- This project has tested it in OpenStack RHOSP 10 
- Make sure resources as flavor, image, SSH Keys, Security Groups referenced in the artifacts exist in the selected region.
- You’ll need OpenStack CLI installed ( tested with CLI version "openstack 3.11.0")
- More minimum requirements can be found examining the Playbooys.
- All use cases required ONAP Base Deployment ( unless indicated at sub-project section )

## ONAP Base Deployment

Source your authentication credentials:

Execute:

	$ source keystonerc
  
Source your authentication credentials:

Deploy:
1) Minimal OOM overriding default templates such as OOMTemplate

	$ openstack stack create -t deploy/oom_onap.yaml --parameter "AnsibleRepository=https://github.com/moffzilla/ONAP_LAB.git" --parameter "AnsiblePlaybook=deploy/site.yaml" --parameter "OOMTemplate=minimal.cfg.j2" ONAP-stack

2) Production OOM overriding default templates, lsuch as VM Flavor

	$ openstack stack create -t deploy/oom_onap.yaml --parameter "AnsibleRepository=https://github.com/moffzilla/ONAP_LAB.git" --parameter "AnsiblePlaybook=deploy/site.yaml" --parameter "OOMTemplate=prod.cfg.j2" --parameter "flavor=ONAP_eSON" ONAP-stack

You can replace the following default settings:

	KeyName": "ONAP"
	
	AnsibleRepository": https://github.com/moffzilla/ONAP_LAB.git"
	
	AnsiblePlaybook: "deploy/site.yaml" 
  
    OOMTemplate: "minimal.cfg.j2"
  
You can also create the stack at the Horizon Dashboard

Use the command 

	openstack stack list 

to verify that the stack was created for the instance.

Display:

Execute nova list to view list virtual machine instances and obtain the virtual machine instance UUID for the virtul machine created by the heat stack template.

        
    openstack stack show ONAP-stack | grep output_value:

	  output_value: OOM                                                                      output_value: <instance IP> 

The command openstack stack show <instance UUID> can be also used

Full details:

	openstack stack show ONAP-stack

You can access by 

	ssh ubuntu@<instance IP>

You could verify your deployment by (Please note it may take from 15 ~ 30 mins with minimal deployment depending on your compute resources ) :

	helm status dev

It shows the status of the charts and associated Pods and Containers

	kubectl get pods --all-namespaces -o=wide

It shows the status of Pods and Containers at Kubernetes level.

Remove

	openstack stack delete ONAP-stack -y
	
You can also delete the stack at the Horizon Dashboard

## Sub-Projects

[ ESON ](https://github.com/moffzilla/ONAP_LAB/tree/master/eson)
MEDIATION

## OpenStack Appendix



You can upload the base Ubuntu 16.04 image as follows:

	openstack image create --private --disk-format qcow2 --container-format bare --file xenial-server-cloudimg-amd64-disk1.img ubuntu1604
	
Image: [ xenial-server-cloudimg-amd64-disk1.img ](http://cloud-images.ubuntu.com/xenial/current/xenial-server-cloudimg-amd64-disk1.img) 

