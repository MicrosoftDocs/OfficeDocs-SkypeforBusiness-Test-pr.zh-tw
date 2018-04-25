---
title: Lync Server 2013：授與權限
TOCTitle: 授與權限
ms:assetid: d1c9ea66-bd07-480e-99a0-011108f97e42
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398901(v=OCS.15)
ms:contentKeyID: 49292395
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的授與權限

 

_**上次修改主題的時間：** 2012-10-15_

委派設定與管理已在 Microsoft Lync Server 2010 中變更。針對設定部分，您可以將權限授與特定 Active Directory 組織單位 (OU) 的 RTCUniversalServerAdmins 萬用群組，讓該 OU 中的 RTCUniversalServerAdmins 群組成員可在指定的網域中安裝 Lync Server 2013。當您將權限授與 OU 時，會授與下列權限：

  - 讀取

  - 寫入

  - ReadSPN

  - WriteSPN

針對管理部分，您可以將權限新增至指定的 OU，讓樹系準備所建立的 RTC 萬用群組成員即可存取 OU，而不需要是 Domain Admins 群組的成員。新增至指定 OU 的權限與 **Enable-CsAdDomain** Cmdlet 新增至電腦和使用者 OU 容器的權限相同。

## 本節內容

  - [在 Lync Server 2013 中授與設定權限](lync-server-2013-granting-setup-permissions.md)

  - [在 Lync Server 2013 中授與組織單位權限](lync-server-2013-granting-organizational-unit-permissions.md)

