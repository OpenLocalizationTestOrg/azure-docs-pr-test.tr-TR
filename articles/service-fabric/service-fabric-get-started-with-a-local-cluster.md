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
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a><span data-ttu-id="6799f-103">Yerel kümenizdeki uygulamaları dağıtma ve yükseltme işlemlerine giriş</span><span class="sxs-lookup"><span data-stu-id="6799f-103">Get started with deploying and upgrading applications on your local cluster</span></span>
<span data-ttu-id="6799f-104">Hello Azure Service Fabric SDK kullanabileceğiniz tam yerel geliştirme ortamı içerir tooquickly yerel bir kümede uygulamaları dağıtma ve yönetme ile çalışmaya başlama.</span><span class="sxs-lookup"><span data-stu-id="6799f-104">hello Azure Service Fabric SDK includes a full local development environment that you can use tooquickly get started with deploying and managing applications on a local cluster.</span></span> <span data-ttu-id="6799f-105">Bu makalede, yerel bir küme oluşturup, var olan bir uygulama tooit dağıtmak ve bu uygulama tooa yeni sürümü, Windows PowerShell tümünden yükseltin.</span><span class="sxs-lookup"><span data-stu-id="6799f-105">In this article, you create a local cluster, deploy an existing application tooit, and then upgrade that application tooa new version, all from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="6799f-106">Bu makale [geliştirme ortamınızı daha önceden ayarladığınızı](service-fabric-get-started.md) varsayar.</span><span class="sxs-lookup"><span data-stu-id="6799f-106">This article assumes that you already [set up your development environment](service-fabric-get-started.md).</span></span>
> 
> 

## <a name="create-a-local-cluster"></a><span data-ttu-id="6799f-107">Yerel bir küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="6799f-107">Create a local cluster</span></span>
<span data-ttu-id="6799f-108">Service Fabric kümesi, uygulamaları dağıtabileceğiniz bir dizi donanım kaynağını ifade eder.</span><span class="sxs-lookup"><span data-stu-id="6799f-108">A Service Fabric cluster represents a set of hardware resources that you can deploy applications to.</span></span> <span data-ttu-id="6799f-109">Genellikle, bir küme herhangi bir yere beş toomany makinelerin binlerce oluşur.</span><span class="sxs-lookup"><span data-stu-id="6799f-109">Typically, a cluster is made up of anywhere from five toomany thousands of machines.</span></span> <span data-ttu-id="6799f-110">Ancak, hello Service Fabric SDK tek bir makinede çalışabilen küme yapılandırması içerir.</span><span class="sxs-lookup"><span data-stu-id="6799f-110">However, hello Service Fabric SDK includes a cluster configuration that can run on a single machine.</span></span>

<span data-ttu-id="6799f-111">Service Fabric yerel kümesinin hello toounderstand bir öykünücü veya benzetici değil önemlidir.</span><span class="sxs-lookup"><span data-stu-id="6799f-111">It is important toounderstand that hello Service Fabric local cluster is not an emulator or simulator.</span></span> <span data-ttu-id="6799f-112">Bunu hello çoklu makine kümelerinde bulunan aynı platform kodu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="6799f-112">It runs hello same platform code that is found on multi-machine clusters.</span></span> <span data-ttu-id="6799f-113">Merhaba tek fark, normalde beş makineye tek bir makinede arasında yayılır hello platform işlemlerini çalıştığını olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="6799f-113">hello only difference is that it runs hello platform processes that are normally spread across five machines on one machine.</span></span>

<span data-ttu-id="6799f-114">Merhaba SDK iki yolu tooset yerel kümesi sağlar: bir Windows PowerShell komut dosyası ve hello yerel Küme Yöneticisi sistemi Tepsisi uygulaması.</span><span class="sxs-lookup"><span data-stu-id="6799f-114">hello SDK provides two ways tooset up a local cluster: a Windows PowerShell script and hello Local Cluster Manager system tray app.</span></span> <span data-ttu-id="6799f-115">Bu öğreticide, hello PowerShell betiğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="6799f-115">In this tutorial, we use hello PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="6799f-116">Visual Studio'dan bir uygulama dağıtarak zaten bir yerel küme oluşturduysanız bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6799f-116">If you have already created a local cluster by deploying an application from Visual Studio, you can skip this section.</span></span>
> 
> 

