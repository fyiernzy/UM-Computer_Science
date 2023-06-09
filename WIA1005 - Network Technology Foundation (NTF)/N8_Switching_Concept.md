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

### 1.4.1 Store and Forward Switching

* Store-and-forward switching makes a forwarding decision after receiving the entire frame and checking it for errors using CRC (Cyclic Redundancy Check).

* **Error checking**
  * Error checking compares the frame check sequence (FCS) value in the last field of the datagram to ensure the frame is error-free
  * If the frame is error-free, the switch forwards the frame; otherwise, it drops the frame

* **Automatic buffering**
  * Automatic buffering is used to support any mix of Ethernet speeds
  * Store-and-forward switches store the entire frame in a buffer if there is a mismatch in speeds between the ingress and egress ports
  * The switch computes the FCS check, forwards it to the egress port buffer, and then sends it.

### 1.4.2 Cut-through switching

* Store-and-forward switching drops frames that fail the FCS check and does not forward invalid frames.
* Cut-through switching can forward invalid frames but has lower latency and faster forwarding decisions.
* This is because cut-through switching begins the forwarding process after determining the destination MAC address and egress port without performing FCS.
* Fragment free switching is a modified form of cut-through switching that provides better error checking without a significant increase in latency.
* Cut-through switching is more suitable for high-performance computing (HPC) applications with low latency requirements.
* If there is a high error rate in the network, cut-through switching can negatively impact bandwidth by forwarding damaged and invalid frames.

## 2.1 Collision Domain

* In legacy hub-based Ethernet segments, devices competed for the shared medium, causing collisions.
* Segments that share the same bandwidth are known as collision domains.
* Half-duplex segments are in their own collision domain, while full-duplex segments have no collisions.
* Switch ports will autonegotiate full-duplex when the adjacent device can also operate in full-duplex, otherwise, they will operate in half-duplex.
* In half-duplex mode, switch ports are part of a collision domain.
* Full-duplex is chosen if both devices have the capability along with their highest common bandwidth.

## 2.2 Broadcast Domain

* A collection of interconnected switches forms a single broadcast domain, which is known as the MAC broadcast domain.
* Routers can divide a Layer 2 broadcast domain and are used to segment broadcast domains.
* A Layer 2 broadcast is sent to all devices in the MAC broadcast domain (Layer 2 broadcast domain) and has a destination MAC address of all binary ones.
* When a switch receives a broadcast frame, switches forward the frames out each of their ports, except the ingress port where the broadcast frame was received.
* Each device connected to the switch receives a copy of the broadcast frame and processes it.
* Broadcasts are necessary for locating devices and network services, but too many can cause congestion and slow down network performance.

* When two switches are connected together, the broadcast domain is increased, and the broadcast frame is propagated to all devices connected to both switches.

## 2.3 Alleviate Network Congestion

* Interconnected switch ports attempt to establish a link in full-duplex, eliminating collision domains and providing the full bandwidth to connected devices.

* **Fast port speeds**
  * Ethernet switch port speeds vary by model and purpose
  * Cost more but can reduce congestion.
* **Fast Internal Switching**
  * Switches use fast internal bus or shared memory to provide high performance.
* **Large memory buffers**
  * Switches use large memory buffers to temporarily store more received frames before having to start dropping them.
  * Hence, switches are able to forward ingress traffic from faster ports to slower egress ports without losing frames.
* **High port density switches**
  * Lower overall costs
  * Reduce the number of switches required
  * Help keep traffic local to alleviate congestion