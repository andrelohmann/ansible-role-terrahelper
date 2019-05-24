terrahelper
===========

[![Build Status](https://travis-ci.org/andrelohmann/ansible-role-terrahelper.svg?branch=master)](https://travis-ci.org/andrelohmann/ansible-role-terrahelper)

terrahelper wraps the following terraform + terrahelp best practice for small teams

### Best practice:
  * create a repository for your terraform template files
  * create a repository for your the regarding terraform state
  * keep the state separated from the terraform templates folder (that's why you need the second repo)
### Workflow:
  * create/edit your templates
  * checkout latest state from the state repo
  * decrypt state using terrahelp and your state secret
  * run terraform plan/apply
  * encrypt new state using terrahelp
  * commit new state to state repo

Requirements
------------

This role requires ubuntu.


Example Playbook
----------------

    - hosts: terrahelper
      roles:
        - { role: andrelohmann.terraform }
        - { role: andrelohmann.terrahelpe }
        - { role: andrelohmann.terrahelper }

Usage
-----

terrahelper wraps the steps to de- and encrypt the terraform state of your terraform templates together with the terraform commands to init, plan, apply and destroy your stack.

Therefor you need a state secret for the de-/encryption of the terraform state and two separate repositories (one for the template and one for the state).

Run terrahelper the same way, you normally run the terraform command from within your terraform templates directory.

usage: terrahelper init | plan | apply | destroy | output [-s | --statesecret __SECRET__] [-d | --statedirectoy __STATEDIRECTORY__] [-f | --statefile terraform.tfstate] [-b | --statefilebackup terraform.tfstate.backup] [-e | --echo] [-h | --help] [any terraform parameters]


If the following environment variables are set, the regarding parameters are obsolete:

TH_SECRET - terrahelp secret used to de/encrypt the state

TH_STATE_DIRECTORY - absolute or relative (from the terraform templates directory) path to the terraform state directory

TH_STATE_FILE - terraform state file (defaults to terraform.tfstate)

TH_STATE_FILE_BACKUP - terraform state file backup (defaults to terraform.tfstate.backup)


You can also add any terrform command specific parameters to the end. They will be attached to the terraform command.

License
-------

MIT

Author Information
------------------

https://github.com/andrelohmann
