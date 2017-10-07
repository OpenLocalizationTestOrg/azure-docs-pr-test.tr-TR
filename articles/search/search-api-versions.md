---
title: "Azure Search'ün aaaAPI sürümlerini | Microsoft Docs"
description: "Azure Search REST API'lerini ve hello istemci Kitaplığı'nda hello .NET SDK sürümü ilkesi."
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 0458053a-164e-4682-a802-00097ecde981
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 4fa722fad5577c6b254be7fa673eb240fff316a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="api-versions-in-azure-search"></a>Azure Search'te API sürümleri
Azure arama özellik güncelleştirmeleri düzenli olarak yapar. Bazen, ancak her zaman, bu güncelleştirmeleri bize toopublish bizim API toopreserve geriye dönük uyumluluk yeni bir sürümünü gerektirir. Yeni bir sürüm yayımlama toocontrol ne zaman ve nasıl kodunuzda arama hizmet güncelleştirmeleri tümleştirme sağlar.

Biraz çaba tooupgrade içerebileceği bir kural olarak, biz toopublish yeni sürümler yalnızca gerekli olduğunda, kod toouse yeni bir API sürümü deneyin. Geriye dönük uyumluluk keser şekilde hello API bazı yönlerinin toochange ihtiyacımız olmadığını biz yalnızca yeni bir sürümünü yayımlar. Bu düzeltmeler tooexisting özellikleri nedeniyle veya varolan API yüzey alanını değiştirme yeni özellikleri nedeniyle ortaya çıkabilir.

Biz aynı SDK güncelleştirmeleri kural hello izleyin. Hello Azure Search SDK izleyen hello [anlamsal sürüm oluşturma](http://semver.org/) sürümü üç kısma sahip olduğu anlamına gelir kuralları: birincil, ikincil ve yapı numarası (örneğin, 1.1.0). Biz hello SDK yalnızca geriye dönük uyumluluk bölün değişiklikler durumunda, yeni bir ana sürüm serbest bırakır. Bölünemez özellik güncelleştirmeleri biz hello alt sürüm artırır, ve hata düzeltmeleri için biz yalnızca hello yapı sürümünü artırır.

> [!NOTE]
> Azure Search Hizmeti örneğinizi hello en son dahil olmak üzere birkaç REST API sürümlerini destekler. En son Merhaba, ancak, kod toouse hello en yeni sürüme geçirmek öneririz artık olduğunda toouse bir sürüm devam edebilirsiniz. Merhaba REST API kullanırken, her istek hello api-version parametresi aracılığıyla hello API sürümü belirtmeniz gerekir. Merhaba .NET SDK kullanarak olduğunda hello hello kullanmakta olduğunuz SDK sürümü hello ilgili hello REST API sürümü belirler. Eski bir SDK kullanıyorsanız, hello hizmet yükseltilmiş toosupport daha yeni bir API sürümü olsa bile, hiçbir değişiklik kodla toorun devam edebilirsiniz.

## <a name="snapshot-of-current-versions"></a>Geçerli sürümlerinin anlık görüntüsü
Aşağıda tüm programlama arabirimleri tooAzure arama geçerli sürümleri hello anlık görüntüsüdür.

| Arabirimleri | Son ana sürümle | Durum |
| --- | --- | --- |
| [.NET SDK](https://aka.ms/search-sdk) |3.0 |Genellikle Kasım 2016 yayımlanan kullanılabilir |
| [.NET SDK Önizleme](https://aka.ms/search-sdk-preview) |2.0-Önizleme |Ağustos 2016 yayımlanan Önizleme |
| [Hizmet REST API'si](https://docs.microsoft.com/rest/api/searchservice/) |2016-09-01 |Genel olarak kullanılabilir |
| [Hizmet REST API Önizleme](search-api-2015-02-28-preview.md) |2015-02-28-Önizleme |Önizleme |
| [.NET Yönetim SDK'sı](https://aka.ms/search-mgmt-sdk) |2015-08-19 |Genel olarak kullanılabilir |
| [Yönetim REST API'si](https://docs.microsoft.com/rest/api/searchmanagement/) |2015-08-19 |Genel olarak kullanılabilir |

Merhaba hello dahil olmak üzere, REST API'leri için `api-version` her çağrıda gereklidir. Bu, kolay tootarget Önizleme API gibi belirli bir sürümü kolaylaştırır. Merhaba aşağıdaki örnekte gösterilmiştir nasıl hello `api-version` parametresi:

    GET https://adventure-works.search.windows.net/indexes/bikes?api-version=2016-09-01

> [!NOTE]
> Her istek olsa da bir `api-version`, hello kullanmanızı öneririz tüm API istekler için aynı sürüm. Bu, özellikle yeni API sürümleri öznitelikler veya önceki sürümleri tarafından tanınmıyor işlemler aldığımızda geçerlidir. API sürümü karıştırma olabilir istenmeyen sonuçlara ve kaçınılmalıdır.
>
> Merhaba hizmeti REST API'si ve Yönetimi REST API diğer bağımsız olarak sürümlü. Sürüm numaraları herhangi benzerlik içerik olarak farklı olur.

Genel olarak kullanılabilir (veya GA) API'leri üretimde kullanıldıkları ve hizmet düzeyi sözleşmelerine konu tooAzure. Önizleme sürümleri, her zaman geçirilen tooa GA sürümü olmayan Deneysel özellikleri vardır. **Önizleme API'leri üretim uygulamalarında kullanılmamasını öneriyoruz.**

## <a name="about-preview-and-generally-available-versions"></a>Önizleme ve genel olarak kullanılabilir sürümleri hakkında
Azure arama her zaman hello REST API aracılığıyla Deneysel özellikleri ilk olarak, ardından yayın öncesi sürümlerini hello .NET SDK önceden serbest bırakır.

Önizleme özellikleri toobe yıkıcıları tooa GA yayın geçişi. GA sürümündeki özellikler kararlı ve tahmin edilemez toochange küçük geriye dönük olarak uyumlu düzeltmeler ve geliştirmeler hello özel olarak kabul edilir gelirken, Önizleme özellikleri için test ve deneme, üzerinde geribildirim toplama hello amacı ile kullanılabilir özellik tasarım ve uygulama.

Ancak, Önizleme özellikleri konu toochange olduğundan, bir bağımlılık Önizleme sürümlerinde alır üretim kod yazmaya karşı öneririz. Eski bir önizleme sürümünü kullanıyorsanız, geçmenizi öneriyoruz toohello genel olarak kullanılabilir (GA) sürümü.

Merhaba .NET SDK'sı için: kod geçiş için yönergeler, adresinde bulunabilir [yükseltme hello .NET SDK'sı](search-dotnet-sdk-migration.md).

Genel kullanılabilirlik Azure Search şimdi hello hizmet düzeyi sözleşmesi altında (SLA) anlamına gelir. Merhaba SLA altında bulunabilir [Azure Search hizmet düzeyi sözleşmeleri](https://azure.microsoft.com/support/legal/sla/search/v1_0/).
