---
title: "bir Azure Event Hubs ad alanı ve etkinleştir yakalama bir şablon kullanarak aaaCreate | Microsoft Docs"
description: "Bir olay hub'ı ile bir Azure Event Hubs ad alanı oluşturma ve Azure Resource Manager şablonu kullanarak Yakalamayı etkinleştirme"
services: event-hubs
documentationcenter: .net
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 8bdda6a2-5ff1-45e3-b696-c553768f1090
ms.service: event-hubs
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: a43b4e8d690ae825047e8a9d609bfda89cf2a06f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a><span data-ttu-id="8a218-103">Bir olay hub'ı ile bir Event Hubs ad alanı oluşturma ve Azure Resource Manager şablonu kullanarak Yakalamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="8a218-103">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>

<span data-ttu-id="8a218-104">Bu makalede nasıl toouse bir Azure Resource Manager şablonu, bir olay hub'ları ad alanı, bir olay hub'ı örneği etkinleştirir hello da oluşturur ve gösterilmektedir [yakalama özelliği](event-hubs-capture-overview.md) hello olay hub'ındaki.</span><span class="sxs-lookup"><span data-stu-id="8a218-104">This article shows how toouse an Azure Resource Manager template that creates an Event Hubs namespace, with one event hub instance, and also enables hello [Capture feature](event-hubs-capture-overview.md) on hello event hub.</span></span> <span data-ttu-id="8a218-105">Merhaba makalede nasıl toodefine hangi kaynağın dağıtılan ve nasıl olan toodefine hello dağıtım zaman yürütülür parametrelerinizi.</span><span class="sxs-lookup"><span data-stu-id="8a218-105">hello article describes how toodefine which resources are deployed, and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="8a218-106">Kendi dağıtımlar için bu şablonu kullanabilir veya toomeet özelleştirebilirsiniz gereksinimlerinizi.</span><span class="sxs-lookup"><span data-stu-id="8a218-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="8a218-107">Bu makale ayrıca nasıl olayları Azure Storage Bloblarında veya bir Azure Data Lake Store yakalanır toospecify üzerinde hello gösterir, seçtiğiniz hedef.</span><span class="sxs-lookup"><span data-stu-id="8a218-107">This article also shows how toospecify that events are captured into either Azure Storage Blobs or an Azure Data Lake Store, based on hello destination you choose.</span></span>

