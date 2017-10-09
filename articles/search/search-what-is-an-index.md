---
title: "Azure Search dizini aaaCreate | Microsoft Azure | Barındırılan bulut arama hizmeti"
description: "Azure Search dizini nedir ve nasıl kullanılır?"
services: search
documentationcenter: 
author: ashmaka
ms.assetid: a395e166-bf2e-4fca-8bfc-116a46c5f7b1
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: c01cc654ff91427c8f1569b2f5b060a0a0f044c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index"></a>Bir Azure Search dizini oluşturma
> [!div class="op_single_selector"]
> * [Genel Bakış](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

## <a name="what-is-an-index"></a>Dizin nedir?
Bir *dizin*, Azure Search hizmeti tarafından kullanılan kalıcı bir *belge* ve diğer yapıların deposudur. Bir belge, dizininizdeki aranabilir verilerin tek bir birimidir. Örneğin, bir e-ticaret satıcısında sattığı her bir öğe için bir belge, bir haber kuruluşunda her bir makale için bir belge, vb. olabilir. Bu kavramları toomore bilinen veritabanı eşdeğerlerine eşleme: bir *dizin* kavramsal olarak benzer tooa olan *tablo*, ve *belgeleri* çok kabaca eşdeğerdir*satırları* bir tabloda.

Ne zaman, ekleme/belgeleri karşıya yükleme ve arama sorguları tooAzure arama, gönderme, istekleri tooa belirli dizininizi arama hizmetinizi gönderin.

## <a name="field-types-and-attributes-in-an-azure-search-index"></a>Bir Azure Search dizinindeki alan türleri ve öznitelikleri
Şemanızı tanımlarken, dizininizdeki hello adını, türünü ve her bir alan özniteliklerini belirtmeniz gerekir. Merhaba alan türü, bu alanda depolanan hello verileri sınıflandırır. Öznitelikleri üzerinde tek tek alanların toospecify hello alanın nasıl kullanıldığını ayarlanır. Merhaba aşağıdaki tablolarda hello türleri ve öznitelikleri numaralandırır.

### <a name="field-types"></a>Alan türleri
| Tür | Açıklama |
| --- | --- |
| *Edm.String* |Tam metin arama için isteğe bağlı olarak belirteç haline getirilebilen metin (sözcük bölünmesi, kök ayırma, vb.). |
| *Collection(Edm.String)* |Tam metin araması için isteğe bağlı olarak belirteç haline getirilebilen dize listesi. Bir koleksiyondaki öğelerin hello sayısına teorik bir üst sınır yoktur ancak yük boyutundaki 16 MB üst sınırı hello toocollections geçerlidir. |
| *Edm.Boolean* |True/false değerlerini içerir. |
| *Edm.Int32* |32 bit tamsayı değerleri. |
| *Edm.Int64* |64 bit tamsayı değerleri. |
| *Edm.Double* |Çift duyarlıklı sayısal veriler. |
| *Edm.DateTimeOffset* |Tarih saat değerlerini temsil hello OData V4 biçiminde (örneğin `yyyy-MM-ddTHH:mm:ss.fffZ` veya `yyyy-MM-ddTHH:mm:ss.fff[+/-]HH:mm`). |
| *Edm.GeographyPoint* |Merhaba dünya üzerindeki bir coğrafi konumu temsil eden bir nokta. |

Azure Search'ün [desteklediği veri türleri hakkında burada](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) daha ayrıntılı bilgiler edinebilirsiniz.

### <a name="field-attributes"></a>Alan öznitelikleri
| Öznitelik | Açıklama |
| --- | --- |
| *Anahtar* |Belge araması için kullanılan her bir belgenin hello benzersiz Kimliğini sağlayan bir dize. Tüm dizinlerin bir anahtarı olması gerekir. Yalnızca bir alan hello anahtar olabilir ve türünü tooEdm.String ayarlamanız gerekir. |
| *Alınabilir* |Bir arama sonucunda bir alanın döndürülüp döndürülemeyeceğini belirtir. |
| *Filtrelenebilir* |Filtre sorgularında kullanılan hello alan toobe sağlar. |
| *Sıralanabilir* |Bir sorgu, bu alanı kullanarak toosort arama sonuçları verir. |
| *Modellenebilir* |Kullanılan alan toobe sağlayan bir [modellenmiş bir gezinmede](search-faceted-navigation.md) kullanıcının bağımsız filtrelemesi için yapısı. Genellikle toogroup kullanabileceğiniz yinelemeli değerler içeren alanlar birden çok belge birlikte (bir tek bir marka veya hizmet kategorisine kalmıyor Örneğin, birden çok belge) model olarak en iyi çalışır. |
| *Aranabilir* |İşaretleri tam metin aranabilir alan hello. |

Azure Search'ün [dizin öznitelikleri hakkında burada](https://docs.microsoft.com/rest/api/searchservice/Create-Index) daha ayrıntılı bilgiler edinebilirsiniz.

## <a name="guidance-for-defining-an-index-schema"></a>Bir dizin şemasını tanımlama kılavuzu
Dizininizi tasarlarken, her bir kararı aracılığıyla aşaması toothink planlama hello içinde zaman ayırın. Bu, arama kullanıcı deneyiminizi ve iş gereksinimlerinizi göz önünde her bir alan hello atanması gerektiğinden, dizininizi tasarlarken tutmanız önemlidir [uygun öznitelikler](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Dağıtıldıktan sonra bir dizini yeniden oluşturma ve hello verileri yeniden yükleme değiştirilmesidir.

Veri depolama gereksinimleri zamanla değişiyorsa bölüm ekleyerek veya kaldırarak kapasiteyi artırabilir ya da azaltabilirsiniz. Ayrıntılı bilgi için bkz. [Azure'da Search hizmetinizi yönetme](search-manage.md) veya [Hizmet Sınırları](search-limits-quotas-capacity.md).

