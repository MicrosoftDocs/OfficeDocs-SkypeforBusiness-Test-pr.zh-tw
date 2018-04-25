---
title: Lync Server 2013：回應群組的技術需求
TOCTitle: 回應群組的技術需求
ms:assetid: 477488bd-124f-437b-9327-732a0d7271ca
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204863(v=OCS.15)
ms:contentKeyID: 49290791
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中回應群組的技術需求

 

_**上次修改主題的時間：** 2015-03-09_

本節描述下列 回應群組應用程式 的技術需求：

  - 硬體需求

  - 軟體需求

  - 連接埠需求

  - 音訊檔需求

  - 回應群組設定工具需求

## 硬體需求

回應群組應用程式 與 前端伺服器 的硬體需求相同。 如需硬體需求的詳細資訊，請參閱支援文件中的 [Lync Server 2013 的伺服器硬體平台](lync-server-2013-server-hardware-platforms.md)。

## 軟體需求

回應群組應用程式 與 前端伺服器 的作業系統需求相同。 如需軟體需求的詳細資訊，請參閱支援文件中的 [Lync Server 2013 中的伺服器及工具作業系統支援](lync-server-2013-server-and-tools-operating-system-support.md)。

如果 回應群組音樂和宣告使用 Windows Media Audio (.wma) 檔案，則在所有執行 回應群組應用程式 的 前端伺服器或 Standard Editions Server 中，執行 Windows Server 2008 R2 的伺服器必須安裝 Windows Media Format Runtime，而執行 Windows Server 2012 或 Windows Server 2012 R2 的伺服器必須安裝 Microsoft Media Foundation。對於 Windows Server 2008 R2，Windows Media Format Runtime 會安裝為 Windows Desktop Experience 的一部分。

如需有關音訊需求的詳細資訊，請參閱本節稍後的＜音訊檔案需求＞。

## 連接埠需求

回應群組應用程式使用下列連接埠：

  - **連接埠 5071**   用於 SIP 偵聽要求

  - **連接埠 8404**   用於伺服器間的通訊
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此連接埠用於配對服務，且在多部 前端伺服器 的集區中部署 回應群組應用程式時，為必要連接埠。</td>
    </tr>
    </tbody>
    </table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>這些連接埠是您可以使用 <strong>Set-CsApplicationServer</strong> Cmdlet 變更的預設設定。如需有關此 Cmdlet 的詳細資訊，請參閱＜ Lync Server 管理命令介面＞文件。</td>
</tr>
</tbody>
</table>


## 音訊檔需求

回應群組應用程式支援 Wave (.wav) 檔案格式和 Windows Media Audio (.wma) 檔案格式，用於回應群組訊息、等候音樂或互動語音回應 (IVR) 問題。

Windows Media 音訊檔案格式必須將 Windows Media Format Runtime 安裝在執行 Windows Server 2008 R2 和 Windows Server 2008 的 前端伺服器上。如需詳細資訊，請參閱本節稍早的＜軟體需求＞。

## 支援的 Wave 檔案格式

所有 Wave 檔案必須符合下列需求：

  - 8 位元或 16 位元檔案

  - 線性脈衝代碼調變 (LPCM)，A-Law 或 mu-Law 格式

  - 單音或立體聲

  - 4MB 以下

為使 Wave 檔案有最佳表現，建議使用 16 kHz 單音的 16 位元 Wave 檔案。

## 支援的 Windows Media 音訊檔案格式

如果您使用 Windows Media 音訊檔案，請考慮使用低位元速率，並驗證系統承受負載時的效能。

您可以使用 Microsoft Expression Encoder 4 將檔案轉換成 Windows Media Audio 格式。如果要下載 Expression Encoder 4，請參閱 [http://go.microsoft.com/fwlink/?linkid=202843\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=202843%26clcid=0x404)。

## 回應群組設定工具需求

回應群組設定工具支援下表中所述之作業系統和網頁瀏覽器的組合。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>支援 32 位元或 64 位元版本的作業系統。只支援 32 位元版本的 Internet Explorer。</td>
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
<td><p>Windows Vista Service Pack (SP) 2</p></td>
<td><p>Internet Explorer 7</p>
<p>Internet Explorer 8 (原生模式)</p>
<p>Internet Explorer 9 (原生模式)</p></td>
</tr>
<tr class="even">
<td><p>Windows 7</p>
<p>Windows 7 Service Pack 1</p></td>
<td><p>Internet Explorer 8 (原生模式)</p>
<p>Internet Explorer 9 (原生模式)</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2008 Service Pack 2</p></td>
<td><p>Internet Explorer 7</p>
<p>Internet Explorer 8 (原生模式)</p>
<p>Internet Explorer 9 (原生模式)</p></td>
</tr>
<tr class="even">
<td><p></p>
<p></p>
<p></p>
<p>Windows Server 2008 R2</p>
<p>Windows Server 2008 R2 Service Pack 1</p></td>
<td><p>Internet Explorer 8 (原生模式)</p>
<p>Internet Explorer 9 (原生模式)</p></td>
</tr>
</tbody>
</table>


## 回應群組代理程式主控台

代理程式主控台支援下表中所述之作業系統和網頁瀏覽器的組合。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>支援 32 位元或 64 位元版本的作業系統。只支援 32 位元版本的 Internet Explorer。</td>
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
<td><p>Windows Vista Service Pack (SP) 2</p></td>
<td><p>Internet Explorer 7</p>
<p>Internet Explorer 8 (原生模式)</p>
<p>Internet Explorer 9 (原生模式)</p></td>
</tr>
<tr class="even">
<td><p>Windows 7</p>
<p>Windows 7 Service Pack 1</p></td>
<td><p>Internet Explorer 8 (原生模式)</p>
<p>Internet Explorer 9 (原生模式)</p>
<p>Firefox 10.0</p>
<p>Chrome 18.0</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2008 Service Pack 2</p></td>
<td><p>Internet Explorer 7</p>
<p>Internet Explorer 8 (原生模式)</p>
<p>Internet Explorer 9 (原生模式)</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2008 R2</p>
<p>Windows Server 2008 R2 Service Pack 1</p></td>
<td><p>Internet Explorer 8 (原生模式)</p>
<p>Internet Explorer 9 (原生模式)</p>
<p>Firefox 10.0</p>
<p>Chrome 18.0</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td></td>
</tr>
</tbody>
</table>

