---
title: "Azure Site Recovery ile Hyper-V (withSystem Center VMM) tooAzure çoğaltma için ağ aaaPlan | Microsoft Docs"
description: "Bu makalede, Hyper-V Vm'lerini (VMM ile) tooAzure çoğaltırken gerekli ağ planlaması anlatılmaktadır."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 41c3c83e-6b1a-496a-8179-498c552ef0c7
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 51ca8b939b6f96880f83599ea8009eb0bfa5b957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-hyper-v-with-vmm-tooazure-replication"></a>4. adım: ağ bağlantısı Hyper-V (VMM ile) tooAzure çoğaltma için planlama

Gerçekleştirdikten sonra [kapasite planlaması](vmm-to-azure-walkthrough-capacity.md) (tam dağıtımını yaptığınız varsa), bu makale toolearn ağ çoğaltmaya Hyper-V sanal makinelerini System Center Virtual Machine Manager (VMM) şirket içi zaman planlama konuları hakkında okuyun Hello kullanarak bulut tooAzure [Azure Site Recovery](site-recovery-overview.md) hizmet.

Bu makalenin hello altındaki tüm yorumlar gönderin ya da hello sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="network-mapping-for-replication-tooazure"></a>Ağ eşlemesi çoğaltma tooAzure için

Ağ eşlemesi, Hyper-V Vm'lerini (VMM yönetilen) tooAzure çoğaltırken kullanılır. Bir kaynak VMM sunucusunda VM ağları arasındaki eşlemeyi eşlemeleri ağ ve hedef Azure ağları. Eşleme aşağıdaki hello:

- **Ağ bağlantısı**— yük devretme sonrasında, tüm çoğaltılan Azure Vm'lerinin bağlı toohello eşlenen Azure ağına şunlardır. Merhaba üzerinde aynı yük devri tüm makineler bunlar farklı kurtarma planları devredilir olsa bile ağ tooeach diğer bağlanabilir.
- **Ağ geçidi**— bir ağ geçidi hello hedef Azure ağında ayarlanıp ayarlanmadığını VM'ler tooother şirket içi sanal makineleri üzerinde premised eşlenen hello içinde ağına bağlanabilir.

### <a name="prepare-vmm-for-network-mapping"></a>VMM ağ eşlemesi için hazırlanma

VMM, ağ eşlemesi için aşağıdaki gibi hazırlayın:

