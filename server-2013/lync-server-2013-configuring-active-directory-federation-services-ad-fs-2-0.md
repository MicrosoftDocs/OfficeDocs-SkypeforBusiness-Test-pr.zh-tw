---
title: 設定 Active Directory Federation Services (AD FS 2.0)
TOCTitle: 設定 Active Directory Federation Services (AD FS 2.0)
ms:assetid: 0ba8657f-55b8-41b3-960c-fdc5eeee6978
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn308561(v=OCS.15)
ms:contentKeyID: 56269060
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 配置 Active Directory 联合身份验证服务 (AD FS 2.0)
 

_**上次修改主題的時間：** 2013-07-03_

下節說明如何設定 Active Directory Federation Service (AD FS 2.0) 以支援多重因素驗證。如需有關如何安裝 AD FS 2.0 的資訊，請參閱《AD FS 2.0 逐步指南》(英文)，網址為：[http://go.microsoft.com/fwlink/p/?LinkId=313374](http://go.microsoft.com/fwlink/p/?linkid=313374)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>安裝 AD FS 2.0 時，請勿使用 Windows 伺服器管理員新增 Active Directory Federation Service 角色。請改為下載並安裝此處的 Active Directory Federation Services 2.0 RTW 套件，網址為：<a href="http://go.microsoft.com/fwlink/p/?linkid=313375">http://go.microsoft.com/fwlink/p/?LinkId=313375</a>。</td>
</tr>
</tbody>
</table>



**設定 AD FS 以支援雙因素驗證**

1.  使用網域管理員帳戶登入 AD FS 2.0 電腦。

2.  啟動 Windows PowerShell。

3.  從 Windows PowerShell 命令列中，執行下列命令：
    
        add-pssnapin Microsoft.Adfs.PowerShell

4.  執行下列命令，取代您部署中的特定伺服器名稱，與每個將啟用被動式驗證且具備 Lync Server 2013 累計更新 (2013 年 7 月) 的 Lync Server 2013 Director、Enterprise 集區和 Standard Edition 伺服器建立合作關係：
    
        Add-ADFSRelyingPartyTrust -Name LyncPool01-PassiveAuth -MetadataURL https://lyncpool01.contoso.com/passiveauth/federationmetadata/2007-06/federationmetadata.xml

5.  從 \[系統管理工具\] 功能表，啟動 AD FS 2.0 管理主控台。

6.  展開 **\[信任關係\]** \> **\[信賴憑證者信任\]**。

7.  確認已為具備 Lync Server 2013 累計更新 (2013 年 7 月) 的 Lync Server 2013 Enterprise 集區或 Standard Edition 伺服器建立新的信任。

8.  執行下列命令，使用 Windows PowerShell 為信賴憑證者信任建立並指派發行授權規則：
    
      ```
      $IssuanceAuthorizationRules = '@RuleTemplate = "AllowAllAuthzRule" => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");'
      ```
      ```
      Set-ADFSRelyingPartyTrust -TargetName LyncPool01-PassiveAuth 
      -IssuanceAuthorizationRules $IssuanceAuthorizationRules
      ```


9.  執行下列命令，使用 Windows PowerShell 為信賴憑證者信任建立並指派發行轉換規則：
    
      ```
      $IssuanceTransformRules = '@RuleTemplate = "PassThroughClaims" @RuleName = "Sid" c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"]=> issue(claim = c);'
      ```
      ```
      Set-ADFSRelyingPartyTrust -TargetName LyncPool01-PassiveAuth -IssuanceTransformRules $IssuanceTransformRules
      ```

10. 從 AD FS 2.0 管理主控台，在信賴憑證者信任上按一下滑鼠右鍵並選取 **\[編輯宣告規則\]**。

11. 選取 **\[發行授權規則\]** 標籤並確認新的授權規則已成功建立。

12. 選取 **\[發行轉換規則\]** 標籤並確認新的轉換規則已成功建立。

