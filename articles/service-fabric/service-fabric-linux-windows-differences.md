---
title: "aaaAzure Service Fabric, Linux ve Windows farkları | Microsoft Docs"
description: "Hello Azure Service Fabric Önizleme Linux ve Windows Azure Service Fabric arasındaki farklar."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 7a16a440dfc8d9006e274f46951be1562e6f10d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="differences-between-service-fabric-on-linux-preview-and-windows-generally-available"></a><span data-ttu-id="19fc3-103">Linux (önizleme) ve Windows (genel kullanıma açık) üzerindeki Service Fabric arasındaki farklar</span><span class="sxs-lookup"><span data-stu-id="19fc3-103">Differences between Service Fabric on Linux (preview) and Windows (generally available)</span></span>

<span data-ttu-id="19fc3-104">Linux üzerinde Service Fabric önizleme aşamasında olduğundan, Windows’ta desteklenip Linux’ta henüz desteklenmeyen bazı özellikler mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="19fc3-104">Since Service Fabric on Linux is a preview, there are some features that are supported on Windows, but not yet on Linux.</span></span> <span data-ttu-id="19fc3-105">Sonuç olarak, Service Fabric Linux üzerinde genel kullanıma sunulduğunda hello özellik kümeleri eşlik olacaktır.</span><span class="sxs-lookup"><span data-stu-id="19fc3-105">Eventually, hello feature sets will be at parity when Service Fabric on Linux becomes generally available.</span></span> <span data-ttu-id="19fc3-106">Gelecek sürümlerle birlikte bu özellik farkı azalacaktır.</span><span class="sxs-lookup"><span data-stu-id="19fc3-106">With upcoming releases, this feature gap will shrink.</span></span> <span data-ttu-id="19fc3-107">Merhaba aşağıdaki hello en son kullanılabilir sürümleri farklar (diğer bir deyişle, sürüm 5.6 Windows ve Linux 5.5 sürümünde arasında):</span><span class="sxs-lookup"><span data-stu-id="19fc3-107">hello following differences exist between hello latest available releases (that is, between version 5.6 on Windows and version 5.5 on Linux):</span></span> 

