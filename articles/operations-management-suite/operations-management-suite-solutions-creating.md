---
title: "aaaBuild OMS Yönetimi çözümünde | Microsoft Docs"
description: "Yönetim çözümleri genişletmek hello işlevselliği Operations Management Suite (OMS) paketlenmiş yönetim senaryoları sağlayarak müşteriler tootheir OMS çalışma ekleyebilirsiniz.  Bu makalede, yönetim çözümleri toobe nasıl oluşturabileceğinizi Ayrıntılar, kendi ortamınızda kullanılan veya kullanılabilir tooyour müşteriler yapılan sağlar."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: dea4c0d9e608d9fe4aa41088705958c9fe999372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-build-a-management-solution-in-operations-management-suite-oms-preview"></a>Tasarlama ve bir yönetim çözümü Operations Management Suite (OMS) (Önizleme) içinde oluşturma
> [!NOTE]
> Bu, şu anda önizlemede OMS yönetim çözümleri oluşturmak için başlangıç belgesidir. Aşağıda açıklanan herhangi bir şema konu toochange ' dir.

[Yönetim çözümleri](operations-management-suite-solutions.md) paketlenmiş yönetim senaryoları sağlayarak hello işlevselliğini Operations Management Suite (OMS) genişletmek müşteriler tootheir OMS çalışma ekleyebilirsiniz.  Bu makalede temel işlem toodesign gösterir ve en yaygın gereksinimleri için uygun bir yönetim çözümü oluşturmak.  Bu işlemi başlangıç noktası olarak kullanın ve gereksinimlerinizi geliştikçe daha karmaşık çözümleri hello kavramlarını yararlanan yeni toobuilding yönetim çözümleri varsa.

## <a name="what-is-a-management-solution"></a>Bir yönetim çözümü nedir?

Yönetim çözümleri OMS ve tooachieve belirli izleme senaryoları birlikte çalışan Azure kaynaklarını içerir.  Olarak uygulanan [kaynak Yönetim Şablonları](../azure-resource-manager/resource-manager-template-walkthrough.md) nasıl ayrıntılarını içeren tooinstall ve hello çözüm yüklendiğinde kapsanan kaynaklarını yapılandırın.

Merhaba temel stratejisi toostart, yönetim hello bileşenleri tek tek Azure ortamınıza oluşturarak çözümüdür.  Merhaba işlevselliği düzgün çalışmasını olduktan sonra sonra bunları paketleme başlatabilirsiniz bir [yönetim çözümü dosyası](operations-management-suite-solutions-solution-file.md). 


## <a name="design-your-solution"></a>Çözümünüzü tasarlayın
bir yönetim çözümü için Hello en yaygın düzeni diyagramı aşağıdaki hello gösterilir.  Bu modelde Hello farklı bileşenleri hello aşağıda ele alınmıştır.

![OMS çözümüne genel bakış](media/operations-management-suite-solutions/solution-overview.png)


### <a name="data-sources"></a>Veri kaynakları
çözümünü tasarlamanın ilk adımı hello hello günlük analizi depodan gerektiren hello veri belirliyor.  Bu veri topladığı bir [veri kaynağı](../log-analytics/log-analytics-data-sources.md) veya [başka bir çözüm](operations-management-suite-solutions.md), ya da çözümünüzü tooprovide hello işlem toocollect gerekebilir.

Merhaba günlük analizi deposunda açıklandığı gibi toplanan veri kaynakları, çeşitli yollarla olan [günlük analizi veri kaynaklarında](../log-analytics/log-analytics-data-sources.md).  Bu hello Windows olay günlüğü olaylarını içerir veya Syslog tarafından Windows ve Linux istemcileri için ayrıca tooperformance sayaçları oluşturulan.  Azure İzleyici tarafından toplanan Azure kaynaklarından verilerini de toplayabilirsiniz.  

Herhangi bir hello kullanılabilir veri kaynakları erişilebilir değil veri gerektiren sonra hello kullanabilirsiniz [HTTP veri toplayıcı API](../log-analytics/log-analytics-data-collector-api.md) olanak sağlayan bir REST çağrısı herhangi bir istemciden toowrite veri toohello günlük analizi deposu API.  Merhaba en yaygın olduğu anlamına gelir özel veri toplama yönetim çözümüne toocreate bir [Azure Automation runbook](../automation/automation-runbook-types.md) , gerekli hello Azure ya da dış kaynaklardan toplar ve kullandığı veri toplayıcı API toowrite hello toohello depo.  

### <a name="log-searches"></a>Günlük aramalar
[Oturum aramaları](../log-analytics/log-analytics-log-searches.md) kullanılan tooextract olan ve hello günlük analizi deposundaki verileri analiz edin.  Bunlar, görünümler ve ayrıca tooallowing hello kullanıcı tooperform geçici veri analizi hello deposundaki uyarılar tarafından kullanılır.  

