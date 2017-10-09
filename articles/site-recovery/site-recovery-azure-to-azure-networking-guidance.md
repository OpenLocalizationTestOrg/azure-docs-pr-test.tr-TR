---
title: "aaaAzure Azure tooAzure sanal makineleri çoğaltmak için Site Recovery Ağ Kılavuzu | Microsoft Docs"
description: "Azure sanal makineleri çoğaltmak için kılavuz ağ oluşturma"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/13/2017
ms.author: sujayt
ms.openlocfilehash: 3a3391b8c3512932d243458fd17d2a2b39248448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="networking-guidance-for-replicating-azure-virtual-machines"></a>Azure sanal makineleri çoğaltmak için kılavuz ağ oluşturma

>[!NOTE]
> Azure sanal makineler için Site Recovery çoğaltma şu anda önizlemede değil.

Bu makale ayrıntıları hello çoğaltmak ve tek bir bölge tooanother bölgesinden Azure sanal makinelerini Kurtarma Kılavuzu Azure Site Recovery için ağ. Azure Site Recovery gereksinimleri hakkında daha fazla bilgi için bkz: Merhaba [Önkoşullar](site-recovery-prereq.md) makalesi.

## <a name="site-recovery-architecture"></a>Site Recovery mimarisi

Site Recovery basit ve kolay bir yol tooreplicate hello birincil bölge kesilme varsa bunlar kurtarılabilir böylece Azure bölgesi Azure sanal makineleri tooanother üzerinde çalışan uygulamalar sağlar. Daha fazla bilgi edinmek [bu senaryo ve Site Recovery mimarisi](site-recovery-azure-to-azure-architecture.md).

## <a name="your-network-infrastructure"></a>Ağ altyapınızın

Merhaba Aşağıdaki diyagramda hello tipik Azure ortamı, Azure sanal makinelerde çalışan bir uygulama için gösterilmektedir:

