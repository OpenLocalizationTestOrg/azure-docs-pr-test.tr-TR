---
title: "Site Recovery ile VMware tooAzure çoğaltma için ağ aaaPlan | Microsoft Docs"
description: "Bu makalede Azure Site Recovery ile Azure sanal makineleri çoğaltırken ağ gerekli planlama açıklanır"
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
ms.date: 08/01/2017
ms.author: sujayt
ms.openlocfilehash: e4036351ca707bd4966cf2a855d4a162f88153e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-networking-for-azure-vm-replication"></a>3. adım: Azure VM çoğaltması için ağ planlama

Merhaba doğrulandıktan sonra [dağıtımının önkoşulları](azure-to-azure-walkthrough-prerequisites.md), çoğaltma ve Azure sanal makineleri (VM'ler) bir Azure bölgesi tooanother kurtarma durumlarda dikkat edilmesi gerekenler ağ Bu makale toounderstand hello okuma hello kullanarak Azure Site Recovery hizmeti. 

- Merhaba makale bitirdikten sonra açık olmalıdır anlama nasıl tooset giden yukarı erişim Azure VM'ler için istediğiniz tooreplicate ve nasıl tooconnect, şirket içi site toothose VM'ler.
- Bu makalenin hello altındaki tüm yorumlar gönderin ya da hello sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

>[!NOTE]
> Site Recovery ile Azure VM çoğaltma şu anda önizlemede değil.



## <a name="network-overview"></a>Ağ genel bakış

Azure ExpressRoute veya bir VPN bağlantısı kullanarak, şirket içi site tooAzure öğesinden bir bağlantı yoktur ve genellikle bir Azure sanal ağ/alt ağında Azure Vm'leriniz bulunur.

Ağlar genellikle güvenlik duvarları kullanarak korunur ve/veya ağ güvenlik grubu (Nsg'ler). Güvenlik duvarları URL tabanlı IP tabanlı listelerde, toocontrol ağ bağlantısını kullanabilirsiniz. Nsg'ler IP aralığı tabanlı kurallarını kullanın. 


Beklenen Site Recovery toowork için toomake bazı değişiklikler tooreplicate istediğiniz vm'lerden giden ağ bağlantısı gerekir. Site kurtarma kimlik doğrulaması proxy toocontrol ağ bağlantısı kullanımını desteklemez. Bir kimlik doğrulama proxy'si varsa, çoğaltma etkinleştirilemez. 


Merhaba Aşağıdaki diyagramda Azure Vm'lerinde çalışan bir uygulama için tipik bir ortamı gösterilmektedir.

![Müşteri ortamı](./media/azure-to-azure-walkthrough-network/source-environment.png)

**Azure VM ortamı**

Ayrıca Azure ExpressRoute veya bir VPN bağlantısı kullanarak şirket içi sitenizden ayarlanan bir bağlantı tooAzure sahip olabilir. 

![Müşteri ortamı](./media/azure-to-azure-walkthrough-network/source-environment-expressroute.png)

**Şirket içi bağlantı tooAzure**



## <a name="outbound-connectivity-for-urls"></a>URL'ler için giden bağlantı

Bir URL tabanlı güvenlik duvarı proxy toocontrol giden bağlantı kullanıyorsanız, Site Recovery tarafından kullanılan bu URL'leri izin emin olun

**URL** | **Ayrıntılar**  
--- | ---
*.blob.core.windows.net | Merhaba VM toohello önbellek depolama hesabı hello kaynak bölgede gelen yazılan veri toobe sağlar.
Login.microsoftonline.com | Yetkilendirme ve kimlik doğrulama tooSite kurtarma hizmeti URL'leri sağlar.
*.hypervrecoverymanager.windowsazure.com | Merhaba hello VM hizmetinden Site Recovery ile iletişim sağlar.
*. servicebus.windows.net | Böylece Hello Site Recovery izleme ve tanılama veri VM hello yazılabilir gereklidir.

## <a name="outbound-connectivity-for-ip-address-ranges"></a>IP adres aralıkları için giden bağlantı

- Otomatik olarak gerekli hello kuralları NSG hello üzerinde indirme ve çalıştırma oluşturabilirsiniz [bu komut dosyası](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).
- Bir test NSG gerekli hello NSG kuralları oluşturmak ve bir üretim NSG hello kuralları oluşturmadan önce herhangi bir sorun olduğunu doğrulayın öneririz.
- NSG kuralları toocreate gerekli hello sayısı aboneliğinizi Güvenilenler listesine olduğundan emin olun. Aboneliğinizde desteğe başvurun tooincrease hello NSG kural sınırı.
Herhangi bir IP tabanlı bir güvenlik duvarı proxy veya NSG kuralları toocontrol giden bağlantı kullanıyorsanız, hello aşağıdaki IP aralıklarını hello kaynak ve hedef konumların hello sanal makinelerin bağlı olarak toobe Güvenilenler listesine gerekir:

    - Toohello kaynak konumu karşılık gelen tüm IP adresi aralığı. İndirme hello [aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653).) Böylece veri toohello önbellek depolama hesabı VM hello yazılabilir uygulamaları güvenilir listeye almayı gereklidir.
    - TooOffice 365 karşılık gelen tüm IP aralıklarını [kimlik doğrulama ve kimlik IP V4 uç noktaları](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity). Yeni IP tooOffice 365 IP aralıkları eklediyseniz, bu toocreate yeni NSG kuralları gerekir.
-     Site Recovery Hizmeti uç noktası IP adresleri ([bir XML dosyasında kullanılabilir](https://aka.ms/site-recovery-public-ips)), hedef konumuna bağlıdır: 

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

## <a name="example-nsg-configuration"></a>Örnek NSG yapılandırma

Bir VM için çoğaltmalar çalışır böylece nasıl tooconfigure NSG kuralları, bu bölümde gösterilmiştir. NSG kuralları toocontrol giden bağlantı kullanıyorsanız, tüm gerekli hello IP aralıkları için "HTTPS Gidene izin ver" kurallarını kullanın.

Bu örnekte, "Doğu ABD" Merhaba VM kaynak konumu değil. Orta ABD Hello çoğaltma hedef konumudur.


### <a name="example"></a>Örnek

#### <a name="east-us"></a>Doğu ABD

1. Çok karşılık gelen kuralları oluşturma[Doğu ABD IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653). Bu, böylece veri toohello önbellek depolama hesabı VM hello yazılabilir gereklidir.
2. TooOffice 365 karşılık gelen tüm IP aralıkları için kurallar oluşturun [kimlik doğrulama ve kimlik IP V4 uç noktaları](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).
3. Toohello hedef konumu karşılık gelen kurallarını oluşturun:

   **Konum** | **Site Recovery hizmeti IP'leri** |  **Site Recovery IP izleme**
    --- | --- | ---
   Orta ABD | 40.69.144.231</br>40.69.167.116 | 52.165.34.144

#### <a name="central-us"></a>Orta ABD

Bu kurallar, böylece yük devretme sonrasında çoğaltma hello hedef bölge toohello Kaynak bölgesi, etkinleştirilebilmesi için gereklidir.

1. Çok karşılık gelen kuralları oluşturma[merkezi ABD IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653).
2. TooOffice 365 karşılık gelen tüm IP aralıkları için kurallar oluşturun [kimlik doğrulama ve kimlik IP V4 uç noktaları](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).
3. Toohello kaynak konumu karşılık gelen kurallarını oluşturun:

   **Konum** | **Site Recovery hizmeti IP'leri** |  **Site Recovery IP izleme**
    --- | --- | ---
   Doğu ABD | 13.82.88.226</br>40.71.38.173 | 104.45.147.24


## <a name="existing-on-premises-connection"></a>Var olan bağlantı şirket içi

Şirket içi siteniz ve azure'da hello kaynak konumu arasında bir ExpressRoute veya VPN bağlantısı varsa, aşağıdaki yönergeleri izleyin:

**Yapılandırma** | **Ayrıntılar**
--- | ---
**Zorlanan tünel** | Genellikle varsayılan yol (0.0.0.0/0) hello şirket içi konum üzerinden giden Internet trafiği tooflow zorlar. Bu önerilmemektedir. Çoğaltma trafiği ve Site Recovery iletişimleri Azure içinde kalır.<br/><br/> Bir çözüm olarak, kullanıcı tanımlı yollar (Udr'ler) add [bu IP aralıkları](#outbound-connectivity-for-azure-site-recovery-ip-ranges), böylece hello trafiği şirket içi Git değil.
**Bağlantı** | Uygulamaların tooconnect tooon içi makineler gerekir ya da şirket içi istemcileri VPN/ExpressRoute şirket içi toohello uygulama bağlama, elinizde en az bir emin [siteden siteye bağlantı](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md), arasında hello hedef Azure bölgesi ve Merhaba şirket içi site.<br/><br/> Merhaba hedef Azure bölgesi ve hello şirket içi site arasında trafiği birimleri yüksekse, başka birini oluşturmak [ExpressRoute bağlantısı](../expressroute/expressroute-introduction.md), hello hedef bölgesi ve şirket içi arasında.<br/><br/> Yük devretme sonrasında VM'ler için tooretain IP'leri istiyorsanız, hello hedef bölgenin site siteye/ExpressRoute bağlantısı bağlantısı kesik durumda tutun. Bu, hiçbir aralık çakışmalarından hello kaynak ve hedef IP adresi aralıkları arasında vardır sağlar.
**ExpressRoute** | Bir expressroute bağlantı hattı hello kaynak ve hedef bölgeler oluşturun.<br/><br/> Hello kaynak ağı hello expressroute bağlantı hattı arasındaki ve hello hedef ağ ile Merhaba hattı arasında bir bağlantı oluşturun.<br/><br/> Kaynak ve hedef bölgeler farklı IP aralıkları kullanmanızı öneririz. bir Azure hello ile aynı ağları daha hello hattı mümkün tooconnect toomore olmayacaktır IP aralıkları, hello aynı anda.<br/><br/> Aynı IP hem bölgelerde aralıkları ve ExpressRoute bağlantı hatları her iki bölgelerde oluşturun hello ile sanal ağlar oluşturabilir. Yük devretme, hello hattı hello kaynak sanal ağdan kesin ve hello hedef sanal ağ'daki hello hattına bağlayın.<br/><br/> Merhaba birincil bölge tamamen aşağı ise, hello bağlantısını kesme işlemi başarısız olabilir. Bu durumda, hello hedef sanal ağ ExpressRoute bağlantısı alamazsınız.
**ExpressRoute Premium** | Hello devreler oluşturabilirsiniz aynı coğrafi bölge.<br/><br/> toocreate devreler farklı coğrafi bölgelerde Azure ExpressRoute Premium gerekir.<br/><br/> Premium ile Merhaba artımlı maliyetidir. Zaten kullanıyorsanız, ek bir maliyet yoktur.<br/><br/> Daha fazla bilgi edinmek [konumları](../expressroute/expressroute-locations.md#azure-regions-to-expressroute-locations-within-a-geopolitical-region) ve [fiyatlandırma](https://azure.microsoft.com/pricing/details/expressroute/).



## <a name="next-steps"></a>Sonraki adımlar

Çok Git[4. adım: bir kasa oluşturun](azure-to-azure-walkthrough-vault.md)

