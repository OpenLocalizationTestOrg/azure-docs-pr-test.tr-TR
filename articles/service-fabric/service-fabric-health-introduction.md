---
title: Service Fabric aaaHealth izleme | Microsoft Docs
description: "Merhaba küme ve uygulamaları ve Hizmetleri izlemeyi sağlayan modeli, bir giriş toohello Azure Service Fabric sistem durumu izleme."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 1d979210-b1eb-4022-be24-799fd9d8e003
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: oanapl
ms.openlocfilehash: 904f36374ca6ca7e4caa1d43c92584e7e4c50087
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooservice-fabric-health-monitoring"></a>Giriş tooService doku sistem durumu izleme
Azure Service Fabric zengin, esnek ve Genişletilebilir sistem durumu değerlendirmesi ve raporlama sağlar bir sistem durumu modeli sunar. Merhaba modeli hello durumunu hello küme içinde çalışan ve hello hizmetler yakın gerçek zamanlı izlenmesini sağlar. Kolayca sistem durumu bilgilerini almak ve düzeltmek olası sorunlar basamaklı ve yoğun kesintileri neden önce. Merhaba tipik modelinde, kendi yerel görünümleri dayalı raporlar Hizmetleri göndermek ve bilgileri tooprovide bir küme düzeyi genel görünümü bir araya getirilir.

Service Fabric bileşenleri bu zengin sistem durumu modeli tooreport geçerli durumlarına kullanın. Kullanabileceğiniz Merhaba, uygulamalardan aynı mekanizması tooreport sistem durumu. Yüksek kaliteli sistem durumu, özel koşullarınızı yakalayan raporlamada yatırım algılamak ve çalışan uygulamanız için daha kolay düzeltin.

Merhaba, aşağıdaki Microsoft Virtual Academy video ayrıca hello Service Fabric sistem durumu modeli ve nasıl kullanıldığı açıklanmaktadır:<center><a target="_blank" href="https://mva.microsoft.com/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tevZw56yC_1906218965">
<img src="./media/service-fabric-health-introduction/HealthIntroVid.png" WIDTH="360" HEIGHT="244">
</a></center>

> [!NOTE]
> Biz hello sistem durumu alt sistemi tooaddress izlenen yükseltmeler gereksinimini başlatıldı. Service Fabric tam kullanılabilirlik, kapalı kalma süresi ve en az toono kullanıcı müdahalesi olun izlenen uygulama ve Küme yükseltme sağlar. Bu hedefleri hello yükseltme denetler temel sistem durumu tooachieve yükseltme İlkesi yapılandırdığınızı düşünün. Yalnızca sistem durumu istediğiniz eşikleri dikkate alır, bir yükseltme devam edebilirsiniz. Aksi takdirde hello yükseltme ya da otomatik olarak geri alındı veya toogive Yöneticiler bir fırsat toofix hello sorunları duraklatıldı. Uygulama yükseltme hakkında daha fazla toolearn bkz [bu makalede](service-fabric-application-upgrade.md).
> 
> 

## <a name="health-store"></a>Sistem durumu deposu
Merhaba sistem durumu deposu durumuyla ilgili bilgi varlıkları hakkındaki kolay alma ve değerlendirme için hello kümedeki tutar. Durum bilgisi olan hizmet tooensure yüksek kullanılabilirlik ve ölçeklenebilirlik Service Fabric kalıcı olarak uygulanır. Merhaba sistem durumu hello parçası deposudur **fabric: / Sistem** uygulama ve hello kümenin çalışır durumda olduğunda kullanılabilir ve çalışır.

## <a name="health-entities-and-hierarchy"></a>Sistem durumu varlıkları ve hiyerarşisi
Merhaba sistem durumu varlıkları etkileşimleri ve farklı varlıklar arasında bağımlılıklar yakalar mantıksal bir hiyerarşide düzenlenir. Merhaba sistem durumu deposu durumu varlıklarını ve hiyerarşi Service Fabric bileşenleri alınan raporları göre otomatik olarak oluşturur.

Merhaba sistem durumu varlıkları hello Service Fabric varlıklar yansıtır. (Örneğin, **sistem durumu uygulama varlığı** uygulama örneğini eşleşen hello kümede dağıtılmışsa, while **sistem durumu düğümünde varlık** eşleşen bir Service Fabric kümesi düğümü.) hello sistem durumu hiyerarşi yakalar Merhaba etkileşimlerinin hello sistem varlıkları ve Gelişmiş Sistem durumu değerlendirmesi hello temelini olur. Anahtar Service Fabric kavramlar hakkında bilgi alabilirsiniz [Service Fabric teknik genel bakış](service-fabric-technical-overview.md). Uygulama hakkında daha fazla bilgi için bkz: [Service Fabric uygulama modeli](service-fabric-application-model.md).

Merhaba durumu varlıklarını ve hiyerarşi etkili bir şekilde bildirilen hata ayıklaması ve izlenen hello küme ve uygulamaları toobe izin verir. Merhaba sistem durumu modeli sağlar doğru bir, *ayrıntılı* hello durumunu gösterimini hello hello kümedeki birçok taşıma parça.