<span data-ttu-id="8a218-108">Şablon oluşturma hakkında daha fazla bilgi için bkz. [Azure Resource Manager şablonları yazma][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="8a218-108">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="8a218-109">Azure Kaynakları adlandırma kurallarına ilişkin uygulama ve yapılar için bkz. [Azure Kaynakları Adlandırma Kuralları][Azure Resources naming conventions].</span><span class="sxs-lookup"><span data-stu-id="8a218-109">For more information about patterns and practices for Azure Resources naming conventions, see [Azure Resources naming conventions][Azure Resources naming conventions].</span></span>

<span data-ttu-id="8a218-110">Merhaba tam şablonları için GitHub bağlantılar aşağıdaki hello tıklatın:</span><span class="sxs-lookup"><span data-stu-id="8a218-110">For hello complete templates, click hello following GitHub links:</span></span>

- <span data-ttu-id="8a218-111">[Olay hub'ı ve etkinleştir yakalama tooStorage şablonu][Event Hub and enable Capture tooStorage template]</span><span class="sxs-lookup"><span data-stu-id="8a218-111">[Event hub and enable Capture tooStorage template][Event Hub and enable Capture tooStorage template]</span></span> 
- <span data-ttu-id="8a218-112">[Olay hub'ı ve etkinleştir yakalama tooAzure Data Lake Store şablonu][Event Hub and enable Capture tooAzure Data Lake Store template]</span><span class="sxs-lookup"><span data-stu-id="8a218-112">[Event hub and enable Capture tooAzure Data Lake Store template][Event Hub and enable Capture tooAzure Data Lake Store template]</span></span>

> [!NOTE]
> <span data-ttu-id="8a218-113">Merhaba son şablonları için toocheck ziyaret hello [Azure hızlı başlangıç şablonlarını] [ Azure Quickstart Templates] Galerisi ve Event Hubs arayın.</span><span class="sxs-lookup"><span data-stu-id="8a218-113">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="8a218-114">Ne dağıtacaksınız?</span><span class="sxs-lookup"><span data-stu-id="8a218-114">What will you deploy?</span></span>

<span data-ttu-id="8a218-115">Bu şablonu kullanarak bir olay hub’ı ile Event Hubs ad alanı dağıtır ve aynı zamanda [Event Hubs Yakalama](event-hubs-capture-overview.md) özelliğini etkinleştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a218-115">With this template, you deploy an Event Hubs namespace with an event hub, and also enable [Event Hubs Capture](event-hubs-capture-overview.md).</span></span>

<span data-ttu-id="8a218-116">[Olay hub'ları](event-hubs-what-is-event-hubs.md) büyük ölçekte kullanılan hizmet tooprovide olayı ve telemetri giriş tooAzure düşük gecikme süreli ve yüksek güvenilirlik işlemeyi bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="8a218-116">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used tooprovide event and telemetry ingress tooAzure at massive scale, with low latency and high reliability.</span></span> <span data-ttu-id="8a218-117">Tooautomatically teslim olay hub'ları tooAzure Blob Depolama birimindeki verileri veya Azure Data Lake Store, belirtilen zaman veya seçtiğiniz boyutu aralığı içinde akış hello olay hub'ları yakalama etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="8a218-117">Event Hubs Capture enables you tooautomatically deliver hello streaming data in Event Hubs tooAzure Blob storage or Azure Data Lake Store, within a specified time or size interval of your choosing.</span></span>

<span data-ttu-id="8a218-118">Azure depolama alanına düğmesi tooenable olay hub'ları yakalama aşağıdaki hello tıklatın:</span><span class="sxs-lookup"><span data-stu-id="8a218-118">Click hello following button tooenable Event Hubs Capture into Azure Storage:</span></span>

<span data-ttu-id="8a218-119">[![TooAzure dağıtma](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="8a218-119">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span></span>

<span data-ttu-id="8a218-120">Azure Data Lake Store düğmesi tooenable olay hub'ları yakalama aşağıdaki hello tıklatın:</span><span class="sxs-lookup"><span data-stu-id="8a218-120">Click hello following button tooenable Event Hubs Capture into Azure Data Lake Store:</span></span>

<span data-ttu-id="8a218-121">[![TooAzure dağıtma](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="8a218-121">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="8a218-122">Parametreler</span><span class="sxs-lookup"><span data-stu-id="8a218-122">Parameters</span></span>

<span data-ttu-id="8a218-123">Azure Resource Manager ile tanımladığınız parametreler için değerler hello şablon dağıtıldığında toospecify istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="8a218-123">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="8a218-124">Merhaba şablonu adlı bir bölüm içerir `Parameters` tüm hello parametre değerlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="8a218-124">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="8a218-125">Dağıttığınız hello projesini temel alan veya dağıttığınız hello ortamı dayanarak farklılık bu değerleri için bir parametre tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a218-125">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="8a218-126">Her zaman kalın değerleri aynı hello için parametreleri tanımlamayın.</span><span class="sxs-lookup"><span data-stu-id="8a218-126">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="8a218-127">Her parametre değeri dağıtılan hello şablonu toodefine hello kaynaklarında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8a218-127">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="8a218-128">Merhaba şablonu şu parametreler hello tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8a218-128">hello template defines hello following parameters.</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="8a218-129">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="8a218-129">eventHubNamespaceName</span></span>

<span data-ttu-id="8a218-130">Merhaba Hello adını [olay hub'ları ad alanı](event-hubs-create.md) toocreate.</span><span class="sxs-lookup"><span data-stu-id="8a218-130">hello name of hello [Event Hubs namespace](event-hubs-create.md) toocreate.</span></span>

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of hello EventHub namespace"
      }
}
```

### <a name="eventhubname"></a><span data-ttu-id="8a218-131">eventHubName</span><span class="sxs-lookup"><span data-stu-id="8a218-131">eventHubName</span></span>

<span data-ttu-id="8a218-132">Merhaba event hub'ı hello oluşturulan Hello adını [olay hub'ları ad alanı](event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="8a218-132">hello name of hello event hub created in hello [Event Hubs namespace](event-hubs-create.md).</span></span>

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of hello event hub"
    }
}
```

### <a name="messageretentionindays"></a><span data-ttu-id="8a218-133">messageRetentionInDays</span><span class="sxs-lookup"><span data-stu-id="8a218-133">messageRetentionInDays</span></span>

<span data-ttu-id="8a218-134">gün tooretain hello iletilerinin hello event hub'ındaki Hello sayısı.</span><span class="sxs-lookup"><span data-stu-id="8a218-134">hello number of days tooretain hello messages in hello event hub.</span></span> 

```json
"messageRetentionInDays":{
    "type":"int",
    "defaultValue": 1,
    "minValue":"1",
    "maxValue":"7",
    "metadata":{
       "description":"How long tooretain hello data in event hub"
     }
 }
```

### <a name="partitioncount"></a><span data-ttu-id="8a218-135">partitionCount</span><span class="sxs-lookup"><span data-stu-id="8a218-135">partitionCount</span></span>

<span data-ttu-id="8a218-136">Merhaba event hub'ındaki bölümleri toocreate Hello sayısı.</span><span class="sxs-lookup"><span data-stu-id="8a218-136">hello number of partitions toocreate in hello event hub.</span></span>

```json
"partitionCount":{
    "type":"int",
    "defaultValue":2,
    "minValue":2,
    "maxValue":32,
    "metadata":{
        "description":"Number of partitions chosen"
    }
 }
```

### <a name="captureenabled"></a><span data-ttu-id="8a218-137">captureEnabled</span><span class="sxs-lookup"><span data-stu-id="8a218-137">captureEnabled</span></span>

<span data-ttu-id="8a218-138">Yakalama hello olay hub'ına etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="8a218-138">Enable Capture on hello event hub.</span></span>

```json
"captureEnabled":{
    "type":"string",
    "defaultValue":"true",
    "allowedValues": [
    "false",
    "true"],
    "metadata":{
        "description":"Enable or disable hello Capture for your event hub"
    }
 }
```
### <a name="captureencodingformat"></a><span data-ttu-id="8a218-139">captureEncodingFormat</span><span class="sxs-lookup"><span data-stu-id="8a218-139">captureEncodingFormat</span></span>

<span data-ttu-id="8a218-140">Merhaba kodlama biçimi tooserialize hello olay verileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="8a218-140">hello encoding format you specify tooserialize hello event data.</span></span>

```json
"captureEncodingFormat":{
    "type":"string",
    "defaultValue":"Avro",
    "allowedValues":[
    "Avro"],
    "metadata":{
        "description":"hello encoding format in which Capture serializes hello EventData"
    }
}
```

### <a name="capturetime"></a><span data-ttu-id="8a218-141">captureTime</span><span class="sxs-lookup"><span data-stu-id="8a218-141">captureTime</span></span>

<span data-ttu-id="8a218-142">Merhaba zaman aralığı içinde olay hub'ları yakalama hello veri yakalamayı başlatır.</span><span class="sxs-lookup"><span data-stu-id="8a218-142">hello time interval in which Event Hubs Capture starts capturing hello data.</span></span>

```json
"captureTime":{
    "type":"int",
    "defaultValue":300,
    "minValue":60,
    "maxValue":900,
    "metadata":{
         "description":"hello time window in seconds for hello capture"
    }
}
```

### <a name="capturesize"></a><span data-ttu-id="8a218-143">captureSize</span><span class="sxs-lookup"><span data-stu-id="8a218-143">captureSize</span></span>
<span data-ttu-id="8a218-144">Başlangıç boyutu aralığı aktarılma hello veri yakalamayı yakalama başlatır.</span><span class="sxs-lookup"><span data-stu-id="8a218-144">hello size interval at which Capture starts capturing hello data.</span></span>

```json
"captureSize":{
    "type":"int",
    "defaultValue":314572800,
    "minValue":10485760,
    "maxValue":524288000,
    "metadata":{
        "description":"hello size window in bytes for capture"
    }
}
```

###<a name="capturenameformat"></a><span data-ttu-id="8a218-145">captureNameFormat</span><span class="sxs-lookup"><span data-stu-id="8a218-145">captureNameFormat</span></span>

<span data-ttu-id="8a218-146">Olay hub'ları yakalama toowrite hello Avro dosyalarının kullandığı hello adı biçimi.</span><span class="sxs-lookup"><span data-stu-id="8a218-146">hello name format used by Event Hubs Capture toowrite hello Avro files.</span></span> <span data-ttu-id="8a218-147">Yakalama adı biçimi `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}` ve `{Second}` alanlarını içermelidir.</span><span class="sxs-lookup"><span data-stu-id="8a218-147">Note that a Capture name format must contain `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}`, and `{Second}` fields.</span></span> <span data-ttu-id="8a218-148">Bu, herhangi bir sırada olabilir, sınırlayıcılar tercihe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="8a218-148">These can be arranged in any order, with or without delimiters.</span></span>
 
```json
"captureNameFormat": {
      "type": "string",
      "defaultValue": "{Namespace}/{EventHub}/{PartitionId}/{Year}/{Month}/{Day}/{Hour}/{Minute}/{Second}",
      "metadata": {
        "description": "A Capture Name Format must contain {Namespace}, {EventHub}, {PartitionId}, {Year}, {Month}, {Day}, {Hour}, {Minute} and {Second} fields. These can be arranged in any order with or without delimeters. E.g.  Prod_{EventHub}/{Namespace}\\{PartitionId}_{Year}_{Month}/{Day}/{Hour}/{Minute}/{Second}"
      }
    }
  }
```

### <a name="apiversion"></a><span data-ttu-id="8a218-149">apiVersion</span><span class="sxs-lookup"><span data-stu-id="8a218-149">apiVersion</span></span>

<span data-ttu-id="8a218-150">Merhaba şablon Hello API sürümü.</span><span class="sxs-lookup"><span data-stu-id="8a218-150">hello API version of hello template.</span></span>

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by hello template"
    }
 }
```

<span data-ttu-id="8a218-151">Hedef olarak Azure Storage'ı seçerseniz şu parametreler hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="8a218-151">Use hello following parameters if you choose Azure Storage as your destination.</span></span>

### <a name="destinationstorageaccountresourceid"></a><span data-ttu-id="8a218-152">destinationStorageAccountResourceId</span><span class="sxs-lookup"><span data-stu-id="8a218-152">destinationStorageAccountResourceId</span></span>

<span data-ttu-id="8a218-153">Yakalama tooyour yakalama bir Azure depolama hesabı kaynak kimliği tooenable istenen depolama hesabı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8a218-153">Capture requires an Azure Storage account resource ID tooenable capturing tooyour desired Storage account.</span></span>

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want hello blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a><span data-ttu-id="8a218-154">blobContainerName</span><span class="sxs-lookup"><span data-stu-id="8a218-154">blobContainerName</span></span>

<span data-ttu-id="8a218-155">hangi toocapture BLOB kapsayıcısında olay verilerinizi hello.</span><span class="sxs-lookup"><span data-stu-id="8a218-155">hello blob container in which toocapture your event data.</span></span>

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want hello blobs captured"
    }
}
```

<span data-ttu-id="8a218-156">Azure Data Lake Store, hedef olarak seçerseniz, şu parametreler hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="8a218-156">Use hello following parameters if you choose Azure Data Lake Store as your destination.</span></span> <span data-ttu-id="8a218-157">TooCapture hello olay istediğiniz, Data Lake Store yolunuza bağlı izinlerini ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a218-157">You must set permissions on your Data Lake Store path, in which you want tooCapture hello event.</span></span> <span data-ttu-id="8a218-158">bkz: tooset izinleri [bu makalede](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="8a218-158">tooset permissions, see [this article](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span></span>

###<a name="subscriptionid"></a><span data-ttu-id="8a218-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="8a218-159">subscriptionId</span></span>

<span data-ttu-id="8a218-160">Merhaba olay hub'ları ad alanı ve Azure Data Lake Store için abonelik kimliği.</span><span class="sxs-lookup"><span data-stu-id="8a218-160">Subscription ID for hello Event Hubs namespace and Azure Data Lake Store.</span></span> <span data-ttu-id="8a218-161">Her iki bu kaynakları hello altında olmalıdır aynı abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="8a218-161">Both these resources must be under hello same subscription ID.</span></span>

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a><span data-ttu-id="8a218-162">dataLakeAccountName</span><span class="sxs-lookup"><span data-stu-id="8a218-162">dataLakeAccountName</span></span>

<span data-ttu-id="8a218-163">Hello Azure Data Lake Store adı hello için olayları yakalandı.</span><span class="sxs-lookup"><span data-stu-id="8a218-163">hello Azure Data Lake Store name for hello captured events.</span></span>

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a><span data-ttu-id="8a218-164">dataLakeFolderPath</span><span class="sxs-lookup"><span data-stu-id="8a218-164">dataLakeFolderPath</span></span>

<span data-ttu-id="8a218-165">Merhaba hedef klasör yolu hello için olayları yakalandı.</span><span class="sxs-lookup"><span data-stu-id="8a218-165">hello destination folder path for hello captured events.</span></span>

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-toodeploy-for-azure-storage-as-destination-toocaptured-events"></a><span data-ttu-id="8a218-166">Azure depolama için kaynakları toodeploy de hedef toocaptured olayları</span><span class="sxs-lookup"><span data-stu-id="8a218-166">Resources toodeploy for Azure Storage as destination toocaptured events</span></span>

<span data-ttu-id="8a218-167">Türü bir ad oluşturur **EventHubs**bir olay hub'ı ve etkinleştirir tooAzure Blob Storage yakalayın.</span><span class="sxs-lookup"><span data-stu-id="8a218-167">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture tooAzure Blob Storage.</span></span>

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('eventHubNamespaceName')]",
         "type":"Microsoft.EventHub/Namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources":[  
            {  
               "apiVersion":"[variables('ehVersion')]",
               "name":"[parameters('eventHubName')]",
               "type":"EventHubs",
               "dependsOn":[  
                  "[concat('Microsoft.EventHub/namespaces/', parameters('eventHubNamespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]",
                  "MessageRetentionInDays":"[parameters('messageRetentionInDays')]",
                  "PartitionCount":"[parameters('partitionCount')]",
                  "CaptureDescription":{
                        "enabled":"[parameters('captureEnabled')]",
                        "encoding":"[parameters('captureEncodingFormat')]",
                        "intervalInSeconds":"[parameters('captureTime')]",
                        "sizeLimitInBytes":"[parameters('captureSize')]",
                        "destination":{
                            "name":"EventHubCapture.AzureBlockBlob",
                            "properties":{
                                "StorageAccountResourceId":"[parameters('destinationStorageAccountResourceId')]",
                                "BlobContainer":"[parameters('blobContainerName')]"
                            }
                        } 
                  }

               }

            }
         ]
      }
   ]
```

## <a name="resources-toodeploy-for-azure-data-lake-store-as-destination"></a><span data-ttu-id="8a218-168">Hedef olarak Azure Data Lake Store için kaynakları toodeploy</span><span class="sxs-lookup"><span data-stu-id="8a218-168">Resources toodeploy for Azure Data Lake Store as destination</span></span>

<span data-ttu-id="8a218-169">Tür bir ad oluşturur **EventHubs**bir olay hub'ı ve yakalama tooAzure Data Lake Store etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="8a218-169">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture tooAzure Data Lake Store.</span></span>

```json
 "resources": [
        {
            "apiVersion": "2015-08-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "2015-08-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('eventHubName')]",
                        "ArchiveDescription": {
                            "enabled": "true",
                            "encoding": "[parameters('archiveEncodingFormat')]",
                            "intervalInSeconds": "[parameters('archiveTime')]",
                            "sizeLimitInBytes": "[parameters('archiveSize')]",
                            "destination": {
                                "name": "EventHubArchive.AzureDataLake",
                                "properties": {
                                    "DataLakeSubscriptionId": "[parameters('subscriptionId')]",
                                    "DataLakeAccountName": "[parameters('dataLakeAccountName')]",
                                    "DataLakeFolderPath": "[parameters('dataLakeFolderPath')]",
                                    "ArchiveNameFormat": "[parameters('archiveNameFormat')]"
                                }
                            }
                        }
                    }
                }
            ]
        }
    ]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="8a218-170">Komutları toorun dağıtımı</span><span class="sxs-lookup"><span data-stu-id="8a218-170">Commands toorun deployment</span></span>

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="8a218-171">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a218-171">PowerShell</span></span>

