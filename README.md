<h1> VPN-Tunneling-Lab</h1>

<h2>Setting Up a Local DNS Server</h2>
 <h4>IP Address </h4>
 
- <b>VPN SERVER : 10.0.2.10 </b>
- <b> HOST V   :  10.0. 2.4  </b>
- <b> VPN CLIENT :  10.0.2.8 </b>
<br />


<h2>Task 1: Network Setup </h2>

![image](https://user-images.githubusercontent.com/99901204/219905677-b02c7f96-c97c-45c9-892a-7f2469ada472.png)

- <b>•	Setting up the internal Network adaptor on Host V and VPN Server</b> 

![image](https://user-images.githubusercontent.com/99901204/219905693-cc2c5dba-2f60-496f-80fa-4e6b1807cc56.png)


 <h5>As shown in above screenshoot enp0s8 interface are created on VPn server  within internal ip Addresses 192.168.60.1 and Host v enp0s3 intervace connecred through internal network ip address on 192.168.60.101.</h5>

![image](https://user-images.githubusercontent.com/99901204/219905712-f2d2aa70-23b5-4d21-8b1f-8a563ebe811a.png)


  -<h5>Host U (VPN Client) can communicate with VPN Server. </h5>
 <h5> Pinging iP address OF VPN Client (10.0.2.8) from VPN server we confirmed that they can be to communicate each other.
</h5
  <h5> VPN Server can communicate with Host V.</h5>

<h5>Pinging Host v from VPN server also able to communicate each other through internal network</h5>

<h5> Host U should not be able to communicate with Host V</h5>
<h5>when try to ping with cllient from the Host V, it is not able to communicate.</h5>

![image](https://user-images.githubusercontent.com/99901204/219906292-e497720f-1b58-4d6f-ba5c-ed86bd2b945d.png)

<h2>Task 2-3-4  Creating the Tunnel </h2>

![image](https://user-images.githubusercontent.com/99901204/219906315-5c211ca8-9cd8-4ac2-84c7-274e14fed3da.png)

![image](https://user-images.githubusercontent.com/99901204/219906322-03995ced-2cc2-4744-a024-58153ff86676.png)

![image](https://user-images.githubusercontent.com/99901204/219906327-9b225e69-8f57-4319-9567-8cffdbfa7798.png)


<h5>On Vpn server machine using the code given by running  sudo ./vpnserver  the VPN server will start. </h5>
- <b> •	This will create third interface </b> 
<h5>Then while the vpn server running by  opening  second terminal "ifconfig tun0  192.168.53.1/24 up"</h5>
- <b> • This will assign ip addrees to the new  interface (tuno) and make it up </b> 

![image](https://user-images.githubusercontent.com/99901204/219906402-92064457-1885-438e-992e-3c9c558553a2.png)

![image](https://user-images.githubusercontent.com/99901204/219906415-2acf7678-d5ea-46cb-835c-d5fd6abcba1a.png)


<h5>On Vpn Client machine using the code given by running "sudo ./vpnClient"  the VPN client will start.</h5>

- <b> • This will create third interface  </b> 

<h5 > Then while the vpn Clientr running by  opening  second terminal “sudo ifconfig tun0  192.168.53.5/24 up ”</h5>

- <b> •	This will assign ip addrees to the new  interface (tuno) and make it up </b> 


<h5> Also Using "route -n " we can see current routing configurations </h5>

![image](https://user-images.githubusercontent.com/99901204/219906633-bd36574d-7872-4104-8319-39e0df29d8dd.png)


![image](https://user-images.githubusercontent.com/99901204/219906685-20a72957-cda3-4e94-97bf-93af2f79ed56.png)




<h4>  On VPN  Client machine by running “ route add -net 192.168.60.0/24 tun0” </h4>
- <b> •  This will add  destination iP address  to the routing configuration. </b> 
- <b> •	Those  192.168.53.0 and 192.168.60.0  should be able to go through tun0. </b> 

<h2>On VPN  Server  machine :- </h2>

- <b> • 192.168.53.0 should be able to go through  tun0 interface.</b>
- <b> •	192.168.60.0 should go through ep0s3 interface. </b>


<h4> Then using command “sudo sysctl net.ipv4ip_forward=1 “on VPN Server then This will make the packet forwarding machine  </h4>

![image](https://user-images.githubusercontent.com/99901204/219906819-8b36f628-1565-458f-9982-4fd862d729a4.png)

<h4> Ping 192.168.60.101 (ping Host V from client through tunnel) </h4>

![image](https://user-images.githubusercontent.com/99901204/219906921-8b7aecef-ae05-4698-ad7c-57a94616847e.png)

<h4>Setup the forward lookup zone file </h4>

![image](https://user-images.githubusercontent.com/99901204/215655695-913eaf4b-ae5f-4182-be9d-0c360ff3cff5.png)

<h4> Ping 192.168.60.101 (ping Host V from client) after breaking the tunnel  as it shows below the ping from client ti host v is not working.</h4>