* <span data-ttu-id="19fc3-108">Güvenilir Koleksiyonlar (ve Güvenilir Durum Bilgisi Olan Hizmetler)</span><span class="sxs-lookup"><span data-stu-id="19fc3-108">Reliable Collections (and Reliable Stateful Services)</span></span> 
* <span data-ttu-id="19fc3-109">Ters ara sunucu</span><span class="sxs-lookup"><span data-stu-id="19fc3-109">ReverseProxy</span></span> 
* <span data-ttu-id="19fc3-110">Tek başına yükleyici</span><span class="sxs-lookup"><span data-stu-id="19fc3-110">Standalone installer</span></span> 
* <span data-ttu-id="19fc3-111">Bildirim dosyaları için XML şema doğrulaması</span><span class="sxs-lookup"><span data-stu-id="19fc3-111">XML schema validation for manifest files</span></span> 
* <span data-ttu-id="19fc3-112">Konsol yeniden yönlendirmesi</span><span class="sxs-lookup"><span data-stu-id="19fc3-112">Console redirection</span></span> 
* <span data-ttu-id="19fc3-113">Merhaba hataya Analiz Hizmeti (SK'lar)</span><span class="sxs-lookup"><span data-stu-id="19fc3-113">hello Fault Analysis Service (FAS)</span></span>
* <span data-ttu-id="19fc3-114">Kapsayıcılar için Docker Compose, birim ve günlük sürücüleri</span><span class="sxs-lookup"><span data-stu-id="19fc3-114">Docker compose and volume and logging drivers for containers</span></span> 
* <span data-ttu-id="19fc3-115">Kapsayıcılar ve hizmetler için kaynak idaresi</span><span class="sxs-lookup"><span data-stu-id="19fc3-115">Resource governance for containers and services</span></span> 
* <span data-ttu-id="19fc3-116">DNS hizmeti</span><span class="sxs-lookup"><span data-stu-id="19fc3-116">DNS service</span></span>
* <span data-ttu-id="19fc3-117">Azure Active Directory desteği</span><span class="sxs-lookup"><span data-stu-id="19fc3-117">Azure Active Directory support</span></span>
* <span data-ttu-id="19fc3-118">Belirli PowerShell komutlarının CLI komutu eşdeğerleri</span><span class="sxs-lookup"><span data-stu-id="19fc3-118">CLI command equivalents of certain Powershell commands</span></span> 
* <span data-ttu-id="19fc3-119">Powershell komutları yalnızca bir kısmı (Merhaba sonraki bölümde genişletilmiş gibi) bir Linux kümesi karşı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19fc3-119">Only a subset of Powershell commands can be run against a Linux cluster (as expanded in hello next section).</span></span>

>[!NOTE]
><span data-ttu-id="19fc3-120">Konsol yönlendirmesi, Windows’ta bile üretim kümelerinde desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="19fc3-120">Console redirection is not supported in production clusters, even on Windows.</span></span>

<span data-ttu-id="19fc3-121">Geliştirme araçları da Windows ile Linux arasında farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="19fc3-121">Development tooling is also different between Windows and Linux.</span></span> <span data-ttu-id="19fc3-122">VisualStudio, Powershell, VSTS ve ETW özellikleri Windows üzerinde kullanılabilirken, Linux üzerinde Yeoman, Eclipse, Jenkins ve LTTng kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="19fc3-122">VisualStudio, Powershell, VSTS, and ETW are used on Windows while Yeoman, Eclipse, Jenkins, and LTTng are used on Linux.</span></span>

## <a name="powershell-cmdlets-that-do-not-work-against-a-linux-service-fabric-cluster"></a><span data-ttu-id="19fc3-123">Linux Service Fabric kümesinde çalışmayan PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="19fc3-123">Powershell cmdlets that do not work against a Linux Service Fabric cluster</span></span>

* <span data-ttu-id="19fc3-124">Invoke-ServiceFabricChaosTestScenario</span><span class="sxs-lookup"><span data-stu-id="19fc3-124">Invoke-ServiceFabricChaosTestScenario</span></span>
* <span data-ttu-id="19fc3-125">Invoke-ServiceFabricFailoverTestScenario</span><span class="sxs-lookup"><span data-stu-id="19fc3-125">Invoke-ServiceFabricFailoverTestScenario</span></span>
* <span data-ttu-id="19fc3-126">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="19fc3-126">Invoke-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="19fc3-127">Invoke-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="19fc3-127">Invoke-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="19fc3-128">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="19fc3-128">Restart-ServiceFabricPartition</span></span>
* <span data-ttu-id="19fc3-129">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="19fc3-129">Start-ServiceFabricNode</span></span>
* <span data-ttu-id="19fc3-130">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="19fc3-130">Stop-ServiceFabricNode</span></span>
* <span data-ttu-id="19fc3-131">Get-ServiceFabricImageStoreContent</span><span class="sxs-lookup"><span data-stu-id="19fc3-131">Get-ServiceFabricImageStoreContent</span></span>
* <span data-ttu-id="19fc3-132">Get-ServiceFabricChaosReport</span><span class="sxs-lookup"><span data-stu-id="19fc3-132">Get-ServiceFabricChaosReport</span></span>
* <span data-ttu-id="19fc3-133">Get-ServiceFabricNodeTransitionProgress</span><span class="sxs-lookup"><span data-stu-id="19fc3-133">Get-ServiceFabricNodeTransitionProgress</span></span>
* <span data-ttu-id="19fc3-134">Get-ServiceFabricPartitionDataLossProgress</span><span class="sxs-lookup"><span data-stu-id="19fc3-134">Get-ServiceFabricPartitionDataLossProgress</span></span>
* <span data-ttu-id="19fc3-135">Get-ServiceFabricPartitionQuorumLossProgress</span><span class="sxs-lookup"><span data-stu-id="19fc3-135">Get-ServiceFabricPartitionQuorumLossProgress</span></span>
* <span data-ttu-id="19fc3-136">Get-ServiceFabricPartitionRestartProgress</span><span class="sxs-lookup"><span data-stu-id="19fc3-136">Get-ServiceFabricPartitionRestartProgress</span></span>
* <span data-ttu-id="19fc3-137">Get-ServiceFabricTestCommandStatusList</span><span class="sxs-lookup"><span data-stu-id="19fc3-137">Get-ServiceFabricTestCommandStatusList</span></span>
* <span data-ttu-id="19fc3-138">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="19fc3-138">Remove-ServiceFabricTestState</span></span>
* <span data-ttu-id="19fc3-139">Start-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="19fc3-139">Start-ServiceFabricChaos</span></span>
* <span data-ttu-id="19fc3-140">Start-ServiceFabricNodeTransition</span><span class="sxs-lookup"><span data-stu-id="19fc3-140">Start-ServiceFabricNodeTransition</span></span>
* <span data-ttu-id="19fc3-141">Start-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="19fc3-141">Start-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="19fc3-142">Start-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="19fc3-142">Start-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="19fc3-143">Start-ServiceFabricPartitionRestart</span><span class="sxs-lookup"><span data-stu-id="19fc3-143">Start-ServiceFabricPartitionRestart</span></span>
* <span data-ttu-id="19fc3-144">Stop-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="19fc3-144">Stop-ServiceFabricChaos</span></span>
* <span data-ttu-id="19fc3-145">Stop-ServiceFabricTestCommand</span><span class="sxs-lookup"><span data-stu-id="19fc3-145">Stop-ServiceFabricTestCommand</span></span>
* <span data-ttu-id="19fc3-146">Cmd</span><span class="sxs-lookup"><span data-stu-id="19fc3-146">Cmd</span></span>
* <span data-ttu-id="19fc3-147">Get-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="19fc3-147">Get-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="19fc3-148">Get-ServiceFabricClusterConfiguration</span><span class="sxs-lookup"><span data-stu-id="19fc3-148">Get-ServiceFabricClusterConfiguration</span></span>
* <span data-ttu-id="19fc3-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span><span class="sxs-lookup"><span data-stu-id="19fc3-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span></span>
* <span data-ttu-id="19fc3-150">Get-ServiceFabricPackageDebugParameters</span><span class="sxs-lookup"><span data-stu-id="19fc3-150">Get-ServiceFabricPackageDebugParameters</span></span>
* <span data-ttu-id="19fc3-151">New-ServiceFabricPackageDebugParameter</span><span class="sxs-lookup"><span data-stu-id="19fc3-151">New-ServiceFabricPackageDebugParameter</span></span>
* <span data-ttu-id="19fc3-152">New-ServiceFabricPackageSharingPolicy</span><span class="sxs-lookup"><span data-stu-id="19fc3-152">New-ServiceFabricPackageSharingPolicy</span></span>
* <span data-ttu-id="19fc3-153">Add-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="19fc3-153">Add-ServiceFabricNode</span></span>
* <span data-ttu-id="19fc3-154">Copy-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="19fc3-154">Copy-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="19fc3-155">Get-ServiceFabricRuntimeSupportedVersion</span><span class="sxs-lookup"><span data-stu-id="19fc3-155">Get-ServiceFabricRuntimeSupportedVersion</span></span>
* <span data-ttu-id="19fc3-156">Get-ServiceFabricRuntimeUpgradeVersion</span><span class="sxs-lookup"><span data-stu-id="19fc3-156">Get-ServiceFabricRuntimeUpgradeVersion</span></span>
* <span data-ttu-id="19fc3-157">New-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="19fc3-157">New-ServiceFabricCluster</span></span>
* <span data-ttu-id="19fc3-158">New-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="19fc3-158">New-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="19fc3-159">Remove-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="19fc3-159">Remove-ServiceFabricCluster</span></span>
* <span data-ttu-id="19fc3-160">Remove-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="19fc3-160">Remove-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="19fc3-161">Remove-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="19fc3-161">Remove-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="19fc3-162">Test-ServiceFabricClusterManifest</span><span class="sxs-lookup"><span data-stu-id="19fc3-162">Test-ServiceFabricClusterManifest</span></span>
* <span data-ttu-id="19fc3-163">Test-ServiceFabricConfiguration</span><span class="sxs-lookup"><span data-stu-id="19fc3-163">Test-ServiceFabricConfiguration</span></span>
* <span data-ttu-id="19fc3-164">Update-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="19fc3-164">Update-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="19fc3-165">Approve-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="19fc3-165">Approve-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="19fc3-166">Complete-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="19fc3-166">Complete-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="19fc3-167">Get-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="19fc3-167">Get-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="19fc3-168">Invoke-ServiceFabricDecryptText</span><span class="sxs-lookup"><span data-stu-id="19fc3-168">Invoke-ServiceFabricDecryptText</span></span>
* <span data-ttu-id="19fc3-169">Invoke-ServiceFabricEncryptSecret</span><span class="sxs-lookup"><span data-stu-id="19fc3-169">Invoke-ServiceFabricEncryptSecret</span></span>
* <span data-ttu-id="19fc3-170">Invoke-ServiceFabricEncryptText</span><span class="sxs-lookup"><span data-stu-id="19fc3-170">Invoke-ServiceFabricEncryptText</span></span>
* <span data-ttu-id="19fc3-171">Invoke-ServiceFabricInfrastructureCommand</span><span class="sxs-lookup"><span data-stu-id="19fc3-171">Invoke-ServiceFabricInfrastructureCommand</span></span>
* <span data-ttu-id="19fc3-172">Invoke-ServiceFabricInfrastructureQuery</span><span class="sxs-lookup"><span data-stu-id="19fc3-172">Invoke-ServiceFabricInfrastructureQuery</span></span>
* <span data-ttu-id="19fc3-173">Remove-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="19fc3-173">Remove-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="19fc3-174">Start-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="19fc3-174">Start-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="19fc3-175">Stop-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="19fc3-175">Stop-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="19fc3-176">Update-ServiceFabricRepairTaskHealthPolicy</span><span class="sxs-lookup"><span data-stu-id="19fc3-176">Update-ServiceFabricRepairTaskHealthPolicy</span></span>



## <a name="next-steps"></a><span data-ttu-id="19fc3-177">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="19fc3-177">Next steps</span></span>
* [<span data-ttu-id="19fc3-178">Linux üzerinde geliştirme ortamınızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="19fc3-178">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="19fc3-179">OSX üzerinde geliştirme ortamınızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="19fc3-179">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="19fc3-180">Linux üzerinde Yeoman kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="19fc3-180">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="19fc3-181">Linux üzerinde Eclipse için Service Fabric Eklentisi kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="19fc3-181">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="19fc3-182">Linux üzerinde ilk CSharp uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="19fc3-182">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="19fc3-183">Merhaba Service Fabric CLI toomanage uygulamalarınızı kullanın</span><span class="sxs-lookup"><span data-stu-id="19fc3-183">Use hello Service Fabric CLI toomanage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
