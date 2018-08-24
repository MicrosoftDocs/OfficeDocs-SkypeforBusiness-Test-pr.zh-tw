---
title: Lync Server 2013：建立或修改代理人群組
TOCTitle: 建立或修改代理人群組
ms:assetid: f1461fff-51c1-4f4b-9311-8cba02c333fc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205370(v=OCS.15)
ms:contentKeyID: 49292779
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立或修改代理人群組

 

_**上次修改主題的時間：** 2014-02-07_

使用下列任一個程序建立或修改代理程式群組。

> [!NOTE]  
> 系統管理員 (例如 CsVoiceAdministrator) 必須先啟用使用者的企業語音與 Lync Server，才能將使用者指派至代理群組。如果您是其中一位受管理工作流程的委派「回應群組管理員」，即可建立代理群組，並在您所管理的工作流程中使用代理群組。



> [!IMPORTANT]  
> 當您將使用者指派為回應群組代理程式時，如果他們已啟用隱私權模式，請通知他們需要搜尋 &quot;RGS Presence Watcher&quot; 連絡人並將他們新增到其連絡人清單。已啟用隱私權模式但其連絡人清單中沒有 &quot;RGS Presence Watcher&quot; 的代理程式，無法接聽打給回應群組的電話。未啟用隱私權模式的代理程式則不受影響。



## 使用 Lync Server 控制台 建立或修改代理人群組

1.  以 RTCUniversalServerAdmins 群組成員或支援回應群組的某個預先定義之管理角色成員的身分登入。
    
    > [!NOTE]  
    > 如果您是其中一位受管理工作流程的委派「回應群組經理」，即可建立群組，並在管理的工作流程中使用這些群組。
    


2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[回應群組\] ，然後按一下 \[群組\] 。

4.  在 \[群組\] 頁面上，執行下列其中一項作業：
    
      - 若要建立新代理程式群組，請按一下 \[新增\] 。在 \[選取服務\] 搜尋欄位中，輸入想要新增群組的全部或部分 \[ApplicationServer\] 服務名稱。在產生的服務清單中，按一下您需要的服務，然後按一下 \[確定\] 。
    
      - 若要修改現有的代理程式群組，請在搜尋欄位中輸入全部或部分的代理程式群組名稱。在結果清單中，按一下您想要的群組，按一下 \[編輯\] ，然後按一下 \[顯示詳細資料\] 。

5.  在 \[名稱\] 中，輸入識別代理程式群組的名稱。

6.  在 \[描述\] 中，輸入群組的描述。

7.  在 \[參與原則\] 中，選取下列其中一項作業來設定群組的登入行為：
    
      - 選取 \[非正式\] 指定群組中的代理程式不需要登入及登出群組。代理程式會在登入 Lync Server 2013 後，自動登入該群組。
    
      - 選取 \[正式\] 指定群組中的代理程式必須登入和登出群組。當您選取這個選項時，代理程式會按一下 Lync 中的功能表項目以開啟 Internet Explorer 並顯示網頁主控台，以便登入和登出群組。

8.  在 \[警示時間 (秒)\] 中，指定代理程式的電話響幾秒 (預設值為 20 秒) 後會轉給下一個線上代理程式。
    
    > [!IMPORTANT]  
    > 代理程式警示時間設定不得超過 180 秒。如果代理程式警示時間超過 180 秒，用戶端應用程式會拒絕通話，因為 SIP 交易計時器達到等候時間的上線。
    


9.  在 \[路由方法\] 中，選取將電話路由轉送給群組代理程式的方式，如下所示：
    
      - 若要將新的來電先提供給閒置時間最長的代理程式 (在 Lync Server 中目前狀態為 \[有空\] 或 \[非使用中\] 的時間最長)，請按一下 \[最長閒置時間\] 。
    
      - 若要將新電話同時提供給所有的線上代理程式，請按一下 \[平行\] 。該電話會路由傳送給第一個接聽的代理程式。
    
      - 若要將新電話輪流提供給每個代理程式，請按一下 \[循環配置資源\] 。
    
      - 若要永遠依照 \[代理程式\] 清單中的順序將新的來電提供給代理程式，請按一下 \[序列\] 。
    
      - 若要將新的來電提供給已同時登入 Lync Server 2013 和 回應群組應用程式的所有代理程式，而不論其目前狀態為何，請按一下 \[服務員\] 。已設定為代理程式的 Lync 2010 Attendant 使用者可以看見所有等待中的來電，並以任何順序接聽等待中的來電。來電會傳送給第一個接聽的代理程式，之後其他 Lync 2010 Attendant 使用者就不再看見此來電。

