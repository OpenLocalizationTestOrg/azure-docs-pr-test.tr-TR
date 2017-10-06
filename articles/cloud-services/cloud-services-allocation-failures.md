---
title: "Bulut hizmeti ayırma hatası aaaTroubleshooting | Microsoft Docs"
description: "Azure’da Cloud Services dağıtımı sırasında oluşan ayırma hatalarını giderme"
services: azure-service-management, cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 529157eb-e4a1-4388-aa2b-09e8b923af74
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: dfd5cc4663ccc6ed1b27ca9df579182737363b0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-allocation-failure-when-you-deploy-cloud-services-in-azure"></a>Azure’da Cloud Services dağıtımı sırasında oluşan ayırma hatalarını giderme
## <a name="summary"></a>Özet
Bulut hizmeti örnekleri tooa dağıtmak veya yeni web veya çalışan rolü örnekleri eklediğinizde, Microsoft Azure işlem kaynakları ayırır. Zaman zaman bile hello Azure abonelik limitleri düşmeden önce bu işlemleri yaparken hatalar alabilirsiniz. Bu makalede, bazı hello ortak ayırma hatalarının hello nedenlerini açıklar ve olası düzeltme önerir. hizmetlerinizin hello dağıtımını planlarken hello bilgiler de yararlı olabilir.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

### <a name="background--how-allocation-works"></a>Arka plan – ayırma nasıl çalışır?
Azure veri merkezlerinde Hello sunucuları kümeler halinde bölümlenir. Yeni bir bulut hizmeti ayırma isteği birden çok kümelerde denenir. Merhaba ilk örneği, bulut hizmeti dağıtılan tooa bulut hizmetinde (hazırlama veya üretim) olduğunda sabitlenmiş tooa küme alır. Herhangi bir daha fazla dağıtımları hello bulut hizmeti hello aynı olacağını için küme. Bu makalede, biz "sabitlenmiş tooa küme olarak" toothis başvurun. Aşağıdaki diyagram 1, birden çok kümelerde denenir normal bir ayırma hello durumunun gösterir; Diyagram 2, burada mevcut bulut hizmeti CS_1 hello çünkü o sabitlenmiş tooCluster 2 barındırılan bir ayırma hello durumunu gösterir.

![Ayırma diyagramı](./media/cloud-services-allocation-failure/Allocation1.png)

### <a name="why-allocation-failure-happens"></a>Ayırma hatası neden olur
Ayırma isteği sabitlenmiş tooa küme olduğunda hello kullanılabilir kaynak havuzu sınırlı tooa küme olduğundan toofind boş kaynak başarısız bir yüksek ihtimalini yoktur. Merhaba küme ücretsiz kaynağa sahip olsa bile Ayrıca, ayırma isteği sabitlenmiş tooa küme olmakla birlikte, istenen kaynak hello türü, küme tarafından desteklenmiyor, isteğiniz başarısız olur. Aşağıdaki diyagram 3 hello çalışması hello yalnızca adayı küme kaynakları serbest bırakmak olmadığından burada Sabitlenmiş ayırma başarısız gösterir. Diyagram 4 gösterir; burada Sabitlenmiş ayırma başarısız hello yalnızca adayı küme desteklemediğinden hello çalışması hello küme kaynakları serbest bırakmak olmasına rağmen hello istenen VM boyutu.

![Sabitlenmiş ayırma hatası](./media/cloud-services-allocation-failure/Allocation2.png)

## <a name="troubleshooting-allocation-failure-for-cloud-services"></a>Bulut Hizmetleri için sorun giderme ayırma hatası
### <a name="error-message"></a>Hata iletisi
Aşağıdaki hata iletisini hello görebilirsiniz:

    "Azure operation '{operation id}' failed with code Compute.ConstrainedAllocationFailed. Details: Allocation failed; unable toosatisfy constraints in request. hello requested new service deployment is bound tooan Affinity Group, or it targets a Virtual Network, or there is an existing deployment under this hosted service. Any of these conditions constrains hello new deployment toospecific Azure resources. Please retry later or try reducing hello VM size or number of role instances. Alternatively, if possible, remove hello aforementioned constraints or try deploying tooa different region."

