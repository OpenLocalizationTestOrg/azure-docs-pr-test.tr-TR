---
title: "aaaAzure içeri/dışarı aktarma günlük dosyası biçimi | Microsoft Docs"
description: "İçeri/dışarı aktarma hizmeti işi için adımları çalıştırıldığında oluşturulan hello günlük dosyalarını hello biçimi hakkında bilgi edinin."
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
ms.openlocfilehash: 15a652455aa947922af0aa39ccefe68811a3db19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-log-file-format"></a><span data-ttu-id="8cb78-103">Azure içeri/dışarı aktarma hizmeti günlük dosyası biçimi</span><span class="sxs-lookup"><span data-stu-id="8cb78-103">Azure Import/Export service log file format</span></span>
<span data-ttu-id="8cb78-104">Merhaba Microsoft Azure içeri/dışarı aktarma hizmeti bir alma işi veya bir dışarı aktarma işinin parçası olarak bir sürücüde bir eylem gerçekleştirdiğinde, günlükleri hello depolama hesabındaki bu işle ilişkili tooblock BLOB'lar yazılır.</span><span class="sxs-lookup"><span data-stu-id="8cb78-104">When hello Microsoft Azure Import/Export service performs an action on a drive as part of an import job or an export job, logs are written tooblock blobs in hello storage account associated with that job.</span></span>  
  
<span data-ttu-id="8cb78-105">İçeri/dışarı aktarma hizmeti hello tarafından yazılan iki günlükleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8cb78-105">There are two logs that may be written by hello Import/Export service:</span></span>  
  
-   <span data-ttu-id="8cb78-106">Merhaba hata günlüğü her zaman bir hata hello olayda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8cb78-106">hello error log is always generated in hello event of an error.</span></span>  
  
