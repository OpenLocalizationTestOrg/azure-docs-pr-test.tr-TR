---
title: "Service Fabric kümesi güvenlik: istemci rolleri | Microsoft Docs"
description: "Bu makalede hello iki istemci rolleri ve toohello rolleri sağlanan hello izinleri açıklar."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: coreysa
editor: 
ms.assetid: 7bc808d9-3609-46a1-ac12-b4f53bff98dd
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 4a4a9f93e91ea816005b730bebbcb317f8bab255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-for-service-fabric-clients"></a><span data-ttu-id="cae13-103">Service Fabric istemciler için rol tabanlı erişim denetimi</span><span class="sxs-lookup"><span data-stu-id="cae13-103">Role-based access control for Service Fabric clients</span></span>
<span data-ttu-id="cae13-104">Azure Service Fabric bağlı tooa Service Fabric kümesi istemciler için iki farklı erişim denetim türlerini destekler: Yönetici ve kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="cae13-104">Azure Service Fabric supports two different access control types for clients that are connected tooa Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="cae13-105">Erişim denetimi hello Küme Yöneticisi toolimit erişim toocertain küme işlemleri farklı hello küme daha güvenli hale getirme kullanıcı grupları için sağlar.</span><span class="sxs-lookup"><span data-stu-id="cae13-105">Access control allows hello cluster administrator toolimit access toocertain cluster operations for different groups of users, making hello cluster more secure.</span></span>  

<span data-ttu-id="cae13-106">**Yöneticiler** (okuma/yazma özellikleri dahil) tam erişim toomanagement özelliklere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="cae13-106">**Administrators** have full access toomanagement capabilities (including read/write capabilities).</span></span> <span data-ttu-id="cae13-107">Varsayılan olarak, **kullanıcılar** yalnızca okuma erişimi toomanagement özellikleri (örneğin, sorgu özellikleri) ve hello özelliği tooresolve uygulamaları ve Hizmetleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="cae13-107">By default, **users** only have read access toomanagement capabilities (for example, query capabilities), and hello ability tooresolve applications and services.</span></span>

<span data-ttu-id="cae13-108">Her biri için ayrı sertifikaların sağlayarak hello küme oluşturma sırasında hello iki istemci rolleri (Yönetici ve istemci) belirtin.</span><span class="sxs-lookup"><span data-stu-id="cae13-108">You specify hello two client roles (administrator and client) at hello time of cluster creation by providing separate certificates for each.</span></span> <span data-ttu-id="cae13-109">Bkz: [Service Fabric kümesi güvenlik](service-fabric-cluster-security.md) güvenli bir Service Fabric kümesi ayarlama hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="cae13-109">See [Service Fabric cluster security](service-fabric-cluster-security.md) for details on setting up a secure Service Fabric cluster.</span></span>

## <a name="default-access-control-settings"></a><span data-ttu-id="cae13-110">Varsayılan erişim denetimi ayarları</span><span class="sxs-lookup"><span data-stu-id="cae13-110">Default access control settings</span></span>
<span data-ttu-id="cae13-111">Hello Yöneticisi erişim denetimi türünü tam erişim tooall hello FabricClient API'leri sahiptir.</span><span class="sxs-lookup"><span data-stu-id="cae13-111">hello administrator access control type has full access tooall hello FabricClient APIs.</span></span> <span data-ttu-id="cae13-112">Merhaba işlemler aşağıdaki gibi hello Service Fabric kümesi tüm okuma ve yazma işlemleri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cae13-112">It can perform any reads and writes on hello Service Fabric cluster, including hello following operations:</span></span>

