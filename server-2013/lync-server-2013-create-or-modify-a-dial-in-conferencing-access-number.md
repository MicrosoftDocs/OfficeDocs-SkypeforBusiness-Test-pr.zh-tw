---
title: Lync Server 2013：建立或修改電話撥入式會議存取號碼
TOCTitle: 建立或修改電話撥入式會議存取號碼
ms:assetid: 06f55c28-57f8-4d4e-8313-9740846796d9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398126(v=OCS.15)
ms:contentKeyID: 49289978
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立或修改電話撥入式會議存取號碼

 

_**上次修改主題的時間：** 2012-09-17_

如果您想建立或修改電話撥入式會議存取號碼，請遵循下列步驟。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須先在與新的撥入存取號碼關聯的撥號對應表中設定電話撥入式會議區域，才可建立新的撥入存取號碼。多個撥號對應表可使用相同的區域。</td>
</tr>
</tbody>
</table>


## 若要建立或修改撥入存取號碼

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[會議\]** ，然後按一下 **\[撥入存取號碼\]** 。

4.  在 **\[撥入存取號碼\]** 頁面中，執行下列其中一項：
    
      - 按一下 **\[新增\]** 以開啟 **\[新增撥入存取號碼\]** 。
    
      - 按一下清單中的其中一個撥入存取號碼，按一下 **\[編輯\]** ，然後按一下 **\[顯示詳細資料\]** 。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>使用搜尋欄位來搜尋撥入存取號碼清單中可能無法產生預期結果的欄內容。請依照您想要的欄排序此清單，找出您想檢視或變更的撥入存取號碼。</td>
        </tr>
        </tbody>
        </table>


5.  在 **\[顯示號碼\]** 中，輸入公用交換電話網路 (PSTN) 電話使用者可撥入以加入會議的電話號碼。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此號碼會顯示在會議邀請中和 [電話撥入式會議設定] 網頁上。</td>
    </tr>
    </tbody>
    </table>


6.  在 **\[顯示名稱\]** 中，輸入撥入存取號碼的描述。這是與 Lync 搜尋結果中的撥入存取號碼關聯的名稱。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此名稱會在使用者撥打存取號碼時顯示於用戶端。</td>
    </tr>
    </tbody>
    </table>


7.  在 **\[線路 URI\]** 中，以 TEL URI 格式輸入撥入存取號碼的 E.164 號碼，號碼前面要加上 + 符號且不可包含空白。例如，tel:+14255550200。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>其他電話撥入式會議存取號碼將無法重複使用相同的線路 URI。</td>
    </tr>
    </tbody>
    </table>


8.  在 **\[SIP URI\]** 中，執行下列作業：
    
      - 在文字方塊中，輸入此電話撥入式會議存取號的唯一 SIP URI。這個 SIP URI 會顯示於各種位置上，包括但不限於來電通知訊息和舊版的 Communicator 用戶端。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>其他電話撥入式會議存取號碼將無法重複使用相同的 SIP URI。建立存取號碼之後，便無法修改 SIP URI。變更 SIP URI 的唯一方法就是刪除並重新建立存取號碼。</td>
        </tr>
        </tbody>
        </table>
    
      - 在下拉式清單方塊中，按一下支援此撥入存取號碼的 會議服務員應用程式網域。

9.  在 **\[集區\]** 中，按一下正在執行可支援此撥入存取號碼之會議服務員執行個體的集區。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您想要在建立存取號碼後變更集區，您必須使用 <strong>Move-CsApplicationEndpoint</strong> Cmdlet 來刪除並重新建立存取號碼。</td>
    </tr>
    </tbody>
    </table>


10. 在 **\[主要語言\]** 中，按一下針對此撥入存取號碼顯示提示時所用的語言。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>主要語言就是會議服務員用於接聽電話的語言。支援的語言會沿著每個存取電話號碼顯示在 [電話撥入式會議設定] 網頁上。</td>
    </tr>
    </tbody>
    </table>


11. (選用) 在 **\[次要語言 (最多四種)\]** 中，按一下 **\[新增\]** ，選取您要支援此撥入存取號碼來電者的一種或多種其他語言，然後按一下 **\[確定\]** 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您最多可以為每一個撥入存取號碼選擇四種次要語言。使用者在撥入會議時，可以在輸入會議 ID 之前先選取次要語言。</td>
    </tr>
    </tbody>
    </table>


12. 若要新增撥入存取號碼的地區，請在 **\[關聯的地區\]** 下，按一下 **\[新增\]** ，再按一下與此撥入存取號碼之撥號對應表關聯的一或多個地區，然後按一下 **\[確定\]** 。

13. 若要刪除撥入存取號碼的地區，請在 **\[關聯的地區\]** 下，按一下您要刪除的地區，然後按一下 **\[移除\]** 。

14. 按一下 \[認可\] 。

