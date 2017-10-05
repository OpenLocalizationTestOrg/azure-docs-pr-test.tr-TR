---
title: "Azure VM'ler için belirli RDP hata iletileri | Microsoft Docs"
description: "Azure'da Windows sanal makine için Uzak Masaüstü Bağlantısı çalışırken karşılaşabileceğiniz belirli hata iletilerinin kullanımını anlamanıza"
keywords: "Uzak Masaüstü hata, Uzak Masaüstü Bağlantısı hatası, VM için bağlantı kuramıyor Uzak Masaüstü sorunlarını giderme"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 5feb1d64-ee6f-4907-949a-a7cffcbc6153
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: e7c049106726a15e96d4ebe7c7c0388a29c546c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-specific-rdp-error-messages-to-a-windows-vm-in-azure"></a><span data-ttu-id="443fb-104">Bir Windows VM Azure belirli RDP hata iletileri sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="443fb-104">Troubleshooting specific RDP error messages to a Windows VM in Azure</span></span>
<span data-ttu-id="443fb-105">Azure'da Windows sanal makine (VM) için Uzak Masaüstü bağlantısı kullanırken, belirli bir hata iletisi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="443fb-105">You may receive a specific error message when using Remote Desktop connection to a Windows virtual machine (VM) in Azure.</span></span> <span data-ttu-id="443fb-106">Bu makalede bazı karşılaştı, sorun giderme bunları gidermek için adımları yanı sıra daha sık karşılaşılan hata iletileri ayrıntılarını verir.</span><span class="sxs-lookup"><span data-stu-id="443fb-106">This article details some of the more common error messages encountered, along with troubleshooting steps to resolve them.</span></span> <span data-ttu-id="443fb-107">VM'nize bağlantı sorunları yaşıyorsanız RDP kullanmayan belirli bir hata iletisi karşılaşırsanız bkz [Uzak Masaüstü için sorun giderme kılavuzu](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="443fb-107">If you are having issues connecting to your VM using RDP but do not encounter a specific error message, see the [troubleshooting guide for Remote Desktop](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="443fb-108">Özel hata iletileri hakkında daha fazla bilgi için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="443fb-108">For information on specific error messages, see the following:</span></span>

* <span data-ttu-id="443fb-109">[Uzak Masaüstü lisans sunucusu lisans sağlamak kullanılabilir olmadığından uzak oturum kesildi](#rdplicense).</span><span class="sxs-lookup"><span data-stu-id="443fb-109">[The remote session was disconnected because there are no Remote Desktop License Servers available to provide a license](#rdplicense).</span></span>
* <span data-ttu-id="443fb-110">[Uzak Masaüstü bilgisayar "name" bulamıyor](#rdpname).</span><span class="sxs-lookup"><span data-stu-id="443fb-110">[Remote Desktop can't find the computer "name"](#rdpname).</span></span>
* <span data-ttu-id="443fb-111">[Bir kimlik doğrulama hatası oluştu. Yerel Güvenlik Yetkilisi kurulamıyor](#rdpauth).</span><span class="sxs-lookup"><span data-stu-id="443fb-111">[An authentication error has occurred. The Local Security Authority cannot be contacted](#rdpauth).</span></span>
* <span data-ttu-id="443fb-112">[Windows güvenlik hatası: kimlik bilgilerinizi çalışmama](#wincred).</span><span class="sxs-lookup"><span data-stu-id="443fb-112">[Windows Security error: Your credentials did not work](#wincred).</span></span>
* <span data-ttu-id="443fb-113">[Bu bilgisayar uzak bilgisayara bağlanamıyor](#rdpconnect).</span><span class="sxs-lookup"><span data-stu-id="443fb-113">[This computer can't connect to the remote computer](#rdpconnect).</span></span>

<a id="rdplicense"></a>

## <a name="the-remote-session-was-disconnected-because-there-are-no-remote-desktop-license-servers-available-to-provide-a-license"></a><span data-ttu-id="443fb-114">Uzak Masaüstü lisans sunucusu lisans sağlamak kullanılabilir olmadığından uzak oturum bağlantısı kesildi.</span><span class="sxs-lookup"><span data-stu-id="443fb-114">The remote session was disconnected because there are no Remote Desktop License Servers available to provide a license.</span></span>
<span data-ttu-id="443fb-115">Neden: Uzak Masaüstü Sunucusu rolü için 120 gün lisans yetkisiz kullanım süresi dolmuştur ve lisansları yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="443fb-115">Cause: The 120-day licensing grace period for the Remote Desktop Server role has expired and you need to install licenses.</span></span>

<span data-ttu-id="443fb-116">Geçici bir çözüm olarak portaldan RDP dosyasını yerel bir kopyasını kaydedin ve bağlanmak için PowerShell komut isteminde şu komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="443fb-116">As a workaround, save a local copy of the RDP file from the portal and run this command at a PowerShell command prompt to connect.</span></span> <span data-ttu-id="443fb-117">Bu adım yalnızca o bağlantı için lisans devre dışı bırakır:</span><span class="sxs-lookup"><span data-stu-id="443fb-117">This step disables licensing for just that connection:</span></span>

        mstsc <File name>.RDP /admin

<span data-ttu-id="443fb-118">VM ikiden fazla eşzamanlı uzak masaüstü bağlantıları gerçekten gerek duymuyorsanız, Uzak Masaüstü sunucu rolünü kaldırmak için Sunucu Yöneticisi'ni kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="443fb-118">If you don't actually need more than two simultaneous Remote Desktop connections to the VM, you can use Server Manager to remove the Remote Desktop Server role.</span></span>

<span data-ttu-id="443fb-119">Daha fazla bilgi için blog gönderisine bakın [Azure VM başarısız "Hiçbir Uzak Masaüstü lisans sunucusu ile"](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/).</span><span class="sxs-lookup"><span data-stu-id="443fb-119">For more information, see the blog post [Azure VM fails with "No Remote Desktop License Servers available"](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/).</span></span>

<a id="rdpname"></a>

## <a name="remote-desktop-cant-find-the-computer-name"></a><span data-ttu-id="443fb-120">Uzak Masaüstü bilgisayar "name" bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="443fb-120">Remote Desktop can't find the computer "name".</span></span>
<span data-ttu-id="443fb-121">Neden: Uzak Masaüstü İstemcisi bilgisayarınızda RDP dosyasını ayarlarında bilgisayarın adını çözümleyemiyor.</span><span class="sxs-lookup"><span data-stu-id="443fb-121">Cause: The Remote Desktop client on your computer can't resolve the name of the computer in the settings of the RDP file.</span></span>

<span data-ttu-id="443fb-122">Olası çözümler:</span><span class="sxs-lookup"><span data-stu-id="443fb-122">Possible solutions:</span></span>

* <span data-ttu-id="443fb-123">Bir kuruluşun intranet üzerinde değilseniz, bilgisayarınızı proxy sunucusu erişimi ve HTTPS trafiğinin gönderebilir emin olun.</span><span class="sxs-lookup"><span data-stu-id="443fb-123">If you're on an organization's intranet, make sure that your computer has access to the proxy server and can send HTTPS traffic to it.</span></span>
* <span data-ttu-id="443fb-124">Yerel olarak saklanan bir RDP dosyası kullanıyorsanız, portal tarafından oluşturulan bir kullanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="443fb-124">If you're using a locally stored RDP file, try using the one that's generated by the portal.</span></span> <span data-ttu-id="443fb-125">Bu adım sanal makinenin veya Bulut hizmeti ve uç nokta bağlantı noktası VM için doğru bir DNS adı sahip olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="443fb-125">This step ensures that you have the correct DNS name for the virtual machine, or the cloud service and the endpoint port of the VM.</span></span> <span data-ttu-id="443fb-126">Portal tarafından oluşturulan örnek bir RDP dosyası şöyledir:</span><span class="sxs-lookup"><span data-stu-id="443fb-126">Here is a sample RDP file generated by the portal:</span></span>
  
        full address:s:tailspin-azdatatier.cloudapp.net:55919
        prompt for credentials:i:1

<span data-ttu-id="443fb-127">Bu RDP dosyası adres bölümü vardır:</span><span class="sxs-lookup"><span data-stu-id="443fb-127">The address portion of this RDP file has:</span></span>

* <span data-ttu-id="443fb-128">("Tailspin-azdatatier.cloudapp.net" Bu örnekte) VM içeren bulut hizmeti tam olarak nitelenmiş etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="443fb-128">The fully qualified domain name of the cloud service that contains the VM ("tailspin-azdatatier.cloudapp.net" in this example).</span></span>
* <span data-ttu-id="443fb-129">Dış TCP bağlantı noktasını uç nokta için Uzak Masaüstü trafiği (55919).</span><span class="sxs-lookup"><span data-stu-id="443fb-129">The external TCP port of the endpoint for Remote Desktop traffic (55919).</span></span>

<a id="rdpauth"></a>

## <a name="an-authentication-error-has-occurred-the-local-security-authority-cannot-be-contacted"></a><span data-ttu-id="443fb-130">Bir kimlik doğrulama hatası oluştu.</span><span class="sxs-lookup"><span data-stu-id="443fb-130">An authentication error has occurred.</span></span> <span data-ttu-id="443fb-131">Yerel Güvenlik Yetkilisi iletişim kurulamıyor.</span><span class="sxs-lookup"><span data-stu-id="443fb-131">The Local Security Authority cannot be contacted.</span></span>
<span data-ttu-id="443fb-132">Neden: Hedef VM kimlik bilgilerinizi kullanıcı adı kısmını güvenlik yetkilisi bulamıyor.</span><span class="sxs-lookup"><span data-stu-id="443fb-132">Cause: The target VM can't locate the security authority in the user name portion of your credentials.</span></span>

<span data-ttu-id="443fb-133">Kullanıcı adınızı biçiminde olduğunda *SecurityAuthority*\\*kullanıcıadı* (örnek: CORP\User1), *SecurityAuthority* bölümüdür VM'in bilgisayar adı (yerel güvenlik yetkilisi) veya bir Active Directory etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="443fb-133">When your user name is in the form *SecurityAuthority*\\*UserName* (example: CORP\User1), the *SecurityAuthority* portion is either the VM's computer name (for the local security authority) or an Active Directory domain name.</span></span>

<span data-ttu-id="443fb-134">Olası çözümler:</span><span class="sxs-lookup"><span data-stu-id="443fb-134">Possible solutions:</span></span>

* <span data-ttu-id="443fb-135">Hesabı VM yerel ise, VM adının doğru yazıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="443fb-135">If the account is local to the VM, make sure that the VM name is spelled correctly.</span></span>
* <span data-ttu-id="443fb-136">Hesap bir Active Directory etki alanındaysa, etki alanı adının yazımını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="443fb-136">If the account is on an Active Directory domain, check the spelling of the domain name.</span></span>
* <span data-ttu-id="443fb-137">Bir Active Directory etki alanı hesabı ise ve etki alanı adının doğru yazıldığından, bu etki alanında etki alanı denetleyicisinin kullanılabilir olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="443fb-137">If it is an Active Directory domain account and the domain name is spelled correctly, verify that a domain controller is available in that domain.</span></span> <span data-ttu-id="443fb-138">Başlatılan kurmadı için bir etki alanı denetleyicisi kullanılamıyor etki alanı denetleyicileri içeren Azure sanal ağlarda yaygın bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="443fb-138">It's a common issue in Azure virtual networks that contain domain controllers that a domain controller is unavailable because it hasn't been started.</span></span> <span data-ttu-id="443fb-139">Geçici bir çözüm olarak, bir etki alanı hesabı yerine yerel yönetici hesabı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="443fb-139">As a workaround, you can use a local administrator account instead of a domain account.</span></span>

<a id="wincred"></a>

## <a name="windows-security-error-your-credentials-did-not-work"></a><span data-ttu-id="443fb-140">Windows güvenlik hatası: kimlik bilgilerinizi çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="443fb-140">Windows Security error: Your credentials did not work.</span></span>
<span data-ttu-id="443fb-141">Neden: Hedef VM hesap adı ve parola doğrulanamıyor.</span><span class="sxs-lookup"><span data-stu-id="443fb-141">Cause: The target VM can't validate your account name and password.</span></span>

<span data-ttu-id="443fb-142">Windows tabanlı bir bilgisayarda yerel bir hesap veya bir etki alanı hesabının kimlik bilgilerini doğrulayabilir.</span><span class="sxs-lookup"><span data-stu-id="443fb-142">A Windows-based computer can validate the credentials of either a local account or a domain account.</span></span>

* <span data-ttu-id="443fb-143">Yerel hesaplar için kullanmak *ComputerName*\\*kullanıcıadı* sözdizimi (örnek: SQL1\Admin4798).</span><span class="sxs-lookup"><span data-stu-id="443fb-143">For local accounts, use the *ComputerName*\\*UserName* syntax (example: SQL1\Admin4798).</span></span>
* <span data-ttu-id="443fb-144">Etki alanı hesapları için *DomainName*\\*kullanıcıadı* sözdizimi (örnek: CONTOSO\peterodman).</span><span class="sxs-lookup"><span data-stu-id="443fb-144">For domain accounts, use the *DomainName*\\*UserName* syntax (example: CONTOSO\peterodman).</span></span>

<span data-ttu-id="443fb-145">Yeni bir Active Directory ormanındaki etki alanı denetleyicisi, VM yükselttiyseniz, yeni orman ve etki alanında aynı parolayı eşdeğer bir hesapla oturum yerel yönetici hesabı dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="443fb-145">If you have promoted your VM to a domain controller in a new Active Directory forest, the local administrator account that you signed in with is converted to an equivalent account with the same password in the new forest and domain.</span></span> <span data-ttu-id="443fb-146">Yerel hesap sonra silinir.</span><span class="sxs-lookup"><span data-stu-id="443fb-146">The local account is then deleted.</span></span>

<span data-ttu-id="443fb-147">Örneğin, DC1\DCAdmin yerel hesabıyla oturum açtığınızdan ve bir etki alanı denetleyicisi corp.contoso.com etki alanı için yeni bir orman olarak sanal makine tanıtılması, DC1\DCAdmin yerel hesap silinir ve yeni bir etki alanı hesabı (CORP\DCAdmin) aynı parola ile oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="443fb-147">For example, if you signed in with the local account DC1\DCAdmin, and then promoted the virtual machine as a domain controller in a new forest for the corp.contoso.com domain, the DC1\DCAdmin local account gets deleted and a new domain account (CORP\DCAdmin) is created with the same password.</span></span>

<span data-ttu-id="443fb-148">Hesap adı sanal makine geçerli bir hesap doğrulayabilirsiniz bir adı olduğunu ve parolanın doğru olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="443fb-148">Make sure that the account name is a name that the virtual machine can verify as a valid account, and that the password is correct.</span></span>

<span data-ttu-id="443fb-149">Yerel yönetici hesabının parolasını değiştirmeniz gerekiyorsa, bkz: [bir parola veya Windows sanal makineler için Uzak Masaüstü hizmetini sıfırlayın nasıl](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="443fb-149">If you need to change the password of the local administrator account, see [How to reset a password or the Remote Desktop service for Windows virtual machines](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<a id="rdpconnect"></a>

## <a name="this-computer-cant-connect-to-the-remote-computer"></a><span data-ttu-id="443fb-150">Bu bilgisayar, uzak bilgisayara bağlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="443fb-150">This computer can't connect to the remote computer.</span></span>
<span data-ttu-id="443fb-151">Neden: bağlanmak için kullanılan hesabın Uzak Masaüstü Oturum açma hakları yok.</span><span class="sxs-lookup"><span data-stu-id="443fb-151">Cause: The account that's used to connect does not have Remote Desktop sign-in rights.</span></span>

<span data-ttu-id="443fb-152">Her Windows bilgisayar hesapları ve içine uzaktan oturum grupları içeren bir Uzak Masaüstü Kullanıcıları yerel grubu vardır.</span><span class="sxs-lookup"><span data-stu-id="443fb-152">Every Windows computer has a Remote Desktop users local group, which contains the accounts and groups that can sign into it remotely.</span></span> <span data-ttu-id="443fb-153">Bu hesaplar Uzak Masaüstü Kullanıcıları yerel Grup listelenmeyen olsa bile yerel Yöneticiler grubunun üyeleri, ayrıca, erişimi.</span><span class="sxs-lookup"><span data-stu-id="443fb-153">Members of the local administrators group also have access, even though those accounts are not listed in the Remote Desktop users local group.</span></span> <span data-ttu-id="443fb-154">Etki alanına katılan makineler için yerel Yöneticiler grubunun da etki alanı için etki alanı yöneticileri içerir.</span><span class="sxs-lookup"><span data-stu-id="443fb-154">For domain-joined machines, the local administrators group also contains the domain administrators for the domain.</span></span>

<span data-ttu-id="443fb-155">Bağlanmak için kullandığınız hesabın Uzak Masaüstü Oturum açma hakları olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="443fb-155">Make sure that the account you're using to connect with has Remote Desktop sign-in rights.</span></span> <span data-ttu-id="443fb-156">Geçici bir çözüm olarak, Uzak Masaüstü üzerinden bağlanmak için bir etki alanı veya yerel yönetici hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="443fb-156">As a workaround, use a domain or local administrator account to connect over Remote Desktop.</span></span> <span data-ttu-id="443fb-157">İstenen hesabı Uzak Masaüstü Kullanıcıları yerel grubuna eklemek için Microsoft Yönetim Konsolu ek bileşenini kullanın (**Sistem Araçları > yerel kullanıcılar ve Gruplar > Gruplar > Uzak Masaüstü Kullanıcıları**).</span><span class="sxs-lookup"><span data-stu-id="443fb-157">To add the desired account to the Remote Desktop users local group, use the Microsoft Management Console snap-in (**System Tools > Local Users and Groups > Groups > Remote Desktop Users**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="443fb-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="443fb-158">Next steps</span></span>
<span data-ttu-id="443fb-159">Hiçbiri bu hatalar oluştu ve RDP kullanarak bağlanma ile bkz bilinmeyen varsa [Uzak Masaüstü için sorun giderme kılavuzu](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="443fb-159">If none of these errors occurred and you have an unknown issue with connecting using RDP, see the [troubleshooting guide for Remote Desktop](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="443fb-160">Bir VM üzerinde çalışan uygulamalar erişimde adımları sorun giderme için bkz: [bir Azure VM üzerinde çalışan bir uygulama için erişim sorunlarını giderme](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="443fb-160">For troubleshooting steps in accessing applications running on a VM, see [Troubleshoot access to an application running on an Azure VM](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="443fb-161">Güvenli Kabuk (SSH) kullanarak azure'da bir Linux VM bağlanmak için bkz: sorunları yaşıyorsanız [sorun giderme SSH bağlantıları azure'da bir Linux VM](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="443fb-161">If you are having issues using Secure Shell (SSH) to connect to a Linux VM in Azure, see [Troubleshoot SSH connections to a Linux VM in Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

