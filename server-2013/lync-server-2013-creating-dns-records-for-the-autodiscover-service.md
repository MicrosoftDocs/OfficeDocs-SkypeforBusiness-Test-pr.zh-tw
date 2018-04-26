---
title: Lync Server 2013：建立自動探索服務的 DNS 記錄
TOCTitle: 建立自動探索服務的 DNS 記錄
ms:assetid: 3756ffe4-c6b1-492d-850e-42a832e06567
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690010(v=OCS.15)
ms:contentKeyID: 49290583
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立自動探索服務的 DNS 記錄

 

_**上次修改主題的時間：** 2014-06-20_

您的 Lync Mobile 使用者將需要啟用自動探索，過程中需要建立部分網域名稱系統 (DNS) 記錄。您可以依照您的需求執行下列動作：

  - 內部 DNS 記錄，以支援正從您組織網路內部連線的行動使用者。

  - 外部 (或公用) DNS 記錄，以支援正從網際網路連線的行動使用者

為什麼需要執行這兩個動作？您必須針對每個 SIP 網域建立內部 DNS 記錄和外部 DNS 記錄。

您建立的 DNS 記錄可以是 A (主機) 記錄或 CNAME 記錄。為了協助您進行，我們會在以下逐步說明如何建立內部及外部 DNS 記錄。如需有關行動使用者之 DNS 需求的其餘資訊，請參閱＜[Lync Server 2013 行動技術需求](lync-server-2013-technical-requirements-for-mobility.md)＞。

## 建立內部 DNS CNAME 記錄

1.  若要製作內部 DNS 記錄，您需要以網域帳戶 (具備 Domain Admins 群組或 DnsAdmins 群組成員身分) 登入網路中的 DNS 伺服器。

2.  開啟 DNS 系統管理嵌入式管理單元：依序按一下 \[開始\] 、\[系統管理工具\] 和 \[DNS\] 。

3.  在 DNS 伺服器的主控台樹狀目錄中，為安裝 Lync Server 2013Director 集區 和 前端集區 的 Active Directory 網域 (例如，contoso.local) 展開 \[正向對應區域\]。

4.  若為內部 DNS 記錄，檢查是否存在 Director 集區 的主機 A (IPv6 為 AAAA) 記錄；若為 Director 集區，內部 Web 服務完整網域名稱 (FQDN) 應有主機 A 記錄存在 (例如，lyncwebdir01.contoso.local)。如果不存在，則您可能未使用 Director 集區，您將需要為 前端集區 使用 FQDN，甚至是單一伺服器 FQDN (若是此類安裝)。

5.  請注意，若為內部 DNS 記錄，請檢查是否存在 前端集區 的主機 A (IPv6 為 AAAA) 記錄；若為 前端集區，內部 Web 服務 FQDN 應有主機 A (或 AAAA) 記錄存在 (例如，lyncwebpool01.contoso.local)。如果不存在，您將需要記錄 前端伺服器 或 Standard Edition 伺服器 的 FQDN。

6.  您知道記錄位於哪個主機 A (或 AAAA) 後，可以在 DNS 伺服器的主控台樹狀目錄中展開您 SIP 網域 (例如 contoso.com) 的 \[正向對應區域\]。

7.  在 SIP 網域名稱上按一下滑鼠右鍵，然後按一下 \[新增別名 (CNAME)\] 。

8.  在 \[別名\] 中，輸入 lyncdiscoverinternal 作為內部自動探索服務 URL 的主機名稱。

9.  在 \[目標主機完整網域名稱 (FQDN)\] 中，輸入或瀏覽 Director 集區 的內部 Web 服務 FQDN (例如 lyncwebdir01.contoso.local)，然後按一下 \[確定\]。

10. 您必須在 Lync Server 2013 環境中，針對您所支援之每個 SIP 網域的正向對應區域，建立新的自動探索 CNAME 記錄。

## 建立外部 DNS CNAME 記錄