![Müşteri ortamı](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

Azure ExpressRoute veya bir VPN bağlantısını bir şirket içi ağ tooAzure kullanıyorsanız, hello ortamı şöyle görünür:

![Müşteri ortamı](./media/site-recovery-azure-to-azure-architecture/source-environment-expressroute.png)

Genellikle, müşteriler güvenlik duvarları ve/veya ağ güvenlik grupları (Nsg'ler) kullanarak kendi ağları koruyun. Merhaba güvenlik duvarları, ağ bağlantısını denetlemek için URL tabanlı ya da IP tabanlı uygulamaları güvenilir listeye almayı kullanabilirsiniz. Nsg'ler, IP aralıkları toocontrol ağ bağlantısını kullanarak için kuralları izin verir.

>[!IMPORTANT]
> Doğrulanmış bir proxy toocontrol ağ bağlantısı kullanıyorsanız, ancak desteklenmez ve Site Recovery çoğaltma etkinleştirilemez. 

Merhaba aşağıdaki bölümlerde Site Recovery çoğaltma toowork için Azure sanal makinelerden gerekli hello ağ giden bağlantı değişiklikleri açıklanmaktadır.

## <a name="outbound-connectivity-for-azure-site-recovery-urls"></a>Azure Site kurtarma URL'ler için giden bağlantı

Tüm URL tabanlı güvenlik duvarı proxy toocontrol giden bağlantı kullanıyorsanız, emin toowhitelist olması bunlar Azure Site Recovery hizmeti URL'lerine gereklidir:


**URL** | **Amacı**  
--- | ---
*.blob.core.windows.net | Böylece VM hello veri toohello önbellek depolama hesabı hello kaynak bölgede yazılabilir gereklidir.
Login.microsoftonline.com | Yetkilendirme ve kimlik doğrulama toohello Site Recovery hizmeti URL'lerine için gereklidir.
*.hypervrecoverymanager.windowsazure.com | Merhaba Site Recovery hizmeti iletişimi VM hello gerçekleştirilmesi gerekir.
*. servicebus.windows.net | Böylece Hello Site Recovery izleme ve tanılama veri VM hello yazılabilir gereklidir.

## <a name="outbound-connectivity-for-azure-site-recovery-ip-ranges"></a>Azure Site kurtarma IP aralıkları için giden bağlantı

>[!NOTE]
> tooautomatically hello ağ güvenlik grubu gerekli hello NSG kuralları oluşturma, şunları yapabilirsiniz [indirin ve bu komut dosyası](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).

>[!IMPORTANT]
> * Gerekli hello NSG kuralları bir test ağ güvenlik grubu oluşturun ve bir üretim ağ güvenlik grubu hello kuralları oluşturmadan önce herhangi bir sorun olduğunu doğrulayın öneririz.
> * NSG kuralları toocreate gerekli hello sayısı aboneliğinizi Güvenilenler listesine olduğundan emin olun. Aboneliğinizde desteğe başvurun tooincrease hello NSG kural sınırı.

Herhangi bir IP tabanlı bir güvenlik duvarı proxy veya NSG kuralları toocontrol giden bağlantı kullanıyorsanız, hello aşağıdaki IP aralıklarını hello kaynak ve hedef konumların hello sanal makinelerin bağlı olarak toobe Güvenilenler listesine gerekir:

- Toohello kaynak konumu karşılık gelen tüm IP aralıkları. (Merhaba indirebilirsiniz [IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653).) Böylece veri toohello önbellek depolama hesabı VM hello yazılabilir uygulamaları güvenilir listeye almayı gereklidir.

- TooOffice 365 karşılık gelen tüm IP aralıklarını [kimlik doğrulama ve kimlik IP V4 uç noktaları](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

    >[!NOTE]
    > Yeni IP tooOffice 365 IP aralıkları hello gelecekteki eklenir, toocreate yeni NSG kuralları gerekir.
    
- Kurtarma Hizmeti uç noktası IP'leri site ([bir XML dosyasında kullanılabilir](https://aka.ms/site-recovery-public-ips)), hedef konumuna bağlıdır: 

   **Hedef konumu** | **Site Recovery hizmeti IP'leri** |  **Site Recovery IP izleme**
   --- | --- | ---
   Doğu Asya | 52.175.17.132</br>40.83.121.61 | 13.94.47.61
   Güneydoğu Asya | 52.187.58.193</br>52.187.169.104 | 13.76.179.223
   Orta Hindistan | 52.172.187.37</br>52.172.157.193 | 104.211.98.185
   Güney Hindistan | 52.172.46.220</br>52.172.13.124 | 104.211.224.190
   Orta Kuzey ABD | 23.96.195.247</br>23.96.217.22 | 168.62.249.226
   Kuzey Avrupa | 40.69.212.238</br>13.74.36.46 | 52.169.18.8
   Batı Avrupa | 52.166.13.64</br>52.166.6.245 | 40.68.93.145
   Doğu ABD | 13.82.88.226</br>40.71.38.173 | 104.45.147.24
   Batı ABD | 40.83.179.48</br>13.91.45.163 | 104.40.26.199
   Orta Güney ABD | 13.84.148.14</br>13.84.172.239 | 104.210.146.250
   Orta ABD | 40.69.144.231</br>40.69.167.116 | 52.165.34.144
   Doğu ABD 2 | 52.184.158.163</br>52.225.216.31 | 40.79.44.59
   Japonya Doğu | 52.185.150.140</br>13.78.87.185 | 138.91.1.105
   Japonya Batı | 52.175.146.69</br>52.175.145.200 | 138.91.17.38
   Güney Brezilya | 191.234.185.172</br>104.41.62.15 | 23.97.97.36
   Avustralya Doğu | 104.210.113.114</br>40.126.226.199 | 191.239.64.144
   Avustralya Güneydoğu | 13.70.159.158</br>13.73.114.68 | 191.239.160.45
   Orta Kanada | 52.228.36.192</br>52.228.39.52 | 40.85.226.62
   Doğu Kanada | 52.229.125.98</br>52.229.126.170 | 40.86.225.142
   Batı Orta ABD | 52.161.20.168</br>13.78.230.131 | 13.78.149.209
   Batı ABD 2 | 52.183.45.166</br>52.175.207.234 | 13.66.228.204
   Birleşik Krallık Batı | 51.141.3.203</br>51.140.226.176 | 51.141.14.113
   Birleşik Krallık Güney | 51.140.43.158</br>51.140.29.146 | 51.140.189.52

## <a name="sample-nsg-configuration"></a>Örnek NSG yapılandırma
Site Recovery çoğaltma sanal bir makinede çalışabilmeniz için bu bölümde hello adımları tooconfigure NSG kuralları açıklanır. NSG kuralları toocontrol giden bağlantı kullanıyorsanız, tüm gerekli hello IP aralıkları için "HTTPS Gidene izin ver" kuralları kullanın.

>[!Note]
> tooautomatically hello ağ güvenlik grubu gerekli hello NSG kuralları oluşturma, şunları yapabilirsiniz [indirin ve bu komut dosyası](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).

Örneğin, VM kaynak konumu "Doğu ABD" ve çoğaltma hedef konumu "Orta ABD" ise, hello sonraki iki bölümde hello adımları izleyin.

>[!IMPORTANT]
> * Gerekli hello NSG kuralları bir test ağ güvenlik grubu oluşturun ve bir üretim ağ güvenlik grubu hello kuralları oluşturmadan önce herhangi bir sorun olduğunu doğrulayın öneririz.
> * NSG kuralları toocreate gerekli hello sayısı aboneliğinizi Güvenilenler listesine olduğundan emin olun. Aboneliğinizde desteğe başvurun tooincrease hello NSG kural sınırı. 

### <a name="nsg-rules-on-hello-east-us-network-security-group"></a>NSG kuralları hello Doğu ABD ağ güvenlik grubu

* Çok karşılık gelen kuralları oluşturma[Doğu ABD IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653). Bu, böylece veri toohello önbellek depolama hesabı VM hello yazılabilir gereklidir.

* TooOffice 365 karşılık gelen tüm IP aralıkları için kurallar oluşturun [kimlik doğrulama ve kimlik IP V4 uç noktaları](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

* Toohello hedef konumu karşılık gelen kurallarını oluşturun:

   **Konum** | **Site Recovery hizmeti IP'leri** |  **Site Recovery IP izleme**
    --- | --- | ---
   Orta ABD | 40.69.144.231</br>40.69.167.116 | 52.165.34.144

### <a name="nsg-rules-on-hello-central-us-network-security-group"></a>NSG kuralları hello Orta ABD ağ güvenlik grubu

Bu kurallar, böylece hello hedef bölge toohello Kaynak bölgesi yük devretme sonrasında çoğaltma etkinleştirilebilir gereklidir:

* Çok karşılık gelen kuralları[merkezi ABD IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653). Veri toohello önbellek depolama hesabı VM hello yazılabilir şekilde bu gereklidir.

* Kuralları tooOffice 365 karşılık gelen tüm IP aralıkları için [kimlik doğrulama ve kimlik IP V4 uç noktaları](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

* Toohello kaynak konumu karşılık gelen kuralları:

   **Konum** | **Site Recovery hizmeti IP'leri** |  **Site Recovery IP izleme**
    --- | --- | ---
   Doğu ABD | 13.82.88.226</br>40.71.38.173 | 104.45.147.24


## <a name="guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration"></a>Var olan Azure--şirket içi için ExpressRoute/VPN yapılandırma yönergeleri

Şirket içi ve hello arasında bir ExpressRoute veya VPN bağlantısı varsa kaynak Azure konumda, bu bölümdeki hello yönergeleri izleyin.

### <a name="forced-tunneling-configuration"></a>Zorlamalı tünel yapılandırma

Bir ortak müşteri toodefine hello şirket içi konum üzerinden giden Internet trafiği tooflow zorlar varsayılan yol (0.0.0.0/0) yapılandırmadır. Bunu önermiyoruz. Merhaba çoğaltma trafiği ve Site Recovery hizmeti iletişimi hello Azure sınır bırakmamalısınız. Merhaba tooadd kullanıcı tanımlı yollar (Udr'ler) için bir çözümdür [bu IP aralıkları](#outbound-connectivity-for-azure-site-recovery-ip-ranges) böylece hello çoğaltma trafiği şirket içi Git değil.

### <a name="connectivity-between-hello-target-and-on-premises-location"></a>Merhaba hedef ve şirket içi konum arasında bağlantı

Hello hedef konumu ve hello içi konumunuz bağlantılar için bu yönergeleri izleyin:
- Uygulamanızı tooconnect toohello şirket içi makineler gerekirse ya da toohello uygulama şirket içi VPN/ExpressRoute bağlanan istemciler varsa, en az bir sağlamak [siteden siteye bağlantı](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) Hedef Azure bölgesi hello şirket içi ve veri merkeziniz arasında.

- Hedef Azure bölgesi ve hello şirket içi veri merkezi arasında trafiği tooflow çok bekliyorsanız, başka bir oluşturmalısınız [ExpressRoute bağlantısı](../expressroute/expressroute-introduction.md) hello hedef Azure bölgesi ve hello şirket içi veri merkezi arasında.

- Yük devretme yaptıktan sonra hello sanal makineler için tooretain IP'leri istiyorsanız, hello hedef bölgenin site siteye/ExpressRoute bağlantısı bağlantısı kesik durumda tutun. Bu toomake hiçbir aralık çakışmasından hello kaynak bölgesinin IP aralıklarını ve hedef bölgenin IP aralıkları arasında olduğundan emin olur.

### <a name="best-practices-for-expressroute-configuration"></a>ExpressRoute yapılandırması için en iyi yöntemler
ExpressRoute yapılandırması için bu en iyi uygulamaları izleyin:

- Bir expressroute bağlantı hattı her iki hello kaynak ve hedef bölgelerde toocreate gerekir. Ardından toocreate arasında bir bağlantı gerekir:
  - Merhaba kaynak sanal ağ ve hello expressroute bağlantı hattı.
  - Merhaba hedef sanal ağ ve hello expressroute bağlantı hattı.

- ExpressRoute standart bir parçası olarak hello devreler oluşturabilirsiniz aynı coğrafi bölge. toocreate ExpressRoute bağlantı hatları farklı coğrafi bölgelerde Azure ExpressRoute Premium gereklidir, artımlı bir maliyet içerir. (ExpressRoute Premium zaten kullanıyorsanız, var. ek bir maliyeti yoktur.) Daha fazla ayrıntı için bkz: Merhaba [ExpressRoute konumları belge](../expressroute/expressroute-locations.md#azure-regions-to-expressroute-locations-within-a-geopolitical-region) ve [ExpressRoute fiyatlandırma](https://azure.microsoft.com/pricing/details/expressroute/).

- Kaynak ve hedef bölgeler farklı IP aralıkları kullanmanızı öneririz. Merhaba expressroute bağlantı hattı edemez tooconnect Merhaba, iki Azure sanal ağ ile aynı IP aralıkları Merhaba aynı anda.

- Aynı IP hem bölgelerde aralıkları ve ExpressRoute bağlantı hatları her iki bölgelerde oluşturursunuz hello ile sanal ağlar oluşturabilir. Hello durumda bir yük devretme olayının hello hattı hello kaynak sanal ağdan kesin ve hello hedef sanal ağ'daki hello hattına bağlayın.

 >[!IMPORTANT]
 > Merhaba birincil bölge tamamen aşağı ise, hello bağlantısını kesme işlemi başarısız olabilir. ExpressRoute bağlantı alma, hello hedef sanal ağ engeller.

## <a name="next-steps"></a>Sonraki adımlar
İş yükleri tarafından korumaya başlamak [Azure sanal makineleri çoğaltmak](site-recovery-azure-to-azure.md).
