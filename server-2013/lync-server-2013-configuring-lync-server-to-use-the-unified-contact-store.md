---
title: 設定 Microsoft Lync Server 2013 使用整合連絡人存放區
TOCTitle: 設定 Microsoft Lync Server 2013 使用整合連絡人存放區
ms:assetid: 6aa17ae3-764e-4986-a900-85a3cdb8c1fc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688083(v=OCS.15)
ms:contentKeyID: 49890104
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定 Microsoft Lync Server 2013 使用整合連絡人存放區

 

_**上次修改主題的時間：** 2014-02-07_

整合連絡人存放區可讓使用者保有單一連絡人清單，然後讓那些連絡人可於多個應用程式中使用，包括 Microsoft Lync 2013、Microsoft Outlook 2013 和 Microsoft Outlook Web App 2013。當您啟用使用者的整合連絡人存放區時，該使用者的連絡人並非儲存於 Microsoft Lync Server 2013 並使用 SIP 通訊協定來擷取。實際上，其連絡人會儲存於 Microsoft Exchange Server 2013 並使用 Exchange Web 服務來擷取。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在技術上，連絡人資訊儲存於一組資料夾，這些資料夾位於使用者的 Exchange 2013 信箱中。連絡人本身儲存在名為 Lync Contacts 的資料夾中，使用者可看到該資料夾；有關連絡人的中繼資料則儲存在使用者無法看到的子資料夾。</td>
</tr>
</tbody>
</table>


## 針對使用者啟用整合連絡人存放區

如果您已經設定 Lync Server 2013 和 Exchange 2013 之間的伺服器對伺服器驗證，則您也會啟用整合連絡人存放區的使用，而無需設定其他伺服器。不過，要將使用者的連絡人移動至整合連絡人存放區，則需設定其他使用者帳戶。根據預設，使用者連絡人會保存在 Lync Server 而非整合連絡人存放區中。

整合連絡人存放區的存取權使用 Lync Server 使用者服務原則來管理。使用者伺服器原則僅有單一屬性 (UcsAllowed)；此屬性用於決定使用者的連絡人所儲存的位置。如果使用者受使用者服務原則管理，而原則中 UcsAllowed 已設為 True ($True)，則使用者的連絡人會儲存在整合連絡人存放區中。如果使用者受使用者服務原則管理，而原則中 UcsAllowed 已設為 False ($False)，則其連絡人會儲存在 Lync Server 中。

當您安裝 Lync Server 2013 時，單一使用者服務原則 (已在全域範圍設定) 也會一併安裝。原則中的 UcsAllowed 值會設為 True，代表使用者連絡人會儲存於統一連絡人存放區 (假設這已經部署及設定)。如果您想要將所有使用者連絡人移轉至統一連絡人存放區，您無須執行任何動作。

如果您不想將所有連絡人移轉至統一連絡人存放區，您可以將全域原則中的 UcsAllowed 屬性設為 False，為所有使用者停用統一連絡人存放區：

    Set-CsUserServicesPolicy -Identity global -UcsAllowed $False

當您在全域規則中停用統一連絡人存放區之後，您可以建立可啟用統一連絡人存放區使用的個別使用者原則；這樣可讓您部分使用者將其連絡人保存於整合連絡人存放區中，同時，其他連絡人則繼續將其連絡人保存於 Lync Server 中。您可以使用類似以下的命令來建立個別使用者的使用者服務原則：

    New-CsUserServicesPolicy -Identity "AllowUnifiedContactStore" -UcsAllowed $True

在您建立新原則之後，接著您必須將該原則指派給應擁有整合連絡人存放區存取權的任何使用者。您可使用類似以下的命令，將個別使用者原則指派給使用者：

    Grant-CsUserServicesPolicy -Identity "Ken Myer" -PolicyName "AllowUnifiedContactStore"

指派原則之後，Lync Server 會開始將使用者的連絡人移轉至整合連絡人存放區。完成移轉後，使用者的連絡人就會儲存在 Exchange，而非 Lync Server 中。如果使用者碰巧在移轉正在完成時登入 Lync 2013，就會顯示訊息方塊並要求使用者登出 Lync，然後重新登入以完成程序。尚未獲指派此個別使用者原則的使用者不會將其連絡人移轉至統一連絡人存放區。這是因為這些使用者受全域原則管理，而全域原則中已停用對於統一連絡人存放區的使用。

您可以從Lync Server 管理命令介面內部執行 [Test-CsUnifiedContactStore](https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsUnifiedContactStore) Cmdlet 以確認使用者的連絡人是否已成功移轉至整合連絡人存放區。

    Test-CsUnifiedContactStore -UserSipAddress "sip:kenmyer@litwareinc.com" -TargetFqdn "atl-cs-001.litwareinc.com"