![Sistem durumu varlıkları.][1]
üst-alt ilişkilere dayanan bir hiyerarşideki düzenlenmiş hello sistem durumu varlıkları.

[1]: ./media/service-fabric-health-introduction/servicefabric-health-hierarchy.png

Merhaba sistem durumu varlıkları şunlardır:

* **Küme**. Service Fabric kümesi Hello durumunu temsil eder. Küme sistem durumu raporlarının hello tüm küme etkileyen koşullar açıklanmaktadır. Bu koşulların birden çok varlık hello küme hello kümenin kendisi de etkiler. Merhaba koşula göre hello Raporlayıcı hello sorunu tuşunu tooone ya da daha fazla sağlıksız alt daraltamazsınız. Örnek hello beyin toonetwork bölümleme veya iletişim sorunları bölme hello kümesinin verilebilir.
* **Düğüm**. Service Fabric düğümü Hello durumunu temsil eder. Düğüm durumu raporları hello düğümü işlevselliğini etkileyen koşullar açıklanmaktadır. Bunlar genellikle üzerinde çalışan tüm dağıtılan hello varlıklar etkiler. Örnekler düğüm disk alanı yetersiz (veya diğer makine genelinde özellikleri, bellek, bağlantıları gibi) ve bir düğüm olduğunda kapalı. Merhaba düğümü varlık hello düğüm adı (dize) tarafından tanımlanır.
* **Uygulama**. Merhaba kümede çalışan bir uygulama örneği Hello durumunu temsil eder. Uygulama durumu raporları açıklamak hello etkileyen koşullar hello uygulamanın genel sistem durumu. Bunlar daraltıldığı tooindividual alt (Hizmetleri veya dağıtılan uygulamalar) olamaz. Merhaba uçtan uca etkileşim farklı hizmetler arasında hello uygulamada örnekler. Merhaba uygulama varlığı hello uygulama adı (URI) tarafından tanımlanır.
* **Hizmet**. Merhaba hello kümede çalışan bir hizmetin durumunu temsil eder. Hizmet durumu raporları açıklamak hello etkileyen koşullar hello hizmetinin genel sistem durumu. Merhaba Raporlayıcı hello sorunu tooan sağlıksız bölüm veya çoğaltma aşağı daraltamazsınız. Örnek tüm bölümler için sorunlara neden bir hizmet yapılandırması (örneğin, bağlantı noktası veya dış dosya paylaşımı) verilebilir. Merhaba hizmet varlığı hello hizmet adı (URI) tarafından tanımlanır.
* **Bölüm**. Bir hizmet bölüm Hello durumunu temsil eder. Bölüm sistem durumu raporlarının hello tüm çoğaltma kümesi etkileyen koşullar açıklanmaktadır. Örnek çoğaltmaları hello sayısı hedef sayısı altında olduğunda ve bir bölüm çekirdek kaybında olduğunda verilebilir. Merhaba bölüm varlık hello bölüm kimlik (GUID) tarafından tanımlanır.
* **Çoğaltma**. Bir durum bilgisi olan hizmet çoğaltmayı veya bir durum bilgisiz hizmet örneği Hello durumunu temsil eder. Merhaba çoğaltma watchdogs ve sistem bileşenleri üzerinde bir uygulama için bildirebilir hello küçük birimdir. Durum bilgisi olan hizmetler için operations toosecondaries ve yavaş çoğaltma çoğaltma yapamaz bir birincil çoğaltma örnek verilebilir. Ayrıca, durum bilgisi olmayan bir örnek kaynaklar yetersiz çalışıyor veya bağlantı sorunları bildirebilirsiniz. Merhaba çoğaltma varlığı (uzun) hello bölüm kimlik (GUID) ve hello çoğaltma veya örnek kimliği tarafından tanımlanır.
* **DeployedApplication**. Temsil hello sistem durumunu bir *bir düğüm üzerinde çalışan uygulama*. Dağıtılmış uygulama sistem durumu raporlarının hello üzerinde dağıtılan tooservice paketleri aşağı daraltıldığı olamaz hello düğümde koşullar belirli toohello uygulama açıklamak aynı düğüm. Örnek uygulama paketi bu düğümde yüklendiğinde ve uygulama güvenlik sorumluları hello düğümde ayarlarken sorun hataları verilebilir. dağıtılan hello uygulama, uygulama adı (URI) ve düğüm adı (dize) tarafından tanımlanır.
* **DeployedServicePackage**. Merhaba kümedeki bir düğüm üzerinde çalışan bir hizmet paketi Hello durumunu temsil eder. Merhaba etkilemez koşullar belirli tooa hizmet paketi diğer hizmet paketlerinin üzerinde hello açıkladığı hello için aynı düğümde aynı uygulama. Örnek kod paketi başlatılamıyor hello hizmet paketi ve okunamıyor bir yapılandırma paketi verilebilir. dağıtılan hello hizmet paketi, uygulama adı (URI), düğüm adı (dize), hizmet bildirim adı (dize) ve hizmet paketi etkinleştirme kimliği (dizesi) tarafından tanımlanır.

