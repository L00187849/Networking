# How mobile staff and maintenance contractors access applications without compromising security

**Mobile Staff & Contractor Access**

To enable secure access for mobile staff and external maintenance
contractors, a remote access VPN solution is implemented using the
FortiGate firewalls. This allows authorized users to connect securely to
internal services over the internet without exposing the network to
unnecessary risk.

**Secure Remote Access (IPsec / SSL VPN)**

Mobile users connect to the network using either IPsec VPN or SSL VPN.\
Authentication is required before access is granted, ensuring that only
authorized personnel can connect.

Security controls include:

- User authentication (username/password)

- Optional multi-factor authentication (MFA) for enhanced security

- Encrypted tunnels to protect data in transit

- Access restricted to specific internal resources

**Role-Based Access Control**

Access for users is controlled based on their role:

- Staff users are granted access to necessary internal applications
  hosted in the data centers

- Contractors are restricted to only the systems they require (e.g.
  maintenance servers or specific services in the DMZ)

This ensures that users only have access to what is strictly necessary,
following the principle of least privilege.

**Network Segmentation**

Remote access users are logically separated from the main internal LAN
using firewall policies and segmentation:

- Users connect into a controlled VPN zone

- Access to the LAN is filtered through firewall rules

- Sensitive systems remain protected behind additional layers of
  security

**DMZ-Based Access for Contractors**

Where possible, contractor access is directed to services hosted in the
DMZ rather than the internal LAN.\
This reduces the risk of exposing critical internal systems while still
allowing necessary functionality.

For example:

- Web-based management interfaces

- Monitoring tools

- Maintenance portals

**Security Protections**

To prevent unauthorized access and reduce attack risk:

- WAN-to-LAN traffic is denied by default

- Only VPN-authenticated users can access internal resources

- Firewall policies strictly control permitted traffic

- Logging and monitoring are enabled for auditing access

**Summary**

This approach ensures that mobile staff and contractors can work
remotely while maintaining strong security.\
By combining VPN encryption, authentication, role-based access, and
network segmentation, the design provides secure and controlled access
without compromising the internal network.
