---
title: "aaaBacking Azure içeri/dışarı aktarma sürücü bildirimlerini ayarlama | Microsoft Docs"
description: "Nasıl toohave sürücünüze hello Microsoft Azure içeri/dışarı aktarma hizmeti için otomatik olarak yedeklenen bildirimlerini öğrenin."
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
ms.openlocfilehash: f48b97a2cce62714aace2b30a393305202c7ecd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a><span data-ttu-id="142c5-103">Azure içeri/dışarı aktarma işleri sürücünün yedekleme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="142c5-103">Backing up drive manifests for Azure Import/Export jobs</span></span>

<span data-ttu-id="142c5-104">Sürücü bildirimleri otomatik olarak yedeklenir tooblobs ayarı hello tarafından `BackupDriveManifest` özelliği çok`true` hello içinde [Put işlemini](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) veya [güncelleştirme işi özellikleri](/rest/api/storageimportexport/jobs#Jobs_Update) REST API işlemleri.</span><span class="sxs-lookup"><span data-stu-id="142c5-104">Drive manifests can be automatically backed up tooblobs by setting hello `BackupDriveManifest` property too`true` in hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) REST API operations.</span></span> <span data-ttu-id="142c5-105">Varsayılan olarak, hello sürücü bildirimleri yedeklenmez.</span><span class="sxs-lookup"><span data-stu-id="142c5-105">By default, hello drive manifests are not backed up.</span></span> <span data-ttu-id="142c5-106">Merhaba sürücü bildirim yedeklemeler, blok bloblar bir kapsayıcıda hello işle ilişkili hello depolama hesabı olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="142c5-106">hello drive manifest backups are stored as block blobs in a container within hello storage account associated with hello job.</span></span> <span data-ttu-id="142c5-107">Varsayılan olarak, hello kapsayıcı adı olan `waimportexport`, ancak hello farklı bir ad belirtebilirsiniz `DiagnosticsPath` hello çağrılırken özelliği `Put Job` veya `Update Job Properties` işlemleri.</span><span class="sxs-lookup"><span data-stu-id="142c5-107">By default, hello container name is `waimportexport`, but you can specify a different name in hello `DiagnosticsPath` property when calling hello `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="142c5-108">Merhaba yedekleme bildirim blob adlı biçimini izleyen hello: `waies/jobname_driveid_timestamp_manifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="142c5-108">hello backup manifest blob are named in hello following format: `waies/jobname_driveid_timestamp_manifest.xml`.</span></span>

 <span data-ttu-id="142c5-109">Merhaba yedekleme sürücü URI'sini bildirimleri için bir iş tarafından arama hello hello alabilir [alma işi](/rest/api/storageimportexport/jobs#Jobs_Get) işlemi.</span><span class="sxs-lookup"><span data-stu-id="142c5-109">You can retrieve hello URI of hello backup drive manifests for a job by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="142c5-110">Merhaba blob URI'si hello döndürülen `ManifestUri` özelliği her bir sürücü için.</span><span class="sxs-lookup"><span data-stu-id="142c5-110">hello blob URI is returned in hello `ManifestUri` property for each drive.</span></span>

## <a name="next-steps"></a><span data-ttu-id="142c5-111">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="142c5-111">Next steps</span></span>

* [<span data-ttu-id="142c5-112">Merhaba içeri/dışarı aktarma hizmeti REST API'si kullanma</span><span class="sxs-lookup"><span data-stu-id="142c5-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
