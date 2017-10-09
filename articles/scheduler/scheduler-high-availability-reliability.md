---
title: "aaaScheduler yüksek kullanılabilirlik ve güvenilirlik"
description: "Yüksek Scheduler kullanılabilirliği ve güvenilirliği"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5ec78e60-a9b9-405a-91a8-f010f3872d50
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2016
ms.author: deli
ms.openlocfilehash: 5c9efb333eb42b393adc5deea657ca99206d425e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-high-availability-and-reliability"></a>Yüksek Scheduler kullanılabilirliği ve güvenilirliği
## <a name="azure-scheduler-high-availability"></a>Yüksek Azure Scheduler kullanılabilirliği
Çekirdek Azure platformu hizmet olarak Azure Scheduler yüksek oranda kullanılabilir ve coğrafi olarak yedekli hizmet dağıtımı ve coğrafi bölge iş çoğaltma özellikleri.

### <a name="geo-redundant-service-deployment"></a>Coğrafi olarak yedekli hizmet dağıtımı
Azure Zamanlayıcı hello Azure'da bugün olduğu neredeyse her coğrafi bölgede kullanıcı Arabirimi aracılığıyla kullanılabilir. Azure Scheduler bulunan bölgelere Hello listesidir [burada listelenen](https://azure.microsoft.com/regions/#services). Bir veri merkezi barındırılan bir bölgede kullanılamıyor işlenen hello hizmet başka bir veri merkezinden kullanılabilir olacak şekilde, Azure Scheduler hello yük devretme özelliklerini demektir.

### <a name="geo-regional-job-replication"></a>Coğrafi bölge iş çoğaltma
Yalnızca olan Azure Scheduler ancak kendi iş yönetim istekleri için de coğrafi olarak çoğaltılmış kullanılabilir ön uç hello. Bir bölgede bir kesinti olduğunda Azure Scheduler yöneltilir ve o hello işi hello eşleştirilmiş coğrafi bölgede başka bir veri merkezi çalıştırıldığı sağlar.

Örneğin, bir iş Orta Güney ABD içinde oluşturduysanız, Azure Scheduler Kuzey Orta ABD o işe otomatik olarak çoğaltır. Olduğunda hata Orta Güney ABD içinde Azure Scheduler Kuzey merkezi Bizden bu hello işini çalıştır sağlar. 

![][1]

Sonuç olarak, Azure Scheduler, veri kalır içinde daha geniş aynı coğrafi bölgede bir Azure hatası durumunda hello sağlar. Sonuç olarak, iş yalnızca tooadd yüksek kullanılabilirlik yinelenen olmayan – Azure Scheduler otomatik olarak işleriniz için yüksek kullanılabilirlik yetenekleri sağlar.

## <a name="azure-scheduler-reliability"></a>Azure Zamanlayıcı güvenilirlik
Azure Zamanlayıcı kendi yüksek oranda kullanılabilirlik garanti eder ve farklı bir yaklaşım toouser oluşturulan işler alır. Örneğin, işinizi kullanılamaz bir HTTP uç noktası çağırabilir. Azure Zamanlayıcı yine de tooexecute işinizi başarılı bir şekilde, diğer seçenekleri toodeal başarısızlıkla vererek çalışır. Azure Scheduler bunu iki şekilde yapar:

### <a name="configurable-retry-policy-via-retrypolicy"></a>"RetryPolicy" aracılığıyla yapılandırılabilir yeniden deneme ilkesi
Azure Zamanlayıcı tooconfigure bir yeniden deneme ilkesi sağlar. Bir işi başarısız olursa, varsayılan olarak 30 saniyelik aralıklarda yeniden dört kez daha, hello iş Zamanlayıcı dener. Bu yeniden deneme ilkesi toobe daha agresif (örneğin, on kez 30 saniyelik aralıklarda) yeniden yapılandırabilir veya ok (örneğin, iki kez günlük aralıklarla.)

Ne zaman bu yardımcı olabilecek örnek olarak, haftada bir kez çalıştırır ve bir HTTP uç noktası çağıran bir iş oluşturabilirsiniz. Merhaba HTTP uç noktası kapalı birkaç saat işiniz çalıştırıldığında ise, bu yana bile hello varsayılan yeniden deneme ilkesi başarısız olur, toowait daha fazla için bir hafta hello iş toorun yeniden istemeyebilirsiniz. Böyle durumlarda, hello standart yeniden deneme ilkesi tooretry üç saatte (örneğin) yerine her 30 saniyede yapılandırabilir.

tooconfigure bir yeniden deneme ilkesi başvurmak çok nasıl toolearn[retryPolicy](scheduler-concepts-terms.md#retrypolicy).

### <a name="alternate-endpoint-configurability-via-erroraction"></a>"ErrorAction" yoluyla diğer uç nokta yapılandırılabilirlik
Azure Scheduler işi için Hello hedef uç noktaya erişilemiyor kalırsa, Azure Scheduler, yeniden deneme ilkesi izledikten sonra toohello alternatif hata işleme uç noktasını geri döner. Alternatif bir hata işleme uç noktasını yapılandırdıysanız, Azure Scheduler bunu çağırır. Başka bir uç nokta ile kendi işleri hatanın hello karşılaştıkları yüksek oranda kullanılabilir.

Örneğin, aşağıdaki hello diyagramındaki kendi yeniden deneme ilkesi toohit New York web hizmeti Azure Scheduler izler. Hello başarısız denemeden sonra alternatif olup olmadığını denetler. Sonra ilerler ve toohello alternatif hello ile aynı istekleri yapan başlatır yeniden deneme ilkesi.

![][2]

Aynı yeniden deneme ilkesi hello Not tooboth hello özgün eylem ve hello alternatif hata eylemi uygular. Ayrıca olası toohave hello alternatif hata eylemin eylem türü hello ana eylemin eylem türünden farklı. Örneğin, Hello ana eylemi bir HTTP uç noktası çağırma, ancak hello hata eylemi bunun yerine bir depolama kuyruğu, hizmet veri yolu kuyruğu ya da hata günlüğünü olmadığından hizmet veri yolu konusu eylemi olabilir.

tooconfigure alternatif bir uç nokta başvurmak çok nasıl toolearn[errorAction](scheduler-concepts-terms.md#action-and-erroraction).

## <a name="see-also"></a>Ayrıca Bkz.
 [Scheduler nedir?](scheduler-intro.md)

 [Azure Scheduler kavramları, terminolojisi ve varlık hiyerarşisi](scheduler-concepts-terms.md)

 [Zamanlayıcı hello Azure portalını kullanmaya başlama](scheduler-get-started-portal.md)

 [Azure Scheduler’da planlar ve faturalama](scheduler-plans-billing.md)

 [Nasıl toobuild karmaşık zamanlar ve Gelişmiş yineleme Azure Scheduler ile](scheduler-advanced-complexity.md)

 [Azure Scheduler REST API başvurusu](https://msdn.microsoft.com/library/mt629143)

 [Azure Scheduler PowerShell cmdlet’leri başvurusu](scheduler-powershell-reference.md)

 [Azure Scheduler sınırları, varsayılanları ve hata kodları](scheduler-limits-defaults-errors.md)

 [Azure Scheduler giden bağlantı kimlik doğrulaması](scheduler-outbound-authentication.md)

[1]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image1.png

[2]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image2.png
