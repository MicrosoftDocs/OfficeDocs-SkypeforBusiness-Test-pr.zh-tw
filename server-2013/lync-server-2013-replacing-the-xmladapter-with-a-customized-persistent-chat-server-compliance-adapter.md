---
title: 在 Lync Server 2013 中以自訂常設聊天室伺服器規範配置器取代 XmlAdapter
TOCTitle: 在 Lync Server 2013 中以自訂常設聊天室伺服器規範配置器取代 XmlAdapter
ms:assetid: 2cb70db2-663f-40a6-abcf-89ea7d4a8b65
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ680106(v=OCS.15)
ms:contentKeyID: 49889997
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中以自訂常設聊天室伺服器規範配置器取代 XmlAdapter

 

_**上次修改主題的時間：** 2012-11-01_

您可以撰寫自訂配接器，而不是使用與 常設聊天室伺服器 一起安裝的 XmlAdapter。若要完成此工作，您必須提供包含公用類別 (實作了 **IComplianceAdapter** 介面) 的 .NET Framework 組件。您必須將此組件放在您 Persistent Chat Server 集區中每部伺服器的 常設聊天室伺服器 安裝資料夾內。所有符合此規範的伺服器皆可提供規範資料給您的配接器，但規範伺服器不會提供重複的規範資料給您配接器的多個執行個體。

## 實作 IComplianceAdapter 介面

此介面被定義在命名空間 `Microsoft.Rtc.Internal.Chat.Server.Compliance` 中的 Compliance.dll 組件內。此介面定義了您自訂介面卡必須實作的兩種方法。

    void SetConfig(AdapterConfig config)

首次載入介面卡時，常設聊天室規範伺服器會呼叫此方法。`AdapterConfig` 包含了與規範介面卡相關的常設聊天室規範組態。

    void Translate(ConversationCollection conversations)

一旦有要轉譯的新資料，常設聊天室規範伺服器就會定期呼叫此方法。其中的時間間隔與常設聊天室規範組態中設定的 `RunInterval` 一樣。

`ConversationCollection` 包含了上一次呼叫此方法時所收集的交談資訊。

