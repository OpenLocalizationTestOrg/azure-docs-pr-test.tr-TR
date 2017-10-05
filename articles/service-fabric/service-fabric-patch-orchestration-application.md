---
title: "Azure Service Fabric düzeltme orchestration uygulaması | Microsoft Docs"
description: "Service Fabric kümesi üzerinde işletim sistemi düzeltme eki uygulama otomatikleştirmek için uygulama."
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
ms.openlocfilehash: 2c5842822e347113e388d570f6ae603a313944d6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="patch-the-windows-operating-system-in-your-service-fabric-cluster"></a><span data-ttu-id="eee9b-103">Service Fabric kümesi Windows işletim sistemi düzeltme eki</span><span class="sxs-lookup"><span data-stu-id="eee9b-103">Patch the Windows operating system in your Service Fabric cluster</span></span>

<span data-ttu-id="eee9b-104">Düzeltme eki orchestration uygulama kapalı kalma süresi olmadan Azure üzerinde bir Service Fabric kümesindeki düzeltme eki uygulama işletim sistemi otomatikleştiren bir Azure Service Fabric uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="eee9b-104">The patch orchestration application is an Azure Service Fabric application that automates operating system patching on a Service Fabric cluster on Azure without downtime.</span></span>

<span data-ttu-id="eee9b-105">Düzeltme eki orchestration uygulama aşağıdakileri sağlar:</span><span class="sxs-lookup"><span data-stu-id="eee9b-105">The patch orchestration app provides the following:</span></span>

- <span data-ttu-id="eee9b-106">**Otomatik işletim sistemi güncelleştirme yüklemesini**.</span><span class="sxs-lookup"><span data-stu-id="eee9b-106">**Automatic operating system update installation**.</span></span> <span data-ttu-id="eee9b-107">İşletim sistemi güncelleştirmeleri otomatik olarak karşıdan yüklenir ve.</span><span class="sxs-lookup"><span data-stu-id="eee9b-107">Operating system updates are automatically downloaded and installed.</span></span> <span data-ttu-id="eee9b-108">Küme düğümleri küme kapalı kalma süresi olmadan gerektiği gibi yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="eee9b-108">Cluster nodes are rebooted as needed without cluster downtime.</span></span>

- <span data-ttu-id="eee9b-109">**Küme durumunu algılayan düzeltme eki uygulama ve sistem durumu tümleştirme**.</span><span class="sxs-lookup"><span data-stu-id="eee9b-109">**Cluster-aware patching and health integration**.</span></span> <span data-ttu-id="eee9b-110">Güncelleştirmeler uygulanırken düzeltme eki orchestration uygulama küme düğümlerinin sistem durumunu izler.</span><span class="sxs-lookup"><span data-stu-id="eee9b-110">While applying updates, the patch orchestration app monitors the health of the cluster nodes.</span></span> <span data-ttu-id="eee9b-111">Küme düğümü yükseltilmiş bir düğümde aynı anda bir saat ya da bir yükseltme etki alanı olan.</span><span class="sxs-lookup"><span data-stu-id="eee9b-111">Cluster nodes are upgraded one node at a time or one upgrade domain at a time.</span></span> <span data-ttu-id="eee9b-112">Küme durumunu düzeltme eki uygulama işlemi nedeniyle kullanılamaz hale gelirse, düzeltme eki uygulama sorun aggravating önlemek için durduruldu.</span><span class="sxs-lookup"><span data-stu-id="eee9b-112">If the health of the cluster goes down due to the patching process, patching is stopped to prevent aggravating the problem.</span></span>

## <a name="internal-details-of-the-app"></a><span data-ttu-id="eee9b-113">Uygulamanın iç ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="eee9b-113">Internal details of the app</span></span>

<span data-ttu-id="eee9b-114">Düzeltme eki orchestration uygulama aşağıdaki bileşenleri oluşur:</span><span class="sxs-lookup"><span data-stu-id="eee9b-114">The patch orchestration app is composed of the following subcomponents:</span></span>

- <span data-ttu-id="eee9b-115">**Düzenleyicisi hizmeti**: Bu durum bilgisi olan hizmet sorumludur:</span><span class="sxs-lookup"><span data-stu-id="eee9b-115">**Coordinator Service**: This stateful service is responsible for:</span></span>
    - <span data-ttu-id="eee9b-116">Windows güncelleştirme işi tüm küme üzerinde Eşgüdümleme.</span><span class="sxs-lookup"><span data-stu-id="eee9b-116">Coordinating the Windows Update job on the entire cluster.</span></span>
    - <span data-ttu-id="eee9b-117">Tamamlanmış Windows Update işlemlerin sonucunu depolamak.</span><span class="sxs-lookup"><span data-stu-id="eee9b-117">Storing the result of completed Windows Update operations.</span></span>
- <span data-ttu-id="eee9b-118">**Düğüm Aracısı hizmeti**: Bu durum bilgisiz hizmet tüm Service Fabric küme düğümleri üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="eee9b-118">**Node Agent Service**: This stateless service runs on all Service Fabric cluster nodes.</span></span> <span data-ttu-id="eee9b-119">Hizmet için sorumludur:</span><span class="sxs-lookup"><span data-stu-id="eee9b-119">The service is responsible for:</span></span>
    - <span data-ttu-id="eee9b-120">Düğüm Aracısı NTService önyükleme.</span><span class="sxs-lookup"><span data-stu-id="eee9b-120">Bootstrapping the Node Agent NTService.</span></span>
    - <span data-ttu-id="eee9b-121">Düğüm Aracısı NTService izleme.</span><span class="sxs-lookup"><span data-stu-id="eee9b-121">Monitoring the Node Agent NTService.</span></span>
- <span data-ttu-id="eee9b-122">**Düğüm Aracısı NTService**: Bu Windows NT hizmeti, üst düzey bir ayrıcalık (Sistem) çalışır.</span><span class="sxs-lookup"><span data-stu-id="eee9b-122">**Node Agent NTService**: This Windows NT service runs at a higher-level privilege (SYSTEM).</span></span> <span data-ttu-id="eee9b-123">Buna karşılık, düğüm Aracısı hizmeti ve Coordinator hizmeti bir alt düzey önceliği (ağ hizmeti) çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="eee9b-123">In contrast, the Node Agent Service and the Coordinator Service run at a lower-level privilege (NETWORK SERVICE).</span></span> <span data-ttu-id="eee9b-124">Hizmet, tüm küme düğümleri üzerinde aşağıdaki Windows Update işlerini gerçekleştirmek için sorumludur:</span><span class="sxs-lookup"><span data-stu-id="eee9b-124">The service is responsible for performing the following Windows Update jobs on all the cluster nodes:</span></span>
    - <span data-ttu-id="eee9b-125">Düğümde otomatik Windows Update devre dışı bırakılıyor.</span><span class="sxs-lookup"><span data-stu-id="eee9b-125">Disabling automatic Windows Update on the node.</span></span>
    - <span data-ttu-id="eee9b-126">Karşıdan yükleme ve Windows Update ilkesine göre kullanıcı sağlamıştır.</span><span class="sxs-lookup"><span data-stu-id="eee9b-126">Downloading and installing Windows Update according to the policy the user has provided.</span></span>
    - <span data-ttu-id="eee9b-127">Makine post Windows Güncelleştirme yüklemesini yeniden başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="eee9b-127">Restarting the machine post Windows Update installation.</span></span>
    - <span data-ttu-id="eee9b-128">Windows güncelleştirmelerini sonuçlarını Coordinator hizmeti yükleniyor.</span><span class="sxs-lookup"><span data-stu-id="eee9b-128">Uploading the results of Windows updates to the Coordinator Service.</span></span>
    - <span data-ttu-id="eee9b-129">Tüm yeniden denemeler tükenmesinden sonra bir işlem başarısız oldu durumda raporlama durumu raporları.</span><span class="sxs-lookup"><span data-stu-id="eee9b-129">Reporting health reports in case an operation has failed after exhausting all retries.</span></span>

> [!NOTE]
> <span data-ttu-id="eee9b-130">Düzeltme eki orchestration app Service Fabric onarım Yöneticisi sistem hizmeti devre dışı bırakın veya düğüm etkinleştirmek ve sistem durumu denetimleri gerçekleştirmek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="eee9b-130">The patch orchestration app uses the Service Fabric repair manager system service to disable or enable the node and perform health checks.</span></span> <span data-ttu-id="eee9b-131">Düzeltme eki orchestration uygulama tarafından oluşturulan onarım görevi her düğüm için Windows Update ilerleme durumunu izler.</span><span class="sxs-lookup"><span data-stu-id="eee9b-131">The repair task created by the patch orchestration app tracks the Windows Update progress for each node.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eee9b-132">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="eee9b-132">Prerequisites</span></span>

