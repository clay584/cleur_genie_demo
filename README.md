# Genie Ansible Demo for CLEUR

There are four playbooks to demonstrate the Ansible Genie collection capabilities.


## Installation


1. Clone the repo.
	- `git clone https://github.com/clay584/cleur_genie_demo.git && cd cleur_genie_demo`
2. Create a virtual environment and activate it with Python 3.4 or newer.
	- `python3 -m venv .venv`
3. Activate the venv
	- `source .venv/bin/activate`
4. Install the requirements.
	- `pip install -r requirements.txt`
5. Re-activate the venv
	- `deactivate && source .venv/bin/activate`
6. Install Ansible Collection
	- `ansible-galaxy collection install clay584.genie`

## Cisco Sandbox

This demo uses the NX-OS always-on sandbox. The `inventory` file has `sbx-nxos-mgmt.cisco.com` in it and will connect to this device. You can 
change it if you want in the `inventory` file.

## Playbook Usage

### 1.yml

`$ ansible-playbook 1.yml`

This playbook learns the `arp` feature and prints the data structure to the screen. It also will fail if the `input_drops` are greater than zero. 
This is meant to show how to use specific pieces of data returned in future plays or tasks within Ansible.

### 2.yml

`$ ansible-playbook 2.yml`

This playbook starts with learning the `ospf` feature. Then the playbook pauses to let the presenter to change some aspect of OSPF configuration 
on the router manually. Then, pressing ctrl+c and c, the next play will kick off, which learns the `ospf` feature a second time, and prints the 
diff of what changed with the `ospf` feature.

### 3.yml

`$ ansible-playbook 3.yml`

This playbook starts with learning the `vlan` feature. Then the playbook pauses to let the presenter to create, change, delete a vlan 
on the device manually. Then, pressing ctrl+c and c, the next play will kick off, which learns the `vlan` feature a second time, and prints the
diff of what changed with the `vlan` feature.

### 4.yml

`$ ansible-playbook 4.yml`

This playbook learns the `routing` feature and stores it for use later in the playbook. It then runs a second task to learn it again, this time showing 
the ability to disable all of the default key exclusions in genie, and let the user specify their own list of keys to exclude from the diff. The output 
of the playbook shows that nothing changed with the `routing` feature between the two `learn_genie` tasks that were run. If you edit the playbook and comment 
out the `exclude` parameter, the diff output will show that `uptime` changed.

### 5.yml

`$ ansible-playbook 5.yml`

This playbook utilizes the `parse_genie` filter plugin to take raw CLI output and parse it using the genie parse library. This playbook does not actually 
reach out to a live device, as there is a locally defined variable that holds the raw CLI output from `show inventory` from an `ios-xe` device.
 
