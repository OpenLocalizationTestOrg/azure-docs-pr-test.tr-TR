---
title: "aaaDeployment işlemleri Azure Resource Manager ile | Microsoft Docs"
description: "Nasıl tooview Azure Resource Manager dağıtım işlemleri ile Merhaba açıklar portal, PowerShell, Azure CLI ve REST API'si."
services: azure-resource-manager,virtual-machines
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: infrastructure
ms.date: 01/13/2017
ms.author: tomfitz
ms.openlocfilehash: ba4823ca73caca83dfc07c99d736344ef8b7b54d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="view-deployment-operations-with-azure-resource-manager"></a><span data-ttu-id="b8a54-103">Görünüm dağıtım işlemlerini Azure Resource Manager ile</span><span class="sxs-lookup"><span data-stu-id="b8a54-103">View deployment operations with Azure Resource Manager</span></span>


<span data-ttu-id="b8a54-104">Merhaba işlemleri hello Azure portal aracılığıyla bir dağıtım için görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8a54-104">You can view hello operations for a deployment through hello Azure portal.</span></span> <span data-ttu-id="b8a54-105">Başarısız olan işlemleri görüntülemek için bu makalede odaklanır şekilde dağıtımı sırasında bir hata aldınız zaman hello işlemleri içinde görüntüleme en ilgi çekici olabilir.</span><span class="sxs-lookup"><span data-stu-id="b8a54-105">You may be most interested in viewing hello operations when you have received an error during deployment so this article focuses on viewing operations that have failed.</span></span> <span data-ttu-id="b8a54-106">Merhaba portal tooeasily Bul hello hataları sağlayan bir arabirim sağlar ve olası düzeltmeleri belirleyin.</span><span class="sxs-lookup"><span data-stu-id="b8a54-106">hello portal provides an interface that enables you tooeasily find hello errors and determine potential fixes.</span></span>

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a><span data-ttu-id="b8a54-107">Portal</span><span class="sxs-lookup"><span data-stu-id="b8a54-107">Portal</span></span>
<span data-ttu-id="b8a54-108">toosee hello dağıtım işlemlerini hello aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="b8a54-108">toosee hello deployment operations, use hello following steps:</span></span>

1. <span data-ttu-id="b8a54-109">Merhaba kaynak grubu için hello dağıtımı ile ilgili hello hello son dağıtımının durumunu dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="b8a54-109">For hello resource group involved in hello deployment, notice hello status of hello last deployment.</span></span> <span data-ttu-id="b8a54-110">Bu durum tooget daha fazla ayrıntı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8a54-110">You can select this status tooget more details.</span></span>
   
    ![Dağıtım durumu](./media/resource-manager-deployment-operations/deployment-status.png)
2. <span data-ttu-id="b8a54-112">Merhaba en son dağıtım geçmişini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b8a54-112">You see hello recent deployment history.</span></span> <span data-ttu-id="b8a54-113">Başarısız hello dağıtımı seçin.</span><span class="sxs-lookup"><span data-stu-id="b8a54-113">Select hello deployment that failed.</span></span>
   
    ![Dağıtım durumu](./media/resource-manager-deployment-operations/select-deployment.png)
3. <span data-ttu-id="b8a54-115">Neden açıklaması hello dağıtılamadı hello bağlantı toosee seçin.</span><span class="sxs-lookup"><span data-stu-id="b8a54-115">Select hello link toosee a description of why hello deployment failed.</span></span> <span data-ttu-id="b8a54-116">Merhaba resimde, hello DNS kaydı benzersiz değil.</span><span class="sxs-lookup"><span data-stu-id="b8a54-116">In hello image below, hello DNS record is not unique.</span></span>  
   
    ![başarısız dağıtım görüntüleyin](./media/resource-manager-deployment-operations/view-error.png)
   
    <span data-ttu-id="b8a54-118">Bu hata iletisini sizin için yeterli olmalıdır toobegin sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="b8a54-118">This error message should be enough for you toobegin troubleshooting.</span></span> <span data-ttu-id="b8a54-119">Ancak, tamamlanan görevler hakkında daha fazla ayrıntı gerekiyorsa, aşağıdaki adımları hello gösterildiği gibi hello işlemleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8a54-119">However, if you need more details about which tasks were completed, you can view hello operations as shown in hello following steps.</span></span>
