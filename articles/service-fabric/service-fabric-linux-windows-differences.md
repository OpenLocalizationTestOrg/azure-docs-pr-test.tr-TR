---
title: "Linux ile Windows arasındaki Azure Service Fabric farkları | Microsoft Docs"
description: "Linux üzerindeki Azure Service Fabric Önizlemesi ile Windows üzerindeki Azure Service Fabric arasındaki farklar."
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
ms.openlocfilehash: 7b80bb7d4a4e6a1b4cf47ce87200f47339785c53
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="differences-between-service-fabric-on-linux-preview-and-windows-generally-available"></a><span data-ttu-id="719e0-103">Linux (önizleme) ve Windows (genel kullanıma açık) üzerindeki Service Fabric arasındaki farklar</span><span class="sxs-lookup"><span data-stu-id="719e0-103">Differences between Service Fabric on Linux (preview) and Windows (generally available)</span></span>

<span data-ttu-id="719e0-104">Linux üzerinde Service Fabric önizleme aşamasında olduğundan, Windows’ta desteklenip Linux’ta henüz desteklenmeyen bazı özellikler mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="719e0-104">Since Service Fabric on Linux is a preview, there are some features that are supported on Windows, but not yet on Linux.</span></span> <span data-ttu-id="719e0-105">Linux üzerindeki Service Fabric genel kullanıma sunulduğunda özellik kümeleri de eşit olacaktır.</span><span class="sxs-lookup"><span data-stu-id="719e0-105">Eventually, the feature sets will be at parity when Service Fabric on Linux becomes generally available.</span></span> <span data-ttu-id="719e0-106">Gelecek sürümlerle birlikte bu özellik farkı azalacaktır.</span><span class="sxs-lookup"><span data-stu-id="719e0-106">With upcoming releases, this feature gap will shrink.</span></span> <span data-ttu-id="719e0-107">Mevcut son sürümler arasında (diğer bir deyişle Windows üzerindeki 5.6 sürümü ve Linux üzerindeki 5.5 sürümü arasında) aşağıdaki farklar mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="719e0-107">The following differences exist between the latest available releases (that is, between version 5.6 on Windows and version 5.5 on Linux):</span></span> 

* <span data-ttu-id="719e0-108">Güvenilir Koleksiyonlar (ve Güvenilir Durum Bilgisi Olan Hizmetler)</span><span class="sxs-lookup"><span data-stu-id="719e0-108">Reliable Collections (and Reliable Stateful Services)</span></span> 
* <span data-ttu-id="719e0-109">Ters ara sunucu</span><span class="sxs-lookup"><span data-stu-id="719e0-109">ReverseProxy</span></span> 
* <span data-ttu-id="719e0-110">Tek başına yükleyici</span><span class="sxs-lookup"><span data-stu-id="719e0-110">Standalone installer</span></span> 
* <span data-ttu-id="719e0-111">Bildirim dosyaları için XML şema doğrulaması</span><span class="sxs-lookup"><span data-stu-id="719e0-111">XML schema validation for manifest files</span></span> 
* <span data-ttu-id="719e0-112">Konsol yeniden yönlendirmesi</span><span class="sxs-lookup"><span data-stu-id="719e0-112">Console redirection</span></span> 
* <span data-ttu-id="719e0-113">Hata Analizi Hizmeti (FAS)</span><span class="sxs-lookup"><span data-stu-id="719e0-113">The Fault Analysis Service (FAS)</span></span>
* <span data-ttu-id="719e0-114">Kapsayıcılar için Docker Compose, birim ve günlük sürücüleri</span><span class="sxs-lookup"><span data-stu-id="719e0-114">Docker compose and volume and logging drivers for containers</span></span> 
* <span data-ttu-id="719e0-115">Kapsayıcılar ve hizmetler için kaynak idaresi</span><span class="sxs-lookup"><span data-stu-id="719e0-115">Resource governance for containers and services</span></span> 
* <span data-ttu-id="719e0-116">DNS hizmeti</span><span class="sxs-lookup"><span data-stu-id="719e0-116">DNS service</span></span>
* <span data-ttu-id="719e0-117">Azure Active Directory desteği</span><span class="sxs-lookup"><span data-stu-id="719e0-117">Azure Active Directory support</span></span>
* <span data-ttu-id="719e0-118">Belirli PowerShell komutlarının CLI komutu eşdeğerleri</span><span class="sxs-lookup"><span data-stu-id="719e0-118">CLI command equivalents of certain Powershell commands</span></span> 
* <span data-ttu-id="719e0-119">Bir Linux kümesinde PowerShell komutlarının yalnızca bir alt kümesi çalıştırılabilir (sonraki bölümde ayrıntılı olarak verilmiştir).</span><span class="sxs-lookup"><span data-stu-id="719e0-119">Only a subset of Powershell commands can be run against a Linux cluster (as expanded in the next section).</span></span>

