---
title: "Azure içeri/dışarı aktarma işleri için tanılama ve hata kurtarma | Microsoft Docs"
description: "Ayrıntılı Microsoft Azure içeri/dışarı aktarma hizmeti işleri için günlüğü etkinleştirmek öğrenin."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 096cc795-9af6-4335-9fe8-fffa9f239a17
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 0068aae9d6780aa41a070db0eb191d0d5a165d21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a><span data-ttu-id="57d16-103">Azure içeri/dışarı aktarma işleri için tanılama ve hata kurtarma</span><span class="sxs-lookup"><span data-stu-id="57d16-103">Diagnostics and error recovery for Azure Import/Export jobs</span></span>
<span data-ttu-id="57d16-104">İşlenen her sürücü için Azure içeri/dışarı aktarma hizmeti ilişkili depolama hesabında bir hata günlüğü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="57d16-104">For each drive processed, the Azure Import/Export service creates an error log in the associated storage account.</span></span> <span data-ttu-id="57d16-105">Ayarlayarak ayrıntılı günlük kaydını etkinleştirebilirsiniz `LogLevel` özelliğine `Verbose` çağrılırken [Put işlemini](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) veya [güncelleştirme işi özellikleri](/rest/api/storageimportexport/jobs#Jobs_Update) işlemleri.</span><span class="sxs-lookup"><span data-stu-id="57d16-105">You can also enable verbose logging by setting the `LogLevel` property to `Verbose` when calling the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operations.</span></span>

 <span data-ttu-id="57d16-106">Varsayılan olarak, günlükler adlı bir kapsayıcı yazılır `waimportexport`.</span><span class="sxs-lookup"><span data-stu-id="57d16-106">By default, logs are written to a container named `waimportexport`.</span></span> <span data-ttu-id="57d16-107">Farklı bir ad ayarlayarak belirtebilirsiniz `DiagnosticsPath` çağrılırken özelliği `Put Job` veya `Update Job Properties` işlemleri.</span><span class="sxs-lookup"><span data-stu-id="57d16-107">You can specify a different name by setting the `DiagnosticsPath` property when calling the `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="57d16-108">Günlükleri aşağıdaki adlandırma kuralıyla blok blobları olarak depolanır: `waies/jobname_driveid_timestamp_logtype.xml`.</span><span class="sxs-lookup"><span data-stu-id="57d16-108">The logs are stored as block blobs with the following naming convention: `waies/jobname_driveid_timestamp_logtype.xml`.</span></span>

 <span data-ttu-id="57d16-109">Bir işi için kayıtlar URI'sini çağırarak alabilir [alma işi](/rest/api/storageimportexport/jobs#Jobs_Get) işlemi.</span><span class="sxs-lookup"><span data-stu-id="57d16-109">You can retrieve the URI of the logs for a job by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="57d16-110">Ayrıntılı günlük URI'sini döndürülür `VerboseLogUri` özelliği, hata günlüğü için URI döndürürken her sürücü için `ErrorLogUri` özelliği.</span><span class="sxs-lookup"><span data-stu-id="57d16-110">The URI for the verbose log is returned in the `VerboseLogUri` property for each drive, while the URI for the error log is returned in the `ErrorLogUri` property.</span></span>

<span data-ttu-id="57d16-111">Günlük verilerini aşağıdaki sorunları belirlemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57d16-111">You can use the logging data to identify the following issues.</span></span>

## <a name="drive-errors"></a><span data-ttu-id="57d16-112">Sürücü hataları</span><span class="sxs-lookup"><span data-stu-id="57d16-112">Drive errors</span></span>

<span data-ttu-id="57d16-113">Aşağıdaki öğeler sürücüsü hataları sınıflandırılan:</span><span class="sxs-lookup"><span data-stu-id="57d16-113">The following items are classified as drive errors:</span></span>

-   <span data-ttu-id="57d16-114">Erişimi veya bildirim dosyasını okuma hataları</span><span class="sxs-lookup"><span data-stu-id="57d16-114">Errors in accessing or reading the manifest file</span></span>

-   <span data-ttu-id="57d16-115">Yanlış BitLocker anahtarları</span><span class="sxs-lookup"><span data-stu-id="57d16-115">Incorrect BitLocker keys</span></span>

-   <span data-ttu-id="57d16-116">Okuma/yazma hataları sürücü</span><span class="sxs-lookup"><span data-stu-id="57d16-116">Drive read/write errors</span></span>

## <a name="blob-errors"></a><span data-ttu-id="57d16-117">BLOB hataları</span><span class="sxs-lookup"><span data-stu-id="57d16-117">Blob errors</span></span>

<span data-ttu-id="57d16-118">Aşağıdaki öğeler blob hataları olarak sınıflandırılan:</span><span class="sxs-lookup"><span data-stu-id="57d16-118">The following items are classified as blob errors:</span></span>

-   <span data-ttu-id="57d16-119">Yanlış veya çakışan blob veya adları</span><span class="sxs-lookup"><span data-stu-id="57d16-119">Incorrect or conflicting blob or names</span></span>

-   <span data-ttu-id="57d16-120">Eksik dosyaları</span><span class="sxs-lookup"><span data-stu-id="57d16-120">Missing files</span></span>

-   <span data-ttu-id="57d16-121">Blob bulunamadı</span><span class="sxs-lookup"><span data-stu-id="57d16-121">Blob not found</span></span>

-   <span data-ttu-id="57d16-122">Kesilmiş dosyaları (diskteki dosyaları bildiriminde belirtilenden daha küçük)</span><span class="sxs-lookup"><span data-stu-id="57d16-122">Truncated files (the files on the disk are smaller than specified in the manifest)</span></span>

-   <span data-ttu-id="57d16-123">Bozuk dosya içerik (için içeri aktarma işi ile bir MD5 sağlama toplamı eşleşmezliği algıladı)</span><span class="sxs-lookup"><span data-stu-id="57d16-123">Corrupted file content (for import jobs, detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="57d16-124">Bozuk blob meta verileri ve özellik dosyaları (ile bir MD5 sağlama toplamı eşleşmezliği algıladı)</span><span class="sxs-lookup"><span data-stu-id="57d16-124">Corrupted blob metadata and property files (detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="57d16-125">Blob özellikleri ve/veya meta veri dosyaları için yanlış şeması</span><span class="sxs-lookup"><span data-stu-id="57d16-125">Incorrect schema for the blob properties and/or metadata files</span></span>

<span data-ttu-id="57d16-126">Genel İş hala tamamlanırken burada bazı bölümleri içe veya dışa aktarma işleminin başarıyla tamamlanması değil durumlar olabilir.</span><span class="sxs-lookup"><span data-stu-id="57d16-126">There may be cases where some parts of an import or export job do not complete successfully, while the overall job still completes.</span></span> <span data-ttu-id="57d16-127">Bu durumda, karşıya yükleme veya ağ üzerinden veri eksik parçalarını indirin veya verileri aktarmak için yeni bir proje oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57d16-127">In this case, you can either upload or download the missing pieces of the data over network, or you can create a new job to transfer the data.</span></span> <span data-ttu-id="57d16-128">Bkz: [Azure içeri/dışarı aktarma aracı başvurusu](storage-import-export-tool-how-to-v1.md) verileri ağ üzerinden onarmak hakkında bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="57d16-128">See the [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) to learn how to repair the data over network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57d16-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="57d16-129">Next steps</span></span>

* [<span data-ttu-id="57d16-130">İçeri/dışarı aktarma hizmeti REST API'si kullanma</span><span class="sxs-lookup"><span data-stu-id="57d16-130">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
