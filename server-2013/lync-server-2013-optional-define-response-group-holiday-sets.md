---
title: (選用) 在 Lync Server 2013 中定義回應群組假日集
TOCTitle: (選用) 在 Lync Server 2013 中定義回應群組假日集
ms:assetid: 56c37b3b-6517-49b9-86b7-ae48cc349119
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688063(v=OCS.15)
ms:contentKeyID: 49890076
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# (選用) 在 Lync Server 2013 中定義回應群組假日集

 

_**上次修改主題的時間：** 2014-02-07_

假日設定會定義回應群組關閉的不營業日期，並且指定在這些日子採取的動作。假日集為套用至回應群組的假日集合。

> [!NOTE]  
> 如果已將工作流程設定為受管理的工作流程，則任何已指派 CsResponseGroupManager 角色的使用者都可以設定和修改其所管理之工作流程的假日。



## 建立假日集

1.  以 RTCUniversalServerAdmins 群組成員或支援回應群組的某個預先定義之管理角色成員的身分登入。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  對於您要定義的每個假日，請執行：
    
        $x = New-CsRgsHoliday [-Name <holiday name>] -StartDate <starting date of holiday> -EndDate <ending date of holiday>
    
    若要建立包含您所定義之假日的假日集，請執行：
    
        New-CsRgsHolidaySet -Parent <service where the workflow is hosted> -Name <unique name for holiday set> -HolidayList <one or more holidays to be included in the holiday set>
    
    下列範例顯示包含兩個假日的假日集：
    
        $a = New-CsRgsHoliday -Name "New Year's Day" -StartDate "1/1/2013 12:00 AM" -EndDate "1/1/2013 12:00 AM" 
        $b = New-CsRgsHoliday -Name "Independence Day" -StartDate "7/4/2013 12:00 AM" -EndDate "7/5/2013 12:00 AM" 
        New-CsRgsHolidaySet -Parent "ApplicationServer:Redmond.contoso.com -Name "2013 Holidays" -HolidayList ($a, $b)

## 請參閱

#### 概念

[在 Lync Server 2013 中建立或修改群組搜尋工作流程](lync-server-2013-create-or-modify-a-hunt-group-workflow.md)  
[在 Lync Server 2013 中建立或修改互動式工作流程](lync-server-2013-create-or-modify-an-interactive-workflow.md)  

#### 其他資源

[New-CsRgsHoliday](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsHoliday)  
[New-CsRgsHolidaySet](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsHolidaySet)

