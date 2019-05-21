# BGP

--- 
- 
  connection: local
  gather_facts: false
  hosts: S1
  name: "Manage GNS3 Devices"
  tasks: 
    - 
      ios_bgp: 
        config: 
          bgp_as: 64001
          neighbors: 
            - 
              description: eBGP_ANSIBLE_TEST_NETWORK
              ebgp_multihop: 100
              neighbor: "20.20.20.3"
              password: ansible
              remote_as: 64002
              timers: 
                holdtime: 360
                keepalive: 300
                min_neighbor_holdtime: 360
        operation: merge
      name: "Configure BGP on S1"
      register: print_output
    - 
      debug: var=print_output
- 
  connection: local
  gather_facts: false
  hosts: S3
  name: "Manage GNS3 Devices"
  tasks: 
    - 
      ios_bgp: 
        config: 
          bgp_as: 64002
          neighbors: 
            - 
              description: eBGP_ANSIBLE_TEST_NETWORK
              ebgp_multihop: 100
              neighbor: "20.20.20.1"
              password: ansible
              remote_as: 64001
              timers: 
                holdtime: 360
                keepalive: 300
                min_neighbor_holdtime: 360
        operation: merge
      name: "Configure BGP on S3"
      register: print_output
    - 
      debug: var=print_output
