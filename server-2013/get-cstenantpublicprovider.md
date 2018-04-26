---
title: Get-CsTenantPublicProvider
TOCTitle: Get-CsTenantPublicProvider
ms:assetid: 0d949ec2-206d-4979-a3be-a5578ae93ed3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994016(v=OCS.15)
ms:contentKeyID: 52056050
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantPublicProvider

 

_**上次修改主題的時間：** 2015-03-09_

傳回資訊以指出 Microsoft Lync Online 使用者是否可與在協力廠商 IM 及目前狀態提供者 Windows Live、AOL 和 Yahoo 上擁有帳戶的人員通訊。

此 Cmdlet 僅可與 商務用 Skype Online 搭配使用。

## 語法

    Get-CsTenantPublicProvider -Tenant <String> [-Verbose]

## 範例

## 範例 1

範例 1 所示的命令會針對租用戶識別碼為 "bf19b7db-6960-41e5-a139-2aa373474354" 的租用戶傳回公用提供者資訊。

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

請注意，Tenant 參數是選用的。您也可以使用下列語法呼叫 Get-CsTenantPublicProvider：

    Get-CsTenantPublicProvider

## 範例 2

上述命令會傳回指派給租用戶 bf19b7db-6960-41e5-a139-2aa373474354 之所有公用提供者的狀態詳細資訊。為達成此目的，命令會先使用 **Get-CsTenantPublicProvider** Cmdlet 傳回指定租用戶的公用提供者資訊。然後，該資訊會以管道方式傳送到 **Select-Object** Cmdlet，而此 Cmdlet 會使用 ExpandProperty 參數「展開」DomainPICStatus 屬性的值。展開屬性的意思只是會以易讀的格式在畫面顯示該屬性中儲存的所有值。

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty DomainPICStatus

像這樣於的命令會用於 Lync Server 2013 的混合式部署。

## 範例 3

範例 3 所示的命令是範例 2 中命令的變化。不過在範例 3 中，「展開」DomainPICStatus 屬性值後傳回的公用提供者資訊，會接著以管道方式傳送到 **Where-Object** Cmdlet。**Where-Object** Cmdlet 接下來只會挑出 Status 屬性設為 Enabled 的提供者。結果是僅顯示已啟用供人員使用的公用提供者。

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty DomainPICStatus | Where-Object {$_.Status -eq "Enabled"}

## 詳細描述

公用提供者是為大眾提供 SIP 通訊服務的組織。當您與公用提供者建立同盟關係時，實際上是與擁有該提供者所提供帳戶的所有使用者建立同盟。例如，如果您與 Windows Live 結盟，您的使用者便能夠與任何具有 Windows Live 立即訊息帳戶的使用者交換立即訊息和目前狀態資訊。

Lync Online 可讓系統管理員選擇與下列一或多個公用 IM 和目前狀態提供者設定同盟：

  - Windows Live

  - AOL

  - Yahoo\!

系統管理員可使用 **Get-CsTenantPublicProvider** Cmdlet 來判定已針對同盟啟用了哪些提供者 (若有的話)。當您呼叫 **Get-CsTenantPublicProvider** Cmdlet 時，會取得以下類似資訊：

    PublicProviderSet     DomainPicStatus
    ------------------    ------------------------
    True                  {Microsoft.Rtc.Management.Hosted.DomainPICStatus}

PublicProviderSet 屬性指出是否已為一或多個公用提供者啟用同盟。如果 PublicProviderSet 等於 True，則表示至少與一名提供者啟用同盟；若 PublicProviderSet 等於 False，則表示停用全部三個公用提供者 (Windows Live、AOL 和 Yahoo) 的同盟。若要判定每個提供者的實際狀態，請使用此命令：

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty DomainPICStatus

請注意，若僅啟用公用提供者的狀態，不代表使用者就可與在該提供者上擁有帳戶的使用者交換立即訊息和目前狀態資訊。除了要與提供者本身締結同盟外，系統管理員也必須將同盟組態設定的 AllowPublicUsers 屬性設為 True。若將此屬性設為 False，則不論公用提供者的組態設定為何，您都無法與任何公用提供者通訊。

如需詳細資訊，請參閱 **Set-CsTenantFederationConfiguration** Cmdlet 的說明主題。

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
<td><p><em>Tenant</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要傳回公用提供者設定之租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>如果您正在使用 Windows PowerShell 的遠端工作階段，並且僅連線至 商務用 Skype Online，您不需要包含 Tenant 參數，而是將會根據您的連線資訊自動填入租用戶 ID。Tenant 參數主要用於混合部署。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsTenantPublicProvider** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsTenantPublicProvider** Cmdlet 會傳回 Microsoft.Rtc.Management.Hosted.TenantPICStatus 物件的執行個體。

## 請參閱

#### 其他資源

[Set-CsTenantPublicProvider](set-cstenantpublicprovider.md)

