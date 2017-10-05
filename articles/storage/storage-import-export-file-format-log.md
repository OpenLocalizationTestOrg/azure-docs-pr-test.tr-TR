---
title: "Azure içeri/dışarı aktarma günlük dosyası biçimi | Microsoft Docs"
description: "İçeri/dışarı aktarma hizmeti işi için adımları çalıştırıldığında oluşturulan günlük dosyalarını biçimi hakkında bilgi edinin."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 16234ccaf13ce1d85cfd207ed4734e683070faa6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-importexport-service-log-file-format"></a><span data-ttu-id="94c7e-103">Azure içeri/dışarı aktarma hizmeti günlük dosyası biçimi</span><span class="sxs-lookup"><span data-stu-id="94c7e-103">Azure Import/Export service log file format</span></span>
<span data-ttu-id="94c7e-104">Microsoft Azure içeri/dışarı aktarma hizmeti bir alma işi veya bir dışarı aktarma işinin parçası olarak bir sürücüde bir eylem gerçekleştirdiğinde, bu işle ilişkili depolama hesabındaki BLOB engellemek için günlüklerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="94c7e-104">When the Microsoft Azure Import/Export service performs an action on a drive as part of an import job or an export job, logs are written to block blobs in the storage account associated with that job.</span></span>  
  
<span data-ttu-id="94c7e-105">İçeri/dışarı aktarma hizmeti tarafından yazılan iki günlükleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="94c7e-105">There are two logs that may be written by the Import/Export service:</span></span>  
  
-   <span data-ttu-id="94c7e-106">Hata günlüğü her zaman bir hata durumunda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="94c7e-106">The error log is always generated in the event of an error.</span></span>  
  
