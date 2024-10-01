---
title: Application isolation
description: Windows 11 security book - Application isolation.
ms.topic: overview
ms.date: 09/06/2024
---

# Application isolation

:::image type="content" source="images/application-security.png" alt-text="Diagram containing a list of application security features." lightbox="images/application-security.png" border="false":::

## Win32 app isolation

Win32 app isolation is a new security feature designed to be the default isolation standard on Windows clients. It's built on [AppContainer](/windows/win32/secauthz/implementing-an-appcontainer), and offers several added security features to help the Windows platform defend against attacks that leverage vulnerabilities in applications or third-party libraries. To isolate their apps, developers can update their applications using Visual Studio.

Win32 app isolation follows a two-step process. In the first step, the Win32 application is launched as a low-integrity process using AppContainer, which is recognized as a security boundary by Microsoft. Consequently, the process is limited to a specific set of Windows APIs by default and is unable to inject code into any process operating at a higher integrity level.

In the second step, least privilege is enforced by granting authorized access to Windows securable objects. This access is determined by capabilities that are added to the application manifest through MSIX packaging. Securable objects in this context refer to Windows resources whose access is safeguarded by capabilities. These capabilities enable the implantation of a [Discretionary Access Control List](/windows/win32/secauthz/access-control-lists) on Windows.

To help ensure that isolated applications run smoothly, developers must define the access requirements for the application via access capability declarations in the application package manifest. The Application Capability Profiler (ACP) simplifies the entire process by allowing the application to run in "learn mode" with low privileges. Instead of denying access if the capability is not present, ACP allows access and logs additional capabilities required for access if the application were to run isolated. For more information on ACP, please refer to the [GitHub documentation page](https://github.com/microsoft/win32-app-isolation/blob/main/docs/profiler/application-capability-profiler.md#stack-tracing---acp-stacktracewpaprofile).

To create a smooth user experience that aligns with nonisolated, native Win32 applications, two key factors should be taken into consideration:

- Approaches for accessing data and privacy information
- Integrating Win32 apps for compatibility with other Windows interfaces

The first factor relates to implementing methods to manage access to files and privacy information within and outside the isolation boundary ([AppContainer](/windows/win32/secauthz/implementing-an-appcontainer)). The second factor involves integrating Win32 apps with other Windows interfaces in a way that helps enable seamless functionality without causing perplexing user consent prompts.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Win32 app isolation](https://github.com/microsoft/win32-app-isolation)
- [Learn how to adop Win32 app isolation with Visual Studio](https://github.com/microsoft/win32-app-isolation/blob/main/docs/packaging/packaging-with-visual-studio.md)
- [Sandboxing Python with Win32 app isolation](https://blogs.windows.com/windowsdeveloper/2024/03/06/sandboxing-python-with-win32-app-isolation/)

## App containers

In addition to Windows Sandbox for Win32 apps, Universal Windows Platform (UWP) applications run in Windows containers known as *app containers*. App containers act as process and resource isolation boundaries, but unlike Docker containers, these are special containers designed to run Windows applications.

Processes that run in app containers operate at a low integrity level, meaning they have limited access to resources they don't own. Because the default integrity level of most resources is medium integrity level, the UWP app can access only a subset of the file system, registry, and other resources. The app container also enforces restrictions on network connectivity. For example, access to a local host isn't allowed. As a result, malware or infected apps have limited footprint for escape.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Windows and app container](/windows/apps/windows-app-sdk/migrate-to-windows-app-sdk/feature-mapping-table?source=recommendations)

## Windows Sandbox

Windows Sandbox provides a lightweight desktop environment to safely run untrusted Win32 applications in isolation using the same hardware-based Hyper-V virtualization technology without fear of lasting impact to the PC. Any untrusted Win32 app installed in Windows Sandbox stays only in the sandbox and can't affect the host.

Once Windows Sandbox is closed, nothing persists on the device. All the software with all its files and state are permanently deleted after the untrusted Win32 application is closed.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**

- [Windows Sandbox](/windows/security/threat-protection/windows-sandbox/windows-sandbox-overview)
- [Windows Sandbox is a new lightweight desktop environment tailored for safely
running applications in isolation](https://techcommunity.microsoft.com/t5/windows-os-platform-blog/windows-sandbox/ba-p/301849)

## Windows Subsystem for Linux (WSL)
Windows Subsystem for Linux (WSL) is a feature of Windows that allows you to run a Linux environment on your Windows machine, without the need for a separate virtual machine or dual booting. WSL is designed to provide a seamless and productive experience for developers who want to use both Windows and Linux at the same time. In Ge, we added 3 networking security features and Intune/MDM integration in WSL on Windows 11 (SV2 and Ge) for Enterprises:
- **Hyper-V Firewall**: This new firewall setting is a network firewall solution that enables filtering of inbound and outbound traffic to/from WSL containers hosted by Windows.

- **DNS Tunneling**: This new networking setting improves compatibility in different networking environments and makes use of virtualization features to obtain DNS information rather than a networking packet.

- **Auto proxy**: This new networking setting enforces WSL to use Windows' HTTP proxy information. Turn on when using a proxy on Windows, as it will make that proxy automatically apply to WSL distributions.

- **Intune/MDM setting in WSL**: Microsoft Defender for Endpoint (MDE) now integrates with WSL, providing the ability to monitor what's running inside of your WSL distros and report them to your online MDE dashboards.

:::image type="icon" source="images/learn-more.svg" border="false"::: **Learn more:**
- [Hyper-V Firewall](/windows/security/operating-system-security/network-security/windows-firewall/hyper-v-firewall)
- [DNS Tunneling](/windows/wsl/networking#dns-tunneling)
- [Auto proxy](/windows/wsl/networking#auto-proxy)
- [Intune/MDM setting in WSL](/windows/wsl/intune)




