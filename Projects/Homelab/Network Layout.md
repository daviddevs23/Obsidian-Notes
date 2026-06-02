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
| 3      | 1    | disabled           |
| 4      | 1    | disabled           |
| 5      | 1    | disabled           |
| 6      | 1    | disabled           |
| 7      | 1    | disabled           |
| 8      | 1    | disabled           |
| 9      | 1    | disabled           |
| 10     | 1    | disabled           |
| 11     | 1    | disabled           |
| 12     | 1    | disabled           |
| 13     | 1    | disabled           |
| 14     | 1    | disabled           |
| 15     | 1    | disabled           |
| 16     | 1    | disabled           |
| 17     | 1    | disabled           |
| 18     | 1    | disabled           |
| 19     | 1    | disabled           |
| 20     | 1    | disabled           |
| 21     | 1    | disabled           |
| 22     | 1    | disabled           |
| 23     | 1    | disabled           |
| 24     | 10   | deco               |
## OPNSense VLAN Setup
Create the VLAN:
1. Go to Interfaces -> Devices -> VLAN
2. Select the orange plus "Add" button on the far right
3. Select a parent (usually lan), vlan tag (10, 20, 30, etc), and give it a description.
4. Hit Save and then hit Apply

Assign the VLAN:
1. Go to Interfaces -> Assignments
2. Go to the bottom section and select the device from the drop down menu. It will be called something along the lines of "vlan01 Guest Network"
3. Hit the Add button

Activate the VLAN:
1. Go to Interfaces -> [NameOfVlan]
2. Select the enable option
3. Unter IPv4 Configuration Type, select "Static IPv4"
4. Go down to Static IPv4 Configuration and give it an IP and subnet. Example for VLAN 10 is IP 10.10.0.1/24
5. Hit the save button
6. Hit apply changes at the top of the screen

Create Default Allow Firewall Rule:
1. Go to Firewall -> Rules -> [NameOfVlan]
2. Select the orange plus "Add" button
3. Change nothing and scroll down to the bottom and hit Save
4. Hit Apply Changes at the top

Set Up DHCP Server:
1. Set up all your VLANs before you set up the KEA DHCP service
2. Go to Services -> Kea DHCP -> Kea DHCPv4
3. Check the enable check box and select all interfaces you want kea on (everything but WAN).
4. Hit save and apply
5. Go to the subnets and select the red plus "Add" button.
6. Fill in the following data (example for vlan 10)
	- Subnet: 10.10.0.0/24
	- Description: Guest Network
	- Pools (range of IPs Kea will assign): 10.10.0.100-10.10.0.254
	- Uncheck "Auto Collect Option Data"
	- Routers (gateway): 10.10.0.1
	- DNS Servers: 1.1.1.1 8.8.8.8
7. Hit save
8. Add the subnets for other vlans
9. Hit apply
## Mikrotik Setup
1. Go to the system tab and enable "Independent VLAN Lookup"
2. Go to VLANs and create an entry for each vlan. You will have to give it an id (number), a name, check "Port Isolation" and "Learning". Then, for every port that should have access to that vlan, check the associated box. For a note, the trunk port should have access to each vlan.
3. Go to VLAN and mark every unused port as disabled.
4. In the VLAN tab still, set up the following ports:
	- Trunk: Vlan Mode: strict, VLAN Receive: only tagged, Default VLAN ID: 30 (servers)
	- Every other Port: Vlan Mode: enabled, VLAN Receive: only untagged, Default VLAN ID: 10 (or whatever), check Force VLAN ID

Here is some addition information:
https://help.mikrotik.com/docs/spaces/SWOS/pages/76415036/CRS3xx+and+CSS3xx+series+Manual#CRS3xxandCSS3xxseriesManual-VLANandVLANs