---
title: Identity protection - Passwordless sign-in
description: Windows 11 security book -Identity protection chapter.
ms.topic: overview
ms.date: 09/06/2024
---

# Passwordless sign-in

:::image type="content" source="images/identity-protection.png" alt-text="Diagram containing a list of security features." lightbox="images/identity-protection.png" border="false":::

Passwords are a fundamental part of digital security, but they're often inconvenient and vulnerable to cyberattacks. With Windows 11, users can enjoy passwordless protection, which offers a more secure and user-friendly alternative. After a secure authorization process, credentials are safeguarded by multiple layers of hardware and software security, providing users with seamless, passwordless access to their apps and cloud services.

## Windows Hello

Too often, passwords are weak, stolen, or forgotten. Organizations are moving toward passwordless sign-in to reduce the risk of breaches, lower the cost of managing passwords, and improve productivity and satisfaction for their employees and customers. Microsoft is committed to helping organizations move toward a secure, passwordless future with Windows Hello, a cornerstone of Windows security and identity protection.

Windows Hello can enable passwordless sign-in using biometric or PIN verification and provides built-in support for the FIDO2 passwordless industry standard. As a result, people no longer need to carry external hardware like a security key for authentication.

The secure, convenient sign-in experience can augment or replace passwords with a stronger authentication model based on a PIN or biometric data such as facial or fingerprint recognition secured by the Trusted Platform Module (TPM). Step-by-step guidance makes setup easy.

Using asymmetric keys provisioned in the TPM, Windows Hello protects authentication by binding a user's credentials to their device. Windows Hello validates the user based on either a PIN or biometrics match and only then allows the use of cryptographic keys bound to that user in the TPM.

PIN and biometric data stay on the device and can't be stored or accessed externally. Since the data can't be accessed by anyone without physical access to the device, credentials are protected against replay attacks, phishing, and spoofing as well as password reuse and leaks.

Windows Hello can authenticate users to a Microsoft account (MSA), identity provider services, or the relying parties that also implement the FIDO2 or WebAuthn standards.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Configure Windows Hello][LINK-1]

### Windows Hello PIN

The Windows Hello PIN, which can only be entered by someone with physical access to the device, can be used for strong multifactor authentication. The PIN is protected by the TPM and, like biometric data, never leaves the device. When a user enters their PIN, an authentication key is unlocked and used to sign a request sent to the authenticating server.

The TPM protects against threats including PIN brute-force attacks on lost or stolen devices. After too many incorrect guesses, the device locks. IT admins can set security policies for PINs, such as complexity, length, and expiration requirements.

### Windows Hello biometric

Windows Hello biometric sign-in enhances both security and productivity with a quick, convenient sign-in experience. There's no need to enter a password every time when a face or fingerprint is the credential.

Windows devices that support biometric hardware such as fingerprint or facial recognition cameras integrate directly with Windows Hello, enabling access to Windows client resources and services. Biometric readers for both face and fingerprint must comply with Windows Hello biometric requirements. Windows Hello facial recognition is designed to only authenticate from trusted cameras used at the time of enrollment.

If a peripheral camera is attached to the device after enrollment, that camera is allowed for facial authentication after it's validated by signing in with the internal camera. For more security, external cameras can be disabled for use with Windows Hello facial recognition.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Windows Hello biometric requirements][LINK-4]

## Windows presence sensing

