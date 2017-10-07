---
title: "Azure VM'ler için aaaSpecific RDP hata iletileri | Microsoft Docs"
description: "Azure'da Uzak Masaüstü Bağlantısı tooa Windows sanal makine çalışırken karşılaşabileceğiniz belirli hata iletilerinin kullanımını anlamanıza"
keywords: "Uzak Masaüstü hata, Uzak Masaüstü Bağlantısı hatası tooVM, bağlanamıyor Uzak Masaüstü sorunlarını giderme"
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
ms.openlocfilehash: 8e1551be23e696bd60adbd76c3e1ea86d9dd11aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-specific-rdp-error-messages-tooa-windows-vm-in-azure"></a><span data-ttu-id="e1f59-104">Özel RDP hata iletileri tooa Azure Windows VM sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="e1f59-104">Troubleshooting specific RDP error messages tooa Windows VM in Azure</span></span>
<span data-ttu-id="e1f59-105">Uzak Masaüstü Bağlantısı tooa Windows sanal makine (VM) Azure'da kullanırken, belirli bir hata iletisi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1f59-105">You may receive a specific error message when using Remote Desktop connection tooa Windows virtual machine (VM) in Azure.</span></span> <span data-ttu-id="e1f59-106">Bazı hello karşılaşılan, sorun giderme adımları tooresolve yanı sıra daha sık karşılaşılan hata iletileri bu makale ayrıntıları bunları.</span><span class="sxs-lookup"><span data-stu-id="e1f59-106">This article details some of hello more common error messages encountered, along with troubleshooting steps tooresolve them.</span></span> <span data-ttu-id="e1f59-107">Tooyour VM bağlantı sorunları yaşıyorsanız RDP kullanmayan belirli bir hata iletisi karşılaşırsanız bkz hello [Uzak Masaüstü için sorun giderme kılavuzu](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e1f59-107">If you are having issues connecting tooyour VM using RDP but do not encounter a specific error message, see hello [troubleshooting guide for Remote Desktop](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="e1f59-108">Özel hata iletileri hakkında daha fazla bilgi için hello aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="e1f59-108">For information on specific error messages, see hello following:</span></span>

