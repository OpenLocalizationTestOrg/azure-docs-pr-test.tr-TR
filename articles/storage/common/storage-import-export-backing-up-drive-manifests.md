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
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a>Azure içeri/dışarı aktarma işleri sürücünün yedekleme bildirimleri

Sürücü bildirimleri otomatik olarak yedeklenir tooblobs ayarı hello tarafından `BackupDriveManifest` özelliği çok`true` hello içinde [Put işlemini](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) veya [güncelleştirme işi özellikleri](/rest/api/storageimportexport/jobs#Jobs_Update) REST API işlemleri. Varsayılan olarak, hello sürücü bildirimleri yedeklenmez. Merhaba sürücü bildirim yedeklemeler, blok bloblar bir kapsayıcıda hello işle ilişkili hello depolama hesabı olarak depolanır. Varsayılan olarak, hello kapsayıcı adı olan `waimportexport`, ancak hello farklı bir ad belirtebilirsiniz `DiagnosticsPath` hello çağrılırken özelliği `Put Job` veya `Update Job Properties` işlemleri. Merhaba yedekleme bildirim blob adlı biçimini izleyen hello: `waies/jobname_driveid_timestamp_manifest.xml`.

 Merhaba yedekleme sürücü URI'sini bildirimleri için bir iş tarafından arama hello hello alabilir [alma işi](/rest/api/storageimportexport/jobs#Jobs_Get) işlemi. Merhaba blob URI'si hello döndürülen `ManifestUri` özelliği her bir sürücü için.

## <a name="next-steps"></a>Sonraki adımlar

* [Merhaba içeri/dışarı aktarma hizmeti REST API'si kullanma](storage-import-export-using-the-rest-api.md)