Merhaba sistem durumu modeli Hello kesinliği kolay toodetect ve doğru sorunları kolaylaştırır. Bir hizmeti yanıt vermiyor, örneğin, uygun olmasına uygulama örneği hello tooreport sağlıksız. Merhaba sorunu bu uygulamadaki tüm hello Hizmetleri etkileyen değil çünkü adresindeki düzeyi ancak ideal, olmadığını raporlama. Daha fazla bilgi toothat bölüm gösteriyorsa hello rapor uygulanan toohello sağlıksız hizmet ya da tooa belirli alt bölüm olması gerekir. Merhaba verileri otomatik olarak hello hiyerarşisi aracılığıyla yüzeyleri ve sağlıksız bir bölüm hale görünür hizmet ve uygulama düzeylerinde. Bu toplama toopinpoint yardımcı olur ve daha hızlı bir şekilde hello kök hello sorunun nedenini çözümleyin.

üst-alt ilişkilerini Hello sistem durumu hiyerarşi oluşur. Bir küme düğümleri ve uygulamaların oluşur. Uygulamaları, hizmetleri ve uygulamaları dağıtılır. Dağıtılmış uygulamalar, hizmet paketleri dağıttım. Hizmetleri bölümleri varsa ve her bölüm bir veya daha fazla çoğaltmalarına sahip. Düğümleri ve dağıtılan varlıklar arasında özel bir ilişki yoktur. Sağlıksız düğüm kendi yetkilisi sistem bileşeni tarafından hello Yük Devretme Yöneticisi hizmeti, bildirilen dağıtılan hello uygulamaları, hizmet paketleri ve çoğaltmalar, üzerinde dağıtılan etkiler.

Merhaba sistem durumu hiyerarşi hello son neredeyse gerçek zamanlı bilgiler hello en son sistem durumu raporlar, temel hello sistem durumunu temsil eder.
İç ve dış watchdogs aynı varlıklar uygulamaya özgü mantığı veya özel izlenen koşullara göre hello rapor edebilir. Kullanıcı raporları hello sistem raporlarla aradadır.

Nasıl tooreport ve yanıt toohealth hello sırasında tasarım bir büyük bulut hizmeti olarak tooinvest planlayın. Bu önceden investement izlemek ve işletmek hello hizmeti daha kolay toodebug, yapar.

## <a name="health-states"></a>Sistem sağlığı durumları
Service Fabric kullanan üç sistem sağlığı durumları toodescribe bir varlık sağlıklı olsun veya olmasın: Tamam, uyarı ve hata. Herhangi bir raporu toohello sistem durumu deposu şu durumlardan birini belirtmelisiniz gönderdi. Merhaba sistem durumu değerlendirme sonucu bu durumlardan biri.

Merhaba olası [sistem durumlarını](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthstate) şunlardır:

* **TAMAM**. Merhaba varlık sağlıklı değil. Bilinen, veya alt öğelerinden (uygunsa) bildirilen herhangi bir sorun vardır.
* **Uyarı**. Merhaba varlık bazı sorunlar vardır, ancak bunu düzgün çalışmaya devam. Örneğin, gecikmeler vardır, ancak bunlar işlevsel sorunları henüz neden olmaz. Bazı durumlarda, hello Uyarı koşulu dış müdahalesi olmadan kendisini düzeltebilir. Bu durumda, sistem durumu raporlarının farkındalığı artırmak ve görünürlük ne olacağına sağlayın. Diğer durumlarda, kullanıcı müdahalesi olmadan ciddi bir sorun içine hello Uyarı koşulu düşürebilir.
* **Hata**. Merhaba varlık sağlam değil. Düzgün çalışamaz çünkü toofix hello hello varlık durumunu yapılması gerekir.
* **Bilinmeyen**. Merhaba varlık hello health store içinde yok. Bu sonucu birden çok bileşen sonuçlarından birleştirme dağıtılan hello sorgularından elde edilebilir. Örneğin, hello get düğüm liste sorgusu çok gider**FailoverManager**, **ClusterManager**, ve **HealthManager**; uygulama alma liste sorgusu gider çok **ClusterManager** ve **HealthManager**. Bu sorguları birden çok sistem bileşenleri sonuçlarından birleştirin. Başka bir sistem bileşeni health store içinde mevcut olmayan bir varlık döndürürse, hello birleştirilmiş sonucu bilinmiyor sahip sistem durumu. Bir varlık deposunda sistem durumu raporlarının henüz işlenmemiş veya silindikten sonra hello varlık temizlendi olduğundan değil.

## <a name="health-policies"></a>Sistem durumu ilkeleri
bir varlık, raporlar ve alt öğelerini göre sağlıklı olup hello sistem durumu deposu sistem durumu ilkeleri toodetermine geçerlidir.

> [!NOTE]
> Sistem durumu ilkeleri hello küme bildirimi (için Küme ve düğüm sistem durumu değerlendirmesi) veya hello uygulama bildirimi (için uygulama değerlendirmesi ve öğelerinden herhangi biri) belirtilebilir. Sistem durumu değerlendirme istekleri, yalnızca bu değerlendirme için kullanılan özel sistem durumu değerlendirme İlkeleri'nde de geçirebilirsiniz.
> 
> 

