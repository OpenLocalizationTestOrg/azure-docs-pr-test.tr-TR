---
title: "Azure Event Hubs ad alanı oluşturma ve şablon kullanarak Yakalamayı etkinleştirme | Microsoft Docs"
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
ms.openlocfilehash: 19bbb51868e767aa1d15f4574628b7fd36607207
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a><span data-ttu-id="a45f6-103">Bir olay hub'ı ile bir Event Hubs ad alanı oluşturma ve Azure Resource Manager şablonu kullanarak Yakalamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="a45f6-103">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>

<span data-ttu-id="a45f6-104">Bu makalede, bir olay hub’ı örneği ile Event Hubs ad alanı oluşturan ve olay hub’ında [Yakalama özelliğini](event-hubs-capture-overview.md) etkinleştiren Azure Resource Manager şablonunun nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a45f6-104">This article shows how to use an Azure Resource Manager template that creates an Event Hubs namespace, with one event hub instance, and also enables the [Capture feature](event-hubs-capture-overview.md) on the event hub.</span></span> <span data-ttu-id="a45f6-105">Makalede, hangi kaynakların dağıtıldığının ve dağıtım yürütülürken belirtilen parametrelerin nasıl tanımlanacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a45f6-105">The article describes how to define which resources are deployed, and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="a45f6-106">Bu şablonu kendi dağıtımlarınız için kullanabilir veya kendi gereksinimlerinize göre özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a45f6-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="a45f6-107">Bu makalede ayrıca seçtiğiniz hedefe göre olayları Azure Storage Bloblarında veya bir Azure Data Lake Store’da yakalamayı belirteceğiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a45f6-107">This article also shows how to specify that events are captured into either Azure Storage Blobs or an Azure Data Lake Store, based on the destination you choose.</span></span>

