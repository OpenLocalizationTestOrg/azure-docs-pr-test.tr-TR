---
title: "aaaFault çözümleme hizmetine genel bakış | Microsoft Docs"
description: "Bu makalede hello hataya Analysis Service Fabric hizmetinde hataları inducing ve test senaryoları hizmetlerinizi karşı çalıştırmak için açıklanmaktadır."
services: service-fabric
documentationcenter: .net
author: anmolah
manager: timlt
editor: vturecek
ms.assetid: 1f064276-293a-4989-a513-e0d0b9fdf703
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: anmola
ms.openlocfilehash: deac16ec830aa10d4e488e60691faa9ef2b6cd33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-fault-analysis-service"></a>Giriş toohello hata analizi hizmeti
Merhaba hata analizi hizmeti Microsoft Azure Service Fabric üzerinde oluşturulmuş Hizmetleri test etmek için tasarlanmıştır. Merhaba hata analizi hizmeti ile anlamlı hataları anlamına ve uygulamalarınızı karşı tam test senaryoları çalıştırın. Bu hataları ve senaryoları uygulamanız ve doğrulama çok sayıda durumları ve hizmet yaşam süresi boyunca, tüm bir denetimli, güvenli ve tutarlı şekilde yaşar geçişleri hello.

Eylemler, bunu test etmek için bir hizmet hedefleme hello tek tek hatalarıdır. Bir hizmet Geliştirici yapı taşları toowrite karmaşık senaryolar olarak kullanabilirsiniz. Örneğin:

* Bir düğüm toosimulate olduğu bir makineye veya VM yeniden durumlarda herhangi bir sayıda yeniden başlatın.
* Bir çoğaltma, durum bilgisi olan hizmet toosimulate Yük Dengeleme, yük devretme veya uygulama yükseltme taşıyın.
* Çekirdek kayıp durum bilgisi olan hizmet toocreate yeterli "yedek" veya "ikincil" çoğaltmaları tooaccept yeni veri olmadığından burada yazma işlemleri devam edemiyor bir durum olarak çağırır.
* Durum bilgisi olan hizmet toocreate burada tüm bellek içi durumu tamamen silinmeden çıkışı bir durum veri kaybı çağırır.

Bir veya daha fazla eylemlerini oluşan karmaşık işlemleri senaryolar verilmiştir. Hello hata analizi hizmeti, iki yerleşik tam senaryoları sağlar:

* Chaos senaryosu
* Yük devretme senaryosu

## <a name="testing-as-a-service"></a>Bir hizmet olarak test etme
Merhaba hata analizi hizmeti ile bir Service Fabric kümesi otomatik olarak başlatılan bir Service Fabric sistem hizmetidir. Bu hizmet hata ekleme, test senaryosu yürütme ve durum Analizi'ni hello ana bilgisayar olarak görev yapar. 

![Hata analizi hizmeti][0]

Bir hata eylemi veya test senaryosu başlatıldığında, bir komut eylemini veya sınama toohello hata Analiz Hizmetleri toorun hello hataya senaryosu gönderilir. Merhaba hata analizi hizmeti durum bilgisi olan, böylelikle, güvenilir bir şekilde hataları ve senaryoları çalıştırabilir ve sonuçlarını doğrulayın. Örneğin, bir uzun süre çalışan testi senaryosu güvenilir bir şekilde hello hata analizi hizmeti tarafından çalıştırılabilir. Ve testleri hello kümesi içinde yürütülmekte çünkü hello hizmet hello kümenin hello durumunu ve Hizmetleri tooprovide hataları hakkında daha ayrıntılı bilgi inceleyebilirsiniz.

## <a name="testing-distributed-systems"></a>Dağıtılmış sistemlerin test etme
Service Fabric yazma ve dağıtılmış ölçeklenebilir uygulamalar önemli ölçüde daha kolay yönetme hello işi yapar. benzer şekilde daha kolay bir dağıtılmış uygulamayı test Hello hata analizi hizmeti sağlar. Test ederken Çözüldü toobe gereken üç ana sorunlar vardır:

1. Gerçek dünya senaryolarında oluşabilecek hatalar benzetimi/oluşturuluyor:, Service Fabric hello önemli yönlerinden biri dağıtılmış uygulamalar toorecover çeşitli hatalardan sağlar. Ancak, uygulama hello tootest Bu hatalardan mümkün toorecover, bir mekanizma toosimulate/oluşturmak Bu gerçek hataları denetimli test ortamında ihtiyacımız.
2. Merhaba özelliği toogenerate bağıntılı hataları: temel ağ hataları ve makine hataları gibi hello sisteminde hatalarıdır kolay tooproduce ayrı ayrı. Çok sayıda hello gerçek dünyadaki hello etkileşimleri bu tek tek başarısızlık nedeniyle oluşabilir senaryolar oluşturma Önemsiz olmayan.
3. Geliştirme ve dağıtım çeşitli düzeylerde arasında birleşik deneyim: hataları çeşitli türlerde yapabilmeniz için birçok hata ekleme sistemi vardır. Bir çalıştırma Geliştirici senaryolarını, büyük test ortamlarında toousing kendileri için aynı sınamaları toorunning hello taşıma üretimde test ancak, bunların tümü hello deneyimi zayıf durumdur.

Bu sorunları aynı gerekli garanti--bir kutusunu Geliştirici ortamından tüm hello yolu ile Merhaba bir sistem birçok mekanizmaları toosolve varken üretim kümeleri--tootest eksik. Merhaba hata analizi hizmeti hello uygulama geliştiricileri kendi iş mantığı sınama odaklanmasına yardımcı olur. Merhaba olanaklarına hello hizmet hello temel Dağıtılmış Sistem tootest hello etkileşimi gerekli Hello hata analizi hizmeti sağlar.

### <a name="simulatinggenerating-real-world-failure-scenarios"></a>Gerçek dünya hatası senaryoları benzetimini yapma ve oluşturma
tootest hello sağlamlık hatalarına karşı dağıtılmış bir sistemin bir mekanizma toogenerate hataları gerekir. Kuramsal karşın, bir düğüm aşağı hello basarsa başlatır kolay görünüyor gibi bir hata oluşturma aynı tutarlılık sorunları Service Fabric toosolve çalışıyor olarak ayarlayın. Bir düğüm aşağı tooshut istiyoruz, örnek olarak, hello iş akışı hello aşağıdaki gereklidir:

1. Merhaba istemciden kapatma düğümü isteği gönderin.
2. Merhaba isteği toohello doğru düğümü gönderin.
   
    a. Merhaba düğümü bulunamadı, başarısız olması.
   
    b. Merhaba düğümü bulunursa, yalnızca hello düğüm kapatma durumunda döndürmelidir.

tooverify hello hatası test açısından hello test tooknow bu hatayı kopyaladığınızda, hello hatası gerçekte gerçekleşmesi gerekir. Service Fabric sağlar hello garanti hello düğümlerden gidecek veya hello komutu hello düğümü erişildiğinde zaten oldu sağlar. Büyük/küçük harf ya da hello test mümkün toocorrectly neden hello durumu hakkında ve başarılı veya doğru şekilde kendi doğrulama başarısız. Service Fabric toodo hello dışında uygulanan bir sistem, birçok ağ isabet, donanım ve vermesini önleyen yazılım konuları, önceki garanti hello aynı hatalarının ayarlayın. Service Fabric hello küme durumu toowork hello sorunları geçici yeniden yapılandırın ve bu nedenle hata analizi hizmeti hello önce belirtilen hello sorunları Hello bulunması garanti hala mümkün toogive hello sağ ayarlanır.

### <a name="generating-required-events-and-scenarios"></a>Gerekli olayları ve senaryolar oluşturma
Gerçek dünya kesintisi tutarlı bir şekilde benzetimi ile zorlu toostart olsa da, hello özelliği bağıntılı toogenerate hataları bile tougher. Örneğin, şeyler aşağıdaki hello gerçekleştiğinde bir veri kaybı bir durum bilgisi olan kalıcı hizmetinde olur:

1. Yalnızca bir yazma çekirdek hello çoğaltmalarının yakalandı çoğaltma. Tüm hello ikincil çoğaltmaları birincil hello öteleme.
2. (son tooa kod paketi veya gitme düğüm) giderek hello çoğaltmaları nedeniyle Hello yazma çekirdek arıza.
3. Merhaba çoğaltmaları Hello verileri (toodisk Bozulması veya makine yeniden görüntüsünü oluşturuyor) kayıp olduğundan hello yazma çekirdek geri gelmesi olamaz.

Bu bağlantılı hataları hello gerçek dünyadaki ancak değil olarak tek tek hataları sıklıkta gerçekleşir. Merhaba özelliği tootest üretimde gerçekleşmeden önce bu senaryoları için önemlidir. Daha da hello özelliği toosimulate denetimli durumlarda üretim iş yükleri ile bu senaryoları (deste üzerindeki tüm mühendisleri ile Merhaba günün hello ortasında) önemlidir. Bunu Merhaba üretim saat 2: 00'da ilk kez gerçekleşecek olması daha iyi

### <a name="unified-experience-across-different-environments"></a>Farklı ortamlar üzerinde birleşik deneyim
Merhaba uygulama geleneksel toocreate üç farklı kümesi deneyimleri, biri hello geliştirme ortamı için testleri için ve bir üretim için bırakıldı. was Hello modeli:

1. Birim testleri tek tek yöntemlerin izin durumu geçişleri Hello geliştirme ortamında üretir.
2. Merhaba test ortamında, çeşitli hatası senaryoları çalışma hataları tooallow uçtan uca testleri üretir.
3. Doğal olmayan hataları ve son derece hızlı İnsan yanıt toofailure olduğunu tooensure Hello üretim ortamı pristine tooprevent tutun.

Service Fabric içinde hello hata analizi hizmeti biz tooturn bu sorunu önerdiği ve kullanım hello aynı Geliştirici ortamı tooproduction gelen Metodoloji. Vardır iki yolu tooachieve bu:

1. Denetlenen tooinduce hataları, tüm hello yolu tooproduction hello hata analizi hizmeti API'leri bir Kutulu Ortamı'ndan kullanmak kümeleri.
2. toogive hello hatalar, kullanım hello hata analizi hizmeti toogenerate otomatik endüksiyon otomatik hatalarına neden oluyor fever küme. Yapılandırma yoluyla hata denetleme hello oranı aynı hizmet toobe farklı farklı ortamlarda test hello sağlar.

Hataları Hello ölçeğini hello farklı ortamlarda farklı olabilir ancak Service Fabric ile Merhaba gerçek mekanizmaları aynı olacaktır. Bu bir çok daha hızlı kod dağıtım ardışık düzen ve hello özelliği tootest hello hizmetler gerçek yükleri sağlar.

## <a name="using-hello-fault-analysis-service"></a>Merhaba hata analizi hizmeti kullanma
**C#**

Hata analizi hizmeti hello System.Fabric ad alanındaki hello Microsoft.ServiceFabric NuGet paketi özellikleridir. toouse hello hata analizi hizmeti özellikleri projenize başvuru olarak hello nuget paketini içerir.

**PowerShell**

PowerShell toouse hello Service Fabric SDK yüklemeniz gerekir. Merhaba ServiceFabric PowerShell hello sonra SDK yüklü olduğu, toouse yüklenen otomatik modülüdür.

## <a name="next-steps"></a>Sonraki adımlar
toocreate gerçekten bulut ölçekli hizmetler, bu kritik tooensure hem önce ve Hizmetleri gerçek dünya hataları dayanabilir dağıtımdan sonra olur. Merhaba Hizmetleri dünyada bugün özelliği tooinnovate hızlı bir şekilde hello ve taşıma kod tooproduction hızlı bir şekilde de çok önemlidir. Merhaba hataya Analysis Services hizmet geliştiricileri toodo tam olarak, yardımcı olur.

Uygulamaları ve Hizmetleri hello yerleşik kullanarak test başlamadan [testi senaryolarında](service-fabric-testability-scenarios.md), veya hello kullanarak kendi test senaryoları Yazar [arıza Eylemler](service-fabric-testability-actions.md) hello hata analizi hizmeti tarafından sağlanan.

<!--Image references-->
[0]: ./media/service-fabric-testability-overview/faultanalysisservice.png
