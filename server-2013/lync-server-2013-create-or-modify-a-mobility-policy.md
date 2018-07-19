---
title: 建立或修改行動性原則
TOCTitle: 建立或修改行動性原則
ms:assetid: fc2dfea0-2215-440d-9f4b-7c985da29211
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721946(v=OCS.15)
ms:contentKeyID: 49890519
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立或修改行動性原則

 

_**上次修改主題的時間：** 2013-02-23_

您可建立或修改行動性原則，讓行動使用者使用支援如即時訊息 (IM)、目前狀態及連絡人等 Lync 功能的行動裝置。您可從 Lync Server 2013 控制台 或 Lync Server 2013 管理命令介面 建立或修改行動性原則。

## 從 Lync Server 控制台 建立行動性原則

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 \[用戶端\]、\[行動性原則\] 導覽按鈕。

4.  按一下 \[行動性原則\] 頁面中的 \[新增\]，然後執行以下任一項作業：
    
    1.  若要建立網站行動性原則，請依序按一下 \[站台原則\]、某個網站及 \[確定\]，檢閱預設值，並視需要變更。
    
    2.  若要建立使用者行動性原則，請按一下 \[使用者原則\]，輸入姓名，檢閱預設值，並視需要變更。

5.  按一下 \[認可\]。

## 從 Lync Server 控制台 修改行動性原則

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 \[用戶端\]、\[行動性原則\] 導覽按鈕。

4.  在 \[行動性原則\] 頁面中，按一下其中一個現有的行動性原則。

5.  在 \[編輯\] 功能表上，按一下 \[顯示詳細資料\]。

6.  編輯任何設定值。

7.  按一下 \[認可\]。

## 使用 Windows PowerShell Cmdlet 移除外部存取原則

您也可使用 Windows PowerShell 與 **New-CsMobilityPolicy** Cmdlet (於網站範圍或每個使用者範圍) 建立行動性原則。此外，您可使用 **Set-CsMobilityPolicy** Cmdlet 修改任何現有原則，包含全域原則。可從 Lync Server 2013 管理命令介面 或 Windows PowerShell 的 如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。 的遠端工作階段執行這些 Cmdlet。

## 於網站範圍建立行動性原則

  - 此命令會建立 Redmond 網站的新行動性原則：
    
        New-CsMobilityPolicy -Identity "site:Redmond"
    
    因為先前的命令並未指定參數 (除了必要識別碼參數之外)，所以原則的所有屬性均會採用預設值。

## 於每個使用者範圍建立行動性原則

  - 若要於每個使用者範圍建立行動性原則，請指定原則的唯一識別碼：
    
        New-CsMobilityPolicy -Identity "RedmondMobilityPolicy"

## 建立行動性原則時變更單一屬性值

  - 若要建立使用不同屬性值，請包含適當參數與參數值的原則。例如，此命令會建立停用「從公司撥號」的行動性原則：
    
        New-CsMobilityPolicy -Identity "site:Redmond" -EnableOutsideVoice $False

## 建立行動性原則時變更多個屬性值

  - 包含多個參數即可修改多個屬性值。例如，此命令會建立同時停用行動性與「從公司撥號」的原則：
    
        New-CsMobilityPolicy "site:Redmond" -EnableMobility $False -EnableOutsideVoice $False

如需詳細資訊，請參閱[New-CsMobilityPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsMobilityPolicy)與[Set-CsMobilityPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsMobilityPolicy) Cmdlet 的說明主題。

## 請參閱

#### 工作

[在 Lync Server 2013 中設定行動原則](lync-server-2013-configuring-mobility-policy.md)

