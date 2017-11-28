---
title: Rapor ve Azure Service Fabric ile sistem durumu denetimi | Microsoft Docs
description: "Hizmet kodunuzdan sistem durumu raporları göndermek nasıl Azure Service Fabric sağlayan sistem durumu izleme araçları kullanarak Hizmetinizin durumunu denetlemek nasıl öğrenin."
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
ms.openlocfilehash: 83981d5bec14c06c509f1a8a4153dc23298f5ce0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="report-and-check-service-health"></a><span data-ttu-id="8da05-103">Hizmet durumunu raporlama ve denetleme</span><span class="sxs-lookup"><span data-stu-id="8da05-103">Report and check service health</span></span>
<span data-ttu-id="8da05-104">Hizmetlerinizin sorunlarla yanıt ve olayları ve kesintileri düzeltme yeteneğinizi sorunları hızla algılamak için yeteneğinizi bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="8da05-104">When your services encounter problems, your ability to respond to and fix incidents and outages depends on your ability to detect the issues quickly.</span></span> <span data-ttu-id="8da05-105">Sorunları ve hataları Azure Service Fabric sistem durumu hizmeti kodunuzdan yöneticiye, standart sistem durumu izleme sistem durumunu denetlemek için Service Fabric sağlayan araçları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8da05-105">If you report problems and failures to the Azure Service Fabric health manager from your service code, you can use standard health monitoring tools that Service Fabric provides to check the health status.</span></span>

<span data-ttu-id="8da05-106">Sistem durumu hizmetinden raporu olan üç yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="8da05-106">There are three ways that you can report health from the service:</span></span>

