---
title: Lync Server 2013：通話駐留的技術需求
TOCTitle: 通話駐留的技術需求
ms:assetid: 38bcf302-2b72-4492-9266-f6dc31b566e1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204818(v=OCS.15)
ms:contentKeyID: 49290610
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中通話駐留的技術需求

 

_**上次修改主題的時間：** 2013-11-07_

本節針對 通話駐留說明下列技術需求：

  - 硬體需求

  - 軟體需求

  - 連接埠需求

  - 音訊檔需求

## 硬體需求

通話駐留應用程式 與 前端伺服器 的硬體需求相同。 如需硬體需求的詳細資訊，請參閱支援文件中的 [Lync Server 2013 的伺服器硬體平台](lync-server-2013-server-hardware-platforms.md)。

## 軟體需求

通話駐留應用程式 與 前端伺服器 的作業系統需求相同。 如需軟體需求的詳細資訊，請參閱支援文件中的 [Lync Server 2013 中的伺服器及工具作業系統支援](lync-server-2013-server-and-tools-operating-system-support.md)。

所有已部署 通話駐留應用程式的 前端伺服器及 Standard Edition Server 皆必須安裝 Windows Media Format Runtime (針對執行 Windows Server 2008 R2 的伺服器)，或是 Microsoft 媒體基礎 (針對執行 Windows Server 2012 或 Windows Server 2012 R2 的伺服器)。對於 Windows Server 2008 R2，Windows Media Format Runtime 會安裝為 Windows 桌面體驗的一部分。 通話駐留 播放等候音樂所用的 Windows Media 音訊 (.wma) 檔案，需要有 Windows Media Format Runtime 或 Microsoft 媒體基礎。

## 連接埠需求

通話駐留應用程式 使用下列連接埠：

  - **連接埠 5075**   用於 SIP 聆聽要求。

> [!NOTE]  
> 此連接埠為預設設定，可使用 <strong>Set-CsApplicationServer</strong> Cmdlet 予以變更。如需此 Cmdlet 的詳細資訊，請參閱＜ Lync Server 管理命令介面＞文件。



## 音訊檔需求

通話駐留應用程式僅支援 Windows Media 音訊 (.wma) 檔案作為等候音樂。您可以使用 Microsoft Expression Encoder 4 自訂檔案作為等候音樂。如要下載 Expression Encoder 4，請參閱 "Expression Encoder 4" (網址為 [http://go.microsoft.com/fwlink/p/?linkId=202843](http://go.microsoft.com/fwlink/p/?linkid=202843))。使用此工具可將檔案轉換成 .wma 格式。 通話駐留等候音樂檔案的建議格式為 Media Audio 9、44 kHz、16 位元、單聲道、CBR、32 kbps。

> [!NOTE]  
> 轉換後的檔案只能以 16 kHz 音頻在電話中播放，即使檔案是以 44 kHz 音頻錄製也一樣。