* <span data-ttu-id="e1f59-109">[bir lisans yok Uzak Masaüstü lisans sunucularını kullanılabilir tooprovide olduğundan Hello uzak oturum kesildi](#rdplicense).</span><span class="sxs-lookup"><span data-stu-id="e1f59-109">[hello remote session was disconnected because there are no Remote Desktop License Servers available tooprovide a license](#rdplicense).</span></span>
* <span data-ttu-id="e1f59-110">[Uzak Masaüstü bilgisayar "name" Merhaba bulamıyor](#rdpname).</span><span class="sxs-lookup"><span data-stu-id="e1f59-110">[Remote Desktop can't find hello computer "name"](#rdpname).</span></span>
* <span data-ttu-id="e1f59-111">[Bir kimlik doğrulama hatası oluştu. Merhaba yerel güvenlik yetkilisi kurulamıyor](#rdpauth).</span><span class="sxs-lookup"><span data-stu-id="e1f59-111">[An authentication error has occurred. hello Local Security Authority cannot be contacted](#rdpauth).</span></span>
* <span data-ttu-id="e1f59-112">[Windows güvenlik hatası: kimlik bilgilerinizi çalışmama](#wincred).</span><span class="sxs-lookup"><span data-stu-id="e1f59-112">[Windows Security error: Your credentials did not work](#wincred).</span></span>
* <span data-ttu-id="e1f59-113">[Bu bilgisayar toohello uzak bilgisayara bağlanamıyor](#rdpconnect).</span><span class="sxs-lookup"><span data-stu-id="e1f59-113">[This computer can't connect toohello remote computer](#rdpconnect).</span></span>

<a id="rdplicense"></a>

## <a name="hello-remote-session-was-disconnected-because-there-are-no-remote-desktop-license-servers-available-tooprovide-a-license"></a><span data-ttu-id="e1f59-114">hiçbir Uzak Masaüstü lisans sunucularını kullanılabilir tooprovide lisans olduğundan hello uzak oturum sonlandırıldı.</span><span class="sxs-lookup"><span data-stu-id="e1f59-114">hello remote session was disconnected because there are no Remote Desktop License Servers available tooprovide a license.</span></span>
<span data-ttu-id="e1f59-115">Neden: hello 120 gün hello Uzak Masaüstü Sunucusu rolü için lisans yetkisiz kullanım süresi dolmuştur ve tooinstall lisans gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="e1f59-115">Cause: hello 120-day licensing grace period for hello Remote Desktop Server role has expired and you need tooinstall licenses.</span></span>

<span data-ttu-id="e1f59-116">Geçici bir çözüm olarak hello portalından hello RDP dosyasını yerel bir kopyasını kaydedin ve PowerShell komut istemi tooconnect bu komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e1f59-116">As a workaround, save a local copy of hello RDP file from hello portal and run this command at a PowerShell command prompt tooconnect.</span></span> <span data-ttu-id="e1f59-117">Bu adım yalnızca o bağlantı için lisans devre dışı bırakır:</span><span class="sxs-lookup"><span data-stu-id="e1f59-117">This step disables licensing for just that connection:</span></span>

        mstsc <File name>.RDP /admin

<span data-ttu-id="e1f59-118">İkiden fazla eşzamanlı uzak masaüstü bağlantıları toohello VM gerçekten gerek duymuyorsanız, Sunucu Yöneticisi'ni tooremove hello Uzak Masaüstü sunucu rolünü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1f59-118">If you don't actually need more than two simultaneous Remote Desktop connections toohello VM, you can use Server Manager tooremove hello Remote Desktop Server role.</span></span>

<span data-ttu-id="e1f59-119">Daha fazla bilgi için bkz: hello blog gönderisi [Azure VM başarısız "Hiçbir Uzak Masaüstü lisans sunucusu ile"](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/).</span><span class="sxs-lookup"><span data-stu-id="e1f59-119">For more information, see hello blog post [Azure VM fails with "No Remote Desktop License Servers available"](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/).</span></span>

<a id="rdpname"></a>

## <a name="remote-desktop-cant-find-hello-computer-name"></a><span data-ttu-id="e1f59-120">Uzak Masaüstü hello bilgisayar "name" bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="e1f59-120">Remote Desktop can't find hello computer "name".</span></span>
<span data-ttu-id="e1f59-121">Neden: hello Uzak Masaüstü İstemcisi bilgisayarınızda hello RDP dosyasının hello ayarlarını hello bilgisayarın hello adı çözümlenemiyor.</span><span class="sxs-lookup"><span data-stu-id="e1f59-121">Cause: hello Remote Desktop client on your computer can't resolve hello name of hello computer in hello settings of hello RDP file.</span></span>

<span data-ttu-id="e1f59-122">Olası çözümler:</span><span class="sxs-lookup"><span data-stu-id="e1f59-122">Possible solutions:</span></span>

* <span data-ttu-id="e1f59-123">Bir kuruluşun intranet üzerinde değilseniz, bilgisayarınızın erişim toohello proxy sunucusu vardır ve HTTPS trafiği tooit gönderebilirsiniz emin olun.</span><span class="sxs-lookup"><span data-stu-id="e1f59-123">If you're on an organization's intranet, make sure that your computer has access toohello proxy server and can send HTTPS traffic tooit.</span></span>
* <span data-ttu-id="e1f59-124">Yerel olarak saklanan bir RDP dosyası kullanıyorsanız, hello portal tarafından oluşturulan hello birini kullanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="e1f59-124">If you're using a locally stored RDP file, try using hello one that's generated by hello portal.</span></span> <span data-ttu-id="e1f59-125">Bu adım, hello sanal makine veya hello bulut hizmeti ve hello VM hello uç nokta bağlantı noktası için doğru DNS adı hello sahip olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="e1f59-125">This step ensures that you have hello correct DNS name for hello virtual machine, or hello cloud service and hello endpoint port of hello VM.</span></span> <span data-ttu-id="e1f59-126">Örnek, hello portal tarafından oluşturulan bir RDP dosyası şöyledir:</span><span class="sxs-lookup"><span data-stu-id="e1f59-126">Here is a sample RDP file generated by hello portal:</span></span>
  
        full address:s:tailspin-azdatatier.cloudapp.net:55919
        prompt for credentials:i:1

<span data-ttu-id="e1f59-127">Bu RDP dosyası Hello adres bölümü vardır:</span><span class="sxs-lookup"><span data-stu-id="e1f59-127">hello address portion of this RDP file has:</span></span>

* <span data-ttu-id="e1f59-128">Merhaba tam etki alanı adı hello VM ("tailspin-azdatatier.cloudapp.net" Bu örnekte) içeren hello bulut hizmetinin.</span><span class="sxs-lookup"><span data-stu-id="e1f59-128">hello fully qualified domain name of hello cloud service that contains hello VM ("tailspin-azdatatier.cloudapp.net" in this example).</span></span>
* <span data-ttu-id="e1f59-129">Merhaba dış TCP bağlantı noktası hello uç noktasının Uzak Masaüstü trafiği (55919).</span><span class="sxs-lookup"><span data-stu-id="e1f59-129">hello external TCP port of hello endpoint for Remote Desktop traffic (55919).</span></span>

<a id="rdpauth"></a>

## <a name="an-authentication-error-has-occurred-hello-local-security-authority-cannot-be-contacted"></a><span data-ttu-id="e1f59-130">Bir kimlik doğrulama hatası oluştu.</span><span class="sxs-lookup"><span data-stu-id="e1f59-130">An authentication error has occurred.</span></span> <span data-ttu-id="e1f59-131">Merhaba yerel güvenlik yetkilisi iletişim kurulamıyor.</span><span class="sxs-lookup"><span data-stu-id="e1f59-131">hello Local Security Authority cannot be contacted.</span></span>
<span data-ttu-id="e1f59-132">Neden: hello hedef VM hello kullanıcı adının kısmında kimlik bilgilerinizi hello güvenlik yetkilisi bulamıyor.</span><span class="sxs-lookup"><span data-stu-id="e1f59-132">Cause: hello target VM can't locate hello security authority in hello user name portion of your credentials.</span></span>

<span data-ttu-id="e1f59-133">Kullanıcı adınızı hello formunda olduğunda *SecurityAuthority*\\*kullanıcıadı* (örnek: CORP\User1), hello *SecurityAuthority* bölümüdür ya da hello VM's bilgisayar adı (Merhaba yerel güvenlik yetkilisi) veya bir Active Directory etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="e1f59-133">When your user name is in hello form *SecurityAuthority*\\*UserName* (example: CORP\User1), hello *SecurityAuthority* portion is either hello VM's computer name (for hello local security authority) or an Active Directory domain name.</span></span>

<span data-ttu-id="e1f59-134">Olası çözümler:</span><span class="sxs-lookup"><span data-stu-id="e1f59-134">Possible solutions:</span></span>

* <span data-ttu-id="e1f59-135">Merhaba hesabı yerel toohello VM ise, o hello VM adının doğru yazıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="e1f59-135">If hello account is local toohello VM, make sure that hello VM name is spelled correctly.</span></span>
* <span data-ttu-id="e1f59-136">Hello hesap bir Active Directory etki alanındaysa hello hello etki alanı adının yazımını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="e1f59-136">If hello account is on an Active Directory domain, check hello spelling of hello domain name.</span></span>
* <span data-ttu-id="e1f59-137">Bir Active Directory etki alanı hesabı ise ve hello etki alanı adının doğru yazıldığından, bu etki alanında etki alanı denetleyicisinin kullanılabilir olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e1f59-137">If it is an Active Directory domain account and hello domain name is spelled correctly, verify that a domain controller is available in that domain.</span></span> <span data-ttu-id="e1f59-138">Başlatılan kurmadı için bir etki alanı denetleyicisi kullanılamıyor etki alanı denetleyicileri içeren Azure sanal ağlarda yaygın bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="e1f59-138">It's a common issue in Azure virtual networks that contain domain controllers that a domain controller is unavailable because it hasn't been started.</span></span> <span data-ttu-id="e1f59-139">Geçici bir çözüm olarak, bir etki alanı hesabı yerine yerel yönetici hesabı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1f59-139">As a workaround, you can use a local administrator account instead of a domain account.</span></span>

<a id="wincred"></a>

## <a name="windows-security-error-your-credentials-did-not-work"></a><span data-ttu-id="e1f59-140">Windows güvenlik hatası: kimlik bilgilerinizi çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="e1f59-140">Windows Security error: Your credentials did not work.</span></span>
<span data-ttu-id="e1f59-141">Neden: hesap adı ve parola hello hedef VM doğrulanamıyor.</span><span class="sxs-lookup"><span data-stu-id="e1f59-141">Cause: hello target VM can't validate your account name and password.</span></span>

<span data-ttu-id="e1f59-142">Windows tabanlı bir bilgisayarda yerel bir hesap veya bir etki alanı hesabı hello kimlik doğrulayabilir.</span><span class="sxs-lookup"><span data-stu-id="e1f59-142">A Windows-based computer can validate hello credentials of either a local account or a domain account.</span></span>

* <span data-ttu-id="e1f59-143">Yerel hesaplar için hello kullan *ComputerName*\\*kullanıcıadı* sözdizimi (örnek: SQL1\Admin4798).</span><span class="sxs-lookup"><span data-stu-id="e1f59-143">For local accounts, use hello *ComputerName*\\*UserName* syntax (example: SQL1\Admin4798).</span></span>
* <span data-ttu-id="e1f59-144">Etki alanı hesapları için hello kullanmak *DomainName*\\*kullanıcıadı* sözdizimi (örnek: CONTOSO\peterodman).</span><span class="sxs-lookup"><span data-stu-id="e1f59-144">For domain accounts, use hello *DomainName*\\*UserName* syntax (example: CONTOSO\peterodman).</span></span>

<span data-ttu-id="e1f59-145">VM tooa etki alanı denetleyicinizi yeni bir Active Directory ormanında yükselttiyseniz, oturum hello yerel yönetici hesabı dönüştürülür tooan eşdeğer hesap hello ile aynı parola hello yeni orman ve etki alanı.</span><span class="sxs-lookup"><span data-stu-id="e1f59-145">If you have promoted your VM tooa domain controller in a new Active Directory forest, hello local administrator account that you signed in with is converted tooan equivalent account with hello same password in hello new forest and domain.</span></span> <span data-ttu-id="e1f59-146">Merhaba yerel hesap sonra silinir.</span><span class="sxs-lookup"><span data-stu-id="e1f59-146">hello local account is then deleted.</span></span>

<span data-ttu-id="e1f59-147">Örneğin, hello yerel hesabıyla DC1\DCAdmin oturum açmış ve hello corp.contoso.com etki alanı için yeni bir orman içindeki etki alanı denetleyicisi olarak hello sanal makine tanıtılması, DC1\DCAdmin yerel hesap silinir ve yeni bir etki alanı hesabı (CORP\DCAdmin hello ) ile Merhaba aynı oluşturulan parola.</span><span class="sxs-lookup"><span data-stu-id="e1f59-147">For example, if you signed in with hello local account DC1\DCAdmin, and then promoted hello virtual machine as a domain controller in a new forest for hello corp.contoso.com domain, hello DC1\DCAdmin local account gets deleted and a new domain account (CORP\DCAdmin) is created with hello same password.</span></span>

<span data-ttu-id="e1f59-148">Merhaba hesap adının hello sanal makine geçerli bir hesap doğrulayabilir ve hello parola doğru bir adı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e1f59-148">Make sure that hello account name is a name that hello virtual machine can verify as a valid account, and that hello password is correct.</span></span>

<span data-ttu-id="e1f59-149">Toochange hello hello yerel yönetici hesabının parolasını gerekirse bkz [nasıl tooreset bir parola veya hello Uzak Masaüstü hizmet Windows sanal makineler için](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e1f59-149">If you need toochange hello password of hello local administrator account, see [How tooreset a password or hello Remote Desktop service for Windows virtual machines](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<a id="rdpconnect"></a>

## <a name="this-computer-cant-connect-toohello-remote-computer"></a><span data-ttu-id="e1f59-150">Bu bilgisayar toohello uzak bilgisayara bağlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="e1f59-150">This computer can't connect toohello remote computer.</span></span>
<span data-ttu-id="e1f59-151">Neden: tooconnect kullandı hello hesabı Uzak Masaüstü Oturum açma hakları yok.</span><span class="sxs-lookup"><span data-stu-id="e1f59-151">Cause: hello account that's used tooconnect does not have Remote Desktop sign-in rights.</span></span>

<span data-ttu-id="e1f59-152">Her Windows bilgisayarın, içine uzaktan oturum hello hesapları ve grupları içeren bir Uzak Masaüstü Kullanıcıları yerel grubu vardır.</span><span class="sxs-lookup"><span data-stu-id="e1f59-152">Every Windows computer has a Remote Desktop users local group, which contains hello accounts and groups that can sign into it remotely.</span></span> <span data-ttu-id="e1f59-153">Bu hesapların hello Uzak Masaüstü Kullanıcıları yerel grubuna listelenmeyen olsa bile hello yerel administrators grubunun üyeleri aynı zamanda, erişimi.</span><span class="sxs-lookup"><span data-stu-id="e1f59-153">Members of hello local administrators group also have access, even though those accounts are not listed in hello Remote Desktop users local group.</span></span> <span data-ttu-id="e1f59-154">Etki alanına katılan makineler için hello yerel Yöneticiler grubunun da hello hello etki alanı için etki alanı yöneticileri içerir.</span><span class="sxs-lookup"><span data-stu-id="e1f59-154">For domain-joined machines, hello local administrators group also contains hello domain administrators for hello domain.</span></span>

<span data-ttu-id="e1f59-155">Tooconnect ile kullanmakta olduğunuz hello hesabı Uzak Masaüstü Oturum açma hakları olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e1f59-155">Make sure that hello account you're using tooconnect with has Remote Desktop sign-in rights.</span></span> <span data-ttu-id="e1f59-156">Geçici bir çözüm olarak, bir etki alanı veya yerel yönetici hesabı tooconnect, Uzak Masaüstü'nü kullanın.</span><span class="sxs-lookup"><span data-stu-id="e1f59-156">As a workaround, use a domain or local administrator account tooconnect over Remote Desktop.</span></span> <span data-ttu-id="e1f59-157">tooadd istenen hesap toohello Uzak Masaüstü Kullanıcıları yerel grubu Merhaba, hello Microsoft Yönetim Konsolu ek bileşenini kullanın (**Sistem Araçları > yerel kullanıcılar ve Gruplar > Gruplar > Uzak Masaüstü Kullanıcıları**).</span><span class="sxs-lookup"><span data-stu-id="e1f59-157">tooadd hello desired account toohello Remote Desktop users local group, use hello Microsoft Management Console snap-in (**System Tools > Local Users and Groups > Groups > Remote Desktop Users**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1f59-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e1f59-158">Next steps</span></span>
<span data-ttu-id="e1f59-159">Hiçbiri bu hatalar oluştu ve RDP kullanarak bağlanma bilinmeyen bir sorun varsa, hello bkz [Uzak Masaüstü için sorun giderme kılavuzu](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e1f59-159">If none of these errors occurred and you have an unknown issue with connecting using RDP, see hello [troubleshooting guide for Remote Desktop](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="e1f59-160">Bir VM üzerinde çalışan uygulamalar erişimde adımları sorun giderme için bkz: [bir Azure VM üzerinde çalışan sorun giderme erişim tooan uygulama](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e1f59-160">For troubleshooting steps in accessing applications running on a VM, see [Troubleshoot access tooan application running on an Azure VM](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="e1f59-161">Azure'da güvenli Kabuk (SSH) tooconnect tooa Linux VM kullanma sorunu yaşıyor olup [sorun giderme SSH bağlantıları tooa Azure Linux VM'de](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e1f59-161">If you are having issues using Secure Shell (SSH) tooconnect tooa Linux VM in Azure, see [Troubleshoot SSH connections tooa Linux VM in Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

