<h2 align="middle">KUBERNETES NETWORKING</h2>

<h4>NETWORKING BASIC</h4>
<img src="Resources/NETWORKING BASIC.png">
<p>NIC : NETWORK INTERFACE CARD<br>
Example : ethernet, wireless net<br>
TCP : Transfer control Protocol
</p>
<img src="Resources/TCP & IP.png">
<h5>IP Address:</h5>
    <li>IPv4 : It has a finite amount of address</li>
    <li>IPv6 : It is a new standard with many more addresses</li>

<p>From router, we get an IP Addresses, but the router itself will external IP, it is provide by your ISP (Internet Service Provider)</p>
<p> <u> Key Takaways,</u></p>
<p>Every device has some form of network enabled controller. We have protocols which are continously talking to each other across network.</p>

<h4>CONTAINER TO CONTAINER NETWORKING</h4>
<img src="Resources/CONTAINER TO CONTAINER.png">
<p>Typically we have a virtual machine, and this VM have a kubelet, on top of it, that kubelet scheduling via its CRI (Container Runtime Interface), container is represented here forms part of pod, a pod is a collections of one or more containers.<br>
Firstly, we have a ethernet device, it allows network traffic in and our of the VM, but on top of it, we have something called network namespace, it is ability to portion the network layer into isolated stacks (root network namespace). We define the pod have its own network namespace (myPodns).<br>
Secondly, when we launch a container we have to rely on a docker command of [-net=container.function] to link these containers into the pod namespaces, and these means the pods can communicate with each other, as if they are on local Host and conjuction with this, the (myPodns) attached to (root network namespace) and this allow to communication with the outside world.</p>

<h4>POD TO POD NETWORKING</h4>
<img src="Resources/POD TO POD.png">
<p>Both have unique pod network namespace and both have to share to root network namespace. This is where the root network namespace plays a much larger role. First thing is going to happen, that you notice it is a change as it we going to have a new type of device added and this is called (veth) it is used as a virtual ethernet device can be used as a patch cabel to connect two different network namespace together. At this point, if I used to send data between pods from one container to another, I still need to have dew more components one of these is the L3 virtual linux switch called Linux Bridge. The Linux Bridge here exists from the host as part of network namespace and said purpose to inspecting data frames from the incomming packets from the container and forwarding them to the correct address.<br>
When a container used to lookup IP Address of the json Pod which is connected than the first thing is happen is it hits the ethernet connection like goes through the (veth pad) and hits the (Bridge). At this point of time the bridge will decapsulates like the packet that will look at the dataframe to inspect the target IP Address and it will check to see if there is an IP Address corresponds to a Mac Address in its lookup table. The MAC Address will bound Network Interface,if it finds thereis a receiver on this network namespace that matches the target, it will send on forward data and add  a MAC Address is that it performs broadcast to every device on this network, this is using the (ARP) protocol. Th ARP Protocol asks every device and clever response will be assigned the MAC Address bound to the IP Address on incoming datatframe. This explains how to communicate between Pods in Kubernetes using IP Addresses.</p>