Windows presence sensing<sup>[\[14\]](conclusion.md#footnote14)</sup> provides another layer of data security protection for hybrid workers. Windows 11 devices can intelligently adapt to a user's presence to help them stay secure and productive, whether they're working at home, the office, or a public environment.

Windows presence sensing combines presence detection sensors with Windows Hello facial recognition to sign the user in hands-free and automatically locks the device when the user leaves. With adaptive dimming, the PC dims the screen when the user looks away on compatible devices with presence sensors. It's also easier than ever to configure presence sensors on devices, with easy enablement in the out-of-the-box experience and new links in Settings to help find presence sensing features. Device manufacturers can customize and build extensions for the presence sensor.

Privacy is top of mind and more important than ever. Customers want to have greater transparency and control over the use of their information. The new app privacy settings enable users to allow or block access to their presence sensor information. Users can decide on these settings during the initial Windows 11 setup.

Users can also take advantage of more granular settings to easily enable and disable differentiated presence sensing features like wake on approach, lock on leave, and adaptive dimming. We're also supporting developers with new APIs for presence sensing for third-party applications. Third-party applications can now access user presence information on devices with presence sensors.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Presence sensing][LINK-7]
- [Manage presence sensing settings in Windows 11][LINK-8]

## Windows Hello for Business

Windows Hello for Business extends Windows Hello to work with an organization's Active Directory and Microsoft Entra ID accounts. It provides single sign-on access to work or school resources such as OneDrive, work email, and other business apps. Windows Hello for Business also give IT admins the ability to manage PIN and other sign-in requirements for devices connecting to work or school resources.

During a device's lifecycle, a password might only need to be used once during the provisioning process. After that, people can use a PIN, face, or fingerprint to unlock credentials and sign into the device.

Provisioning methods include:

- Temporary Access Pass (TAP), a time-limited passcode with strong authentication requirements issued through Microsoft Entra ID
- Existing multifactor authentication with Microsoft Entra ID, including the Microsoft Authenticator app

Windows Hello for Business replaces the username and password by combining a security key or certificate with a PIN or biometric data and then mapping the credentials to a user account during setup. There are multiple ways to deploy Windows Hello for Business depending on an organization's needs. Organizations that rely on certificates typically use on-premises public key infrastructure (PKI) to support authentication through Certificate Trust. Organizations using key trust deployment require root-of-trust provided by certificates on domain controllers.

Organizations with hybrid scenarios can eliminate the need for on-premises domain controllers and simplify passwordless adoption by using Windows Hello for Business cloud Kerberos trust<sup>[\[13\]](conclusion.md#footnote13)</sup>. This solution uses security keys and replaces on-premises domain controllers with a cloud-based root-of-trust. As a result, organizations can take advantage of Windows Hello for Business and deploy security keys with minimal extra setup or infrastructure.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Windows Hello for Business overview][LINK-2]

### Windows Hello for Business multi-factor unlock

For organizations that need an extra layer of sign-in security, multi-factor unlock enables IT admins to configure Windows by requiring a combination of two unique trusted signals to sign in. Trusted signal examples include a PIN or biometric data (face or fingerprint) combined with either a PIN, Bluetooth, IP configuration, or Wi-Fi.

Multi-factor unlock is useful for organizations who need to prevent information workers from sharing credentials or need to comply with regulatory requirements for a two-factor authentication policy.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Multi-factor unlock][LINK-6]

### Windows passwordless experience

Windows 11 devices with Windows Hello for Business can protect user identities by removing the need to use passwords from day one.

IT can configure a policy setting for Microsoft Entra ID joined machines so users no longer see the option to enter a password when accessing company resources<sup>[\[12\]](conclusion.md#footnote12)</sup>. Once the policy is configured, passwords are removed from the Windows user experience, both for device unlock and in-session authentication scenarios. However, passwords aren't eliminated from the identity directory yet. Users are expected to navigate through their core authentication scenarios using strong, phish-resistant, possession-based credentials like Windows Hello for Business and FIDO2 security keys. If necessary, users can use passwordless recovery mechanisms such as Microsoft PIN reset service or web sign-in.

Users authenticate directly with Microsoft Entra ID, helping speed access to on-premises applications and other resources.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Windows passwordless experience][LINK-3]

## Enhanced Sign-in Security (ESS)

Windows Hello biometrics also supports Enhanced Sign-in Security, which uses specialized hardware and software components to raise the security bar even higher for biometric sign-in.

Enhanced Sign-in Security biometrics uses Virtualization-based security (VBS) and the TPM to isolate user authentication processes and data and secure the pathway by which the information is communicated.

These specialized components protect against a class of attacks that includes biometric sample injection, replay, and tampering. For example, fingerprint readers must implement Secure Device Connection Protocol, which uses key negotiation and a Microsoft-issued certificate to protect and securely store user authentication data. For facial recognition, components such as the Secure Devices (SDEV) table and process isolation with trustlets help prevent more attack classes.

Enhanced Sign-in Security is configured by device manufacturers during the manufacturing process and is most typically supported in Secured-core PCs. For facial recognition, Enhanced Sign-in Security is supported by specific silicon and camera combinations -  check with the specific device manufacturer. Fingerprint authentication is available across all processor types. Reach out to specific OEMs for support details.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Windows Hello Enhanced Sign-in Security][LINK-5]

### Passkeys

Windows 11 makes it much harder for hackers who exploit stolen passwords via phishing attacks by empowering users to replace passwords with passkeys. Passkeys are the cross-platform future of secure sign-in. Microsoft and other technology leaders are supporting passkeys across their platforms and services.

A passkey is a unique, unguessable cryptographic secret that is securely stored on the device. Instead of using a username and password to sign in to a website or application, Windows 11 users can create and use a passkey with Windows Hello, an external security provider, or their mobile device.

Passkeys on Windows 11 are protected by Windows Hello or Windows Hello for Business. This enables users to sign in to the site or app using their face, fingerprint, or device PIN. Passkeys on Windows work in any browsers or apps that support them for sign in. Users can manage passkeys on their device on Windows 11 account settings.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Support for passkeys in Windows][LINK-10]
- [Enable passkeys (FIDO2) for your organization][LINK-9]

