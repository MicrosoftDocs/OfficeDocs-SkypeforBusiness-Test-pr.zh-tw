---
title: 填入位置資料庫
TOCTitle: 填入位置資料庫
ms:assetid: fb84f5b6-c991-4893-bdbf-f195b4b7d28e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413069(v=OCS.15)
ms:contentKeyID: 49292904
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 填入位置資料庫

 

_**上次修改主題的時間：** 2015-03-09_

若要在網路內自動尋找用戶端，您首先需要在位置資料庫中填入網路*線路圖*，該線路圖會將網路元素對應至市街地址。您可以使用子網路、無線存取點、交換器和連接埠定義路線圖。

您可以個別將地址加入至位置資料庫，或是使用包含下表所述資料行格式的 CSV 檔大量加入。

如果您使用 Emergency Location Identification Number (ELIN) 閘道，請在每個位置的 \[公司名稱\] 欄位中包含 ELIN。每個地點可包含多個 ELIN，請以分號分隔。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>網路元素</th>
<th>必要資料行</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>無線存取點</strong></p></td>
<td><p>&lt;BSSID&gt;,&lt;Description&gt;,&lt;Location&gt;,&lt;CompanyName&gt;,&lt;HouseNumber&gt;,&lt;HouseNumberSuffix&gt;,&lt;PreDirectional&gt;,…</p>
<p>…&lt;StreetName&gt;,&lt;StreetSuffix&gt;,&lt;PostDirectional&gt;,&lt;City&gt;,&lt;State&gt;,&lt;PostalCode&gt;,&lt;Country&gt;</p></td>
</tr>
<tr class="even">
<td><p><strong>子網路</strong></p></td>
<td><p>&lt;Subnet&gt;,&lt;Description&gt;,&lt;Location&gt;,&lt;CompanyName&gt;,&lt;HouseNumber&gt;,&lt;HouseNumberSuffix&gt;,&lt;PreDirectional&gt;,…</p>
<p>…&lt;StreetName&gt;,&lt;StreetSuffix&gt;,&lt;PostDirectional&gt;,&lt;City&gt;,&lt;State&gt;,&lt;PostalCode&gt;,&lt;Country&gt;</p></td>
</tr>
<tr class="odd">
<td><p><strong>連接埠</strong></p></td>
<td><p>&lt;ChassisID&gt;,&lt;PortIDSubType&gt;,&lt;PortID&gt;,&lt;Description&gt;,&lt;Location&gt;,&lt;CompanyName&gt;,&lt;HouseNumber&gt;,&lt;HouseNumberSuffix&gt;,…</p>
<p>…&lt;PreDirectional&gt;,&lt;StreetName&gt;,&lt;StreetSuffix&gt;,&lt;PostDirectional&gt;,&lt;City&gt;,&lt;State&gt;,&lt;PostalCode&gt;,&lt;Country&gt;</p></td>
</tr>
<tr class="even">
<td><p><strong>交換器</strong></p></td>
<td><p>&lt;ChassisID&gt;,&lt;Description&gt;,&lt;Location&gt;,&lt;CompanyName&gt;,&lt;HouseNumber&gt;,&lt;HouseNumberSuffix&gt;,&lt;PreDirectional&gt;,…</p>
<p>…&lt;StreetName&gt;,&lt;StreetSuffix&gt;,&lt;PostDirectional&gt;,&lt;City&gt;,&lt;State&gt;,&lt;PostalCode&gt;,&lt;Country&gt;</p></td>
</tr>
</tbody>
</table>


如果您未填入位置資料庫，而且 \[位置原則\] 中的 \[所需地點\] 設定為 \[是\] 或 \[免責聲明\]，則用戶端將會提示使用者手動輸入位置。