-   <span data-ttu-id="94c7e-107">Ayrıntılı günlük varsayılan olarak etkin değildir, ancak ayarlayarak etkinleştirilebilir `EnableVerboseLog` özelliği bir [Put işlemini](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) veya [güncelleştirme işi özellikleri](/rest/api/storageimportexport/jobs#Jobs_Update) işlemi.</span><span class="sxs-lookup"><span data-stu-id="94c7e-107">The verbose log is not enabled by default, but may be enabled by setting the `EnableVerboseLog` property on a [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation.</span></span>  
  
## <a name="log-file-location"></a><span data-ttu-id="94c7e-108">Günlük dosyası konumu</span><span class="sxs-lookup"><span data-stu-id="94c7e-108">Log file location</span></span>  
<span data-ttu-id="94c7e-109">Günlükleri kapsayıcı veya sanal dizini tarafından belirtilen blok yazılan `ImportExportStatesPath` üzerinde ayarlayabilirsiniz ayarı bir `Put Job` işlemi.</span><span class="sxs-lookup"><span data-stu-id="94c7e-109">The logs are written to block blobs in the container or virtual directory specified by the `ImportExportStatesPath` setting, which you can set on a `Put Job` operation.</span></span> <span data-ttu-id="94c7e-110">Günlüklere yazılır konumu nasıl kimlik doğrulaması için belirtilen değer birlikte iş için belirtilen üzerinde bağlıdır `ImportExportStatesPath`.</span><span class="sxs-lookup"><span data-stu-id="94c7e-110">The location to which the logs are written depends on how authentication is specified for the job, together with the value specified for `ImportExportStatesPath`.</span></span> <span data-ttu-id="94c7e-111">Kimlik doğrulama iş için bir depolama hesabı anahtarı ya da bir kapsayıcı SAS (paylaşılan erişim imzası) belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="94c7e-111">Authentication for the job may be specified via a storage account key, or a container SAS (shared access signature).</span></span>  
  
<span data-ttu-id="94c7e-112">Kapsayıcı veya sanal dizin adını ya da varsayılan adı olabilir. `waimportexport`, veya başka bir kapsayıcı veya sanal dizin adı.</span><span class="sxs-lookup"><span data-stu-id="94c7e-112">The name of the container or virtual directory may either be the default name of `waimportexport`, or another container or virtual directory name that you specify.</span></span>  
  
<span data-ttu-id="94c7e-113">Aşağıdaki tabloda olası seçenekleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="94c7e-113">The table below shows the possible options:</span></span>  
  
|<span data-ttu-id="94c7e-114">Kimlik Doğrulama Yöntemi</span><span class="sxs-lookup"><span data-stu-id="94c7e-114">Authentication Method</span></span>|<span data-ttu-id="94c7e-115">Değeri `ImportExportStatesPath`öğesi</span><span class="sxs-lookup"><span data-stu-id="94c7e-115">Value of `ImportExportStatesPath`Element</span></span>|<span data-ttu-id="94c7e-116">Günlük BLOB'lar konumu</span><span class="sxs-lookup"><span data-stu-id="94c7e-116">Location of Log Blobs</span></span>|  
|---------------------------|----------------------------------------------|---------------------------|  
|<span data-ttu-id="94c7e-117">Depolama hesabı anahtarı</span><span class="sxs-lookup"><span data-stu-id="94c7e-117">Storage account key</span></span>|<span data-ttu-id="94c7e-118">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="94c7e-118">Default value</span></span>|<span data-ttu-id="94c7e-119">Adlı bir kapsayıcı `waimportexport`, varsayılan kapsayıcı olduğu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-119">A container named `waimportexport`, which is the default container.</span></span> <span data-ttu-id="94c7e-120">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="94c7e-120">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|<span data-ttu-id="94c7e-121">Depolama hesabı anahtarı</span><span class="sxs-lookup"><span data-stu-id="94c7e-121">Storage account key</span></span>|<span data-ttu-id="94c7e-122">Kullanıcı tarafından belirtilen değeri</span><span class="sxs-lookup"><span data-stu-id="94c7e-122">User-specified value</span></span>|<span data-ttu-id="94c7e-123">Kullanıcı tarafından adlı bir kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="94c7e-123">A container named by the user.</span></span> <span data-ttu-id="94c7e-124">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="94c7e-124">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|<span data-ttu-id="94c7e-125">Kapsayıcı SAS</span><span class="sxs-lookup"><span data-stu-id="94c7e-125">Container SAS</span></span>|<span data-ttu-id="94c7e-126">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="94c7e-126">Default value</span></span>|<span data-ttu-id="94c7e-127">Adlı bir sanal dizini `waimportexport`, SAS belirtilen kapsayıcısı altında varsayılan adı.</span><span class="sxs-lookup"><span data-stu-id="94c7e-127">A virtual directory named `waimportexport`, which is the default name, beneath the container specified in the SAS.</span></span><br /><br /> <span data-ttu-id="94c7e-128">Örneğin, SAS belirtilen iş ise `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, sonra da günlük konumunu olacaktır`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span><span class="sxs-lookup"><span data-stu-id="94c7e-128">For example, if the SAS specified for the job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, then the log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span></span>|  
|<span data-ttu-id="94c7e-129">Kapsayıcı SAS</span><span class="sxs-lookup"><span data-stu-id="94c7e-129">Container SAS</span></span>|<span data-ttu-id="94c7e-130">Kullanıcı tarafından belirtilen değeri</span><span class="sxs-lookup"><span data-stu-id="94c7e-130">User-specified value</span></span>|<span data-ttu-id="94c7e-131">SAS belirtilen kapsayıcısı altında kullanıcı tarafından adlı bir sanal dizini.</span><span class="sxs-lookup"><span data-stu-id="94c7e-131">A virtual directory named by the user, beneath the container specified in the SAS.</span></span><br /><br /> <span data-ttu-id="94c7e-132">Örneğin, SAS belirtilen iş ise `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, ve belirtilen sanal dizin adlı `mylogblobs`, sonra da günlük konumunu olacaktır `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span><span class="sxs-lookup"><span data-stu-id="94c7e-132">For example, if the SAS specified for the job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, and the specified virtual directory is named `mylogblobs`, then the log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span></span>|  
  
<span data-ttu-id="94c7e-133">Çağırarak URL'sini hata ve ayrıntılı günlükleri alabilirsiniz [alma işi](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) işlemi.</span><span class="sxs-lookup"><span data-stu-id="94c7e-133">You can retrieve the URL for the error and verbose logs by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="94c7e-134">Günlükleri, sürücünün işlem tamamlandıktan sonra kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="94c7e-134">The logs are available after processing of the drive is complete.</span></span>  
  
## <a name="log-file-format"></a><span data-ttu-id="94c7e-135">Günlük dosyası biçimi</span><span class="sxs-lookup"><span data-stu-id="94c7e-135">Log file format</span></span>  
<span data-ttu-id="94c7e-136">Her iki günlük için biçim aynıdır: sabit sürücü ve müşterinin hesabına arasında BLOB'ları kopyalanırken oluşan olaylarla XML açıklamaları içeren blob.</span><span class="sxs-lookup"><span data-stu-id="94c7e-136">The format for both logs is the same: a blob containing XML descriptions of the events that occurred while copying blobs between the hard drive and the customer's account.</span></span>  
  
<span data-ttu-id="94c7e-137">Hata günlüğü yalnızca BLOB veya içe veya dışa aktarma işi sırasında hatalarla karşılaştı dosyaları bilgileri içerirken ayrıntılı günlüğü her blob (için içeri aktarma işi için) veya (bir dışa aktarma işi için), dosya kopyalama işlemi durumu hakkında tam bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="94c7e-137">The verbose log contains complete information about the status of the copy operation for every blob (for an import job) or file (for an export job), whereas the error log contains only the information for blobs or files that encountered errors during the import or export job.</span></span>  
  
<span data-ttu-id="94c7e-138">Ayrıntılı günlük biçimi aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="94c7e-138">The verbose log format is shown below.</span></span> <span data-ttu-id="94c7e-139">Hata günlüğü aynı yapıya sahip, ancak başarılı işlemleri filtreler.</span><span class="sxs-lookup"><span data-stu-id="94c7e-139">The error log has the same structure, but filters out successful operations.</span></span>  

```xml
<DriveLog Version="2014-11-01">  
  <DriveId>drive-id</DriveId>  
  [<Blob Status="blob-status">  
   <BlobPath>blob-path</BlobPath>  
   <FilePath>file-path</FilePath>  
   [<Snapshot>snapshot</Snapshot>]  
   <Length>length</Length>  
   [<LastModified>last-modified</LastModified>]  
   [<ImportDisposition Status="import-disposition-status">import-disposition</ImportDisposition>]  
   [page-range-list-or-block-list]  
   [metadata-status]  
   [properties-status]  
  </Blob>]  
  [<Blob>  
    . . .  
  </Blob>]  
  <Status>drive-status</Status>  
</DriveLog>  
  
page-range-list-or-block-list ::= 
  page-range-list | block-list  
  
page-range-list ::=   
<PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
</PageRangeList>  
  
block-list ::=  
<BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       [Hash="md5-hash"] Status="block-status"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       [Hash="md5-hash"] Status="block-status"/>]  
</BlockList>  
  
metadata-status ::=  
<Metadata Status="metadata-status">  
   [<GlobalPath Hash="md5-hash">global-metadata-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">metadata-file-path</Path>]  
</Metadata>  
  
properties-status ::=  
<Properties Status="properties-status">  
   [<GlobalPath Hash="md5-hash">global-properties-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">properties-file-path</Path>]  
</Properties>  
```

<span data-ttu-id="94c7e-140">Aşağıdaki tabloda günlük dosyasının öğelerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="94c7e-140">The following table describes the elements of the log file.</span></span>  
  
|<span data-ttu-id="94c7e-141">XML öğesi</span><span class="sxs-lookup"><span data-stu-id="94c7e-141">XML Element</span></span>|<span data-ttu-id="94c7e-142">Tür</span><span class="sxs-lookup"><span data-stu-id="94c7e-142">Type</span></span>|<span data-ttu-id="94c7e-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="94c7e-143">Description</span></span>|  
|-----------------|----------|-----------------|  
|`DriveLog`|<span data-ttu-id="94c7e-144">XML öğesi</span><span class="sxs-lookup"><span data-stu-id="94c7e-144">XML Element</span></span>|<span data-ttu-id="94c7e-145">Bir sürücü günlük temsil eder.</span><span class="sxs-lookup"><span data-stu-id="94c7e-145">Represents a drive log.</span></span>|  
|`Version`|<span data-ttu-id="94c7e-146">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="94c7e-146">Attribute, String</span></span>|<span data-ttu-id="94c7e-147">Günlük biçimi sürümü.</span><span class="sxs-lookup"><span data-stu-id="94c7e-147">The version of the log format.</span></span>|  
|`DriveId`|<span data-ttu-id="94c7e-148">Dize</span><span class="sxs-lookup"><span data-stu-id="94c7e-148">String</span></span>|<span data-ttu-id="94c7e-149">Sürücünün donanım seri numarası.</span><span class="sxs-lookup"><span data-stu-id="94c7e-149">The drive's hardware serial number.</span></span>|  
|`Status`|<span data-ttu-id="94c7e-150">Dize</span><span class="sxs-lookup"><span data-stu-id="94c7e-150">String</span></span>|<span data-ttu-id="94c7e-151">Sürücü işlem durumu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-151">Status of the drive processing.</span></span> <span data-ttu-id="94c7e-152">Bkz: `Drive Status Codes` daha fazla bilgi için tablo aşağıda.</span><span class="sxs-lookup"><span data-stu-id="94c7e-152">See the `Drive Status Codes` table below for more information.</span></span>|  
|`Blob`|<span data-ttu-id="94c7e-153">İç içe geçmiş XML öğesi</span><span class="sxs-lookup"><span data-stu-id="94c7e-153">Nested XML element</span></span>|<span data-ttu-id="94c7e-154">Bir blob temsil eder.</span><span class="sxs-lookup"><span data-stu-id="94c7e-154">Represents a blob.</span></span>|  
|`Blob/BlobPath`|<span data-ttu-id="94c7e-155">Dize</span><span class="sxs-lookup"><span data-stu-id="94c7e-155">String</span></span>|<span data-ttu-id="94c7e-156">Blob URI'si.</span><span class="sxs-lookup"><span data-stu-id="94c7e-156">The URI of the blob.</span></span>|  
|`Blob/FilePath`|<span data-ttu-id="94c7e-157">Dize</span><span class="sxs-lookup"><span data-stu-id="94c7e-157">String</span></span>|<span data-ttu-id="94c7e-158">Sürücüsündeki dosyanın göreli yolu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-158">The relative path to the file on the drive.</span></span>|  
|`Blob/Snapshot`|<span data-ttu-id="94c7e-159">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="94c7e-159">DateTime</span></span>|<span data-ttu-id="94c7e-160">Yalnızca bir dışa aktarma işi için blob anlık görüntü sürümü.</span><span class="sxs-lookup"><span data-stu-id="94c7e-160">The snapshot version of the blob, for an export job only.</span></span>|  
|`Blob/Length`|<span data-ttu-id="94c7e-161">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="94c7e-161">Integer</span></span>|<span data-ttu-id="94c7e-162">Blob bayt cinsinden uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-162">The total length of the blob in bytes.</span></span>|  
|`Blob/LastModified`|<span data-ttu-id="94c7e-163">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="94c7e-163">DateTime</span></span>|<span data-ttu-id="94c7e-164">Blob son değiştirildiği, tarih yalnızca bir dışa aktarma işi için.</span><span class="sxs-lookup"><span data-stu-id="94c7e-164">The date/time that the blob was last modified, for an export job only.</span></span>|  
|`Blob/ImportDisposition`|<span data-ttu-id="94c7e-165">Dize</span><span class="sxs-lookup"><span data-stu-id="94c7e-165">String</span></span>|<span data-ttu-id="94c7e-166">Yalnızca bir içeri aktarma işi için blob alma değerlendirme.</span><span class="sxs-lookup"><span data-stu-id="94c7e-166">The import disposition of the blob, for an import job only.</span></span>|  
|`Blob/ImportDisposition/@Status`|<span data-ttu-id="94c7e-167">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="94c7e-167">Attribute, String</span></span>|<span data-ttu-id="94c7e-168">İçeri aktarma değerlendirme durumu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-168">The status of the import disposition.</span></span>|  
|`PageRangeList`|<span data-ttu-id="94c7e-169">İç içe geçmiş XML öğesi</span><span class="sxs-lookup"><span data-stu-id="94c7e-169">Nested XML element</span></span>|<span data-ttu-id="94c7e-170">Bir sayfa blob'u için sayfa aralıklarını listesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="94c7e-170">Represents a list of page ranges for a page blob.</span></span>|  
|`PageRange`|<span data-ttu-id="94c7e-171">XML öğesi</span><span class="sxs-lookup"><span data-stu-id="94c7e-171">XML element</span></span>|<span data-ttu-id="94c7e-172">Sayfa aralığını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="94c7e-172">Represents a page range.</span></span>|  
|`PageRange/@Offset`|<span data-ttu-id="94c7e-173">Öznitelik, tamsayı</span><span class="sxs-lookup"><span data-stu-id="94c7e-173">Attribute, Integer</span></span>|<span data-ttu-id="94c7e-174">Blob sayfa aralığında başlangıç uzaklığı.</span><span class="sxs-lookup"><span data-stu-id="94c7e-174">Starting offset of the page range in the blob.</span></span>|  
|`PageRange/@Length`|<span data-ttu-id="94c7e-175">Öznitelik, tamsayı</span><span class="sxs-lookup"><span data-stu-id="94c7e-175">Attribute, Integer</span></span>|<span data-ttu-id="94c7e-176">Sayfa aralığının bayt cinsinden uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-176">Length in bytes of the page range.</span></span>|  
|`PageRange/@Hash`|<span data-ttu-id="94c7e-177">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="94c7e-177">Attribute, String</span></span>|<span data-ttu-id="94c7e-178">Base16 kodlu MD5 karması sayfa aralığı.</span><span class="sxs-lookup"><span data-stu-id="94c7e-178">Base16-encoded MD5 hash of the page range.</span></span>|  
|`PageRange/@Status`|<span data-ttu-id="94c7e-179">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="94c7e-179">Attribute, String</span></span>|<span data-ttu-id="94c7e-180">Sayfa aralığı işlem durumu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-180">Status of processing the page range.</span></span>|  
|`BlockList`|<span data-ttu-id="94c7e-181">İç içe geçmiş XML öğesi</span><span class="sxs-lookup"><span data-stu-id="94c7e-181">Nested XML element</span></span>|<span data-ttu-id="94c7e-182">Bir blok blobu için blok listesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="94c7e-182">Represents a list of blocks for a block blob.</span></span>|  
|`Block`|<span data-ttu-id="94c7e-183">XML öğesi</span><span class="sxs-lookup"><span data-stu-id="94c7e-183">XML element</span></span>|<span data-ttu-id="94c7e-184">Bloğunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="94c7e-184">Represents a block.</span></span>|  
|`Block/@Offset`|<span data-ttu-id="94c7e-185">Öznitelik, tamsayı</span><span class="sxs-lookup"><span data-stu-id="94c7e-185">Attribute, Integer</span></span>|<span data-ttu-id="94c7e-186">Blob bloğunda başlangıç uzaklığı.</span><span class="sxs-lookup"><span data-stu-id="94c7e-186">Starting offset of the block in the blob.</span></span>|  
|`Block/@Length`|<span data-ttu-id="94c7e-187">Öznitelik, tamsayı</span><span class="sxs-lookup"><span data-stu-id="94c7e-187">Attribute, Integer</span></span>|<span data-ttu-id="94c7e-188">Bloğun bayt cinsinden uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-188">Length in bytes of the block.</span></span>|  
|`Block/@Id`|<span data-ttu-id="94c7e-189">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="94c7e-189">Attribute, String</span></span>|<span data-ttu-id="94c7e-190">Blok kimliği.</span><span class="sxs-lookup"><span data-stu-id="94c7e-190">The block ID.</span></span>|  
|`Block/@Hash`|<span data-ttu-id="94c7e-191">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="94c7e-191">Attribute, String</span></span>|<span data-ttu-id="94c7e-192">Base16 kodlu MD5 karma değeri bloğunun.</span><span class="sxs-lookup"><span data-stu-id="94c7e-192">Base16-encoded MD5 hash of the block.</span></span>|  
|`Block/@Status`|<span data-ttu-id="94c7e-193">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="94c7e-193">Attribute, String</span></span>|<span data-ttu-id="94c7e-194">Blok işlem durumu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-194">Status of processing the block.</span></span>|  
|`Metadata`|<span data-ttu-id="94c7e-195">İç içe geçmiş XML öğesi</span><span class="sxs-lookup"><span data-stu-id="94c7e-195">Nested XML element</span></span>|<span data-ttu-id="94c7e-196">Blob'un meta verileri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="94c7e-196">Represents the blob's metadata.</span></span>|  
|`Metadata/@Status`|<span data-ttu-id="94c7e-197">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="94c7e-197">Attribute, String</span></span>|<span data-ttu-id="94c7e-198">Blob verilerinin işlenmesini durumu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-198">Status of processing of the blob metadata.</span></span>|  
|`Metadata/GlobalPath`|<span data-ttu-id="94c7e-199">Dize</span><span class="sxs-lookup"><span data-stu-id="94c7e-199">String</span></span>|<span data-ttu-id="94c7e-200">Genel meta veri dosyası göreli yolu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-200">Relative path to the global metadata file.</span></span>|  
|`Metadata/GlobalPath/@Hash`|<span data-ttu-id="94c7e-201">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="94c7e-201">Attribute, String</span></span>|<span data-ttu-id="94c7e-202">Base16 kodlu MD5 karma değeri genel meta veri dosyasının.</span><span class="sxs-lookup"><span data-stu-id="94c7e-202">Base16-encoded MD5 hash of the global metadata file.</span></span>|  
|`Metadata/Path`|<span data-ttu-id="94c7e-203">Dize</span><span class="sxs-lookup"><span data-stu-id="94c7e-203">String</span></span>|<span data-ttu-id="94c7e-204">Meta veri dosyası göreli yolu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-204">Relative path to the metadata file.</span></span>|  
|`Metadata/Path/@Hash`|<span data-ttu-id="94c7e-205">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="94c7e-205">Attribute, String</span></span>|<span data-ttu-id="94c7e-206">Base16 kodlu MD5 karması meta veri dosyası.</span><span class="sxs-lookup"><span data-stu-id="94c7e-206">Base16-encoded MD5 hash of the metadata file.</span></span>|  
|`Properties`|<span data-ttu-id="94c7e-207">İç içe geçmiş XML öğesi</span><span class="sxs-lookup"><span data-stu-id="94c7e-207">Nested XML element</span></span>|<span data-ttu-id="94c7e-208">Blob özellikleri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="94c7e-208">Represents the blob properties.</span></span>|  
|`Properties/@Status`|<span data-ttu-id="94c7e-209">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="94c7e-209">Attribute, String</span></span>|<span data-ttu-id="94c7e-210">Blob özellikleri, örneğin dosya bulunamadı, işleme durumunu tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="94c7e-210">Status of processing the blob properties, e.g. file not found, completed.</span></span>|  
|`Properties/GlobalPath`|<span data-ttu-id="94c7e-211">Dize</span><span class="sxs-lookup"><span data-stu-id="94c7e-211">String</span></span>|<span data-ttu-id="94c7e-212">Genel Özellikler dosyanın göreli yolu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-212">Relative path to the global properties file.</span></span>|  
|`Properties/GlobalPath/@Hash`|<span data-ttu-id="94c7e-213">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="94c7e-213">Attribute, String</span></span>|<span data-ttu-id="94c7e-214">Base16 kodlu MD5 karma değeri genel özellikleri dosyasının.</span><span class="sxs-lookup"><span data-stu-id="94c7e-214">Base16-encoded MD5 hash of the global properties file.</span></span>|  
|`Properties/Path`|<span data-ttu-id="94c7e-215">Dize</span><span class="sxs-lookup"><span data-stu-id="94c7e-215">String</span></span>|<span data-ttu-id="94c7e-216">Özellikler dosyanın göreli yolu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-216">Relative path to the properties file.</span></span>|  
|`Properties/Path/@Hash`|<span data-ttu-id="94c7e-217">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="94c7e-217">Attribute, String</span></span>|<span data-ttu-id="94c7e-218">Base16 kodlu MD5 karma özellikleri dosyasının.</span><span class="sxs-lookup"><span data-stu-id="94c7e-218">Base16-encoded MD5 hash of the properties file.</span></span>|  
|`Blob/Status`|<span data-ttu-id="94c7e-219">Dize</span><span class="sxs-lookup"><span data-stu-id="94c7e-219">String</span></span>|<span data-ttu-id="94c7e-220">Blob işlem durumu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-220">Status of processing the blob.</span></span>|  
  
# <a name="drive-status-codes"></a><span data-ttu-id="94c7e-221">Sürücü durum kodları</span><span class="sxs-lookup"><span data-stu-id="94c7e-221">Drive status codes</span></span>  
<span data-ttu-id="94c7e-222">Aşağıdaki tabloda bir sürücü işlemek için durum kodları listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="94c7e-222">The following table lists the status codes for processing a drive.</span></span>  
  
|<span data-ttu-id="94c7e-223">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="94c7e-223">Status code</span></span>|<span data-ttu-id="94c7e-224">Açıklama</span><span class="sxs-lookup"><span data-stu-id="94c7e-224">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="94c7e-225">Sürücü hatasız işleme tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="94c7e-225">The drive has finished processing without any errors.</span></span>|  
|`CompletedWithWarnings`|<span data-ttu-id="94c7e-226">Sürücü işleme BLOB'lar için belirtilen içeri aktarma değerlendirmeleri başına bir veya daha fazla BLOB uyarılarla tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="94c7e-226">The drive has finished processing with warnings in one or more blobs per the import dispositions specified for the blobs.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="94c7e-227">Sürücü, bir veya daha fazla BLOB veya öbekleri hatalarla tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="94c7e-227">The drive has finished with errors in one or more blobs or chunks.</span></span>|  
|`DiskNotFound`|<span data-ttu-id="94c7e-228">Disk sürücüsünde bulunur.</span><span class="sxs-lookup"><span data-stu-id="94c7e-228">No disk is found on the drive.</span></span>|  
|`VolumeNotNtfs`|<span data-ttu-id="94c7e-229">Disk üzerindeki ilk veri birimi NTFS biçiminde değil.</span><span class="sxs-lookup"><span data-stu-id="94c7e-229">The first data volume on the disk is not in NTFS format.</span></span>|  
|`DiskOperationFailed`|<span data-ttu-id="94c7e-230">Sürücü üzerindeki işlemleri gerçekleştirirken bilinmeyen bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-230">An unknown failure occurred when performing operations on the drive.</span></span>|  
|`BitLockerVolumeNotFound`|<span data-ttu-id="94c7e-231">BitLocker encryptable birim bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="94c7e-231">No BitLocker encryptable volume is found.</span></span>|  
|`BitLockerNotActivated`|<span data-ttu-id="94c7e-232">Birimde BitLocker etkin değil.</span><span class="sxs-lookup"><span data-stu-id="94c7e-232">BitLocker is not enabled on the volume.</span></span>|  
|`BitLockerProtectorNotFound`|<span data-ttu-id="94c7e-233">Sayısal parola anahtar koruyucusu birim üzerinde yok.</span><span class="sxs-lookup"><span data-stu-id="94c7e-233">The numerical password key protector does not exist on the volume.</span></span>|  
|`BitLockerKeyInvalid`|<span data-ttu-id="94c7e-234">Sağlanan sayısal parola, birimin kilidi açılamıyor.</span><span class="sxs-lookup"><span data-stu-id="94c7e-234">The numerical password provided cannot unlock the volume.</span></span>|  
|`BitLockerUnlockVolumeFailed`|<span data-ttu-id="94c7e-235">Birimin kilidini açmak çalışılırken bilinmeyen bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-235">Unknown failure has happened when trying to unlock the volume.</span></span>|  
|`BitLockerFailed`|<span data-ttu-id="94c7e-236">BitLocker işlem gerçekleştirilirken bilinmeyen bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-236">An unknown failure occurred while performing BitLocker operations.</span></span>|  
|`ManifestNameInvalid`|<span data-ttu-id="94c7e-237">Yayılma dosyası adı geçersiz.</span><span class="sxs-lookup"><span data-stu-id="94c7e-237">The manifest file name is invalid.</span></span>|  
|`ManifestNameTooLong`|<span data-ttu-id="94c7e-238">Yayılma dosyası adı çok uzun.</span><span class="sxs-lookup"><span data-stu-id="94c7e-238">The manifest file name is too long.</span></span>|  
|`ManifestNotFound`|<span data-ttu-id="94c7e-239">Bildirim dosyası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="94c7e-239">The manifest file is not found.</span></span>|  
|`ManifestAccessDenied`|<span data-ttu-id="94c7e-240">Bildirim dosyası için erişim reddedildi.</span><span class="sxs-lookup"><span data-stu-id="94c7e-240">Access to the manifest file is denied.</span></span>|  
|`ManifestCorrupted`|<span data-ttu-id="94c7e-241">Bildirim dosyası bozuk (içerik karması eşleşmiyor).</span><span class="sxs-lookup"><span data-stu-id="94c7e-241">The manifest file is corrupted (the content does not match its hash).</span></span>|  
|`ManifestFormatInvalid`|<span data-ttu-id="94c7e-242">Bildirim içerik gerekli biçime uymuyor.</span><span class="sxs-lookup"><span data-stu-id="94c7e-242">The manifest content does not conform to the required format.</span></span>|  
|`ManifestDriveIdMismatch`|<span data-ttu-id="94c7e-243">Sürücü Kimliği bildirim dosyasındaki sürücüden bir okuma eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="94c7e-243">The drive ID in the manifest file does not match the one read from the drive.</span></span>|  
|`ReadManifestFailed`|<span data-ttu-id="94c7e-244">Bildirimden okunurken bir disk g/ç hatası oluştu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-244">A disk I/O failure occurred while reading from the manifest.</span></span>|  
|`BlobListFormatInvalid`|<span data-ttu-id="94c7e-245">Dışarı aktarma blob listesi blob gerekli biçime uymuyor.</span><span class="sxs-lookup"><span data-stu-id="94c7e-245">The export blob list blob does not conform to the required format.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="94c7e-246">Depolama hesabındaki BLOB'ları erişmesine izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="94c7e-246">Access to the blobs in the storage account is forbidden.</span></span> <span data-ttu-id="94c7e-247">Bu geçersiz depolama hesabı anahtarı veya kapsayıcı SAS nedeniyle olabilir.</span><span class="sxs-lookup"><span data-stu-id="94c7e-247">This might be due to invalid storage account key or container SAS.</span></span>|  
|`InternalError`|<span data-ttu-id="94c7e-248">Ve sürücü işlenirken iç hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-248">And internal error occurred while processing the drive.</span></span>|  
  
## <a name="blob-status-codes"></a><span data-ttu-id="94c7e-249">BLOB durum kodları</span><span class="sxs-lookup"><span data-stu-id="94c7e-249">Blob status codes</span></span>  
<span data-ttu-id="94c7e-250">Aşağıdaki tabloda bir blob işlemek için durum kodları listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="94c7e-250">The following table lists the status codes for processing a blob.</span></span>  
  
|<span data-ttu-id="94c7e-251">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="94c7e-251">Status code</span></span>|<span data-ttu-id="94c7e-252">Açıklama</span><span class="sxs-lookup"><span data-stu-id="94c7e-252">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="94c7e-253">Blob hatasız işleme tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="94c7e-253">The blob has finished processing without errors.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="94c7e-254">Blob işleme bir veya daha fazla sayfa aralıklarını veya blokları, meta verileri veya özellikler hatalarla tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="94c7e-254">The blob has finished processing with errors in one or more page ranges or blocks, metadata, or properties.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="94c7e-255">Dosya adı geçersiz.</span><span class="sxs-lookup"><span data-stu-id="94c7e-255">The file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="94c7e-256">Dosya adı çok uzun.</span><span class="sxs-lookup"><span data-stu-id="94c7e-256">The file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="94c7e-257">Dosyası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="94c7e-257">The file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="94c7e-258">Dosyaya erişim reddedildi.</span><span class="sxs-lookup"><span data-stu-id="94c7e-258">Access to the file is denied.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="94c7e-259">Blob erişmek için Blob hizmeti isteği başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-259">The Blob service request to access the blob has failed.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="94c7e-260">Blob erişmek için Blob hizmeti isteği izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="94c7e-260">The Blob service request to access the blob is forbidden.</span></span> <span data-ttu-id="94c7e-261">Bu geçersiz depolama hesabı anahtarı veya kapsayıcı SAS nedeniyle olabilir.</span><span class="sxs-lookup"><span data-stu-id="94c7e-261">This might be due to invalid storage account key or container SAS.</span></span>|  
|`RenameFailed`|<span data-ttu-id="94c7e-262">Blob (için içeri aktarma işi için) veya dosyası (bir dışarı aktarma işinin) yeniden adlandırmak başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-262">Failed to rename the blob (for an import job) or the file (for an export job).</span></span>|  
|`BlobUnexpectedChange`|<span data-ttu-id="94c7e-263">Beklenmedik bir değişikliği (için bir dışarı aktarma işinin) blob ile oluştu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-263">An unexpected change has occurred with the blob (for an export job).</span></span>|  
|`LeasePresent`|<span data-ttu-id="94c7e-264">Blob üzerindeki mevcut bir kira var.</span><span class="sxs-lookup"><span data-stu-id="94c7e-264">There is a lease present on the blob.</span></span>|  
|`IOFailed`|<span data-ttu-id="94c7e-265">Blob işlenirken bir disk veya ağ g/ç hatası oluştu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-265">A disk or network I/O failure occurred while processing the blob.</span></span>|  
|`Failed`|<span data-ttu-id="94c7e-266">Blob işlenirken bilinmeyen bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-266">An unknown failure occurred while processing the blob.</span></span>|  
  
## <a name="import-disposition-status-codes"></a><span data-ttu-id="94c7e-267">İçeri aktarma değerlendirme durum kodları</span><span class="sxs-lookup"><span data-stu-id="94c7e-267">Import disposition status codes</span></span>  
<span data-ttu-id="94c7e-268">Aşağıdaki tabloda bir alma değerlendirme çözmek için durum kodları listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="94c7e-268">The following table lists the status codes for resolving an import disposition.</span></span>  
  
|<span data-ttu-id="94c7e-269">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="94c7e-269">Status code</span></span>|<span data-ttu-id="94c7e-270">Açıklama</span><span class="sxs-lookup"><span data-stu-id="94c7e-270">Description</span></span>|  
|-----------------|-----------------|  
|`Created`|<span data-ttu-id="94c7e-271">Blob oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-271">The blob has been created.</span></span>|  
|`Renamed`|<span data-ttu-id="94c7e-272">Blob adlandırma alma değerlendirme adlandırıldı.</span><span class="sxs-lookup"><span data-stu-id="94c7e-272">The blob has been renamed per rename import disposition.</span></span> <span data-ttu-id="94c7e-273">`Blob/BlobPath` Öğe yeniden adlandırılmış blob URI'sini içeriyor.</span><span class="sxs-lookup"><span data-stu-id="94c7e-273">The `Blob/BlobPath` element contains the URI for the renamed blob.</span></span>|  
|`Skipped`|<span data-ttu-id="94c7e-274">Blob başına atlandı `no-overwrite` değerlendirme içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="94c7e-274">The blob has been skipped per `no-overwrite` import disposition.</span></span>|  
|`Overwritten`|<span data-ttu-id="94c7e-275">Blob başına bir blob geçersiz kıldı `overwrite` değerlendirme içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="94c7e-275">The blob has overwritten an existing blob per `overwrite` import disposition.</span></span>|  
|`Cancelled`|<span data-ttu-id="94c7e-276">Önceki bir hata alma eğilimini işlenmesi durduruldu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-276">A prior failure has stopped further processing of the import disposition.</span></span>|  
  
## <a name="page-rangeblock-status-codes"></a><span data-ttu-id="94c7e-277">Sayfa aralık/blok durum kodları</span><span class="sxs-lookup"><span data-stu-id="94c7e-277">Page range/block status codes</span></span>  
<span data-ttu-id="94c7e-278">Aşağıdaki tabloda bir sayfa aralığı veya bir blok işlemek için durum kodları listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="94c7e-278">The following table lists the status codes for processing a page range or a block.</span></span>  
  
|<span data-ttu-id="94c7e-279">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="94c7e-279">Status code</span></span>|<span data-ttu-id="94c7e-280">Açıklama</span><span class="sxs-lookup"><span data-stu-id="94c7e-280">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="94c7e-281">Sayfa aralık veya blok hatasız işleme tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="94c7e-281">The page range or block has finished processing without any errors.</span></span>|  
|`Committed`|<span data-ttu-id="94c7e-282">Blok kaydedildi, ancak değil tam bloğunda listesi diğer blokları başarısız oldu veya tam engelleme listesi kendisini put başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-282">The block has been committed,  but not in the full block list because other blocks have failed, or put full block list itself has failed.</span></span>|  
|`Uncommitted`|<span data-ttu-id="94c7e-283">Blok karşıya ancak edilmemiş.</span><span class="sxs-lookup"><span data-stu-id="94c7e-283">The block is uploaded but not committed.</span></span>|  
|`Corrupted`|<span data-ttu-id="94c7e-284">Sayfa aralık veya blok bozuk (içerik karması eşleşmiyor).</span><span class="sxs-lookup"><span data-stu-id="94c7e-284">The page range or block is corrupted (the content does not match its hash).</span></span>|  
|`FileUnexpectedEnd`|<span data-ttu-id="94c7e-285">Bir beklenmeyen dosya sonu karşılaşıldı.</span><span class="sxs-lookup"><span data-stu-id="94c7e-285">An unexpected end of file has been encountered.</span></span>|  
|`BlobUnexpectedEnd`|<span data-ttu-id="94c7e-286">Blob beklenmeyen dosya sonuyla karşılaşıldı.</span><span class="sxs-lookup"><span data-stu-id="94c7e-286">An unexpected end of blob has been encountered.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="94c7e-287">Sayfa aralık veya blok erişmek için Blob hizmeti isteği başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-287">The Blob service request to access the page range or block has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="94c7e-288">Bir disk veya ağ g/ç hatası sayfası aralık veya blok işlenirken hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-288">A disk or network I/O failure occurred while processing the page range or block.</span></span>|  
|`Failed`|<span data-ttu-id="94c7e-289">Sayfa aralık veya blok işlenirken bilinmeyen bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-289">An unknown failure occurred while processing the page range or block.</span></span>|  
|`Cancelled`|<span data-ttu-id="94c7e-290">Önceki bir hata sayfası aralık veya blok işlenmesi durduruldu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-290">A prior failure has stopped further processing of the page range or block.</span></span>|  
  
## <a name="metadata-status-codes"></a><span data-ttu-id="94c7e-291">Meta veriler durum kodları</span><span class="sxs-lookup"><span data-stu-id="94c7e-291">Metadata status codes</span></span>  
<span data-ttu-id="94c7e-292">Aşağıdaki tabloda blob meta verileri işlemek için durum kodları listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="94c7e-292">The following table lists the status codes for processing blob metadata.</span></span>  
  
|<span data-ttu-id="94c7e-293">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="94c7e-293">Status code</span></span>|<span data-ttu-id="94c7e-294">Açıklama</span><span class="sxs-lookup"><span data-stu-id="94c7e-294">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="94c7e-295">Meta veri işleme hatasız bitirdi.</span><span class="sxs-lookup"><span data-stu-id="94c7e-295">The metadata has finished processing without errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="94c7e-296">Meta veri dosyası adı geçersiz.</span><span class="sxs-lookup"><span data-stu-id="94c7e-296">The metadata file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="94c7e-297">Meta veri dosya adı çok uzun.</span><span class="sxs-lookup"><span data-stu-id="94c7e-297">The metadata file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="94c7e-298">Meta veri dosyası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="94c7e-298">The metadata file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="94c7e-299">Meta veri dosyası için erişim reddedildi.</span><span class="sxs-lookup"><span data-stu-id="94c7e-299">Access to the metadata file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="94c7e-300">Meta veri dosyası bozuk (içerik karması eşleşmiyor).</span><span class="sxs-lookup"><span data-stu-id="94c7e-300">The metadata file is corrupted (the content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="94c7e-301">Meta veri içeriği gerekli biçime uymuyor.</span><span class="sxs-lookup"><span data-stu-id="94c7e-301">The metadata content does not conform to the required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="94c7e-302">Meta veri yazma XML başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-302">Writing the metadata XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="94c7e-303">Meta verilerine erişmek için Blob hizmeti isteği başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-303">The Blob service request to access the metadata has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="94c7e-304">Meta veriler işlenirken bir disk veya ağ g/ç hatası oluştu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-304">A disk or network I/O failure occurred while processing the metadata.</span></span>|  
|`Failed`|<span data-ttu-id="94c7e-305">Meta verileri işlenirken bilinmeyen bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-305">An unknown failure occurred while processing the metadata.</span></span>|  
|`Cancelled`|<span data-ttu-id="94c7e-306">Önceki bir hata meta işlenmesi durduruldu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-306">A prior failure has stopped further processing of the metadata.</span></span>|  
  
## <a name="properties-status-codes"></a><span data-ttu-id="94c7e-307">Özellikler durum kodları</span><span class="sxs-lookup"><span data-stu-id="94c7e-307">Properties status codes</span></span>  
<span data-ttu-id="94c7e-308">Aşağıdaki tabloda blob özellikleri işlemek için durum kodları listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="94c7e-308">The following table lists the status codes for processing blob properties.</span></span>  
  
|<span data-ttu-id="94c7e-309">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="94c7e-309">Status code</span></span>|<span data-ttu-id="94c7e-310">Açıklama</span><span class="sxs-lookup"><span data-stu-id="94c7e-310">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="94c7e-311">Özellikleri işleme hatasız bitti.</span><span class="sxs-lookup"><span data-stu-id="94c7e-311">The properties have finished processing without any errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="94c7e-312">Özellikler dosya adı geçersiz.</span><span class="sxs-lookup"><span data-stu-id="94c7e-312">The properties file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="94c7e-313">Özellikler dosya adı çok uzun.</span><span class="sxs-lookup"><span data-stu-id="94c7e-313">The properties file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="94c7e-314">Özellikler dosyası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="94c7e-314">The properties file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="94c7e-315">Özellikler dosyaya erişim reddedildi.</span><span class="sxs-lookup"><span data-stu-id="94c7e-315">Access to the properties file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="94c7e-316">Özellikler dosya bozulmuş (içerik karması eşleşmiyor).</span><span class="sxs-lookup"><span data-stu-id="94c7e-316">The properties file is corrupted (the content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="94c7e-317">Özellikler içerik gerekli biçime uymuyor.</span><span class="sxs-lookup"><span data-stu-id="94c7e-317">The properties content does not conform to the required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="94c7e-318">Özellikleri yazma XML başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-318">Writing the properties XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="94c7e-319">Özelliklerine erişmek için Blob hizmeti isteği başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-319">The Blob service request to access the properties has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="94c7e-320">Bir disk veya ağ g/ç hatası özellikleri işlenirken hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-320">A disk or network I/O failure occurred while processing the properties.</span></span>|  
|`Failed`|<span data-ttu-id="94c7e-321">Özellikler işlenirken bilinmeyen bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-321">An unknown failure occurred while processing the properties.</span></span>|  
|`Cancelled`|<span data-ttu-id="94c7e-322">Önceki bir hata özelliklerini işlenmesi durduruldu.</span><span class="sxs-lookup"><span data-stu-id="94c7e-322">A prior failure has stopped further processing of the properties.</span></span>|  
  
## <a name="sample-logs"></a><span data-ttu-id="94c7e-323">Örnek günlükleri</span><span class="sxs-lookup"><span data-stu-id="94c7e-323">Sample logs</span></span>  
<span data-ttu-id="94c7e-324">Ayrıntılı günlük bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="94c7e-324">The following is an example of verbose log.</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV123456</DriveId>  
    <Blob Status="Completed">  
       <BlobPath>pictures/bob/wild/desert.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\wild\desert.jpg</FilePath>  
       <Length>98304</Length>  
       <ImportDisposition Status="Created">overwrite</ImportDisposition>  
       <BlockList>  
          <Block Offset="0" Length="65536" Id="AAAAAA==" Hash=" 9C8AE14A55241F98533C4D80D85CDC68" Status="Completed"/>  
          <Block Offset="65536" Length="32768" Id="AQAAAA==" Hash=" DF54C531C9B3CA2570FDDDB3BCD0E27D" Status="Completed"/>  
       </BlockList>  
       <Metadata Status="Completed">  
          <GlobalPath Hash=" E34F54B7086BCF4EC1601D056F4C7E37">\Users\bob\Pictures\wild\metadata.xml</GlobalPath>  
       </Metadata>  
    </Blob>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="0" Length="65536" Hash="19701B8877418393CB3CB567F53EE225" Status="Completed"/>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
          <PageRange Offset="131072" Length="4096" Hash="9BA552E1C3EEAFFC91B42B979900A996" Status="Completed"/>  
       </PageRangeList>  
       <Properties Status="Completed">  
          <Path Hash="38D7AE80653F47F63C0222FEE90EC4E7">\Users\bob\Pictures\animals\koala.jpg.properties</Path>  
       </Properties>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
<span data-ttu-id="94c7e-325">Karşılık gelen hata günlüğü aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="94c7e-325">The corresponding error log is shown below.</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV6965824</DriveId>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
       </PageRangeList>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

 <span data-ttu-id="94c7e-326">İçe aktarma işi için izleme hata günlüğünü bir dosya içeri aktarma sürücüsünde bulunamadı hakkında bir hata içeriyor.</span><span class="sxs-lookup"><span data-stu-id="94c7e-326">The follow error log for an import job contains an error about a file not found on the import drive.</span></span> <span data-ttu-id="94c7e-327">Sonraki bileşenlerinin durumunu olduğuna dikkat edin `Cancelled`.</span><span class="sxs-lookup"><span data-stu-id="94c7e-327">Note that the status of subsequent components is `Cancelled`.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="FileNotFound">  
    <BlobPath>pictures/animals/koala.jpg</BlobPath>  
    <FilePath>\animals\koala.jpg</FilePath>  
    <Length>30310</Length>  
    <ImportDisposition Status="Cancelled">rename</ImportDisposition>  
    <BlockList>  
      <Block Offset="0" Length="6062" Id="MD5/cAzn4h7VVSWXf696qp5Uaw==" Hash="700CE7E21ED55525977FAF7AAA9E546B" Status="Cancelled" />  
      <Block Offset="6062" Length="6062" Id="MD5/PEnGwYOI8LPLNYdfKr7kAg==" Hash="3C49C6C18388F0B3CB35875F2ABEE402" Status="Cancelled" />  
      <Block Offset="12124" Length="6062" Id="MD5/FG4WxqfZKuUWZ2nGTU2qVA==" Hash="146E16C6A7D92AE5166769C64D4DAA54" Status="Cancelled" />  
      <Block Offset="18186" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
      <Block Offset="24248" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

<span data-ttu-id="94c7e-328">Aşağıdaki hata günlüğü dışarı aktarma işi için blob içeriğinin diske yazıldı, ancak blob'un özellikleri dışarı aktarılırken bir hata oluştu gösterir.</span><span class="sxs-lookup"><span data-stu-id="94c7e-328">The following error log for an export job indicates that the blob content has been successfully written to the drive, but that an error occurred while exporting the blob's properties.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C3U</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
    <FilePath>\pictures\wild\canyon.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList />  
    <Properties Status="Failed" />  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
## <a name="next-steps"></a><span data-ttu-id="94c7e-329">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="94c7e-329">Next steps</span></span>
 
* [<span data-ttu-id="94c7e-330">Depolama içeri/dışarı aktarma REST API'si</span><span class="sxs-lookup"><span data-stu-id="94c7e-330">Storage Import/Export REST API</span></span>](/rest/api/storageimportexport/)
