---
title: Azure Service Fabric Linux'ta | Microsoft Docs
description: "Service Fabric kümeleri, Linux ve Java, anlamına gelir, dağıtabilmesi ve Java ve C# Linux'ta yazılmış konak Service Fabric uygulamaları destekler."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 459afade-145d-4ee6-b72b-ddf380ccd1bf
ms.service: service-fabric
ms.devlang: Java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: SubramaR
ms.openlocfilehash: dddc9f698d9776999d406117b46285a0f90d9620
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="service-fabric-on-linux"></a>Service Fabric Linux
Service Fabric Linux'ta önizlemesini oluşturmak, dağıtmak ve Linux üzerinde yüksek oranda kullanılabilir, ölçeklendirilebilir uygulamalar Windows üzerinde gibi yönetme sağlar. Service Fabric çerçeveleri (Reliable Services ve Reliable Actors) yanı sıra C# (.NET Core) Linux'ta Java mevcuttur.  Ayrıca, oluşturabilirsiniz [Konuk yürütülebilir Hizmetleri](service-fabric-deploy-existing-app.md) herhangi bir dil veya framework ile. Ayrıca, preview yönetme Docker kapsayıcıları destekler. Docker kapsayıcıları Konuk yürütülebilir dosyalar veya Service Fabric çerçeveleri kullanan yerel Service Fabric hizmetler çalıştırabilirsiniz.

Service Fabric Linux (işletim sistemi özellikleri ve programlama dili desteği hariç) kavramsal olarak Windows Service Fabric eşdeğerdir. Bu nedenle, çoğu bizim [var olan belgeler](http://aka.ms/servicefabricdocs) teknolojisiyle tanıdık alma yardımcı uygular.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a>Desteklenen işletim sistemleri ve programlama dilleri
Sınırlı Önizleme Ubuntu Server 16.04 çalıştıran Azure'da çoklu makine kümeleri yanı sıra bir kutusunu geliştirme kümelerin oluşturulmasını destekler. Önizleme Reliable Actors ve güvenilir durum bilgisi olmayan hizmetler çerçeveleri Java ve C# içinde Konuk yürütülebilir dosyaları ve Docker kapsayıcıları yönetme ek olarak destekler.  

> [!NOTE]
> Güvenilir koleksiyonları Linux içinde henüz desteklenmiyor. Tek başına kümeleri desteklenmeyen ya - yalnızca bir kutusunu ve de Azure Linux çoklu makine kümeleri Önizleme'de desteklenir.
>
>


## <a name="supported-tooling"></a>Desteklenen araçları
Önizleme Service Fabric CLI aracılığıyla etkileşim destekler. Java geliştiricileri için Eclipse ve Yeoman ile tümleştirme, OSX ve Linux üzerinde desteklenen Eclipse ile sağlanır. OSX tümleştirme vagrant aracılığıyla başlık altında bir Linux VM kullanır. C# geliştiricileri için Yeoman ile tümleştirme, uygulama şablonları oluşturmak için sağlanır.

## <a name="next-steps"></a>Sonraki adımlar

* İle tanışın [Reliable Actors](service-fabric-reliable-actors-introduction.md) ve [Reliable Services](service-fabric-reliable-services-introduction.md) çerçeveleri programlama
* [Linux üzerinde geliştirme ortamınızı hazırlama](service-fabric-get-started-linux.md)
* [OSX üzerinde geliştirme ortamınızı hazırlama](service-fabric-get-started-mac.md)
* [Linux üzerinde ilk Service Fabric Java uygulamanızı oluşturma](service-fabric-create-your-first-linux-application-with-java.md)
* [Service Fabric sürekli tümleştirme ve dağıtım Jenkins ve GitHub ile Kurulum](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [Service Fabric Windows/Linux farkları](service-fabric-linux-windows-differences.md)
