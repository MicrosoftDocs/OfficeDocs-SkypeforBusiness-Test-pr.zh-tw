---
title: Configuring the Various Policies
TOCTitle: Configuring the Various Policies
ms:assetid: e3b3cbda-7c17-470b-acb0-82fdcc473184
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945610(v=OCS.15)
ms:contentKeyID: 52056021
ms.date: 09/13/2014
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configuring the Various Policies

 

_**上次修改主題的時間：** 2013-02-24_

## Configuring the Various Policies

Here are the various policies that you can configure in your Lync Server 2013 topology, prior to running the Lync Server 2013 Stress and Performance Tool.

## Configuring the Archiving Policy

See the example script ArchivingPolicy.ps1. You need to use this script only if an Archiving Server is deployed in your topology. For details, see the Lync Server 2013 documentation and cmdlet Help for [封存與監控 Cmdlet](https://technet.microsoft.com/zh-tw/library/gg415629\(v=ocs.15\)).

## Configuring the Conferencing Policy

See the example script MeetingPolicy.ps1. For details, see the Lync Server 2013 documentation and the cmdlet Help for [Web 會議 Cmdlet](https://technet.microsoft.com/zh-tw/library/gg415675\(v=ocs.15\)).

## Configuring the Contacts Policy

See the example ContactsPolicy.ps1. For details, see the Lync Server 2013 documentation and the cmdlet Help for [IM 和顯示狀態 Cmdlet](https://technet.microsoft.com/zh-tw/library/gg398611\(v=ocs.15\)).

## Configuring the Federation Policy

See the example FederationPolicy.ps1. For details, see the Lync Server 2013 documentation and the cmdlet Help for [Edge Server Cmdlet](https://technet.microsoft.com/zh-tw/library/gg415635\(v=ocs.15\)) and [Lync Server 2013 中的同盟和外部存取 Cmdlet](https://technet.microsoft.com/zh-tw/library/gg415651\(v=ocs.15\)).

## Configuring the Call Admission Control Policy

See the example BandwidthPolicy.ps1. For details, see the Lync Server 2013 documentation [Lync Server 2013 中的通話許可控制概觀](https://technet.microsoft.com/zh-tw/library/gg398529\(v=ocs.15\)) and the cmdlet Help for [通話許可控制 Cmdlet](https://technet.microsoft.com/zh-tw/library/gg415676\(v=ocs.15\)).

## Configuring the Voice Routing Rules

See the example RoutingRules.ps1. When you configure the voice routing rules, take note of the Phone Context (that is, /Location Profile or /SimpleName) and Internal/External Area Codes so that you can specify them when creating users and during LyncPerfTool configuration (specifically for PSTN-UC and UC-PSTN). For example, the SimpleName parameter in the call to the **New-CsDialPlan** cmdlet in the RoutingRules.ps1 example should be used for the LocationProfile value in the following figure of UserProfileGenerator.exe.

![語音路由規則範例。](images/JJ945610.9f34d971-4ed0-4a4c-b101-086a91c4578c(OCS.15).jpg "語音路由規則範例。")

For details, see the Lync Server 2013 documentation and the cmdlet Help for [Enterprise Voice Cmdlet](https://technet.microsoft.com/zh-tw/library/gg415658\(v=ocs.15\)).

## Configuring Conferencing Attendant application

See the example ConferenceAutoAttendantConfiguration.ps1. Take note of the ConferencingAutoAttendant phone number (1121111111, by default), so that you can type it into the LyncPerf Tool Configuration tool for configuration generation.

![設定會議服務員應用程式](images/JJ945610.0618a22f-27a9-423a-9085-d2bf71e82db6(OCS.15).jpg "設定會議服務員應用程式")

For details, see the Lync Server 2013 documentation and the cmdlet Help for [Web 會議 Cmdlet](https://technet.microsoft.com/zh-tw/library/gg415675\(v=ocs.15\)) and [電話撥入式會議 Cmdlet](https://technet.microsoft.com/zh-tw/library/gg415630\(v=ocs.15\)).

## Configuring Lync Server Call Park Service

Call Park is disabled by default. See the example CallParkConfiguration.ps1. For details, see the Lync Server 2013 documentation and the cmdlet Help for [通話保留應用程式 Cmdlet](https://technet.microsoft.com/zh-tw/library/gg415639\(v=ocs.15\)).

## Configuring Emergency Calls

Perform the following steps to configure stress and performance testing for emergency calls.

1.  Set up a voice route for emergency calls. See the RoutingRules.ps1 script under the comment "Route E911 to PSTN" for an example of setting up this voice route.
    
    > [!CAUTION]
    > The example command in RoutingRules.ps1 has a number pattern that includes the number 119 rather than 911. You should avoid using 911 (or your actual local emergency number) to prevent accidental calls to your local emergency operators during load testing. This configuration is for simulation purposes only.


2.  Configure addresses by filling in the values on the **LIS** tab in the UserProvisioningTool, as shown in the following figure.
    
    ![設定位置資訊服務。](images/JJ945610.8ac1faa1-e9f9-40d0-b8b7-b159f4f459f7(OCS.15).jpg "設定位置資訊服務。")  

3.  Click **Generate LIS Config Files**.

4.  CSV files for ports, subnets, switches, and wireless access points (WAPs), and an XML file for the Lync Server 2013 Stress and Performance Tool, are generated. The CSV files are to be used as inputs (in the same folder) when configuring Location Information service (LIS) with the LisConfiguration.ps1 script. Move the generated Locations0.xml file to the same folder as the Lync Server 2013 Stress and Performance Tool executable (LyncPerfTool.exe), which will run location profile (dial plan) scenarios.

## Creating, Enabling, Configuring and Disabling Users

You should create all your users before running the following scripts. Follow the instructions in [Create Users and Contacts](create-users-and-contacts.md) to create users. For details, see the Lync Server 2013 cmdlet documentation for the [Get-CsUser](https://technet.microsoft.com/zh-tw/library/gg398125\(v=ocs.15\)), [Set-CsUser](https://technet.microsoft.com/zh-tw/library/gg398510\(v=ocs.15\)), and [Disable-CsUser](https://technet.microsoft.com/zh-tw/library/gg398747\(v=ocs.15\)) cmdlets.

## Configuring Response Group application

See the example ResponseGroupConfiguration.ps1. For details, see the Lync Server 2013 documentation and the cmdlet Help for [回應群組應用程式 Cmdlet](https://technet.microsoft.com/zh-tw/library/gg415654\(v=ocs.15\)).To review the Response Group application configuration, see `https://<poolfqdn>/RgsConfig/`, as shown in the following figure.

![回應群組設定工具。](images/JJ945610.480a9440-2283-4533-98f8-86daaab4781c(OCS.15).jpg "回應群組設定工具。")

