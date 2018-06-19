# ONAP_LAB

This project provides steps and artifacts for building ESON with ONAP.

![ESON](https://github.com/moffzilla/ONAP_LAB/blob/master/media/OOM_ONAP_ESON_Single.png)
 	
## Requirements

- [ONAP](https://github.com/moffzilla/CAE/blob/master/media/CAE-Conceptual.png) working platform 

## ESON Base Deployment

Source your authentication credentials:

Execute:

	$ source keystonerc
  
Source your authentication credentials:

Execute:

	$ openstack stack create -t deploy/oom_onap.yaml --parameters "AnsibleRepository=https://github.com/moffzilla/ONAP.git;	AnsiblePlaybook=deploy/ap_onap.yml;OOMTemplate=minimal.cfg.j2" OOM

You can replace the following default settings:

	KeyName": "generic-cloud-wk"
	
	AnsibleRepository": https://github.com/moffzilla/ONAP.git"
	
	AnsiblePlaybook: "deploy/ap_onap.yml" 
  
    OOMTemplate: "minimal.cfg.j2"
  
You can also create the stack at the Horizon Dashboard

Use the command _openstack stack list to view stack that was created for the instance.

Display:

Execute nova list to view list virtual machine instances and obtain the virtual machine instance UUID for the virtul machine created by the heat stack template.

The command openstack server show <instance UUID> will provide details about the newly deployed instance.
        
    openstack server show 6a4ca385-a901-48bb-8a51-eb301108ce13

You can see the public IP and FQDN

Remove:

	openstack stack delete ONAP-stack
	
You can also delete the stack at the Horizon Dashboard
