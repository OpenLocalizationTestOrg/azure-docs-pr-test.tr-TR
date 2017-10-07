---
title: "aaaDetailed bir Azure VM için SSH sorunlarını giderme | Microsoft Docs"
description: "Daha ayrıntılı SSH tooan Azure sanal makine bağlantı sorunları için sorun giderme adımları"
keywords: "SSH bağlantı reddedildi, ssh hatası, azure ssh, SSH bağlantısı başarısız oldu"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: b8e8be5f-e8a6-489d-9922-9df8de32e839
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: support-article
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: 3f711e53a8251f8c06dbb589a258222566a4ae1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-ssh-troubleshooting-steps-for-issues-connecting-tooa-linux-vm-in-azure"></a>Ayrıntılı SSH tooa Azure Linux VM'de bağlantı sorunları için sorun giderme adımları
Merhaba SSH istemci mümkün tooreach hello SSH hello VM hizmette olmayabilir birçok olası nedeni vardır. Hello daha izlediyseniz [sorun giderme adımları genel SSH](troubleshoot-ssh-connection.md), toofurther ihtiyacınız hello bağlantı sorunu giderme. Bu makalede, ayrıntılı sorun giderme adımları toodetermine hello SSH bağlantısı başarısız olduğunda nasıl kılavuzları ve tooresolve bunu.

## <a name="take-preliminary-steps"></a>Ön adımlar
Merhaba Aşağıdaki diyagramda oynayan hello bileşenlerini gösterir.

![SSH Hizmeti bileşenlerinin gösteren diyagram](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot1.png)

Merhaba aşağıdaki adımları hello kaynak hello hatanın yalıtmak ve çözümleri veya geçici çözümler dağıtamadığını bulmak yardımcı olur.

