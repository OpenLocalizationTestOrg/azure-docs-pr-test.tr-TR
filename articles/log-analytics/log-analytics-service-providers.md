---
title: "Hizmet sağlayıcıları için Analytics özellikleri aaaLog | Microsoft Docs"
description: "Günlük analizi yönetilen hizmet sağlayıcıları (MSP'ler), büyük kuruluşlar, bağımsız yazılım satıcıları (ISV) yardımcı olabilir ve barındırma hizmeti sağlayıcıları yönetebilir ve müşterinin şirket içi veya Bulut altyapı sunucularını izleyebilirsiniz."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: c07f0b9f-ec37-480d-91ec-d9bcf6786464
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: richrund
ms.openlocfilehash: 3c0a93232293f90385c6c724be436cee1cf855f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-features-for-service-providers"></a>Hizmet sağlayıcıları için günlük analizi özellikleri
Günlük analizi, yönetilen hizmet sağlayıcıları (MSP'ler), büyük kuruluşlar, bağımsız yazılım satıcılarının (ISV'ler) ve barındırma hizmeti sağlayıcıları yönetmek ve müşterinin şirket içi veya Bulut altyapı sunucularını izlemek yardımcı olabilir. 

Büyük kuruluşlar özellikle yönetmekten sorumlu merkezi bir BT Ekibi olduğunda bu benzer şekilde hizmet sağlayıcıları ile paylaşmak için birçok farklı iş birimleri BT. Kolaylık olması için bu belgede hello terimini kullanır *hizmet sağlayıcısı* ancak hello aynı işlevselliği da kuruluşlar ve diğer müşteriler için kullanılabilir.

