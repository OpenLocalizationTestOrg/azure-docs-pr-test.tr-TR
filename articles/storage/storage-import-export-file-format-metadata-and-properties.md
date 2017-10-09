---
title: "aaaAzure içeri/dışarı aktarma meta verileri ve özellikleri dosya biçimi | Microsoft Docs"
description: "Bilgi nasıl toospecify meta verileri ve bir veya daha fazla özellikleri BLOB, bir içeri aktarma parçası olan veya iş dışarı aktarma."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 840364c6-d9a8-4b43-a9f3-f7441c625069
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: bb13c1f1a27baea77298cb224970cd521d02d8c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a><span data-ttu-id="7d667-103">Azure içeri/dışarı aktarma hizmeti meta verileri ve özellikleri dosya biçimi</span><span class="sxs-lookup"><span data-stu-id="7d667-103">Azure Import/Export service metadata and properties file format</span></span>
<span data-ttu-id="7d667-104">Meta veri ve bir veya daha fazla BLOB özelliklerini alma işi veya bir dışarı aktarma işinin parçası olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d667-104">You can specify metadata and properties for one or more blobs as part of an import job or an export job.</span></span> <span data-ttu-id="7d667-105">tooset meta verileri veya bir alma işinin bir parçası olarak oluşturulan BLOB'lar için özellikleri, bir meta veri ya da özellikler dosyası içeri hello veri toobe içeren hello sabit sürücüsünde sağlayın.</span><span class="sxs-lookup"><span data-stu-id="7d667-105">tooset metadata or properties for blobs being created as part of an import job, you provide a metadata or properties file on hello hard drive containing hello data toobe imported.</span></span> <span data-ttu-id="7d667-106">Bir dışarı aktarma işi için meta verileri ve özellikler dahil tooa meta verileri veya özellikleri dosya tooyou döndürülen hello sabit sürücüde yazılır.</span><span class="sxs-lookup"><span data-stu-id="7d667-106">For an export job, metadata and properties are written tooa metadata or properties file that is included on hello hard drive returned tooyou.</span></span>  
  
## <a name="metadata-file-format"></a><span data-ttu-id="7d667-107">Meta veri dosyası biçimi</span><span class="sxs-lookup"><span data-stu-id="7d667-107">Metadata file format</span></span>  
<span data-ttu-id="7d667-108">meta veri dosyasının Hello biçimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="7d667-108">hello format of a metadata file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|<span data-ttu-id="7d667-109">XML öğesi</span><span class="sxs-lookup"><span data-stu-id="7d667-109">XML Element</span></span>|<span data-ttu-id="7d667-110">Tür</span><span class="sxs-lookup"><span data-stu-id="7d667-110">Type</span></span>|<span data-ttu-id="7d667-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d667-111">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Metadata`|<span data-ttu-id="7d667-112">Kök öğesi</span><span class="sxs-lookup"><span data-stu-id="7d667-112">Root element</span></span>|<span data-ttu-id="7d667-113">Merhaba meta veri dosyasının kök öğesinin Hello.</span><span class="sxs-lookup"><span data-stu-id="7d667-113">hello root element of hello metadata file.</span></span>|  
|`metadata-name`|<span data-ttu-id="7d667-114">Dize</span><span class="sxs-lookup"><span data-stu-id="7d667-114">String</span></span>|<span data-ttu-id="7d667-115">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="7d667-115">Optional.</span></span> <span data-ttu-id="7d667-116">Merhaba XML öğesi hello blob hello meta verilerin hello adını belirtir ve değerini hello hello meta verileri ayarın değerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="7d667-116">hello XML element specifies hello name of hello metadata for hello blob, and its value specifies hello value of hello metadata setting.</span></span>|  
  
## <a name="properties-file-format"></a><span data-ttu-id="7d667-117">Özellikler dosya biçimi</span><span class="sxs-lookup"><span data-stu-id="7d667-117">Properties file format</span></span>  
<span data-ttu-id="7d667-118">Özellikler dosyasının Hello biçimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="7d667-118">hello format of a properties file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
[<Last-Modified>date-time-value</Last-Modified>]  
[<Etag>etag</Etag>]  
[<Content-Length>size-in-bytes<Content-Length>]  
[<Content-Type>content-type</Content-Type>]  
[<Content-MD5>content-md5</Content-MD5>]  
[<Content-Encoding>content-encoding</Content-Encoding>]  
[<Content-Language>content-language</Content-Language>]  
[<Cache-Control>cache-control</Cache-Control>]  
</Properties>  
```
  
