# OSPF-Troubleshooting

<h2>Description</h2>
Troubleshooting problems with OSPF configurations.

<h2>Environments Used </h2>

- <b>Cisco Packet Tracer</b> (2.2.43) <br />

- <b>Cisco IOS C2900 Software, Version 15.1(4)M5 <br />

<h2>Diagram </h2>
<img src="https://i.imgur.com/40NU5jx.png" height="80%" width="80%" />

<h2>Walk-through:</h2>
Configure interfaces connecting R1 and R2 with IP addresses, clock rate and OSPF. <br />
R1(config)#int s0/0/0 <br />
R1(config-if)#ip address 192.168.12.1 255.255.255.252 <br />
R1(config-if)#clock rate 128000 <br />
R1(config-if)#ip ospf 1 area 0 <br />
R1(config-if)#no shut <br />
R1(config-if)#do show ip ospf neigh <br />
Follow R1 example for R2. <br />
<img src="https://i.imgur.com/jw3fRqG.png" height="80%" width="80%" /> <br />
<br />
<br />
