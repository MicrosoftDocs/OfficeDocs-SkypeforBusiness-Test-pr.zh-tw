---
title: Windows PowerShell 與 Lync Online 的簡介
TOCTitle: Windows PowerShell 與 Lync Online 的簡介
ms:assetid: 4b4cf534-c950-4d6c-abd9-d3d0e6f53bb7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362785(v=OCS.15)
ms:contentKeyID: 56269085
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Windows PowerShell 與 Lync Online 的簡介

 

_**上次修改主題的時間：** 2015-06-22_

Windows PowerShell 是命令殼層與指令碼語言，可用於管理 商務用 Skype Online。除了使用 商務用 Skype Online 系統管理中心畫面管理 商務用 Skype Online，您還可以使用類似以下的命令列命令管理該產品：

    Get-CsOnlineUser -Identity "kenmyer@litwareinc.com"

除了執行上述範例 (傳回 UPN 為 kenmyer@litwareinc.com 之使用者的相關資訊) 之類的簡單命令外，熟悉 Windows PowerShell 的使用者亦可將這些命令組織為指令碼。這些指令碼可將程序自動化及/或執行重複工作。

一般而言，任何可使用 商務用 Skype Online 系統管理中心執行的工作亦可使用 Windows PowerShell 執行。例如，您可以使用系統管理中心管理行動電話通知 (亦稱為「推播通知」。推播通知可讓您將事件相關通知，例如新的立即訊息或新的語音留言，傳送至 iPhone 與 Windows Phone 等行動裝置。即使行動裝置上的那些 Lync 應用程式是在背景執行，那些裝置同樣也能收到通知。

若要管理推播通知，其中一種方法是使用 商務用 Skype Online 系統管理中心，從 \[組織\] 索引標籤選取適當選項，以啟用或停用推播通知：

![LyncOnlinePowerShell\_Push\_Notifications](images/Dn362807.0a6ec1f5-1999-427f-880b-0587c98d7670(OCS.15).png "LyncOnlinePowerShell_Push_Notifications")

您亦可使用遠端 Windows PowerShell 工作階段與 [Set-CsPushNotificationConfiguration](set-cspushnotificationconfiguration.md) Cmdlet 來啟用或停用推播通知。例如，下列命令會停用 iPhone 與 Windows Phone 的推播通知：

    Set-CsPushNotificationConfiguration -EnableApplePushNotificationService $False -EnableMicrosoftPushNotificationService $False

如您所見，與 **Set-CsPushNotificationConfiguration** Cmdlet 搭配使用的參數 (即 EnableApplePushNotificationService 與 EnableMicrosoftPushNotificationService) 可對應至 商務用 Skype Online 系統管理中心中提供的選項：

![Lync 選項 / PS Cmdlet 之間顯示的關聯](images/Dn362785.f20086fd-3b51-4bbf-8d81-e643d9bf3a2e(OCS.15).png "Lync 選項 / PS Cmdlet 之間顯示的關聯")

總而言之，系統管理中心或 Windows PowerShell Cmdlet 搭配適當參數均可用於管理推播通知。這兩種途徑皆可行且同樣有效。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需特定 Windows PowerShell 詞彙的定義，例如 <em>Cmdlet</em>、「參數」、「參數值」及「引數」，請參閱<a href="windows-powershell-cmdlets-parameters-and-parameter-values-in-skype-for-business-online.md">Windows PowerShell Cmdlet、參數，以及參數值</a>。</td>
</tr>
</tbody>
</table>


這突顯出一個問題：如果 商務用 Skype Online 系統管理中心與 Windows PowerShell 提供的功能完全相同，在選擇時要如何做出取捨？也就是說，為何要選擇在 Windows PowerShell 中輸入命令，而非直接在系統管理中心中選取或清除核取方塊？

在先前範例之類的單純狀況下，決定採用哪個方法取決於個人偏好：有些偏好使用圖形化使用者介面，有些則偏好命令列工具，例如 Windows PowerShell。然而，在部分案例中，Windows PowerShell 是執行管理工作最為有效的方法或唯一的方法。例如 商務用 Skype Online 系統管理中心可讓您自訂會議邀請：

![Lync 管理中心會議邀請設定](images/Dn362785.3fb00c33-0bd4-46dd-beb1-8f71e24cf630(OCS.15).png "Lync 管理中心會議邀請設定")

您可使用 [Set-CsMeetingConfiguration](set-csmeetingconfiguration.md) Cmdlet 進行相同的自訂作業。然而，**Set-CsMeetingConfiguration** Cmdlet 另外亦提供 商務用 Skype Online 系統管理中心所沒有的選項。例如，若是組織中有人加入會議，根據預設，系統會將這些人員自動設為會議簡報者。這項設定無法使用 商務用 Skype Online 系統管理中心變更，而僅能使用 Windows PowerShell 與 **Set-CsMeetingConfiguration** Cmdlet 來變更。明確的說，這項命令會將 DesignateAsPresenter 屬性設為 \[無\]，代表只有會議召集人在加入會議時才設為簡報者：

    Set-CsMeetingConfiguration -DesignateAsPresenter "Everyone"

如需更多有關使用 Windows PowerShell 的詳細資訊，請參閱下列主題：

  - [Windows PowerShell Cmdlet、參數，以及參數值](windows-powershell-cmdlets-parameters-and-parameter-values-in-skype-for-business-online.md)

  - [使用參數](working-with-parameters-in-skype-for-business-online.md)

  - [強制參數與選擇性參數](mandatory-and-optional-parameters-in-skype-for-business-online.md)

  - [參數 vs. 屬性](parameters-vs-properties-in-skype-for-business-online.md)

  - [結合 Lync Online Cmdlet 與其他 Windows PowerShell Cmdlet](combining-skype-for-business-online-cmdlets-with-other-windows-powershell-cmdlets-in.md)

  - [使用 Windows PowerShell 的詳細說明](more-help-for-using-windows-powershell-in-skype-for-business-online.md)

