---
title: Azure Service Fabric ile aaaReport ve onay durumunu | Microsoft Docs
description: "Hizmet kodunuzdan nasıl toosend durumu raporları ve toocheck hello durumu, Azure Service Fabric hello sistem durumu izleme araçları kullanarak hizmetinizin nasıl sağladığını öğrenin."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: mfussell
editor: 
ms.assetid: 7c712c22-d333-44bc-b837-d0b3603d9da8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: bcb838fefe3f2054447e1731d709e455560260e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="report-and-check-service-health"></a><span data-ttu-id="9617d-103">Hizmet durumunu raporlama ve denetleme</span><span class="sxs-lookup"><span data-stu-id="9617d-103">Report and check service health</span></span>
<span data-ttu-id="9617d-104">Hizmetlerinizin sorunlarla, özelliği toorespond tooand düzeltme olaylar ve kesintileri bağlıdır özelliği toodetect hello sorunlarınızı hızla.</span><span class="sxs-lookup"><span data-stu-id="9617d-104">When your services encounter problems, your ability toorespond tooand fix incidents and outages depends on your ability toodetect hello issues quickly.</span></span> <span data-ttu-id="9617d-105">Sorunları ve hataları toohello Azure Service Fabric sistem durumu Yöneticisi hizmeti kodunuzdan rapor standart sistem durumu izleme Service Fabric toocheck hello sistem durumunu sağlar araçları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9617d-105">If you report problems and failures toohello Azure Service Fabric health manager from your service code, you can use standard health monitoring tools that Service Fabric provides toocheck hello health status.</span></span>

<span data-ttu-id="9617d-106">Merhaba hizmetinden sistem durumu raporu olan üç yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="9617d-106">There are three ways that you can report health from hello service:</span></span>

