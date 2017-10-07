---
title: aaaAzure faturalama API'leri | Microsoft Docs
description: "Azure kaynak tüketimini ve eğilimleri kullanılan tooprovide Öngörüler olan Azure faturalama kullanımını ve RateCard API'ları hakkında bilgi edinin."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/18/2017
ms.author: mobandyo;bryanla
ms.openlocfilehash: b3214996cc3279f76fdc7f0dbd2059c3ae7bb15c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-billing-apis-tooprogrammatically-get-insight-into-your-azure-usage"></a>Kullanım Azure faturalama API'leri tooprogrammatically Azure kullanımınızı bir anlayış Al
Azure faturalama API'leri toopull kullanımı ve kaynak verileri, tercih edilen veri çözümleme araçları kullanın. Hello Azure kaynak kullanımı ve RateCard API'leri doğru şekilde tahmin etmek ve maliyetlerinizi yönetmenize yardımcı olabilir. Merhaba API'leri bir kaynak sağlayıcısı ve Azure Resource Manager hello tarafından kullanıma sunulan API hello ailesinin bir parçası olarak uygulanır.  

## <a name="azure-invoice-download-api-preview"></a>Azure fatura indirme API (Önizleme)
Bir kez hello [katılımı tam](billing-manage-access.md#opt-in), indirme faturalar hello preview sürümünü kullanarak [fatura API](/rest/api/billing). Merhaba özellikleri içerir:

* **Azure rol tabanlı erişim denetimi** -erişimi yapılandırma hello ilkeleri [Azure portal](https://portal.azure.com) aracılığıyla veya [Azure PowerShell cmdlet'lerini](/powershell/azure/overview) toospecify hangi kullanıcıların veya uygulamaların erişim alabilirsiniz toohello aboneliğin kullanım verileri. Arayanlar, kimlik doğrulaması için standart Azure Active Directory belirteçleri kullanmanız gerekir. Merhaba arayan tooeither hello faturalama Okuyucu, okuyucu, sahibi veya katkıda bulunan rolü tooget erişim toohello kullanım verilerini belirli bir Azure aboneliği için ekleyin.
* **Tarih filtreleme** -kullanım hello `$filter` parametresi tooget hello tarafından ters kronolojik sırada tüm hello faturaları Fatura dönemi bitiş tarihi. 

> [!NOTE]
> Bu özellik ilk önizleme sürümünde olduğu ve konu toobackward uyumsuz değişiklikler olabilir. Şu anda kullanılabilir belirli abonelik teklifler (Kurumsal Sözleşme, CSP, desteklenmeyen AIO) ve Azure Almanya değil.

## <a name="azure-resource-usage-api-preview"></a>Azure kaynak kullanım API'si (Önizleme)
Kullanım hello Azure [kaynak kullanım API'si](https://msdn.microsoft.com/library/azure/mt219003) tooget tahmini Azure tüketim verilerinizi. Merhaba API içerir:

* **Azure rol tabanlı erişim denetimi** -erişimi yapılandırma hello ilkeleri [Azure portal](https://portal.azure.com) aracılığıyla veya [Azure PowerShell cmdlet'lerini](/powershell/azure/overview) toospecify hangi kullanıcıların veya uygulamaların erişim alabilirsiniz toohello aboneliğin kullanım verileri. Arayanlar, kimlik doğrulaması için standart Azure Active Directory belirteçleri kullanmanız gerekir. Merhaba arayan tooeither hello faturalama Okuyucu, okuyucu, sahibi veya katkıda bulunan rolü tooget erişim toohello kullanım verilerini belirli bir Azure aboneliği için ekleyin.
* **Saatlik veya günlük toplamalar** - arayanlar olup Azure kullanım verilerini saatlik istedikleri aralıkları belirtebilirsiniz veya günlük aralıkları. Merhaba varsayılan günlük.
* **(Kaynak etiketleri içerir) örneği meta veri** – tam Kaynak URI hello gibi örnek düzeyinde ayrıntı almak (/subscriptions/ {subscrıptıon-ID} /..), kaynak grubu bilgileri ve kaynak etiketleri hello. Bu meta veriler belirleyici biçimde yardımcı olur ve program aracılığıyla çapraz ücretlendirme gibi kullanım örnekleri için hello etiketleriyle kullanım paylaştırabilirsiniz.
* **Kaynak meta verilerini** -kaynak ayrıntılarını hello ölçüm adı, ölçüm kategori, ölçüm alt kategorisi, birim ve bölge gibi daha iyi ne tüketilen anlamak hello çağıran verin. Ayrıca tooalign kaynak meta verileri terminolojisi hello Azure portal, Azure kullanım CSV, CSV, faturalama EA ve diğer genel kullanıma yönelik deneyimleri deneyimleri arasında verilerin bağıntısını toolet üzerinde çalışıyoruz.
* **Tüm kullanım teklif türleri** – kullanım verilerini, tüm Kullandıkça Öde, MSDN, parasal taahhüt, kredi ve EA gibi türlerinde sunmak için kullanılabilir.

## <a name="azure-resource-ratecard-api-preview"></a>Azure kaynak RateCard API (Önizleme)
Kullanım hello [Azure kaynak RateCard API](https://msdn.microsoft.com/library/azure/mt219005) tooget hello listesi kullanılabilir Azure kaynakları ve her biri için tahmini fiyatlandırma bilgileri. Merhaba API içerir:

* **Azure rol tabanlı erişim denetimi** -hello üzerinde erişim ilkelerinizi yapılandırmak [Azure portal](https://portal.azure.com) aracılığıyla veya [Azure PowerShell cmdlet'lerini](/powershell/azure/overview) toospecify hangi kullanıcıların veya uygulamaların erişim alabilirsiniz toohello RateCard veri. Arayanlar, kimlik doğrulaması için standart Azure Active Directory belirteçleri kullanmanız gerekir. Merhaba arayan tooeither hello Okuyucu, sahibi veya katkıda bulunan rolü tooget erişim toohello kullanım verilerini belirli bir Azure aboneliği için ekleyin.
* **Kullandıkça Öde, MSDN, parasal taahhüt ve kredi desteği sunar (EA desteklenmiyor)** -bu API Azure teklifi düzeyi oranı bilgi sağlar.  Bu API Hello çağıran hello teklif bilgileri tooget kaynak ayrıntıları ve ücretlerin geçmesi gerekir. EA teklifleri kayıt göre oranları özelleştirilmiş olduğundan şu anda işleyemiyor tooprovide EA oranları çalışıyoruz. 

## <a name="scenarios"></a>Senaryolar
Merhaba kullanım ve hello RateCard API'leri hello birlikte olası hale getirilen hello senaryolardan bazıları şunlardır:

* **Azure hello ay sırasında harcadığı** -kullanım hello hello kullanım ve RateCard API'leri tooget daha iyi fikir bulut birleşimi hello ay sırasında harcadığı. Hello saatlik çözümleyebilir ve kullanımı ve Ücret günlük demet tahmin eder.
* **Uyarıları ayarlamak** – hello kullanım kullanın ve hello RateCard API'leri tooget tahmini bulut kullanımı ve ücretleri ve kaynak veya parasal tabanlı uyarıları ayarlayın.
* **Fatura tahmin** – tahmini tüketim ve bulut harcamanız ve hangi hello fatura döngüsü faturalama hello hello sonunda olacaktır algoritmaları toopredict öğrenme makinesi geçerli alın.
* **Analiz maliyetiyle öncesi tüketim** – ne kadar faturanızı, beklenen kullanımınız için olacaktır, iş yüklerini tooAzure taşıdığınızda hello RateCard API toopredict kullanın. Var olan iş yükleri diğer Bulut veya özel bulutlara varsa, ayrıca Azure daha iyi bir tahmin harcamanız hello Azure oranları tooget ile kullanımınızı eşleyebilirsiniz. Teklif ve karşılaştırma ve Kullandıkça Öde, ötesinde hello farklı teklif türleri arasında karşıtlığı özelliği toopivot hello tahmin kazandırır parasal taahhüt ve kredi gibi. Merhaba API de size hello özelliği toosee maliyet farkları bölgeye göre ve toodo dağıtım kararları yaptığınız benzetim maliyet analiz toohelp sağlar.
* **Çözümlemeleri** -
  
  * Daha fazla uygun maliyetli toorun iş yükünü başka bir bölgede ya da başka bir yapılandırması hello Azure kaynak olup olmadığını belirleyebilirsiniz. Azure kaynak maliyetleri değişebilir kullanmakta olduğunuz Azure bölgesi hello üzerinde temel.
  * Başka bir Azure Teklif türü bir Azure kaynağı üzerinde daha iyi oranı sağlar, ayrıca belirleyebilirsiniz.
  
## <a name="partner-solutions"></a>İş ortağı çözümleri
[Microsoft Azure kullanım ve RateCard API'leri etkinleştirin Cloudyn tooProvide müşteriler için ITFM](billing-usage-rate-card-partner-solution-cloudyn.md) Azure faturalama API iş ortağı tarafından sunulan hello tümleştirme deneyimini açıklamaktadır [Cloudyn](https://www.cloudyn.com/microsoft-azure/). Bu makalede deneyimlerini hakkında konuşur ve nasıl Cloudyn kullanın ve Azure faturalama API'leri tooget Öngörüler Azure tüketim verilerden hello gösteren bir video içerir.

[Cruiser ve Microsoft Azure fatura API tümleştirme bulut](billing-usage-rate-card-partner-solution-cloudcruiser.md) açıklar nasıl [Azure Pack için bulut Cruiser'ın Express](http://www.cloudcruiser.com/partners/microsoft/) doğrudan hello Microsoft Azure Pack (WAP) portalından çalışır. Bu gibi durumlarda, her iki hello işletimsel ve finansal yönlerini hello Microsoft Azure özel veya barındırılan genel bulut sorunsuz bir şekilde bir tek kullanıcı arabiriminden yönetebilirsiniz.   

## <a name="next-steps"></a>Sonraki adımlar
* Github'da hello kod örnekleri gözden geçirin:
  * [Fatura API kod örneği](https://go.microsoft.com/fwlink/?linkid=845124)

  * [Kullanım API'si kod örneği](https://github.com/Azure-Samples/billing-dotnet-usage-api)

  * [RateCard API kod örneği](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)

* toolearn hello Azure Resource Manager hakkında daha fazla bilgi görmek [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md). 

* Bulut bir anlayış almanız gerekli toohelp harcamanız hello suite araçları hakkında daha fazla bilgi için bkz: hello Gartner makale [BT Finansal Yönetimi (ITFM) araçları için Pazar Kılavuzu](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).

