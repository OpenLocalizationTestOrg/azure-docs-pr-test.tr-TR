---
title: "Azure Active Directory'de özellik eşlemeleri için ifade aaaWriting | Microsoft Docs"
description: "Otomatik Azure Active Directory'de SaaS uygulama nesnelerinin sağlama sırasında toouse ifade eşlemeleri tootransform özniteliği kabul edilebilir bir biçime nasıl değerleri öğrenin."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: b13c51cd-1bea-4e5e-9791-5d951a518943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: markvi
ms.openlocfilehash: caa0dd8144f6e5279a869e015ed75bd24169d585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="writing-expressions-for-attribute-mappings-in-azure-active-directory"></a>Azure Active Directory'de özellik eşlemeleri için ifade yazma
Sağlama tooa SaaS uygulamasına yapılandırdığınızda belirtebilirsiniz öznitelik eşlemelerini hello tür bir ifade eşlemesi biridir. Bunlar için tootransform sağlayan bir komut dosyası benzeri ifadesi, kullanıcılarınızın veri Merhaba SaaS uygulaması için daha kabul edilebilir biçimlere yazmanız gerekir.

## <a name="syntax-overview"></a>Söz dizimi genel bakış
Hello için özellik eşlemeleri için ifade Applications (VBA) işlevleri için Visual Basic reminiscent söz dizimi.

* Hello tüm ifadesi parantez içinde bağımsız değişken adından sonra oluşur işlevleri bakımından tanımlanmış olması gerekir: <br>
  *FunctionName (<< bağımsız değişkeni 1 >>, <<argument N>>)*
* Birbirine içinde işlevleri iç içe. Örneğin: <br> *FunctionOne (FunctionTwo (<<argument1>>))*
* Bağımsız değişkenler üç farklı türde işlevlerini geçirebilirsiniz:
  
  1. Öznitelikleri kare köşeli parantez içine alınmalıdır. Örneğin: [attributeName]
  2. Dize sabitleri çift tırnak içine alınmalıdır. Örneğin: "ABD"
  3. Diğer işlevleri. Örneğin: FunctionOne (<<argument1>>, FunctionTwo (<<argument2>>))