<span data-ttu-id="a45f6-108">Şablon oluşturma hakkında daha fazla bilgi için bkz. [Azure Resource Manager şablonları yazma][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="a45f6-108">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="a45f6-109">Azure Kaynakları adlandırma kurallarına ilişkin uygulama ve yapılar için bkz. [Azure Kaynakları Adlandırma Kuralları][Azure Resources naming conventions].</span><span class="sxs-lookup"><span data-stu-id="a45f6-109">For more information about patterns and practices for Azure Resources naming conventions, see [Azure Resources naming conventions][Azure Resources naming conventions].</span></span>

<span data-ttu-id="a45f6-110">Tam şablonlar için aşağıdaki GitHub bağlantılarına tıklayın:</span><span class="sxs-lookup"><span data-stu-id="a45f6-110">For the complete templates, click the following GitHub links:</span></span>

- <span data-ttu-id="a45f6-111">[Olay hub'ı ve Depolama alanına Yakalamayı etkinleştirme şablonu][Event Hub and enable Capture to Storage template]</span><span class="sxs-lookup"><span data-stu-id="a45f6-111">[Event hub and enable Capture to Storage template][Event Hub and enable Capture to Storage template]</span></span> 
- <span data-ttu-id="a45f6-112">[Olay hub'ı ve Azure Data Lake Store’a Yakalamayı etkinleştirme şablonu][Event Hub and enable Capture to Azure Data Lake Store template]</span><span class="sxs-lookup"><span data-stu-id="a45f6-112">[Event hub and enable Capture to Azure Data Lake Store template][Event Hub and enable Capture to Azure Data Lake Store template]</span></span>

> [!NOTE]
> <span data-ttu-id="a45f6-113">En yeni şablonları denetlemek için [Azure Hızlı Başlangıç Şablonları][Azure Quickstart Templates] galerisini ziyaret edin ve Event Hubs araması yapın.</span><span class="sxs-lookup"><span data-stu-id="a45f6-113">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="a45f6-114">Ne dağıtacaksınız?</span><span class="sxs-lookup"><span data-stu-id="a45f6-114">What will you deploy?</span></span>

<span data-ttu-id="a45f6-115">Bu şablonu kullanarak bir olay hub’ı ile Event Hubs ad alanı dağıtır ve aynı zamanda [Event Hubs Yakalama](event-hubs-capture-overview.md) özelliğini etkinleştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a45f6-115">With this template, you deploy an Event Hubs namespace with an event hub, and also enable [Event Hubs Capture](event-hubs-capture-overview.md).</span></span>

<span data-ttu-id="a45f6-116">[Event Hubs](event-hubs-what-is-event-hubs.md), düşük gecikme süresi ve yüksek güvenilirlikle Azure’a büyük ölçekte olay ve telemetri girişi sağlayan bir olay işleme hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="a45f6-116">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used to provide event and telemetry ingress to Azure at massive scale, with low latency and high reliability.</span></span> <span data-ttu-id="a45f6-117">Event Hubs Yakalama özelliği, tercih ettiğiniz bir süre veya boyut aralığı içinde Event Hubs’dan Azure Blob depolama alanına veya Azure Data Lake Store’a akış verilerini otomatik olarak iletmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a45f6-117">Event Hubs Capture enables you to automatically deliver the streaming data in Event Hubs to Azure Blob storage or Azure Data Lake Store, within a specified time or size interval of your choosing.</span></span>

<span data-ttu-id="a45f6-118">Event Hubs Yakalama özelliğini Azure Depolamada etkinleştirmek için aşağıdaki düğmeye tıklayın:</span><span class="sxs-lookup"><span data-stu-id="a45f6-118">Click the following button to enable Event Hubs Capture into Azure Storage:</span></span>

<span data-ttu-id="a45f6-119">[![Azure’a dağıtma](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="a45f6-119">[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span></span>

<span data-ttu-id="a45f6-120">Event Hubs Yakalama özelliğini Azure Data Lake Store’da etkinleştirmek için aşağıdaki düğmeye tıklayın:</span><span class="sxs-lookup"><span data-stu-id="a45f6-120">Click the following button to enable Event Hubs Capture into Azure Data Lake Store:</span></span>

<span data-ttu-id="a45f6-121">[![Azure’a dağıtma](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="a45f6-121">[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="a45f6-122">Parametreler</span><span class="sxs-lookup"><span data-stu-id="a45f6-122">Parameters</span></span>

<span data-ttu-id="a45f6-123">Azure Resource Manager sayesinde, şablon dağıtıldığında belirtmek istediğiniz değerlerin parametrelerini siz tanımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="a45f6-123">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="a45f6-124">Şablon, tüm parametre değerlerini içeren `Parameters` adlı bir bölüm içerir.</span><span class="sxs-lookup"><span data-stu-id="a45f6-124">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="a45f6-125">Dağıtmakta olduğunuz projeye veya dağıtım yaptığınız ortama göre değişen değerler için bir parametre tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a45f6-125">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="a45f6-126">Her zaman aynı kalan değerler için parametre tanımlamayın.</span><span class="sxs-lookup"><span data-stu-id="a45f6-126">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="a45f6-127">Her parametre değeri, dağıtılan kaynakları tanımlamak için şablonda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a45f6-127">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="a45f6-128">Şablon aşağıdaki parametreleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a45f6-128">The template defines the following parameters.</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="a45f6-129">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="a45f6-129">eventHubNamespaceName</span></span>

<span data-ttu-id="a45f6-130">Oluşturulacak [Event Hubs ad alanının](event-hubs-create.md) adı.</span><span class="sxs-lookup"><span data-stu-id="a45f6-130">The name of the [Event Hubs namespace](event-hubs-create.md) to create.</span></span>

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of the EventHub namespace"
      }
}
```

### <a name="eventhubname"></a><span data-ttu-id="a45f6-131">eventHubName</span><span class="sxs-lookup"><span data-stu-id="a45f6-131">eventHubName</span></span>

<span data-ttu-id="a45f6-132">[Event Hubs ad alanında](event-hubs-create.md) oluşturulan olay hub’ının adı.</span><span class="sxs-lookup"><span data-stu-id="a45f6-132">The name of the event hub created in the [Event Hubs namespace](event-hubs-create.md).</span></span>

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of the event hub"
    }
}
```

### <a name="messageretentionindays"></a><span data-ttu-id="a45f6-133">messageRetentionInDays</span><span class="sxs-lookup"><span data-stu-id="a45f6-133">messageRetentionInDays</span></span>

<span data-ttu-id="a45f6-134">İletilerin olay hub'ında tutulacağı gün sayısı.</span><span class="sxs-lookup"><span data-stu-id="a45f6-134">The number of days to retain the messages in the event hub.</span></span> 

```json
"messageRetentionInDays":{
    "type":"int",
    "defaultValue": 1,
    "minValue":"1",
    "maxValue":"7",
    "metadata":{
       "description":"How long to retain the data in event hub"
     }
 }
```

### <a name="partitioncount"></a><span data-ttu-id="a45f6-135">partitionCount</span><span class="sxs-lookup"><span data-stu-id="a45f6-135">partitionCount</span></span>

<span data-ttu-id="a45f6-136">Olay hub'ında oluşturulacak bölüm sayısı.</span><span class="sxs-lookup"><span data-stu-id="a45f6-136">The number of partitions to create in the event hub.</span></span>

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

### <a name="captureenabled"></a><span data-ttu-id="a45f6-137">captureEnabled</span><span class="sxs-lookup"><span data-stu-id="a45f6-137">captureEnabled</span></span>

<span data-ttu-id="a45f6-138">Olay hub’ında Yakalama özelliğini etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="a45f6-138">Enable Capture on the event hub.</span></span>

```json
"captureEnabled":{
    "type":"string",
    "defaultValue":"true",
    "allowedValues": [
    "false",
    "true"],
    "metadata":{
        "description":"Enable or disable the Capture for your event hub"
    }
 }
```
### <a name="captureencodingformat"></a><span data-ttu-id="a45f6-139">captureEncodingFormat</span><span class="sxs-lookup"><span data-stu-id="a45f6-139">captureEncodingFormat</span></span>

<span data-ttu-id="a45f6-140">Olay verilerini seri hale getirmek için belirttiğiniz kodlama biçimi.</span><span class="sxs-lookup"><span data-stu-id="a45f6-140">The encoding format you specify to serialize the event data.</span></span>

```json
"captureEncodingFormat":{
    "type":"string",
    "defaultValue":"Avro",
    "allowedValues":[
    "Avro"],
    "metadata":{
        "description":"The encoding format in which Capture serializes the EventData"
    }
}
```

### <a name="capturetime"></a><span data-ttu-id="a45f6-141">captureTime</span><span class="sxs-lookup"><span data-stu-id="a45f6-141">captureTime</span></span>

<span data-ttu-id="a45f6-142">Event Hubs Yakalama özelliğinin veri yakalamaya başladığı zaman aralığı.</span><span class="sxs-lookup"><span data-stu-id="a45f6-142">The time interval in which Event Hubs Capture starts capturing the data.</span></span>

```json
"captureTime":{
    "type":"int",
    "defaultValue":300,
    "minValue":60,
    "maxValue":900,
    "metadata":{
         "description":"the time window in seconds for the capture"
    }
}
```

### <a name="capturesize"></a><span data-ttu-id="a45f6-143">captureSize</span><span class="sxs-lookup"><span data-stu-id="a45f6-143">captureSize</span></span>
<span data-ttu-id="a45f6-144">Yakalama özelliğinin veri yakalamaya başladığı boyut aralığı.</span><span class="sxs-lookup"><span data-stu-id="a45f6-144">The size interval at which Capture starts capturing the data.</span></span>

```json
"captureSize":{
    "type":"int",
    "defaultValue":314572800,
    "minValue":10485760,
    "maxValue":524288000,
    "metadata":{
        "description":"The size window in bytes for capture"
    }
}
```

###<a name="capturenameformat"></a><span data-ttu-id="a45f6-145">captureNameFormat</span><span class="sxs-lookup"><span data-stu-id="a45f6-145">captureNameFormat</span></span>

<span data-ttu-id="a45f6-146">Event Hubs Yakalama özelliği tarafından Avro dosyalarını yazmak için kullanılan ad biçimi.</span><span class="sxs-lookup"><span data-stu-id="a45f6-146">The name format used by Event Hubs Capture to write the Avro files.</span></span> <span data-ttu-id="a45f6-147">Yakalama adı biçimi `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}` ve `{Second}` alanlarını içermelidir.</span><span class="sxs-lookup"><span data-stu-id="a45f6-147">Note that a Capture name format must contain `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}`, and `{Second}` fields.</span></span> <span data-ttu-id="a45f6-148">Bu, herhangi bir sırada olabilir, sınırlayıcılar tercihe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="a45f6-148">These can be arranged in any order, with or without delimiters.</span></span>
 
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

### <a name="apiversion"></a><span data-ttu-id="a45f6-149">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a45f6-149">apiVersion</span></span>

<span data-ttu-id="a45f6-150">Şablonun API sürümü.</span><span class="sxs-lookup"><span data-stu-id="a45f6-150">The API version of the template.</span></span>

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by the template"
    }
 }
```

<span data-ttu-id="a45f6-151">Hedef olarak Azure Depolama’yı seçerseniz aşağıdaki parametreleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="a45f6-151">Use the following parameters if you choose Azure Storage as your destination.</span></span>

### <a name="destinationstorageaccountresourceid"></a><span data-ttu-id="a45f6-152">destinationStorageAccountResourceId</span><span class="sxs-lookup"><span data-stu-id="a45f6-152">destinationStorageAccountResourceId</span></span>

<span data-ttu-id="a45f6-153">Yakalama özelliğinin istediğiniz Depolama hesabında yakalamayı etkinleştirmesi için bir Azure Depolama hesabı kaynak kimliği gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a45f6-153">Capture requires an Azure Storage account resource ID to enable capturing to your desired Storage account.</span></span>

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want the blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a><span data-ttu-id="a45f6-154">blobContainerName</span><span class="sxs-lookup"><span data-stu-id="a45f6-154">blobContainerName</span></span>

<span data-ttu-id="a45f6-155">Olay verilerinin yakalanacağı blob kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="a45f6-155">The blob container in which to capture your event data.</span></span>

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want the blobs captured"
    }
}
```

<span data-ttu-id="a45f6-156">Hedef olarak Azure Data Lake Store’u seçerseniz aşağıdaki parametreleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="a45f6-156">Use the following parameters if you choose Azure Data Lake Store as your destination.</span></span> <span data-ttu-id="a45f6-157">Olayı yakalamak istediğiniz Data Lake Store yolunuzda izinleri ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a45f6-157">You must set permissions on your Data Lake Store path, in which you want to Capture the event.</span></span> <span data-ttu-id="a45f6-158">İzinleri ayarlamak için [bu makaleye](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account) bakın.</span><span class="sxs-lookup"><span data-stu-id="a45f6-158">To set permissions, see [this article](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span></span>

###<a name="subscriptionid"></a><span data-ttu-id="a45f6-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="a45f6-159">subscriptionId</span></span>

<span data-ttu-id="a45f6-160">Azure Data Lake Store ve Event Hubs ad alanı için abonelik kimliği.</span><span class="sxs-lookup"><span data-stu-id="a45f6-160">Subscription ID for the Event Hubs namespace and Azure Data Lake Store.</span></span> <span data-ttu-id="a45f6-161">Bu iki kaynağın aynı abonelik kimliği altında olması gerekir</span><span class="sxs-lookup"><span data-stu-id="a45f6-161">Both these resources must be under the same subscription ID.</span></span>

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a><span data-ttu-id="a45f6-162">dataLakeAccountName</span><span class="sxs-lookup"><span data-stu-id="a45f6-162">dataLakeAccountName</span></span>

<span data-ttu-id="a45f6-163">Yakalanan olaylar için Azure Data Lake Store adı.</span><span class="sxs-lookup"><span data-stu-id="a45f6-163">The Azure Data Lake Store name for the captured events.</span></span>

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a><span data-ttu-id="a45f6-164">dataLakeFolderPath</span><span class="sxs-lookup"><span data-stu-id="a45f6-164">dataLakeFolderPath</span></span>

<span data-ttu-id="a45f6-165">Yakalanan olaylar için hedef klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="a45f6-165">The destination folder path for the captured events.</span></span>

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-to-deploy-for-azure-storage-as-destination-to-captured-events"></a><span data-ttu-id="a45f6-166">Yakalanan olaylar için hedef olarak Azure Depolama kullanıldığında dağıtılacak kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a45f6-166">Resources to deploy for Azure Storage as destination to captured events</span></span>

<span data-ttu-id="a45f6-167">Bir olay hub’ı ile **EventHubs** türünde bir ad alanı oluşturur ve aynı zamanda Azure Blob Depolama’ya Yakalama özelliğini etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="a45f6-167">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture to Azure Blob Storage.</span></span>

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

## <a name="resources-to-deploy-for-azure-data-lake-store-as-destination"></a><span data-ttu-id="a45f6-168">Hedef olarak Azure Data Lake Store kullanıldığında dağıtılacak kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a45f6-168">Resources to deploy for Azure Data Lake Store as destination</span></span>

<span data-ttu-id="a45f6-169">Bir olay hub’ı ile **EventHubs** türünde bir ad alanı oluşturur ve aynı zamanda Azure Data Lake Store’a Yakalama özelliğini etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="a45f6-169">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture to Azure Data Lake Store.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="a45f6-170">Dağıtımı çalıştırma komutları</span><span class="sxs-lookup"><span data-stu-id="a45f6-170">Commands to run deployment</span></span>

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="a45f6-171">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a45f6-171">PowerShell</span></span>

<span data-ttu-id="a45f6-172">Azure Depolamada Event Hubs Yakalama özelliğini etkinleştirmek için şablonunuzu dağıtın:</span><span class="sxs-lookup"><span data-stu-id="a45f6-172">Deploy your template to enable Event Hubs Capture into Azure Storage:</span></span>
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

<span data-ttu-id="a45f6-173">Azure Data Lake Store’da Event Hubs Yakalama özelliğini etkinleştirmek için şablonunuzu dağıtın:</span><span class="sxs-lookup"><span data-stu-id="a45f6-173">Deploy your template to enable Event Hubs Capture into Azure Data Lake Store:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="a45f6-174">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a45f6-174">Azure CLI</span></span>

<span data-ttu-id="a45f6-175">Hedef olarak Azure Blob Depolamayı seçme:</span><span class="sxs-lookup"><span data-stu-id="a45f6-175">Choosing Azure Blob Storage as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

<span data-ttu-id="a45f6-176">Hedef olarak Azure Data Lake Store’u seçme:</span><span class="sxs-lookup"><span data-stu-id="a45f6-176">Choosing Azure Data Lake Store as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="a45f6-177">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a45f6-177">Next steps</span></span>

<span data-ttu-id="a45f6-178">Event Hubs Yakalama özelliğini [Azure portalı](https://portal.azure.com) üzerinden de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a45f6-178">You can also configure Event Hubs Capture via the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a45f6-179">Daha fazla bilgi için bkz. [Azure portalını kullanarak Event Hubs Yakalama özelliğini etkinleştirme](event-hubs-capture-enable-through-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a45f6-179">For more information, see [Enable Event Hubs Capture using the Azure portal](event-hubs-capture-enable-through-portal.md).</span></span>

<span data-ttu-id="a45f6-180">Aşağıdaki bağlantıları inceleyerek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a45f6-180">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="a45f6-181">Event Hubs’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="a45f6-181">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="a45f6-182">Olay Hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a45f6-182">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="a45f6-183">Event Hubs ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="a45f6-183">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture to Storage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture to Azure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls