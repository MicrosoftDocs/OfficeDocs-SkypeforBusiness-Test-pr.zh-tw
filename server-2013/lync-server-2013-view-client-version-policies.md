---
title: 檢視用戶端版本原則
TOCTitle: 檢視用戶端版本原則
ms:assetid: 6cd9a897-c694-4d6a-8259-2d3c01fce275
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ898479(v=OCS.15)
ms:contentKeyID: 52056147
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視用戶端版本原則

 

_**上次修改主題的時間：** 2013-02-23_

用戶端版本原則用於套用一組全域的用戶端版本設定規則，或用於特殊網站、集區，或使用者群組。您可以從 Lync Server 2013 控制台或 Lync Server 2013 管理命令介面檢視已在 Lync Server 2013 環境中設定的用戶端版本原則。

## 使用 Lync Server 控制台檢視用戶端版本原則

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列，按一下 \[用戶端\]，然後按一下 \[用戶端版本原則\] 導覽按鈕。

4.  如果您想要檢視用戶端版本原則的規則，請在「用戶端版本原則」頁面中，按兩下您想要檢視的原則。

## 使用 Windows PowerShell Cmdlet 檢視用戶端版本原則

您可以使用 **Get-CsClientVersionPolicy** Cmdlet 來檢視用戶端版本原則。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段來執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 檢視用戶端版本原則

  - 若要檢視所有用戶端版本原則的相關資訊，請在 Lync Server 管理命令介面輸入下列命令，然後按 ENTER：
    
        Get-CsClientVersionPolicy
    
    隨即傳回類似下列的資訊：
    
        Identity    : Global
        Rules       : {RuleId=2336c611-a243-4c5d-994b-eea8a524d0e4;
                      Description=;Action=Block;ActionUrl=;MajorVersion=1;
                      MinorVersion=3;BuildNumber=;QfeNumber=;
                      UserAgent=RTC;UserAgentFullName=;Enabled=True;
                      CompareOp=LEQ, RuleId=342c9b90-4cef-483a-a73a-
                      4fe75c88711d;Description=;Action=Block;ActionUrl=;
                      MajorVersion=5;MinorVersion=;BuildNumber=;QfeNumber=;
                      UserAgent=WM;UserAgentFullName=;Enabled=True;
                      CompareOp=LEQ,RuleId=ea03af61-9db5-4bf9-af3f-042
                      ab8dd9994;Description=;Action=Block;ActionUrl=;
                      MajorVersion=3;MinorVersion=5;BuildNumber=6907;
                      QfeNumber=83;UserAgent=OC;UserAgentFullName=;
                      Enabled=True;CompareOp=LEQ, RuleId=831edb68-
                      e482-4431-a10e-add365ba8099;Description=;
                      Action=Block;ActionUrl=;MajorVersion=2;MinorVersion=0;
                      BuildNumber=5999;QfeNumber=;UserAgent=UCCP;
                      UserAgentFullName=;Enabled=True;CompareOp=LEQ...}
        Description :

如需詳細資訊，請參閱 [Get-CsClientVersionPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsClientVersionPolicy) Cmdlet 的說明主題。

