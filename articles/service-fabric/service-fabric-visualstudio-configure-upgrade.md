---
title: "Service Fabric uygulaması aaaConfigure hello yükseltme | Microsoft Docs"
description: "Nasıl tooconfigure hello ayarları Microsoft Visual Studio kullanarak bir Service Fabric uygulama yükseltme için bilgi edinin."
services: service-fabric
documentationcenter: na
author: mikkelhegn
manager: mfussell
editor: tglee
ms.assetid: 1757ba85-0b7b-4f16-8a23-2ddaa61c86c6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/29/2017
ms.author: mikkelhegn
ms.openlocfilehash: 8ca50aa9d911f3c98f017490c8fe29011e8d80cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-upgrade-of-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="85be9-103">Visual Studio'da bir Service Fabric uygulaması Hello yükseltmesini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="85be9-103">Configure hello upgrade of a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="85be9-104">Azure Service Fabric için Visual Studio Araçları toolocal veya uzak bir küme yayımlamak için yükseltme desteği sağlar.</span><span class="sxs-lookup"><span data-stu-id="85be9-104">Visual Studio tools for Azure Service Fabric provide upgrade support for publishing toolocal or remote clusters.</span></span> <span data-ttu-id="85be9-105">Test ve hata ayıklama sırasında Merhaba uygulaması değiştirme yerine, uygulama tooa daha yeni sürümü tooupgrade istediğiniz üç senaryo vardır:</span><span class="sxs-lookup"><span data-stu-id="85be9-105">There are three scenarios in which you want tooupgrade your application tooa newer version instead of replacing hello application during testing and debugging:</span></span>

* <span data-ttu-id="85be9-106">Uygulama verileri hello yükseltme sırasında kaybı olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="85be9-106">Application data won't be lost during hello upgrade.</span></span>
* <span data-ttu-id="85be9-107">Olmayacak şekilde hello yükseltme sırasında herhangi bir hizmet kesintisi yükseltme etki alanları arasında yeterli hizmet örnekleri yaymak ise yüksek kullanılabilirlik kalır.</span><span class="sxs-lookup"><span data-stu-id="85be9-107">Availability remains high so there won't be any service interruption during hello upgrade, if there are enough service instances spread across upgrade domains.</span></span>
* <span data-ttu-id="85be9-108">Bunu yükseltilirken testleri bir uygulamaya karşı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85be9-108">Tests can be run against an application while it's being upgraded.</span></span>

## <a name="parameters-needed-tooupgrade"></a><span data-ttu-id="85be9-109">Parametreler tooupgrade gerekli</span><span class="sxs-lookup"><span data-stu-id="85be9-109">Parameters needed tooupgrade</span></span>
<span data-ttu-id="85be9-110">İki dağıtım türlerinden birini seçebilirsiniz: normal veya yükseltme.</span><span class="sxs-lookup"><span data-stu-id="85be9-110">You can choose from two types of deployment: regular or upgrade.</span></span> <span data-ttu-id="85be9-111">Bir yükseltme dağıtımı, korur ancak normal dağıtım tüm önceki dağıtım bilgileri ve verileri hello kümede siler.</span><span class="sxs-lookup"><span data-stu-id="85be9-111">A regular deployment erases any previous deployment information and data on hello cluster, while an upgrade deployment preserves it.</span></span> <span data-ttu-id="85be9-112">Visual Studio'da bir Service Fabric uygulaması yükselttiğinizde tooprovide uygulama yükseltme parametreleri ve sistem durumu denetimi ilkeleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="85be9-112">When you upgrade a Service Fabric application in Visual Studio, you need tooprovide application upgrade parameters and health check policies.</span></span> <span data-ttu-id="85be9-113">Uygulama yükseltme parametreleri Yardım sistem durumu denetimi ilkeleri hello yükseltme başarılı olup olmadığını belirlenirken hello yükseltme denetler.</span><span class="sxs-lookup"><span data-stu-id="85be9-113">Application upgrade parameters help control hello upgrade, while health check policies determine whether hello upgrade was successful.</span></span> <span data-ttu-id="85be9-114">Bkz: [Service Fabric uygulama yükseltme: yükseltme parametreleri](service-fabric-application-upgrade-parameters.md) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="85be9-114">See [Service Fabric application upgrade: upgrade parameters](service-fabric-application-upgrade-parameters.md) for more details.</span></span>

