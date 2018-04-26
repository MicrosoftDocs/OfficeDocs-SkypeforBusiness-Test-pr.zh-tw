---
title: Lync Server 2013：Active Directory 網域服務準備工作概觀
TOCTitle: Active Directory 網域服務準備工作概觀
ms:assetid: cdd2a652-6a0d-4728-9950-3fcaa7a80066
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398869(v=OCS.15)
ms:contentKeyID: 49292349
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Active Directory 網域服務準備工作概觀

 

_**上次修改主題的時間：** 2015-03-09_

若要為您的 Lync Server 2013 部署準備 Active Directory 網域服務，必須依照特定順序執行三個步驟。

下表描述為 Lync Server 準備 AD DS 所需的步驟。

### Active Directory 準備步驟

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>步驟</th>
<th>說明</th>
<th>執行位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1.</p></td>
<td><p><a href="lync-server-2013-preparing-the-active-directory-schema.md">在 Lync Server 2013 中準備 Active Directory 結構描述</a></p></td>
<td><p>加入 Lync Server 所使用的新類別與屬性，藉以擴充 Active Directory 架構。</p>
<p>為部署中即將部署 Lync Server 的每個樹系執行一次。</p></td>
<td><p>針對每個樹系之根網域中即將部署 Lync Server 的架構主機。</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您有架構主機的權限，就不需要在根網域中執行此步驟。但是，您必須是根網域中的 Schema Admins 群組成員，以及架構主機上的 Enterprise Admins 群組成員。在資源樹系拓撲中，只會在資源樹系中執行此步驟，不會在任何使用者樹系中執行。在中央樹系拓撲中，只會在中央樹系中執行此步驟，不會在任何使用者樹系中執行。</td>
</tr>
</tbody>
</table>

</div></td>
</tr>
<tr class="even">
<td><p>2.</p></td>
<td><p><a href="lync-server-2013-preparing-the-forest.md">為 Lync Server 2013 準備樹系</a></p></td>
<td><p>建立 Lync Server 所使用的全域設定和萬用群組。</p>
<p>為部署中即將部署 Lync Server 的每個樹系執行一次。</p></td>
<td><p>在即將部署 Lync Server 之每個樹系的根網域中。您必須是 Enterprise Admins 群組的成員，才能夠執行這個步驟。</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在資源樹系拓撲中，只會在資源樹系中執行此步驟，不會在任何使用者樹系中執行。在中央樹系拓撲中，只會在中央樹系中執行此步驟，不會在任何使用者樹系中執行。</td>
</tr>
</tbody>
</table>

</div></td>
</tr>
<tr class="odd">
<td><p>3.</p></td>
<td><p><a href="lync-server-2013-preparing-domains.md">針對 Lync Server 2013 準備網域</a></p></td>
<td><p>新增萬用群組成員所使用之物件的權限。</p>
<p>為每個使用者網域或伺服器網域執行一次。</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您要從 Lync Server 2010 移轉至 Lync Server 2013，「部署精靈」可能會指出網域準備已經完成。您不需要再次執行網域準備。權限並未從 Lync Server 2010 變更為 Lync Server 2013。</td>
</tr>
</tbody>
</table>

</div></td>
<td><p>在即將部署 Lync Server 之每個網域的成員伺服器上。您必須是 Domain Admins 群組的成員，才能夠執行這個步驟。</p></td>
</tr>
</tbody>
</table>


就像 Lync Server 2010， Lync Server 2013 將大部分的組態資訊儲存在 中央管理存放區中，而不像 Office Communications Server 2007 R2 是儲存在 AD DS 中。不過，下列資訊仍會儲存在 AD DS 中：

  - **架構延伸 ：**
    
      - 使用者物件延伸
    
      - Office Communications Server 2007 R2 類別的延伸以維持回溯相容性

<!-- end list -->

  - **資料** (儲存在 Lync Server 延伸架構和現有的架構類別中)：
    
      - 使用者 SIP 統一資源識別項 (URI) 及其他使用者設定
    
      - 回應群組與會議服務員等應用程式的連絡人物件
    
      - 中央管理存放區的指標
    
      - Kerberos 驗證帳戶 (選用的電腦物件)

在 Lync Server 2013 中，您會藉由將安裝程式權限授與 RTCUniversalServerAdmins 萬用群組，以便該群組的成員可以在本機伺服器上安裝及啟動 Lync Server 2013 (在伺服器已新增至拓撲，並已發佈及啟用之後) 的方式來委派安裝和管理。受委派的使用者必須是要安裝及啟動 Lync Server 2013 之電腦的本機系統管理員，但是不需要是 Domain Admins 群組的成員。您也可以針對指定之組織單元 (OU) 中的物件授與權限，以便在樹系準備期間建立的萬用群組成員可以存取這些物件，而不需要是 Domain Admins 群組的成員。

針對 Lync Server 2013 的新部署，全域設定必須儲存在設定容器中。如果您的組織是要從舊版升級，且系統容器中仍有全域設定，則仍然支援系統容器。

## 請參閱

#### 概念

[在 Lync Server 2013 中準備 Active Directory 結構描述](lync-server-2013-preparing-the-active-directory-schema.md)  
[Lync Server 2013 使用的 Active Directory 結構描述擴充功能、類別及屬性](lync-server-2013-active-directory-schema-extensions-classes-and-attributes-used-by-lync-server.md)  

#### 其他資源

[為 Lync Server 2013 準備樹系](lync-server-2013-preparing-the-forest.md)  
[針對 Lync Server 2013 準備網域](lync-server-2013-preparing-domains.md)