如果 Test-CsUnifiedContactStore 成功，就代表使用者 sip:kenmyer@litwareinc.com 的連絡人已經移轉至整合連絡人存放區。

## 復原連絡人存放區

如果您需從整合連絡人存放區移動使用者的連絡人 (例如，如果使用者需重新放置到 Microsoft Lync Server 2010 上，而因此無法再使用整合連絡人存放區)，您就必須執行兩項作業。 首先，您必須將新的使用者服務原則指派給使用者，該原則須禁止將連絡人儲存於整合連絡人存放區中 (即原則中的 UcsAllowed 屬性已設為 $False)。如果您沒有此類的原則，您可使用類似以下的命令來建立原則：

    New-CsUserServicesPolicy -Identity NoUnifiedContactStore -UcsAllowed $False

然後您可使用如下命令來指派這個新的個別使用者原則 (NoUnifiedContactStore)：

    Grant-CsUserServicesPolicy -Identity "Ken Myer" -PolicyName NoUnifiedContactStore

上述命令會將新原則指派給使用者 Ken Myer，同時也會防止 Ken 的連絡人移轉至整合連絡人存放區。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在某些情況下，您可以單單解除指派使用者的目前使用者服務原則達到相同的整體效果。例如，假設 Ken Myer 擁有個別使用者的使用者服務原則，該原則可啟用整合連絡人存放區，但是您的全域原則禁止整合連絡人存放區的使用。在該情況下，您可以解除指派 Ken 的個別使用者服務原則。當您那樣做時，Ken 會自動受全域原則管理，因此不再有整合連絡人存放區的存取權。<br />
若要解除指派先前所指派的個別使用者原則，請使用如前所示的相同命令，但這次需將 PolicyName 參數設為 Null 值：<br />
Grant-CsUserServicesPolicy –識別 &quot;Ken Myer&quot; –PolicyName $Null</td>
</tr>
</tbody>
</table>


在處理整合連絡人存放區時，須牢記「防止 Ken 的連絡人移轉至整合連絡人存放區」這個術語。單單將新的使用者服務原則指派給 Ken 並不會將其連絡人從整合連絡人存放區移出。當使用者登入 Lync Server 2013 時，系統會檢查使用者的使用者服務原則，以決定是否應將其連絡人保存於整合連絡人存放區中。如果結果為肯定 (也就是說，如果 UcsAllowed 屬性設為 $True)，那些連絡人就會移轉至整合連絡人存放區 (假設那些連絡人尚未存放在整合連絡人存放區)。如果結果為否定，Lync Server 就會忽略使用者的連絡人並移至下一個工作。這表示無論 UcsAllowed 屬性的值為何，Lync Server 皆不會從整合連絡人存放區之外移動使用者的連絡人。

這也表示，在將新的使用者服務原則指派給使用者後，接著您必須執行 [Invoke-CsUcsRollback](invoke-csucsrollback.md) Cmdlet 才能將使用者的連絡人移出 Exchange 2013 ，然後再移回 Lync Server 2013。例如，在將新的使用者服務原則指派給 Ken Myer 之後，您就可以使用下列命令將其連絡人移出整合連絡人存放區：

    Invoke-CsUcsRollback -Identity "Ken Myer"

果您變更使用者服務原則，但是未執行 Invoke-CsUcsRollback Cmdlet，Ken 的連絡人就不會從整合連絡人存放區移除。如果您執行 Invoke-CsUcsRollback，但未變更 Ken Myer 的使用者服務原則，會有什麼結果呢？在這種情況下，Ken 的連絡人會暫時從整合連絡人存放區中遭移除。您務必牢記此移除作業為暫時性的。在 Ken 的連絡人從整合連絡人存放區移除後，Lync Server 2013 會等待 7 天，然後進行檢查，以查看哪個使用者服務原則已指派給 Ken。如果指派給 Ken 的原則仍然可啟用整合來連絡人存放區，其連絡人就會自動移回連絡人存放區。若要將連絡人從整合連絡人存放區永久移除，除了執行 Invoke-CsUcsRollback Cmdlet 之外，您還必須變更使用者服務原。

由於可能會有大量變數影響移轉，因此很難估算需要花多少時間才能將帳戶完全移轉至統一連絡人存放區。但是，就一般規則而言，移轉並不會立即生效：即使當移轉少數連絡人時，也可能要花 10 分鐘或更多的時間才能完成移動。