1. Merhaba VM hello portalında Hello durumunu denetleyin.
   Merhaba, [Azure portal](https://portal.azure.com)seçin **sanal makineleri** > *VM adı*.

   Merhaba hello VM için durum bölmesi göstermelidir **çalıştıran**. İşlem, depolama ve ağ kaynakları için son etkinliğin tooshow aşağı kaydırın.

2. Seçin **ayarları** tooexamine uç noktaları, IP adresleri, ağ güvenlik grupları ve diğer ayarlar.

   Merhaba VM içinde görüntüleyebilirsiniz SSH trafiği için tanımlanmış bir uç nokta olmalıdır **uç noktaları** veya  **[ağ güvenlik grubu](../../virtual-network/virtual-networks-nsg.md)**. Resource Manager kullanılarak oluşturulan sanal makineleri uç noktalarını bir ağ güvenlik grubundaki depolanır. Ayrıca, hello kuralları uygulanan toohello ağ güvenlik grubu kaldırıldı ve hello alt ağında başvurulan doğrulayın.

tooverify ağ bağlantısını, yapılandırılmış hello uç noktaları denetleyin ve HTTP veya başka bir hizmeti gibi başka bir protokol üzerinden hello VM ulaşmak bakın.

Bu adımlar, hello SSH bağlantıyı yeniden deneyin.

## <a name="find-hello-source-of-hello-issue"></a>Merhaba kaynak hello sorun bulunamadı
Merhaba SSH istemcisi bilgisayarınızda tooreach hello SSH hizmeti hello Azure VM tooissues veya hello alanları aşağıdaki yapılandırma hataları nedeniyle başarısız olabilir:

* [SSH istemci bilgisayar](#source-1-ssh-client-computer)
* [Kuruluş sınır cihazı](#source-2-organization-edge-device)
* [Bulut Hizmeti uç noktası ve erişim denetimi listesi (ACL)](#source-3-cloud-service-endpoint-and-acl)
* [Ağ güvenlik grupları](#source-4-network-security-groups)
* [Linux tabanlı Azure VM](#source-5-linux-based-azure-virtual-machine)

## <a name="source-1-ssh-client-computer"></a>1. kaynak: SSH istemci bilgisayar
tooeliminate bilgisayarınızı hello hatanın hello kaynağı olarak doğrulayın SSH bağlantıları tooanother şirket yapabilirsiniz Linux tabanlı bir bilgisayar.

![SSH istemci bilgisayar bileşenleri vurgular diyagramı](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot2.png)

Merhaba bağlantı başarısız olursa, sorunlar, bilgisayarınızda aşağıdaki hello denetle:

* Gelen veya giden SSH trafiği (TCP 22) engelleyen bir yerel güvenlik duvarı ayarı
* Yerel olarak SSH bağlantısını engelliyor istemci ara yazılımı yüklü
* Yerel olarak yüklü ağ SSH bağlantısını engelliyor yazılım izleme
* Trafiği izlemek ya da belirli trafik türlerine izin ver/engellemek diğer güvenlik yazılım türleri

Bu koşullardan biri geçerliyse, geçici olarak hello yazılımınızı devre dışı bırakın ve bir SSH bağlantısı tooan şirket içi bilgisayar toofind hello bağlantı bilgisayarınızda engellenen hello neden çıkışı deneyin. Ardından, ağ yöneticisi toocorrect hello yazılım ayarları tooallow SSH bağlantıları ile çalışır.

Sertifika kimlik doğrulaması kullanıyorsanız, giriş dizininizde bu izinleri toohello .ssh klasörü olduğunu doğrulayın:

* Chmod 700 ~/.ssh
* Chmod 644 ~/.ssh/\*.pub
* Chmod 600 ~/.ssh/id_rsa (ya da bunlarda depolanan özel anahtarlarınızı sahip diğer dosyalar)
* Chmod 644 ~/.ssh/known_hosts (toovia SSH bağlantı kurduğunuz konakları içerir)

## <a name="source-2-organization-edge-device"></a>2. kaynak: Kuruluş sınır cihazı
tooeliminate kuruluş sınır Cihazınızı hello hatanın hello kaynağı olarak doğrulayın toohello Internet doğrudan bağlı olduğu bir bilgisayara SSH bağlantıları tooyour Azure VM yapabilirsiniz. Siteden siteye VPN veya Azure ExpressRoute bağlantısı hello VM erişiyorsanız, çok atla[kaynak 4: ağ güvenlik grupları](#nsg).

![Kuruluş sınır cihazı vurgular diyagramı](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot3.png)

Doğrudan bağlı toohello Internet olan bir bilgisayarda yoksa, kendi kaynak grubu veya Bulut hizmetinde yeni bir Azure VM oluşturun ve bunu kullanın. Daha fazla bilgi için bkz: [Linux Azure üzerinde çalışan bir sanal makine oluşturma](quick-create-cli.md). Test ile işiniz bitince hello kaynak grubu veya VM ve bulut hizmeti silin.

Toohello Internet doğrudan bağlı olduğu bir bilgisayar ile bir SSH bağlantısı oluşturabilir, kuruluş sınır cihazınız için denetleyin:

* Merhaba Internet ile SSH trafiği engelleyen bir iç güvenlik duvarı
* SSH bağlantısını engelleyen bir proxy sunucu
* Yetkisiz erişim algılama veya ağ kenar ağınızdaki SSH bağlantısını engelliyor cihazlarda çalışan yazılım izleme

Ağ Yöneticisi toocorrect hello ayarlarınızı trafiğinizin kuruluş sınır cihazları tooallow SSH hello Internet ile birlikte çalışın.

## <a name="source-3-cloud-service-endpoint-and-acl"></a>3. kaynak: Bulut Hizmeti uç noktası ve ACL
> [!NOTE]
> Bu kaynak hello Klasik dağıtım modeli kullanılarak oluşturulan tooVMs geçerlidir. Resource Manager kullanılarak oluşturulan VM'ler için çok atla[kaynak 4: ağ güvenlik grupları](#nsg).

tooeliminate hello bulut Hizmeti uç noktası ACL hello hatanın hello kaynağı olarak doğrulayıp başka bir Azure VM ile Merhaba, aynı sanal ağ, SSH bağlantıları tooyour VM yapabilir.

![Bulut Hizmeti uç noktası ve ACL vurgular diyagramı](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot4.png)

Başka bir VM hello yoksa, aynı sanal ağı kolayca oluşturabileceğiniz bir. Daha fazla bilgi için bkz: [hello CLI kullanarak Azure'da bir Linux VM oluşturma](quick-create-cli.md). Silme, test ile bittiğinde ek VM hello.

Bir VM ile bir SSH bağlantısı oluşturup oluşturamayacağını aynı sanal hello ağ, aşağıdaki alanlarda hello denetleyin:

* **Merhaba hedef VM SSH trafiğini Hello uç nokta yapılandırması.** Merhaba özel TCP bağlantı noktası hello uç noktasının hangi hello SSH hizmeti hello VM üzerinde dinleme hello TCP bağlantı noktası eşleşmesi gerekir. (Merhaba varsayılan bağlantı noktası 22'dir). Merhaba SSH TCP bağlantı noktası numarası hello Azure portal seçerek doğrulayın **sanal makineleri** > *VM adı* > **ayarları**  >  **Uç noktaları**.
* **Merhaba hedef sanal makinedeki hello SSH trafiği uç noktası için ACL Hello.** Bir ACL izin verilen veya kaynak IP adresine göre hello Internet alanından gelen trafik reddedilen toospecify sağlar. Yanlış yapılandırılmış ACL'ler gelen SSH trafiği toohello endpoint engelleyebilir. Merhaba ortak IP adreslerinden proxy'niz veya başka bir uç sunucusu gelen trafiğe izin verilir, ACL'ler tooensure denetleyin. Daha fazla bilgi için bkz: [ağ erişimi denetim listeleri (ACL'ler)](../../virtual-network/virtual-networks-acl.md).

Merhaba sorunun kaynağı olarak tooeliminate hello endpoint hello geçerli uç nokta kaldırın, başka bir uç noktası oluşturma ve hello SSH adı (TCP bağlantı noktası 22 hello ortak ve özel bağlantı noktası numarası için) belirtin. Daha fazla bilgi için bkz: [azure'da bir sanal makine üzerindeki uç noktaları ayarlama](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

<a id="nsg"></a>

## <a name="source-4-network-security-groups"></a>4. kaynak: Ağ güvenlik grupları
Ağ güvenlik grupları toohave etkinleştirmek izin verilen gelen ve giden trafik konusunda daha ayrıntılı denetim. Alt ağlar span ve bulut hizmetlerini bir Azure sanal ağında kurallar oluşturabilirsiniz. Ağ güvenlik grubu kuralları tooensure bu SSH trafiği tooand Internet izin hello gelen denetleyin.
Daha fazla bilgi için bkz: [ağ güvenlik grupları hakkında](../../virtual-network/virtual-networks-nsg.md).

IP doğrulayın toovalidate hello NSG yapılandırması de kullanabilirsiniz. Daha fazla bilgi için bkz: [izlemeye genel bakış Azure ağ](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview). 

## <a name="source-5-linux-based-azure-virtual-machine"></a>Kaynak 5: Linux tabanlı Azure sanal makine
Merhaba son olası sorunlar hello Azure sanal makinesi kendisini kaynağıdır.

![Linux tabanlı Azure sanal makine vurgular diyagramı](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot5.png)

Henüz yapmadıysanız, hello yönergeleri [tooreset bir parola veya SSH Linux tabanlı sanal makineler için](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

Bilgisayarınızı yeniden bağlanmayı deneyin. Yine başarısız olursa hello hello olası sorunlardan bazıları şunlardır:

* Merhaba SSH hizmeti hello hedef sanal makine üzerinde çalışmıyor.
* Merhaba SSH hizmeti TCP bağlantı noktası 22 dinlemiyor. tootest, telnet istemcisi yerel bilgisayarınıza yüklemek ve çalıştırmak "telnet *cloudServiceName*. cloudapp.net 22". Merhaba sanal makine gelen ve giden iletişim toohello SSH uç nokta sağlar, bu adımı belirler.
* Merhaba hello hedef sanal makinedeki yerel güvenlik duvarı gelen veya giden SSH trafiğini engelliyor kuralları vardır.
* Yetkisiz erişim algılama veya ağ hello Azure sanal makine üzerinde çalışan yazılım izleme SSH bağlantısını engelliyor.

## <a name="additional-resources"></a>Ek kaynaklar
Uygulama erişimi sorunlarını giderme hakkında daha fazla bilgi için bkz: [bir Azure sanal makine üzerinde çalışan sorun giderme erişim tooan uygulama](troubleshoot-app-connection.md)
