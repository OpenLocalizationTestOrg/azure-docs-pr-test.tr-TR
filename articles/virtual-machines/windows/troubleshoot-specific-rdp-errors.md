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
# <a name="troubleshooting-specific-rdp-error-messages-tooa-windows-vm-in-azure"></a>Özel RDP hata iletileri tooa Azure Windows VM sorunlarını giderme
Uzak Masaüstü Bağlantısı tooa Windows sanal makine (VM) Azure'da kullanırken, belirli bir hata iletisi alabilirsiniz. Bazı hello karşılaşılan, sorun giderme adımları tooresolve yanı sıra daha sık karşılaşılan hata iletileri bu makale ayrıntıları bunları. Tooyour VM bağlantı sorunları yaşıyorsanız RDP kullanmayan belirli bir hata iletisi karşılaşırsanız bkz hello [Uzak Masaüstü için sorun giderme kılavuzu](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Özel hata iletileri hakkında daha fazla bilgi için hello aşağıdakilere bakın:

* [bir lisans yok Uzak Masaüstü lisans sunucularını kullanılabilir tooprovide olduğundan Hello uzak oturum kesildi](#rdplicense).
* [Uzak Masaüstü bilgisayar "name" Merhaba bulamıyor](#rdpname).
* [Bir kimlik doğrulama hatası oluştu. Merhaba yerel güvenlik yetkilisi kurulamıyor](#rdpauth).
* [Windows güvenlik hatası: kimlik bilgilerinizi çalışmama](#wincred).
* [Bu bilgisayar toohello uzak bilgisayara bağlanamıyor](#rdpconnect).

<a id="rdplicense"></a>

## <a name="hello-remote-session-was-disconnected-because-there-are-no-remote-desktop-license-servers-available-tooprovide-a-license"></a>hiçbir Uzak Masaüstü lisans sunucularını kullanılabilir tooprovide lisans olduğundan hello uzak oturum sonlandırıldı.
Neden: hello 120 gün hello Uzak Masaüstü Sunucusu rolü için lisans yetkisiz kullanım süresi dolmuştur ve tooinstall lisans gerekiyor.

Geçici bir çözüm olarak hello portalından hello RDP dosyasını yerel bir kopyasını kaydedin ve PowerShell komut istemi tooconnect bu komutu çalıştırın. Bu adım yalnızca o bağlantı için lisans devre dışı bırakır:

        mstsc <File name>.RDP /admin

İkiden fazla eşzamanlı uzak masaüstü bağlantıları toohello VM gerçekten gerek duymuyorsanız, Sunucu Yöneticisi'ni tooremove hello Uzak Masaüstü sunucu rolünü kullanabilirsiniz.

Daha fazla bilgi için bkz: hello blog gönderisi [Azure VM başarısız "Hiçbir Uzak Masaüstü lisans sunucusu ile"](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/).

<a id="rdpname"></a>

## <a name="remote-desktop-cant-find-hello-computer-name"></a>Uzak Masaüstü hello bilgisayar "name" bulunamıyor.
Neden: hello Uzak Masaüstü İstemcisi bilgisayarınızda hello RDP dosyasının hello ayarlarını hello bilgisayarın hello adı çözümlenemiyor.

Olası çözümler:

* Bir kuruluşun intranet üzerinde değilseniz, bilgisayarınızın erişim toohello proxy sunucusu vardır ve HTTPS trafiği tooit gönderebilirsiniz emin olun.
* Yerel olarak saklanan bir RDP dosyası kullanıyorsanız, hello portal tarafından oluşturulan hello birini kullanmayı deneyin. Bu adım, hello sanal makine veya hello bulut hizmeti ve hello VM hello uç nokta bağlantı noktası için doğru DNS adı hello sahip olmasını sağlar. Örnek, hello portal tarafından oluşturulan bir RDP dosyası şöyledir:
  
        full address:s:tailspin-azdatatier.cloudapp.net:55919
        prompt for credentials:i:1

Bu RDP dosyası Hello adres bölümü vardır:

* Merhaba tam etki alanı adı hello VM ("tailspin-azdatatier.cloudapp.net" Bu örnekte) içeren hello bulut hizmetinin.
* Merhaba dış TCP bağlantı noktası hello uç noktasının Uzak Masaüstü trafiği (55919).

<a id="rdpauth"></a>

## <a name="an-authentication-error-has-occurred-hello-local-security-authority-cannot-be-contacted"></a>Bir kimlik doğrulama hatası oluştu. Merhaba yerel güvenlik yetkilisi iletişim kurulamıyor.
Neden: hello hedef VM hello kullanıcı adının kısmında kimlik bilgilerinizi hello güvenlik yetkilisi bulamıyor.

Kullanıcı adınızı hello formunda olduğunda *SecurityAuthority*\\*kullanıcıadı* (örnek: CORP\User1), hello *SecurityAuthority* bölümüdür ya da hello VM's bilgisayar adı (Merhaba yerel güvenlik yetkilisi) veya bir Active Directory etki alanı adı.

Olası çözümler:

* Merhaba hesabı yerel toohello VM ise, o hello VM adının doğru yazıldığından emin olun.
* Hello hesap bir Active Directory etki alanındaysa hello hello etki alanı adının yazımını denetleyin.
* Bir Active Directory etki alanı hesabı ise ve hello etki alanı adının doğru yazıldığından, bu etki alanında etki alanı denetleyicisinin kullanılabilir olduğunu doğrulayın. Başlatılan kurmadı için bir etki alanı denetleyicisi kullanılamıyor etki alanı denetleyicileri içeren Azure sanal ağlarda yaygın bir sorundur. Geçici bir çözüm olarak, bir etki alanı hesabı yerine yerel yönetici hesabı kullanabilirsiniz.

<a id="wincred"></a>

## <a name="windows-security-error-your-credentials-did-not-work"></a>Windows güvenlik hatası: kimlik bilgilerinizi çalışmaz.
Neden: hesap adı ve parola hello hedef VM doğrulanamıyor.

Windows tabanlı bir bilgisayarda yerel bir hesap veya bir etki alanı hesabı hello kimlik doğrulayabilir.

* Yerel hesaplar için hello kullan *ComputerName*\\*kullanıcıadı* sözdizimi (örnek: SQL1\Admin4798).
* Etki alanı hesapları için hello kullanmak *DomainName*\\*kullanıcıadı* sözdizimi (örnek: CONTOSO\peterodman).

VM tooa etki alanı denetleyicinizi yeni bir Active Directory ormanında yükselttiyseniz, oturum hello yerel yönetici hesabı dönüştürülür tooan eşdeğer hesap hello ile aynı parola hello yeni orman ve etki alanı. Merhaba yerel hesap sonra silinir.

Örneğin, hello yerel hesabıyla DC1\DCAdmin oturum açmış ve hello corp.contoso.com etki alanı için yeni bir orman içindeki etki alanı denetleyicisi olarak hello sanal makine tanıtılması, DC1\DCAdmin yerel hesap silinir ve yeni bir etki alanı hesabı (CORP\DCAdmin hello ) ile Merhaba aynı oluşturulan parola.

Merhaba hesap adının hello sanal makine geçerli bir hesap doğrulayabilir ve hello parola doğru bir adı olduğundan emin olun.

Toochange hello hello yerel yönetici hesabının parolasını gerekirse bkz [nasıl tooreset bir parola veya hello Uzak Masaüstü hizmet Windows sanal makineler için](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

<a id="rdpconnect"></a>

## <a name="this-computer-cant-connect-toohello-remote-computer"></a>Bu bilgisayar toohello uzak bilgisayara bağlanamıyor.
Neden: tooconnect kullandı hello hesabı Uzak Masaüstü Oturum açma hakları yok.

Her Windows bilgisayarın, içine uzaktan oturum hello hesapları ve grupları içeren bir Uzak Masaüstü Kullanıcıları yerel grubu vardır. Bu hesapların hello Uzak Masaüstü Kullanıcıları yerel grubuna listelenmeyen olsa bile hello yerel administrators grubunun üyeleri aynı zamanda, erişimi. Etki alanına katılan makineler için hello yerel Yöneticiler grubunun da hello hello etki alanı için etki alanı yöneticileri içerir.

Tooconnect ile kullanmakta olduğunuz hello hesabı Uzak Masaüstü Oturum açma hakları olduğundan emin olun. Geçici bir çözüm olarak, bir etki alanı veya yerel yönetici hesabı tooconnect, Uzak Masaüstü'nü kullanın. tooadd istenen hesap toohello Uzak Masaüstü Kullanıcıları yerel grubu Merhaba, hello Microsoft Yönetim Konsolu ek bileşenini kullanın (**Sistem Araçları > yerel kullanıcılar ve Gruplar > Gruplar > Uzak Masaüstü Kullanıcıları**).

## <a name="next-steps"></a>Sonraki adımlar
Hiçbiri bu hatalar oluştu ve RDP kullanarak bağlanma bilinmeyen bir sorun varsa, hello bkz [Uzak Masaüstü için sorun giderme kılavuzu](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

* Bir VM üzerinde çalışan uygulamalar erişimde adımları sorun giderme için bkz: [bir Azure VM üzerinde çalışan sorun giderme erişim tooan uygulama](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Azure'da güvenli Kabuk (SSH) tooconnect tooa Linux VM kullanma sorunu yaşıyor olup [sorun giderme SSH bağlantıları tooa Azure Linux VM'de](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

