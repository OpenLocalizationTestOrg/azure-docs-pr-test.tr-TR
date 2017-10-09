---
title: aaaIntegrating Operations Management Suite (OMS) | Microsoft Docs
description: "Ayrıca toousing Merhaba OMS standart özelliklerini, onu diğer yönetim uygulamaları ve Hizmetleri tooprovide ile karma yönetim ortamı, tooprovide özel yönetim senaryoları benzersiz tooyour ortamı veya tooprovide özel tümleştirebilirsiniz Müşterileriniz için yönetim deneyimi.  Bu makalede farklı seçeneklerinizi OMS ile tümleştirmek için genel bir bakış sağlar ve ayrıntılı teknik bilgi sağlama tooarticles bağlar."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: fc5f3a8a-77f7-4103-bd7e-744c15ffcca7
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: dce752dcdc6c725bbafd49db4a5055750487ecf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-with-operations-management-suite-oms"></a>Operations Management Suite (OMS) ile tümleştirme
Operations Management Suite, yönetmek ve şirket içi korumak ve altyapı bulut yardımcı olan Microsoft'un bulut tabanlı BT yönetimi çözümüdür.  Ayrıca toousing Merhaba OMS standart özelliklerini, onu diğer yönetim uygulamaları ve Hizmetleri tooprovide ile karma yönetim ortamı, tooprovide özel yönetim senaryoları benzersiz tooyour ortamı veya tooprovide özel tümleştirebilirsiniz Müşterileriniz için yönetim deneyimi.  Bu makale, farklı seçeneklerinizi OMS ile tümleştirmek için genel bir bakış Hizmetleri ve ayrıntılı teknik bilgi sağlama tooarticles bağlantılar sağlar. 

## <a name="log-analytics"></a>Log Analytics
Günlük analizi tarafından toplanan yönetim verilerini Azure üzerinde barındırılan bir havuzda depolanır.  Merhaba deposunda depolanan tüm verileri son derece büyük miktarlarda verinin hızlı analiz sağlayan günlük aramaları mevcut değil.  Tümleştirme gereksinimlerinizi toopopulate hello deposuyla yeni veri analizi için kullanılabilir hale getirme ya da hello depo tooprovide yeni bir görsel öğe tooextract verileri veya başka bir yönetim aracı ile toointegrate olabilir.

Her veri hello deposundaki parçasının bir kayıt olarak depolanır.  Merhaba deposu doldurmak, kullanıcıların çözümünüzü kullanan hello kayıt türü ve bir açıklama ve özelliklerini sağlamalıdır.  Verileri almak için bu bilgileri hello verileri ile çalışma hakkında gerekir.

![Merhaba OMS deposu doldurma](media/operations-management-suite-integration/repository.png)

### <a name="populate-hello-log-analytics-repository"></a>Merhaba günlük analizi deposu doldurma
Merhaba OMS deposu doldurmak için birden çok yöntem bulunmaktadır.  Merhaba kullandığınız yöntemi hello kaynak verilerin bulunduğu, hello veri ve hangi hello biçimi gibi etkenlere bağlıdır istemcileri toosupport gerekir.  Veri hello deposunda depolandıktan sonra nasıl toplanan fark etmez.

Merhaba aşağıdaki bölümlerde hello OMS deposu doldurmak için hello farklı seçenekler açıklanmaktadır.

#### <a name="connected-sources-and-data-sources"></a>Bağlı kaynakları ve veri kaynakları
Bağlı kaynakları burada veri hello OMS depo için alınabilecek şekilde hello yerlerdir.  Veri kaynakları ve çözümleri bağlı kaynakları çalıştırın ve toplanan hello belirli veri tanımlayın.  Uygulamanızın veri tooone, bu veri kaynaklarının yazıyorsa sonra onu hello veri kaynağı yapılandırarak toplayabilirsiniz.  Syslog olayları, uygulamanızın oluşturduğu, örneğin, ardından bunlar hello Syslog veri kaynağı tarafından Linux Aracısı'nı toplanabilir.

