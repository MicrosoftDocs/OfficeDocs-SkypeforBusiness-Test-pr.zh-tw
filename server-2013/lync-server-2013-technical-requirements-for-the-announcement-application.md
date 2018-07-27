---
title: Lync Server 2013：宣告應用程式的技術需求
TOCTitle: 宣告應用程式的技術需求
ms:assetid: fbd8c204-3765-4b22-a0c9-a781b5126366
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205413(v=OCS.15)
ms:contentKeyID: 49292907
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的宣告應用程式的技術需求

 

_**上次修改主題的時間：** 2013-11-07_

本節描述下列 宣告應用程式 的技術需求：

  - 硬體需求

  - 軟體需求

  - 連接埠需求

  - 音訊檔需求

## 硬體需求

宣告應用程式 與 前端伺服器 的硬體需求相同。 如需硬體需求的詳細資訊，請參閱支援文件中的 [Lync Server 2013 的伺服器硬體平台](lync-server-2013-server-hardware-platforms.md)。

## 軟體需求

宣告應用程式 與 前端伺服器 的作業系統需求相同。 如需軟體需求的詳細資訊，請參閱支援文件中的 [Lync Server 2013 中的伺服器及工具作業系統支援](lync-server-2013-server-and-tools-operating-system-support.md)。

所有執行 宣告應用程式 的 前端伺服器 或 Standard Edition 伺服器皆必須安裝 Windows Media Format Runtime (針對執行 Windows Server 2008 R2 的伺服器)，或是 Microsoft Media Foundation (針對執行 Windows Server 2012 或 Windows Server 2012 R2 的伺服器)。對於 Windows Server 2008 R2，Windows Media Format Runtime 為安裝為 Windows Desktop Experience 的一部分。 宣告應用程式 播放宣告或音樂所用的 Windows Media 音訊 (.wma) 檔案，需要有 Windows Media Format Runtime 或 Microsoft 媒體基礎。

## 連接埠需求

宣告應用程式 使用下列連接埠：

  - **連接埠 5071**   用於 SIP 偵聽要求

> [!NOTE]  
> 此連接埠是預設值，您可使用 <strong>Set-CsApplicationServer</strong> Cmdlet 變更。如需此 Cmdlet 的詳細資訊，請參閱 Lync Server 管理命令介面 文件。



## 音訊檔需求

宣告應用程式 支援 Wave (.wav) 檔案格式與 Windows Media audio (.wma) 檔案格式的音樂與宣告。 宣告應用程式 的音訊檔案需求與 回應群組應用程式 的相同。如需詳細資訊，請參閱 [Lync Server 2013 中回應群組的技術需求](lync-server-2013-technical-requirements-for-response-group.md)。

