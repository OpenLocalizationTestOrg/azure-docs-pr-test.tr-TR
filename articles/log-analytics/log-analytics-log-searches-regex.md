---
title: "OMS günlük analizi aaaRegular ifadelerinde oturum aramaları | Microsoft Docs"
description: "Tooa normal ifade göre günlük analizi günlük aramaları toohello filtre hello sonuçlarında hello RegEx anahtar sözcüğünü kullanabilirsiniz.  Bu makalede bu ifadelerle çeşitli örnekler hello sözdizimi sağlar."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: bwren
ms.openlocfilehash: 3033593dac2c50e911fc69054947d40d4a74369b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-regular-expressions-toofilter-log-searches-in-log-analytics"></a>Normal ifadeler toofilter kullanarak günlük günlük analizi arar

[Oturum aramaları](log-analytics-log-searches.md) tooextract bilgilerin hello günlük analizi depodan izin.  [Filtre ifadelerini](log-analytics-search-reference.md#filter-expressions) toofilter hello toospecific ölçütleri göre hello arama sonuçlarını izin verin.  Merhaba **RegEx** anahtar sözcüğü toospecify Bu filtre için normal bir ifade sağlar.  

Bu makalede, günlük analizi tarafından kullanılan hello normal ifade sözdizimi hakkında ayrıntılar sağlar.

> [!NOTE]
> Bu gibi durumlarda, RegEx yalnızca aranabilir alanlara ile kullanabilirsiniz.  Aranabilir alanları hakkında daha fazla bilgi için bkz: **alan türleri** içinde [Bul günlük aramaları günlük analizi kullanarak verileri](log-analytics-log-searches.md#use-additional-filters).


## <a name="regex-keyword"></a>RegEx anahtar sözcüğü

Aşağıdaki sözdizimi toouse hello kullan hello **RegEx** günlük arama anahtar sözcük.  Kullanabileceğiniz diğer bölümleri Bu makale toodetermine hello sözdiziminde normal ifade hello kendisini hello.

    field:Regex("Regular Expression")
    field=Regex("Regular Expression")

Örneğin, bir tür ile toouse bir normal ifade tooreturn uyarı kaydeder *uyarı* veya *hata*, günlük arama aşağıdaki hello kullanırsınız.

    Type=Alert AlertSeverity=RegEx("Warning|Error")

## <a name="partial-matches"></a>Kısmi eşleşmeler
Merhaba normal ifade hello özelliğinin hello tüm metni eşleşmesi gerektiğini unutmayın.  Kısmi eşleşmeler herhangi bir kayıt döndürmez.  Örneğin, günlük arama aşağıdaki hello tooreturn kayıtları srv01.contoso.com adlı bir bilgisayardan çalışıyorsanız misiniz **değil** herhangi bir kayıt döndürür.

    Computer=RegEx("srv..")

Yalnızca ilk kısmı hello adı hello hello normal ifadeyle eşleşen olmasıdır.  Adın tamamını hello eşleştiğinden hello aşağıdaki iki günlük aramaları kayıtları bu bilgisayardan döndürecektir.

    Computer=RegEx("srv..@")
    Computer=RegEx("srv...contoso.com")

## <a name="characters"></a>Karakterleri
Farklı karakterlere belirtin.

| Karakter | Açıklama | Örnek | Örnek eşleşiyor |
|:--|:--|:--|:--|
| bir | Merhaba karakteri bir oluşumu. | Computer=Regex("Srv01.contoso.com") | Srv01.contoso.com |
| . | Herhangi bir tek karakteri. | Computer=Regex("Srv...contoso.com") | Srv01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |
| bir? | Sıfır veya bir oluşumu hello karakter. | Bilgisayar RegEx = ("srv01?. "contoso.com") | srv0.contoso.com<br>Srv01.contoso.com |
| bir * | Sıfır veya daha fazla karakterin yineleme sayısını hello. | Computer=Regex("Srv01*.contoso.com") | srv0.contoso.com<br>Srv01.contoso.com<br>srv011.contoso.com<br>srv0111.contoso.com |
| bir + | Bir veya daha fazla karakterin yineleme sayısını hello. | Computer=Regex("Srv01+.contoso.com") | Srv01.contoso.com<br>srv011.contoso.com<br>srv0111.contoso.com |
| [*abc*] | Herhangi bir tek karakteri hello köşeli eşleşmesi | Computer=Regex("srv0[123].contoso.com") | Srv01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |
| [*bir*-*z*] | Merhaba aralıktaki tek bir karakter eşleşmesi.  Birden çok aralık içerebilir. | Computer=Regex("srv0[1-3].contoso.com") | Srv01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |
| [^*abc*] | Merhaba karakter hello köşeli hiçbiri | Computer=Regex("srv0[^123].contoso.com") | srv05.contoso.com<br>SRV06.contoso.com<br>srv07.contoso.com |
| [^*bir*-*z*] | Merhaba aralığı hello karakter hiçbiri. | Computer=Regex("srv0[^1-3].contoso.com") | srv05.contoso.com<br>SRV06.contoso.com<br>srv07.contoso.com |
| [*n*-*m*] | Sayısal karakter aralığı eşleşir. | Computer=Regex("SRV[01-03].contoso.com") | Srv01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |
| @ | Bir karakter dizesi. | Bilgisayar RegEx = ("srv@.contoso.com") | Srv01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |


## <a name="multiple-occurences-of-character"></a>Birden çok örnek karakter
Belirli bir karakter birden çok tekrarı belirtin.

| Karakter | Açıklama | Örnek | Örnek eşleşiyor |
|:--|:--|:--|:--|
| {n} |  *n*karakterin yineleme sayısını hello. | Computer=Regex("BW-Win-sc01{3}.bwren.Lab") | BW win sc0111.bwren.lab |
| bir {n} |  *n*veya daha fazla karakterin yineleme sayısını hello. | Computer=Regex("BW-Win-sc01{3,}.bwren.Lab") | BW win sc0111.bwren.lab<br>BW win sc01111.bwren.lab<br>BW win sc011111.bwren.lab<br>BW win sc0111111.bwren.lab |
| {n, m} |  *n*çok*m* hello karakterin yineleme sayısını. | Computer=Regex("BW-Win-sc01{3,5}.bwren.Lab") | BW win sc0111.bwren.lab<br>BW win sc01111.bwren.lab<br>BW win sc011111.bwren.lab |


## <a name="logical-expressions"></a>Mantıksal ifadeler
Birden çok değerlerden birini seçin.

| Karakter | Açıklama | Örnek | Örnek eşleşiyor |
|:--|:--|:--|:--|
| &#124; | Mantıksal OR.  Sonuç döndürür üzerinde ya da ifadeyle eşleşir. | Tür uyarı AlertSeverity = RegEx = ("uyarısı &#124; "Error") | Uyarı<br>Hata |
| & | Mantıksal and  Sonuç döndürür eşleşme üzerinde hem ifadeleri | EventData regex = ("(güvenlik.\* &. \*başarılı. \*)") | Güvenlik denetimi başarılı |


## <a name="literals"></a>Değişmez değerler
Özel karakterleri tooliteral karakterleri dönüştürün.  Bu işlevler sağlayan tooregular ifadeler gibi karakterler içeren?-\*^\[\]{}\(\)+\|. &.

| Karakter | Açıklama | Örnek | Örnek eşleşiyor |
|:--|:--|:--|:--|
| \\ | Değişmez değer bir özel karakter tooa dönüştürür. | Status_CF =\\[Hata\\] @<br>Status_CF hata =\\-@ | [Hata] Dosyası bulunamadı.<br>Hata-dosya bulunamadı. |


## <a name="next-steps"></a>Sonraki Adımlar

* İle tanışın [oturum aramaları](log-analytics-log-searches.md) tooview hello günlük analizi deposundaki verileri ve analiz.