## <a name="cloud-solution-provider"></a>Bulut Çözümü Sağlayıcısı
İş ortakları ve hello parçası olan hizmet sağlayıcıları için [bulut çözümü sağlayıcısı (CSP)](https://partner.microsoft.com/Solutions/cloud-reseller-overview) program, günlük analizi hello Azure hizmetlerini bir CSP abonelikte kullanılabilir biridir. 

Aşağıdaki yetenekleri hello günlük analizi için etkinleştirilmiş olan *bulut çözümü sağlayıcısı* abonelikleri.

Farklı bir *bulut çözümü sağlayıcısı* şunları yapabilirsiniz:

* Günlük analizi çalışma alanları (müşterinin adına) Kiracı aboneliği oluşturun.
* Erişim çalışma alanları kiracılar tarafından oluşturuldu. 
* Kullanıcı erişim toohello çalışma Azure kullanıcı Yönetimi'ni kullanarak ekleyip yeniden açın. Bir kiracının çalışma alanında hello OMS portalı hello kullanıcı yönetimi sayfasına ayarlar altında bulunmaması durumunda
  * Rol tabanlı erişim henüz - kullanıcı vermiş günlük analizi desteklemiyor `reader` hello Azure portal'ın izni bunları toomake yapılandırma değişiklikleri hello OMS portalında

toolog tooa kiracının Abonelikteki toospecify hello Kiracı tanımlayıcı gerekir. Merhaba Kiracı genellikle hello e-posta adresi kullanılan toosign son kısmı tanımlayıcısıdır.

* Merhaba OMS portalında ekleme `?tenant=contoso.com` hello portalı için hello URL'de. Örneğin, `mms.microsoft.com/?tenant=contoso.com`
* PowerShell'de hello kullanın `-Tenant contoso.com` kullanırken parametresi `Add-AzureRmAccount` cmdlet'i
* Merhaba Kiracı tanımlayıcı hello kullandığınızda otomatik olarak eklenen `OMS portal` bağlantı hello Azure portal tooopen ve seçili hello çalışma alanı için toohello OMS portalında oturum

Farklı bir *müşteri* bir bulut çözümü sağlayıcısı şunları yapabilirsiniz:

* Günlük analizi çalışma alanları bir CSP abonelikte oluşturun.
* Merhaba CSP tarafından oluşturulan erişim çalışma alanları
  * Kullanım hello `OMS portal` bağlantı hello Azure portal tooopen ve seçili hello çalışma alanı için toohello OMS portalında oturum
* Görüntüleme ve Itanium tabanlı sistemler için hello kullanıcı yönetimi sayfasına ayarlar altında hello OMS portalında kullanma

> [!NOTE]
> Yedekleme Hello dahil ve Site kurtarma çözümleri için günlük analizi yapabilir tooconnect tooa kurtarma Hizmetleri kasası olup olmadığı ve CSP aboneliğindeki yapılandırılamıyor. 
> 
> 

## <a name="managing-multiple-customers-using-log-analytics"></a>Günlük analizi kullanarak birden çok müşterileri yönetme
Yönettiğiniz her müşteri için günlük analizi çalışma alanı oluşturma önerilir. Günlük analizi çalışma alanı sağlar:

* Depolanan verileri toobe için bir coğrafi konum. 
* Fatura için ayrıntı düzeyi 
* Veri yalıtımı 
* Benzersiz yapılandırma

Bir çalışma alanı Müşteri başına oluşturarak, mümkün tookeep her müşterinin verileri ayrı ve ayrıca her bir müşteri hello kullanımını izlemek.

Ne zaman ve neden toocreate birden çok çalışma açıklanan hakkında daha fazla ayrıntı [erişim toolog Analytics'i yönetme](log-analytics-manage-access.md#determine-the-number-of-workspaces-you-need).

Oluşturma ve yapılandırma müşteri çalışma alanlarının otomatik hale getirilebilir kullanarak [PowerShell](log-analytics-powershell-workspace-configuration.md), [Resource Manager şablonları](log-analytics-template-workspace-configuration.md), veya hello kullanarak [REST API](https://www.nuget.org/packages/Microsoft.Azure.Management.OperationalInsights/).

Çalışma alanı yapılandırması için Resource Manager şablonları Hello kullanımı toohave kullanılan toocreate ve çalışma alanları yapılandırma bir ana yapılandırma sağlar. Çalışma alanları için oluşturulan otomatik olarak oldukları müşteriler tooyour gereksinimleri yapılandırılmış emin olabilir. Gereksinimlerinizi güncelleştirdiğinizde hello şablon güncelleştirilir ve hello varolan çalışma alanları yeniden. Bu işlem, hatta varolan çalışma yeni standartlarınızı karşılamak sağlar.    

Birden çok günlük analizi çalışma yönetirken, her çalışma alanında varolan gişe sistemiyle tümleştirme öneririz / işletim konsolunu kullanarak hello [uyarıları](log-analytics-alerts.md) işlevselliği. Varolan sistemlerinizi ile tümleştirerek, destek personeli toofollow tanıdık süreçlerinin devam edebilirsiniz. Günlük analizi düzenli olarak her çalışma hello Uyarı ölçütleri belirttiğiniz karşı denetler ve eylem gerekli olduğunda bir uyarı oluşturur.

Merhaba veri kişiselleştirilmiş görünümleri kullanma [Pano](../azure-portal/azure-portal-dashboards.md) hello Azure portal özelliği.  

Yönetici düzeyi için kullanabileceğiniz çalışma alanları arasında verileri özetleyen raporları hello günlük analizi arasında tümleştirme ve [Powerbı](log-analytics-powerbi.md). Başka bir raporlama sistemi toointegrate gerekirse hello arama API kullanabilirsiniz (PowerShell aracılığıyla veya [REST](log-analytics-log-search-api.md)) toorun sorgular ve dışarı aktarma arama sonuçlarında.

## <a name="next-steps"></a>Sonraki Adımlar
* Oluşturma ve kullanarak çalışma yapılandırılmasını otomatikleştirmek [Resource Manager şablonları](log-analytics-template-workspace-configuration.md)
* Kullanarak çalışma oluşturulmasını otomatik hale [PowerShell](log-analytics-powershell-workspace-configuration.md) 
* Kullanım [uyarıları](log-analytics-alerts.md) toointegrate mevcut sistemlerle
* Özet raporları kullanarak oluşturmak [Powerbı](log-analytics-powerbi.md)

