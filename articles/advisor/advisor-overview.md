---
title: "aaaIntroduction tooAzure Danışmanı | Microsoft Docs"
description: "Azure Danışmanı toooptimize Azure dağıtımlarınızı kullanın."
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
ms.openlocfilehash: 5d796fc06366221efdb6f1bda39ab3fb676abfd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-advisor"></a>Giriş tooAzure Danışmanı

Azure Danışmanı ve temel işlevleri hakkında bilgi edinin ve sorulan soruları yanıtlar toofrequently alın.

## <a name="what-is-advisor"></a>Advisor nedir?
Advisor yardımcı olan kişiselleştirilmiş bulut Danışman Azure dağıtımlarınızı en iyi yöntemler toooptimize izleyin;. Kaynak yapılandırması ve kullanım telemetri analiz eder ve yardımcı olabilecek çözümler hello maliyet verimliliği, performans, yüksek kullanılabilirlik ve Azure kaynaklarınızın güvenliğini artırmak önerir.

Advisor ile şunları yapabilirsiniz:
* Get öngörülü, işlem yapılabilir ve öneriler kişiselleştirilmiş en iyi yöntemler. 
* Genel Azure harcamanız fırsatları tooreduce tanımlarken hello performans, güvenlik ve kaynaklarınızın yüksek kullanılabilirliğini artırır.
* Önerilen eylemleri satır içi ile ilgili öneriler alın.

Advisor hello erişebilirsiniz [Azure portal](https://aka.ms/azureadvisordashboard). İçinde toohello oturum [portal](https://portal.azure.com)seçin **Gözat**, çok kaydırarak**Azure Danışmanı**. Merhaba Danışmanı Pano seçili abonelik için kişiselleştirilmiş önerileri görüntüler. 

Merhaba önerileri dört kategoriye ayrılır: 

* **Yüksek kullanılabilirlik**: tooensure ve iş açısından kritik uygulamalar hello sürekliliği geliştirin. Daha fazla bilgi için bkz: [Danışmanı yüksek kullanılabilirlik önerileri](advisor-high-availability-recommendations.md).

* **Güvenlik**: toodetect Tehditler ve toosecurity ihlallerinden yol açabilecek güvenlik açıkları. Daha fazla bilgi için bkz: [Danışmanı güvenlik önerileri](advisor-security-recommendations.md).

* **Performans**: uygulamalarınızın tooimprove hello hızı. Daha fazla bilgi için bkz: [Danışmanı performans önerileri](advisor-performance-recommendations.md).

* **Maliyet**: toooptimize ve genel Azure azaltmak ayırın. Daha fazla bilgi için bkz: [Danışmanı maliyet önerileri](advisor-cost-recommendations.md).

  ![Advisor öneri türleri](./media/advisor-overview/advisor-all-tab-examples.png)

> [!NOTE]
> tooaccess Advisor önerileri, şunları yapmalısınız ilk *aboneliğinizi kaydetmek* Danışmanı ile. Bir abonelik kayıtlı olduğunda bir *abonelik sahibi* başlatır hello Danışmanı Pano ve tıklama hello **alma önerileri** düğmesi. Bu bir *tek seferlik işlem*. Merhaba abonelik kaydedildikten sonra Advisor önerileri olarak erişebilir *sahibi*, *katkıda bulunan*, veya *okuyucu* abonelik, bir kaynak grubu için veya bir belirli kaynak.

Bunun hakkında daha fazla bir öneri toolearn tıklayabilirsiniz. Ayrıca, fırsatı tootake avantajlarından gerçekleştirmek veya bir sorunu gidermek eylemler hakkında bilgi edinebilirsiniz. 

Advisor satır içi eylemler veya belgelere bağlantılar ile ilgili öneriler sunar. Satır içi eylemi tıklatarak alır, bir "Destekli kullanıcı gezisine" tooimplement bu. Bir belge bağlantıyı tıklatmak nasıl toomanually uygulamak hello eylemi açıklayan toodocumentation işaret eder. 

Advisor önerileri saatlik güncelleştirir. Bir öneriye tootake Acil eylem düşünmüyorsanız, belirli bir süre için uykuda ya da onu yok sayın. 

## <a name="frequently-asked-questions"></a>Sık sorulan sorular

### <a name="how-do-i-access-advisor"></a>Advisor nasıl erişirim?
Advisor hello erişebilirsiniz [Azure portal](https://aka.ms/azureadvisordashboard). İçinde toohello oturum [portal](https://portal.azure.com)seçin **Gözat**, çok kaydırarak**Azure Danışmanı**. Merhaba Danışmanı Pano seçili abonelik için kişiselleştirilmiş önerileri görüntüler. 

Bu gibi durumlarda, Advisor önerileri de hello sanal makine kaynak dikey penceresinde görüntüleyebilirsiniz. Bir sanal makine seçin ve ardından tooAdvisor önerileri hello menüde gidin. 

### <a name="what-permissions-do-i-need-tooaccess-advisor"></a>İzinleri ne tooaccess Danışmanı gerekir?

tooaccess Advisor önerileri, şunları yapmalısınız ilk *aboneliğinizi kaydetmek* Danışmanı ile. Bir abonelik kayıtlı olduğunda bir *abonelik sahibi* başlatır hello Danışmanı Pano ve tıklama hello **alma önerileri** düğmesi. Bu bir *tek seferlik işlem*. Merhaba abonelik kaydedildikten sonra Advisor önerileri olarak erişebilir *sahibi*, *katkıda bulunan*, veya *okuyucu* abonelik, bir kaynak grubu için veya bir belirli kaynak.

### <a name="how-often-are-advisor-recommendations-updated"></a>Ne sıklıkta güncelleştirilmiş Advisor önerileri misiniz?

Advisor önerileri saatlik güncelleştirilir.

### <a name="what-resources-does-advisor-provide-recommendations-for"></a>Hangi kaynaklara Danışmanı önerileri için sağlar?

Advisor sanal makineler, kullanılabilirlik kümeleri, uygulama ağ geçitleri, uygulama hizmetleri, SQL Server, SQL veritabanları ve Redis önbelleği için öneriler sağlar.

### <a name="can-i-snooze-or-dismiss-a-recommendation"></a>Uykuda veya miyim öneri yok sayın?

toosnooze veya bir öneri yok sayın, hello tıklatın **uykuda** düğmesini veya bağlantısını. Erteleme saati dönem veya select belirtebilirsiniz **hiçbir zaman** toodismiss hello öneri.

## <a name="next-steps"></a>Sonraki adımlar

Advisor önerileri hakkında daha fazla toolearn bakın:

* [Danışman’ı kullanmaya başlama](advisor-get-started.md)
* [Advisor yüksek kullanılabilirlik önerileri](advisor-high-availability-recommendations.md)
* [Advisor güvenlik önerileri](advisor-security-recommendations.md)
* [Advisor performans önerileri](advisor-performance-recommendations.md)
* [Advisor maliyet önerileri](advisor-cost-recommendations.md)