1. <span data-ttu-id="6799f-117">Yönetici olarak yeni bir PowerShell penceresi başlatın.</span><span class="sxs-lookup"><span data-stu-id="6799f-117">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="6799f-118">Merhaba Küme kurulumu betiğini hello SDK klasöründen çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6799f-118">Run hello cluster setup script from hello SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    <span data-ttu-id="6799f-119">Küme kurulumu biraz zaman alır.</span><span class="sxs-lookup"><span data-stu-id="6799f-119">Cluster setup takes a few moments.</span></span> <span data-ttu-id="6799f-120">Kurulum tamamlandıktan sonra şunun gibi görünen bir çıktı görmelisiniz:</span><span class="sxs-lookup"><span data-stu-id="6799f-120">After setup is finished, you should see output similar to:</span></span>
   
    ![Küme kurulumu çıktısı][cluster-setup-success]
   
    <span data-ttu-id="6799f-122">Bir uygulama tooyour kümesi dağıtma hazır tootry sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="6799f-122">You are now ready tootry deploying an application tooyour cluster.</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="6799f-123">Uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="6799f-123">Deploy an application</span></span>
<span data-ttu-id="6799f-124">Merhaba Service Fabric SDK çerçeveler ve geliştirici araçları uygulamaları oluşturmak için zengin bir dizi içerir.</span><span class="sxs-lookup"><span data-stu-id="6799f-124">hello Service Fabric SDK includes a rich set of frameworks and developer tooling for creating applications.</span></span> <span data-ttu-id="6799f-125">Visual Studio'da toocreate uygulamaları nasıl görürüm öğrenmede ilgileniyorsanız [Visual Studio'da ilk Service Fabric uygulamanızı oluşturma](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="6799f-125">If you are interested in learning how toocreate applications in Visual Studio, see [Create your first Service Fabric application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>

<span data-ttu-id="6799f-126">Bu öğreticide, üzerinde hello platform hello yönetim özelliklerine odaklanabiliriz (WordCount olarak adlandırılır) var olan bir örnek uygulamasını kullanın: dağıtım, izleme ve yükseltme.</span><span class="sxs-lookup"><span data-stu-id="6799f-126">In this tutorial, you use an existing sample application (called WordCount) so that you can focus on hello management aspects of hello platform: deployment, monitoring, and upgrade.</span></span>

1. <span data-ttu-id="6799f-127">Yönetici olarak yeni bir PowerShell penceresi başlatın.</span><span class="sxs-lookup"><span data-stu-id="6799f-127">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="6799f-128">Merhaba Service Fabric SDK PowerShell modülünü içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="6799f-128">Import hello Service Fabric SDK PowerShell module.</span></span>
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. <span data-ttu-id="6799f-129">Karşıdan yükleme ve dağıtma, C:\ServiceFabric gibi bir dizin toostore hello uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6799f-129">Create a directory toostore hello application that you download and deploy, such as C:\ServiceFabric.</span></span>
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. <span data-ttu-id="6799f-130">[Merhaba WordCount uygulamasını indirin](http://aka.ms/servicefabric-wordcountapp) oluşturduğunuz toohello konumu.</span><span class="sxs-lookup"><span data-stu-id="6799f-130">[Download hello WordCount application](http://aka.ms/servicefabric-wordcountapp) toohello location you created.</span></span>  <span data-ttu-id="6799f-131">Not: hello Microsoft Edge tarayıcısının hello dosyasıyla kaydeder. bir *.zip* uzantısı.</span><span class="sxs-lookup"><span data-stu-id="6799f-131">Note: hello Microsoft Edge browser saves hello file with a *.zip* extension.</span></span>  <span data-ttu-id="6799f-132">Merhaba dosya uzantısını da değiştirmem*.sfpkg*.</span><span class="sxs-lookup"><span data-stu-id="6799f-132">Change hello file extension too*.sfpkg*.</span></span>
5. <span data-ttu-id="6799f-133">Toohello yerel kümeye bağlanın:</span><span class="sxs-lookup"><span data-stu-id="6799f-133">Connect toohello local cluster:</span></span>
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. <span data-ttu-id="6799f-134">Bir ad ve yol toohello uygulama paketi Hello SDK dağıtımı komutunu kullanarak yeni bir uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6799f-134">Create a new application using hello SDK's deployment command with a name and a path toohello application package.</span></span>
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="6799f-135">Tüm kalırsa de, çıktı aşağıdaki hello görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="6799f-135">If all goes well, you should see hello following output:</span></span>
   
    ![Bir uygulama toohello yerel kümeyi dağıtma][deploy-app-to-local-cluster]
7. <span data-ttu-id="6799f-137">Eylem toosee hello uygulama başlatma hello tarayıcı ve çok gidin[http://localhost: 8081/WordCount/index.HTML](http://localhost:8081/wordcount/index.html).</span><span class="sxs-lookup"><span data-stu-id="6799f-137">toosee hello application in action, launch hello browser and navigate too[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span></span> <span data-ttu-id="6799f-138">Şunu görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="6799f-138">You should see:</span></span>
   
    ![Dağıtılan uygulama kullanıcı arabirimi][deployed-app-ui]
   
    <span data-ttu-id="6799f-140">Merhaba WordCount uygulamasını basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="6799f-140">hello WordCount application is simple.</span></span> <span data-ttu-id="6799f-141">İstemci tarafı JavaScript kodu toogenerate rastgele beş karakterli "sözcükler" içeren olan toohello uygulamayı ASP.NET Web API aracılığıyla geçişli.</span><span class="sxs-lookup"><span data-stu-id="6799f-141">It includes client-side JavaScript code toogenerate random five-character "words", which are then relayed toohello application via ASP.NET Web API.</span></span> <span data-ttu-id="6799f-142">Durum bilgisi olan hizmet sayılan sözcükler hello sayısını izler.</span><span class="sxs-lookup"><span data-stu-id="6799f-142">A stateful service tracks hello number of words counted.</span></span> <span data-ttu-id="6799f-143">Bunlar, hello word'ün hello ilk karakterine bağlı bölümlenir.</span><span class="sxs-lookup"><span data-stu-id="6799f-143">They are partitioned based on hello first character of hello word.</span></span> <span data-ttu-id="6799f-144">Merhaba hello WordCount uygulaması hello kaynak kodu bulabilirsiniz [Klasik Başlarken örnekleri](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span><span class="sxs-lookup"><span data-stu-id="6799f-144">You can find hello source code for hello WordCount app in hello [classic getting started samples](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span></span>
   
    <span data-ttu-id="6799f-145">dağıttığımız hello uygulama dört bölüm içerir.</span><span class="sxs-lookup"><span data-stu-id="6799f-145">hello application that we deployed contains four partitions.</span></span> <span data-ttu-id="6799f-146">A ile G arasında olan kelimeler hello ilk bölümünde depolanır şekilde karakteri h ile N arasında olan kelimeler hello ikinci bölümü vb. depolanır.</span><span class="sxs-lookup"><span data-stu-id="6799f-146">So words beginning with A through G are stored in hello first partition, words beginning with H through N are stored in hello second partition, and so on.</span></span>

## <a name="view-application-details-and-status"></a><span data-ttu-id="6799f-147">Uygulama bilgilerini ve durumu görüntüleme</span><span class="sxs-lookup"><span data-stu-id="6799f-147">View application details and status</span></span>
<span data-ttu-id="6799f-148">Merhaba uygulaması dağıtmış olan, bazı PowerShell hello uygulama ayrıntıları bakalım.</span><span class="sxs-lookup"><span data-stu-id="6799f-148">Now that we have deployed hello application, let's look at some of hello app details in PowerShell.</span></span>

1. <span data-ttu-id="6799f-149">Merhaba kümedeki tüm dağıtılan uygulamaları sorgulayın:</span><span class="sxs-lookup"><span data-stu-id="6799f-149">Query all deployed applications on hello cluster:</span></span>
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    <span data-ttu-id="6799f-150">Yalnızca hello WordCount uygulamasını dağıttığınızı varsayarsak, benzer bir şey bakın:</span><span class="sxs-lookup"><span data-stu-id="6799f-150">Assuming that you have only deployed hello WordCount app, you see something similar to:</span></span>
   
    ![PowerShell'deki dağıtılan uygulamaların tümünü sorgulama][ps-getsfapp]
2. <span data-ttu-id="6799f-152">Merhaba WordCount uygulamasında bulunan Hizmetler hello kümesini sorgulayarak toohello sonraki düzeye gidin.</span><span class="sxs-lookup"><span data-stu-id="6799f-152">Go toohello next level by querying hello set of services that are included in hello WordCount application.</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![PowerShell hello uygulamaya ait hizmetleri listeleme][ps-getsfsvc]
   
    <span data-ttu-id="6799f-154">Merhaba uygulaması, iki hizmet, hello web ön uç ve hello sözcükleri yöneten durum bilgisi olan hizmet hello yapılır.</span><span class="sxs-lookup"><span data-stu-id="6799f-154">hello application is made up of two services, hello web front end, and hello stateful service that manages hello words.</span></span>
3. <span data-ttu-id="6799f-155">Son olarak, WordCountService için bölümlerin hello listesine bakın:</span><span class="sxs-lookup"><span data-stu-id="6799f-155">Finally, look at hello list of partitions for WordCountService:</span></span>
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![PowerShell'de Hello hizmet bölümlerini görüntüleme][ps-getsfpartitions]
   
    <span data-ttu-id="6799f-157">Tüm Service Fabric PowerShell komutları gibi kullanılan komutlar kümesi Merhaba, yerel veya uzak için bağlanmak isteyebileceğiniz herhangi bir küme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6799f-157">hello set of commands that you used, like all Service Fabric PowerShell commands, are available for any cluster that you might connect to, local or remote.</span></span>
   
    <span data-ttu-id="6799f-158">Merhaba kümesi ile daha görsel bir şekilde toointeract için çok giderek hello web tabanlı Service Fabric Explorer aracını kullanabilirsiniz[http://localhost: 19080/Explorer](http://localhost:19080/Explorer) hello tarayıcıda.</span><span class="sxs-lookup"><span data-stu-id="6799f-158">For a more visual way toointeract with hello cluster, you can use hello web-based Service Fabric Explorer tool by navigating too[http://localhost:19080/Explorer](http://localhost:19080/Explorer) in hello browser.</span></span>
   
    ![Service Fabric Explorer'da uygulama bilgilerini görüntüleme][sfx-service-overview]
   
   > [!NOTE]
   > <span data-ttu-id="6799f-160">Service Fabric Explorer hakkında daha fazla toolearn bkz [Service Fabric Explorer ile kümenizi görselleştirme](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="6799f-160">toolearn more about Service Fabric Explorer, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
   > 
   > 

## <a name="upgrade-an-application"></a><span data-ttu-id="6799f-161">Uygulama yükseltme</span><span class="sxs-lookup"><span data-stu-id="6799f-161">Upgrade an application</span></span>
<span data-ttu-id="6799f-162">Service Fabric hello kümede yapar gibi hello uygulama hello durumunu izleme yok ve kapalı kalma süresi yükseltmeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="6799f-162">Service Fabric provides no-downtime upgrades by monitoring hello health of hello application as it rolls out across hello cluster.</span></span> <span data-ttu-id="6799f-163">Merhaba WordCount uygulamasını yükseltme gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="6799f-163">Perform an upgrade of hello WordCount application.</span></span>

<span data-ttu-id="6799f-164">Şimdi hello uygulamanın yeni sürümü Hello yalnızca sesli bir harfle başlayan sözcükleri sayar.</span><span class="sxs-lookup"><span data-stu-id="6799f-164">hello new version of hello application now counts only words that begin with a vowel.</span></span> <span data-ttu-id="6799f-165">Merhaba yükseltme uygulanırken gibi biz hello uygulamanın davranışında iki değişiklik bakın.</span><span class="sxs-lookup"><span data-stu-id="6799f-165">As hello upgrade rolls out, we see two changes in hello application's behavior.</span></span> <span data-ttu-id="6799f-166">Daha az sözcük sayıldığından ilk olarak, hangi hello sayaç büyümesinin hello hızı azalacaktır.</span><span class="sxs-lookup"><span data-stu-id="6799f-166">First, hello rate at which hello count grows should slow, since fewer words are being counted.</span></span> <span data-ttu-id="6799f-167">İkinci olarak, hello ilk bölüm iki sesli harf (A ve E) vardır ve diğer tüm bölümler yalnızca birini içeren beri sayımına sonunda toooutpace hello başkalarının başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6799f-167">Second, since hello first partition has two vowels (A and E) and all other partitions contain only one each, its count should eventually start toooutpace hello others.</span></span>

1. <span data-ttu-id="6799f-168">[Merhaba WordCount sürüm 2 paketini indirin](http://aka.ms/servicefabric-wordcountappv2) toohello hello sürüm 1 paketini indirdiğiniz aynı konumu.</span><span class="sxs-lookup"><span data-stu-id="6799f-168">[Download hello WordCount version 2 package](http://aka.ms/servicefabric-wordcountappv2) toohello same location where you downloaded hello version 1 package.</span></span>
2. <span data-ttu-id="6799f-169">Tooyour PowerShell penceresine dönün ve tooregister hello hello küme yeni sürümde hello SDK'ın yükseltme komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="6799f-169">Return tooyour PowerShell window and use hello SDK's upgrade command tooregister hello new version in hello cluster.</span></span> <span data-ttu-id="6799f-170">Hello doku yükseltme başlayın: / WordCount uygulamasını.</span><span class="sxs-lookup"><span data-stu-id="6799f-170">Then begin upgrading hello fabric:/WordCount application.</span></span>
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    <span data-ttu-id="6799f-171">PowerShell'de yükseltme hello gibi çıktı hello aşağıdaki başlar görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6799f-171">You should see hello following output in PowerShell as hello upgrade begins.</span></span>
   
    ![PowerShell'de yükseltme süreci][ps-appupgradeprogress]
3. <span data-ttu-id="6799f-173">Merhaba yükseltme devam ederken, daha kolay toomonitor bulabilirsiniz durumunu Service Fabric Explorer'dan.</span><span class="sxs-lookup"><span data-stu-id="6799f-173">While hello upgrade is proceeding, you may find it easier toomonitor its status from Service Fabric Explorer.</span></span> <span data-ttu-id="6799f-174">Bir tarayıcı penceresi başlatın ve çok gidin[http://localhost: 19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="6799f-174">Launch a browser window and navigate too[http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="6799f-175">Genişletin **uygulamaları** hello soldaki hello ağacında ardından **WordCount**ve son olarak **fabric: / WordCount**.</span><span class="sxs-lookup"><span data-stu-id="6799f-175">Expand **Applications** in hello tree on hello left, then choose **WordCount**, and finally **fabric:/WordCount**.</span></span> <span data-ttu-id="6799f-176">Merhaba kümenin yükseltme etki alanlarında ilerlerken ettikçe hello temel bilgiler sekmesinde hello yükseltme hello durumunu görebilir.</span><span class="sxs-lookup"><span data-stu-id="6799f-176">In hello essentials tab, you see hello status of hello upgrade as it proceeds through hello cluster's upgrade domains.</span></span>
   
    ![Service Fabric Explorer'da yükseltme süreci][sfx-upgradeprogress]
   
    <span data-ttu-id="6799f-178">Hello yükseltme her bir etki alanı devam ettikçe, sistem durumu denetimleri hello uygulamanın uygun şekilde davrandığından gerçekleştirilen tooensure verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6799f-178">As hello upgrade proceeds through each domain, health checks are performed tooensure that hello application is behaving properly.</span></span>
4. <span data-ttu-id="6799f-179">Merhaba yeniden çalıştırın, daha önce sorgu hello doku Hizmetleri'nde hello kümesi: / WordCount uygulamasını WordCountService sürümü değişti hello ancak WordCountWebService sürümünün hello bildirimi belirtmiyor:</span><span class="sxs-lookup"><span data-stu-id="6799f-179">If you rerun hello earlier query for hello set of services in hello fabric:/WordCount application, notice that hello WordCountService version changed but hello WordCountWebService version did not:</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Yükseltme işleminden sonra uygulama hizmetlerini sorgulama][ps-getsfsvc-postupgrade]
   
    <span data-ttu-id="6799f-181">Bu örnekte Service Fabric hizmetinin uygulama yükseltmelerini yönetme şekli vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="6799f-181">This example highlights how Service Fabric manages application upgrades.</span></span> <span data-ttu-id="6799f-182">Bu, daha hızlı ve daha güvenilir yükseltme işleminin hello kılan değişen, yalnızca hello kümesi Hizmetleri (veya bu hizmetlerin içindeki kod/yapılandırma paketleri) ele alınır.</span><span class="sxs-lookup"><span data-stu-id="6799f-182">It touches only hello set of services (or code/configuration packages within those services) that have changed, which makes hello process of upgrading faster and more reliable.</span></span>
5. <span data-ttu-id="6799f-183">Son olarak, toohello tarayıcı tooobserve hello hello yeni uygulama sürümünün davranışını döndürür.</span><span class="sxs-lookup"><span data-stu-id="6799f-183">Finally, return toohello browser tooobserve hello behavior of hello new application version.</span></span> <span data-ttu-id="6799f-184">Beklendiği gibi sayısı ilerledikçe daha yavaş hello ve hello ilk bölüm kısmen daha fazla hello birim ile sona erer.</span><span class="sxs-lookup"><span data-stu-id="6799f-184">As expected, hello count progresses more slowly, and hello first partition ends up with slightly more of hello volume.</span></span>
   
    ![Görünüm hello uygulamanın yeni sürümü hello hello tarayıcıda][deployed-app-ui-v2]

## <a name="cleaning-up"></a><span data-ttu-id="6799f-186">Temizleme</span><span class="sxs-lookup"><span data-stu-id="6799f-186">Cleaning up</span></span>
<span data-ttu-id="6799f-187">Sonlandırmadan önce yerel küme hello tooremember gerçek önemlidir.</span><span class="sxs-lookup"><span data-stu-id="6799f-187">Before wrapping up, it's important tooremember that hello local cluster is real.</span></span> <span data-ttu-id="6799f-188">Siz kaldırana kadar uygulamaları toorun hello arka planda devam eder.</span><span class="sxs-lookup"><span data-stu-id="6799f-188">Applications continue toorun in hello background until you remove them.</span></span>  <span data-ttu-id="6799f-189">Uygulamalarınızın Hello yapısına bağlı olarak, çalışan bir uygulamanın makinenizde önemli kaynakları alabilir.</span><span class="sxs-lookup"><span data-stu-id="6799f-189">Depending on hello nature of your apps, a running app can take up significant resources on your machine.</span></span> <span data-ttu-id="6799f-190">Çeşitli seçenekler toomanage uygulamaları ve hello küme vardır:</span><span class="sxs-lookup"><span data-stu-id="6799f-190">You have several options toomanage applications and hello cluster:</span></span>

1. <span data-ttu-id="6799f-191">tooremove tek bir uygulamayı ve tüm, kullanıcının verileri, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6799f-191">tooremove an individual application and all it's data, run hello following command:</span></span>
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="6799f-192">Veya, Service Fabric Explorer hello hello uygulamayı silmek **Eylemler** menüsü veya hello hello sol uygulama listesi görünümündeki bağlam menüsü.</span><span class="sxs-lookup"><span data-stu-id="6799f-192">Or, delete hello application from hello Service Fabric Explorer **ACTIONS** menu or hello context menu in hello left-hand application list view.</span></span>
   
    ![Service Fabric Explorer'da uygulama silme][sfe-delete-application]
2. <span data-ttu-id="6799f-194">Merhaba uygulaması hello kümeden sildikten sonra 1.0.0 ve hello WordCount uygulama türü 2.0.0 sürümleri kaydını silin.</span><span class="sxs-lookup"><span data-stu-id="6799f-194">After deleting hello application from hello cluster, unregister versions 1.0.0 and 2.0.0 of hello WordCount application type.</span></span> <span data-ttu-id="6799f-195">Silme hello kodu ve yapılandırmasından hello kümenin görüntü deposu dahil olmak üzere hello uygulama paketleri kaldırır.</span><span class="sxs-lookup"><span data-stu-id="6799f-195">Deletion removes hello application packages, including hello code and configuration, from hello cluster's image store.</span></span>
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    <span data-ttu-id="6799f-196">Veya, Service Fabric Explorer'da seçin **sağlamayı kaldırma türü** Merhaba uygulaması için.</span><span class="sxs-lookup"><span data-stu-id="6799f-196">Or, in Service Fabric Explorer, choose **Unprovision Type** for hello application.</span></span>
3. <span data-ttu-id="6799f-197">Merhaba küme ancak Koru hello uygulama verilerini ve izlemelerini, aşağı tooshut tıklatın **yerel kümeyi Durdur** hello sistem tepsisi uygulamasında.</span><span class="sxs-lookup"><span data-stu-id="6799f-197">tooshut down hello cluster but keep hello application data and traces, click **Stop Local Cluster** in hello system tray app.</span></span>
4. <span data-ttu-id="6799f-198">toodelete hello küme tamamen tıklatın **yerel kümeyi Kaldır** hello sistem tepsisi uygulamasında.</span><span class="sxs-lookup"><span data-stu-id="6799f-198">toodelete hello cluster entirely, click **Remove Local Cluster** in hello system tray app.</span></span> <span data-ttu-id="6799f-199">Bu seçenek başka bir yavaş dağıtımla hello açtığınızda Visual Studio'da F5'e basın neden olur.</span><span class="sxs-lookup"><span data-stu-id="6799f-199">This option will result in another slow deployment hello next time you press F5 in Visual Studio.</span></span> <span data-ttu-id="6799f-200">Yalnızca toouse planlamıyorsanız hello yerel küme için biraz zaman veya tooreclaim kaynakları ihtiyacınız varsa kaldırın.</span><span class="sxs-lookup"><span data-stu-id="6799f-200">Remove hello local cluster only if you don't intend toouse it for some time or if you need tooreclaim resources.</span></span>

## <a name="one-node-and-five-node-cluster-mode"></a><span data-ttu-id="6799f-201">Tek düğümlü ve beş düğümlü küme modu</span><span class="sxs-lookup"><span data-stu-id="6799f-201">One-node and five-node cluster mode</span></span>
<span data-ttu-id="6799f-202">Uygulama geliştirirken çoğunlukla kendinizi kod yazma, hata ayıklama, kod değiştirme ve hata ayıklama işlemlerini yinelerken bulursunuz.</span><span class="sxs-lookup"><span data-stu-id="6799f-202">When developing applications, you often find yourself doing quick iterations of writing code, debugging, changing code, and debugging.</span></span> <span data-ttu-id="6799f-203">toohelp, bu işlem en iyi duruma, hello yerel küme, iki modda çalışabilir: tek düğümlü veya beş düğümlü.</span><span class="sxs-lookup"><span data-stu-id="6799f-203">toohelp optimize this process, hello local cluster can run in two modes: one-node or five-node.</span></span> <span data-ttu-id="6799f-204">Her iki küme modunun da faydaları vardır.</span><span class="sxs-lookup"><span data-stu-id="6799f-204">Both cluster modes have their benefits.</span></span> <span data-ttu-id="6799f-205">Beş düğümlü kümeyi modu gerçek bir kümeyle toowork sağlar.</span><span class="sxs-lookup"><span data-stu-id="6799f-205">Five-node cluster mode enables you toowork with a real cluster.</span></span> <span data-ttu-id="6799f-206">Yük devretme senaryolarını test edebilir, hizmetlerinizin daha fazla örneği ve yinelemeleri ile çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6799f-206">You can test failover scenarios, work with more instances and replicas of your services.</span></span> <span data-ttu-id="6799f-207">Tek düğümlü kümenize en iyi duruma getirilmiş toodo hızlı dağıtım ve kayıt toohelp hızlı bir şekilde hello Service Fabric çalışma zamanı kullanarak kod doğrulama hizmetlerinin modudur.</span><span class="sxs-lookup"><span data-stu-id="6799f-207">One-node cluster mode is optimized toodo quick deployment and registration of services, toohelp you quickly validate code using hello Service Fabric runtime.</span></span>

<span data-ttu-id="6799f-208">Tek düğümlü küme de beş düğümlü küme de öykünücü veya benzetici değildir.</span><span class="sxs-lookup"><span data-stu-id="6799f-208">Neither one-node cluster or five-node cluster modes are an emulator or simulator.</span></span> <span data-ttu-id="6799f-209">Merhaba yerel geliştirme küme çalıştırmaları hello çoklu makine kümelerinde bulunan aynı platform kodu.</span><span class="sxs-lookup"><span data-stu-id="6799f-209">hello local development cluster runs hello same platform code that is found on multi-machine clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="6799f-210">Merhaba küme modu değiştirdiğinizde, hello geçerli küme sisteminizden kaldırılır ve yeni bir küme oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6799f-210">When you change hello cluster mode, hello current cluster is removed from your system and a new cluster is created.</span></span> <span data-ttu-id="6799f-211">küme modu değiştirdiğinizde hello kümesinde depolanan hello verileri silinir.</span><span class="sxs-lookup"><span data-stu-id="6799f-211">hello data stored in hello cluster is deleted when you change cluster mode.</span></span>
> 
> 

<span data-ttu-id="6799f-212">toochange hello modu tooone düğümlü bir küme, select **anahtar küme modu** hello Service Fabric yerel Küme Yöneticisi olarak.</span><span class="sxs-lookup"><span data-stu-id="6799f-212">toochange hello mode tooone-node cluster, select **Switch Cluster Mode** in hello Service Fabric Local Cluster Manager.</span></span>

![Küme moduna geçme][switch-cluster-mode]

<span data-ttu-id="6799f-214">Veya PowerShell kullanarak hello küme modunu değiştirin:</span><span class="sxs-lookup"><span data-stu-id="6799f-214">Or, change hello cluster mode using PowerShell:</span></span>

1. <span data-ttu-id="6799f-215">Yönetici olarak yeni bir PowerShell penceresi başlatın.</span><span class="sxs-lookup"><span data-stu-id="6799f-215">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="6799f-216">Merhaba Küme kurulumu betiğini hello SDK klasöründen çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6799f-216">Run hello cluster setup script from hello SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    <span data-ttu-id="6799f-217">Küme kurulumu biraz zaman alır.</span><span class="sxs-lookup"><span data-stu-id="6799f-217">Cluster setup takes a few moments.</span></span> <span data-ttu-id="6799f-218">Kurulum tamamlandıktan sonra şunun gibi görünen bir çıktı görmelisiniz:</span><span class="sxs-lookup"><span data-stu-id="6799f-218">After setup is finished, you should see output similar to:</span></span>
   
    ![Küme kurulumu çıktısı][cluster-setup-success-1-node]

## <a name="next-steps"></a><span data-ttu-id="6799f-220">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6799f-220">Next steps</span></span>
* <span data-ttu-id="6799f-221">Önceden derlenen bazı uygulamaları dağıtıp geliştirdiğinize göre [Visual Studio'da kendi uygulamanızı derlemeyi deneyebilirsiniz](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="6799f-221">Now that you have deployed and upgraded some pre-built applications, you can [try building your own in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>
* <span data-ttu-id="6799f-222">Bu makalede hello yerel kümede gerçekleştirilen tüm hello eylemler gerçekleştirilebilir bir [Azure küme](service-fabric-cluster-creation-via-portal.md) de.</span><span class="sxs-lookup"><span data-stu-id="6799f-222">All hello actions performed on hello local cluster in this article can be performed on an [Azure cluster](service-fabric-cluster-creation-via-portal.md) as well.</span></span>
* <span data-ttu-id="6799f-223">Biz bu makalede gerçekleştirilen hello yükseltme temel.</span><span class="sxs-lookup"><span data-stu-id="6799f-223">hello upgrade that we performed in this article was basic.</span></span> <span data-ttu-id="6799f-224">Merhaba bkz [yükseltme belgelerine](service-fabric-application-upgrade.md) toolearn hello gücü ve esnekliği Service Fabric yükseltmelerinin hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="6799f-224">See hello [upgrade documentation](service-fabric-application-upgrade.md) toolearn more about hello power and flexibility of Service Fabric upgrades.</span></span>

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