### <a name="minimum-supported-service-fabric-runtime-version"></a><span data-ttu-id="eee9b-133">Service Fabric çalışma zamanı sürümü desteklenen en düşük</span><span class="sxs-lookup"><span data-stu-id="eee9b-133">Minimum supported Service Fabric runtime version</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="eee9b-134">Azure kümeleri</span><span class="sxs-lookup"><span data-stu-id="eee9b-134">Azure clusters</span></span>
<span data-ttu-id="eee9b-135">Düzeltme eki orchestration app Service Fabric çalışma zamanı sürümü v5.5 sahip Azure kümelerinde çalıştırılması gerekir ya da daha sonra.</span><span class="sxs-lookup"><span data-stu-id="eee9b-135">The patch orchestration app must be run on Azure clusters that have Service Fabric runtime version v5.5 or later.</span></span>

#### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="eee9b-136">Tek başına şirket içi kümeleri</span><span class="sxs-lookup"><span data-stu-id="eee9b-136">Standalone on-premises Clusters</span></span>
<span data-ttu-id="eee9b-137">Düzeltme eki orchestration app Service Fabric çalışma zamanı sürümü v5.6 sahip tek başına kümelerinde çalıştırılması gerekir ya da daha sonra.</span><span class="sxs-lookup"><span data-stu-id="eee9b-137">The patch orchestration app must be run on Standalone clusters that have Service Fabric runtime version v5.6 or later.</span></span>

### <a name="enable-the-repair-manager-service-if-its-not-running-already"></a><span data-ttu-id="eee9b-138">(Bu zaten çalışmıyorsa) onarım Yöneticisi hizmetini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="eee9b-138">Enable the repair manager service (if it's not running already)</span></span>

<span data-ttu-id="eee9b-139">Düzeltme eki orchestration uygulama kümede etkinleştirilmesi için onarım Yöneticisi sistem hizmeti gerektirir.</span><span class="sxs-lookup"><span data-stu-id="eee9b-139">The patch orchestration app requires the repair manager system service to be enabled on the cluster.</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="eee9b-140">Azure kümeleri</span><span class="sxs-lookup"><span data-stu-id="eee9b-140">Azure clusters</span></span>

<span data-ttu-id="eee9b-141">Gümüş dayanıklılık katmanı Azure kümelerinde varsayılan olarak etkin onarım Yöneticisi hizmeti sahip.</span><span class="sxs-lookup"><span data-stu-id="eee9b-141">Azure clusters in the silver durability tier have the repair manager service enabled by default.</span></span> <span data-ttu-id="eee9b-142">Altın dayanıklılık katmanı Azure kümelerde olabilir ya da bu kümeleri oluşturulduğu bağlı olarak, etkin onarım Yöneticisi hizmeti sahip olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="eee9b-142">Azure clusters in the gold durability tier might or might not have the repair manager service enabled, depending on when those clusters were created.</span></span> <span data-ttu-id="eee9b-143">Varsayılan olarak, Bronz dayanıklılık katmanı Azure kümelerde etkin onarım Yöneticisi hizmeti yok.</span><span class="sxs-lookup"><span data-stu-id="eee9b-143">Azure clusters in the bronze durability tier, by default, do not have the repair manager service enabled.</span></span> <span data-ttu-id="eee9b-144">Hizmet zaten etkin değilse, Service Fabric Explorer Sistem Hizmetleri bölümünde çalışmasını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eee9b-144">If the service is already enabled, you can see it running in the system services section in the Service Fabric Explorer.</span></span>

