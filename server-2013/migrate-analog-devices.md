---
title: 移轉類比裝置
TOCTitle: 移轉類比裝置
ms:assetid: ad072916-87ed-4d44-8289-aab87da86250
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721846(v=OCS.15)
ms:contentKeyID: 49890254
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移轉類比裝置

 

_**上次修改主題的時間：** 2012-10-16_

Lync Server 提供類比裝置的支援。具體來說，支援的類比裝置屬於類比語音電話與類比傳真機。 您可以設定合格的閘道，以支援在 Lync Server 環境中使用類比裝置。從 Lync Server 2010 移轉至 Lync Server 2013 之後，您也必須移轉與類比裝置關聯的連絡人物件。請使用 Lync Server 管理命令介面 先擷取與 Lync Server 2010 類比裝置關聯的所有連絡人物件，然後將這些物件移至 Lync Server 2013 集區。

## 移轉類比裝置

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  在命令列中輸入：
    
        Get-CsAnalogDevice -Filter {RegistrarPool -eq "pool01.contoso.net"} | Move-CsAnalogDevice -Target pool02.contoso.net

3.  請確認已將所有連絡人物件移動至 Lync Server 2013 集區。在命令列中輸入：
    
        Get-CsAnalogDevice -Filter {RegistrarPool -eq "pool02.contoso.net"}

4.  請確認所有連絡人物件現在已與 Lync Server 2013 集區關聯。

