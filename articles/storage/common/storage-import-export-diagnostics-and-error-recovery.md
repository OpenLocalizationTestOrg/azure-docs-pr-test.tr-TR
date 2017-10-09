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
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a>Azure içeri/dışarı aktarma işleri için tanılama ve hata kurtarma
İşlenen her sürücü için hello Azure içeri/dışarı aktarma hizmeti ilişkili hello depolama hesabında bir hata günlüğü oluşturur. Ayrıntılı günlük kaydını ayarlama hello tarafından etkinleştirebilirsiniz `LogLevel` özelliği çok`Verbose` hello çağrılırken [Put işlemini](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) veya [güncelleştirme işi özellikleri](/rest/api/storageimportexport/jobs#Jobs_Update) işlemleri.

 Varsayılan olarak, günlükler adlı tooa kapsayıcı yazılır `waimportexport`. Ayarı hello tarafından farklı bir ad belirtebilirsiniz `DiagnosticsPath` hello çağrılırken özelliği `Put Job` veya `Update Job Properties` işlemleri. Merhaba günlükleri blok blobları adlandırma kuralı aşağıdaki hello ile depolanır: `waies/jobname_driveid_timestamp_logtype.xml`.

 Merhaba hello günlüklerinin bir iş için URI arama hello tarafından alabilir [alma işi](/rest/api/storageimportexport/jobs#Jobs_Get) işlemi. Merhaba URI hello ayrıntılı günlük hello döndürülen `VerboseLogUri` özelliği hello URI hello hata günlüğü hello döndürürken her sürücü için `ErrorLogUri` özelliği.

Sorunları aşağıdaki veri tooidentify hello günlüğü hello kullanabilirsiniz.

## <a name="drive-errors"></a>Sürücü hataları

Aşağıdaki öğelerindeki hello sürücüsü hataları sınıflandırılan:

-   Bildirim dosyası erişme veya hello okuma hataları

-   Yanlış BitLocker anahtarları

-   Okuma/yazma hataları sürücü

## <a name="blob-errors"></a>BLOB hataları

Aşağıdaki öğelerindeki hello blob hataları olarak sınıflandırılan:

-   Yanlış veya çakışan blob veya adları

-   Eksik dosyaları

-   Blob bulunamadı

-   Kesilmiş dosyaları (Merhaba diskteki hello dosyaları hello bildiriminde belirtilenden daha küçük)

-   Bozuk dosya içerik (için içeri aktarma işi ile bir MD5 sağlama toplamı eşleşmezliği algıladı)

-   Bozuk blob meta verileri ve özellik dosyaları (ile bir MD5 sağlama toplamı eşleşmezliği algıladı)

-   Yanlış şema hello blob özellikleri ve/veya meta veri dosyaları

Merhaba genel iş hala tamamlanırken burada içe veya dışa aktarma işinin bazı bölümleri başarıyla tamamlamayın durumlar olabilir. Bu durumda, karşıya yükleme veya ağ üzerinden hello veri parçalarını eksik hello indirin veya yeni bir iş tootransfer hello veri oluşturabilirsiniz. Merhaba bkz [Azure içeri/dışarı aktarma aracı başvurusu](storage-import-export-tool-how-to-v1.md) toolearn nasıl toorepair hello verileri ağ üzerinden.

## <a name="next-steps"></a>Sonraki adımlar

* [Merhaba içeri/dışarı aktarma hizmeti REST API'si kullanma](storage-import-export-using-the-rest-api.md)