##### <a name="azure-portal"></a><span data-ttu-id="eee9b-145">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="eee9b-145">Azure portal</span></span>
<span data-ttu-id="eee9b-146">Kümenin kurma sırasında onarım Yöneticisi Azure portalından etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eee9b-146">You can enable repair manager from Azure portal at the time of setting up of cluster.</span></span> <span data-ttu-id="eee9b-147">Seçin `Include Repair Manager` altında seçeneği `Add on features` küme yapılandırması zaman.</span><span class="sxs-lookup"><span data-stu-id="eee9b-147">Select `Include Repair Manager` option under `Add on features` at the time of Cluster configuration.</span></span>
<span data-ttu-id="eee9b-148">![Azure portalından etkinleştirme onarım Yöneticisi'nin resmi](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span><span class="sxs-lookup"><span data-stu-id="eee9b-148">![Image of Enabling Repair Manager from Azure portal](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span></span>

##### <a name="azure-resource-manager-template"></a><span data-ttu-id="eee9b-149">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="eee9b-149">Azure Resource Manager template</span></span>
<span data-ttu-id="eee9b-150">Alternatif olarak kullanabileceğiniz [Azure Resource Manager şablonu](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) yeni ve mevcut Service Fabric kümeleri üzerinde onarım Yöneticisi hizmeti etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="eee9b-150">Alternatively you can use the [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) to enable the repair manager service on new and existing Service Fabric clusters.</span></span> <span data-ttu-id="eee9b-151">Şablonu dağıtmak istediğiniz kümenin alın.</span><span class="sxs-lookup"><span data-stu-id="eee9b-151">Get the template for the cluster that you want to deploy.</span></span> <span data-ttu-id="eee9b-152">Örnek şablonları kullanabilir veya özel bir Resource Manager şablonu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="eee9b-152">You can either use the sample templates or create a custom Resource Manager template.</span></span> 

<span data-ttu-id="eee9b-153">Onarım Yöneticisi hizmetini kullanarak etkinleştirmek için [Azure Resource Manager şablonu](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span><span class="sxs-lookup"><span data-stu-id="eee9b-153">To enable the repair manager service using [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span></span>

1. <span data-ttu-id="eee9b-154">İlk denetleyin `apiversion` ayarlanır `2017-07-01-preview` için `Microsoft.ServiceFabric/clusters` aşağıdaki kod parçacığında gösterildiği gibi kaynak.</span><span class="sxs-lookup"><span data-stu-id="eee9b-154">First check that the `apiversion` is set to `2017-07-01-preview` for the `Microsoft.ServiceFabric/clusters` resource, as shown in the following snippet.</span></span> <span data-ttu-id="eee9b-155">Farklı sonra güncelleştirmek gereken `apiVersion` değerine `2017-07-01-preview`:</span><span class="sxs-lookup"><span data-stu-id="eee9b-155">If it is different, then you need to update the `apiVersion` to the value `2017-07-01-preview`:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="eee9b-156">Aşağıdakileri ekleyerek onarım Yöneticisi hizmeti şimdi etkinleştirmek `addonFeatures` sonra bölümünde `fabricSettings` bölümü:</span><span class="sxs-lookup"><span data-stu-id="eee9b-156">Now enable the repair manager service by adding the following `addonFeatures` section after the `fabricSettings` section:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="eee9b-157">Bu değişikliklerle küme şablonunuzu güncelleştirildikten sonra bunları uygulamak ve son yükseltme sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eee9b-157">After you have updated your cluster template with these changes, apply them and let the upgrade finish.</span></span> <span data-ttu-id="eee9b-158">Kümenizde çalışan onarım Yöneticisi sistem hizmeti şimdi görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eee9b-158">You can now see the repair manager system service running in your cluster.</span></span> <span data-ttu-id="eee9b-159">Çağrılır `fabric:/System/RepairManagerService` Service Fabric Explorer Sistem Hizmetleri bölümünde.</span><span class="sxs-lookup"><span data-stu-id="eee9b-159">It is called `fabric:/System/RepairManagerService` in the system services section in the Service Fabric Explorer.</span></span> 

### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="eee9b-160">Tek başına şirket içi kümeleri</span><span class="sxs-lookup"><span data-stu-id="eee9b-160">Standalone on-premises clusters</span></span>

<span data-ttu-id="eee9b-161">Kullanabileceğiniz [tek başına Windows kümesi için yapılandırma ayarlarını](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) yeni ve mevcut Service Fabric kümesi üzerinde onarım Yöneticisi hizmeti etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="eee9b-161">You can use the [Configuration settings for standalone Windows cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) to enable the repair manager service on new and existing Service Fabric cluster.</span></span>

<span data-ttu-id="eee9b-162">Onarım Yöneticisi hizmeti etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="eee9b-162">To enable the repair manager service:</span></span>

1. <span data-ttu-id="eee9b-163">İlk denetleyin `apiversion` içinde [genel küme yapılandırmaları](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) ayarlanır `04-2017` veya üstü:</span><span class="sxs-lookup"><span data-stu-id="eee9b-163">First check that the `apiversion` in [General cluster configurations](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) is set to `04-2017` or higher:</span></span>

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. <span data-ttu-id="eee9b-164">Aşağıdakileri ekleyerek onarım Yöneticisi hizmeti şimdi etkinleştirmek `addonFeaturres` sonra bölümünde `fabricSettings` bölümünde aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="eee9b-164">Now enable repair manager service by adding the following `addonFeaturres` section after the `fabricSettings` section as shown below:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="eee9b-165">Küme bildiriminizi güncelleştirilmiş küme bildirimini kullanarak bu değişikliklerle güncelleştirmek [yeni küme oluşturma](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) veya [küme yapılandırmasını yükseltme](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span><span class="sxs-lookup"><span data-stu-id="eee9b-165">Update your cluster manifest with these changes, using the updated cluster manifest [create a new cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) or [upgrade the cluster configuration](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span></span> <span data-ttu-id="eee9b-166">Küme güncelleştirilmiş küme bildirimini ile çalışmaya başladıktan sonra olarak adlandırılır, kümede çalışan onarım Yöneticisi sistem hizmeti şimdi görebilirsiniz `fabric:/System/RepairManagerService`altında sistem hizmetleri Service Fabric explorer bölümünde.</span><span class="sxs-lookup"><span data-stu-id="eee9b-166">Once the cluster is running with updated cluster manifest, you can now see the repair manager system service running in your cluster, which is called `fabric:/System/RepairManagerService`, under system services section in the Service Fabric explorer.</span></span>

### <a name="disable-automatic-windows-update-on-all-nodes"></a><span data-ttu-id="eee9b-167">Tüm düğümlerde otomatik Windows Update devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="eee9b-167">Disable automatic Windows Update on all nodes</span></span>

<span data-ttu-id="eee9b-168">Aynı anda birden çok küme düğümüne yeniden başlatabilirsiniz olduğundan otomatik Windows güncelleştirmelerini kullanılabilirlik kaybına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="eee9b-168">Automatic Windows updates might lead to availability loss because multiple cluster nodes can restart at the same time.</span></span> <span data-ttu-id="eee9b-169">Düzeltme eki orchestration uygulama varsayılan olarak, her küme düğümünde otomatik Windows Update devre dışı bırakmak çalışır.</span><span class="sxs-lookup"><span data-stu-id="eee9b-169">The patch orchestration app, by default, tries to disable the automatic Windows Update on each cluster node.</span></span> <span data-ttu-id="eee9b-170">Ancak, ayarları Grup İlkesi veya bir yönetici tarafından yönetiliyorsa, "Bildirim önce karşıdan" Windows Update ilke açık olarak ayarlanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="eee9b-170">However, if the settings are managed by an administrator or group policy, we recommend setting the Windows Update policy to “Notify before Download” explicitly.</span></span>

### <a name="optional-enable-azure-diagnostics"></a><span data-ttu-id="eee9b-171">İsteğe bağlı: Azure tanılamayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="eee9b-171">Optional: Enable Azure Diagnostics</span></span>

<span data-ttu-id="eee9b-172">Service Fabric çalışma zamanı sürümü çalıştıran kümeler `5.6.220.9494` ve yukarıdaki toplama düzeltme eki orchestration uygulama günlükleri Service Fabric bir parçası olarak günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="eee9b-172">Clusters running Service Fabric runtime version `5.6.220.9494` and above collect patch orchestration app logs as part of Service Fabric logs.</span></span>
<span data-ttu-id="eee9b-173">Kümenizi Service Fabric çalışma zamanı sürümünde çalışıyorsa, bu adımı atlayabilirsiniz `5.6.220.9494` ve üstü.</span><span class="sxs-lookup"><span data-stu-id="eee9b-173">You can skip this step if your cluster is running on Service Fabric runtime version `5.6.220.9494` and above.</span></span>

<span data-ttu-id="eee9b-174">Service Fabric çalışma zamanı sürümü çalıştıran kümeler için değerinden `5.6.220.9494`, düzeltme eki orchestration uygulama günlüklerini toplanan yerel olarak her küme düğümü.</span><span class="sxs-lookup"><span data-stu-id="eee9b-174">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs for the patch orchestration app are collected locally on each of the cluster nodes.</span></span>
<span data-ttu-id="eee9b-175">Merkezi bir konuma tüm düğümlerdeki günlükleri karşıya yüklemek için Azure tanılama yapılandırmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="eee9b-175">We recommend that you configure Azure Diagnostics to upload logs from all nodes to a central location.</span></span>

<span data-ttu-id="eee9b-176">Azure Tanılama'yı etkinleştirme hakkında daha fazla bilgi için bkz: [Azure tanılama kullanarak günlükleri toplamak](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span><span class="sxs-lookup"><span data-stu-id="eee9b-176">For information on enabling Azure Diagnostics, see [Collect logs by using Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span></span>

<span data-ttu-id="eee9b-177">Düzeltme eki orchestration uygulama günlüklerini aşağıdaki sabit sağlayıcısında kimlikleri oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="eee9b-177">Logs for the patch orchestration app are generated on the following fixed provider IDs:</span></span>

- <span data-ttu-id="eee9b-178">e39b723c-590c-4090-abb0-11e3e6616346</span><span class="sxs-lookup"><span data-stu-id="eee9b-178">e39b723c-590c-4090-abb0-11e3e6616346</span></span>
- <span data-ttu-id="eee9b-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span><span class="sxs-lookup"><span data-stu-id="eee9b-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span></span>
- <span data-ttu-id="eee9b-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span><span class="sxs-lookup"><span data-stu-id="eee9b-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span></span>
- <span data-ttu-id="eee9b-181">05dc046c-60e9-4ef7-965e-91660adffa68</span><span class="sxs-lookup"><span data-stu-id="eee9b-181">05dc046c-60e9-4ef7-965e-91660adffa68</span></span>

<span data-ttu-id="eee9b-182">Resource Manager şablonu goto içinde `EtwEventSourceProviderConfiguration` altında bölümünde `WadCfg` ve aşağıdaki girdileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="eee9b-182">In Resource Manager template goto `EtwEventSourceProviderConfiguration` section under `WadCfg` and add the following entries:</span></span>

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
> <span data-ttu-id="eee9b-183">Birden çok düğüm türleri, Service Fabric kümesi var. sonra önceki bölümde tüm eklenmelidir `WadCfg` bölümler.</span><span class="sxs-lookup"><span data-stu-id="eee9b-183">If your Service Fabric cluster has multiple node types, then the previous section must be added for all the `WadCfg` sections.</span></span>

## <a name="download-the-app-package"></a><span data-ttu-id="eee9b-184">Uygulama paketi yükle</span><span class="sxs-lookup"><span data-stu-id="eee9b-184">Download the app package</span></span>

<span data-ttu-id="eee9b-185">Uygulamayı karşıdan [bağlantı karşıdan](https://go.microsoft.com/fwlink/P/?linkid=849590).</span><span class="sxs-lookup"><span data-stu-id="eee9b-185">Download the application from the [download link](https://go.microsoft.com/fwlink/P/?linkid=849590).</span></span>

## <a name="configure-the-app"></a><span data-ttu-id="eee9b-186">Uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="eee9b-186">Configure the app</span></span>

<span data-ttu-id="eee9b-187">Düzeltme eki orchestration uygulamanın davranışı gereksinimlerinizi karşılayacak şekilde yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="eee9b-187">The behavior of the patch orchestration app can be configured to meet your needs.</span></span> <span data-ttu-id="eee9b-188">Uygulama oluşturma veya güncelleştirme işlemi sırasında uygulama parametresini geçirerek varsayılan değerleri geçersiz.</span><span class="sxs-lookup"><span data-stu-id="eee9b-188">Override the default values by passing in the application parameter during application creation or update.</span></span> <span data-ttu-id="eee9b-189">Uygulama parametreleri belirterek sağlanabilir `ApplicationParameter` için `Start-ServiceFabricApplicationUpgrade` veya `New-ServiceFabricApplication` cmdlet'leri.</span><span class="sxs-lookup"><span data-stu-id="eee9b-189">Application parameters can be provided by specifying `ApplicationParameter` to the `Start-ServiceFabricApplicationUpgrade` or `New-ServiceFabricApplication` cmdlets.</span></span>

|<span data-ttu-id="eee9b-190">**Parametre**</span><span class="sxs-lookup"><span data-stu-id="eee9b-190">**Parameter**</span></span>        |<span data-ttu-id="eee9b-191">**Tür**</span><span class="sxs-lookup"><span data-stu-id="eee9b-191">**Type**</span></span>                          | <span data-ttu-id="eee9b-192">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="eee9b-192">**Details**</span></span>|
|:-|-|-|
|<span data-ttu-id="eee9b-193">MaxResultsToCache</span><span class="sxs-lookup"><span data-stu-id="eee9b-193">MaxResultsToCache</span></span>    |<span data-ttu-id="eee9b-194">Uzun</span><span class="sxs-lookup"><span data-stu-id="eee9b-194">Long</span></span>                              | <span data-ttu-id="eee9b-195">Önbelleğe alınması gereken Windows Update sonuçlarının maksimum sayısı.</span><span class="sxs-lookup"><span data-stu-id="eee9b-195">Maximum number of Windows Update results, which should be cached.</span></span> <br><span data-ttu-id="eee9b-196">Varsayılan değer 3000 varsayılır:</span><span class="sxs-lookup"><span data-stu-id="eee9b-196">Default value is 3000 assuming the:</span></span> <br> <span data-ttu-id="eee9b-197">-Düğüm sayısı 20'dir.</span><span class="sxs-lookup"><span data-stu-id="eee9b-197">- Number of nodes is 20.</span></span> <br> <span data-ttu-id="eee9b-198">-Ayda bir düğümde gerçekleştiği güncelleştirme sayısı beştir.</span><span class="sxs-lookup"><span data-stu-id="eee9b-198">- Number of updates happening on a node per month is five.</span></span> <br> <span data-ttu-id="eee9b-199">-İşlemi başına sonuç sayısı 10 olabilir.</span><span class="sxs-lookup"><span data-stu-id="eee9b-199">- Number of results per operation can be 10.</span></span> <br> <span data-ttu-id="eee9b-200">-Son üç ay için sonuçları depolanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eee9b-200">- Results for the past three months should be stored.</span></span> |
|<span data-ttu-id="eee9b-201">TaskApprovalPolicy</span><span class="sxs-lookup"><span data-stu-id="eee9b-201">TaskApprovalPolicy</span></span>   |<span data-ttu-id="eee9b-202">Enum</span><span class="sxs-lookup"><span data-stu-id="eee9b-202">Enum</span></span> <br> <span data-ttu-id="eee9b-203">{NodeWise, UpgradeDomainWise}</span><span class="sxs-lookup"><span data-stu-id="eee9b-203">{ NodeWise, UpgradeDomainWise }</span></span>                          |<span data-ttu-id="eee9b-204">Service Fabric küme düğümleri arasında Windows güncelleştirmelerini yüklemek için Koordinatör hizmeti tarafından kullanılacak ilkeyi TaskApprovalPolicy gösterir.</span><span class="sxs-lookup"><span data-stu-id="eee9b-204">TaskApprovalPolicy indicates the policy that is to be used by the Coordinator Service to install Windows updates across the Service Fabric cluster nodes.</span></span><br>                         <span data-ttu-id="eee9b-205">İzin verilen değerler:</span><span class="sxs-lookup"><span data-stu-id="eee9b-205">Allowed values are:</span></span> <br>                                                           <span data-ttu-id="eee9b-206"><b>NodeWise</b>.</span><span class="sxs-lookup"><span data-stu-id="eee9b-206"><b>NodeWise</b>.</span></span> <span data-ttu-id="eee9b-207">Windows Update yüklü bir aynı anda düğümdür.</span><span class="sxs-lookup"><span data-stu-id="eee9b-207">Windows Update is installed one node at a time.</span></span> <br>                                                           <span data-ttu-id="eee9b-208"><b>UpgradeDomainWise</b>.</span><span class="sxs-lookup"><span data-stu-id="eee9b-208"><b>UpgradeDomainWise</b>.</span></span> <span data-ttu-id="eee9b-209">Windows Update aynı anda yüklü bir yükseltme etki alanıdır.</span><span class="sxs-lookup"><span data-stu-id="eee9b-209">Windows Update is installed one upgrade domain at a time.</span></span> <span data-ttu-id="eee9b-210">(Üst sınırda bir yükseltme etki alanına ait tüm düğümlerde Windows güncelleştirmesi gidebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="eee9b-210">(At the maximum, all the nodes belonging to an upgrade domain can go for Windows Update.)</span></span>
|<span data-ttu-id="eee9b-211">LogsDiskQuotaInMB</span><span class="sxs-lookup"><span data-stu-id="eee9b-211">LogsDiskQuotaInMB</span></span>   |<span data-ttu-id="eee9b-212">Uzun</span><span class="sxs-lookup"><span data-stu-id="eee9b-212">Long</span></span>  <br> <span data-ttu-id="eee9b-213">(Varsayılan: 1024)</span><span class="sxs-lookup"><span data-stu-id="eee9b-213">(Default: 1024)</span></span>               |<span data-ttu-id="eee9b-214">Yerel olarak düğümlerinde kalıcı MB cinsinden en büyük boyutunu düzeltme eki orchestration uygulama kaydeder.</span><span class="sxs-lookup"><span data-stu-id="eee9b-214">Maximum size of patch orchestration app logs in MB, which can be persisted locally on nodes.</span></span>
| <span data-ttu-id="eee9b-215">WUQuery</span><span class="sxs-lookup"><span data-stu-id="eee9b-215">WUQuery</span></span>               | <span data-ttu-id="eee9b-216">Dize</span><span class="sxs-lookup"><span data-stu-id="eee9b-216">string</span></span><br><span data-ttu-id="eee9b-217">(Varsayılan: "IsInstalled = 0")</span><span class="sxs-lookup"><span data-stu-id="eee9b-217">(Default: "IsInstalled=0")</span></span>                | <span data-ttu-id="eee9b-218">Windows güncelleştirmelerini almak için sorgu.</span><span class="sxs-lookup"><span data-stu-id="eee9b-218">Query to get Windows updates.</span></span> <span data-ttu-id="eee9b-219">Daha fazla bilgi için bkz: [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="eee9b-219">For more information, see [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span></span>
| <span data-ttu-id="eee9b-220">InstallWindowsOSOnlyUpdates</span><span class="sxs-lookup"><span data-stu-id="eee9b-220">InstallWindowsOSOnlyUpdates</span></span> | <span data-ttu-id="eee9b-221">bool</span><span class="sxs-lookup"><span data-stu-id="eee9b-221">Bool</span></span> <br> <span data-ttu-id="eee9b-222">(varsayılan: True)</span><span class="sxs-lookup"><span data-stu-id="eee9b-222">(default: True)</span></span>                 | <span data-ttu-id="eee9b-223">Bu bayrak Windows işletim sistemi güncelleştirmelerinin yüklenmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="eee9b-223">This flag allows Windows operating system updates to be installed.</span></span>            |
| <span data-ttu-id="eee9b-224">WUOperationTimeOutInMinutes</span><span class="sxs-lookup"><span data-stu-id="eee9b-224">WUOperationTimeOutInMinutes</span></span> | <span data-ttu-id="eee9b-225">Int</span><span class="sxs-lookup"><span data-stu-id="eee9b-225">Int</span></span> <br><span data-ttu-id="eee9b-226">(Varsayılan: 90).</span><span class="sxs-lookup"><span data-stu-id="eee9b-226">(Default: 90)</span></span>                   | <span data-ttu-id="eee9b-227">(Arama veya indirme veya yükleme) herhangi bir Windows Update işlemi için zaman aşımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="eee9b-227">Specifies the timeout for any Windows Update operation (search or download or install).</span></span> <span data-ttu-id="eee9b-228">İşlemi belirtilen zaman aşımı süresi içinde tamamlanmazsa durdurulur.</span><span class="sxs-lookup"><span data-stu-id="eee9b-228">If the operation is not completed within the specified timeout, it is aborted.</span></span>       |
| <span data-ttu-id="eee9b-229">WURescheduleCount</span><span class="sxs-lookup"><span data-stu-id="eee9b-229">WURescheduleCount</span></span>     | <span data-ttu-id="eee9b-230">Int</span><span class="sxs-lookup"><span data-stu-id="eee9b-230">Int</span></span> <br> <span data-ttu-id="eee9b-231">(Varsayılan: 5).</span><span class="sxs-lookup"><span data-stu-id="eee9b-231">(Default: 5)</span></span>                  | <span data-ttu-id="eee9b-232">Bir işlem kalıcı olarak başarısız olursa en fazla kaç kez Windows hizmet reschedules güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="eee9b-232">The maximum number of times the service reschedules the Windows update in case an operation fails persistently.</span></span>          |
| <span data-ttu-id="eee9b-233">WURescheduleTimeInMinutes</span><span class="sxs-lookup"><span data-stu-id="eee9b-233">WURescheduleTimeInMinutes</span></span> | <span data-ttu-id="eee9b-234">Int</span><span class="sxs-lookup"><span data-stu-id="eee9b-234">Int</span></span> <br><span data-ttu-id="eee9b-235">(Varsayılan: 30).</span><span class="sxs-lookup"><span data-stu-id="eee9b-235">(Default: 30)</span></span> | <span data-ttu-id="eee9b-236">Hata devam ederse durumunda, hizmet Windows update reschedules aralığı.</span><span class="sxs-lookup"><span data-stu-id="eee9b-236">The interval at which the service reschedules the Windows update in case failure persists.</span></span> |
| <span data-ttu-id="eee9b-237">WUFrequency</span><span class="sxs-lookup"><span data-stu-id="eee9b-237">WUFrequency</span></span>           | <span data-ttu-id="eee9b-238">Virgülle ayrılmış dize (varsayılan: "Haftalık, Çarşamba, 7:00:00")</span><span class="sxs-lookup"><span data-stu-id="eee9b-238">Comma-separated string (Default: "Weekly, Wednesday, 7:00:00")</span></span>     | <span data-ttu-id="eee9b-239">Windows Update yükleme sıklığı.</span><span class="sxs-lookup"><span data-stu-id="eee9b-239">The frequency for installing Windows Update.</span></span> <span data-ttu-id="eee9b-240">Biçim ve olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="eee9b-240">The format and possible values are:</span></span> <br><span data-ttu-id="eee9b-241">-Örneğin, aylık, 5, 12 aylık, gg ss: 22:32.</span><span class="sxs-lookup"><span data-stu-id="eee9b-241">-   Monthly, DD,HH:MM:SS, for example, Monthly, 5,12:22:32.</span></span> <br> <span data-ttu-id="eee9b-242">-Örneğin, haftalık, Salı, 12:22:32 için haftalık, gün, ss.</span><span class="sxs-lookup"><span data-stu-id="eee9b-242">-   Weekly, DAY,HH:MM:SS, for example, Weekly, Tuesday, 12:22:32.</span></span>  <br> <span data-ttu-id="eee9b-243">-Örneğin, günlük, 12:22:32 günlük, ss.</span><span class="sxs-lookup"><span data-stu-id="eee9b-243">-   Daily, HH:MM:SS, for example, Daily, 12:22:32.</span></span>  <br> <span data-ttu-id="eee9b-244">-Hiçbiri, Windows Update yapılması döndürmemelidir gösterir.</span><span class="sxs-lookup"><span data-stu-id="eee9b-244">-  None indicates that Windows Update shouldn't be done.</span></span>  <br><br> <span data-ttu-id="eee9b-245">Tüm saatler UTC biçiminde olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="eee9b-245">Note that all the times are in UTC.</span></span>|
| <span data-ttu-id="eee9b-246">AcceptWindowsUpdateEula</span><span class="sxs-lookup"><span data-stu-id="eee9b-246">AcceptWindowsUpdateEula</span></span> | <span data-ttu-id="eee9b-247">bool</span><span class="sxs-lookup"><span data-stu-id="eee9b-247">Bool</span></span> <br><span data-ttu-id="eee9b-248">(Varsayılan: true)</span><span class="sxs-lookup"><span data-stu-id="eee9b-248">(Default: true)</span></span> | <span data-ttu-id="eee9b-249">Bu bayrak ayarlayarak, uygulamanın Windows Update için son kullanıcı lisans sözleşmesi makine sahibi adına kabul eder.</span><span class="sxs-lookup"><span data-stu-id="eee9b-249">By setting this flag, the application accepts the End-User License Agreement for Windows Update on behalf of the owner of the machine.</span></span>              |

> [!TIP]
> <span data-ttu-id="eee9b-250">Windows Update hemen olmasını istiyorsanız, ayarlayın `WUFrequency` uygulama dağıtım süresini göre.</span><span class="sxs-lookup"><span data-stu-id="eee9b-250">If you want Windows Update to happen immediately, set `WUFrequency` relative to the application deployment time.</span></span> <span data-ttu-id="eee9b-251">Örneğin, beş düğümlü test kümesi olduğunu ve yaklaşık 5: 00'da uygulama dağıtmayı planladığınız varsayalım UTC.</span><span class="sxs-lookup"><span data-stu-id="eee9b-251">For example, suppose that you have a five-node test cluster and plan to deploy the app at around 5:00 PM UTC.</span></span> <span data-ttu-id="eee9b-252">Uygulama yükseltme veya dağıtım en 30 dakika sürer olduğunu varsayarsak, WUFrequency "Günlük, 17:30:00." ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="eee9b-252">If you assume that the application upgrade or deployment takes 30 minutes at the maximum, set the WUFrequency as "Daily, 17:30:00."</span></span>

## <a name="deploy-the-app"></a><span data-ttu-id="eee9b-253">Uygulamayı dağıtma</span><span class="sxs-lookup"><span data-stu-id="eee9b-253">Deploy the app</span></span>

1. <span data-ttu-id="eee9b-254">Küme hazırlama tüm önkoşul adımlarını tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="eee9b-254">Finish all the prerequisite steps to prepare the cluster.</span></span>
2. <span data-ttu-id="eee9b-255">Düzeltme eki orchestration uygulamayı başka bir Service Fabric uygulaması gibi dağıtın.</span><span class="sxs-lookup"><span data-stu-id="eee9b-255">Deploy the patch orchestration app like any other Service Fabric app.</span></span> <span data-ttu-id="eee9b-256">PowerShell kullanarak uygulamayı dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eee9b-256">You can deploy the app by using PowerShell.</span></span> <span data-ttu-id="eee9b-257">Adımları [PowerShell kullanarak uygulamaları dağıtma ve Kaldır](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="eee9b-257">Follow the steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>
3. <span data-ttu-id="eee9b-258">Geçişi dağıtım zamanında uygulama yapılandırmak için `ApplicationParamater` için `New-ServiceFabricApplication` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="eee9b-258">To configure the application at the time of deployment, pass the `ApplicationParamater` to the `New-ServiceFabricApplication` cmdlet.</span></span> <span data-ttu-id="eee9b-259">Size kolaylık olması için uygulamanın yanı sıra Deploy.ps1 komut dosyası sağladık.</span><span class="sxs-lookup"><span data-stu-id="eee9b-259">For your convenience, we’ve provided the script Deploy.ps1 along with the application.</span></span> <span data-ttu-id="eee9b-260">Betik kullanmak için:</span><span class="sxs-lookup"><span data-stu-id="eee9b-260">To use the script:</span></span>

    - <span data-ttu-id="eee9b-261">Bir Service Fabric kümeye bağlanırken `Connect-ServiceFabricCluster`.</span><span class="sxs-lookup"><span data-stu-id="eee9b-261">Connect to a Service Fabric cluster by using `Connect-ServiceFabricCluster`.</span></span>
    - <span data-ttu-id="eee9b-262">Uygun olan Deploy.ps1 PowerShell betiğini yürütün `ApplicationParameter` değeri.</span><span class="sxs-lookup"><span data-stu-id="eee9b-262">Execute the PowerShell script Deploy.ps1 with the appropriate `ApplicationParameter` value.</span></span>

> [!NOTE]
> <span data-ttu-id="eee9b-263">Komut dosyası ve uygulama klasörü PatchOrchestrationApplication aynı dizinde tutun.</span><span class="sxs-lookup"><span data-stu-id="eee9b-263">Keep the script and the application folder PatchOrchestrationApplication in the same directory.</span></span>

## <a name="upgrade-the-app"></a><span data-ttu-id="eee9b-264">Uygulama yükseltme</span><span class="sxs-lookup"><span data-stu-id="eee9b-264">Upgrade the app</span></span>

<span data-ttu-id="eee9b-265">PowerShell kullanarak var olan bir düzeltme eki orchestration uygulamaya yükseltmek için adımları [PowerShell kullanarak Service Fabric uygulama yükseltme](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span><span class="sxs-lookup"><span data-stu-id="eee9b-265">To upgrade an existing patch orchestration app by using PowerShell, follow the steps in [Service Fabric application upgrade using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span></span>

## <a name="remove-the-app"></a><span data-ttu-id="eee9b-266">Uygulamayı kaldırma</span><span class="sxs-lookup"><span data-stu-id="eee9b-266">Remove the app</span></span>

<span data-ttu-id="eee9b-267">Uygulamayı kaldırmak için adımları [PowerShell kullanarak uygulamaları dağıtma ve Kaldır](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="eee9b-267">To remove the application, follow the steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>

<span data-ttu-id="eee9b-268">Size kolaylık olması için uygulamanın yanı sıra Undeploy.ps1 komut dosyası sağladık.</span><span class="sxs-lookup"><span data-stu-id="eee9b-268">For your convenience, we've provided the script Undeploy.ps1 along with the application.</span></span> <span data-ttu-id="eee9b-269">Betik kullanmak için:</span><span class="sxs-lookup"><span data-stu-id="eee9b-269">To use the script:</span></span>

  - <span data-ttu-id="eee9b-270">Bir Service Fabric kümeye bağlanırken ```Connect-ServiceFabricCluster```.</span><span class="sxs-lookup"><span data-stu-id="eee9b-270">Connect to a Service Fabric cluster by using ```Connect-ServiceFabricCluster```.</span></span>

  - <span data-ttu-id="eee9b-271">Undeploy.ps1 PowerShell betiğini yürütün.</span><span class="sxs-lookup"><span data-stu-id="eee9b-271">Execute the PowerShell script Undeploy.ps1.</span></span>

> [!NOTE]
> <span data-ttu-id="eee9b-272">Komut dosyası ve uygulama klasörü PatchOrchestrationApplication aynı dizinde tutun.</span><span class="sxs-lookup"><span data-stu-id="eee9b-272">Keep the script and the application folder PatchOrchestrationApplication in the same directory.</span></span>

## <a name="view-the-windows-update-results"></a><span data-ttu-id="eee9b-273">Windows Update sonuçları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="eee9b-273">View the Windows Update results</span></span>

<span data-ttu-id="eee9b-274">Düzeltme eki orchestration uygulama kullanıcıya geçmiş sonuçlarını görüntülemek için REST API'lerini kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="eee9b-274">The patch orchestration app exposes REST APIs to display the historical results to the user.</span></span> <span data-ttu-id="eee9b-275">JSON sonuç örneği:</span><span class="sxs-lookup"><span data-stu-id="eee9b-275">An example of the result JSON:</span></span>
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
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of the issues that are included in this update, see the associated Microsoft Knowledge Base article. After you install this update, you may have to restart your system.",
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
<span data-ttu-id="eee9b-276">Hiçbir güncelleştirme henüz zamanladıysanız JSON sonuç boştur.</span><span class="sxs-lookup"><span data-stu-id="eee9b-276">If no update is scheduled yet, the result JSON is empty.</span></span>

<span data-ttu-id="eee9b-277">Sorgu Windows Update kümeye sonuçları oturum açın.</span><span class="sxs-lookup"><span data-stu-id="eee9b-277">Log in to the cluster to query Windows Update results.</span></span> <span data-ttu-id="eee9b-278">Ardından Coordinator hizmeti birincil çoğaltma adresi bulmak ve tarayıcı URL'den isabet: http://&lt;çoğaltma IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1 / GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="eee9b-278">Then find out the replica address for the primary of the Coordinator Service, and hit the URL from the browser: http://&lt;REPLICA-IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="eee9b-279">REST uç noktası Coordinator hizmeti için dinamik bir bağlantı noktası var.</span><span class="sxs-lookup"><span data-stu-id="eee9b-279">The REST endpoint for the Coordinator Service has a dynamic port.</span></span> <span data-ttu-id="eee9b-280">Tam URL'yi denetlemek için Service Fabric Explorer bakın.</span><span class="sxs-lookup"><span data-stu-id="eee9b-280">To check the exact URL, refer to the Service Fabric Explorer.</span></span> <span data-ttu-id="eee9b-281">Örneğin, sonuçların kullanılabilir `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span><span class="sxs-lookup"><span data-stu-id="eee9b-281">For example, the results are available at `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span></span>

![REST uç noktasını görüntüsü](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


<span data-ttu-id="eee9b-283">Ters proxy kümede etkinleştirilirse, küme de dışındaki URL'yi erişebilir.</span><span class="sxs-lookup"><span data-stu-id="eee9b-283">If the reverse proxy is enabled on the cluster, you can access the URL from outside of the cluster as well.</span></span>
<span data-ttu-id="eee9b-284">Http:// isabet gereken uç noktadır&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="eee9b-284">The endpoint that needs to be hit is http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="eee9b-285">Ters proxy küme üzerinde etkinleştirmek için adımları [ters proxy Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span><span class="sxs-lookup"><span data-stu-id="eee9b-285">To enable the reverse proxy on the cluster, follow the steps in [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span></span> 

> 
> [!WARNING]
> <span data-ttu-id="eee9b-286">Ters proxy yapılandırıldıktan sonra bir HTTP uç noktası kullanıma tüm mikro hizmetler kümedeki küme dışında adreslenebilir.</span><span class="sxs-lookup"><span data-stu-id="eee9b-286">After the reverse proxy is configured, all micro services in the cluster that expose an HTTP endpoint are addressable from outside the cluster.</span></span>

## <a name="diagnosticshealth-events"></a><span data-ttu-id="eee9b-287">Tanılama/sistem durumu olayları</span><span class="sxs-lookup"><span data-stu-id="eee9b-287">Diagnostics/health events</span></span>

### <a name="collect-patch-orchestration-app-logs"></a><span data-ttu-id="eee9b-288">Toplama düzeltme eki orchestration uygulama günlükleri</span><span class="sxs-lookup"><span data-stu-id="eee9b-288">Collect patch orchestration app logs</span></span>

<span data-ttu-id="eee9b-289">Düzeltme eki orchestration uygulama günlükleri, çalışma zamanı sürümünden Service Fabric günlükleri bir parçası olarak toplanır `5.6.220.9494` ve üstü.</span><span class="sxs-lookup"><span data-stu-id="eee9b-289">Patch orchestration app logs are collected as part of Service Fabric logs from runtime version `5.6.220.9494` and above.</span></span>
<span data-ttu-id="eee9b-290">Service Fabric çalışma zamanı sürümü çalıştıran kümeler için değerinden `5.6.220.9494`, günlükleri aşağıdaki yöntemlerden birini kullanarak toplanmasını.</span><span class="sxs-lookup"><span data-stu-id="eee9b-290">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs can be collected by using one of the following methods.</span></span>

#### <a name="locally-on-each-node"></a><span data-ttu-id="eee9b-291">Her bir düğümde yerel olarak</span><span class="sxs-lookup"><span data-stu-id="eee9b-291">Locally on each node</span></span>

<span data-ttu-id="eee9b-292">Günlükleri toplanır yerel olarak her Service Fabric küme düğümünde Service Fabric çalışma zamanı sürümü ise değerinden `5.6.220.9494`.</span><span class="sxs-lookup"><span data-stu-id="eee9b-292">Logs are collected locally on each Service Fabric cluster node if Service Fabric runtime version is less than `5.6.220.9494`.</span></span> <span data-ttu-id="eee9b-293">Günlükleri erişmek için konum \[Service Fabric\_yükleme\_sürücü\]:\\PatchOrchestrationApplication\\günlükleri.</span><span class="sxs-lookup"><span data-stu-id="eee9b-293">The location to access the logs is \[Service Fabric\_Installation\_Drive\]:\\PatchOrchestrationApplication\\logs.</span></span>

<span data-ttu-id="eee9b-294">Service Fabric D sürücüsünde yüklüyse, örneğin, D: yoludur\\PatchOrchestrationApplication\\günlükleri.</span><span class="sxs-lookup"><span data-stu-id="eee9b-294">For example, if Service Fabric is installed on drive D, the path is D:\\PatchOrchestrationApplication\\logs.</span></span>

#### <a name="central-location"></a><span data-ttu-id="eee9b-295">Merkezi bir konum</span><span class="sxs-lookup"><span data-stu-id="eee9b-295">Central location</span></span>

<span data-ttu-id="eee9b-296">Azure tanılama önkoşul adımlarını bir parçası olarak yapılandırılmışsa, düzeltme eki orchestration uygulama günlüklerini Azure depolama alanında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="eee9b-296">If Azure Diagnostics is configured as part of prerequisite steps, logs for the patch orchestration app are available in Azure Storage.</span></span>

### <a name="health-reports"></a><span data-ttu-id="eee9b-297">Sistem durumu raporları</span><span class="sxs-lookup"><span data-stu-id="eee9b-297">Health reports</span></span>

<span data-ttu-id="eee9b-298">Düzeltme eki orchestration uygulama sistem durumu raporlarının Düzenleyicisi hizmeti veya düğüm Aracısı hizmeti karşı aşağıdaki durumlarda da yayımlar:</span><span class="sxs-lookup"><span data-stu-id="eee9b-298">The patch orchestration app also publishes health reports against the Coordinator Service or the Node Agent Service in the following cases:</span></span>

#### <a name="a-windows-update-operation-failed"></a><span data-ttu-id="eee9b-299">Windows Update işlemi başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="eee9b-299">A Windows Update operation failed</span></span>

<span data-ttu-id="eee9b-300">Bir düğümde Windows güncelleştirme işlemi başarısız olursa, bir sistem durumu raporu karşı düğüm Aracısı hizmeti oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="eee9b-300">If a Windows Update operation fails on a node, a health report is generated against the Node Agent Service.</span></span> <span data-ttu-id="eee9b-301">Sistem Durumu raporu ayrıntılarını sorunlu bir düğüm adı içeriyor.</span><span class="sxs-lookup"><span data-stu-id="eee9b-301">Details of the health report contain the problematic node name.</span></span>

<span data-ttu-id="eee9b-302">Düzeltme eki uygulama sorunlu bir düğüm üzerinde başarıyla tamamlandıktan sonra raporu otomatik olarak temizlenir.</span><span class="sxs-lookup"><span data-stu-id="eee9b-302">After patching is successfully completed on the problematic node, the report is automatically cleared.</span></span>

#### <a name="the-node-agent-ntservice-is-down"></a><span data-ttu-id="eee9b-303">Düğüm Aracısı NTService çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="eee9b-303">The Node Agent NTService is down</span></span>

<span data-ttu-id="eee9b-304">Düğüm Aracısı NTService bir düğümde çalışmıyorsa, bir uyarı düzeyi sistem durumu raporu karşı düğüm Aracısı hizmeti oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="eee9b-304">If the Node Agent NTService is down on a node, a warning-level health report is generated against the Node Agent Service.</span></span>

#### <a name="the-repair-manager-service-is-not-enabled"></a><span data-ttu-id="eee9b-305">Onarım Yöneticisi hizmeti etkin değil</span><span class="sxs-lookup"><span data-stu-id="eee9b-305">The repair manager service is not enabled</span></span>

<span data-ttu-id="eee9b-306">Onarım Yöneticisi hizmeti kümede bulunmazsa, bir uyarı düzeyi sistem durumu raporu Düzenleyicisi hizmeti için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="eee9b-306">If the repair manager service is not found on the cluster, a warning-level health report is generated for the Coordinator Service.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="eee9b-307">Sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="eee9b-307">Frequently asked questions</span></span>

<span data-ttu-id="eee9b-308">Q.</span><span class="sxs-lookup"><span data-stu-id="eee9b-308">Q.</span></span> <span data-ttu-id="eee9b-309">**Düzeltme eki orchestration uygulama çalışırken neden bir hata durumuna my küme görüyor?**</span><span class="sxs-lookup"><span data-stu-id="eee9b-309">**Why do I see my cluster in an error state when the patch orchestration app is running?**</span></span>

<span data-ttu-id="eee9b-310">A.</span><span class="sxs-lookup"><span data-stu-id="eee9b-310">A.</span></span> <span data-ttu-id="eee9b-311">Yükleme işlemi sırasında düzeltme eki orchestration uygulama devre dışı bırakır veya geçici olarak giderek küme durumunu sonuçlanabilir düğümleri yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="eee9b-311">During the installation process, the patch orchestration app disables or restarts nodes, which can temporarily result in the health of the cluster going down.</span></span>

<span data-ttu-id="eee9b-312">İlke uygulama için bağlı olarak, herhangi bir düğümün bir düzeltme eki uygulama işlemi sırasında gidebilirsiniz *veya* tüm yükseltme etki alanı aynı anda Git aşağı.</span><span class="sxs-lookup"><span data-stu-id="eee9b-312">Based on the policy for the application, either one node can go down during a patching operation *or* an entire upgrade domain can go down simultaneously.</span></span>

<span data-ttu-id="eee9b-313">Windows Update yükleme sonuna düğümlerin yeniden iler hale getirilir yeniden başlatma gönderin.</span><span class="sxs-lookup"><span data-stu-id="eee9b-313">By the end of the Windows Update installation, the nodes are reenabled post restart.</span></span>

<span data-ttu-id="eee9b-314">Bir hata durumu kümeyi aşağıdaki örnekte, geçici olarak oluştu çünkü iki düğüm olan aşağı ve MaxPercentageUnhealthNodes ilke ihlal.</span><span class="sxs-lookup"><span data-stu-id="eee9b-314">In the following example, the cluster went to an error state temporarily because two nodes were down and the MaxPercentageUnhealthNodes policy was violated.</span></span> <span data-ttu-id="eee9b-315">Düzeltme eki uygulama işlemi devam eden olana kadar geçici bir hatadır.</span><span class="sxs-lookup"><span data-stu-id="eee9b-315">The error is temporary until the patching operation is ongoing.</span></span>

![Sağlıksız küme görüntüsü](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

<span data-ttu-id="eee9b-317">Sorun devam ederse, sorun giderme bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="eee9b-317">If the issue persists, refer to the Troubleshooting section.</span></span>

<span data-ttu-id="eee9b-318">Q.</span><span class="sxs-lookup"><span data-stu-id="eee9b-318">Q.</span></span> <span data-ttu-id="eee9b-319">**Düzeltme eki orchestration uygulama uyarı durumunda**</span><span class="sxs-lookup"><span data-stu-id="eee9b-319">**Patch orchestration app is in warning state**</span></span>

<span data-ttu-id="eee9b-320">A.</span><span class="sxs-lookup"><span data-stu-id="eee9b-320">A.</span></span> <span data-ttu-id="eee9b-321">Uygulamaya karşı gönderilen bir sistem durumu raporu kök neden olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="eee9b-321">Check to see if a health report posted against the application is the root cause.</span></span> <span data-ttu-id="eee9b-322">Genellikle, uyarı sorunun ayrıntılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="eee9b-322">Usually, the warning contains details of the problem.</span></span> <span data-ttu-id="eee9b-323">Sorun geçici ise, uygulama otomatik kurtarma bu durumdan olması beklenir.</span><span class="sxs-lookup"><span data-stu-id="eee9b-323">If the issue is transient, the application is expected to auto-recover from this state.</span></span>

<span data-ttu-id="eee9b-324">Q.</span><span class="sxs-lookup"><span data-stu-id="eee9b-324">Q.</span></span> <span data-ttu-id="eee9b-325">**My küme sağlıksız ise ve Acil işletim sistemi güncelleştirmesi yapmanız ne yapabilirim?**</span><span class="sxs-lookup"><span data-stu-id="eee9b-325">**What can I do if my cluster is unhealthy and I need to do an urgent operating system update?**</span></span>

<span data-ttu-id="eee9b-326">A.</span><span class="sxs-lookup"><span data-stu-id="eee9b-326">A.</span></span> <span data-ttu-id="eee9b-327">Küme sağlıksız durumdayken düzeltme eki orchestration uygulama güncelleştirmelerini yüklemez.</span><span class="sxs-lookup"><span data-stu-id="eee9b-327">The patch orchestration app does not install updates while the cluster is unhealthy.</span></span> <span data-ttu-id="eee9b-328">Kümenizi düzeltme eki orchestration uygulama iş akışı engellemesini kaldırmak için sağlıklı bir duruma getirmek deneyin.</span><span class="sxs-lookup"><span data-stu-id="eee9b-328">Try to bring your cluster to a healthy state to unblock the patch orchestration app workflow.</span></span>

<span data-ttu-id="eee9b-329">Q.</span><span class="sxs-lookup"><span data-stu-id="eee9b-329">Q.</span></span> <span data-ttu-id="eee9b-330">**Neden kümelerinde düzeltme eki uygulama kadar çalıştırmak için sürer?**</span><span class="sxs-lookup"><span data-stu-id="eee9b-330">**Why does patching across clusters take so long to run?**</span></span>

<span data-ttu-id="eee9b-331">A.</span><span class="sxs-lookup"><span data-stu-id="eee9b-331">A.</span></span> <span data-ttu-id="eee9b-332">Düzeltme eki orchestration uygulama tarafından gereken süre genellikle aşağıdaki etkenlere bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="eee9b-332">The time needed by the patch orchestration app is mostly dependent on the following factors:</span></span>

- <span data-ttu-id="eee9b-333">Düzenleyici hizmet ilkesi.</span><span class="sxs-lookup"><span data-stu-id="eee9b-333">The policy of the Coordinator Service.</span></span> 
  - <span data-ttu-id="eee9b-334">Varsayılan ilke `NodeWise`, sonuçlarını aynı anda yalnızca tek bir düğüme düzeltme eki uygulama içinde.</span><span class="sxs-lookup"><span data-stu-id="eee9b-334">The default policy, `NodeWise`, results in patching only one node at a time.</span></span> <span data-ttu-id="eee9b-335">Özellikle büyük kümeleri söz konusu olduğunda, kullanmanızı öneririz `UpgradeDomainWise` kümeler arasında daha hızlı düzeltme eki uygulama elde etmek için ilke.</span><span class="sxs-lookup"><span data-stu-id="eee9b-335">Especially in the case of bigger clusters, we recommend that you use the `UpgradeDomainWise` policy to achieve faster patching across clusters.</span></span>
- <span data-ttu-id="eee9b-336">İndirme ve yükleme için kullanılabilir güncelleştirmeleri sayısı.</span><span class="sxs-lookup"><span data-stu-id="eee9b-336">The number of updates available for download and installation.</span></span> 
- <span data-ttu-id="eee9b-337">Karşıdan yüklemek ve bir güncelleştirmeyi yüklemek için gereken ortalama süre, birkaç saat aşamaz.</span><span class="sxs-lookup"><span data-stu-id="eee9b-337">The average time needed to download and install an update, which should not exceed a couple of hours.</span></span>
- <span data-ttu-id="eee9b-338">VM ve ağ bant genişliği performans.</span><span class="sxs-lookup"><span data-stu-id="eee9b-338">The performance of the VM and network bandwidth.</span></span>

<span data-ttu-id="eee9b-339">Q.</span><span class="sxs-lookup"><span data-stu-id="eee9b-339">Q.</span></span> <span data-ttu-id="eee9b-340">**Bazı güncelleştirmeler Windows Update sonuçlarında REST API'nin aracılığıyla ancak makinede Windows Update geçmişi altında elde neden görüyor musunuz?**</span><span class="sxs-lookup"><span data-stu-id="eee9b-340">**Why do I see some updates in Windows Update results obtained via REST api's, but not under the Windows Update history on machine?**</span></span>

<span data-ttu-id="eee9b-341">A.</span><span class="sxs-lookup"><span data-stu-id="eee9b-341">A.</span></span> <span data-ttu-id="eee9b-342">Bazı ürün güncelleştirmelerini ilgili güncelleştirme/düzeltme eki geçmişlerini denetlenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="eee9b-342">Some product updates need to be checked in their respective update/patch history.</span></span> <span data-ttu-id="eee9b-343">Örneğin: Windows Defender'ın güncelleştirmeleri Windows Update geçmişinde Windows Server 2016 görünmüyor.</span><span class="sxs-lookup"><span data-stu-id="eee9b-343">Eg: Windows Defender updates do not show up in Windows Update history on Windows Server 2016.</span></span>

## <a name="disclaimers"></a><span data-ttu-id="eee9b-344">Bildirimler</span><span class="sxs-lookup"><span data-stu-id="eee9b-344">Disclaimers</span></span>

- <span data-ttu-id="eee9b-345">Düzeltme eki orchestration uygulama Windows Update, son kullanıcı lisans sözleşmesi kullanıcı adına kabul eder.</span><span class="sxs-lookup"><span data-stu-id="eee9b-345">The patch orchestration app accepts the End-User License Agreement of Windows Update on behalf of the user.</span></span> <span data-ttu-id="eee9b-346">İsteğe bağlı olarak, ayar uygulama yapılandırmasında kapatılabilir.</span><span class="sxs-lookup"><span data-stu-id="eee9b-346">Optionally, the setting can be turned off in the configuration of the application.</span></span>

- <span data-ttu-id="eee9b-347">Düzeltme eki orchestration uygulama kullanımını ve performansını izlemek için telemetri toplar.</span><span class="sxs-lookup"><span data-stu-id="eee9b-347">The patch orchestration app collects telemetry to track usage and performance.</span></span> <span data-ttu-id="eee9b-348">Uygulamanın telemetri (varsayılan olarak etkindir) Service Fabric çalışma zamanı telemetri ayarını ayarı izler.</span><span class="sxs-lookup"><span data-stu-id="eee9b-348">The application’s telemetry follows the setting of the Service Fabric runtime’s telemetry setting (which is on by default).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="eee9b-349">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="eee9b-349">Troubleshooting</span></span>

### <a name="a-node-is-not-coming-back-to-up-state"></a><span data-ttu-id="eee9b-350">Bir düğüm geri durumu yukarı geliyor değil</span><span class="sxs-lookup"><span data-stu-id="eee9b-350">A node is not coming back to up state</span></span>

<span data-ttu-id="eee9b-351">**Düğümü devre dışı bırakma durumunda olduğundan takılmış olabilir**:</span><span class="sxs-lookup"><span data-stu-id="eee9b-351">**The node might be stuck in a disabling state because**:</span></span>

<span data-ttu-id="eee9b-352">Güvenlik onay bekliyor.</span><span class="sxs-lookup"><span data-stu-id="eee9b-352">A safety check is pending.</span></span> <span data-ttu-id="eee9b-353">Bu durumu düzeltmek için sağlam bir durumda yeterli düğüm kullanılabilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="eee9b-353">To remedy this situation, ensure that enough nodes are available in a healthy state.</span></span>

<span data-ttu-id="eee9b-354">**Düğümü devre dışı durumda olduğundan takılmış olabilir**:</span><span class="sxs-lookup"><span data-stu-id="eee9b-354">**The node might be stuck in a disabled state because**:</span></span>

- <span data-ttu-id="eee9b-355">Düğüm el ile devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="eee9b-355">The node was disabled manually.</span></span>
- <span data-ttu-id="eee9b-356">Düğüm, devam eden Azure altyapı iş nedeniyle devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="eee9b-356">The node was disabled due to an ongoing Azure infrastructure job.</span></span>
- <span data-ttu-id="eee9b-357">Düğüm düğüm düzeltme eki için düzeltme eki orchestration uygulama tarafından geçici olarak devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="eee9b-357">The node was disabled temporarily by the patch orchestration app to patch the node.</span></span>

<span data-ttu-id="eee9b-358">**Düğüm aşağı bir durumda olduğundan takılmış olabilir**:</span><span class="sxs-lookup"><span data-stu-id="eee9b-358">**The node might be stuck in a down state because**:</span></span>

- <span data-ttu-id="eee9b-359">Düğüm aşağı durumda el ile askıya alınmış.</span><span class="sxs-lookup"><span data-stu-id="eee9b-359">The node was put in a down state manually.</span></span>
- <span data-ttu-id="eee9b-360">Düğüm (hangi düzeltme eki orchestration uygulama tarafından tetiklenen) yeniden yapılıyor.</span><span class="sxs-lookup"><span data-stu-id="eee9b-360">The node is undergoing a restart (which might be triggered by the patch orchestration app).</span></span>
- <span data-ttu-id="eee9b-361">Düğümü hatalı VM veya makine ya da ağ bağlantısı sorunları nedeniyle çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="eee9b-361">The node is down due to a faulty VM or machine or network connectivity issues.</span></span>

### <a name="updates-were-skipped-on-some-nodes"></a><span data-ttu-id="eee9b-362">Güncelleştirmeleri bazı düğümler üzerinde atlandı</span><span class="sxs-lookup"><span data-stu-id="eee9b-362">Updates were skipped on some nodes</span></span>

<span data-ttu-id="eee9b-363">Düzeltme eki orchestration uygulama bir Windows güncelleştirmesi yeniden zamanlama ilkesine göre yüklemeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="eee9b-363">The patch orchestration app tries to install a Windows update according to the rescheduling policy.</span></span> <span data-ttu-id="eee9b-364">Düğüm kurtarmak ve uygulama ilkesi göre güncelleştirme atlamak hizmeti çalışır.</span><span class="sxs-lookup"><span data-stu-id="eee9b-364">The service tries to recover the node and skip the update according to the application policy.</span></span>

<span data-ttu-id="eee9b-365">Böyle bir durumda, bir uyarı düzeyi sistem durumu raporu karşı düğüm Aracısı hizmeti oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="eee9b-365">In such a case, a warning-level health report is generated against the Node Agent Service.</span></span> <span data-ttu-id="eee9b-366">Windows Update için sonucu hatanın olası nedenini de içerir.</span><span class="sxs-lookup"><span data-stu-id="eee9b-366">The result for Windows Update also contains the possible reason for the failure.</span></span>

### <a name="the-health-of-the-cluster-goes-to-error-while-the-update-installs"></a><span data-ttu-id="eee9b-367">Güncelleştirmeyi yüklerken küme durumunu hata durumuna geçer</span><span class="sxs-lookup"><span data-stu-id="eee9b-367">The health of the cluster goes to error while the update installs</span></span>

<span data-ttu-id="eee9b-368">Bir uygulama veya belirli düğüme veya yükseltme etki alanı küme durumunu aşağı hatalı bir Windows güncelleştirmesi kullanıma sunabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eee9b-368">A faulty Windows update can bring down the health of an application or cluster on a particular node or upgrade domain.</span></span> <span data-ttu-id="eee9b-369">Düzeltme eki orchestration uygulama kümeye yeniden sağlıklı duruma gelene kadar sonraki tüm Windows Update işlemi sona erdirir.</span><span class="sxs-lookup"><span data-stu-id="eee9b-369">The patch orchestration app discontinues any subsequent Windows Update operation until the cluster is healthy again.</span></span>

<span data-ttu-id="eee9b-370">Bir yönetici, müdahale ve uygulama ya da küme neden nedeniyle Windows Update sağlıksız olduğunu belirler.</span><span class="sxs-lookup"><span data-stu-id="eee9b-370">An administrator must intervene and determine why the application or cluster became unhealthy due to Windows Update.</span></span>

## <a name="release-notes-"></a><span data-ttu-id="eee9b-371">Sürüm Notları:</span><span class="sxs-lookup"><span data-stu-id="eee9b-371">Release Notes :</span></span>

### <a name="version-110"></a><span data-ttu-id="eee9b-372">Sürüm 1.1.0</span><span class="sxs-lookup"><span data-stu-id="eee9b-372">Version 1.1.0</span></span>
- <span data-ttu-id="eee9b-373">Ortak sürüm</span><span class="sxs-lookup"><span data-stu-id="eee9b-373">Public release</span></span>

### <a name="version-111"></a><span data-ttu-id="eee9b-374">Sürüm 1.1.1</span><span class="sxs-lookup"><span data-stu-id="eee9b-374">Version 1.1.1</span></span>
- <span data-ttu-id="eee9b-375">Bir hata SetupEntryPoint, NodeAgentNTService yüklemesini engelleyen NodeAgentService içinde sabit.</span><span class="sxs-lookup"><span data-stu-id="eee9b-375">Fixed a bug in SetupEntryPoint of NodeAgentService that prevented installation of NodeAgentNTService.</span></span>

### <a name="version-120-latest"></a><span data-ttu-id="eee9b-376">Sürüm 1.2.0 (en yeni)</span><span class="sxs-lookup"><span data-stu-id="eee9b-376">Version 1.2.0 (Latest)</span></span>

- <span data-ttu-id="eee9b-377">Hata düzeltmeleri sistem geçici iş akışını yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="eee9b-377">Bug fixes around system restart workflow.</span></span>
- <span data-ttu-id="eee9b-378">Hangi sistem durumu nedeniyle, beklendiği gibi onarım görevlerin hazırlanması sırasında onay gerçekleştiği değildi RM görevler oluşturma hata düzeltmesi.</span><span class="sxs-lookup"><span data-stu-id="eee9b-378">Bug fix in creation of RM tasks due to which health check during preparing repair tasks wasn't happening as expected.</span></span>
- <span data-ttu-id="eee9b-379">Windows POANodeSvc otomatik otomatik Gecikmeli hizmetinin başlangıç modu değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="eee9b-379">Changed the startup mode for windows service POANodeSvc from auto to delayed-auto.</span></span>
