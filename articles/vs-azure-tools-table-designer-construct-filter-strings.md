---
title: "Filtre dizeleri için Tablo Tasarımcısı oluşturma | Microsoft Docs"
description: "Filtre dizeleri için Tablo Tasarımcısı oluşturma"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a1a10ea1-687a-4ee1-a952-6b24c2fe1a22
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 069224d84462b4955912ce1462a65298a5acc04a
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="constructing-filter-strings-for-the-table-designer"></a>Filtre dizeleri için Tablo Tasarımcısı oluşturma
## <a name="overview"></a>Genel Bakış
Visual Studio'da görüntülenen bir Azure tablosu filtre verilerde **Tablo Tasarımcısı**, bir filtre dizesi oluşturmak ve filtre alanına girin. Filtre dizesi sözdizimi WCF Veri Hizmetleri tarafından tanımlanır ve bir SQL WHERE yan tümcesine benzer, ancak tablo hizmeti bir HTTP isteği aracılığıyla gönderilir. **Tablo Tasarımcısı** uygun sizin için kodlama işler üzerinde istenen özellik değeri filtrelemek için yalnızca özellik adı, karşılaştırma işleci, ölçütleri değeri ve isteğe bağlı olarak, Boolean girmeniz filtre alanına işleci. $Filter sorgu seçeneği aracılığıyla tabloyu sorgulamak için bir URL oluşturma yaptığınız gibi dahil gerekmez [depolama hizmetleri REST API Başvurusu](http://go.microsoft.com/fwlink/p/?LinkId=400447).

WCF Veri Hizmetleri dayalı [açık veri Protokolü](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData). Filtre sistem sorgusu seçeneği hakkında ayrıntılı bilgi için (**$filter**), bkz: [OData URI kurallarını belirtimi](http://go.microsoft.com/fwlink/p/?LinkId=214806).

## <a name="comparison-operators"></a>Karşılaştırma İşleçleri
Aşağıdaki mantıksal işleçler tüm özellik türleri için desteklenir:

| Mantıksal işleci | Açıklama | Örnek filtre dizesi |
| --- | --- | --- |
| EQ |Eşittir |Şehir eq 'Redmond' |
| gt |Şu değerden fazla: |Fiyat gt 20 |
| Ge |Büyüktür veya eşittir |Fiyat ge 10 |
| lt |Şu değerden az: |Fiyat lt 20 |
| le |Küçüktür veya eşittir |Fiyat le 100 |
| ne |Eşit değildir |Şehir ne 'Londra' |
| ve |Ve |Fiyat le 200 ve fiyat gt 3.5 |
| or |Veya |Fiyat le 3.5 veya fiyat gt 200 |
| değil |değil |IsAvailable değil |

Aşağıdaki kuralları, bir filtre dizesi oluşturulurken önemlidir:

* Mantıksal işleçler bir özellik için bir değer karşılaştırmak için kullanın. Özelliği dinamik bir değere karşılaştırmak mümkün olmadığını göz önünde bulundurun; ifade bir tarafındaki bir sabit olmalıdır.
* Filtre dizesi tüm parçalarını büyük/küçük harfe duyarlıdır.
* Geçerli sonuçları döndürmek için aynı veri türünde filtre sırasını özelliği olarak sabit değeri olmalıdır. Desteklenen özellik türleri hakkında daha fazla bilgi için bkz: [tablo hizmeti veri modelini anlama](http://go.microsoft.com/fwlink/p/?LinkId=400448).

## <a name="filtering-on-string-properties"></a>Dize özellikleri filtreleme
Dize özellikleri filtre uygularken dize sabiti tek tırnak işaretleri içine alın.

Aşağıdaki örnek filtrelerle **PartitionKey** ve **RowKey** özellikleri; ek anahtar olmayan özellikler için filtre dizesini de eklenebiliyordu:

    PartitionKey eq 'Partition1' and RowKey eq '00001'

Gerekli olmamasına rağmen her filtre ifadesi parantez içine alın:

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

Tablo hizmeti joker sorguları desteklemez ve Tablo Tasarımcısı'nda ya da desteklenmez unutmayın. Ancak, önek eşleştirme istenen öneki Karşılaştırma işleçleri kullanarak gerçekleştirebilirsiniz. Aşağıdaki örnek varlıklar harf 'A' ile başlayan bir soyadı özelliği ile döndürür:

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a>Sayısal özellikleri filtreleme
Bir tamsayı veya kayan noktalı sayı filtrelemek için tırnak işaretleri olmadan belirtin.

Bu örnek değeri 30'dan büyük olan bir geçerlilik süresi özelliğine sahip tüm varlıkları döndürür:

    Age gt 30

Bu örnek, değeri 100.25 küçük veya buna eşit olan bir AmountDue özelliğine sahip tüm varlıkları döndürür:

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a>Boole özellikleri filtreleme
Bir Boole değeri filtrelemek için belirtin **true** veya **false** tırnak işaretleri olmadan.

Aşağıdaki örnek Isactive özelliğinin ayarlandığı tüm varlıkları döndürür **true**:

    IsActive eq true

Bu filtre ifadesi mantıksal işleç olmadan da yazabilirsiniz. Aşağıdaki örnekte, tablo hizmeti de tüm varlıklar Isactive olduğu döndürülecek **true**:

    IsActive

Isactive yanlış olduğu tüm varlıklar döndürmek için not kullanabilirsiniz işleci:

    not IsActive

## <a name="filtering-on-datetime-properties"></a>DateTime özellikleri üzerinde filtreleme
Bir tarih saat değerinde filtrelemek için belirtin **datetime** anahtar sözcüğü, tek tırnak işaretleri içindeki tarih sabiti arkasından. Tarih/saat sabit açıklandığı gibi birleşik UTC biçiminde olmalıdır [biçimlendirme DateTime özellik değerlerini](http://go.microsoft.com/fwlink/p/?LinkId=400449).

Aşağıdaki örnek, CustomerSince özelliği 10 Temmuz 2008'e eşit olduğu varlıklar döndürüyor:

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
