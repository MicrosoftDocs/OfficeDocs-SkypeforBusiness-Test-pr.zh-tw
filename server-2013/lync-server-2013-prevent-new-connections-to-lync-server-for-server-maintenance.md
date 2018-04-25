---
title: 不允許與 Lync Server 建立新連線以進行伺服器維護
TOCTitle: 不允許與 Lync Server 建立新連線以進行伺服器維護
ms:assetid: 22b27adf-a590-43bd-9306-a5789ae108d7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520964(v=OCS.15)
ms:contentKeyID: 49290336
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 不允許與 Lync Server 建立新連線以進行伺服器維護

 

_**上次修改主題的時間：** 2012-11-01_

Lync Server 讓您將伺服器離線 (例如，為了套用軟體或硬體升級)，完全不會對使用者中斷服務。

當您指定該選項以防止對集區中的伺服器進行新的連線或呼叫時，該選項會在您正式實作這個選項時停止接受任何新的連線與呼叫。這些新的連線和呼叫會路由轉送給集區中的其他伺服器。伺服器會防止新的連線進入，以讓現有連線的工作階段持續進行到自然結束為止。當所有現有的工作階段都結束時，伺服器就可以準備離線。

當您阻止對前端伺服器進行新的連線時，某些 Lync Server 功能與服務需要仰賴 DNS 負載平衡以確保正常運作。如果您的集區沒有使用 DNS 負載平衡，透過這些服務進行的連線可能無法在伺服器阻止新的連線傳入期間，由系統重新路由傳送至其他伺服器，因此當該伺服器離線時，有些工作階段及呼叫便會中斷。以下是仰賴 DNS 負載平衡以確保此選項正常運作的相關功能：

  - Attendant

  - 會議宣告應用程式

  - 回應群組應用程式

  - 宣告應用程式

  - 通話駐留應用程式

如需 DNS 負載平衡的詳細資訊，請參閱規劃文件中的＜[Lync Server 2013 中的 DNS 負載平衡](lync-server-2013-dns-load-balancing.md)＞。

除了防止執行 Lync Server 的伺服器上的所有服務進行新的連線，您還可以防止個別 Lync Server 服務進行新的連線。例如，當您需要套用無須讓整部伺服器關機的 Lync Server 更新時，這個方法就很有用。請注意，當您要防止某個服務進行連線，必須選取已經顯示在 Windows 服務清單中的分組服務項目。例如，Lync Server 前端服務與監控的資料收集代理程式等，都是個別的 Lync Server 服務，不過在 Windows 服務清單裡，這些服務都會整合並顯示為 Lync Server 前端服務。您可以防止 Lync Server 前端服務進行新的連線，不過您無法防止這兩個基礎 Lync Server 服務個別進行新的連線。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>設定伺服器防止新連線、接著重新啟動伺服器後，依預設伺服器會在啟動後立即開始接受新連線。若要避免這種情形，請在重新啟動伺服器前，將伺服器設為僅能手動暫停和繼續。</td>
</tr>
</tbody>
</table>


## 防止新連線連入 Lync Server：

1.  以 Administrators 群組成員的身分登入本機電腦。

2.  開啟 \[服務\] 嵌入式管理單元主控台：按一下 **\[開始\]**，依序指向 **\[所有程式\]** 和 **\[系統管理工具\]**，然後按一下 **\[服務\]**。

3.  在清單中，按兩下您要防止新連線的 Lync Server Windows 服務。

4.  在 \[內容\] 對話方塊的 **\[服務狀態: 已啟動\]** 下方，按一下 **\[暫停\]**。

5.  (選用，但建議) 按一下 **\[啟動類型\]** 旁的 **\[手動\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>設定伺服器防止新連線、接著重新啟動伺服器後，依預設伺服器會在啟動後立即開始接受新連線。若要避免這種情形，請在重新啟動伺服器前，將伺服器設為僅能手動暫停和繼續。</td>
    </tr>
    </tbody>
    </table>


6.  完成時，請按一下 **\[確定\]**。

