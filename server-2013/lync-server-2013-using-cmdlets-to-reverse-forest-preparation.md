---
title: Lync Server 2013：使用 Cmdlet 進行反向樹系準備
TOCTitle: 使用 Cmdlet 進行反向樹系準備
ms:assetid: f48c7eb3-ccb0-48e6-ac79-ab7c7062b9d3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413024(v=OCS.15)
ms:contentKeyID: 49292816
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用 Cmdlet 進行 Lync Server 2013 的反向樹系準備

 

_**上次修改主題的時間：** 2013-06-19_

使用 **Disable-CsAdForest** Cmdlet 反向樹系準備步驟。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ205186.Caution(OCS.15).gif" title="Caution" alt="Caution" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您在已部署舊版 Lync Server 的環境中執行 <strong>Disable-CsAdForest</strong> Cmdlet，則也會刪除舊版的全域設定。</td>
</tr>
</tbody>
</table>


## 若要使用 Cmdlet 反向樹系準備

1.  登入已加入樹系根網域中 Domain Admins 群組成員網域的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  執行：
    
        Disable-CsAdForest [-Force] [-GroupDomain <FQDN of the domain in which universal groups were created>]
    
    例如：
    
        Disable-CsAdForest -Force -GroupDomain contoso.net
    
    Force 參數會指定是否強制執行工作。如果此參數不存在，則只要樹系中有一個網域仍在進行 Lync Server 2013 的準備工作，命令就不會執行。如果指定了 Force 參數，則無論樹系中其他網域的狀態為何，動作都會繼續。
    
    如果您未指定 GroupDomain 參數，則預設值會是本機網域。

## 請參閱

#### 工作

[針對 Lync Server 2013 執行樹系準備](lync-server-2013-running-forest-preparation.md)  

#### 其他資源

[為 Lync Server 2013 準備樹系](lync-server-2013-preparing-the-forest.md)

