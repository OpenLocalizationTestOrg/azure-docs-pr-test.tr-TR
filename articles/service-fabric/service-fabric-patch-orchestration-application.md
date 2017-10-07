---
title: "Service Fabric düzeltme eki orchestration uygulama aaaAzure | Microsoft Docs"
description: "Uygulama tooautomate işletim sistemi bir Service Fabric kümesi düzeltme eki uygulama."
services: service-fabric
documentationcenter: .net
author: novino
manager: timlt
editor: 
ms.assetid: de7dacf5-4038-434a-a265-5d0de80a9b1d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/9/2017
ms.author: nachandr
ms.openlocfilehash: fbb89aa2ea418181ee908a01850178c113c462fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="patch-hello-windows-operating-system-in-your-service-fabric-cluster"></a><span data-ttu-id="08c05-103">Service Fabric kümenizdeki Hello Windows işletim sistemi düzeltme eki</span><span class="sxs-lookup"><span data-stu-id="08c05-103">Patch hello Windows operating system in your Service Fabric cluster</span></span>

<span data-ttu-id="08c05-104">Merhaba düzeltme eki orchestration uygulama kapalı kalma süresi olmadan Azure üzerinde bir Service Fabric kümesindeki düzeltme eki uygulama işletim sistemi otomatikleştiren bir Azure Service Fabric uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="08c05-104">hello patch orchestration application is an Azure Service Fabric application that automates operating system patching on a Service Fabric cluster on Azure without downtime.</span></span>

<span data-ttu-id="08c05-105">Merhaba düzeltme eki orchestration uygulama hello şunları sağlar:</span><span class="sxs-lookup"><span data-stu-id="08c05-105">hello patch orchestration app provides hello following:</span></span>

- <span data-ttu-id="08c05-106">**Otomatik işletim sistemi güncelleştirme yüklemesini**.</span><span class="sxs-lookup"><span data-stu-id="08c05-106">**Automatic operating system update installation**.</span></span> <span data-ttu-id="08c05-107">İşletim sistemi güncelleştirmeleri otomatik olarak karşıdan yüklenir ve.</span><span class="sxs-lookup"><span data-stu-id="08c05-107">Operating system updates are automatically downloaded and installed.</span></span> <span data-ttu-id="08c05-108">Küme düğümleri küme kapalı kalma süresi olmadan gerektiği gibi yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="08c05-108">Cluster nodes are rebooted as needed without cluster downtime.</span></span>

- <span data-ttu-id="08c05-109">**Küme durumunu algılayan düzeltme eki uygulama ve sistem durumu tümleştirme**.</span><span class="sxs-lookup"><span data-stu-id="08c05-109">**Cluster-aware patching and health integration**.</span></span> <span data-ttu-id="08c05-110">Güncelleştirmeler uygulanırken hello düzeltme eki orchestration uygulama hello küme düğümleri hello durumunu izler.</span><span class="sxs-lookup"><span data-stu-id="08c05-110">While applying updates, hello patch orchestration app monitors hello health of hello cluster nodes.</span></span> <span data-ttu-id="08c05-111">Küme düğümü yükseltilmiş bir düğümde aynı anda bir saat ya da bir yükseltme etki alanı olan.</span><span class="sxs-lookup"><span data-stu-id="08c05-111">Cluster nodes are upgraded one node at a time or one upgrade domain at a time.</span></span> <span data-ttu-id="08c05-112">Hello küme Hello durumunu nedeniyle toohello düzeltme eki uygulama işlemi devre dışı kalırsa, düzeltme eki uygulama hello sorun aggravating durdurulmuş tooprevent ' dir.</span><span class="sxs-lookup"><span data-stu-id="08c05-112">If hello health of hello cluster goes down due toohello patching process, patching is stopped tooprevent aggravating hello problem.</span></span>

## <a name="internal-details-of-hello-app"></a><span data-ttu-id="08c05-113">Merhaba uygulamasının iç ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="08c05-113">Internal details of hello app</span></span>

<span data-ttu-id="08c05-114">Merhaba düzeltme eki orchestration uygulama bileşenleri şu Merhaba oluşur:</span><span class="sxs-lookup"><span data-stu-id="08c05-114">hello patch orchestration app is composed of hello following subcomponents:</span></span>

- <span data-ttu-id="08c05-115">**Düzenleyicisi hizmeti**: Bu durum bilgisi olan hizmet sorumludur:</span><span class="sxs-lookup"><span data-stu-id="08c05-115">**Coordinator Service**: This stateful service is responsible for:</span></span>
    - <span data-ttu-id="08c05-116">Denetleyici hello Windows Update işinde hello tüm küme.</span><span class="sxs-lookup"><span data-stu-id="08c05-116">Coordinating hello Windows Update job on hello entire cluster.</span></span>
    - <span data-ttu-id="08c05-117">Tamamlanan Windows Update işlemleri depolanmasını hello sonucu.</span><span class="sxs-lookup"><span data-stu-id="08c05-117">Storing hello result of completed Windows Update operations.</span></span>
- <span data-ttu-id="08c05-118">**Düğüm Aracısı hizmeti**: Bu durum bilgisiz hizmet tüm Service Fabric küme düğümleri üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="08c05-118">**Node Agent Service**: This stateless service runs on all Service Fabric cluster nodes.</span></span> <span data-ttu-id="08c05-119">Merhaba hizmet sorumludur:</span><span class="sxs-lookup"><span data-stu-id="08c05-119">hello service is responsible for:</span></span>
    - <span data-ttu-id="08c05-120">Önyükleme hello düğüm Aracısı NTService.</span><span class="sxs-lookup"><span data-stu-id="08c05-120">Bootstrapping hello Node Agent NTService.</span></span>
    - <span data-ttu-id="08c05-121">Merhaba düğüm Aracısı NTService izleme.</span><span class="sxs-lookup"><span data-stu-id="08c05-121">Monitoring hello Node Agent NTService.</span></span>
- <span data-ttu-id="08c05-122">**Düğüm Aracısı NTService**: Bu Windows NT hizmeti, üst düzey bir ayrıcalık (Sistem) çalışır.</span><span class="sxs-lookup"><span data-stu-id="08c05-122">**Node Agent NTService**: This Windows NT service runs at a higher-level privilege (SYSTEM).</span></span> <span data-ttu-id="08c05-123">Buna karşılık, hello düğüm Aracısı hizmeti ve hello Düzenleyicisi hizmetindeki bir alt düzey önceliği (ağ hizmeti) çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="08c05-123">In contrast, hello Node Agent Service and hello Coordinator Service run at a lower-level privilege (NETWORK SERVICE).</span></span> <span data-ttu-id="08c05-124">Merhaba hizmet hello tüm küme düğümlerinde Windows Update işleri aşağıdaki hello gerçekleştirmek için sorumludur:</span><span class="sxs-lookup"><span data-stu-id="08c05-124">hello service is responsible for performing hello following Windows Update jobs on all hello cluster nodes:</span></span>
    - <span data-ttu-id="08c05-125">Otomatik Windows Update hello düğüm üzerinde devre dışı bırakılıyor.</span><span class="sxs-lookup"><span data-stu-id="08c05-125">Disabling automatic Windows Update on hello node.</span></span>
    - <span data-ttu-id="08c05-126">Windows Update yükleyip toohello ilke hello kullanıcı according sağlamıştır.</span><span class="sxs-lookup"><span data-stu-id="08c05-126">Downloading and installing Windows Update according toohello policy hello user has provided.</span></span>
    - <span data-ttu-id="08c05-127">Merhaba makine post Windows Güncelleştirme yüklemesini yeniden başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="08c05-127">Restarting hello machine post Windows Update installation.</span></span>
    - <span data-ttu-id="08c05-128">Windows güncelleştirmeleri toohello Coordinator hizmeti Hello sonuçlarını karşıya yükleniyor.</span><span class="sxs-lookup"><span data-stu-id="08c05-128">Uploading hello results of Windows updates toohello Coordinator Service.</span></span>
    - <span data-ttu-id="08c05-129">Tüm yeniden denemeler tükenmesinden sonra bir işlem başarısız oldu durumda raporlama durumu raporları.</span><span class="sxs-lookup"><span data-stu-id="08c05-129">Reporting health reports in case an operation has failed after exhausting all retries.</span></span>

> [!NOTE]
> <span data-ttu-id="08c05-130">Merhaba düzeltme eki orchestration uygulama kullandığı hello Service Fabric Yöneticisi sistem hizmeti toodisable onarmak veya başlangıç düğümü etkinleştirin ve sistem durumu denetimleri gerçekleştirmek.</span><span class="sxs-lookup"><span data-stu-id="08c05-130">hello patch orchestration app uses hello Service Fabric repair manager system service toodisable or enable hello node and perform health checks.</span></span> <span data-ttu-id="08c05-131">Merhaba onarım görev hello düzeltme eki orchestration uygulama parçaları hello her düğüm için Windows Update ilerleme tarafından oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="08c05-131">hello repair task created by hello patch orchestration app tracks hello Windows Update progress for each node.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08c05-132">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="08c05-132">Prerequisites</span></span>

