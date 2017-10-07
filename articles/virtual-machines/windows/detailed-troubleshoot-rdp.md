---
title: "Azure'da sorun giderme aaaDetailed Uzak Masaüstü | Microsoft Docs"
description: "Burada tooa Windows Azure sanal makinelerde yapamazsınız Uzak Masaüstü hataları için ayrıntılı sorun giderme adımlarını gözden geçirin"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
keywords: "gönderilemiyor tooremote Masaüstü Bağlantısı, Uzak Masaüstü, sorun giderme Uzak Masaüstü bağlantı kuramıyor, Uzak Masaüstü hataları, Uzak Masaüstü sorunlarını giderme, Uzak Masaüstü sorunları"
ms.assetid: 9da36f3d-30dd-44af-824b-8ce5ef07e5e0
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: fcb0d06aa66b748f3ebbbbe3431471d3cbe7c60d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-troubleshooting-steps-for-remote-desktop-connection-issues-toowindows-vms-in-azure"></a>Uzak Masaüstü bağlantısı için ayrıntılı sorun giderme adımları sorunları tooWindows azure'da VM
Bu makale, Windows tabanlı Azure sanal makineler için toodiagnose ve düzeltme karmaşık Uzak Masaüstü hatalarını ayrıntılı sorun giderme adımları sağlar.

> [!IMPORTANT]
> tooeliminate hello daha yaygın Uzak Masaüstü hataları, yapma emin tooread [hello temel sorun giderme makalesi, Uzak Masaüstü için](troubleshoot-rdp-connection.md) devam etmeden önce.

