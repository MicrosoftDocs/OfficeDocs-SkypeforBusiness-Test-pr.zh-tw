---
title: Lync Server 2013：(選用) 定義回應群組營業時間
TOCTitle: (選用) 定義回應群組營業時間
ms:assetid: d62551b2-1847-4e1b-abe8-683b72aa94d5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205291(v=OCS.15)
ms:contentKeyID: 49292468
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# (選用) 在 Lync Server 2013 中定義回應群組營業時間

 

_**上次修改主題的時間：** 2012-11-01_

## 定義營業時間

營業時間設定會定義工作流程能夠接聽來電的時間，以及指定對營業時間以外的來電採取的動作。回應群組系統管理員可以使用 **New-CsRgsHoursOfBusiness** Cmdlet 建立預先定義的排程，這些排程可用於任意數目的回應群組。

> [!TIP]
> 當您建立或修改工作流程時，您可以指定只限該工作流程套用的自訂排程。如需詳細資訊，請參閱＜ <a href="lync-server-2013-create-or-modify-a-hunt-group-workflow.md">在 Lync Server 2013 中建立或修改群組搜尋工作流程</a>＞或＜ <a href="lync-server-2013-create-or-modify-an-interactive-workflow.md">在 Lync Server 2013 中建立或修改互動式工作流程</a>＞。


> [!NOTE]  
> 如果工作流程定義為受管理工作流程，指派為 CsResponseGroupManager 角色的任何使用者都可以針對其管理的工作流程設定和修改自訂營業時間。



> [!IMPORTANT]  
> 對於下列 Cmdlet 中的參數，請使用 24 小時制的標記法 (例如，20:00=8:00 P.M.)。



## 建立預先定義的營業時間集合

1.  以 RTCUniversalServerAdmins 群組成員或支援回應群組的某個預先定義之管理角色成員的身分登入。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  對於您要定義的每個唯一時間範圍，請執行：
    
        $x = New-CsRgsTimeRange [-Name <name of time range>] -OpenTime <time when business hours begin> -CloseTime <time when business hours end>
    
    若要使用您定義的範圍來建立營業時間集合，請執行：
    
        New-CsRgsHoursOfBusiness -Parent <service where the workflow is hosted> -Name <unique name for collection> [-MondayHours1 <first set of opening and closing times for Monday>] [-MondayHours2 <second set of opening and closing times for Monday>] [-TuesdayHours1 <first set of opening and closing times for Tuesday>] [-TuesdayHours2 <second set of opening and closing times for Tuesday>] [-WednesdayHours1 <first set of opening and closing times for Wednesday>] [-WednesdayHours2 <second set of opening and closing times for Wednesday>] [-ThursdayHours1 <first set of opening and closing times for Thursday>] [-ThursdayHours2 <second set of opening and closing times for Thursday>] [-FridayHours1 <first set of opening and closing times for Friday>] [-FridayHours2 <second set of opening and closing times for Friday>] [-SaturdayHours1 <first set of opening and closing times for Saturday>] [-SaturdayHours2 <second set of opening and closing times for Saturday>] [-SundayHours1 <first set of opening and closing times for Sunday>] [-SundayHours2 <second set of opening and closing times for Sunday>]
    
    下列範例會將工作日的營業時間指定為上午 9:00 到下午 5:00，星期六則為上午 8:00 到上午 10:00 以及下午 2:00 到下午 6:00，星期日不上班：
    
        $a = NewRgsTimeRange -Name "Weekday Hours" -OpenTime "9:00" -CloseTime "17:00"
        $b = NewRgsTimeRange -Name "Saturday Morning Hours" -OpenTime "8:00" -CloseTime "10:00" 
        $c = NewRgsTimeRange -Name "Saturday Afternoon Hours" -OpenTime "14:00" -CloseTime "18:00" 
        New-CsRgsHoursOfBusiness -Parent "ApplicationServer:Redmond.contoso.com" -Name "Help Desk Business Hours" -MondayHours1 $a -TuesdayHours1 $a -WednesdayHours1 $a -ThursdayHours1 $a -FridayHours1 $a -SaturdayHours1 $b -SaturdayHours2 $c

## 請參閱

#### 概念

[在 Lync Server 2013 中建立或修改群組搜尋工作流程](lync-server-2013-create-or-modify-a-hunt-group-workflow.md)  
[在 Lync Server 2013 中建立或修改互動式工作流程](lync-server-2013-create-or-modify-an-interactive-workflow.md)  

#### 其他資源

[New-CsRgsTimeRange](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsTimeRange)  
[New-CsRgsHoursOfBusiness](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsHoursOfBusiness)

