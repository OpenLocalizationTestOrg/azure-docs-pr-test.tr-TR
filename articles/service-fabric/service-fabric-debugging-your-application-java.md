---
title: "Azure Service Fabric uygulamanızı eclipse'te hata ayıklama | Microsoft Docs"
description: "Güvenilirliğini ve performansını hizmetlerinizi geliştirmek ve bunları Eclipse'te yerel geliştirme kümede hata ayıklama tarafından geliştirin."
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
ms.date: 02/10/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: f3bcee3794de35005bd387ecfae7e6707f3cb5ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a><span data-ttu-id="89f56-103">Java Service Fabric uygulamanızı Eclipse kullanarak hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="89f56-103">Debug your Java Service Fabric application using Eclipse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="89f56-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="89f56-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="89f56-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="89f56-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
> 

1. <span data-ttu-id="89f56-106">İçindeki adımları izleyerek yerel bir geliştirme kümesi Başlat [, Service Fabric geliştirme ortamını ayarlama](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="89f56-106">Start a local development cluster by following the steps in [Setting up your Service Fabric development environment](service-fabric-get-started-linux.md).</span></span>

2. <span data-ttu-id="89f56-107">Uzaktan hata ayıklama parametrelerle java işlemi başlatır böylece hata ayıklamak için istediğiniz hizmet entryPoint.sh güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="89f56-107">Update entryPoint.sh of the service you wish to debug, so that it starts the java process with remote debug parameters.</span></span> <span data-ttu-id="89f56-108">Bu dosya şu konumda bulunabilir: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span><span class="sxs-lookup"><span data-stu-id="89f56-108">This file can be found at the following location: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span></span> <span data-ttu-id="89f56-109">Bu örnekte, hata ayıklama için bağlantı noktası 8001 ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="89f56-109">Port 8001 is set for debugging in this example.</span></span>

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. <span data-ttu-id="89f56-110">Uygulama bildirimi örneği sayısını veya ayıklanacak hizmet için yineleme sayısı 1 olarak ayarlayarak güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="89f56-110">Update the Application Manifest by setting the instance count or the replica count for the service that is being debugged to 1.</span></span> <span data-ttu-id="89f56-111">Bu ayar, hata ayıklama için kullanılan bağlantı noktası için çakışmalarını önler.</span><span class="sxs-lookup"><span data-stu-id="89f56-111">This setting avoids conflicts for the port that is used for debugging.</span></span> <span data-ttu-id="89f56-112">Örneğin, durum bilgisi olmayan hizmetler için ayarlar ``InstanceCount="1"`` ve durum bilgisi olan hizmetler hedef ayarlamak ve min çoğaltma boyutları gibi 1 olarak ayarlayın: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span><span class="sxs-lookup"><span data-stu-id="89f56-112">For example, for stateless services, set ``InstanceCount="1"`` and for stateful services set the target and min replica set sizes to 1 as follows: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span></span>

4. <span data-ttu-id="89f56-113">Uygulamayı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="89f56-113">Deploy the application.</span></span>

5. <span data-ttu-id="89f56-114">Eclipse IDE'de seçin **Çalıştır -> hata ayıklama yapılandırmaları uzak Java uygulaması -> ve giriş bağlantı özelliklerini** ve özelliklerini şu şekilde ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="89f56-114">In the Eclipse IDE, select **Run -> Debug Configurations -> Remote Java Application and input connection properties** and set the properties as follows:</span></span>

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  <span data-ttu-id="89f56-115">Uygulamada hata ayıklama ve istenen noktalarda kesme noktaları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="89f56-115">Set breakpoints at desired points and debug the application.</span></span>

<span data-ttu-id="89f56-116">Uygulama kilitlenme, coredumps etkinleştirmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89f56-116">If the application is crashing, you may also want to enable coredumps.</span></span> <span data-ttu-id="89f56-117">Yürütme ``ulimit -c`` bir Kabuğu'nda ve 0 döndürür sonra coredumps etkin değil.</span><span class="sxs-lookup"><span data-stu-id="89f56-117">Execute ``ulimit -c`` in a shell and if it returns 0, then coredumps are not enabled.</span></span> <span data-ttu-id="89f56-118">Sınırsız coredumps etkinleştirmek için aşağıdaki komutu yürütün: ``ulimit -c unlimited``.</span><span class="sxs-lookup"><span data-stu-id="89f56-118">To enable unlimited coredumps, execute the following command: ``ulimit -c unlimited``.</span></span> <span data-ttu-id="89f56-119">Komutunu kullanarak durum da doğrulayabilirsiniz ``ulimit -a``.</span><span class="sxs-lookup"><span data-stu-id="89f56-119">You can also verify the status using the command ``ulimit -a``.</span></span>  <span data-ttu-id="89f56-120">Coredump oluşturma yolu güncelleştirmek istiyorsanız, yürütme ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span><span class="sxs-lookup"><span data-stu-id="89f56-120">If you wanted to update the coredump generation path, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span></span> 

### <a name="next-steps"></a><span data-ttu-id="89f56-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="89f56-121">Next steps</span></span>

* <span data-ttu-id="89f56-122">[Linux Azure Tanılama'yı kullanarak günlükleri toplamak](service-fabric-diagnostics-how-to-setup-lad.md).</span><span class="sxs-lookup"><span data-stu-id="89f56-122">[Collect logs using Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span></span>
* <span data-ttu-id="89f56-123">[İzleme ve Hizmetleri yerel olarak tanılamak](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span><span class="sxs-lookup"><span data-stu-id="89f56-123">[Monitor and diagnose services locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span></span>