1.  若要建立外部 DNS CNAME 記錄，您將需要連線至公用 DNS 提供者，然後依照我們的步驟執行。我們無法明確說明您在 DNS 提供者環境中的動作，因為您可能需要使用不同的方式來管理外部 DNS，但我們希望這些步驟能協助您管理。

2.  使用可在該環境中建立 DNS 記錄的帳戶登入您的外部 DNS 提供者。

3.  您應已針對此環境建立 SIP 網域。展開此 SIP 網域的 \[正向對應區域\]，或依據正在使用的外部 DNS 介面選取它。

4.  您應已看到 Director 集區 的主機 A (IPv6 為 AAAA) 記錄 (例如 lyncwebexdir01.contoso.com)，因此請確認出現該記錄。如果不存在，則您目前可能未使用 Director 集區。若是這種情況，您將需要使用前端集區的 FQDN，否則您必須針對單一伺服器、前端伺服器或 Standard Edition Server 執行此工作。

5.  您也需要確認您的前端集區的外部 Web 服務完整網域名稱 (FQDN) 存在主機 A (IPv6 為 AAAA) 記錄 (例如 lyncwebextpool01.contoso.com)；或如果沒有前端集區，則為單一伺服器 FQDN 的 FQDN。如前一個步驟說明，如果沒有 Director 集區，您需要執行下列步驟以取得此集區。

6.  現在請針對您的外部 DNS 提供者使用適當的格式，選擇用來建立 \[新增別名 (CNAME)\] 的選項 (可能是功能表選項或連結，視 DNS 提供者的格式而定)。

7.  內部 DNS 必須有某些形式的 \[別名\] 文字方塊，您應輸入 lyncdiscover 作為外部自動探索服務 URL 的主機名稱。

8.  必須另有某些形式的 \[目標主機完整網域名稱 (FQDN)\] 文字方塊，您可在此方塊中輸入 Director 集區 的外部 Web 服務 FQDN (例如，lyncwebexdir01.contoso.com)，然後按一下 \[確定\]，或在外部 DNS 中採取任何動作來接受此項目的建立作業。如步驟 4 所述，如果沒有 Director 集區，您將需要使用已安裝的前端集區 FQDN 或單一伺服器 FQDN (視何者較適合)。

9.  您將需要在 Lync 2013 環境支援之每個 SIP 網域的正向對應區域中，製作新的自動探索 CNAME 記錄。

## 建立內部 DNS A 記錄

1.  若要製作內部 DNS 記錄，您需要以網域帳戶 (具備 Domain Admins 群組或 DnsAdmins 群組成員身分) 登入網路中的 DNS 伺服器。

2.  開啟 DNS 系統管理嵌入式管理單元：依序按一下 \[開始\] 、\[系統管理工具\] 和 \[DNS\] 。

3.  若為內部 DNS 記錄，在 DNS 伺服器的主控台樹狀目錄中展開 Active Directory 網域 (例如 contoso.local) 的 \[正向對應區域\]，即安裝您的 Lync Server 2013Director 集區和 前端集區 的位置。

4.  若為內部 DNS 記錄，檢查是否存在 Director 集區 的主機 A (IPv6 為 AAAA) 記錄；若為 Director 集區，內部 Web 服務完整網域名稱 (FQDN) 應有主機 A 記錄存在 (例如，lyncwebdir01.contoso.local)。如果不存在，則您可能未使用 Director 集區，您將為前端集區使用 IP 位址，或甚至是單一伺服器 IP 位址 (若是此類安裝)。

5.  請注意，若為內部 DNS 記錄，請檢查是否存在 前端集區 的主機 A (IPv6 為 AAAA) 記錄；若為 前端集區，內部 Web 服務 FQDN 應有主機 A (或 AAAA) 記錄存在 (例如，lyncwebpool01.contoso.local)。如果不存在，您將需要記錄 前端伺服器 或 Standard Edition 伺服器 的 IP 位址。

6.  您知道記錄位於哪個主機 A (或 AAAA) 後，可以在 DNS 伺服器的主控台樹狀目錄中展開您 SIP 網域 (例如 contoso.com) 的 \[正向對應區域\]。

