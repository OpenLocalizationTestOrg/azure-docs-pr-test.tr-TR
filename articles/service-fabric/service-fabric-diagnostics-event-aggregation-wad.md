---
title: Windows Azure Diagnostics Service Fabric olay toplama aaaAzure | Microsoft Docs
description: "Toplama ve izleme ve tanılama Azure Service Fabric kümeleri için WAD kullanarak olay toplama hakkında bilgi edinin."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 4827ce66620e61c5b4a8682db55952333113188a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a><span data-ttu-id="d7f33-103">Olay toplama ve Windows Azure Tanılama'yı kullanarak koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="d7f33-103">Event aggregation and collection using Windows Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d7f33-104">Windows</span><span class="sxs-lookup"><span data-stu-id="d7f33-104">Windows</span></span>](service-fabric-diagnostics-event-aggregation-wad.md)
> * [<span data-ttu-id="d7f33-105">Linux</span><span class="sxs-lookup"><span data-stu-id="d7f33-105">Linux</span></span>](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

<span data-ttu-id="d7f33-106">Azure Service Fabric kümesi çalıştırdığınız bir fikir toocollect hello günlüklerini merkezi bir konumda tüm hello düğümlerinden olur.</span><span class="sxs-lookup"><span data-stu-id="d7f33-106">When you're running an Azure Service Fabric cluster, it's a good idea toocollect hello logs from all hello nodes in a central location.</span></span> <span data-ttu-id="d7f33-107">Merhaba günlüklerini merkezi bir konumda sahip çözümlemek ve sorunları kümenizdeki veya bu kümede çalışan hello uygulamaları ve Hizmetleri sorunları gidermenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d7f33-107">Having hello logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in hello applications and services running in that cluster.</span></span>

<span data-ttu-id="d7f33-108">Bir yolu tooupload ve toplama günlükleri günlükleri tooAzure depolama yükler ve ayrıca hello seçeneği toosend günlükleri tooAzure Application Insights veya olay hub'ları içeren toouse hello Windows Azure tanılama (WAD) uzantısı olur.</span><span class="sxs-lookup"><span data-stu-id="d7f33-108">One way tooupload and collect logs is toouse hello Windows Azure Diagnostics (WAD) extension, which uploads logs tooAzure Storage, and also has hello option toosend logs tooAzure Application Insights or Event Hubs.</span></span> <span data-ttu-id="d7f33-109">Ayrıca bir dış işlem tooread hello olayları depolama biriminden kullanın ve analiz platformu üründe gibi yerleştirin [OMS günlük analizi](../log-analytics/log-analytics-service-fabric.md) veya başka bir çözüm günlük ayrıştırma.</span><span class="sxs-lookup"><span data-stu-id="d7f33-109">You can also use an external process tooread hello events from storage and place them in an analysis platform product, such as [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7f33-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d7f33-110">Prerequisites</span></span>
<span data-ttu-id="d7f33-111">Bu araçları kullanılan tooperform olan bazı bu belgedeki hello işlemlerinin:</span><span class="sxs-lookup"><span data-stu-id="d7f33-111">These tools are used tooperform some of hello operations in this document:</span></span>

* <span data-ttu-id="d7f33-112">[Azure tanılama](../cloud-services/cloud-services-dotnet-diagnostics.md) (tooAzure bulut Hizmetleri ancak sahip iyi bilgi ve örnekler ilgili)</span><span class="sxs-lookup"><span data-stu-id="d7f33-112">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related tooAzure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="d7f33-113">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d7f33-113">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="d7f33-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7f33-114">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="d7f33-115">Azure Resource Manager istemci</span><span class="sxs-lookup"><span data-stu-id="d7f33-115">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="d7f33-116">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="d7f33-116">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a><span data-ttu-id="d7f33-117">Günlük ve olay kaynakları</span><span class="sxs-lookup"><span data-stu-id="d7f33-117">Log and event sources</span></span>

### <a name="service-fabric-platform-events"></a><span data-ttu-id="d7f33-118">Service Fabric platform olayları</span><span class="sxs-lookup"><span data-stu-id="d7f33-118">Service Fabric platform events</span></span>
<span data-ttu-id="d7f33-119">' Da anlatıldığı gibi [bu makalede](service-fabric-diagnostics-event-generation-infra.md), Service Fabric ayarlayan, birkaç Giden kutusu günlük kanalları, hangi Merhaba aşağıdaki kanallar kolayca WAD toosend izleme ve tanılama veri tooa depolama tablosu ile yapılandırılmış olan veya başka bir yerde:</span><span class="sxs-lookup"><span data-stu-id="d7f33-119">As discussed in [this article](service-fabric-diagnostics-event-generation-infra.md), Service Fabric sets you up with a few out-of-the-box logging channels, of which hello following channels are easily configured with WAD toosend monitoring and diagnostics data tooa storage table or elsewhere:</span></span>
  * <span data-ttu-id="d7f33-120">Çalışma olaylarını: hizmet platform uygular doku hello üst düzey işlem.</span><span class="sxs-lookup"><span data-stu-id="d7f33-120">Operational events: higher-level operations that hello Service Fabric platform performs.</span></span> <span data-ttu-id="d7f33-121">Örnek uygulamalar ve hizmetler, düğüm durumu değişiklikleri ve yükseltme bilgileri oluşturulmasını verilebilir.</span><span class="sxs-lookup"><span data-stu-id="d7f33-121">Examples include creation of applications and services, node state changes, and upgrade information.</span></span> <span data-ttu-id="d7f33-122">Bu olay için Windows izleme (ETW) günlükleri olarak gösterilen</span><span class="sxs-lookup"><span data-stu-id="d7f33-122">These are emitted as Event Tracing for Windows (ETW) logs</span></span>
  * [<span data-ttu-id="d7f33-123">Reliable Actors programlama modelini olayları</span><span class="sxs-lookup"><span data-stu-id="d7f33-123">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="d7f33-124">Programlama modeli olaylarının güvenilir hizmetler</span><span class="sxs-lookup"><span data-stu-id="d7f33-124">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a><span data-ttu-id="d7f33-125">Uygulama olayları</span><span class="sxs-lookup"><span data-stu-id="d7f33-125">Application events</span></span>
 <span data-ttu-id="d7f33-126">Uygulamaların ve hizmetlerin koddan yayılan ve hello EventSource yardımcı sınıfı kullanılarak yazılan olaylar hello Visual Studio şablonları sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d7f33-126">Events emitted from your applications' and services' code and written out by using hello EventSource helper class provided in hello Visual Studio templates.</span></span> <span data-ttu-id="d7f33-127">Toowrite EventSource uygulamanızdan nasıl günlüğe yazacağını daha fazla bilgi için bkz: [İzleyici ve yerel makine geliştirme Kurulum Hizmetleri'nde tanılamak](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="d7f33-127">For more information on how toowrite EventSource logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-hello-diagnostics-extension"></a><span data-ttu-id="d7f33-128">Merhaba tanılama uzantısını dağıtma</span><span class="sxs-lookup"><span data-stu-id="d7f33-128">Deploy hello Diagnostics extension</span></span>
<span data-ttu-id="d7f33-129">günlükleri toplamayı hello ilk toodeploy hello tanılama uzantısını her hello VM'ler hello Service Fabric kümesindeki bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="d7f33-129">hello first step in collecting logs is toodeploy hello Diagnostics extension on each of hello VMs in hello Service Fabric cluster.</span></span> <span data-ttu-id="d7f33-130">Merhaba tanılama uzantısını her VM günlükleri toplar ve bunları belirttiğiniz toohello depolama hesabı yükler.</span><span class="sxs-lookup"><span data-stu-id="d7f33-130">hello Diagnostics extension collects logs on each VM and uploads them toohello storage account that you specify.</span></span> <span data-ttu-id="d7f33-131">Merhaba adımlar hello Azure portalında veya Azure Resource Manager kullanıp biraz göre farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="d7f33-131">hello steps vary a little based on whether you use hello Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="d7f33-132">Merhaba adımlar da hello dağıtım küme oluşturmanın bir parçası değil veya zaten bir küme için göre değişir.</span><span class="sxs-lookup"><span data-stu-id="d7f33-132">hello steps also vary based on whether hello deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="d7f33-133">Her senaryo için hello adımları bakalım.</span><span class="sxs-lookup"><span data-stu-id="d7f33-133">Let's look at hello steps for each scenario.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a><span data-ttu-id="d7f33-134">Azure portal ile küme oluşturma bir parçası olarak Hello tanılama uzantısını dağıtma</span><span class="sxs-lookup"><span data-stu-id="d7f33-134">Deploy hello Diagnostics extension as part of cluster creation through Azure portal</span></span>
<span data-ttu-id="d7f33-135">Küme oluşturma bir parçası olarak hello kümedeki toodeploy hello tanılama uzantısını toohello VM'ler, hello aşağıda gösterildiği hello tanılama ayarları bölmesini kullanın görüntü - tanılama çok ayarlandığından emin olun**üzerinde** (Merhaba varsayılan ayar) .</span><span class="sxs-lookup"><span data-stu-id="d7f33-135">toodeploy hello Diagnostics extension toohello VMs in hello cluster as part of cluster creation, you use hello Diagnostics settings panel shown in hello following image - ensure that Diagnostics is set too**On** (hello default setting).</span></span> <span data-ttu-id="d7f33-136">Merhaba kümeyi oluşturduktan sonra hello portalını kullanarak bu ayarları değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7f33-136">After you create hello cluster, you can't change these settings by using hello portal.</span></span>

![Küme oluşturma hello portalındaki Azure tanılama ayarları](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

<span data-ttu-id="d7f33-138">Merhaba portalını kullanarak bir küme oluştururken, hello şablonunu indirebilir öneririz **Tamam'ı tıklatmadan önce** toocreate hello küme.</span><span class="sxs-lookup"><span data-stu-id="d7f33-138">When you're creating a cluster by using hello portal, we highly recommend that you download hello template **before you click OK** toocreate hello cluster.</span></span> <span data-ttu-id="d7f33-139">Ayrıntılar için çok başvurun[bir Azure Resource Manager şablonu kullanarak bir Service Fabric kümesi ayarlayın](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="d7f33-139">For details, refer too[Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="d7f33-140">Merhaba portalını kullanarak bazı değişiklik yapılamıyor çünkü hello şablonu toomake değişiklikleri daha sonra gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7f33-140">You'll need hello template toomake changes later, because you can't make some changes by using hello portal.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="d7f33-141">Azure Kaynak Yöneticisi'ni kullanarak küme oluşturmanın bir parçası olarak Hello tanılama uzantısını dağıtma</span><span class="sxs-lookup"><span data-stu-id="d7f33-141">Deploy hello Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="d7f33-142">Merhaba küme oluşturmadan önce toocreate Kaynak Yöneticisi'ni kullanarak bir küme, tooadd hello tanılama yapılandırması JSON toohello tam küme Resource Manager şablonu gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7f33-142">toocreate a cluster by using Resource Manager, you need tooadd hello Diagnostics configuration JSON toohello full cluster Resource Manager template before you create hello cluster.</span></span> <span data-ttu-id="d7f33-143">Eklenen tanılama yapılandırması bir örnek beş VM küme Resource Manager şablonu sağladığımız tooit Resource Manager şablonu örneklerimizi bir parçası olarak.</span><span class="sxs-lookup"><span data-stu-id="d7f33-143">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added tooit as part of our Resource Manager template samples.</span></span> <span data-ttu-id="d7f33-144">Bu konumda hello Azure Örnekleri Galerisi bkz: [beş düğümlü kümeyi tanılama Resource Manager şablonu örneği ile](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span><span class="sxs-lookup"><span data-stu-id="d7f33-144">You can see it at this location in hello Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span></span>

<span data-ttu-id="d7f33-145">toosee hello tanılama ayarını hello Resource Manager şablonu, açık hello azuredeploy.json dosyasını ve arama **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="d7f33-145">toosee hello Diagnostics setting in hello Resource Manager template, open hello azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="d7f33-146">Bu şablon, select hello'ı kullanarak bir küme toocreate **tooAzure dağıtmak** düğmesini hello önceki bağlantıda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d7f33-146">toocreate a cluster by using this template, select hello **Deploy tooAzure** button available at hello previous link.</span></span>

<span data-ttu-id="d7f33-147">Alternatif olarak, hello Resource Manager örnek indirebilir, değişiklikleri tooit olun ve hello kullanarak hello değiştirilmiş şablonu ile bir küme oluşturma `New-AzureRmResourceGroupDeployment` bir Azure PowerShell penceresinde komutu.</span><span class="sxs-lookup"><span data-stu-id="d7f33-147">Alternatively, you can download hello Resource Manager sample, make changes tooit, and create a cluster with hello modified template by using hello `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="d7f33-148">Kod toohello komutta geçirdiğiniz hello parametreleri için aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="d7f33-148">See hello following code for hello parameters that you pass in toohello command.</span></span> <span data-ttu-id="d7f33-149">Merhaba makale toodeploy bir kaynak grup PowerShell kullanarak nasıl hakkında ayrıntılı bilgi için bkz [hello Azure Resource Manager şablonu ile bir kaynak grubu dağıtma](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d7f33-149">For detailed information on how toodeploy a resource group by using PowerShell, see hello article [Deploy a resource group with hello Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a><span data-ttu-id="d7f33-150">Merhaba tanılama uzantısını tooan var olan küme dağıtma</span><span class="sxs-lookup"><span data-stu-id="d7f33-150">Deploy hello Diagnostics extension tooan existing cluster</span></span>
<span data-ttu-id="d7f33-151">Dağıtılan tanılama yok varolan bir kümeye varsa veya toomodify var olan yapılandırmasını istiyorsanız, ekleyebilir veya güncelleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="d7f33-151">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want toomodify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="d7f33-152">Kullanılan toocreate hello var olan kümesinin hello Resource Manager şablonu değiştirin veya daha önce açıklandığı gibi hello portalından hello şablonu indirin.</span><span class="sxs-lookup"><span data-stu-id="d7f33-152">Modify hello Resource Manager template that's used toocreate hello existing cluster or download hello template from hello portal as described earlier.</span></span> <span data-ttu-id="d7f33-153">Merhaba aşağıdaki görevleri gerçekleştirerek Hello template.json dosyasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d7f33-153">Modify hello template.json file by performing hello following tasks.</span></span>

<span data-ttu-id="d7f33-154">Yeni bir depolama kaynak toohello şablonu toohello kaynakları bölümü ekleme.</span><span class="sxs-lookup"><span data-stu-id="d7f33-154">Add a new storage resource toohello template by adding toohello resources section.</span></span>

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

 <span data-ttu-id="d7f33-155">Ardından, toohello parametreleri yalnızca hello depolama hesabı tanımlarını sonra arasında bölüm eklemek `supportLogStorageAccountName` ve `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="d7f33-155">Next, add toohello parameters section just after hello storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="d7f33-156">Merhaba yer tutucu metni değiştirmek *depolama hesabı adı buraya* hello depolama hesabı hello adı.</span><span class="sxs-lookup"><span data-stu-id="d7f33-156">Replace hello placeholder text *storage account name goes here* with hello name of hello storage account.</span></span>

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
<span data-ttu-id="d7f33-157">Ardından, hello güncelleştirin `VirtualMachineProfile` hello uzantıları dizi koddan hello ekleyerek hello template.json dosyasının bölümü.</span><span class="sxs-lookup"><span data-stu-id="d7f33-157">Then, update hello `VirtualMachineProfile` section of hello template.json file by adding hello following code within hello extensions array.</span></span> <span data-ttu-id="d7f33-158">Emin tooadd hello başındaki veya burada eklenen bağlı olarak hello son virgül olabilir.</span><span class="sxs-lookup"><span data-stu-id="d7f33-158">Be sure tooadd a comma at hello beginning or hello end, depending on where it's inserted.</span></span>

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

<span data-ttu-id="d7f33-159">Açıklandığı gibi hello template.json dosyasını değiştirdikten sonra hello Resource Manager şablonunu yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="d7f33-159">After you modify hello template.json file as described, republish hello Resource Manager template.</span></span> <span data-ttu-id="d7f33-160">Merhaba şablonu dışarı aktarılmışsa çalışan hello deploy.ps1 dosyasını hello şablonu yeniden yayımlar.</span><span class="sxs-lookup"><span data-stu-id="d7f33-160">If hello template was exported, running hello deploy.ps1 file republishes hello template.</span></span> <span data-ttu-id="d7f33-161">Dağıttıktan sonra emin **ProvisioningState** olan **başarılı**.</span><span class="sxs-lookup"><span data-stu-id="d7f33-161">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="collect-health-and-load-events"></a><span data-ttu-id="d7f33-162">Sistem durumu toplama ve olayları yükleme</span><span class="sxs-lookup"><span data-stu-id="d7f33-162">Collect health and load events</span></span>

<span data-ttu-id="d7f33-163">Service Fabric Hello 5.4 sürümünden başlayarak, sistem durumu ve yük ölçüm olayları koleksiyonu için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d7f33-163">Starting with hello 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="d7f33-164">Bu olaylar hello durumu kullanarak hello sistemi veya kodunuzu tarafından oluşturulan olayları yansıtmak veya Raporlama API'leri gibi yük [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) veya [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="d7f33-164">These events reflect events generated by hello system or your code by using hello health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="d7f33-165">Bu, toplama ve zaman içinde sistem durumu görüntüleme ve sistem durumu veya yük olaylara dayanarak uyarı verme sağlar.</span><span class="sxs-lookup"><span data-stu-id="d7f33-165">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="d7f33-166">Visual Studio'nun Tanılama Olay Görüntüleyicisi'nde bu olayları eklemek tooview "Microsoft-ServiceFabric:4:0x4000000000000008" toohello ETW sağlayıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="d7f33-166">tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" toohello list of ETW providers.</span></span>

<span data-ttu-id="d7f33-167">toocollect hello olaylar, değişiklik hello Resource Manager şablonu tooinclude</span><span class="sxs-lookup"><span data-stu-id="d7f33-167">toocollect hello events, modify hello Resource Manager template tooinclude</span></span>

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

## <a name="collect-reverse-proxy-events"></a><span data-ttu-id="d7f33-168">Ters proxy olaylarını Topla</span><span class="sxs-lookup"><span data-stu-id="d7f33-168">Collect reverse proxy events</span></span>

<span data-ttu-id="d7f33-169">Service Fabric Hello 5.7 sürümünden başlayarak [ters proxy](service-fabric-reverseproxy.md) olayları koleksiyonu için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d7f33-169">Starting with hello 5.7 release of Service Fabric, [reverse proxy](service-fabric-reverseproxy.md) events are available for collection.</span></span>
<span data-ttu-id="d7f33-170">Ters proxy iki kanallarına bir içeren hata olayları yayar yansıtma olayları istek işleme hataları ve başka bir hello ters proxy işlenen tüm hello istekler hakkında ayrıntılı olayları içeren hello.</span><span class="sxs-lookup"><span data-stu-id="d7f33-170">Reverse proxy emits events into two channels, one containing error events reflecting request processing failures and hello other one containing verbose events about all hello requests processed at hello reverse proxy.</span></span> 

1. <span data-ttu-id="d7f33-171">Hatası olaylarını Topla: Visual Studio'nun Tanılama Olay Görüntüleyicisi'nde bu olayları eklemek tooview "Microsoft-ServiceFabric:4:0x4000000000000010" toohello ETW sağlayıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="d7f33-171">Collect error events: tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000010" toohello list of ETW providers.</span></span>
<span data-ttu-id="d7f33-172">Azure kümeleri toocollect hello olaylarından hello Resource Manager şablonu tooinclude değiştirme</span><span class="sxs-lookup"><span data-stu-id="d7f33-172">toocollect hello events from Azure clusters, modify hello Resource Manager template tooinclude</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387920",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

2. <span data-ttu-id="d7f33-173">Toplama tüm olayları işlemeyi istek: Visual Studio'da 's Tanılama Olay Görüntüleyicisi'ni güncelleştirme hello Microsoft ServiceFabric girişi hello ETW sağlayıcı listesi çok "Microsoft-ServiceFabric:4:0x4000000000000020".</span><span class="sxs-lookup"><span data-stu-id="d7f33-173">Collect all request processing events: In Visual Studio's Diagnostic Event Viewer, update hello Microsoft-ServiceFabric entry in hello ETW provider list too"Microsoft-ServiceFabric:4:0x4000000000000020".</span></span>
<span data-ttu-id="d7f33-174">Azure Service Fabric kümeleri için hello resource manager şablonu tooinclude değiştirme</span><span class="sxs-lookup"><span data-stu-id="d7f33-174">For Azure Service Fabric clusters, modify hello resource manager template tooinclude</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387936",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```
> <span data-ttu-id="d7f33-175">Bu tüm trafiğini hello ters proxy üzerinden toplar ve depolama kapasitesini hızlıca tüketebileceği toojudiciously etkinleştir toplama olayları bu kanal önerilir.</span><span class="sxs-lookup"><span data-stu-id="d7f33-175">It is recommended toojudiciously enable collecting events from this channel as this collects all traffic through hello reverse proxy and can quickly consume storage capacity.</span></span>

<span data-ttu-id="d7f33-176">Azure Service Fabric kümeleri için tüm hello düğümlerinden hello olayları toplanır ve hello SystemEventTable bir araya getirilir.</span><span class="sxs-lookup"><span data-stu-id="d7f33-176">For Azure Service Fabric clusters, hello events from all hello nodes are collected and aggregated in hello SystemEventTable.</span></span>
<span data-ttu-id="d7f33-177">Ayrıntılı Hello ters proxy olaylarını sorun giderme için hello başvuran [ters proxy tanılama Kılavuzu](service-fabric-reverse-proxy-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="d7f33-177">For detailed troubleshooting of hello reverse proxy events, refer hello [reverse proxy diagnostics guide](service-fabric-reverse-proxy-diagnostics.md).</span></span>

## <a name="collect-from-new-eventsource-channels"></a><span data-ttu-id="d7f33-178">Yeni EventSource kanaldan Topla</span><span class="sxs-lookup"><span data-stu-id="d7f33-178">Collect from new EventSource channels</span></span>

<span data-ttu-id="d7f33-179">tooupdate tanılama toocollect toodeploy hakkında olduğunuz yeni bir uygulama temsil eden yeni EventSource kanallar günlüklerinden tanılama hello Kurulum var olan bir küme için için aynı adımları daha önce açıklandığı gibi hello gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="d7f33-179">tooupdate Diagnostics toocollect logs from new EventSource channels that represent a new application that you're about toodeploy, perform hello same steps as previously described for hello setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="d7f33-180">Merhaba güncelleştirme `EtwEventSourceProviderConfiguration` hello kullanarak hello yapılandırma uygulamadan önce hello yeni EventSource kanallar güncelleştirmek için hello template.json dosyasını tooadd girişlerinde bölümünde `New-AzureRmResourceGroupDeployment` PowerShell komutu.</span><span class="sxs-lookup"><span data-stu-id="d7f33-180">Update hello `EtwEventSourceProviderConfiguration` section in hello template.json file tooadd entries for hello new EventSource channels before you apply hello configuration update by using hello `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="d7f33-181">Merhaba olay kaynağı Hello adını hello ServiceEventSource.cs Visual Studio tarafından oluşturulan dosya kodunuzda bir parçası olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="d7f33-181">hello name of hello event source is defined as part of your code in hello Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="d7f33-182">Olay kaynağı Eventsource My olarak adlandırılmışsa, örneğin, kod tooplace hello olayları Eventsource My MyDestinationTableName adlı bir tabloya aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d7f33-182">For example, if your event source is named My-Eventsource, add hello following code tooplace hello events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="d7f33-183">toocollect performans sayaçlarını veya olay günlükleri, değişiklik hello Resource Manager şablonu sağlanan hello örnekleri kullanarak [bir Azure Resource Manager şablonukullanılarakizlemeveTanılamaileWindowssanalmakineoluşturma](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d7f33-183">toocollect performance counters or event logs, modify hello Resource Manager template by using hello examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="d7f33-184">Ardından, hello Resource Manager şablonunu yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="d7f33-184">Then, republish hello Resource Manager template.</span></span>

## <a name="collect-performance-counters"></a><span data-ttu-id="d7f33-185">Performans sayaçlarını Topla</span><span class="sxs-lookup"><span data-stu-id="d7f33-185">Collect Performance Counters</span></span>

<span data-ttu-id="d7f33-186">Kümenizde toocollect performans ölçümleri kümenizin hello Resource Manager şablonunda hello performans sayaçları tooyour "WadCfg > DiagnosticMonitorConfiguration" ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d7f33-186">toocollect performance metrics from your cluster, add hello performance counters tooyour "WadCfg > DiagnosticMonitorConfiguration" in hello Resource Manager template for your cluster.</span></span> <span data-ttu-id="d7f33-187">Bkz: [Service Fabric performans sayaçları](service-fabric-diagnostics-event-generation-perf.md) performans sayaçları için toplama öneririz.</span><span class="sxs-lookup"><span data-stu-id="d7f33-187">See [Service Fabric Performance Counters](service-fabric-diagnostics-event-generation-perf.md) for performance counters that we recommend collecting.</span></span>

<span data-ttu-id="d7f33-188">Örneğin, burada örneklenen 15 dakikada bir performans sayacı ayarlarız (Bu değiştirilebilir ve aşağıdaki biçimi hello "PT\<zaman >\<birim >", PT3M üç dakikalık aralıklarla Örneğin, örnek) ve toohello aktarıldı uygun depolama tablo her bir dakika.</span><span class="sxs-lookup"><span data-stu-id="d7f33-188">For example, here we set one performance counter, sampled every 15 seconds (this can be changed and follows hello format of "PT\<time>\<unit>", for example, PT3M would sample at three minute intervals), and transferred toohello appropriate storage table every one minute.</span></span>

  ```json
  "PerformanceCounters": {
      "scheduledTransferPeriod": "PT1M",
      "PerformanceCounterConfiguration": [
          {
              "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
              "sampleRate": "PT15S",
              "unit": "Percent",
              "annotation": [
              ],
              "sinks": ""
          }
      ]
  }
  ```
  
<span data-ttu-id="d7f33-189">Application Insights havuz hello aşağıdaki bölümde açıklandığı gibi kullanıyorsanız ve bu ölçümleri tooshow Application Insights'ta istediğiniz, emin tooadd hello havuz adı yukarıda gösterildiği gibi hello "havuzlarını" bölümünde olun.</span><span class="sxs-lookup"><span data-stu-id="d7f33-189">If you are using an Application Insights sink, as described in hello section below, and want these metrics tooshow up in Application Insights, then make sure tooadd hello sink name in hello "sinks" section as shown above.</span></span> <span data-ttu-id="d7f33-190">Bunlar hello yönelik kitle olmayan şekilde Ayrıca, performans sayaçları için ayrı bir tablo toosend oluşturmayı düşünün gelen veri hello etkinleştirdiğiniz diğer günlük kanalları.</span><span class="sxs-lookup"><span data-stu-id="d7f33-190">Additionally, consider creating a separate table toosend your Performance Counters to, so they don't crowd out hello data coming from hello other logging channels you have enabled.</span></span>


## <a name="send-logs-tooapplication-insights"></a><span data-ttu-id="d7f33-191">Gönderme tooApplication Öngörüler günlüğe kaydeder</span><span class="sxs-lookup"><span data-stu-id="d7f33-191">Send logs tooApplication Insights</span></span>

<span data-ttu-id="d7f33-192">İzleme ve tanılama veri tooApplication Öngörüler (AI) gönderme hello WAD yapılandırmasının bir parçası yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="d7f33-192">Sending monitoring and diagnostics data tooApplication Insights (AI) can be done as part of hello WAD configuration.</span></span> <span data-ttu-id="d7f33-193">Olay çözümleme ve görselleştirme için AI toouse karar verirseniz, okuma [olay çözümleme ve görselleştirme Application Insights ile](service-fabric-diagnostics-event-analysis-appinsights.md) tooset AI havuz, "WadCfg" nın bir parçası olarak ayarlama.</span><span class="sxs-lookup"><span data-stu-id="d7f33-193">If you decide toouse AI for event analysis and visualization, read [Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tooset up an AI Sink as part of your "WadCfg".</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7f33-194">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d7f33-194">Next steps</span></span>

<span data-ttu-id="d7f33-195">Azure tanılama doğru şekilde yapılandırdıktan sonra hello ETW ve EventSource günlükler, depolama tablolardaki verileri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d7f33-195">Once you have correctly configured Azure diagnostics, you will see data in your Storage tables from hello ETW and EventSource logs.</span></span> <span data-ttu-id="d7f33-196">Toouse OMS seçerseniz, Kibana ya da doğrudan hello Resource Manager şablonunda yapılandırılmamış başka bir veri analizi ve görselleştirme platform olun, seçim tooread hello platformunu oluşturan emin tooset bu depolama tablolardan hello verilerdeki.</span><span class="sxs-lookup"><span data-stu-id="d7f33-196">If you choose toouse OMS, Kibana, or any other data analytics and visualization platform that is not directly configured in hello Resource Manager template, make sure tooset up hello platform of your choice tooread in hello data from these storage tables.</span></span> <span data-ttu-id="d7f33-197">Bunu yapmak için OMS görece önemsiz ve içinde açıklanan [OMS olay ve Günlük çözümlemesi](service-fabric-diagnostics-event-analysis-oms.md).</span><span class="sxs-lookup"><span data-stu-id="d7f33-197">Doing this for OMS is relatively trivial, and is explained in [Event and log analysis through OMS](service-fabric-diagnostics-event-analysis-oms.md).</span></span> <span data-ttu-id="d7f33-198">Application Insights biraz bu bağlamda bir özel durum, hello tanılama uzantı yapılandırmasını bir parçası olarak yapılandırıldıktan sonra bu nedenle toohello başvuran [uygun makale](service-fabric-diagnostics-event-analysis-appinsights.md) toouse AI seçerseniz.</span><span class="sxs-lookup"><span data-stu-id="d7f33-198">Application Insights is a bit of a special case in this sense, since it can be configured as part of hello Diagnostics extension configuration, so refer toohello [appropriate article](service-fabric-diagnostics-event-analysis-appinsights.md) if you choose toouse AI.</span></span>

>[!NOTE]
><span data-ttu-id="d7f33-199">Şu anda toohello tablo gönderilen yolu toofilter veya Temizle hello olayı yok.</span><span class="sxs-lookup"><span data-stu-id="d7f33-199">There is currently no way toofilter or groom hello events that are sent toohello table.</span></span> <span data-ttu-id="d7f33-200">Bir işlem tooremove olaylarını hello tablosundan uygularsanız yok hello tablo toogrow devam eder.</span><span class="sxs-lookup"><span data-stu-id="d7f33-200">If you don't implement a process tooremove events from hello table, hello table will continue toogrow.</span></span> <span data-ttu-id="d7f33-201">Şu anda hello çalışan bir veri temizleme hizmet örneği yoktur [izleme örnek](https://github.com/Azure-Samples/service-fabric-watchdog-service), ve olmadığı sürece, 30 veya 90 günlük süre toostore kaydettiği iyi nedeni için kendiniz bir tane de yazma önerilir.</span><span class="sxs-lookup"><span data-stu-id="d7f33-201">Currently, there is an example of a data grooming service running in hello [Watchdog sample](https://github.com/Azure-Samples/service-fabric-watchdog-service), and it is recommended that you write one for yourself as well, unless there is a good reason for you toostore logs beyond a 30 or 90 day timeframe.</span></span>

* [<span data-ttu-id="d7f33-202">Tanılama uzantısını toocollect performans sayaçlarını veya kullanarak günlükleri nasıl hello öğrenin</span><span class="sxs-lookup"><span data-stu-id="d7f33-202">Learn how toocollect performance counters or logs by using hello Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="d7f33-203">Olay çözümleme ve görselleştirme Application Insights ile</span><span class="sxs-lookup"><span data-stu-id="d7f33-203">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="d7f33-204">Olay çözümleme ve OMS Görselleştirme</span><span class="sxs-lookup"><span data-stu-id="d7f33-204">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)