---
title: Operating System security
description: Windows 11 security book - Operating System security chapter.
ms.topic: overview
ms.date: 09/06/2024
---

# Encryption and data protection

:::image type="content" source="images/operating-system.png" alt-text="Diagram containing a list of security features." lightbox="images/operating-system.png" border="false":::

When people travel with their PCs, their confidential information travels with them. Wherever confidential data is stored, it must be protected against unauthorized access, whether through physical device theft or from malicious applications.

## BitLocker

BitLocker is a data protection feature that integrates with the operating system and addresses the threats of data theft or exposure from lost, stolen, or inappropriately decommissioned devices. BitLocker uses the AES algorithm in XTS or CBC mode of operation with 128-bit or 256-bit key length to encrypt data on the volume. BitLocker can save its recovery password to a Microsoft account for retrieval if needed. This happens automatically during the initial setup when BitLocker is enabled in OOE (Out of Box Experience) on modern devices and the user signs into their Microsoft account for the first time. Additionally, users have the option to export the recovery password if they have manually enabled BitLocker. Cloud storage on Microsoft OneDrive or Azure<sup>[\[9\]](conclusion.md#footnote9)</sup> can be used to save recovery key content. BitLocker can be managed by a device management solution like Microsoft Intune<sup>[\[6\]](conclusion.md#footnote6)</sup> using a configuration service provider (CSP)<sup>[\[9\]](conclusion.md#footnote9)</sup>. BitLocker provides encryption for the OS, fixed data, and removable data drives (BitLocker To Go), using technologies like Hardware Security Test Interface (HSTI), Modern Standby, UEFI Secure Boot, and TPM.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [BitLocker overview](../operating-system-security/data-protection/bitlocker/index.md)

## BitLocker To Go

BitLocker To Go refers to BitLocker on removable data drives. BitLocker To Go includes the encryption of USB flash drives, SD cards, and external hard disk drives. Drives can be unlocked using a password, certificate on a smart card, or recovery password.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [BitLocker FAQ](../operating-system-security/data-protection/bitlocker/faq.yml)

## Device Encryption

Device encryption is a Windows feature that simplifies the process of enabling BitLocker encryption on certain devices. It ensures that only the OS drive and fixed drives are encrypted, while external/USB drives remain unencrypted. Additionally, devices with externally accessible ports that allow DMA access are not eligible for device encryption. Unlike standard BitLocker implementation, device encryption is enabled automatically to ensure continuous protection. Once a clean installation of Windows is completed and the out-of-box experience is finished, the device is prepared for first use with encryption already in place.

Organizations have the option to disable device encryption in favor of a full BitLocker implementation. This allows for more granular control over encryption policies and settings, ensuring that the organization's specific security requirements are met.

🆕 Starting with Windows 11, version 24H2, the prerequisites of DMA and HSTI/Modern Standby is removed. This change makes more devices eligible for both automatic and manual device encryption.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Device encryption](../operating-system-security/data-protection/bitlocker/index.md#device-encryption)

## Encrypted hard drive

Encrypted hard drives are a class of hard drives that are self-encrypted at the hardware level. They allow for full-disk hardware encryption and are transparent to the user. These drives combine the security and management benefits provided by BitLocker Drive Encryption, with the power of self-encrypting drives.

By offloading the cryptographic operations to hardware, encrypted hard drives increase BitLocker performance and reduce CPU usage and power consumption. Because encrypted hard drives encrypt data quickly, BitLocker deployment can be expanded across enterprise devices with little to no impact on productivity.

Encrypted hard drives enable:

- Smooth performance: encryption hardware integrated into the drive controller allows the drive to operate at full data rate without performance degradation
- Strong security based in hardware: encryption is always-on, and the keys for encryption never leave the hard drive. The drive authenticates the user independently from the operating system before it unlocks
- Ease of use: encryption is transparent to the user, and the user doesn't need to enable it. Encrypted hard drives are easily erased using an onboard encryption key. There's no need to re-encrypt data on the drive
- Lower cost of ownership: there's no need for new infrastructure to manage encryption keys since BitLocker uses your existing infrastructure to store recovery information. Your device operates more efficiently because processor cycles don't need to be used for the encryption process

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Encrypted hard drive](../operating-system-security/data-protection/encrypted-hard-drive.md)

## Personal data encryption (PDE)

Personal Data Encryption (PDE) is a user-authenticated encryption mechanism designed to protect user's content. PDE uses Windows Hello for Business as its modern authentication scheme, with PIN or biometric authentication methods. The encryption keys used by PDE are securely stored within the Windows Hello container. When a user signs in with Windows Hello, the container is unlocked, making the keys available to decrypt the user's content.

The initial release of PDE in Windows 11, version 22H2, introduced a set of public APIs that applications can adopt to safeguard content.

🆕 Starting in Windows 11, version 24H2, PDE is further enhanced with *PDE for known folders*, which extends protection to the Windows folders: Documents, Pictures, and Desktop.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Personal Data Encryption (PDE)](../operating-system-security/data-protection/personal-data-encryption/index.md)

## Email encryption

Email encryption allows users to secure email messages and attachments so that only the intended recipients with a digital identification (ID), or certificate, can read them<sup>[\[10\]](conclusion.md#footnote10)</sup>. Users can also *digitally sign* a message, which verifies the sender's identity and ensures the message hasn't been tampered with.

The new Outlook app included in Windows 11 supports various types of email encryption, including Microsoft Purview Message Encryption, S/MIME, and Information Rights Management (IRM).

When using Secure/Multipurpose Internet Mail Extensions (S/MIME), users can send encrypted messages to people within their organization and to external contacts who have the proper encryption certificates. Recipients can only read encrypted messages if they have the corresponding decryption keys. If an encrypted message is sent to recipients whose encryption certificates aren't available, Outlook asks you to remove these recipients before sending the email.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [S/MIME for message signing and encryption in Exchange Online](/exchange/security-and-compliance/smime-exo/smime-exo)
- [Get started with the new Outlook for Windows](https://support.microsoft.com/topic/656bb8d9-5a60-49b2-a98b-ba7822bc7627)
- [Email encryption](/purview/email-encryption)
