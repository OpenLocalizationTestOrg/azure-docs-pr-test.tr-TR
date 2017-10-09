---
title: "Azure tanılama kullanarak aaaCollect günlükleri | Microsoft Docs"
description: "Bu makalede, Azure'da çalışan Service Fabric kümesinden Azure tanılama toocollect yukarı tooset nasıl günlüğe yazacağını açıklanmaktadır."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 9f7e1fa5-6543-4efd-b53f-39510f18df56
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: afbcfbe972b1847ef33bf0539b4398794b1bd56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a><span data-ttu-id="ed6dc-103">Azure Tanılama’yı kullanarak günlük toplama</span><span class="sxs-lookup"><span data-stu-id="ed6dc-103">Collect logs by using Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ed6dc-104">Windows</span><span class="sxs-lookup"><span data-stu-id="ed6dc-104">Windows</span></span>](service-fabric-diagnostics-how-to-setup-wad.md)
> * [<span data-ttu-id="ed6dc-105">Linux</span><span class="sxs-lookup"><span data-stu-id="ed6dc-105">Linux</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

<span data-ttu-id="ed6dc-106">Azure Service Fabric kümesi çalıştırdığınız bir fikir toocollect hello günlüklerini merkezi bir konumda tüm hello düğümlerinden olur.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-106">When you're running an Azure Service Fabric cluster, it's a good idea toocollect hello logs from all hello nodes in a central location.</span></span> <span data-ttu-id="ed6dc-107">Merhaba günlüklerini merkezi bir konumda sahip çözümlemek ve sorunları kümenizdeki veya bu kümede çalışan hello uygulamaları ve Hizmetleri sorunları gidermenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-107">Having hello logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in hello applications and services running in that cluster.</span></span>

<span data-ttu-id="ed6dc-108">Bir yolu tooupload toplama günlükleri ise toouse hello Azure tanılama uzantısını, hangi yüklemeleri tooAzure depolama, Azure Application Insights ya da Azure Event Hubs günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-108">One way tooupload and collect logs is toouse hello Azure Diagnostics extension, which uploads logs tooAzure Storage, Azure Application Insights, or Azure Event Hubs.</span></span> <span data-ttu-id="ed6dc-109">Merhaba günlükleri doğrudan depolama veya olay hub'ları bu kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-109">hello logs are not that useful directly in storage or in Event Hubs.</span></span> <span data-ttu-id="ed6dc-110">Ancak bir dış işlem tooread hello olayları depolama biriminden kullanın ve bunları bir üründe gibi yerleştirmek [günlük analizi](../log-analytics/log-analytics-service-fabric.md) veya başka bir çözüm günlük ayrıştırma.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-110">But you can use an external process tooread hello events from storage and place them in a product such as [Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span> <span data-ttu-id="ed6dc-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) bir kapsamlı günlük arama ve analizi hizmeti ile yerleşik gelir.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) comes with a comprehensive log search and analytics service built-in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed6dc-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ed6dc-112">Prerequisites</span></span>
<span data-ttu-id="ed6dc-113">Bu araçlar tooperform kullandığınız hello işlemlerin bu belgede:</span><span class="sxs-lookup"><span data-stu-id="ed6dc-113">You use these tools tooperform some of hello operations in this document:</span></span>

