# Home-Lab
### Intention
I would like to deepen my understanding of networking, firewalls, SIEM tools, security and system administration by working hands-on since uni left out a lot of practical content. Currently v1.0 will develop practical skills in firewall management, routing, server configuration. Obvious expansions will be adding in splunk as the SIEM and then similuating attacks on the system for security testing

### Topology v1.0
<img alt="image" src="https://github.com/user-attachments/assets/07ce89a7-71f3-41a2-b17b-4e6d25410171"/>

I went with a super basic initial topology since i've never done something like this and simple = better. I'm pretty sure that expanding this setup should be *easier* (especially since this is all vm hosted at the moment) however i am looking at buying a raspberry pi and configuring old computers to help with sharing load and just add additional end hosts which are not all essentially running on my one laptops hardware (fan jetplane noises).

### Virtual Machines
Virtual Machines (VMs) are isolated computing environments that function as independent systems, each with their own dedicated CPU, memory, network interface, and storage. A hypervisor (virtualization software) manages the allocation of these resources, ensuring isolation and efficient performance.

The device running these VMs (in my case, a laptop) is called the host, while the VMs are guests. The hypervisor dynamically distributes resources from the host to the guests and allows for flexible reallocation when needed. VMs enable multiple operating systems to run on a single machine, it's a similar experience to running them on dedicated hardware, however with fewer resources, which can sometimes be frustrating. 

A key benefit is when no VMs are running all resources are reallocated back to the host machine (excluding disk space). 

## Device Setup
### pfSense
You can find the link for the .iso files below. Note if on windows you will need 7z or some equivalent to unzip the file. 

🔗 **Reference:** [pfSense .iso](https://atxfiles.netgate.com/mirror/downloads/) 

#### Configuration 
<img alt="image" src="https://github.com/user-attachments/assets/904781d7-a48c-46a0-8099-60872cd85520"/>

In the network section you can see 3 adapters, categorised as Paravirtualised Networks. To understand Paravirtualised we first must understand traditional network virtualisation (NV). NV seperates network services from physical hardware and allows virtual provision of an entire network. This allows for a programmable control to create, provision and manage networks while still relying on physical hardware for packet forwarding.  

The most common example of network virtualisation is the virtual LAN (VLAN), which segments a physical LAN into multiple isolated virtual networks. VLANs allow devices to communicate as if they were on the same physical network, even when spread across different locations, improving security and traffic management.

Paravirtualisation is a type of virtualisation where the guest operating system communicates with the hypervisor directly using special instructions called hypercalls (similair to system calls but designed for hypervisors specifically). This approach allows guest vms to interact with hardware more efficently without having direct access to the hosts kernel space. In this system all network activities in the paravirtualised network are handles through hypercalls allowing the hypervisor to manage packet transmission on the physical network. 

This improves performance compared to full emulation while still maintaining a level of isolation between VMs and the host, **though the security boundaries depend on the hypervisor’s implementation and configuration**. 

The actual configuration of pfSense is ongoing and since there currently are *no connections or managers there is nothing to add here*.

### Kali Linux
You can find the link for the .iso files below. Note if on windows you will need 7z or some equivalent to unzip the file. 

🔗 **Reference:** [Kali Linux .iso](https://www.kali.org/get-kali/#kali-installer-images) 

#### Configuration 
<img alt="image" src="https://github.com/user-attachments/assets/bfec9081-2dcc-4cb0-aee4-1e0782b11032"/>

This Kali machine, although named "VictimLinux", will be used for managing the pfSense firewall. Once the image is booted up and installed, you can navigate to 10.0.0.1 (the assigned IP of pfSense) to configure firewall rules.

After setting up the system, we need to:

1. Name our interfaces
2. Set the DNS resolver
3. Configure networking settings

Once these configurations are complete, we can proceed to firewall rules.

#### Firewall Configuration: Handling RFC1918
Proper handling of RFC1918 addresses, we must ensure that we block all private networks.

10.0.0.0/8 : 172.16.0.0/12 : 192.168.0.0/16

We will create an alias for these addresses and also include additional special-use networks:

Link-Local Address Space : 169.254.0.0/16 

Loopback Address Space : 127.0.0.0/8

This is to protect against devices assigning themselves ips in this range when they cannot obtain one from DHCP. Blocking this range prevents unwanted traffic from devices that are unable to properly join the network. 

### Topology v1.1
<img alt="image" src="https://github.com/user-attachments/assets/39da9938-4716-42bf-bf5d-14bef64f9907" />

This topology adds a new guest into the system, metaspoitable2. The guest will be hosted on LAN 1 unlike the already configured kali linux on LAN 0. 


