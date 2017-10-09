---
title: "aaaDeploy ve yerel olarak Azure mikro yükseltme | Microsoft Docs"
description: "Nasıl tooset yerel Service Fabric kümesi, var olan bir uygulama tooit dağıtın ve ardından uygulamayı yükseltin öğrenin."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 60a1f6a5-5478-46c0-80a8-18fe62da17a8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi;mikhegn
ms.openlocfilehash: e5f5adc9edb71433b2a7635e9d661ff92a4b18ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a>Yerel kümenizdeki uygulamaları dağıtma ve yükseltme işlemlerine giriş
Hello Azure Service Fabric SDK kullanabileceğiniz tam yerel geliştirme ortamı içerir tooquickly yerel bir kümede uygulamaları dağıtma ve yönetme ile çalışmaya başlama. Bu makalede, yerel bir küme oluşturup, var olan bir uygulama tooit dağıtmak ve bu uygulama tooa yeni sürümü, Windows PowerShell tümünden yükseltin.

> [!NOTE]
> Bu makale [geliştirme ortamınızı daha önceden ayarladığınızı](service-fabric-get-started.md) varsayar.
> 
> 

## <a name="create-a-local-cluster"></a>Yerel bir küme oluşturma
Service Fabric kümesi, uygulamaları dağıtabileceğiniz bir dizi donanım kaynağını ifade eder. Genellikle, bir küme herhangi bir yere beş toomany makinelerin binlerce oluşur. Ancak, hello Service Fabric SDK tek bir makinede çalışabilen küme yapılandırması içerir.

Service Fabric yerel kümesinin hello toounderstand bir öykünücü veya benzetici değil önemlidir. Bunu hello çoklu makine kümelerinde bulunan aynı platform kodu çalıştırır. Merhaba tek fark, normalde beş makineye tek bir makinede arasında yayılır hello platform işlemlerini çalıştığını olmasıdır.

Merhaba SDK iki yolu tooset yerel kümesi sağlar: bir Windows PowerShell komut dosyası ve hello yerel Küme Yöneticisi sistemi Tepsisi uygulaması. Bu öğreticide, hello PowerShell betiğini kullanın.

> [!NOTE]
> Visual Studio'dan bir uygulama dağıtarak zaten bir yerel küme oluşturduysanız bu bölümü atlayabilirsiniz.
> 
> 

1. Yönetici olarak yeni bir PowerShell penceresi başlatın.
2. Merhaba Küme kurulumu betiğini hello SDK klasöründen çalıştırın:
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    Küme kurulumu biraz zaman alır. Kurulum tamamlandıktan sonra şunun gibi görünen bir çıktı görmelisiniz:
   
    ![Küme kurulumu çıktısı][cluster-setup-success]
   
    Bir uygulama tooyour kümesi dağıtma hazır tootry sunulmuştur.

## <a name="deploy-an-application"></a>Uygulama dağıtma
Merhaba Service Fabric SDK çerçeveler ve geliştirici araçları uygulamaları oluşturmak için zengin bir dizi içerir. Visual Studio'da toocreate uygulamaları nasıl görürüm öğrenmede ilgileniyorsanız [Visual Studio'da ilk Service Fabric uygulamanızı oluşturma](service-fabric-create-your-first-application-in-visual-studio.md).

Bu öğreticide, üzerinde hello platform hello yönetim özelliklerine odaklanabiliriz (WordCount olarak adlandırılır) var olan bir örnek uygulamasını kullanın: dağıtım, izleme ve yükseltme.

