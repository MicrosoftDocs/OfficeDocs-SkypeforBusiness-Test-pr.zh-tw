---
title: 在 Lync Server 2013 中設定 SNMP 應用程式
TOCTitle: 在 Lync Server 2013 中設定 SNMP 應用程式
ms:assetid: c4b4a736-3b2e-45b9-a965-19d22161ad57
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412972(v=OCS.15)
ms:contentKeyID: 49292254
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定 SNMP 應用程式

 

_**上次修改主題的時間：** 2012-10-03_

Lync Server 2013 包含標準 Web 服務介面，可供您用來將位置資訊服務連接到會以連接埠和交換器資訊比對 MAC 位址的簡易網路管理通訊協定 (SNMP) 應用程式。

如果安裝了 SNMP 應用程式，而位置資訊服務在位置資料庫中找不到相符項目，則位置資訊服務會自動使用用戶端所提供的 MAC 位址來查詢該應用程式。然後，位置資訊服務會使用 SNMP 應用程式所傳回的連接埠和交換器資訊，再次查詢位置資料庫。

如需詳細資訊，請參閱 [Set-CsWebServiceConfiguration](set-cswebserviceconfiguration.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>MAC 位址不適用於執行 Windows 8 的電腦。</td>
</tr>
</tbody>
</table>


## 若要設定 SNMP 應用程式 URL

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行下列 Cmdlet 可設定 SNMP 應用程式的 URL。
    
        Set-CsWebServiceConfiguration -MACResolverUrl "<SNMP application url>"

