---
title: Lync Server 2013：宣告應用程式的部署程序
TOCTitle: 宣告應用程式的部署程序
ms:assetid: 72c66249-c4ce-48ce-b1b9-90ebf77d7805
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398545(v=OCS.15)
ms:contentKeyID: 49291299
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中宣告應用程式的部署程序

 

_**上次修改主題的時間：** 2015-03-09_

本節將概要說明部署 宣告應用程式的所需步驟。您必須先部署 企業語音，之後才能設定宣告。 宣告應用程式需要的元件在您部署 企業語音時就會加以安裝和啟用。

### 宣告部署程序

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>階段</th>
<th>步驟</th>
<th>角色</th>
<th>部署文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>設定宣告設定</p></td>
<td><ul>
<li><p>錄製及上傳音訊檔案，或是使用文字轉語音 (TTS)，以建立宣告。</p></li>
<li><p>設定未指派號碼表格中的未指派號碼範圍，並建立它們與適當宣告的關聯。</p></li>
</ul></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsVoiceAdministrator</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p>
<p>CsViewOnlyAdministrator</p></td>
<td><p><a href="lync-server-2013-create-an-announcement.md">在 Lync Server 2013 中建立宣告</a></p>
<p><a href="lync-server-2013-configure-the-unassigned-number-table.md">在 Lync Server 2013 中設定未指派號碼表</a></p></td>
</tr>
<tr class="even">
<td><p>驗證宣告部署</p></td>
<td><p>透過接聽宣告以驗證設定如預期運作。</p></td>
<td><p>-</p></td>
<td><p><a href="lync-server-2013-optional-verify-announcement-deployment.md">(選用) 在 Lync Server 2013 中驗證宣告部署</a></p></td>
</tr>
</tbody>
</table>