1. Yoksa, hazırlama bir [VMM mantıksal ağı](https://docs.microsoft.com/system-center/vmm/network-logical) hello Hyper-V konakları konumlandırıldığını hello bulutla ilişkili.
2. Yoksa, oluşturulan bir [VM ağı](https://docs.microsoft.com/system-center/vmm/network-virtual) bağlantılı toohello mantıksal ağ üzerinde hazırlanmış.
3. Merhaba Hyper-V ana bilgisayar sunucu/kümesinde hello VMM bulut, toohello VM ağı üzerinde sanal makineleri bağlayın.

 
Şunlara dikkat edin: 
- Toohello kaynak VM ağına bağlı yeni VM'ler eklendiğinde Çoğaltma gerçekleştiğinde eşlenen Azure ağ toohello.
- Merhaba hedef ağ birden çok alt ağı varsa ve bu alt ağlardan biri olan hello adıyla aynı alt ağda hangi hello kaynak sanal makinenin bulunduğu sonra hello çoğaltma sanal makinesi yük devretme sonrasında toothat hedef alt bağlanır.
- Eşleşen ada sahip bir hedef alt ağ varsa, hello sanal makine toohello hello ağdaki ilk alt ağa bağlanır.
- Bir Azure ağı hazırlamak ve hello senaryo dağıtırken, ağ eşlemelerini ayarlamak.

## <a name="connecting-tooazure-vms-after-failover"></a>Yük devretme sonrasında tooAzure VM'ler bağlanma

Çoğaltma ve yük devretme stratejinizi planlarken hello önemli sorular biri nasıl yük devretme sonrasında Azure VM'de tooconnect toohello. Çoğaltma Azure VM'ler için ağ stratejinizi tasarlarken, birkaç seçeneğiniz vardır:

- **Farklı bir IP adresi kullanmak**: hello çoğaltılan Azure VM ağında için farklı bir IP adresi aralığı toouse seçebilirsiniz. Bu senaryo hello VM yük devretme sonrasında yeni bir IP adresi alır ve DNS güncelleştirme gerekli değildir.
- **Korumak hello aynı IP adresini**:, isteyebilirsiniz, birincil şirket içi, Merhaba Azure ağı yük devretme sonrasında ağ olarak toouse hello aynı IP adresi aralığı.  Aynı IP adreslerini basitleştirir tutma hello azaltarak hello kurtarma yük devretme sonrasında ilgili sorunlar ağ. Ancak, tooAzure çoğaltırken, yük devretme sonrasında tooupdate yollar hello IP adreslerinin hello yeni konumla gerekir.


## <a name="retain-ip-addresses"></a>IP adreslerini korur

Site Recovery, bir alt ağ yük devretme ile tooAzure üzerinden başarısız olduğunda hello yetenek tooretain sabit IP adresleri sağlar.

Alt ağ yük devretmesi ile belirli bir alt aynı anda Site 1 veya her iki sitede ancak hiçbir Site 2 konumunda bulunur. Sipariş toomaintain hello IP adres alanı bir yük devretme hello olaydaki, program aracılığıyla hello yönlendirici altyapı toomove hello alt ağlardan bir site tooanother için düzenleyin. Yük devretme sırasında korumalı VM'lerin hello alt ağlar taşıma hello ile ilişkilendirilmiş. Merhaba asıl sakıncası bir hatanın hello olayı, toomove hello tüm alt ağı olmasıdır.



### <a name="failover-example"></a>Yük devretme örneği

Yük devretme tooAzure için bir örneğe bakalım.

- Ficticious şirket, Woodgrove Bank, iş uygulamalarını barındıran bir şirket içi altyapı sahiptir. Kullanıcıların mobil uygulamalar Azure üzerinde barındırılır.
- Azure ve şirket içi sunucularda Woodgrove Bank VM'ler arasında bağlantı hello şirket içi uç ağ hello Azure sanal ağı arasında bir siteden siteye (VPN) bağlantısı tarafından sağlanır.
- Azure sanal ağında şirketin hello VPN deyişle kendi şirket içi ağ bir uzantısı olarak görünür.
- Woodgrove toouse Site Recovery tooreplicate şirket içi iş yüklerini tooAzure istemektedir.
 - Woodgrove toodeal uygulamaları ve IP adreslerini sabit kodlanmış bağlıdır ve dolayısıyla tooretain IP adresi için kendi uygulamalarında sonra Yük devretme tooAzure kullanması gereken yapılandırmaları vardır.
 - Woodgrove atanmış IP adresleri aralığı 172.16.1.0/24 Azure'da çalışan 172.16.2.0/24 tooits kaynakları.


Kendi sanal makineleri tooAzure korunuyor hello sırada IP adresleri Woodgrove toobe mümkün tooreplicate için işte hangi hello şirketin toodo gerekir:

1. Bir Azure sanal ağı oluşturun. Böylece uygulamaları sorunsuz bir şekilde yük devredebildiğini hello uzantısı ağ, şirket içi olmalıdır.
2. Azure, tooadd siteden siteye VPN bağlantısı, ayrıca Azure içinde oluşturulan toopoint site bağlantısı toohello sanal ağlar sağlar.
3. Merhaba siteden siteye bağlantı kurma, hello Azure ağ, başlangıç IP adresi aralığı hello şirket içi IP adresi aralığından farklı olduğunda trafiği toohello şirket içi konumu (yerel ağ) yönlendirebilir.
    - Azure esnetilen alt ağları desteklemiyor olmasıdır. Bu nedenle içi 192.168.1.0/24 alt ağı varsa, bir yerel ağ 192.168.1.0/24 hello Azure ağı eklenemiyor.
    - Azure hello alt ağda etkin VM yok ve yalnızca olağanüstü durum kurtarma için oluşturulan hello alt bilmiyor çünkü bu beklenir.
    - toobe mümkün toocorrectly ağ trafiğini yönlendirmek hello ağ ve hello yerel ağ bir Azure ağı hello alt dışında çakışma gerekir.

![Alt ağ yük devretme önce](./media/vmm-to-azure-walkthrough-network/network-design7.png)

### <a name="before-failover"></a>Önce yük devretme

1. Ek bir ağa (örneğin kurtarma ağ) oluşturun. Bu hello ağdır VM'ler başarısız olarak oluşturulur.
2. IP adresi için bir VM hello tooensure hello VM Özellikleri'nde, yük devretme sonrasında tutulur > **yapılandırma**, aynı IP adresi VM içi sahip ve'ı tıklatın, hello hello belirtin **kaydetmek**.
3. Merhaba VM üzerinden başarısız olduğunda, Azure Site Recovery IP adresi tooit sağlanan hello atayın.

    ![Ağ Özellikleri](./media/vmm-to-azure-walkthrough-network/network-design8.png)

4. Yük devretme tetikleyici tetiklenir ve hello VM'ler Azure'da hello gerekli IP adresi ile oluşturulur olduktan sonra ağ toohello kullanarak bağlanabilir bir [Vnet tooVnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md). Bu eylem betiği yazılabilir.
5. Yollar uygun şekilde değiştirilmiş toobe tooreflect gerekir, 192.168.1.0/24 şimdi tooAzure taşındı.

    ![Alt ağ yük devretme sonrasında](./media/vmm-to-azure-walkthrough-network/network-design9.png)

### <a name="after-failover"></a>Yük devretme sonrasında

Yukarıda gösterildiği gibi bir Azure ağı yoksa, failvoer sonra birincil site ile Azure arasında siteden siteye VPN bağlantısı oluşturabilirsiniz.

## <a name="change-ip-addresses"></a>IP adreslerini değiştirin

Bu [blog gönderisi](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) tooset hello tooretain IP gerekmediğinde Azure ağ altyapısı yukarı yük devretme sonrasında nasıl ele açıklar. Uygulama açıklaması ile başlayan, nasıl tooset ağ şirket içi ve Azure arar ve yük devretme işlemleri çalıştırma hakkında bilgi ile sonlanır.  

## <a name="next-steps"></a>Sonraki adımlar

Çok Git[5. adım: Azure hazırlama](vmm-to-azure-walkthrough-prepare-azure.md)
