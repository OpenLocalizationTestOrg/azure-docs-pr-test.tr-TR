---
title: "Azure Service Fabric destek seçenekleri hakkında bilgi edinin | Microsoft Docs"
description: "Azure Service Fabric kümesi sürümleri desteklenir ve dosya bağlantılarını biletleri destekleyen"
services: service-fabric
documentationcenter: .net
author: pkc
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: pkc
ms.openlocfilehash: 78e68cff3a757cbbcd8dc6f53120e6a4af54591a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-service-fabric-support-options"></a>Azure Service Fabric destek seçenekleri

Uygulama iş yükleri çalıştıran, Service Fabric kümeleri için uygun desteği teslim etmek için size çeşitli seçenekler oluşturdunuz. Gerekli destek düzeyini ve sorunun önem derecesini bağlı olarak, doğru seçenekler çekme alın. 


<a id="getlivesitesupportonazure"></a>

## <a name="report-production-or-live-site-issues-or-request-paid-support-for-azure"></a>Üretim ya da Canlı site sorunları rapor veya Azure Ücretli destek isteği

Azure üzerinde dağıtılan Service Fabric kümenizdeki Canlı site sorunlarını raporlama için profesyonel desteği için bilet [Azure Portal'daki](https://ms.portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview) veya [Microsoft destek portalı](http://support.microsoft.com/oas/default.aspx?prid=16146).

Daha fazla bilgi edinin:
 
- [Microsoft Profesyonel desteği Azure](https://azure.microsoft.com/en-us/support/plans/?b=16.44).
- [Microsoft premier Destek](https://support.microsoft.com/en-us/premier).

<a id="getlivesitesupportonprem"></a>

## <a name="report-production-or-live-site-issues-or-request-paid-support-for-standalone-service-fabric-clusters"></a>Üretim ya da Canlı site sorunları rapor veya tek başına Service Fabric kümeleri için Ücretli destek isteği

Şirket içi dağıtılan Service Fabric kümenizde Canlı site sorunlarını raporlama için veya diğer Bulutları, profesyonel desteği için üzerinde bilet [Microsoft destek portalı](http://support.microsoft.com/oas/default.aspx?prid=16146).

Daha fazla bilgi edinin:

- [Şirket içi Microsoft Profesyonel desteği](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).
- [Microsoft premier Destek](https://support.microsoft.com/en-us/premier).


<a id="getsupportonissues"></a>
## <a name="report-azure-service-fabric-issues"></a>Rapor Azure Service Fabric sorunları 
Biz Service Fabric sorunları raporlama için GitHub deposuna oluşturdunuz.  Biz de etkin bir şekilde aşağıdaki forumları izlemekte olduğunuz.

### <a name="github-repo"></a>GitHub depo 
Azure Service Fabric sorunların rapor [Service Fabric sorunların git deposuna](https://github.com/Azure/service-fabric-issues). Bu depodaki raporlama ve sorunları küçük özellik istekleri yapmak için Azure Service Fabric ile izleme yöneliktir. **Bu rapor Canlı site sorunları kullanmayın**.

### <a name="stackoverflow-and-msdn-forums"></a>StackOverflow ve MSDN Forumları

[StackOverflow Service Fabric etiketinde] [ stackoverflow] ve [Service Fabric MSDN Forumu] [ msdn-forum] sorular hakkında nasıl sormak için kullanılan en iyi olan Platform çalışır ve bazı görevlerle nasıl yapabilirsiniz.

### <a name="azure-feedback-forum"></a>Azure görüş Forumu

[Azure Service Fabric için geri bildirim Forumunda] [ uservoice-forum] biz en popüler isteklerini gözden geçirirken ürün için sahip büyük özellik fikirleri uzun vadeli planlama için bizim Orta parçası olan göndermek için en iyi yerdir. Topluluk içinde önerilerinizi desteği rally öneririz.


<a id="releasesuport"></a>
## <a name="supported-service-fabric-versions"></a>Desteklenen Service Fabric sürümleri.

Kümenizi, desteklenen bir Service Fabric sürümü her zaman çalışır durumda olduğundan emin olun. Gibi ve size yeni bir Service Fabric sürümü sunmaktan olduğunda, önceki sürümü en az 60 gün o tarihten sonra destek sonu için işaretlenir. Yeni sürümler duyurulur [Service Fabric ekip blogunda](https://blogs.msdn.microsoft.com/azureservicefabric/).

Desteklenen bir Service Fabric sürümünü çalıştıran kümenizi tutmak hakkında ayrıntılar aşağıdaki belgelere bakın.

- [Bir Azure kümede yükseltme Service Fabric sürümü](service-fabric-cluster-upgrade.md)
- [Tek başına windows server kümesi Service Fabric sürümüne yükseltme](service-fabric-cluster-upgrade-windows-server.md)
 
Desteklenen Service Fabric sürümlerinin listesini ve bunların destek bitiş tarihlerini aşağıda verilmiştir.

| **Service Fabric çalışma kümesi** | **Uyumlu SDK / NuGet paketi sürümleri** | **Destek tarih sonu** |
| --- | --- | --- |
| Tüm küme 5.3.121'den önceki sürümleri |Sürüm 2.3 küçük veya eşit |20 Ocak 2017 |
| 5.3.* |Sürüm 2.3 küçük veya eşit |24 Şubat 2017 |
| 5.4.* |Sürüm 2.4 küçük veya eşit |10,2017 olabilir     |
| 5.5.* |Sürüm 2.5 küçük veya eşit |Ağustos 10,2017    |
| 5.6.* |Sürüm 2.6 küçük veya eşit |Ekim 13,2017    |
| 5.7.* |Sürüm 2.7 küçük veya eşit |Geçerli sürüm ve dolayısıyla bitiş tarihi

<a id="previewversion"></a>
## <a name="service-fabric-preview-versions---unsupported-for-production-use"></a>Service Fabric Önizleme sürümlerini - üretim kullanımı için desteklenmiyor.
Zaman zaman önizlemeleri sunulan, geri bildirim istiyoruz önemli özellikleri olan sürümleri bırakın. Bu önizleme sürümleri yalnızca sınama amacıyla kullanılmalıdır. Üretim kümenizi her zaman bir desteklenen ve kararlı, Service Fabric sürümünü çalıştırması gerekir. Önizleme sürümü her zaman 255 birincil ve ikincil sürüm numarası ile başlar. Örneğin, Service Fabric sürümü 255.255.5703.949 görürseniz, bu sürümü yalnızca test kümelerde kullanılacak ve önizleme aşamasındadır. Bu önizleme sürümleri de üzerinde duyurulur [Service Fabric ekip blogu](https://blogs.msdn.microsoft.com/azureservicefabric) ve dahil edilen özellikler ayrıntıları sahip olacaktır.

Bu önizleme sürümleri için Ücretli destek seçeneği yoktur. Altında listelenen seçeneklerden birini kullanın [rapor Azure Service Fabric sorunları](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support#report-azure-service-fabric-issues) sorular sormak veya görüş bildirin.

## <a name="next-steps"></a>Sonraki adımlar

- [Service fabric sürümü Azure bir kümede yükseltme](service-fabric-cluster-upgrade.md)
- [Tek başına windows server kümesi Service Fabric sürümüne yükseltme](service-fabric-cluster-upgrade-windows-server.md)

<!--references-->
[msdn-forum]: https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureServiceFabric
[stackoverflow]: http://stackoverflow.com/questions/tagged/azure-service-fabric
[uservoice-forum]: https://feedback.azure.com/forums/293901-service-fabric
[acom-docs]: http://aka.ms/servicefabricdocs
[sample-repos]: http://aka.ms/servicefabricsamples