-   <span data-ttu-id="8cb78-107">Merhaba ayrıntılı günlük varsayılan olarak etkin değildir, ancak ayarı hello tarafından etkinleştirilebilir `EnableVerboseLog` özelliği bir [Put işlemini](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) veya [güncelleştirme işi özellikleri](/rest/api/storageimportexport/jobs#Jobs_Update) işlemi.</span><span class="sxs-lookup"><span data-stu-id="8cb78-107">hello verbose log is not enabled by default, but may be enabled by setting hello `EnableVerboseLog` property on a [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation.</span></span>  
  
## <a name="log-file-location"></a><span data-ttu-id="8cb78-108">Günlük dosyası konumu</span><span class="sxs-lookup"><span data-stu-id="8cb78-108">Log file location</span></span>  
<span data-ttu-id="8cb78-109">Merhaba günlükleri tooblock BLOB'lar hello kapsayıcı veya hello tarafından belirtilen sanal dizin yazılır `ImportExportStatesPath` üzerinde ayarlayabilirsiniz ayarı bir `Put Job` işlemi.</span><span class="sxs-lookup"><span data-stu-id="8cb78-109">hello logs are written tooblock blobs in hello container or virtual directory specified by hello `ImportExportStatesPath` setting, which you can set on a `Put Job` operation.</span></span> <span data-ttu-id="8cb78-110">Merhaba konumu toowhich hello günlükleri bağlıdır nasıl kimlik doğrulaması için belirtilen başlangıç değeri ile birlikte hello işi için belirtilen üzerine yazılır `ImportExportStatesPath`.</span><span class="sxs-lookup"><span data-stu-id="8cb78-110">hello location toowhich hello logs are written depends on how authentication is specified for hello job, together with hello value specified for `ImportExportStatesPath`.</span></span> <span data-ttu-id="8cb78-111">Kimlik doğrulaması hello işi için bir depolama hesabı anahtarı ya da bir kapsayıcı SAS (paylaşılan erişim imzası) belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="8cb78-111">Authentication for hello job may be specified via a storage account key, or a container SAS (shared access signature).</span></span>  
  
<span data-ttu-id="8cb78-112">Merhaba hello kapsayıcı veya sanal dizin adını olabilir ya da olması hello varsayılan adını `waimportexport`, veya başka bir kapsayıcı veya sanal dizin adı.</span><span class="sxs-lookup"><span data-stu-id="8cb78-112">hello name of hello container or virtual directory may either be hello default name of `waimportexport`, or another container or virtual directory name that you specify.</span></span>  
  
<span data-ttu-id="8cb78-113">Merhaba tabloda hello olası seçenekleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="8cb78-113">hello table below shows hello possible options:</span></span>  
  
|<span data-ttu-id="8cb78-114">Kimlik Doğrulama Yöntemi</span><span class="sxs-lookup"><span data-stu-id="8cb78-114">Authentication Method</span></span>|<span data-ttu-id="8cb78-115">Değeri `ImportExportStatesPath`öğesi</span><span class="sxs-lookup"><span data-stu-id="8cb78-115">Value of `ImportExportStatesPath`Element</span></span>|<span data-ttu-id="8cb78-116">Günlük BLOB'lar konumu</span><span class="sxs-lookup"><span data-stu-id="8cb78-116">Location of Log Blobs</span></span>|  
|---------------------------|----------------------------------------------|---------------------------|  
|<span data-ttu-id="8cb78-117">Depolama hesabı anahtarı</span><span class="sxs-lookup"><span data-stu-id="8cb78-117">Storage account key</span></span>|<span data-ttu-id="8cb78-118">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="8cb78-118">Default value</span></span>|<span data-ttu-id="8cb78-119">Adlı bir kapsayıcı `waimportexport`, hello varsayılan kapsayıcı olduğu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-119">A container named `waimportexport`, which is hello default container.</span></span> <span data-ttu-id="8cb78-120">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8cb78-120">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|<span data-ttu-id="8cb78-121">Depolama hesabı anahtarı</span><span class="sxs-lookup"><span data-stu-id="8cb78-121">Storage account key</span></span>|<span data-ttu-id="8cb78-122">Kullanıcı tarafından belirtilen değeri</span><span class="sxs-lookup"><span data-stu-id="8cb78-122">User-specified value</span></span>|<span data-ttu-id="8cb78-123">Merhaba kullanıcı tarafından adlı bir kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="8cb78-123">A container named by hello user.</span></span> <span data-ttu-id="8cb78-124">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8cb78-124">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|<span data-ttu-id="8cb78-125">Kapsayıcı SAS</span><span class="sxs-lookup"><span data-stu-id="8cb78-125">Container SAS</span></span>|<span data-ttu-id="8cb78-126">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="8cb78-126">Default value</span></span>|<span data-ttu-id="8cb78-127">Adlı bir sanal dizini `waimportexport`, hello SAS belirtilen hello kapsayıcısı altında hello varsayılan adı olduğu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-127">A virtual directory named `waimportexport`, which is hello default name, beneath hello container specified in hello SAS.</span></span><br /><br /> <span data-ttu-id="8cb78-128">Örneğin, hello SAS belirtilen hello iş ise `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, hello günlük konumu şu şekilde olacaktır`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span><span class="sxs-lookup"><span data-stu-id="8cb78-128">For example, if hello SAS specified for hello job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, then hello log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span></span>|  
|<span data-ttu-id="8cb78-129">Kapsayıcı SAS</span><span class="sxs-lookup"><span data-stu-id="8cb78-129">Container SAS</span></span>|<span data-ttu-id="8cb78-130">Kullanıcı tarafından belirtilen değeri</span><span class="sxs-lookup"><span data-stu-id="8cb78-130">User-specified value</span></span>|<span data-ttu-id="8cb78-131">Merhaba SAS belirtilen hello kapsayıcısı altında hello kullanıcı tarafından adlı bir sanal dizini.</span><span class="sxs-lookup"><span data-stu-id="8cb78-131">A virtual directory named by hello user, beneath hello container specified in hello SAS.</span></span><br /><br /> <span data-ttu-id="8cb78-132">Örneğin, hello SAS belirtilen hello iş ise `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, ve hello belirtilen sanal dizin adlandırılan `mylogblobs`, hello günlük konumu şu şekilde olacaktır `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span><span class="sxs-lookup"><span data-stu-id="8cb78-132">For example, if hello SAS specified for hello job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, and hello specified virtual directory is named `mylogblobs`, then hello log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span></span>|  
  
<span data-ttu-id="8cb78-133">Arama hello tarafından hello URL'sini hello hata ve ayrıntılı günlükleri alabilirsiniz [alma işi](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) işlemi.</span><span class="sxs-lookup"><span data-stu-id="8cb78-133">You can retrieve hello URL for hello error and verbose logs by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="8cb78-134">Merhaba günlüklerini hello sürücü işlenmesini tamamlandıktan sonra kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8cb78-134">hello logs are available after processing of hello drive is complete.</span></span>  
  
## <a name="log-file-format"></a><span data-ttu-id="8cb78-135">Günlük dosyası biçimi</span><span class="sxs-lookup"><span data-stu-id="8cb78-135">Log file format</span></span>  
<span data-ttu-id="8cb78-136">Merhaba her iki günlük biçimi olan hello aynı: hello sabit sürücü ve hello müşterinin hesabına arasında BLOB'ları kopyalanırken oluştu hello olayları XML açıklamaları içeren blob.</span><span class="sxs-lookup"><span data-stu-id="8cb78-136">hello format for both logs is hello same: a blob containing XML descriptions of hello events that occurred while copying blobs between hello hard drive and hello customer's account.</span></span>  
  
<span data-ttu-id="8cb78-137">Hello hata günlüğü yalnızca hello bilgi BLOB veya hello sırasında hatalarla karşılaştı dosyaları için içerirken hello ayrıntılı günlüğü, her blob (için içeri aktarma işi için) veya dosyası (bir dışarı aktarma işinin), başlangıç kopyalama işlemi hello durumu hakkında tam bilgi içerir. içeri veya dışarı aktarma işi.</span><span class="sxs-lookup"><span data-stu-id="8cb78-137">hello verbose log contains complete information about hello status of hello copy operation for every blob (for an import job) or file (for an export job), whereas hello error log contains only hello information for blobs or files that encountered errors during hello import or export job.</span></span>  
  
<span data-ttu-id="8cb78-138">Merhaba ayrıntılı günlük biçimi aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8cb78-138">hello verbose log format is shown below.</span></span> <span data-ttu-id="8cb78-139">Merhaba hata günlüğü aynı yapısı, ancak başarılı işlemleri filtreler hello vardır.</span><span class="sxs-lookup"><span data-stu-id="8cb78-139">hello error log has hello same structure, but filters out successful operations.</span></span>  

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

<span data-ttu-id="8cb78-140">Merhaba aşağıdaki tabloda hello günlük dosyasının hello öğelerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="8cb78-140">hello following table describes hello elements of hello log file.</span></span>  
  
|<span data-ttu-id="8cb78-141">XML öğesi</span><span class="sxs-lookup"><span data-stu-id="8cb78-141">XML Element</span></span>|<span data-ttu-id="8cb78-142">Tür</span><span class="sxs-lookup"><span data-stu-id="8cb78-142">Type</span></span>|<span data-ttu-id="8cb78-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cb78-143">Description</span></span>|  
|-----------------|----------|-----------------|  
|`DriveLog`|<span data-ttu-id="8cb78-144">XML öğesi</span><span class="sxs-lookup"><span data-stu-id="8cb78-144">XML Element</span></span>|<span data-ttu-id="8cb78-145">Bir sürücü günlük temsil eder.</span><span class="sxs-lookup"><span data-stu-id="8cb78-145">Represents a drive log.</span></span>|  
|`Version`|<span data-ttu-id="8cb78-146">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="8cb78-146">Attribute, String</span></span>|<span data-ttu-id="8cb78-147">Merhaba günlük biçimi Hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="8cb78-147">hello version of hello log format.</span></span>|  
|`DriveId`|<span data-ttu-id="8cb78-148">Dize</span><span class="sxs-lookup"><span data-stu-id="8cb78-148">String</span></span>|<span data-ttu-id="8cb78-149">sürücünün donanım seri numarası hello.</span><span class="sxs-lookup"><span data-stu-id="8cb78-149">hello drive's hardware serial number.</span></span>|  
|`Status`|<span data-ttu-id="8cb78-150">Dize</span><span class="sxs-lookup"><span data-stu-id="8cb78-150">String</span></span>|<span data-ttu-id="8cb78-151">Merhaba sürücü işlem durumu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-151">Status of hello drive processing.</span></span> <span data-ttu-id="8cb78-152">Merhaba bkz `Drive Status Codes` daha fazla bilgi için tablo aşağıda.</span><span class="sxs-lookup"><span data-stu-id="8cb78-152">See hello `Drive Status Codes` table below for more information.</span></span>|  
|`Blob`|<span data-ttu-id="8cb78-153">İç içe geçmiş XML öğesi</span><span class="sxs-lookup"><span data-stu-id="8cb78-153">Nested XML element</span></span>|<span data-ttu-id="8cb78-154">Bir blob temsil eder.</span><span class="sxs-lookup"><span data-stu-id="8cb78-154">Represents a blob.</span></span>|  
|`Blob/BlobPath`|<span data-ttu-id="8cb78-155">Dize</span><span class="sxs-lookup"><span data-stu-id="8cb78-155">String</span></span>|<span data-ttu-id="8cb78-156">Merhaba hello blob URI'si.</span><span class="sxs-lookup"><span data-stu-id="8cb78-156">hello URI of hello blob.</span></span>|  
|`Blob/FilePath`|<span data-ttu-id="8cb78-157">Dize</span><span class="sxs-lookup"><span data-stu-id="8cb78-157">String</span></span>|<span data-ttu-id="8cb78-158">Merhaba sürücüde Hello göreli yol toohello dosyası.</span><span class="sxs-lookup"><span data-stu-id="8cb78-158">hello relative path toohello file on hello drive.</span></span>|  
|`Blob/Snapshot`|<span data-ttu-id="8cb78-159">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="8cb78-159">DateTime</span></span>|<span data-ttu-id="8cb78-160">Anlık görüntü sürümü yalnızca bir dışa aktarma işi için hello blob Hello.</span><span class="sxs-lookup"><span data-stu-id="8cb78-160">hello snapshot version of hello blob, for an export job only.</span></span>|  
|`Blob/Length`|<span data-ttu-id="8cb78-161">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="8cb78-161">Integer</span></span>|<span data-ttu-id="8cb78-162">Merhaba toplam hello blob bayt cinsinden uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-162">hello total length of hello blob in bytes.</span></span>|  
|`Blob/LastModified`|<span data-ttu-id="8cb78-163">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="8cb78-163">DateTime</span></span>|<span data-ttu-id="8cb78-164">Merhaba tarih o hello blob son, yalnızca bir dışarı aktarma işinin değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="8cb78-164">hello date/time that hello blob was last modified, for an export job only.</span></span>|  
|`Blob/ImportDisposition`|<span data-ttu-id="8cb78-165">Dize</span><span class="sxs-lookup"><span data-stu-id="8cb78-165">String</span></span>|<span data-ttu-id="8cb78-166">Merhaba, yalnızca bir içeri aktarma işi için hello blob eğilimini alın.</span><span class="sxs-lookup"><span data-stu-id="8cb78-166">hello import disposition of hello blob, for an import job only.</span></span>|  
|`Blob/ImportDisposition/@Status`|<span data-ttu-id="8cb78-167">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="8cb78-167">Attribute, String</span></span>|<span data-ttu-id="8cb78-168">Merhaba Hello durumunu değerlendirme içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="8cb78-168">hello status of hello import disposition.</span></span>|  
|`PageRangeList`|<span data-ttu-id="8cb78-169">İç içe geçmiş XML öğesi</span><span class="sxs-lookup"><span data-stu-id="8cb78-169">Nested XML element</span></span>|<span data-ttu-id="8cb78-170">Bir sayfa blob'u için sayfa aralıklarını listesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="8cb78-170">Represents a list of page ranges for a page blob.</span></span>|  
|`PageRange`|<span data-ttu-id="8cb78-171">XML öğesi</span><span class="sxs-lookup"><span data-stu-id="8cb78-171">XML element</span></span>|<span data-ttu-id="8cb78-172">Sayfa aralığını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="8cb78-172">Represents a page range.</span></span>|  
|`PageRange/@Offset`|<span data-ttu-id="8cb78-173">Öznitelik, tamsayı</span><span class="sxs-lookup"><span data-stu-id="8cb78-173">Attribute, Integer</span></span>|<span data-ttu-id="8cb78-174">Merhaba sayfa aralığı uzaklığı hello blob başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="8cb78-174">Starting offset of hello page range in hello blob.</span></span>|  
|`PageRange/@Length`|<span data-ttu-id="8cb78-175">Öznitelik, tamsayı</span><span class="sxs-lookup"><span data-stu-id="8cb78-175">Attribute, Integer</span></span>|<span data-ttu-id="8cb78-176">Merhaba sayfa aralığının bayt cinsinden uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-176">Length in bytes of hello page range.</span></span>|  
|`PageRange/@Hash`|<span data-ttu-id="8cb78-177">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="8cb78-177">Attribute, String</span></span>|<span data-ttu-id="8cb78-178">Base16 kodlanmış MD5 karması hello sayfa aralığı.</span><span class="sxs-lookup"><span data-stu-id="8cb78-178">Base16-encoded MD5 hash of hello page range.</span></span>|  
|`PageRange/@Status`|<span data-ttu-id="8cb78-179">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="8cb78-179">Attribute, String</span></span>|<span data-ttu-id="8cb78-180">Merhaba sayfa aralığı işlem durumu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-180">Status of processing hello page range.</span></span>|  
|`BlockList`|<span data-ttu-id="8cb78-181">İç içe geçmiş XML öğesi</span><span class="sxs-lookup"><span data-stu-id="8cb78-181">Nested XML element</span></span>|<span data-ttu-id="8cb78-182">Bir blok blobu için blok listesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="8cb78-182">Represents a list of blocks for a block blob.</span></span>|  
|`Block`|<span data-ttu-id="8cb78-183">XML öğesi</span><span class="sxs-lookup"><span data-stu-id="8cb78-183">XML element</span></span>|<span data-ttu-id="8cb78-184">Bloğunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="8cb78-184">Represents a block.</span></span>|  
|`Block/@Offset`|<span data-ttu-id="8cb78-185">Öznitelik, tamsayı</span><span class="sxs-lookup"><span data-stu-id="8cb78-185">Attribute, Integer</span></span>|<span data-ttu-id="8cb78-186">Merhaba blob hello bloğunda başlangıç uzaklığı.</span><span class="sxs-lookup"><span data-stu-id="8cb78-186">Starting offset of hello block in hello blob.</span></span>|  
|`Block/@Length`|<span data-ttu-id="8cb78-187">Öznitelik, tamsayı</span><span class="sxs-lookup"><span data-stu-id="8cb78-187">Attribute, Integer</span></span>|<span data-ttu-id="8cb78-188">Merhaba bloğunun bayt cinsinden uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-188">Length in bytes of hello block.</span></span>|  
|`Block/@Id`|<span data-ttu-id="8cb78-189">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="8cb78-189">Attribute, String</span></span>|<span data-ttu-id="8cb78-190">Merhaba blok kimliği</span><span class="sxs-lookup"><span data-stu-id="8cb78-190">hello block ID.</span></span>|  
|`Block/@Hash`|<span data-ttu-id="8cb78-191">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="8cb78-191">Attribute, String</span></span>|<span data-ttu-id="8cb78-192">Base16 kodlu MD5 karması hello bloğu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-192">Base16-encoded MD5 hash of hello block.</span></span>|  
|`Block/@Status`|<span data-ttu-id="8cb78-193">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="8cb78-193">Attribute, String</span></span>|<span data-ttu-id="8cb78-194">Merhaba blok işlem durumu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-194">Status of processing hello block.</span></span>|  
|`Metadata`|<span data-ttu-id="8cb78-195">İç içe geçmiş XML öğesi</span><span class="sxs-lookup"><span data-stu-id="8cb78-195">Nested XML element</span></span>|<span data-ttu-id="8cb78-196">Merhaba blob'un meta verileri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="8cb78-196">Represents hello blob's metadata.</span></span>|  
|`Metadata/@Status`|<span data-ttu-id="8cb78-197">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="8cb78-197">Attribute, String</span></span>|<span data-ttu-id="8cb78-198">Merhaba blob meta verileri işlenmesini durumu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-198">Status of processing of hello blob metadata.</span></span>|  
|`Metadata/GlobalPath`|<span data-ttu-id="8cb78-199">Dize</span><span class="sxs-lookup"><span data-stu-id="8cb78-199">String</span></span>|<span data-ttu-id="8cb78-200">Göreli yol toohello genel meta veri dosyası.</span><span class="sxs-lookup"><span data-stu-id="8cb78-200">Relative path toohello global metadata file.</span></span>|  
|`Metadata/GlobalPath/@Hash`|<span data-ttu-id="8cb78-201">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="8cb78-201">Attribute, String</span></span>|<span data-ttu-id="8cb78-202">Base16 kodlu MD5 karması hello genel meta veri dosyası.</span><span class="sxs-lookup"><span data-stu-id="8cb78-202">Base16-encoded MD5 hash of hello global metadata file.</span></span>|  
|`Metadata/Path`|<span data-ttu-id="8cb78-203">Dize</span><span class="sxs-lookup"><span data-stu-id="8cb78-203">String</span></span>|<span data-ttu-id="8cb78-204">Göreli yol toohello meta veri dosyası.</span><span class="sxs-lookup"><span data-stu-id="8cb78-204">Relative path toohello metadata file.</span></span>|  
|`Metadata/Path/@Hash`|<span data-ttu-id="8cb78-205">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="8cb78-205">Attribute, String</span></span>|<span data-ttu-id="8cb78-206">Base16 kodlu MD5 karması hello meta veri dosyası.</span><span class="sxs-lookup"><span data-stu-id="8cb78-206">Base16-encoded MD5 hash of hello metadata file.</span></span>|  
|`Properties`|<span data-ttu-id="8cb78-207">İç içe geçmiş XML öğesi</span><span class="sxs-lookup"><span data-stu-id="8cb78-207">Nested XML element</span></span>|<span data-ttu-id="8cb78-208">Merhaba blob özelliklerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="8cb78-208">Represents hello blob properties.</span></span>|  
|`Properties/@Status`|<span data-ttu-id="8cb78-209">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="8cb78-209">Attribute, String</span></span>|<span data-ttu-id="8cb78-210">Merhaba blob özellikleri, örneğin dosya bulunamadı, işleme durumunu tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="8cb78-210">Status of processing hello blob properties, e.g. file not found, completed.</span></span>|  
|`Properties/GlobalPath`|<span data-ttu-id="8cb78-211">Dize</span><span class="sxs-lookup"><span data-stu-id="8cb78-211">String</span></span>|<span data-ttu-id="8cb78-212">Göreli yol toohello genel özellikleri dosya.</span><span class="sxs-lookup"><span data-stu-id="8cb78-212">Relative path toohello global properties file.</span></span>|  
|`Properties/GlobalPath/@Hash`|<span data-ttu-id="8cb78-213">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="8cb78-213">Attribute, String</span></span>|<span data-ttu-id="8cb78-214">Base16 kodlu MD5 karma değeri hello genel özellikleri dosyasının.</span><span class="sxs-lookup"><span data-stu-id="8cb78-214">Base16-encoded MD5 hash of hello global properties file.</span></span>|  
|`Properties/Path`|<span data-ttu-id="8cb78-215">Dize</span><span class="sxs-lookup"><span data-stu-id="8cb78-215">String</span></span>|<span data-ttu-id="8cb78-216">Göreli yol toohello özellikleri dosya.</span><span class="sxs-lookup"><span data-stu-id="8cb78-216">Relative path toohello properties file.</span></span>|  
|`Properties/Path/@Hash`|<span data-ttu-id="8cb78-217">Öznitelik, dize</span><span class="sxs-lookup"><span data-stu-id="8cb78-217">Attribute, String</span></span>|<span data-ttu-id="8cb78-218">Base16 kodlu MD5 karma değeri hello özellikleri dosyasının.</span><span class="sxs-lookup"><span data-stu-id="8cb78-218">Base16-encoded MD5 hash of hello properties file.</span></span>|  
|`Blob/Status`|<span data-ttu-id="8cb78-219">Dize</span><span class="sxs-lookup"><span data-stu-id="8cb78-219">String</span></span>|<span data-ttu-id="8cb78-220">Merhaba blob işlem durumu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-220">Status of processing hello blob.</span></span>|  
  
# <a name="drive-status-codes"></a><span data-ttu-id="8cb78-221">Sürücü durum kodları</span><span class="sxs-lookup"><span data-stu-id="8cb78-221">Drive status codes</span></span>  
<span data-ttu-id="8cb78-222">Merhaba aşağıdaki tabloda bir sürücü işlemeye hello durum kodlarını listeler.</span><span class="sxs-lookup"><span data-stu-id="8cb78-222">hello following table lists hello status codes for processing a drive.</span></span>  
  
|<span data-ttu-id="8cb78-223">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="8cb78-223">Status code</span></span>|<span data-ttu-id="8cb78-224">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cb78-224">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="8cb78-225">Merhaba sürücü hatasız işleme tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="8cb78-225">hello drive has finished processing without any errors.</span></span>|  
|`CompletedWithWarnings`|<span data-ttu-id="8cb78-226">Merhaba sürücü işleme hello BLOB'lar için belirtilen hello alma değerlendirmeleri başına bir veya daha fazla BLOB uyarılarla tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="8cb78-226">hello drive has finished processing with warnings in one or more blobs per hello import dispositions specified for hello blobs.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="8cb78-227">Merhaba sürücü bir veya daha fazla BLOB veya öbekleri hatalarla tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="8cb78-227">hello drive has finished with errors in one or more blobs or chunks.</span></span>|  
|`DiskNotFound`|<span data-ttu-id="8cb78-228">Hello sürücüsünde hiçbir disk bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8cb78-228">No disk is found on hello drive.</span></span>|  
|`VolumeNotNtfs`|<span data-ttu-id="8cb78-229">Merhaba disk üzerindeki Hello ilk veri birimi NTFS biçiminde değil.</span><span class="sxs-lookup"><span data-stu-id="8cb78-229">hello first data volume on hello disk is not in NTFS format.</span></span>|  
|`DiskOperationFailed`|<span data-ttu-id="8cb78-230">Merhaba sürücü üzerinde işlem gerçekleştirilirken bilinmeyen bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-230">An unknown failure occurred when performing operations on hello drive.</span></span>|  
|`BitLockerVolumeNotFound`|<span data-ttu-id="8cb78-231">BitLocker encryptable birim bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8cb78-231">No BitLocker encryptable volume is found.</span></span>|  
|`BitLockerNotActivated`|<span data-ttu-id="8cb78-232">Merhaba birimde BitLocker etkin değil.</span><span class="sxs-lookup"><span data-stu-id="8cb78-232">BitLocker is not enabled on hello volume.</span></span>|  
|`BitLockerProtectorNotFound`|<span data-ttu-id="8cb78-233">Merhaba sayısal parola anahtar koruyucusu hello birimde yok.</span><span class="sxs-lookup"><span data-stu-id="8cb78-233">hello numerical password key protector does not exist on hello volume.</span></span>|  
|`BitLockerKeyInvalid`|<span data-ttu-id="8cb78-234">sağlanan hello sayısal parola hello birimin kilidi açılamıyor.</span><span class="sxs-lookup"><span data-stu-id="8cb78-234">hello numerical password provided cannot unlock hello volume.</span></span>|  
|`BitLockerUnlockVolumeFailed`|<span data-ttu-id="8cb78-235">Toounlock hello birim çalışırken bilinmeyen bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-235">Unknown failure has happened when trying toounlock hello volume.</span></span>|  
|`BitLockerFailed`|<span data-ttu-id="8cb78-236">BitLocker işlem gerçekleştirilirken bilinmeyen bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-236">An unknown failure occurred while performing BitLocker operations.</span></span>|  
|`ManifestNameInvalid`|<span data-ttu-id="8cb78-237">Merhaba yayılma dosyası adı geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8cb78-237">hello manifest file name is invalid.</span></span>|  
|`ManifestNameTooLong`|<span data-ttu-id="8cb78-238">Merhaba yayılma dosyası adı çok uzun.</span><span class="sxs-lookup"><span data-stu-id="8cb78-238">hello manifest file name is too long.</span></span>|  
|`ManifestNotFound`|<span data-ttu-id="8cb78-239">Merhaba bildirim dosyası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8cb78-239">hello manifest file is not found.</span></span>|  
|`ManifestAccessDenied`|<span data-ttu-id="8cb78-240">Bildirim toohello dosyası, erişim reddedildi.</span><span class="sxs-lookup"><span data-stu-id="8cb78-240">Access toohello manifest file is denied.</span></span>|  
|`ManifestCorrupted`|<span data-ttu-id="8cb78-241">Merhaba bildirim dosyası bozuk (Merhaba içerik karması eşleşmiyor).</span><span class="sxs-lookup"><span data-stu-id="8cb78-241">hello manifest file is corrupted (hello content does not match its hash).</span></span>|  
|`ManifestFormatInvalid`|<span data-ttu-id="8cb78-242">Merhaba bildirim içerik toohello gerekli biçime uymuyor.</span><span class="sxs-lookup"><span data-stu-id="8cb78-242">hello manifest content does not conform toohello required format.</span></span>|  
|`ManifestDriveIdMismatch`|<span data-ttu-id="8cb78-243">Sürücü Kimliği hello bildirim dosyasında bir hello sürücüden okumayı hello eşleşmiyor hello.</span><span class="sxs-lookup"><span data-stu-id="8cb78-243">hello drive ID in hello manifest file does not match hello one read from hello drive.</span></span>|  
|`ReadManifestFailed`|<span data-ttu-id="8cb78-244">Merhaba bildirimindeki okunurken bir disk g/ç hatası oluştu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-244">A disk I/O failure occurred while reading from hello manifest.</span></span>|  
|`BlobListFormatInvalid`|<span data-ttu-id="8cb78-245">Merhaba verme blob listesi blob toohello gerekli biçime uymuyor.</span><span class="sxs-lookup"><span data-stu-id="8cb78-245">hello export blob list blob does not conform toohello required format.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="8cb78-246">Merhaba depolama hesabındaki toohello blob'lara erişim yasaklandı.</span><span class="sxs-lookup"><span data-stu-id="8cb78-246">Access toohello blobs in hello storage account is forbidden.</span></span> <span data-ttu-id="8cb78-247">Bu tooinvalid depolama hesabı anahtarı veya kapsayıcı SAS olabilir.</span><span class="sxs-lookup"><span data-stu-id="8cb78-247">This might be due tooinvalid storage account key or container SAS.</span></span>|  
|`InternalError`|<span data-ttu-id="8cb78-248">Ve hello sürücü işlenirken iç hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-248">And internal error occurred while processing hello drive.</span></span>|  
  
## <a name="blob-status-codes"></a><span data-ttu-id="8cb78-249">BLOB durum kodları</span><span class="sxs-lookup"><span data-stu-id="8cb78-249">Blob status codes</span></span>  
<span data-ttu-id="8cb78-250">Merhaba aşağıdaki tabloda bir blob işlemeye hello durum kodlarını listeler.</span><span class="sxs-lookup"><span data-stu-id="8cb78-250">hello following table lists hello status codes for processing a blob.</span></span>  
  
|<span data-ttu-id="8cb78-251">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="8cb78-251">Status code</span></span>|<span data-ttu-id="8cb78-252">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cb78-252">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="8cb78-253">Merhaba blob hatasız işleme tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="8cb78-253">hello blob has finished processing without errors.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="8cb78-254">Merhaba blob işleme bir veya daha fazla sayfa aralıklarını veya blokları, meta verileri veya özellikler hatalarla tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="8cb78-254">hello blob has finished processing with errors in one or more page ranges or blocks, metadata, or properties.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="8cb78-255">Merhaba dosya adı geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8cb78-255">hello file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="8cb78-256">Merhaba dosya adı çok uzun.</span><span class="sxs-lookup"><span data-stu-id="8cb78-256">hello file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="8cb78-257">Merhaba dosyası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8cb78-257">hello file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="8cb78-258">Toohello dosyasına erişim engellendi.</span><span class="sxs-lookup"><span data-stu-id="8cb78-258">Access toohello file is denied.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="8cb78-259">blob tooaccess hello hello Blob hizmeti isteği başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-259">hello Blob service request tooaccess hello blob has failed.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="8cb78-260">blob tooaccess hello hello Blob hizmet isteği izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="8cb78-260">hello Blob service request tooaccess hello blob is forbidden.</span></span> <span data-ttu-id="8cb78-261">Bu tooinvalid depolama hesabı anahtarı veya kapsayıcı SAS olabilir.</span><span class="sxs-lookup"><span data-stu-id="8cb78-261">This might be due tooinvalid storage account key or container SAS.</span></span>|  
|`RenameFailed`|<span data-ttu-id="8cb78-262">(İçin bir alma işi) toorename hello blob veya hello dosyası (bir dışarı aktarma işinin) başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-262">Failed toorename hello blob (for an import job) or hello file (for an export job).</span></span>|  
|`BlobUnexpectedChange`|<span data-ttu-id="8cb78-263">Beklenmedik bir değişikliği (için bir dışarı aktarma işinin) hello blob ile oluştu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-263">An unexpected change has occurred with hello blob (for an export job).</span></span>|  
|`LeasePresent`|<span data-ttu-id="8cb78-264">Merhaba blob üzerindeki mevcut bir kira var.</span><span class="sxs-lookup"><span data-stu-id="8cb78-264">There is a lease present on hello blob.</span></span>|  
|`IOFailed`|<span data-ttu-id="8cb78-265">Bir disk veya ağ g/ç hatası hello blob işlenirken hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-265">A disk or network I/O failure occurred while processing hello blob.</span></span>|  
|`Failed`|<span data-ttu-id="8cb78-266">Merhaba blob işlenirken bilinmeyen bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-266">An unknown failure occurred while processing hello blob.</span></span>|  
  
## <a name="import-disposition-status-codes"></a><span data-ttu-id="8cb78-267">İçeri aktarma değerlendirme durum kodları</span><span class="sxs-lookup"><span data-stu-id="8cb78-267">Import disposition status codes</span></span>  
<span data-ttu-id="8cb78-268">Merhaba aşağıdaki tabloda bir alma değerlendirme çözmek için hello durum kodlarını listeler.</span><span class="sxs-lookup"><span data-stu-id="8cb78-268">hello following table lists hello status codes for resolving an import disposition.</span></span>  
  
|<span data-ttu-id="8cb78-269">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="8cb78-269">Status code</span></span>|<span data-ttu-id="8cb78-270">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cb78-270">Description</span></span>|  
|-----------------|-----------------|  
|`Created`|<span data-ttu-id="8cb78-271">Merhaba blob oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-271">hello blob has been created.</span></span>|  
|`Renamed`|<span data-ttu-id="8cb78-272">Merhaba blob adlandırma alma değerlendirme adlandırıldı.</span><span class="sxs-lookup"><span data-stu-id="8cb78-272">hello blob has been renamed per rename import disposition.</span></span> <span data-ttu-id="8cb78-273">Merhaba `Blob/BlobPath` öğe yeniden adlandırılmış hello blob Merhaba URI içeriyor.</span><span class="sxs-lookup"><span data-stu-id="8cb78-273">hello `Blob/BlobPath` element contains hello URI for hello renamed blob.</span></span>|  
|`Skipped`|<span data-ttu-id="8cb78-274">Merhaba blob atlandı başına `no-overwrite` değerlendirme içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="8cb78-274">hello blob has been skipped per `no-overwrite` import disposition.</span></span>|  
|`Overwritten`|<span data-ttu-id="8cb78-275">Merhaba blob bir blob başına üzerine `overwrite` değerlendirme içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="8cb78-275">hello blob has overwritten an existing blob per `overwrite` import disposition.</span></span>|  
|`Cancelled`|<span data-ttu-id="8cb78-276">Önceki bir hata hello alma eğilimini işlenmesi durduruldu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-276">A prior failure has stopped further processing of hello import disposition.</span></span>|  
  
## <a name="page-rangeblock-status-codes"></a><span data-ttu-id="8cb78-277">Sayfa aralık/blok durum kodları</span><span class="sxs-lookup"><span data-stu-id="8cb78-277">Page range/block status codes</span></span>  
<span data-ttu-id="8cb78-278">Merhaba aşağıdaki tabloda bir sayfa aralığı veya bir blok işlemeye hello durum kodlarını listeler.</span><span class="sxs-lookup"><span data-stu-id="8cb78-278">hello following table lists hello status codes for processing a page range or a block.</span></span>  
  
|<span data-ttu-id="8cb78-279">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="8cb78-279">Status code</span></span>|<span data-ttu-id="8cb78-280">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cb78-280">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="8cb78-281">Başlangıç sayfası aralık veya blok hatasız işleme tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="8cb78-281">hello page range or block has finished processing without any errors.</span></span>|  
|`Committed`|<span data-ttu-id="8cb78-282">Merhaba blok kaydedildi, ancak değil hello tam engelleme listesi diğer blokları başarısız oldu veya tam engelleme listesi kendisini put başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-282">hello block has been committed,  but not in hello full block list because other blocks have failed, or put full block list itself has failed.</span></span>|  
|`Uncommitted`|<span data-ttu-id="8cb78-283">Merhaba blok karşıya ancak edilmemiş.</span><span class="sxs-lookup"><span data-stu-id="8cb78-283">hello block is uploaded but not committed.</span></span>|  
|`Corrupted`|<span data-ttu-id="8cb78-284">Başlangıç sayfası aralık veya blok bozuk (Merhaba içerik karması eşleşmiyor).</span><span class="sxs-lookup"><span data-stu-id="8cb78-284">hello page range or block is corrupted (hello content does not match its hash).</span></span>|  
|`FileUnexpectedEnd`|<span data-ttu-id="8cb78-285">Bir beklenmeyen dosya sonu karşılaşıldı.</span><span class="sxs-lookup"><span data-stu-id="8cb78-285">An unexpected end of file has been encountered.</span></span>|  
|`BlobUnexpectedEnd`|<span data-ttu-id="8cb78-286">Blob beklenmeyen dosya sonuyla karşılaşıldı.</span><span class="sxs-lookup"><span data-stu-id="8cb78-286">An unexpected end of blob has been encountered.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="8cb78-287">Blob hizmeti isteği tooaccess sayfa aralığı hello hello veya blok başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-287">hello Blob service request tooaccess hello page range or block has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="8cb78-288">Bir disk veya ağ g/ç hatası hello sayfası aralık veya blok işlenirken hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-288">A disk or network I/O failure occurred while processing hello page range or block.</span></span>|  
|`Failed`|<span data-ttu-id="8cb78-289">Başlangıç sayfası aralık veya blok işlenirken bilinmeyen bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-289">An unknown failure occurred while processing hello page range or block.</span></span>|  
|`Cancelled`|<span data-ttu-id="8cb78-290">Önceki bir hata hello sayfası aralık veya blok işlenmesi durduruldu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-290">A prior failure has stopped further processing of hello page range or block.</span></span>|  
  
## <a name="metadata-status-codes"></a><span data-ttu-id="8cb78-291">Meta veriler durum kodları</span><span class="sxs-lookup"><span data-stu-id="8cb78-291">Metadata status codes</span></span>  
<span data-ttu-id="8cb78-292">Merhaba aşağıdaki tabloda işleme blob meta verileri için hello durum kodları listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="8cb78-292">hello following table lists hello status codes for processing blob metadata.</span></span>  
  
|<span data-ttu-id="8cb78-293">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="8cb78-293">Status code</span></span>|<span data-ttu-id="8cb78-294">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cb78-294">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="8cb78-295">Merhaba meta veri işleme hatasız bitirdi.</span><span class="sxs-lookup"><span data-stu-id="8cb78-295">hello metadata has finished processing without errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="8cb78-296">Merhaba meta veri dosyası adı geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8cb78-296">hello metadata file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="8cb78-297">Merhaba meta veri dosya adı çok uzun.</span><span class="sxs-lookup"><span data-stu-id="8cb78-297">hello metadata file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="8cb78-298">Merhaba meta veri dosyası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8cb78-298">hello metadata file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="8cb78-299">Erişim toohello meta veri dosyası reddedildi.</span><span class="sxs-lookup"><span data-stu-id="8cb78-299">Access toohello metadata file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="8cb78-300">Merhaba meta veri dosyası bozuk (Merhaba içerik karması eşleşmiyor).</span><span class="sxs-lookup"><span data-stu-id="8cb78-300">hello metadata file is corrupted (hello content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="8cb78-301">Merhaba meta veri içeriği toohello gerekli biçime uymuyor.</span><span class="sxs-lookup"><span data-stu-id="8cb78-301">hello metadata content does not conform toohello required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="8cb78-302">Yazma hello meta veri XML başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-302">Writing hello metadata XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="8cb78-303">meta veri tooaccess hello hello Blob hizmeti isteği başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-303">hello Blob service request tooaccess hello metadata has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="8cb78-304">Bir disk veya ağ g/ç hatası hello meta verileri işlenirken hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-304">A disk or network I/O failure occurred while processing hello metadata.</span></span>|  
|`Failed`|<span data-ttu-id="8cb78-305">Merhaba meta verileri işlenirken bilinmeyen bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-305">An unknown failure occurred while processing hello metadata.</span></span>|  
|`Cancelled`|<span data-ttu-id="8cb78-306">Önceki bir hata hello meta verilerinin işlenmesi durduruldu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-306">A prior failure has stopped further processing of hello metadata.</span></span>|  
  
## <a name="properties-status-codes"></a><span data-ttu-id="8cb78-307">Özellikler durum kodları</span><span class="sxs-lookup"><span data-stu-id="8cb78-307">Properties status codes</span></span>  
<span data-ttu-id="8cb78-308">Merhaba aşağıdaki tabloda blob özellikleri işlemeye hello durum kodlarını listeler.</span><span class="sxs-lookup"><span data-stu-id="8cb78-308">hello following table lists hello status codes for processing blob properties.</span></span>  
  
|<span data-ttu-id="8cb78-309">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="8cb78-309">Status code</span></span>|<span data-ttu-id="8cb78-310">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cb78-310">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="8cb78-311">Merhaba özellikleri işleme hatasız bitti.</span><span class="sxs-lookup"><span data-stu-id="8cb78-311">hello properties have finished processing without any errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="8cb78-312">Merhaba özellikleri dosya adı geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8cb78-312">hello properties file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="8cb78-313">Merhaba özellikleri dosya adı çok uzun.</span><span class="sxs-lookup"><span data-stu-id="8cb78-313">hello properties file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="8cb78-314">Merhaba özellikleri dosyası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8cb78-314">hello properties file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="8cb78-315">Toohello özellikleri dosyasına erişim engellendi.</span><span class="sxs-lookup"><span data-stu-id="8cb78-315">Access toohello properties file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="8cb78-316">Merhaba özellikleri dosya bozuk (Merhaba içerik karması eşleşmiyor).</span><span class="sxs-lookup"><span data-stu-id="8cb78-316">hello properties file is corrupted (hello content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="8cb78-317">Merhaba özellikleri içerik toohello gerekli biçime uymuyor.</span><span class="sxs-lookup"><span data-stu-id="8cb78-317">hello properties content does not conform toohello required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="8cb78-318">XML başarısız oldu hello özellikleri yazma.</span><span class="sxs-lookup"><span data-stu-id="8cb78-318">Writing hello properties XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="8cb78-319">Özellikler tooaccess hello hello Blob hizmeti isteği başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-319">hello Blob service request tooaccess hello properties has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="8cb78-320">Merhaba özellikleri işlenirken bir disk veya ağ g/ç hatası oluştu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-320">A disk or network I/O failure occurred while processing hello properties.</span></span>|  
|`Failed`|<span data-ttu-id="8cb78-321">Merhaba özellikleri işlenirken bilinmeyen bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-321">An unknown failure occurred while processing hello properties.</span></span>|  
|`Cancelled`|<span data-ttu-id="8cb78-322">Önceki bir hata hello özelliklerini işlenmesi durduruldu.</span><span class="sxs-lookup"><span data-stu-id="8cb78-322">A prior failure has stopped further processing of hello properties.</span></span>|  
  
## <a name="sample-logs"></a><span data-ttu-id="8cb78-323">Örnek günlükleri</span><span class="sxs-lookup"><span data-stu-id="8cb78-323">Sample logs</span></span>  
<span data-ttu-id="8cb78-324">Merhaba, ayrıntılı günlüğü örneği verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8cb78-324">hello following is an example of verbose log.</span></span>  
  
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
  
<span data-ttu-id="8cb78-325">Merhaba karşılık gelen hata günlüğü aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8cb78-325">hello corresponding error log is shown below.</span></span>  
  
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

 <span data-ttu-id="8cb78-326">Merhaba izleyin hata günlüğü içe aktarma işi için bir dosya hello alma sürücüde bulunamadı hakkında bir hata içerir.</span><span class="sxs-lookup"><span data-stu-id="8cb78-326">hello follow error log for an import job contains an error about a file not found on hello import drive.</span></span> <span data-ttu-id="8cb78-327">Sonraki bileşenleri Hello durumunu olduğuna dikkat edin `Cancelled`.</span><span class="sxs-lookup"><span data-stu-id="8cb78-327">Note that hello status of subsequent components is `Cancelled`.</span></span>  
  
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

<span data-ttu-id="8cb78-328">Merhaba bir dışa aktarma işi için aşağıdaki hata günlüğünü hello blob içeriğinin toohello sürücü yazıldı, ancak hello blob'un özellikleri dışarı aktarılırken bir hata oluştu gösterir.</span><span class="sxs-lookup"><span data-stu-id="8cb78-328">hello following error log for an export job indicates that hello blob content has been successfully written toohello drive, but that an error occurred while exporting hello blob's properties.</span></span>  
  
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
  
## <a name="next-steps"></a><span data-ttu-id="8cb78-329">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8cb78-329">Next steps</span></span>
 
* [<span data-ttu-id="8cb78-330">Depolama içeri/dışarı aktarma REST API'si</span><span class="sxs-lookup"><span data-stu-id="8cb78-330">Storage Import/Export REST API</span></span>](/rest/api/storageimportexport/)
