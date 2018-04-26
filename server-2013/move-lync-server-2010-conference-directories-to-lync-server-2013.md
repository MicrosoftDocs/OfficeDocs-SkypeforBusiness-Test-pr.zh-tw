---
title: 將 Lync Server 2010 會議目錄移至 Lync Server 2013
TOCTitle: 移動會議目錄
ms:assetid: 659867e0-ce91-4a95-9787-b1c1566460a8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn727126(v=OCS.15)
ms:contentKeyID: 62388497
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移動會議目錄

 

_**上次修改主題的時間：** 2014-05-28_

在解除委任集區前，您必須針對 Lync Server 2010 中的每個會議目錄執行下列程序。

## 將會議目錄移至 Lync Server 2013

1.  開啟 Lync Server 管理命令介面。

2.  若要取得組織中會議目錄的識別資料，請執行下列命令：
    
        Get-CsConferenceDirectory
    
    前一個命令會傳回組織中的所有會議目錄。所以您可能會想要將結果限定在正在解除委任的集區。例如，如果解除委任完整網域名稱 (FQDN) 為 pool01.contoso.net 的集區，請使用此命令來限制將資料傳回至該集區的會議目錄：
    
        Get-CsConferenceDirectory | Where-Object {$_.ServiceID -match "pool01.contoso.net"}
    
    該命令只會傳回內含 FQDN pool01.contoso.net 之 ServiceID 屬性的會議目錄。

3.  若要移動會議目錄，請針對集區中的每個會議記錄執行下列命令：
    
        Move-CsConferenceDirectory -Identity <Numeric identity of conference directory> -TargetPool <FQDN of pool where ownership is to be transitioned>
    
    例如，若要使用此命令移動會議目錄 3，請將 Lync Server 2013 集區指定為 TargetPool：
    
        Move-CsConferenceDirectory -Identity 3 -TargetPool "pool02.contoso.net"
    
    若要移動集區上的所有會議目錄，請使用以下的類似命令：
    
        Get-CsConferenceDirectory | Where-Object {$_.ServiceID -match "pool01.contoso.net"} | Move-CsConferenceDirectory -TargetPool "pool02.contoso.net"

如需解除委任 Lync 2010 集區的完整、逐步指示，請參閱《解除安裝 Microsoft Lync Server 2010 和移除伺服器角色》文件 (可從 [http://go.microsoft.com/fwlink/p/?linkId=246227](http://go.microsoft.com/fwlink/p/?linkid=246227) 下載)。

移動會議目錄時可能會遇到下列錯誤：

    WARNING: Move operation failed for conference directory with ID "5". Cannot perform a rollback because data migration might have already started. Retry the operation.
    WARNING: Before using the -Force parameter, ensure that you have exported the conference directory data using DBImpExp.exe and imported the data on the target pool. Refer to the DBImpExp-Readme.htm file for more information.
    Move-CsConferenceDirectory : Unable to cast COM object of type 'System._ComObject' to interface type 'Microsoft.Rtc.Interop.User.IRtcConfDirManagement'. 
    This operation failed because the QueryInterface call on the COM component for the interface with SID '{4262B886-503F-4BEA-868C-04E8DF562CEB}' failed due to the following error: The specified module could not be found.

此錯誤一般是在 Lync Server 管理命令介面 要求更新的 Active Directory 權限集以便完成工作時所發生。若要解決問題，請關閉目前的管理命令介面執行個體，然後開啟命令介面的新執行個體並重新執行命令，以便移動會議目錄。

