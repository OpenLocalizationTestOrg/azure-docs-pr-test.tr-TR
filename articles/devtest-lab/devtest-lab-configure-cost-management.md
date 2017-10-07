---
title: "aaaView hello aylık tahmini Laboratuvar maliyet eğilimi Azure DevTest Labs | Microsoft Docs"
description: "Hello Azure DevTest Labs aylık tahmini maliyet eğilim Grafiği hakkında bilgi edinin."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1f46fdc5-d917-46e3-a1ea-f6dd41212ba4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 47c7dd4cf91b76de74b502c50f05e79cd501ee35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="view-hello-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a>Görünüm hello aylık tahmini Laboratuvar maliyet eğilimi Azure DevTest Labs
DevTest Labs Hello maliyet yönetim özelliği Laboratuvarınızı hello maliyetini izlemenize yardımcı olur. Bu makalede gösterilmektedir nasıl toouse hello **aylık tahmini maliyet eğilimi** grafik tooview geçerli Takvim ayın tahmini maliyet-to-date hello ve geçerli bir takvim ayının hello tahmini ayın son maliyeti hello. Bu makalede, nasıl tooview hello hello Azure portal aylık tahmini maliyet eğilimi grafikte öğrenin.

## <a name="viewing-hello-monthly-estimated-cost-trend-chart"></a>Merhaba aylık tahmini maliyet eğilim grafiği görüntüleme
tooview hello aylık tahmini maliyet eğilim Grafiği, şu adımları izleyin: 

1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Seçin **daha Hizmetleri**ve ardından **DevTest Labs** hello listeden.
3. Merhaba istenen Laboratuvar labs Hello listeden seçin.   
4. Merhaba Laboratuvar'ın dikey penceresinde, seçin **maliyet ayarlarına**.
5. Merhaba Laboratuvar'ın üzerinde **maliyet ayarlarına** dikey penceresinde, select **Laboratuvar maliyet eğilimi**.
6. Merhaba aşağıdaki ekran görüntüsünde bir maliyet grafik örneği gösterilmektedir. 
   
    ![Maliyet grafik](./media/devtest-lab-configure-cost-management/graph.png)

Merhaba **maliyet tahmini** değeri geçerli bir takvim ayının ait tahmini maliyet-to-date hello. Merhaba **tahmini maliyet** hello hello tamamı için tahmini maliyet geçerli Takvim ayı hello Laboratuvar maliyet Merhaba önceki beş gün kullanılarak hesaplanır.

Merhaba maliyet tutarlar toohello sonraki tam sayıya yuvarlanır. Örneğin: 

* 5.01 too6 yuvarlar 
* 5.50 too6 yuvarlar
* 5.99 too6 yuvarlar

Hello grafik durumları gibi hello grafikte gördüğünüz hello maliyetleri olduğundan *tahmini* kullanarak maliyetlerini [Kullandıkça Öde](https://azure.microsoft.com/offers/ms-azr-0003p/) hızları sunar.
Ayrıca, hello şunlardır *değil* hesaplama maliyet hello dahil:

* CSP ve Dreamspark abonelik şu anda desteklenmiyor Azure DevTest Labs hello kullandıkça [Azure fatura API'leri](../billing/billing-usage-rate-card-overview.md) toocalculate hello Laboratuvar maliyet, CSP veya Dreamspark abonelik desteklemiyor.
* Teklif ücretlerinizi. Şu anda, biz mümkün toouse olmayan teklif ücretlerinizi (abonelik altında Microsoft veya Microsoft iş ortakları anlaşılan olduğunu gösterilmiştir). Kullandıkça Öde oranları kullanıyoruz.
* Vergiler
* İndirim
* Fatura para birimi. Şu anda hello Laboratuvar maliyet yalnızca ABD Doları para birimi görüntülenir.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>İlgili blog gönderileri
* [İki daha fazla şey tookeep maliyetinizi DevTest Labs kanalındaki](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [Neden eşikleri maliyet?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a>Sonraki adımlar
Sonraki bazı şeyleri tootry şunlardır:

* [Laboratuvar ilkeleri tanımlar](devtest-lab-set-lab-policy.md) -nasıl tooset hello kullanılan çeşitli ilkeler öğrenin toogovern nasıl Laboratuvarınızı ve Vm'lerini kullanılır. 
* [Özel görüntü oluşturma](devtest-lab-create-template.md) - bir VM oluşturduğunuzda, özel bir görüntü veya bir Market görüntüsü olabilecek bir taban belirtin. Bu makalede nasıl toocreate özel bir görüntü bir VHD dosyasından gösterilmektedir.
* [Market görüntülerini yapılandırma](devtest-lab-configure-marketplace-images.md) - VMs Azure Market görüntülerini temel oluşturmayı DevTest Labs destekler. Bu makalede gösterilmektedir nasıl olabilen, varsa, Azure Market görüntülerini toospecify VM'ler bir laboratuar ortamında oluşturulurken kullanılır.
* [Bir laboratuar ortamında bir VM oluşturma](devtest-lab-add-vm-with-artifacts.md) -gösterilmektedir nasıl toocreate temel görüntü bir VM'den (ya da özel veya Market) ve nasıl toowork yapıtlarla birlikte, VM.

