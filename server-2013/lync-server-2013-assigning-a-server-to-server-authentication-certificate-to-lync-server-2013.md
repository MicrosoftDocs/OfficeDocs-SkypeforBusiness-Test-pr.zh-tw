---
title: 將伺服器對伺服器驗證憑證指派給 Microsoft Lync Server 2013
TOCTitle: 將伺服器對伺服器驗證憑證指派給 Microsoft Lync Server 2013
ms:assetid: c7413954-2504-47f4-a073-44548aff1c0c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205253(v=OCS.15)
ms:contentKeyID: 49292269
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將伺服器對伺服器驗證憑證指派給 Microsoft Lync Server 2013

 

_**上次修改主題的時間：** 2013-10-24_

若要判斷某個伺服器對伺服器的驗證憑證是否已被指派給 Microsoft Lync Server 2013，請從 Lync Server 2013 管理命令介面執行下列命令：

    Get-CsCertificate -Type OAuthTokenIssuer

如果如此並未傳回任何憑證資訊，您必須先指派權仗簽發者憑證，然後才能使用伺服器對伺服器驗證。一般的規則是，任何 Lync Server 2013 憑證都能當成 OAuthTokenIssuer 憑證使用；例如，您的 Lync Server 2013 預設憑證也可以當成 OAuthTokenIssuer 憑證使用。(OAUthTokenIssuer 憑證也可以是任何在主旨欄位包含您 SIP 網域名稱的 Web 伺服器憑證。) 伺服器對伺服器驗證所用的憑證有兩項主要的需求：1) 相同的憑證必須設定在所有前端伺服器上做為 OAuthTokenIssuer 憑證；2) 憑證必須至少有 2048 個位元。

如果您沒有憑證可用於伺服器對伺服器驗證，可以取得新的憑證、匯入新的憑證，然後將該憑證用於伺服器對伺服器驗證。在索取到新的憑證之後，您可以登入任何一部前端伺服器，並使用類似如下的 Windows PowerShell 命令來匯入並指派該憑證：

    Import-CsCertificate -Identity global -Type OAuthTokenIssuer -Path C:\Certificates\ServerToServerAuth.pfx  -Password "P@ssw0rd"

在上述的命令中，Path 參數代表憑證檔的完整路徑，而 Password 參數則代表已指派給該憑證的密碼。此程序應該只執行一次：Lync Server 的複寫服務接著會自動建立一組排程的工作，來將憑證解密並部署到所有的前端伺服器上。

您也可以將現有的憑證當成伺服器對伺服器驗證憑證使用。(如前所述，預設的憑證可當成伺服器對伺服器驗證憑證使用。) 下列這對 Windows PowerShell 命令會擷取預設憑證上 Thumbprint 屬性的值，然後使用該值讓預設憑證成為伺服器對伺服器驗證憑證：

    $x = (Get-CsCertificate -Type Default).Thumbprint
    Set-CsCertificate -Identity global -Type OAuthTokenIssuer -Thumbprint $x

在上述的命令中，擷取的憑證會被設做全域的伺服器對伺服器驗證憑證；這表示憑證將會複寫到所有的前端伺服器並供其使用。同樣地，此命令應該只執行一次，並且只在其中一部前端伺服器上執行。雖然所有的前端伺服器都必須使用相同的憑證，但您不應該在每部前端伺服器上都設定 OAuthTokenIssuer 憑證。取而代之的是，請設定一次憑證，然後讓 Lync Server 的複寫伺服器負責將該憑證複製到每部伺服器。

Set-CsCertificate Cmdlet 會收下該憑證，並立即設定該憑證擔任目前的 OAuthTokenIssuer 憑證。(Lync Server 2013 保留兩份憑證類型：目前的憑證和先前的憑證。) 如果您需要新憑證立即開始擔任 OAuthTokenIssuer 憑證，則應該使用 Set-CsCertificate Cmdlet。

您也可以使用 Set-CsCertificate Cmdlet「預訂」新的憑證。「預訂」憑證的意思就是您將新憑證設定在指定的時間點成為目前的 OAuthTokenIssuer 憑證。例如，此命令會擷取預設憑證，然後設定該憑證在 2012 年 7 月 1 日接手成為目前的 OAuthTokenIssuer 憑證：

    $x = (Get-CsCertificate -Type Default).Thumbprint
    Set-CsCertificate -Identity global -Type OAuthTokenIssuer -Thumbprint $x -EffectiveDate "7/1/2012" -Roll

在 2012 年 7 月 1 日時，新的憑證會被設做目前的 OAuthTokenIssuer 憑證，而舊的 OAuthTokenIssuer 憑證則會被設做先前的憑證。

如果您不想使用 Windows PowerShell，也可以使用 \[憑證\] MMC 主控台從某部前端伺服器中匯出憑證，然後在所有其他前端伺服器上匯入該憑證。如果這麼做，請務必將私密金鑰隨著憑證本身一起匯出。

> [!CAUTION]
> 在此情況下，您必須在每部前端伺服器上執行此程序。以此方式匯出再匯入憑證時，Lync Server 2013 並不會將該憑證複寫到每部前端伺服器。


將憑證匯入到所有前端伺服器之後，便可以使用 \[Lync Server 部署精靈\] (而不是使用 Windows PowerShell) 指派該憑證。若要使用 \[部署精靈\] 指派憑證，請在已安裝 \[部署精靈\] 的電腦上完成下列步驟：

1.  依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\]，然後按一下 \[Lync Server 部署精靈\]。

2.  在 \[部署精靈\] 中按一下 \[安裝或更新 Lync Server 系統\]。

3.  在 Microsoft Lync Server 2013 頁面上按一下標題 \[步驟 3：要求、安裝或指派憑證\] 下的 \[執行\] 按鈕。(請注意，如果您已在此電腦上安裝憑證，則 \[執行\] 按鈕的標籤將為 \[再執行一次\]。)

4.  在 \[憑證精靈\] 中選取 \[OAuthTokenIssuer\] 憑證，然後按一下 \[指派\]。

5.  在 \[憑證指派精靈\] 的 \[憑證指派\] 頁面上，按 \[下一步\]。

6.  在 \[憑證存放區\] 頁面上，選取要用於伺服器對伺服器驗證的憑證，然後按 \[下一步\]。

7.  在 \[憑證指派摘要\] 頁面上，按 \[下一步\]。

8.  在 \[執行命令\] 頁面上，按一下 \[完成\]。

9.  關閉 \[憑證精靈\] 及 \[部署精靈\]。

