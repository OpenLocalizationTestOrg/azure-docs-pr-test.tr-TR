---
title: "Azure mikro aaaSimulate başarısızlık | Microsoft Docs"
description: "Bu makalede, Microsoft Azure Service Fabric bulunan hello Test Edilebilirlik eylemler hakkında alınmaktadır."
services: service-fabric
documentationcenter: .net
author: motanv
manager: timlt
editor: toddabel
ms.assetid: ed53ca5c-4d5e-4b48-93c9-e386f32d8b7a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv;heeldin
ms.openlocfilehash: 5bdda1c0c5a40b243ab956c4791afd52e11c4089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="testability-actions"></a><span data-ttu-id="1c3e7-103">Test Edilebilirlik Eylemler</span><span class="sxs-lookup"><span data-stu-id="1c3e7-103">Testability actions</span></span>
<span data-ttu-id="1c3e7-104">Sipariş toosimulate güvenilir olmayan bir altyapı'da, Azure Service Fabric, yolları toosimulate ile Merhaba Geliştirici çeşitli gerçek hataları ve durumu geçişleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-104">In order toosimulate an unreliable infrastructure, Azure Service Fabric provides you, hello developer, with ways toosimulate various real-world failures and state transitions.</span></span> <span data-ttu-id="1c3e7-105">Bu Test Edilebilirlik eylemler olarak sunulur.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-105">These are exposed as testability actions.</span></span> <span data-ttu-id="1c3e7-106">Merhaba Eylemler hello belirli bir arıza ekleme, durum geçişi veya doğrulama neden alt düzey API'leri.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-106">hello actions are hello low-level APIs that cause a specific fault injection, state transition, or validation.</span></span> <span data-ttu-id="1c3e7-107">Bu eylemler ile birleştirerek kapsamlı test senaryoları için hizmetlerinizi yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-107">By combining these actions, you can write comprehensive test scenarios for your services.</span></span>

<span data-ttu-id="1c3e7-108">Service Fabric, bazı ortak test senaryoları bu eylemleri oluşan sağlar.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-108">Service Fabric provides some common test scenarios composed of these actions.</span></span> <span data-ttu-id="1c3e7-109">Tootest ortak durumu geçişleri ve hata durumları dikkatle seçilen bu yerleşik senaryolar kullanan öneririz.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-109">We highly recommend that you utilize these built-in scenarios, which are carefully chosen tootest common state transitions and failure cases.</span></span> <span data-ttu-id="1c3e7-110">Ancak, hello yerleşik senaryolarla henüz kapsamında yer almayan veya uygulamanız için özel olarak hazırlanmış özel olan senaryolar için tooadd kapsamı istediğinizde Eylemler kullanılan toocreate özel test senaryoları olabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-110">However, actions can be used toocreate custom test scenarios when you want tooadd coverage for scenarios that are not covered by hello built-in scenarios yet or that are custom tailored for your application.</span></span>

<span data-ttu-id="1c3e7-111">C# uygulamalarının hello eylemlerin hello System.Fabric.dll derlemesi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-111">C# implementations of hello actions are found in hello System.Fabric.dll assembly.</span></span> <span data-ttu-id="1c3e7-112">Merhaba sistem Fabric PowerShell modülü hello Microsoft.ServiceFabric.Powershell.dll derlemesi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-112">hello System Fabric PowerShell module is found in hello Microsoft.ServiceFabric.Powershell.dll assembly.</span></span> <span data-ttu-id="1c3e7-113">Çalışma zamanı yüklemesinin bir parçası olarak hello ServiceFabric PowerShell Modülü yüklü tooallow kullanım kolaylığı için ' dir.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-113">As part of runtime installation, hello ServiceFabric PowerShell module is installed tooallow for ease of use.</span></span>

## <a name="graceful-vs-ungraceful-fault-actions"></a><span data-ttu-id="1c3e7-114">Normal durunda hataya Eylemler karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="1c3e7-114">Graceful vs. ungraceful fault actions</span></span>
<span data-ttu-id="1c3e7-115">Test Edilebilirlik Eylemler iki ana demet sınıflandırılır:</span><span class="sxs-lookup"><span data-stu-id="1c3e7-115">Testability actions are classified into two major buckets:</span></span>

* <span data-ttu-id="1c3e7-116">Durunda hatası: Bu hataları hataları makine yeniden başlatmaları gibi benzetimini gerçekleştirmek ve işlem kilitleniyor.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-116">Ungraceful faults: These faults simulate failures like machine restarts and process crashes.</span></span> <span data-ttu-id="1c3e7-117">Hatalar bu gibi durumlarda hello yürütme bağlamı işleminin aniden durdurur.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-117">In such cases of failures, hello execution context of process stops abruptly.</span></span> <span data-ttu-id="1c3e7-118">Bu, hello uygulama yeniden başlatılmadan önce hello durumunun temizleme çalıştırabileceğiniz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-118">This means no cleanup of hello state can run before hello application starts up again.</span></span>
* <span data-ttu-id="1c3e7-119">Normal hatası: Bu hataları çoğaltma taşır gibi normal eylemlerin ve Yük Dengeleme tarafından tetiklenen düşme benzetimini yapma.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-119">Graceful faults: These faults simulate graceful actions like replica moves and drops triggered by load balancing.</span></span> <span data-ttu-id="1c3e7-120">Böyle durumlarda, hello hizmeti hello bildirimi Kapat alır ve hello durumunu çıkmadan önce temizleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-120">In such cases, hello service gets a notification of hello close and can clean up hello state before exiting.</span></span>