Uzak Masaüstü hello belirli hata iletilerinden birini benzemez hata iletisi ele karşılaşabileceğiniz [sorun giderme kılavuzu temel Uzak Masaüstü hello](troubleshoot-rdp-connection.md). Bu adımları toodetermine neden hello Uzak Masaüstü (RDP) istemci oluşturulamıyor tooconnect toohello RDP hello Azure VM üzerinde hizmetidir izleyin.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz üzerinde Azure uzmanlar hello [MSDN Azure hello ve yığın taşması forumları hello](https://azure.microsoft.com/support/forums/). Alternatif olarak, Azure destek olay dosya. Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/support/options/) tıklatıp **destek alın**. Hello Azure destek kullanma hakkında daha fazla bilgi için okuma [Microsoft Azure desteği ile ilgili SSS](https://azure.microsoft.com/support/faq/).

## <a name="components-of-a-remote-desktop-connection"></a>Uzak Masaüstü bağlantısının bileşenleri
Aşağıdaki bileşenler hello bir RDP bağlantısının oynayan:

![](./media/detailed-troubleshoot-rdp/tshootrdp_0.png)

Devam etmeden önce nelerin hello son başarılı Uzak Masaüstü Bağlantısı toohello itibaren VM değiştiğini gözden toomentally yardımcı olabilir. Örneğin:

* Merhaba hello VM içeren hello VM veya hello bulut hizmetinin genel IP adresi (Merhaba sanal IP adresi olarak da bilinir [VIP](https://en.wikipedia.org/wiki/Virtual_IP_address)) değişti. DNS istemci önbelleği hala hello olduğundan Hello RDP hatası olabilir *eski IP adresi* hello DNS adı için kayıtlı. DNS istemci önbelleğini temizlemek ve hello VM yeniden bağlanmayı deneyin. Veya doğrudan hello yeni VIP ile bağlanmayı deneyin.
* Bir üçüncü taraf uygulama toomanage hello Azure portal tarafından oluşturulan hello bağlantısı kullanmak yerine, Uzak Masaüstü bağlantıları kullanıyor. Merhaba doğru TCP bağlantı noktası hello Uzak Masaüstü trafiği için bu hello uygulama yapılandırması içerir doğrulayın. Bu bağlantı noktası hello klasik bir sanal makine için kontrol edebilirsiniz [Azure portal](https://portal.azure.com), hello VM'in ayarları tıklayarak > uç noktaları.

## <a name="preliminary-steps"></a>Başlangıç adımları
Devam etmeden önce toohello ayrıntılı sorun giderme,

* Merhaba hello belirgin sorunları için Azure portalı hello sanal makinenin durumunu denetleyin.
* Merhaba izleyin [hızlı düzeltme adımları hello temel sorun gidermeyi ortak RDP hataları için kılavuzluk](troubleshoot-rdp-connection.md#quick-troubleshooting-steps).

Uzak Masaüstü VM toohello adımları sonra yeniden bağlanmayı deneyin.

## <a name="detailed-troubleshooting-steps"></a>Ayrıntılı sorun giderme adımları
Merhaba uzak masaüstü istemcisini kullanabilirsiniz tooreach hello Uzak Masaüstü hizmetini hello Azure VM olmayabilir aşağıdaki kaynaklar hello en son tooissues:

* [Uzak Masaüstü istemcisi bilgisayar](#source-1-remote-desktop-client-computer)
* [Kuruluş intranet sınır cihazı](#source-2-organization-intranet-edge-device)
* [Bulut Hizmeti uç noktası ve erişim denetimi listesi (ACL)](#source-3-cloud-service-endpoint-and-acl)
* [Ağ güvenlik grupları](#source-4-network-security-groups)
* [Windows tabanlı Azure VM](#source-5-windows-based-azure-vm)

## <a name="source-1-remote-desktop-client-computer"></a>Kaynak 1: Uzak Masaüstü istemcisi bilgisayar
Bilgisayarınızı Uzak Masaüstü yapabilirsiniz doğrulayın içi tooanother bağlantıları, Windows tabanlı bir bilgisayar.

![](./media/detailed-troubleshoot-rdp/tshootrdp_1.png)

Şunları yapamazsınız ayarları bilgisayarınızda aşağıdaki hello için kontrol edin:

* Uzak Masaüstü trafiği engelleyen bir yerel güvenlik duvarı ayarı.
* Yerel olarak Uzak Masaüstü bağlantıları engelliyor istemci ara yazılımı yüklü.
* Yerel ağ Uzak Masaüstü bağlantıları engelliyor yazılım izleme yüklü.
* Trafiği izlemek ya da belirli Uzak Masaüstü bağlantıları engelliyor trafik türlerine izin ver/engellemek diğer güvenlik yazılım türleri.

Tüm bu durumlarda, geçici olarak hello yazılımını devre dışı bırakma ve Uzak Masaüstü üzerinden tooconnect tooan şirket içi bilgisayara deneyin. Bu şekilde hello gerçek nedenini bulabilirsiniz, ağ yöneticisi toocorrect hello yazılım ayarları tooallow Uzak Masaüstü bağlantıları ile çalışır.

## <a name="source-2-organization-intranet-edge-device"></a>2. kaynak: Kuruluş intranet sınır cihazı
Bir bilgisayarın Uzak Masaüstü bağlantıları tooyour Azure sanal makinesi Internet yapabilirsiniz toohello doğrudan bağlı emin olun.

![](./media/detailed-troubleshoot-rdp/tshootrdp_2.png)

Doğrudan bağlı bir bilgisayarda yoksa toohello Internet oluşturun ve yeni bir Azure sanal makine bir kaynak grubu veya Bulut hizmetinde sınayın. Daha fazla bilgi için bkz: [Windows Azure üzerinde çalışan bir sanal makine oluşturma](../virtual-machines-windows-hero-tutorial.md). Merhaba test ettikten sonra hello sanal makine ve hello kaynak grubu ya da hello bulut hizmeti silebilirsiniz.

Doğrudan bağlı bilgisayar toohello Internet ile bir Uzak Masaüstü bağlantısı oluşturabilirsiniz kuruluş intranet kenar cihazınız için kontrol edin:

* HTTPS bağlantıları toohello Internet engelleyen bir iç güvenlik duvarı.
* Uzak Masaüstü bağlantıları engelleyen bir proxy sunucu.
* Yetkisiz erişim algılama veya ağ kenar ağınızdaki Uzak Masaüstü bağlantıları engelliyor cihazlarda çalışan yazılım izleme.

Ağ Yöneticisi toocorrect hello ayarlarının, kuruluş intranet kenar aygıt tooallow HTTPS tabanlı Uzak Masaüstü bağlantıları toohello Internet ile çalışır.

## <a name="source-3-cloud-service-endpoint-and-acl"></a>3. kaynak: Bulut Hizmeti uç noktası ve ACL
Oluşturulan VM'ler hello Klasik dağıtım modeli kullanılarak başka bir Azure VM, olduğunu doğrulamak için hello aynı bulut hizmeti veya Uzak Masaüstü bağlantıları tooyour Azure VM sanal ağ yapabilirsiniz.

![](./media/detailed-troubleshoot-rdp/tshootrdp_3.png)

> [!NOTE]
> Kaynak Yöneticisi'nde oluşturulan sanal makineler için çok atla[kaynak 4: ağ güvenlik grupları](#source-4-network-security-groups).

Başka bir sanal aynı bulut hizmeti ya da sanal ağ Merhaba, bir tane oluşturun makine yoksa. Merhaba adımları [Windows Azure üzerinde çalışan bir sanal makine oluşturma](../virtual-machines-windows-hero-tutorial.md). Merhaba test tamamlandıktan sonra hello test sanal makinesi silin.

Merhaba tooa sanal makinede Uzak Masaüstü aracılığıyla bağlanabiliyorsa aynı hizmet veya sanal ağ, bulut için bu ayarları kontrol edin:

* Uzak Masaüstü trafiğini hello hedef VM Hello uç nokta yapılandırması: hello özel TCP bağlantı noktası hello uç noktasının hangi hello üzerinde VM'ın Uzak Masaüstü hizmetini dinliyor hello TCP bağlantı noktası eşleşmesi gerekir (varsayılan olarak 3389).
* VM hello hedefte hello Uzak Masaüstü trafiği uç noktası için ACL Hello: ACL'leri izin verilen veya Internet tabanlı kaynak IP adresine hello öğesinden gelen trafiği reddedilen toospecify tanır. Yanlış yapılandırılmış ACL'ler gelen Uzak Masaüstü trafiği toohello endpoint engelleyebilir. Proxy ya da diğer uç sunucu, ortak IP adreslerinden gelen trafiğe izin verilir, ACL'ler tooensure denetleyin. Daha fazla bilgi için bkz: [bir ağ erişim denetimi listesi (ACL) nedir?](../../virtual-network/virtual-networks-acl.md)

toocheck hello endpoint hello kaynağı hello sorununun ise hello geçerli uç nokta kaldırın ve hello aralığı 49152 – 65535 hello harici bağlantı noktası numarası için de bir rastgele bağlantı noktası seçerek yeni bir tane oluşturun. Daha fazla bilgi için bkz: [nasıl tooset uç noktaları tooa sanal makineyi](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="source-4-network-security-groups"></a>4. kaynak: Ağ güvenlik grupları
Ağ güvenlik grupları, izin verilen gelen ve giden trafik daha ayrıntılı denetim sağlar. Alt ağlar kapsayıcı kurallar oluşturabilir ve bir Azure sanal ağı Hizmetleri'nde bulut.

Kullanım [IP akış doğrulayın](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) trafiği tooor bir sanal makineden bir ağ güvenlik grubu kural engelliyorsa tooconfirm. Ayrıca, etkin güvenlik grubu kuralları tooensure gelen "NSG izin ver" kuralı var ve RDP bağlantı noktası (varsayılan 3389) öncelik gözden geçirebilirsiniz. Daha fazla bilgi için bkz: [kullanarak etkili güvenlik kuralları tootroubleshoot VM trafiğinin akmasını](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).

## <a name="source-5-windows-based-azure-vm"></a>Kaynak 5: Windows tabanlı Azure VM
![](./media/detailed-troubleshoot-rdp/tshootrdp_5.png)

Merhaba yönergeleri izleyin [bu makalede](reset-rdp.md). Bu makalede hello Uzak Masaüstü hizmetini hello sanal makineye sıfırlar:

* Merhaba "Uzak Masaüstü" Windows Güvenlik Duvarı varsayılan kuralı (TCP bağlantı noktası 3389) etkinleştirin.
* Uzak Masaüstü bağlantıları hello HKLM\System\CurrentControlSet\Control\Terminal Server\fDenyTSConnections kayıt defteri değeri too0 ayarlayarak etkinleştirin.

Merhaba bağlantıyı bilgisayarınızdan yeniden deneyin. Uzak Masaüstü hala erişilemiyor tooconnect varsa, aşağıdaki olası sorunları Merhaba denetleyin:

* Merhaba Uzak Masaüstü hizmetini hello hedef VM üzerinde çalışmıyor.
* Uzak Masaüstü hizmetini Hello TCP bağlantı noktası 3389 dinlemiyor.
* Windows Güvenlik Duvarı veya başka bir yerel güvenlik duvarı Uzak Masaüstü trafiği engelleyen bir giden kuralı vardır.
* Yetkisiz erişim algılama veya ağ hello Azure sanal makine üzerinde çalışan yazılımı izleme Uzak Masaüstü bağlantıları engelliyor.

Merhaba Klasik dağıtım modeli kullanılarak oluşturulan VM'ler için uzak bir Azure PowerShell oturumu toohello Azure sanal makinesini kullanabilirsiniz. İlk olarak, hello sanal makinenin barındırma bulut hizmeti için tooinstall bir sertifika gerekir. Çok Git[güvenli uzaktan PowerShell erişimi Yapılandır tooAzure sanal makineleri](http://gallery.technet.microsoft.com/scriptcenter/Configures-Secure-Remote-b137f2fe) ve hello indirme **InstallWinRMCertAzureVM.ps1** komut dosyası tooyour yerel bilgisayar.

Ardından, henüz yapmadıysanız Azure PowerShell'i yükleyin. Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

Ardından, bir Azure PowerShell komut istemi açın ve hello geçerli klasör toohello konumunu hello değiştirmek **InstallWinRMCertAzureVM.ps1** komut dosyası. bir Azure PowerShell Betiği toorun hello doğru yürütme ilkesini ayarlamanız gerekir. Merhaba çalıştırmak **Get-ExecutionPolicy** toodetermine geçerli ilke düzeyinizi komutu. Merhaba uygun düzeyini ayarlama hakkında daha fazla bilgi için bkz: [Set-ExecutionPolicy](https://technet.microsoft.com/library/hh849812.aspx).

Ardından, Azure aboneliği adınızı, hello bulut hizmeti adı ve (merhaba < ve > karakterleri kaldırma), sanal makine adı doldurun ve ardından aşağıdaki komutları çalıştırın.

```powershell
$subscr="<Name of your Azure subscription>"
$serviceName="<Name of hello cloud service that contains hello target virtual machine>"
$vmName="<Name of hello target virtual machine>"
.\InstallWinRMCertAzureVM.ps1 -SubscriptionName $subscr -ServiceName $serviceName -Name $vmName
```

Hello hello doğru abonelik adı alabilirsiniz *varlığıyla SubscriptionName* hello hello görüntüsünü özelliğinin **Get-AzureSubscription** komutu. Merhaba bulut hizmeti adı hello sanal makine için hello alabilirsiniz *ServiceName* hello hello görüntüsünü sütununda **Get-AzureVM** komutu.

Merhaba yeni bir sertifika olup olmadığını denetleyin. Merhaba geçerli kullanıcı ile bir sertifika ek bileşenini açın ve hello arayın **güvenilen kök sertifika Authorities\Certificates** klasör. Bulut hizmetinizi hello verilen toocolumn hello DNS adına sahip bir sertifika görmeniz gerekir (örnek: cloudservice4testing.cloudapp.net).

Ardından, bu komutları kullanarak uzak bir Azure PowerShell oturumu başlatın.

```powershell
$uri = Get-AzureWinRMUri -ServiceName $serviceName -Name $vmName
$creds = Get-Credential
Enter-PSSession -ConnectionUri $uri -Credential $creds
```

Geçerli yönetici kimlik bilgileri girdikten sonra Azure PowerShell komut isteminde aşağıdaki benzeri toohello görmeniz gerekir:

```powershell
[cloudservice4testing.cloudapp.net]: PS C:\Users\User1\Documents>
```

Merhaba ilk bu istemi hello hedef VM, "cloudservice4testing.cloudapp.net" farklı olabilir içeren bulut hizmeti adınızı parçasıdır. Şimdi, belirtilen hizmet tooinvestigate hello sorunlarına bu bulut için Azure PowerShell komutlarını verin ve hello yapılandırmasını düzeltin.

### <a name="toomanually-correct-hello-remote-desktop-services-listening-tcp-port"></a>toomanually doğru hello Uzak Masaüstü Hizmetleri dinleme TCP bağlantı noktası
Merhaba uzaktan Azure PowerShell oturumu isteminde bu komutu çalıştırın.

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

Merhaba PortNumber özelliği hello geçerli bağlantı noktası numarasını gösterir. Gerekirse, hello Uzak Masaüstü bağlantı noktası numarası geri tooits varsayılan değeri (3389'dur) Bu komutu kullanarak değiştirin.

```powershell
Set-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber" -Value 3389
```

Bu komutu kullanarak Hello bağlantı noktası değiştirilen too3389 etkinleştirilmiş olduğunu doğrulayın.

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

Merhaba uzaktan Azure PowerShell oturumunda bu komutu kullanarak çıkın.

```powershell
Exit-PSSession
```

Bu hello Uzak Masaüstü uç noktası hello Azure VM için de kendi iç bağlantı noktası olarak TCP bağlantı noktası 3398 kullanıyor doğrulayın. Hello Azure VM yeniden başlatın ve hello Uzak Masaüstü bağlantısı yeniden deneyin.

## <a name="additional-resources"></a>Ek kaynaklar
[Nasıl tooreset bir parola veya hello Uzak Masaüstü hizmet için Windows sanal makineler](reset-rdp.md)

[Nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview)

[Güvenli Kabuk (SSH) bağlantı tooa Linux tabanlı Azure sanal makine sorunlarını giderme](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Bir Azure sanal makine üzerinde çalışan erişim tooan uygulama sorunlarını giderme](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

