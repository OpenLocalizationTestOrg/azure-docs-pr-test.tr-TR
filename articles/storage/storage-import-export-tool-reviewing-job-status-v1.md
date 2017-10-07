---
title: "Azure içeri/dışarı aktarma iş durumu - v1 aaaReviewing | Microsoft Docs"
description: "Bilgi nasıl oluşturduğunuzda toouse hello veya günlük dosyaları hello alma işi verme toosee hello hello içeri/dışarı aktarma işinin durumunu çalıştırıldı."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: c69d1d69-6403-4eee-9949-0185faeecfa1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: muralikk
ms.openlocfilehash: 378bc9a7ef6bfe65209413c8c4134f313a2c0d79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a>Azure içeri/dışarı aktarma iş durumu kopyalama günlük dosyalarıyla gözden geçirme
Merhaba Microsoft Azure içeri/dışarı aktarma hizmeti bir içe veya dışa aktarma işi ile ilişkili sürücüleri işlediğinde, kendisinden, içeri aktarma veya BLOB'ları dışarı aktarma kopyalama günlük dosyaları toohello depolama hesabı tooor yazar. Merhaba günlük dosyası, dışarı veya içeri aktarılan her dosya hakkında ayrıntılı durumunu içerir. tamamlanmış iş hello durumunu sorguladığınızda hello URL tooeach kopyalama günlük dosyası döndürülür; bkz: [alma işi](/rest/api/storageservices/Get-Job3) daha fazla bilgi için.  

## <a name="example-urls"></a>Örnek URL'leri

Merhaba, örnek URL'ler için iki sürücü içeri aktarma işlemiyle kopyalama günlük dosyalarını şunlardır:  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 Bkz: [içeri/dışarı aktarma hizmeti günlük dosyası biçimi](storage-import-export-file-format-log.md) hello biçimi günlükleri ve durum kodları hello tam listesi için.  
  
## <a name="next-steps"></a>Sonraki adımlar
 
 * [Kurulum hello Azure içeri/dışarı aktarma aracı](storage-import-export-tool-setup-v1.md)   
 * [Sabit sürücüleri içeri aktarma işine hazırlama](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [Bir içeri aktarma işini onarma](storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [Bir dışarı aktarma işini onarma](storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [Sorun giderme hello Azure içeri/dışarı aktarma aracı](storage-import-export-tool-troubleshooting-v1.md)