## FIDO2

The FIDO Alliance, the Fast Identity Online industry standards body, was established to promote authentication technologies and standards that reduce reliance on passwords. FIDO Alliance and World Wide Web Consortium (W3C) have worked together to define the Client to Authenticator Protocol (CTAP2) and Web Authentication (WebAuthn) specifications, which are the industry standard for providing strong, phishing-resistant, user friendly, and privacy preserving authentication across the web and apps. FIDO standards and certifications are becoming recognized as the leading standard for creating secure authentication solutions across enterprises, governments, and consumer markets.

Windows 11 can also use passkeys from external FIDO2 security keys for authentication alongside or in addition to Windows Hello and Windows Hello for Business, which is also a FIDO2-certified passwordless solution. As a result, Windows 11 can be used as a FIDO authenticator for many popular identity management services.

## Microsoft Authenticator

The Microsoft Authenticator app, which runs on iOS and Android devices, helps keeping Windows 11 users secure and productive. Microsoft Authenticator can be used to bootstrap Windows Hello for Business, which removes the need for a password to get started on Windows 11.

Microsoft Authenticator also enables easy, secure sign-in for all online accounts using multifactor authentication, passwordless phone sign-in, phishing-resistant authentication (passkeys), or password autofill. The accounts in the Authenticator app are secured with a public/private key pair in hardware-backed storage such as the Keychain in iOS and Keystore on Android. IT admins can use different tools to nudge their users to set up the Authenticator app, provide them with extra context about where the authentication is coming from, and ensure that they're actively using it.

Individual users can back up their credentials to the cloud by enabling the encrypted backup option in settings. They can also see their sign-in history and security settings for Microsoft personal, work, or school accounts.

Using this secure app for authentication and authorization enables people to be in control of how, where, and when their credentials are used. To keep up with an ever-changing security landscape, the app is constantly updated, and new capabilities are added to stay ahead of emerging threat vectors.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Authentication methods in Microsoft Entra ID - Microsoft Authenticator app][LINK-11]

## Web sign-in

With the support of web sign-in, users can sign in without a password using the Microsoft Authenticator app or a Temporary Access Pass (TAP). Web sign in also enables federated sign in with a SAML-P identity provider.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Web sign-in for Windows][LINK-13]

## Federated sign-in

Windows 11 supports federated sign-in with external education identity management services. For students unable to type easily or remember complex passwords, this capability enables secure sign-in through methods like QR codes or pictures.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Configure federated sign-in for Windows devices][LINK-14]

## Smart cards for Windows service

Organizations can also opt for smart cards, an authentication method that existed before biometric authentication. These tamper-resistant, portable storage devices enhance Windows security by authenticating users, signing code, securing e-mails, and signing in with Windows domain accounts.

Smart cards provide:

- Ease of use in scenarios such as healthcare, where users need to sign in and out quickly without using their hands or when sharing a workstation
- Isolation of security-critical computations that involve authentication, digital signatures, and key exchange from other parts of the computer. These computations are performed on the smart card
- Portability of credentials and other private information between computers at work, home, or on the road

Smart cards can only be used to sign in to domain accounts or Microsoft Entra ID accounts.

When a password is used to sign in to a domain account, Windows uses the Kerberos Version 5 (V5) protocol for authentication. If you use a smart card, the operating system uses Kerberos V5 authentication with X.509 V3 certificates. On Microsoft Entra ID joined devices, a smart card can be used with Microsoft Entra ID certificate-based authentication. Smart cards can't be used with local accounts.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Smart Card technical reference][LINK-12]

<!--links-->

[LINK-1]: https://support.microsoft.com/topic/dae28983-8242-bb2a-d3d1-87c9d265a5f0
[LINK-2]: /windows/security/identity-protection/hello-for-business
[LINK-3]: /windows/security/identity-protection/passwordless-experience
[LINK-4]: /windows-hardware/design/device-experiences/windows-hello-biometric-requirements
[LINK-5]: /windows-hardware/design/device-experiences/windows-hello-enhanced-sign-in-security
[LINK-6]: /windows/security/identity-protection/hello-for-business/feature-multifactor-unlock
[LINK-7]: /windows-hardware/design/device-experiences/sensors-presence-sensing
[LINK-8]: https://support.microsoft.com/topic/82285c93-440c-4e15-9081-c9e38c1290bb
[LINK-9]: /entra/identity/authentication/how-to-enable-passkey-fido2
[LINK-10]: /windows/security/identity-protection/passkeys
[LINK-11]: /entra/identity/authentication/concept-authentication-authenticator-app
[LINK-12]: /windows/security/identity-protection/smart-cards/smart-card-windows-smart-card-technical-reference
[LINK-13]: /windows/security/identity-protection/web-sign-in
[LINK-14]: /education/windows/federated-sign-in