### <a name="common-issues"></a>Yaygın Sorunlar
Bir ayırma isteği toobe sabitlenmiş tooa tek küme neden hello ortak ayırma senaryolar verilmiştir.

* Bir bulut hizmeti her iki yuvada bir dağıtım varsa tooStaging yuva - dağıtma, ardından hello tüm bulut sabitlenmiş tooa belirli küme hizmetidir.  Bu, zaten bir dağıtım hello üretim yuvasında zaten varsa, ardından yeni bir hazırlama dağıtımı yalnızca aynı hello üretim yuvasına küme hello tahsis edilebilir olduğunu anlamına gelir. Merhaba küme kapasitesine yaklaşıyor hello isteği başarısız olabilir.
* Ölçeklendirme - yeni örnekleri tooan mevcut bulut hizmetine eklenmesi gerekir tahsis hello aynı küme.  Küçük istekleri ölçekleme genellikle ayrılan, ancak her zaman değil. Merhaba küme kapasitesine yaklaşıyor hello isteği başarısız olabilir.
* Merhaba bulut hizmeti sabitlenmiş tooan benzeşim grubu olmadıkça benzeşim grubu - hello yapıda bu bölgedeki herhangi bir küme tarafından yeni bir dağıtım tooan boş bulut hizmeti ayrılabilir. Aynı benzeşim grubu üzerinde hello deneneceğini dağıtımları toohello aynı küme. Merhaba küme kapasitesine yaklaşıyor hello isteği başarısız olabilir.
* Benzeşim grubu vNet - eski sanal ağları olan bölgeler yerine bağlı tooaffinity grupları ve bu sanal ağlar bulut Hizmetleri'nde sabitlenmiş toohello benzeşim grubu küme olacaktır. Sanal ağ dağıtımları toothis türü sabitlenmiş hello kümede denenir. Merhaba küme kapasitesine yaklaşıyor hello isteği başarısız olabilir.

## <a name="solutions"></a>Çözümler
1. Bu bölgedeki tüm küme hello platform toochoose verdiğinden dağıtın tooa yeni bulut - Bu çözüm büyük olasılıkla toobe en başarılı hizmetidir.

   * Merhaba iş yükü tooa yeni bulut hizmeti dağıtma  
   * Merhaba CNAME veya bir kayıt toopoint trafiği toohello yeni bulut hizmeti güncelleştir
   * Sıfır trafiği toohello eski site geçiyor sonra hello eski bulut hizmeti silebilirsiniz. Bu çözüm, sıfır kapalı kalma süresi maruz.
2. Üretim ve hazırlama yuvası delete - Bu çözüm, var olan DNS adınızı korur ancak kapalı kalma süresi tooyour uygulama oluşturulmasına neden olur.

   * Merhaba üretim ve böylece hello bulut hizmeti boştur var olan bir bulut hizmetini yuvaları hazırlama silin ve ardından
   * Yeni bir dağıtımını hello mevcut bulut hizmeti oluşturun. Bu tooallocation hello bölgedeki tüm kümelerde yeniden deneyecek. Merhaba bulut hizmetinin değil bağlı tooan benzeşim grubu olduğundan emin olun.
3. Ayrılmış IP - Bu çözüm korumak, var olan IP adresi, ancak kapalı kalma süresi tooyour uygulama oluşturulmasına neden olur.  

   * Powershell kullanarak, varolan dağıtım için bir ReservedIP oluşturma

     ```
     New-AzureReservedIP -ReservedIPName {new reserved IP name} -Location {location} -ServiceName {existing service name}
     ```
   * Yukarıdaki hello hizmetin CSCFG içinde yeni ReservedIP hello emin toospecify yapmadan #2 izleyin.
4. Yeni dağıtımlar - benzeşim grubunun benzeşim grupları artık önerilen kaldırın. #1 toodeploy yeni bir bulut hizmeti yukarıdaki adımları izleyin. Bulut hizmeti bir benzeşim grubunda değil emin olun.
5. Tooa bölgesel sanal ağ - bakın Dönüştür [nasıl toomigrate benzeşim grupları tooa bölgesel sanal ağ (VNet) gelen](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