4. <span data-ttu-id="b8a54-120">Tüm hello dağıtım işlemlerini hello görüntüleyebilirsiniz **dağıtım** dikey.</span><span class="sxs-lookup"><span data-stu-id="b8a54-120">You can view all hello deployment operations in hello **Deployment** blade.</span></span> <span data-ttu-id="b8a54-121">Hiçbir işlem toosee daha fazla ayrıntı seçin.</span><span class="sxs-lookup"><span data-stu-id="b8a54-121">Select any operation toosee more details.</span></span>
   
    ![Görünüm işlemleri](./media/resource-manager-deployment-operations/view-operations.png)
   
    <span data-ttu-id="b8a54-123">Bu durumda, hello depolama hesabı, sanal ağ ve kullanılabilirlik kümesi başarıyla oluşturulduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b8a54-123">In this case, you see that hello storage account, virtual network, and availability set were successfully created.</span></span> <span data-ttu-id="b8a54-124">Merhaba genel IP adresi başarısız oldu ve diğer kaynakları değil girişiminde bulunuldu.</span><span class="sxs-lookup"><span data-stu-id="b8a54-124">hello public IP address failed, and other resources were not attempted.</span></span>
5. <span data-ttu-id="b8a54-125">Merhaba dağıtımı için olayları seçerek görüntüleyebilirsiniz **olayları**.</span><span class="sxs-lookup"><span data-stu-id="b8a54-125">You can view events for hello deployment by selecting **Events**.</span></span>
   
    ![olaylarını görüntüle](./media/resource-manager-deployment-operations/view-events.png)
