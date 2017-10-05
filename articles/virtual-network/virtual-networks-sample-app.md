---
title: "DMZ'ler ile kullanmak için örnek uygulama | Microsoft Docs"
description: "Trafik akışı senaryolarını sınamak için DMZ oluşturduktan sonra bu basit web uygulaması dağıtma"
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
ms.openlocfilehash: 8506238e41c5d9dac8d76d729d4919b30a0528b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="sample-application-for-use-with-dmzs"></a><span data-ttu-id="ea5b1-103">Örnek bir uygulama DMZ'ler ile kullanmak için</span><span class="sxs-lookup"><span data-stu-id="ea5b1-103">Sample application for use with DMZs</span></span>
<span data-ttu-id="ea5b1-104">[Güvenlik sınırı en iyi yöntemler sayfasına dön][HOME]</span><span class="sxs-lookup"><span data-stu-id="ea5b1-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="ea5b1-105">Bu PowerShell komut dosyalarını yerel olarak yükleyin ve arka uç AppVM01 sunucusundan içerik ile ön uç IIS01 sunucusundan html sayfalarını görüntüleyen basit bir web uygulaması için IIS01 ve AppVM01 sunucularda çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea5b1-105">These PowerShell scripts can be run locally on the IIS01 and AppVM01 servers to install and set up a simple web application that displays an html page from the front-end IIS01 server with content from the back-end AppVM01 server.</span></span>

<span data-ttu-id="ea5b1-106">Bu uygulama basit bir sınama ortamında pek çok DMZ örnekler sağlar ve nasıl değişiklikleri uç noktaları, Nsg'ler, UDR ve güvenlik duvarı kuralları trafik akışına etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="ea5b1-106">This application provides a simple testing environment for many of the DMZ Examples and how changes on the Endpoints, NSGs, UDR, and Firewall rules can affect traffic flows.</span></span>