* <span data-ttu-id="ed6dc-114">[Azure tanılama](../cloud-services/cloud-services-dotnet-diagnostics.md) (tooAzure bulut Hizmetleri ancak sahip iyi bilgi ve örnekler ilgili)</span><span class="sxs-lookup"><span data-stu-id="ed6dc-114">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related tooAzure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="ed6dc-115">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ed6dc-115">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="ed6dc-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed6dc-116">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="ed6dc-117">Azure Resource Manager istemci</span><span class="sxs-lookup"><span data-stu-id="ed6dc-117">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="ed6dc-118">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="ed6dc-118">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-toocollect"></a><span data-ttu-id="ed6dc-119">Günlük kaynakları toocollect isteyebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ed6dc-119">Log sources that you might want toocollect</span></span>
* <span data-ttu-id="ed6dc-120">**Service Fabric günlükleri**: hello platform toostandard olay izleme için Windows (ETW) ve EventSource kanaldan yayılan.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-120">**Service Fabric logs**: Emitted from hello platform toostandard Event Tracing for Windows (ETW) and EventSource channels.</span></span> <span data-ttu-id="ed6dc-121">Günlükleri birkaç türlerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="ed6dc-121">Logs can be one of several types:</span></span>
  * <span data-ttu-id="ed6dc-122">Çalışma olaylarını: hizmet platform uygular doku hello işlemleri için günlükleri.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-122">Operational events: Logs for operations that hello Service Fabric platform performs.</span></span> <span data-ttu-id="ed6dc-123">Örnek uygulamalar ve hizmetler, düğüm durumu değişiklikleri ve yükseltme bilgileri oluşturulmasını verilebilir.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-123">Examples include creation of applications and services, node state changes, and upgrade information.</span></span>
  * [<span data-ttu-id="ed6dc-124">Reliable Actors programlama modelini olayları</span><span class="sxs-lookup"><span data-stu-id="ed6dc-124">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="ed6dc-125">Programlama modeli olaylarının güvenilir hizmetler</span><span class="sxs-lookup"><span data-stu-id="ed6dc-125">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)
* <span data-ttu-id="ed6dc-126">**Uygulama olaylarını**: hizmetinizin koddan yayılan ve hello Visual Studio şablonları sağlanan hello EventSource yardımcı sınıfı kullanılarak yazılan olaylar.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-126">**Application events**: Events emitted from your service's code and written out by using hello EventSource helper class provided in hello Visual Studio templates.</span></span> <span data-ttu-id="ed6dc-127">Toowrite uygulamanızdan nasıl günlüğe yazacağını daha fazla bilgi için bkz: [İzleyici ve yerel makine geliştirme Kurulum Hizmetleri'nde tanılamak](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="ed6dc-127">For more information on how toowrite logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-hello-diagnostics-extension"></a><span data-ttu-id="ed6dc-128">Merhaba tanılama uzantısını dağıtma</span><span class="sxs-lookup"><span data-stu-id="ed6dc-128">Deploy hello Diagnostics extension</span></span>
<span data-ttu-id="ed6dc-129">günlükleri toplamayı hello ilk toodeploy hello tanılama uzantısını her hello VM'ler hello Service Fabric kümesindeki bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-129">hello first step in collecting logs is toodeploy hello Diagnostics extension on each of hello VMs in hello Service Fabric cluster.</span></span> <span data-ttu-id="ed6dc-130">Merhaba tanılama uzantısını her VM günlükleri toplar ve bunları belirttiğiniz toohello depolama hesabı yükler.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-130">hello Diagnostics extension collects logs on each VM and uploads them toohello storage account that you specify.</span></span> <span data-ttu-id="ed6dc-131">Merhaba adımlar hello Azure portalında veya Azure Resource Manager kullanıp biraz göre farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-131">hello steps vary a little based on whether you use hello Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="ed6dc-132">Merhaba adımlar da hello dağıtım küme oluşturmanın bir parçası değil veya zaten bir küme için göre değişir.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-132">hello steps also vary based on whether hello deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="ed6dc-133">Her senaryo için hello adımları bakalım.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-133">Let's look at hello steps for each scenario.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-hello-portal"></a><span data-ttu-id="ed6dc-134">Küme oluşturma hello portal aracılığıyla bir parçası olarak Hello tanılama uzantısını dağıtma</span><span class="sxs-lookup"><span data-stu-id="ed6dc-134">Deploy hello Diagnostics extension as part of cluster creation through hello portal</span></span>
<span data-ttu-id="ed6dc-135">Küme oluşturma bir parçası olarak hello kümedeki toodeploy hello tanılama uzantısını toohello VM'ler, görüntü aşağıdaki hello gösterilen hello tanılama Ayarları panelini kullanın.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-135">toodeploy hello Diagnostics extension toohello VMs in hello cluster as part of cluster creation, you use hello Diagnostics settings panel shown in hello following image.</span></span> <span data-ttu-id="ed6dc-136">tooenable Reliable Actors veya güvenilir hizmetler olay toplama olun tanılama çok ayarlandığını**üzerinde** (Merhaba varsayılan ayar).</span><span class="sxs-lookup"><span data-stu-id="ed6dc-136">tooenable Reliable Actors or Reliable Services event collection, ensure that Diagnostics is set too**On** (hello default setting).</span></span> <span data-ttu-id="ed6dc-137">Merhaba kümeyi oluşturduktan sonra hello portalını kullanarak bu ayarları değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-137">After you create hello cluster, you can't change these settings by using hello portal.</span></span>

