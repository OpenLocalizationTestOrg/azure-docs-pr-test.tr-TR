---
title: "aaaAzure örnek uygulama DMZ'ler ile kullanılmak üzere | Microsoft Docs"
description: "Trafik akışı senaryoları DMZ tootest oluşturduktan sonra bu basit bir web uygulaması dağıtma"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 60340ab7-b82b-40e0-bd87-83e41fe4519c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: e0d9cf14590f75b50c64b677efce2c5425b83ec6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-application-for-use-with-dmzs"></a>Örnek bir uygulama DMZ'ler ile kullanmak için
[Dönüş toohello güvenlik sınırı en iyi uygulamalar sayfası][HOME]

Bu PowerShell komut dosyalarını hello IIS01 ve AppVM01 sunucuları tooinstall üzerinde yerel olarak çalıştırın ve bir html sayfasıyla hello ön uç IIS01 sunucusundan hello arka uç AppVM01 sunucusundan içerik görüntüleyen basit bir web uygulaması ayarlayın.

Bu uygulama basit bir sınama ortamı birçok hello DMZ örnekler ve değişiklikleri nasıl hello uç noktaları, Nsg'ler, UDR sağlar ve güvenlik duvarı kuralları trafik akışına etkileyebilir.

## <a name="firewall-rule-tooallow-icmp"></a>Güvenlik duvarı kuralı tooallow ICMP
Bu basit bir PowerShell ifadesi herhangi bir Windows VM tooallow ICMP (Ping) trafiği çalıştırabilirsiniz. Bu Güvenlik Duvarı'nı güncelleştirme daha kolay sınama ve hello ping Protokolü toopass (için ICMP varsayılan olarak açık çoğu Linux distro'lar) hello windows güvenlik duvarı aracılığıyla izin vererek sorun giderme sağlar.

```PowerShell
# Turn On ICMPv4
New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" `
    -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow
```

Komut dosyaları aşağıdaki hello kullanırsanız, bu güvenlik duvarı kuralı hello ilk ifade ektir.

## <a name="iis01---web-application-installation-script"></a>IIS01 - Web uygulama yükleme betiği
Bu komut dosyası aşağıdakileri yapar:

1. Açık IMCPv4 (Ping) daha kolay test hello yerel sunucunun windows güvenlik duvarı
2. IIS'yi yükleyip hello .net Framework v4.5
3. Bir ASP.NET web sayfası ve Web.config dosyası oluşturma
4. Merhaba varsayılan uygulama havuzunu toomake dosya erişimini daha kolay değiştirme
5. Merhaba anonim kullanıcı tooyour yönetici hesabı ve parolası ayarlayın

RDP IIS01 alırken bu PowerShell komut dosyasını yerel olarak çalıştırmanız gerekir.

```PowerShell
# IIS Server Post Build Config Script
# Get Admin Account and Password
    Write-Host "Please enter hello admin account information used toocreate this VM:" -ForegroundColor Cyan
    $theAdmin = Read-Host -Prompt "hello Admin Account Name (no domain or machine name)"
    $thePassword = Read-Host -Prompt "hello Admin Password"

# Turn On ICMPv4
    Write-Host "Creating ICMP Rule in Windows Firewall" -ForegroundColor Cyan
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Install IIS
    Write-Host "Installing IIS and .Net 4.5, this can take some time, like 15+ minutes..." -ForegroundColor Cyan
    add-windowsfeature Web-Server, Web-WebServer, Web-Common-Http, Web-Default-Doc, Web-Dir-Browsing, Web-Http-Errors, Web-Static-Content, Web-Health, Web-Http-Logging, Web-Performance, Web-Stat-Compression, Web-Security, Web-Filtering, Web-App-Dev, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Net-Ext, Web-Net-Ext45, Web-Asp-Net45, Web-Mgmt-Tools, Web-Mgmt-Console

# Create Web App Pages
    Write-Host "Creating Web page and Web.Config file" -ForegroundColor Cyan
    $MainPage = '<%@ Page Language="vb" AutoEventWireup="false" %>
    <%@ Import Namespace="System.IO" %>
    <script language="vb" runat="server">
        Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Load
            Dim FILENAME As String = "\\10.0.2.5\WebShare\Rand.txt"
            Dim objStreamReader As StreamReader
            objStreamReader = File.OpenText(FILENAME)
            Dim contents As String = objStreamReader.ReadToEnd()
            lblOutput.Text = contents
            objStreamReader.Close()
            lblTime.Text = Now()
        End Sub
    </script>

    <!DOCTYPE html>
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
        <title>DMZ Example App</title>
    </head>
    <body style="font-family: Optima,Segoe,Segoe UI,Candara,Calibri,Arial,sans-serif;">
      <form id="frmMain" runat="server">
        <div>
          <h1>Looks like you made it!</h1>
          This is a page from hello inside (a web server on a private network),<br />
          and it is making its way toohello outside! (If you are viewing this from hello internet)<br />
          <br />
          hello following sections show:
          <ul style="margin-top: 0px;">
            <li> Local Server Time - Shows if this page is or isnt cached anywhere</li>
            <li> File Output - Shows that hello web server is reaching AppVM01 on hello backend subnet and successfully returning content</li>
            <li> Image from hello Internet - Doesnt really show anything, but it made me happy toosee this when hello app worked</li>
          </ul>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Local Web Server Time</b>: <asp:Label runat="server" ID="lblTime" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>File Output from AppVM01</b>: <asp:Label runat="server" ID="lblOutput" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Image File Linked from hello Internet</b>:<br />
            <br />
            <img src="http://sd.keepcalm-o-matic.co.uk/i/keep-calm-you-made-it-7.png" alt="You made it!" width="150" length="175"/></div>
        </div>
      </form>
    </body>
    </html>'

    $WebConfig ='<?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.web>
        <compilation debug="true" strict="false" explicit="true" targetFramework="4.5" />
        <httpRuntime targetFramework="4.5" />
        <identity impersonate="true" />
        <customErrors mode="Off"/>
      </system.web>
      <system.webServer>
        <defaultDocument>
          <files>
            <add value="Home.aspx" />
          </files>
        </defaultDocument>
      </system.webServer>
    </configuration>'

    $MainPage | Out-File -FilePath "C:\inetpub\wwwroot\Home.aspx" -Encoding ascii
    $WebConfig | Out-File -FilePath "C:\inetpub\wwwroot\Web.config" -Encoding ascii

