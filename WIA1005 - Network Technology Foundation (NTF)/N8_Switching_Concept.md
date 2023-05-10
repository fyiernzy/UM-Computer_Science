# Switching concept

## 1.1 Switching in Networking

* Ingress refers to the port where a frame enters a device, while egress refers to the port that frames use when leaving the device.
* A LAN switch uses a table to forward traffic through the switch, and its only intelligence is its ability to use this table.
* The LAN switch forwards traffic based on the ingress port and destination MAC address of an Ethernet frame.
* There is only one master switching table in a LAN switch that associates MAC addresses with ports.
* An Ethernet frame with a particular destination address always exits the same egress port, regardless of the ingress port it entered.

## 1.2 The Switch MAC Address Table

* A switch is composed of integrated circuits and software that control data paths through the switch.
* Switches use destination MAC addresses to direct network communications through the appropriate port toward the destination.
* A switch learns which devices exist on each port to know which port to use to transmit a frame. It builds a MAC address table as it learns this relationship.
* The MAC address table is stored in content addressable memory (CAM), which is a special type of memory used for high-speed searching applications.
* LAN switches determine how to handle incoming data frames by maintaining the MAC address table.
* A switch populates its MAC address table by recording the source MAC address of each device connected to each of its ports.
* The switch uses the MAC address table to send frames destined for a specific device out of the port assigned to that device.

## 1.3 The Switch Learn and Forward Method

* The process of forwarding frames in a switch involves two steps: learning and forwarding.
* In the learning step, the switch examines the source MAC address and port number of an incoming frame.
  * If the MAC address is not in the MAC address table, the switch adds it along with the incoming port number.
  * If the MAC address already exists but on a different port, the switch updates the entry with the new port number.
* In the forwarding step, the switch examines the destination MAC address of the frame.
  * If the address is a unicast and is in the MAC address table, the switch forwards the frame out of the specified port.
  * If the address is not in the table, the switch floods the frame out all ports except the incoming port (unknown unicast).
  * If the address is a broadcast or multicast, the frame is also flooded out all ports except the incoming port.

## 1.4 Switching Forwarding Methods

* Switches make fast Layer 2 forwarding decisions using software on application-specific-integrated circuits (ASICs).
* Two methods are used to switch frames: Store-and-forward switching and Cut-through switching.
* Store-and-forward switching makes a forwarding decision after receiving the entire frame and checking it for errors using CRC.
* Cut-through switching begins the forwarding process after determining the destination MAC address and egress port.