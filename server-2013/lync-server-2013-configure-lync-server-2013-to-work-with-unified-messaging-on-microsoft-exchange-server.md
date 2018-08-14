---
title: "Lync Server 2013：設定 Lync Server 2013 與 Microsoft Exchange Server 上的整合通訊搭配使用"
TOCTitle: 設定 Lync Server 2013 以搭配 Microsoft Exchange Server 上的 Unified Messaging 使用
ms:assetid: 1098ae4d-f57f-44f3-804e-39889d9fc14e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398193(v=OCS.15)
ms:contentKeyID: 49290118
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定 Lync Server 2013 以搭配 Microsoft Exchange Server 上的 Unified Messaging 使用

 

_**上次修改主題的時間：** 2013-04-03_

這個步驟需要 Exchange UM 整合公用程式 (OcsUmUtil.exe)。此工具位於 Lync Server 2013 伺服器的 ..\\Program Files\\Common Files\\Microsoft Lync Server 2013\\Support 資料夾。

## 執行 Exchange UM 整合公用程式

Exchange UM 整合公用程式必須從具有下列特性的使用者帳戶執行：

  - RTCUniversalServerAdmins 與 RtcUniversalUserAdmins 群組的成員資格 (包括讀取 Exchange Server Unified Messaging 設定的權限)。

  - 在指定之組織單位 (OU) 容器中建立連絡人物件的網域內使用者權限。

當您執行 Exchange UM 整合公用程式時，它會執行下列工作：

  - 針對 企業語音使用者所要使用的每一個自動語音應答和訂戶存取號碼來建立連絡人物件。

  - 確認每個 企業語音撥號對應表的名稱與對應的整合通訊 (UM) 撥號對應表電話內容相符。只有當 UM 撥號對應表在版本比 Exchange 2010 Service Pack 1 (SP1) 還「舊」 的 Exchange 上執行，才需要要求上述兩者相符。

> [!IMPORTANT]  
> 在您執行 Exchange UM 整合公用程式之前，請確定您已完成下列步驟：
> <ul><li><p>如 Exchange 產品文件中所述，建立一個以上的 Exchange UM 撥號對應表。</p>
> <p>如果是 Microsoft Exchange Server 2010，請參閱＜建立 UM 撥號對應表＞，網址是 <a href="http://go.microsoft.com/fwlink/?linkid=186177%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=186177&amp;clcid=0x404</a>。</p>
> <p>如果是 Microsoft Exchange Server 2007 Service Pack 1 (SP1)，請參閱＜如何建立整合通訊 SIP URI 撥號對應表＞，網址是 <a href="http://go.microsoft.com/fwlink/?linkid=185771%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=185771&amp;clcid=0x404</a>。</p></li>
> <li><p>如＜<a href="lync-server-2013-create-a-dial-plan.md">在 Lync Server 2013 中建立撥號對應表</a>＞中所述，建立一個以上的對應 Lync Server 撥號對應表。</p></li> 
> <ul><li>如果您使用的 Exchange 版本比 Microsoft Exchange Server 2010 SP1 還舊，則您必須在 Lync Server 2013 撥號對應表的 [簡單名稱] 欄位中，輸入對應 Exchange 整合通訊 (UM) SIP 撥號對應表的完整網域名稱 (FQDN)。如果您是使用 Microsoft Exchange Server 2010 SP1 或最新的 Service Pack，則這項撥號對應表名稱不一定得相符。</li></ul>
> <li><p>請建立一個自動語音應答，並且確定訂戶存取號碼和自動語音應答號碼的格式都是 E.164。</p></li></ul>


## 若要執行 Exchange UM 整合公用程式

1.  在 前端伺服器，開啟命令提示字元，輸入 **cd %CommonProgramFiles%\\Microsoft Lync Server 2013\\Support** ，然後按 ENTER。

2.  輸入 **OcsUmUtil.exe** ，然後按 ENTER。

3.  按一下 **\[載入資料\]** 以找出所有受信任的 Exchange 樹系。

4.  在 **\[SIP 撥號對應表\]** 清單中，選取您要為它建立連絡人物件的 UM SIP 撥號對應表，然後按一下 **\[新增\]** 。

5.  在 **\[連絡人\]** 方塊中，接受預設的組織單位，或按一下 **\[瀏覽\]** 來啟動 **\[OU 選擇器\]** 。在 **\[OU 選擇器\]** 方塊中，您可以選擇一個 OU，再按一下 **\[確定\]** ，或者您可以按一下 **\[建立新的 OU\]** ，在根目錄底下或網域中其他任何 OU 底下建立新的組織單位 (例如，"OU=RTC Special Accounts,DC=fourthcoffee,DC=com")，然後按一下 **\[確定\]** 。
    
    > [!NOTE]  
    > 您所選取或建立之 OU 的辨別名稱 (DN)，現在會在 <strong>[組織單位]</strong> 方塊中顯示。
    


6.  在 **\[名稱\]** 方塊中，接受預設的撥號對應表名稱，或者為您要建立的連絡人物件輸入新的顯示名稱。
    
    > [!NOTE]  
    > 例如，如果您要建立訂閱者存取連絡人物件，可以直接命名為「訂閱者存取」。
    


7.  在 **\[SIP 位址\]** 方塊中，接受預設 SIP 位址或輸入新的 SIP 位址。
    
    > [!NOTE]  
    > 如果輸入新的 SIP 位址，必須以 <strong>SIP:</strong> 開頭 (也就是 &quot;SIP:&quot;，包括冒號)。
    


8.  在 **\[伺服器或集區\]** 清單中，選取要啟用連絡人物件的 Standard Edition Server 或 前端集區。
    
    > [!NOTE]  
    > 您選取的集區最好是與啟用 企業語音與 Exchange UM 之使用者部署的集區相同。
    


9.  在 **\[電話號碼\]** 清單中，選取 **\[輸入電話號碼\]** 或 **\[從 Exchange UM 使用此整合通訊接駁電話號碼\]** ，然後輸入電話號碼。

10. 在 **\[連絡人類型\]** 清單中，選取您要建立的連絡人類型，然後按一下 **\[確定\]** 。

11. 為您要建立的其他連絡人物件重複步驟 1 到 10。
    
    > [!NOTE]  
    > 您應該為每個自動語音應答至少建立一個連絡人。如果您想要提供外部存取，也需要具備「訂戶存取」連絡人，並指定直接向內撥號 (DID) 號碼。
    


若要確認已經建立了連絡人物件，請開啟 \[Active Directory 使用者及電腦\]，再選取建立物件的 OU。連絡人物件應會在詳細資料窗格中顯示。

