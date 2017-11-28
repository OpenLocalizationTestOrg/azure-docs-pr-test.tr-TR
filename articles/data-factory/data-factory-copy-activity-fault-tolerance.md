---
title: "Azure Data Factory kopyalama etkinliğinde aaaAdd hata toleransı uyumsuz satır atlanıyor tarafından | Microsoft Docs"
description: "Nasıl tooadd hataya dayanıklılık Azure Data Factory kopyalama etkinliğinde kopyalama sırasında uyumsuz satır atlayarak öğrenin"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: e7cf6117655910844b292d340674d8d631450a81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a><span data-ttu-id="c9f3e-103">Hataya dayanıklılık uyumsuz satır atlayarak kopyalama etkinliği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-103">Add fault tolerance in Copy Activity by skipping incompatible rows</span></span>

<span data-ttu-id="c9f3e-104">Azure Data Factory [kopyalama etkinliği](data-factory-data-movement-activities.md) kaynak ve havuz veri depoları arasında veri kopyalama işlemi sırasında iki yolla toohandle uyumsuz satırları sunar:</span><span class="sxs-lookup"><span data-stu-id="c9f3e-104">Azure Data Factory [Copy Activity](data-factory-data-movement-activities.md) offers you two ways toohandle incompatible rows when copying data between source and sink data stores:</span></span>

- <span data-ttu-id="c9f3e-105">İptal etmek ve hello kopya başarısız uyumsuz veriler olduğunda etkinliği karşılaştı (varsayılan davranıştır).</span><span class="sxs-lookup"><span data-stu-id="c9f3e-105">You can abort and fail hello copy activity when incompatible data is encountered (default behavior).</span></span>
- <span data-ttu-id="c9f3e-106">Toocopy devam edebilmeniz için tüm hata toleransı ekleyerek ve uyumsuz veri satırları atlanıyor hello verileri.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-106">You can continue toocopy all of hello data by adding fault tolerance and skipping incompatible data rows.</span></span> <span data-ttu-id="c9f3e-107">Ayrıca, Azure Blob depolama alanına hello uyumsuz satırları oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-107">In addition, you can log hello incompatible rows in Azure Blob storage.</span></span> <span data-ttu-id="c9f3e-108">Merhaba günlük toolearn hello hello başarısızlık nedeni inceleyin hello veri hello veri kaynağında düzeltin ve hello kopyalama etkinliği yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-108">You can then examine hello log toolearn hello cause for hello failure, fix hello data on hello data source, and retry hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="c9f3e-109">Desteklenen senaryolar</span><span class="sxs-lookup"><span data-stu-id="c9f3e-109">Supported scenarios</span></span>
<span data-ttu-id="c9f3e-110">Kopyalama etkinliği algılama, atlanıyor ve uyumsuz verilerini günlüğe kaydetme için üç senaryoları destekler:</span><span class="sxs-lookup"><span data-stu-id="c9f3e-110">Copy Activity supports three scenarios for detecting, skipping, and logging incompatible data:</span></span>

