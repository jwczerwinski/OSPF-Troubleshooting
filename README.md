# OSPF-Troubleshooting

<h2>Description</h2>
Troubleshooting problems with OSPF configurations with DCE / DTE serial connections, missing routes, network types, hello / dead intervals, and ASBR default route advertising.

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
Troubleshoot only R3 having a route to the network 10.0.2.0/24. Identify by checking OSPF neighboring interfaces characteristics to see that they match. Resolve problem and verify results. <br />
R3(config)#do show ip ospf int (command on R3 and R4 to see that Network Type does not match) <br />
<img src="https://i.imgur.com/vhi0YEx.png" height="80%" width="80%" /> <br />
R3(config)#int g0/1 <br />
R3(config-if)#no ip ospf network point-to-point (remove point-to-point, defaults back to broadcast network type) <br />
R4(config)#do show ip route <br />
<img src="https://i.imgur.com/To9bMdE.png" height="80%" width="80%" /> <br />
<br />
<br />
Troubleshoot R2 and R4 lacking the OSPF neighbor of R5. Identify by checking OSPF neighboring interfaces characteristics to see that they match. Resolve problem and verify results. <br />
R5(config)#do show ip ospf int (command on R3 and R4 to see that Network Type does not match) <br />
<img src="https://i.imgur.com/I0ZCI44.png" height="80%" width="80%" /> <br />
R5(config)#int g0/0 <br />
R5(config-if)#ip ospf hello-interval 10 (10 seconds is default) <br />
R5(config-if)#ip ospf dead-interval 40 (40 seconds is default) <br />
R5(config-if)#do show ip ospf neigh <br />
<img src="https://i.imgur.com/MMXA71E.png" height="80%" width="80%" /> <br />
<br />
<br />
Troubleshoot PC1 and PC2 can't ping 8.8.8.8. Identify by checking OSPF 'default-information orginate' and OSPF interfaces on R5, as well as OSPF interfaces on R1. Resolve problem and verify results. <br />
R5(config)#do show run (default-information originate tells all routers to use default route of the autonomous system boundary router) <br />
<img src="https://i.imgur.com/Dq5SOcU.png" height="80%" width="80%" /> <br />
R5(config)#do show ip route (need default route / gateway of last resort set so that default-information originate can advertise it to other routers) <br />
<img src="https://i.imgur.com/glNjR71.png" height="80%" width="80%" /> <br />
R5(config)#ip route 0.0.0.0 0.0.0.0 203.0.113.2 <br />
R5(config)#do show ip route <br />
<img src="https://i.imgur.com/0iXAV5B.png" height="80%" width="80%" /> <br />
R1(config)#do show ip ospf int  <br />
<img src="https://i.imgur.com/H7gjrzT.png" height="80%" width="80%" /> <br />
R1(config)#int g0/0 <br />
R1(config-if)#ip ospf 1 area 0 <br />
<img src="https://i.imgur.com/ddQbeFQ.png" height="80%" width="80%" /> <br />
<br />
<br />
