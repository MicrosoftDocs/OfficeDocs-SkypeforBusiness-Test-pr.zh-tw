---
title: Lync Server 2013：每週工作
TOCTitle: 每週工作
ms:assetid: d564839b-b49d-4c5d-b67e-dc5abb0f6980
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn722432(v=OCS.15)
ms:contentKeyID: 62281953
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的每週工作

 

_**上次修改主題的時間：** 2015-08-17_

每週工作一般是關於收集和分析記錄和報告。

## 封存事件記錄

如果事件記錄未設定為視需要覆寫事件，則必須定期封存和刪除。此動作對安全性記錄尤其重要，在調查有企圖的安全性缺口時必須執行此動作。

您的組織將必須定義記錄封存的原則和程序。

## 建立報告

建立狀態報告以協助處理容量規劃、SLA 檢閱和效能分析。使用事件記錄和系統監視器的每日資料可建立磁碟、記憶體和 CPU 使用量的報告。使用 System Center Operations Manager 可產生上線時間和可用性報告。

您的組織將必須定義狀態報告的原則和程序。

## 事件報告

對您組織有關 Lync Server 的事件報告執行每日稽核。此稽核應包含下列項目：

  - 首要已產生、已解決和擱置的事件。

  - 未解決事件的解決方案。

  - 更新報告以包含新的問題票證。

  - 更新疑難排解指南的文件存放庫並張貼有關系統中斷的分析。

既然您組織選擇的事件追蹤系統獨立於 Lync Server，即表示無法使用特定指示或指標。請參閱文件以找出您組織所選擇的系統。

## 檢查 IIS 記錄和效能

執行 Internet Information Services (IIS) 記錄和效能的每週檢閱。如需有關如何監控 IIS 記錄和效能的詳細資訊，請參閱 [Windows Server 2003 Internet Information Services (IIS) 事件記錄概觀](http://go.microsoft.com/fwlink/?linkid=36077)。檢閱應包含下列項目：

  - Web 服務快取計數器可監控 WWW 服務快取。

  - 動態伺服器網頁 (ASP) 計數器可監控以 ASP 身分執行的應用程式。

如需有關如何監控 IIS 記錄和效能的詳細資訊，請參閱 [Windows Server 2003 Internet Information Services (IIS) 事件記錄概觀](http://go.microsoft.com/fwlink/?linkid=36077)。

## 產生資料庫報告

**若要在 SQL 資料庫上產生報告，請執行下列動作**

1.  開啟 Lync Server 2013。

2.  在主控台樹狀目錄中，展開樹系節點，接著展開 **\[企業集區\]**，然後按一下您要產生資料庫報告的集區。

3.  在詳細資料窗格中，按一下 **\[資料庫\]** 索引標籤。

4.  在 **\[資料庫\]** 索引標籤上，執行下列動作：
    
    1.  若要檢視資料庫的名稱，請展開 **\[一般設定\]**，然後檢視資料庫名稱。
    
    2.  若要擷取集區的使用者摘要統計，請展開 **\[使用者摘要報告\]**，接著按一下 **\[前往\]**，然後檢視結果。
    
    3.  若要擷取集區單一使用者的目前個別使用者資料，請展開 **\[個別使用者報告\]**，接著輸入使用者的 SIP URI，按一下 **\[前往\]**，然後檢視結果。

若要擷取集區的目前會議摘要統計，請展開 **\[會議摘要報告\]**，按一下 **\[前往\]**，然後檢視結果。

## 檢查安全性和 Lync Server 更新

找出任何新的服務套件、Hotfix 或更新。如果適合，請在測試實驗室中測試這些項目，然後使用變更控制程序來安排部署至生產伺服器。此外， Lync Server 元件更新現在於 Windows 更新過程中即可獲得。所有 Lync Server 元件更新必須在執行 Lync Server (適用更新) 的所有伺服器上同時更新。

## 執行 Lync Server 2013 Best Practice Analyzer

Lync Server 2013 Best Practices Analyzer 工具是一種診斷工具，可收集組態資訊並判斷是否根據 Microsoft 最佳作法來設定組態。此工具的文件位於 [Lync Server 2013 最佳做法分析程式](lync-server-2013-lync-server-best-practices-analyzer.md) 和 [執行 Best Practices Analyzer](https://technet.microsoft.com/zh-tw/library/gg398652\(v=ocs.15\)) (執行 Best Practices Analyzer)。

這款工具可針對一組 Lync Server 的預先定義規則來比較您的部署組態資料並報告潛在問題。針對報告的每個問題，該工具會在 Lync Server 環境中提供目前組態和建議的組態。

正確存取網路之後，該工具可以檢查 AD DS 和執行 Lync Server 2013 的伺服器以執行下列動作：

  - 主動執行狀況檢查，確認已根據建議的最佳作法驗證組態。

  - 產生問題清單，例如不是很理想的組態設定、不支援或不建議的選項。

  - 判斷系統一般狀況

  - 協助疑難排解特定問題

  - 提示您在有更新可用時下載更新

  - 提供有關所報告問題的線上和本機文件，並包含疑難排解提示

  - 產生可以擷取以供日後檢閱的組態資訊

確保 RTCBPA.msi 安裝在所有 Lync Server 2013 伺服器上，並產生每週狀況檢查報告。留意報告結果並視需要更正狀況。

## 檢閱 SLA 效能數據

檢查上週的主要效能資料。檢閱根據 SLA 需求的效能。找出趨勢和尚不符合其目標的項目。

## 檢閱 System Center Operations Manager 管理套件和體驗報告的品質

取得並檢閱 Lync Server 2013 管理套件和體驗報告的品質。

## 產生並檢視企業集區的資料庫報告

**若要產生集區報告，請執行下列動作**

1.  開啟 Lync Server 2013。

2.  在主控台樹狀目錄中，展開樹系節點，接著展開 **\[企業集區\]**，然後按一下您要產生資料庫報告的集區。

3.  在詳細資料窗格中，按一下 **\[資料庫\]** 索引標籤。

4.  在 **\[資料庫\]** 索引標籤中，執行下列動作：
    
    1.  若要檢視資料庫名稱，請展開 **\[一般設定\]**，然後檢視資料庫名稱。
    
    2.  若要擷取集區的目前使用者摘要統計，請展開 **\[使用者摘要報告\]**，按一下 **\[前往\]**，然後檢視結果。
    
    3.  若要擷取集區單一使用者的目前個別使用者資料，請展開 **\[個別使用者報告\]**，輸入使用者的 SIP URI，按一下 **\[前往\]**，然後檢視結果。

若要擷取集區的目前會議摘要統計，請展開 **\[會議摘要報告\]**，按一下 **\[前往\]**，然後檢視結果。

針對每個企業集區，系統管理員可以使用 **\[資料庫\]** 索引標籤來檢視資料庫名稱，和從資料庫中擷取報告並加以檢視。

### 資料庫報告和說明

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>章節</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>使用者摘要報告</p></td>
<td><p>Dbanalyze /v /report:diag [/sqlserver:value]</p>
<p>本節顯示有關集區中使用者的彙總資訊，例如已啟用的使用者人數、每位使用者的平均聯絡人人數，以及特定功能的使用者人數。</p>
<p>使用這些報告時，下列資訊或許有幫助：</p>
<ul>
<li><p>已啟用的使用者是指使用 Active Directory 使用者和電腦嵌入式管理單元而針對 Lync Server 2013 啟用的使用者。</p></li>
<li><p>作用中使用者是指已登入或註冊的使用者。</p></li>
<li><p>摘要報告也會提供有關聯絡人的一組統計資訊。這些統計資料僅適用於至少登入一次和至少有一個聯絡人的使用者族群。因此，一般不會看到最低的聯絡人人數為 0。有鑑於此，如果使用者沒有聯絡人 (但為已註冊的作用中使用者)，則可能會看見某些統計欄位為 &lt;空白&gt;。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>個別使用者報告</p></td>
<td><p>Dbanalyze /v /report:disk [/sqlserver:value]</p>
<p>與摘要報告不同，而是透過使用者族群來計算，是有關特定使用者的報告。</p></td>
</tr>
<tr class="odd">
<td><p>會議摘要報告</p></td>
<td><p>Dbanalyze /v /report:conf [/sqlserver:value]</p>
<p>本節顯示有關集區會議摘要統計的彙總資訊，例如作用中會議的數量和參與者的總人數。</p></td>
</tr>
<tr class="even">
<td><p>使用者摘要報告</p></td>
<td><p>Dbanalyze /v /report:diag [/sqlserver:value]</p>
<p>本節顯示有關集區中使用者的彙總資訊，例如已啟用的使用者人數、每位使用者的平均聯絡人人數，以及特定功能的使用者人數。</p>
<p>使用這些報告時，下列資訊或許有幫助：</p>
<ul>
<li><p>已啟用的使用者是指使用 Active Directory 使用者和電腦嵌入式管理單元而針對 Lync Server 2013 啟用的使用者。</p></li>
<li><p>作用中使用者是指已登入或註冊的使用者。</p></li>
<li><p>摘要報告也會提供有關聯絡人的一組統計資訊。這些統計資料僅適用於至少登入一次和至少有一個聯絡人的使用者族群。因此，一般不會看到最低的聯絡人人數為 0。有鑑於此，如果使用者沒有聯絡人 (但為已註冊的作用中使用者)，則可能會看見某些統計欄位為 &lt;空白&gt;。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>個別使用者報告</p></td>
<td><p>Dbanalyze /v /report:disk [/sqlserver:value]</p>
<p>與摘要報告不同，而是透過使用者族群來計算，是有關特定使用者的報告。</p></td>
</tr>
<tr class="even">
<td><p>會議摘要報告</p></td>
<td><p>Dbanalyze /v /report:conf [/sqlserver:value]</p>
<p>本節顯示有關集區會議摘要統計的彙總資訊，例如作用中會議的數量和參與者的總人數。</p></td>
</tr>
</tbody>
</table>


## 執行 Bandwidth Utilization Analyzer

Bandwidth Utilization Analyzer 乃是可針對企業網路中 WAN 連結之 UC 端點頻寬使用量的各種檢視畫面建立相關報告的工具。您可以使用這些報告來瞭解目前頻寬使用量模式並協助處理頻寬容量規劃。這項工具亦會逐一查看指派至各個連結的頻寬容量。

L\\rquote outil effectue les operations suivantes :

  - 產生網路間音訊使用量的特定報告

  - 協助高效執行容量規劃並逐一查看指派至各個連結的頻寬容量

Bandwidth Utilization Analyzer 可以產生頻寬容量和使用量報告的圖形化繪圖。如下所示：

  - 企業網路中的所有 WAN 連結

  - 依已選擇的特定 WAN 連結進行篩選

  - 依超過連結容量的 WAN 連結進行篩選

  - 依所佈建頻寬不足使用的 WAN 連結進行篩選

  - 依已達到重大層級 (大於 WAN 連結之頻寬容量 90% 的頻寬使用量) 的 WAN 連結進行篩選

  - 依 WAN 連結類型進行篩選：網路網站連結、區域間連結，以及網站內連結。

  - 依網路地區進行篩選

此工具的文件可以從下列位置取得 [Lync Server 2013 Resource Kit 工具文件](https://technet.microsoft.com/zh-tw/library/jj945604\(v=ocs.15\)) (Lync Server 2013 Resource Kit 工具文件)。

## 請參閱

#### 其他資源

[每週工作檢查清單](lync-server-2013-operations-checklists.md)

