---
title: "Lync Server：保護 Edge Server 避免 DoS 和暴力密碼破解攻擊"
TOCTitle: Protecting the Edge Server Against DoS and Password Brute-Force Attacks in Lync Server
ms:assetid: a2aff6d2-8e3e-4c25-9dbd-07b535e90b73
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn879446(v=OCS.15)
ms:contentKeyID: 63845447
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Protecting the Edge Server Against DoS and Password Brute-Force Attacks in Lync Server

 

_**上次修改主題的時間：** 2014-12-09_

Learn about how to protect your Edge server from DoS and brute-force attacks.

When exposing services to the Internet to allow employees more flexibility and mobility in working remotely, there's always the concern of attacks. In Lync Server, the Edge Server provides protection against unauthorized access by using industry-standard security measures. All communications are encrypted and authenticated. However, some customers might be concerned about denial-of-service (DoS) and password brute-force attacks, and these are legitimate types of attacks. Brute-force attacks on user passwords can be prevented by using client certificates for authentication (TLS-DSK) or the lockout security policy in Active Directory 網域服務. However, this policy poses a nuisance to legitimate employees who are trying to connect to the corporate service when their Active Directory accounts have been locked out.

## About Denial of Service attacks

DoS attacks are nearly indistinguishable from legitimate sign-in requests. The only differentiation is in the frequency of sign-in attempts and their origin. A large number of sign-in attempts in rapid succession can be indicative of a DoS attack. DoS attacks attempt to guess the user's password to gain unauthorized access, and often result in locking out the user account if the security policy is enabled in Active Directory Domain Services. The Edge Server doesn't protect against such DoS attacks. However, because Lync Server provides a flexible programming platform, you can use the Microsoft SIP Processing Language (MSPL) to create server applications that intercept SIP messages on the server and perform specialized logic. This is exactly what the security filter does. It's a server application that inspects all incoming sign-in requests. Because the remote user is not authenticated at the Edge Server, the sign-in request is passed to the Director or directly to the internal pool, which then performs the authentication process. The response is passed back to the Edge Server. The security filter inspects the response. If the sign-in failed, the security filter tracks the number of failed attempts for each user account. The next time a client attempts to sign in to the same user account, and the number of failed attempts exceeds the maximum number of allowed sign-in attempts, the security filter immediately rejects the request without passing the request to the Director or internal pool for authentication. By enforcing account lock-out at the Edge Server, the security filter blocks DoS attacks at the edge of the network perimeter. As a result, the security filter protects the internal Lync Server resources.

## Using Transport layer security pre-shared key (TLS-DSK) authentication

Lync Server introduces support for the TLS-DSK authentication protocol. With TLS-DSK, remote users can be authenticated by using a client certificate that was issued by Lync Server. TLS-DSK provides a much stronger authentication mechanism because it uses certificate-based authentication. By presenting the client certificate that was issued by the internal Lync Server, the remote user is authenticated from a device (that is, computer, IP phone) that was pre-authorized. Because the device must have been connected at least once to the internal corporate network to be issued a client certificate from Lync Server, there is stronger assurance that the remote user is connecting from an authorized device. An attacker would need to either steal the user's device or at the very least the client certificate from the device to stage an attack. Of course, the disappearance of the device would tip off the owner to immediately notify corporate IT security.

It is possible to force the Edge Server to negotiate down the authentication protocol to NTLM 2. In this case, the attacker can attack the user's account. The attacker can lock out the account if it is configured by an Active Directory group policy to lock the account after X number of failed attempts. This causes a denial of service attack. If the account isn't protected by an Active Directory group policy, the attacker can brute-force the user's password.

There are several options to how to uniquely identify the user in order to prevent attacks on user accounts. We could have used the source IP address, sign-in name (that is, the SIP URI), or account name. When we investigated each of these options, we determined that rogue clients that were mounting a DoS attack could spoof the source IP address, eliminating this choice as a way to uniquely identify the user. The sign-in name, although necessary to successfully sign in to Lync, is not used to authenticate the user. The sign-in name can be changed in sign-in requests and still lock out the same user account. Therefore, neither the source IP address nor the sign-in name were good sources to identify the user. Only the account name uniquely identifies the user account.