10. 在 \[代理人\] 中，指定要如何建立代理人清單：
    
      - 若要使用自訂代理程式清單，請按一下 \[定義代理程式自訂群組\] ，然後執行下列其中一項作業：
        
          - 若要將使用者新增至代理程式群組，請按一下 \[選取\] ，然後在 \[選取代理程式\] 搜尋欄位中，輸入您要新增至此群組的使用者全部或部分名稱，然後按一下 \[尋找\] 。在產生的代理程式清單中，按一下使用者，然後按一下 \[確定\] 。
        
          - 若要從代理程式群組中移除使用者，請在代理程式的清單中，按一下您要移除的使用者，然後按一下 \[移除\] 。
        
          - 若要在使用循環配置資源路由或序列路由的群組中變更代理程式接到來電的順序，請在代理程式清單中，按一下使用者，然後按一下向上鍵或向下鍵。
    
      - 若要使用 Microsoft Exchange Server 通訊群組清單做為代理程式群組，請按一下 \[使用現有的電子郵件通訊群組清單\] ，然後在 \[通訊群組清單位址\] 中，輸入通訊群組清單的電子郵件地址 (例如 NetworkSupport@contoso.com)。
        
        如果您使用電子郵件通訊群組清單，您會受到下列限制：
        
          - 您無法為代理程式群組選取多個通訊群組清單。每一個群組只支援一個通訊群組清單。
        
          - 如果通訊群組清單包含一或多個通訊群組清單，則巢狀通訊群組清單的成員不會加入到代理程式清單中。
        
          - 如果已選取序列或循環配置資源路由，則伺服器會根據路由方法以及通訊群組清單中的代理程式順序，將來電提供給適當的代理程式。
        
          - 通訊群組清單中的使用者若已啟用 Lync Server 2010 但未啟用企業語音，則使用者會以功能運作正常之代理人的身分新增至代理人群組中。請確認通訊群組清單中所有成員的使用者帳戶皆已啟用企業語音。
        
        > [!IMPORTANT]  
        > 如果您使用電子郵件通訊群組清單，則 回應群組 系統管理員或使用者可能會看得見隱藏的成員資格或隱藏的清單。
        
        
        在下列情況下，隱藏的成員資格或隱藏的清單會顯現出來：
        
          - 如果已設定通訊群組清單以便隱藏成員資格，且 回應群組 系統管理員將此通訊群組清單指派至代理程式清單，則使用者可以呼叫群組以找出成員。
        
          - 如果已設定通訊群組清單以便在 Exchange 全域通訊清單中隱藏， 回應群組 系統管理員可能得以看見此通訊群組清單並將它指派到代理程式清單，但前提是 回應群組程序具有適當的使用者權限，即使系統管理員沒有適當的使用者權限亦然。

11. 按一下 \[認可\] 。

## 使用 Windows PowerShell 建立或修改代理人群組

1.  以 RTCUniversalServerAdmins 群組成員或支援回應群組的某個預先定義之管理角色成員的身分登入。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  使用 **New-CsRgsAgentGroup** 建立新代理程式群組。使用 **Set-CsRgsAgentGroup** 修改現有代理程式群組。在命令列中執行：
    
        New-CsRgsAgentGroup -Name "<agent group name>" -Parent $serviceId [-Description "<agent group description>"] -[AgentAlertTime <# seconds until call is routed to next agent>] [-ParticipationPolicy <Formal | Informal>] [-RoutingMethod <method for routing calls>] [-AgentsByUri("<first agent's SIP address>","<second agent's SIP address>")];
    
    例如：
    
        New-CsRgsAgentGroup -Name "Help Desk" -Parent "service:ApplicationServer:atl-cs-001.contoso.com"  -Description "Contoso Help Desk" -AgentAlertTime 20 -ParticipationPolicy Formal -RoutingMethod RoundRobin -AgentsByUri("sip:mindy@contoso.com","sip:bob@contoso.com")
    
    > [!IMPORTANT]  
    > 代理程式警示時間設定不得超過 180 秒。如果代理程式警示時間超過 180 秒，用戶端應用程式會拒絕通話，因為 SIP 交易計時器達到等候時間的上線。
    


4.  確認是否已建立代理程式群組。執行：
    
        Get-CsRgsAgentGroup -Name "Help Desk"

## 請參閱

#### 工作

[刪除專員群組](lync-server-2013-delete-an-agent-group.md)  

#### 其他資源

[管理回應群組代理程式群組](lync-server-2013-managing-response-group-agent-groups.md)  
[Get-CsService](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsService)  
[New-CsRgsAgentGroup](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsAgentGroup)  
[Set-CsRgsAgentGroup](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsRgsAgentGroup)  
[Get-CsRgsAgentGroup](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsRgsAgentGroup)