* [Günlük analizi veri kaynaklarında](../log-analytics/log-analytics-data-sources.md)

#### <a name="solutions"></a>Çözümler
Çözümleri OMS hello yeteneklerini genişletir.  Bir çözüm hello bağlı kaynaktan veri toplayabilir veya hello deposunda toplanmış kayıtlar üzerinde analiz gerçekleştirebilir.  Microsoft tarafından sağlanan her bir çözüm topladığı hello veri hello Ayrıntılar sağlayan tek tek makale sahiptir.

* [Günlük analizi çözümleri](../log-analytics/log-analytics-add-solutions.md)

#### <a name="http-data-collector-api"></a>HTTP veri toplayıcı API
Merhaba günlük analizi HTTP veri toplayıcı API tooadd JSON veri toohello günlük analizi deposu sağlayan bir REST API'dır.  Merhaba biri aracılığıyla verileri diğer veri kaynakları veya çözümleri sağlamıyorsa bir uygulamanız varsa, bu API'yı kullanabilir.  Kullanılan toopopulate hello hello API çağırabilir ve herhangi bir veri kaynağı veya çözüm hello koleksiyonu zamanlamaya göre kalmaz herhangi bir istemciyi depodan olabilir.

* [Günlük analizi HTTP veri toplayıcı API](../log-analytics/log-analytics-data-collector-api.md)

### <a name="retrieve-data-from-hello-log-analytics-repository"></a>Merhaba günlük analizi depodan veri alma
Merhaba OMS depodan veri almak için birden çok yöntem bulunmaktadır.  Merhaba OMS konsolunu kullanarak kullanıcıları tooretrieve veri istediğiniz ve farklı türdeki görselleştirmeleri ve analiz verin.  Başka bir yönetim çözümü gibi bir dış işleminden hello verileri de alabilirsiniz.

#### <a name="log-searches"></a>Günlük aramalar
Günlük arar Hello OMS deposunda depolanan tüm verileri kullanılabilir.  Kullanıcılar kendi geçici analiz hello OMS konsolundaki gerçekleştirme veya belirli günlük arama için bir görsel öğe içeren bir pano oluşturun.  Çözümleri, önceden tanımlanmış aramaları dayalı görselleştirmelerle özel görünümler içerebilir.  Merhaba günlük arama API tooaccess veri hello OMS depodan bir dış uygulama veya yönetim aracını kullanabilirsiniz.  