The account name, which consists of the user name and domain name, can only be extracted from the authentication protocol. Users trying to sign in from the Internet use the NTLM 2 authentication protocol, not Kerberos. The NTLM protocol uses a three-stage handshake authentication process. The client passes the user's credentials in the third stage of the NTLM handshake. Because the security filter runs as a trusted server application on the Edge Server, it's allowed to intercept this sign-in (that is, REGISTER) request. The security filter decodes the user name and domain name from the NTLM authentication message. Because the account name is not available in the response, the security filter maps the response to the request by using the message ID.

When either the internal pool or the Director sends the authentication response to the Edge Server, the security filter captures the REGISTER response. If the sign-in failed, the security filter increments the count of failed attempts. If the sign-in succeeds, the security filter resets the count of failed attempts to zero.

Every time the Edge Server receives a sign-in request, it is passed to the security filter. It checks whether the sign-in request has exceeded the maximum allowed number for the particular user account. If the request has not exceeded the maximum lock-out count permitted, the security filter allows the request to continue its course to either the internal pool or the Director. If the request exceeds the maximum lock-out count permitted, the security filter blocks the request, and returns a 403 response. This rejects the request. Any further sign-in attempts are rejected for the duration of the lock-out period. After the lock-out period expires, it is reset to allow new sign-in requests to be authenticated.

## Register and configure the security filter application

Before you can run the security filter application, you must first register the application with your Edge Server. This registration needs to be done only once. Perform the following steps to complete this registration. Run these Lync Server PowerShell cmdlets with Lync Server administrative permissions.

1.  From any Lync Server in your deployment, run the following cmdlet to register the security\_filter application. Specify the fully qualified domain name (FQDN) for the Edge Server in the parameter, \<Edge Server FQDN\>:
    
        new-CsServerApplication -identity "EdgeServer:<Edge Server FQDN>/security_filter" -uri "http://www.contoso.com/security_filter" -critical $false

2.  Run the following cmdlet to initiate the replication of the Central Management store configuration to the Edge Server:
    
        invoke-CsManagementStoreReplication

3.  Run the following cmdlet on the Edge Server to verify the proper registration of the security\_filter application:
    
        get-CsServerApplication -localstore


## Run the security filter application

To run the security filter, three parameters must be passed to the command-line version. For the Windows service version, the installer will prompt you for these parameters.

The first parameter specifies a comma-delimited list of your internal domain names. They are the domain names that are used by remote users who are authenticating to your internal Lync Server when connecting through your Edge Server. For example, if your company, Litware, Inc., has the following three internal Active Directory forests (a legacy from mergers and acquisitions), litware.com, contoso.com and fabrikam.com, and employees have accounts from each of each forests, you should specify "litware,contoso,fabrikam" as the value for this first parameter to the security filter. These domain names are used to verify that remote users who are trying to sign in to Lync Server are connecting by using credentials from one of these three domains (for example, contoso\\bob, fabrikam\\alice, and so on).

The second parameter is the account lock-out count. This is the number of failed sign-in attempts that are allowed before an account lock out is triggered.

The third parameter is the account lock-out period. After an account is locked out, this lock-out period specifies how long the account remains locked before another sign-in attempt is allowed. Any sign-in attempts during this lock-out period are immediately rejected without verification.

## Summary

With support for the authentication protocol, TLS-DSK, introduced in Lync Server, it becomes more difficult for attackers to either attempt to brute-force user's passwords or to stage a denial-of-service attack. These attacks can still be mounted against valid Active Directory user accounts from the Internet by targeting the Edge Server, forcing the authentication negotiation to use NTLM. Thus, it's possible to lock out valid remote users from connecting to your internal Lync Servers.

By taking advantage of the programmable extensibility that is available in the Lync Server SDK, I was able to create a security filter application that runs on the Edge Server. This server application inspects SIP REGISTER requests and responses, and then enforces logic similar to the account lock-out policy in Active Directory Domain Services to prevent DoS attacks on user accounts.

Here are a few things you can do to mitigate security risks:

  - Enforce complex passwords

  - Enforce password change policies

  - Make lockout temporary (ex: 5 min)

  - Monitor lockouts through SCOM alarming

