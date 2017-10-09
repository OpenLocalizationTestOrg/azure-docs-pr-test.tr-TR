---
title: "fiziksel sunucu çoğaltma tooAzure için ağ aaaPlan | Microsoft Docs"
description: "Bu makalede ağ fiziksel sunucuları tooAzure çoğaltırken gerekli planlama açıklanır"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 71db2435-b5ce-4263-83f6-093d10d1d4e1
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: e2ca2db2a1cb58ca5468d4ee2b0406f29ff09479
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-physical-server-replication-tooazure"></a>4. adım: ağ fiziksel sunucu çoğaltma tooAzure için planlama

Bu makalede ağ çoğaltmaya fiziksel sunucuları tooAzure hello kullanarak şirket içi zaman planlama konuları özetler [Azure Site Recovery](site-recovery-overview.md) hizmet.

Bu makalenin hello altındaki tüm yorumlar gönderin ya da hello sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="connect-tooreplica-azure-vms"></a>Tooreplica Azure Vm'lerine bağlanmak

Çoğaltma ve yük devretme stratejinizi planlarken hello önemli sorular biri nasıl yük devretme sonrasında Azure VM'de tooconnect toohello. Çoğaltma Azure VM'ler için ağ stratejinizi tasarlarken, birkaç seçeneğiniz vardır:

- **Farklı bir IP adresi kullanmak**: hello çoğaltılan Azure VM ağında için farklı bir IP adresi aralığı toouse seçebilirsiniz. Bu senaryoda, yük devretme ve DNS güncelleştirme tamamlandıktan sonra gerekli hello makine yeni bir IP adresi alır.
- **Kullanım hello aynı IP adresi**: bunu istemeyebilirsiniz toouse hello aynı IP adresi aralığı olarak hello yük devretme sonrasında Azure ağ için birincil şirket içi sitenizdeki. Aynı IP adreslerini basitleştirir tutma hello azaltarak hello kurtarma yük devretme sonrasında ilgili sorunlar ağ. Ancak, tooAzure çoğaltırken, yük devretme sonrasında tooupdate yollar hello IP adreslerinin hello yeni konumla gerekir.

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


Kendi sunucuları tooAzure korunuyor hello sırada IP adresleri Woodgrove toobe mümkün tooreplicate için işte hangi hello şirketin toodo gerekir:

1. Bir Azure sanal ağı oluşturun. Böylece uygulamaları sorunsuz bir şekilde yük devredebildiğini hello uzantısı ağ, şirket içi olmalıdır.
2. Azure, tooadd siteden siteye VPN bağlantısı, ayrıca Azure içinde oluşturulan toopoint site bağlantısı toohello sanal ağlar sağlar.
3. Merhaba siteden siteye bağlantı kurma, hello Azure ağ, başlangıç IP adresi aralığı hello şirket içi IP adresi aralığından farklı olduğunda trafiği toohello şirket içi konumu (yerel ağ) yönlendirebilir.
    - Azure esnetilen alt ağları desteklemiyor olmasıdır. Bu nedenle içi 192.168.1.0/24 alt ağı varsa, bir yerel ağ 192.168.1.0/24 hello Azure ağı eklenemiyor.
    - Azure hello alt ağda etkin bir makinelere vardır ve hello alt yalnızca olağanüstü durum kurtarma için oluşturulan bilmiyor çünkü bu beklenir.
    - toobe mümkün toocorrectly ağ trafiğini yönlendirmek hello ağ ve hello yerel ağ bir Azure ağı hello alt dışında çakışma gerekir.

![Alt ağ yük devretme önce](./media/physical-walkthrough-network/network-design7.png)

#### <a name="before-failover"></a>Önce yük devretme

1. Ek bir ağa (örneğin kurtarma ağ) oluşturun. Bu hello ağdır VM'ler başarısız olarak oluşturulur.
2. bir makine için IP adresi hello tooensure hello makine özelliklerinde bir yük devretme sonrasında tutulur > **yapılandırma**, sunucu hello aynı IP adresini şirket içi sahip ve'ı tıklatın hello belirtin **kaydetmek**.
3. Merhaba makine üzerinden başarısız olduğunda, Azure Site Recovery IP adresi tooit sağlanan hello atayın.
4. Yük devretme tetikleyici tetiklenir ve hello VM'ler Azure'da hello gerekli IP adresi ile oluşturulur olduktan sonra ağ toohello kullanarak bağlanabilir bir [Vnet tooVnet bağlantı](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md). Bu eylem betiği yazılabilir.
5. Yollar uygun şekilde değiştirilmiş toobe tooreflect gerekir, 192.168.1.0/24 şimdi tooAzure taşındı.

    ![Alt ağ yük devretme sonrasında](./media/physical-walkthrough-network/network-design9.png)

#### <a name="after-failover"></a>Yük devretme sonrasında

Yukarıda gösterildiği gibi bir Azure ağı yoksa, yük devretme sonrasında birincil site ile Azure arasında siteden siteye VPN bağlantısı oluşturabilirsiniz.

## <a name="change-ip-addresses"></a>IP adreslerini değiştirin

Bu [blog gönderisi](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) tooset hello tooretain IP gerekmediğinde Azure ağ altyapısı yukarı yük devretme sonrasında nasıl ele açıklar. Uygulama açıklaması ile başlayan, nasıl tooset ağ şirket içi ve Azure arar ve yük devretme işlemleri çalıştırma hakkında bilgi ile sonlanır.  

## <a name="next-steps"></a>Sonraki adımlar

Çok Git[5. adım: Azure hazırlama](physical-walkthrough-prepare-azure.md)
