---
title: Lync Server 2013：擷取位置
TOCTitle: 擷取位置
ms:assetid: 9bf069aa-d240-4d95-be3a-e795537f8e70
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205110(v=OCS.15)
ms:contentKeyID: 49291798
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中擷取位置

 

_**上次修改主題的時間：** 2012-06-06_

在 Lync Server 2013 E9-1-1 部署中，每個內部連線的 Lync 或 Lync Phone Edition 用戶端都會主動取得自己的位置。註冊 SIP 之後，用戶端會在傳送給 位置資訊服務 (以複寫的 SQL Server 資料庫為後盾的 Web 服務) 的位置要求中提供對本身自知的所有網路連線資訊。每個中央網站集區都有 位置資訊服務，此服務使用網路資訊來查詢本身記錄中是否有相符的位置。如果有相符項目，則 位置資訊服務會傳回位置給用戶端。如果沒有相符項目，則會提示使用者手動輸入位置 (視位置原則設定而定)。位置資料會以名為 Presence Information Data Format Location Object (PIDF-LO) 的格式 (這是網際網路工程任務推動小組 (IETF) 所制定的標準化 XML 格式) 傳回給用戶端。

Lync Server 用戶端會在緊急電話中包含 PIDF-LO 資料，供 E9-1-1 服務提供者用來判斷適當的 PSAP，並將電話連同正確的 ESQK 一起路由至該 PSAP，讓 PSAP 調度員得以取得來電者的位置。

下圖顯示 Lync Server 用戶端如何取得位置 (以第三方用戶端 MAC 位址為基礎的位置方法除外)：

![用戶端如何取得位置圖表](images/JJ205110.4438f5fc-f1b2-444b-8565-09035363ed43(OCS.15).jpg "用戶端如何取得位置圖表")

若要讓用戶端取得位置，必須執行下列步驟：

1.  系統管理員將網路接線圖 (一種將各種不同的網路位址對應到相對應緊急回應位置 (ERL) 的表格) 填入 位置資訊服務資料庫。

2.  如果您使用 SIP 主幹 E9-1-1 服務提供者，系統管理員會根據 E9-1-1 服務提供者所維護的主要街道地址指南 (MSAG) 資料庫驗證 ERL 的市民地址部分。如果您使用 ELIN 閘道，系統管理員會確定 PSTN 業者將 ELIN 上傳至自動位置識別 (ALI) 資料庫。

3.  註冊期間或網路發生變更時，內部連線用戶端會傳送位置要求 (其中包含用戶端被發現的網路位址) 給 位置資訊服務。

4.  位置資訊服務會查詢已發行的記錄中是否有某個位置，並在找到相符項目時傳回 PIDF-LO 格式的 ERL 給用戶端。

