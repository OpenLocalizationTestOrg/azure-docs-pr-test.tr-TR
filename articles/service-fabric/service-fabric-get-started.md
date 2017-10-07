---
title: "Azure mikro hizmetler için bir geliştirme ortamı kurma aaaSet | Microsoft Docs"
description: "Merhaba çalışma zamanı, SDK ve araçları yükleyip yerel bir geliştirme kümesi oluşturun. Bu kurulumu tamamladıktan sonra hazır toobuild uygulamalar olur."
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
ms.openlocfilehash: 9b0442778999d4c3d2b99adb98f6596dcbdc36d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment"></a><span data-ttu-id="597ad-104">Geliştirme ortamınızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="597ad-104">Prepare your development environment</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="597ad-105">Windows</span><span class="sxs-lookup"><span data-stu-id="597ad-105">Windows</span></span>](service-fabric-get-started.md) 
> * [<span data-ttu-id="597ad-106">Linux</span><span class="sxs-lookup"><span data-stu-id="597ad-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="597ad-107">OSX</span><span class="sxs-lookup"><span data-stu-id="597ad-107">OSX</span></span>](service-fabric-get-started-mac.md)
> 
> 

 <span data-ttu-id="597ad-108">toobuild çalıştırıp [Azure Service Fabric uygulamaları] [ 1] geliştirme makinenizde hello çalışma zamanı, SDK'yı ve araçları yükleyin.</span><span class="sxs-lookup"><span data-stu-id="597ad-108">toobuild and run [Azure Service Fabric applications][1] on your development machine, install hello runtime, SDK, and tools.</span></span> <span data-ttu-id="597ad-109">Ayrıca tooenable hello SDK dahil hello Windows PowerShell betiklerinin yürütülmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="597ad-109">You also need tooenable execution of hello Windows PowerShell scripts included in hello SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="597ad-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="597ad-110">Prerequisites</span></span>
### <a name="supported-operating-system-versions"></a><span data-ttu-id="597ad-111">Desteklenen işletim sistemi sürümleri</span><span class="sxs-lookup"><span data-stu-id="597ad-111">Supported operating system versions</span></span>
<span data-ttu-id="597ad-112">işletim sistemi sürümleri aşağıdaki hello geliştirme için desteklenir:</span><span class="sxs-lookup"><span data-stu-id="597ad-112">hello following operating system versions are supported for development:</span></span>

* <span data-ttu-id="597ad-113">Windows 7</span><span class="sxs-lookup"><span data-stu-id="597ad-113">Windows 7</span></span>
* <span data-ttu-id="597ad-114">Windows 8/Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="597ad-114">Windows 8/Windows 8.1</span></span>
* <span data-ttu-id="597ad-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="597ad-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="597ad-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="597ad-116">Windows Server 2016</span></span>
* <span data-ttu-id="597ad-117">Windows 10</span><span class="sxs-lookup"><span data-stu-id="597ad-117">Windows 10</span></span>

> [!NOTE]
> <span data-ttu-id="597ad-118">Windows 7 varsayılan olarak yalnızca Windows PowerShell 2.0 içerir.</span><span class="sxs-lookup"><span data-stu-id="597ad-118">Windows 7 only includes Windows PowerShell 2.0 by default.</span></span> <span data-ttu-id="597ad-119">Service Fabric PowerShell cmdlet’leri PowerShell 3.0 veya üzerini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="597ad-119">Service Fabric PowerShell cmdlets requires PowerShell 3.0 or higher.</span></span> <span data-ttu-id="597ad-120">Yapabilecekleriniz [Windows PowerShell 5.0 indirme] [ powershell5-download] hello Microsoft Download Center gelen.</span><span class="sxs-lookup"><span data-stu-id="597ad-120">You can [download Windows PowerShell 5.0][powershell5-download] from hello Microsoft Download Center.</span></span>
> 
> 

## <a name="install-hello-sdk-and-tools"></a><span data-ttu-id="597ad-121">Merhaba SDK ve araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="597ad-121">Install hello SDK and tools</span></span>
### <a name="toouse-visual-studio-2017"></a><span data-ttu-id="597ad-122">Visual Studio 2017 toouse</span><span class="sxs-lookup"><span data-stu-id="597ad-122">toouse Visual Studio 2017</span></span>
<span data-ttu-id="597ad-123">Service Fabric araçları hello Azure geliştirme ve yönetim iş yükünü Visual Studio 2017'ın bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="597ad-123">Service Fabric Tools are part of hello Azure Development and Management workload in Visual Studio 2017.</span></span> <span data-ttu-id="597ad-124">Bu iş yükünü Visual Studio yüklemenizin bir parçası olarak etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="597ad-124">Enable this workload as part of your Visual Studio installation.</span></span>
<span data-ttu-id="597ad-125">Ayrıca, Microsoft Azure Service Fabric Web Platformu Yükleyicisi'ni kullanarak SDK, tooinstall hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="597ad-125">In addition, you need tooinstall hello Microsoft Azure Service Fabric SDK, using Web Platform Installer.</span></span>

* <span data-ttu-id="597ad-126">[Merhaba Microsoft Azure Service Fabric SDK yükleme][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="597ad-126">[Install hello Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

### <a name="toouse-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a><span data-ttu-id="597ad-127">Visual Studio 2015 toouse (Visual Studio 2015 güncelleştirme 2 veya sonrasını gerektirir)</span><span class="sxs-lookup"><span data-stu-id="597ad-127">toouse Visual Studio 2015 (requires Visual Studio 2015 Update 2 or later)</span></span>
<span data-ttu-id="597ad-128">Visual Studio 2015 için Service Fabric araçları hello hello Web Platformu yükleyicisi kullanılarak SDK ile birlikte yüklenir:</span><span class="sxs-lookup"><span data-stu-id="597ad-128">For Visual Studio 2015, Service Fabric tools are installed together with hello SDK, using hello Web Platform Installer:</span></span>

* <span data-ttu-id="597ad-129">[Merhaba Microsoft Azure Service Fabric SDK ve araçlarını yükleme][full-bundle-vs2015]</span><span class="sxs-lookup"><span data-stu-id="597ad-129">[Install hello Microsoft Azure Service Fabric SDK and Tools][full-bundle-vs2015]</span></span>

### <a name="sdk-installation-only"></a><span data-ttu-id="597ad-130">Yalnızca SDK'yı yükleme</span><span class="sxs-lookup"><span data-stu-id="597ad-130">SDK installation only</span></span>
<span data-ttu-id="597ad-131">Merhaba SDK yalnızca gereksiniminiz varsa, bu paketi yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="597ad-131">If you only need hello SDK, you can install this package:</span></span>
* <span data-ttu-id="597ad-132">[Merhaba Microsoft Azure Service Fabric SDK yükleme][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="597ad-132">[Install hello Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

<span data-ttu-id="597ad-133">Merhaba geçerli sürümleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="597ad-133">hello current versions are:</span></span>
* <span data-ttu-id="597ad-134">Service Fabric SDK 2.7.198</span><span class="sxs-lookup"><span data-stu-id="597ad-134">Service Fabric SDK 2.7.198</span></span>
* <span data-ttu-id="597ad-135">Service Fabric çalışma zamanı 5.7.198</span><span class="sxs-lookup"><span data-stu-id="597ad-135">Service Fabric runtime 5.7.198</span></span>
* <span data-ttu-id="597ad-136">Visual Studio 2015 1.7.50721 için Service Fabric Araçları</span><span class="sxs-lookup"><span data-stu-id="597ad-136">Service Fabric Tools for Visual Studio 2015 1.7.50721</span></span>
* <span data-ttu-id="597ad-137">Visual Studio 2017 Güncelleştirme 2, Visual Studio 1.6.20170504 için Service Fabric Araçlarını içerir</span><span class="sxs-lookup"><span data-stu-id="597ad-137">Visual Studio 2017 Update 2 includes Service Fabric Tools for Visual Studio 1.6.20170504</span></span>
* <span data-ttu-id="597ad-138">Visual Studio 2017 Güncelleştirme 3 Önizleme 7, (15.3.0 Önizleme 7.0) Visual Studio 1.7.20170721 için Service Fabric Araçlarını içerir</span><span class="sxs-lookup"><span data-stu-id="597ad-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) includes Service Fabric Tools for Visual Studio 1.7.20170721</span></span>

<span data-ttu-id="597ad-139">Desteklenen sürümlerin listesi için bkz. [Service Fabric desteği](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="597ad-139">For a list of supported versions, see [Service Fabric support](service-fabric-support.md)</span></span>

## <a name="enable-powershell-script-execution"></a><span data-ttu-id="597ad-140">PowerShell betik yürütmesini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="597ad-140">Enable PowerShell script execution</span></span>
<span data-ttu-id="597ad-141">Service Fabric, yerel geliştirme merkezi oluşturmak ve Visual Studio'dan uygulamaları dağıtmak için Windows PowerShell betiklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="597ad-141">Service Fabric uses Windows PowerShell scripts for creating a local development cluster and for deploying applications from Visual Studio.</span></span> <span data-ttu-id="597ad-142">Varsayılan olarak, Windows bu betiklerin çalışmasını engeller.</span><span class="sxs-lookup"><span data-stu-id="597ad-142">By default, Windows blocks these scripts from running.</span></span> <span data-ttu-id="597ad-143">tooenable bunları, PowerShell yürütme ilkenizi değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="597ad-143">tooenable them, you must modify your PowerShell execution policy.</span></span> <span data-ttu-id="597ad-144">Bir yönetici olarak PowerShell'i açın ve hello aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="597ad-144">Open PowerShell as an administrator and enter hello following command:</span></span>

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a><span data-ttu-id="597ad-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="597ad-145">Next steps</span></span>
<span data-ttu-id="597ad-146">Artık geliştirme ortamınızı ayarlamayı tamamladığınıza göre, uygulama derlemeye ve çalıştırmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="597ad-146">Now that you've finished setting up your development environment, start building and running apps.</span></span>

* [<span data-ttu-id="597ad-147">Visual Studio'da ilk Service Fabric uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="597ad-147">Create your first Service Fabric application in Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
* [<span data-ttu-id="597ad-148">Bilgi nasıl toodeploy ve yerel kümenizdeki uygulamaları yönetme</span><span class="sxs-lookup"><span data-stu-id="597ad-148">Learn how toodeploy and manage applications on your local cluster</span></span>](service-fabric-get-started-with-a-local-cluster.md)
* [<span data-ttu-id="597ad-149">Programlama modelleri hello hakkında bilgi edinin: Reliable Services ve Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="597ad-149">Learn about hello programming models: Reliable Services and Reliable Actors</span></span>](service-fabric-choose-framework.md)
* [<span data-ttu-id="597ad-150">Service Fabric Hello github'daki kod örnekleri denetleyin</span><span class="sxs-lookup"><span data-stu-id="597ad-150">Check out hello Service Fabric code samples on GitHub</span></span>](https://aka.ms/servicefabricsamples)
* [<span data-ttu-id="597ad-151">Service Fabric Explorer kullanarak kümenizi görselleştirme</span><span class="sxs-lookup"><span data-stu-id="597ad-151">Visualize your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)
* [<span data-ttu-id="597ad-152">Merhaba Service Fabric yolu tooget geniş kapsamlı bilgi toohello platform öğrenme izleyin</span><span class="sxs-lookup"><span data-stu-id="597ad-152">Follow hello Service Fabric learning path tooget a broad introduction toohello platform</span></span>](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* <span data-ttu-id="597ad-153">[Service Fabric destek seçenekleri](service-fabric-support.md) hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="597ad-153">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Service Fabric kampanya sayfası"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI bağlantısı"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI bağlantısı"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI bağlantısı"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
