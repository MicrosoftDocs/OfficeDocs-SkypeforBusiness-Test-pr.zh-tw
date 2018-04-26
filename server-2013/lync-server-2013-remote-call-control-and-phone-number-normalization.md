---
title: Lync Server 2013：遠端呼叫控制和電話號碼正規化
TOCTitle: 遠端呼叫控制和電話號碼正規化
ms:assetid: 291d9e87-4c65-4ea2-888f-517741391de5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558630(v=OCS.15)
ms:contentKeyID: 49290422
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的遠端呼叫控制和電話號碼正規化

 

_**上次修改主題的時間：** 2012-09-22_

Lync 用戶端在下載通訊錄服務 (ABS) 檔案時，會下載電話號碼正規化規則。在遠端呼叫控制案例中，通訊錄服務電話號碼正規化規則會同時套用至撥入與撥出的遠端呼叫控制電話。有來電撥打給已啟用遠端呼叫控制的使用者時，來電者的電話號碼會先由 SIP/CSTA 閘道或專用交換機 (PBX) 正規化為 E.164 格式。 Lync Server 2013 從閘道接收到來電時，會先根據受話者的 Microsoft Office Outlook 連絡人清單或存放在通訊錄服務中的全域通訊清單 (GAL) 之中的正規化號碼，對來電者的電話號碼執行反向號碼查閱。如果反向號碼查閱順利找到相符項目，則會以來電通知中的名稱識別來電者。

針對撥出的遠端呼叫控制電話， Lync 則會先對撥打的號碼套用通訊錄服務電話號碼正規化規則，再將電話路由至 SIP/CSTA 閘道。

如需有關為遠端呼叫控制建立電話號碼正規化規則的詳細資訊，請參閱規劃文件中的＜ [Lync Server 2013 中的撥號對應表和正規化規則](lync-server-2013-dial-plans-and-normalization-rules.md)＞。

## 移轉電話號碼正規化規則

如果您要移轉先前啟用遠端呼叫控制的使用者，請參閱移轉文件中的下列主題：

  - 若為 Lync Server 2010，請參閱移轉文件中的＜ [移轉通訊錄](migrate-address-book.md)＞。

  - 若為 Communications Server 2007 R2，請參閱移轉文件中的＜ [移轉通訊錄](migrate-address-book_1.md)＞。

