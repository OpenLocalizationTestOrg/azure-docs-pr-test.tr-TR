---
title: "Windows Azure Service Fabric olay toplama Azure tanılama | Microsoft Docs"
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
ms.openlocfilehash: 5773361fdec4cb8ee54fa2856f6aa969d5dac4e9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a><span data-ttu-id="06a21-103">Olay toplama ve Windows Azure Tanılama'yı kullanarak koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="06a21-103">Event aggregation and collection using Windows Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="06a21-104">Windows</span><span class="sxs-lookup"><span data-stu-id="06a21-104">Windows</span></span>](service-fabric-diagnostics-event-aggregation-wad.md)
> * [<span data-ttu-id="06a21-105">Linux</span><span class="sxs-lookup"><span data-stu-id="06a21-105">Linux</span></span>](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

<span data-ttu-id="06a21-106">Azure Service Fabric kümesi çalıştırırken, merkezi bir konumda tüm düğümlerdeki günlükleri toplamak için iyi bir fikirdir.</span><span class="sxs-lookup"><span data-stu-id="06a21-106">When you're running an Azure Service Fabric cluster, it's a good idea to collect the logs from all the nodes in a central location.</span></span> <span data-ttu-id="06a21-107">Merkezi bir konumda günlükler sahip çözümlemek ve sorunları kümenizdeki veya bu kümede çalışan hizmetler ve uygulamalar sorunları gidermenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="06a21-107">Having the logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in the applications and services running in that cluster.</span></span>

<span data-ttu-id="06a21-108">Karşıya yükleme ve günlükleri toplamak için bir yol günlükleri Azure Storage'a yükler ve ayrıca Azure Application Insights veya olay hub'ları için günlükleri gönderme seçeneği içeren Windows Azure tanılama (WAD) uzantısı kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="06a21-108">One way to upload and collect logs is to use the Windows Azure Diagnostics (WAD) extension, which uploads logs to Azure Storage, and also has the option to send logs to Azure Application Insights or Event Hubs.</span></span> <span data-ttu-id="06a21-109">Olayları depolama alanından okuyun ve bunları bir analiz platformu üründe gibi yerleştirmek için bir dış işlem kullanabilirsiniz [OMS günlük analizi](../log-analytics/log-analytics-service-fabric.md) veya başka bir çözüm günlük ayrıştırma.</span><span class="sxs-lookup"><span data-stu-id="06a21-109">You can also use an external process to read the events from storage and place them in an analysis platform product, such as [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06a21-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="06a21-110">Prerequisites</span></span>
<span data-ttu-id="06a21-111">Bu araçlar, bu belgede bazı işlemleri gerçekleştirmek için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="06a21-111">These tools are used to perform some of the operations in this document:</span></span>

* <span data-ttu-id="06a21-112">[Azure tanılama](../cloud-services/cloud-services-dotnet-diagnostics.md) (Azure bulut Hizmetleri ile ilgili ancak iyi bilgi ve örnekler var)</span><span class="sxs-lookup"><span data-stu-id="06a21-112">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related to Azure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="06a21-113">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="06a21-113">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="06a21-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="06a21-114">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="06a21-115">Azure Resource Manager istemci</span><span class="sxs-lookup"><span data-stu-id="06a21-115">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="06a21-116">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="06a21-116">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a><span data-ttu-id="06a21-117">Günlük ve olay kaynakları</span><span class="sxs-lookup"><span data-stu-id="06a21-117">Log and event sources</span></span>

### <a name="service-fabric-platform-events"></a><span data-ttu-id="06a21-118">Service Fabric platform olayları</span><span class="sxs-lookup"><span data-stu-id="06a21-118">Service Fabric platform events</span></span>
<span data-ttu-id="06a21-119">' Da anlatıldığı gibi [bu makalede](service-fabric-diagnostics-event-generation-infra.md), Service Fabric ayarlayan, hangisinin aşağıdaki kanallar kolayca yapılandırılır izleme göndermek için WAD ve tanılama verilerini depolama tabloya birkaç Giden kutusu günlük kanallar ile veya başka bir yerde:</span><span class="sxs-lookup"><span data-stu-id="06a21-119">As discussed in [this article](service-fabric-diagnostics-event-generation-infra.md), Service Fabric sets you up with a few out-of-the-box logging channels, of which the following channels are easily configured with WAD to send monitoring and diagnostics data to a storage table or elsewhere:</span></span>
  * <span data-ttu-id="06a21-120">Çalışma olaylarını: Service Fabric platformundan gerçekleştirir üst düzey işlem.</span><span class="sxs-lookup"><span data-stu-id="06a21-120">Operational events: higher-level operations that the Service Fabric platform performs.</span></span> <span data-ttu-id="06a21-121">Örnek uygulamalar ve hizmetler, düğüm durumu değişiklikleri ve yükseltme bilgileri oluşturulmasını verilebilir.</span><span class="sxs-lookup"><span data-stu-id="06a21-121">Examples include creation of applications and services, node state changes, and upgrade information.</span></span> <span data-ttu-id="06a21-122">Bu olay için Windows izleme (ETW) günlükleri olarak gösterilen</span><span class="sxs-lookup"><span data-stu-id="06a21-122">These are emitted as Event Tracing for Windows (ETW) logs</span></span>
  * [<span data-ttu-id="06a21-123">Reliable Actors programlama modelini olayları</span><span class="sxs-lookup"><span data-stu-id="06a21-123">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="06a21-124">Programlama modeli olaylarının güvenilir hizmetler</span><span class="sxs-lookup"><span data-stu-id="06a21-124">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a><span data-ttu-id="06a21-125">Uygulama olayları</span><span class="sxs-lookup"><span data-stu-id="06a21-125">Application events</span></span>
 <span data-ttu-id="06a21-126">Uygulamaların ve hizmetlerin koddan yayılan ve Visual Studio şablonları sağlanan EventSource yardımcı sınıfı kullanılarak yazılan olaylar.</span><span class="sxs-lookup"><span data-stu-id="06a21-126">Events emitted from your applications' and services' code and written out by using the EventSource helper class provided in the Visual Studio templates.</span></span> <span data-ttu-id="06a21-127">EventSource günlüklerine uygulamanızdan yazma hakkında daha fazla bilgi için bkz: [İzleyici ve yerel makine geliştirme Kurulum Hizmetleri'nde tanılamak](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="06a21-127">For more information on how to write EventSource logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-the-diagnostics-extension"></a><span data-ttu-id="06a21-128">Tanılama uzantısını dağıtma</span><span class="sxs-lookup"><span data-stu-id="06a21-128">Deploy the Diagnostics extension</span></span>
<span data-ttu-id="06a21-129">Günlükleri toplamayı ilk adımı, Service Fabric kümesindeki VM'lerin her birinde tanılama uzantısını dağıtmaktır.</span><span class="sxs-lookup"><span data-stu-id="06a21-129">The first step in collecting logs is to deploy the Diagnostics extension on each of the VMs in the Service Fabric cluster.</span></span> <span data-ttu-id="06a21-130">Tanılama uzantısını her VM günlükleri toplar ve bunları belirttiğiniz depolama hesabı yükler.</span><span class="sxs-lookup"><span data-stu-id="06a21-130">The Diagnostics extension collects logs on each VM and uploads them to the storage account that you specify.</span></span> <span data-ttu-id="06a21-131">Adımlar Azure portalında veya Azure Resource Manager kullanıp biraz göre farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="06a21-131">The steps vary a little based on whether you use the Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="06a21-132">Adımlar ayrıca dağıtım küme oluşturmanın bir parçası değil veya zaten bir küme için göre değişir.</span><span class="sxs-lookup"><span data-stu-id="06a21-132">The steps also vary based on whether the deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="06a21-133">Her senaryo için adımları bakalım.</span><span class="sxs-lookup"><span data-stu-id="06a21-133">Let's look at the steps for each scenario.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a><span data-ttu-id="06a21-134">Azure portal ile küme oluşturma bir parçası olarak tanılama uzantısını dağıtma</span><span class="sxs-lookup"><span data-stu-id="06a21-134">Deploy the Diagnostics extension as part of cluster creation through Azure portal</span></span>
<span data-ttu-id="06a21-135">Tanılama uzantısını kümedeki sanal makineleri küme oluşturmanın bir parçası dağıtmak için tanılama Ayarları panelini kullanın. aşağıdaki görüntüde - gösterilen tanılama ayarlandığından emin olun **üzerinde** (varsayılan ayar).</span><span class="sxs-lookup"><span data-stu-id="06a21-135">To deploy the Diagnostics extension to the VMs in the cluster as part of cluster creation, you use the Diagnostics settings panel shown in the following image - ensure that Diagnostics is set to **On** (the default setting).</span></span> <span data-ttu-id="06a21-136">Kümeyi oluşturduktan sonra portal kullanarak bu ayarları değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="06a21-136">After you create the cluster, you can't change these settings by using the portal.</span></span>

![Küme oluşturma için Portalı'nda Azure tanılama ayarları](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

<span data-ttu-id="06a21-138">Portalı kullanarak bir küme oluştururken, şablonu indirme öneririz **Tamam'ı tıklatmadan önce** küme oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="06a21-138">When you're creating a cluster by using the portal, we highly recommend that you download the template **before you click OK** to create the cluster.</span></span> <span data-ttu-id="06a21-139">Ayrıntılar için başvurmak [bir Azure Resource Manager şablonu kullanarak bir Service Fabric kümesi ayarlayın](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="06a21-139">For details, refer to [Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="06a21-140">Portalı kullanarak bazı değişiklik yapılamıyor çünkü daha sonra değişiklikler yapmak için şablonu gerekir.</span><span class="sxs-lookup"><span data-stu-id="06a21-140">You'll need the template to make changes later, because you can't make some changes by using the portal.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="06a21-141">Azure Kaynak Yöneticisi'ni kullanarak küme oluşturmanın bir parçası olarak tanılama uzantısını dağıtma</span><span class="sxs-lookup"><span data-stu-id="06a21-141">Deploy the Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="06a21-142">Kaynak Yöneticisi'ni kullanarak bir küme oluşturmak için küme oluşturmadan önce tam küme Resource Manager şablonu JSON tanılama yapılandırması eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="06a21-142">To create a cluster by using Resource Manager, you need to add the Diagnostics configuration JSON to the full cluster Resource Manager template before you create the cluster.</span></span> <span data-ttu-id="06a21-143">Resource Manager şablonu örneklerimizi parçası olarak eklenecek tanılama yapılandırması içeren bir örnek beş VM küme Resource Manager şablonu sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="06a21-143">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added to it as part of our Resource Manager template samples.</span></span> <span data-ttu-id="06a21-144">Azure Örnekler Galerisi bu konumda bkz: [beş düğümlü kümeyi tanılama Resource Manager şablonu örneği ile](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span><span class="sxs-lookup"><span data-stu-id="06a21-144">You can see it at this location in the Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span></span>

<span data-ttu-id="06a21-145">Resource Manager şablonu tanılama ayarında görmek için azuredeploy.json dosyasını açın ve arama **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="06a21-145">To see the Diagnostics setting in the Resource Manager template, open the azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="06a21-146">Bu şablonu kullanarak bir küme oluşturmak için seçin **Azure'a Dağıt** düğmesini önceki bağlantıda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="06a21-146">To create a cluster by using this template, select the **Deploy to Azure** button available at the previous link.</span></span>

<span data-ttu-id="06a21-147">Alternatif olarak, Resource Manager örnek indirebilir, değişiklik ve kullanarak bir küme ile değiştirilen şablon oluşturma `New-AzureRmResourceGroupDeployment` bir Azure PowerShell penceresinde komutu.</span><span class="sxs-lookup"><span data-stu-id="06a21-147">Alternatively, you can download the Resource Manager sample, make changes to it, and create a cluster with the modified template by using the `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="06a21-148">Aşağıdaki kod, komuta geçirdiğiniz parametreler için bkz.</span><span class="sxs-lookup"><span data-stu-id="06a21-148">See the following code for the parameters that you pass in to the command.</span></span> <span data-ttu-id="06a21-149">PowerShell kullanarak bir kaynak grubu dağıtma hakkında ayrıntılı bilgi için bkz: [Azure Resource Manager şablonu ile bir kaynak grubu dağıtma](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="06a21-149">For detailed information on how to deploy a resource group by using PowerShell, see the article [Deploy a resource group with the Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

### <a name="deploy-the-diagnostics-extension-to-an-existing-cluster"></a><span data-ttu-id="06a21-150">Varolan bir kümeye tanılama uzantısını dağıtma</span><span class="sxs-lookup"><span data-stu-id="06a21-150">Deploy the Diagnostics extension to an existing cluster</span></span>
<span data-ttu-id="06a21-151">Dağıtılan tanılama yok varolan bir kümeye varsa veya var olan yapılandırmasını değiştirmek istiyorsanız, ekleyebilir veya güncelleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="06a21-151">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want to modify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="06a21-152">Var olan küme oluşturmak veya daha önce açıklandığı gibi portaldan şablonu karşıdan yüklemek için kullanılan Resource Manager şablonu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="06a21-152">Modify the Resource Manager template that's used to create the existing cluster or download the template from the portal as described earlier.</span></span> <span data-ttu-id="06a21-153">Aşağıdaki görevleri gerçekleştirerek template.json dosyasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="06a21-153">Modify the template.json file by performing the following tasks.</span></span>

<span data-ttu-id="06a21-154">Yeni bir depolama kaynağı kaynaklar bölümüne ekleyerek şablonuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="06a21-154">Add a new storage resource to the template by adding to the resources section.</span></span>

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

 <span data-ttu-id="06a21-155">Ardından, parametreleri bölüme yalnızca depolama hesabı tanımlarını sonra arasında eklemek `supportLogStorageAccountName` ve `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="06a21-155">Next, add to the parameters section just after the storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="06a21-156">Yer tutucu metni değiştirmek *depolama hesabı adı buraya* depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="06a21-156">Replace the placeholder text *storage account name goes here* with the name of the storage account.</span></span>

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for the application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for the storage account that contains application diagnostics data from the cluster"
      }
    },
```
<span data-ttu-id="06a21-157">Ardından, güncelleştirme `VirtualMachineProfile` uzantıları dizi içinde aşağıdaki kodu ekleyerek template.json dosyasının bölümü.</span><span class="sxs-lookup"><span data-stu-id="06a21-157">Then, update the `VirtualMachineProfile` section of the template.json file by adding the following code within the extensions array.</span></span> <span data-ttu-id="06a21-158">Başında veya burada eklenen bağlı olarak bitiş virgül eklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="06a21-158">Be sure to add a comma at the beginning or the end, depending on where it's inserted.</span></span>

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

<span data-ttu-id="06a21-159">Template.json dosyasını açıklandığı şekilde değiştirdikten sonra Resource Manager şablonunu yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="06a21-159">After you modify the template.json file as described, republish the Resource Manager template.</span></span> <span data-ttu-id="06a21-160">Şablonu dışarı aktarılmışsa deploy.ps1 dosyasını çalıştıran şablonu yeniden yayımlar.</span><span class="sxs-lookup"><span data-stu-id="06a21-160">If the template was exported, running the deploy.ps1 file republishes the template.</span></span> <span data-ttu-id="06a21-161">Dağıttıktan sonra emin **ProvisioningState** olan **başarılı**.</span><span class="sxs-lookup"><span data-stu-id="06a21-161">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="collect-health-and-load-events"></a><span data-ttu-id="06a21-162">Sistem durumu toplama ve olayları yükleme</span><span class="sxs-lookup"><span data-stu-id="06a21-162">Collect health and load events</span></span>

<span data-ttu-id="06a21-163">Service Fabric 5.4 sürümünden itibaren sistem durumu ve yük ölçüm olayları koleksiyonu için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="06a21-163">Starting with the 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="06a21-164">Bu olaylar Sistem kullanarak sistem veya kodunuzu tarafından oluşturulan olayları yansıtmak veya Raporlama API'leri gibi yük [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) veya [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="06a21-164">These events reflect events generated by the system or your code by using the health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="06a21-165">Bu, toplama ve zaman içinde sistem durumu görüntüleme ve sistem durumu veya yük olaylara dayanarak uyarı verme sağlar.</span><span class="sxs-lookup"><span data-stu-id="06a21-165">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="06a21-166">Visual Studio'nun Tanılama Olay Görüntüleyicisi'nde bu olayları görüntülemek için Ekle "Microsoft-ServiceFabric:4:0x4000000000000008" ETW sağlayıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="06a21-166">To view these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" to the list of ETW providers.</span></span>

<span data-ttu-id="06a21-167">Olaylarını toplamak için dahil etmek için Resource Manager şablonu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="06a21-167">To collect the events, modify the Resource Manager template to include</span></span>

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

## <a name="collect-reverse-proxy-events"></a><span data-ttu-id="06a21-168">Ters proxy olaylarını Topla</span><span class="sxs-lookup"><span data-stu-id="06a21-168">Collect reverse proxy events</span></span>

<span data-ttu-id="06a21-169">Service Fabric 5.7 sürümünden başlayarak [ters proxy](service-fabric-reverseproxy.md) olayları koleksiyonu için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="06a21-169">Starting with the 5.7 release of Service Fabric, [reverse proxy](service-fabric-reverseproxy.md) events are available for collection.</span></span>
<span data-ttu-id="06a21-170">Ters proxy olayları bir istek hataları ve tüm istekler hakkında ayrıntılı olayları içeren başka bir işleme yansıtarak içeren hata olayları ters proxy işlenen iki kanalı halinde yayar.</span><span class="sxs-lookup"><span data-stu-id="06a21-170">Reverse proxy emits events into two channels, one containing error events reflecting request processing failures and the other one containing verbose events about all the requests processed at the reverse proxy.</span></span> 

1. <span data-ttu-id="06a21-171">Hatası olaylarını Topla: görüntülemek için bu olayları Visual Studio'nun Tanılama Olay Görüntüleyicisi'nde Ekle "Microsoft-ServiceFabric:4:0x4000000000000010" ETW sağlayıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="06a21-171">Collect error events: To view these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000010" to the list of ETW providers.</span></span>
<span data-ttu-id="06a21-172">Azure kümelerdeki olaylarını toplamak için dahil etmek için Resource Manager şablonu değiştirin</span><span class="sxs-lookup"><span data-stu-id="06a21-172">To collect the events from Azure clusters, modify the Resource Manager template to include</span></span>

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

2. <span data-ttu-id="06a21-173">Toplama tüm olayları işlemeyi istek: içinde Visual Studio'nun Tanılama Olay Görüntüleyicisi'ni ETW sağlayıcı listesine güncelleştirme Microsoft ServiceFabric girişinde "Microsoft-ServiceFabric:4:0x4000000000000020".</span><span class="sxs-lookup"><span data-stu-id="06a21-173">Collect all request processing events: In Visual Studio's Diagnostic Event Viewer, update the Microsoft-ServiceFabric entry in the ETW provider list to "Microsoft-ServiceFabric:4:0x4000000000000020".</span></span>
<span data-ttu-id="06a21-174">Azure Service Fabric kümeleri için dahil etmek için resource manager şablonu değiştirme</span><span class="sxs-lookup"><span data-stu-id="06a21-174">For Azure Service Fabric clusters, modify the resource manager template to include</span></span>

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
> <span data-ttu-id="06a21-175">Bu ters proxy aracılığıyla tüm trafiği toplar ve depolama kapasitesini hızlıca tüketebileceği gibi bu kanal toplama olaylarından dikkatli etkinleştirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="06a21-175">It is recommended to judiciously enable collecting events from this channel as this collects all traffic through the reverse proxy and can quickly consume storage capacity.</span></span>

<span data-ttu-id="06a21-176">Azure Service Fabric kümeleri için tüm düğümler olaylardan toplanır ve SystemEventTable bir araya getirilir.</span><span class="sxs-lookup"><span data-stu-id="06a21-176">For Azure Service Fabric clusters, the events from all the nodes are collected and aggregated in the SystemEventTable.</span></span>
<span data-ttu-id="06a21-177">Ayrıntılı ters proxy olaylarını sorun giderme için başvuruda [ters proxy tanılama Kılavuzu](service-fabric-reverse-proxy-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="06a21-177">For detailed troubleshooting of the reverse proxy events, refer the [reverse proxy diagnostics guide](service-fabric-reverse-proxy-diagnostics.md).</span></span>

## <a name="collect-from-new-eventsource-channels"></a><span data-ttu-id="06a21-178">Yeni EventSource kanaldan Topla</span><span class="sxs-lookup"><span data-stu-id="06a21-178">Collect from new EventSource channels</span></span>

<span data-ttu-id="06a21-179">Yeni bir uygulama, olduğunuz hakkında dağıtmak için gerçekleştirmenizi aynı temsil eden yeni EventSource kanaldan günlükleri toplamak için tanılama güncelleştirmek için varolan bir tanılama kurulumu için daha önce açıklanan adımları küme.</span><span class="sxs-lookup"><span data-stu-id="06a21-179">To update Diagnostics to collect logs from new EventSource channels that represent a new application that you're about to deploy, perform the same steps as previously described for the setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="06a21-180">Güncelleştirme `EtwEventSourceProviderConfiguration` yapılandırma uygulamadan önce yeni EventSource kanalları kullanarak güncelleştirmek için girdileri eklemek için template.json dosyasını bölümünde `New-AzureRmResourceGroupDeployment` PowerShell komutu.</span><span class="sxs-lookup"><span data-stu-id="06a21-180">Update the `EtwEventSourceProviderConfiguration` section in the template.json file to add entries for the new EventSource channels before you apply the configuration update by using the `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="06a21-181">Olay kaynağı adı, kodunuz Visual Studio tarafından oluşturulan ServiceEventSource.cs dosyasındaki bir parçası olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="06a21-181">The name of the event source is defined as part of your code in the Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="06a21-182">Örneğin, olay kaynağı Eventsource My adlandırılmışsa Eventsource My olayların MyDestinationTableName adlı bir tabloya yerleştirmek için aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="06a21-182">For example, if your event source is named My-Eventsource, add the following code to place the events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="06a21-183">Performans sayaçlarını veya olayları toplamak için Resource Manager şablonu sağlanan örnekler kullanarak değiştirme [bir Azure Resource Manager şablonu kullanarak bir Windows sanal makine izleme ve tanılama oluşturmak](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="06a21-183">To collect performance counters or event logs, modify the Resource Manager template by using the examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="06a21-184">Ardından, Resource Manager şablonunu yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="06a21-184">Then, republish the Resource Manager template.</span></span>

## <a name="collect-performance-counters"></a><span data-ttu-id="06a21-185">Performans sayaçlarını Topla</span><span class="sxs-lookup"><span data-stu-id="06a21-185">Collect Performance Counters</span></span>

<span data-ttu-id="06a21-186">Kümenizden performans ölçümlerini derleme için "WadCfg > DiagnosticMonitorConfiguration" kümeniz için Resource Manager şablonunda performans sayaçları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="06a21-186">To collect performance metrics from your cluster, add the performance counters to your "WadCfg > DiagnosticMonitorConfiguration" in the Resource Manager template for your cluster.</span></span> <span data-ttu-id="06a21-187">Bkz: [Service Fabric performans sayaçları](service-fabric-diagnostics-event-generation-perf.md) performans sayaçları için toplama öneririz.</span><span class="sxs-lookup"><span data-stu-id="06a21-187">See [Service Fabric Performance Counters](service-fabric-diagnostics-event-generation-perf.md) for performance counters that we recommend collecting.</span></span>

<span data-ttu-id="06a21-188">Örneğin, burada örneklenen 15 dakikada bir performans sayacı ayarlarız (Bu değiştirilebilir ve biçimi izler "PT\<zaman >\<birim >", örneğin, PT3M üç dakikalık aralıklarla örnek) ve aktarılan için uygun depolama tablo her bir dakika.</span><span class="sxs-lookup"><span data-stu-id="06a21-188">For example, here we set one performance counter, sampled every 15 seconds (this can be changed and follows the format of "PT\<time>\<unit>", for example, PT3M would sample at three minute intervals), and transferred to the appropriate storage table every one minute.</span></span>

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
  
<span data-ttu-id="06a21-189">Aşağıdaki bölümde açıklandığı gibi bir Application Insights havuz kullanıyorsanız ve bu ölçümleri Application Insights'ta gösterilmesini istiyorsanız sonra yukarıda gösterildiği gibi "havuzlarını" bölümünde havuz adı eklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="06a21-189">If you are using an Application Insights sink, as described in the section below, and want these metrics to show up in Application Insights, then make sure to add the sink name in the "sinks" section as shown above.</span></span> <span data-ttu-id="06a21-190">Ayrıca, bunlar etkinleştirdiğiniz diğer günlük kanaldan gelen veriler kullanıma yönelik kitle olmayan şekilde, performans sayaçları için göndermek için ayrı bir tablo oluşturmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="06a21-190">Additionally, consider creating a separate table to send your Performance Counters to, so they don't crowd out the data coming from the other logging channels you have enabled.</span></span>


## <a name="send-logs-to-application-insights"></a><span data-ttu-id="06a21-191">Günlükleri Application Insights'a gönderme</span><span class="sxs-lookup"><span data-stu-id="06a21-191">Send logs to Application Insights</span></span>

<span data-ttu-id="06a21-192">Uygulama Öngörüler (AI) izleme ve Tanılama verileri gönderme WAD yapılandırmasının bir parçası yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="06a21-192">Sending monitoring and diagnostics data to Application Insights (AI) can be done as part of the WAD configuration.</span></span> <span data-ttu-id="06a21-193">Olay çözümleme ve görselleştirme için AI kullanmaya karar verirseniz, okuma [olay çözümleme ve görselleştirme Application Insights ile](service-fabric-diagnostics-event-analysis-appinsights.md) , "WadCfg" bir parçası olarak bir AI havuzunu kurmak için.</span><span class="sxs-lookup"><span data-stu-id="06a21-193">If you decide to use AI for event analysis and visualization, read [Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) to set up an AI Sink as part of your "WadCfg".</span></span>

## <a name="next-steps"></a><span data-ttu-id="06a21-194">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="06a21-194">Next steps</span></span>

<span data-ttu-id="06a21-195">Azure tanılama doğru şekilde yapılandırdıktan sonra ETW ve EventSource günlüklerinden, depolama tablolardaki verileri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="06a21-195">Once you have correctly configured Azure diagnostics, you will see data in your Storage tables from the ETW and EventSource logs.</span></span> <span data-ttu-id="06a21-196">OMS, Kibana veya doğrudan Resource Manager şablonunda yapılandırılmamış başka bir veri analizi ve görselleştirme platform kullanmayı seçerseniz, bu depolama tablolardaki verileri okumak için seçtiğiniz platform ayarlamak emin olun.</span><span class="sxs-lookup"><span data-stu-id="06a21-196">If you choose to use OMS, Kibana, or any other data analytics and visualization platform that is not directly configured in the Resource Manager template, make sure to set up the platform of your choice to read in the data from these storage tables.</span></span> <span data-ttu-id="06a21-197">Bunu yapmak için OMS görece önemsiz ve içinde açıklanan [OMS olay ve Günlük çözümlemesi](service-fabric-diagnostics-event-analysis-oms.md).</span><span class="sxs-lookup"><span data-stu-id="06a21-197">Doing this for OMS is relatively trivial, and is explained in [Event and log analysis through OMS](service-fabric-diagnostics-event-analysis-oms.md).</span></span> <span data-ttu-id="06a21-198">Application Insights biraz bu bağlamda bir özel durum, bu nedenle başvurmak tanılama uzantı yapılandırmasını bir parçası olarak yapılandırıldıktan sonra [uygun makale](service-fabric-diagnostics-event-analysis-appinsights.md) AI kullanmayı tercih ederseniz.</span><span class="sxs-lookup"><span data-stu-id="06a21-198">Application Insights is a bit of a special case in this sense, since it can be configured as part of the Diagnostics extension configuration, so refer to the [appropriate article](service-fabric-diagnostics-event-analysis-appinsights.md) if you choose to use AI.</span></span>

>[!NOTE]
><span data-ttu-id="06a21-199">Şu anda filtre veya tabloya gönderilen olaylar bölümlendirmek mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="06a21-199">There is currently no way to filter or groom the events that are sent to the table.</span></span> <span data-ttu-id="06a21-200">Olayları tablodan kaldırmak için bir işlem uygulayın yok, tablo büyümeye devam edecek.</span><span class="sxs-lookup"><span data-stu-id="06a21-200">If you don't implement a process to remove events from the table, the table will continue to grow.</span></span> <span data-ttu-id="06a21-201">Şu anda çalışan bir veri temizleme hizmeti örneği yok [izleme örnek](https://github.com/Azure-Samples/service-fabric-watchdog-service), ve 30 veya 90 günlük süre kaydettiği depolamak için iyi bir neden olmadıkça kendiniz için bir tane de yazma önerilir.</span><span class="sxs-lookup"><span data-stu-id="06a21-201">Currently, there is an example of a data grooming service running in the [Watchdog sample](https://github.com/Azure-Samples/service-fabric-watchdog-service), and it is recommended that you write one for yourself as well, unless there is a good reason for you to store logs beyond a 30 or 90 day timeframe.</span></span>

* [<span data-ttu-id="06a21-202">Tanılama uzantısını kullanarak performans sayaçlarını veya günlükleri toplamak öğrenin</span><span class="sxs-lookup"><span data-stu-id="06a21-202">Learn how to collect performance counters or logs by using the Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="06a21-203">Olay çözümleme ve görselleştirme Application Insights ile</span><span class="sxs-lookup"><span data-stu-id="06a21-203">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="06a21-204">Olay çözümleme ve OMS Görselleştirme</span><span class="sxs-lookup"><span data-stu-id="06a21-204">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)