1. Yönetici olarak yeni bir PowerShell penceresi başlatın.
2. Merhaba Service Fabric SDK PowerShell modülünü içeri aktarın.
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. Karşıdan yükleme ve dağıtma, C:\ServiceFabric gibi bir dizin toostore hello uygulaması oluşturun.
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. [Merhaba WordCount uygulamasını indirin](http://aka.ms/servicefabric-wordcountapp) oluşturduğunuz toohello konumu.  Not: hello Microsoft Edge tarayıcısının hello dosyasıyla kaydeder. bir *.zip* uzantısı.  Merhaba dosya uzantısını da değiştirmem*.sfpkg*.
5. Toohello yerel kümeye bağlanın:
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. Bir ad ve yol toohello uygulama paketi Hello SDK dağıtımı komutunu kullanarak yeni bir uygulama oluşturun.
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    Tüm kalırsa de, çıktı aşağıdaki hello görmeniz gerekir:
   
    ![Bir uygulama toohello yerel kümeyi dağıtma][deploy-app-to-local-cluster]
7. Eylem toosee hello uygulama başlatma hello tarayıcı ve çok gidin[http://localhost: 8081/WordCount/index.HTML](http://localhost:8081/wordcount/index.html). Şunu görmeniz gerekir:
   
    ![Dağıtılan uygulama kullanıcı arabirimi][deployed-app-ui]
   
    Merhaba WordCount uygulamasını basit bir işlemdir. İstemci tarafı JavaScript kodu toogenerate rastgele beş karakterli "sözcükler" içeren olan toohello uygulamayı ASP.NET Web API aracılığıyla geçişli. Durum bilgisi olan hizmet sayılan sözcükler hello sayısını izler. Bunlar, hello word'ün hello ilk karakterine bağlı bölümlenir. Merhaba hello WordCount uygulaması hello kaynak kodu bulabilirsiniz [Klasik Başlarken örnekleri](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).
   
    dağıttığımız hello uygulama dört bölüm içerir. A ile G arasında olan kelimeler hello ilk bölümünde depolanır şekilde karakteri h ile N arasında olan kelimeler hello ikinci bölümü vb. depolanır.

## <a name="view-application-details-and-status"></a>Uygulama bilgilerini ve durumu görüntüleme
Merhaba uygulaması dağıtmış olan, bazı PowerShell hello uygulama ayrıntıları bakalım.

1. Merhaba kümedeki tüm dağıtılan uygulamaları sorgulayın:
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    Yalnızca hello WordCount uygulamasını dağıttığınızı varsayarsak, benzer bir şey bakın:
   
    ![PowerShell'deki dağıtılan uygulamaların tümünü sorgulama][ps-getsfapp]
2. Merhaba WordCount uygulamasında bulunan Hizmetler hello kümesini sorgulayarak toohello sonraki düzeye gidin.
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![PowerShell hello uygulamaya ait hizmetleri listeleme][ps-getsfsvc]
   
    Merhaba uygulaması, iki hizmet, hello web ön uç ve hello sözcükleri yöneten durum bilgisi olan hizmet hello yapılır.
3. Son olarak, WordCountService için bölümlerin hello listesine bakın:
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![PowerShell'de Hello hizmet bölümlerini görüntüleme][ps-getsfpartitions]
   
    Tüm Service Fabric PowerShell komutları gibi kullanılan komutlar kümesi Merhaba, yerel veya uzak için bağlanmak isteyebileceğiniz herhangi bir küme için kullanılabilir.
   
    Merhaba kümesi ile daha görsel bir şekilde toointeract için çok giderek hello web tabanlı Service Fabric Explorer aracını kullanabilirsiniz[http://localhost: 19080/Explorer](http://localhost:19080/Explorer) hello tarayıcıda.
   
    ![Service Fabric Explorer'da uygulama bilgilerini görüntüleme][sfx-service-overview]
   
   > [!NOTE]
   > Service Fabric Explorer hakkında daha fazla toolearn bkz [Service Fabric Explorer ile kümenizi görselleştirme](service-fabric-visualizing-your-cluster.md).
   > 
   > 

## <a name="upgrade-an-application"></a>Uygulama yükseltme
Service Fabric hello kümede yapar gibi hello uygulama hello durumunu izleme yok ve kapalı kalma süresi yükseltmeler sağlar. Merhaba WordCount uygulamasını yükseltme gerçekleştirin.

Şimdi hello uygulamanın yeni sürümü Hello yalnızca sesli bir harfle başlayan sözcükleri sayar. Merhaba yükseltme uygulanırken gibi biz hello uygulamanın davranışında iki değişiklik bakın. Daha az sözcük sayıldığından ilk olarak, hangi hello sayaç büyümesinin hello hızı azalacaktır. İkinci olarak, hello ilk bölüm iki sesli harf (A ve E) vardır ve diğer tüm bölümler yalnızca birini içeren beri sayımına sonunda toooutpace hello başkalarının başlamanız gerekir.

1. [Merhaba WordCount sürüm 2 paketini indirin](http://aka.ms/servicefabric-wordcountappv2) toohello hello sürüm 1 paketini indirdiğiniz aynı konumu.
2. Tooyour PowerShell penceresine dönün ve tooregister hello hello küme yeni sürümde hello SDK'ın yükseltme komutunu kullanın. Hello doku yükseltme başlayın: / WordCount uygulamasını.
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    PowerShell'de yükseltme hello gibi çıktı hello aşağıdaki başlar görmeniz gerekir.
   
    ![PowerShell'de yükseltme süreci][ps-appupgradeprogress]
3. Merhaba yükseltme devam ederken, daha kolay toomonitor bulabilirsiniz durumunu Service Fabric Explorer'dan. Bir tarayıcı penceresi başlatın ve çok gidin[http://localhost: 19080/Explorer](http://localhost:19080/Explorer). Genişletin **uygulamaları** hello soldaki hello ağacında ardından **WordCount**ve son olarak **fabric: / WordCount**. Merhaba kümenin yükseltme etki alanlarında ilerlerken ettikçe hello temel bilgiler sekmesinde hello yükseltme hello durumunu görebilir.
   
    ![Service Fabric Explorer'da yükseltme süreci][sfx-upgradeprogress]
   
    Hello yükseltme her bir etki alanı devam ettikçe, sistem durumu denetimleri hello uygulamanın uygun şekilde davrandığından gerçekleştirilen tooensure verilmiştir.
4. Merhaba yeniden çalıştırın, daha önce sorgu hello doku Hizmetleri'nde hello kümesi: / WordCount uygulamasını WordCountService sürümü değişti hello ancak WordCountWebService sürümünün hello bildirimi belirtmiyor:
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Yükseltme işleminden sonra uygulama hizmetlerini sorgulama][ps-getsfsvc-postupgrade]
   
    Bu örnekte Service Fabric hizmetinin uygulama yükseltmelerini yönetme şekli vurgulanır. Bu, daha hızlı ve daha güvenilir yükseltme işleminin hello kılan değişen, yalnızca hello kümesi Hizmetleri (veya bu hizmetlerin içindeki kod/yapılandırma paketleri) ele alınır.
5. Son olarak, toohello tarayıcı tooobserve hello hello yeni uygulama sürümünün davranışını döndürür. Beklendiği gibi sayısı ilerledikçe daha yavaş hello ve hello ilk bölüm kısmen daha fazla hello birim ile sona erer.
   
    ![Görünüm hello uygulamanın yeni sürümü hello hello tarayıcıda][deployed-app-ui-v2]

## <a name="cleaning-up"></a>Temizleme
Sonlandırmadan önce yerel küme hello tooremember gerçek önemlidir. Siz kaldırana kadar uygulamaları toorun hello arka planda devam eder.  Uygulamalarınızın Hello yapısına bağlı olarak, çalışan bir uygulamanın makinenizde önemli kaynakları alabilir. Çeşitli seçenekler toomanage uygulamaları ve hello küme vardır:

1. tooremove tek bir uygulamayı ve tüm, kullanıcının verileri, hello aşağıdaki komutu çalıştırın:
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    Veya, Service Fabric Explorer hello hello uygulamayı silmek **Eylemler** menüsü veya hello hello sol uygulama listesi görünümündeki bağlam menüsü.
   
    ![Service Fabric Explorer'da uygulama silme][sfe-delete-application]
2. Merhaba uygulaması hello kümeden sildikten sonra 1.0.0 ve hello WordCount uygulama türü 2.0.0 sürümleri kaydını silin. Silme hello kodu ve yapılandırmasından hello kümenin görüntü deposu dahil olmak üzere hello uygulama paketleri kaldırır.
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    Veya, Service Fabric Explorer'da seçin **sağlamayı kaldırma türü** Merhaba uygulaması için.
3. Merhaba küme ancak Koru hello uygulama verilerini ve izlemelerini, aşağı tooshut tıklatın **yerel kümeyi Durdur** hello sistem tepsisi uygulamasında.
4. toodelete hello küme tamamen tıklatın **yerel kümeyi Kaldır** hello sistem tepsisi uygulamasında. Bu seçenek başka bir yavaş dağıtımla hello açtığınızda Visual Studio'da F5'e basın neden olur. Yalnızca toouse planlamıyorsanız hello yerel küme için biraz zaman veya tooreclaim kaynakları ihtiyacınız varsa kaldırın.

## <a name="one-node-and-five-node-cluster-mode"></a>Tek düğümlü ve beş düğümlü küme modu
Uygulama geliştirirken çoğunlukla kendinizi kod yazma, hata ayıklama, kod değiştirme ve hata ayıklama işlemlerini yinelerken bulursunuz. toohelp, bu işlem en iyi duruma, hello yerel küme, iki modda çalışabilir: tek düğümlü veya beş düğümlü. Her iki küme modunun da faydaları vardır. Beş düğümlü kümeyi modu gerçek bir kümeyle toowork sağlar. Yük devretme senaryolarını test edebilir, hizmetlerinizin daha fazla örneği ve yinelemeleri ile çalışabilirsiniz. Tek düğümlü kümenize en iyi duruma getirilmiş toodo hızlı dağıtım ve kayıt toohelp hızlı bir şekilde hello Service Fabric çalışma zamanı kullanarak kod doğrulama hizmetlerinin modudur.

Tek düğümlü küme de beş düğümlü küme de öykünücü veya benzetici değildir. Merhaba yerel geliştirme küme çalıştırmaları hello çoklu makine kümelerinde bulunan aynı platform kodu.

> [!WARNING]
> Merhaba küme modu değiştirdiğinizde, hello geçerli küme sisteminizden kaldırılır ve yeni bir küme oluşturulur. küme modu değiştirdiğinizde hello kümesinde depolanan hello verileri silinir.
> 
> 

toochange hello modu tooone düğümlü bir küme, select **anahtar küme modu** hello Service Fabric yerel Küme Yöneticisi olarak.

![Küme moduna geçme][switch-cluster-mode]

Veya PowerShell kullanarak hello küme modunu değiştirin:

1. Yönetici olarak yeni bir PowerShell penceresi başlatın.
2. Merhaba Küme kurulumu betiğini hello SDK klasöründen çalıştırın:
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    Küme kurulumu biraz zaman alır. Kurulum tamamlandıktan sonra şunun gibi görünen bir çıktı görmelisiniz:
   
    ![Küme kurulumu çıktısı][cluster-setup-success-1-node]

## <a name="next-steps"></a>Sonraki adımlar
* Önceden derlenen bazı uygulamaları dağıtıp geliştirdiğinize göre [Visual Studio'da kendi uygulamanızı derlemeyi deneyebilirsiniz](service-fabric-create-your-first-application-in-visual-studio.md).
* Bu makalede hello yerel kümede gerçekleştirilen tüm hello eylemler gerçekleştirilebilir bir [Azure küme](service-fabric-cluster-creation-via-portal.md) de.
* Biz bu makalede gerçekleştirilen hello yükseltme temel. Merhaba bkz [yükseltme belgelerine](service-fabric-application-upgrade.md) toolearn hello gücü ve esnekliği Service Fabric yükseltmelerinin hakkında daha fazla bilgi.

<!-- Images -->

[cluster-setup-success]: ./media/service-fabric-get-started-with-a-local-cluster/LocalClusterSetup.png
[extracted-app-package]: ./media/service-fabric-get-started-with-a-local-cluster/ExtractedAppPackage.png
[deploy-app-to-local-cluster]: ./media/service-fabric-get-started-with-a-local-cluster/DeployAppToLocalCluster.png
[deployed-app-ui]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-v1.png
[deployed-app-ui-v2]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-PostUpgrade.png
[sfx-app-instance]: ./media/service-fabric-get-started-with-a-local-cluster/SfxAppInstance.png
[sfx-two-app-instances-different-partitions]: ./media/service-fabric-get-started-with-a-local-cluster/SfxTwoAppInstances-DifferentPartitionCount.png
[ps-getsfapp]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFApp.png
[ps-getsfsvc]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc.png
[ps-getsfpartitions]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFPartitions.png
[ps-appupgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/PS-AppUpgradeProgress.png
[ps-getsfsvc-postupgrade]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc-PostUpgrade.png
[sfx-upgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/SfxUpgradeOverview.png
[sfx-service-overview]: ./media/service-fabric-get-started-with-a-local-cluster/sfx-service-overview.png
[sfe-delete-application]: ./media/service-fabric-get-started-with-a-local-cluster/sfe-delete-application.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
[switch-cluster-mode]: ./media/service-fabric-get-started-with-a-local-cluster/switch-cluster-mode.png