### <a name="application-and-service-operations"></a><span data-ttu-id="cae13-113">Uygulama ve hizmet işlemleri</span><span class="sxs-lookup"><span data-stu-id="cae13-113">Application and service operations</span></span>
* <span data-ttu-id="cae13-114">**CreateService**: hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="cae13-114">**CreateService**: service creation</span></span>                             
* <span data-ttu-id="cae13-115">**CreateServiceFromTemplate**: hizmet şablonundan oluşturma</span><span class="sxs-lookup"><span data-stu-id="cae13-115">**CreateServiceFromTemplate**: service creation from template</span></span>                             
* <span data-ttu-id="cae13-116">**UpdateService**: hizmet güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="cae13-116">**UpdateService**: service updates</span></span>                             
* <span data-ttu-id="cae13-117">**DeleteService**: Hizmet silme</span><span class="sxs-lookup"><span data-stu-id="cae13-117">**DeleteService**: service deletion</span></span>                             
* <span data-ttu-id="cae13-118">**ProvisionApplicationType**: uygulama sağlama türünü</span><span class="sxs-lookup"><span data-stu-id="cae13-118">**ProvisionApplicationType**: application type provisioning</span></span>                             
* <span data-ttu-id="cae13-119">**CreateApplication**: uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="cae13-119">**CreateApplication**: application creation</span></span>                               
* <span data-ttu-id="cae13-120">**DeleteApplication**: uygulama silme</span><span class="sxs-lookup"><span data-stu-id="cae13-120">**DeleteApplication**: application deletion</span></span>                             
* <span data-ttu-id="cae13-121">**UpgradeApplication**: başlatılması veya uygulama yükseltmelerini kesintiye</span><span class="sxs-lookup"><span data-stu-id="cae13-121">**UpgradeApplication**: starting or interrupting application upgrades</span></span>                             
* <span data-ttu-id="cae13-122">**UnprovisionApplicationType**: uygulama türü sağlamanın kaldırılması</span><span class="sxs-lookup"><span data-stu-id="cae13-122">**UnprovisionApplicationType**: application type unprovisioning</span></span>                             
* <span data-ttu-id="cae13-123">**MoveNextUpgradeDomain**: uygulama yükseltmelerini açıkça güncelleştirme etki alanı ile sürdürülüyor</span><span class="sxs-lookup"><span data-stu-id="cae13-123">**MoveNextUpgradeDomain**: resuming application upgrades with an explicit update domain</span></span>                             
* <span data-ttu-id="cae13-124">**ReportUpgradeHealth**: uygulama yükseltmelerini hello geçerli yükseltme ilerleme durumu ile sürdürülüyor</span><span class="sxs-lookup"><span data-stu-id="cae13-124">**ReportUpgradeHealth**: resuming application upgrades with hello current upgrade progress</span></span>                             
* <span data-ttu-id="cae13-125">**ReportHealth**: sistem durumu raporlama</span><span class="sxs-lookup"><span data-stu-id="cae13-125">**ReportHealth**: reporting health</span></span>                             
* <span data-ttu-id="cae13-126">**PredeployPackageToNode**: dağıtım öncesi API</span><span class="sxs-lookup"><span data-stu-id="cae13-126">**PredeployPackageToNode**: predeployment API</span></span>                            
* <span data-ttu-id="cae13-127">**CodePackageControl**: kod paketler yeniden başlatılıyor</span><span class="sxs-lookup"><span data-stu-id="cae13-127">**CodePackageControl**: restarting code packages</span></span>                             
* <span data-ttu-id="cae13-128">**RecoverPartition**: bir bölüm kurtarma</span><span class="sxs-lookup"><span data-stu-id="cae13-128">**RecoverPartition**: recovering a partition</span></span>                             
* <span data-ttu-id="cae13-129">**RecoverPartitions**: bölümleri kurtarma</span><span class="sxs-lookup"><span data-stu-id="cae13-129">**RecoverPartitions**: recovering partitions</span></span>                             
* <span data-ttu-id="cae13-130">**RecoverServicePartitions**: hizmet bölümlerini kurtarma</span><span class="sxs-lookup"><span data-stu-id="cae13-130">**RecoverServicePartitions**: recovering service partitions</span></span>                             
* <span data-ttu-id="cae13-131">**RecoverSystemPartitions**: sistem hizmeti bölümleri kurtarma</span><span class="sxs-lookup"><span data-stu-id="cae13-131">**RecoverSystemPartitions**: recovering system service partitions</span></span>                             