|<span data-ttu-id="7d667-119">XML öğesi</span><span class="sxs-lookup"><span data-stu-id="7d667-119">XML Element</span></span>|<span data-ttu-id="7d667-120">Tür</span><span class="sxs-lookup"><span data-stu-id="7d667-120">Type</span></span>|<span data-ttu-id="7d667-121">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d667-121">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Properties`|<span data-ttu-id="7d667-122">Kök öğesi</span><span class="sxs-lookup"><span data-stu-id="7d667-122">Root element</span></span>|<span data-ttu-id="7d667-123">Merhaba özellikleri dosyasının kök öğesinin Hello.</span><span class="sxs-lookup"><span data-stu-id="7d667-123">hello root element of hello properties file.</span></span>|  
|`Last-Modified`|<span data-ttu-id="7d667-124">Dize</span><span class="sxs-lookup"><span data-stu-id="7d667-124">String</span></span>|<span data-ttu-id="7d667-125">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="7d667-125">Optional.</span></span> <span data-ttu-id="7d667-126">Merhaba son değişiklik zamanı hello blob için.</span><span class="sxs-lookup"><span data-stu-id="7d667-126">hello last-modified time for hello blob.</span></span> <span data-ttu-id="7d667-127">Dışarı aktarma işleri yalnızca.</span><span class="sxs-lookup"><span data-stu-id="7d667-127">For export jobs only.</span></span>|  
|`Etag`|<span data-ttu-id="7d667-128">Dize</span><span class="sxs-lookup"><span data-stu-id="7d667-128">String</span></span>|<span data-ttu-id="7d667-129">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="7d667-129">Optional.</span></span> <span data-ttu-id="7d667-130">blob'un ETag değeri hello.</span><span class="sxs-lookup"><span data-stu-id="7d667-130">hello blob's ETag value.</span></span> <span data-ttu-id="7d667-131">Dışarı aktarma işleri yalnızca.</span><span class="sxs-lookup"><span data-stu-id="7d667-131">For export jobs only.</span></span>|  
|`Content-Length`|<span data-ttu-id="7d667-132">Dize</span><span class="sxs-lookup"><span data-stu-id="7d667-132">String</span></span>|<span data-ttu-id="7d667-133">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="7d667-133">Optional.</span></span> <span data-ttu-id="7d667-134">Merhaba blob bayt cinsinden boyutu Hello.</span><span class="sxs-lookup"><span data-stu-id="7d667-134">hello size of hello blob in bytes.</span></span> <span data-ttu-id="7d667-135">Dışarı aktarma işleri yalnızca.</span><span class="sxs-lookup"><span data-stu-id="7d667-135">For export jobs only.</span></span>|  
|`Content-Type`|<span data-ttu-id="7d667-136">Dize</span><span class="sxs-lookup"><span data-stu-id="7d667-136">String</span></span>|<span data-ttu-id="7d667-137">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="7d667-137">Optional.</span></span> <span data-ttu-id="7d667-138">Merhaba hello BLOB içerik türü.</span><span class="sxs-lookup"><span data-stu-id="7d667-138">hello content type of hello blob.</span></span>|  
|`Content-MD5`|<span data-ttu-id="7d667-139">Dize</span><span class="sxs-lookup"><span data-stu-id="7d667-139">String</span></span>|<span data-ttu-id="7d667-140">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="7d667-140">Optional.</span></span> <span data-ttu-id="7d667-141">Merhaba blob'un MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="7d667-141">hello blob's MD5 hash.</span></span>|  
|`Content-Encoding`|<span data-ttu-id="7d667-142">Dize</span><span class="sxs-lookup"><span data-stu-id="7d667-142">String</span></span>|<span data-ttu-id="7d667-143">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="7d667-143">Optional.</span></span> <span data-ttu-id="7d667-144">Merhaba blob'un içerik kodlaması.</span><span class="sxs-lookup"><span data-stu-id="7d667-144">hello blob's content encoding.</span></span>|  
|`Content-Language`|<span data-ttu-id="7d667-145">Dize</span><span class="sxs-lookup"><span data-stu-id="7d667-145">String</span></span>|<span data-ttu-id="7d667-146">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="7d667-146">Optional.</span></span> <span data-ttu-id="7d667-147">blob'un içerik dil hello.</span><span class="sxs-lookup"><span data-stu-id="7d667-147">hello blob's content language.</span></span>|  
|`Cache-Control`|<span data-ttu-id="7d667-148">Dize</span><span class="sxs-lookup"><span data-stu-id="7d667-148">String</span></span>|<span data-ttu-id="7d667-149">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="7d667-149">Optional.</span></span> <span data-ttu-id="7d667-150">Merhaba önbellek denetimi dizesi hello blob.</span><span class="sxs-lookup"><span data-stu-id="7d667-150">hello cache control string for hello blob.</span></span>|  

## <a name="next-steps"></a><span data-ttu-id="7d667-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7d667-151">Next steps</span></span>

<span data-ttu-id="7d667-152">Bkz: [blob özelliklerini ayarlama](/rest/api/storageservices/set-blob-properties), [Blob meta verileri ayarlama](/rest/api/storageservices/set-blob-metadata), ve [ayarı ve alınırken özelliklerini ve meta verileri için blob kaynakları](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) için blob meta verileri ve özellikleri ayarlama hakkında ayrıntılı kurallar.</span><span class="sxs-lookup"><span data-stu-id="7d667-152">See [Set blob properties](/rest/api/storageservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata), and [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) for detailed rules about setting blob metadata and properties.</span></span>
