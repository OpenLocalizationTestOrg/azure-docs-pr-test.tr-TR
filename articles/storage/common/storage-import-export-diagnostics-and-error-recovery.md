---
title: "Azure içeri/dışarı aktarma işleri için aaaDiagnostics ve hata kurtarma | Microsoft Docs"
description: "Bilgi nasıl tooenable ayrıntılı günlük kaydı için Microsoft Azure içeri/dışarı aktarma hizmeti işler."
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
ms.openlocfilehash: 48164279e7904c78fed802aa3cff66e589c3f12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a><span data-ttu-id="af0cb-103">Azure içeri/dışarı aktarma işleri için tanılama ve hata kurtarma</span><span class="sxs-lookup"><span data-stu-id="af0cb-103">Diagnostics and error recovery for Azure Import/Export jobs</span></span>
<span data-ttu-id="af0cb-104">İşlenen her sürücü için hello Azure içeri/dışarı aktarma hizmeti ilişkili hello depolama hesabında bir hata günlüğü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="af0cb-104">For each drive processed, hello Azure Import/Export service creates an error log in hello associated storage account.</span></span> <span data-ttu-id="af0cb-105">Ayrıntılı günlük kaydını ayarlama hello tarafından etkinleştirebilirsiniz `LogLevel` özelliği çok`Verbose` hello çağrılırken [Put işlemini](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) veya [güncelleştirme işi özellikleri](/rest/api/storageimportexport/jobs#Jobs_Update) işlemleri.</span><span class="sxs-lookup"><span data-stu-id="af0cb-105">You can also enable verbose logging by setting hello `LogLevel` property too`Verbose` when calling hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operations.</span></span>

 <span data-ttu-id="af0cb-106">Varsayılan olarak, günlükler adlı tooa kapsayıcı yazılır `waimportexport`.</span><span class="sxs-lookup"><span data-stu-id="af0cb-106">By default, logs are written tooa container named `waimportexport`.</span></span> <span data-ttu-id="af0cb-107">Ayarı hello tarafından farklı bir ad belirtebilirsiniz `DiagnosticsPath` hello çağrılırken özelliği `Put Job` veya `Update Job Properties` işlemleri.</span><span class="sxs-lookup"><span data-stu-id="af0cb-107">You can specify a different name by setting hello `DiagnosticsPath` property when calling hello `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="af0cb-108">Merhaba günlükleri blok blobları adlandırma kuralı aşağıdaki hello ile depolanır: `waies/jobname_driveid_timestamp_logtype.xml`.</span><span class="sxs-lookup"><span data-stu-id="af0cb-108">hello logs are stored as block blobs with hello following naming convention: `waies/jobname_driveid_timestamp_logtype.xml`.</span></span>

 <span data-ttu-id="af0cb-109">Merhaba hello günlüklerinin bir iş için URI arama hello tarafından alabilir [alma işi](/rest/api/storageimportexport/jobs#Jobs_Get) işlemi.</span><span class="sxs-lookup"><span data-stu-id="af0cb-109">You can retrieve hello URI of hello logs for a job by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="af0cb-110">Merhaba URI hello ayrıntılı günlük hello döndürülen `VerboseLogUri` özelliği hello URI hello hata günlüğü hello döndürürken her sürücü için `ErrorLogUri` özelliği.</span><span class="sxs-lookup"><span data-stu-id="af0cb-110">hello URI for hello verbose log is returned in hello `VerboseLogUri` property for each drive, while hello URI for hello error log is returned in hello `ErrorLogUri` property.</span></span>

<span data-ttu-id="af0cb-111">Sorunları aşağıdaki veri tooidentify hello günlüğü hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af0cb-111">You can use hello logging data tooidentify hello following issues.</span></span>

## <a name="drive-errors"></a><span data-ttu-id="af0cb-112">Sürücü hataları</span><span class="sxs-lookup"><span data-stu-id="af0cb-112">Drive errors</span></span>

<span data-ttu-id="af0cb-113">Aşağıdaki öğelerindeki hello sürücüsü hataları sınıflandırılan:</span><span class="sxs-lookup"><span data-stu-id="af0cb-113">hello following items are classified as drive errors:</span></span>

-   <span data-ttu-id="af0cb-114">Bildirim dosyası erişme veya hello okuma hataları</span><span class="sxs-lookup"><span data-stu-id="af0cb-114">Errors in accessing or reading hello manifest file</span></span>

-   <span data-ttu-id="af0cb-115">Yanlış BitLocker anahtarları</span><span class="sxs-lookup"><span data-stu-id="af0cb-115">Incorrect BitLocker keys</span></span>

-   <span data-ttu-id="af0cb-116">Okuma/yazma hataları sürücü</span><span class="sxs-lookup"><span data-stu-id="af0cb-116">Drive read/write errors</span></span>

## <a name="blob-errors"></a><span data-ttu-id="af0cb-117">BLOB hataları</span><span class="sxs-lookup"><span data-stu-id="af0cb-117">Blob errors</span></span>

<span data-ttu-id="af0cb-118">Aşağıdaki öğelerindeki hello blob hataları olarak sınıflandırılan:</span><span class="sxs-lookup"><span data-stu-id="af0cb-118">hello following items are classified as blob errors:</span></span>

-   <span data-ttu-id="af0cb-119">Yanlış veya çakışan blob veya adları</span><span class="sxs-lookup"><span data-stu-id="af0cb-119">Incorrect or conflicting blob or names</span></span>

-   <span data-ttu-id="af0cb-120">Eksik dosyaları</span><span class="sxs-lookup"><span data-stu-id="af0cb-120">Missing files</span></span>

-   <span data-ttu-id="af0cb-121">Blob bulunamadı</span><span class="sxs-lookup"><span data-stu-id="af0cb-121">Blob not found</span></span>

-   <span data-ttu-id="af0cb-122">Kesilmiş dosyaları (Merhaba diskteki hello dosyaları hello bildiriminde belirtilenden daha küçük)</span><span class="sxs-lookup"><span data-stu-id="af0cb-122">Truncated files (hello files on hello disk are smaller than specified in hello manifest)</span></span>

-   <span data-ttu-id="af0cb-123">Bozuk dosya içerik (için içeri aktarma işi ile bir MD5 sağlama toplamı eşleşmezliği algıladı)</span><span class="sxs-lookup"><span data-stu-id="af0cb-123">Corrupted file content (for import jobs, detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="af0cb-124">Bozuk blob meta verileri ve özellik dosyaları (ile bir MD5 sağlama toplamı eşleşmezliği algıladı)</span><span class="sxs-lookup"><span data-stu-id="af0cb-124">Corrupted blob metadata and property files (detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="af0cb-125">Yanlış şema hello blob özellikleri ve/veya meta veri dosyaları</span><span class="sxs-lookup"><span data-stu-id="af0cb-125">Incorrect schema for hello blob properties and/or metadata files</span></span>

<span data-ttu-id="af0cb-126">Merhaba genel iş hala tamamlanırken burada içe veya dışa aktarma işinin bazı bölümleri başarıyla tamamlamayın durumlar olabilir.</span><span class="sxs-lookup"><span data-stu-id="af0cb-126">There may be cases where some parts of an import or export job do not complete successfully, while hello overall job still completes.</span></span> <span data-ttu-id="af0cb-127">Bu durumda, karşıya yükleme veya ağ üzerinden hello veri parçalarını eksik hello indirin veya yeni bir iş tootransfer hello veri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af0cb-127">In this case, you can either upload or download hello missing pieces of hello data over network, or you can create a new job tootransfer hello data.</span></span> <span data-ttu-id="af0cb-128">Merhaba bkz [Azure içeri/dışarı aktarma aracı başvurusu](storage-import-export-tool-how-to-v1.md) toolearn nasıl toorepair hello verileri ağ üzerinden.</span><span class="sxs-lookup"><span data-stu-id="af0cb-128">See hello [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) toolearn how toorepair hello data over network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af0cb-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="af0cb-129">Next steps</span></span>

* [<span data-ttu-id="af0cb-130">Merhaba içeri/dışarı aktarma hizmeti REST API'si kullanma</span><span class="sxs-lookup"><span data-stu-id="af0cb-130">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