### <a name="cluster-operations"></a><span data-ttu-id="cae13-132">Küme işlemleri</span><span class="sxs-lookup"><span data-stu-id="cae13-132">Cluster operations</span></span>
* <span data-ttu-id="cae13-133">**ProvisionFabric**: MSI ve/veya küme bildirim sağlama</span><span class="sxs-lookup"><span data-stu-id="cae13-133">**ProvisionFabric**: MSI and/or cluster manifest provisioning</span></span>                             
* <span data-ttu-id="cae13-134">**UpgradeFabric**: Küme yükseltme başlatılıyor</span><span class="sxs-lookup"><span data-stu-id="cae13-134">**UpgradeFabric**: starting cluster upgrades</span></span>                             
* <span data-ttu-id="cae13-135">**UnprovisionFabric**: MSI ve/veya küme bildirimi sağlamanın kaldırılması</span><span class="sxs-lookup"><span data-stu-id="cae13-135">**UnprovisionFabric**: MSI and/or cluster manifest unprovisioning</span></span>                         
* <span data-ttu-id="cae13-136">**MoveNextFabricUpgradeDomain**: Küme yükseltme açıkça güncelleştirme etki alanı ile sürdürülüyor</span><span class="sxs-lookup"><span data-stu-id="cae13-136">**MoveNextFabricUpgradeDomain**: resuming cluster upgrades with an explicit update domain</span></span>                             
* <span data-ttu-id="cae13-137">**ReportFabricUpgradeHealth**: Küme yükseltme hello geçerli yükseltme ilerleme durumu ile sürdürülüyor</span><span class="sxs-lookup"><span data-stu-id="cae13-137">**ReportFabricUpgradeHealth**: resuming cluster upgrades with hello current upgrade progress</span></span>                             
* <span data-ttu-id="cae13-138">**StartInfrastructureTask**: altyapı görevleri başlatma</span><span class="sxs-lookup"><span data-stu-id="cae13-138">**StartInfrastructureTask**: starting infrastructure tasks</span></span>                             
* <span data-ttu-id="cae13-139">**FinishInfrastructureTask**: altyapı görevleri tamamlama</span><span class="sxs-lookup"><span data-stu-id="cae13-139">**FinishInfrastructureTask**: finishing infrastructure tasks</span></span>                             
* <span data-ttu-id="cae13-140">**InvokeInfrastructureCommand**: altyapı görev yönetimi komutları</span><span class="sxs-lookup"><span data-stu-id="cae13-140">**InvokeInfrastructureCommand**: infrastructure task management commands</span></span>                              
* <span data-ttu-id="cae13-141">**ActivateNode**: bir düğümü etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="cae13-141">**ActivateNode**: activating a node</span></span>                             
* <span data-ttu-id="cae13-142">**DeactivateNode**: bir düğümü devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="cae13-142">**DeactivateNode**: deactivating a node</span></span>                             
* <span data-ttu-id="cae13-143">**DeactivateNodesBatch**: birden çok düğüm devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="cae13-143">**DeactivateNodesBatch**: deactivating multiple nodes</span></span>                             
* <span data-ttu-id="cae13-144">**RemoveNodeDeactivations**: birden çok düğümde geri alma devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="cae13-144">**RemoveNodeDeactivations**: reverting deactivation on multiple nodes</span></span>                             
* <span data-ttu-id="cae13-145">**GetNodeDeactivationStatus**: devre dışı bırakma durumu denetleniyor</span><span class="sxs-lookup"><span data-stu-id="cae13-145">**GetNodeDeactivationStatus**: checking deactivation status</span></span>                             
* <span data-ttu-id="cae13-146">**NodeStateRemoved**: düğüm durumu raporlama kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="cae13-146">**NodeStateRemoved**: reporting node state removed</span></span>                             
* <span data-ttu-id="cae13-147">**ReportFault**: hata raporlama</span><span class="sxs-lookup"><span data-stu-id="cae13-147">**ReportFault**: reporting fault</span></span>                             
* <span data-ttu-id="cae13-148">**FileContent**: Image store istemcisi dosya aktarımı (Dış toocluster)</span><span class="sxs-lookup"><span data-stu-id="cae13-148">**FileContent**: image store client file transfer (external toocluster)</span></span>                             
* <span data-ttu-id="cae13-149">**FileDownload**: Image store istemcisi dosya indirme başlatma (Dış toocluster)</span><span class="sxs-lookup"><span data-stu-id="cae13-149">**FileDownload**: image store client file download initiation (external toocluster)</span></span>                             
* <span data-ttu-id="cae13-150">**InternalList**: görüntü deposu istemci dosya listesi işlemi (iç)</span><span class="sxs-lookup"><span data-stu-id="cae13-150">**InternalList**: image store client file list operation (internal)</span></span>                             
* <span data-ttu-id="cae13-151">**Silme**: görüntü deposu istemci silme işlemi</span><span class="sxs-lookup"><span data-stu-id="cae13-151">**Delete**: image store client delete operation</span></span>                              
* <span data-ttu-id="cae13-152">**Karşıya yükleme**: Image store istemcisi karşıya yükleme işlemi</span><span class="sxs-lookup"><span data-stu-id="cae13-152">**Upload**: image store client upload operation</span></span>                             
* <span data-ttu-id="cae13-153">**NodeControl**: başlatma, durdurma ve düğüm yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="cae13-153">**NodeControl**: starting, stopping, and restarting nodes</span></span>                             
* <span data-ttu-id="cae13-154">**MoveReplicaControl**: bir düğümü tooanother çoğaltmaları taşıma</span><span class="sxs-lookup"><span data-stu-id="cae13-154">**MoveReplicaControl**: moving replicas from one node tooanother</span></span>                             

