---
title: 設定圖庫檢視
TOCTitle: 設定圖庫檢視
ms:assetid: 4a609178-47d8-4682-ac8d-29f882801924
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204871(v=OCS.15)
ms:contentKeyID: 49290830
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定圖庫檢視

 

_**上次修改主題的時間：** 2012-10-30_

在 Lync Server 2013 中，您在會議原則中設定「圖庫檢視」視訊會議。「圖庫檢視」預設為開啟狀態。如果您不想允許「圖庫檢視」，或只想針對部分使用者允許「圖庫檢視」，必須在會議原則中關閉此功能。

當會議參與者的視訊無法使用時，如果您部署高解析度相片 (Lync Server 2013 中的新功能)，可以增強使用者的「圖庫檢視」體驗。高解析度相片針對儲存在 Active Directory 網域服務 中解析度較小且有限的連絡人相片提供替代方案。由於高解析度相片儲存在使用者的 Exchange 2013 信箱中，因此您必須整合 Lync Server 2013 和 Exchange 2013。如需詳細資訊，請參閱 NextHop 部落格文章＜整合 Exchange 2013 與 Lync Server 2013＞，網址為 [http://go.microsoft.com/fwlink/?linkid=260987\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=260987%26clcid=0x404)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>每個部落格的內容及其 URL 如有任何變更，恕不另行通知。</td>
</tr>
</tbody>
</table>


您可以使用 Lync Server 2013 控制台或使用下列其中一個 Cmdlet 來檢視或修改「圖庫檢視」參數：

  - **Get-CsConferencingPolicy**

  - **Set-CsConferencingPolicy**

  - **New-CsConferencingPolicy**

請使用下列會議原則設定來設定「圖庫檢視」：

  - **AllowMultiview**   此參數會控制是否允許使用者召集「圖庫檢視」視訊會議。此參數適用於排程會議及使用者建立的臨時會議。
    
    範例：
    
      - 此參數對隸屬於 Lync Server 2013 集區的使用者 A 設定為 True。由使用者 A 召集的會議可讓使用者加入及接收多個視訊資料流。
    
      - 此參數對隸屬於 Lync Server 2013 集區的使用者 B 設定為 False。由使用者 B 召集的會議有與 Lync Server 2010 提供的視訊會議體驗類似的單一視訊流。
    
    此參數決定誰可以召集允許多個視訊資料流的會議。允許多個視訊資料流的會議的參與者是否可以接收多個視訊資料流，要視他們的個人權限而定 (請參閱 EnableMultiviewJoin 參數描述)。

  - **EnableMultiviewJoin**   此參數控制會議參與者是否在允許「圖庫檢視」視訊體驗的會議中接收該經驗。此參數控制使用者在所有參與的會議中的體驗。
    
    範例：
    
      - 此參數對使用者 C 設定為 True。使用者 C 在參與由使用者 A 召集或啟動的會議時，可以接收多個視訊資料流。使用者 C 在參與由使用者 B 召集或啟動的會議時，會接收與 Lync Server 2010 提供的視訊會議體驗類似的單一視訊資料流。
    
      - 此參數對使用者 D 設定為 False。使用者 D 在參與由使用者 A 或使用者 B 召開的會議時，會接收與 Lync Server 2010 提供的視訊會議經驗類似的單一視訊資料流。

下列程序是使用 Lync Server 管理命令介面來啟用「圖庫檢視」視訊會議的範例。

## 修改「圖庫檢視」視訊會議的會議原則

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  在命令列上執行下列 Cmdlet 以編輯會議原則：
    
        Set-CsConferencingPolicy -Identity Pool01ConferencingPolicy -AllowMultiview $true -EnableMultiviewJoin $true