* [Günlük analizi günlük aramalarda](../log-analytics/log-analytics-log-searches.md)
* [Günlük analizi günlük arama REST API'si](../log-analytics/log-analytics-log-search-api.md)
* [Günlük analizi cmdlet'leri](https://msdn.microsoft.com/library/mt188224.aspx)

#### <a name="custom-views"></a>Özel görünümler
Merhaba Görünüm Tasarımcısı kullanıcılar Görselleştirme ve çözümünüzdeki hello veri analizini sağlayan toocreate özel görünümler hello OMS konsolunda sağlar.  Her görünüm hello konsol ve tanımladığınız günlük aramaları temel görselleştirme bölümleri herhangi bir sayıda hello ana sayfada görüntülenen bir kutucuğu içerir.

* [Günlük analizi Görünüm Tasarımcısı](../log-analytics/log-analytics-view-designer.md)

#### <a name="power-bi"></a>Power BI
Görselleştirmeleri ve çözümleme araçları yararlanabilirsiniz şekilde günlük analizi otomatik olarak veri hello OMS depodan Power BI'a aktarabilirsiniz.  Merhaba verileri toodate Tutuluyor şekilde bir zamanlamaya göre bu verme işlemi gerçekleştirir. 

* [Günlük analizi veri tooPower BI dışarı aktarma](../log-analytics/log-analytics-powerbi.md)

## <a name="automation"></a>Otomasyon
OMS işlemleri tooreact toocollected veri veya tooperform diğer yönetim işlevlerini otomatik hale getirebilirsiniz.  Uygulamanızdan veri toplamak ve hello OMS depoya ekleyin ya da hello deposunda bulunan yanıt toodata içinde bilinen bir sorundur hello düzeltilmesi otomatikleştirebilir. 

![Otomasyon](media/operations-management-suite-integration/automate.png)

### <a name="runbooks"></a>Runbook'lar
Azure Otomasyonu runbook'ları, PowerShell komut dosyaları ve iş akışları hello Azure bulut çalıştırın.  Bunları azure'da toomanage kaynakları veya yalnızca hello buluttan erişilebilen diğer kaynakları kullanabilirsiniz.  Runbook'ları karma Runbook çalışanı kullanarak bir yerel veri merkezinde da çalıştırılabilir.  Hello Azure portalı veya dış işlemlere çok sayıda PowerShell gibi yöntemleri kullanarak bir runbook başlatın ya da Otomasyon API hello.

* [Azure Otomasyonu runbook başlatma](../automation/automation-starting-a-runbook.md)
* [Azure Automation cmdlet'leri](https://msdn.microsoft.com/library/dn690262.aspx)
* [Otomasyon REST API'si](https://msdn.microsoft.com/library/mt662285.aspx)
* [Otomasyon .NET](https://msdn.microsoft.com//library/mt465763.aspx)

### <a name="alerts"></a>Uyarılar
Uyarı kuralları otomatik olarak günlük aramaları tooa zamanlamaya göre çalıştır.  Merhaba sonuçları belirli eşleşiyorsa ölçütleri hello ortaya çıkan uyarı Azure Otomasyonu'nda bir runbook başlatın veya bir dış işlem başlatmak için bir Web kancası çağırın.  Bu yanıtları her ikisi de hello günlük arama sonucu hello verileri dahil olmak üzere hello uyarı ayrıntılarını içerebilir.

* [Günlük analizi uyarıları](../log-analytics/log-analytics-alerts.md)
* [Günlük analizi uyarı API](../log-analytics/log-analytics-api-alerts.md)

## <a name="backup-and-site-recovery"></a>Yedekleme ve Site kurtarma
Azure yedekleme ve Site Recovery, kurumsal veri koruma ve sunucuları ve uygulamaları hello kullanılabilir olmasını sağlamaya yönelik hizmetler sağlar.  Uygulamanız için yedekleme hizmetleri sağlamak veya bir sanal makinenin yük devretmeyi başlatmadan olarak bu senaryolara bu hizmetleri tooperform yararlanabilirsiniz.

* [Azure yedekleme cmdlet'lerini](https://msdn.microsoft.com/library/mt619253.aspx)
* [Azure Site Recovery REST API'si](https://msdn.microsoft.com/library/azure/mt750497.aspx)
* [Azure Site kurtarma cmdlet'leri](https://msdn.microsoft.com/library/mt637930.aspx)

## <a name="custom-solutions"></a>Özel çözümler
Çalışma alanınızdaki ya da Müşteri'nin çalışma alanında bir özel çözüm toorun tümleştirme mantığı yerleştirebilirsiniz.  Çözümünüzü hello tümleştirme yöntemlerden herhangi birini toplama tooother kaynakları tooprovide bu makaledeki tam Yönetimi senaryosu içerebilir.  sağlayacak şekilde Hello çözüm kaldırıldığında, oluşturulduğu hello kaynakların tümünü hello OMS çalışma ve Azure abonelik kaldırılır hello çözüm hello kaynaklarında paketlenir.

Örneğin, çözümünüzün bir Otomasyon runbook toogather ve işlem verileri içerir ve hello HTTP veri toplayıcı API kullanarak hello günlük analizi deposu doldurmak.  Gösterir ve hello toplanan verileri çözümler özel bir görünümü de içerebilir.  

* (Yakında) özel çözümler oluşturma    

## <a name="next-steps"></a>Sonraki adımlar
* Başvuru hello [OMS SDK](operations-management-suite-sdk.md) OMS Hizmetleri otomatikleştirme hakkında teknik bilgi için.  

