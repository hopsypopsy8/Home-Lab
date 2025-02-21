# Home-Lab
### Intention
I would like to deepen my understanding of networking, security and system administration by working hands-on since cough uni didn't do that. Currently v1.0 will develop practical skills in firewall management, routing, server configuration. Obvious expansions will be adding in a SIEM and then similuating attacks on the system ("testing") 

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

### pfSense
You can find the link for the .iso files below. Note if on windows you will need 7z or some equivalent to unzip the file. 

🔗 **Reference:** [Kali Linux .iso](https://www.kali.org/get-kali/#kali-installer-images) 

#### Configuration 
<img alt="image" src="https://github.com/user-attachments/assets/bfec9081-2dcc-4cb0-aee4-1e0782b11032"/>


still to do **a lot**
**talk about paravirtualized networks, internal network so all traffic goes thru pfSense (duh), what is WAN, setting up kali, using kali to**