# Set App Pool tooClasic Pipeline tooremote file access will work easier
    Write-Host "Updaing IIS Settings" -ForegroundColor Cyan
    c:\windows\system32\inetsrv\appcmd.exe set app "Default Web Site/" /applicationPool:".NET v4.5 Classic"
    c:\windows\system32\inetsrv\appcmd.exe set config "Default Web Site/" /section:system.webServer/security/authentication/anonymousAuthentication /userName:$theAdmin /password:$thePassword /commit:apphost

# Make sure hello IIS settings take
    Write-Host "Restarting hello W3SVC" -ForegroundColor Cyan
    Restart-Service -Name W3SVC

    Write-Host
    Write-Host "Web App Creation Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="appvm01---file-server-installation-script"></a>AppVM01 - dosya sunucusu yükleme betiği
Bu komut dosyası hello arka uç basit bu uygulama için ayarlar. Bu komut dosyası aşağıdakileri yapar:

1. Açık IMCPv4 (Ping) daha kolay test etmek için Güvenlik Duvarı'nda hello
2. Merhaba web sitesi için bir dizin oluşturun
3. Bir metin dosyası toobe uzaktan oluşturmak erişim tarafından hello web sayfası
4. Merhaba dizin ve dosya tooAnonymous tooallow erişim izinlerini ayarlayın
5. IE Artırılmış Güvenlik tooallow bu sunucudan gözatma daha kolay Aç 

> [!IMPORTANT]
> **En iyi uygulaması**: hiçbir zaman bir üretim sunucuda IE Artırılmış Güvenlik devre dışı kapatın, artı genellikle bir üretim sunucusu kötü bir fikir toosurf hello Web'den içindir. Ayrıca, dosya paylaşımları anonim erişim için açma tamamlandı ancak kötü bir fikir burada kolaylık sağlamak için geçerlidir.
> 
> 

RDP AppVM01 alırken bu PowerShell komut dosyasını yerel olarak çalıştırmanız gerekir. Yönetici tooensure başarılı yürütülmesi gereken toobe powershell'dir.

```PowerShell
# AppVM01 Server Post Build Config Script
# PowerShell must be run as Administrator for Net Share commands toowork

# Turn On ICMPv4
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Create Directory
    New-Item "C:\WebShare" -ItemType Directory

# Write out Rand.txt
    $FileContent = "Hello, I'm hello contents of a remote file on AppVM01."
    $FileContent | Out-File -FilePath "C:\WebShare\Rand.txt" -Encoding ascii

# Set Permissions on share
    $Acl = Get-Acl "C:\WebShare"
    $AccessRule = New-Object system.security.accesscontrol.filesystemaccessrule("Everyone","ReadAndExecute, Synchronize","ContainerInherit, ObjectInherit","InheritOnly","Allow")
    $Acl.SetAccessRule($AccessRule)
    Set-Acl "C:\WebShare" $Acl

# Create network share
    Net Share WebShare=C:\WebShare "/grant:Everyone,READ"

# Turn Off IE Enhanced Security Configuration for Admins
    Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A7-37EF-4b3f-8CFC-4F3A74704073}" -Name "IsInstalled" -Value 0

    Write-Host
    Write-Host "File Server Set up Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="dns01---dns-server-installation-script"></a>DNS01 - DNS sunucusu yükleme betiği
Bu örnek uygulama tooset hello DNS sunucusu dahil betik yok. Merhaba güvenlik duvarı kuralları, NSG veya UDR sınama tooinclude DNS trafiğinin gerekirse, hello DNS01 server toobe gerekir el ile ayarlayın. Merhaba ağ yapılandırma xml dosyasını ve örneklerin her ikisi de Resource Manager şablonu hello birincil DNS sunucusu ve Düzey 3 hello yedekleme DNS sunucusu tarafından barındırılan hello ortak DNS sunucusu olarak DNS01 içerir. Merhaba düzeyi 3 DNS sunucusu yerel olmayan trafik için kullanılan hello gerçek bir DNS sunucusunun ve DNS01 ile ayarlanmadı, DNS oluşacak yerel ağ.

## <a name="next-steps"></a>Sonraki adımlar
* Bir IIS sunucusunda Hello IIS01 betiği çalıştırın
* AppVM01 üzerinde dosya sunucusu komut dosyasını çalıştır
* Toohello genel IP IIS01 toovalidate üzerinde yapınızın Gözat

<!--Link References-->
[HOME]: ../best-practices-network-security.md
