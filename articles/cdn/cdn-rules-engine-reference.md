---
title: "aaaAzure CDN kurallar altyapısı başvurusu | Microsoft Docs"
description: "Azure CDN başvuru belgelerine altyapısı eşleşme koşulları ve özellikleri kuralları."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 4159715d15fc792afb49dcd2a30752fabcd94a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine"></a>Azure CDN kurallar altyapısı
Bu konu Azure içerik teslim ağı (CDN) için ayrıntılı açıklamaları hello kullanılabilir eşleşme koşulları ve özellikleri listelenmektedir [kurallar altyapısı](cdn-rules-engine.md).

Merhaba HTTP kurallar altyapısı tasarlanmış toobe hello son yetkilisi olan istekleri nasıl belirli türlerdeki hello CDN tarafından işlenir.

**Ortak kullanımlar**:

- Geçersiz kılma veya özel önbellek ilkesi tanımlayın.
- Güvenli veya hassas içerik isteklerini reddedin.
- Yeniden yönlendirme istekleri.
- Özel günlük verilerini depolar.

## <a name="terminology"></a>Terminoloji
Bir kural hello kullanımı tanımlanmıştır [ **koşullu ifadeler**](cdn-rules-engine-reference-conditional-expressions.md), [ **eşleşen**](cdn-rules-engine-reference-match-conditions.md), ve [  **Özellikler**](cdn-rules-engine-reference-features.md). Bu öğeler çizimde aşağıdaki hello vurgulanır.

 ![CDN eşleşme koşulu](./media/cdn-rules-engine-reference/cdn-rules-engine-terminology.png)

## <a name="syntax"></a>Sözdizimi

özel karakterleri kabul edilecek hello şekilde according toohow bir eşleşme koşul veya özellik tanıtıcıları metin değerleri değişir. Bir eşleşme koşul veya özellik yolları aşağıdaki hello birinde metin yorumlayabilir:

1. [**Değişmez değerler**](#literal-values) 
2. [**Joker karakter değerleri**](#wildcard-values)
3. [**Normal ifadeler**](#regular-expressions)

### <a name="literal-values"></a>Değişmez değerler
Değişmez değer yorumlanır metin hello % simgesinin hello durumla tüm özel karakterleri eşleşmesi gereken hello değerinin bir parçası kabul eder. Diğer bir deyişle, bir hazır değer eşleşen koşul çok Ayarla`\'*'\` değeri tam olduğunda yalnızca karşılanması (yani, `\'*'\`) bulunur.
 
Bir yüzde simge kullanılan tooindicate URL'dir kodlama (örn., `%20`).

### <a name="wildcard-values"></a>Joker karakter değerleri
Bir joker karakter değeri olarak yorumlanır metin ek anlam toospecial karakter atar. Aşağıdaki tablonun hello karakter kümesi aşağıdaki hello nasıl yorumlanacak açıklar.

Karakter | Açıklama
----------|------------
\ | Ters eğik çizgi hello karakterlerden herhangi birini bu tabloda belirtilen kullanılan tooescape ' dir. Ters eğik çizgi, kaçışlı doğrudan hello özel karakter önce belirtilmiş olması gerekir.<br/>Örneğin, bir yıldız işareti sözdizimi aşağıdaki hello çıkışları:`\*`
% | Bir yüzde simge kullanılan tooindicate URL'dir kodlama (örn., `%20`).
* | Bir yıldız işareti bir veya daha fazla karakter temsil eden bir joker karakterdir.
Alanı | Bir eşleşme koşul belirtilen hello birini tarafından karşılanması, bir boşluk karakteri gösteren değer veya desen.
'value' | Tek bir tırnakla özel bir anlamı yoktur. Ancak, tek tırnak kümesi kullanılan bir değer olmalıdır tooindicate bir hazır değer işlem görür. Aşağıdaki şekilde hello kullanılabilir:<br><br/>-Bu hello değeri eşleşen herhangi bir kısmının hello karşılaştırma değeri belirtilen her bir eşleşme koşulu toobe memnun sağlar.  Örneğin, `'ma'` dizeleri aşağıdaki hello hiçbiriyle: <br/><br/>/Business/**ma**rathon/asset.htm<br/>**ma**p.gif<br/>/ İş/şablonu. **ma**p<br /><br />-Bu harf karakter olarak belirtilen bir özel karakter toobe sağlar. Örneğin, bir dizi tek tırnak içinde bir boşluk karakteri kapsayan tarafından bir değişmez değer boşluk karakteri belirtmiş olabilir (yani, `' '` veya `'sample value'`).<br/>-Belirtilen bir boş değer toobe sağlar. Tek tırnak kümesi belirterek boş bir değer belirtin (yani, '').<br /><br/>**Önemli:**<br/>-Merhaba değer bir joker karakter içermemesi belirtilmişse, ardından bunu otomatik olarak bir hazır değer kabul edilir. Bu, gerekli toospecify tek tırnak kümesi olmadığını anlamına gelir.<br/>-Bir ters eğik çizgi bu tablodaki başka bir karakteri kaçış değil, ardından bunu bir dizi tek tırnak içinde belirtildiğinde yoksayılacak.<br/>-Başka bir şekilde toospecify bir özel karakter değişmez değer karakter olarak tooescape olan bir ters eğik çizgi kullanarak (yani, `\`).

### <a name="regular-expressions"></a>Normal ifadeler

Normal ifadeler bir metin değerini, içinde arama yapılacak bir desen tanımlayın. Normal ifade gösterimi belirli anlamları tooa çeşitli simgeler tanımlar. Merhaba aşağıdaki tabloda gösterir nasıl özel karakterler eşleşme koşullar ve normal ifadeler destek özellikleri tarafından kabul edilir.

Özel karakter | Açıklama
------------------|------------
\ | Bir ters eğik çizgi çıkışları hello karakter hello onu izler. Bu, normal ifade anlamlarını almak yerine bir hazır değer olarak kabul bu karakter toobe neden olur. Örneğin, bir yıldız işareti sözdizimi aşağıdaki hello çıkışları:`\*`
% | Merhaba anlamı yüzde simgesi üzerinde kullanım bağlıdır.<br/><br/> `%{HTTPVariable}`: Bu sözdizimi bir HTTP değişkeni tanımlar.<br/>`%{HTTPVariable%Pattern}`: Bu söz dizimini yüzde simgesi tooidentify değişken ve ayırıcı olarak bir HTTP kullanır.<br />`\%`: Bir yüzde simge kaçış sağlar, bir hazır değer veya tooindicate URL kodlaması olarak kullanılan toobe (örn., `\%20`).
* | Bir yıldız işareti karakteri toobe sıfır veya daha fazla kez eşleşen önceki hello sağlar. 
Alanı | Bir boşluk karakteri genellikle harf karakter olarak kabul edilir. 
'value' | Tek tırnak değişmez değer karakter olarak kabul edilir. Tek tırnak birtakım özel bir anlamı yok.


## <a name="next-steps"></a>Sonraki adımlar
* [Kurallar altyapısı eşleşme koşulları](cdn-rules-engine-reference-match-conditions.md)
* [Kurallar altyapısı koşullu ifadeler](cdn-rules-engine-reference-conditional-expressions.md)
* [Kurallar altyapısı özellikleri](cdn-rules-engine-reference-features.md)
* [Merhaba kurallar altyapısı kullanarak varsayılan HTTP davranışı geçersiz kılma](cdn-rules-engine.md)
* [Azure CDN'ye genel bakış](cdn-overview.md)
