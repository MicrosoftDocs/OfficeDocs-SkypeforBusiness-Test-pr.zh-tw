---
title: 最佳做法分析程式概觀
TOCTitle: 最佳做法分析程式概觀
ms:assetid: c5fcaa05-eb1c-4092-90ad-177b127e795b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg591349(v=OCS.15)
ms:contentKeyID: 49292260
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 最佳做法分析程式概觀

 

_**上次修改主題的時間：** 2012-09-19_

您可以使用 Lync Server 2013 最佳做法分析程式找出並解決 Lync Server 2013 部署的問題。Lync Server 2013 最佳做法分析程式會從 Lync Server 2013 元件收集組態資訊。

只要有適當的網路連線，最佳做法分析程式就能檢查執行 Active Directory 網域服務、Exchange Server Unified Messaging (UM) 和 Lync Server 2013 的伺服器。您可以使用最佳做法分析程式執行下列動作：

  - 主動執行檢查，確認組態是根據建議的最佳做法進行設定。

  - 自動偵測必要的 Lync Server 2013 更新。

  - 產生問題清單，例如不是很理想的組態設定、不支援的選項、遺漏的更新或不建議的做法。

  - 協助您疑難排解並修正特定問題。

最佳做法分析程式提供下列功能：

  - 基本安裝先決條件。

  - 所報告問題的相關線上文件，包括疑難排解提示。

  - 您可儲存起來供日後檢閱的組態資訊。

  - 最先進的系統分析。

最佳做法分析程式使用一組 XML 組態檔來決定要從您 Lync Server 2013 環境收集的資訊。它除了會檢查 Active Directory 網域服務之外，還會檢查 Windows Server 作業系統登錄和 Windows Management Instrumentation (WMI) 中的設定等來源。

最佳做法分析程式會將針對 Lync Server 2013 部署的設定與組態而收集到的資料與一組預先定義的規則進行比較。

在將收集到的資料與預先定義的規則比較過後，工具會報告問題。最佳做法分析程式會針對所報告的每項問題，提供在所掃描 Lync Server 2013 環境中發現的組態以及建議的組態等資訊。最佳做法分析程式也會提供特定問題的詳細資訊連結。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync Server 2013 最佳做法分析程式只會從 Lync Server 2013 元件收集組態資訊。您可以使用舊版此工具來掃描舊版環境。如需詳細資訊，請參閱<a href="lync-server-2013-requirements-for-running-best-practices-analyzer.md">執行最佳做法分析程式的需求</a>。</td>
</tr>
</tbody>
</table>

