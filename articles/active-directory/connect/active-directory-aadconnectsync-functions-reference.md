---
title: "Azure AD Connect eşitleme: işlevleri başvurusu | Microsoft Docs"
description: "Azure AD Connect eşitleme bildirim temelli hazırlama ifadelerini başvuru."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 4f525ca0-be0e-4a2e-8da1-09b6b567ed5f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: fbe0df856ca2efda965650fb85c7e831a0be32c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a>Azure AD Connect eşitleme: işlevleri başvurusu
Azure AD Connect eşitleme sırasında kullanılan toomanipulate bir öznitelik değeri işlevlerdir.  
Merhaba hello işlevlerin sözdizimi biçimini izleyen hello kullanarak ifade edilir:  
`<output type> FunctionName(<input type> <position name>, ..)`

İşlev aşırı yüklendi ve birden çok sözdizimleri kabul eder, tüm geçerli sözdizimi listelenir.  
Merhaba işlevleri kesin türü belirtilmiş ve geçirilen eşleşmeleri belgelenen hello tür hello türü doğrulayın.  
Merhaba türü eşleşmiyorsa, bir hata oluşturulur.

Merhaba türleri sözdizimi aşağıdaki hello ile ifade edilir:

* **Depo** – ikili
* **bool** – Boole
* **dt** – UTC tarihi/saati
* **Enum** – bilinen sabitleri numaralandırması
* **exp** – olan ifade tooevaluate tooa Boolean bekleniyor
* **mvbin** – birden çok değerli ikili
* **mvstr** – birden çok değerli dize
* **mvref** – birden çok değerli başvurusu
* **NUM** – sayısal
* **Ref** – başvurusu
* **str** – dize
* **var** – bir değişken (neredeyse) herhangi bir tür
* **void** – bir değer döndürmüyor

Merhaba işlevleri hello türleriyle **mvbin**, **mvstr**, ve **mvref** birden çok değerli öznitelikleri yalnızca çalışabilirsiniz. İle işlevleri **bin**, **str**, ve **ref** hem tek değerli ve birden çok değerli öznitelikleri üzerinde çalışır.

