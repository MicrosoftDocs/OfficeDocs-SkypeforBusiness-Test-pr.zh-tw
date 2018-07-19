---
title: 在 Lync Server 2013 中檢視電腦上執行之服務的狀態
TOCTitle: 在 Lync Server 2013 中檢視電腦上執行之服務的狀態
ms:assetid: f41918e7-4c02-431e-840a-88a1f36ae499
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182606(v=OCS.15)
ms:contentKeyID: 49292808
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中檢視電腦上執行之服務的狀態

 

_**上次修改主題的時間：** 2013-02-22_

您可以使用 Lync Server 2013 控制台來檢視 Lync Server 拓撲中特定電腦上執行的所有服務，並查看每個服務的狀態。

## 若要檢視電腦上執行的服務狀態

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[拓撲\]。

4.  在 \[狀態\] 頁面上，視需要排序或搜尋清單以找出您所要的電腦，然後按一下電腦名稱。

5.  執行下列任一項作業：
    
      - 若要查看電腦上執行之服務的最新狀態，請按一下 \[取得服務狀態\]。
    
      - 若要查看電腦上執行之特定服務清單，以及每項服務的狀態，請按一下 \[內容\]，然後按一下 \[關閉\] 以返回清單。

## 使用 Lync Server 管理命令介面 Cmdlet 檢視服務狀態

您也可使用 Lync Server 管理命令介面 與 **Get-CsWindowsService** Cmdlet 檢視服務狀態。也可從 Lync Server 2013 管理命令介面 或 Windows PowerShell 的 如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。 的遠端工作階段執行此 Cmdlet。

## 檢視服務狀態

  - 若要檢視電腦中的服務狀態，請輸入與 Lync Server 管理命令介面 中相似的下列命令，然後按 ENTER 鍵：
    
        Get-CsWindowsService -ComputerName atl-cs-001.litwareinc.com | Select-Object RoleName, Status
    
    此命令會傳回與下列相似的資訊：
    
        RoleName                                  Status
        --------                                  ------
        {W3SVC}                                   Running
        {CentralManagement}                       Running
        {ClsAgent}                                Running
        {Registrar, UserServer, EdgeServer}       Running
        {ApplicationServer}                       Running
        {ConferencingServer}                      Running
        {MediationServer}                         Running

如需詳細資訊，請參閱[Get-CsWindowsService](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsWindowsService)。

## 請參閱

#### 其他資源

[在 Lync Server 2013 中管理裝置、電話及用戶端應用程式](lync-server-2013-managing-devices-phones-and-client-applications.md)