* <span data-ttu-id="8da05-107">Kullanım [bölüm](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) veya [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) nesneleri.</span><span class="sxs-lookup"><span data-stu-id="8da05-107">Use [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) or [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objects.</span></span>  
  <span data-ttu-id="8da05-108">Kullanabileceğiniz `Partition` ve `CodePackageActivationContext` geçerli bağlamı parçası olan öğeleri durumunu bildirmek için nesneleri.</span><span class="sxs-lookup"><span data-stu-id="8da05-108">You can use the `Partition` and `CodePackageActivationContext` objects to report the health of elements that are part of the current context.</span></span> <span data-ttu-id="8da05-109">Örneğin, bir çoğaltma bir parçası olarak çalışan bir kod yalnızca bu çoğaltma, ait olduğu bölüm ve bir parçası olan uygulama sistem durumu bildirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8da05-109">For example, code that runs as part of a replica can report health only on that replica, the partition that it belongs to, and the application that it is a part of.</span></span>
* <span data-ttu-id="8da05-110">Kullanım `FabricClient`.</span><span class="sxs-lookup"><span data-stu-id="8da05-110">Use `FabricClient`.</span></span>   
  <span data-ttu-id="8da05-111">Kullanabileceğiniz `FabricClient` rapor durumu kümeyi değilse, hizmet kodundan için [güvenli](service-fabric-cluster-security.md) veya yönetici ayrıcalıkları olan hizmeti çalışıyorsa.</span><span class="sxs-lookup"><span data-stu-id="8da05-111">You can use `FabricClient` to report health from the service code if the cluster is not [secure](service-fabric-cluster-security.md) or if the service is running with admin privileges.</span></span> <span data-ttu-id="8da05-112">Çoğu gerçek dünya senaryoları değil güvenli olmayan kümeler kullanın veya yönetici ayrıcalıkları sağlayın.</span><span class="sxs-lookup"><span data-stu-id="8da05-112">Most real-world scenarios do not use unsecured clusters, or provide admin privileges.</span></span> <span data-ttu-id="8da05-113">İle `FabricClient`, sistem durumu kümesinin parçası olan herhangi bir varlıkta bildirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8da05-113">With `FabricClient`, you can report health on any entity that is a part of the cluster.</span></span> <span data-ttu-id="8da05-114">İdeal olarak, ancak hizmet kod yalnızca kendi sağlığı ile ilgili raporları göndermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8da05-114">Ideally, however, service code should only send reports that are related to its own health.</span></span>
* <span data-ttu-id="8da05-115">Küme, uygulama, dağıtılan bir uygulama, hizmet, hizmet paketi, bölüm, çoğaltma veya düğüm düzeyleri REST API'leri kullanın.</span><span class="sxs-lookup"><span data-stu-id="8da05-115">Use the REST APIs at the cluster, application, deployed application, service, service package, partition, replica, or node levels.</span></span> <span data-ttu-id="8da05-116">Bu sistem durumu bir kapsayıcıdaki raporlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8da05-116">This can be used to report health from within a container.</span></span>

<span data-ttu-id="8da05-117">Bu makalede, hizmet kodundan durumu raporları bir örnek adım adım anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8da05-117">This article walks you through an example that reports health from the service code.</span></span> <span data-ttu-id="8da05-118">Bu örnek ayrıca sistem durumunu denetlemek için Service Fabric tarafından sağlanan araçları nasıl kullanılabileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="8da05-118">The example also shows how the tools provided by Service Fabric can be used to check the health status.</span></span> <span data-ttu-id="8da05-119">Bu makale, Service Fabric yeteneklerini izleme sistem durumu bir giriş olması amaçlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8da05-119">This article is intended to be a quick introduction to the health monitoring capabilities of Service Fabric.</span></span> <span data-ttu-id="8da05-120">Daha ayrıntılı bilgi için bu makalenin sonunda bağlantıyla Başlat sistem durumu hakkında kapsamlı makaleleri bir dizi okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="8da05-120">For more detailed information, you can read the series of in-depth articles about health that start with the link at the end of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8da05-121">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8da05-121">Prerequisites</span></span>
<span data-ttu-id="8da05-122">Aşağıdakilerin yüklü olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="8da05-122">You must have the following installed:</span></span>

* <span data-ttu-id="8da05-123">Visual Studio 2015 veya Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="8da05-123">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="8da05-124">Service Fabric SDK</span><span class="sxs-lookup"><span data-stu-id="8da05-124">Service Fabric SDK</span></span>

## <a name="to-create-a-local-secure-dev-cluster"></a><span data-ttu-id="8da05-125">Yerel güvenli geliştirme küme oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="8da05-125">To create a local secure dev cluster</span></span>
* <span data-ttu-id="8da05-126">PowerShell'i yönetici ayrıcalıklarıyla açın ve aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8da05-126">Open PowerShell with admin privileges, and run the following commands:</span></span>

![Güvenli geliştirme kümesi oluşturmayı gösteren komutları](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="to-deploy-an-application-and-check-its-health"></a><span data-ttu-id="8da05-128">Bir uygulamayı dağıtmak ve durumunu denetlemek için</span><span class="sxs-lookup"><span data-stu-id="8da05-128">To deploy an application and check its health</span></span>
1. <span data-ttu-id="8da05-129">Visual Studio'yu yönetici olarak açın.</span><span class="sxs-lookup"><span data-stu-id="8da05-129">Open Visual Studio as an administrator.</span></span>
2. <span data-ttu-id="8da05-130">Kullanarak bir proje oluşturma **durum bilgisi olan hizmet** şablonu.</span><span class="sxs-lookup"><span data-stu-id="8da05-130">Create a project by using the **Stateful Service** template.</span></span>
   
    ![Durum bilgisi olan hizmeti ile bir Service Fabric uygulaması oluşturma](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. <span data-ttu-id="8da05-132">Tuşuna **F5** uygulamayı hata ayıklama modunda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8da05-132">Press **F5** to run the application in debug mode.</span></span> <span data-ttu-id="8da05-133">Uygulamayı yerel kümeye dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="8da05-133">The application is deployed to the local cluster.</span></span>
4. <span data-ttu-id="8da05-134">Uygulama çalışmaya başladıktan sonra bildirim alanında yerel Küme Yöneticisi simgesine sağ tıklayın ve seçin **yerel kümeyi Yönet** Service Fabric Explorer açmak için kısayol menüsünden.</span><span class="sxs-lookup"><span data-stu-id="8da05-134">After the application is running, right-click the Local Cluster Manager icon in the notification area and select **Manage Local Cluster** from the shortcut menu to open Service Fabric Explorer.</span></span>
   
    ![Bildirim alanından Service Fabric Explorer'ı açın](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. <span data-ttu-id="8da05-136">Uygulama durumunu olduğu gibi bu görüntüyü görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8da05-136">The application health should be displayed as in this image.</span></span> <span data-ttu-id="8da05-137">Şu anda uygulama hatasız sağlıklı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8da05-137">At this time, the application should be healthy with no errors.</span></span>
   
    ![Service Fabric Explorer'da sağlıklı uygulama](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. <span data-ttu-id="8da05-139">Ayrıca, sistem durumu PowerShell kullanarak da kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8da05-139">You can also check the health by using PowerShell.</span></span> <span data-ttu-id="8da05-140">Kullanabileceğiniz ```Get-ServiceFabricApplicationHealth``` uygulamaya ait sağlık ve denetlemek için kullanabileceğiniz ```Get-ServiceFabricServiceHealth``` bir hizmetin sistem durumu denetlemek için.</span><span class="sxs-lookup"><span data-stu-id="8da05-140">You can use ```Get-ServiceFabricApplicationHealth``` to check an application's health, and you can use ```Get-ServiceFabricServiceHealth``` to check a service's health.</span></span> <span data-ttu-id="8da05-141">Sistem Durumu raporu PowerShell'de aynı uygulama için bu görüntüyü kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8da05-141">The health report for the same application in PowerShell is in this image.</span></span>
   
    ![PowerShell'de sağlıklı uygulama](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="to-add-custom-health-events-to-your-service-code"></a><span data-ttu-id="8da05-143">Özel durum olayları hizmet kodunuzun eklemek için</span><span class="sxs-lookup"><span data-stu-id="8da05-143">To add custom health events to your service code</span></span>
<span data-ttu-id="8da05-144">Visual Studio Service Fabric proje şablonlarını örnek kod içerir.</span><span class="sxs-lookup"><span data-stu-id="8da05-144">The Service Fabric project templates in Visual Studio contain sample code.</span></span> <span data-ttu-id="8da05-145">Aşağıdaki adımlar, nasıl özel durum olayları hizmet kodunuzdan bildirebilirsiniz gösterir.</span><span class="sxs-lookup"><span data-stu-id="8da05-145">The following steps show how you can report custom health events from your service code.</span></span> <span data-ttu-id="8da05-146">Bu raporlar otomatik olarak Service Fabric, Service Fabric Explorer, Azure portal durum görünümü ve PowerShell gibi sağladığı sistem durumu izleme için standart Araçları'nda görünür.</span><span class="sxs-lookup"><span data-stu-id="8da05-146">Such reports show up automatically in the standard tools for health monitoring that Service Fabric provides, such as Service Fabric Explorer, Azure portal health view, and PowerShell.</span></span>

1. <span data-ttu-id="8da05-147">Visual Studio'da daha önce oluşturduğunuz uygulamayı kapatıp yeniden açmanız veya kullanarak yeni bir uygulama oluşturma **durum bilgisi olan hizmet** Visual Studio şablonu.</span><span class="sxs-lookup"><span data-stu-id="8da05-147">Reopen the application that you created previously in Visual Studio, or create a new application by using the **Stateful Service** Visual Studio template.</span></span>
2. <span data-ttu-id="8da05-148">Stateful1.cs dosyasını açın ve Bul `myDictionary.TryGetValueAsync` Çağır `RunAsync` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="8da05-148">Open the Stateful1.cs file, and find the `myDictionary.TryGetValueAsync` call in the `RunAsync` method.</span></span> <span data-ttu-id="8da05-149">Bu yöntem döndürdüğünü gördüğünüz bir `result` çalışan sayısı tutmak için bu uygulamayı anahtar mantık olduğu için geçerli sayaç değerini tutan.</span><span class="sxs-lookup"><span data-stu-id="8da05-149">You can see that this method returns a `result` that holds the current value of the counter because the key logic in this application is to keep a count running.</span></span> <span data-ttu-id="8da05-150">Bu gerçek bir uygulamada olsaydı ve bir hata sonucu eksikliği temsil varsa, bu olay bayrak istersiniz.</span><span class="sxs-lookup"><span data-stu-id="8da05-150">If this were a real application, and if the lack of result represented a failure, you would want to flag that event.</span></span>
3. <span data-ttu-id="8da05-151">Bir hata sonucu eksikliği temsil eden sistem durumu olayı bildirmek için aşağıdaki adımları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8da05-151">To report a health event when the lack of result represents a failure, add the following steps.</span></span>
   
    <span data-ttu-id="8da05-152">a.</span><span class="sxs-lookup"><span data-stu-id="8da05-152">a.</span></span> <span data-ttu-id="8da05-153">Ekleme `System.Fabric.Health` Stateful1.cs dosyaya ad alanı.</span><span class="sxs-lookup"><span data-stu-id="8da05-153">Add the `System.Fabric.Health` namespace to the Stateful1.cs file.</span></span>
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    <span data-ttu-id="8da05-154">b.</span><span class="sxs-lookup"><span data-stu-id="8da05-154">b.</span></span> <span data-ttu-id="8da05-155">Sonra aşağıdaki kodu ekleyin `myDictionary.TryGetValueAsync` çağırın</span><span class="sxs-lookup"><span data-stu-id="8da05-155">Add the following code after the `myDictionary.TryGetValueAsync` call</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    <span data-ttu-id="8da05-156">Bir durum bilgisi olan hizmetinden raporlandığını çünkü biz çoğaltma sistem durumu raporu.</span><span class="sxs-lookup"><span data-stu-id="8da05-156">We report replica health because it's being reported from a stateful service.</span></span> <span data-ttu-id="8da05-157">`HealthInformation` Parametre rapor edilen sistem durumu sorun hakkında bilgi depolar.</span><span class="sxs-lookup"><span data-stu-id="8da05-157">The `HealthInformation` parameter stores information about the health issue that's being reported.</span></span>
   
    <span data-ttu-id="8da05-158">Durum bilgisiz hizmet oluşturduysanız, aşağıdaki kodu kullanın</span><span class="sxs-lookup"><span data-stu-id="8da05-158">If you had created a stateless service, use the following code</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. <span data-ttu-id="8da05-159">Hizmetinizin yönetici ayrıcalıklarıyla çalıştırıyorsa veya küme değilse [güvenli](service-fabric-cluster-security.md), aynı zamanda `FabricClient` aşağıdaki adımlarda gösterildiği gibi sistem durumu raporu için.</span><span class="sxs-lookup"><span data-stu-id="8da05-159">If your service is running with admin privileges or if the cluster is not [secure](service-fabric-cluster-security.md), you can also use `FabricClient` to report health as shown in the following steps.</span></span>  
   
    <span data-ttu-id="8da05-160">a.</span><span class="sxs-lookup"><span data-stu-id="8da05-160">a.</span></span> <span data-ttu-id="8da05-161">Oluşturma `FabricClient` sonra örnek `var myDictionary` bildirimi.</span><span class="sxs-lookup"><span data-stu-id="8da05-161">Create the `FabricClient` instance after the `var myDictionary` declaration.</span></span>
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    <span data-ttu-id="8da05-162">b.</span><span class="sxs-lookup"><span data-stu-id="8da05-162">b.</span></span> <span data-ttu-id="8da05-163">Sonra aşağıdaki kodu ekleyin `myDictionary.TryGetValueAsync` çağırın.</span><span class="sxs-lookup"><span data-stu-id="8da05-163">Add the following code after the `myDictionary.TryGetValueAsync` call.</span></span>
   
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
5. <span data-ttu-id="8da05-164">Şimdi bu arızanın benzetimini gerçekleştirin ve bu sistem durumu izleme araçları görünmesini bakın.</span><span class="sxs-lookup"><span data-stu-id="8da05-164">Let's simulate this failure and see it show up in the health monitoring tools.</span></span> <span data-ttu-id="8da05-165">Hata benzetimi için sistem durumu, daha önce eklediğiniz kod raporlama ilk satırı açıklama.</span><span class="sxs-lookup"><span data-stu-id="8da05-165">To simulate the failure, comment out the first line in the health reporting code that you added earlier.</span></span> <span data-ttu-id="8da05-166">İlk satırını açıklama sonra kod aşağıdaki gibi görünecektir.</span><span class="sxs-lookup"><span data-stu-id="8da05-166">After you comment out the first line, the code will look like the following example.</span></span>
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   <span data-ttu-id="8da05-167">Bu kodu her zaman sistem durumu raporu harekete `RunAsync` yürütür.</span><span class="sxs-lookup"><span data-stu-id="8da05-167">This code fires the health report each time `RunAsync` executes.</span></span> <span data-ttu-id="8da05-168">Değişikliği yaptıktan sonra basın **F5** uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8da05-168">After you make the change, press **F5** to run the application.</span></span>
6. <span data-ttu-id="8da05-169">Uygulamayı çalıştırdıktan sonra uygulama durumunu denetlemek için Service Fabric Explorer açın.</span><span class="sxs-lookup"><span data-stu-id="8da05-169">After the application is running, open Service Fabric Explorer to check the health of the application.</span></span> <span data-ttu-id="8da05-170">Bu süre, Service Fabric Explorer uygulamanın sağlıksız olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="8da05-170">This time, Service Fabric Explorer shows that the application is unhealthy.</span></span> <span data-ttu-id="8da05-171">Daha önce eklediğimiz koddan bildirilen hata nedeniyle budur.</span><span class="sxs-lookup"><span data-stu-id="8da05-171">This is because of the error that was reported from the code that we added previously.</span></span>
   
    ![Service Fabric Explorer'da düzgün çalışmayan uygulama](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. <span data-ttu-id="8da05-173">Service Fabric Explorer ağaç görünümünde birincil çoğaltma seçerseniz, görürsünüz **sistem durumu** çok bir hata gösterir.</span><span class="sxs-lookup"><span data-stu-id="8da05-173">If you select the primary replica in the tree view of Service Fabric Explorer, you will see that **Health State** indicates an error, too.</span></span> <span data-ttu-id="8da05-174">Service Fabric Explorer de eklenmiştir sistem durumu rapor ayrıntıları görüntüler `HealthInformation` kodu parametresi.</span><span class="sxs-lookup"><span data-stu-id="8da05-174">Service Fabric Explorer also displays the health report details that were added to the `HealthInformation` parameter in the code.</span></span> <span data-ttu-id="8da05-175">PowerShell ve Azure portalı aynı sistem durumu raporları görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8da05-175">You can see the same health reports in PowerShell and the Azure portal.</span></span>
   
    ![Service Fabric Explorer'da çoğaltma durumu](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

<span data-ttu-id="8da05-177">Bu çoğaltma silinene kadar veya başka bir raporu tarafından değiştirilene kadar bu rapor sistem durumu Yöneticisi'nde kalır.</span><span class="sxs-lookup"><span data-stu-id="8da05-177">This report remains in the health manager until it is replaced by another report or until this replica is deleted.</span></span> <span data-ttu-id="8da05-178">Biz ayarlanmamış olduğundan `TimeToLive` bu sistem durumu raporu için `HealthInformation` nesne, rapor her zaman geçerli olsun.</span><span class="sxs-lookup"><span data-stu-id="8da05-178">Because we did not set `TimeToLive` for this health report in the `HealthInformation` object, the report never expires.</span></span>

<span data-ttu-id="8da05-179">Sistem durumu çoğaltma bu durumda olan en ayrıntılı düzeyi, bildirilen olduğunu öneririz.</span><span class="sxs-lookup"><span data-stu-id="8da05-179">We recommend that health should be reported on the most granular level, which in this case is the replica.</span></span> <span data-ttu-id="8da05-180">Üzerindeki sistem durumu bildirebilirsiniz `Partition`.</span><span class="sxs-lookup"><span data-stu-id="8da05-180">You can also report health on `Partition`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

<span data-ttu-id="8da05-181">Rapor sistem durumunu için `Application`, `DeployedApplication`, ve `DeployedServicePackage`, kullanmak `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="8da05-181">To report health on `Application`, `DeployedApplication`, and `DeployedServicePackage`, use  `CodePackageActivationContext`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a><span data-ttu-id="8da05-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8da05-182">Next steps</span></span>
* [<span data-ttu-id="8da05-183">Service Fabric sistem üzerinde derin Dalış</span><span class="sxs-lookup"><span data-stu-id="8da05-183">Deep dive on Service Fabric health</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="8da05-184">Hizmet durumu raporlama için REST API</span><span class="sxs-lookup"><span data-stu-id="8da05-184">REST API for reporting service health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [<span data-ttu-id="8da05-185">Uygulama durumu raporlama için REST API</span><span class="sxs-lookup"><span data-stu-id="8da05-185">REST API for reporting application health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

