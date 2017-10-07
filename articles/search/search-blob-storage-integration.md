---
title: aaaAdding Azure Search tooBlob depolama | Microsoft Docs
description: "Hello Azure Search HTTP REST API'sini kullanarak kod içinde bir dizin oluşturun."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
ms.service: search
ms.topic: article
ms.date: 05/04/2017
ms.author: ashmaka
ms.openlocfilehash: a3801790067bf169693b500e83799286b7387a77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="searching-blob-storage-with-azure-search"></a>Azure Search ile Blob deposu arama

Merhaba çeşitli Azure Blob depolamada depolanan içerik türleri arasında arama zor sorun toosolve olabilir. Ancak, dizin arayın ve Azure Search kullanarak yalnızca birkaç tıklama içinde Bloblarınızın içeriğini hello. BLOB storage arama Azure Search Hizmeti sağlanması gerekir. Merhaba çeşitli hizmet sınırları ve fiyatlandırma katmanlarına Azure Search'ün üzerinde hello bulunabilir [fiyatlandırma sayfası](https://aka.ms/azspricing).

## <a name="what-is-azure-search"></a>Azure Search nedir?
[Azure arama](https://aka.ms/whatisazsearch) tooweb ve mobil uygulamalar geliştiriciler tooadd güçlü tam metin arama deneyimleri için kolaylaştıran bir arama çözümüdür. Hizmet olarak Azure arama hello gerek toomanage sunumu sırasında herhangi bir arama altyapı kaldırır bir [% 99,9 çalışma süresi SLA](https://aka.ms/azuresearchsla).

Azure Search 56 diller için gelişmiş destek ile içeriğinizi çözümleyebilir ve dile özgü yapıları akıllıca ele. Azure arama hello araçları toobuild zengin arama kullanıcı deneyimi de sağlar. Bu, çok yönlü gezinme, typeahead arama önerileri ve Azure Search kullanarak isabet vurgulama toouser arabirimleri gibi basit tooadd özellikleri gösterir. toolearn Azure Search'ün özellikleri hakkında hello hizmetin okuyabilir [belgelerine](https://aka.ms/azsearchdocs).

## <a name="crack-open-and-search-through-hello-content-of-enterprise-document-formats"></a>Kırma açık ve kurumsal Belge biçimleri Merhaba içeriğine arama
Desteğiyle [belge ayıklama](https://aka.ms/azsblobindexer) Azure Blob Depolama biriminde, çeşitli dosya türlerini blob'larda depolanan Merhaba içeriğine Azure Search dizin oluşturabilirsiniz:
- PDF
- Microsoft Office: DOCX/DOC, XLSX/XLS, PPTX/PPT, MSG (Outlook e-postalar)
- HTML
- Düz metin dosyaları

Metin ve bu dosya türlerini meta verilerini ayıklayarak kolay toosearch belgelerle bir tek sorgu toofind hello en uygun türü ne olursa olsun birden çok dosya biçimleri arasında olduğu. Blob Depolama ve Azure Search kullanan güçlü bir kurumsal içerik yönetim çözümü Hello içeriği ve hello meta verilerini Microsoft Office belgeleri, PDF ve e-postalar, kendi olası toobuild dizin.

## <a name="search-through-your-blob-metadata"></a>, Blob meta veri arama
Herhangi bir içerik türüne, BLOB'ları aracılığıyla kolay toosort kolaylaştırır yaygın bir senaryo tooindex Merhaba, kullanıcı tanımlı özel blob meta verileri gibi hello Sistem özellikleri her bloblarınızın için gereklidir. Bu şekilde, her blob bilgileri kolayca sıralayabilirsiniz şekilde hello blob ve model belgenin hello türü ne olursa olsun tüm Blob Depolama içeriğinizi dizine alınır.

[Meta veriler blob dizin oluşturma hakkında daha fazla bilgi edinin.](https://aka.ms/azsblobmetadataindexing)

## <a name="image-search"></a>Görüntü arama
Artık Azure Search'ün tam metin araması, çok yönlü gezinme ve yetenekleri sıralama blob'larda depolanan görüntülerinin uygulanan toohello meta verileri olabilir.

Bu görüntüleri hello kullanarak önceden işlenirse [bilgisayar görme API](https://www.microsoft.com/cognitive-services/computer-vision-api) Microsoft'un Bilişsel hizmetlerinden sonra onu OCR ve el yazısı tanıma dahil olmak üzere her görüntüde bulunan olası tooindex hello visual içeriktir. OCR ve diğer tooAzure arama, bu yetenekleri ilgileniyorsanız Lütfen gönderin üzerinde doğrudan bir istek işleme özellikleri resim eklemek için çalışıyoruz bizim [UserVoice](https://aka.ms/azsuv) veya [bize e-posta](mailto:azscustquestions@microsoft.com).

## <a name="index-and-search-through-json-blobs"></a>Dizin ve JSON BLOB'ları ile arama
Azure arama yapılandırılmış yapılandırılmış tooextract içerik JSON içeren BLOB'ları bulundu olabilir. Azure arama, JSON BLOB'ları okuma ve hello uygun bir Azure Search belge alanlarına yapılandırılmış hello içeriği ayrıştırılamıyor. Azure arama, ayrıca her öğe tooa ayrı Azure Search'te belge harita ve bir dizi JSON nesnesi içeren BLOB'ları alabilir.

JSON ayrıştırma hello Portalı aracılığıyla şu anda yapılandırılabilir değildir. [Azure Search'te JSON ayrıştırma hakkında daha fazla bilgi edinin.](https://aka.ms/azsjsonblobindexing)

## <a name="quick-start"></a>Hızlı başlangıç
Azure arama tooblobs doğrudan hello Blob Depolama portal dikey penceresinden eklenebilir.

![](./media/search-blob-storage-integration/blob-blade.png)

Merhaba üzerinde "Azure arama Ekle" seçeneğini tıklatarak, var olan bir Azure Search hizmetini seçin veya yeni bir hizmet Oluştur bir akış başlatır. Yeni bir hizmet oluşturursanız, depolama hesabınızın portal deneyimi dışında yönlendirileceksiniz. Toore gerekir-toohello depolama portal dikey gidin ve yeniden hello varolan hizmet seçebileceğiniz hello "Azure arama Ekle" seçeneğini seçin.

### <a name="next-steps"></a>Sonraki Adımlar
Merhaba tam olarak Azure arama Blob dizin oluşturucu hello hakkında daha fazla bilgi [belgelerine](https://aka.ms/azsblobindexer).
