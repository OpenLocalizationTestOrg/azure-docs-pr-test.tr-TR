---
title: "aaaAzure Danışmanı maliyet önerileri | Microsoft Docs"
description: "Azure Danışmanı toooptimize hello Azure dağıtımlarınızı maliyetini kullanın."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 50f70c33a17f550c8753795435cdfddd51e409f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-cost-recommendations"></a>Advisor maliyet önerileri

En iyi duruma getirme ve genel Azure azaltmak Danışmanı yardımcı olur, boşta ve az kaynaklarını tanımlayarak ayırın. Merhaba önerileri maliyet **maliyet** hello Danışmanı Pano sekmesinde.

![Advisor maliyet sekmesi](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a>En iyi duruma getirme sanal makine harcamanız az örneklerini yeniden boyutlandırma 
Belirli uygulama senaryoları düşük kullanımı tasarım gereği neden olabilir ancak genellikle hello boyutunu ve sanal makinelerinizi sayısını yöneterek para kaydedebilirsiniz. Advisor 14 gün boyunca, sanal makine kullanımını izler ve düşük kullanımı sanal makineleri tanımlar. Sanal makineler, CPU kullanımı yüzde 5'idir veya daha az ve ağ kullanımını 7 MB veya daha az dört veya daha fazla gün düşük kullanımı sanal makineler olarak kabul edilir.

Aşağı ya da yeniden boyutlandırmak tooshut seçebilmeleri sanal makineniz toorun etmeden tahmini maliyeti hello Danışmanı gösterir.  

![Sanal makineler yeniden boyutlandırma için öneriler maliyet Danışmanı](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-toomanage-performance-goals-of-multiple-sql-databases"></a>Birden çok SQL veritabanları, uygun maliyetli bir çözüm toomanage performans hedeflerini kullanın
Advisor esnek veritabanı havuzu oluşturma yararlanabilir SQL server örnekleri tanımlar. Esnek veritabanı havuzları basit ve ekonomik çözüm toomanage hello performans hedeflerini değişen kullanım desenlerini sahip birden çok veritabanlarının sağlar. Azure esnek havuzları hakkında daha fazla bilgi için bkz: [bir Azure esnek havuz nedir?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).

![Esnek veritabanı havuzlarına ilişkin öneriler maliyet Danışmanı](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-tooaccess-cost-recommendations-in-azure-advisor"></a>Nasıl tooaccess Azure Advisor önerileri maliyet

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).

2. Merhaba sol bölmede **daha fazla hizmet**.

3. Hello menü bölmesi altında hizmet **izleme ve Yönetim**, tıklatın **Azure Danışmanı**.  
 Merhaba Danışmanı Panosu görüntülenir.

4. Hello Danışmanı Panoda hello tıklatın **maliyet** sekmesi.

5. Kendisi için tooreceive önerileri istediğiniz ve ardından hello aboneliği seçin **alma önerileri**.

> [!NOTE]
> tooaccess Advisor önerileri, şunları yapmalısınız ilk *aboneliğinizi kaydetmek* Danışmanı ile. Bir abonelik kayıtlı olduğunda bir *abonelik sahibi* başlatır hello Danışmanı Pano ve tıklama hello **alma önerileri** düğmesi. Bu bir *tek seferlik işlem*. Merhaba abonelik kaydedildikten sonra Advisor önerileri olarak erişebilir *sahibi*, *katkıda bulunan*, veya *okuyucu* abonelik, bir kaynak grubu için veya bir belirli kaynak.

## <a name="next-steps"></a>Sonraki adımlar

Advisor önerileri hakkında daha fazla toolearn bakın:
* [Giriş tooAdvisor](advisor-overview.md)
* [Kullanmaya Başlama](advisor-get-started.md)
* [Advisor performans önerileri](advisor-cost-recommendations.md)
* [Advisor yüksek kullanılabilirlik önerileri](advisor-cost-recommendations.md)
* [Advisor güvenlik önerileri](advisor-cost-recommendations.md)