<span data-ttu-id="85be9-115">Üç yükseltme modu vardır: *izlenen*, *UnmonitoredAuto*, ve *UnmonitoredManual*.</span><span class="sxs-lookup"><span data-stu-id="85be9-115">There are three upgrade modes: *Monitored*, *UnmonitoredAuto*, and *UnmonitoredManual*.</span></span>

* <span data-ttu-id="85be9-116">İzlenen yükseltme hello yükseltme ve uygulama otomatikleştirir sistem durumu denetimi.</span><span class="sxs-lookup"><span data-stu-id="85be9-116">A Monitored upgrade automates hello upgrade and application health check.</span></span>
* <span data-ttu-id="85be9-117">Hello yükseltme UnmonitoredAuto yükseltme otomatik hale getirir, ancak uygulama sistem durumu denetimi atlar hello.</span><span class="sxs-lookup"><span data-stu-id="85be9-117">An UnmonitoredAuto upgrade automates hello upgrade, but skips hello application health check.</span></span>
* <span data-ttu-id="85be9-118">UnmonitoredManual yükseltme yaptığınızda, toomanually gereken her bir yükseltme etki alanı yükseltme.</span><span class="sxs-lookup"><span data-stu-id="85be9-118">When you do an UnmonitoredManual upgrade, you need toomanually upgrade each upgrade domain.</span></span>

<span data-ttu-id="85be9-119">Her yükseltme modu parametreleri farklı kümelerini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="85be9-119">Each upgrade mode requires different sets of parameters.</span></span> <span data-ttu-id="85be9-120">Bkz: [uygulama yükseltme parametreleri](service-fabric-application-upgrade-parameters.md) toolearn hello kullanılabilir yükseltme seçenekleri hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="85be9-120">See [Application upgrade parameters](service-fabric-application-upgrade-parameters.md) toolearn more about hello available upgrade options.</span></span>

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="85be9-121">Visual Studio'da bir Service Fabric uygulama yükseltme</span><span class="sxs-lookup"><span data-stu-id="85be9-121">Upgrade a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="85be9-122">Merhaba Visual Studio Service Fabric araçları tooupgrade Service Fabric uygulaması kullanıyorsanız, yayımlama işlemi toobe normal dağıtım yerine yükseltme hello denetleyerek belirtebilirsiniz **yükseltme Merhaba uygulaması** denetleyin bir kutu.</span><span class="sxs-lookup"><span data-stu-id="85be9-122">If you’re using hello Visual Studio Service Fabric tools tooupgrade a Service Fabric application, you can specify a publish process toobe an upgrade rather than a regular deployment by checking hello **Upgrade hello application** check box.</span></span>

### <a name="tooconfigure-hello-upgrade-parameters"></a><span data-ttu-id="85be9-123">tooconfigure hello yükseltme parametreleri</span><span class="sxs-lookup"><span data-stu-id="85be9-123">tooconfigure hello upgrade parameters</span></span>
1. <span data-ttu-id="85be9-124">Merhaba tıklatın **ayarları** düğmesi sonraki toohello onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="85be9-124">Click hello **Settings** button next toohello check box.</span></span> <span data-ttu-id="85be9-125">Merhaba **yükseltme parametreleri Düzenle** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="85be9-125">hello **Edit Upgrade Parameters** dialog box appears.</span></span> <span data-ttu-id="85be9-126">Merhaba **yükseltme parametreleri Düzenle** iletişim kutusu hello izlenen, UnmonitoredAuto ve UnmonitoredManual yükseltme modlarını destekler.</span><span class="sxs-lookup"><span data-stu-id="85be9-126">hello **Edit Upgrade Parameters** dialog box supports hello Monitored, UnmonitoredAuto, and UnmonitoredManual upgrade modes.</span></span>
2. <span data-ttu-id="85be9-127">Toouse istediğiniz ve hello parametre Kılavuz doldurun hello yükseltme modu seçin.</span><span class="sxs-lookup"><span data-stu-id="85be9-127">Select hello upgrade mode that you want toouse and then fill out hello parameter grid.</span></span>

    <span data-ttu-id="85be9-128">Her parametre varsayılan değerlerine sahip.</span><span class="sxs-lookup"><span data-stu-id="85be9-128">Each parameter has default values.</span></span> <span data-ttu-id="85be9-129">İsteğe bağlı parametre hello *DefaultServiceTypeHealthPolicy* bir karma tablosu girişi alır.</span><span class="sxs-lookup"><span data-stu-id="85be9-129">hello optional parameter *DefaultServiceTypeHealthPolicy* takes a hash table input.</span></span> <span data-ttu-id="85be9-130">Merhaba karma tablosu için giriş biçimi örneği şudur *DefaultServiceTypeHealthPolicy*:</span><span class="sxs-lookup"><span data-stu-id="85be9-130">Here’s an example of hello hash table input format for *DefaultServiceTypeHealthPolicy*:</span></span>

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    <span data-ttu-id="85be9-131">*ServiceTypeHealthPolicyMap* hello bir karma tablosu girdi alır başka bir isteğe bağlı parametre izlemektir biçimi:</span><span class="sxs-lookup"><span data-stu-id="85be9-131">*ServiceTypeHealthPolicyMap* is another optional parameter that takes a hash table input in hello following format:</span></span>

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    <span data-ttu-id="85be9-132">Gerçekçi örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="85be9-132">Here's a real-life example:</span></span>

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. <span data-ttu-id="85be9-133">UnmonitoredManual yükseltme modu seçerseniz, el ile bir PowerShell konsol toocontinue başlamalı ve hello yükseltme işlemini tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="85be9-133">If you select UnmonitoredManual upgrade mode, you must manually start a PowerShell console toocontinue and finish hello upgrade process.</span></span> <span data-ttu-id="85be9-134">Çok başvuran[Service Fabric uygulama yükseltme: Gelişmiş konular](service-fabric-application-upgrade-advanced.md) toolearn nasıl el ile yükseltme çalışır.</span><span class="sxs-lookup"><span data-stu-id="85be9-134">Refer too[Service Fabric application upgrade: advanced topics](service-fabric-application-upgrade-advanced.md) toolearn how manual upgrade works.</span></span>