<span data-ttu-id="1c3e7-121">Daha iyi kalite doğrulama hello hizmetini çalıştırmak ve iş yükünü inducing çeşitli normal ve durunda hataları oluştu.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-121">For better quality validation, run hello service and business workload while inducing various graceful and ungraceful faults.</span></span> <span data-ttu-id="1c3e7-122">Durunda hataları burada hello hizmeti aniden bazı iş akışı hello ortadaki çıkılıyor senaryoları uygulamaktadır.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-122">Ungraceful faults exercise scenarios where hello service process abruptly exits in hello middle of some workflow.</span></span> <span data-ttu-id="1c3e7-123">Merhaba hizmet çoğaltma Service Fabric tarafından geri yüklendikten sonra bu testleri hello kurtarma yolu.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-123">This tests  hello recovery path once hello service replica is restored by Service Fabric.</span></span> <span data-ttu-id="1c3e7-124">Bu, veri tutarlılığı ve hello hizmeti durumu hataları sonra doğru olup olmadığını yönetilmesini test yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-124">This will help test data consistency and whether hello service state is maintained correctly after failures.</span></span> <span data-ttu-id="1c3e7-125">Merhaba diğer hatalar (Merhaba normal hata sayısı) sınama kümesi hello hizmet Service Fabric tarafından taşınan tooreplicas doğru şekilde yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-125">hello other set of failures (hello graceful failures) test that hello service correctly reacts tooreplicas being moved around by Service Fabric.</span></span> <span data-ttu-id="1c3e7-126">Bu işleme iptal hello RunAsync yönteminde sınar.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-126">This tests handling of cancellation in hello RunAsync method.</span></span> <span data-ttu-id="1c3e7-127">Merhaba hizmetinin toocheck hello iptal belirteci ayarlayın, durumunu doğru şekilde kaydedin ve hello RunAsync yöntemi çıkın olmak için gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-127">hello service needs toocheck for hello cancellation token being set, correctly save its state, and exit hello RunAsync method.</span></span>