Varsayılan olarak, Service Fabric (her şeyi sağlıklı olmalıdır) katı kuralları hello üst-alt hiyerarşik bir ilişki için geçerlidir. Merhaba alt biri bile bir sağlıksız olay varsa, hello üst kötü olarak değerlendirilir.

### <a name="cluster-health-policy"></a>Küme sistem durumu ilkesi
Merhaba [küme sistem durumu ilkesi](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy) kullanılan tooevaluate hello küme sistem durumu ve düğüm sistem durumları olan. Hello İlkesi hello küme bildiriminde tanımlanabilir. Mevcut değilse, hello varsayılan ilke (toleranslı hataları sıfır) kullanılır.
Merhaba küme sistem durumu ilkesi içerir:

* [ConsiderWarningAsError](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.considerwarningaserror). Tootreat uyarı durumu sistem durumu değerlendirmesi sırasında hata olarak raporları olup olmadığını belirtir. Varsayılan: false.
* [MaxPercentUnhealthyApplications](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.maxpercentunhealthyapplications). Merhaba maksimum toleranslı yüzdesi hello küme hata olarak kabul edilmeden önce sağlıksız uygulamaları belirtir.
* [MaxPercentUnhealthyNodes](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.maxpercentunhealthynodes). Merhaba maksimum toleranslı yüzdesi hello küme hata olarak kabul edilmeden önce sağlıksız düğümleri belirtir. Büyük kümelerinde, bazı düğümler her zaman aşağı ya da çıkışı onarım için bu nedenle bu yüzde olmalı yapılandırılmış tootolerate.
* [ApplicationTypeHealthPolicyMap](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.applicationtypehealthpolicymap). Merhaba uygulama türü sistem durumu ilkesi eşlem sırasında küme sistem durumu değerlendirme toodescribe özel uygulama türleri kullanılabilir. Varsayılan olarak, tüm uygulamaları bir havuza yerleştirin ve MaxPercentUnhealthyApplications ile değerlendirilir. Bazı uygulama türleri farklı şekilde ele alınması gerektiğini, hello genel havuzunun dışına alınabilir. Bunun yerine, bunlar hello harita kendi uygulama türü adı ile ilişkili hello yüzdeleri karşı değerlendirilir. Örneğin, bir küme var. uygulamaları farklı türlerde binlerce ve bir özel uygulama türünün birkaç denetim uygulama örnekleri Merhaba denetim uygulamalarını hiç hata olmalıdır. Bazı hatalar genel MaxPercentUnhealthyApplications too20% tootolerate belirtebilirsiniz, ancak hello için uygulama türü "ControlApplicationType" Merhaba MaxPercentUnhealthyApplications too0 ayarlayın. Bu şekilde hello birçok uygulama sağlıksız bazıları, ancak genel hello sağlıksız yüzdenin altında hello küme olacaktır tooWarning değerlendirilir. Sistem Durumu Uyarısı Küme yükseltme etkilemez veya diğer izleme tarafından hata durumu tetiklendi. Ancak hata bile bir denetim uygulamada geri tetikler veya hello yükseltme yapılandırmasına bağlı olarak hello Küme yükseltme duraklatır küme sağlıksız, hale getirir.
  Merhaba eşlemesinde hello uygulama türleri için tanımlı tüm uygulama örnekleri hello dışında uygulamaların genel havuzu alınır. Merhaba toplam sayısına hello uygulama türünde uygulamalar göre değerlendirilir, hello kullanan hello gelen belirli MaxPercentUnhealthyApplications eşlemesi. Merhaba uygulamalarının tüm hello rest hello genel havuzda kalır ve MaxPercentUnhealthyApplications ile değerlendirilir.

Aşağıdaki örnek hello bir alıntı küme bildirimindeki ' dir. Merhaba uygulaması toodefine girişleri harita, "ApplicationTypeMaxPercentUnhealthyApplications hello uygulama türü adından-" ile önek hello parametre adı yazın.

```xml
<FabricSettings>
  <Section Name="HealthManager/ClusterHealthPolicy">
    <Parameter Name="ConsiderWarningAsError" Value="False" />
    <Parameter Name="MaxPercentUnhealthyApplications" Value="20" />
    <Parameter Name="MaxPercentUnhealthyNodes" Value="20" />
    <Parameter Name="ApplicationTypeMaxPercentUnhealthyApplications-ControlApplicationType" Value="0" />
  </Section>
</FabricSettings>
```

### <a name="application-health-policy"></a>Uygulama durumu ilkesi
Merhaba [uygulama durumu ilkesi](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy) hello değerlendirme olayları ve alt durumları bir toplama uygulamaları ve bunların alt öğeleri için nasıl yapılacağı açıklanır. Merhaba uygulama bildiriminde tanımlanabilir **ApplicationManifest.xml**, hello uygulama paketi. İlke belirtilirse, Service Fabric hello varlık hello uyarı veya hata durumu bir sistem durumu raporu ya da bir alt sahipse sağlıksız olduğunu varsayar.
Merhaba yapılandırılabilir ilkeler şunlardır:

* [ConsiderWarningAsError](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.considerwarningaserror.aspx). Tootreat uyarı durumu sistem durumu değerlendirmesi sırasında hata olarak raporları olup olmadığını belirtir. Varsayılan: false.
* [MaxPercentUnhealthyDeployedApplications](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.maxpercentunhealthydeployedapplications). Merhaba uygulaması hata olarak kabul edilmeden önce sağlıksız dağıtılmış uygulamalar hello en fazla izin yüzdesini belirtir. Bu yüzde hello hello uygulamalar şu anda hello kümede dağıtılan düğüm sayısı üzerinden sağlıksız dağıtılmış uygulamalar hello sayısının bölünmesiyle hesaplanır. Merhaba hesaplama düğümleri küçük sayıda bir arıza tootolerate yuvarlar. Varsayılan yüzdesi: sıfır.
* [DefaultServiceTypeHealthPolicy](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.defaultservicetypehealthpolicy). Merhaba varsayılan sistem durumu ilkesi hello uygulamadaki tüm hizmet türleri yerini alan hello varsayılan service type durum ilkesi, belirtir.
* [ServiceTypeHealthPolicyMap](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.servicetypehealthpolicymap). Hizmet türü başına hizmet sistem durumu ilkeleri haritasını sağlar. Bu ilkeler hello varsayılan hizmet türü sistem durumu ilkeleri her belirtilen hizmet türü için değiştirin. Örneğin, bir uygulama bir durum bilgisi olmayan ağ geçidi hizmet türü ve bir durum bilgisi olan altyapısı hizmet türü varsa, kendi değerlendirme hello sistem durumu ilkeleri farklı şekilde yapılandırabilirsiniz. Hizmet türü bazında ilke belirttiğinizde, hello hizmetinin hello durumunun konusunda daha ayrıntılı denetim kazanmadan.

### <a name="service-type-health-policy"></a>Service type durum ilkesi
Merhaba [service type durum ilkesi](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy) nasıl tooevaluate ve toplama hello Hizmetleri ve Hizmetleri alt hello belirtir. Hello İlkesi içerir:

* [MaxPercentUnhealthyPartitionsPerService](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthypartitionsperservice). Bir hizmet sağlıksız kabul edilmeden önce sağlıksız bölümleri hello en fazla izin yüzdesini belirtir. Varsayılan yüzdesi: sıfır.
* [MaxPercentUnhealthyReplicasPerPartition](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthyreplicasperpartition). Bir bölüm sağlıksız kabul edilmeden önce sağlıksız çoğaltmaları hello en fazla izin yüzdesini belirtir. Varsayılan yüzdesi: sıfır.
* [MaxPercentUnhealthyServices](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthyservices). Merhaba uygulaması sağlıksız kabul edilmeden önce sağlıksız Hizmetleri hello en fazla izin yüzdesini belirtir. Varsayılan yüzdesi: sıfır.

Aşağıdaki örnek hello bir uygulama bildirimi yapılan bir alıntı şöyledir:

```xml
    <Policies>
        <HealthPolicy ConsiderWarningAsError="true" MaxPercentUnhealthyDeployedApplications="20">
            <DefaultServiceTypeHealthPolicy
                   MaxPercentUnhealthyServices="0"
                   MaxPercentUnhealthyPartitionsPerService="10"
                   MaxPercentUnhealthyReplicasPerPartition="0"/>
            <ServiceTypeHealthPolicy ServiceTypeName="FrontEndServiceType"
                   MaxPercentUnhealthyServices="0"
                   MaxPercentUnhealthyPartitionsPerService="20"
                   MaxPercentUnhealthyReplicasPerPartition="0"/>
            <ServiceTypeHealthPolicy ServiceTypeName="BackEndServiceType"
                   MaxPercentUnhealthyServices="20"
                   MaxPercentUnhealthyPartitionsPerService="0"
                   MaxPercentUnhealthyReplicasPerPartition="0">
            </ServiceTypeHealthPolicy>
        </HealthPolicy>
    </Policies>
```

## <a name="health-evaluation"></a>Sistem durumu değerlendirmesi
Kullanıcılar ve otomatik hizmetler için herhangi bir varlık health herhangi bir zamanda değerlendirebilirsiniz. tooevaluate bir varlığın sistem durumu, hello sistem durumu deposu toplamalar, tüm sistem durumu raporları hello varlıkta'yı ve tüm alt öğelerini (uygunsa) değerlendirir. Merhaba sistem durumu toplama algoritması nasıl tooevaluate durumu raporları ve nasıl tooaggregate alt sistem (uygunsa) durumları belirtin sistem durumu ilkeleri kullanır.

### <a name="health-report-aggregation"></a>Sistem durumu rapor toplama
Bir varlığın farklı özellikleri farklı reporters (sistem bileşenleri veya watchdogs) tarafından gönderilen birden fazla sistem durumu raporlarının olabilir. Merhaba toplama kullanır ilişkili sistem durumu ilkeleri Merhaba, özellikle uygulama ConsiderWarningAsError üyesi hello veya sistem durumu ilkesi küme. ConsiderWarningAsError belirtir nasıl tooevaluate uyarıları.