6. <span data-ttu-id="b8a54-127">Merhaba dağıtımı için tüm hello olaylara bakın ve daha fazla ayrıntı için herhangi bir tanesini seçin.</span><span class="sxs-lookup"><span data-stu-id="b8a54-127">You see all hello events for hello deployment and select any one for more details.</span></span> <span data-ttu-id="b8a54-128">Çok bağıntı kimlikleri hello dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="b8a54-128">Notice too hello correlation IDs.</span></span> <span data-ttu-id="b8a54-129">Bu değer, teknik destek tootroubleshoot ile bir dağıtım çalışırken yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="b8a54-129">This value can be helpful when working with technical support tootroubleshoot a deployment.</span></span>
   
    ![olaylara bakın](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a><span data-ttu-id="b8a54-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8a54-131">PowerShell</span></span>
1. <span data-ttu-id="b8a54-132">tooget hello bir dağıtım, kullanım hello genel durumunu **Get-AzureRmResourceGroupDeployment** komutu.</span><span class="sxs-lookup"><span data-stu-id="b8a54-132">tooget hello overall status of a deployment, use hello **Get-AzureRmResourceGroupDeployment** command.</span></span> 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   <span data-ttu-id="b8a54-133">Veya, başarısız olan dağıtımları için hello sonuçları filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8a54-133">Or, you can filter hello results for only those deployments that have failed.</span></span>

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. <span data-ttu-id="b8a54-134">Her dağıtımda birden çok işlemlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="b8a54-134">Each deployment includes multiple operations.</span></span> <span data-ttu-id="b8a54-135">Her bir işlemin hello dağıtım işlemi bir adımda temsil eder.</span><span class="sxs-lookup"><span data-stu-id="b8a54-135">Each operation represents a step in hello deployment process.</span></span> <span data-ttu-id="b8a54-136">bir dağıtımı ile neyin yanlış gittiğini toodiscover, genellikle hello dağıtım işlemlerini toosee ayrıntılarını gerekir.</span><span class="sxs-lookup"><span data-stu-id="b8a54-136">toodiscover what went wrong with a deployment, you usually need toosee details about hello deployment operations.</span></span> <span data-ttu-id="b8a54-137">Merhaba işlemleriyle hello durumunu görebilirsiniz **Get-AzureRmResourceGroupDeploymentOperation**.</span><span class="sxs-lookup"><span data-stu-id="b8a54-137">You can see hello status of hello operations with **Get-AzureRmResourceGroupDeploymentOperation**.</span></span>

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    <span data-ttu-id="b8a54-138">Birden çok biçim aşağıdaki hello her birinde işlemleriyle döndürür:</span><span class="sxs-lookup"><span data-stu-id="b8a54-138">Which returns multiple operations with each one in hello following format:</span></span>

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. <span data-ttu-id="b8a54-139">tooget başarısız işlemler hakkında daha fazla ayrıntı almak işlemleriyle hello özelliklerini **başarısız** durumu.</span><span class="sxs-lookup"><span data-stu-id="b8a54-139">tooget more details about failed operations, retrieve hello properties for operations with **Failed** state.</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    <span data-ttu-id="b8a54-140">Tüm başarısız işlemler hello biçimini izleyen her birinde ile Merhaba döndürür:</span><span class="sxs-lookup"><span data-stu-id="b8a54-140">Which returns all hello failed operations with each one in hello following format:</span></span>

  ```powershell
  provisioningOperation : Create
  provisioningState     : Failed
  timestamp             : 2016-06-14T21:54:55.1468068Z
  duration              : PT3.1449887S
  trackingId            : f4ed72f8-4203-43dc-958a-15d041e8c233
  serviceRequestId      : a426f689-5d5a-448d-a2f0-9784d14c900a
  statusCode            : BadRequest
  statusMessage         : @{error=}
  targetResource        : @{id=/subscriptions/{guid}/resourceGroups/ExampleGroup/providers/
                          Microsoft.Network/publicIPAddresses/myPublicIP;
                          resourceType=Microsoft.Network/publicIPAddresses; resourceName=myPublicIP}
  ```

    <span data-ttu-id="b8a54-141">Merhaba serviceRequestId ve hello işlemi hello Trackingıd unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b8a54-141">Note hello serviceRequestId and hello trackingId for hello operation.</span></span> <span data-ttu-id="b8a54-142">Merhaba serviceRequestId teknik destek tootroubleshoot ile bir dağıtım çalışırken yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="b8a54-142">hello serviceRequestId can be helpful when working with technical support tootroubleshoot a deployment.</span></span> <span data-ttu-id="b8a54-143">Merhaba Trackingıd hello sonraki adım toofocus belirli bir işlem üzerinde kullanır.</span><span class="sxs-lookup"><span data-stu-id="b8a54-143">You will use hello trackingId in hello next step toofocus on a particular operation.</span></span>
4. <span data-ttu-id="b8a54-144">belirli başarısız işlem, komutu aşağıdaki kullanım hello tooget hello durum iletisi:</span><span class="sxs-lookup"><span data-stu-id="b8a54-144">tooget hello status message of a particular failed operation, use hello following command:</span></span>

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    <span data-ttu-id="b8a54-145">Hangi döndürür:</span><span class="sxs-lookup"><span data-stu-id="b8a54-145">Which returns:</span></span>

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. <span data-ttu-id="b8a54-146">Her dağıtım işlem Azure, istek ve yanıt içeriği içerir.</span><span class="sxs-lookup"><span data-stu-id="b8a54-146">Every deployment operation in Azure includes request and response content.</span></span> <span data-ttu-id="b8a54-147">Merhaba istek içeriği, ne, dağıtım sırasında tooAzure gönderilen (örneğin, bir VM oluşturma işletim sistemi diski ve diğer kaynakları).</span><span class="sxs-lookup"><span data-stu-id="b8a54-147">hello request content is what you sent tooAzure during deployment (for example, create a VM, OS disk, and other resources).</span></span> <span data-ttu-id="b8a54-148">Azure Hello yanıt içeriği ne geri dağıtımı isteğinden sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="b8a54-148">hello response content is what Azure sent back from your deployment request.</span></span> <span data-ttu-id="b8a54-149">Dağıtım sırasında kullandığınız **DeploymentDebugLogLevel** isteğin ve/veya yanıt hello paramenter toospecify hello günlüğüne korunur.</span><span class="sxs-lookup"><span data-stu-id="b8a54-149">During deployment, you can use **DeploymentDebugLogLevel** paramenter toospecify that hello request and/or response are retained in hello log.</span></span> 

  <span data-ttu-id="b8a54-150">Merhaba günlüğü'nden bu bilgileri almak ve PowerShell komutlarını aşağıdaki hello kullanarak yerel olarak kaydedin:</span><span class="sxs-lookup"><span data-stu-id="b8a54-150">You get that information from hello log, and save it locally by using hello following PowerShell commands:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a><span data-ttu-id="b8a54-151">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b8a54-151">Azure CLI</span></span>

1. <span data-ttu-id="b8a54-152">Alma ile Merhaba dağıtımı genel durumunu hello **azure Grup dağıtım Göster** komutu.</span><span class="sxs-lookup"><span data-stu-id="b8a54-152">Get hello overall status of a deployment with hello **azure group deployment show** command.</span></span>

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  <span data-ttu-id="b8a54-153">Döndürülen hello biri hello **correlationıd değeri**.</span><span class="sxs-lookup"><span data-stu-id="b8a54-153">One of hello returned values is hello **correlationId**.</span></span> <span data-ttu-id="b8a54-154">Bu değer kullanılır tootrack ilgili olayları ve olması yararlı olduğunda çalışma teknik destek tootroubleshoot ile bir dağıtım.</span><span class="sxs-lookup"><span data-stu-id="b8a54-154">This value is used tootrack related events, and can be helpful when working with technical support tootroubleshoot a deployment.</span></span>

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. <span data-ttu-id="b8a54-155">toosee hello işlemleri bir dağıtım için kullanın:</span><span class="sxs-lookup"><span data-stu-id="b8a54-155">toosee hello operations for a deployment, use:</span></span>

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a><span data-ttu-id="b8a54-156">REST</span><span class="sxs-lookup"><span data-stu-id="b8a54-156">REST</span></span>

1. <span data-ttu-id="b8a54-157">Merhaba olan bir dağıtım hakkında bilgi almak [şablon dağıtımı hakkında bilgi alma](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) işlemi.</span><span class="sxs-lookup"><span data-stu-id="b8a54-157">Get information about a deployment with hello [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operation.</span></span>

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    <span data-ttu-id="b8a54-158">Merhaba yanıt olarak, özellikle hello Not **provisioningState**, **correlationıd değeri**, ve **hata** öğeleri.</span><span class="sxs-lookup"><span data-stu-id="b8a54-158">In hello response, note in particular hello **provisioningState**, **correlationId**, and **error** elements.</span></span> <span data-ttu-id="b8a54-159">Merhaba **correlationıd değeri** kullanılan tootrack ilgili olayları ve olması yararlı olduğunda çalışma teknik destek tootroubleshoot ile bir dağıtım.</span><span class="sxs-lookup"><span data-stu-id="b8a54-159">hello **correlationId** is used tootrack related events, and can be helpful when working with technical support tootroubleshoot a deployment.</span></span>

  ```json
  { 
    ...
    "properties": {
      "provisioningState":"Failed",
      "correlationId":"d5062e45-6e9f-4fd3-a0a0-6b2c56b15757",
      ...
      "error":{
        "code":"DeploymentFailed","message":"At least one resource deployment operation failed. Please list deployment operations for details. Please see http://aka.ms/arm-debug for usage details.",
        "details":[{"code":"Conflict","message":"{\r\n  \"error\": {\r\n    \"message\": \"Conflict\",\r\n    \"code\": \"Conflict\"\r\n  }\r\n}"}]
      }  
    }
  }
  ```

2. <span data-ttu-id="b8a54-160">Dağıtım işlemleri hello ile ilgili bilgi almak [tüm şablon dağıtım işlemlerini listelemek](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) işlemi.</span><span class="sxs-lookup"><span data-stu-id="b8a54-160">Get information about deployment operations with hello [List all template deployment operations](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operation.</span></span> 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    <span data-ttu-id="b8a54-161">Merhaba yanıt içeriyor isteğin ve/veya yanıt bilgileri hello belirtilen göre **debugSetting** dağıtımı sırasında özelliği.</span><span class="sxs-lookup"><span data-stu-id="b8a54-161">hello response includes request and/or response information based on what you specified in hello **debugSetting** property during deployment.</span></span>

  ```json
  {
    ...
    "properties": 
    {
      ...
      "request":{
        "content":{
          "location":"West US",
          "properties":{
            "accountType": "Standard_LRS"
          }
        }
      },
      "response":{
        "content":{
          "error":{
            "message":"Conflict","code":"Conflict"
          }
        }
      }
    }
  }
  ```


## <a name="next-steps"></a><span data-ttu-id="b8a54-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b8a54-162">Next steps</span></span>
* <span data-ttu-id="b8a54-163">Belirli dağıtım hatalarını çözme konusunda daha fazla yardım için bkz: [kaynakları tooAzure Azure Resource Manager ile dağıtırken sık karşılaşılan hataları gidermek](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="b8a54-163">For help with resolving particular deployment errors, see [Resolve common errors when deploying resources tooAzure with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="b8a54-164">Merhaba etkinlik kullanma hakkında toolearn eylemler diğer türleri toomonitor günlükleri, bkz: [etkinliği görüntüle günlüklerini toomanage Azure kaynakları](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="b8a54-164">toolearn about using hello activity logs toomonitor other types of actions, see [View activity logs toomanage Azure resources](resource-group-audit.md).</span></span>
* <span data-ttu-id="b8a54-165">Dağıtımınız, yürütmeden önce toovalidate bkz [Azure Resource Manager şablonu ile bir kaynak grubu dağıtma](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="b8a54-165">toovalidate your deployment before executing it, see [Deploy a resource group with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

