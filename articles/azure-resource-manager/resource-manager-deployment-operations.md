---
title: "Dağıtım işlemlerini Azure Resource Manager ile | Microsoft Docs"
description: "Portal, PowerShell, Azure CLI ve REST API ile Azure Resource Manager dağıtım işlemlerini görüntülemeyi açıklar."
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
ms.openlocfilehash: fb6b3b357fd1f66184e480115a9c863ba31ac193
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="view-deployment-operations-with-azure-resource-manager"></a><span data-ttu-id="48b17-103">Görünüm dağıtım işlemlerini Azure Resource Manager ile</span><span class="sxs-lookup"><span data-stu-id="48b17-103">View deployment operations with Azure Resource Manager</span></span>


<span data-ttu-id="48b17-104">Azure Portalı aracılığıyla bir dağıtım için işlemleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48b17-104">You can view the operations for a deployment through the Azure portal.</span></span> <span data-ttu-id="48b17-105">Başarısız olan işlemleri görüntülemek için bu makalede odaklanır şekilde dağıtımı sırasında bir hata aldınız zaman işlemleri içinde görüntüleme en ilgi çekici olabilir.</span><span class="sxs-lookup"><span data-stu-id="48b17-105">You may be most interested in viewing the operations when you have received an error during deployment so this article focuses on viewing operations that have failed.</span></span> <span data-ttu-id="48b17-106">Portal, kolayca hataları bulma ve olası düzeltmeleri belirlemek sağlayan bir arabirim sağlar.</span><span class="sxs-lookup"><span data-stu-id="48b17-106">The portal provides an interface that enables you to easily find the errors and determine potential fixes.</span></span>

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a><span data-ttu-id="48b17-107">Portal</span><span class="sxs-lookup"><span data-stu-id="48b17-107">Portal</span></span>
<span data-ttu-id="48b17-108">Dağıtım işlemlerini görmek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="48b17-108">To see the deployment operations, use the following steps:</span></span>

1. <span data-ttu-id="48b17-109">Dağıtımı ile ilgili kaynak grubu için son dağıtım durumunu dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="48b17-109">For the resource group involved in the deployment, notice the status of the last deployment.</span></span> <span data-ttu-id="48b17-110">Daha fazla bilgi almak için bu durum seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48b17-110">You can select this status to get more details.</span></span>
   
    ![Dağıtım durumu](./media/resource-manager-deployment-operations/deployment-status.png)
2. <span data-ttu-id="48b17-112">En son dağıtım geçmişini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="48b17-112">You see the recent deployment history.</span></span> <span data-ttu-id="48b17-113">Başarısız olan dağıtımı seçin.</span><span class="sxs-lookup"><span data-stu-id="48b17-113">Select the deployment that failed.</span></span>
   
    ![Dağıtım durumu](./media/resource-manager-deployment-operations/select-deployment.png)
3. <span data-ttu-id="48b17-115">Dağıtım neden başarısız açıklamasını görmek için bağlantıya seçin.</span><span class="sxs-lookup"><span data-stu-id="48b17-115">Select the link to see a description of why the deployment failed.</span></span> <span data-ttu-id="48b17-116">Aşağıdaki resimde DNS kaydı benzersiz değil.</span><span class="sxs-lookup"><span data-stu-id="48b17-116">In the image below, the DNS record is not unique.</span></span>  
   
    ![başarısız dağıtım görüntüleyin](./media/resource-manager-deployment-operations/view-error.png)
   
    <span data-ttu-id="48b17-118">Bu hata iletisi, sorun giderme başlatmak yeterli olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="48b17-118">This error message should be enough for you to begin troubleshooting.</span></span> <span data-ttu-id="48b17-119">Ancak, hakkında daha fazla ayrıntı gerekiyorsa hangi görevlerin tamamlandığını, aşağıdaki adımlarda gösterildiği gibi işlemleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48b17-119">However, if you need more details about which tasks were completed, you can view the operations as shown in the following steps.</span></span>
4. <span data-ttu-id="48b17-120">İçindeki tüm dağıtım işlemlerini görüntüleyebilirsiniz **dağıtım** dikey.</span><span class="sxs-lookup"><span data-stu-id="48b17-120">You can view all the deployment operations in the **Deployment** blade.</span></span> <span data-ttu-id="48b17-121">Daha fazla ayrıntı için herhangi bir işlem seçin.</span><span class="sxs-lookup"><span data-stu-id="48b17-121">Select any operation to see more details.</span></span>
   
    ![Görünüm işlemleri](./media/resource-manager-deployment-operations/view-operations.png)
   
    <span data-ttu-id="48b17-123">Bu durumda, depolama hesabı, sanal ağ ve kullanılabilirlik kümesi başarıyla oluşturulduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="48b17-123">In this case, you see that the storage account, virtual network, and availability set were successfully created.</span></span> <span data-ttu-id="48b17-124">Genel IP adresi başarısız oldu ve diğer kaynakları değil girişiminde bulunuldu.</span><span class="sxs-lookup"><span data-stu-id="48b17-124">The public IP address failed, and other resources were not attempted.</span></span>
