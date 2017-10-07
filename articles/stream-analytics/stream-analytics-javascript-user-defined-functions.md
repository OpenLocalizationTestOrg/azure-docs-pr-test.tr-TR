---
title: "aaaAzure Stream Analytics JavaScript kullanıcı tanımlı işlevler | Microsoft Docs"
description: "JavaScript kullanıcı tanımlı işlevler ile Gelişmiş sorgu mekanizması gerçekleştirmek"
keywords: "JavaScript, kullanıcı tanımlı işlevler, udf"
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 28eeb8f6437c23989e8887687b950361fed4414c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a>Azure Stream Analytics JavaScript kullanıcı tanımlı işlevler
Azure akış analizi, kullanıcı tanımlı işlevler JavaScript'te yazılmış destekler. Merhaba zengin kümesiyle **dize**, **RegExp**, **matematik**, **dizi**, ve **tarih** yöntemleri, JavaScript sağlar, karmaşık veri dönüşümleri akış analizi işleri ile daha kolay toocreate haline gelir.

## <a name="javascript-user-defined-functions"></a>JavaScript kullanıcı tanımlı işlevler
JavaScript kullanıcı tanımlı işlevler harici bağlantı gerektirmeyen durum bilgisiz, yalnızca işlem skaler işlevler destekler. Merhaba dönüş değeri işlevinin yalnızca bir skaler (tek) olabilir. Bir JavaScript kullanıcı tanımlı işlev tooa işi ekledikten sonra hello işlevi herhangi bir yere yerleşik bir skaler işlev gibi hello sorgu kullanabilirsiniz.

Burada JavaScript kullanıcı tanımlı işlevler kullanışlı bulabileceğiniz bazı senaryolar verilmiştir:
* Ayrıştırma ve normal ifade İşlevler, örneğin, sahip dizeleri düzenleme **Regexp_Replace()** ve **Regexp_Extract()**
* Kod çözme ve kodlama verileri, örneğin, ikili onaltılık dönüştürme
* JavaScript ile mathematic hesaplamalar gerçekleştirmek **matematik** işlevleri
* Sıralama, birleştirme, bulma ve dolgu gibi dizi işlemlerini gerçekleştirme

Stream Analytics içinde JavaScript kullanıcı tanımlı işlev ile yapamayacağınız bazı noktalar şunlardır:
* Duyurmak gerçekleştirme dış REST uç noktalar, örneğin, bir dış kaynaktan IP arama veya başvuru veri çekilmesini ters
* Özel olay biçimi serileştirme gerçekleştirmek veya giriş/çıkış üzerinde seri durumundan çıkarma
* Özel toplamaları oluşturun

Gibi çalışır ancak **Date.GetDate()** veya **Math.random()** engellenmediğinden hello işlevleri tanımında bunları yapmaktan kaçınmalısınız. Bu işlevler **sağlamadığı** dönüş hello aynı bunları arayın ve hello Azure Stream Analytics hizmeti, işlev çağrılarını günlüğü tutun değil her zaman ve neden sonuç döndürmedi. Bir işlev, farklı sonuç hello üzerinde aynı olayları döndürürse, sizin tarafınızdan veya hello Stream Analytics hizmeti tarafından bir iş yeniden başlatıldığında Yinelenebilirlik garanti edilmez.

## <a name="add-a-javascript-user-defined-function-in-hello-azure-portal"></a>Kullanıcı tanımlı bir JavaScript işlevi hello Azure portal Ekle
toocreate basit JavaScript kullanıcı tanımlı bir işlev var olan bir akış analizi işi altındaki adımları yapın:

1.  Hello Azure portal, Stream Analytics işi bulun.
2.  Altında **iş TOPOLOJİ**, işlevinizi seçin. İşlevler boş bir listesi görüntülenir.
3.  Yeni bir kullanıcı tanımlı işlev, toocreate seçin **Ekle**.
4.  Merhaba üzerinde **yeni işlev** dikey penceresinde için **işlev türü**seçin **JavaScript**. Varsayılan işlev şablonunun hello Düzenleyicisi'nde görüntülenir.
5.  Hello için **UDF diğer**, girin **hex2Int**ve hello işlevi uygulamasını aşağıdaki gibi değiştirin:

    ```
    // Convert Hex value toointeger.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  **Kaydet**’i seçin. İşlevinizi hello işlevleri listesinde görüntülenir.
7.  Select hello yeni **hex2Int** işlev ve hello işlevi tanımını denetleyin. Tüm İşlevler sahip bir **UDF** öneki eklenen toohello işlevi diğer adı. Çok ihtiyacınız*hello önekini ekleyin* Stream Analytics sorgunuzu hello işlevi çağırdığınızda. Bu durumda, çağrı **UDF.hex2Int**.

## <a name="call-a-javascript-user-defined-function-in-a-query"></a>Sorguda kullanıcı tanımlı bir JavaScript işlevi çağırma

1. Hello Düzenleyicisi altında sorgu **iş TOPOLOJİ**seçin **sorgu**.
2.  Sorgunuzu düzenleme ve hello kullanıcı tanımlı işlev, bu gibi çağırın:

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  tooupload hello örnek veri dosyası, sağ hello iş girişi.
4.  tootest sorgunuzu, select **Test**.


## <a name="supported-javascript-objects"></a>Desteklenen JavaScript nesneleri
Azure Stream Analytics JavaScript kullanıcı tanımlı işlevler, standart, yerleşik JavaScript nesneleri destekler. Bu nesnelerin bir listesi için bkz: [genel nesneler](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).

### <a name="stream-analytics-and-javascript-type-conversion"></a>Akış analizi ve JavaScript tür dönüştürmeleri

Merhaba Stream Analytics sorgu dilini ve JavaScript desteği hello türleri farklılıklar vardır. Bu tabloda hello iki arasındaki hello dönüştürme eşlemeleri listelenmektedir:

Akış Analizi | JavaScript
--- | ---
bigint | Sayı (JavaScript yalnızca tamsayı tooprecisely 2 Yukarı temsil eden ^ 53)
Tarih saat | Tarih (JavaScript yalnızca destekler milisaniye)
Çift | Sayı
nvarchar(max) | Dize
Kayıt | Nesne
Dizi | Dizi
NULL | Null


JavaScript Stream Analytics dönüşümleri şunlardır:


JavaScript | Akış Analizi
--- | ---
Sayı | Bigint (Merhaba numarası yuvarlak ve uzun arasında ise. MinValue ve uzun süre. MaxValue; Aksi takdirde, çift)
Tarih | Tarih saat
Dize | nvarchar(max)
Nesne | Kayıt
Dizi | Dizi
Null, tanımlanmamış | NULL
Herhangi bir türü (örneğin, bir işlev veya hata) | (Çalışma zamanı hatası sonuçlarında) desteklenmiyor

## <a name="troubleshooting"></a>Sorun giderme
JavaScript çalışma zamanı hataları önemli kabul edilir ve hello etkinlik günlüğü ortaya çıkmış. hello Azure portal, Git tooyour işi seçip tooretrieve hello günlük **etkinlik günlüğü**.


## <a name="other-javascript-user-defined-function-patterns"></a>Diğer JavaScript kullanıcı tanımlı işlev desenleri

### <a name="write-nested-json-toooutput"></a>İç içe geçmiş JSON toooutput yazma
Çıkış akış analizi işi giriş olarak kullanan bir izleme işleme adımı vardır ve bir JSON biçimi gerektiriyorsa, JSON dizesi toooutput yazabilirsiniz. Merhaba sonraki örneği çağırır hello **JSON.stringify()** hello tüm ad/değer çiftlerini giriş ve çıkış tek bir dize değer olarak yazma toopack işlev.

**JavaScript kullanıcı tanımlı işlev tanımı:**

```
function main(x) {
return JSON.stringify(x);
}
```

**Örnek Sorgu:**
```
SELECT
    DataString,
    DataValue,
    HexValue,
    UDF.json_stringify(input) As InputEvent
INTO
    output
FROM
    input PARTITION BY PARTITIONID
```

## <a name="get-help"></a>Yardım alın
Ek Yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics sorgu dili başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Yönetimi REST API Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)
