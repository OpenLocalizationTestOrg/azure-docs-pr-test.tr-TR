---
title: Service Fabric Linux'ta aaaAzure | Microsoft Docs
description: "Service Fabric kümeleri, Linux ve mümkün toodeploy ve ana bilgisayar Service Fabric uygulamaları Linux üzerinde Java ve C# içinde yazılmış olacak anlamına gelir Java destekler."
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
ms.openlocfilehash: ca0e092b00faec560963c0d6cc379593d085f6a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-on-linux"></a>Service Fabric Linux
Service Fabric Linux'ta Hello önizlemesini toobuild sağlar, dağıtın ve Linux üzerinde yüksek oranda kullanılabilir, ölçeklendirilebilir uygulamalar Windows üzerinde gibi yönetin. Merhaba Service Fabric çerçeveler (Reliable Services ve Reliable Actors) toplama tooC # (.NET Core) Linux üzerinde Java mevcuttur.  Ayrıca, oluşturabilirsiniz [Konuk yürütülebilir Hizmetleri](service-fabric-deploy-existing-app.md) herhangi bir dil veya framework ile. Ayrıca, hello Önizleme yönetme Docker kapsayıcıları destekler. Docker kapsayıcıları Konuk yürütülebilir dosyalar veya hello Service Fabric çerçeveler kullanan yerel Service Fabric hizmetler çalıştırabilirsiniz.

Service Fabric Linux'ta (dışında işletim sistemi özellikleri ve programlama dili desteği) kavramsal olarak eşdeğer tooService Windows Fabric ' dir. Bu nedenle, çoğu bizim [var olan belgeler](http://aka.ms/servicefabricdocs) hello teknolojisiyle tanıdık alma yardımcı uygular.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a>Desteklenen işletim sistemleri ve programlama dilleri
sınırlı hello Önizleme destekler hello bir kutusunu geliştirme oluşturulmasını ayrıca toomulti makine Azure Ubuntu Server 16.04 çalıştıran kümeler. Reliable Actors hello ve ayrıca tooguest yürütülebilir dosyaları ve Docker kapsayıcıları yönetme Java ve C# içinde güvenilir durum bilgisi olmayan hizmetler çerçeve hello Hello Önizleme destekler.  

> [!NOTE]
> Güvenilir koleksiyonları Linux içinde henüz desteklenmiyor. Tek başına kümeleri desteklenmeyen ya - yalnızca bir kutusunu ve de Azure Linux çoklu makine kümeleri hello Önizleme'de desteklenir.
>
>


## <a name="supported-tooling"></a>Desteklenen araçları
Merhaba Önizleme Service Fabric CLI aracılığıyla hello kümesi ile etkileşimi destekler. Java geliştiricileri için Eclipse ve Yeoman ile tümleştirme, OSX ve Linux üzerinde desteklenen Eclipse ile sağlanır. Merhaba OSX tümleştirme vagrant aracılığıyla hello başlık altında bir Linux VM kullanır. C# geliştiricileri için Yeoman ile tümleştirme toogenerate uygulama şablonları sağlanır.

## <a name="next-steps"></a>Sonraki adımlar

* Merhaba ile tanışın [Reliable Actors](service-fabric-reliable-actors-introduction.md) ve [Reliable Services](service-fabric-reliable-services-introduction.md) çerçeveleri programlama
* [Linux üzerinde geliştirme ortamınızı hazırlama](service-fabric-get-started-linux.md)
* [OSX üzerinde geliştirme ortamınızı hazırlama](service-fabric-get-started-mac.md)
* [Linux üzerinde ilk Service Fabric Java uygulamanızı oluşturma](service-fabric-create-your-first-linux-application-with-java.md)
* [Service Fabric sürekli tümleştirme ve dağıtım Jenkins ve GitHub ile Kurulum](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [Service Fabric Windows/Linux farkları](service-fabric-linux-windows-differences.md)