### <a name="miscellaneous-operations"></a><span data-ttu-id="cae13-155">Çeşitli işlemler</span><span class="sxs-lookup"><span data-stu-id="cae13-155">Miscellaneous operations</span></span>
* <span data-ttu-id="cae13-156">**Ping**: istemci ping isteği</span><span class="sxs-lookup"><span data-stu-id="cae13-156">**Ping**: client pings</span></span>                             
* <span data-ttu-id="cae13-157">**Sorgu**: izin verilen tüm sorgular</span><span class="sxs-lookup"><span data-stu-id="cae13-157">**Query**: all queries allowed</span></span>
* <span data-ttu-id="cae13-158">**NameExists**: URI varlığı denetimleri adlandırma</span><span class="sxs-lookup"><span data-stu-id="cae13-158">**NameExists**: naming URI existence checks</span></span>                             

<span data-ttu-id="cae13-159">Merhaba kullanıcı erişim denetimi türü varsayılan olarak, aşağıdaki işlemleri sınırlı toohello verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="cae13-159">hello user access control type is, by default, limited toohello following operations:</span></span> 

* <span data-ttu-id="cae13-160">**EnumerateSubnames**: URI numaralandırması adlandırma</span><span class="sxs-lookup"><span data-stu-id="cae13-160">**EnumerateSubnames**: naming URI enumeration</span></span>                             
* <span data-ttu-id="cae13-161">**EnumerateProperties**: özellik numaralandırma adlandırma</span><span class="sxs-lookup"><span data-stu-id="cae13-161">**EnumerateProperties**: naming property enumeration</span></span>                             
* <span data-ttu-id="cae13-162">**PropertyReadBatch**: özellik adlandırma okuma işlemleri</span><span class="sxs-lookup"><span data-stu-id="cae13-162">**PropertyReadBatch**: naming property read operations</span></span>                             
* <span data-ttu-id="cae13-163">**GetServiceDescription**: uzun yoklama hizmet bildirimleri ve okuma hizmeti açıklamaları</span><span class="sxs-lookup"><span data-stu-id="cae13-163">**GetServiceDescription**: long-poll service notifications and reading service descriptions</span></span>                             
* <span data-ttu-id="cae13-164">**ResolveService**: hizmet uyumlu tabanlı çözümleme</span><span class="sxs-lookup"><span data-stu-id="cae13-164">**ResolveService**: complaint-based service resolution</span></span>                             
* <span data-ttu-id="cae13-165">**ResolveNameOwner**: çözümleme adlandırma URI'si sahibi</span><span class="sxs-lookup"><span data-stu-id="cae13-165">**ResolveNameOwner**: resolving naming URI owner</span></span>                             
* <span data-ttu-id="cae13-166">**ResolvePartition**: Sistem Hizmetleri çözme</span><span class="sxs-lookup"><span data-stu-id="cae13-166">**ResolvePartition**: resolving system services</span></span>                             
* <span data-ttu-id="cae13-167">**ServiceNotifications**: olay tabanlı hizmet bildirimleri</span><span class="sxs-lookup"><span data-stu-id="cae13-167">**ServiceNotifications**: event-based service notifications</span></span>                             
* <span data-ttu-id="cae13-168">**GetUpgradeStatus**: Uygulama yükseltme durumunu yoklama</span><span class="sxs-lookup"><span data-stu-id="cae13-168">**GetUpgradeStatus**: polling application upgrade status</span></span>                             
* <span data-ttu-id="cae13-169">**GetFabricUpgradeStatus**: Küme yükseltme durumunu yoklama</span><span class="sxs-lookup"><span data-stu-id="cae13-169">**GetFabricUpgradeStatus**: polling cluster upgrade status</span></span>                             
* <span data-ttu-id="cae13-170">**InvokeInfrastructureQuery**: altyapısı görevlerini sorgulama</span><span class="sxs-lookup"><span data-stu-id="cae13-170">**InvokeInfrastructureQuery**: querying infrastructure tasks</span></span>                             
* <span data-ttu-id="cae13-171">**Liste**: görüntü deposu istemci dosya listesi işlemi</span><span class="sxs-lookup"><span data-stu-id="cae13-171">**List**: image store client file list operation</span></span>                             
* <span data-ttu-id="cae13-172">**ResetPartitionLoad**: bir yük devretme biriminin yükünü sıfırlama</span><span class="sxs-lookup"><span data-stu-id="cae13-172">**ResetPartitionLoad**: resetting load for a failover unit</span></span>                             
* <span data-ttu-id="cae13-173">**ToggleVerboseServicePlacementHealthReporting**: ayrıntılı hizmet sistem durumu yerleştirme raporlama geçiş</span><span class="sxs-lookup"><span data-stu-id="cae13-173">**ToggleVerboseServicePlacementHealthReporting**: toggling verbose service placement health reporting</span></span>                             