## <a name="functions-reference"></a>İşlevler Başvurusu
| İşlevlerin listesi |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| **Sertifika** | | | | |
| [CertExtensionOids](#certextensionoids) |[CertFormat](#certformat) |[CertFriendlyName](#certfriendlyname) |[CertHashString](#certhashstring) | |
| [CertIssuer](#certissuer) |[CertIssuerDN](#certissuerdn) |[CertIssuerOid](#certissueroid) |[CertKeyAlgorithm](#certkeyalgorithm) | |
| [CertKeyAlgorithmParams](#certkeyalgorithmparams) |[CertNameInfo](#certnameinfo) |[CertNotAfter](#certnotafter) |[CertNotBefore](#certnotbefore) | |
| [CertPublicKeyOid](#certpublickeyoid) |[CertPublicKeyParametersOid](#certpublickeyparametersoid) |[CertSerialNumber](#certserialnumber) |[CertSignatureAlgorithmOid](#certsignaturealgorithmoid) | |
| [CertSubject](#certsubject) |[CertSubjectNameDN](#certsubjectnamedn) |[CertSubjectNameOid](#certsubjectnameoid) |[Certthumbprınt](#certthumbprint) | |
[CertVersion](#certversion) |[IsCert](#iscert) | | | |
| **Dönüştürme** | | | | |
| [CBool](#cbool) |[CDate](#cdate) |[CGuid](#cguid) |[ConvertFromBase64](#convertfrombase64) | |
| [ConvertToBase64](#converttobase64) |[ConvertFromUTF8Hex](#convertfromutf8hex) |[ConvertToUTF8Hex](#converttoutf8hex) |[CNum](#cnum) | |
| [CRef](#cref) |[CStr](#cstr) |[StringFromGuid](#StringFromGuid) |[StringFromSid](#stringfromsid) | |
| **Tarih / saat** | | | | |
| [DateAdd](#dateadd) |[DateFromNum](#datefromnum) |[FormatDateTime](#formatdatetime) |[Şimdi](#now) | |
| [NumFromDate](#numfromdate) | | | | |
| **Dizin** | | | | |
| [DNComponent](#dncomponent) |[DNComponentRev](#dncomponentrev) |[EscapeDNComponent](#escapedncomponent) | | |
| **Değerlendirme** | | | | |
| [IsBitSet](#isbitset) |[IsDate](#isdate) |[IsEmpty](#isempty) |[IsGuid](#isguid) | |
| [IsNull](#isnull) |[IsNullOrEmpty](#isnullorempty) |[IsNumeric](#isnumeric) |[Olmasına](#ispresent) | |
| [IsString](#isstring) | | | | |
| **Matematik** | | | | |
| [BitAnd](#bitand) |[BitOr](#bitor) |[RandomNum](#randomnum) | | |
| **Birden çok değerli** | | | | |
| [İçerir](#contains) |[Sayısı](#count) |[Öğesi](#item) |[ItemOrNull](#itemornull) | |
| [Birleştir](#join) |[RemoveDuplicates](#removeduplicates) |[Böl](#split) | | |
| **Program akışı** | | | | |
| [Hata](#error) |[IIF](#iif) |[Seç](#select) |[Anahtar](#switch) | |
| [Burada](#where) |[İle](#with) | | | |
| **Metin** | | | | |
| [GUID](#guid) |[InStr](#instr) |[InStrRev](#instrrev) |[LCase](#lcase) | |
| [Sol](#left) |[Len](#len) |[LTrim](#ltrim) |[Orta](#mid) | |
| [PadLeft](#padleft) |[PadRight](#padright) |[PCase](#pcase) |[Değiştir](#replace) | |
| [ReplaceChars](#replacechars) |[Sağ](#right) |[RTrim](#rtrim) |[Kırpma](#trim) | |
| [UCase](#ucase) |[Word](#word) | | | |

- - -
### <a name="bitand"></a>BitAnd
**Açıklama:**  
Merhaba BitAnd işlevi belirtilen BITS üzerinde bir değer ayarlar.

**Sözdizimi:**  
`num BitAnd(num value1, num value2)`

* value1, value2: and değerini birlikte olmalıdır sayısal değerler

**Notlar:**  
Bu işlev, her iki parametre toohello ikili gösterimine dönüştürür ve biraz ayarlar:

* biri veya her ikisi içinde karşılık gelen bitler hello yoksa 0 - *maskesi* ve *bayrağı* 0
* 1 - hello karşılık gelen bit hem de 1 olması gerekir.

Diğer bir deyişle, her iki parametre karşılık gelen bitleri hello 1 olduğu durumlar dışında tüm durumlarda 0 döndürür.

**Örnek:**  
`BitAnd(&HF, &HF7)`  
Onaltılık "F" ve "F7" toothis değeri değerlendirmek için 7 döndürür.

- - -
### <a name="bitor"></a>BitOr
**Açıklama:**  
Merhaba BitOr işlevi belirtilen BITS üzerinde bir değer ayarlar.

**Sözdizimi:**  
`num BitOr(num value1, num value2)`

* value1, value2: or birlikte olmalıdır sayısal değerler

**Notlar:**  
Bu işlev, her iki parametre toohello ikili gösterimine dönüştürür ve hello karşılık gelen BITS her ikisi de 0 olduğunda birini veya her ikisini hello karşılık gelen bit maskesi ve bayrağı 1 ve too0 olması durumunda bir bit too1 ayarlar. Diğer bir deyişle, her iki parametre hello karşılık gelen bitleri 0 nerede dışında tüm durumlarda 1 döndürür.

- - -
### <a name="cbool"></a>CBool
**Açıklama:**  
Bir Boole değeri hesaplanan hello ifadesi temelinde Hello CBool işlevi döndürür

**Sözdizimi:**  
`bool CBool(exp Expression)`

**Notlar:**  
CBool True değerini döndürür sonra hello ifadeyi tooa sıfır olmayan bir değer, hesaplar varsa, aksi takdirde, False değerini döndürür.

**Örnek:**  
`CBool([attrib1] = [attrib2])`  

Hello aynı değeri true hem öznitelikleri döndürür.

- - -
### <a name="cdate"></a>CDate
**Açıklama:**  
Merhaba CDate işlevi bir dizeden bir UTC DateTime değeri döndürür. Tarih saat yerel öznitelik türü eşitlenmiş değil ancak bazı işlevler tarafından kullanılır.

**Sözdizimi:**  
`dt CDate(str value)`

* Değer: Bir dizeyi bir tarih, saat ve isteğe bağlı olarak saat dilimi

**Notlar:**  
Merhaba dize her zaman UTC olarak döndürülür.

**Örnek:**  
`CDate([employeeStartTime])`  
Merhaba çalışanın başlangıç zamanı temel alınarak bir DateTime döndürür

`CDate("2013-01-10 4:00 PM -8")`  
Döndürür DateTime temsil eden bir "2013-01-11 12: 00'da"








- - -
### <a name="certextensionoids"></a>CertExtensionOids
**Açıklama:**  
Bir sertifika nesnesinin tüm hello Kritik Uzantılar OID değerlerini döndürür hello.

**Sözdizimi:**  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi. Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.

- - -
### <a name="certformat"></a>CertFormat
**Açıklama:**  
Bu X.509v3 sertifikasını hello biçimi adını döndürür hello.

**Sözdizimi:**  
`str CertFormat(binary certificateRawData)`  
*   certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi. Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.

- - -
### <a name="certfriendlyname"></a>CertFriendlyName
**Açıklama:**  
Diğer adı için bir sertifika ilişkili hello döndürür.

**Sözdizimi:**  
`str CertFriendlyName(binary certificateRawData)`  
*   certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi. Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.

- - -
### <a name="certhashstring"></a>CertHashString
**Açıklama:**  
Döndürür hello X.509v3 sertifikasını SHA1 karma değeri bir onaltılık dize hello.

**Sözdizimi:**  
`str CertHashString(binary certificateRawData)`  
*   certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi. Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.

- - -
### <a name="certissuer"></a>CertIssuer
**Açıklama:**  
Döndürür hello X.509v3 sertifikasını veren hello sertifika yetkilisinin adı hello.

**Sözdizimi:**  
`str CertIssuer(binary certificateRawData)`  
*   certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi. Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.

- - -
### <a name="certissuerdn"></a>CertIssuerDN
**Açıklama:**  
Döndürür hello sertifikayı verenin ayırt edici adı hello.

**Sözdizimi:**  
`str CertIssuerDN(binary certificateRawData)`  
*   certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi. Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.

- - -
### <a name="certissueroid"></a>CertIssuerOid
**Açıklama:**  
Döndürür hello sertifika verenin OID hello.

**Sözdizimi:**  
`str CertIssuerOid(binary certificateRawData)`  
*   certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi. Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.

- - -
### <a name="certkeyalgorithm"></a>CertKeyAlgorithm
**Açıklama:**  
Merhaba anahtar algoritması bilgi bu X.509v3 sertifikasını için bir dize olarak döndürür.

**Sözdizimi:**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi. Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.

- - -
### <a name="certkeyalgorithmparams"></a>CertKeyAlgorithmParams
**Açıklama:**  
Merhaba anahtar algoritması parametreleri hello X.509v3 sertifikasını için bir onaltılık dize döndürür.

**Sözdizimi:**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi. Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.

- - -
### <a name="certnameinfo"></a>CertNameInfo
**Açıklama:**  
Merhaba konu ve sertifikayı veren adları bir sertifika verir.

**Sözdizimi:**  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi. Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.
*   X509NameType: hello hello konu X509NameType değeri.
*   includesIssuerName: true tooinclude hello verenin adı; Aksi takdirde false.

- - -
### <a name="certnotafter"></a>CertNotAfter
**Açıklama:**  
Yerel saatle sonra bir sertifika artık geçerli olduğu başlangıç tarihi döndürür.

**Sözdizimi:**  
`dt CertNotAfter(binary certificateRawData)`  
*   certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi. Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.

- - -
### <a name="certnotbefore"></a>CertNotBefore
**Açıklama:**  
Yerel saatte bir sertifikanın geçerli hale geldiği Hello tarihi döndürür.

**Sözdizimi:**  
`dt CertNotBefore(binary certificateRawData)`  
*   certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi. Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.

- - -
### <a name="certpublickeyoid"></a>CertPublicKeyOid
**Açıklama:**  
Döndürür hello X.509v3 sertifikası için ortak anahtar hello OID hello.

**Sözdizimi:**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi. Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.

- - -
### <a name="certpublickeyparametersoid"></a>CertPublicKeyParametersOid
**Açıklama:**  
Ortak anahtar parametrelerini hello X.509v3 sertifikasını hello OID döndürür hello.

**Sözdizimi:**  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi. Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.

- - -
### <a name="certserialnumber"></a>CertSerialNumber
**Açıklama:**  
Merhaba X.509v3 sertifikasını Hello seri numarasını döndürür.

**Sözdizimi:**  
`str CertSerialNumber(binary certificateRawData)`  
*   certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi. Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.

- - -
### <a name="certsignaturealgorithmoid"></a>CertSignatureAlgorithmOid
**Açıklama:**  
Döndürür hello hello algoritmasının OID toocreate hello bir sertifikanın imzasını kullanılır.

**Sözdizimi:**  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi. Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.

- - -
### <a name="certsubject"></a>CertSubject
**Açıklama:**  
Bir sertifikadan konu ayırt edici adı alır hello.

**Sözdizimi:**  
`str CertSubject(binary certificateRawData)`  
*   certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi. Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.

- - -
### <a name="certsubjectnamedn"></a>CertSubjectNameDN
**Açıklama:**  
Bir sertifikadan konu ayırt edici adı döndürür hello.

**Sözdizimi:**  
`str CertSubjectNameDN(binary certificateRawData)`  
*   certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi. Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.

- - -
### <a name="certsubjectnameoid"></a>CertSubjectNameOid
**Açıklama:**  
Bir sertifikadan konu adı hello OID döndürür hello.

**Sözdizimi:**  
`str CertSubjectNameOid(binary certificateRawData)`  
*   certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi. Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.

- - -
### <a name="certthumbprint"></a>Certthumbprınt
**Açıklama:**  
Bir sertifikanın parmak izini döndürür hello.

**Sözdizimi:**  
`str CertThumbprint(binary certificateRawData)`  
*   certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi. Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.

- - -
### <a name="certversion"></a>CertVersion
**Açıklama:**  
Bir sertifikanın X.509 biçimindeki sürümü döndürür hello.

**Sözdizimi:**  
`str CertThumbprint(binary certificateRawData)`  
*   certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi. Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.

- - -
### <a name="cguid"></a>CGuid
**Açıklama:**  
Merhaba CGuid işlevi bir GUID tooits ikili gösterim hello dize gösterimini dönüştürür.

**Sözdizimi:**  
`bin CGuid(str GUID)`

* Bu desen biçimlendirilmiş bir dize: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx veya {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}

- - -
### <a name="contains"></a>Contains
**Açıklama:**  
Merhaba içerir işlev bir dize birden çok değerli özniteliğinde bulur

**Sözdizimi:**  
`num Contains (mvstring attribute, str search)`-büyük küçük harfe duyarlı  
`num Contains (mvstring attribute, str search, enum Casetype)`  
`num Contains (mvref attribute, str search)`-büyük küçük harfe duyarlı

* Öznitelik: hello birden çok değerli özniteliği toosearch.
* Arama: hello özniteliğinde toofind dize.
* Casetype: CaseInsensitive veya CaseSensitive.

Dizin hello dize bulunduğu hello birden çok değerli özniteliği döndürür. Merhaba dize bulunamazsa, 0 döndürülür.

**Notlar:**  
Birden çok değerli dize öznitelikleri için hello arama alt dizeler hello değerleri bulur.  
Başvuru özniteliği için hello Aranan dize tam olarak bir eşleşme olarak kabul hello değeri toobe eşleşmelidir.

**Örnek:**  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
Bir birincil e-posta adresi Hello proxyAddresses özniteliğine sahipse, (büyük harf tarafından gösterilen "SMTP:"), hello proxyAddress özniteliği döndürür, aksi takdirde bir hata döndürür.

- - -
### <a name="convertfrombase64"></a>ConvertFromBase64
**Açıklama:**  
Merhaba ConvertFromBase64 işlevi dönüştürür hello base64 kodlu değer tooa normal dizesi belirtildi.

**Sözdizimi:**  
`str ConvertFromBase64(str source)`-Unicode kodlama için varsayar.  
`str ConvertFromBase64(str source, enum Encoding)`

* Kaynak: Base64 ile kodlanmış dize  
* Kodlaması: Unicode, ASCII, UTF8

**Örnek**  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

Örneklerin her ikisi de döndürmek "*Merhaba Dünya!*"

- - -
### <a name="convertfromutf8hex"></a>ConvertFromUTF8Hex
**Açıklama:**  
Merhaba ConvertFromUTF8Hex işlevi dönüştürür hello UTF8 olarak kodlanmış onaltılık değer tooa dizesi belirtildi.

**Sözdizimi:**  
`str ConvertFromUTF8Hex(str source)`

* Kaynak: UTF8 2-bayt kodlanmış dizesi

**Notlar:**  
Merhaba ile arasındaki fark bu işlevi ConvertFromBase64([],UTF8) hello sonucunda ortaya çıkan hello DN özniteliği için kolay.  
Bu biçim DN Azure Active Directory tarafından kullanılır.

**Örnek:**  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
Döndürür "*Merhaba Dünya!*"

- - -
### <a name="converttobase64"></a>ConvertToBase64
**Açıklama:**  
Merhaba ConvertToBase64 işlev bir dize tooa Unicode base64 dizesi dönüştürür.  
Base-64 basamak ile kodlanmış tamsayı tooits eşdeğer dize gösterimi dizisi Hello değerini dönüştürür.

**Sözdizimi:**  
`str ConvertToBase64(str source)`

**Örnek:**  
`ConvertToBase64("Hello world!")`  
"SABlAGwAbABvACAAdwBvAHIAbABkACEA" döndürür

- - -
### <a name="converttoutf8hex"></a>ConvertToUTF8Hex
**Açıklama:**  
Merhaba ConvertToUTF8Hex işlev bir dize tooa UTF8 olarak kodlanmış onaltılık değer dönüştürür.

**Sözdizimi:**  
`str ConvertToUTF8Hex(str source)`

**Notlar:**  
Bu işlevin Hello çıktı biçimi DN özniteliği biçimi olarak Azure Active Directory tarafından kullanılır.

**Örnek:**  
`ConvertToUTF8Hex("Hello world!")`  
Döndürür 48656C6C6F20776F726C6421

- - -
### <a name="count"></a>Sayı
**Açıklama:**  
Merhaba Count işlevi, birden çok değerli bir öznitelikte hello sayıda öğeyi döndürür

**Sözdizimi:**  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a>CNum
**Açıklama:**  
Merhaba CNum işlev bir dize alır ve sayısal veri türü döndürür.

**Sözdizimi:**  
`num CNum(str value)`

- - -
### <a name="cref"></a>CRef
**Açıklama:**  
Bir dize tooa başvuru özniteliği dönüştürür

**Sözdizimi:**  
`ref CRef(str value)`

**Örnek:**  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a>CStr
**Açıklama:**  
CStr işlevi Hello tooa dize veri türü dönüştürür.

**Sözdizimi:**  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* değer: bir sayısal değer, başvuru özniteliği ya da Boole değeri olabilir.

**Örnek:**  
`CStr([dn])`  
Döndürebilirsiniz "cn = Can, dc = contoso, dc = com"

- - -
### <a name="dateadd"></a>DateAdd
**Açıklama:**  
Belirli bir zaman aralığı eklenen tarih toowhich içeren bir tarih döndürür.

**Sözdizimi:**  
`dt DateAdd(str interval, num value, dt date)`

* aralığı: dize hello aralığı tooadd istediğiniz süreyi ifade. Merhaba dize değerlerini aşağıdaki hello birine sahip olmalıdır:
  * yyyy yıl
  * q üç aylık dönem
  * m ay
  * yılın y günü
  * d gün
  * w haftanın günü
  * ww hafta
  * h Saat
  * n dakika
  * s ikinci
* değer: Merhaba sayı ölçü tooadd istiyor. Pozitif olabilir (Merhaba gelecekteki tooget tarihleri) veya negatif (Merhaba son tarihleri tooget).
* Tarih: DateTime temsil eden tarih toowhich hello aralığı eklenir.

**Örnek:**  
`DateAdd("m", 3, CDate("2001-01-01"))`  
3 ay ekler ve "2001-04-01" temsil eden bir DateTime döndürür.

- - -
### <a name="datefromnum"></a>DateFromNum
**Açıklama:**  
Merhaba DateFromNum işlevi Reklamın tarih biçimi tooa DateTime türü bir değere dönüştürür.

**Sözdizimi:**  
`dt DateFromNum(num value)`

**Örnek:**  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
2012-01-01 temsil eden bir DateTime döndürür 23:00:00

- - -
### <a name="dncomponent"></a>DNComponent
**Açıklama:**  
Merhaba DNComponent işlevi soldan giderek belirtilen bir DN bileşen hello değerini döndürür.

**Sözdizimi:**  
`str DNComponent(ref dn, num ComponentNumber)`

* DN: hello başvuru özniteliği toointerpret
* ComponentNumber: Merhaba DN tooreturn hello bileşeni

**Örnek:**  
`DNComponent([dn],1)`  
DN ise "CN = Joe, ou = =..." Can döndürür

- - -
### <a name="dncomponentrev"></a>DNComponentRev
**Açıklama:**  
Merhaba DNComponentRev işlevi (Merhaba uç) sağdan giderek belirtilen bir DN bileşen hello değerini döndürür.

**Sözdizimi:**  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* DN: hello başvuru özniteliği toointerpret
* ComponentNumber - hello DN tooreturn hello bileşeni
* Seçenekler: DC – tüm bileşenleri Yoksay "dc ="

**Örnek:**  
DN ise "CN = Joe, ou = Atlanta, ou = GA, ou = = US, dc = contoso, dc = com" sonra  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
Her ikisi de BİZE döndür.

- - -
### <a name="error"></a>Hata
**Açıklama:**  
Merhaba hata işlevi kullanılan tooreturn özel bir hata var.

**Sözdizimi:**  
`void Error(str ErrorMessage)`

**Örnek:**  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
Merhaba özniteliği accountName mevcut değilse, bir hata hello nesnesinde atar.

- - -
### <a name="escapedncomponent"></a>EscapeDNComponent
**Açıklama:**  
Merhaba EscapeDNComponent işlevi bir DN biri bileşenini alır ve LDAP temsil edilebilir şekilde çıkışları.

**Sözdizimi:**  
`str EscapeDNComponent(str value)`

**Örnek:**  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
Merhaba displayName özniteliği LDAP'de kaçış karakterleri olsa bile, bir LDAP dizininde hello nesne oluşturulabilir emin olur.

- - -
### <a name="formatdatetime"></a>FormatDateTime
**Açıklama:**  
Hello FormatDateTime işlevi kullanılan tooformat DateTime tooa dizesi belirtilen biçime sahip değil

**Sözdizimi:**  
`str FormatDateTime(dt value, str format)`

* değer: hello tarih saat biçiminde bir değer
* Biçim: hello biçimi tooconvert temsil eden dize.

**Notlar:**  
Merhaba olası değerler hello biçimi burada bulunabilir: [kullanıcı tanımlı tarih/saat biçimleri (biçim işlevi)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)

**Örnek:**  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
"2007-12-25" sonuçlanır.

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
"İçinde 20140905081453.0Z" neden olabilir

- - -
### <a name="guid"></a>GUID
**Açıklama:**  
Yeni bir rastgele GUID Hello işlevi GUID oluşturur

**Sözdizimi:**  
`str GUID()`

- - -
### <a name="iif"></a>IIF
**Açıklama:**  
Merhaba IIF işlevi belirtilen bir koşula göre olası değerlerin kümesini döndürür.

**Sözdizimi:**  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* koşul: herhangi bir değer veya olabilir ifade hesaplanan tootrue ya da yanlış.
* Koşul: hello koşul tootrue değerlendirilirse hello değer döndürdü.
* valueIfFalse: hello koşul toofalse değerlendirilirse hello değer döndürdü.

**Örnek:**  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 Merhaba kullanıcı bir stajyer ise, bir kullanıcı ile "t-" Merhaba diğer adı olarak hello kullanıcının diğer adı, başka toohello başlangıcını döndürür eklenen döndürür.

- - -
### <a name="instr"></a>InStr
**Açıklama:**  
Merhaba InStr işlevi bir alt dizenin ilk örneğinin hello dizede bulur.

**Sözdizimi:**  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* stringcheck: arama toobe dize
* stringmatch: bulunan toobe dize
* Başlat: konum toofind hello substring başlatılıyor
* karşılaştırma: vbTextCompare veya vbBinaryCompare

**Notlar:**  
Merhaba substring bulunduğu döndürür hello konum veya 0 ise bulunamadı.

**Örnek:**  
`InStr("hello quick brown fox","quick")`  
Evalues too5

`InStr("repEated","e",3,vbBinaryCompare)`  
Too7 hesaplar

- - -
### <a name="instrrev"></a>InStrRev
**Açıklama:**  
Merhaba InStrRev işlevi dizesi içinde son a geçişi hello bir alt dizenin bulur

**Sözdizimi:**  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* stringcheck: arama toobe dize
* stringmatch: bulunan toobe dize
* Başlat: konum toofind hello substring başlatılıyor
* karşılaştırma: vbTextCompare veya vbBinaryCompare

**Notlar:**  
Merhaba substring bulunduğu döndürür hello konum veya 0 ise bulunamadı.

**Örnek:**  
`InStrRev("abbcdbbbef","bb")`  
7 döndürür

- - -
### <a name="isbitset"></a>IsBitSet
**Açıklama:**  
Merhaba işlevi IsBitSet veya bir bit ayarlanmışsa, testleri

**Sözdizimi:**  
`bool IsBitSet(num value, num flag)`

* değer: evaluated.flag bir sayısal değer: hello olan sayısal bir değer bit hesaplanan toobe

**Örnek:**  
`IsBitSet(&HF,4)`  
Bit "4" Merhaba on altılık değeri "F" olarak ayarlandığından True değerini döndürür

- - -
### <a name="isdate"></a>IsDate
**Açıklama:**  
Merhaba ifade olabiliyorsa tooTrue hello IsDate işlevi değerlendirir sonra bir DateTime türü değerlendirir.

**Sözdizimi:**  
`bool IsDate(var Expression)`

**Notlar:**  
CDate() başarılı olması durumunda toodetermine kullanılır.

- - -
### <a name="iscert"></a>IsCert
**Açıklama:**  
.NET X509Certificate2 sertifika nesnesine Hello ham verileri seri hale getirilebilir true değerini döndürür.

**Sözdizimi:**  
`bool CertThumbprint(binary certificateRawData)`  
*   certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi. Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.
- - -
### <a name="isempty"></a>IsEmpty
**Açıklama:**  
Merhaba özniteliği hello CS veya MV var, ancak tooan boş dize olarak değerlendirilir, hello IsEmpty işlevi tooTrue değerlendirir.

**Sözdizimi:**  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a>IsGuid
**Açıklama:**  
Merhaba dize dönüştürülmüş tooa GUID edilebiliyorsa Merhaba IsGuid işlevi tootrue değerlendirilir.

**Sözdizimi:**  
`bool IsGuid(str GUID)`

**Notlar:**  
Bir GUID bu desenleri birini izleyen bir dize olarak tanımlanır: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx veya {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}

CGuid() başarılı olması durumunda toodetermine kullanılır.

**Örnek:**  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
Merhaba StrAttribute GUID biçimine varsa, bir ikili biçimi döndürür, aksi takdirde null değeri döndürür.

- - -
### <a name="isnull"></a>IsNull
**Açıklama:**  
TooNull Hello ifadeyi hesaplar, hello IsNull işlevi true döndürür.

**Sözdizimi:**  
`bool IsNull(var Expression)`

**Notlar:**  
Bir öznitelik için bir Null hello özniteliği hello yokluğu tarafından ifade edilir.

**Örnek:**  
`IsNull([displayName])`  
Merhaba özniteliği hello CS veya MV mevcut değilse True değerini döndürür.

- - -
### <a name="isnullorempty"></a>IsNullOrEmpty
**Açıklama:**  
Hello ifade null veya boş bir dize ise, hello IsNullOrEmpty işlevi true döndürür.

**Sözdizimi:**  
`bool IsNullOrEmpty(var Expression)`

**Notlar:**  
Hello özniteliği yok veya var ancak boş bir dize için bir öznitelik, bu tooTrue değerlendirmek.  
Bu işlev Hello tersini olmasına adlandırılır.

**Örnek:**  
`IsNullOrEmpty([displayName])`  
Merhaba özniteliği mevcut değil ya da boş bir dize hello CS veya MV varsa True değerini döndürür.

- - -
### <a name="isnumeric"></a>IsNumeric
**Açıklama:**  
Merhaba IsNumeric işlevi bir ifadenin sayı türü değerlendirilebilir olup olmadığını gösteren bir Boole değeri döndürür.

**Sözdizimi:**  
`bool IsNumeric(var Expression)`

**Notlar:**  
CNum() başarılı tooparse hello ifade olabiliyorsa toodetermine kullanılır.

- - -
### <a name="isstring"></a>IsString
**Açıklama:**  
Merhaba ifade yapabiliyorsanız olması değerlendirilen tooa dize türünde, tooTrue hello IsString işlevi değerlendirir sonra.

**Sözdizimi:**  
`bool IsString(var expression)`

**Notlar:**  
CStr() başarılı tooparse hello ifade olabiliyorsa toodetermine kullanılır.

- - -
### <a name="ispresent"></a>Olmasına
**Açıklama:**  
Null olmayan ve boş değil tooa dize Hello ifadeyi hesaplar, işlevi true değerini döndürür olmasına hello.

**Sözdizimi:**  
`bool IsPresent(var expression)`

**Notlar:**  
Bu işlev Hello tersini IsNullOrEmpty olarak adlandırılır.

**Örnek:**  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a>Öğe
**Açıklama:**  
Merhaba öğesi işlevi, birden çok değerli bir dize/özniteliğinden bir öğeyi döndürür.

**Sözdizimi:**  
`var Item(mvstr attribute, num index)`

* Öznitelik: birden çok değerli özniteliği
* Dizin: dizin tooan öğesinde hello birden çok değerli dize.

**Notlar:**  
Merhaba ikinci işlevi hello birden çok değerli özniteliğinde hello dizin tooan öğesi döndürdüğünden hello öğesi işlevi içerir işlevi hello birlikte yararlıdır.

Dizin sınırların dışında olması durumunda bir hata oluşturur.

**Örnek:**  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
Birincil e-posta adresi döndürür hello.

- - -
### <a name="itemornull"></a>ItemOrNull
**Açıklama:**  
Merhaba ItemOrNull işlevi, birden çok değerli bir dize/özniteliğinden bir öğeyi döndürür.

**Sözdizimi:**  
`var ItemOrNull(mvstr attribute, num index)`

* Öznitelik: birden çok değerli özniteliği
* Dizin: dizin tooan öğesinde hello birden çok değerli dize.

**Notlar:**  
Merhaba ikinci işlevi hello birden çok değerli özniteliğinde hello dizin tooan öğesi döndürdüğünden hello ItemOrNull işlevi içerir işlevi hello birlikte yararlıdır.

Dizin sınırların dışında ise, bir Null değeri döndürür.

- - -
### <a name="join"></a>Birleştir
**Açıklama:**  
Merhaba birleştirme işlevi birden çok değerli bir dize alır ve her bir öğe eklenen belirtilen ayırıcı ile tek değerli bir dize döndürür.

**Sözdizimi:**  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* Öznitelik: birden çok değerli özniteliği içeren dizeleri birleştirilmiş toobe.
* sınırlayıcı: herhangi bir dize, dize döndürdü hello içinde kullanılan tooseparate hello alt dizeler. Atlanırsa, boşluk karakteri hello ("") kullanılır. Sınırlayıcı sıfır uzunlukta bir dize ise ("") veya hiçbir şey hello listedeki tüm öğelerin hiçbir sınırlayıcıları ile birleşir.

**Açıklamalar**  
Merhaba birleştirme ve bölme işlevleri arasında eşlik bulunur. Merhaba birleştirme işlevi bir dizeler dizisi alır ve bunları tooreturn tek bir dize sınırlayıcı bir dize kullanarak birleştirir. Merhaba bölünmüş işlev bir dize alır ve tooreturn bir dizeler dizisi hello sınırlayıcı ayırır. Ancak, bir anahtar farktır birleştirme sınırlayıcı dizesiyle dizeyi birleştirmek, bölme yalnızca bir tek karakter ayırıcısı kullanarak dizeleri ayırabilirsiniz.

**Örnek:**  
`Join([proxyAddresses],",")`  
Döndürebilirsiniz: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"

- - -
### <a name="lcase"></a>LCase
**Açıklama:**  
Merhaba LCase işlev bir dize toolower durumda tüm karakterleri dönüştürür.

**Sözdizimi:**  
`str LCase(str value)`

**Örnek:**  
`LCase("TeSt")`  
"Test" döndürür.

- - -
### <a name="left"></a>Sol
**Açıklama:**  
Merhaba sol işlevi bir dize hello soldan belirtilen sayıda karakteri döndürür.

**Sözdizimi:**  
`str Left(str string, num NumChars)`

* dize: Merhaba dize tooreturn karakterler
* NumChars: başından (sol) hello dizenin karakter tooreturn hello sayısı tanımlayan bir numara

**Notlar:**  
Dizedeki Hello ilk numChars karakter içeren bir dize:

* Varsa numChars = 0, boş bir dize döndürür.
* NumChars < 0, döndürmesi durumunda giriş dizesi.
* Dize null ise, boş bir dize döndürür.

Dize numChars içinde belirtilen hello sayıdan daha az karakter içeriyorsa, (yani parametre 1'deki tüm karakterleri içeren) bir dize aynı toostring döndürülür.

**Örnek:**  
`Left("John Doe", 3)`  
"Joh" döndürür.

- - -
### <a name="len"></a>Len
**Açıklama:**  
Merhaba Len işlevi bir dizedeki karakter sayısını döndürür.

**Sözdizimi:**  
`num Len(str value)`

**Örnek:**  
`Len("John Doe")`  
8 döndürür

- - -
### <a name="ltrim"></a>LTrim
**Açıklama:**  
Merhaba LTrim işlevi bir dizeden öndeki boşlukları kaldırır.

**Sözdizimi:**  
`str LTrim(str value)`

**Örnek:**  
`LTrim(" Test ")`  
"Test" döndürür

- - -
### <a name="mid"></a>Orta
**Açıklama:**  
Mid Merhaba işlevi bir dizedeki belirtilen konumdan belirtilen sayıda karakteri döndürür.

**Sözdizimi:**  
`str Mid(str string, num start, num NumChars)`

* dize: Merhaba dize tooreturn karakterler
* Başlat: dize tooreturn karakterlerinden konumda başlangıç hello tanımlayan bir numara
* NumChars: dizesinde konumundan karakterleri tooreturn hello sayısı tanımlayan bir numara

**Notlar:**  
Konumundan başlayan dönüş numChars karakter dizesi içinde başlatın.  
Konumu başlangıç dizesinde numChars karakterler içeren bir dize:

* Varsa numChars = 0, boş bir dize döndürür.
* NumChars < 0, döndürmesi durumunda giriş dizesi.
* Başlat > merhaba dize uzunluğu, giriş dizesi döndürür.
* Varsa Başlat < = 0, giriş dizesi döndürür.
* Dize null ise, boş bir dize döndürür.

NumChar karakter değilse kadar çok konumu başından dizesinde kalan karakterler mümkün olduğunca döndürülür.

**Örnek:**  
`Mid("John Doe", 3, 5)`  
"Hn" döndürür.

`Mid("John Doe", 6, 999)`  
"Doe" döndürür

- - -
### <a name="now"></a>Şimdi
**Açıklama:**  
Merhaba şimdi işlevi tooyour bilgisayarın sistem tarihi ve saati göre geçerli tarih ve saat, hello belirten bir DateTime döndürür.

**Sözdizimi:**  
`dt Now()`

- - -
### <a name="numfromdate"></a>NumFromDate
**Açıklama:**  
Merhaba NumFromDate işlevi bir tarih Reklamın tarih biçiminde döndürür.

**Sözdizimi:**  
`num NumFromDate(dt value)`

**Örnek:**  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
129699324000000000 döndürür

- - -
### <a name="padleft"></a>PadLeft
**Açıklama:**  
Belirtilen dize tooa Hello PadLeft işlev sol klavye takımı sağlanan doldurma karakteri kullanarak uzunluğu.

**Sözdizimi:**  
`str PadLeft(str string, num length, str padCharacter)`

* dize: dize toopad hello.
* Uzunluk: hello temsil eden bir tamsayı istenen dize uzunluğu.
* padCharacter: hello doldurma karakteri tek karakter toouse oluşan bir dize

**Notlar:**

* Dize uzunluğu Hello uzunluğundan az ise, bir uzunluk eşit toolength olana kadar sonra padCharacter (sol) art arda eklenmiş toohello dize başlangıcıdır.
* padCharacter bir boşluk karakteri olabilir, ancak bir null değer olamaz.
* Dize uzunluğu Hello eşit tooor uzunluğundan fazla ise, dize değişmeden döndürülür.
* Dize uzunluğu daha büyük veya eşit toolength varsa, bir dize aynı toostring döndürülür.
* Dize uzunluğu Hello uzunluğundan az ise, hello yeni bir dize uzunluğu padCharacter ile doldurulan dizeyi içeren döndürülür istenen.
* Dize null ise, hello işlevi boş bir dize döndürür.

**Örnek:**  
`PadLeft("User", 10, "0")`  
"000000User" döndürür.

- - -
### <a name="padright"></a>PadRight
**Açıklama:**  
Belirtilen dize tooa Hello PadRight işlev sağ klavye takımı sağlanan doldurma karakteri kullanarak uzunluğu.

**Sözdizimi:**  
`str PadRight(str string, num length, str padCharacter)`

* dize: dize toopad hello.
* Uzunluk: hello temsil eden bir tamsayı istenen dize uzunluğu.
* padCharacter: hello doldurma karakteri tek karakter toouse oluşan bir dize

**Notlar:**

* Dize uzunluğu Hello uzunluğundan az uzunluğu eşit toolength olana kadar sonra padCharacter art arda eklenmiş toohello (sağdaki) dize sonu ise.
* padCharacter bir boşluk karakteri olabilir, ancak bir null değer olamaz.
* Dize uzunluğu Hello eşit tooor uzunluğundan fazla ise, dize değişmeden döndürülür.
* Dize uzunluğu daha büyük veya eşit toolength varsa, bir dize aynı toostring döndürülür.
* Dize uzunluğu Hello uzunluğundan az ise, hello yeni bir dize uzunluğu padCharacter ile doldurulan dizeyi içeren döndürülür istenen.
* Dize null ise, hello işlevi boş bir dize döndürür.

**Örnek:**  
`PadRight("User", 10, "0")`  
"User000000" döndürür.

- - -
### <a name="pcase"></a>PCase
**Açıklama:**  
Merhaba PCase işlevi hello ilk karakteri bir dize tooupper durumda her boşlukla ayrılmış sözcük dönüştürür ve diğer tüm karakterler dönüştürülür toolower durumda.

**Sözdizimi:**  
`String PCase(string)`

**Notlar:**

* Bu işlev bir kısaltma gibi tamamen büyük bir sözcük doğru büyük/küçük harf tooconvert şu anda sağlamaz.

**Örnek:**  
`PCase("TEsT")`  
"Test" döndürür.

`PCase(LCase("TEST"))`  
"Test" döndürür

- - -
### <a name="randomnum"></a>RandomNum
**Açıklama:**  
Merhaba RandomNum işlevi, belirtilen aralık arasında rastgele bir sayı döndürür.

**Sözdizimi:**  
`num RandomNum(num start, num end)`

* Başlat: numara tanımlayıcı hello alt sınır olarak hello rastgele bir değeri toogenerate
* Son: bir numara tanımlayıcı hello sayısı üst sınırı hello rastgele bir değeri toogenerate

**Örnek:**  
`Random(100,999)`  
734 döndürebilir.

- - -
### <a name="removeduplicates"></a>RemoveDuplicates
**Açıklama:**  
Merhaba RemoveDuplicates işlevi, birden çok değerli bir dize alır ve her değerin benzersiz olduğundan emin olun.

**Sözdizimi:**  
`mvstr RemoveDuplicates(mvstr attribute)`

**Örnek:**  
`RemoveDuplicates([proxyAddresses])`  
Burada tüm yinelenen değerleri kaldırılmış bir ayıklanmış proxyAddress özniteliği döndürür.

- - -
### <a name="replace"></a>Değiştir
**Açıklama:**  
Merhaba Değiştir işlev bir dize tooanother dize tüm oluşumlarını değiştirir.

**Sözdizimi:**  
`str Replace(str string, str OldValue, str NewValue)`

* dize: dize tooreplace değerler.
* OldValue: hello dize toosearch ve tooreplace.
* NewValue: dize tooreplace hello.

**Notlar:**  
Merhaba işlevi özel adlar aşağıdaki hello tanır:

* \n – yeni satır
* \r – satır başı
* \t – sekmesi

**Örnek:**  
`Replace([address],"\r\n",", ")`  
CRLF virgül ve boşluk ile değiştirir ve çok neden olabilir "Bir Microsoft yolu, Redmond, WA, ABD"

- - -
### <a name="replacechars"></a>ReplaceChars
**Açıklama:**  
Merhaba ReplaceChars işlevi karakterler hello ReplacePattern dize bulundu tüm oluşumlarını değiştirir.

**Sözdizimi:**  
`str ReplaceChars(str string, str ReplacePattern)`

* dize: içinde bir dize tooreplace karakter.
* ReplacePattern: karakter tooreplace ile bir sözlük içeren bir dize.

Hello biçimi {kaynak1} şeklindedir: {target1}, {kaynak2}: {target2}, {kaynakN}, {targetN} kaynak hello karakter toofind ve hedef hello dize tooreplace sahip olduğu.

**Notlar:**

* Hello işlev her oluşumu tanımlanan kaynakları alır ve bunları hello hedefleri ile değiştirir.
* Merhaba kaynak tam olarak bir (unicode) karakter olmalıdır.
* Merhaba kaynağı boş veya bir karakter (ayrıştırma hatası) daha uzun olamaz.
* Merhaba hedef örneğin ö:oe, β:ss birden çok karakter uzunluğunda olabilir.
* Merhaba hedef hello karakter kaldırılması gerektiğini belirten boş olabilir.
* Merhaba kaynak küçük harfe duyarlıdır ve tam bir eşleşme olmalıdır.
* Merhaba, (virgül) ve: (iki nokta üst üste) ayrılmış karakterler ve bu işlevi kullanılarak değiştirilemez.
* Alanları ve diğer beyaz karakter hello ReplacePattern dize göz ardı edilir.

**Örnek:**  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
Raksmorgas döndürür

`ReplaceChars("O’Neil",%ReplaceString%)`  
Kaldırılan tanımlı toobe değilse "ONeil", hello tek değer döndürür.

- - -
### <a name="right"></a>Sağ
**Açıklama:**  
Merhaba sağ işlevi hello bir dize sağ (Bitiş) belirtilen sayıda karakteri döndürür.

**Sözdizimi:**  
`str Right(str string, num NumChars)`

* dize: Merhaba dize tooreturn karakterler
* NumChars: hello uçtan (sağdaki) dizenin karakter tooreturn hello sayısı tanımlayan bir numara

**Notlar:**  
NumChars karakter hello son dize konumundan döndürülür.

Dizedeki son numChars karakter Hello içeren bir dize:

* Varsa numChars = 0, boş bir dize döndürür.
* NumChars < 0, döndürmesi durumunda giriş dizesi.
* Dize null ise, boş bir dize döndürür.

Sayı belirtilen NumChars hello daha az karakter dizesini içeren bir dize aynı toostring döndürülür.

**Örnek:**  
`Right("John Doe", 3)`  
"Doe" döndürür.

- - -
### <a name="rtrim"></a>RTrim
**Açıklama:**  
Merhaba RTrim işlevi bir dizeden sondaki boşluk kaldırır.

**Sözdizimi:**  
`str RTrim(str value)`

**Örnek:**  
`RTrim(" Test ")`  
"Test" döndürür.

- - -
### <a name="select"></a>Şunu seçin:
**Açıklama:**  
Birden çok değerli bir öznitelik (veya bir ifade çıktısını) içindeki tüm değerleri belirtilen işlevine dayalı işlemi.

**Sözdizimi:**  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* Madde: hello birden çok değerli öznitelik bir öğeyi temsil eder
* Öznitelik: hello birden çok değerli özniteliği
* ifade: değerler koleksiyonu döndüren bir ifadeye
* koşul: hello özniteliği bir öğeyi işleyebilir işlevi

**Örnekler:**  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
Tire (-) kaldırdıktan sonra tüm hello değerler hello birden çok değerli özniteliği otherPhone döndürür.

- - -
### <a name="split"></a>Böl
**Açıklama:**  
Merhaba bölünmüş işlevi bir sınırlayıcı ile ayrılmış bir dize alır ve birden çok değerli bir dize kolaylaştırır.

**Sözdizimi:**  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* değer: Merhaba sınırlayıcı karakter tooseparate dizesi.
* sınırlayıcı: tek bir sınırlayıcı hello olarak kullanılan karakter toobe.
* sınır: en yüksek sayıda döndürebilir değeri.

**Örnek:**  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
Merhaba proxyAddress özniteliği için yararlı 2 öğeleri birden çok değerli bir dize döndürür.

- - -
### <a name="stringfromguid"></a>StringFromGuid
**Açıklama:**  
Merhaba StringFromGuid işlevi bir ikili GUID alır ve tooa dizesini sayıya dönüştürür

**Sözdizimi:**  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a>StringFromSid
**Açıklama:**  
Merhaba StringFromSid işlevi bir güvenlik tanımlayıcısı tooa dizesi içeren bir bayt dizisi dönüştürür.

**Sözdizimi:**  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a>Anahtar
**Açıklama:**  
Merhaba anahtar kullanılan tooreturn değerlendirilen koşullara göre tek bir değer işlevdir.

**Sözdizimi:**  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* Expr: tooevaluate istediğiniz değişken ifadesi.
* değer: değerin toobe döndürülen hello karşılık gelen ifadesi True ise.

**Notlar:**  
Merhaba anahtar işlevi bağımsız değişken listesi ifadeleri ve değer çiftlerinden oluşur. Merhaba ifadeler sol tooright değerlendirilir ve hello ilk ifade tooevaluate tooTrue ile ilişkili hello değeri döndürülür. Merhaba bölümleri düzgün eşleştirilmedi, bir çalışma zamanı hatası oluşur.

Örneğin, Expr1 True ise, anahtar value1 döndürür. Yanlış ifade 1., ancak expr 2 True ise, anahtar değeri 2 vb. döndürür.

Anahtar döndüren bir hiçbir şeyin varsa:

* Merhaba ifadeleri hiçbiri True olarak ayarlanır.
* Merhaba ilk True ifadenin null karşılık gelen bir değere sahip.

Bunlardan yalnızca birini döndürür olsa bile anahtar tüm ifadeler değerlendirir. Bu nedenle, istenmeyen yan etkileri için izlemeniz gerekir. Örneğin, herhangi bir ifade Hello değerlendirmesi sıfır hatası bir bölme sonuçlanırsa, bir hata oluşur.

Değer, özel bir dize döndürür hello hata işlevi de olabilir.

**Örnek:**  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
Bazı önemli şehirlerde konuşulan hello dili döndürür, aksi takdirde bir hata döndürür.

- - -
### <a name="trim"></a>Kırpma
**Açıklama:**  
Merhaba kırpma işlevi baştaki ve sondaki boşlukları bir dizeden kaldırır.

**Sözdizimi:**  
`str Trim(str value)`  

**Örnek:**  
`Trim(" Test ")`  
"Test" döndürür.

`Trim([proxyAddresses])`  
Baştaki ve sondaki boşlukları hello proxyAddress özniteliğinde her bir değer için kaldırır.

- - -
### <a name="ucase"></a>UCase
**Açıklama:**  
Merhaba UCase işlev bir dize tooupper durumda tüm karakterleri dönüştürür.

**Sözdizimi:**  
`str UCase(str string)`

**Örnek:**  
`UCase("TeSt")`  
"TEST" döndürür.

- - -
### <a name="where"></a>Burada

**Açıklama:**  
Belirli bir koşula dayalı birden çok değerli özniteliği (veya bir ifade çıktısını) değerleri kümesini döndürür.

**Sözdizimi:**  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* Madde: hello birden çok değerli öznitelik bir öğeyi temsil eder
* Öznitelik: hello birden çok değerli özniteliği
* koşul: olabilir herhangi bir ifade hesaplanan tootrue ya da yanlış
* ifade: değerler koleksiyonu döndüren bir ifadeye

**Örnek:**  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
Merhaba sertifika değerler, süresi dolmuş olmayan hello birden çok değerli özniteliği userCertificate içinde döndürür.

- - -
### <a name="with"></a>İle
**Açıklama:**  
işlevi ile Merhaba yolu toosimplify değişken toorepresent bir görünen bir alt kullanarak veya birden fazla kez hello karmaşık ifadesinde karmaşık bir ifade sağlar.

**Sözdizimi:**
`With(var variable, exp subExpression, exp complexExpression)`  
* değişken: Merhaba alt temsil eder.
* Alt: değişkeni tarafından temsil edilen alt.
* complexExpression: karmaşık bir ifade.

**Örnek:**  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
İşlevsel olarak eşdeğerdir:  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
Hangi hello userCertificate özniteliği yalnızca süresi dolmamış sertifika değerleri döndürür.


- - -
### <a name="word"></a>Word
**Açıklama:**  
Hello Word işlevi hello sınırlayıcıları toouse ve hello word numara tooreturn açıklayan parametrelerine göre bir dize içindeki bir sözcük döndürür.

**Sözdizimi:**  
`str Word(str string, num WordNumber, str delimiters)`

* dize: dize tooreturn bir sözcük hello.
* WordNumber: hangi word numarasını tanımlayan bir sayı döndürmelidir.
* Sınırlayıcılar: kullanılan tooidentify sözcükler olmalıdır hello delimiter(s) temsil eden bir dize

**Notlar:**  
Her bir hello sınırlayıcıları hello karakter birini ayırarak dizedeki karakter dizesini sözcükler olarak tanımlanır:

* Varsa < 1 sayı, boş dize döndürür.
* Dize null ise, boş bir dize döndürür.

Sözcük sayısı sayısından az dize içeriyor ya da dizesi sınırlayıcıları tarafından tanımlanan herhangi bir sözcük içermiyor, boş bir dize döndürdü.

**Örnek:**  
`Word("hello quick brown fox",3," ")`  
"Kahverengi" döndürür

`Word("This,string!has&many separators",3,",!&#")`  
"Var" döndürür

## <a name="additional-resources"></a>Ek Kaynaklar
* [Bildirim temelli hazırlama ifadelerini anlama](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [Azure AD Connect eşitleme: Eşitleme seçeneklerini özelleştirme](active-directory-aadconnectsync-whatis.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)
