---
title: "aaaTroubleshoot, yerel Service Fabric kümesi Kurulumu | Microsoft Docs"
description: "Bu makalede, yerel geliştirme kümeniz sorun giderme önerileri bir dizi kapsar"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 97f4feaa-bba0-47af-8fdd-07f811fe2202
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: ce36f62a4bc69d2cd5b6c3df4abda6ca88fa84f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a><span data-ttu-id="0edf8-103">Yerel geliştirme Küme kurulumu sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="0edf8-103">Troubleshoot your local development cluster setup</span></span>
<span data-ttu-id="0edf8-104">Yerel Azure Service Fabric geliştirme kümenizle etkileşim sırasında bir sorun çalıştırırsanız, olası çözümler için öneriler aşağıdaki hello gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="0edf8-104">If you run into an issue while interacting with your local Azure Service Fabric development cluster, review hello following suggestions for potential solutions.</span></span>

## <a name="cluster-setup-failures"></a><span data-ttu-id="0edf8-105">Küme kurulumu hataları</span><span class="sxs-lookup"><span data-stu-id="0edf8-105">Cluster setup failures</span></span>
### <a name="cannot-clean-up-service-fabric-logs"></a><span data-ttu-id="0edf8-106">Service Fabric günlüklerini temizleyemiyor</span><span class="sxs-lookup"><span data-stu-id="0edf8-106">Cannot clean up Service Fabric logs</span></span>
#### <a name="problem"></a><span data-ttu-id="0edf8-107">Sorun</span><span class="sxs-lookup"><span data-stu-id="0edf8-107">Problem</span></span>
<span data-ttu-id="0edf8-108">Merhaba DevClusterSetup komut dosyası çalıştırılırken, bu gibi bir hata görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="0edf8-108">While running hello DevClusterSetup script, you see an error like this:</span></span>

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held tooitems in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a><span data-ttu-id="0edf8-109">Çözüm</span><span class="sxs-lookup"><span data-stu-id="0edf8-109">Solution</span></span>
<span data-ttu-id="0edf8-110">Geçerli PowerShell penceresinde hello kapatıp yönetici olarak yeni bir PowerShell penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="0edf8-110">Close hello current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="0edf8-111">Artık hello komut dosyasını çalıştırmak mümkün toosuccessfully olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0edf8-111">You should now be able toosuccessfully run hello script.</span></span>

## <a name="cluster-connection-failures"></a><span data-ttu-id="0edf8-112">Küme bağlantı hataları</span><span class="sxs-lookup"><span data-stu-id="0edf8-112">Cluster connection failures</span></span>
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a><span data-ttu-id="0edf8-113">Service Fabric PowerShell cmdlet'leri Azure PowerShell'de tanınmıyor.</span><span class="sxs-lookup"><span data-stu-id="0edf8-113">Service Fabric PowerShell cmdlets are not recognized in Azure PowerShell</span></span>
#### <a name="problem"></a><span data-ttu-id="0edf8-114">Sorun</span><span class="sxs-lookup"><span data-stu-id="0edf8-114">Problem</span></span>
<span data-ttu-id="0edf8-115">Toorun herhangi birini hello Service Fabric PowerShell cmdlet'leri gibi deneyin, `Connect-ServiceFabricCluster` bir Azure PowerShell penceresinde, o hello cmdlet tanınmıyor belirten başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="0edf8-115">If you try toorun any of hello Service Fabric PowerShell cmdlets, such as `Connect-ServiceFabricCluster` in an Azure PowerShell window, it fails, saying that hello cmdlet is not recognized.</span></span> <span data-ttu-id="0edf8-116">Merhaba Service Fabric cmdlet'leri yalnızca çalışır ancak 64-bit ortamlarda hello neden Azure PowerShell hello 32 bit sürümünde Windows PowerShell (hatta 64-bit işletim sistemi sürümleri), kullanmasıdır.</span><span class="sxs-lookup"><span data-stu-id="0edf8-116">hello reason for this is that Azure PowerShell uses hello 32-bit version of Windows PowerShell (even on 64-bit OS versions), whereas hello Service Fabric cmdlets only work in 64-bit environments.</span></span>

#### <a name="solution"></a><span data-ttu-id="0edf8-117">Çözüm</span><span class="sxs-lookup"><span data-stu-id="0edf8-117">Solution</span></span>
<span data-ttu-id="0edf8-118">Her zaman Windows Powershell'den doğrudan Service Fabric cmdlet'lerini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0edf8-118">Always run Service Fabric cmdlets directly from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="0edf8-119">Bu artık gerçekleşmesi gereken şekilde hello Azure PowerShell'in en son sürümünü özel bir kısayol oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="0edf8-119">hello latest version of Azure PowerShell does not create a special shortcut, so this should no longer occur.</span></span>
> 
> 

### <a name="type-initialization-exception"></a><span data-ttu-id="0edf8-120">Tür başlatma özel durumu oluştu</span><span class="sxs-lookup"><span data-stu-id="0edf8-120">Type Initialization exception</span></span>
#### <a name="problem"></a><span data-ttu-id="0edf8-121">Sorun</span><span class="sxs-lookup"><span data-stu-id="0edf8-121">Problem</span></span>
<span data-ttu-id="0edf8-122">PowerShell toohello kümeye bağlanırken hello hata Typeınitializationexception System.Fabric.Common.AppTrace için bkz.</span><span class="sxs-lookup"><span data-stu-id="0edf8-122">When you are connecting toohello cluster in PowerShell, you see hello error TypeInitializationException for System.Fabric.Common.AppTrace.</span></span>

