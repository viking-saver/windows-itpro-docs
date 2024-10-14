---
title: Application and driver control
description: Windows 11 security book - Application and driver control.
ms.topic: overview
ms.date: 09/06/2024
---

# Application and driver control

:::image type="content" source="images/application-security.png" alt-text="Diagram containing a list of application security features." lightbox="images/application-security.png" border="false":::

Windows 11 offers a rich application platform with layers of security like isolation and code integrity that help protect your valuable data. Developers can also take advantage of these
capabilities to build in security from the ground up to protect against breaches and malware.

## Smart App Control

Smart App Control prevents users from running malicious applications by blocking untrusted or unsigned applications. Smart App Control goes beyond previous built-in browser protections by adding another layer of security that is woven directly into the core of the OS at the process level. Using AI, Smart App Control only allows processes to run if they're predicted to be safe based on existing and new intelligence updated daily.

Smart App Control builds on top of the same cloud-based AI used in App Control for Business to predict the safety of an application so that users can be confident that their applications are safe and reliable on their new Windows devices. Additionally, Smart App Control blocks unknown script files and macros from the web, greatly improving security for everyday users. Smart App Control shipped in evaluation mode for new device starting in Windows 11, version 22H2.

We've been making significant improvements to Smart App Control to increase the security, usability, and cloud intelligence response for apps in the Windows ecosystem. Users can get the latest and best experience with Smart App Control by keeping their PC up to date via Windows Update every month.

Additionally, evaluation mode starts automatically enabling devices that the cloud AI model predicts will have a good experience with Smart App Control in the coming months, first starting with users in North America and eventually expanding to other regions.

As a developer, to ensure that your users have a seamless experience with Smart App Control enabled, we ask that you sign your application with a code signing certificate from the Microsoft Trusted Root Program.  Make sure to include all binaries, such as exe, dll, temp installer files, and uninstallers. Trusted signing makes the process of obtaining, maintaining, and signing with a trusted certificate simple and secure. More on that later in this doc.

Devices running previous versions of Windows 11 will have to be reset with a clean installation of Windows 11, version 22H2 or later to take advantage of this feature. Smart App Control will be disabled on devices enrolled in enterprise management. We suggest enterprises running line-of-business applications continue to leverage App Control for Business.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Smart App Control][LINK-1]

## App Control for Business

Your organization is only as secure as the applications that run on your devices. With *application control*, apps must earn trust to run, in contrast to an application trust model where all code is assumed trustworthy. By helping prevent unwanted or malicious code from running, application control is an important part of an effective security strategy. Many organizations cite application control as one of the most effective means of defending against executable file-based malware.

App Control for Business (previously called *Windows Defender Application Control*) and AppLocker are both included in Windows. App Control for Business is the next-generation app control solution for Windows and provides powerful control over what runs in your environment. Customers who were using AppLocker on previous versions of Windows can continue to use the feature as they consider whether to switch to App Control for Business for stronger protection.

Customers using Microsoft Intune to manage their devices are now able to configure App Control for Business in the admin console, including setting up Intune as a managed installer.

Customers can use some built-in options for App Control for Business or upload their own policy as an XML file for Intune to package and deploy.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Application Control for Windows][LINK-2]
- [Automatically allow apps deployed by a managed installer with App Control for Business][LINK-3]

## User Account Control

User Account Control (UAC) helps prevent malware from damaging a PC and enables organizations to deploy a better-managed desktop. With UAC, apps and tasks always run in the security context of a non-administrator account unless an administrator specifically authorizes administrator-level access to the system. UAC can block the automatic installation of unauthorized apps and prevent inadvertent changes to system settings.

Organizations can use a device management solution like Microsoft Intune to remotely configure UAC settings. For those without such a solution, settings can be adjusted directly on the device.

Enabling UAC helps prevent malware from altering PC settings and potentially gaining access to networks and sensitive data. UAC can also block the automatic installation of unauthorized
apps and prevent inadvertent changes to system settings.

Users with standard accounts, or those using administrative accounts with UAC enabled, run most programs with limited access rights. This includes the Windows shell and any apps started from the shell, such as Windows Explorer, a web browser, productivity suite, graphics programs, or games.

Some apps require more permissions and won't work properly (or at all) when running with limited permissions. When an app needs to run with more than standard user rights, UAC allows users to run apps with a *full* administrator token (with administrative groups and privileges) instead of their default user access token. Users continue to operate in the standard user security context while enabling certain executables to run with elevated privileges if needed.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [How User Account Control works](/windows/security/identity-protection/user-account-control/how-user-account-control-works)

## Microsoft vulnerable driver blocklist

The Windows kernel is the most privileged software and is therefore a compelling target for malware authors. Since Windows has strict requirements for code running in the kernel, cybercriminals commonly exploit vulnerabilities in kernel drivers to get access. Microsoft works with ecosystem partners to constantly identify and respond to potentially vulnerable kernel drivers. Prior to the Windows 11 2022 Update, Windows enforced a block policy when hypervisor-protected code integrity (HVCI) was enabled to prevent vulnerable versions of drivers from running. Beginning with the Windows 11 2022 Update, the block policy is now on by default for all new Windows PCs, and users can opt in to enforce the policy from the Windows Security app.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [Microsoft recommended driver block rules](/windows/security/threat-protection/windows-defender-application-control/microsoft-recommended-driver-block-rules)

## Trusted signing

Trsuted Signing is a Microsoft fully managed, end-to-end signing solution that simplifies the signing process and empowers third-party developers to easily build and distribute applications.

[!INCLUDE [learn-more](includes/learn-more.md)]

- [What is Trusted Signing](/azure/trusted-signing/overview)

<!--links-->

[LINK-1]: /windows/apps/develop/smart-app-control/overview
[LINK-2]: /windows/security/application-security/application-control/windows-defender-application-control/wdac
[LINK-3]: /windows/security/application-security/application-control/app-control-for-business/design/configure-authorized-apps-deployed-with-a-managed-installer