- <span data-ttu-id="c9f3e-111">**Merhaba kaynak veri türü ve hello havuz yerel türü arasında uyumsuzluk**</span><span class="sxs-lookup"><span data-stu-id="c9f3e-111">**Incompatibility between hello source data type and hello sink native type**</span></span>

    <span data-ttu-id="c9f3e-112">Örneğin: Blob Depolama tooa SQL bir CSV dosyasından veri Kopyala veritabanı üç içeren bir şema tanımı **INT** sütunları yazın.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-112">For example: Copy data from a CSV file in Blob storage tooa SQL database with a schema definition that contains three **INT** type columns.</span></span> <span data-ttu-id="c9f3e-113">sayısal veri gibi içeren CSV dosyası sıra hello `123,456,789` başarıyla kopyalandı toohello havuz deposu.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-113">hello CSV file rows that contain numeric data, such as `123,456,789` are copied successfully toohello sink store.</span></span> <span data-ttu-id="c9f3e-114">Ancak, gibi sayısal olmayan değerler içeren satırları hello `123,456,abc` uyumsuz algılanır ve atlanır.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-114">However, hello rows that contain non-numeric values, such as `123,456,abc` are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="c9f3e-115">**Merhaba sütun sayısı olarak hello kaynak ve hello havuz arasında uyuşmazlık**</span><span class="sxs-lookup"><span data-stu-id="c9f3e-115">**Mismatch in hello number of columns between hello source and hello sink**</span></span>

    <span data-ttu-id="c9f3e-116">Örneğin: Blob Depolama tooa SQL bir CSV dosyasından veri Kopyala veritabanı altı sütunları içeren bir şema tanımı.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-116">For example: Copy data from a CSV file in Blob storage tooa SQL database with a schema definition that contains six columns.</span></span> <span data-ttu-id="c9f3e-117">Merhaba altı sütunlar içeren satırlar CSV dosyası başarıyla toohello havuz saklayın.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-117">hello CSV file rows that contain six columns are copied successfully toohello sink store.</span></span> <span data-ttu-id="c9f3e-118">Daha fazla veya az altı sütunları içeren hello CSV dosyası satırları uyumsuz olarak algılanır ve atlanır.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-118">hello CSV file rows that contain more or fewer than six columns are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="c9f3e-119">**Tooa ilişkisel veritabanı yazılırken birincil anahtar ihlali**</span><span class="sxs-lookup"><span data-stu-id="c9f3e-119">**Primary key violation when writing tooa relational database**</span></span>

    <span data-ttu-id="c9f3e-120">Örneğin: bir SQL server tooa SQL veritabanından veri kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-120">For example: Copy data from a SQL server tooa SQL database.</span></span> <span data-ttu-id="c9f3e-121">Merhaba havuz SQL veritabanında tanımlı bir birincil anahtara, ancak böyle bir birincil anahtar hello kaynak SQL Server'da tanımlanmadı.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-121">A primary key is defined in hello sink SQL database, but no such primary key is defined in hello source SQL server.</span></span> <span data-ttu-id="c9f3e-122">Merhaba kaynağında mevcut hello yinelenen satırları kopyalanan toohello havuz olamaz.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-122">hello duplicated rows that exist in hello source cannot be copied toohello sink.</span></span> <span data-ttu-id="c9f3e-123">Kopyalama etkinliği yalnızca hello verilerin ilk satırında hello kaynak hello havuz kopyalar.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-123">Copy Activity copies only hello first row of hello source data into hello sink.</span></span> <span data-ttu-id="c9f3e-124">Merhaba hello yinelenen birincil anahtar değeri içeren sonraki kaynak satırları uyumsuz olarak algılanır ve atlanır.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-124">hello subsequent source rows that contain hello duplicated primary key value are detected as incompatible and are skipped.</span></span>

## <a name="configuration"></a><span data-ttu-id="c9f3e-125">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c9f3e-125">Configuration</span></span>
<span data-ttu-id="c9f3e-126">Merhaba aşağıdaki örnek hello uyumsuz satırları kopyalama etkinliğinde atlanıyor JSON tanımı tooconfigure sağlar:</span><span class="sxs-lookup"><span data-stu-id="c9f3e-126">hello following example provides a JSON definition tooconfigure skipping hello incompatible rows in Copy Activity:</span></span>

```json
"typeProperties": {
    "source": {
        "type": "BlobSource"
    },
    "sink": {
        "type": "SqlSink",
    },         
    "enableSkipIncompatibleRow": true,           
    "redirectIncompatibleRowSettings": {
        "linkedServiceName": "BlobStorage",
        "path": "redirectcontainer/erroroutput"
    }
}
```