7.  在 SIP 網域名稱上按一下滑鼠右鍵，然後按一下 \[新增主機 (A 或 AAAA)\] 。

8.  在 \[名稱\] 中，輸入 lyncdiscoverinternal 作為內部自動探索服務 URL 的主機名稱。

9.  在 \[IP 位址\] 中，輸入 Director 的內部 Web 服務 IP 位址 (或者，如果您使用負載平衡器，則輸入 Director 負載平衡器的虛擬 IP (VIP))。UNRESOLVED\_TOKEN\_VAL()UNRESOLVED\_TOKEN\_VAL()如上述的步驟 4 所述，如果不是使用 Director，您可能需要輸入 前端伺服器 或 Standard Edition 伺服器 的 IP 位址，或者，如果使用負載平衡器，請輸入 前端集區 負載平衡器的 VIP。

10. 按一下 \[新增主機\] ，然後按一下 \[確定\] 。

11. 若要建立其他 A 或 AAAA 記錄，請重複步驟 8 到 10。請注意，您將需要在 Lync Server 2013 環境支援之每個 SIP 網域的正向對應區域中，建立新的自動探索 A 或 AAAA 記錄。

12. 完成建立 A (IPv6 為 AAAA) 記錄後，按一下 \[完成\] 。

## 建立外部 DNS A 記錄

1.  若要建立外部 DNS 記錄，請連線至公用 DNS 提供者，然後依照我們的步驟執行。我們無法明確說明您在 DNS 提供者環境中的動作，因為您可能需要使用不同的方式來管理外部 DNS，但我們希望這些步驟能協助您管理。

2.  您將需要使用帳戶登入，且該帳戶必須可在該環境中建立 DNS 記錄。

3.  若為外部 DNS 記錄，在 DNS 伺服器的主控台樹狀目錄中展開 SIP 網域 (例如 contoso.com) 的 \[正向對應區域\]。若為外部 DNS 記錄，在 DNS 伺服器的主控台樹狀目錄中展開 SIP 網域 (例如 contoso.com) 的 \[正向對應區域\]。

4.  您應已看到 Director 集區 的主機 A (IPv6 為 AAAA) 記錄 (例如 lyncwebexdir01.contoso.com)，因此請確認出現該記錄及 IP 位址為何。如果不存在，則您目前可能未使用 Director 集區。若是這種情況，您將需要使用集端集區的 IP 位址，否則您必須針對單一伺服器、前端伺服器或 Standard Edition Server 執行此工作。請注意，伺服器也可能位於負載平衡區後方，或正在使用反向 Proxy。請同時針對下列步驟記錄 IP 位址。

5.  您也需要確認您的前端集區的外部 Web 服務完整網域名稱 (FQDN) 存在主機 A (IPv6 為 AAAA) 記錄 (例如 lyncwebextpool01.contoso.com)；或如果沒有前端集區，則為單一伺服器 Lync 安裝的 IP 位址。如前一個步驟說明，如果沒有 Director 集區，您需要執行下列步驟以取得它。

6.  現在請針對您的外部 DNS 提供者使用適當的格式，選擇用來建立 \[新增主機 A 或 AAAA\] 的選項 (可能是功能表選項或連結，視 DNS 提供者的格式而定)。

7.  必須有一個位置可輸入 \[名稱\]，請輸入 lyncdiscover 作為外部自動探索服務 URL 的主機名稱。

8.  應另有一個 \[IP 位址\] 文字方塊，您可在此方塊中輸入 Director 集區 的 IP (例如，lyncwebexdir01.contoso.com)，或可能是集區之負載平衡器的 IP (或等效的反向 Proxy IP)，然後按一下 \[確定\]，或在外部 DNS 中採取任何動作來接受此項目的建立作業。如步驟 4 所述，如果沒有 Director 集區，您將需要使用已安裝的前端集區 IP 位址或單一伺服器 IP 位址 (視何者較適合)。

9.  您將需要在 Lync 2013 環境支援之每個 SIP 網域的正向對應區域中，製作新的自動探索 A 或 AAAA 記錄。

