---
title: "aaaScale kotalar ve sınırlar laboratuvarınızda Azure DevTest Labs | Microsoft Docs"
description: "Bilgi nasıl tooscale Azure DevTest Labs laboratuvarda"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: ae624155-9181-45fa-bd2b-1983339b7e0e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: tarcher
ms.openlocfilehash: 7fb429c0aabdfbce3a4a5aa6d9259daa2ee270d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a>Kotalar ve sınırlar DevTest Labs'de ölçeklendirme
DevTest Labs'de çalışırken hello DevTest Labs hizmet etkileyebilir Azure kaynaklarını belirli varsayılan sınırları toosome olduğunu fark edebilirsiniz. Başvurulan tooas bu kısıtlamalardır **kotaları**.

> [!NOTE]
> Merhaba DevTest Labs hizmet hiçbir kota zorunlu tuttukları değil. Karşılaşabileceğiniz kotaları hello genel Azure aboneliği varsayılan kısıtlamaları ' dir.

Kotasına ulaşana kadar her Azure kaynak kullanabilirsiniz. Her abonelik ayrı kotaları sahiptir ve abonelik başına kullanım izlenir.

Örneğin, her abonelik varsayılan kota 20 olarak belirlenen çekirdek sahiptir. Dört çekirdek ile laboratuvarınızda VM'ler oluşturuyorsanız, bu nedenle, daha sonra yalnızca beş VM'ler oluşturabilirsiniz. 

[Azure aboneliği ve hizmet sınırları](https://docs.microsoft.com/azure/azure-subscription-service-limits) bazı Azure kaynakları için en yaygın kotaları hello yer almaktadır. en yaygın olarak kullanılan bir laboratuar ortamında kaynakları hello ve hangi karşılaşabileceğiniz için kotaları dahil VM çekirdek, genel IP adresleri, ağ arabirimi, yönetilen diskleri, RBAC rol ataması ve ExpressRoute bağlantı hatları.

## <a name="view-your-usage-and-quotas"></a>Kotalar ve kullanım görüntüleyin
Bu adımlar nasıl tooview hello geçerli kotalar aboneliğinizde belirli Azure kaynaklarını ve toosee için kullandığınız her kota yüzdesini gösterir.

1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Seçin **daha Hizmetleri**ve ardından **faturalama** hello listeden.
1. Merhaba faturalama dikey penceresinde bir abonelik seçin.
4. Seçin **kullanım + kotaları**.

   ![Kullanım ve kotaları düğmesi](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   Merhaba kullanım + kotaları dikey penceresi görünür, farklı kaynaklar Bu abonelik ve hello yüzdesi kaynak başına kullanılan hello kota olarak listeleniyor.

   ![Kotalar ve kullanım](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a>Daha fazla kaynak aboneliğinizde isteme
Bir kota cap ulaştıysanız, bir kaynağın bir abonelik hello varsayılan sınır tooa sınırını, açıklandığı gibi artırılabilir [Azure aboneliği ve hizmet sınırları](https://docs.microsoft.com/azure/azure-subscription-service-limits).

Bu adımları nasıl toorequest kota artırma hello Göster [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Seçin **daha Hizmetleri**seçin **faturalama**ve ardından **kullanım + kotaları**.
1. Merhaba kullanım + kotaları dikey biçiminde hello seçin **isteği artırmak** düğmesi.

   ![İstek artış düğmesi](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. toocomplete ve hello isteği göndermek, gerekli hello bilgileri Merhaba, tüm üç sekmelerde doldurun **yeni destek isteği** formu.

   ![İstek artış formu](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

[Anlama Azure sınırları ve artar](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) Azure destek toorequest bağlantı kurma hakkında daha fazla bilgi sağlayan bir kota artırma.



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a>Sonraki adımlar
* Merhaba keşfedin [DevTest Labs Azure Resource Manager hızlı başlangıç Şablon Galerisi](https://github.com/Azure/azure-devtestlab/tree/master/Samples).
