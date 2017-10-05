---
title: "Azure mikro hizmetleri için geliştirme ortamı ayarlama | Microsoft Docs"
description: "Çalışma zamanını, SDK'yı ve araçları yükleyip yerel bir geliştirme kümesi oluşturun. Bu kurulumu tamamladıktan sonra uygulama derlemek için hazır hale gelirsiniz."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b94e2d2e-435c-474a-ae34-4adecd0e6f8f
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/10/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: f0c6957217c21bdfd76498944e248fc808f2d271
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="prepare-your-development-environment"></a><span data-ttu-id="67b0f-104">Geliştirme ortamınızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="67b0f-104">Prepare your development environment</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="67b0f-105">Windows</span><span class="sxs-lookup"><span data-stu-id="67b0f-105">Windows</span></span>](service-fabric-get-started.md) 
> * [<span data-ttu-id="67b0f-106">Linux</span><span class="sxs-lookup"><span data-stu-id="67b0f-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="67b0f-107">OSX</span><span class="sxs-lookup"><span data-stu-id="67b0f-107">OSX</span></span>](service-fabric-get-started-mac.md)
> 
> 

 <span data-ttu-id="67b0f-108">Geliştirme makinenizde [Azure Service Fabric uygulamaları][1] derlemek ve çalıştırmak için çalışma zamanını, SDK'yı ve araçları yükleyin.</span><span class="sxs-lookup"><span data-stu-id="67b0f-108">To build and run [Azure Service Fabric applications][1] on your development machine, install the runtime, SDK, and tools.</span></span> <span data-ttu-id="67b0f-109">Ayrıca, SDK'da bulunan Windows PowerShell betiklerinin çalıştırılmasını da etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="67b0f-109">You also need to enable execution of the Windows PowerShell scripts included in the SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67b0f-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="67b0f-110">Prerequisites</span></span>
### <a name="supported-operating-system-versions"></a><span data-ttu-id="67b0f-111">Desteklenen işletim sistemi sürümleri</span><span class="sxs-lookup"><span data-stu-id="67b0f-111">Supported operating system versions</span></span>
<span data-ttu-id="67b0f-112">Geliştirme için şu işletim sistemi sürümleri desteklenir:</span><span class="sxs-lookup"><span data-stu-id="67b0f-112">The following operating system versions are supported for development:</span></span>

* <span data-ttu-id="67b0f-113">Windows 7</span><span class="sxs-lookup"><span data-stu-id="67b0f-113">Windows 7</span></span>
* <span data-ttu-id="67b0f-114">Windows 8/Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="67b0f-114">Windows 8/Windows 8.1</span></span>
* <span data-ttu-id="67b0f-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="67b0f-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="67b0f-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="67b0f-116">Windows Server 2016</span></span>
* <span data-ttu-id="67b0f-117">Windows 10</span><span class="sxs-lookup"><span data-stu-id="67b0f-117">Windows 10</span></span>

> [!NOTE]
> <span data-ttu-id="67b0f-118">Windows 7 varsayılan olarak yalnızca Windows PowerShell 2.0 içerir.</span><span class="sxs-lookup"><span data-stu-id="67b0f-118">Windows 7 only includes Windows PowerShell 2.0 by default.</span></span> <span data-ttu-id="67b0f-119">Service Fabric PowerShell cmdlet’leri PowerShell 3.0 veya üzerini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="67b0f-119">Service Fabric PowerShell cmdlets requires PowerShell 3.0 or higher.</span></span> <span data-ttu-id="67b0f-120">Microsoft Yükleme Merkezi'nden [Windows PowerShell 5.0'ı indirebilirsiniz][powershell5-download].</span><span class="sxs-lookup"><span data-stu-id="67b0f-120">You can [download Windows PowerShell 5.0][powershell5-download] from the Microsoft Download Center.</span></span>
> 
> 

