---
title: "aaaConstructing filtre dizeleri hello Tablo Tasarımcısı için | Microsoft Docs"
description: "Filtre dizeleri hello Tablo Tasarımcısı için oluşturma"
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
ms.openlocfilehash: 48b38d27b97936064daa875e41881d51546bc11f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="constructing-filter-strings-for-hello-table-designer"></a>Tablo Tasarımcısı hello için filtre dizeler oluşturma
## <a name="overview"></a>Genel Bakış
görüntülenen bir Azure tablosunda toofilter veri hello Visual Studio **Tablo Tasarımcısı**, bir filtre dizesi oluşturmak ve hello filtre alanına girin. Merhaba filtre dizesi sözdizimi hello WCF Veri Hizmetleri tarafından tanımlanır ve benzer tooa SQL WHERE yan tümcesi, ancak toohello tablo hizmeti bir HTTP isteği aracılığıyla gönderilir. Merhaba **Tablo Tasarımcısı** tanıtıcıları Merhaba, bunu toofilter istenen özellik değeri için uygun kodlama, hello özellik adı, karşılaştırma işleci ölçüt değeri yalnızca girmeniz gerekiyor ve isteğe bağlı olarak, hello Boole işleci filtre alan. Bir URL tooquery hello tablo hello aracılığıyla oluşturma yaptığınız gibi tooinclude hello $filter sorgu seçeneği gerekmez [depolama hizmetleri REST API Başvurusu](http://go.microsoft.com/fwlink/p/?LinkId=400447).

Merhaba WCF veri hizmetleri üzerinde hello dayalı [açık veri Protokolü](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData). Merhaba filtre sistem sorgusu seçeneği hakkında ayrıntılı bilgi için (**$filter**), hello bkz [OData URI kurallarını belirtimi](http://go.microsoft.com/fwlink/p/?LinkId=214806).

## <a name="comparison-operators"></a>Karşılaştırma İşleçleri
Merhaba aşağıdaki mantıksal işleçler tüm özellik türleri için desteklenir:

| Mantıksal işleci | Açıklama | Örnek filtre dizesi |
| --- | --- | --- |
| EQ |Eşittir |Şehir eq 'Redmond' |
| gt |Şu değerden fazla: |Fiyat gt 20 |
| Ge |Büyük veya ona eşit çok|Fiyat ge 10 |
| lt |Şu değerden az: |Fiyat lt 20 |
| le |Küçüktür veya eşittir |Fiyat le 100 |
| ne |Eşit değildir |Şehir ne 'Londra' |
| ve |Ve |Fiyat le 200 ve fiyat gt 3.5 |
| or |Veya |Fiyat le 3.5 veya fiyat gt 200 |
| değil |değil |IsAvailable değil |

Bir filtre dizesi oluşturulurken hello aşağıdaki kuralları önemlidir:

* Merhaba mantıksal işleçler toocompare özellik tooa değerini kullanın. Olası toocompare bir özellik tooa dinamik değeri olmadığını unutmayın; sütunlardan biri hello ifade bir sabit olmalıdır.
* Tüm parçalarını hello filtre dizesi büyük/küçük harfe duyarlıdır.
* Merhaba sabit değer hello olmalıdır aynı veri türü hello filtre tooreturn geçerli sonuçları düzenini hello özelliği olarak. Desteklenen özellik türleri hakkında daha fazla bilgi için bkz: [anlama hello tablo hizmeti veri modelini](http://go.microsoft.com/fwlink/p/?LinkId=400448).

## <a name="filtering-on-string-properties"></a>Dize özellikleri filtreleme
Dize özellikleri filtre uygularken hello dize sabiti tek tırnak işaretleri içine alın.

Örnek filtreleri hello üzerinde aşağıdaki hello **PartitionKey** ve **RowKey** özellikleri; ek anahtar olmayan özellikler toohello filtre dizesini de eklenebiliyordu:

    PartitionKey eq 'Partition1' and RowKey eq '00001'

Gerekli olmamasına rağmen her filtre ifadesi parantez içine alın:

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

Merhaba tablo hizmeti joker sorguları desteklemez ve hello Tablo Tasarımcısı da desteklenmez unutmayın. Ancak, önek eşleştirme hello istenen ön ekini temel Karşılaştırma işleçleri kullanarak gerçekleştirebilirsiniz. Merhaba aşağıdaki örnek varlıklar hello harf 'A' ile başlayan bir soyadı özelliği ile döndürür:

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a>Sayısal özellikleri filtreleme
bir tamsayı veya kayan noktalı sayı toofilter tırnak işaretleri olmadan hello numarasını belirtin.

Bu örnek değeri 30'dan büyük olan bir geçerlilik süresi özelliğine sahip tüm varlıkları döndürür:

    Age gt 30

Bu örnek, değeri olan bir AmountDue özelliğine sahip tüm varlıklar döndürüyor küçüktür veya too100.25 eşit:

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a>Boole özellikleri filtreleme
toofilter bir Boole değeri belirtin **true** veya **false** tırnak işaretleri olmadan.

Merhaba aşağıdaki örnekte tüm varlıklar hello Isactive özelliği çok ayarlandığı döndürür**true**:

    IsActive eq true

Bu filtre ifadesi hello mantıksal işleç olmadan da yazabilirsiniz. Aşağıdaki örneğine hello hello tablo hizmeti de tüm varlıklar Isactive olduğu döndürülecek **true**:

    IsActive

Isactive olduğu false, kullanabileceğiniz tüm varlıklar hello değil tooreturn işleci:

    not IsActive

## <a name="filtering-on-datetime-properties"></a>DateTime özellikleri üzerinde filtreleme
bir DateTime değeri toofilter belirtin hello **datetime** anahtar sözcüğü, tek tırnak işaretleri içindeki hello tarih sabiti arkasından. bölümünde açıklandığı gibi Hello tarih sabiti birleşik UTC biçiminde olmalıdır [biçimlendirme DateTime özellik değerlerini](http://go.microsoft.com/fwlink/p/?LinkId=400449).

Aşağıdaki örnek hello hello CustomerSince özelliği 2008 eşit tooJuly 10 olduğu varlıklar döndürüyor:

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