* Bir ters eğik çizgi (\) ya da hello dizesinde tırnak işareti (") gerekiyorsa dize sabitleri için bunu hello ters eğik çizgi (\) simgesiyle kaçış uygulanmalıdır. Örneğin: "şirket adı: \"Contoso\""

## <a name="list-of-functions"></a>İşlevlerin listesi
[Append](#append) &nbsp; &nbsp; &nbsp; &nbsp; [FormatDateTime](#formatdatetime) &nbsp; &nbsp; &nbsp; &nbsp; [katılın](#join) &nbsp; &nbsp; &nbsp; &nbsp; [Mid](#mid) &nbsp; &nbsp; &nbsp; &nbsp; [değil](#not) &nbsp; &nbsp; &nbsp; &nbsp; [Değiştir](#replace) &nbsp; &nbsp; &nbsp; &nbsp; [StripSpaces](#stripspaces) &nbsp; &nbsp; &nbsp; &nbsp; [Anahtarı](#switch)

- - -
### <a name="append"></a>Ekle
**İşlev:**<br> Append(Source, Suffix)

**Açıklama:**<br> Bir kaynak dize değeri alır ve bunu hello soneki toohello son ekler.

**Parametreler:**<br> 

| Ad | Gerekli / yinelenen | Tür | Notlar |
| --- | --- | --- | --- |
| **Kaynak** |Gerekli |Dize |Genellikle hello kaynak nesneden hello özniteliğinin adı |
| **son eki** |Gerekli |Dize |hello dize tooappend toohello hello kaynak değerin sonuna istiyor. |

- - -
### <a name="formatdatetime"></a>FormatDateTime
**İşlev:**<br> FormatDateTime (kaynak, inputFormat, outputFormat)

**Açıklama:**<br> Bir tarih dizesi bir biçimden alır ve farklı bir biçime dönüştürür.

**Parametreler:**<br> 

| Ad | Gerekli / yinelenen | Tür | Notlar |
| --- | --- | --- | --- |
| **Kaynak** |Gerekli |Dize |Genellikle hello kaynak nesneden hello özniteliğinin adı. |
| **inputFormat** |Gerekli |Dize |Merhaba kaynak değer beklenen biçimi. Desteklenen biçimler için bkz: [http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx](http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx). |
| **outputFormat** |Gerekli |Dize |Merhaba çıkış tarihi biçimi. |

- - -
### <a name="join"></a>Birleştir
**İşlev:**<br> Birleştirme (ayırıcı kaynak1, kaynak2,...)

**Açıklama:**<br> Join() olduğunu benzer tooAppend() birden çok birleştirebilirsiniz dışında **kaynak** dize değerlerini tek bir dize halinde ve her bir değeri ile ayrılmış bir **ayırıcı** dize.

Merhaba kaynak değerlerden biri birden çok değerli özniteliği ise, bu öznitelik her değer birlikte birleştirilmiş, ayrılmış hello ayırıcı değer olacaktır.

**Parametreler:**<br> 

| Ad | Gerekli / yinelenen | Tür | Notlar |
| --- | --- | --- | --- |
| **ayırıcı** |Gerekli |Dize |Dize bir dizeye birleşir tooseparate kaynak değerler kullanılacaktır. Olabilir "" ayırıcı gerekiyorsa. |
| ** kaynak1... kaynakN ** |Gerekli, değişken-sayısı |Dize |Dize değerlerini toobe birlikte katıldı. |

- - -
### <a name="mid"></a>Orta
**İşlev:**<br> Mid (kaynak, başlangıç, uzunluk)

**Açıklama:**<br> Merhaba kaynak değerinin bir alt dizeyi döndürür. Bir alt dizesi yalnızca bazı hello kaynak dizesi hello karakterler içeren bir dizedir.

**Parametreler:**<br> 

| Ad | Gerekli / yinelenen | Tür | Notlar |
| --- | --- | --- | --- |
| **Kaynak** |Gerekli |Dize |Genellikle hello özniteliğinin adı. |
| **start** |Gerekli |tamsayı |Merhaba dizinde **kaynak** dize substring burada başlamalıdır. Merhaba dizedeki ilk karakter dizini 1 sahip olur, ikinci karakter dizin 2 sahip ve benzeri. |
| **uzunluğu** |Gerekli |tamsayı |Merhaba dizenin uzunluğu. Uzunluk dış hello ererse **kaynak** dize işlevi alt dizeyi döndürecektir **Başlat** dizin sonuna kadar **kaynak** dize. |

- - -
### <a name="not"></a>değil
**İşlev:**<br> Not(Source)

**Açıklama:**<br> Çevirir hello hello Boole değeri **kaynak**. Varsa **kaynak** değer "*True*", döndürür "*False*". Aksi takdirde, döndürür "*True*".

**Parametreler:**<br> 

| Ad | Gerekli / yinelenen | Tür | Notlar |
| --- | --- | --- | --- |
| **Kaynak** |Gerekli |Boole dizesi |Beklenen **kaynak** değerler: "True" veya "False"... |

- - -
### <a name="replace"></a>Değiştir
**İşlev:**<br> ObsoleteReplace (kaynak, oldValue, regexPattern, regexGroupName, replacementValue, replacementAttributeName, şablonu)

**Açıklama:**<br>
Bir dize içindeki değerleri değiştirir. Ayrıca sağlanan hello parametre bağlı olarak farklı şekilde çalışır:

* Zaman **oldValue** ve **replacementValue** sağlanır:
  
  * İle replacementValue oldValue hello kaynağındaki tüm oluşumlarını değiştirir
* Zaman **oldValue** ve **şablonu** sağlanır:
  
  * Merhaba tüm oluşumlarını değiştirir **oldValue** hello içinde **şablonu** hello ile **kaynak** değeri
* Zaman **oldValueRegexPattern**, **oldValueRegexGroupName**, **replacementValue** sağlanır:
  
  * OldValueRegexPattern hello kaynak dizesindeki replacementValue ile eşleşen tüm değerleri değiştirir
* Zaman **oldValueRegexPattern**, **oldValueRegexGroupName**, **replacementPropertyName** sağlanır:
  
  * Varsa **kaynak** değerine sahip **kaynak** döndürülür
  * Varsa **kaynak** değeri yok, kullanan **oldValueRegexPattern** ve **oldValueRegexGroupName** tooextract değiştirme değeri ile Merhaba özelliğinden  **replacementPropertyName**. Merhaba sonucu olarak değiştirme değeri döndürülür

**Parametreler:**<br> 

| Ad | Gerekli / yinelenen | Tür | Notlar |
| --- | --- | --- | --- |
| **Kaynak** |Gerekli |Dize |Genellikle hello kaynak nesneden hello özniteliğinin adı. |
| **oldValue** |İsteğe bağlı |Dize |Değer içinde değiştirilen toobe **kaynak** veya **şablon**. |
| **regexPattern** |İsteğe bağlı |Dize |Regex düzenidir içinde değiştirilen hello değer toobe için **kaynak**. Veya replacementPropertyName kullanıldığında, desen değiştirme özelliğinden tooextract değeri. |
| **regexGroupName** |İsteğe bağlı |Dize |İçinde hello grubunun adı **regexPattern**. Yalnızca replacementPropertyName kullanıldığında, biz bu grubun değerini değiştirme özelliğinden replacementValue olarak ayıklar. |
| **replacementValue** |İsteğe bağlı |Dize |İle yeni değer tooreplace eskisinin. |
| **replacementAttributeName** |İsteğe bağlı |Dize |Kaynak yok değerine sahip olduğunda değiştirme değeri için kullanılan hello özniteliği toobe adı. |
| **şablonu** |İsteğe bağlı |Dize |Zaman **şablonu** değeri sağlanır, biz görüneceğini **oldValue** içinde hello şablon ve kaynak değerle değiştirin. |

- - -
### <a name="stripspaces"></a>StripSpaces
**İşlev:**<br> StripSpaces(source)

**Açıklama:**<br> Tüm alanı kaldırır ("") hello karakterlerinden kaynak dizesi.

**Parametreler:**<br> 

| Ad | Gerekli / yinelenen | Tür | Notlar |
| --- | --- | --- | --- |
| **Kaynak** |Gerekli |Dize |**Kaynak** değeri tooupdate. |

- - -
### <a name="switch"></a>Anahtar
**İşlev:**<br> Anahtar (kaynak, defaultValue, key1, value1, key2, value2,...)

**Açıklama:**<br> Zaman **kaynak** değer eşleşen bir **anahtar**, döndürür **değeri** söz konusu **anahtar**. Varsa **kaynak** değeri döndürür tüm anahtarları eşleşmiyor **defaultValue**.  **Anahtar** ve **değeri** parametreleri çiftler halinde her zaman gelmesi gerekir. Merhaba işlevi her zaman çift sayıda parametre bekliyor.

**Parametreler:**<br> 

| Ad | Gerekli / yinelenen | Tür | Notlar |
| --- | --- | --- | --- |
| **Kaynak** |Gerekli |Dize |**Kaynak** değeri tooupdate. |
| **defaultValue** |İsteğe bağlı |Dize |Varsayılan değer toobe kaynak herhangi bir anahtarı eşleşmediğinde kullanılır. Boş bir dize olabilir (""). |
| **anahtarı** |Gerekli |Dize |**Anahtar** toocompare **kaynak** ile değer. |
| **değer** |Gerekli |Dize |Merhaba değiştirme değeri **kaynak** eşleşen hello anahtarı. |

## <a name="examples"></a>Örnekler
### <a name="strip-known-domain-name"></a>Şerit bilinen etki alanı adı
Bir kullanıcının e-posta tooobtain bir kullanıcı adı bilinen etki alanı adından toostrip gerekir. <br>
Örneğin, "contoso.com" Merhaba etki alanındaysa, ifade aşağıdaki hello kullanabilirsiniz:

**İfade:** <br>
`Replace([mail], "@contoso.com", , ,"", ,)`

**Giriş / Çıkış örneği:** <br>

* **Giriş** (posta): "john.doe@contoso.com"
* **Çıktı**: "john.doe"

### <a name="append-constant-suffix-toouser-name"></a>Sabit soneki toouser ad ekleme
Salesforce korumalı alan kullanıyorsanız, eşitlemeden önce kullanıcı adlarınız tooappend ek soneki tooall gerekebilir.

**İfade:** <br>
`Append([userPrincipalName], ".test"))`

**Giriş/Çıkış örneği:** <br>

* **Giriş**: (userPrincipalName): "John.Doe@contoso.com"
* **ÇIKTI**: "John.Doe@contoso.com.test"

### <a name="generate-user-alias-by-concatenating-parts-of-first-and-last-name"></a>Birleştirme bölümleri adı ve Soyadı tarafından kullanıcı diğer adı oluştur
Kullanıcının ilk adını, ilk 3 harf ve kullanıcının soyadını ilk 5 harfini gerçekleştirerek toogenerate bir kullanıcı diğer adı gerekir.

**İfade:** <br>
`Append(Mid([givenName], 1, 3), Mid([surname], 1, 5))`

**Giriş/Çıkış örneği:** <br>

* **Giriş** (givenName): "John"
* **Giriş** (Soyadı): "Doe"
* **Çıktı**: "JohDoe"

### <a name="output-date-as-a-string-in-a-certain-format"></a>Çıkış tarihi belirli biçiminde bir dize olarak
Belirli bir biçiminde toosend tarihleri tooa SaaS uygulaması istiyor. <br>
Örneğin, tooformat tarihler için ServiceNow isteyebilirsiniz.

**İfade:** <br>

`FormatDateTime([extensionAttribute1], "yyyyMMddHHmmss.fZ", "yyyy-MM-dd")`

**Giriş/Çıkış örneği:**

* **Giriş** (extensionAttribute1): "20150123105347.1Z"
* **ÇIKTI**: "2015-01-23"

### <a name="replace-a-value-based-on-predefined-set-of-options"></a>Önceden tanımlanmış seçenekleri kümesini temel alan bir değer değiştirin
Azure AD'de depolanan hello durum kodunu göre hello kullanıcı toodefine hello saat dilimini gerekir. <br>
Önceden tanımlanmış hello seçeneklerinden herhangi birini Hello durum kodunu eşleşmiyorsa, "Avustralya/Sidney" varsayılan değeri kullanın.

**İfade:** <br>

`Switch([state], "Australia/Sydney", "NSW", "Australia/Sydney","QLD", "Australia/Brisbane", "SA", "Australia/Adelaide")`

**Giriş/Çıkış örneği:**

* **Giriş** (durum): "QLD"
* **Çıktı**: "Avustralya/Brisbane"

## <a name="related-articles"></a>İlgili makaleler
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
* [Kullanıcı hazırlama/sağlama kaldırmayı tooSaaS uygulamaları otomatikleştirme](active-directory-saas-app-provisioning.md)
* [Kullanıcı sağlama öznitelik eşlemelerini özelleştirme](active-directory-saas-customizing-attribute-mappings.md)
* [Kapsam belirleme filtreleri kullanıcı sağlama](active-directory-saas-scoping-filters.md)
* [SCIM'yi tooenable otomatik kullanıcıların ve grupların Azure Active Directory tooapplications sağlama kullanma](active-directory-scim-provisioning.md)
* [Hesap sağlama bildirimleri](active-directory-saas-account-provisioning-notifications.md)
* [İlgili nasıl öğreticiler listesi tooIntegrate SaaS uygulamaları](active-directory-saas-tutorial-list.md)