<span data-ttu-id="8a218-172">Azure depolama alanına, şablon tooenable olay hub'ları yakalama dağıtın:</span><span class="sxs-lookup"><span data-stu-id="8a218-172">Deploy your template tooenable Event Hubs Capture into Azure Storage:</span></span>
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

<span data-ttu-id="8a218-173">Azure Data Lake Store, şablon tooenable olay hub'ları yakalama dağıtın:</span><span class="sxs-lookup"><span data-stu-id="8a218-173">Deploy your template tooenable Event Hubs Capture into Azure Data Lake Store:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="8a218-174">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8a218-174">Azure CLI</span></span>

<span data-ttu-id="8a218-175">Hedef olarak Azure Blob Depolamayı seçme:</span><span class="sxs-lookup"><span data-stu-id="8a218-175">Choosing Azure Blob Storage as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

<span data-ttu-id="8a218-176">Hedef olarak Azure Data Lake Store’u seçme:</span><span class="sxs-lookup"><span data-stu-id="8a218-176">Choosing Azure Data Lake Store as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="8a218-177">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8a218-177">Next steps</span></span>

<span data-ttu-id="8a218-178">Ayrıca olay hub'ları yakalama hello yapılandırabilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8a218-178">You can also configure Event Hubs Capture via hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8a218-179">Daha fazla bilgi için bkz: [etkinleştirmek olay hub'ları yakalama kullanarak hello Azure portal](event-hubs-capture-enable-through-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8a218-179">For more information, see [Enable Event Hubs Capture using hello Azure portal](event-hubs-capture-enable-through-portal.md).</span></span>

<span data-ttu-id="8a218-180">Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8a218-180">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="8a218-181">Event Hubs’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="8a218-181">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="8a218-182">Olay Hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8a218-182">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="8a218-183">Event Hubs ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="8a218-183">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture tooStorage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture tooAzure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls
