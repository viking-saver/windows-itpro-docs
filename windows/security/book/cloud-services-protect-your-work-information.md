---
title: Cloud services - Protect your work information
description: Windows 11 security book - Cloud services chapter - Protect your work information.
ms.topic: overview
ms.date: 09/06/2024
---

# Protect your work information

:::image type="content" source="images/cloud-security.png" alt-text="Diagram containing a list of security features for cloud security." lightbox="images/cloud-security.png" border="false":::

## Microsoft Entra ID

Microsoft Entra ID is a comprehensive cloud-based identity management solution that helps enable secure access to applications, networks, and other resources and guard against threats. Microsoft Entra ID can also be used with Windows Autopilot for zero-touch provisioning of devices preconfigured with corporate security policies.

Organizations can deploy Microsoft Entra ID joined devices to enable access to both cloud and on-premises apps and resources. Access to resources can be controlled based on the Microsoft Entra ID account and Conditional Access policies applied to the device. For the most seamless and delightful end to end single sign-on (SSO) experience, we recommend users configure Windows Hello for Business during the out of box experience for easy passwordless sign-in to Entra ID .

For people wanting to connect to Microsoft Entra on their personal devices, they can do so by using *workplace join* or *add account*.  These two actions registers that user's personal device with Microsoft Entra ID, allowing IT admins to support users in bring your own device (BYOD) scenarios. Credentials are authenticated and bound to the joined device, and cannot be copied to another device without explicit reverification.

To provide more security and control for IT and a seamless experience for end users, Microsoft Entra ID works with apps and services, including on-premises software and thousands of software-as-a-service (SaaS) applications. Microsoft Entra ID protections include single sign-on, multifactor authentication, conditional access policies, identity protection, identity governance, and privileged identity management.

Windows 11 works with Microsoft Entra ID to provide secure access, identity management, and single sign-on to apps and services from anywhere. Windows has built-in settings to add work or school accounts by syncing the device configuration to an Active Directory domain or Microsoft Entra ID tenant.

:::image type="content" source="images/access-work-or-school.png" alt-text="Screenshot of the add work or school account in Settings." border="false":::

When a device is Microsoft Entra ID joined and managed with Microsoft Intune<sup>[\[9\]](conclusion.md#footnote9)</sup>, it receives the following security benefits:

- Default managed user and device settings and policies
- Single sign-in to all Microsoft Online Services
- Full suite of authentication management capabilities using Windows Hello for Business
- Single sign-on (SSO) to enterprise and SaaS applications
- No use of consumer Microsoft Account identity

Organizations and users can join or register their Windows devices with Microsoft Entra ID to get a seamless experience to both native and web applications. In addition, users can setup Windows Hello for Business or FIDO2 security keys with Microsoft Entra ID and benefit from greater security with passwordless authentication.

In combination with Microsoft Intune, Microsoft Entra ID offers powerful security control through Conditional Access to restrict access to organizational resources to healthy and compliant devices. Note that Microsoft Entra ID is only supported on Windows Pro and Enterprise editions.

Every Windows device has a built-in local administrator account that must be secured and protected to mitigate any Pass-the-Hash (PtH) and lateral traversal attacks. Many customers have been using our standalone, on-premises Windows Local Administrator Password Solution (LAPS) to manage their domain-joined Windows machines. We heard from many customers that LAPS support was needed as they modernized their Windows environment to join directly to Microsoft Entra ID.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Microsoft Entra ID documentation](/entra)
- [Microsoft Entra plans and pricing](https://www.microsoft.com/security/business/microsoft-entra-pricing?rtc=1)

### Microsoft Entra Private Access

Microsoft Entra Private Access provides organizations the ability to manage and give users access to private or internal fully qualified domain names (FQDNs) and IP addresses. With Private Access, you can modernize how your organization's users access private apps and resources. Remote workers don't need to use a VPN to access these resources if they have the Global Secure Access Client installed. The client quietly and seamlessly connects them to the resources they need.

### Microsoft Entra Internet Access

Microsoft Entra Internet Access provides an identity-centric Secure Web Gateway (SWG) solution for Software as a Service (SaaS) applications and other Internet traffic. It protects users, devices, and data from the Internet's wide threat landscape with best-in-class security controls and visibility through Traffic Logs.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Microsoft Entra Internet Access](/entra/global-secure-access/concept-internet-access)

> [!NOTE]
> Both Microsoft Entra Private Access and Microsoft Entra Internet Access requires Microsoft Entra ID and Microsoft Entra Joined devices and for deployment.

Both Microsoft Entra Private Access and Microsoft Entra Internet Access use the *Global Secure Access client for Windows*, which secures and controls the features.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Microsoft Entra Private Access](/entra/global-secure-access/concept-private-access)
- [Microsoft's Security Service Edge Solution Deployment Guide for Microsoft Entra Internet Access Proof of Concept](/entra/architecture/sse-deployment-guide-internet-access)
- [Global Secure Access client for Windows](/entra/global-secure-access/how-to-install-windows-client)

### Enterprise State Roaming

Available to any organization with a Microsoft Entra ID Premium<sup>[\[9\]](conclusion.md#footnote9)</sup> `license, Enterprise State Roaming provides users with a unified Windows Settings experience across their Windows devices and reduces the time needed for configuring a new device.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Enterprise State Roaming in Microsoft Entra ID](/entra/identity/devices/enterprise-state-roaming-enable)

## Microsoft Azure Attestation Service

Remote attestation helps ensure that devices are compliant with security policies and are operating in a trusted state before they are allowed to access resources. Microsoft Intune<sup>[\[9\]](conclusion.md#footnote9)</sup> integrates with [Microsoft Azure Attestation Service](/azure/attestation/overview) to review Windows device health comprehensively and connect this information with Microsoft Entra ID<sup>[\[9\]](conclusion.md#footnote9)</sup> Conditional Access.

**Attestation policies are configured in the Microsoft Azure Attestation Service which can then:**

- Verify the integrity of evidence provided by the Windows Attestation component by validating the signature and ensuring the Platform Configuration Registers (PCRs) match the values recomputed by replaying the measured boot log
- Verify that the TPM has a valid Attestation Identity Key issued by the authenticated TPM
- Verify that security features are in the expected states

Once this verification is complete, the attestation service returns a signed report with the security features state to the relying party - such as Microsoft Intune - to assess the trustworthiness of the platform relative to the admin-configured device compliance specifications. Conditional access is then granted or denied based on the device's compliance.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Azure Attestation overview](/azure/attestation/overview)

## Cloud-native device management

Microsoft recommends cloud-based device management so that IT professionals can manage company security policies and business applications without compromising user privacy on corporate or employee-owned devices. With cloud-native device management solutions like Microsoft Intune<sup>[\[9\]](conclusion.md#footnote9)</sup>, IT can manage Windows 11 using industry standard protocols. To simplify setup for users, management features are built directly into Windows, eliminating the need for a separate device management client.

Windows 11 built-in management features include:

- The enrollment client, which enrolls and configures the device to securely communicate with the enterprise device management server
- The management client, which periodically synchronizes with the management server to check for updates and apply the latest policies set by IT

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Mobile device management overview](/windows/client-management/mdm-overview)

### Remote wipe

When a device is lost or stolen, IT administrators might want to remotely wipe data stored in memory and hard disks. A helpdesk agent might also want to reset devices to fix issues encountered by remote workers. A remote wipe can also be used to prepare a previously used device for a new user.

Windows 11 supports the Remote Wipe configuration service provider (CSP) so that device management solutions can remotely initiate any of the following operations:

- Reset the device and remove user accounts and data
- Reset the device and clean the drive
- Reset the device but persist user accounts and data

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Remote wipe CSP](/windows/client-management/mdm/remotewipe-csp)

## Microsoft security baselines

Every organization faces security threats. However, different organizations can be concerned with different types of security threats. For example, an e-commerce company might focus on protecting its internet-facing web apps, while a hospital on confidential patient information. The one thing that all organizations have in common is a need to keep their apps and devices secure. These devices must be compliant with the security standards (or security baselines) defined by the organization.

A security baseline is a group of Microsoft-recommended configuration settings that explains their security implications. These settings are based on feedback from Microsoft security engineering teams, product groups, partners, and customers.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Security baselines](/windows/security/operating-system-security/device-management/windows-security-configuration-framework/windows-security-baselines)

## Microsoft Intune

Microsoft Intune<sup>[\[15\]](conclusion.md#footnote15)</sup> is a comprehensive cloud-native endpoint management solution that helps secure, deploy, and manage users, apps, and devices. Intune brings together technologies like Microsoft Configuration Manager and Windows Autopilot to simplify provisioning, configuration management, and software updates across the organization.

Intune works with Microsoft Entra ID to manage security features and processes, including multifactor authentication and conditional access.

Organizations can cut costs while securing and managing remote devices through the cloud in compliance with company policies<sup>[\[16\]](conclusion.md#footnote16)</sup>. For example, organizations can save time and money by provisioning preconfigured devices to remote employees using Windows Autopilot.

Windows 11 enables IT professionals to move to the cloud while consistently enforcing security policies. Windows 11 provides expanded support for group policy administrative templates (ADMX-backed policies) in cloud-native device management solutions like Microsoft Intune, enabling IT professionals to easily apply the same security policies to both on-premises and remote devices.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [What is Microsoft Intune](/mem/intune/fundamentals/what-is-intune)

### Windows enrollment attestation

When a device enrolls into device management, the administrator expects it to receive the appropriate policies to secure and manage the PC. However, in some cases, malicious actors can remove enrollment certificates and use them on unmanaged PCs, making them appear enrolled but without the intended security and management policies.

With Windows enrollment attestation, Microsoft Entra and Microsoft Intune certificates are bound to a device using the Trusted Platform Module (TPM). This ensures that the certificates cannot be transferred from one device to another, maintaining the integrity of the enrollment process.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Windows enrollment attestation](/mem/intune/enrollment/windows-enrollment-attestation)

### Endpoint Privilege Management (EPM)

Intune Endpoint Privilege Management supports organizations' Zero Trust journeys by helping them achieve a broad user base running with least privilege, while still permitting users to run tasks allowed by the organization to remain productive.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Endpoint Privilege Management](/mem/intune/protect/epm-overview?formCode=MG0AV3)

### Mobile Application Management (MAM)

With Intune, organizations can also extend MAM App Config, MAM App Protection, and App Protection Conditional Access capabilities to Windows. This enables people to access protected organizational content without having the device managed by IT. The first application to support MAM for Windows is Microsoft Edge.

Customers have asked for App Control for Business (previously called Windows Defender Application Control) to manage Installer support for a long time. Now customers will be able to enable allowlisting of Win32 apps within their enterprise to proactively reduce the number of malware infections.

Finally, Config Refresh helps organizations move to cloud from on-premises by protecting against settings deviating from the admin's intent.

Microsoft Intune also has policies and settings to configure and manage the flow of operating system updates to devices, working with WUfB and WUfB-DS and giving admins great control over their deployments

With Intune, organizations can also extend MAM App Config, MAM App Protection, and App Protection Conditional Access capabilities to Windows. This enables people to access protected organizational content without having the device managed by IT. The first application to support MAM for Windows is Microsoft Edge.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Data protection for Windows MAM](/mem/intune/apps/protect-mam-windows?formCode=MG0AV3)

### Security baseline for cloud-based device management solutions

Windows 11 can be configured with Microsoft's security baseline, designed for cloud-based device management solutions like Microsoft Intune. These security baselines function similarly to group policy-based ones and can be easily integrated into existing device management tools.

The security baseline includes policies for:

- Microsoft inbox security technologies such as BitLocker, Microsoft Defender SmartScreen, virtualization-based security, Exploit Guard, Microsoft Defender Antivirus, and Windows Firewall
- Restricting remote access to devices
- Setting credential requirements for passwords and PINs
- Restricting the use of legacy technology

The security baseline has been enhanced with over 70 new settings, enabling local user rights assignment, services management, and local security policies that were previously only available through group policy. This enhancement facilitates the adoption of cloud-based device management solutions and ensures closer adherence to industry-standard security benchmarks.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Intune security baseline overview](/mem/intune/protect/security-baselines)
- [List of the settings in the Windows security baseline in Intune](/mem/intune/protect/security-baseline-settings-mdm-all)