## <a name="upgrade-an-application-by-using-powershell"></a><span data-ttu-id="85be9-135">PowerShell kullanarak uygulama yükseltme</span><span class="sxs-lookup"><span data-stu-id="85be9-135">Upgrade an application by using PowerShell</span></span>
<span data-ttu-id="85be9-136">PowerShell cmdlet'leri tooupgrade Service Fabric uygulaması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85be9-136">You can use PowerShell cmdlets tooupgrade a Service Fabric application.</span></span> <span data-ttu-id="85be9-137">Bkz: [Service Fabric uygulama yükseltme öğretici](service-fabric-application-upgrade-tutorial.md) ve [başlangıç ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="85be9-137">See [Service Fabric application upgrade tutorial](service-fabric-application-upgrade-tutorial.md) and [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) for detailed information.</span></span>

## <a name="specify-a-health-check-policy-in-hello-application-manifest-file"></a><span data-ttu-id="85be9-138">Bir sistem durumu denetimi İlkesi hello uygulama bildirim dosyasında belirtin</span><span class="sxs-lookup"><span data-stu-id="85be9-138">Specify a health check policy in hello application manifest file</span></span>
<span data-ttu-id="85be9-139">Her bir Service Fabric uygulaması hizmetinde hello varsayılan değerleri geçersiz kılmak kendi sistem durumu ilkesi parametrelerine sahip olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85be9-139">Every service in a Service Fabric application can have its own health policy parameters that override hello default values.</span></span> <span data-ttu-id="85be9-140">Bu parametre değerlerini hello uygulama bildirim dosyasında sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="85be9-140">You can provide these parameter values in hello application manifest file.</span></span>

<span data-ttu-id="85be9-141">Merhaba aşağıdaki örnek tooapply benzersiz bir sistem durumu ilkesi hello uygulama bildiriminde her hizmet için nasıl kontrol edin gösterir.</span><span class="sxs-lookup"><span data-stu-id="85be9-141">hello following example shows how tooapply a unique health check policy for each service in hello application manifest.</span></span>

```xml
<Policies>
    <HealthPolicy ConsiderWarningAsError="false" MaxPercentUnhealthyDeployedApplications="20">
        <DefaultServiceTypeHealthPolicy MaxPercentUnhealthyServices="20"               
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />
        <ServiceTypeHealthPolicy ServiceTypeName="ServiceTypeName1"
                MaxPercentUnhealthyServices="20"
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />      
    </HealthPolicy>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="85be9-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="85be9-142">Next steps</span></span>
<span data-ttu-id="85be9-143">Bir uygulama dağıtımı hakkında daha fazla bilgi için bkz: [Azure Service Fabric, var olan bir uygulamayı dağıtmak](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="85be9-143">For more information about deploying an application, see [Deploy an existing application in Azure Service Fabric](service-fabric-deploy-existing-app.md).</span></span>