* <span data-ttu-id="9617d-107">Kullanım [bölüm](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) veya [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) nesneleri.</span><span class="sxs-lookup"><span data-stu-id="9617d-107">Use [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) or [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objects.</span></span>  
  <span data-ttu-id="9617d-108">Merhaba kullanabilirsiniz `Partition` ve `CodePackageActivationContext` tooreport hello hello geçerli bağlam parçası olan öğeleri durumunu nesneleri.</span><span class="sxs-lookup"><span data-stu-id="9617d-108">You can use hello `Partition` and `CodePackageActivationContext` objects tooreport hello health of elements that are part of hello current context.</span></span> <span data-ttu-id="9617d-109">Örneğin, bir çoğaltma bir parçası olarak çalışan bir kod yalnızca bu çoğaltma, ait hello bölüm ve bir parçası olan hello uygulama sistem durumu bildirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9617d-109">For example, code that runs as part of a replica can report health only on that replica, hello partition that it belongs to, and hello application that it is a part of.</span></span>
* <span data-ttu-id="9617d-110">Kullanım `FabricClient`.</span><span class="sxs-lookup"><span data-stu-id="9617d-110">Use `FabricClient`.</span></span>   
  <span data-ttu-id="9617d-111">Kullanabileceğiniz `FabricClient` tooreport durumu hello küme değilse hello hizmet kodundan [güvenli](service-fabric-cluster-security.md) veya yönetici ayrıcalıkları olan hello Hizmeti çalışıyorsa.</span><span class="sxs-lookup"><span data-stu-id="9617d-111">You can use `FabricClient` tooreport health from hello service code if hello cluster is not [secure](service-fabric-cluster-security.md) or if hello service is running with admin privileges.</span></span> <span data-ttu-id="9617d-112">Çoğu gerçek dünya senaryoları değil güvenli olmayan kümeler kullanın veya yönetici ayrıcalıkları sağlayın.</span><span class="sxs-lookup"><span data-stu-id="9617d-112">Most real-world scenarios do not use unsecured clusters, or provide admin privileges.</span></span> <span data-ttu-id="9617d-113">İle `FabricClient`, sistem durumu hello kümesinin parçası olan herhangi bir varlıkta bildirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9617d-113">With `FabricClient`, you can report health on any entity that is a part of hello cluster.</span></span> <span data-ttu-id="9617d-114">İdeal olarak, ancak hizmet kod yalnızca ilgili tooits kendi sistem durumu raporları göndermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="9617d-114">Ideally, however, service code should only send reports that are related tooits own health.</span></span>
* <span data-ttu-id="9617d-115">Merhaba REST API'leri hello küme, uygulama, dağıtılan bir uygulama, hizmet, hizmet paketi, bölüm, çoğaltma veya düğüm düzeylerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="9617d-115">Use hello REST APIs at hello cluster, application, deployed application, service, service package, partition, replica, or node levels.</span></span> <span data-ttu-id="9617d-116">Bu, kullanılan tooreport durumu bir kapsayıcı içinde olabilir.</span><span class="sxs-lookup"><span data-stu-id="9617d-116">This can be used tooreport health from within a container.</span></span>

<span data-ttu-id="9617d-117">Bu makalede, hello hizmet kodundan durumu raporları bir örnek adım adım anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9617d-117">This article walks you through an example that reports health from hello service code.</span></span> <span data-ttu-id="9617d-118">Service Fabric tarafından sağlanan hello araçları kullanılan toocheck hello sistem durumunu nasıl olabilir Hello örnek ayrıca gösterir.</span><span class="sxs-lookup"><span data-stu-id="9617d-118">hello example also shows how hello tools provided by Service Fabric can be used toocheck hello health status.</span></span> <span data-ttu-id="9617d-119">Bu makalede Hızlı Giriş toohello durumunu Service Fabric yeteneklerini izleme hedeflenen toobe olduğu.</span><span class="sxs-lookup"><span data-stu-id="9617d-119">This article is intended toobe a quick introduction toohello health monitoring capabilities of Service Fabric.</span></span> <span data-ttu-id="9617d-120">Daha ayrıntılı bilgi için bu makalenin hello sonunda hello bağlantıyla Başlat sistem durumu hakkında ayrıntılı makaleleri hello dizi okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="9617d-120">For more detailed information, you can read hello series of in-depth articles about health that start with hello link at hello end of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9617d-121">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9617d-121">Prerequisites</span></span>
<span data-ttu-id="9617d-122">Merhaba aşağıdakilerin yüklü olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="9617d-122">You must have hello following installed:</span></span>

* <span data-ttu-id="9617d-123">Visual Studio 2015 veya Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="9617d-123">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="9617d-124">Service Fabric SDK</span><span class="sxs-lookup"><span data-stu-id="9617d-124">Service Fabric SDK</span></span>

## <a name="toocreate-a-local-secure-dev-cluster"></a><span data-ttu-id="9617d-125">toocreate yerel güvenli geliştirme küme</span><span class="sxs-lookup"><span data-stu-id="9617d-125">toocreate a local secure dev cluster</span></span>
* <span data-ttu-id="9617d-126">PowerShell'i yönetici ayrıcalıklarıyla açın ve hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9617d-126">Open PowerShell with admin privileges, and run hello following commands:</span></span>

![Gösteren nasıl komutları toocreate güvenli geliştirme küme](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="toodeploy-an-application-and-check-its-health"></a><span data-ttu-id="9617d-128">toodeploy bir uygulama ve sistem durumu denetleyin</span><span class="sxs-lookup"><span data-stu-id="9617d-128">toodeploy an application and check its health</span></span>
1. <span data-ttu-id="9617d-129">Visual Studio'yu yönetici olarak açın.</span><span class="sxs-lookup"><span data-stu-id="9617d-129">Open Visual Studio as an administrator.</span></span>
2. <span data-ttu-id="9617d-130">Hello kullanarak bir proje oluşturma **durum bilgisi olan hizmet** şablonu.</span><span class="sxs-lookup"><span data-stu-id="9617d-130">Create a project by using hello **Stateful Service** template.</span></span>
   
    ![Durum bilgisi olan hizmeti ile bir Service Fabric uygulaması oluşturma](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. <span data-ttu-id="9617d-132">Tuşuna **F5** toorun hello uygulama hata ayıklama modunda.</span><span class="sxs-lookup"><span data-stu-id="9617d-132">Press **F5** toorun hello application in debug mode.</span></span> <span data-ttu-id="9617d-133">Merhaba, dağıtılan toohello yerel küme uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="9617d-133">hello application is deployed toohello local cluster.</span></span>
4. <span data-ttu-id="9617d-134">Merhaba uygulaması çalıştırdıktan sonra hello bildirim alanında hello yerel Küme Yöneticisi simgesini sağ tıklatın ve seçin **yerel kümeyi Yönet** hello kısayol menüsü tooopen Service Fabric Explorer gelen.</span><span class="sxs-lookup"><span data-stu-id="9617d-134">After hello application is running, right-click hello Local Cluster Manager icon in hello notification area and select **Manage Local Cluster** from hello shortcut menu tooopen Service Fabric Explorer.</span></span>
   
    ![Bildirim alanından Service Fabric Explorer'ı açın](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. <span data-ttu-id="9617d-136">Bu görüntü olduğu gibi Hello uygulama sağlığını görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="9617d-136">hello application health should be displayed as in this image.</span></span> <span data-ttu-id="9617d-137">Şu anda Merhaba uygulaması hatasız sağlıklı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9617d-137">At this time, hello application should be healthy with no errors.</span></span>
   
    ![Service Fabric Explorer'da sağlıklı uygulama](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. <span data-ttu-id="9617d-139">Ayrıca, hello sistem durumu PowerShell kullanarak da kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9617d-139">You can also check hello health by using PowerShell.</span></span> <span data-ttu-id="9617d-140">Kullanabileceğiniz ```Get-ServiceFabricApplicationHealth``` uygulamanın durumu ve kullanabilir toocheck ```Get-ServiceFabricServiceHealth``` toocheck bir hizmetin sistem durumu.</span><span class="sxs-lookup"><span data-stu-id="9617d-140">You can use ```Get-ServiceFabricApplicationHealth``` toocheck an application's health, and you can use ```Get-ServiceFabricServiceHealth``` toocheck a service's health.</span></span> <span data-ttu-id="9617d-141">hello ait hello sistem durumu raporu aynı PowerShell'de bu görüntüde uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="9617d-141">hello health report for hello same application in PowerShell is in this image.</span></span>
   
    ![PowerShell'de sağlıklı uygulama](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="tooadd-custom-health-events-tooyour-service-code"></a><span data-ttu-id="9617d-143">tooadd özel durum olayları tooyour servis kodu</span><span class="sxs-lookup"><span data-stu-id="9617d-143">tooadd custom health events tooyour service code</span></span>
<span data-ttu-id="9617d-144">Visual Studio'da Hello Service Fabric proje şablonları örnek kod içerir.</span><span class="sxs-lookup"><span data-stu-id="9617d-144">hello Service Fabric project templates in Visual Studio contain sample code.</span></span> <span data-ttu-id="9617d-145">Merhaba aşağıdaki adımlar hizmet kodunuzdan özel durum olayları nasıl raporlayabilirsiniz gösterir.</span><span class="sxs-lookup"><span data-stu-id="9617d-145">hello following steps show how you can report custom health events from your service code.</span></span> <span data-ttu-id="9617d-146">Bu raporlar otomatik olarak durumunu Service Fabric, Service Fabric Explorer, Azure portal durum görünümü ve PowerShell gibi sağladığı izleme için standart araçları hello gösterilir.</span><span class="sxs-lookup"><span data-stu-id="9617d-146">Such reports show up automatically in hello standard tools for health monitoring that Service Fabric provides, such as Service Fabric Explorer, Azure portal health view, and PowerShell.</span></span>

1. <span data-ttu-id="9617d-147">Visual Studio'da daha önce oluşturduğunuz hello uygulamasını yeniden açın veya hello kullanarak yeni bir uygulama oluşturma **durum bilgisi olan hizmet** Visual Studio şablonu.</span><span class="sxs-lookup"><span data-stu-id="9617d-147">Reopen hello application that you created previously in Visual Studio, or create a new application by using hello **Stateful Service** Visual Studio template.</span></span>
2. <span data-ttu-id="9617d-148">Merhaba Stateful1.cs dosyasını açın ve hello bulun `myDictionary.TryGetValueAsync` hello çağrı `RunAsync` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9617d-148">Open hello Stateful1.cs file, and find hello `myDictionary.TryGetValueAsync` call in hello `RunAsync` method.</span></span> <span data-ttu-id="9617d-149">Bu yöntem döndürdüğünü gördüğünüz bir `result` bu uygulamada hello anahtar mantığı tookeep sayısı çalışıyor olduğundan ayrı tutma hello sayacının geçerli değeri hello.</span><span class="sxs-lookup"><span data-stu-id="9617d-149">You can see that this method returns a `result` that holds hello current value of hello counter because hello key logic in this application is tookeep a count running.</span></span> <span data-ttu-id="9617d-150">Bu gerçek bir uygulamada olsaydı ve bir hata sonucu hello eksikliği temsil varsa, bu olay tooflag istersiniz.</span><span class="sxs-lookup"><span data-stu-id="9617d-150">If this were a real application, and if hello lack of result represented a failure, you would want tooflag that event.</span></span>
3. <span data-ttu-id="9617d-151">tooreport bir hata sonucu hello eksikliği temsil eden bir sistem durumu olayı aşağıdaki adımları hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9617d-151">tooreport a health event when hello lack of result represents a failure, add hello following steps.</span></span>
   
    <span data-ttu-id="9617d-152">a.</span><span class="sxs-lookup"><span data-stu-id="9617d-152">a.</span></span> <span data-ttu-id="9617d-153">Merhaba eklemek `System.Fabric.Health` ad alanı toohello Stateful1.cs dosya.</span><span class="sxs-lookup"><span data-stu-id="9617d-153">Add hello `System.Fabric.Health` namespace toohello Stateful1.cs file.</span></span>
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    <span data-ttu-id="9617d-154">b.</span><span class="sxs-lookup"><span data-stu-id="9617d-154">b.</span></span> <span data-ttu-id="9617d-155">Koddan sonra hello hello eklemek `myDictionary.TryGetValueAsync` çağırın</span><span class="sxs-lookup"><span data-stu-id="9617d-155">Add hello following code after hello `myDictionary.TryGetValueAsync` call</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    <span data-ttu-id="9617d-156">Bir durum bilgisi olan hizmetinden raporlandığını çünkü biz çoğaltma sistem durumu raporu.</span><span class="sxs-lookup"><span data-stu-id="9617d-156">We report replica health because it's being reported from a stateful service.</span></span> <span data-ttu-id="9617d-157">Merhaba `HealthInformation` parametre rapor edilen hello sistem durumu sorun hakkında bilgi depolar.</span><span class="sxs-lookup"><span data-stu-id="9617d-157">hello `HealthInformation` parameter stores information about hello health issue that's being reported.</span></span>
   
    <span data-ttu-id="9617d-158">Durum bilgisiz hizmet oluşturduysanız koddan hello kullanın</span><span class="sxs-lookup"><span data-stu-id="9617d-158">If you had created a stateless service, use hello following code</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. <span data-ttu-id="9617d-159">Hizmetinizin yönetici ayrıcalıklarıyla çalıştığından veya hello küme değilse [güvenli](service-fabric-cluster-security.md), de kullanabilirsiniz `FabricClient` aşağıdaki adımları hello gösterildiği gibi tooreport sistem durumu.</span><span class="sxs-lookup"><span data-stu-id="9617d-159">If your service is running with admin privileges or if hello cluster is not [secure](service-fabric-cluster-security.md), you can also use `FabricClient` tooreport health as shown in hello following steps.</span></span>  
   
    <span data-ttu-id="9617d-160">a.</span><span class="sxs-lookup"><span data-stu-id="9617d-160">a.</span></span> <span data-ttu-id="9617d-161">Merhaba oluşturma `FabricClient` örneği hello sonra `var myDictionary` bildirimi.</span><span class="sxs-lookup"><span data-stu-id="9617d-161">Create hello `FabricClient` instance after hello `var myDictionary` declaration.</span></span>
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    <span data-ttu-id="9617d-162">b.</span><span class="sxs-lookup"><span data-stu-id="9617d-162">b.</span></span> <span data-ttu-id="9617d-163">Koddan sonra hello hello eklemek `myDictionary.TryGetValueAsync` çağırın.</span><span class="sxs-lookup"><span data-stu-id="9617d-163">Add hello following code after hello `myDictionary.TryGetValueAsync` call.</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
       var replicaHealthReport = new StatefulServiceReplicaHealthReport(
            this.Context.PartitionId,
            this.Context.ReplicaId,
            new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error));
        fabricClient.HealthManager.ReportHealth(replicaHealthReport);
    }
    ```
5. <span data-ttu-id="9617d-164">Şimdi bu arızanın benzetimini gerçekleştirin ve bunu hello sistem durumu izleme araçları görünmesini bakın.</span><span class="sxs-lookup"><span data-stu-id="9617d-164">Let's simulate this failure and see it show up in hello health monitoring tools.</span></span> <span data-ttu-id="9617d-165">toosimulate hello hatası, yorum hello sistem durumu raporlama daha önce eklediğiniz kodu hello ilk satırı çıkışı.</span><span class="sxs-lookup"><span data-stu-id="9617d-165">toosimulate hello failure, comment out hello first line in hello health reporting code that you added earlier.</span></span> <span data-ttu-id="9617d-166">Merhaba ilk satırını açıklama sonra hello kodu örneği aşağıdaki hello gibi görünecektir.</span><span class="sxs-lookup"><span data-stu-id="9617d-166">After you comment out hello first line, hello code will look like hello following example.</span></span>
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   <span data-ttu-id="9617d-167">Bu kod hello sistem durumu raporu her zaman harekete `RunAsync` yürütür.</span><span class="sxs-lookup"><span data-stu-id="9617d-167">This code fires hello health report each time `RunAsync` executes.</span></span> <span data-ttu-id="9617d-168">Merhaba değişiklik yaptıktan sonra basın **F5** toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="9617d-168">After you make hello change, press **F5** toorun hello application.</span></span>
6. <span data-ttu-id="9617d-169">Merhaba uygulaması çalıştırdıktan sonra Service Fabric Explorer toocheck hello hello uygulama durumunu açın.</span><span class="sxs-lookup"><span data-stu-id="9617d-169">After hello application is running, open Service Fabric Explorer toocheck hello health of hello application.</span></span> <span data-ttu-id="9617d-170">Bu süre, Service Fabric Explorer hello uygulamanın sağlıksız olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="9617d-170">This time, Service Fabric Explorer shows that hello application is unhealthy.</span></span> <span data-ttu-id="9617d-171">Daha önce eklediğimiz hello koddan bildirilen hello hata nedeniyle budur.</span><span class="sxs-lookup"><span data-stu-id="9617d-171">This is because of hello error that was reported from hello code that we added previously.</span></span>
   
    ![Service Fabric Explorer'da düzgün çalışmayan uygulama](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. <span data-ttu-id="9617d-173">Merhaba ağaç görünümünde Service Fabric Explorer hello birincil çoğaltma seçerseniz, görürsünüz **sistem durumu** çok bir hata gösterir.</span><span class="sxs-lookup"><span data-stu-id="9617d-173">If you select hello primary replica in hello tree view of Service Fabric Explorer, you will see that **Health State** indicates an error, too.</span></span> <span data-ttu-id="9617d-174">Service Fabric Explorer da olan Ayrıntılar eklenen toohello hello sistem durumu raporu görüntüler `HealthInformation` hello kodu parametresi.</span><span class="sxs-lookup"><span data-stu-id="9617d-174">Service Fabric Explorer also displays hello health report details that were added toohello `HealthInformation` parameter in hello code.</span></span> <span data-ttu-id="9617d-175">Gördüğünüz hello aynı sistem durumu raporlarının PowerShell ve Azure portal hello.</span><span class="sxs-lookup"><span data-stu-id="9617d-175">You can see hello same health reports in PowerShell and hello Azure portal.</span></span>
   
    ![Service Fabric Explorer'da çoğaltma durumu](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

<span data-ttu-id="9617d-177">Bu çoğaltma silinene kadar veya başka bir raporu tarafından değiştirilene kadar bu rapor hello sistem durumu Yöneticisi'nde kalır.</span><span class="sxs-lookup"><span data-stu-id="9617d-177">This report remains in hello health manager until it is replaced by another report or until this replica is deleted.</span></span> <span data-ttu-id="9617d-178">Biz ayarlanmamış olduğundan `TimeToLive` hello bu sistem durumu raporu için `HealthInformation` nesne hello rapor her zaman geçerli olsun.</span><span class="sxs-lookup"><span data-stu-id="9617d-178">Because we did not set `TimeToLive` for this health report in hello `HealthInformation` object, hello report never expires.</span></span>

<span data-ttu-id="9617d-179">Sistem durumu hello çoğaltma bu durumda olan hello en parçalı düzeyde, bildirilen olduğunu öneririz.</span><span class="sxs-lookup"><span data-stu-id="9617d-179">We recommend that health should be reported on hello most granular level, which in this case is hello replica.</span></span> <span data-ttu-id="9617d-180">Üzerindeki sistem durumu bildirebilirsiniz `Partition`.</span><span class="sxs-lookup"><span data-stu-id="9617d-180">You can also report health on `Partition`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

<span data-ttu-id="9617d-181">tooreport sistem durumunu `Application`, `DeployedApplication`, ve `DeployedServicePackage`, kullanmak `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="9617d-181">tooreport health on `Application`, `DeployedApplication`, and `DeployedServicePackage`, use  `CodePackageActivationContext`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a><span data-ttu-id="9617d-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9617d-182">Next steps</span></span>
* [<span data-ttu-id="9617d-183">Service Fabric sistem üzerinde derin Dalış</span><span class="sxs-lookup"><span data-stu-id="9617d-183">Deep dive on Service Fabric health</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="9617d-184">Hizmet durumu raporlama için REST API</span><span class="sxs-lookup"><span data-stu-id="9617d-184">REST API for reporting service health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [<span data-ttu-id="9617d-185">Uygulama durumu raporlama için REST API</span><span class="sxs-lookup"><span data-stu-id="9617d-185">REST API for reporting application health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