<span data-ttu-id="cae13-174">Merhaba yönetici erişim denetimi işlemleri önceki erişim toohello de vardır.</span><span class="sxs-lookup"><span data-stu-id="cae13-174">hello admin access control also has access toohello preceding operations.</span></span>

## <a name="changing-default-settings-for-client-roles"></a><span data-ttu-id="cae13-175">İstemci rolleri için varsayılan ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="cae13-175">Changing default settings for client roles</span></span>
<span data-ttu-id="cae13-176">Merhaba küme bildirim dosyasında, gerekirse, yönetim yetenekleri toohello istemci sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cae13-176">In hello cluster manifest file, you can provide admin capabilities toohello client if needed.</span></span> <span data-ttu-id="cae13-177">Giden toohello tarafından hello Varsayılanları değiştirebilirsiniz **yapı ayarları** sırasında seçeneği [küme oluşturma](service-fabric-cluster-creation-via-portal.md), hello ayarları önceki hello sağlayarak ve **adı**, **yönetici**, **kullanıcı**, ve **değeri** alanları.</span><span class="sxs-lookup"><span data-stu-id="cae13-177">You can change hello defaults by going toohello **Fabric Settings** option during [cluster creation](service-fabric-cluster-creation-via-portal.md), and providing hello preceding settings in hello **name**, **admin**, **user**, and **value** fields.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cae13-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cae13-178">Next steps</span></span>
[<span data-ttu-id="cae13-179">Service Fabric kümesi güvenliği</span><span class="sxs-lookup"><span data-stu-id="cae13-179">Service Fabric cluster security</span></span>](service-fabric-cluster-security.md)

[<span data-ttu-id="cae13-180">Service Fabric kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="cae13-180">Service Fabric cluster creation</span></span>](service-fabric-cluster-creation-via-portal.md)

