---
title: Lync Server 2013：規劃通話駐留災害復原
TOCTitle: 規劃通話駐留災害復原
ms:assetid: f7cf3958-177b-4340-a864-35a6f44d6d88
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205395(v=OCS.15)
ms:contentKeyID: 49292854
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中規劃通話駐留災害復原

 

_**上次修改主題的時間：** 2012-10-30_

本節描述準備讓 通話駐留應用程式 進行災難復原的方式，以及某些災難復原程序的考量。

## 準備讓 通話駐留 進行災難復原

準備或實際進行災難復原程序時，請記住下列事項。

  - 進行容量規劃時請規劃災難復原。在災難復原容量中，每個配對集區的集區均應可處理兩個集區中 通話駐留 服務的工作量。如需 通話駐留 容量規劃的詳細資訊，請參閱 [Lync Server 2013 中通話駐留的容量規劃](lync-server-2013-capacity-planning-for-call-park.md)。

  - 難復原期間，屬於部分容錯移轉程序而重新導向至備份集區的使用者，會使用在備份集區執行的「通話駐留」服務；因此，災難復原期間若要支援 通話駐留，必須在兩個主要集區與備份集區中部署與啟用 通話駐留應用程式。

  - 每個集區的軌道數必須是有效範圍，以供隸屬於該集區的使用者駐留通話。

  - 永遠記得另外備份任何上傳的 通話駐留 自訂保留音樂。 Lync Server 2013 災難復原程序中，並不會備份這些檔案，且如果上傳至集區的檔案毀壞、受損或遭到抹除，就會遺失。

## 通話駐留 災難復原考量

您可定義僅有一組 通話駐留應用程式 組態設定，每個集區一個自訂保留音樂音訊檔案。這些設定包含逾時臨界值、保留音樂、接聽通話次數上限以及逾時 URI。若要檢視這些組態設定，請執行 **Get-CsCpsConfiguration** Cmdlet。如需 **Get-CsCpsConfiguration** Cmdlet 的詳細資訊，請參閱 [Get-CsCpsConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsCpsConfiguration)。

災難復原期間， 通話駐留 會使用備份集區中的 通話駐留應用程式，因此不會備份主集區中的設定值。如果主集區無法復原，且您要部署新集區來取代主集區，則主集區的設定值會遺失，您也必須設定 通話駐留 設定值以及任何新集區中的自訂保留音樂音訊檔案。

如果您以不同的完整網域名稱 (FQDN) 部署新集區，以取代主集區，您必須重新指派與主集區至新集區 FQDN 相關聯的所有 通話駐留 軌道範圍。若要將軌道範圍重新指派新集區，可使用 Lync Server 控制台 或 **Set-CsCallParkOrbit** Cmdlet。如需 **Set-CsCallParkOrbit** Cmdlet 的詳細資訊，請參閱 [Set-CsCallParkOrbit](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCallParkOrbit)。

