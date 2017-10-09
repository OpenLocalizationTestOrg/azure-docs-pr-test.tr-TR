---
title: "aaaDebug Visual Studio uygulamanızda | Microsoft Docs"
description: "Merhaba güvenilirliğini ve performansını hizmetlerinizi geliştirmek ve bunları Visual Studio'da bir yerel geliştirme kümede hata ayıklama tarafından geliştirin."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: 8d08689e82195d09f57b462631ad04fd237bc4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a>Service Fabric uygulamanızı Visual Studio kullanarak hata ayıklama
> [!div class="op_single_selector"]
> * [Visual Studio/CSharp](service-fabric-debugging-your-application.md) 
> * [Eclipse/Java](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a>Yerel bir Service Fabric uygulama hata ayıklama
Saat ve para dağıtma ve yerel bilgisayar geliştirme küme Azure Service Fabric uygulamanızda hata ayıklama kaydedebilirsiniz. Visual Studio 2017 veya Visual Studio 2015 hello uygulama toohello yerel küme dağıtabilir ve uygulamanızın hello hata ayıklayıcı tooall örnekleri otomatik olarak bağlan.

1. Merhaba adımları izleyerek yerel bir geliştirme kümesi Başlat [, Service Fabric geliştirme ortamını ayarlama](service-fabric-get-started.md).
2. Tuşuna **F5** veya **hata ayıklama** > **hata ayıklamayı Başlat**.
   
    ![Bir uygulamanın hata ayıklamayı Başlat][startdebugging]
3. Kesme kodu ve adım hello uygulaması aracılığıyla hello komutlarda tıklayarak **hata ayıklama** menüsü.
   
   > [!NOTE]
   > Visual Studio uygulamanızı tooall örneklerini ekler. Kod atlama olsa da, kesme noktaları eşzamanlı oturumlarında kaynaklanan birden çok işlemler tarafından isabet. Bunlar, her kesme hello iş parçacığı kimliği koşullu yaparak veya tanılama olayları kullanarak isabet sonra hello kesme noktaları devre dışı bırakmayı deneyin.
   > 
   > 
4. Merhaba **tanılama olayları** penceresi gerçek zamanlı olarak tanılama olayları görebilecek şekilde otomatik olarak açılır.
   
    ![Gerçek zamanlı tanılama olaylarını görüntüle][diagnosticevents]
5. Merhaba da açabilirsiniz **tanılama olayları** Cloud Explorer penceresinde.  Altında **Service Fabric**, herhangi bir düğüme sağ tıklayın ve seçin **görünüm akış izlemeleri**.
   
    ![Açık hello Tanılama Olayları penceresi][viewdiagnosticevents]
   
    İzlemeler tooa belirli hizmeti veya uygulamayı toofilter istiyorsanız, yalnızca belirli hizmet veya uygulama akış izlemeleri etkinleştirin.
6. Merhaba Tanılama Olayları otomatik olarak oluşturulan hello görülen **ServiceEventSource.cs** dosya ve uygulama kodundan denir.
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. Merhaba **tanılama olayları** penceresi filtreleme, duraklatma ve gerçek zamanlı olayları inceleniyor destekler.  Merhaba, hello olay iletisi içeriği de dahil olmak üzere, bir basit bir dize arama filtredir.
   
    ![Filtre, duraklatma ve sürdürme veya gerçek zamanlı olayları inceleyin.][diagnosticeventsactions]
8. Hata Ayıklama Hizmetleri başka bir uygulama hata ayıklama gibi değildir. Kesme noktaları Visual Studio aracılığıyla kolay hata ayıklamak için normal olarak ayarlarsınız. Güvenilir koleksiyonları birden çok düğümü arasında çoğaltma olsa da, bunlar hala IEnumerable uygulayın. Bu, hello sonuçları görünümü Visual Studio'da toosee hata ayıklarken içine koyduğunuz kullanabileceğiniz anlamına gelir. Yalnızca bir kesme noktası kodunuzda herhangi bir yere ayarlayın.
   
    ![Bir uygulamanın hata ayıklamayı Başlat][breakpoint]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a>Uzak bir Service Fabric uygulaması hata ayıklama
Service Fabric uygulamalarınızı Azure Service Fabric kümesi üzerinde çalıştırıyorsanız, mümkün tooremotely bunlar, doğrudan Visual Studio'dan hata ayıklama.

> [!NOTE]
> Merhaba özellik gerektirir [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) ve [.NET 2.9 için Azure SDK](https://azure.microsoft.com/downloads/).    
> 
> 

<!-- -->
> [!WARNING]
> Uzaktan hata ayıklama, geliştirme ve test senaryoları ve üretim ortamlarında çalışan uygulamalar hello hello etkisini nedeniyle kullanılan toobe için tasarlanmıştır.
> 
> 

1. Tooyour kümesinde gezinmek **Cloud Explorer**seçin ve sağ tıklatıp **etkinleştirmek hata ayıklama**
   
    ![Uzaktan hata ayıklamayı etkinleştirme][enableremotedebugging]
   
    Bu kapatma hello hata ayıklama uzantısı, küme düğümlerinde uzak etkinleştirme hello işlemini kazandırın yanı ağ yapılandırmaları gerekir.
2. Sağ hello küme düğümünde **Cloud Explorer**ve seçin **ekleme hata ayıklayıcı**
   
    ![Hata ayıklayıcıyı Ekle][attachdebugger]
3. Merhaba, **tooprocess Attach** iletişim kutusunda, toodebug istediğiniz ve tıklatın hello işlem seçin **Ekle**
   
    ![İşlem seçin][chooseprocess]
   
    Merhaba adı için tooattach istediğiniz hello işlemi, eşittir hello hizmet projesi derleme adı.
   
    Merhaba hata ayıklayıcı hello işlem çalışan tooall düğümlerini ekleyecek.
   
   * Bir durum bilgisi olmayan Hizmetin nerede ayıkladığınız hello durumda da, tüm düğümlerde hello hizmetin tüm örneklerine ait hello hata ayıklama oturumu bir parçasıdır.
   * Durum bilgisi olan hizmet hata ayıklama, yalnızca birincil çoğaltmasını herhangi bir bölümü hello etkin ve bu nedenle hello hata ayıklayıcı tarafından yakalanan olacaktır. Merhaba birincil çoğaltma hello hata ayıklama oturumu sırasında geçerse, bu çoğaltma hello işlenmesini hello hata ayıklama oturumunun parçası olmaya devam edecektir.
   * Sipariş tooonly catch ilgili bölümleri veya belirli bir hizmeti örneklerini koşullu kesme noktaları tooonly sonu belirli bir bölüm veya örnek kullanabilirsiniz.
     
     ![Koşullu kesme noktası][conditionalbreakpoint]
     
     > [!NOTE]
     > Service Fabric kümesi hello birden çok örneği ile hata ayıklama şu anda desteklemiyoruz aynı hizmet yürütülebilir dosya adı.
     > 
     > 
4. Uygulamanızın hatalarını ayıklama tamamladıktan sonra hello uzaktan hata ayıklama uzantısı hello kümede sağ tıklayarak devre dışı bırakabilirsiniz **Cloud Explorer** ve **devre dışı bırakmak hata ayıklama**
   
    ![Uzaktan hata ayıklama devre dışı bırak][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a>Uzak küme düğümüne izlemeleri akış
Ayrıca, doğrudan bir uzak küme düğümü tooVisual Studio mümkün toostream izlemeleri de değildir. Bu özellik toostream ETW İzleme olayları, Service Fabric küme düğümünde üretilen sağlar.

> [!NOTE]
> Bu özellik gerektirir [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) ve [.NET 2.9 için Azure SDK](https://azure.microsoft.com/downloads/).
> Bu özellik yalnızca Azure üzerinde çalışan kümelerle destekler.
> 
> 

<!-- -->
> [!WARNING]
> İzlemeler akış geliştirme ve test senaryoları ve üretim ortamlarında çalışan uygulamalar hello hello etkisini nedeniyle kullanılan toobe için tasarlanmıştır.
> Bir üretim senaryosunda, Azure Tanılama'yı kullanarak olayları iletme yararlanmalıdır.
> 
> 

1. Tooyour kümesinde gezinmek **Cloud Explorer**seçin ve sağ tıklatıp **akış izlemeleri etkinleştir**
   
    ![Uzak akış izlemeleri etkinleştir][enablestreamingtraces]
   
    Bu, küme düğümlerinde izlemeleri uzantısı akış hello etkinleştirme işleminin hello kapalı kazandırın yanı ağ yapılandırmaları gerekir.
2. Merhaba genişletin **düğümleri** öğesinde **Cloud Explorer**, toostream izlemeleri istediğiniz ve seçin sağ hello düğümünü **görünüm akış izlemeleri**
   
    ![İzlemeler akış uzak görünümü][viewremotestreamingtraces]
   
    Toosee izlemeleri istediğiniz sayıda düğümleri için 2. adımı yineleyin. Her düğüm akış adanmış bir pencerede gösterir.
   
    Service Fabric ve hizmetlerinizi tarafından gösterilen mümkün toosee hello izlemeleri sunulmuştur. Belirli bir uygulama toofilter hello olayları tooonly Göster istiyorsanız, yalnızca hello hello filtresi hello uygulamanın adını yazın.
   
    ![İzlemeler akış görüntüleme][viewingstreamingtraces]
3. Akış izlemeleri kümenizden tamamladıktan sonra uzak akış izlemeleri hello kümede sağ tıklayarak devre dışı bırakabilirsiniz **Cloud Explorer** ve **akış izlemelerini devre dışı bırak**
   
    ![Uzak akış izlemelerini devre dışı bırak][disablestreamingtraces]

## <a name="next-steps"></a>Sonraki adımlar
* [Service Fabric hizmeti test](service-fabric-testability-overview.md).
* [Visual Studio'da, Service Fabric uygulamaları yönetmek](service-fabric-manage-application-in-visual-studio.md).

<!--Image references-->
[startdebugging]: ./media/service-fabric-debugging-your-application/startdebugging.png
[diagnosticevents]: ./media/service-fabric-debugging-your-application/diagnosticevents.png
[viewdiagnosticevents]: ./media/service-fabric-debugging-your-application/viewdiagnosticevents.png
[diagnosticeventsactions]: ./media/service-fabric-debugging-your-application/diagnosticeventsactions.png
[breakpoint]: ./media/service-fabric-debugging-your-application/breakpoint.png
[enableremotedebugging]: ./media/service-fabric-debugging-your-application/enableremotedebugging.png
[attachdebugger]: ./media/service-fabric-debugging-your-application/attachdebugger.png
[chooseprocess]: ./media/service-fabric-debugging-your-application/chooseprocess.png
[conditionalbreakpoint]: ./media/service-fabric-debugging-your-application/conditionalbreakpoint.png
[disableremotedebugging]: ./media/service-fabric-debugging-your-application/disableremotedebugging.png
[enablestreamingtraces]: ./media/service-fabric-debugging-your-application/enablestreamingtraces.png
[viewingstreamingtraces]: ./media/service-fabric-debugging-your-application/viewingstreamingtraces.png
[viewremotestreamingtraces]: ./media/service-fabric-debugging-your-application/viewremotestreamingtraces.png
[disablestreamingtraces]: ./media/service-fabric-debugging-your-application/disablestreamingtraces.png