## Windows Local Administrator Password Solution (LAPS)

Local Administrator Password solution was a key consideration for many customers when deciding to make the transition from on-premises to cloud-managed devices using Intune. With LAPS, organizations can automatically manage and back up the password of a local administrator account on Microsoft Entra ID joined or Microsoft Entra hybrid joined devices.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Windows LAPS overview](/windows-server/identity/laps/laps-overview)

## Windows Autopilot

Traditionally, IT professionals spend significant time building and customizing images that will later be deployed to devices. If you're purchasing new devices or managing device refresh cycles, you can use Windows Autopilot to set up and preconfigure new devices, getting them ready for productive use. Autopilot helps you ensure your devices are delivered locked down and compliant with corporate security policies. The solution can also be used to reset, repurpose, and recover devices with zero touch by your IT team and no infrastructure to manage, enhancing efficiency with a process that's both easy and simple.

With Windows Autopilot, there's no need to reimage or manually set-up devices before giving them to the users. Your hardware vendor can ship them, ready to go, directly to the users. From a user perspective, they turn their device on, go online, and Windows Autopilot delivers apps and settings.

Windows Autopilot enables you to:

- Automatically join devices to Microsoft Entra ID or Active Directory via Microsoft Entra hybrid join
- Auto-enroll devices into a device management solution like Microsoft Intune (requires an Microsoft Entra ID Premium subscription for configuration)
- Create and auto-assignment of devices to configuration groups based on a device's profile
- Customize of the out-of-box experience (OOBE) content specific to your organization