>[!NOTE]
><span data-ttu-id="719e0-120">Konsol yönlendirmesi, Windows’ta bile üretim kümelerinde desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="719e0-120">Console redirection is not supported in production clusters, even on Windows.</span></span>

<span data-ttu-id="719e0-121">Geliştirme araçları da Windows ile Linux arasında farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="719e0-121">Development tooling is also different between Windows and Linux.</span></span> <span data-ttu-id="719e0-122">VisualStudio, Powershell, VSTS ve ETW özellikleri Windows üzerinde kullanılabilirken, Linux üzerinde Yeoman, Eclipse, Jenkins ve LTTng kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="719e0-122">VisualStudio, Powershell, VSTS, and ETW are used on Windows while Yeoman, Eclipse, Jenkins, and LTTng are used on Linux.</span></span>

## <a name="powershell-cmdlets-that-do-not-work-against-a-linux-service-fabric-cluster"></a><span data-ttu-id="719e0-123">Linux Service Fabric kümesinde çalışmayan PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="719e0-123">Powershell cmdlets that do not work against a Linux Service Fabric cluster</span></span>

* <span data-ttu-id="719e0-124">Invoke-ServiceFabricChaosTestScenario</span><span class="sxs-lookup"><span data-stu-id="719e0-124">Invoke-ServiceFabricChaosTestScenario</span></span>
* <span data-ttu-id="719e0-125">Invoke-ServiceFabricFailoverTestScenario</span><span class="sxs-lookup"><span data-stu-id="719e0-125">Invoke-ServiceFabricFailoverTestScenario</span></span>
* <span data-ttu-id="719e0-126">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="719e0-126">Invoke-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="719e0-127">Invoke-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="719e0-127">Invoke-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="719e0-128">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="719e0-128">Restart-ServiceFabricPartition</span></span>
* <span data-ttu-id="719e0-129">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="719e0-129">Start-ServiceFabricNode</span></span>
* <span data-ttu-id="719e0-130">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="719e0-130">Stop-ServiceFabricNode</span></span>
* <span data-ttu-id="719e0-131">Get-ServiceFabricImageStoreContent</span><span class="sxs-lookup"><span data-stu-id="719e0-131">Get-ServiceFabricImageStoreContent</span></span>
* <span data-ttu-id="719e0-132">Get-ServiceFabricChaosReport</span><span class="sxs-lookup"><span data-stu-id="719e0-132">Get-ServiceFabricChaosReport</span></span>
* <span data-ttu-id="719e0-133">Get-ServiceFabricNodeTransitionProgress</span><span class="sxs-lookup"><span data-stu-id="719e0-133">Get-ServiceFabricNodeTransitionProgress</span></span>
* <span data-ttu-id="719e0-134">Get-ServiceFabricPartitionDataLossProgress</span><span class="sxs-lookup"><span data-stu-id="719e0-134">Get-ServiceFabricPartitionDataLossProgress</span></span>
* <span data-ttu-id="719e0-135">Get-ServiceFabricPartitionQuorumLossProgress</span><span class="sxs-lookup"><span data-stu-id="719e0-135">Get-ServiceFabricPartitionQuorumLossProgress</span></span>
* <span data-ttu-id="719e0-136">Get-ServiceFabricPartitionRestartProgress</span><span class="sxs-lookup"><span data-stu-id="719e0-136">Get-ServiceFabricPartitionRestartProgress</span></span>
* <span data-ttu-id="719e0-137">Get-ServiceFabricTestCommandStatusList</span><span class="sxs-lookup"><span data-stu-id="719e0-137">Get-ServiceFabricTestCommandStatusList</span></span>
* <span data-ttu-id="719e0-138">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="719e0-138">Remove-ServiceFabricTestState</span></span>
* <span data-ttu-id="719e0-139">Start-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="719e0-139">Start-ServiceFabricChaos</span></span>
* <span data-ttu-id="719e0-140">Start-ServiceFabricNodeTransition</span><span class="sxs-lookup"><span data-stu-id="719e0-140">Start-ServiceFabricNodeTransition</span></span>
* <span data-ttu-id="719e0-141">Start-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="719e0-141">Start-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="719e0-142">Start-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="719e0-142">Start-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="719e0-143">Start-ServiceFabricPartitionRestart</span><span class="sxs-lookup"><span data-stu-id="719e0-143">Start-ServiceFabricPartitionRestart</span></span>
* <span data-ttu-id="719e0-144">Stop-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="719e0-144">Stop-ServiceFabricChaos</span></span>
* <span data-ttu-id="719e0-145">Stop-ServiceFabricTestCommand</span><span class="sxs-lookup"><span data-stu-id="719e0-145">Stop-ServiceFabricTestCommand</span></span>
* <span data-ttu-id="719e0-146">Cmd</span><span class="sxs-lookup"><span data-stu-id="719e0-146">Cmd</span></span>
* <span data-ttu-id="719e0-147">Get-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="719e0-147">Get-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="719e0-148">Get-ServiceFabricClusterConfiguration</span><span class="sxs-lookup"><span data-stu-id="719e0-148">Get-ServiceFabricClusterConfiguration</span></span>
* <span data-ttu-id="719e0-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span><span class="sxs-lookup"><span data-stu-id="719e0-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span></span>
* <span data-ttu-id="719e0-150">Get-ServiceFabricPackageDebugParameters</span><span class="sxs-lookup"><span data-stu-id="719e0-150">Get-ServiceFabricPackageDebugParameters</span></span>
* <span data-ttu-id="719e0-151">New-ServiceFabricPackageDebugParameter</span><span class="sxs-lookup"><span data-stu-id="719e0-151">New-ServiceFabricPackageDebugParameter</span></span>
* <span data-ttu-id="719e0-152">New-ServiceFabricPackageSharingPolicy</span><span class="sxs-lookup"><span data-stu-id="719e0-152">New-ServiceFabricPackageSharingPolicy</span></span>
* <span data-ttu-id="719e0-153">Add-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="719e0-153">Add-ServiceFabricNode</span></span>
* <span data-ttu-id="719e0-154">Copy-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="719e0-154">Copy-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="719e0-155">Get-ServiceFabricRuntimeSupportedVersion</span><span class="sxs-lookup"><span data-stu-id="719e0-155">Get-ServiceFabricRuntimeSupportedVersion</span></span>
* <span data-ttu-id="719e0-156">Get-ServiceFabricRuntimeUpgradeVersion</span><span class="sxs-lookup"><span data-stu-id="719e0-156">Get-ServiceFabricRuntimeUpgradeVersion</span></span>
* <span data-ttu-id="719e0-157">New-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="719e0-157">New-ServiceFabricCluster</span></span>
* <span data-ttu-id="719e0-158">New-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="719e0-158">New-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="719e0-159">Remove-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="719e0-159">Remove-ServiceFabricCluster</span></span>
* <span data-ttu-id="719e0-160">Remove-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="719e0-160">Remove-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="719e0-161">Remove-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="719e0-161">Remove-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="719e0-162">Test-ServiceFabricClusterManifest</span><span class="sxs-lookup"><span data-stu-id="719e0-162">Test-ServiceFabricClusterManifest</span></span>
* <span data-ttu-id="719e0-163">Test-ServiceFabricConfiguration</span><span class="sxs-lookup"><span data-stu-id="719e0-163">Test-ServiceFabricConfiguration</span></span>
* <span data-ttu-id="719e0-164">Update-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="719e0-164">Update-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="719e0-165">Approve-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="719e0-165">Approve-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="719e0-166">Complete-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="719e0-166">Complete-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="719e0-167">Get-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="719e0-167">Get-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="719e0-168">Invoke-ServiceFabricDecryptText</span><span class="sxs-lookup"><span data-stu-id="719e0-168">Invoke-ServiceFabricDecryptText</span></span>
* <span data-ttu-id="719e0-169">Invoke-ServiceFabricEncryptSecret</span><span class="sxs-lookup"><span data-stu-id="719e0-169">Invoke-ServiceFabricEncryptSecret</span></span>
* <span data-ttu-id="719e0-170">Invoke-ServiceFabricEncryptText</span><span class="sxs-lookup"><span data-stu-id="719e0-170">Invoke-ServiceFabricEncryptText</span></span>
* <span data-ttu-id="719e0-171">Invoke-ServiceFabricInfrastructureCommand</span><span class="sxs-lookup"><span data-stu-id="719e0-171">Invoke-ServiceFabricInfrastructureCommand</span></span>
* <span data-ttu-id="719e0-172">Invoke-ServiceFabricInfrastructureQuery</span><span class="sxs-lookup"><span data-stu-id="719e0-172">Invoke-ServiceFabricInfrastructureQuery</span></span>
* <span data-ttu-id="719e0-173">Remove-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="719e0-173">Remove-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="719e0-174">Start-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="719e0-174">Start-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="719e0-175">Stop-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="719e0-175">Stop-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="719e0-176">Update-ServiceFabricRepairTaskHealthPolicy</span><span class="sxs-lookup"><span data-stu-id="719e0-176">Update-ServiceFabricRepairTaskHealthPolicy</span></span>



## <a name="next-steps"></a><span data-ttu-id="719e0-177">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="719e0-177">Next steps</span></span>
* [<span data-ttu-id="719e0-178">Linux üzerinde geliştirme ortamınızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="719e0-178">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="719e0-179">OSX üzerinde geliştirme ortamınızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="719e0-179">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="719e0-180">Linux üzerinde Yeoman kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="719e0-180">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="719e0-181">Linux üzerinde Eclipse için Service Fabric Eklentisi kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="719e0-181">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="719e0-182">Linux üzerinde ilk CSharp uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="719e0-182">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="719e0-183">Uygulamalarınızı yönetmek için Service Fabric CLI'yı kullanma</span><span class="sxs-lookup"><span data-stu-id="719e0-183">Use the Service Fabric CLI to manage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
