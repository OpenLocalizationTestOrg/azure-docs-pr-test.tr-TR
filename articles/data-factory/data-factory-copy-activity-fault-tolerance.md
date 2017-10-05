---
title: "Hataya dayanıklılık uyumsuz satır atlayarak Azure Data Factory kopyalama etkinliği ekleyin | Microsoft Docs"
description: "Kopyalama sırasında uyumsuz satır atlayarak hata toleransı Azure Data Factory kopyalama etkinliği eklemeyi öğrenin"
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
ms.openlocfilehash: e2a108752259d5da3b401666c6bdbaad13b7ea90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a><span data-ttu-id="c091a-103">Hataya dayanıklılık uyumsuz satır atlayarak kopyalama etkinliği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c091a-103">Add fault tolerance in Copy Activity by skipping incompatible rows</span></span>

<span data-ttu-id="c091a-104">Azure Data Factory [kopyalama etkinliği](data-factory-data-movement-activities.md) uyumsuz satırları kaynak ve havuz veri depoları arasında veri kopyalama işlemi sırasında işleme için iki yol sunar:</span><span class="sxs-lookup"><span data-stu-id="c091a-104">Azure Data Factory [Copy Activity](data-factory-data-movement-activities.md) offers you two ways to handle incompatible rows when copying data between source and sink data stores:</span></span>

- <span data-ttu-id="c091a-105">İptal etmek ve kopyalama başarısız uyumsuz veriler olduğunda etkinliği karşılaştı (varsayılan davranıştır).</span><span class="sxs-lookup"><span data-stu-id="c091a-105">You can abort and fail the copy activity when incompatible data is encountered (default behavior).</span></span>
- <span data-ttu-id="c091a-106">Tüm verileri hata toleransı ekleme ve uyumsuz veri satırları atlanıyor kopyalama devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c091a-106">You can continue to copy all of the data by adding fault tolerance and skipping incompatible data rows.</span></span> <span data-ttu-id="c091a-107">Ayrıca, Azure Blob depolama alanına uyumsuz satırları oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="c091a-107">In addition, you can log the incompatible rows in Azure Blob storage.</span></span> <span data-ttu-id="c091a-108">Ardından, hatanın nedenini öğrenmek, veri kaynağındaki verileri düzeltin ve kopyalama etkinliği yeniden deneme için günlüğünü de inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c091a-108">You can then examine the log to learn the cause for the failure, fix the data on the data source, and retry the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="c091a-109">Desteklenen senaryolar</span><span class="sxs-lookup"><span data-stu-id="c091a-109">Supported scenarios</span></span>
<span data-ttu-id="c091a-110">Kopyalama etkinliği algılama, atlanıyor ve uyumsuz verilerini günlüğe kaydetme için üç senaryoları destekler:</span><span class="sxs-lookup"><span data-stu-id="c091a-110">Copy Activity supports three scenarios for detecting, skipping, and logging incompatible data:</span></span>