| <span data-ttu-id="c9f3e-127">Özellik</span><span class="sxs-lookup"><span data-stu-id="c9f3e-127">Property</span></span> | <span data-ttu-id="c9f3e-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c9f3e-128">Description</span></span> | <span data-ttu-id="c9f3e-129">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="c9f3e-129">Allowed values</span></span> | <span data-ttu-id="c9f3e-130">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c9f3e-130">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c9f3e-131">**enableSkipIncompatibleRow**</span><span class="sxs-lookup"><span data-stu-id="c9f3e-131">**enableSkipIncompatibleRow**</span></span> | <span data-ttu-id="c9f3e-132">Atlanıyor uyumsuz satırları kopyalama sırasında veya etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-132">Enable skipping incompatible rows during copy or not.</span></span> | <span data-ttu-id="c9f3e-133">True</span><span class="sxs-lookup"><span data-stu-id="c9f3e-133">True</span></span><br/><span data-ttu-id="c9f3e-134">False (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="c9f3e-134">False (default)</span></span> | <span data-ttu-id="c9f3e-135">Hayır</span><span class="sxs-lookup"><span data-stu-id="c9f3e-135">No</span></span> |
| <span data-ttu-id="c9f3e-136">**redirectIncompatibleRowSettings**</span><span class="sxs-lookup"><span data-stu-id="c9f3e-136">**redirectIncompatibleRowSettings**</span></span> | <span data-ttu-id="c9f3e-137">Bir grup olabilir özellik toolog hello uyumsuz satırları istediğinizde belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-137">A group of properties that can be specified when you want toolog hello incompatible rows.</span></span> | &nbsp; | <span data-ttu-id="c9f3e-138">Hayır</span><span class="sxs-lookup"><span data-stu-id="c9f3e-138">No</span></span> |
| <span data-ttu-id="c9f3e-139">**linkedServiceName**</span><span class="sxs-lookup"><span data-stu-id="c9f3e-139">**linkedServiceName**</span></span> | <span data-ttu-id="c9f3e-140">Merhaba bağlı hizmeti Azure Storage toostore hello günlüğünün atlandı hello satırları içeren.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-140">hello linked service of Azure Storage toostore hello log that contains hello skipped rows.</span></span> | <span data-ttu-id="c9f3e-141">Merhaba adını bir [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) veya [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) bağlantılı toouse toostore hello günlük dosyası istediğiniz toohello depolama örneğini başvuruyor hizmeti.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-141">hello name of an [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) linked service, which refers toohello storage instance that you want toouse toostore hello log file.</span></span> | <span data-ttu-id="c9f3e-142">Hayır</span><span class="sxs-lookup"><span data-stu-id="c9f3e-142">No</span></span> |
| <span data-ttu-id="c9f3e-143">**yol**</span><span class="sxs-lookup"><span data-stu-id="c9f3e-143">**path**</span></span> | <span data-ttu-id="c9f3e-144">Merhaba içeren hello günlük dosyası yolu Hello satır atlandı.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-144">hello path of hello log file that contains hello skipped rows.</span></span> | <span data-ttu-id="c9f3e-145">Toouse toolog hello uyumsuz veri istediğiniz hello Blob Depolama Birimi yolu belirtin.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-145">Specify hello Blob storage path that you want toouse toolog hello incompatible data.</span></span> <span data-ttu-id="c9f3e-146">Bir yol belirtmezseniz, hello hizmeti sizin için bir kapsayıcı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-146">If you do not provide a path, hello service creates a container for you.</span></span> | <span data-ttu-id="c9f3e-147">Hayır</span><span class="sxs-lookup"><span data-stu-id="c9f3e-147">No</span></span> |

## <a name="monitoring"></a><span data-ttu-id="c9f3e-148">İzleme</span><span class="sxs-lookup"><span data-stu-id="c9f3e-148">Monitoring</span></span>
<span data-ttu-id="c9f3e-149">Çalıştırma hello kopyalama etkinliği tamamlandıktan sonra bölüm izleme hello Atlanan satır sayısı hello görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c9f3e-149">After hello copy activity run completes, you can see hello number of skipped rows in hello monitoring section:</span></span>

![İzleyici uyumsuz satır atlandı](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

<span data-ttu-id="c9f3e-151">Toolog hello uyumsuz satırları yapılandırırsanız, bu yolda hello günlük dosyasını bulabilirsiniz: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` hello günlük dosyasında, atlanan hello satırları görebilir ve hello hello uyumsuzluk kök nedenini.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-151">If you configure toolog hello incompatible rows, you can find hello log file at this path: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In hello log file, you can see hello rows that were skipped and hello root cause of hello incompatibility.</span></span>

<span data-ttu-id="c9f3e-152">Merhaba özgün veriler ve hello karşılık gelen hata hello dosyasına kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="c9f3e-152">Both hello original data and hello corresponding error are logged in hello file.</span></span> <span data-ttu-id="c9f3e-153">Merhaba günlük dosyası içeriğine bir örnek aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="c9f3e-153">An example of hello log file content is as follows:</span></span>
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' tootype 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. hello duplicate key value is (data4).
```

## <a name="next-steps"></a><span data-ttu-id="c9f3e-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c9f3e-154">Next steps</span></span>
<span data-ttu-id="c9f3e-155">Azure Data Factory kopyalama etkinliği hakkında daha fazla toolearn bkz [Kopyala etkinliğini kullanarak veri taşıma](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c9f3e-155">toolearn more about Azure Data Factory Copy Activity, see [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>