### <a name="minimum-supported-service-fabric-runtime-version"></a><span data-ttu-id="08c05-133">Service Fabric çalışma zamanı sürümü desteklenen en düşük</span><span class="sxs-lookup"><span data-stu-id="08c05-133">Minimum supported Service Fabric runtime version</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="08c05-134">Azure kümeleri</span><span class="sxs-lookup"><span data-stu-id="08c05-134">Azure clusters</span></span>
<span data-ttu-id="08c05-135">Merhaba düzeltme eki orchestration app Service Fabric çalışma zamanı sürümü v5.5 sahip Azure kümelerinde çalıştırılması gerekir ya da daha sonra.</span><span class="sxs-lookup"><span data-stu-id="08c05-135">hello patch orchestration app must be run on Azure clusters that have Service Fabric runtime version v5.5 or later.</span></span>

#### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="08c05-136">Tek başına şirket içi kümeleri</span><span class="sxs-lookup"><span data-stu-id="08c05-136">Standalone on-premises Clusters</span></span>
<span data-ttu-id="08c05-137">Merhaba düzeltme eki orchestration app Service Fabric çalışma zamanı sürümü v5.6 sahip tek başına kümelerinde çalıştırılması gerekir ya da daha sonra.</span><span class="sxs-lookup"><span data-stu-id="08c05-137">hello patch orchestration app must be run on Standalone clusters that have Service Fabric runtime version v5.6 or later.</span></span>

### <a name="enable-hello-repair-manager-service-if-its-not-running-already"></a><span data-ttu-id="08c05-138">(Bu zaten çalışmıyorsa) hello onarım Yöneticisi hizmetini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="08c05-138">Enable hello repair manager service (if it's not running already)</span></span>

<span data-ttu-id="08c05-139">Merhaba düzeltme eki orchestration uygulama hello kümede etkin hello onarım Yöneticisi sistem hizmeti toobe gerektirir.</span><span class="sxs-lookup"><span data-stu-id="08c05-139">hello patch orchestration app requires hello repair manager system service toobe enabled on hello cluster.</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="08c05-140">Azure kümeleri</span><span class="sxs-lookup"><span data-stu-id="08c05-140">Azure clusters</span></span>

<span data-ttu-id="08c05-141">Hello Yöneticisi hizmeti varsayılan olarak etkinleştirilmiş onarmaya hello Gümüş dayanıklılık katmanındaki Azure kümeniz vardır.</span><span class="sxs-lookup"><span data-stu-id="08c05-141">Azure clusters in hello silver durability tier have hello repair manager service enabled by default.</span></span> <span data-ttu-id="08c05-142">Merhaba altın dayanıklılık katmanı Azure kümelerde sahip olabilir veya hello onarım Yöneticisi hizmeti bu kümeleri oluşturulduğu bağlı olarak, etkin değil.</span><span class="sxs-lookup"><span data-stu-id="08c05-142">Azure clusters in hello gold durability tier might or might not have hello repair manager service enabled, depending on when those clusters were created.</span></span> <span data-ttu-id="08c05-143">Varsayılan olarak, hello Bronz dayanıklılık katmanı Azure kümelerde hello Yöneticisi hizmetinin etkinleştirilmiş onarmaya gerekmez.</span><span class="sxs-lookup"><span data-stu-id="08c05-143">Azure clusters in hello bronze durability tier, by default, do not have hello repair manager service enabled.</span></span> <span data-ttu-id="08c05-144">Merhaba hizmet zaten etkinleştirilmişse hello Sistem Hizmetleri bölümünde hello Service Fabric Explorer çalışmasını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08c05-144">If hello service is already enabled, you can see it running in hello system services section in hello Service Fabric Explorer.</span></span>