## <a name="testability-actions-list"></a><span data-ttu-id="1c3e7-128">Test Edilebilirlik eylemler listesi</span><span class="sxs-lookup"><span data-stu-id="1c3e7-128">Testability actions list</span></span>
| <span data-ttu-id="1c3e7-129">Eylem</span><span class="sxs-lookup"><span data-stu-id="1c3e7-129">Action</span></span> | <span data-ttu-id="1c3e7-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1c3e7-130">Description</span></span> | <span data-ttu-id="1c3e7-131">Yönetilen API</span><span class="sxs-lookup"><span data-stu-id="1c3e7-131">Managed API</span></span> | <span data-ttu-id="1c3e7-132">PowerShell cmdlet'i</span><span class="sxs-lookup"><span data-stu-id="1c3e7-132">PowerShell cmdlet</span></span> | <span data-ttu-id="1c3e7-133">Normal/durunda hataları</span><span class="sxs-lookup"><span data-stu-id="1c3e7-133">Graceful/ungraceful faults</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="1c3e7-134">CleanTestState</span><span class="sxs-lookup"><span data-stu-id="1c3e7-134">CleanTestState</span></span> |<span data-ttu-id="1c3e7-135">Merhaba küme hello test sürücüsünün hatalı bir kapanma durumunda tüm hello test durumlarını kaldırır.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-135">Removes all hello test state from hello cluster in case of a bad shutdown of hello test driver.</span></span> |<span data-ttu-id="1c3e7-136">CleanTestStateAsync</span><span class="sxs-lookup"><span data-stu-id="1c3e7-136">CleanTestStateAsync</span></span> |<span data-ttu-id="1c3e7-137">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="1c3e7-137">Remove-ServiceFabricTestState</span></span> |<span data-ttu-id="1c3e7-138">Uygulanamaz</span><span class="sxs-lookup"><span data-stu-id="1c3e7-138">Not applicable</span></span> |
| <span data-ttu-id="1c3e7-139">InvokeDataLoss</span><span class="sxs-lookup"><span data-stu-id="1c3e7-139">InvokeDataLoss</span></span> |<span data-ttu-id="1c3e7-140">Veri kaybı hizmet bölüme uygulanmasını.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-140">Induces data loss into a service partition.</span></span> |<span data-ttu-id="1c3e7-141">InvokeDataLossAsync</span><span class="sxs-lookup"><span data-stu-id="1c3e7-141">InvokeDataLossAsync</span></span> |<span data-ttu-id="1c3e7-142">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="1c3e7-142">Invoke-ServiceFabricPartitionDataLoss</span></span> |<span data-ttu-id="1c3e7-143">Normal</span><span class="sxs-lookup"><span data-stu-id="1c3e7-143">Graceful</span></span> |
| <span data-ttu-id="1c3e7-144">InvokeQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="1c3e7-144">InvokeQuorumLoss</span></span> |<span data-ttu-id="1c3e7-145">Belirtilen durum bilgisi olan hizmet bölüm çekirdek kayıp yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-145">Puts a given stateful service partition into quorum loss.</span></span> |<span data-ttu-id="1c3e7-146">InvokeQuorumLossAsync</span><span class="sxs-lookup"><span data-stu-id="1c3e7-146">InvokeQuorumLossAsync</span></span> |<span data-ttu-id="1c3e7-147">Çağırma ServiceFabricQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="1c3e7-147">Invoke-ServiceFabricQuorumLoss</span></span> |<span data-ttu-id="1c3e7-148">Normal</span><span class="sxs-lookup"><span data-stu-id="1c3e7-148">Graceful</span></span> |
| <span data-ttu-id="1c3e7-149">Birincil taşıma</span><span class="sxs-lookup"><span data-stu-id="1c3e7-149">Move Primary</span></span> |<span data-ttu-id="1c3e7-150">Taşıma hello birincil çoğaltma bir durum bilgisi olan hizmet toohello belirtilen küme düğümü belirtilen.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-150">Moves hello specified primary replica of a stateful service toohello specified cluster node.</span></span> |<span data-ttu-id="1c3e7-151">MovePrimaryAsync</span><span class="sxs-lookup"><span data-stu-id="1c3e7-151">MovePrimaryAsync</span></span> |<span data-ttu-id="1c3e7-152">Taşıma ServiceFabricPrimaryReplica</span><span class="sxs-lookup"><span data-stu-id="1c3e7-152">Move-ServiceFabricPrimaryReplica</span></span> |<span data-ttu-id="1c3e7-153">Normal</span><span class="sxs-lookup"><span data-stu-id="1c3e7-153">Graceful</span></span> |
| <span data-ttu-id="1c3e7-154">İkincil taşıma</span><span class="sxs-lookup"><span data-stu-id="1c3e7-154">Move Secondary</span></span> |<span data-ttu-id="1c3e7-155">Merhaba geçerli ikincil çoğaltma bir durum bilgisi olan hizmet tooa farklı küme düğümü taşır.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-155">Moves hello current secondary replica of a stateful service tooa different cluster node.</span></span> |<span data-ttu-id="1c3e7-156">MoveSecondaryAsync</span><span class="sxs-lookup"><span data-stu-id="1c3e7-156">MoveSecondaryAsync</span></span> |<span data-ttu-id="1c3e7-157">Taşıma ServiceFabricSecondaryReplica</span><span class="sxs-lookup"><span data-stu-id="1c3e7-157">Move-ServiceFabricSecondaryReplica</span></span> |<span data-ttu-id="1c3e7-158">Normal</span><span class="sxs-lookup"><span data-stu-id="1c3e7-158">Graceful</span></span> |
| <span data-ttu-id="1c3e7-159">RemoveReplica</span><span class="sxs-lookup"><span data-stu-id="1c3e7-159">RemoveReplica</span></span> |<span data-ttu-id="1c3e7-160">Bir çoğaltma hatası bir kümeden bir çoğaltma kaldırarak benzetimini yapar.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-160">Simulates a replica failure by removing a replica from a cluster.</span></span> <span data-ttu-id="1c3e7-161">Bu hello çoğaltma kapatılacak ve toorole geçirecektir 'None', durumunun tamamı hello kümeden kaldırma.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-161">This will close hello replica and will transition it toorole 'None', removing all of its state from hello cluster.</span></span> |<span data-ttu-id="1c3e7-162">RemoveReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="1c3e7-162">RemoveReplicaAsync</span></span> |<span data-ttu-id="1c3e7-163">Remove-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="1c3e7-163">Remove-ServiceFabricReplica</span></span> |<span data-ttu-id="1c3e7-164">Normal</span><span class="sxs-lookup"><span data-stu-id="1c3e7-164">Graceful</span></span> |
| <span data-ttu-id="1c3e7-165">RestartDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="1c3e7-165">RestartDeployedCodePackage</span></span> |<span data-ttu-id="1c3e7-166">Kod paketi işlemi başarısız bir kümedeki bir düğümün dağıtılmış kod paketi yeniden başlatarak benzetimini yapar.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-166">Simulates a code package process failure by restarting a code package deployed on a node in a cluster.</span></span> <span data-ttu-id="1c3e7-167">Bu işlemde barındırılan tüm hello kullanıcı hizmet çoğaltmalar yeniden hello kod paket işlemi durdurur.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-167">This aborts hello code package process, which will restart all hello user service replicas hosted in that process.</span></span> |<span data-ttu-id="1c3e7-168">RestartDeployedCodePackageAsync</span><span class="sxs-lookup"><span data-stu-id="1c3e7-168">RestartDeployedCodePackageAsync</span></span> |<span data-ttu-id="1c3e7-169">Yeniden başlatma ServiceFabricDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="1c3e7-169">Restart-ServiceFabricDeployedCodePackage</span></span> |<span data-ttu-id="1c3e7-170">Durunda</span><span class="sxs-lookup"><span data-stu-id="1c3e7-170">Ungraceful</span></span> |
| <span data-ttu-id="1c3e7-171">RestartNode</span><span class="sxs-lookup"><span data-stu-id="1c3e7-171">RestartNode</span></span> |<span data-ttu-id="1c3e7-172">Bir Service Fabric kümesi düğüm hatasından bir düğümü yeniden başlatarak benzetimini yapar.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-172">Simulates a Service Fabric cluster node failure by restarting a node.</span></span> |<span data-ttu-id="1c3e7-173">RestartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="1c3e7-173">RestartNodeAsync</span></span> |<span data-ttu-id="1c3e7-174">Yeniden başlatma ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="1c3e7-174">Restart-ServiceFabricNode</span></span> |<span data-ttu-id="1c3e7-175">Durunda</span><span class="sxs-lookup"><span data-stu-id="1c3e7-175">Ungraceful</span></span> |
| <span data-ttu-id="1c3e7-176">RestartPartition</span><span class="sxs-lookup"><span data-stu-id="1c3e7-176">RestartPartition</span></span> |<span data-ttu-id="1c3e7-177">Bir veri merkezi Kararma veya küme Kararma senaryosu bir bölüm, bazı veya tüm çoğaltmaları yeniden başlatarak benzetimini yapar.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-177">Simulates a datacenter blackout or cluster blackout scenario by restarting some or all replicas of a partition.</span></span> |<span data-ttu-id="1c3e7-178">RestartPartitionAsync</span><span class="sxs-lookup"><span data-stu-id="1c3e7-178">RestartPartitionAsync</span></span> |<span data-ttu-id="1c3e7-179">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="1c3e7-179">Restart-ServiceFabricPartition</span></span> |<span data-ttu-id="1c3e7-180">Normal</span><span class="sxs-lookup"><span data-stu-id="1c3e7-180">Graceful</span></span> |
| <span data-ttu-id="1c3e7-181">RestartReplica</span><span class="sxs-lookup"><span data-stu-id="1c3e7-181">RestartReplica</span></span> |<span data-ttu-id="1c3e7-182">Bir çoğaltma hatası kalıcı çoğaltma bir kümede yeniden hello çoğaltma kapatma ve yeniden açmayı benzetimini yapar.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-182">Simulates a replica failure by restarting a persisted replica in a cluster, closing hello replica and then reopening it.</span></span> |<span data-ttu-id="1c3e7-183">RestartReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="1c3e7-183">RestartReplicaAsync</span></span> |<span data-ttu-id="1c3e7-184">Yeniden başlatma ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="1c3e7-184">Restart-ServiceFabricReplica</span></span> |<span data-ttu-id="1c3e7-185">Normal</span><span class="sxs-lookup"><span data-stu-id="1c3e7-185">Graceful</span></span> |
| <span data-ttu-id="1c3e7-186">BaşlangıçDüğümü</span><span class="sxs-lookup"><span data-stu-id="1c3e7-186">StartNode</span></span> |<span data-ttu-id="1c3e7-187">Bir düğüm zaten durdurulmuş bir kümede başlatır.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-187">Starts a node in a cluster that is already stopped.</span></span> |<span data-ttu-id="1c3e7-188">StartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="1c3e7-188">StartNodeAsync</span></span> |<span data-ttu-id="1c3e7-189">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="1c3e7-189">Start-ServiceFabricNode</span></span> |<span data-ttu-id="1c3e7-190">Uygulanamaz</span><span class="sxs-lookup"><span data-stu-id="1c3e7-190">Not applicable</span></span> |
| <span data-ttu-id="1c3e7-191">StopNode</span><span class="sxs-lookup"><span data-stu-id="1c3e7-191">StopNode</span></span> |<span data-ttu-id="1c3e7-192">Bir düğüm hatasından bir küme düğümünde durdurarak benzetimini yapar.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-192">Simulates a node failure by stopping a node in a cluster.</span></span> <span data-ttu-id="1c3e7-193">BaşlangıçDüğümü çağrılıncaya kadar hello düğümü kapalı kalır.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-193">hello node will stay down until StartNode is called.</span></span> |<span data-ttu-id="1c3e7-194">StopNodeAsync</span><span class="sxs-lookup"><span data-stu-id="1c3e7-194">StopNodeAsync</span></span> |<span data-ttu-id="1c3e7-195">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="1c3e7-195">Stop-ServiceFabricNode</span></span> |<span data-ttu-id="1c3e7-196">Durunda</span><span class="sxs-lookup"><span data-stu-id="1c3e7-196">Ungraceful</span></span> |
| <span data-ttu-id="1c3e7-197">ValidateApplication</span><span class="sxs-lookup"><span data-stu-id="1c3e7-197">ValidateApplication</span></span> |<span data-ttu-id="1c3e7-198">Merhaba kullanılabilirlik ve bazı hata hello sisteme inducing sonra genellikle bir uygulamadaki tüm Service Fabric Hizmetleri durumunu doğrular.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-198">Validates hello availability and health of all Service Fabric services within an application, usually after inducing some fault into hello system.</span></span> |<span data-ttu-id="1c3e7-199">ValidateApplicationAsync</span><span class="sxs-lookup"><span data-stu-id="1c3e7-199">ValidateApplicationAsync</span></span> |<span data-ttu-id="1c3e7-200">Test-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="1c3e7-200">Test-ServiceFabricApplication</span></span> |<span data-ttu-id="1c3e7-201">Uygulanamaz</span><span class="sxs-lookup"><span data-stu-id="1c3e7-201">Not applicable</span></span> |
| <span data-ttu-id="1c3e7-202">ValidateService</span><span class="sxs-lookup"><span data-stu-id="1c3e7-202">ValidateService</span></span> |<span data-ttu-id="1c3e7-203">Merhaba kullanılabilirlik ve Service Fabric hizmeti bazı hata hello sisteme genellikle inducing sonra doğrular.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-203">Validates hello availability and health of a Service Fabric service, usually after inducing some fault into hello system.</span></span> |<span data-ttu-id="1c3e7-204">ValidateServiceAsync</span><span class="sxs-lookup"><span data-stu-id="1c3e7-204">ValidateServiceAsync</span></span> |<span data-ttu-id="1c3e7-205">Test-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="1c3e7-205">Test-ServiceFabricService</span></span> |<span data-ttu-id="1c3e7-206">Uygulanamaz</span><span class="sxs-lookup"><span data-stu-id="1c3e7-206">Not applicable</span></span> |

