# Ansible Plug-in Workflow Step Package

This package contains a Commander plug-in workflow step for integrating with Ansible (https://www.ansible.com/). 

It was designed specifically for use in the Commander workflow extension scenario *Installing Ansible Playbooks*, which can be found on the [Embotics Support Knowledge Base](https://support.embotics.com/support/home).

## Changelog

**Version 1.1**
  * Added "Use Credentials for sudo Password" option. Users who require a password prompt can run the script when this option is enabled.

**Version 1.0:** Initial version. 

## Plug-in steps in this package
+ Run ansible-playbook

### Run ansible-playbook
**Purpose:** Executes the ansible-playbook command to install a playbook on a target VM

**Details:** 
 * https://docs.ansible.com/ansible/2.4/ansible-playbook.html
 * Copies playbook from URL or inline YAML to `/tmp/pb-[Workflow ID].yaml` on target VM
 * Executes `ansible-playbook -i localhost, -c local /tmp/pb-[Workflow ID].yaml`
 * If successful, deletes `/tmp/pb-[Workflow ID].yaml`

**Workflows supporting this plug-in step:**

  * Command workflows
  * Completion workflows for a VM
  * Completion workflows for a change request
  * Completion workflows for a custom component
  * Completion workflows for a cloud template

**Inputs:** 

* Step Name: Input field for the name of the step
* Step Execution: Drop-down that sets the step execution behavior. By default, steps execute automatically. However, you can set the step to execute only for specific conditions.
* Timeout: Input field for timeout (in seconds)
* OS Credentials: Input field for OS credentials required to execute the command on the target VM
* User Credentials for sudo Password: Enable this checkbox to use the given OS credentials for the sudo privileges that are required when the playbook uses "become". Checking this box enables the --ask-become argument and vCommander will supply the credentials. Unchecked by default.
* Playbook URL: Input field for Playbook URL - HTTP(s), file S3 path for playbook (one of URL or YAML must be specified)
* Playbook YAML: Text Area for Playbook YAML - Inline YAML playbook (one of URL or YAML must be specified)
* Extra Variables: Text Area for Extra Variables - Set of additional variables as key=value (one per line) or YAML/JSON. If filename, prepend with @.

## Installation

Plug-in workflow steps are supported with Commander release 7.0.2 and higher. 

See [Adding plug-in workflow steps](http://docs.embotics.com/vCommander/Using-Plug-In-WF-Steps.htm#Adding) in the Commander documentation to learn how to install this package. 

## Return codes

* For ansible-playbook return codes and output, see https://docs.ansible.com/ansible/2.4/ansible-playbook.html

### Generic return codes

+ **0** - *Step completed successfully*

### Ansible return codes
+ **1** - *Unable to download playbook*
+ **2** - *SSL connection errors*
+ **3** - *Unable to create playbook file*
+ **4** - *Unable install Ansible playbook*
+ **5** - *Validation error*

## Logging
To change the logging level, add the following named loggers to the Log4j configuration file located at: 

`<vcommander-install>\tomcat\common\classes\log4j2.xml` 

+ **Run ansible-playbook** 
    + Loggers:
      + `<Logger level="DEBUG" name="wfplugins.ansible.runplaybook"/>`

## Notes
   * To use the plug-in workflow step, you must install the ansible-playbook command on the target VM. See *Installing Ansible Playbooks* on the [Embotics Support Knowledge Base](https://support.embotics.com/support/home).

   * You must install Ansible playbooks as the root user. 