Merhaba toplanan sistem durumu hello tarafından tetiklenir *kötü* durumu raporları hello varlık üzerinde. En az bir hata sistem durumu raporu ise hello toplanan sistem durumu bir hatadır.

![Hata raporu sistem durumu rapor toplama.][2]

Bir veya daha fazla hata durumu raporların bulunduğu bir sistem durumu varlık hata olarak değerlendirilir. Merhaba aynı sistem durumu bakılmaksızın bir süresi dolmuş durum raporu için geçerlidir.

[2]: ./media/service-fabric-health-introduction/servicefabric-health-report-eval-error.png

Hiçbir hata raporlarını ve bir veya daha fazla uyarı varsa hello toplanan sistem durumu, uyarı veya hata hello ConsiderWarningAsError İlkesi bayrağı bağlı olarak olur.

![Sistem durumu rapor toplama uyarı raporu ve ConsiderWarningAsError false.][3]

Sistem durumu rapor toplama uyarı raporu ve ConsiderWarningAsError toofalse (varsayılan) ayarlayın.

[3]: ./media/service-fabric-health-introduction/servicefabric-health-report-eval-warning.png

### <a name="child-health-aggregation"></a>Alt sistem durumu toplama
Merhaba toplanan sistem durumu bir varlığın hello alt sistem durumlarını (uygunsa) yansıtır. alt sistem durumlarını toplamak için hello algoritması hello varlık türüne göre hello sistem durumu ilkeleri uygulanabilir kullanır.

![Alt varlık sistem durumu toplama.][4]

Sistem durumu ilkeleri temel alan bir alt toplama.

[4]: ./media/service-fabric-health-introduction/servicefabric-health-hierarchy-eval.png

Merhaba sistem durumu deposu tüm hello alt değerlendirildi sonra sağlıksız alt yapılandırılmış hello en yüksek yüzde tabanlı sistem durumlarını toplar. Bu yüzde hello varlık ve alt türüne göre hello İlkesi alınır.

* Tüm alt öğeleri Tamam durumlar varsa, hello toplanan alt sistem durumu normaldir.
* Alt öğe Tamam ve uyarı durumları varsa hello toplanan alt sistem durumu uyarı konumunda.
* Sağlıksız alt yüzdesi izin hello maksimum uymaz hata durumları alt varsa, hello toplanan sistem durumu bir hatadır.
* Sağlıksız alt yüzdesi izin Hello alt hata durumları saygı hello en fazla ile Merhaba, toplanan sistem durumu uyarı konumunda.

## <a name="health-reporting"></a>Sistem durumu raporlama
Sistem bileşenleri, sistem Fabric uygulamaları ve iç/dış watchdogs Service Fabric varlıklar karşı bildirebilirsiniz. Merhaba reporters olun *yerel* belirlemeleri izleme hello koşullara göre izlenen hello varlıkların hello sistem durumu. Bunlar, herhangi bir genel durum veya veri toplama sırasında toolook gerek yoktur. Merhaba davranışı toohave basit reporters ve hangi bilgi toosend pek çok şey tooinfer adresindeki toolook gereken karmaşık organizmalar istenen.

toosend sistem durumu veri toohello sistem durumu deposu, bir Raporlayıcı tooidentify etkilenen hello varlık gerekir ve bir sistem durumu raporu oluşturun. toosend hello raporu, kullanım hello [FabricClient.HealthClient.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth) API, API hello üzerinde gösterilen rapor sistem durumu `Partition` veya `CodePackageActivationContext` nesneleri, PowerShell cmdlet'leri ve REST.

### <a name="health-reports"></a>Sistem durumu raporları
Merhaba [sistem durumu raporlarının](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthreport) hello varlıkların hello kümedeki her bilgisinden hello içerir:

* **SourceId**. Merhaba Raporlayıcı hello sistem olay benzersiz olarak tanımlayan bir dize.
* **Varlık tanımlayıcısı**. Burada hello rapor uygulanan hello varlık tanımlar. Merhaba göre farklı [varlık türü](service-fabric-health-introduction.md#health-entities-and-hierarchy):
  
  * Küme. yok.
  * Düğüm. Düğüm adı (dize).
  * Uygulama. Uygulama adı (URI). Merhaba hello kümede dağıtılan hello Uygulama örneğinin adını temsil eder.
  * Hizmet. Hizmet adı (URI). Merhaba kümede dağıtılan hello hizmet örneği Hello adını temsil eder.
  * Bölüm. Bölüm kimliği (GUID). Merhaba bölüm benzersiz tanımlayıcıyı temsil eder.
  * Çoğaltma. Merhaba durum bilgisi olan hizmet çoğaltma kimliği veya hello durum bilgisiz hizmet örneği kimliği (Int64).
  * DeployedApplication. Uygulama adı (URI) ve düğüm adı (dize).
  * DeployedServicePackage. Uygulama adı (URI), düğüm adı (dize) ve hizmet adı (dize) bildirim.
* **Özellik**. A *dize* (sabit numaralandırma değil) izin veren hello Raporlayıcı toocategorize hello sistem durumu olayı hello varlığın belirli bir özellik için. Örneğin, bir Raporlayıcı hello Node01 "Depo" özelliği hello durumunu bildirebilirsiniz ve Raporlayıcı B hello Node01 "Bağlantı" özelliği hello durumunu bildirebilirsiniz. Merhaba health store içinde bu raporları hello Node01 varlık için ayrı sistem durumu olayları olarak kabul edilir.
* **Açıklama**. Ayrıntılı bilgi hello sistem durumu olayı hakkında bir Raporlayıcı tooprovide izin veren bir dize. **SourceId**, **özelliği**, ve **HealthState** hello rapor tam olarak açıklamalıdır. Merhaba açıklama hello raporu okunabilir bilgilerini ekler. Merhaba metin, Yöneticiler ve kullanıcılar toounderstand hello sistem durumu raporu kolaylaştırır.
* **HealthState**. Bir [numaralandırma](service-fabric-health-introduction.md#health-states) hello rapor hello sistem durumunu açıklar. Merhaba Tamam, uyarı ve hata değerlerdir kabul edildi.
* **TimeToLive**. Ne kadar süreyle hello sistem durumu raporu belirten bir timespan geçerli değil. İle birlikte **RemoveWhenExpired**, tooevaluate olayları nasıl süresi bilmeniz hello sistem durumu depolama sağlar. Varsayılan olarak, hello değer sonsuzdur ve hello rapor sonsuza kadar geçerlidir.
* **RemoveWhenExpired**. Bir Boole değeri. Varsa Ayarla tootrue, hello süresi dolan sistem durumu raporu hello sistem durumu Mağazası'ndan otomatik olarak kaldırılır ve hello rapor varlık sistem durumu değerlendirmesi etkilemez. Hello rapor yalnızca bir kerelik hello Raporlayıcı ve belirli bir dönem için geçerli olduğunda kullanılan tooexplicitly, temizlemez. Ayrıca hello health Store'dan toodelete raporları kullandı (örneğin, bir izleme değiştirilir ve raporları önceki kaynak ve özelliği ile gönderme durdurur). Herhangi bir önceki durumu hello health Store'dan yukarı RemoveWhenExpired tooclear yanı sıra kısa TimeToLive sahip bir rapor gönderebilirsiniz. Merhaba değer toofalse ayarlanırsa hello süresi dolan rapor hello sistem durumu değerlendirmesi üzerinde hata olarak kabul edilir. Merhaba false değeri, hello kaynak düzenli aralıklarla bu özellikte bildirmelisiniz toohello sistem durumu deposu işaret eder. Seçili değilse, ardından olmalıdır hello izleme ile bir sorun. Merhaba İzleme'nin sistem durumu hello olay hata olarak dikkate alarak yakalanır.
* **SequenceNumber**. Toobe gitgide artan gerektiren bir pozitif tamsayı hello raporları hello sırasını temsil eder. Ağ gecikmesi veya diğer sorunlar nedeniyle geç alınan hello durum deposu toodetect eski raporları tarafından kullanılır. Başlangıç sıra numarası küçük veya buna eşit olan bir raporu reddedilir en son uygulanan toohello numaralı hello aynı varlık, kaynak ve özellik. Başlangıç sıra numarası belirtilmemişse, otomatik olarak oluşturulur. Yalnızca durumu geçişleri raporlama durumunda hello sıra numarasında gerekli tooput olur. Bu durumda, hangi raporların gönderilen ve yük devretme hello bilgi kurtarma için tutmak tooremember hello kaynak gerekir.

Bu dört parça bilgi--SourceId, varlık tanımlayıcısı, özellik ve HealthState--her sistem durumu raporu için gereklidir. Merhaba SourceId dize hello önekiyle toostart izin verilmez "**sistem**", sistem raporlar için ayrılmış. Hello için aynı varlık hello için yalnızca bir rapor yoktur aynı kaynak ve özellik. Aynı kaynak için birden çok rapor hello ve özellik geçersiz kılma birbirlerine hello sistem istemci tarafında (bunlar toplu olarak gönderilir ise) ya da hello sistem durumu deposu tarafında. Merhaba değiştirme sıra numaraları temel alır; Yeni raporlarla (yüksek sıra numaraları) eski raporları değiştirin.

### <a name="health-events"></a>Sistem durumu olayları
Dahili olarak, hello sistem durumu deposu tutar [sistem durumu olayları](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthevent), tüm hello bilgileri hello raporları ve ek meta veriler içerir. Merhaba meta verileri hello rapor toohello sistem istemci belirtilen hello ve hello sunucu tarafında değiştirildiği hello saatini içerir. Merhaba sistem durumu olayları tarafından döndürülen [sistem durumu sorgularının](service-fabric-view-entities-aggregated-health.md#health-queries).

Merhaba eklenen meta veriler içeriyor:

* **SourceUtcTimestamp**. Merhaba süresi hello raporu toohello sistem istemci (Eşgüdümlü Evrensel Saat) verildi.
* **LastModifiedUtcTimestamp**. Merhaba süresi hello raporu hello sunucu tarafında (Eşgüdümlü Evrensel Saat) son değiştirildiği.
* **IsExpired**. A hello sorgu hello sistem durumu mağaza tarafından çalıştırıldığında hello raporun süresi sona erdi olup olmadığını tooindicate bayrak. Yalnızca RemoveWhenExpired false ise bir olay süresi dolmuş. Aksi takdirde hello olay sorgu tarafından döndürülen değil ve hello Mağazası'ndan kaldırıldı.
* **LastOkTransitionAt**, **LastWarningTransitionAt**, **LastErrorTransitionAt**. Merhaba Tamam/uyarı/hata geçişleri son kez. Bu alanların hello olay için hello sağlık durumu geçişleri hello geçmişini verin.

Merhaba durumu geçişi alanları akıllı uyarıları veya "geçmiş" sistem durumu olay bilgileri için kullanılabilir. Bunlar senaryoları aşağıdaki gibi etkinleştirin:

* Bir özellik uyarı/hata için birden fazla X dakika sırasında bırakıldı olduğunda uyarır. Bir süre için Hello koşul denetimi uyarılar geçici koşullara önler. Örneğin, hello sistem durumu beş dakikadan fazla uyarı, bir uyarı içine çevrilebilir (HealthState uyarı ve şimdi - LastWarningTransitionTime == > 5 dakika).
* Son X dakika hello değişen koşullara uyarı. Merhaba belirtilen süre önce bir rapor zaten hata varsa, onu zaten daha önce sinyal çünkü yoksayılabilir.
* Bir özellik uyarı ve hata arasında geçiş, ne kadar süreyle sağlıksız edildikten belirleyin (diğer bir deyişle, Tamam değil). Örneğin, hello özelliği beş dakikadan daha iyi bırakılmamışsa bir uyarı içine çevrilebilir (HealthState! Tamam ve şimdi - LastOkTransitionTime = > 5 dakika).

## <a name="example-report-and-evaluate-application-health"></a>Örnek: Rapor etme ve uygulama sağlığını değerlendir
Merhaba aşağıdaki örnekte bir sistem durumu raporu PowerShell aracılığıyla hello uygulama üzerinde gönderir **fabric: / WordCount** hello kaynağından **MyWatchdog**. Merhaba sistem durumu raporu hello sistem durumu özelliği "kullanılabilirlik" sonsuz TimeToLive ile bir hata sistem durumu hakkında bilgi içerir. Merhaba uygulama sistem durumu, sorgular ardından sistem durumu olayları sistem durumu olayları hello listesinde bildirilen sağlık durumu hataları ve hello döndüren bir araya getirilir.

```powershell
PS C:\> Send-ServiceFabricApplicationHealthReport –ApplicationName fabric:/WordCount –SourceId "MyWatchdog" –HealthProperty "Availability" –HealthState Error

PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            :
                                  Error event: SourceId='MyWatchdog', Property='Availability'.

ServiceHealthStates             :
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error

                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok

DeployedApplicationHealthStates :
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok

HealthEvents                    :
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 360
                                  SentAt                : 3/22/2016 7:56:53 PM
                                  ReceivedAt            : 3/22/2016 7:56:53 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 3/22/2016 7:56:53 PM, LastWarning = 1/1/0001 12:00:00 AM

                                  SourceId              : MyWatchdog
                                  Property              : Availability
                                  HealthState           : Error
                                  SequenceNumber        : 131032204762818013
                                  SentAt                : 3/23/2016 3:27:56 PM
                                  ReceivedAt            : 3/23/2016 3:27:56 PM
                                  TTL                   : Infinite
                                  Description           :
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Ok->Error = 3/23/2016 3:27:56 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="health-model-usage"></a>Sistem durumu modeli kullanımı
İzleme ve sistem durumu belirlemeleri hello farklı İzleyici hello kümedeki arasında dağıtıldığı için bulut Hizmetleri ve Service Fabric platform tooscale temel Merhaba, hello sistem durumu modeli sağlar.
Diğer sistemler, merkezi bir hizmettir tüm hello ayrıştırır hello küme düzeyinde sahip *olası* Hizmetleri tarafından gösterilen yararlı bilgiler. Bu yaklaşım, ölçeklenebilirlik yavaşlattığını. Bu da onları toocollect belirli bilgiler gibi mümkün olduğunca yakın toohello kök neden toohelp tanımlamak sorunları ve olası sorunları izin vermez.

Merhaba sistem durumu modeli, izleme ve Tanılama, küme ve uygulama durumunu değerlendirme ve izlenen yükseltmeler için yoğun olarak kullanılır. Diğer hizmetler veri tooperform otomatik onarır durumu kullanın, küme sistem durumu geçmişini oluşturmak ve belirli koşullar uyarılar sorun.

## <a name="next-steps"></a>Sonraki adımlar
[Service Fabric sistem durumu raporlarını görüntüle](service-fabric-view-entities-aggregated-health.md)

[Sorunlarını gidermek için sistem durumu raporlarını kullanma](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Nasıl tooreport ve onay sistem durumu hizmeti](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Özel Service Fabric sistem durumu rapor ekleme](service-fabric-report-health.md)

[İzleme ve Hizmetleri yerel olarak tanılama](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Service Fabric uygulama yükseltme](service-fabric-application-upgrade.md)

