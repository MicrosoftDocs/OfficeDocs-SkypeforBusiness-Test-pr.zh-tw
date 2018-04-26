---
title: Lync Server 2013：設定 Edge 支援的 DNS
TOCTitle: 設定 Edge 支援的 DNS
ms:assetid: 955493e6-aa29-424d-bb81-1ef87b3b15e3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398756(v=OCS.15)
ms:contentKeyID: 49291706
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定 Edge 支援的 DNS

 

_**上次修改主題的時間：** 2013-02-15_

您必須為內部和外部 Edge 介面設定網域名稱系統 (DNS) 記錄，介面包括 Edge Server 和反向 Proxy 介面。Edge Server 預設不會加入網域，而且將不會具備完整網域名稱。Edge Server 只能透過簡短 (電腦) 名稱來稱呼，而不能使用完整網域名稱來稱呼。但是， 拓撲產生器會使用 FQDN，而不是簡短名稱。Edge Server 的名稱必須符合 拓撲產生器所使用的 FQDN。若要執行此動作，您需定義 DNS 尾碼，在組合電腦名稱時，即會產生預期的 FQDN。請使用＜將 DNS 尾碼新增至未加入網域之 Edge Server 上的電腦名稱＞中的程序，將 DNS 尾碼新增至電腦名稱。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>根據預設，DNS 會使用循環配置資源演算法來旋轉查詢解答中所傳回的資源記錄資料順序，其中對於所查詢的 DNS 網域名稱有多個相同類型的資源記錄存在。 Lync Server 2013 DNS 負載平衡，會根據 DNS 循環配置資源而成為 DNS 負載平衡機制的一部分。請確認尚未停用循環配置資源設定。如果您使用的 DNS 伺服器不是執行 Windows 作業系統，請確認已啟用循環配置資源的記錄順序。</td>
</tr>
</tbody>
</table>


使用「建立 DNS SRV 記錄」 中的程序，來建立和確認每個 DNS SRV 記錄。請使用「建立 DNS A 記錄」 中的程序，來定義外部使用者存取所需的 DNS A 記錄。若要確認記錄已設定且可正確運作，請參閱本主題中的「確認 DNS 記錄」 。如需關於支援外部使用者存取所需之每個記錄的詳細資訊，請參閱＜ [針對 Lync Server 2013 判定 DNS 需求](lync-server-2013-determine-dns-requirements.md)＞。

## 將 DNS 尾碼新增至未加入網域之 Edge Server 上的電腦名稱

1.  在電腦上，按一下 \[開始\] 、在 \[電腦\] 上按一下滑鼠右鍵，然後按一下 \[內容\] 。

2.  在 \[電腦名稱、網域及工作群組設定\] 下，按一下 \[變更設定\] 。

3.  在 \[電腦名稱\] 索引標籤上，按一下 \[變更\] 。

4.  在 \[電腦名稱/網域變更\] 中，按一下 \[其他\] 。

5.  在 \[DNS 尾碼和 NetBIOS 電腦名稱\] 的 \[這部電腦的主要 DNS 尾碼\] 中，輸入內部網域的名稱 (例如，corp.contoso.com)，然後按三次 \[確定\] 。

6.  重新啟動電腦。

## 建立 DNS SRV 記錄

1.  在適當的 DNS 伺服器上，依序按一下 \[開始\] 、\[控制台\] 、\[系統管理工具\] 和 \[DNS\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您需要設定 DNS，才會有：1) 外部 DNS 項目，適用於遠端使用者和同盟協力廠商的外部 DNS 查閱；2) DNS 查閱的項目，適用於周邊網路 (也稱為 DMZ、非軍事區域和遮蔽式子網路) 內的 Edge Server，包括執行 Lync Server 2013 之內部伺服器的 A 記錄；3) 內部 DNS 項目，適用於內部用戶端和執行 Lync Server 2013 的伺服器進行查閱。</td>
    </tr>
    </tbody>
    </table>


2.  在 SIP 網域的主控台樹狀目錄中，展開 \[正向對應區域\] ，然後在安裝 Lync Server 2013 的網域上按一下滑鼠右鍵。

3.  按一下 \[新增其他記錄\] 。

4.  在 \[選擇資源記錄類型\] 中，輸入 \[服務位置 (SRV)\] ，然後按一下 \[建立記錄\] 。

5.  提供 DNS SRV 記錄的所有必要資訊。

## 建立 DNS A 記錄

1.  在 DNS 伺服器上，依序按一下 \[開始\] 、\[控制台\] 、\[系統管理工具\] 和 \[DNS\] 。

2.  在 SIP 網域的主控台樹狀目錄中，展開 \[正向對應區域\] ，然後在安裝 Lync Server 2013 的網域上按一下滑鼠右鍵。

3.  按一下 \[新增主機 (A)\] 。

4.  提供 DNS SRV 記錄的所有必要資訊。

## 確認 DNS 記錄

1.  登入網域中的用戶端電腦。

2.  按一下 \[開始\] ，然後再按一下 \[執行\] 。

3.  在命令提示字元中執行下列命令：
    
        nslookup <FQDN edge interface>

4.  確認您收到回覆，且可解析為 FQDN 的適當 IP 位址。

## 請參閱

#### 工作

[針對與主控 Exchange UM 的整合建立 DNS SRV 記錄](lync-server-2013-create-a-dns-srv-record-for-integration-with-hosted-exchange-um.md)  

#### 概念

[針對 Lync Server 2013 判定 DNS 需求](lync-server-2013-determine-dns-requirements.md)