## <a name="running-a-testability-action-using-powershell"></a><span data-ttu-id="1c3e7-207">PowerShell kullanarak bir Test Edilebilirlik eylem çalıştırma</span><span class="sxs-lookup"><span data-stu-id="1c3e7-207">Running a testability action using PowerShell</span></span>
<span data-ttu-id="1c3e7-208">Bu öğretici şunların nasıl yapıldığını gösterir toorun PowerShell kullanarak bir Test Edilebilirlik eylem.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-208">This tutorial shows you how toorun a testability action by using PowerShell.</span></span> <span data-ttu-id="1c3e7-209">Şunları öğreneceksiniz nasıl toorun yerel (bir çalıştırma) küme veya bir Azure kümesine karşı Test Edilebilirlik eylem.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-209">You will learn how toorun a testability action against a local (one-box) cluster or an Azure cluster.</span></span> <span data-ttu-id="1c3e7-210">Microsoft.Fabric.Powershell.dll--hello Service Fabric PowerShell modülü--otomatik olarak yüklenir hello Microsoft Service Fabric MSI yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-210">Microsoft.Fabric.Powershell.dll--hello Service Fabric PowerShell module--is installed automatically when you install hello Microsoft Service Fabric MSI.</span></span> <span data-ttu-id="1c3e7-211">Merhaba modülü, PowerShell istemi açtığınızda otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-211">hello module is loaded automatically when you open a PowerShell prompt.</span></span>