5. <span data-ttu-id="48b17-125">Dağıtım için olayları seçerek görüntüleyebilirsiniz **olayları**.</span><span class="sxs-lookup"><span data-stu-id="48b17-125">You can view events for the deployment by selecting **Events**.</span></span>
   
    ![olaylarını görüntüle](./media/resource-manager-deployment-operations/view-events.png)
6. <span data-ttu-id="48b17-127">Dağıtımı için tüm olayları görmek ve daha fazla ayrıntı için herhangi bir tanesini seçin.</span><span class="sxs-lookup"><span data-stu-id="48b17-127">You see all the events for the deployment and select any one for more details.</span></span> <span data-ttu-id="48b17-128">Çok fark bağıntı kimlikleri.</span><span class="sxs-lookup"><span data-stu-id="48b17-128">Notice too the correlation IDs.</span></span> <span data-ttu-id="48b17-129">Bu değer, bir dağıtım gidermek için teknik destek ile çalışırken yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="48b17-129">This value can be helpful when working with technical support to troubleshoot a deployment.</span></span>
   
    ![olaylara bakın](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a><span data-ttu-id="48b17-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="48b17-131">PowerShell</span></span>
1. <span data-ttu-id="48b17-132">Bir dağıtımın genel durumunu almak için **Get-AzureRmResourceGroupDeployment** komutu.</span><span class="sxs-lookup"><span data-stu-id="48b17-132">To get the overall status of a deployment, use the **Get-AzureRmResourceGroupDeployment** command.</span></span> 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   <span data-ttu-id="48b17-133">Veya, başarısız olan dağıtımları için sonuçları filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48b17-133">Or, you can filter the results for only those deployments that have failed.</span></span>

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. <span data-ttu-id="48b17-134">Her dağıtımda birden çok işlemlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="48b17-134">Each deployment includes multiple operations.</span></span> <span data-ttu-id="48b17-135">Her işlem, dağıtım işlemi bir adımda temsil eder.</span><span class="sxs-lookup"><span data-stu-id="48b17-135">Each operation represents a step in the deployment process.</span></span> <span data-ttu-id="48b17-136">Neyin dağıtımla yanlış gittiğini bulmak için genellikle dağıtım işlemleri ile ilgili ayrıntıları görmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="48b17-136">To discover what went wrong with a deployment, you usually need to see details about the deployment operations.</span></span> <span data-ttu-id="48b17-137">İşlemlerle durumunu görebilirsiniz **Get-AzureRmResourceGroupDeploymentOperation**.</span><span class="sxs-lookup"><span data-stu-id="48b17-137">You can see the status of the operations with **Get-AzureRmResourceGroupDeploymentOperation**.</span></span>

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    <span data-ttu-id="48b17-138">Aşağıdaki biçimde her biri birden çok işlemleriyle döndürür:</span><span class="sxs-lookup"><span data-stu-id="48b17-138">Which returns multiple operations with each one in the following format:</span></span>

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. <span data-ttu-id="48b17-139">Başarısız işlemler hakkında daha fazla bilgi almak için işlemleriyle özelliklerini almak **başarısız** durumu.</span><span class="sxs-lookup"><span data-stu-id="48b17-139">To get more details about failed operations, retrieve the properties for operations with **Failed** state.</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    <span data-ttu-id="48b17-140">Aşağıdaki biçimde her biri ile başarısız olan tüm işlemler döndürür:</span><span class="sxs-lookup"><span data-stu-id="48b17-140">Which returns all the failed operations with each one in the following format:</span></span>

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

    <span data-ttu-id="48b17-141">ServiceRequestId ve işlem için Trackingıd unutmayın.</span><span class="sxs-lookup"><span data-stu-id="48b17-141">Note the serviceRequestId and the trackingId for the operation.</span></span> <span data-ttu-id="48b17-142">ServiceRequestId bir dağıtım gidermek için teknik destek ile çalışırken yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="48b17-142">The serviceRequestId can be helpful when working with technical support to troubleshoot a deployment.</span></span> <span data-ttu-id="48b17-143">Belirli bir işlemi odaklanmak için sonraki adımda Trackingıd kullanır.</span><span class="sxs-lookup"><span data-stu-id="48b17-143">You will use the trackingId in the next step to focus on a particular operation.</span></span>
4. <span data-ttu-id="48b17-144">Belirli bir başarısız işlem durum iletisini almak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="48b17-144">To get the status message of a particular failed operation, use the following command:</span></span>

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    <span data-ttu-id="48b17-145">Hangi döndürür:</span><span class="sxs-lookup"><span data-stu-id="48b17-145">Which returns:</span></span>

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. <span data-ttu-id="48b17-146">Her dağıtım işlem Azure, istek ve yanıt içeriği içerir.</span><span class="sxs-lookup"><span data-stu-id="48b17-146">Every deployment operation in Azure includes request and response content.</span></span> <span data-ttu-id="48b17-147">Ne, dağıtım sırasında Azure'a gönderilen istek içeriği olduğu (örneğin, bir VM oluşturma işletim sistemi diski ve diğer kaynakları).</span><span class="sxs-lookup"><span data-stu-id="48b17-147">The request content is what you sent to Azure during deployment (for example, create a VM, OS disk, and other resources).</span></span> <span data-ttu-id="48b17-148">Azure yanıt içeriği ne geri dağıtımı isteğinden sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="48b17-148">The response content is what Azure sent back from your deployment request.</span></span> <span data-ttu-id="48b17-149">Dağıtım sırasında kullandığınız **DeploymentDebugLogLevel** paramenter isteğin ve/veya yanıt günlüğüne korunur belirtin.</span><span class="sxs-lookup"><span data-stu-id="48b17-149">During deployment, you can use **DeploymentDebugLogLevel** paramenter to specify that the request and/or response are retained in the log.</span></span> 

  <span data-ttu-id="48b17-150">Günlükteki bu bilgileri almak ve aşağıdaki PowerShell komutlarını kullanarak yerel olarak kaydedin:</span><span class="sxs-lookup"><span data-stu-id="48b17-150">You get that information from the log, and save it locally by using the following PowerShell commands:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a><span data-ttu-id="48b17-151">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="48b17-151">Azure CLI</span></span>

1. <span data-ttu-id="48b17-152">Dağıtımla genel durumunu elde **azure Grup dağıtım Göster** komutu.</span><span class="sxs-lookup"><span data-stu-id="48b17-152">Get the overall status of a deployment with the **azure group deployment show** command.</span></span>

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  <span data-ttu-id="48b17-153">Döndürülen değerlerinden biri **correlationıd değeri**.</span><span class="sxs-lookup"><span data-stu-id="48b17-153">One of the returned values is the **correlationId**.</span></span> <span data-ttu-id="48b17-154">Bu değer, ilgili olayları izlemek için kullanılır ve bir dağıtım gidermek için teknik destek ile çalışırken yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="48b17-154">This value is used to track related events, and can be helpful when working with technical support to troubleshoot a deployment.</span></span>

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. <span data-ttu-id="48b17-155">Bir dağıtım için işlemleri görmek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="48b17-155">To see the operations for a deployment, use:</span></span>

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a><span data-ttu-id="48b17-156">REST</span><span class="sxs-lookup"><span data-stu-id="48b17-156">REST</span></span>

1. <span data-ttu-id="48b17-157">Olan bir dağıtım hakkında bilgi almak [şablon dağıtımı hakkında bilgi alma](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) işlemi.</span><span class="sxs-lookup"><span data-stu-id="48b17-157">Get information about a deployment with the [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operation.</span></span>

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    <span data-ttu-id="48b17-158">Yanıtta, özellikle dikkat edin **provisioningState**, **correlationıd değeri**, ve **hata** öğeleri.</span><span class="sxs-lookup"><span data-stu-id="48b17-158">In the response, note in particular the **provisioningState**, **correlationId**, and **error** elements.</span></span> <span data-ttu-id="48b17-159">**Correlationıd değeri** ilgili olayları izlemek için kullanılır ve bir dağıtım gidermek için teknik destek ile çalışırken yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="48b17-159">The **correlationId** is used to track related events, and can be helpful when working with technical support to troubleshoot a deployment.</span></span>

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

2. <span data-ttu-id="48b17-160">Dağıtım işlemleri ile ilgili bilgi almak [tüm şablon dağıtım işlemlerini listelemek](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) işlemi.</span><span class="sxs-lookup"><span data-stu-id="48b17-160">Get information about deployment operations with the [List all template deployment operations](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operation.</span></span> 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    <span data-ttu-id="48b17-161">İsteğin ve/veya yanıt bilgileri ne belirttiğiniz üzerinde göre yanıt içeriyor **debugSetting** dağıtımı sırasında özelliği.</span><span class="sxs-lookup"><span data-stu-id="48b17-161">The response includes request and/or response information based on what you specified in the **debugSetting** property during deployment.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="48b17-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="48b17-162">Next steps</span></span>
* <span data-ttu-id="48b17-163">Belirli dağıtım hatalarını çözme konusunda daha fazla yardım için bkz: [kaynakları Azure Azure Resource Manager ile dağıtırken sık karşılaşılan hataları gidermek](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="48b17-163">For help with resolving particular deployment errors, see [Resolve common errors when deploying resources to Azure with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="48b17-164">Diğer Eylemler türlerini izlemek için etkinlik günlükleri kullanma hakkında bilgi edinmek için bkz: [görüntülemek Azure kaynaklarınızı yönetmek için etkinlik günlükleri](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="48b17-164">To learn about using the activity logs to monitor other types of actions, see [View activity logs to manage Azure resources](resource-group-audit.md).</span></span>
* <span data-ttu-id="48b17-165">Dağıtımınız, yürütmeden önce doğrulamak için bkz: [Azure Resource Manager şablonu ile bir kaynak grubu dağıtma](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="48b17-165">To validate your deployment before executing it, see [Deploy a resource group with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