Existing devices can also be quickly prepared for a new user with [Windows Autopilot Reset](/mem/autopilot/windows-autopilot-reset). The reset capability is also useful in break/fix scenarios to quickly bring a device back to a business-ready state.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Windows Autopilot](https://aka.ms/WindowsAutopilot)

## Windows Update for Business

Windows Update for Business empowers IT administrators to ensure that their organization's Windows client devices are consistently up to date with the latest security updates and features. By directly connecting these systems to the Windows Update service, administrators can maintain a high level of security and functionality.

Administrators can utilize group policy or a device management solution like Microsoft Intune, to configure Windows Update for Business settings. These settings control the timing and manner in which updates are applied, allowing for thorough reliability and performance testing on a subset of devices before deploying updates across the entire organization.

This approach not only provides control over the update process but also ensures a seamless and positive update experience for all users within the organization. By using Windows Update for Business, organizations can achieve a more secure and efficient operational environment.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Windows Update for Business documentation](/windows/deployment/update/waas-manage-updates-wufb)

## Windows Autopatch

Cybercriminals commonly exploit obsolete or unpatched software to infiltrate networks. It's essential to maintain current updates to seal security gaps. Windows Autopatch is a cloud service that automates Windows, Microsoft 365 Apps for enterprise, Microsoft Edge, and Microsoft Teams updates to improve security and productivity across your organization. Autopatch helps you minimize the involvement of your scarce IT resources in the planning and deployment of updates so your IT Admins can focus on other activities and tasks.

There's a lot more to learn about Windows Autopatch: this [Forrester Consulting Total Economic Impact&trade; Study](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RW10vlw) commissioned by Microsoft, features insights from customers who deployed Windows Autopatch and its impact on their organizations. You can also find out more information about new Autopatch features and the future of the service in the regularly published [Windows IT Pro Blog](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/bg-p/Windows-ITPro-blog/label-name/Windows%20Autopatch) and [Windowes Autopatch community](https://techcommunity.microsoft.com/t5/windows-autopatch/bd-p/Windows-Autopatch).

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Windows Autopatch documentation](/windows/deployment/windows-autopatch/)
- [Windows updates API overview](/graph/windowsupdates-concept-overview)

## OneDrive for work or school

Data in OneDrive for work or school is protected both in transit and at rest.

When data transits either into the service from clients or between datacenters, it's protected using transport layer security (TLS) encryption. OneDrive only permits secure access.

Authenticated connections are not allowed over HTTP and instead redirect to HTTPS.

There are several ways that OneDrive for work or school is protected at rest:

