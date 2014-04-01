easyOVS
=======

Provide easier and powerful operation on OpenvSwitch bridges.

version 0.2

#What is easyOVS
easyOVS provides more convinient and fluent way to operation your OpenvSwitch bridges, such as list them, dump their flows and add/del some flows. The tool is also recommended to be utilized in OpenStack environment, which can show ports with the vm MAC/IP and VLAN Tag information.

After the installation, just run:

`sudo easyovs`

easyOVS will show an interactive CLI, which supports command suggestions and formatted and colorful output.
  
#Documentation

##Commands

###help
Show the available commands and some usage examples.

###list
List the available bridges. The output would look like
```
 EasyOVS> list
s1
 Port:		s1-eth2 s1 s1-eth1
 Interface:	s1-eth2 s1 s1-eth1
 Controller:	ptcp:6634 tcp:127.0.0.1:6633
 Fail_Mode:	secure
s2
 Port:		s2 s2-eth3 s2-eth2 s2-eth1
 Interface:	s2 s2-eth3 s2-eth2 s2-eth1
 Controller:	tcp:127.0.0.1:6633 ptcp:6635
 Fail_Mode:	secure
s3
 Port:		s3-eth1 s3-eth3 s3-eth2 s3
 Interface:	s3-eth1 s3-eth3 s3-eth2 s3
 Controller:	ptcp:6636 tcp:127.0.0.1:6633
 Fail_Mode:	secure

```

###show
`EasyOVS> [bridge|default] show`

Show the ports information of a given bridge. The output would look like
```
 EasyOVS> br-int show
br-int
Intf                Port        Tag     Type        vmIP            vmMAC                   
int-br-eth0         15          0                                                           
qvo260209fa-72      11          1                   192.168.0.4     fa:16:3e:0f:17:04       
qvo583c7038-d3      2           1                   192.168.0.2     fa:16:3e:9c:dc:3a       
qvo68af47bc-2a      3           4095                                                        
qvo8bf9cba2-3f      9           1                   192.168.0.5     fa:16:3e:a2:2f:0e       
qvod4de9fe0-6d      8           2                   10.0.0.2        fa:16:3e:38:2b:2e       
br-int              LOCAL       0       internal                          
```

###dump
`EasyOVS> [bridge|default] dump`

Dump flows in a bridge. The output would look like

```
EasyOVS> s1 dump
ID TAB PKT       PRI   MATCH                                                       ACT
0  0   0         2400  dl_dst=ff:ff:ff:ff:ff:ff                                    CONTROLLER:65535
1  0   0         2400  arp                                                         CONTROLLER:65535
2  0   0         2400  dl_type=0x88cc                                              CONTROLLER:65535
3  0   0         2400  ip,nw_proto=2                                               CONTROLLER:65535
4  0   0         801   ip                                                          CONTROLLER:65535
5  0   2         800
```

###delflow
`EasyOVS> [bridge|default] delflow id`

Delete a flow with given id (see the first column of the `dump` output).


###set
`EasyOVS> bridge set`

Set the default bridge. Then you can ignore the bridge parameter when using the command.
```
EasyOVS> set br-int
Set the default bridge to br-int.
EasyOVS: br-int> 
```

###get
`EasyOVS> get`

Get the current default bridge.
```
EasyOVS: br-int> get
Current default bridge is br-int
```

###exit|quit
Input `exit` or `quit` to exit it.

#Features
* Support OpenvSwitch version 1.4.6 ~ 1.11.0.
* Format the output to make it clear and easy to compare.
* Integrate the OpenStack information
 with the bridge port (In OpenStack environment).
* Delete a flow with its id.
* Smart command completion, try tab everywhere.
* Support colorful output.

#Installation
Just run `sudo util/install.sh`.
More options can be found with `-h`.

#Credits
Thanks to the [OpenvSwitch](http://openvswitch.org) Team, [Mininet](http://mininet.org) Team and [OpenStack](http://openstack.org) Team, who gives helpful implementation example and useful tools.