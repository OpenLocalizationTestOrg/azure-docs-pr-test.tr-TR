---
title: "aaaDeployment sorunlar için Microsoft Azure bulut Hizmetleri ile ilgili SSS | Microsoft Docs"
description: "Bu makalede, Microsoft Azure bulut Hizmetleri için dağıtım hakkında sık sorulan sorular hello listelenmektedir."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 8d67e36aa87fb5794d358e5cc235123ac7286028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Azure bulut Hizmetleri için dağıtım sorunlarını: sık sorulan sorular (SSS)

Bu makale için dağıtım sorunları hakkında sık sorulan sorular içerir [Microsoft Azure bulut Hizmetleri](https://azure.microsoft.com/services/cloud-services). Merhaba de başvurabilirsiniz [bulut Hizmetleri VM boyutu sayfa](cloud-services-sizes-specs.md) boyutu bilgi.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-does-deploying-a-cloud-service-toohello-staging-slot-sometimes-fail-with-a-resource-allocation-error-if-there-is-already-an-existing-deployment-in-hello-production-slot"></a>Var olan bir dağıtıma hello üretim yuvasında zaten varsa neden bir bulut hizmeti toohello dağıtımı hazırlık yuvasındaki bazen bir kaynak ayırma hatası ile başarısız oluyor?
Bir bulut hizmeti dağıtımı her iki yuvada hello tüm bulut hizmeti sabitlenmiş tooa belirli küme ise. Bu, zaten bir dağıtım hello üretim yuvasında zaten varsa, yeni bir hazırlama dağıtımı yalnızca aynı hello üretim yuvasına küme hello tahsis edilebilir olduğunu anlamına gelir.

Bulut hizmetinizi bulunduğu hello küme dağıtım isteğiniz kaynakları toosatisfy işlem yeterli fiziksel yok ayırma hataları oluşur.

Bu tür ayırma hataları Azaltıcı Yardım için bkz. [bulut hizmeti ayırma hatası: çözümleri](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-scaling-up-or-scaling-out-a-cloud-service-deployment-sometimes-result-in-allocation-failure"></a>Neden ölçeklendirmeyi veya bir bulut hizmeti dağıtımı bazen neden ayırma hatası çıkış ölçeklendirme mu?
Bir bulut hizmeti dağıtıldığında, genellikle sabitlenmiş tooa belirli küme alır. Bu yükseltme anlamına gelir / var olan bir bulut hizmeti hello yeni durumlarda ayırmalısınız aynı küme. Merhaba küme kapasitesine yaklaşıyor veya hello istenen VM boyutu/türü mevcut değil, hello isteği başarısız olabilir.

Bu tür ayırma hataları Azaltıcı Yardım için bkz. [bulut hizmeti ayırma hatası: çözümleri](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-deploying-a-cloud-service-into-an-affinity-group-sometimes-result-in-allocation-failure"></a>Neden bir bulut hizmeti bir benzeşim grubuna bazen dağıtma ayırma hatasına neden?
Merhaba bulut hizmeti sabitlenmiş tooan benzeşim grubu olmadıkça yeni bir dağıtım tooan boş bulut hizmeti bu bölgedeki herhangi bir küme hello yapıda ayrılabilir. Aynı benzeşim grubu üzerinde hello deneneceğini dağıtımları toohello aynı küme. Merhaba küme kapasitesine yaklaşıyor hello isteği başarısız olabilir.

Bu tür ayırma hataları Azaltıcı Yardım için bkz. [bulut hizmeti ayırma hatası: çözümleri](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-changing-vm-size-or-adding-a-new-vm-tooan-existing-cloud-service-sometimes-result-in-allocation-failure"></a>Neden yeni bir VM tooan mevcut bulut hizmeti bazen ekleme veya VM boyutunu değiştirme ayırma hatasına neden?
bir veri merkezinde Hello kümeleri makine türlerinin (örneğin, bir seri, Av2 serisi, D serisi, Dv2 serisi, G serisi, H serisi, vb.) farklı yapılandırmalara sahip. Ancak tüm hello kümeleri mutlaka türlü hello VM'ler gerekir. Örneğin, tooadd D serisinin bir A yalnızca serisi kümede dağıtılmış VM tooa bulut hizmeti çalışırsanız, bir ayırma hatası karşılaşırsınız. Çalışırsanız, bu da (örneğin, bir A series tooa D serisinden değiştirme) toochange SKU VM boyutları gerçekleşir.

Bu tür ayırma hataları Azaltıcı Yardım için bkz. [bulut hizmeti ayırma hatası: çözümleri](cloud-services-allocation-failures.md#solutions).

toocheck hello boyutları kullanılabilir, bölgenizdeki bkz [Microsoft Azure: bölgeye göre ürünleri](https://azure.microsoft.com/regions/services).

## <a name="why-does-deploying-a-cloud-service-sometime-fail-due-toolimitsquotasconstraints-on-my-subscription-or-service"></a>Neden bir buluta dağıtma hizmet süre başarısız son toolimits/kotaları/kısıtlamaları abonelik veya hizmet?
Ayrılmış gerekli toobe hello kaynaklarını hello varsayılan veya hello bölge/veri merkezi düzeyinde hizmetiniz için izin verilen en yüksek kota aşarsanız bir bulut hizmeti dağıtımının başarısız olabilir. Daha fazla bilgi için bkz: [bulut Hizmetleri sınırlar](../azure-subscription-service-limits.md#cloud-services-limits).

Merhaba portal aboneliğinizi için hello geçerli kullanım/kotası izlemek de: Azure Portal = > abonelikleri = > \<uygun abonelik > = > "Kullanım + kota".

Kaynak kullanım/kullanımı ile ilgili bilgileri de hello Azure faturalama API'leri alınabilir. Bkz: [Azure kaynak kullanım API'si (Önizleme)](../billing/billing-usage-rate-card-overview.md#azure-resource-usage-api-preview).

## <a name="how-can-i-change-hello-size-of-a-deployed-cloud-service-vm-without-redeploying-it"></a>Dağıtılan bulut hizmeti VM hello boyutunu yeniden dağıtmadan nasıl değiştirebilirim?
Merhaba VM boyutu dağıtılan bulut hizmetinin yeniden dağıtmadan değiştiremezsiniz. Merhaba VM boyutu hello dağıtın ile yalnızca güncelleştirilebilir CSDEF içinde yerleşik olarak bulunur.

Daha fazla bilgi için bkz: [nasıl tooupdate bir bulut hizmeti](cloud-services-update-azure-service.md).

 