<span data-ttu-id="1c3e7-212">Eğitmen kesimleri:</span><span class="sxs-lookup"><span data-stu-id="1c3e7-212">Tutorial segments:</span></span>

* [<span data-ttu-id="1c3e7-213">Bir eylem karşı bir kutusunu küme çalıştırın</span><span class="sxs-lookup"><span data-stu-id="1c3e7-213">Run an action against a one-box cluster</span></span>](#run-an-action-against-a-one-box-cluster)
* [<span data-ttu-id="1c3e7-214">Bir eylem Azure bir küme karşı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="1c3e7-214">Run an action against an Azure cluster</span></span>](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a><span data-ttu-id="1c3e7-215">Bir eylem karşı bir kutusunu küme çalıştırın</span><span class="sxs-lookup"><span data-stu-id="1c3e7-215">Run an action against a one-box cluster</span></span>
<span data-ttu-id="1c3e7-216">toorun yerel bir küme karşı Test Edilebilirlik eylem, toohello küme ve Yönetici modu açık hello PowerShell komut isteminde önce bağlanın.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-216">toorun a testability action against a local cluster, first connect toohello cluster and open hello PowerShell prompt in administrator mode.</span></span> <span data-ttu-id="1c3e7-217">Bize hello Ara **yeniden ServiceFabricNode** eylem.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-217">Let us look at hello **Restart-ServiceFabricNode** action.</span></span>

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

<span data-ttu-id="1c3e7-218">Burada, eylemin hello **yeniden ServiceFabricNode** "Düğüm1" adlı bir düğümde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-218">Here hello action **Restart-ServiceFabricNode** is being run on a node named "Node1".</span></span> <span data-ttu-id="1c3e7-219">Hello tamamlanma modu, hello düğümü yeniden başlatma eylemi gerçekten başarılı olup olmadığını doğrulamalıdır değil olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-219">hello completion mode specifies that it should not verify whether hello restart-node action actually succeeded.</span></span> <span data-ttu-id="1c3e7-220">Hello yeniden başlatma eylemi gerçekten başarılı olup olmadığını belirten hello tamamlama modu "Doğrula" olarak tooverify neden olur.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-220">Specifying hello completion mode as "Verify" will cause it tooverify whether hello restart action actually succeeded.</span></span> <span data-ttu-id="1c3e7-221">Merhaba düğüm adıyla doğrudan belirtmek yerine, çoğaltma, bir bölüm anahtarı ve hello tür ile aşağıdaki gibi belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1c3e7-221">Instead of directly specifying hello node by its name, you can specify it via a partition key and hello kind of replica, as follows:</span></span>

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

<span data-ttu-id="1c3e7-222">**Yeniden başlatma ServiceFabricNode** kullanılan toorestart bir kümede bir Service Fabric olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-222">**Restart-ServiceFabricNode** should be used toorestart a Service Fabric node in a cluster.</span></span> <span data-ttu-id="1c3e7-223">Bu, tüm bu düğümde barındırılan hello sistemi hizmeti ve kullanıcı hizmet çoğaltmalar yeniden hello Fabric.exe işlemi durdurulacak.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-223">This will stop hello Fabric.exe process, which will restart all of hello system service and user service replicas hosted on that node.</span></span> <span data-ttu-id="1c3e7-224">Bu API tootest kullanarak, hizmetinizi hello yük devretme kurtarma yolları boyunca hatalar ortaya çıkarmaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-224">Using this API tootest your service helps uncover bugs along hello failover recovery paths.</span></span> <span data-ttu-id="1c3e7-225">Merhaba kümedeki düğüm hatalarını benzetimini yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-225">It helps simulate node failures in hello cluster.</span></span>

<span data-ttu-id="1c3e7-226">Merhaba aşağıdaki ekran gösterilir hello **yeniden ServiceFabricNode** eylem Test Edilebilirlik komutu.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-226">hello following screenshot shows hello **Restart-ServiceFabricNode** testability command in action.</span></span>

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

<span data-ttu-id="1c3e7-227">Merhaba hello ilk çıkış **Get-ServiceFabricNode** (Merhaba Service Fabric PowerShell modülden bir cmdlet) bu hello yerel küme sahip beş düğüm gösterir: Node.1 tooNode.5.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-227">hello output of hello first **Get-ServiceFabricNode** (a cmdlet from hello Service Fabric PowerShell module) shows that hello local cluster has five nodes: Node.1 tooNode.5.</span></span> <span data-ttu-id="1c3e7-228">Merhaba Test Edilebilirlik eylem (cmdlet'ini) sonra **yeniden ServiceFabricNode** hello düğümde yürütülen Node.4 adlı, biz bu hello düğümün çalışır durumda kalma süresi sıfırlama bakın.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-228">After hello testability action (cmdlet) **Restart-ServiceFabricNode** is executed on hello node, named Node.4, we see that hello node's uptime has been reset.</span></span>

### <a name="run-an-action-against-an-azure-cluster"></a><span data-ttu-id="1c3e7-229">Bir eylem Azure bir küme karşı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="1c3e7-229">Run an action against an Azure cluster</span></span>
<span data-ttu-id="1c3e7-230">Bir Test Edilebilirlik eylemi (PowerShell kullanarak) çalıştıran bir Azure küme karşı benzer toorunning hello yerel bir küme karşı eylemdir.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-230">Running a testability action (by using PowerShell) against an Azure cluster is similar toorunning hello action against a local cluster.</span></span> <span data-ttu-id="1c3e7-231">bağlantı toohello yerel küme, yerine hello eylem çalıştırmadan önce fark, yalnızca hello tooconnect toohello Azure ihtiyacınız ilk küme.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-231">hello only difference is that before you can run hello action, instead of connecting toohello local cluster, you need tooconnect toohello Azure cluster first.</span></span>

## <a name="running-a-testability-action-using-c35"></a><span data-ttu-id="1c3e7-232">C & #35 kullanarak bir Test Edilebilirlik eylemi çalıştıran;</span><span class="sxs-lookup"><span data-stu-id="1c3e7-232">Running a testability action using C&#35;</span></span>
<span data-ttu-id="1c3e7-233">C# kullanarak bir Test Edilebilirlik eylemi toorun, öncelikle tooconnect toohello küme FabricClient kullanarak gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-233">toorun a testability action by using C#, first you need tooconnect toohello cluster by using FabricClient.</span></span> <span data-ttu-id="1c3e7-234">Ardından hello gerekli parametreleri toorun hello eylem edinin.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-234">Then obtain hello parameters needed toorun hello action.</span></span> <span data-ttu-id="1c3e7-235">Farklı parametreler kullanılabilir toorun hello aynı eylemi.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-235">Different parameters can be used toorun hello same action.</span></span>
<span data-ttu-id="1c3e7-236">Merhaba kümede hello RestartServiceFabricNode eylemin hello düğümü bilgileri (düğüm adı ve düğüm örnek kimliği) kullanarak olan tek yönlü toorun bakarak.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-236">Looking at hello RestartServiceFabricNode action, one way toorun it is by using hello node information (node name and node instance ID) in hello cluster.</span></span>

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

<span data-ttu-id="1c3e7-237">Parametre açıklaması:</span><span class="sxs-lookup"><span data-stu-id="1c3e7-237">Parameter explanation:</span></span>

* <span data-ttu-id="1c3e7-238">**CompleteMode** bu hello modu doğrulama hello yeniden başlatma eylemi gerçekten başarılı olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-238">**CompleteMode** specifies that hello mode should not verify whether hello restart action actually succeeded.</span></span> <span data-ttu-id="1c3e7-239">Hello yeniden başlatma eylemi gerçekten başarılı olup olmadığını belirten hello tamamlama modu "Doğrula" olarak tooverify neden olur.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-239">Specifying hello completion mode as "Verify" will cause it tooverify whether hello restart action actually succeeded.</span></span>  
* <span data-ttu-id="1c3e7-240">**OperationTimeout** kümeleri hello hello işlemi toofinish süresini TimeoutException özel durum önce.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-240">**OperationTimeout** sets hello amount of time for hello operation toofinish before a TimeoutException exception is thrown.</span></span>
* <span data-ttu-id="1c3e7-241">**CancellationToken** iptal bekleyen çağrı toobe sağlar.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-241">**CancellationToken** enables a pending call toobe canceled.</span></span>

<span data-ttu-id="1c3e7-242">Merhaba düğüm adıyla doğrudan belirtmek yerine, bir bölüm anahtarı ve hello tür çoğaltma aracılığıyla belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-242">Instead of directly specifying hello node by its name, you can specify it via a partition key and hello kind of replica.</span></span>

<span data-ttu-id="1c3e7-243">Daha fazla bilgi için bkz: [PartitionSelector ve ReplicaSelector](#partition_replica_selector).</span><span class="sxs-lookup"><span data-stu-id="1c3e7-243">For further information, see [PartitionSelector and ReplicaSelector](#partition_replica_selector).</span></span>

```csharp
// Add a reference tooSystem.Fabric.Testability.dll and System.Fabric.dll
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Fabric.Testability;
using System.Fabric;
using System.Threading;
using System.Numerics;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");
        string nodeName = "N0040";
        BigInteger nodeInstanceId = 130743013389060139;

        Console.WriteLine("Starting RestartNode test");
        try
        {
            //Restart hello node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way toorestart node is by using nodeName and nodeInstanceId
            RestartNodeAsync(clusterConnection, nodeName, nodeInstanceId).Wait();
        }
        catch (AggregateException exAgg)
        {
            Console.WriteLine("RestartNode did not complete: ");
            foreach (Exception ex in exAgg.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("RestartNode completed.");
        return 0;
    }

    static async Task RestartNodeAsync(string clusterConnection, Uri serviceName)
    {
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);
        ReplicaSelector primaryofReplicaSelector = ReplicaSelector.PrimaryOf(randomPartitionSelector);

        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(primaryofReplicaSelector, CompletionMode.Verify);
    }

    static async Task RestartNodeAsync(string clusterConnection, string nodeName, BigInteger nodeInstanceId)
    {
        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(nodeName, nodeInstanceId, CompletionMode.Verify);
    }
}
```

## <a name="partitionselector-and-replicaselector"></a><span data-ttu-id="1c3e7-244">PartitionSelector ve ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="1c3e7-244">PartitionSelector and ReplicaSelector</span></span>
### <a name="partitionselector"></a><span data-ttu-id="1c3e7-245">PartitionSelector</span><span class="sxs-lookup"><span data-stu-id="1c3e7-245">PartitionSelector</span></span>
<span data-ttu-id="1c3e7-246">PartitionSelector Test Edilebilirlik kullanıma sunulan bir yardımcı olan ve olduğu kullanılan tooselect belirli bir bölüm üzerinde hangi tooperform hello Test Edilebilirlik eylemlerden herhangi birini.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-246">PartitionSelector is a helper exposed in testability and is used tooselect a specific partition on which tooperform any of hello testability actions.</span></span> <span data-ttu-id="1c3e7-247">Merhaba bölüm kimliği önceden biliniyorsa kullanılan tooselect belirli bir bölüm olabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-247">It can be used tooselect a specific partition if hello partition ID is known beforehand.</span></span> <span data-ttu-id="1c3e7-248">Veya, hello bölüm anahtarı sağlayabilir ve hello işlemi hello bölüm kimliği dahili olarak çözer.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-248">Or, you can provide hello partition key and hello operation will resolve hello partition ID internally.</span></span> <span data-ttu-id="1c3e7-249">Rastgele bir bölüm seçme hello seçeneğiniz de vardır.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-249">You also have hello option of selecting a random partition.</span></span>

<span data-ttu-id="1c3e7-250">toouse bu yardımcı hello PartitionSelector nesnesi oluşturun ve hello Select * yöntemlerden birini kullanarak hello bölümü seçin.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-250">toouse this helper, create hello PartitionSelector object and select hello partition by using one of hello Select* methods.</span></span> <span data-ttu-id="1c3e7-251">Daha sonra hello PartitionSelector nesne toohello gerektirdiği API geçirin.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-251">Then pass in hello PartitionSelector object toohello API that requires it.</span></span> <span data-ttu-id="1c3e7-252">Hiçbir seçeneği seçili değilse tooa rastgele bölümü varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-252">If no option is selected, it defaults tooa random partition.</span></span>

```csharp
Uri serviceName = new Uri("fabric:/samples/InMemoryToDoListApp/InMemoryToDoListService");
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
string partitionName = "Partition1";
Int64 partitionKeyUniformInt64 = 1;

// Select a random partition
PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

// Select a partition based on ID
PartitionSelector partitionSelectorById = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);

// Select a partition based on name
PartitionSelector namedPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionName);

// Select a partition based on partition key
PartitionSelector uniformIntPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionKeyUniformInt64);
```

### <a name="replicaselector"></a><span data-ttu-id="1c3e7-253">ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="1c3e7-253">ReplicaSelector</span></span>
<span data-ttu-id="1c3e7-254">ReplicaSelector Test Edilebilirlik kullanıma sunulan bir yardımcı olan ve kullanılan toohelp seçin hangi tooperform kopyada hello Test Edilebilirlik eylemlerden herhangi birini.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-254">ReplicaSelector is a helper exposed in testability and is used toohelp select a replica on which tooperform any of hello testability actions.</span></span> <span data-ttu-id="1c3e7-255">Merhaba çoğaltma kimliği önceden biliniyorsa kullanılan tooselect belirli bir çoğaltma olabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-255">It can be used tooselect a specific replica if hello replica ID is known beforehand.</span></span> <span data-ttu-id="1c3e7-256">Ayrıca, bir birincil çoğaltmayı veya rastgele ikincil seçme hello seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-256">In addition, you have hello option of selecting a primary replica or a random secondary.</span></span> <span data-ttu-id="1c3e7-257">ReplicaSelector PartitionSelector türetilen, yani tooselect gerekiyor her ikisi de tooperform hello Test Edilebilirlik işlemi istediğiniz çoğaltma ve hello bölüm hello.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-257">ReplicaSelector derives from PartitionSelector, so you need tooselect both hello replica and hello partition on which you wish tooperform hello testability operation.</span></span>

<span data-ttu-id="1c3e7-258">toouse bu yardımcı ReplicaSelector nesnesi oluşturun ve tooselect hello çoğaltma ve hello bölümü istediğiniz hello biçimde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-258">toouse this helper, create a ReplicaSelector object and set hello way you want tooselect hello replica and hello partition.</span></span> <span data-ttu-id="1c3e7-259">Ardından hello gerektirdiği API geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-259">You can then pass it into hello API that requires it.</span></span> <span data-ttu-id="1c3e7-260">Hiçbir seçeneği seçili değilse tooa rastgele çoğaltma ve rastgele bölümü varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="1c3e7-260">If no option is selected, it defaults tooa random replica and random partition.</span></span>

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select hello primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select hello replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a><span data-ttu-id="1c3e7-261">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1c3e7-261">Next steps</span></span>
* [<span data-ttu-id="1c3e7-262">Test Edilebilirlik senaryoları</span><span class="sxs-lookup"><span data-stu-id="1c3e7-262">Testability scenarios</span></span>](service-fabric-testability-scenarios.md)
* <span data-ttu-id="1c3e7-263">Nasıl tootest hizmetinizi</span><span class="sxs-lookup"><span data-stu-id="1c3e7-263">How tootest your service</span></span>
  * [<span data-ttu-id="1c3e7-264">Hataları sırasında hizmet iş yüklerinin benzetimi</span><span class="sxs-lookup"><span data-stu-id="1c3e7-264">Simulate failures during service workloads</span></span>](service-fabric-testability-workload-tests.md)
  * [<span data-ttu-id="1c3e7-265">Hizmetten hizmete iletişim hatası</span><span class="sxs-lookup"><span data-stu-id="1c3e7-265">Service-to-service communication failures</span></span>](service-fabric-testability-scenarios-service-communication.md)