Herhangi bir görünüm veya Uyarıları tarafından kullanılmayan olsa bile yararlı toohello kullanıcı olacağını düşündüğünüz herhangi bir sorgu tanımlamanız gerekir.  Bunlar kullanılabilir toothem hello Portalı'nda kayıtlı aramaları olacaktır ve bunları da içerebilir bir [listesini, sorgular görselleştirme bölümü](../log-analytics/log-analytics-view-designer-parts.md#list-of-queries-part) özel görünümünüzde.

### <a name="alerts"></a>Uyarılar
[Günlük analizi uyarılarını](../log-analytics/log-analytics-alerts.md) aracılığıyla sorunları belirlemek [oturum aramaları](#log-searches) hello veri hello deposundaki karşı.  Bunlar hello kullanıcıya bildir ya da otomatik olarak bir eylem yanıt olarak çalıştırın. Uygulamanız için farklı uyarı koşulları tanımlamak ve çözüm dosyanızdaki karşılık gelen uyarı kuralları içerir.

Merhaba sorun büyük olasılıkla otomatik bir işlemle düzeltilebilir, ardından, genellikle bir runbook'un Azure Otomasyon tooperform bu düzeltme oluşturacaksınız.  Çoğu Azure Hizmetleri ile yönetilebilir [cmdlet'leri](/powershell/azure/overview) hangi hello runbook tooperform bu tür işlevselliği yararlanan.

Çözümünüzü yanıt tooan uyarı dış işlevler gerektirir sonra kullanabileceğiniz bir [Web kancası yanıt](../log-analytics/log-analytics-alerts-actions.md).  Bu, toocall hello uyarıdan bilgi gönderirken bir dış web hizmeti sağlar.

### <a name="views"></a>Görünümler
Günlük analizi görünümlerde hello günlük analizi depodan kullanılan toovisualize verilerdir.  Her çözüm genellikle tek bir görünümle içerecek bir [döşeme](../log-analytics/log-analytics-view-designer-tiles.md) hello kullanıcının ana panosunda görüntülenir.  Merhaba görünümü, herhangi bir sayıda içerebilir [görselleştirme bölümleri](../log-analytics/log-analytics-view-designer-parts.md) tooprovide farklı görselleştirmesini hello toplanan verileri toohello kullanıcı.

[Hello Görünüm Tasarımcısı kullanarak özel görünümlerini oluşturma](../log-analytics/log-analytics-view-designer.md) , daha sonra çözüm dosyanızda için içerme dışarı aktarabilirsiniz.  


## <a name="create-solution-file"></a>Çözüm dosyası oluşturma
Yapılandırılmış ve test çözümünüzü parçası olacak hello bileşenleri sonra [çözüm dosyanızı oluşturun](operations-management-suite-solutions-solution-file.md).  Merhaba çözüm bileşenlerinde uygulayacak bir [Resource Manager şablonu](../azure-resource-manager/resource-group-authoring-templates.md) içeren bir [çözüm kaynak](operations-management-suite-solutions-solution-file.md#solution-resource) ilişkileri toohello ile diğer kaynaklar dosya hello.  


## <a name="test-your-solution"></a>Çözümünüzü
Çözümünüzü geliştirirken tooinstall gerekir ve çalışma alanınızda test.  Merhaba kullanılabilir yöntemlerin herhangi biriyle çok kullanarak bunu yapabilirsiniz[test ve Resource Manager şablonları yükleme](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="publish-your-solution"></a>Çözümünüzü yayımlama
Tamamlandı ve çözümünüzü test sonra aşağıdaki kaynaklar ya da hello aracılığıyla kullanılabilir toocustomers yapabilirsiniz.

- **Azure hızlı başlangıç şablonları**.  [Azure hızlı başlangıç şablonları](https://azure.microsoft.com/resources/templates/) GitHub aracılığıyla hello topluluk katkıda bulunan Resource Manager şablonları kümesidir.  Çözümünüzü kullanılabilir hello aşağıdaki bilgileri tarafından yapabileceğiniz [katkı Kılavuzu](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE).
- **Azure Market**.  Merhaba [Azure Marketi](https://azuremarketplace.microsoft.com/marketplace/) toodistribute sağlar ve tooother geliştiriciler, ISV, çözümünüzü satmak ve BT uzmanları.  Bilgi edinebilirsiniz nasıl toopublish, çözüm tooAzure Market adresindeki [nasıl toopublish ve bir teklif hello Azure Marketi yönetmek](../marketplace-publishing/marketplace-publishing-getting-started.md).



## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[bir çözüm dosyası oluşturma](operations-management-suite-solutions-solution-file.md) Yönetimi çözümünüz için.
* Merhaba ayrıntılarını öğrenmek [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).
* Arama [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates) farklı Resource Manager şablonları örneklerini için.