## <a name="firewall-rule-to-allow-icmp"></a><span data-ttu-id="ea5b1-107">ICMP izin veren güvenlik duvarı kuralı</span><span class="sxs-lookup"><span data-stu-id="ea5b1-107">Firewall rule to allow ICMP</span></span>
<span data-ttu-id="ea5b1-108">Bu basit bir PowerShell ifadesi ICMP (Ping) trafiğine izin vermek için bir Windows VM üzerinde çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="ea5b1-108">This simple PowerShell statement can be run on any Windows VM to allow ICMP (Ping) traffic.</span></span> <span data-ttu-id="ea5b1-109">Windows güvenlik duvarı (çoğu Linux distro'lar ICMP varsayılan olarak etkindir) üzerinden iletmek için daha kolay test ve ping Protokolü vererek sorun giderme için bu Güvenlik Duvarı'nı güncelleştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="ea5b1-109">This firewall update allows for easier testing and troubleshooting by allowing the ping protocol to pass through the windows firewall (for most Linux distros ICMP is on by default).</span></span>

```PowerShell
# Turn On ICMPv4
New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" `
    -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow
```

<span data-ttu-id="ea5b1-110">Aşağıdaki komut dosyaları kullanırsanız, bu güvenlik duvarı kuralı ilk ifade ektir.</span><span class="sxs-lookup"><span data-stu-id="ea5b1-110">If you use the following scripts, this firewall rule addition is the first statement.</span></span>

## <a name="iis01---web-application-installation-script"></a><span data-ttu-id="ea5b1-111">IIS01 - Web uygulama yükleme betiği</span><span class="sxs-lookup"><span data-stu-id="ea5b1-111">IIS01 - Web application installation script</span></span>
<span data-ttu-id="ea5b1-112">Bu komut dosyası aşağıdakileri yapar:</span><span class="sxs-lookup"><span data-stu-id="ea5b1-112">This script will:</span></span>

1. <span data-ttu-id="ea5b1-113">Açık IMCPv4 (Ping) daha kolay test etmek için yerel sunucunun windows güvenlik duvarı</span><span class="sxs-lookup"><span data-stu-id="ea5b1-113">Open IMCPv4 (Ping) on the local server windows firewall for easier testing</span></span>
2. <span data-ttu-id="ea5b1-114">IIS ve .net yükleme Framework v4.5</span><span class="sxs-lookup"><span data-stu-id="ea5b1-114">Install IIS and the .Net Framework v4.5</span></span>
3. <span data-ttu-id="ea5b1-115">Bir ASP.NET web sayfası ve Web.config dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea5b1-115">Create an ASP.NET web page and a Web.config file</span></span>
4. <span data-ttu-id="ea5b1-116">Dosya erişimi kolaylaştırmak için varsayılan uygulama havuzunu Değiştir</span><span class="sxs-lookup"><span data-stu-id="ea5b1-116">Change the Default application pool to make file access easier</span></span>
5. <span data-ttu-id="ea5b1-117">Yönetici hesabınız ve parolanız için anonim kullanıcı Ayarla</span><span class="sxs-lookup"><span data-stu-id="ea5b1-117">Set the Anonymous user to your admin account and password</span></span>

<span data-ttu-id="ea5b1-118">RDP IIS01 alırken bu PowerShell komut dosyasını yerel olarak çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea5b1-118">This PowerShell script should be run locally while RDP’d into IIS01.</span></span>

```PowerShell
# IIS Server Post Build Config Script
# Get Admin Account and Password
    Write-Host "Please enter the admin account information used to create this VM:" -ForegroundColor Cyan
    $theAdmin = Read-Host -Prompt "The Admin Account Name (no domain or machine name)"
    $thePassword = Read-Host -Prompt "The Admin Password"

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
          This is a page from the inside (a web server on a private network),<br />
          and it is making its way to the outside! (If you are viewing this from the internet)<br />
          <br />
          The following sections show:
          <ul style="margin-top: 0px;">
            <li> Local Server Time - Shows if this page is or isnt cached anywhere</li>
            <li> File Output - Shows that the web server is reaching AppVM01 on the backend subnet and successfully returning content</li>
            <li> Image from the Internet - Doesnt really show anything, but it made me happy to see this when the app worked</li>
          </ul>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Local Web Server Time</b>: <asp:Label runat="server" ID="lblTime" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>File Output from AppVM01</b>: <asp:Label runat="server" ID="lblOutput" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Image File Linked from the Internet</b>:<br />
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

# Set App Pool to Clasic Pipeline to remote file access will work easier
    Write-Host "Updaing IIS Settings" -ForegroundColor Cyan
    c:\windows\system32\inetsrv\appcmd.exe set app "Default Web Site/" /applicationPool:".NET v4.5 Classic"
    c:\windows\system32\inetsrv\appcmd.exe set config "Default Web Site/" /section:system.webServer/security/authentication/anonymousAuthentication /userName:$theAdmin /password:$thePassword /commit:apphost

# Make sure the IIS settings take
    Write-Host "Restarting the W3SVC" -ForegroundColor Cyan
    Restart-Service -Name W3SVC

    Write-Host
    Write-Host "Web App Creation Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="appvm01---file-server-installation-script"></a><span data-ttu-id="ea5b1-119">AppVM01 - dosya sunucusu yükleme betiği</span><span class="sxs-lookup"><span data-stu-id="ea5b1-119">AppVM01 - File server installation script</span></span>
<span data-ttu-id="ea5b1-120">Bu komut dosyası basit bu uygulama için arka uç ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ea5b1-120">This script sets up the back-end for this simple application.</span></span> <span data-ttu-id="ea5b1-121">Bu komut dosyası aşağıdakileri yapar:</span><span class="sxs-lookup"><span data-stu-id="ea5b1-121">This script will:</span></span>

1. <span data-ttu-id="ea5b1-122">Açık IMCPv4 (Ping) daha kolay test etmek için Güvenlik Duvarı'nda</span><span class="sxs-lookup"><span data-stu-id="ea5b1-122">Open IMCPv4 (Ping) on the firewall for easier testing</span></span>
2. <span data-ttu-id="ea5b1-123">Web sitesi için bir dizin oluşturun</span><span class="sxs-lookup"><span data-stu-id="ea5b1-123">Create a directory for the web site</span></span>
3. <span data-ttu-id="ea5b1-124">Uzaktan Erişim tarafından web sayfasını olması için bir metin dosyası oluşturun</span><span class="sxs-lookup"><span data-stu-id="ea5b1-124">Create a text file to be remotely access by the web page</span></span>
4. <span data-ttu-id="ea5b1-125">Anonim erişime izin vermek için dosya ve dizin izinlerini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="ea5b1-125">Set permissions on the directory and file to Anonymous to allow access</span></span>
5. <span data-ttu-id="ea5b1-126">IE Artırılmış Güvenlik bu sunucudan daha kolay gezinme izin vermek için devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="ea5b1-126">Turn off IE Enhanced Security to allow easier browsing from this server</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ea5b1-127">**En iyi uygulaması**: hiçbir zaman bir üretim sunucuda IE Artırılmış Güvenlik devre dışı kapatın, artı, genellikle bir üretim sunucusundan Web'de gezinmek için kötü bir fikirdir.</span><span class="sxs-lookup"><span data-stu-id="ea5b1-127">**Best Practice**: Never turn off IE Enhanced Security on a production server, plus it's generally a bad idea to surf the web from a production server.</span></span> <span data-ttu-id="ea5b1-128">Ayrıca, dosya paylaşımları anonim erişim için açma tamamlandı ancak kötü bir fikir burada kolaylık sağlamak için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="ea5b1-128">Also, opening up file shares for anonymous access is a bad idea, but done here for simplicity.</span></span>
> 
> 

<span data-ttu-id="ea5b1-129">RDP AppVM01 alırken bu PowerShell komut dosyasını yerel olarak çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea5b1-129">This PowerShell script should be run locally while RDP’d into AppVM01.</span></span> <span data-ttu-id="ea5b1-130">PowerShell aktarılmadığı sağlamak için yönetici olarak çalıştırmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ea5b1-130">PowerShell is required to be run as Administrator to ensure successful execution.</span></span>

```PowerShell
# AppVM01 Server Post Build Config Script
# PowerShell must be run as Administrator for Net Share commands to work

# Turn On ICMPv4
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Create Directory
    New-Item "C:\WebShare" -ItemType Directory

# Write out Rand.txt
    $FileContent = "Hello, I'm the contents of a remote file on AppVM01."
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

## <a name="dns01---dns-server-installation-script"></a><span data-ttu-id="ea5b1-131">DNS01 - DNS sunucusu yükleme betiği</span><span class="sxs-lookup"><span data-stu-id="ea5b1-131">DNS01 - DNS server installation script</span></span>
<span data-ttu-id="ea5b1-132">DNS sunucusu kurmak için bu örnek uygulama dahil betik yok.</span><span class="sxs-lookup"><span data-stu-id="ea5b1-132">There is no script included in this sample application to set up the DNS server.</span></span> <span data-ttu-id="ea5b1-133">Güvenlik duvarı kuralları, NSG veya UDR sınama DNS trafiğinin eklenmesi gerekiyorsa, DNS01 sunucusunun elle ayarlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea5b1-133">If testing of the firewall rules, NSG, or UDR needs to include DNS traffic, the DNS01 server needs to be set up manually.</span></span> <span data-ttu-id="ea5b1-134">Ağ yapılandırma xml dosyasını ve Resource Manager şablonu hem örnekleri için birincil DNS sunucusu ve düzeyi 3'ü yedekleme DNS sunucusu tarafından barındırılan ortak DNS sunucusu olarak DNS01 içerir.</span><span class="sxs-lookup"><span data-stu-id="ea5b1-134">The Network Configuration xml file and Resource Manager Template for both examples includes DNS01 as the primary DNS server and the public DNS server hosted by Level 3 as the backup DNS server.</span></span> <span data-ttu-id="ea5b1-135">Düzey 3 DNS sunucusu yerel olmayan trafik için kullanılan gerçek bir DNS sunucusunun ve DNS01 ile ayarlanmadı, DNS oluşacak yerel ağ.</span><span class="sxs-lookup"><span data-stu-id="ea5b1-135">The Level 3 DNS server would be the actual DNS server used for non-local traffic, and with DNS01 not setup, no local network DNS would occur.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea5b1-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ea5b1-136">Next steps</span></span>
* <span data-ttu-id="ea5b1-137">Bir IIS sunucusunda IIS01 komut dosyasını çalıştır</span><span class="sxs-lookup"><span data-stu-id="ea5b1-137">Run the IIS01 script on an IIS server</span></span>
* <span data-ttu-id="ea5b1-138">AppVM01 üzerinde dosya sunucusu komut dosyasını çalıştır</span><span class="sxs-lookup"><span data-stu-id="ea5b1-138">Run File Server script on AppVM01</span></span>
* <span data-ttu-id="ea5b1-139">IIS01 yapınızın doğrulamak için ortak IP göz atın</span><span class="sxs-lookup"><span data-stu-id="ea5b1-139">Browse to the Public IP on IIS01 to validate your build</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
