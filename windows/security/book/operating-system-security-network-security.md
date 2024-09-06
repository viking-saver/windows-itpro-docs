---
title: Operating System security
description: Windows 11 security book - Operating System security chapter.
ms.topic: overview
ms.date: 09/06/2024
---

# Network security

:::image type="content" source="images/operating-system.png" alt-text="Diagram containing a list of security features." lightbox="images/operating-system.png" border="false":::

Windows 11 raises the bar for network security, offering comprehensive protection to help people work with confidence from almost anywhere. To help reduce an organization's attack
surface, network protection in Windows prevents people from accessing dangerous IP addresses and domains that may host phishing scams, exploits, and other malicious content.
Using reputation-based services, network protection blocks access to potentially harmful, low-reputation domains and IP addresses.

New DNS and TLS protocol versions strengthen the end-to-end protections needed for applications, web services, and Zero Trust networking. File access adds an untrusted network scenario with Server Message Block over QUIC, as well as new encryption and signing capabilities. Wi-Fi and Bluetooth advancements also provide greater trust in connections to other devices. In addition, VPN and Windows Firewall (previously called Windows Defender Firewall) platforms offer new ways to easily configure and debug software.

In enterprise environments, network protection works best with Microsoft Defender for Endpoint, which provides detailed reporting on protection events as part of larger investigation scenarios.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [How to protect your network](/defender-endpoint/network-protection)

## Transport Layer Security (TLS)

Transport Layer Security (TLS) is the internet's most deployed security protocol, encrypting data in transit to provide a secure communication channel between two endpoints. Windows defaults to the latest protocol versions and strong cipher suites unless policies are in effect to limit them. There are many extensions available, such as client authentication for enhanced server security and session resumption for improved application performance.

We have now added support for certificate transparency policy in certificate chain validation. This provides additional protection from trusting mis-issued certificates that have not yet been revoked. When paired with CT log monitoring, it can replace the need for certificate pinning for a domain owner.
Additionally, we have disallowed RSA certificates with keys <2048 bits within the Microsoft 3rd party trusted root store for stronger security by default.

TLS 1.3 is the latest version of the protocol and is enabled by default starting with Windows 11 and Windows Server 2022. TLS 1.3 eliminates obsolete cryptographic algorithms, enhances security over older versions, and encrypts as much of the TLS handshake as possible. The handshake is more performant, with one fewer round trip per connection on average, and supports only five strong cipher suites, which provide perfect forward secrecy and reduced operational risk.
TLS 1.3 now includes ephemeral key reuse, which improves performance (especially for high-load TLS servers) and brings it on par with TLS 1.2. The reuse time is 30 seconds by default, but is configurable. We also added the ability to enable/disable specific signature schemes (such as RSA-PSS) per-SNI binding.

Customers using TLS 1.3 (or Windows components that support it, including HTTP.SYS, WinInet, .NET, MsQuic, and more) will get enhanced privacy and lower latencies for their encrypted online connections. Note that if either the client or server does not support TLS 1.3, Windows will fall back to TLS 1.2.

Legacy protocol versions TLS 1.0 and 1.1 are officially deprecated and are now disabled by default in Azure Host 2024, but remain enabled in Windows server and client. We are planning to continue this deprecation in RS_prerelease starting July 2024. Organizations and application developers are strongly encouraged to begin to identify and remove code dependencies on TLS 1.0/1.1 if they have not done so already.




:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [TLS/SSL overview (Schannel SSP)](/windows-server/security/tls/tls-ssl-schannel-ssp-overview)
- [TLS 1.0 and TLS 1.1 soon to be disabled in Windows](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/tls-1-0-and-tls-1-1-soon-to-be-disabled-in-windows/bc-p/3894928/emcs_t/S2h8ZW1haWx8dG9waWNfc3Vic2NyaXB0aW9ufExMM0hCN0VURDk3OU9OfDM4OTQ5Mjh8U1VCU0NSSVBUSU9OU3xoSw#M6180)
- [TLS 1.0 and TLS 1.1 deprecation in Windows](https://learn.microsoft.com/en-us/windows/win32/secauthn/tls-10-11-deprecation-in-windows?tabs=registry-editor)

## Domain Name System (DNS) security

In Windows 11, the Windows DNS client supports DNS over HTTPS and DNS over TLS, two encrypted DNS protocols. These allow administrators to ensure their devices protect their
name queries from on-path attackers, whether they are passive observers logging browsing behavior or active attackers trying to redirect clients to malicious sites. In a Zero Trust
model where no trust is placed in a network boundary, having a secure connection to a trusted name resolver is required.

Windows 11 provides Group Policy as well as programmatic controls to configure DNS over HTTPS behavior. As a result, IT administrators can extend existing security to adopt new models such as Zero Trust. IT administrators can mandate DNS over HTTPS protocol, ensuring that devices that use insecure DNS will fail to connect to network resources. IT administrators also have the option not to use DNS over HTTPS or DNS over TLS for legacy deployments where network edge appliances are trusted to inspect plain-text DNS traffic. By default, Windows 11 will defer to the local administrator on which resolvers should use encrypted DNS.

Support for DNS encryption integrates with existing Windows DNS configurations such as the Name Resolution Policy Table (NRPT) and the system Hosts file, as well as resolvers specified per network adapter or network profile. The integration helps Windows 11 ensure that the benefits of greater DNS security do not regress existing DNS control mechanisms.

## Bluetooth protection

The number of Bluetooth devices connected to Windows 11 continues to increase. Windows users connect their Bluetooth headsets, mice, keyboards, and other accessories and improve their day-to-day PC experience by enjoying streaming, productivity, and gaming. Windows supports all standard Bluetooth pairing protocols, including classic and LE Secure connections, secure simple pairing, and classic and LE legacy pairing. Windows also implements host-based LE privacy. Windows updates help users stay current with OS and driver security features in accordance with the Bluetooth Special Interest Group (SIG) and Standard Vulnerability Reports, as well as issues beyond those required by the Bluetooth core industry standards. Microsoft strongly recommends that Bluetooth accessories' firmware and software are kept up to date.

IT-managed environments have a number of [Bluetooth policies](/windows/client-management/mdm/policy-csp-bluetooth) (MDM, Group Policy, and PowerShell) that can be managed through MDM tools such as Microsoft Intune<sup>[\[9\]](conclusion.md#footnote9)</sup>. You can configure Windows to use Bluetooth technology while supporting the security needs of your organization. For example, you can allow input and audio while blocking file transfer, force encryption standards, limit Windows discoverability, or even disable Bluetooth entirely for the most sensitive environments.

## Securing Wi-Fi connections

Windows Wi-Fi supports industry-standard authentication and encryption methods when connecting to Wi-Fi networks. WPA (Wi-Fi Protected Access) is a security standard defined by the Wi-Fi Alliance (WFA) to provide sophisticated data encryption and better user authentication.

The current security standard for Wi-Fi authentication is WPA3, which provides a more secure and reliable connection method as compared to WPA2 and older security protocols. Windows supports three WPA3 modes - WPA3 Personal, WPA3 Enterprise, and WPA3 Enterprise 192-bit Suite B.

Windows 11 includes WPA3 Personal with the new H2E protocol and WPA3 Enterprise 192-bit Suite B. Windows 11 also supports WPA3 Enterprise, which includes enhanced server certificate validation and TLS 1.3 for authentication using EAP-TLS authentication.

Opportunistic Wireless Encryption (OWE), a technology that allows wireless devices to establish encrypted connections to public Wi-Fi hotspots, is also included.

## 5G and eSIM

5G networks use stronger encryption and better network segmentation compared to previous generations of cellular protocols. Unlike Wi-Fi, 5G access is always mutually authenticated. Access credentials are stored in an EAL4-certified eSIM that is physically embedded in the device, making it much harder for attackers to tamper with. Together, 5G and eSIM provide a strong foundation for security.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [eSIM configuration of a download server](/mem/intune/configuration/esim-device-configuration-download-server)

## Windows Firewall

Windows Firewall with Advanced Security (previously called Windows Defender Firewall) is an important part of a layered security model. It provides host-based, two-way network traffic
filtering, blocking unauthorized traffic flowing into or out of the local device based on the types of networks the device is connected to.

Windows Firewall in Windows 11 offers the following benefits:

- Reduces the risk of network security threats: Windows Firewall reduces the attack surface of a device with rules that restrict or allow traffic by many properties, such as IP addresses,
ports, or program paths. This functionality increases manageability and decreases the likelihood of a successful attack
- Safeguards sensitive data and intellectual property: By integrating with Internet Protocol Security (IPSec), Windows Firewall provides a simple way to enforce authenticated, end-to-end network communications. It provides scalable, tiered access to trusted network resources, helping to enforce integrity of the data, and optionally helping to protect the confidentiality of the data
- Extends the value of existing investments: Because Windows Firewall is a host-based firewall that is included with the operating system, there is no additional hardware or software required. Windows Firewall is also designed to complement existing non-Microsoft network security solutions through a documented application programming interface (API)

Windows 11 makes the Windows Firewall easier to analyze and debug. IPSec behavior has been integrated with Packet Monitor (pktmon), an in-box, cross-component network diagnostic tool for Windows. Additionally, the Windows Firewall event logs have been enhanced to ensure an audit can identify the specific filter that was responsible for any given event. This enables analysis of firewall behavior and rich packet capture without relying on third-party tools.

Admins can now configure additional settings through the Firewall and Firewall Rule policy templates in the Endpoint Security node in Microsoft Intune<sup>[\[9\]](conclusion.md#footnote9)</sup>, leveraging the platform
support from the Firewall configuration service provider (CSP) and applying these settings to Windows endpoints.

Firewall  rule configuration with Package Family Name (PFN) is a new security feature introduced with the 22H2 release of Windows 11.  PFN based rules enforced on an app will include processes request by the app to run on its behalf.
Currently FW rules can be set on UWP apps with packageSID. However, the processes requested by the app can have different SID and hence the rules applied to the app can be bypassed. The new PFN condition feature ensures the FW rule is uniformly applied to a package and its associated processes.


:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Windows Firewall overview](../operating-system-security/network-security/windows-firewall/index.md)

## Virtual private networks (VPN)

Organizations have long relied on Windows to provide reliable, secured, and manageable virtual private network (VPN) solutions. The Windows VPN client platform includes built-in VPN
protocols, configuration support, a common VPN user interface, and programming support for custom VPN protocols. VPN apps are available in the Microsoft Store for both enterprise and
consumer VPNs, including apps for the most popular enterprise VPN gateways.

In Windows 11, we've integrated the most commonly used VPN controls right into the Windows 11 Quick Actions pane. From the Quick Actions pane, users can see the status of their VPN, start and stop the VPN tunnels, and with one click, go to the modern Settings app for more control.

The Windows VPN platform connects to Microsoft Entra ID<sup>[\[9\]](conclusion.md#footnote9)</sup> and Conditional Access for single sign-on, including multifactor authentication (MFA) through Microsoft Entra ID. The VPN platform also supports classic domain-joined authentication. It's supported by Microsoft Intune and other modern device management (MDM) providers. The flexible VPN profile supports both built-in protocols and custom protocols. It can configure multiple authentication methods and can be automatically started as needed or manually started by the end user. It also supports split-tunnel VPN and exclusive VPN with exceptions for trusted external sites.

With Universal Windows Platform (UWP) VPN apps, end users never get stuck on an old version of their VPN client. VPN apps from the store will be automatically updated as needed. Naturally, the updates are in the control of your IT admins.

The Windows VPN platform has been tuned and hardened for cloud-based VPN providers like Azure VPN. Features like Microsoft Entra ID authentication, Windows user interface integration, plumbing IKE traffic selectors, and server support are all built into the Windows VPN platform. The integration into the Windows VPN platform leads to a simpler IT admin experience. User authentication is more consistent, and users can easily find and control their VPN.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Windows VPN technical guide](../operating-system-security/network-security/vpn/vpn-guide.md)

## Server Message Block file services

Server Message Block (SMB) and file services are the most common Windows workloads in the commercial and public sector ecosystem. Users and applications rely on SMB to access the files that run organizations of all sizes. In Windows 11, the SMB protocol has significant security updates to meet today's threats, including AES-256 encryption, accelerated SMB signing, Remote Directory Memory Access (RDMA) network encryption, and SMB over QUIC for untrusted networks.

Signing is now required by default for all SMB outbound and inbound connections. This changes legacy behavior, where Windows 10 and 11 required SMB signing by default only when connecting to shares named SYSVOL and NETLOGON and where Active Directory domain controllers required SMB signing when any client connected to them. Signing prevents data tampering and relay attacks to malicious servers.

SMB NTLM blocking: The SMB client now supports blocking NTLM authentication for remote outbound connections. Blocking NTLM authentication prevents bad actors from tricking clients into sending NTLM requests to malicious servers, counteracting brute force, cracking, and pass-the-hash attacks. NTLM blocking is also required for switching an organization's authentication protocols to Kerberos, which is more secure than NTLM because it can verify server identities with its ticket system. You can also allow exceptions to allow NTLM authentication over SMB to specific servers only.

SMB authentication rate limiter: The SMB authentication rate limiter is a feature of SMB server designed to address brute force authentication attacks. Bruce force authentication attacks bombard the SMB server with multiple username and password-guesses and the frequency can range from dozens to thousands of attempts per second. The SMB authentication rate limiter is enabled by default with a 2 second delay between each failed NTLM or Local KDC Kerberos-based authentication attempt. An attack that sends 300 guesses per second for 5 minutes, for example  - 90,000 password guess attempts - would now take 50 hours to complete, increasing the likelihood of detection and diminishing the likelihood of successful guessing.

SMB insecure guest auth now off by default in Windows Pro editions: SMB insecure guest auth now off by default in Windows Pro editions: Windows 11 Pro no longer allows SMB client guest connections or guest fallback to an SMB server by default. This makes Windows 11 Pro operate like Windows 10 and Windows 11 Enterprise, Education, and Pro for Workstation editions have for years. Guest logons don't require passwords & don't support standard security features like signing and encryption. Allowing a client to use guest logons makes the user vulnerable to attacker-in-the-middle scenarios or malicious server scenarios - for instance, a phishing attack that tricks a user into opening a file on a remote share or a spoofed server that tricks a client into thinking it's a legitimate one. The attacker doesn't need to know the user's credentials and a bad password is ignored. Only third-party remote devices might require guest access by default. Microsoft-provided operating systems haven't allowed the general use of guest in server scenarios since Windows 2000.

SMB over QUIC client access control: SMB over QUIC client access control enables you to restrict which clients can access SMB over QUIC servers. Client access control creates allow and blocklists for devices to connect to the file server. Client access control gives organizations more protection without changing the authentication used when making the SMB connection, nor does it alter the end user experience. SMB over QUIC is available in Windows Server 2022 Datacenter: Azure Edition and now also in Windows Server 2025 (all editions). The SMB over QUIC client can now also be completely disabled or configured only to allow connection to specific servers.
SMB encryption provides end-to-end encryption of SMB data and protects data from eavesdropping occurrences on internal networks. Windows 11 introduces AES-256-GCM and AES-256-CCM cryptographic suites for SMB 3.1.1 encryption. Windows administrators can mandate the use of this more advanced security or continue to use the more compatible and still-safe AES-128 encryption.

SMB dialect management: By default SMB server and client automatically negotiates the highest matched dialect from SMB 2.0.2 to 3.1.1. You can now specify the SMB protocols used, blocking older, less secure, versions from connecting to the server. For example, you can specify connection to only use SMB 3.1.1, the most secure dialect of the protocol. The minimum and maximum can be set independently on both the SMB client and server, and you can set just a minimum if desired.

SMB client encryption mandate now supported: The SMB client now supports requiring encryption of all outbound SMB connections. Encryption of all outbound SMB client connections enforces the highest level of network security and brings management parity to SMB signing, which allows both client and server requirements. When enabled, the SMB client won't connect to an SMB server that doesn't support SMB 3.0 or later, or that doesn't support SMB encryption. For example, a third-party SMB server might support SMB 3.0 but not SMB encryption. Unlike SMB signing, encryption is not required by default.

Remote Mailslots are now deprecated and disabled by default for SMB and DCLocator usage with Active Directory. The Remote Mailslot protocol is a dated, simple, unreliable, insecure IPC method first introduced in MS DOS.

SMB alternative ports: You can use the SMB client to connect to alternative IANA/IETF TCP, QUIC, and RDMA ports than their defaults of 445, 5445, and 443. You can only connect to alternative ports if the SMB server is configured to support listening on that port. You can also configure your deployment to block configuring alternative ports or specify that ports can only connect to certain servers. In the case of Windows Server, only SMB over QUIC on Windows Server 2025 can be configured to listen on an alternative port.

SMB Firewall changes: The built-in firewall rules doesn't contain the SMB NetBIOS ports anymore.If you need to use an SMB1 server for legacy compatibility reasons, you must manually reconfigure the firewall to open those portsThis change brings SMB firewall rules more in line with the standard behavior for the Windows Server File Server role. Administrators can reconfigure the rules to restore the legacy ports.

SMB auditing improvements: SMB now supports auditing use of SMB over QUIC, missing third party support for encryption, and missing third party support for signing. These all operate at the SMB server and SMB client level.





:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [File sharing using the SMB 3 protocol](/windows-server/storage/file-server/file-server-smb-overview)
