---
title: "aaaDebug Azure Service Fabric uygulamanızı eclipse'te | Microsoft Docs"
description: "Merhaba güvenilirliğini ve performansını hizmetlerinizi geliştirmek ve bunları Eclipse'te yerel geliştirme kümede hata ayıklama tarafından geliştirin."
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
ms.openlocfilehash: ab86254a5c312db40fd631746c89aab0bbb9d1a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a><span data-ttu-id="4702b-103">Java Service Fabric uygulamanızı Eclipse kullanarak hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="4702b-103">Debug your Java Service Fabric application using Eclipse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4702b-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="4702b-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="4702b-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="4702b-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
> 

1. <span data-ttu-id="4702b-106">Merhaba adımları izleyerek yerel bir geliştirme kümesi Başlat [, Service Fabric geliştirme ortamını ayarlama](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4702b-106">Start a local development cluster by following hello steps in [Setting up your Service Fabric development environment](service-fabric-get-started-linux.md).</span></span>

2. <span data-ttu-id="4702b-107">EntryPoint.sh güncelleştirme hello hizmeti uzaktan hata ayıklama parametrelerle hello java işlemi başlatılır böylece toodebug, istiyor.</span><span class="sxs-lookup"><span data-stu-id="4702b-107">Update entryPoint.sh of hello service you wish toodebug, so that it starts hello java process with remote debug parameters.</span></span> <span data-ttu-id="4702b-108">Bu dosya konumu aşağıdaki hello bulunabilir: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span><span class="sxs-lookup"><span data-stu-id="4702b-108">This file can be found at hello following location: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span></span> <span data-ttu-id="4702b-109">Bu örnekte, hata ayıklama için bağlantı noktası 8001 ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="4702b-109">Port 8001 is set for debugging in this example.</span></span>

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. <span data-ttu-id="4702b-110">Merhaba örnek sayısı ayarlayarak Hello uygulama bildirimi güncelleştirin veya hello yüklenmekte olan hello hizmeti için çoğaltma sayısını too1 hata ayıklaması.</span><span class="sxs-lookup"><span data-stu-id="4702b-110">Update hello Application Manifest by setting hello instance count or hello replica count for hello service that is being debugged too1.</span></span> <span data-ttu-id="4702b-111">Bu ayar, hata ayıklama için kullanılan başlangıç bağlantı noktası için çakışmalarını önler.</span><span class="sxs-lookup"><span data-stu-id="4702b-111">This setting avoids conflicts for hello port that is used for debugging.</span></span> <span data-ttu-id="4702b-112">Örneğin, durum bilgisi olmayan hizmetler için ayarlar ``InstanceCount="1"`` ve boyutları too1 kümesi hello hedef ve min çoğaltma durum bilgisi olan hizmetler için aşağıdaki gibi ayarlayın: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span><span class="sxs-lookup"><span data-stu-id="4702b-112">For example, for stateless services, set ``InstanceCount="1"`` and for stateful services set hello target and min replica set sizes too1 as follows: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span></span>

4. <span data-ttu-id="4702b-113">Merhaba uygulamayı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="4702b-113">Deploy hello application.</span></span>

5. <span data-ttu-id="4702b-114">Hello Eclipse IDE seçin **Çalıştır -> hata ayıklama yapılandırmaları uzak Java uygulaması -> ve giriş bağlantı özelliklerini** ve hello özelliklerini aşağıdaki gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="4702b-114">In hello Eclipse IDE, select **Run -> Debug Configurations -> Remote Java Application and input connection properties** and set hello properties as follows:</span></span>

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  <span data-ttu-id="4702b-115">Merhaba uygulamada hata ayıklama ve istenen noktalarda kesme noktaları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4702b-115">Set breakpoints at desired points and debug hello application.</span></span>

<span data-ttu-id="4702b-116">Merhaba uygulaması kilitlenen, tooenable coredumps da isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4702b-116">If hello application is crashing, you may also want tooenable coredumps.</span></span> <span data-ttu-id="4702b-117">Yürütme ``ulimit -c`` bir Kabuğu'nda ve 0 döndürür sonra coredumps etkin değil.</span><span class="sxs-lookup"><span data-stu-id="4702b-117">Execute ``ulimit -c`` in a shell and if it returns 0, then coredumps are not enabled.</span></span> <span data-ttu-id="4702b-118">tooenable sınırsız coredumps yürütme komutu aşağıdaki hello: ``ulimit -c unlimited``.</span><span class="sxs-lookup"><span data-stu-id="4702b-118">tooenable unlimited coredumps, execute hello following command: ``ulimit -c unlimited``.</span></span> <span data-ttu-id="4702b-119">Merhaba durum hello komutunu kullanarak da doğrulayabilirsiniz ``ulimit -a``.</span><span class="sxs-lookup"><span data-stu-id="4702b-119">You can also verify hello status using hello command ``ulimit -a``.</span></span>  <span data-ttu-id="4702b-120">Tooupdate hello coredump oluşturma yolu istediyseniz, yürütme ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span><span class="sxs-lookup"><span data-stu-id="4702b-120">If you wanted tooupdate hello coredump generation path, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span></span> 

### <a name="next-steps"></a><span data-ttu-id="4702b-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4702b-121">Next steps</span></span>

* <span data-ttu-id="4702b-122">[Linux Azure Tanılama'yı kullanarak günlükleri toplamak](service-fabric-diagnostics-how-to-setup-lad.md).</span><span class="sxs-lookup"><span data-stu-id="4702b-122">[Collect logs using Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span></span>
* <span data-ttu-id="4702b-123">[İzleme ve Hizmetleri yerel olarak tanılamak](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4702b-123">[Monitor and diagnose services locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span></span>
