# FosAgent Functionalities

- Provide state of the agent (CPU,RAM,Network,Disk,I/O,Arch,Position [GPS Coordinates])

		@AC: In general we need to provide monitoring of nodes as well as 
		deployed entities.
		

		@GB: Yes, for entities there should be a lifecycle monitor which allow access to lifecycle managment and monitoring
		Also possibility to decide what the node should monitor

		@AC: Pinning should be supported for entities that should never be migrated.
		That is important for real-time or applications depending on I/O latency. 
		Added to the list below.
		
- Pinning
- Support for Accelerators and I/O awareness in deployment
- Should be able to describe attributes of the target platform that are (1) required, (2) desirable, (3) optional, ...
- Start/Stop of native applications
- Managment of µServices (current status,configuration,deploy,relation changes,scaling,migration,shutdown)
- Managment of containers (via Docker/Kuberentes/LXC/LXD API)
- Managment of VM/Unikernels (via libvirt, support migration)
- Advertising and discovery of other agents (should come free thanks to DDS)
- Dashboard (eg. a operator pc can have an agent that discover the FogAgent and provide a simple url for accessing the dashboard)

		@AC: Eventually we also want to provide node-related functionalities, 
		such as software update, etc.
		
		The other question to address -- relevant for our collaboration with Intel -- 
		is node identity. 
		
All these functionalities should be exposed by API

		@AC: We should also list the network-releated control features 
		that will eventually be provided. Then we'll do a roadmap to
		describe what will be the intial focus.

		@GB: As we discussed network-relater control features should be:
		- assign bandwidth to a entity 
		- probably modify linux wireless stack in a way to allocate bandwidth even on wireless interfaces
		- tunnels between entities that should appear on the same network (VxLAN/OpenVSwitch VOSYS-OVSwitch/L2 Tunnels/VPN) this should also address network slicing

		Also the agent as to be extensible with plugins, these plugins can cover all the functionalites
		eg. underlying os interaction, new hypervisor/entity support
		In this way the agent become very light and can load functionalities at runtime