## <a name="install-the-sdk-and-tools"></a><span data-ttu-id="67b0f-121">SDK'yı ve araçları yükleme</span><span class="sxs-lookup"><span data-stu-id="67b0f-121">Install the SDK and tools</span></span>
### <a name="to-use-visual-studio-2017"></a><span data-ttu-id="67b0f-122">Visual Studio 2017’yi kullanmak için</span><span class="sxs-lookup"><span data-stu-id="67b0f-122">To use Visual Studio 2017</span></span>
<span data-ttu-id="67b0f-123">Service Fabric Araçları, Visual Studio 2017’de Azure Geliştirme ve Yönetim iş yükünün parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="67b0f-123">Service Fabric Tools are part of the Azure Development and Management workload in Visual Studio 2017.</span></span> <span data-ttu-id="67b0f-124">Bu iş yükünü Visual Studio yüklemenizin bir parçası olarak etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="67b0f-124">Enable this workload as part of your Visual Studio installation.</span></span>
<span data-ttu-id="67b0f-125">Ayrıca Web Platformu Yükleyicisini kullanarak Microsoft Azure Service Fabric SDK'sını da yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="67b0f-125">In addition, you need to install the Microsoft Azure Service Fabric SDK, using Web Platform Installer.</span></span>

* <span data-ttu-id="67b0f-126">[Microsoft Azure Service Fabric SDK'sını yükleyin][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="67b0f-126">[Install the Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

### <a name="to-use-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a><span data-ttu-id="67b0f-127">Visual Studio 2015'i kullanmak için (Visual Studio 2015 Güncelleştirme 2 veya üzeri gerekir)</span><span class="sxs-lookup"><span data-stu-id="67b0f-127">To use Visual Studio 2015 (requires Visual Studio 2015 Update 2 or later)</span></span>
<span data-ttu-id="67b0f-128">Visual Studio 2015 için Service Fabric araçları Web Platformu Yükleyicisi kullanılarak SDK ile birlikte yüklenir:</span><span class="sxs-lookup"><span data-stu-id="67b0f-128">For Visual Studio 2015, Service Fabric tools are installed together with the SDK, using the Web Platform Installer:</span></span>

* <span data-ttu-id="67b0f-129">[Microsoft Azure Service Fabric SDK’sını ve Araçları yükleyin][full-bundle-vs2015]</span><span class="sxs-lookup"><span data-stu-id="67b0f-129">[Install the Microsoft Azure Service Fabric SDK and Tools][full-bundle-vs2015]</span></span>

### <a name="sdk-installation-only"></a><span data-ttu-id="67b0f-130">Yalnızca SDK'yı yükleme</span><span class="sxs-lookup"><span data-stu-id="67b0f-130">SDK installation only</span></span>
<span data-ttu-id="67b0f-131">Yalnızca SDK'yı yüklemeniz gerekiyorsa bu paketi yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="67b0f-131">If you only need the SDK, you can install this package:</span></span>
* <span data-ttu-id="67b0f-132">[Microsoft Azure Service Fabric SDK'sını yükleyin][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="67b0f-132">[Install the Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

<span data-ttu-id="67b0f-133">Geçerli sürümler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="67b0f-133">The current versions are:</span></span>
* <span data-ttu-id="67b0f-134">Service Fabric SDK 2.7.198</span><span class="sxs-lookup"><span data-stu-id="67b0f-134">Service Fabric SDK 2.7.198</span></span>
* <span data-ttu-id="67b0f-135">Service Fabric çalışma zamanı 5.7.198</span><span class="sxs-lookup"><span data-stu-id="67b0f-135">Service Fabric runtime 5.7.198</span></span>
* <span data-ttu-id="67b0f-136">Visual Studio 2015 1.7.50721 için Service Fabric Araçları</span><span class="sxs-lookup"><span data-stu-id="67b0f-136">Service Fabric Tools for Visual Studio 2015 1.7.50721</span></span>
* <span data-ttu-id="67b0f-137">Visual Studio 2017 Güncelleştirme 2, Visual Studio 1.6.20170504 için Service Fabric Araçlarını içerir</span><span class="sxs-lookup"><span data-stu-id="67b0f-137">Visual Studio 2017 Update 2 includes Service Fabric Tools for Visual Studio 1.6.20170504</span></span>
* <span data-ttu-id="67b0f-138">Visual Studio 2017 Güncelleştirme 3 Önizleme 7, (15.3.0 Önizleme 7.0) Visual Studio 1.7.20170721 için Service Fabric Araçlarını içerir</span><span class="sxs-lookup"><span data-stu-id="67b0f-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) includes Service Fabric Tools for Visual Studio 1.7.20170721</span></span>

<span data-ttu-id="67b0f-139">Desteklenen sürümlerin listesi için bkz. [Service Fabric desteği](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="67b0f-139">For a list of supported versions, see [Service Fabric support](service-fabric-support.md)</span></span>

## <a name="enable-powershell-script-execution"></a><span data-ttu-id="67b0f-140">PowerShell betik yürütmesini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="67b0f-140">Enable PowerShell script execution</span></span>
<span data-ttu-id="67b0f-141">Service Fabric, yerel geliştirme merkezi oluşturmak ve Visual Studio'dan uygulamaları dağıtmak için Windows PowerShell betiklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="67b0f-141">Service Fabric uses Windows PowerShell scripts for creating a local development cluster and for deploying applications from Visual Studio.</span></span> <span data-ttu-id="67b0f-142">Varsayılan olarak, Windows bu betiklerin çalışmasını engeller.</span><span class="sxs-lookup"><span data-stu-id="67b0f-142">By default, Windows blocks these scripts from running.</span></span> <span data-ttu-id="67b0f-143">Betikleri etkinleştirmek için PowerShell yürütme ilkenizi değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="67b0f-143">To enable them, you must modify your PowerShell execution policy.</span></span> <span data-ttu-id="67b0f-144">PowerShell'i yönetici olarak açın ve şu komutu girin:</span><span class="sxs-lookup"><span data-stu-id="67b0f-144">Open PowerShell as an administrator and enter the following command:</span></span>

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a><span data-ttu-id="67b0f-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="67b0f-145">Next steps</span></span>
<span data-ttu-id="67b0f-146">Artık geliştirme ortamınızı ayarlamayı tamamladığınıza göre, uygulama derlemeye ve çalıştırmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="67b0f-146">Now that you've finished setting up your development environment, start building and running apps.</span></span>

* [<span data-ttu-id="67b0f-147">Visual Studio'da ilk Service Fabric uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="67b0f-147">Create your first Service Fabric application in Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
* [<span data-ttu-id="67b0f-148">Yerel kümenizde uygulamaları dağıtmayı ve yönetmeyi öğrenin</span><span class="sxs-lookup"><span data-stu-id="67b0f-148">Learn how to deploy and manage applications on your local cluster</span></span>](service-fabric-get-started-with-a-local-cluster.md)
* [<span data-ttu-id="67b0f-149">Programlama modelleri hakkında bilgi edinin: Reliable Services ve Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="67b0f-149">Learn about the programming models: Reliable Services and Reliable Actors</span></span>](service-fabric-choose-framework.md)
* [<span data-ttu-id="67b0f-150">GitHub'da Service Fabric kod örneklerine bakın</span><span class="sxs-lookup"><span data-stu-id="67b0f-150">Check out the Service Fabric code samples on GitHub</span></span>](https://aka.ms/servicefabricsamples)
* [<span data-ttu-id="67b0f-151">Service Fabric Explorer kullanarak kümenizi görselleştirme</span><span class="sxs-lookup"><span data-stu-id="67b0f-151">Visualize your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)
* [<span data-ttu-id="67b0f-152">Platforma yönelik daha geniş kapsamlı bilgi edinmek için Service Fabric öğrenme yolunu uygulayın</span><span class="sxs-lookup"><span data-stu-id="67b0f-152">Follow the Service Fabric learning path to get a broad introduction to the platform</span></span>](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* <span data-ttu-id="67b0f-153">[Service Fabric destek seçenekleri](service-fabric-support.md) hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="67b0f-153">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>

<span data-ttu-id="67b0f-154">[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Service Fabric kampanya sayfası"</span><span class="sxs-lookup"><span data-stu-id="67b0f-154">[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Service Fabric campaign page"</span></span>
<span data-ttu-id="67b0f-155">[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"</span><span class="sxs-lookup"><span data-stu-id="67b0f-155">[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"</span></span>
<span data-ttu-id="67b0f-156">[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI bağlantısı"</span><span class="sxs-lookup"><span data-stu-id="67b0f-156">[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI link"</span></span>
<span data-ttu-id="67b0f-157">[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI bağlantısı"</span><span class="sxs-lookup"><span data-stu-id="67b0f-157">[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI link"</span></span>
<span data-ttu-id="67b0f-158">[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI bağlantısı"</span><span class="sxs-lookup"><span data-stu-id="67b0f-158">[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI link"</span></span>
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
