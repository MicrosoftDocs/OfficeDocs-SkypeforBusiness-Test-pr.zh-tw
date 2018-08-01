---
title: Lync Server 2013：協力廠商 PSTN 閘道或 PBX 的通話許可控制
TOCTitle: 協力廠商 PSTN 閘道或 PBX 的通話許可控制
ms:assetid: 95dc4ceb-bcad-48ee-86ec-af911727f853
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398762(v=OCS.15)
ms:contentKeyID: 49291720
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的協力廠商 PSTN 閘道或 PBX 的通話許可控制

 

_**上次修改主題的時間：** 2012-10-20_

本主題說明如何將通話許可控制 (CAC) 部署於中繼伺服器閘道介面和協力廠商公用交換電話網路 (PSTN) 閘道或專用交換機 (PBX) 間連結上的範例。

## 案例 1：中繼伺服器和 PSTN 閘道間的 CAC

將 CAC 部署於中繼伺服器閘道介面和協力廠商 PBX 或 PSTN 閘道間的 WAN 連結上。

**案例 1：中繼伺服器和 PSTN 閘道間的 CAC**

![案例 1：中繼伺服器和 PSTN 閘道間的 CAC](images/Gg398762.4bebf9ee-2732-4ea6-bbe5-0269b2903d8c(OCS.15).jpg "案例 1：中繼伺服器和 PSTN 閘道間的 CAC")

此範例會將 CAC 套用於中繼伺服器和 PSTN 閘道間。如果位在網路網站 1 的 Lync 用戶端使用者透過位在網路網站 2 的 PSTN 閘道撥打 PSTN 通話，媒體會流經 WAN 連結。因此，系統會針對每個 PSTN 工作階段執行兩次 CAC 檢查：

  - Lync 用戶端應用程式和中繼伺服器之間

  - 中繼伺服器和 PSTN 閘道之間

這項措施適用於通往網路網站 1 之用戶端的傳入 PSTN 通話，以及適用於源自網路網站 1 之用戶端應用程式的傳出 PSTN 通話。

> [!Note]  
> 請確定 PSTN 閘道隸屬的 IP 子網路已經過設定，並與網路網站 2 相關聯。<br />
> 請確定中繼伺服器之兩個介面隸屬的 IP 子網路已經過設定，並與網路網站 1 相關聯。<br />
> 如需詳細資訊，請參閱＜<a href="lync-server-2013-associate-a-subnet-with-a-network-site.md">在 Lync Server 2013 中建立子網路與網路站台的關聯</a>＞。



## 案例 2：中繼伺服器和具有媒體終端點之協力廠商 PBX 間的 CAC

這項設定和案例 1 相似。在這兩個案例中，中繼伺服器都知道在 WAN 連結對面終止媒體的裝置為何，且已在中繼伺服器上將 PSTN 閘道的 IP 位址或具有媒體終端點 (MTP) 的 PBX 設定為下一個躍點。

**案例 2：中繼伺服器和具有 MTP 之協力廠商 PBX 間的 CAC**

![案例 2：中繼伺服器和具有 MTP 之 PBX 間的 CAC](images/Gg398762.1c0b5263-c053-4cca-842f-85dd670760c8(OCS.15).jpg "案例 2：中繼伺服器和具有 MTP 之 PBX 間的 CAC")

此範例將 CAC 套用於中繼伺服器和 PBX/MTP 閘道間。如果位在網路網站 1 的 Lync 用戶端使用者透過位在網路網站 2 的 PBX/MTP 撥打 PSTN 通話，媒體會流經 WAN 連結。因此，系統會針對每個 PSTN 工作階段執行兩次 CAC 檢查：

  - Lync 用戶端應用程式和中繼伺服器之間

  - 中繼伺服器和 PBX/MTP 閘道之間

這項措施適用於通往網路網站 1 之用戶端的傳入 PSTN 通話，以及源自網路網站 1 之用戶端的傳出 PSTN 通話。

> [!Note]  
> 請確定 MTP 隸屬的 IP 子網路已經過設定，並與網路網站 2 相關聯。<br />
> 請確定中繼伺服器之兩個介面隸屬的 IP 子網路已經過設定，並與網路網站 1 相關聯。<br />
> 如需詳細資訊，請參閱＜<a href="lync-server-2013-associate-a-subnet-with-a-network-site.md">在 Lync Server 2013 中建立子網路與網路站台的關聯</a>＞。



## 案例 3：中繼伺服器和不具有媒體終端點之協力廠商 PBX 間的 CAC

案例 3 與前兩個案例有些許差異。如果協力廠商 PBX 上沒有 MTP，中繼伺服器便無法得知通往協力廠商 PBX 之傳出工作階段要求的媒體該在 PBX 界限中的何處終止。在這種情況下，媒體會直接在中繼伺服器和協力廠商端點裝置之間流動。

**案例 3：中繼伺服器和不具有 MTP 之協力廠商 PBX 間的 CAC**

![案例 3：中繼伺服器和不具有 MTP 之 PBX 間的 CAC](images/Gg398762.f4bcf800-3a68-4037-bb3f-adb2fdf50d32(OCS.15).jpg "案例 3：中繼伺服器和不具有 MTP 之 PBX 間的 CAC")

在此範例中，如果位在網路網站 1 的 Lync 用戶端使用者透過 PBX 與使用者通話，中繼伺服器只能在 Proxy Leg (介於 Lync 用戶端應用程式和中繼伺服器之間) 上執行 CAC 檢查。由於中繼伺服器在工作階段要求提出之際並沒有端點裝置的相關資訊，因此無法在建立通話之前於 WAN 連結 (介於中繼伺服器和協力廠商端點之間) 上執行 CAC 檢查。然而在工作階段建立後，中繼伺服器會促成主幹使用之頻寬的數據統計。

對於源自協力廠商端點的通話，由於在工作階段要求提出之際能取得端點裝置的相關資訊，因此中繼伺服器能在兩端執行 CAC 檢查。

> [!Note]  
> 請確定端點裝置隸屬的 IP 子網路已經過設定，並與網路網站 2 相關聯。<br />
> 請確定中繼伺服器之兩個介面隸屬的 IP 子網路已經過設定，並與網路網站 1 相關聯。<br />
> 如需詳細資訊，請參閱＜<a href="lync-server-2013-associate-a-subnet-with-a-network-site.md">在 Lync Server 2013 中建立子網路與網路站台的關聯</a>＞。


