Base IP Range:
- 10.0.0.0/8

Networks:
- Guests
	- VLAN: 10
	- Subnet: 10.10.0.0/24
	- Gateway: 10.10.0.1
- Workstations
	- VLAN: 20
	- Subnet: 10.20.0.0/24
	- Gateway: 10.20.0.1
- Servers
	- VLAN: 30
	- Subnet: 10.30.0.0/24
	- Gateway: 10.30.0.1
- IOT/Automation
	- VLAN: 40
	- Subnet: 10.40.0.0/24
	- Gateway: 10.40.0.1
- Security
	- VLAN: 50
	- Subnet: 10.50.0.0/24
	- Gateway: 10.50.0.1


## Mikrotik Ports

| Port # | VLAN | Connection         |
| ------ | ---- | ------------------ |
| 1      | 30   | Uplink to Firewall |
| 2      | 20   | devStation         |
| 3      |      | disabled           |
| 4      |      | disabled           |
| 5      |      | disabled           |
| 6      |      | disabled           |
| 7      |      | disabled           |
| 8      |      | disabled           |
| 9      |      | disabled           |
| 10     |      | disabled           |
| 11     |      | disabled           |
| 12     |      | disabled           |
| 13     |      | disabled           |
| 14     |      | disabled           |
| 15     |      | disabled           |
| 16     |      | disabled           |
| 17     |      | disabled           |
| 18     |      | disabled           |
| 19     |      | disabled           |
| 20     |      | disabled           |
| 21     |      | disabled           |
| 22     |      | disabled           |
| 23     |      | disabled           |
| 24     | 10   | deco               |
## OPNSense VLAN Setup


## Mikrotik Setup
1. Go to the system tab and enable "Independent VLAN Lookup"
2. Go to VLANs and create an entry for each vlan. You will have to give it an id (number), a name, check "Port Isolation" and "Learning". Then, for every port that should have access to that vlan, check the associated box. For a note, the trunk port should have access to each vlan.
3. Go to VLAN and mark ever port as disabled.
4. Then on the ports you want to use, set the VLAN mode to optional, VLAN receive to any, give it a default vlan id (the vlan it will use), and leave force vlan id unchecked.

Here is some addition information:
https://help.mikrotik.com/docs/spaces/SWOS/pages/76415036/CRS3xx+and+CSS3xx+series+Manual#CRS3xxandCSS3xxseriesManual-VLANandVLANs