- <span data-ttu-id="c091a-111">**Kaynak veri türü ve havuz yerel türü arasında uyumsuzluk**</span><span class="sxs-lookup"><span data-stu-id="c091a-111">**Incompatibility between the source data type and the sink native type**</span></span>

    <span data-ttu-id="c091a-112">Örneğin: veri kopyalama bir Blob depolamada CSV dosyasından üç içeren bir şema tanımı olan bir SQL veritabanına **INT** sütunları yazın.</span><span class="sxs-lookup"><span data-stu-id="c091a-112">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains three **INT** type columns.</span></span> <span data-ttu-id="c091a-113">Sayısal veri gibi içeren CSV dosyası satırları `123,456,789` havuz deposuna başarıyla kopyalandı.</span><span class="sxs-lookup"><span data-stu-id="c091a-113">The CSV file rows that contain numeric data, such as `123,456,789` are copied successfully to the sink store.</span></span> <span data-ttu-id="c091a-114">Ancak, satırları içeren sayısal olmayan değerleri gibi `123,456,abc` uyumsuz algılanır ve atlanır.</span><span class="sxs-lookup"><span data-stu-id="c091a-114">However, the rows that contain non-numeric values, such as `123,456,abc` are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="c091a-115">**Kaynak ve havuz arasında sütun sayısı uyuşmazlığı**</span><span class="sxs-lookup"><span data-stu-id="c091a-115">**Mismatch in the number of columns between the source and the sink**</span></span>

    <span data-ttu-id="c091a-116">Örneğin: veri kopyalama bir Blob depolamada CSV dosyasından altı sütunları içeren bir şema tanımı olan bir SQL veritabanına.</span><span class="sxs-lookup"><span data-stu-id="c091a-116">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains six columns.</span></span> <span data-ttu-id="c091a-117">Altı sütunları içeren CSV dosyası satırları başarıyla havuz deposuna kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="c091a-117">The CSV file rows that contain six columns are copied successfully to the sink store.</span></span> <span data-ttu-id="c091a-118">Daha fazla veya az altı sütunları içeren CSV dosyası satırları uyumsuz olarak algılanır ve atlanır.</span><span class="sxs-lookup"><span data-stu-id="c091a-118">The CSV file rows that contain more or fewer than six columns are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="c091a-119">**İlişkisel bir veritabanına yazılırken birincil anahtar ihlali**</span><span class="sxs-lookup"><span data-stu-id="c091a-119">**Primary key violation when writing to a relational database**</span></span>

    <span data-ttu-id="c091a-120">Örneğin: veri kopyalama SQL Server'dan SQL veritabanına.</span><span class="sxs-lookup"><span data-stu-id="c091a-120">For example: Copy data from a SQL server to a SQL database.</span></span> <span data-ttu-id="c091a-121">Havuz SQL veritabanında tanımlı bir birincil anahtara, ancak böyle bir birincil anahtar kaynak SQL Server'da tanımlanmadı.</span><span class="sxs-lookup"><span data-stu-id="c091a-121">A primary key is defined in the sink SQL database, but no such primary key is defined in the source SQL server.</span></span> <span data-ttu-id="c091a-122">Havuz için kaynak olarak mevcut yinelenen satırları kopyalanamaz.</span><span class="sxs-lookup"><span data-stu-id="c091a-122">The duplicated rows that exist in the source cannot be copied to the sink.</span></span> <span data-ttu-id="c091a-123">Kopyalama etkinliği yalnızca ilk satır kaynak verilerin havuz kopyalar.</span><span class="sxs-lookup"><span data-stu-id="c091a-123">Copy Activity copies only the first row of the source data into the sink.</span></span> <span data-ttu-id="c091a-124">Yinelenen birincil anahtar değeri içeren sonraki kaynak satırları uyumsuz olarak algılanır ve atlanır.</span><span class="sxs-lookup"><span data-stu-id="c091a-124">The subsequent source rows that contain the duplicated primary key value are detected as incompatible and are skipped.</span></span>

## <a name="configuration"></a><span data-ttu-id="c091a-125">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c091a-125">Configuration</span></span>
<span data-ttu-id="c091a-126">Aşağıdaki örnek kopyalama etkinliği uyumsuz satırları atlanıyor yapılandırmak için JSON tanımını sağlar:</span><span class="sxs-lookup"><span data-stu-id="c091a-126">The following example provides a JSON definition to configure skipping the incompatible rows in Copy Activity:</span></span>

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