#### <a name="solution"></a><span data-ttu-id="0edf8-123">Çözüm</span><span class="sxs-lookup"><span data-stu-id="0edf8-123">Solution</span></span>
<span data-ttu-id="0edf8-124">Path değişkeni yükleme sırasında düzgün ayarlanmadı.</span><span class="sxs-lookup"><span data-stu-id="0edf8-124">Your path variable was not correctly set during installation.</span></span> <span data-ttu-id="0edf8-125">Windows oturumunu kapatmanız ve yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="0edf8-125">Sign out of Windows and sign back in.</span></span> <span data-ttu-id="0edf8-126">Bu yolunuzu yeniler.</span><span class="sxs-lookup"><span data-stu-id="0edf8-126">This refreshes your path.</span></span>

### <a name="cluster-connection-fails-with-object-is-closed"></a><span data-ttu-id="0edf8-127">"Nesnesi kapalı" Küme bağlantı başarısız</span><span class="sxs-lookup"><span data-stu-id="0edf8-127">Cluster connection fails with "Object is closed"</span></span>
#### <a name="problem"></a><span data-ttu-id="0edf8-128">Sorun</span><span class="sxs-lookup"><span data-stu-id="0edf8-128">Problem</span></span>
<span data-ttu-id="0edf8-129">Bir arama tooConnect-ServiceFabricCluster şuna benzer bir hata ile başarısız olur:</span><span class="sxs-lookup"><span data-stu-id="0edf8-129">A call tooConnect-ServiceFabricCluster fails with an error like this:</span></span>

    Connect-ServiceFabricCluster : hello object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a><span data-ttu-id="0edf8-130">Çözüm</span><span class="sxs-lookup"><span data-stu-id="0edf8-130">Solution</span></span>
<span data-ttu-id="0edf8-131">Geçerli PowerShell penceresinde hello kapatıp yönetici olarak yeni bir PowerShell penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="0edf8-131">Close hello current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="0edf8-132">Şimdi görüntüleyebiliyor olmalısınız toosuccessfully bağlanın.</span><span class="sxs-lookup"><span data-stu-id="0edf8-132">You should now be able toosuccessfully connect.</span></span>

### <a name="fabric-connection-denied-exception"></a><span data-ttu-id="0edf8-133">Doku bağlantı reddedildi özel durumu</span><span class="sxs-lookup"><span data-stu-id="0edf8-133">Fabric Connection Denied exception</span></span>
#### <a name="problem"></a><span data-ttu-id="0edf8-134">Sorun</span><span class="sxs-lookup"><span data-stu-id="0edf8-134">Problem</span></span>
<span data-ttu-id="0edf8-135">Visual Studio'da hata ayıklama sırasında bir FabricConnectionDeniedException hatası alırsınız.</span><span class="sxs-lookup"><span data-stu-id="0edf8-135">When debugging from Visual Studio, you get a FabricConnectionDeniedException error.</span></span>

#### <a name="solution"></a><span data-ttu-id="0edf8-136">Çözüm</span><span class="sxs-lookup"><span data-stu-id="0edf8-136">Solution</span></span>
<span data-ttu-id="0edf8-137">Bu hata genellikle, toostart hizmeti ana bilgisayar işlemi el ile Merhaba Service Fabric çalışma zamanı toostart izin vermek yerine çalıştığınızda oluşur, sizin için.</span><span class="sxs-lookup"><span data-stu-id="0edf8-137">This error usually occurs when you try toostart a service host process manually, rather than allowing hello Service Fabric runtime toostart it for you.</span></span>

<span data-ttu-id="0edf8-138">Çözümünüzdeki başlangıç projesi olarak ayarla tüm hizmet projeleri yok emin olun.</span><span class="sxs-lookup"><span data-stu-id="0edf8-138">Ensure that you do not have any service projects set as startup projects in your solution.</span></span> <span data-ttu-id="0edf8-139">Yalnızca Service Fabric uygulaması projeleri başlangıç projesi ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0edf8-139">Only Service Fabric application projects should be set as startup projects.</span></span>

> [!TIP]
> <span data-ttu-id="0edf8-140">Kurulum aşağıdaki olduğunda yerel kümenizdeki toobehave aşırı başlar, hello yerel Küme Yöneticisi sistemi Tepsisi uygulaması kullanarak sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0edf8-140">If, following setup, your local cluster begins toobehave abnormally, you can reset it using hello local cluster manager system tray application.</span></span> <span data-ttu-id="0edf8-141">Bu kaldırır, mevcut küme hello ve yeni bir tane kurun.</span><span class="sxs-lookup"><span data-stu-id="0edf8-141">This removes hello existing cluster and set up a new one.</span></span> <span data-ttu-id="0edf8-142">Tüm dağıtılan uygulamaları ve ilişkili veriler kaldırılır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0edf8-142">Note that all deployed applications and associated data is removed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0edf8-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0edf8-143">Next steps</span></span>
* [<span data-ttu-id="0edf8-144">Anlama ve sistem durumu raporlarını kümenizle sorun giderme</span><span class="sxs-lookup"><span data-stu-id="0edf8-144">Understand and troubleshoot your cluster with system health reports</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="0edf8-145">Service Fabric Explorer ile kümenizi görselleştirme</span><span class="sxs-lookup"><span data-stu-id="0edf8-145">Visualize your cluster with Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