如需填入位置資料庫的詳細資訊，請參閱 Lync Server 管理命令介面文件中的下列 Cmdlet：

  - **Get-CsLisSubnet**

  - **Set-CsLisSubnet**

  - Remove-CsLisSubnet

  - **Get-CsLisWirelessAccessPoint**

  - **Set-CsLisWirelessAccessPoint**

  - **Remove-CsLisWirelessAccessPoint**

  - **Get-CsLisSwitch**

  - **Set-CsLisSwitch**

  - **Remove-CsLisSwitch**

  - **Get-CsLisPort**

  - **Set-CsLisPort**

  - **Remove-CsLisPort**

## 若要將網路元素加入至位置資料庫

1.  執行下列 Cmdlet，將子網路位置加入至位置資料庫。
    
        Set-CsLisSubnet -Subnet 157.56.66.0 -Description "Subnet 1" -Location Location1 -CompanyName "Litware" -HouseNumber 1234 -HouseNumberSuffix "" -PreDirectional "" -StreetName 163rd -StreetSuffix Ave -PostDirectional NE -City Redmond -State WA -PostalCode 99123 -Country US
    
    在 ELIN 閘道中，請於 \[公司欄位\] 欄位中輸入 ELIN。可包含一個以上的 ELIN。例如：
    
        Set-CsLisSubnet -Subnet 157.56.66.0 -Description "Subnet 1" -Location Location1 -CompanyName 425-555-0100; 425-555-0200; 425-555-0300 -HouseNumber 1234 -HouseNumberSuffix "" -PreDirectional "" -StreetName 163rd -StreetSuffix Ave -PostDirectional NE -City Redmond -State WA -PostalCode 99123 -Country US
    
    或者，您可以執行下列 Cmdlet 並使用名為 ‘subnets.csv’ 的檔案大量更新子網路位置。
    
        $g = Import-Csv subnets.csv
        $g | Set-CsLisSubnet

2.  執行下列 Cmdlet，將無線網路位置加入至位置資料庫。
    
        Set-CsLisWirelessAccessPoint -BSSID 0A-23-CD-16-AA-2E -Description "Wireless1" -Location Location2 -CompanyName "Litware" -HouseNumber 2345 -HouseNumberSuffix "" -PreDirectional "" -StreetName 163rd -StreetSuffix Ave -PostDirectional NE -City Bellevue -State WA -PostalCode 99234 -Country US
    
    或者，您可以執行下列 Cmdlet，使用名為 ‘waps.csv’ 的 csv 檔案大量更新無線網路位置。
    
        $g = Import-Csv waps.csv
        $g | Set-CsLisWirelessAccessPoint

3.  執行下列 Cmdlet，將交換器位置加入至位置資料庫。
    
        Set-CsLisSwitch-ChassisID 0B-23-CD-16-AA-BB -Description "Switch1" -Location Location1 -CompanyName "Litware" -HouseNumber 1234 -HouseNumberSuffix "" -PreDirectional "" -StreetName 163rd -StreetSuffix Ave -PostDirectional NE -City Redmond -State WA -PostalCode 99123 -Country US
    
    或者，您可以執行下列 Cmdlet，使用名為 ‘switches.csv’ 的 csv 檔案大量更新交換器位置。
    
        $g = Import-Csv switches.csv
        $g | Set-CsLisSwitch

4.  執行下列 Cmdlet，將連接埠位置加入至位置資料庫。
    
        Set-CsLisPort -ChassisID 0C-23-CD-16-AA-CC -PortID 0A-abcd -Description "Port1" -Location Location2 -CompanyName "Litware" -HouseNumber 2345 -HouseNumberSuffix "" -PreDirectional "" -StreetName 163rd -StreetSuffix Ave -PostDirectional NE -City Bellevue -State WA -PostalCode 99234 -Country US
    
    PortIDSubType 的預設值為 LocallyAssigned。您也可以將它設定為 InterfaceAlias 或 InterfaceName
    
    或者，您可以執行下列 Cmdlet，使用名為 ‘ports.csv’ 的 csv 檔案大量更新連接埠位置。
    
        $g = Import-Csv ports.csv
        $g | Set-CsLisPort