| <span data-ttu-id="c091a-127">Özellik</span><span class="sxs-lookup"><span data-stu-id="c091a-127">Property</span></span> | <span data-ttu-id="c091a-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c091a-128">Description</span></span> | <span data-ttu-id="c091a-129">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="c091a-129">Allowed values</span></span> | <span data-ttu-id="c091a-130">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c091a-130">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c091a-131">**enableSkipIncompatibleRow**</span><span class="sxs-lookup"><span data-stu-id="c091a-131">**enableSkipIncompatibleRow**</span></span> | <span data-ttu-id="c091a-132">Atlanıyor uyumsuz satırları kopyalama sırasında veya etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c091a-132">Enable skipping incompatible rows during copy or not.</span></span> | <span data-ttu-id="c091a-133">True</span><span class="sxs-lookup"><span data-stu-id="c091a-133">True</span></span><br/><span data-ttu-id="c091a-134">False (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="c091a-134">False (default)</span></span> | <span data-ttu-id="c091a-135">Hayır</span><span class="sxs-lookup"><span data-stu-id="c091a-135">No</span></span> |
| <span data-ttu-id="c091a-136">**redirectIncompatibleRowSettings**</span><span class="sxs-lookup"><span data-stu-id="c091a-136">**redirectIncompatibleRowSettings**</span></span> | <span data-ttu-id="c091a-137">Zaman uyumsuz satırları günlüğe kaydetmek istediğiniz bir grup olabilir özellik belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="c091a-137">A group of properties that can be specified when you want to log the incompatible rows.</span></span> | &nbsp; | <span data-ttu-id="c091a-138">Hayır</span><span class="sxs-lookup"><span data-stu-id="c091a-138">No</span></span> |
| <span data-ttu-id="c091a-139">**linkedServiceName**</span><span class="sxs-lookup"><span data-stu-id="c091a-139">**linkedServiceName**</span></span> | <span data-ttu-id="c091a-140">Atlanan satırları içeren günlüğü depolamak için Azure Storage bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="c091a-140">The linked service of Azure Storage to store the log that contains the skipped rows.</span></span> | <span data-ttu-id="c091a-141">Adı bir [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) veya [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) bağlantılı günlük dosyasını depolamak için kullanmak istediğiniz depolama örneğine başvurur hizmeti.</span><span class="sxs-lookup"><span data-stu-id="c091a-141">The name of an [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) linked service, which refers to the storage instance that you want to use to store the log file.</span></span> | <span data-ttu-id="c091a-142">Hayır</span><span class="sxs-lookup"><span data-stu-id="c091a-142">No</span></span> |
| <span data-ttu-id="c091a-143">**yol**</span><span class="sxs-lookup"><span data-stu-id="c091a-143">**path**</span></span> | <span data-ttu-id="c091a-144">Atlanan satır içeren bir günlük dosyası yolu.</span><span class="sxs-lookup"><span data-stu-id="c091a-144">The path of the log file that contains the skipped rows.</span></span> | <span data-ttu-id="c091a-145">Uyumsuz verileri günlüğe kaydetmek için kullanmak istediğiniz Blob Depolama yolunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="c091a-145">Specify the Blob storage path that you want to use to log the incompatible data.</span></span> <span data-ttu-id="c091a-146">Bir yol belirtmezseniz, hizmet bir kapsayıcı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c091a-146">If you do not provide a path, the service creates a container for you.</span></span> | <span data-ttu-id="c091a-147">Hayır</span><span class="sxs-lookup"><span data-stu-id="c091a-147">No</span></span> |

## <a name="monitoring"></a><span data-ttu-id="c091a-148">İzleme</span><span class="sxs-lookup"><span data-stu-id="c091a-148">Monitoring</span></span>
<span data-ttu-id="c091a-149">Çalıştırma kopyalama etkinliği tamamlandıktan sonra izleme bölümünde Atlanan satır sayısını görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c091a-149">After the copy activity run completes, you can see the number of skipped rows in the monitoring section:</span></span>

![İzleyici uyumsuz satır atlandı](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

<span data-ttu-id="c091a-151">Uyumsuz satırları oturum yapılandırırsanız, günlük dosyası bu yolunda bulabilirsiniz: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` günlük dosyasında, atlanan satır ve uyumsuzluk kök nedenini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c091a-151">If you configure to log the incompatible rows, you can find the log file at this path: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In the log file, you can see the rows that were skipped and the root cause of the incompatibility.</span></span>

<span data-ttu-id="c091a-152">Özgün veriler ve karşılık gelen hata dosyasına kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="c091a-152">Both the original data and the corresponding error are logged in the file.</span></span> <span data-ttu-id="c091a-153">Günlük dosyası içeriğine bir örnek aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="c091a-153">An example of the log file content is as follows:</span></span>
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' to type 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. The duplicate key value is (data4).
```

## <a name="next-steps"></a><span data-ttu-id="c091a-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c091a-154">Next steps</span></span>
<span data-ttu-id="c091a-155">Azure Data Factory kopyalama etkinliği hakkında daha fazla bilgi için bkz: [Kopyala etkinliğini kullanarak veri taşıma](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c091a-155">To learn more about Azure Data Factory Copy Activity, see [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>