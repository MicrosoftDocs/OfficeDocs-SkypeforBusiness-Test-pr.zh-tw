---
title: 安裝 Lync Server 2013 管理套件
TOCTitle: 安裝 Lync Server 2013 管理套件
ms:assetid: b800d4ab-fdc8-4c72-a76a-b78932779fe3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205202(v=OCS.15)
ms:contentKeyID: 49292100
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 安裝 Lync Server 2013 管理套件

 

_**上次修改主題的時間：** 2012-10-22_

System Center Operations Manager 本身具有的監控功能可監控小部分的 Windows 作業系統。您可安裝管理套件來擴充 System Center Operations Manager 的功能。管理套件是能指出 System Center Operations Manager 可監控項目的軟體，包含如何監控這些項目與如何觸發與報告警示。Microsoft Lync Server 2013 包含兩個 System Center Operations Manager 管理套件，可提供下列功能：

  - 元件與使用者管理套件 (Microsoft.LS.2013.Monitoring.ComponentAndUser.mp) 可追蹤的 Lync Server 問題包含事件記錄中所記錄的問題、效能計數器登錄的問題，或詳細通話記錄 (CDR) 或品質經驗 (QoE) 資料庫所記錄的問題。對於重大問題，可設定 System Center Operations Manager 立即透過電子郵件、立即訊息或短訊息服務 (SMS) 訊息通知系統管理員。SMS 是用來在行動裝置間傳送文字訊息的技術。
    
    > [!NOTE]  
    > 如需關於設定 Operations Manager 通知的詳細資訊，請參閱 TechNet Library 中的「設定通知」，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=268785%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=268785&amp;clcid=0x404</a>。
    


  - 主動監視套件 (Microsoft.LS.2013.Monitoring.ActiveMonitoring.mp) 可主動測試主要的 Lync Server 元件，如登入系統、交換立即訊息或撥號至位於公開交換電話網路 (PSTN) 上的電話。這些測試是使用 Lync Server 綜合交易 Cmdlet 進行。例如：使用 **Test-CsIM** Cmdlet 來模擬一組測試使用者間的立即訊息交談。如果此模擬訊息交談失敗，則會產生警示。

這兩個管理套件包含在 Lync Server 2013 中，且包含搭配 Microsoft Lync Server 2010 使用之管理套件的多項增強功能。例如，Lync Server 2013 元件管理套件不限於監控 Lync Server 本身。除了監控 Lync Server 的事件記錄與效能計數器之外，元件管理套件還可追蹤重要項目的效能，與發出警示，如：

  - **網際網路資訊服務 (IIS)**   如果網際網路資訊服務離線，會發出警示。因為 Lync Server Web 服務依賴 IIS，所以這點很重要。

  - **處理程序使用狀況**   若系統資源 (如可用記憶體) 開始降低，會發出警示。即使 Lync Server 不負責高系統使用量，還是會發出這些警示。

  - **電腦失敗事件**   當軟硬體問題威脅到伺服器的可靠性時，會發出警示。例如，如果伺服器遭遇硬碟失敗而產生危險時，會通知 Lync Server 系統管理員。

新的管理套件也包含增強的報告功能。Lync Server 2013 新報告包含：

  - **端對端案例可用性報告**   此報告會詳細記錄主要 Lync Server 服務的可用性/執行時間，如註冊或目前狀態。

  - **容量報告**   此報告使用效能計數器資訊，顯示系統元件的趨勢，如記憶體可用性與處理器使用狀況。

  - **元件報告**   此報告可列出熱門的警示產生器，由 Lync Server 元件群組排列。

除了這些預先設計的報告以外，Lync Server 2013 的管理套件還可自動報告通話可靠性 (由詳細通話記錄測量的計量) 與 QoE 狀態 (由經驗品質測量的計量)。如果您啟用詳細通話記錄，您可從 System Center Operations Manager 主控台完成下列程序來檢視通話可靠性警示：

  - 依序展開 \[監視\]、\[Microsoft Lync Server 2013 狀況\]、\[通話可靠性與媒體品質\]，然後按一下 \[通話可靠性\]。

若要檢視經驗品質警示，請從 System Center Operations Manager 主控台完成下列程序：

  - 依序展開 \[監視\]、\[Microsoft Lync Server 2013 狀況\]、\[通話可靠性與媒體品質\]，然後再展開 \[媒體品質\]。

Lync Server 2013 的管理套件現在使用機器層級的探索，而非 Microsoft Lync Server 2010 中使用的集中探索機制。這表示每個系統中心代理程式本質上會自我探索，然後向 中央管理伺服器 報告其存在。使用機器層級的探索可簡化系統中心基礎結構的管理，並同時允許使用不同版本的 Lync Server 管理套件 (例如，Lync Server 2010 的管理套件與 Lync Server 2013 的管理套件) 同時存在。

