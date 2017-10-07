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
# <a name="view-deployment-operations-with-azure-resource-manager"></a>Görünüm dağıtım işlemlerini Azure Resource Manager ile


Merhaba işlemleri hello Azure portal aracılığıyla bir dağıtım için görüntüleyebilirsiniz. Başarısız olan işlemleri görüntülemek için bu makalede odaklanır şekilde dağıtımı sırasında bir hata aldınız zaman hello işlemleri içinde görüntüleme en ilgi çekici olabilir. Merhaba portal tooeasily Bul hello hataları sağlayan bir arabirim sağlar ve olası düzeltmeleri belirleyin.

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a>Portal
toosee hello dağıtım işlemlerini hello aşağıdaki adımları kullanın:

1. Merhaba kaynak grubu için hello dağıtımı ile ilgili hello hello son dağıtımının durumunu dikkat edin. Bu durum tooget daha fazla ayrıntı seçebilirsiniz.
   
    ![Dağıtım durumu](./media/resource-manager-deployment-operations/deployment-status.png)
2. Merhaba en son dağıtım geçmişini görürsünüz. Başarısız hello dağıtımı seçin.
   
    ![Dağıtım durumu](./media/resource-manager-deployment-operations/select-deployment.png)
3. Neden açıklaması hello dağıtılamadı hello bağlantı toosee seçin. Merhaba resimde, hello DNS kaydı benzersiz değil.  
   
    ![başarısız dağıtım görüntüleyin](./media/resource-manager-deployment-operations/view-error.png)
   
    Bu hata iletisini sizin için yeterli olmalıdır toobegin sorun giderme. Ancak, tamamlanan görevler hakkında daha fazla ayrıntı gerekiyorsa, aşağıdaki adımları hello gösterildiği gibi hello işlemleri görüntüleyebilirsiniz.
4. Tüm hello dağıtım işlemlerini hello görüntüleyebilirsiniz **dağıtım** dikey. Hiçbir işlem toosee daha fazla ayrıntı seçin.
   
    ![Görünüm işlemleri](./media/resource-manager-deployment-operations/view-operations.png)
   
    Bu durumda, hello depolama hesabı, sanal ağ ve kullanılabilirlik kümesi başarıyla oluşturulduğunu görürsünüz. Merhaba genel IP adresi başarısız oldu ve diğer kaynakları değil girişiminde bulunuldu.
5. Merhaba dağıtımı için olayları seçerek görüntüleyebilirsiniz **olayları**.
   
    ![olaylarını görüntüle](./media/resource-manager-deployment-operations/view-events.png)
6. Merhaba dağıtımı için tüm hello olaylara bakın ve daha fazla ayrıntı için herhangi bir tanesini seçin. Çok bağıntı kimlikleri hello dikkat edin. Bu değer, teknik destek tootroubleshoot ile bir dağıtım çalışırken yararlı olabilir.
   
    ![olaylara bakın](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a>PowerShell
1. tooget hello bir dağıtım, kullanım hello genel durumunu **Get-AzureRmResourceGroupDeployment** komutu. 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   Veya, başarısız olan dağıtımları için hello sonuçları filtreleyebilirsiniz.

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. Her dağıtımda birden çok işlemlerini içerir. Her bir işlemin hello dağıtım işlemi bir adımda temsil eder. bir dağıtımı ile neyin yanlış gittiğini toodiscover, genellikle hello dağıtım işlemlerini toosee ayrıntılarını gerekir. Merhaba işlemleriyle hello durumunu görebilirsiniz **Get-AzureRmResourceGroupDeploymentOperation**.

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    Birden çok biçim aşağıdaki hello her birinde işlemleriyle döndürür:

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. tooget başarısız işlemler hakkında daha fazla ayrıntı almak işlemleriyle hello özelliklerini **başarısız** durumu.

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    Tüm başarısız işlemler hello biçimini izleyen her birinde ile Merhaba döndürür:

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

    Merhaba serviceRequestId ve hello işlemi hello Trackingıd unutmayın. Merhaba serviceRequestId teknik destek tootroubleshoot ile bir dağıtım çalışırken yararlı olabilir. Merhaba Trackingıd hello sonraki adım toofocus belirli bir işlem üzerinde kullanır.
4. belirli başarısız işlem, komutu aşağıdaki kullanım hello tooget hello durum iletisi:

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    Hangi döndürür:

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. Her dağıtım işlem Azure, istek ve yanıt içeriği içerir. Merhaba istek içeriği, ne, dağıtım sırasında tooAzure gönderilen (örneğin, bir VM oluşturma işletim sistemi diski ve diğer kaynakları). Azure Hello yanıt içeriği ne geri dağıtımı isteğinden sayısıdır. Dağıtım sırasında kullandığınız **DeploymentDebugLogLevel** isteğin ve/veya yanıt hello paramenter toospecify hello günlüğüne korunur. 

  Merhaba günlüğü'nden bu bilgileri almak ve PowerShell komutlarını aşağıdaki hello kullanarak yerel olarak kaydedin:

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a>Azure CLI

1. Alma ile Merhaba dağıtımı genel durumunu hello **azure Grup dağıtım Göster** komutu.

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  Döndürülen hello biri hello **correlationıd değeri**. Bu değer kullanılır tootrack ilgili olayları ve olması yararlı olduğunda çalışma teknik destek tootroubleshoot ile bir dağıtım.

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. toosee hello işlemleri bir dağıtım için kullanın:

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a>REST

1. Merhaba olan bir dağıtım hakkında bilgi almak [şablon dağıtımı hakkında bilgi alma](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) işlemi.

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    Merhaba yanıt olarak, özellikle hello Not **provisioningState**, **correlationıd değeri**, ve **hata** öğeleri. Merhaba **correlationıd değeri** kullanılan tootrack ilgili olayları ve olması yararlı olduğunda çalışma teknik destek tootroubleshoot ile bir dağıtım.

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

2. Dağıtım işlemleri hello ile ilgili bilgi almak [tüm şablon dağıtım işlemlerini listelemek](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) işlemi. 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    Merhaba yanıt içeriyor isteğin ve/veya yanıt bilgileri hello belirtilen göre **debugSetting** dağıtımı sırasında özelliği.

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


## <a name="next-steps"></a>Sonraki adımlar
* Belirli dağıtım hatalarını çözme konusunda daha fazla yardım için bkz: [kaynakları tooAzure Azure Resource Manager ile dağıtırken sık karşılaşılan hataları gidermek](resource-manager-common-deployment-errors.md).
* Merhaba etkinlik kullanma hakkında toolearn eylemler diğer türleri toomonitor günlükleri, bkz: [etkinliği görüntüle günlüklerini toomanage Azure kaynakları](resource-group-audit.md).
* Dağıtımınız, yürütmeden önce toovalidate bkz [Azure Resource Manager şablonu ile bir kaynak grubu dağıtma](resource-group-template-deploy.md).

