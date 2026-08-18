# Building a Secure Network with OPNsense

## Overview


OPNsense serves as the security boundary for my home lab, providing routing, firewall policy, DNS services, DHCP, VPN connectivity, intrusion detection, and network segmentation.

Rather than selecting a firewall based solely on features, I wanted a platform that would allow me to better understand enterprise networking concepts while remaining flexible enough to support continuous experimentation.

The environment uses OPNsense as the primary gateway while a separate network infrastructure platform provides switching and wireless connectivity.

Objectives

The firewall should:

Protect the internal network.
Support secure remote administration.
Enable network segmentation.
Provide visibility into network traffic.
Support future security integrations.
Maintain clear separation between trusted and untrusted networks.
Provide a controlled security boundary between internal networks and the Internet.
Environment
Firewall
OPNsense
Protectli firewall appliance
Dedicated WAN interface
Dedicated LAN/trunk interface
WireGuard VPN
Network Infrastructure
OPNsense provides routing and firewall services.
A dedicated network infrastructure platform provides switching and wireless connectivity.
VLANs are used to separate networks with different trust levels.
Network Architecture

The network is designed around multiple security zones rather than a single flat LAN.

                     Internet
                        |
                        |
                 +-------------+
                 |   OPNsense  |
                 |   Firewall  |
                 +------+------+
                        |
                   VLAN Trunk
                        |
                 +------+------+
                 |   Network   |
                 |Infrastructure|
                 +-------------+
                        |
          +-------------+-------------+
          |             |             |
       Trusted         IoT          Media
       Network        Network       Network


                        |
                      Guest
                      Network


                        |
                 Isolated Network

The exact addressing, VLAN identifiers, interface assignments, and management details are intentionally omitted from this public documentation.

Network Segmentation

The environment uses separate network segments for:

Network	Purpose
Trusted	Infrastructure and trusted clients
IoT	Smart home and embedded devices
Media	Media and entertainment systems
Guest	Guest devices and temporary access
Isolated	Devices requiring Internet access without access to trusted networks

Each security zone is controlled through firewall policy appropriate to its trust level.

Isolated Network Design

One dedicated network is intentionally isolated from the trusted internal environment.

Its security model allows:

Internet access
Required DNS services
DHCP

while preventing unrestricted access to:

Trusted systems
Internal infrastructure
Other private network segments
Firewall administration interfaces

This provides a separate trust boundary for devices that should not have access to the primary home lab.

Why OPNsense?

I selected OPNsense because it provides a modern, open-source firewall platform with capabilities commonly found in enterprise and SMB environments.

Key features include:

Stateful firewall
VLAN support
WireGuard VPN
Suricata IDS/IPS
Unbound DNS
Flexible routing
Extensive logging and monitoring

It also provides an excellent environment for studying network security concepts through hands-on experimentation.

Security Design

Rather than relying on a single security control, the environment uses multiple defensive layers.

Current controls include:

Network segmentation
WireGuard VPN
Suricata IDS
CrowdSec
DNS filtering
Stateful firewall policies

Each layer provides additional protection while reducing reliance on any individual technology.

Key Decisions
VLAN Segmentation

IoT, media, guest, and isolated devices are separated from trusted systems to reduce unnecessary communication and limit the impact of a compromised device.

The segmentation model also provides an environment where firewall policies can be developed and tested independently between security zones.

DNS Protection

Local DNS resolution and filtering are used to block known malicious, advertising, and tracking domains.

This provides an additional defensive layer while improving visibility into DNS activity.

WireGuard

Remote administration is performed through WireGuard rather than exposing management interfaces directly to the Internet.

Suricata

Suricata currently operates in IDS mode.

Running in IDS mode allows me to understand normal traffic patterns, evaluate alerts, and tune detections before considering IPS enforcement.

Network Infrastructure Integration

The network infrastructure platform is responsible for switching and wireless connectivity while OPNsense remains responsible for routing, firewall policy, and security boundaries.

This separation provides clear ownership of network access and security policy.

DHCP

During the original configuration, multiple DHCP services were running simultaneously.

After identifying the conflict, DHCP services were consolidated into a single service, simplifying administration and eliminating address conflicts.

This reinforced the importance of maintaining a single authoritative DHCP service for each network.

Recovery and Rebuild

The OPNsense environment has undergone a firewall rebuild.

The recovery required validating the underlying firewall hardware and OPNsense installation before reconstructing the network configuration.

The rebuilt environment restored:

Primary network connectivity
VLAN segmentation
Network infrastructure integration
Isolated network connectivity
DHCP
Firewall policy
WireGuard infrastructure

The recovery process reinforced the importance of documenting network architecture independently of the firewall configuration itself.

See:

Case Study: Rebuilding and Restoring the OPNsense Firewall

for the detailed recovery process.

Validation

The network configuration is validated by testing individual network paths rather than relying solely on the OPNsense dashboard.

Validation includes:

WAN connectivity
Trusted network connectivity
VLAN connectivity
DHCP address assignment
DNS resolution
Internet access
Inter-VLAN firewall behavior
Network isolation
WireGuard connectivity
Firewall logging
IDS visibility
Challenges

One issue encountered during deployment involved multiple DHCP services operating simultaneously.

After identifying the conflict, DHCP services were consolidated into a single DHCP implementation, simplifying administration and eliminating address conflicts.

The OPNsense rebuild also required separating hardware and boot troubleshooting from firewall configuration recovery.

Lessons Learned

Building a firewall is relatively straightforward.

Building a network that is secure, understandable, and maintainable requires thoughtful planning and continuous refinement.

One of the most valuable lessons has been learning to make intentional design decisions instead of simply enabling every available security feature.

The OPNsense rebuild also reinforced the importance of documenting network architecture independently of the firewall itself.

Security boundaries, trust relationships, routing responsibilities, and network dependencies should be clearly understood before they are needed during a recovery.

Skills Demonstrated
OPNsense administration
Firewall configuration
Network segmentation
VLAN architecture
Network infrastructure integration
DHCP administration
DNS administration
Firewall policy design
Network troubleshooting
WireGuard administration
IDS deployment
Infrastructure recovery
Security architecture
Technical documentation
