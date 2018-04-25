---
title: New-CsWebTrustedCACertificate
TOCTitle: New-CsWebTrustedCACertificate
ms:assetid: a0a94971-372a-401a-8ae0-9ff649a9c301
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412746(v=OCS.15)
ms:contentKeyID: 49291858
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsWebTrustedCACertificate

 

_**上次修改主題的時間：** 2015-03-09_

根據現有的憑證授權單位 (CA) 憑證建立新的憑證識別碼物件。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsWebTrustedCACertificate -CAStore <TrustedRootCA | IntermediateCA | ThirdPartyRootCA> -Thumbprint <String>

## 範例

## 範例 1

範例 1 所示的命令會新建信任的 CA 憑證，然後將該憑證新增至 Redmond 網站之 Web 服務組態設定的 TrustedCACerts 屬性。為了執行此工作，範例中的第一個命令會使用 **New-CsWebTrustedCACertificate** Cmdlet 新建信任的 CA 憑證 (此憑證位於受信任根憑證存放區中，而且具有指紋 D543DFF74FEEA425162FD25F342786F1AB453BB3)。產生的憑證物件會儲存於名為 $x 的變數中。

建立憑證物件之後，範例中的第二個命令會將該憑證新增至 TrustedCACerts 內容。為達此目的，此命令會使用 **Set-CsWebServiceConfiguration** Cmdlet 搭配 TrustedCACerts 參數。參數值 ${Add=$x} 會指示 Cmdlet，將變數 $x 中儲存的憑證新增至信任的 CA 憑證集合。

    $x = New-CsWebTrustedCACertificate -Thumbprint "D543DFF74FEEA425162FD25F342786F1AB453BB3" -CAStore TrustedRootCA
    
    Set-CsWebServiceConfiguration -Identity site:Redmond -TrustedCACerts @{Add=$x}

## 詳細描述

Web 服務組態設定是用來協助管理 Lync Server 網頁伺服器和 Web 服務。在可利用這些設定來管理的屬性值中，其中一個就是 TrustedCACerts 屬性；此屬性代表 Lync Phone Edition 信任之憑證授權單位的集合。從信任的 CA 取得之憑證允許這些用戶端增強與執行 Lync Server 之伺服器的連線安全性。若要將新的 CA 新增至信任的憑證授權單位集合，您必須在本機電腦的憑證存放區中新增該 CA 的憑證鏈結。在確認已安裝憑證鏈結之後，接著可使用 **New-CsWebTrustedCACertificate** Cmdlet 來建立可新增至 Web 服務組態設定集合的憑證識別碼物件。

請注意，簽署安裝 Lync Server 時所使用之預設伺服器憑證的憑證授權單位會自動獲得信任，不需要新增至 Web 服務組態設定集合的 TrustedCACerts 內容。除了發行預設憑證的 CA 之外，TrustedCACerts 還應該包含需要信任之 CA 的識別身分。在大部分的情況下，發行預設憑證的 CA 就是唯一需要信任的憑證授權單位。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsWebTrustedCACertificate** Cmdlet：RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsWebTrustedCACertificate"}

## 參數


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>必要</th>
<th>類型</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>CAStore</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Web.CAStore</p></td>
<td><p>表示 (在本機電腦上) 儲存憑證的憑證存放區名稱。有效值為：</p>
<p>TrustedRootCA</p>
<p>IntermediateCA</p>
<p>ThirdPartyRootCA</p></td>
</tr>
<tr class="even">
<td><p><em>Thumbprint</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>應受到 Lync Phone Edition 信任之憑證的指紋。您可以執行下列命令來擷取憑證簽發者和指紋值：</p>
<p>Get-CsCertificate | Select-Object Issuer, Thumbprint。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsWebTrustedCACertificate** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsWebTrustedCACertificate** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.Web.CACertID 物件的新執行個體。

## 請參閱

#### 其他資源

[New-CsWebServiceConfiguration](new-cswebserviceconfiguration.md)  
[Set-CsWebServiceConfiguration](set-cswebserviceconfiguration.md)