- Physical protection: Microsoft understands the importance of protecting customer data and is committed to securing the datacenters that contain it. Microsoft datacenters are designed, built, and operated to strictly limit physical access to the areas where customer data is stored. Physical security at datacenters is in alignment with the defense-in-depth principle. Multiple security measures are implemented to reduce the risk of unauthorized users accessing data and other datacenter resources. Learn more [here](/compliance/assurance/assurance-datacenter-physical-access-security)
- Network protection: The networks and identities are isolated from the corporate network. Firewalls limit traffic into the environment from unauthorized locations
- Application security: Engineers who build features follow the security development lifecycle. Automated and manual analyses help identify possible vulnerabilities. The [Microsoft Security Response Center](https://technet.microsoft.com/security/dn440717.aspx) helps triage incoming vulnerability reports and evaluate mitigations. Through the [Microsoft Cloud Bug Bounty Terms](https://technet.microsoft.com/dn800983), people across the world can earn money by reporting vulnerabilities
- Content protection: Each file is encrypted at rest with a unique AES-256 key. These unique keys are encrypted with a set of master keys that are stored in Azure Key Vault

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [How OneDrive safeguards data in the cloud](https://support.microsoft.com/topic/23c6ea94-3608-48d7-8bf0-80e142edd1e1)

## Universal Print

Universal Print eliminates the need for on-premises print servers. It also eliminates the need for print drivers from the users' Windows devices and makes the devices secure, reducing the malware attacks that typically exploit vulnerabilities in driver model. It enables Universal Print-ready printers (with native support) to connect directly to the Microsoft Cloud. All major printer OEMs have these [models](/universal-print/fundamentals/universal-print-partner-integrations). It also supports existing printers by using the connector software that comes with Universal Print.

Unlike traditional print solutions that rely on Windows print servers, Universal Print is a Microsoft-hosted cloud subscription service that supports a Zero Trust security model when using the Universal Print-ready printers. Customers can enable network isolation of printers, including the Universal Print connector software, from the rest of the organization's resources. Users and their devices do not need to be on the same local network as the printers or the Universal Print connector.

Universal Print supports Zero Trust security by requiring that:

- Each connection and API call to Universal Print cloud service requires authentication validated by Microsoft Entra ID<sup>[\[9\]](conclusion.md#footnote9)</sup>. A hacker would have to have knowledge of the right credentials to successfully connect to the Universal Print service
- Every connection established by the user's device (client), the printer, or another cloud service to the Universal Print cloud service uses SSL with TLS 1.2 protection. This protects network snooping of traffic to gain access to sensitive data
- Each printer registered with Universal Print is created as a device object in the customer's Microsoft Entra ID tenant and issued its own device certificate. Every connection from the printer is authenticated using this certificate. The printer can access only its own data and no other device's data
- Applications can connect to Universal Print using either user, device, or application authentication. To ensure data security, it is highly recommended that only cloud applications use application authentication
- Each acting application must register with Microsoft Entra ID and specify the set of permission scopes it requires. Microsoft's own acting applications - for example, the Universal Print connector - are registered with the Microsoft Entra ID service. Customer administrators need to provide their consent to the required permission scopes as part of onboarding the application to their tenant
- Each authentication with Microsoft Entra ID from an acting application cannot extend the permission scope as defined by the acting client app. This prevents the app from requesting additional permissions if the app is breached

Additionally, Windows 11 and Windows 10 include MDM support to simplify printer setup for users. With initial support from Microsoft Intune<sup>[\[9\]](conclusion.md#footnote9)</sup>, admins can now configure policies to provision specific printers onto the user's Windows devices.

Universal Print stores the print data in cloud securely in Office Storage, the same storage used by other Microsoft Office products.

More information about handling of Microsoft 365 data (this includes Universal Print data) can be found [here](/microsoft-365/enterprise/m365-dr-overview).

The Universal Print secure release platform ensures user privacy, secures organizational data, and reduces print wastage. It eliminates the need for people to rush to a shared printer as soon as they send a print job to ensure that no one sees the private or confidential content. Sometimes, printed documents are picked up by another person or not picked up at all and discarded. Detailed support and configuration information can be found [here](/universal-print/fundamentals/universal-print-qrcode).

Universal Print has integrated with Administrative Units in Microsoft Entra ID to enable customers to assign a Printer Administrator role to their local IT team in the same way customers assign User Administrator or Groups Administrator roles. The local IT team can configure only the printers that are part of the same Administrative Unit.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Universal Print](https://www.microsoft.com/microsoft-365/windows/universal-print)
- [Data handling in Universal Print](/universal-print/data-handling)
- [Delegate Printer Administration with Administrative Units](/universal-print/portal/delegated-admin)

For customers who want to stay on Print Servers, we recommend using the Microsoft IPP Print driver. For features beyond what's covered in the standard IPP driver, use Print Support Applications (PSA) for Windows from the respective printer OEM.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Print support app design guide](/windows-hardware/drivers/devapps/print-support-app-design-guide)
