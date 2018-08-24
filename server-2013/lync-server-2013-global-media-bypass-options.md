---
title: Lync Server 2013 中的全域媒體旁路選項
TOCTitle: Lync Server 2013 中的全域媒體旁路選項
ms:assetid: 1bd35f90-8587-48a1-b0c2-095a4053fc77
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398255(v=OCS.15)
ms:contentKeyID: 49290254
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的全域媒體旁路選項

 

_**上次修改主題的時間：** 2012-10-04_

> [!NOTE]  
> 本主題假設前提為您已針對希望媒體略過中繼伺服器的特定網站或服務，設定好主幹對等端 (公用交換電話網路 (PSTN) 閘道、IP-PBX 或網際網路電話語音服務提供者上的工作階段邊界控制器 (SBC)) 的媒體旁路。



除了啟用對等端相關之個別主幹連線的媒體旁路，您也必須全域啟用媒體旁路。全域媒體旁路設定可以指定為 PSTN 的來電一律嘗試使用媒體旁路，或是使用網路網站和網路地區的子網路對應來採用媒體旁路，此方法與通話許可控制 (此為另一個進階語音功能) 類似。媒體旁路和通話許可控制都啟用時，在判斷是否採用媒體旁路時，會自動使用指定給通話許可控制的網路地區、網路網站以及子網路資訊。亦即，在啟用通話許可控制的狀況下，您無法指定對 PSTN 的來電一律嘗試使用媒體旁路。

本主題說明如何搭配使用 Lync Server 控制台和 Lync Server 管理命令介面，來進行全域媒體旁路設定。

> [!NOTE]  
> 使用下列步驟設定媒體旁路時，假設前提是用戶端和中繼伺服器對等端 (例如 PSTN 閘道、IP-PBX 或 SIP 主幹提供者上的 SBC) 之間的連線良好。如果連結上有頻寬限制，就無法將媒體旁路套用至通話。媒體旁路不會與每個 PSTN 閘道、IP-PBX 以及 SBC 相互溝通。Microsoft 已經與認證的合作夥伴測試了一組 PSTN 閘道和 SBC，並用 Cisco IP-PBX 完成部分測試。只有列在 Unified Communications Open Interoperability Program – Lync Server 中的產品和版本支援媒體旁路，網址為：<a href="http://go.microsoft.com/fwlink/?linkid=214406%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=214406&amp;clcid=0x404</a>。



## 後續步驟：選擇全域媒體旁路設定

在針對特定網站或服務對等端的主幹連線啟用媒體旁路後，使用下列內容可執行下列其中一項：

  - 一律啟用媒體旁路，如[在 Lync Server 2013 中設定媒體旁路以一律略過中繼伺服器](lync-server-2013-configure-media-bypass-to-always-bypass-the-mediation-server.md)所述。

  - 或者，設定媒體旁路使用網站與地區資訊，如＜[在 Lync Server 2013 中設定媒體旁路全域設定以使用網站和區域資訊](lync-server-2013-configure-media-bypass-global-settings-to-use-site-and-region-information.md)＞所述。

## 請參閱

#### 工作

[在 Lync Server 2013 中設定含媒體旁路的主幹](lync-server-2013-configure-a-trunk-with-media-bypass.md)  
[在 Lync Server 2013 中建立子網路與網路站台的關聯](lync-server-2013-associate-a-subnet-with-a-network-site.md)  

#### 概念

[在 Lync Server 2013 中設定媒體旁路](lync-server-2013-configure-media-bypass.md)  
[Lync Server 2013 中的媒體旁路和中繼伺服器](lync-server-2013-media-bypass-and-mediation-server.md)

