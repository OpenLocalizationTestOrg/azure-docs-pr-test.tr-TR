---
title: Windows Azure mikro aaaDebug | Microsoft Docs
description: "Bilgi nasıl toomonitor ve bir yerel geliştirme makinede Microsoft Azure Service Fabric kullanılarak yazılmış hizmetlerinizi tanılama."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: edcc0631-ed2d-45a3-851d-2c4fa0f4a326
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/24/2017
ms.author: dekapur
ms.openlocfilehash: 24868aa194b8a28fa3e6de95c1de5506d912a544
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a>İzleme ve yerel makine geliştirme Kurulum Hizmetleri'nde tanılama
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
> 
> 

İzleme, algılama, tanılama ve sorun giderme hizmetleri toocontinue en az kesintiyi toohello kullanıcı deneyimi ile ayırın. İzleme ve tanılama gerçek dağıtılmış üretim ortamında kritik olsa da, benzer bir model tooa gerçek kurulum taşıdığınızda çalıştıkları Hizmetleri tooensure geliştirme sırasında benimsenmesi hello verimliliği bağlıdır. Service Fabric tek makineli yerel geliştirme kurulumları ve gerçek üretim küme kurulumları arasında sorunsuz bir şekilde çalışabilirsiniz hizmet geliştiricileri tooimplement tanılama kolaylaştırır.

## <a name="event-tracing-for-windows"></a>Windows için olay izleme
[Windows için olay izleme](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) teknolojisi Service Fabric izleme iletiler için önerilen hello değil. ETW kullanmanın bazı avantajları şunlardır:

* **ETW hızlıdır.** Kod yürütme süreleri etkisi en az bir izleme teknoloji olarak oluşturuldu.
* **ETW İzleme, yerel geliştirme ortamları ve ayrıca gerçek küme kurulumları arasında sorunsuz çalışır.** Bu kod tooa gerçek kümenizi, izleme kod hazır toodeploy olduğunda toorewrite yok anlamına gelir.
* **Service Fabric sistem kodu ETW iç izleme için de kullanır.** Bu, uygulama izlemelerini Service Fabric sistem izlemeleri ile araya eklemeli tooview sağlar. Ayrıca kolayca hello sıraları ve uygulama kodu ve olaylar birbiriyle hello temel sistemde anlamak toomore yardımcı olur.
* **Tooview ETW olayları Service Fabric Visual Studio Araçları'nda yerleşik desteği yoktur.** Visual Studio Service Fabric ile doğru şekilde yapılandırıldıktan sonra ETW olayları hello Visual Studio Tanılama Olayları görünümünü görünür. 

## <a name="view-service-fabric-system-events-in-visual-studio"></a>Visual Studio'da Service Fabric sistem olayları görüntülemek
Service Fabric toohelp uygulama geliştiricileri hello platformunda neler olduğunu anlama ETW olayları gösterir. Zaten yapmadıysanız, bir tane hello adımları [Visual Studio'da ilk uygulamanızı oluşturma](service-fabric-create-your-first-application-in-visual-studio.md). Bu bilgiler yardımcı olur, bir uygulama başlamak ve çalıştırmak hello hello izleme iletilerini gösteren Tanılama Olayları Görüntüleyicisi ile.

1. Merhaba Tanılama Olayları penceresi otomatik olarak göstermiyor, toohello giderseniz **Görünüm** sekmesinde Visual Studio'da, seçin **diğer pencereler** ve ardından **Tanılama Olayları Görüntüleyicisi**.
2. Her bir olay hello düğümü, uygulama ve hizmet hello olay geldiğini belirten standart meta veri bilgileri yok. Hello kullanarak hello olayların listesini filtreleyebilirsiniz **filtre olayları** kutusunu hello olayları penceresinin hello üstünde. Örneğin, filtreleyebilirsiniz **düğüm adı** veya **hizmet adı.** Ve olay ayrıntılarını bakarken, ayrıca hello kullanarak duraklatabilirsiniz **duraklatma** hello olayları penceresinin hello üstünde düğmesine tıklayın ve daha sonra olayları herhangi bir kayıp devam.
   
   ![Visual Studio Tanılama Olayları Görüntüleyicisi](./media/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally/DiagEventsExamples2.png)

## <a name="add-your-own-custom-traces-toohello-application-code"></a>Kendi özel izlemeleri toohello uygulama kodu ekleyin
Merhaba Service Fabric Visual Studio Proje şablonları örnek kod içerir. Merhaba kodunu nasıl tooadd özel uygulama kodu ETW gösteren yukarı Service Fabric sistem izlemeleri yanında hello Visual Studio ETW görüntüleyicide izlediğini gösterir. Merhaba bu yöntemin avantajı meta veri tootraces otomatik olarak eklenir ve Visual Studio Tanılama Olayları Görüntüleyicisi bulunmakta hello toodisplay yapılandırılmış olan bunları.

Hello oluşturulan projeleri için **hizmet şablonları** hello (durum bilgisiz veya durum bilgisi olan) yalnızca arama `RunAsync` uygulama:

1. Çağrı çok hello`ServiceEventSource.Current.ServiceMessage` hello içinde `RunAsync` yöntemi bir özel ETW İzleme örneği hello uygulama kodundan gösterir.
2. Merhaba, **ServiceEventSource.cs** dosya, bir aşırı Merhaba bulacaksınız `ServiceEventSource.ServiceMessage` tooperformance nedenlerden dolayı yüksek sıklıkta olayları için kullanılması gereken yöntemi.

Hello oluşturulan projeleri için **aktör şablonları** (durum bilgisiz veya durum bilgisi olan):

1. Açık hello **"ProjectName".cs** dosya nerede *ProjectName* Visual Studio projeniz için seçtiğiniz hello adıdır.  
2. Merhaba kod Bul `ActorEventSource.Current.ActorMessage(this, "Doing Work");` hello içinde *DoWorkAsync* yöntemi.  Bu, uygulama kodundan yazılmış özel bir ETW İzleme örneğidir.  
3. Dosyasındaki **ActorEventSource.cs**, bir aşırı Merhaba bulacaksınız `ActorEventSource.ActorMessage` tooperformance nedenlerden dolayı yüksek sıklıkta olayları için kullanılması gereken yöntemi.

Tooyour servis kodu izleme özel ETW ekledikten sonra oluşturmak, dağıtmak ve hello uygulamayı çalıştırmak yeniden toosee hello Tanılama Olayları Görüntüleyicisi içinde olay. Merhaba uygulamayla ayıklaması **F5**, hello Tanılama Olayları Görüntüleyicisi'ni otomatik olarak açılır.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba yukarıda tooyour uygulama yerel tanılama için eklenen aynı izleme kodu tooview kullanabileceğiniz araçları ile uygulamanızı Azure bir kümede çalışırken bu olayları çalışır. Merhaba hello araçları için farklı seçenekleri ele ve nasıl bunları ayarlayabilirsiniz açıklayan Bu makaleler göz atın.

* [Nasıl toocollect ile Azure tanılama günlükleri](service-fabric-diagnostics-how-to-setup-wad.md)
* [Olay toplama ve EventFlow kullanarak koleksiyonu](service-fabric-diagnostics-event-aggregation-eventflow.md)

