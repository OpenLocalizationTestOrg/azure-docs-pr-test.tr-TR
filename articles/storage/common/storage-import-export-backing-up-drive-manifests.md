---
title: "Azure içeri/dışarı aktarma sürücü bildirimlerini yedekleme | Microsoft Docs"
description: "Sürücü bildirimlerinizi otomatik olarak yedeklenen Microsoft Azure içeri/dışarı aktarma hizmeti için sahip öğrenin."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 594abd80-b834-4077-a474-d8a0f4b7928a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 33eb8e1eea8f8aa7b79ef3e54f2b1ed88dc794ae
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a><span data-ttu-id="9b690-103">Azure içeri/dışarı aktarma işleri sürücünün yedekleme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="9b690-103">Backing up drive manifests for Azure Import/Export jobs</span></span>

<span data-ttu-id="9b690-104">Sürücü bildirimleri otomatik olarak yedeklenebilir BLOB'larını ayarlayarak `BackupDriveManifest` özelliğine `true` içinde [Put işlemini](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) veya [güncelleştirme işi özellikleri](/rest/api/storageimportexport/jobs#Jobs_Update) REST API işlemleri.</span><span class="sxs-lookup"><span data-stu-id="9b690-104">Drive manifests can be automatically backed up to blobs by setting the `BackupDriveManifest` property to `true` in the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) REST API operations.</span></span> <span data-ttu-id="9b690-105">Varsayılan olarak, sürücü bildirimleri yedeklenmez.</span><span class="sxs-lookup"><span data-stu-id="9b690-105">By default, the drive manifests are not backed up.</span></span> <span data-ttu-id="9b690-106">Sürücü bildirim yedeklemeler, blok bloblar bir kapsayıcıda işle ilişkili depolama hesabı olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="9b690-106">The drive manifest backups are stored as block blobs in a container within the storage account associated with the job.</span></span> <span data-ttu-id="9b690-107">Varsayılan olarak, kapsayıcı addır `waimportexport`, ancak farklı bir ad belirtebilirsiniz `DiagnosticsPath` çağrılırken özelliği `Put Job` veya `Update Job Properties` işlemleri.</span><span class="sxs-lookup"><span data-stu-id="9b690-107">By default, the container name is `waimportexport`, but you can specify a different name in the `DiagnosticsPath` property when calling the `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="9b690-108">Yedekleme bildirim blob şu biçimde adlandırılır: `waies/jobname_driveid_timestamp_manifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="9b690-108">The backup manifest blob are named in the following format: `waies/jobname_driveid_timestamp_manifest.xml`.</span></span>

 <span data-ttu-id="9b690-109">Çağırarak işi için yedekleme sürücü bildirimleri URI'sini alabilir [alma işi](/rest/api/storageimportexport/jobs#Jobs_Get) işlemi.</span><span class="sxs-lookup"><span data-stu-id="9b690-109">You can retrieve the URI of the backup drive manifests for a job by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="9b690-110">URI döndürülür blob `ManifestUri` özelliği her bir sürücü için.</span><span class="sxs-lookup"><span data-stu-id="9b690-110">The blob URI is returned in the `ManifestUri` property for each drive.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b690-111">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9b690-111">Next steps</span></span>

* [<span data-ttu-id="9b690-112">İçeri/dışarı aktarma hizmeti REST API'si kullanma</span><span class="sxs-lookup"><span data-stu-id="9b690-112">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
