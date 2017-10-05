---
title: "Azure arama Blob depolama alanına ekleme | Microsoft Docs"
description: "Azure Search HTTP REST API'sini kullanarak kod içinde bir dizin oluşturun."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
ms.service: search
ms.topic: article
ms.date: 05/04/2017
ms.author: ashmaka
ms.openlocfilehash: 0cd0cbb05c465d32a9ef02f9350ebdf9ccea36c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="searching-blob-storage-with-azure-search"></a>Azure Search ile Blob deposu arama

Azure Blob depolamada depolanan içerik türleri çeşitli genelinde arama çözmek için zor bir sorun olabilir. Ancak, dizin ve Azure Search kullanarak yalnızca birkaç tıklama ile Bloblarınızın içeriğini arayın. BLOB storage arama Azure Search Hizmeti sağlanması gerekir. Çeşitli hizmet sınırları ve Azure Search'ün fiyatlandırma katmanlarına bulunabilir [fiyatlandırma sayfası](https://aka.ms/azspricing).

## <a name="what-is-azure-search"></a>Azure Search nedir?
[Azure arama](https://aka.ms/whatisazsearch) güçlü tam metin arama deneyimleri web ve mobil uygulamalar eklemek geliştiriciler için kolaylaştıran bir arama çözümüdür. Hizmet olarak Azure arama sunumu sırasında herhangi bir arama altyapı yönetme ihtiyacını ortadan kaldırır. bir [% 99,9 çalışma süresi SLA](https://aka.ms/azuresearchsla).

Azure Search 56 diller için gelişmiş destek ile içeriğinizi çözümleyebilir ve dile özgü yapıları akıllıca ele. Azure Search zengin arama kullanıcı deneyimini oluşturmak için araçlar da sağlar. Modellenmiş bir gezinmede, typeahead arama önerileri gibi özellikleri eklemek ve isabet vurgulama Azure Search kullanarak kullanıcı arabirimleri basit bir işlemdir. Azure Search'ün özellikleri hakkında bilgi edinmek için hizmetin okuyabilirsiniz [belgelerine](https://aka.ms/azsearchdocs).

## <a name="crack-open-and-search-through-the-content-of-enterprise-document-formats"></a>Kırma açık ve kurumsal Belge biçimleri içeriğini arama
Desteğiyle [belge ayıklama](https://aka.ms/azsblobindexer) Azure Blob depolama alanına blob'larda depolanan dosya türleri, çeşitli içerik Azure Search dizin oluşturabilirsiniz:
- PDF
- Microsoft Office: DOCX/DOC, XLSX/XLS, PPTX/PPT, MSG (Outlook e-postalar)
- HTML
- Düz metin dosyaları

Metin ve bu dosya türlerini meta verilerini ayıklayarak türü ne olursa olsun en ilgili belgeleri bulmak için tek bir sorgu ile birden çok dosya biçimleri arasında arama kolaydır. İçerik ve Microsoft Office belgeleri, PDF ve e-postaları meta dizin tarafından Blob Depolama ve Azure Search kullanarak güçlü enterprise içerik yönetimi çözümü oluşturmak mümkündür.

## <a name="search-through-your-blob-metadata"></a>, Blob meta veri arama
Özel, kullanıcı tanımlı blob meta verileri ve bunun yanı sıra Sistem özellikleri her bloblarınızın için dizin için herhangi bir içerik türüne BLOB'lar sıralama kolaylaştırır yaygın bir senaryo değil. Bu şekilde, her blob bilgileri kolayca sıralayabilirsiniz şekilde blob ve model belgede türüne bakılmaksızın tüm Blob Depolama içeriğinizi dizine alınır.

[Meta veriler blob dizin oluşturma hakkında daha fazla bilgi edinin.](https://aka.ms/azsblobmetadataindexing)

## <a name="image-search"></a>Görüntü arama
Azure Search'ün tam metin araması, çok yönlü gezinme ve sıralama yeteneklerini görüntülerinin blob'larda depolanan meta veriler artık uygulanabilir.

Bu görüntüleri kullanarak önceden işlenirse [bilgisayar görme API](https://www.microsoft.com/cognitive-services/computer-vision-api) Microsoft'un Bilişsel hizmetlerinden sonra OCR ve el yazısı tanıma dahil olmak üzere her görüntüde bulunan görsel içerik dizin oluşturmak mümkündür. OCR eklemek için çalışıyoruz ve bu özelliklere ilgileniyorsanız diğer görüntü işleme özelliklerini doğrudan Azure arama için lütfen bir istek üzerinde göndermek bizim [UserVoice](https://aka.ms/azsuv) veya [bize e-posta](mailto:azscustquestions@microsoft.com).

## <a name="index-and-search-through-json-blobs"></a>Dizin ve JSON BLOB'ları ile arama
Azure arama, yapılandırılmış içerik JSON içeren BLOB'ları bulundu ayıklamak için yapılandırılabilir. Azure arama, JSON BLOB'ları okuyun ve bir Azure Search belge uygun alanlara yapılandırılmış içeriği ayrıştırılamıyor. Azure Search, her öğe ayrı bir Azure Search belgeye eşleyin ve bir dizi JSON nesnesi içeren BLOB'ları da alabilir.

JSON ayrıştırma Portalı aracılığıyla şu anda yapılandırılabilir değildir. [Azure Search'te JSON ayrıştırma hakkında daha fazla bilgi edinin.](https://aka.ms/azsjsonblobindexing)

## <a name="quick-start"></a>Hızlı başlangıç
Azure arama BLOB'larını doğrudan Blob Depolama portal dikey pencereden eklenebilir.

![](./media/search-blob-storage-integration/blob-blade.png)

"Azure arama Ekle" seçeneğini tıklatarak, var olan bir Azure Search hizmetini seçin veya yeni bir hizmet Oluştur bir akış başlatır. Yeni bir hizmet oluşturursanız, depolama hesabınızın portal deneyimi dışında yönlendirileceksiniz. Yeniden depolama portal dikey penceresine gidin ve varolan hizmet seçebileceğiniz "Azure arama Ekle" seçeneğini yeniden gerekecektir.

### <a name="next-steps"></a>Sonraki Adımlar
Tam Azure arama Blob oluşturucuda hakkında daha fazla bilgi [belgelerine](https://aka.ms/azsblobindexer).
