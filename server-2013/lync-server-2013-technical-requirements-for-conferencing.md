---
title: Lync Server 2013 會議的技術需求
TOCTitle: 會議的技術需求
ms:assetid: 3c0d89e1-53e6-46d7-bf8c-491260b292ea
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425889(v=OCS.15)
ms:contentKeyID: 49290656
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中會議的技術需求

 

_**上次修改主題的時間：** 2015-03-09_

對於 Lync Server 2013 而言，電話撥入式會議、A/V 會議、立即訊息 (IM) 會議和 Web 會議功能一律在 前端伺服器上執行。

本節將詳細說明這些伺服器的硬體和軟體需求，以及支援的組合。

電話撥入式會議是一項包含許多不同元件的功能。有些是電話撥入式會議專用的元件，而有些則是 企業語音元件。本節說明電話撥入式會議專用元件的需求。如需 中繼伺服器和公用交換電話網路 (PSTN) 閘道需求的詳細資訊，請參閱規劃文件中的＜ [Lync Server 2013 中的中繼伺服器元件](lync-server-2013-mediation-server-component.md)＞及＜ [Lync Server 2013 中之中繼伺服器的元件和拓撲](lync-server-2013-components-and-topologies-for-mediation-server.md)＞。

## 硬體需求

因為 Web 會議及 A/V 會議與 前端伺服器組合，伺服器硬體需求與 前端伺服器相同。如需硬體需求的詳細資訊，請參閱支援文件中的＜ [Lync Server 2013 的伺服器硬體平台](lync-server-2013-server-hardware-platforms.md)＞。下列電話撥入式會議所需元件的硬體需求也與 前端伺服器相同：

  - 應用程式服務

  - 會議服務員應用程式

  - 會議宣告應用程式

前端伺服器的硬體需求與 Lync Server 2013 中的多數伺服器角色相同，如下表所示。

## 軟體需求

因為 Web 會議及 A/V 會議與 前端伺服器組合，伺服器軟體需求與 前端伺服器相同。如需軟體需求的詳細資訊，請參閱支援文件中的＜ [Lync Server 2013 中的伺服器及工具作業系統支援](lync-server-2013-server-and-tools-operating-system-support.md)＞。

對於 Web 會議， Lync Server 2013 還需要 Office Web Apps 及 Office Web Apps Server (舊稱為 WAC Server) 來處理 PowerPoint 簡報。如需詳細資訊，請參閱＜ [設定 Office Web Apps Server 與 Lync Server 2013 的整合](lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md)＞。

對於電話撥入式會議， 應用程式服務、 會議服務員應用程式及 會議宣告應用程式的作業系統需求與 前端伺服器相同。如需軟體需求的詳細資訊，請參閱支援文件中的＜ [Lync Server 2013 中的伺服器及工具作業系統支援](lync-server-2013-server-and-tools-operating-system-support.md)＞。

會議服務員應用程式及 會議宣告應用程式需要 前端伺服器安裝有 Windows Media Format Runtime。您必須有 Windows Media Format Runtime 才能播放等候音樂、錄音名稱和提示所用的 Windows Media Audio (WMA) 檔案。除了 Windows Server 2012 和 Windows Server 2012 R2 之外，Windows Media Format Runtime 會在您執行安裝程式時，自動安裝為 Windows Desktop Experience的一部分，但可能需要重新啟動電腦。因此，在執行安裝程式前，建議安裝為 Windows Desktop Experience 的一部分 (Windows Desktop Experience 包括 Windows Media Format Runtime)。 Windows Server 2012 和 Windows Server 2012 R2 需要有 Microsoft Media Foundation。

## 電話撥入式會議的連接埠需求

下表描述電話撥入式會議所使用的連接埠。如果您使用負載平衡器，務必針對將在集區中執行的任何應用程式所使用的連接埠設定負載平衡器。

這些連接埠是您可以使用 **Set-CsApplicationServer** Cmdlet 變更的預設設定。如需有關此 Cmdlet 的詳細資訊，請參閱＜ Lync Server 管理命令介面＞文件。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>集區中同一個應用程式的所有執行個體都使用相同的 SIP 聆聽連接埠。</td>
</tr>
</tbody>
</table>


### 電話撥入式會議使用的連接埠

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>連接埠編號</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>5072</p></td>
<td><p>會議服務員應用程式用於 SIP 聆聽要求</p></td>
</tr>
<tr class="even">
<td><p>5073</p></td>
<td><p>會議宣告應用程式用於 SIP 聆聽要求</p></td>
</tr>
</tbody>
</table>


## 支援的電話撥入式會議用戶端

您可以使用下列用戶端，排程支援電話撥入式存取的內部部署會議：

  - Lync 2013 的線上會議增益集 (在您安裝 Lync 2013 或 Attendee 時自動安裝)

## 電話撥入式會議設定頁面需求

電話撥入式會議設定頁面支援下表中所述之作業系統和網頁瀏覽器的組合。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>支援 32 位元和 64 位元版本的作業系統。</td>
</tr>
</tbody>
</table>


### 支援的作業系統和網頁瀏覽器

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>作業系統</th>
<th>網頁瀏覽器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows 7</p></td>
<td><p>Internet Explorer 9</p>
<p>Internet Explorer 8</p>
<p>Firefox</p></td>
</tr>
<tr class="even">
<td> </td>
<td> </td>
</tr>
<tr class="odd">
<td> </td>
<td> </td>
</tr>
<tr class="even">
<td><p>Windows Server 2008 R2</p></td>
<td><p>Internet Explorer 9</p>
<p>Internet Explorer 8</p>
<p>Internet Explorer 7</p></td>
</tr>
<tr class="odd">
<td><p>Mac OS</p></td>
<td><p>Firefox</p>
<p>Safari</p></td>
</tr>
</tbody>
</table>


## 電話撥入式會議的音訊檔需求

Lync Server 2013 不支援自訂電話撥入式會議的語音提示和音樂。不過，如果您因為業務上的強烈需求而必須變更預設的音訊檔，請參閱 Microsoft 知識庫文件 961177，[如何在 Microsoft Office Communications Server 2007 R2 中自訂電話撥入式音訊會議的語音提示或音樂檔](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=961177)。

您也可以使用 [Microsoft Lync Server 會議服務員自訂語音提示](http://go.microsoft.com/fwlink/p/?linkid=396880) (英文)管理公用程式，讓系統管理員使用自訂的提示，取代來電者加入 Lync 會議時所使用的預設語音提示，從而提供不同的進入會議體驗。可在執行 Lync Server 2010 或 Lync Server 2013 Enterprise 或 Standard Edition 的伺服器上安裝自訂的語音提示。

會議服務員應用程式及 會議宣告應用程式對於等候音樂、錄音名稱和音訊提示檔有下列需求：

  - Windows Media Audio (WMA) 檔案格式

  - 16 位元單聲道

  - 48 kbps 2-pass CBR (常數位元速率)

  - 語音層級為 -24DB

## 電話撥入式會議的使用者需求

必須指派唯一的電話號碼或分機至電話撥入式會議使用者的帳戶。此需求可支援電話撥入式會議期間的驗證。企業使用者 (也就是組織內擁有 Active Directory 網域服務 認證和 Lync Server 帳戶的使用者) 可輸入其電話號碼 (或分機) 和個人識別碼 (PIN)，即可以驗證使用者的身分撥入會議。