##### <a name="azure-portal"></a><span data-ttu-id="08c05-145">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="08c05-145">Azure portal</span></span>
<span data-ttu-id="08c05-146">Onarım Yöneticisi Azure portalından kümesinin kurma hello zaman etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08c05-146">You can enable repair manager from Azure portal at hello time of setting up of cluster.</span></span> <span data-ttu-id="08c05-147">Seçin `Include Repair Manager` altında seçeneği `Add on features` küme yapılandırmasının hello zaman.</span><span class="sxs-lookup"><span data-stu-id="08c05-147">Select `Include Repair Manager` option under `Add on features` at hello time of Cluster configuration.</span></span>
<span data-ttu-id="08c05-148">![Azure portalından etkinleştirme onarım Yöneticisi'nin resmi](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span><span class="sxs-lookup"><span data-stu-id="08c05-148">![Image of Enabling Repair Manager from Azure portal](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span></span>

##### <a name="azure-resource-manager-template"></a><span data-ttu-id="08c05-149">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="08c05-149">Azure Resource Manager template</span></span>
<span data-ttu-id="08c05-150">Alternatif olarak, hello kullanabilirsiniz [Azure Resource Manager şablonu](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable hello onarım Yöneticisi hizmetine yeni ve mevcut Service Fabric kümeleri.</span><span class="sxs-lookup"><span data-stu-id="08c05-150">Alternatively you can use hello [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable hello repair manager service on new and existing Service Fabric clusters.</span></span> <span data-ttu-id="08c05-151">Merhaba şablonu toodeploy istediğiniz hello küme için alın.</span><span class="sxs-lookup"><span data-stu-id="08c05-151">Get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="08c05-152">Merhaba örnek şablonları kullanabilir veya özel bir Resource Manager şablonu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08c05-152">You can either use hello sample templates or create a custom Resource Manager template.</span></span> 

<span data-ttu-id="08c05-153">tooenable hello onarım Yöneticisi hizmetini kullanarak [Azure Resource Manager şablonu](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span><span class="sxs-lookup"><span data-stu-id="08c05-153">tooenable hello repair manager service using [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span></span>

1. <span data-ttu-id="08c05-154">İlk olarak bu hello denetleyin `apiversion` çok ayarlanır`2017-07-01-preview` hello için `Microsoft.ServiceFabric/clusters` hello aşağıdaki kod parçacığında gösterildiği gibi kaynak.</span><span class="sxs-lookup"><span data-stu-id="08c05-154">First check that hello `apiversion` is set too`2017-07-01-preview` for hello `Microsoft.ServiceFabric/clusters` resource, as shown in hello following snippet.</span></span> <span data-ttu-id="08c05-155">Farklı sonra tooupdate hello gereksinim `apiVersion` toohello değeri `2017-07-01-preview`:</span><span class="sxs-lookup"><span data-stu-id="08c05-155">If it is different, then you need tooupdate hello `apiVersion` toohello value `2017-07-01-preview`:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="08c05-156">Merhaba aşağıdakileri ekleyerek hello onarım Yöneticisi hizmeti şimdi etkinleştirmek `addonFeatures` bölümünden hello sonra `fabricSettings` bölümü:</span><span class="sxs-lookup"><span data-stu-id="08c05-156">Now enable hello repair manager service by adding hello following `addonFeatures` section after hello `fabricSettings` section:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="08c05-157">Bu değişikliklerle küme şablonunuzu güncelleştirildikten sonra bunları uygulamak ve son hello yükseltme sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08c05-157">After you have updated your cluster template with these changes, apply them and let hello upgrade finish.</span></span> <span data-ttu-id="08c05-158">Kümenizde çalışan hello onarım Yöneticisi sistem hizmeti şimdi görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08c05-158">You can now see hello repair manager system service running in your cluster.</span></span> <span data-ttu-id="08c05-159">Çağrılır `fabric:/System/RepairManagerService` hello Sistem Hizmetleri bölümünde hello Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="08c05-159">It is called `fabric:/System/RepairManagerService` in hello system services section in hello Service Fabric Explorer.</span></span> 

### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="08c05-160">Tek başına şirket içi kümeleri</span><span class="sxs-lookup"><span data-stu-id="08c05-160">Standalone on-premises clusters</span></span>

<span data-ttu-id="08c05-161">Merhaba kullanabilirsiniz [tek başına Windows kümesi için yapılandırma ayarlarını](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable hello onarım Yöneticisi hizmetine yeni ve mevcut Service Fabric kümesi.</span><span class="sxs-lookup"><span data-stu-id="08c05-161">You can use hello [Configuration settings for standalone Windows cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable hello repair manager service on new and existing Service Fabric cluster.</span></span>

<span data-ttu-id="08c05-162">tooenable hello onarım Yöneticisi hizmeti:</span><span class="sxs-lookup"><span data-stu-id="08c05-162">tooenable hello repair manager service:</span></span>

1. <span data-ttu-id="08c05-163">İlk olarak bu hello denetleyin `apiversion` içinde [genel küme yapılandırmaları](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) çok ayarlanır`04-2017` veya üstü:</span><span class="sxs-lookup"><span data-stu-id="08c05-163">First check that hello `apiversion` in [General cluster configurations](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) is set too`04-2017` or higher:</span></span>

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. <span data-ttu-id="08c05-164">Merhaba aşağıdakileri ekleyerek onarım Yöneticisi hizmeti şimdi etkinleştirmek `addonFeaturres` bölümünden hello sonra `fabricSettings` bölümünde aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="08c05-164">Now enable repair manager service by adding hello following `addonFeaturres` section after hello `fabricSettings` section as shown below:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="08c05-165">Küme bildiriminizi güncelleştirilmiş hello küme bildirimini kullanarak bu değişikliklerle güncelleştirmek [yeni küme oluşturma](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) veya [yükseltme hello küme yapılandırması](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span><span class="sxs-lookup"><span data-stu-id="08c05-165">Update your cluster manifest with these changes, using hello updated cluster manifest [create a new cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) or [upgrade hello cluster configuration](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span></span> <span data-ttu-id="08c05-166">Merhaba küme güncelleştirilmiş küme bildirimini ile çalışmaya başladıktan sonra artık hello onarım Yöneticisi sistem hizmeti olarak adlandırılır, kümede çalışan görebilirsiniz `fabric:/System/RepairManagerService`altında sistem hizmetleri hello Service Fabric explorer bölümünde.</span><span class="sxs-lookup"><span data-stu-id="08c05-166">Once hello cluster is running with updated cluster manifest, you can now see hello repair manager system service running in your cluster, which is called `fabric:/System/RepairManagerService`, under system services section in hello Service Fabric explorer.</span></span>

### <a name="disable-automatic-windows-update-on-all-nodes"></a><span data-ttu-id="08c05-167">Tüm düğümlerde otomatik Windows Update devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="08c05-167">Disable automatic Windows Update on all nodes</span></span>

<span data-ttu-id="08c05-168">Birden çok küme düğümleri aynı hello yeniden başlatarak, otomatik Windows güncelleştirmelerini tooavailability kaybına neden zaman.</span><span class="sxs-lookup"><span data-stu-id="08c05-168">Automatic Windows updates might lead tooavailability loss because multiple cluster nodes can restart at hello same time.</span></span> <span data-ttu-id="08c05-169">Varsayılan olarak, çalıştığında toodisable Hello düzeltme eki orchestration uygulama, her küme düğümünde otomatik Windows Update hello.</span><span class="sxs-lookup"><span data-stu-id="08c05-169">hello patch orchestration app, by default, tries toodisable hello automatic Windows Update on each cluster node.</span></span> <span data-ttu-id="08c05-170">Ancak, Hello ayarları Grup İlkesi veya bir yönetici tarafından yönetiliyorsa, ayarı hello Windows Update ilke çok "bildir önce yükleme" açıkça öneririz.</span><span class="sxs-lookup"><span data-stu-id="08c05-170">However, if hello settings are managed by an administrator or group policy, we recommend setting hello Windows Update policy too“Notify before Download” explicitly.</span></span>

### <a name="optional-enable-azure-diagnostics"></a><span data-ttu-id="08c05-171">İsteğe bağlı: Azure tanılamayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="08c05-171">Optional: Enable Azure Diagnostics</span></span>

<span data-ttu-id="08c05-172">Service Fabric çalışma zamanı sürümü çalıştıran kümeler `5.6.220.9494` ve yukarıdaki toplama düzeltme eki orchestration uygulama günlükleri Service Fabric bir parçası olarak günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="08c05-172">Clusters running Service Fabric runtime version `5.6.220.9494` and above collect patch orchestration app logs as part of Service Fabric logs.</span></span>
<span data-ttu-id="08c05-173">Kümenizi Service Fabric çalışma zamanı sürümünde çalışıyorsa, bu adımı atlayabilirsiniz `5.6.220.9494` ve üstü.</span><span class="sxs-lookup"><span data-stu-id="08c05-173">You can skip this step if your cluster is running on Service Fabric runtime version `5.6.220.9494` and above.</span></span>

<span data-ttu-id="08c05-174">Service Fabric çalışma zamanı sürümü çalıştıran kümeler için değerinden `5.6.220.9494`, günlükleri hello düzeltme eki orchestration uygulama için toplanan yerel olarak her hello küme düğümleri üzerinde.</span><span class="sxs-lookup"><span data-stu-id="08c05-174">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs for hello patch orchestration app are collected locally on each of hello cluster nodes.</span></span>
<span data-ttu-id="08c05-175">Azure tanılama tooupload günlükleri tüm düğümleri tooa merkezi konumdan yapılandırmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="08c05-175">We recommend that you configure Azure Diagnostics tooupload logs from all nodes tooa central location.</span></span>

<span data-ttu-id="08c05-176">Azure Tanılama'yı etkinleştirme hakkında daha fazla bilgi için bkz: [Azure tanılama kullanarak günlükleri toplamak](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span><span class="sxs-lookup"><span data-stu-id="08c05-176">For information on enabling Azure Diagnostics, see [Collect logs by using Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span></span>

<span data-ttu-id="08c05-177">Merhaba düzeltme eki orchestration uygulama günlüklerini sabit sağlayıcısı kimlikleri aşağıdaki hello üzerinde oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="08c05-177">Logs for hello patch orchestration app are generated on hello following fixed provider IDs:</span></span>

- <span data-ttu-id="08c05-178">e39b723c-590c-4090-abb0-11e3e6616346</span><span class="sxs-lookup"><span data-stu-id="08c05-178">e39b723c-590c-4090-abb0-11e3e6616346</span></span>
- <span data-ttu-id="08c05-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span><span class="sxs-lookup"><span data-stu-id="08c05-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span></span>
- <span data-ttu-id="08c05-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span><span class="sxs-lookup"><span data-stu-id="08c05-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span></span>
- <span data-ttu-id="08c05-181">05dc046c-60e9-4ef7-965e-91660adffa68</span><span class="sxs-lookup"><span data-stu-id="08c05-181">05dc046c-60e9-4ef7-965e-91660adffa68</span></span>

<span data-ttu-id="08c05-182">Resource Manager şablonu goto içinde `EtwEventSourceProviderConfiguration` altında bölümünde `WadCfg` ve girişleri aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="08c05-182">In Resource Manager template goto `EtwEventSourceProviderConfiguration` section under `WadCfg` and add hello following entries:</span></span>

```json
  {
    "provider": "e39b723c-590c-4090-abb0-11e3e6616346",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
      "eventDestination": "PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "fc0028ff-bfdc-499f-80dc-ed922c52c5e9",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "24afa313-0d3b-4c7c-b485-1047fd964b60",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "05dc046c-60e9-4ef7-965e-91660adffa68",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  }
```

> [!NOTE]
> <span data-ttu-id="08c05-183">Birden çok düğüm türleri, Service Fabric kümesi var. sonra tüm Merhaba hello önceki bölümde eklediğiniz `WadCfg` bölümler.</span><span class="sxs-lookup"><span data-stu-id="08c05-183">If your Service Fabric cluster has multiple node types, then hello previous section must be added for all hello `WadCfg` sections.</span></span>

## <a name="download-hello-app-package"></a><span data-ttu-id="08c05-184">Merhaba uygulama paketini indirin</span><span class="sxs-lookup"><span data-stu-id="08c05-184">Download hello app package</span></span>

<span data-ttu-id="08c05-185">Hello Hello uygulamayı karşıdan [bağlantı karşıdan](https://go.microsoft.com/fwlink/P/?linkid=849590).</span><span class="sxs-lookup"><span data-stu-id="08c05-185">Download hello application from hello [download link](https://go.microsoft.com/fwlink/P/?linkid=849590).</span></span>

## <a name="configure-hello-app"></a><span data-ttu-id="08c05-186">Merhaba uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="08c05-186">Configure hello app</span></span>

<span data-ttu-id="08c05-187">Merhaba hello düzeltme eki orchestration uygulamanın davranışı yapılandırılmış toomeet gereksinimlerinizi olabilir.</span><span class="sxs-lookup"><span data-stu-id="08c05-187">hello behavior of hello patch orchestration app can be configured toomeet your needs.</span></span> <span data-ttu-id="08c05-188">Uygulama oluşturma veya güncelleştirme işlemi sırasında hello uygulama parametresini geçirerek Hello varsayılan değerlerini geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="08c05-188">Override hello default values by passing in hello application parameter during application creation or update.</span></span> <span data-ttu-id="08c05-189">Uygulama parametreleri belirterek sağlanabilir `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` veya `New-ServiceFabricApplication` cmdlet'leri.</span><span class="sxs-lookup"><span data-stu-id="08c05-189">Application parameters can be provided by specifying `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` or `New-ServiceFabricApplication` cmdlets.</span></span>

|<span data-ttu-id="08c05-190">**Parametre**</span><span class="sxs-lookup"><span data-stu-id="08c05-190">**Parameter**</span></span>        |<span data-ttu-id="08c05-191">**Tür**</span><span class="sxs-lookup"><span data-stu-id="08c05-191">**Type**</span></span>                          | <span data-ttu-id="08c05-192">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="08c05-192">**Details**</span></span>|
|:-|-|-|
|<span data-ttu-id="08c05-193">MaxResultsToCache</span><span class="sxs-lookup"><span data-stu-id="08c05-193">MaxResultsToCache</span></span>    |<span data-ttu-id="08c05-194">Uzun</span><span class="sxs-lookup"><span data-stu-id="08c05-194">Long</span></span>                              | <span data-ttu-id="08c05-195">Önbelleğe alınması gereken Windows Update sonuçlarının maksimum sayısı.</span><span class="sxs-lookup"><span data-stu-id="08c05-195">Maximum number of Windows Update results, which should be cached.</span></span> <br><span data-ttu-id="08c05-196">Varsayılan değer 3000 varsayılır:</span><span class="sxs-lookup"><span data-stu-id="08c05-196">Default value is 3000 assuming the:</span></span> <br> <span data-ttu-id="08c05-197">-Düğüm sayısı 20'dir.</span><span class="sxs-lookup"><span data-stu-id="08c05-197">- Number of nodes is 20.</span></span> <br> <span data-ttu-id="08c05-198">-Ayda bir düğümde gerçekleştiği güncelleştirme sayısı beştir.</span><span class="sxs-lookup"><span data-stu-id="08c05-198">- Number of updates happening on a node per month is five.</span></span> <br> <span data-ttu-id="08c05-199">-İşlemi başına sonuç sayısı 10 olabilir.</span><span class="sxs-lookup"><span data-stu-id="08c05-199">- Number of results per operation can be 10.</span></span> <br> <span data-ttu-id="08c05-200">-Sonuçlar hello son üç ay için depolanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="08c05-200">- Results for hello past three months should be stored.</span></span> |
|<span data-ttu-id="08c05-201">TaskApprovalPolicy</span><span class="sxs-lookup"><span data-stu-id="08c05-201">TaskApprovalPolicy</span></span>   |<span data-ttu-id="08c05-202">Enum</span><span class="sxs-lookup"><span data-stu-id="08c05-202">Enum</span></span> <br> <span data-ttu-id="08c05-203">{NodeWise, UpgradeDomainWise}</span><span class="sxs-lookup"><span data-stu-id="08c05-203">{ NodeWise, UpgradeDomainWise }</span></span>                          |<span data-ttu-id="08c05-204">TaskApprovalPolicy hello Service Fabric küme düğümleri arasında hello Coordinator hizmeti tooinstall Windows güncelleştirmelerini tarafından kullanılan toobe hello İlkesi gösterir.</span><span class="sxs-lookup"><span data-stu-id="08c05-204">TaskApprovalPolicy indicates hello policy that is toobe used by hello Coordinator Service tooinstall Windows updates across hello Service Fabric cluster nodes.</span></span><br>                         <span data-ttu-id="08c05-205">İzin verilen değerler:</span><span class="sxs-lookup"><span data-stu-id="08c05-205">Allowed values are:</span></span> <br>                                                           <span data-ttu-id="08c05-206"><b>NodeWise</b>.</span><span class="sxs-lookup"><span data-stu-id="08c05-206"><b>NodeWise</b>.</span></span> <span data-ttu-id="08c05-207">Windows Update yüklü bir aynı anda düğümdür.</span><span class="sxs-lookup"><span data-stu-id="08c05-207">Windows Update is installed one node at a time.</span></span> <br>                                                           <span data-ttu-id="08c05-208"><b>UpgradeDomainWise</b>.</span><span class="sxs-lookup"><span data-stu-id="08c05-208"><b>UpgradeDomainWise</b>.</span></span> <span data-ttu-id="08c05-209">Windows Update aynı anda yüklü bir yükseltme etki alanıdır.</span><span class="sxs-lookup"><span data-stu-id="08c05-209">Windows Update is installed one upgrade domain at a time.</span></span> <span data-ttu-id="08c05-210">(En fazla hello sırasında Windows Update tooan yükseltme etki alanına ait tüm hello düğümleri gidebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="08c05-210">(At hello maximum, all hello nodes belonging tooan upgrade domain can go for Windows Update.)</span></span>
|<span data-ttu-id="08c05-211">LogsDiskQuotaInMB</span><span class="sxs-lookup"><span data-stu-id="08c05-211">LogsDiskQuotaInMB</span></span>   |<span data-ttu-id="08c05-212">Uzun</span><span class="sxs-lookup"><span data-stu-id="08c05-212">Long</span></span>  <br> <span data-ttu-id="08c05-213">(Varsayılan: 1024)</span><span class="sxs-lookup"><span data-stu-id="08c05-213">(Default: 1024)</span></span>               |<span data-ttu-id="08c05-214">Yerel olarak düğümlerinde kalıcı MB cinsinden en büyük boyutunu düzeltme eki orchestration uygulama kaydeder.</span><span class="sxs-lookup"><span data-stu-id="08c05-214">Maximum size of patch orchestration app logs in MB, which can be persisted locally on nodes.</span></span>
| <span data-ttu-id="08c05-215">WUQuery</span><span class="sxs-lookup"><span data-stu-id="08c05-215">WUQuery</span></span>               | <span data-ttu-id="08c05-216">Dize</span><span class="sxs-lookup"><span data-stu-id="08c05-216">string</span></span><br><span data-ttu-id="08c05-217">(Varsayılan: "IsInstalled = 0")</span><span class="sxs-lookup"><span data-stu-id="08c05-217">(Default: "IsInstalled=0")</span></span>                | <span data-ttu-id="08c05-218">Sorgu tooget Windows güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="08c05-218">Query tooget Windows updates.</span></span> <span data-ttu-id="08c05-219">Daha fazla bilgi için bkz: [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="08c05-219">For more information, see [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span></span>
| <span data-ttu-id="08c05-220">InstallWindowsOSOnlyUpdates</span><span class="sxs-lookup"><span data-stu-id="08c05-220">InstallWindowsOSOnlyUpdates</span></span> | <span data-ttu-id="08c05-221">bool</span><span class="sxs-lookup"><span data-stu-id="08c05-221">Bool</span></span> <br> <span data-ttu-id="08c05-222">(varsayılan: True)</span><span class="sxs-lookup"><span data-stu-id="08c05-222">(default: True)</span></span>                 | <span data-ttu-id="08c05-223">Bu bayrak, Windows işletim sistemi güncelleştirmeleri toobe yüklü sağlar.</span><span class="sxs-lookup"><span data-stu-id="08c05-223">This flag allows Windows operating system updates toobe installed.</span></span>            |
| <span data-ttu-id="08c05-224">WUOperationTimeOutInMinutes</span><span class="sxs-lookup"><span data-stu-id="08c05-224">WUOperationTimeOutInMinutes</span></span> | <span data-ttu-id="08c05-225">Int</span><span class="sxs-lookup"><span data-stu-id="08c05-225">Int</span></span> <br><span data-ttu-id="08c05-226">(Varsayılan: 90).</span><span class="sxs-lookup"><span data-stu-id="08c05-226">(Default: 90)</span></span>                   | <span data-ttu-id="08c05-227">Herhangi bir Windows Update işlemi (arama veya indirme veya yükleme) için Hello zaman aşımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="08c05-227">Specifies hello timeout for any Windows Update operation (search or download or install).</span></span> <span data-ttu-id="08c05-228">İçinde Hello işlemi tamamlanmazsa Merhaba belirtilen zaman aşımı, iptal edilir.</span><span class="sxs-lookup"><span data-stu-id="08c05-228">If hello operation is not completed within hello specified timeout, it is aborted.</span></span>       |
| <span data-ttu-id="08c05-229">WURescheduleCount</span><span class="sxs-lookup"><span data-stu-id="08c05-229">WURescheduleCount</span></span>     | <span data-ttu-id="08c05-230">Int</span><span class="sxs-lookup"><span data-stu-id="08c05-230">Int</span></span> <br> <span data-ttu-id="08c05-231">(Varsayılan: 5).</span><span class="sxs-lookup"><span data-stu-id="08c05-231">(Default: 5)</span></span>                  | <span data-ttu-id="08c05-232">bir işlem kalıcı olarak başarısız olursa Windows hello en fazla kaç kez hello hello hizmet reschedules güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="08c05-232">hello maximum number of times hello service reschedules hello Windows update in case an operation fails persistently.</span></span>          |
| <span data-ttu-id="08c05-233">WURescheduleTimeInMinutes</span><span class="sxs-lookup"><span data-stu-id="08c05-233">WURescheduleTimeInMinutes</span></span> | <span data-ttu-id="08c05-234">Int</span><span class="sxs-lookup"><span data-stu-id="08c05-234">Int</span></span> <br><span data-ttu-id="08c05-235">(Varsayılan: 30).</span><span class="sxs-lookup"><span data-stu-id="08c05-235">(Default: 30)</span></span> | <span data-ttu-id="08c05-236">Hata devam ederse durumunda Windows güncelleştirme sırasında hangi hello hizmet hello reschedules hello aralığı.</span><span class="sxs-lookup"><span data-stu-id="08c05-236">hello interval at which hello service reschedules hello Windows update in case failure persists.</span></span> |
| <span data-ttu-id="08c05-237">WUFrequency</span><span class="sxs-lookup"><span data-stu-id="08c05-237">WUFrequency</span></span>           | <span data-ttu-id="08c05-238">Virgülle ayrılmış dize (varsayılan: "Haftalık, Çarşamba, 7:00:00")</span><span class="sxs-lookup"><span data-stu-id="08c05-238">Comma-separated string (Default: "Weekly, Wednesday, 7:00:00")</span></span>     | <span data-ttu-id="08c05-239">Windows Update yükleme hello sıklığı.</span><span class="sxs-lookup"><span data-stu-id="08c05-239">hello frequency for installing Windows Update.</span></span> <span data-ttu-id="08c05-240">Merhaba biçimi ve olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="08c05-240">hello format and possible values are:</span></span> <br><span data-ttu-id="08c05-241">-Örneğin, aylık, 5, 12 aylık, gg ss: 22:32.</span><span class="sxs-lookup"><span data-stu-id="08c05-241">-   Monthly, DD,HH:MM:SS, for example, Monthly, 5,12:22:32.</span></span> <br> <span data-ttu-id="08c05-242">-Örneğin, haftalık, Salı, 12:22:32 için haftalık, gün, ss.</span><span class="sxs-lookup"><span data-stu-id="08c05-242">-   Weekly, DAY,HH:MM:SS, for example, Weekly, Tuesday, 12:22:32.</span></span>  <br> <span data-ttu-id="08c05-243">-Örneğin, günlük, 12:22:32 günlük, ss.</span><span class="sxs-lookup"><span data-stu-id="08c05-243">-   Daily, HH:MM:SS, for example, Daily, 12:22:32.</span></span>  <br> <span data-ttu-id="08c05-244">-Hiçbiri, Windows Update yapılması döndürmemelidir gösterir.</span><span class="sxs-lookup"><span data-stu-id="08c05-244">-  None indicates that Windows Update shouldn't be done.</span></span>  <br><br> <span data-ttu-id="08c05-245">Tüm hello saatler UTC biçiminde olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="08c05-245">Note that all hello times are in UTC.</span></span>|
| <span data-ttu-id="08c05-246">AcceptWindowsUpdateEula</span><span class="sxs-lookup"><span data-stu-id="08c05-246">AcceptWindowsUpdateEula</span></span> | <span data-ttu-id="08c05-247">bool</span><span class="sxs-lookup"><span data-stu-id="08c05-247">Bool</span></span> <br><span data-ttu-id="08c05-248">(Varsayılan: true)</span><span class="sxs-lookup"><span data-stu-id="08c05-248">(Default: true)</span></span> | <span data-ttu-id="08c05-249">Bu bayrak ayarlayarak Merhaba uygulaması hello Windows Update için son kullanıcı lisans sözleşmesi hello makine hello sahibi adına kabul eder.</span><span class="sxs-lookup"><span data-stu-id="08c05-249">By setting this flag, hello application accepts hello End-User License Agreement for Windows Update on behalf of hello owner of hello machine.</span></span>              |

> [!TIP]
> <span data-ttu-id="08c05-250">Windows Update toohappen hemen istiyorsanız ayarlayın `WUFrequency` göreli toohello uygulama dağıtım süresini.</span><span class="sxs-lookup"><span data-stu-id="08c05-250">If you want Windows Update toohappen immediately, set `WUFrequency` relative toohello application deployment time.</span></span> <span data-ttu-id="08c05-251">Örneğin, bir beş düğümlü test kümesi ve planı toodeploy hello uygulaması yaklaşık 5: 00'da olduğunu varsayalım UTC.</span><span class="sxs-lookup"><span data-stu-id="08c05-251">For example, suppose that you have a five-node test cluster and plan toodeploy hello app at around 5:00 PM UTC.</span></span> <span data-ttu-id="08c05-252">Merhaba uygulama yükseltme veya dağıtım sırasında 30 dakika sürer olduğunu varsayarsak, en fazla, ayarlanmış hello WUFrequency "Günlük, 17:30:00." Merhaba</span><span class="sxs-lookup"><span data-stu-id="08c05-252">If you assume that hello application upgrade or deployment takes 30 minutes at hello maximum, set hello WUFrequency as "Daily, 17:30:00."</span></span>

## <a name="deploy-hello-app"></a><span data-ttu-id="08c05-253">Merhaba uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="08c05-253">Deploy hello app</span></span>

1. <span data-ttu-id="08c05-254">Tüm hello önkoşul adımlarını tooprepare hello küme tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="08c05-254">Finish all hello prerequisite steps tooprepare hello cluster.</span></span>
2. <span data-ttu-id="08c05-255">Başka bir Service Fabric uygulaması gibi Hello düzeltme eki orchestration uygulamasını dağıtın.</span><span class="sxs-lookup"><span data-stu-id="08c05-255">Deploy hello patch orchestration app like any other Service Fabric app.</span></span> <span data-ttu-id="08c05-256">PowerShell kullanarak hello uygulama dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08c05-256">You can deploy hello app by using PowerShell.</span></span> <span data-ttu-id="08c05-257">Merhaba adımları [PowerShell kullanarak uygulamaları dağıtma ve Kaldır](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="08c05-257">Follow hello steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>
3. <span data-ttu-id="08c05-258">tooconfigure hello Uygulama dağıtımının geçişi hello hello zamanında `ApplicationParamater` toohello `New-ServiceFabricApplication` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="08c05-258">tooconfigure hello application at hello time of deployment, pass hello `ApplicationParamater` toohello `New-ServiceFabricApplication` cmdlet.</span></span> <span data-ttu-id="08c05-259">Size kolaylık olması için hello betik Deploy.ps1 Merhaba uygulaması birlikte sağladık.</span><span class="sxs-lookup"><span data-stu-id="08c05-259">For your convenience, we’ve provided hello script Deploy.ps1 along with hello application.</span></span> <span data-ttu-id="08c05-260">toouse hello komut dosyası:</span><span class="sxs-lookup"><span data-stu-id="08c05-260">toouse hello script:</span></span>

    - <span data-ttu-id="08c05-261">Tooa Service Fabric kümesi kullanarak bağlanmak `Connect-ServiceFabricCluster`.</span><span class="sxs-lookup"><span data-stu-id="08c05-261">Connect tooa Service Fabric cluster by using `Connect-ServiceFabricCluster`.</span></span>
    - <span data-ttu-id="08c05-262">Merhaba PowerShell betiğini Deploy.ps1 hello uygun yürütün `ApplicationParameter` değeri.</span><span class="sxs-lookup"><span data-stu-id="08c05-262">Execute hello PowerShell script Deploy.ps1 with hello appropriate `ApplicationParameter` value.</span></span>

> [!NOTE]
> <span data-ttu-id="08c05-263">Merhaba komut dosyası ve hello uygulama klasörü PatchOrchestrationApplication hello tutmak aynı dizin.</span><span class="sxs-lookup"><span data-stu-id="08c05-263">Keep hello script and hello application folder PatchOrchestrationApplication in hello same directory.</span></span>

## <a name="upgrade-hello-app"></a><span data-ttu-id="08c05-264">Merhaba uygulama yükseltme</span><span class="sxs-lookup"><span data-stu-id="08c05-264">Upgrade hello app</span></span>

<span data-ttu-id="08c05-265">tooupgrade PowerShell kullanarak mevcut bir düzeltme eki orchestration uygulamayı izleyin hello adımlarda [PowerShell kullanarak Service Fabric uygulama yükseltme](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span><span class="sxs-lookup"><span data-stu-id="08c05-265">tooupgrade an existing patch orchestration app by using PowerShell, follow hello steps in [Service Fabric application upgrade using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span></span>

## <a name="remove-hello-app"></a><span data-ttu-id="08c05-266">Merhaba uygulamasını kaldırın</span><span class="sxs-lookup"><span data-stu-id="08c05-266">Remove hello app</span></span>

<span data-ttu-id="08c05-267">tooremove hello uygulama izleme hello adımlarda [PowerShell kullanarak uygulamaları dağıtma ve Kaldır](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="08c05-267">tooremove hello application, follow hello steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>

<span data-ttu-id="08c05-268">Size kolaylık olması için hello betik Undeploy.ps1 Merhaba uygulaması birlikte sağladık.</span><span class="sxs-lookup"><span data-stu-id="08c05-268">For your convenience, we've provided hello script Undeploy.ps1 along with hello application.</span></span> <span data-ttu-id="08c05-269">toouse hello komut dosyası:</span><span class="sxs-lookup"><span data-stu-id="08c05-269">toouse hello script:</span></span>

  - <span data-ttu-id="08c05-270">Tooa Service Fabric kümesi kullanarak bağlanmak ```Connect-ServiceFabricCluster```.</span><span class="sxs-lookup"><span data-stu-id="08c05-270">Connect tooa Service Fabric cluster by using ```Connect-ServiceFabricCluster```.</span></span>

  - <span data-ttu-id="08c05-271">Merhaba PowerShell betiğini Undeploy.ps1 yürütün.</span><span class="sxs-lookup"><span data-stu-id="08c05-271">Execute hello PowerShell script Undeploy.ps1.</span></span>

> [!NOTE]
> <span data-ttu-id="08c05-272">Merhaba komut dosyası ve hello uygulama klasörü PatchOrchestrationApplication hello tutmak aynı dizin.</span><span class="sxs-lookup"><span data-stu-id="08c05-272">Keep hello script and hello application folder PatchOrchestrationApplication in hello same directory.</span></span>

## <a name="view-hello-windows-update-results"></a><span data-ttu-id="08c05-273">Merhaba Windows Update sonuçları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="08c05-273">View hello Windows Update results</span></span>

<span data-ttu-id="08c05-274">Merhaba düzeltme eki orchestration uygulama REST API'leri toodisplay hello geçmiş sonuçlarını toohello kullanıcı kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="08c05-274">hello patch orchestration app exposes REST APIs toodisplay hello historical results toohello user.</span></span> <span data-ttu-id="08c05-275">Merhaba sonuç JSON örneği:</span><span class="sxs-lookup"><span data-stu-id="08c05-275">An example of hello result JSON:</span></span>
```json
[
  {
    "NodeName": "_stg1vm_1",
    "WindowsUpdateOperationResults": [
      {
        "OperationResult": 0,
        "NodeName": "_stg1vm_1",
        "OperationTime": "2017-05-21T11:46:52.1953713Z",
        "UpdateDetails": [
          {
            "UpdateId": "7392acaf-6a85-427c-8a8d-058c25beb0d6",
            "Title": "Cumulative Security Update for Internet Explorer 11 for Windows Server 2012 R2 (KB3185319)",
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of hello issues that are included in this update, see hello associated Microsoft Knowledge Base article. After you install this update, you may have toorestart your system.",
            "ResultCode": 0
          }
        ],
        "OperationType": 1,
        "WindowsUpdateQuery": "IsInstalled=0",
        "WindowsUpdateFrequency": "Daily,10:00:00",
        "RebootRequired": false
      }
    ]
  },
  ...
]
```
<span data-ttu-id="08c05-276">Hiçbir güncelleştirme henüz planlandıysa hello sonuç JSON boştur.</span><span class="sxs-lookup"><span data-stu-id="08c05-276">If no update is scheduled yet, hello result JSON is empty.</span></span>

<span data-ttu-id="08c05-277">Toohello küme tooquery Windows Update sonuçları günlüğü.</span><span class="sxs-lookup"><span data-stu-id="08c05-277">Log in toohello cluster tooquery Windows Update results.</span></span> <span data-ttu-id="08c05-278">Ardından hello Coordinator hizmeti hello birincil hello çoğaltma adresini bulmak ve hello tarayıcı hello URL'den isabet: http://&lt;çoğaltma IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1 / GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="08c05-278">Then find out hello replica address for hello primary of hello Coordinator Service, and hit hello URL from hello browser: http://&lt;REPLICA-IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="08c05-279">Merhaba REST uç noktasını hello Coordinator hizmeti için dinamik bir bağlantı noktası var.</span><span class="sxs-lookup"><span data-stu-id="08c05-279">hello REST endpoint for hello Coordinator Service has a dynamic port.</span></span> <span data-ttu-id="08c05-280">toocheck tam URL'yi Merhaba, toohello Service Fabric Explorer bakın.</span><span class="sxs-lookup"><span data-stu-id="08c05-280">toocheck hello exact URL, refer toohello Service Fabric Explorer.</span></span> <span data-ttu-id="08c05-281">Örneğin, hello sonuçları kullanılabilir `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span><span class="sxs-lookup"><span data-stu-id="08c05-281">For example, hello results are available at `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span></span>

![REST uç noktasını görüntüsü](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


<span data-ttu-id="08c05-283">Merhaba ters proxy hello kümede etkinleştirilirse, hello küme dışındaki hello URL'den erişebilir.</span><span class="sxs-lookup"><span data-stu-id="08c05-283">If hello reverse proxy is enabled on hello cluster, you can access hello URL from outside of hello cluster as well.</span></span>
<span data-ttu-id="08c05-284">toobe gereken uç nokta hello isabet olduğu http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="08c05-284">hello endpoint that needs toobe hit is http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="08c05-285">tooenable hello ters proxy hello kümede izleyin hello adımlarda [ters proxy Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span><span class="sxs-lookup"><span data-stu-id="08c05-285">tooenable hello reverse proxy on hello cluster, follow hello steps in [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span></span> 

> 
> [!WARNING]
> <span data-ttu-id="08c05-286">Hello ters proxy yapılandırıldıktan sonra bir HTTP uç noktası kullanıma tüm mikro hizmetler hello kümedeki hello küme dışında adreslenebilir.</span><span class="sxs-lookup"><span data-stu-id="08c05-286">After hello reverse proxy is configured, all micro services in hello cluster that expose an HTTP endpoint are addressable from outside hello cluster.</span></span>

## <a name="diagnosticshealth-events"></a><span data-ttu-id="08c05-287">Tanılama/sistem durumu olayları</span><span class="sxs-lookup"><span data-stu-id="08c05-287">Diagnostics/health events</span></span>

### <a name="collect-patch-orchestration-app-logs"></a><span data-ttu-id="08c05-288">Toplama düzeltme eki orchestration uygulama günlükleri</span><span class="sxs-lookup"><span data-stu-id="08c05-288">Collect patch orchestration app logs</span></span>

<span data-ttu-id="08c05-289">Düzeltme eki orchestration uygulama günlükleri, çalışma zamanı sürümünden Service Fabric günlükleri bir parçası olarak toplanır `5.6.220.9494` ve üstü.</span><span class="sxs-lookup"><span data-stu-id="08c05-289">Patch orchestration app logs are collected as part of Service Fabric logs from runtime version `5.6.220.9494` and above.</span></span>
<span data-ttu-id="08c05-290">Service Fabric çalışma zamanı sürümü çalıştıran kümeler için değerinden `5.6.220.9494`, günlükleri yöntemler aşağıdaki hello birini kullanarak toplanmasını.</span><span class="sxs-lookup"><span data-stu-id="08c05-290">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs can be collected by using one of hello following methods.</span></span>

#### <a name="locally-on-each-node"></a><span data-ttu-id="08c05-291">Her bir düğümde yerel olarak</span><span class="sxs-lookup"><span data-stu-id="08c05-291">Locally on each node</span></span>

<span data-ttu-id="08c05-292">Günlükleri toplanır yerel olarak her Service Fabric küme düğümünde Service Fabric çalışma zamanı sürümü ise değerinden `5.6.220.9494`.</span><span class="sxs-lookup"><span data-stu-id="08c05-292">Logs are collected locally on each Service Fabric cluster node if Service Fabric runtime version is less than `5.6.220.9494`.</span></span> <span data-ttu-id="08c05-293">Merhaba konumu tooaccess hello günlükleri olan \[Service Fabric\_yükleme\_sürücü\]:\\PatchOrchestrationApplication\\günlükleri.</span><span class="sxs-lookup"><span data-stu-id="08c05-293">hello location tooaccess hello logs is \[Service Fabric\_Installation\_Drive\]:\\PatchOrchestrationApplication\\logs.</span></span>

<span data-ttu-id="08c05-294">Service Fabric D sürücüsünde yüklüyse, örneğin, hello D: yoludur\\PatchOrchestrationApplication\\günlükleri.</span><span class="sxs-lookup"><span data-stu-id="08c05-294">For example, if Service Fabric is installed on drive D, hello path is D:\\PatchOrchestrationApplication\\logs.</span></span>

#### <a name="central-location"></a><span data-ttu-id="08c05-295">Merkezi bir konum</span><span class="sxs-lookup"><span data-stu-id="08c05-295">Central location</span></span>

<span data-ttu-id="08c05-296">Azure tanılama önkoşul adımlarını bir parçası olarak yapılandırılmışsa, hello düzeltme eki orchestration uygulama günlüklerini Azure depolama alanında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="08c05-296">If Azure Diagnostics is configured as part of prerequisite steps, logs for hello patch orchestration app are available in Azure Storage.</span></span>

### <a name="health-reports"></a><span data-ttu-id="08c05-297">Sistem durumu raporları</span><span class="sxs-lookup"><span data-stu-id="08c05-297">Health reports</span></span>

<span data-ttu-id="08c05-298">Merhaba düzeltme eki orchestration uygulama sistem durumu raporlarının hello Coordinator hizmetini veya hello düğüm Aracısı hizmeti karşı durumlarda aşağıdaki hello de yayımlar:</span><span class="sxs-lookup"><span data-stu-id="08c05-298">hello patch orchestration app also publishes health reports against hello Coordinator Service or hello Node Agent Service in hello following cases:</span></span>

#### <a name="a-windows-update-operation-failed"></a><span data-ttu-id="08c05-299">Windows Update işlemi başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="08c05-299">A Windows Update operation failed</span></span>

<span data-ttu-id="08c05-300">Bir düğümde Windows güncelleştirme işlemi başarısız olursa, bir sistem durumu raporu düğüm Aracısı hizmeti hello karşı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="08c05-300">If a Windows Update operation fails on a node, a health report is generated against hello Node Agent Service.</span></span> <span data-ttu-id="08c05-301">Merhaba sistem durumu raporu ayrıntılarını hello sorunlu bir düğüm adı içeriyor.</span><span class="sxs-lookup"><span data-stu-id="08c05-301">Details of hello health report contain hello problematic node name.</span></span>

<span data-ttu-id="08c05-302">Düzeltme eki uygulama hello sorunlu düğümde başarıyla tamamlandıktan sonra hello rapor otomatik olarak temizlenir.</span><span class="sxs-lookup"><span data-stu-id="08c05-302">After patching is successfully completed on hello problematic node, hello report is automatically cleared.</span></span>

#### <a name="hello-node-agent-ntservice-is-down"></a><span data-ttu-id="08c05-303">Merhaba düğüm Aracısı NTService çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="08c05-303">hello Node Agent NTService is down</span></span>

<span data-ttu-id="08c05-304">Merhaba düğüm Aracısı NTService bir düğümde çalışmıyorsa, bir uyarı düzeyi sistem durumu raporu düğüm Aracısı hizmeti hello karşı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="08c05-304">If hello Node Agent NTService is down on a node, a warning-level health report is generated against hello Node Agent Service.</span></span>

#### <a name="hello-repair-manager-service-is-not-enabled"></a><span data-ttu-id="08c05-305">Merhaba onarım Yöneticisi hizmeti etkin değil</span><span class="sxs-lookup"><span data-stu-id="08c05-305">hello repair manager service is not enabled</span></span>

<span data-ttu-id="08c05-306">Merhaba onarım Yöneticisi hizmeti hello kümede bulunmazsa, bir uyarı düzeyi sistem durumu raporu Merhaba Coordinator hizmeti oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="08c05-306">If hello repair manager service is not found on hello cluster, a warning-level health report is generated for hello Coordinator Service.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="08c05-307">Sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="08c05-307">Frequently asked questions</span></span>

<span data-ttu-id="08c05-308">Q.</span><span class="sxs-lookup"><span data-stu-id="08c05-308">Q.</span></span> <span data-ttu-id="08c05-309">**Merhaba düzeltme eki orchestration uygulama çalışırken neden bir hata durumuna my küme görüyor?**</span><span class="sxs-lookup"><span data-stu-id="08c05-309">**Why do I see my cluster in an error state when hello patch orchestration app is running?**</span></span>

<span data-ttu-id="08c05-310">A.</span><span class="sxs-lookup"><span data-stu-id="08c05-310">A.</span></span> <span data-ttu-id="08c05-311">Merhaba yükleme işlemi sırasında hello düzeltme eki orchestration uygulama devre dışı bırakır veya geçici olarak giderek hello küme hello durumunu sonuçlanabilir düğümleri yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="08c05-311">During hello installation process, hello patch orchestration app disables or restarts nodes, which can temporarily result in hello health of hello cluster going down.</span></span>

<span data-ttu-id="08c05-312">Hello İlkesi hello uygulama için bağlı olarak, herhangi bir düğümün bir düzeltme eki uygulama işlemi sırasında gidebilirsiniz *veya* tüm yükseltme etki alanı aynı anda Git aşağı.</span><span class="sxs-lookup"><span data-stu-id="08c05-312">Based on hello policy for hello application, either one node can go down during a patching operation *or* an entire upgrade domain can go down simultaneously.</span></span>

<span data-ttu-id="08c05-313">Merhaba Windows Update yükleme Hello sonuna düğümler yeniden iler hale hello yeniden gönderin.</span><span class="sxs-lookup"><span data-stu-id="08c05-313">By hello end of hello Windows Update installation, hello nodes are reenabled post restart.</span></span>

<span data-ttu-id="08c05-314">Aşağıdaki örneğine hello tooan hata durumu geçici olarak iki düğüm aşağı olan ve MaxPercentageUnhealthNodes İlkesi hello çünkü ihlal edildiğini hello küme geçti.</span><span class="sxs-lookup"><span data-stu-id="08c05-314">In hello following example, hello cluster went tooan error state temporarily because two nodes were down and hello MaxPercentageUnhealthNodes policy was violated.</span></span> <span data-ttu-id="08c05-315">devam eden işlemi düzeltme eki uygulama hello olana kadar hello hata geçicidir.</span><span class="sxs-lookup"><span data-stu-id="08c05-315">hello error is temporary until hello patching operation is ongoing.</span></span>

![Sağlıksız küme görüntüsü](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

<span data-ttu-id="08c05-317">Merhaba sorun devam ederse toohello sorun giderme bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="08c05-317">If hello issue persists, refer toohello Troubleshooting section.</span></span>

<span data-ttu-id="08c05-318">Q.</span><span class="sxs-lookup"><span data-stu-id="08c05-318">Q.</span></span> <span data-ttu-id="08c05-319">**Düzeltme eki orchestration uygulama uyarı durumunda**</span><span class="sxs-lookup"><span data-stu-id="08c05-319">**Patch orchestration app is in warning state**</span></span>

<span data-ttu-id="08c05-320">A.</span><span class="sxs-lookup"><span data-stu-id="08c05-320">A.</span></span> <span data-ttu-id="08c05-321">Merhaba uygulamaya karşı gönderilen bir sistem durumu raporu hello kök nedeni toosee kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="08c05-321">Check toosee if a health report posted against hello application is hello root cause.</span></span> <span data-ttu-id="08c05-322">Genellikle, hello uyarı hello sorunun ayrıntılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="08c05-322">Usually, hello warning contains details of hello problem.</span></span> <span data-ttu-id="08c05-323">Merhaba sorun geçici ise, hello beklenen tooauto kurtarma bu durumdan uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="08c05-323">If hello issue is transient, hello application is expected tooauto-recover from this state.</span></span>

<span data-ttu-id="08c05-324">Q.</span><span class="sxs-lookup"><span data-stu-id="08c05-324">Q.</span></span> <span data-ttu-id="08c05-325">**My küme sağlıksız ise ve toodo Acil işletim sistemi güncelleştirmesi gerekir ne yapabilirim?**</span><span class="sxs-lookup"><span data-stu-id="08c05-325">**What can I do if my cluster is unhealthy and I need toodo an urgent operating system update?**</span></span>

<span data-ttu-id="08c05-326">A.</span><span class="sxs-lookup"><span data-stu-id="08c05-326">A.</span></span> <span data-ttu-id="08c05-327">Merhaba küme sağlıksız durumdayken hello düzeltme eki orchestration uygulama güncelleştirmelerini yüklemez.</span><span class="sxs-lookup"><span data-stu-id="08c05-327">hello patch orchestration app does not install updates while hello cluster is unhealthy.</span></span> <span data-ttu-id="08c05-328">Toobring küme tooa sağlıklı duruma toounblock hello düzeltme eki orchestration uygulama iş akışınızı deneyin.</span><span class="sxs-lookup"><span data-stu-id="08c05-328">Try toobring your cluster tooa healthy state toounblock hello patch orchestration app workflow.</span></span>

<span data-ttu-id="08c05-329">Q.</span><span class="sxs-lookup"><span data-stu-id="08c05-329">Q.</span></span> <span data-ttu-id="08c05-330">**Neden kümelerinde düzeltme eki uygulama çok uzun toorun sürer?**</span><span class="sxs-lookup"><span data-stu-id="08c05-330">**Why does patching across clusters take so long toorun?**</span></span>

<span data-ttu-id="08c05-331">A.</span><span class="sxs-lookup"><span data-stu-id="08c05-331">A.</span></span> <span data-ttu-id="08c05-332">Merhaba düzeltme eki orchestration uygulama tarafından gerekli hello zaman çoğunlukla Etkenler aşağıdaki hello üzerinde bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="08c05-332">hello time needed by hello patch orchestration app is mostly dependent on hello following factors:</span></span>

- <span data-ttu-id="08c05-333">Merhaba Coordinator hizmeti Hello ilkesi.</span><span class="sxs-lookup"><span data-stu-id="08c05-333">hello policy of hello Coordinator Service.</span></span> 
  - <span data-ttu-id="08c05-334">Merhaba varsayılan ilke, `NodeWise`, sonuçlarını aynı anda yalnızca tek bir düğüme düzeltme eki uygulama içinde.</span><span class="sxs-lookup"><span data-stu-id="08c05-334">hello default policy, `NodeWise`, results in patching only one node at a time.</span></span> <span data-ttu-id="08c05-335">Merhaba kullanmanızı tavsiye ederiz özellikle hello durumda daha büyük kümeleri `UpgradeDomainWise` İlkesi tooachieve kümeler arasında düzeltme eki uygulama daha hızlı.</span><span class="sxs-lookup"><span data-stu-id="08c05-335">Especially in hello case of bigger clusters, we recommend that you use hello `UpgradeDomainWise` policy tooachieve faster patching across clusters.</span></span>
- <span data-ttu-id="08c05-336">indirme ve yükleme için kullanılabilir güncelleştirmeleri Hello sayısı.</span><span class="sxs-lookup"><span data-stu-id="08c05-336">hello number of updates available for download and installation.</span></span> 
- <span data-ttu-id="08c05-337">gerekli ortalama süre toodownload hello ve birkaç saat aşmamalıdır bir güncelleştirme yükleyin.</span><span class="sxs-lookup"><span data-stu-id="08c05-337">hello average time needed toodownload and install an update, which should not exceed a couple of hours.</span></span>
- <span data-ttu-id="08c05-338">Merhaba performans hello VM ve ağ bant genişliği.</span><span class="sxs-lookup"><span data-stu-id="08c05-338">hello performance of hello VM and network bandwidth.</span></span>

<span data-ttu-id="08c05-339">Q.</span><span class="sxs-lookup"><span data-stu-id="08c05-339">Q.</span></span> <span data-ttu-id="08c05-340">**Bazı güncelleştirmeler Windows Update sonuçlarında REST API'nin aracılığıyla ancak hello makinede Windows Update geçmişi altında elde neden görüyor musunuz?**</span><span class="sxs-lookup"><span data-stu-id="08c05-340">**Why do I see some updates in Windows Update results obtained via REST api's, but not under hello Windows Update history on machine?**</span></span>

<span data-ttu-id="08c05-341">A.</span><span class="sxs-lookup"><span data-stu-id="08c05-341">A.</span></span> <span data-ttu-id="08c05-342">Bazı ürün güncelleştirmelerini ilgili güncelleştirme/düzeltme eki geçmişlerini işaretli toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="08c05-342">Some product updates need toobe checked in their respective update/patch history.</span></span> <span data-ttu-id="08c05-343">Örneğin: Windows Defender'ın güncelleştirmeleri Windows Update geçmişinde Windows Server 2016 görünmüyor.</span><span class="sxs-lookup"><span data-stu-id="08c05-343">Eg: Windows Defender updates do not show up in Windows Update history on Windows Server 2016.</span></span>

## <a name="disclaimers"></a><span data-ttu-id="08c05-344">Bildirimler</span><span class="sxs-lookup"><span data-stu-id="08c05-344">Disclaimers</span></span>

- <span data-ttu-id="08c05-345">Merhaba düzeltme eki orchestration uygulama hello Windows Update, son kullanıcı lisans sözleşmesi hello kullanıcı adına kabul eder.</span><span class="sxs-lookup"><span data-stu-id="08c05-345">hello patch orchestration app accepts hello End-User License Agreement of Windows Update on behalf of hello user.</span></span> <span data-ttu-id="08c05-346">İsteğe bağlı olarak, hello ayarı hello hello uygulama yapılandırmasında kapatılabilir.</span><span class="sxs-lookup"><span data-stu-id="08c05-346">Optionally, hello setting can be turned off in hello configuration of hello application.</span></span>

- <span data-ttu-id="08c05-347">Merhaba düzeltme eki orchestration uygulama telemetri tootrack kullanımını ve performansını toplar.</span><span class="sxs-lookup"><span data-stu-id="08c05-347">hello patch orchestration app collects telemetry tootrack usage and performance.</span></span> <span data-ttu-id="08c05-348">Merhaba uygulamanın telemetri (varsayılan olarak etkindir) hello Service Fabric çalışma zamanı telemetri ayarını hello ayarı izler.</span><span class="sxs-lookup"><span data-stu-id="08c05-348">hello application’s telemetry follows hello setting of hello Service Fabric runtime’s telemetry setting (which is on by default).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="08c05-349">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="08c05-349">Troubleshooting</span></span>

### <a name="a-node-is-not-coming-back-tooup-state"></a><span data-ttu-id="08c05-350">Bir düğüme geri tooup durumu gelmelerini değil</span><span class="sxs-lookup"><span data-stu-id="08c05-350">A node is not coming back tooup state</span></span>

<span data-ttu-id="08c05-351">**Merhaba düğümü takılmış devre dışı bırakma durumunda olduğundan**:</span><span class="sxs-lookup"><span data-stu-id="08c05-351">**hello node might be stuck in a disabling state because**:</span></span>

<span data-ttu-id="08c05-352">Güvenlik onay bekliyor.</span><span class="sxs-lookup"><span data-stu-id="08c05-352">A safety check is pending.</span></span> <span data-ttu-id="08c05-353">tooremedy bu durum iyi durumda yeterli düğüm kullanılabilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="08c05-353">tooremedy this situation, ensure that enough nodes are available in a healthy state.</span></span>

<span data-ttu-id="08c05-354">**Merhaba düğümü takılmış devre dışı durumda olduğundan**:</span><span class="sxs-lookup"><span data-stu-id="08c05-354">**hello node might be stuck in a disabled state because**:</span></span>

- <span data-ttu-id="08c05-355">Merhaba düğümü el ile devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="08c05-355">hello node was disabled manually.</span></span>
- <span data-ttu-id="08c05-356">Merhaba düğümü vade tooan devam eden Azure altyapı işini devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="08c05-356">hello node was disabled due tooan ongoing Azure infrastructure job.</span></span>
- <span data-ttu-id="08c05-357">Merhaba düğümü hello düzeltme eki orchestration uygulama toopatch hello düğümü tarafından geçici olarak devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="08c05-357">hello node was disabled temporarily by hello patch orchestration app toopatch hello node.</span></span>

<span data-ttu-id="08c05-358">**Merhaba düğümü aşağı bir durumda olduğundan takılmış olabilir**:</span><span class="sxs-lookup"><span data-stu-id="08c05-358">**hello node might be stuck in a down state because**:</span></span>

- <span data-ttu-id="08c05-359">Merhaba düğümü aşağı durumda el ile askıya alınmış.</span><span class="sxs-lookup"><span data-stu-id="08c05-359">hello node was put in a down state manually.</span></span>
- <span data-ttu-id="08c05-360">Merhaba düğümü (hangi hello düzeltme eki orchestration uygulama tarafından tetiklenen) yeniden yapılıyor.</span><span class="sxs-lookup"><span data-stu-id="08c05-360">hello node is undergoing a restart (which might be triggered by hello patch orchestration app).</span></span>
- <span data-ttu-id="08c05-361">tooa hatalı VM veya makine ya da ağ bağlantısı sorunları Hello düğümü çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="08c05-361">hello node is down due tooa faulty VM or machine or network connectivity issues.</span></span>

### <a name="updates-were-skipped-on-some-nodes"></a><span data-ttu-id="08c05-362">Güncelleştirmeleri bazı düğümler üzerinde atlandı</span><span class="sxs-lookup"><span data-stu-id="08c05-362">Updates were skipped on some nodes</span></span>

<span data-ttu-id="08c05-363">Merhaba düzeltme eki orchestration uygulama tooinstall Windows update according toohello yeniden zamanlama ilkesi çalışır.</span><span class="sxs-lookup"><span data-stu-id="08c05-363">hello patch orchestration app tries tooinstall a Windows update according toohello rescheduling policy.</span></span> <span data-ttu-id="08c05-364">Merhaba hizmeti toorecover hello düğümü çalışır ve hello güncelleştirme according toohello uygulama ilkesi atlayın.</span><span class="sxs-lookup"><span data-stu-id="08c05-364">hello service tries toorecover hello node and skip hello update according toohello application policy.</span></span>

<span data-ttu-id="08c05-365">Böyle bir durumda, bir uyarı düzeyi sistem durumu raporu düğüm Aracısı hizmeti hello karşı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="08c05-365">In such a case, a warning-level health report is generated against hello Node Agent Service.</span></span> <span data-ttu-id="08c05-366">Windows Update için Hello sonuç hello olası hello başarısızlık nedeni de içerir.</span><span class="sxs-lookup"><span data-stu-id="08c05-366">hello result for Windows Update also contains hello possible reason for hello failure.</span></span>

### <a name="hello-health-of-hello-cluster-goes-tooerror-while-hello-update-installs"></a><span data-ttu-id="08c05-367">Merhaba güncelleştirmeyi yüklerken hello küme hello durumunu tooerror gider.</span><span class="sxs-lookup"><span data-stu-id="08c05-367">hello health of hello cluster goes tooerror while hello update installs</span></span>

<span data-ttu-id="08c05-368">Bir uygulama veya belirli düğüme veya yükseltme etki alanı küme hello durumunu aşağı hatalı bir Windows güncelleştirmesi kullanıma sunabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08c05-368">A faulty Windows update can bring down hello health of an application or cluster on a particular node or upgrade domain.</span></span> <span data-ttu-id="08c05-369">Merhaba küme yeniden sağlıklı duruma gelene kadar hello düzeltme eki orchestration uygulama sonraki tüm Windows Update işlemi sona erdirir.</span><span class="sxs-lookup"><span data-stu-id="08c05-369">hello patch orchestration app discontinues any subsequent Windows Update operation until hello cluster is healthy again.</span></span>

<span data-ttu-id="08c05-370">Bir yönetici müdahale ve Merhaba uygulaması ya da küme neden nedeniyle sağlıksız olduğunu belirlemek tooWindows güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="08c05-370">An administrator must intervene and determine why hello application or cluster became unhealthy due tooWindows Update.</span></span>

## <a name="release-notes-"></a><span data-ttu-id="08c05-371">Sürüm Notları:</span><span class="sxs-lookup"><span data-stu-id="08c05-371">Release Notes :</span></span>

### <a name="version-110"></a><span data-ttu-id="08c05-372">Sürüm 1.1.0</span><span class="sxs-lookup"><span data-stu-id="08c05-372">Version 1.1.0</span></span>
- <span data-ttu-id="08c05-373">Ortak sürüm</span><span class="sxs-lookup"><span data-stu-id="08c05-373">Public release</span></span>

### <a name="version-111"></a><span data-ttu-id="08c05-374">Sürüm 1.1.1</span><span class="sxs-lookup"><span data-stu-id="08c05-374">Version 1.1.1</span></span>
- <span data-ttu-id="08c05-375">Bir hata SetupEntryPoint, NodeAgentNTService yüklemesini engelleyen NodeAgentService içinde sabit.</span><span class="sxs-lookup"><span data-stu-id="08c05-375">Fixed a bug in SetupEntryPoint of NodeAgentService that prevented installation of NodeAgentNTService.</span></span>

### <a name="version-120-latest"></a><span data-ttu-id="08c05-376">Sürüm 1.2.0 (en yeni)</span><span class="sxs-lookup"><span data-stu-id="08c05-376">Version 1.2.0 (Latest)</span></span>

- <span data-ttu-id="08c05-377">Hata düzeltmeleri sistem geçici iş akışını yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="08c05-377">Bug fixes around system restart workflow.</span></span>
- <span data-ttu-id="08c05-378">Onarım görevlerin hazırlanması sırasında toowhich sistem durumu denetimi RM görevlerin oluşturulmasını hata düzeltme beklendiği gibi gerçekleştiği değildi.</span><span class="sxs-lookup"><span data-stu-id="08c05-378">Bug fix in creation of RM tasks due toowhich health check during preparing repair tasks wasn't happening as expected.</span></span>
- <span data-ttu-id="08c05-379">Windows hizmet POANodeSvc otomatik toodelayed-otomatik değiştirilen hello başlangıç modu.</span><span class="sxs-lookup"><span data-stu-id="08c05-379">Changed hello startup mode for windows service POANodeSvc from auto toodelayed-auto.</span></span>
