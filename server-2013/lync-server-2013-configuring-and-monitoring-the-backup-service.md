---
title: Lync Server 2013：設定和監控備份服務
TOCTitle: 設定和監控備份服務
ms:assetid: c608280e-a7d1-4ae0-a75c-da6b524752fa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205252(v=OCS.15)
ms:contentKeyID: 49292258
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定和監控備份服務

 

_**上次修改主題的時間：** 2012-11-01_

您可以使用下列 Lync Server 管理命令介面命令來設定和監控備份服務。

> [!NOTE]  
> 根據預設，RTCUniversalServerAdmins 群組是唯一有權執行 <strong>Get-CsBackupServiceStatus</strong> 的群組。若要使用此 Cmdlet，請以此群組的成員身分登入。或者，您也可以使用 <strong>Set-CsBackupServiceConfiguration</strong> Cmdlet，將此命令的存取權授與其他群組 (例如 CSAdministrator)。



## 查看備份服務組態

執行下列 Cmdlet：

    Get-CsBackupServiceConfiguration

SyncInterval 的預設值為 2 分鐘。

## 設定備份服務同步間隔

執行下列 Cmdlet：

    Set-CsBackupServiceConfiguration -SyncInterval interval

例如，下列命令會將間隔設定為 3 分鐘。

    Set-CsBackupServiceConfiguration -SyncInterval 00:03:00

> [!IMPORTANT]  
> 雖然可以使用此 Cmdlet 變更備份服務的預設同步間隔，但除非必要絕不建議您這麼做，因為同步間隔對備份服務的效能和復原點目標 (RPO) 有極大影響。



## 取得特定集區的備份服務狀態

執行下列 Cmdlet：

    Get-CsBackupServiceStatus -PoolFqdn <pool-FQDN>

> [!NOTE]  
> 備份服務同步狀態的定義是採集區 (P1) 至其備份集區 (P2) 的單一方向。P1 至 P2 的同步狀態可能與 P2 至 P1 的同步狀態不同。對於 P1 至 P2 的方向，如果在 P1 做出的變更全都在同步間隔內完整複寫至 P2，則備份服務處於「穩定」狀態。如果不再有需要從 P1 同步至 P2 的變更，則備份服務處於「最終」狀態。這兩種狀態都代表 Cmdlet 執行時當下的備份服務快照，並不表示之後傳回的狀態都會保持一樣。尤其是，Cmdlet 執行後 P1 必須未產生任何變更，「最終」狀態才會繼續保持。例如， <strong>Invoke-CsPoolfailover</strong> 的執行邏輯將 P1 置入唯讀模式，再將 P1 容錯移轉至 P2 時，就會如此。



## 取得特定集區的備份關係資訊

執行下列 Cmdlet：

    Get-CsPoolBackupRelationship -PoolFQDN <poolFQDN>

## 強制備份服務進行同步

執行下列 Cmdlet：

    Invoke-CsBackupServiceSync -PoolFqdn <poolFqdn> [-BackupModule  {All|PresenceFocus|DataConf|CMSMaster}]