![Küme oluşturma hello portalındaki Azure tanılama ayarları](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

<span data-ttu-id="ed6dc-139">Azure destek ekibinin hello *gerektirir* destek oluşturduğunuz hiç destek isteği toohelp çözümleme günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-139">hello Azure support team *requires* support logs toohelp resolve any support requests that you create.</span></span> <span data-ttu-id="ed6dc-140">Bu günlükler gerçek zamanlı olarak toplanır ve hello kaynak grubunda oluşturduğunuz hello depolama hesaplarından birini depolanır.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-140">These logs are collected in real time and are stored in one of hello storage accounts created in hello resource group.</span></span> <span data-ttu-id="ed6dc-141">Uygulama düzeyi olaylarını Hello tanılama ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-141">hello Diagnostics settings configure application-level events.</span></span> <span data-ttu-id="ed6dc-142">Bu olayları dahil [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) olayları [Reliable Services](service-fabric-reliable-services-diagnostics.md) olaylar ve Azure Storage'da depolanan bazı sistem düzeyinde Service Fabric olayları toobe.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-142">These events include [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) events, [Reliable Services](service-fabric-reliable-services-diagnostics.md) events, and some system-level Service Fabric events toobe stored in Azure Storage.</span></span>

<span data-ttu-id="ed6dc-143">Ürünler gibi [Elasticsearch](https://www.elastic.co/guide/index.html) veya kendi işlem hello depolama hesabından hello olayları alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-143">Products such as [Elasticsearch](https://www.elastic.co/guide/index.html) or your own process can get hello events from hello storage account.</span></span> <span data-ttu-id="ed6dc-144">Şu anda toohello tablo gönderilen yolu toofilter veya Temizle hello olayı yok.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-144">There is currently no way toofilter or groom hello events that are sent toohello table.</span></span> <span data-ttu-id="ed6dc-145">Bir işlem tooremove olaylarını hello tablosundan uygularsanız yok hello tablo toogrow devam eder.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-145">If you don't implement a process tooremove events from hello table, hello table will continue toogrow.</span></span>

<span data-ttu-id="ed6dc-146">Merhaba portalını kullanarak bir küme oluştururken, hello şablonunu indirebilir öneririz **Tamam'ı tıklatmadan önce** toocreate hello küme.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-146">When you're creating a cluster by using hello portal, we highly recommend that you download hello template **before you click OK** toocreate hello cluster.</span></span> <span data-ttu-id="ed6dc-147">Ayrıntılar için çok başvurun[bir Azure Resource Manager şablonu kullanarak bir Service Fabric kümesi ayarlayın](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="ed6dc-147">For details, refer too[Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="ed6dc-148">Merhaba portalını kullanarak bazı değişiklik yapılamıyor çünkü hello şablonu toomake değişiklikleri daha sonra gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-148">You'll need hello template toomake changes later, because you can't make some changes by using hello portal.</span></span>

<span data-ttu-id="ed6dc-149">Merhaba aşağıdaki adımları kullanarak şablonları hello Portalı'ndan dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-149">You can export templates from hello portal by using hello following steps.</span></span> <span data-ttu-id="ed6dc-150">Ancak, gerekli bilgiler eksik null değerler olabileceği için bu şablonları daha zor toouse olabilir.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-150">However, these templates can be more difficult toouse because they might have null values that are missing required information.</span></span>

1. <span data-ttu-id="ed6dc-151">Kaynak grubu açın.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-151">Open your resource group.</span></span>
2. <span data-ttu-id="ed6dc-152">Seçin **ayarları** toodisplay hello Ayarları panelini.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-152">Select **Settings** toodisplay hello settings panel.</span></span>
3. <span data-ttu-id="ed6dc-153">Seçin **dağıtımları** toodisplay hello dağıtım Geçmiş paneli.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-153">Select **Deployments** toodisplay hello deployment history panel.</span></span>
4. <span data-ttu-id="ed6dc-154">Merhaba dağıtım dağıtım toodisplay hello ayrıntılarını seçin.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-154">Select a deployment toodisplay hello details of hello deployment.</span></span>
5. <span data-ttu-id="ed6dc-155">Seçin **şablonu dışarı aktar** toodisplay hello şablon paneli.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-155">Select **Export Template** toodisplay hello template panel.</span></span>
6. <span data-ttu-id="ed6dc-156">Seçin **toofile kaydetmek** tooexport hello şablonu, parametre ve PowerShell dosyalarını içeren bir .zip dosyası.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-156">Select **Save toofile** tooexport a .zip file that contains hello template, parameter, and PowerShell files.</span></span>

<span data-ttu-id="ed6dc-157">Merhaba dosyaları dışarı aktardıktan sonra toomake değişiklik gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-157">After you export hello files, you need toomake a modification.</span></span> <span data-ttu-id="ed6dc-158">Merhaba parameters.json dosyasını düzenleyin ve hello kaldırmak **Admınpassword** öğesi.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-158">Edit hello parameters.json file and remove hello **adminPassword** element.</span></span> <span data-ttu-id="ed6dc-159">Merhaba dağıtım betiğini çalıştırdığınızda bu hello parola için bir isteme neden olur.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-159">This will cause a prompt for hello password when hello deployment script is run.</span></span> <span data-ttu-id="ed6dc-160">Merhaba dağıtım betiği çalıştırırken toofix null parametre değerleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-160">When you're running hello deployment script, you might have toofix null parameter values.</span></span>

<span data-ttu-id="ed6dc-161">toouse hello bir yapılandırma şablonu tooupdate yüklenen:</span><span class="sxs-lookup"><span data-stu-id="ed6dc-161">toouse hello downloaded template tooupdate a configuration:</span></span>

1. <span data-ttu-id="ed6dc-162">Yerel bilgisayarınızdaki Hello içeriği tooa klasöre ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-162">Extract hello contents tooa folder on your local computer.</span></span>
2. <span data-ttu-id="ed6dc-163">Merhaba içeriği tooreflect hello yeni yapılandırmasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-163">Modify hello contents tooreflect hello new configuration.</span></span>
3. <span data-ttu-id="ed6dc-164">PowerShell'i başlatın ve hello içeriği ayıkladığınız toohello klasöre değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-164">Start PowerShell and change toohello folder where you extracted hello content.</span></span>
4. <span data-ttu-id="ed6dc-165">Çalıştırma **deploy.ps1** ve hello abonelik kimliği hello kaynak grubu adı girin (kullanım hello aynı adı tooupdate hello yapılandırma) ve benzersiz dağıtım adı.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-165">Run **deploy.ps1** and fill in hello subscription ID, hello resource group name (use hello same name tooupdate hello configuration), and a unique deployment name.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="ed6dc-166">Azure Kaynak Yöneticisi'ni kullanarak küme oluşturmanın bir parçası olarak Hello tanılama uzantısını dağıtma</span><span class="sxs-lookup"><span data-stu-id="ed6dc-166">Deploy hello Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="ed6dc-167">Merhaba küme oluşturmadan önce toocreate Kaynak Yöneticisi'ni kullanarak bir küme, tooadd hello tanılama yapılandırması JSON toohello tam küme Resource Manager şablonu gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-167">toocreate a cluster by using Resource Manager, you need tooadd hello Diagnostics configuration JSON toohello full cluster Resource Manager template before you create hello cluster.</span></span> <span data-ttu-id="ed6dc-168">Eklenen tanılama yapılandırması bir örnek beş VM küme Resource Manager şablonu sağladığımız tooit Resource Manager şablonu örneklerimizi bir parçası olarak.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-168">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added tooit as part of our Resource Manager template samples.</span></span> <span data-ttu-id="ed6dc-169">Bu konumda hello Azure Örnekleri Galerisi bkz: [beş düğümlü kümeyi tanılama Resource Manager şablonu örneği ile](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span><span class="sxs-lookup"><span data-stu-id="ed6dc-169">You can see it at this location in hello Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span></span>

<span data-ttu-id="ed6dc-170">toosee hello tanılama ayarını hello Resource Manager şablonu, açık hello azuredeploy.json dosyasını ve arama **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-170">toosee hello Diagnostics setting in hello Resource Manager template, open hello azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="ed6dc-171">Bu şablon, select hello'ı kullanarak bir küme toocreate **tooAzure dağıtmak** düğmesini hello önceki bağlantıda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-171">toocreate a cluster by using this template, select hello **Deploy tooAzure** button available at hello previous link.</span></span>

<span data-ttu-id="ed6dc-172">Alternatif olarak, hello Resource Manager örnek indirebilir, değişiklikleri tooit olun ve hello kullanarak hello değiştirilmiş şablonu ile bir küme oluşturma `New-AzureRmResourceGroupDeployment` bir Azure PowerShell penceresinde komutu.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-172">Alternatively, you can download hello Resource Manager sample, make changes tooit, and create a cluster with hello modified template by using hello `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="ed6dc-173">Kod toohello komutta geçirdiğiniz hello parametreleri için aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-173">See hello following code for hello parameters that you pass in toohello command.</span></span> <span data-ttu-id="ed6dc-174">Merhaba makale toodeploy bir kaynak grup PowerShell kullanarak nasıl hakkında ayrıntılı bilgi için bkz [hello Azure Resource Manager şablonu ile bir kaynak grubu dağıtma](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ed6dc-174">For detailed information on how toodeploy a resource group by using PowerShell, see hello article [Deploy a resource group with hello Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a><span data-ttu-id="ed6dc-175">Merhaba tanılama uzantısını tooan var olan küme dağıtma</span><span class="sxs-lookup"><span data-stu-id="ed6dc-175">Deploy hello Diagnostics extension tooan existing cluster</span></span>
<span data-ttu-id="ed6dc-176">Dağıtılan tanılama yok varolan bir kümeye varsa veya toomodify var olan yapılandırmasını istiyorsanız, ekleyebilir veya güncelleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-176">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want toomodify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="ed6dc-177">Kullanılan toocreate hello var olan kümesinin hello Resource Manager şablonu değiştirin veya daha önce açıklandığı gibi hello portalından hello şablonu indirin.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-177">Modify hello Resource Manager template that's used toocreate hello existing cluster or download hello template from hello portal as described earlier.</span></span> <span data-ttu-id="ed6dc-178">Merhaba aşağıdaki görevleri gerçekleştirerek Hello template.json dosyasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-178">Modify hello template.json file by performing hello following tasks.</span></span>

<span data-ttu-id="ed6dc-179">Yeni bir depolama kaynak toohello şablonu toohello kaynakları bölümü ekleme.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-179">Add a new storage resource toohello template by adding toohello resources section.</span></span>

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[parameters('applicationDiagnosticsStorageAccountName')]",
  "location": "[parameters('computeLocation')]",
  "properties": {
    "accountType": "[parameters('applicationDiagnosticsStorageAccountType')]"
  },
  "tags": {
    "resourceType": "Service Fabric",
    "clusterName": "[parameters('clusterName')]"
  }
},
```

 <span data-ttu-id="ed6dc-180">Ardından, toohello parametreleri yalnızca hello depolama hesabı tanımlarını sonra arasında bölüm eklemek `supportLogStorageAccountName` ve `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-180">Next, add toohello parameters section just after hello storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="ed6dc-181">Merhaba yer tutucu metni değiştirmek *depolama hesabı adı buraya* hello depolama hesabı hello adı.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-181">Replace hello placeholder text *storage account name goes here* with hello name of hello storage account.</span></span>

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for hello application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for hello storage account that contains application diagnostics data from hello cluster"
      }
    },
```
<span data-ttu-id="ed6dc-182">Ardından, hello güncelleştirin `VirtualMachineProfile` hello uzantıları dizi koddan hello ekleyerek hello template.json dosyasının bölümü.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-182">Then, update hello `VirtualMachineProfile` section of hello template.json file by adding hello following code within hello extensions array.</span></span> <span data-ttu-id="ed6dc-183">Emin tooadd hello başındaki veya burada eklenen bağlı olarak hello son virgül olabilir.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-183">Be sure tooadd a comma at hello beginning or hello end, depending on where it's inserted.</span></span>

```json
{
    "name": "[concat(parameters('vmNodeType0Name'),'_Microsoft.Insights.VMDiagnosticsSettings')]",
    "properties": {
        "type": "IaaSDiagnostics",
        "autoUpgradeMinorVersion": true,
        "protectedSettings": {
        "storageAccountName": "[parameters('applicationDiagnosticsStorageAccountName')]",
        "storageAccountKey": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName')),'2015-05-01-preview').key1]",
        "storageAccountEndPoint": "https://core.windows.net/"
        },
        "publisher": "Microsoft.Azure.Diagnostics",
        "settings": {
        "WadCfg": {
            "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": "50000",
            "EtwProviders": {
                "EtwEventSourceProviderConfiguration": [
                {
                    "provider": "Microsoft-ServiceFabric-Actors",
                    "scheduledTransferKeywordFilter": "1",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableActorEventTable"
                    }
                },
                {
                    "provider": "Microsoft-ServiceFabric-Services",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableServiceEventTable"
                    }
                }
                ],
                "EtwManifestProviderConfiguration": [
                {
                    "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
                    "scheduledTransferLogLevelFilter": "Information",
                    "scheduledTransferKeywordFilter": "4611686018427387904",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricSystemEventTable"
                    }
                }
                ]
            }
            }
        },
        "StorageAccount": "[parameters('applicationDiagnosticsStorageAccountName')]"
        },
        "typeHandlerVersion": "1.5"
    }
}
```

<span data-ttu-id="ed6dc-184">Açıklandığı gibi hello template.json dosyasını değiştirdikten sonra hello Resource Manager şablonunu yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-184">After you modify hello template.json file as described, republish hello Resource Manager template.</span></span> <span data-ttu-id="ed6dc-185">Merhaba şablonu dışarı aktarılmışsa çalışan hello deploy.ps1 dosyasını hello şablonu yeniden yayımlar.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-185">If hello template was exported, running hello deploy.ps1 file republishes hello template.</span></span> <span data-ttu-id="ed6dc-186">Dağıttıktan sonra emin **ProvisioningState** olan **başarılı**.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-186">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="update-diagnostics-toocollect-health-and-load-events"></a><span data-ttu-id="ed6dc-187">Tanılama toocollect sistem durumu ve yükleme olaylarını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="ed6dc-187">Update diagnostics toocollect health and load events</span></span>

<span data-ttu-id="ed6dc-188">Service Fabric Hello 5.4 sürümünden başlayarak, sistem durumu ve yük ölçüm olayları koleksiyonu için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-188">Starting with hello 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="ed6dc-189">Bu olaylar hello durumu kullanarak hello sistemi veya kodunuzu tarafından oluşturulan olayları yansıtmak veya Raporlama API'leri gibi yük [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) veya [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed6dc-189">These events reflect events generated by hello system or your code by using hello health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="ed6dc-190">Bu, toplama ve zaman içinde sistem durumu görüntüleme ve sistem durumu veya yük olaylara dayanarak uyarı verme sağlar.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-190">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="ed6dc-191">Visual Studio'nun Tanılama Olay Görüntüleyicisi'nde bu olayları eklemek tooview "Microsoft-ServiceFabric:4:0x4000000000000008" toohello ETW sağlayıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-191">tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" toohello list of ETW providers.</span></span>

<span data-ttu-id="ed6dc-192">toocollect hello olaylar, değişiklik hello resource manager şablonu tooinclude</span><span class="sxs-lookup"><span data-stu-id="ed6dc-192">toocollect hello events, modify hello resource manager template tooinclude</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387912",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

## <a name="update-diagnostics-toocollect-and-upload-logs-from-new-eventsource-channels"></a><span data-ttu-id="ed6dc-193">Tanılama toocollect güncelleştirin ve yeni EventSource kanallar günlükleri karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="ed6dc-193">Update Diagnostics toocollect and upload logs from new EventSource channels</span></span>
<span data-ttu-id="ed6dc-194">tooupdate tanılama toocollect toodeploy hakkında olduğunuz yeni bir uygulama temsil eden yeni EventSource kanallar günlüklerinden gerçekleştirmek hello olduğu gibi aynı adımları hello [önceki bölümde](#deploywadarm) mevcut bir tanılama kurulumu için Küme.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-194">tooupdate Diagnostics toocollect logs from new EventSource channels that represent a new application that you're about toodeploy, perform hello same steps as in hello [previous section](#deploywadarm) for setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="ed6dc-195">Merhaba güncelleştirme `EtwEventSourceProviderConfiguration` hello kullanarak hello yapılandırma uygulamadan önce hello yeni EventSource kanallar güncelleştirmek için hello template.json dosyasını tooadd girişlerinde bölümünde `New-AzureRmResourceGroupDeployment` PowerShell komutu.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-195">Update hello `EtwEventSourceProviderConfiguration` section in hello template.json file tooadd entries for hello new EventSource channels before you apply hello configuration update by using hello `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="ed6dc-196">Merhaba olay kaynağı Hello adını hello ServiceEventSource.cs Visual Studio tarafından oluşturulan dosya kodunuzda bir parçası olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-196">hello name of hello event source is defined as part of your code in hello Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="ed6dc-197">Olay kaynağı Eventsource My olarak adlandırılmışsa, örneğin, kod tooplace hello olayları Eventsource My MyDestinationTableName adlı bir tabloya aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-197">For example, if your event source is named My-Eventsource, add hello following code tooplace hello events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="ed6dc-198">toocollect performans sayaçlarını veya olay günlükleri, değişiklik hello Resource Manager şablonu sağlanan hello örnekleri kullanarak [bir Azure Resource Manager şablonukullanılarakizlemeveTanılamaileWindowssanalmakineoluşturma](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ed6dc-198">toocollect performance counters or event logs, modify hello Resource Manager template by using hello examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="ed6dc-199">Ardından, hello Resource Manager şablonunu yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="ed6dc-199">Then, republish hello Resource Manager template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed6dc-200">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ed6dc-200">Next steps</span></span>
<span data-ttu-id="ed6dc-201">daha ayrıntılı toounderstand, görünmelidir sorunlarını giderme sırasında hangi olayların görmek için gösterilen hello tanılama olayları [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) ve [Reliable Services](service-fabric-reliable-services-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="ed6dc-201">toounderstand in more detail what events you should look for while troubleshooting issues, see hello diagnostic events emitted for [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) and [Reliable Services](service-fabric-reliable-services-diagnostics.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="ed6dc-202">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="ed6dc-202">Related articles</span></span>
* [<span data-ttu-id="ed6dc-203">Tanılama uzantısını toocollect performans sayaçlarını veya kullanarak günlükleri nasıl hello öğrenin</span><span class="sxs-lookup"><span data-stu-id="ed6dc-203">Learn how toocollect performance counters or logs by using hello Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ed6dc-204">Service Fabric çözümde günlük analizi</span><span class="sxs-lookup"><span data-stu-id="ed6dc-204">Service Fabric solution in Log Analytics</span></span>](../log-analytics/log-analytics-service-fabric.md)

