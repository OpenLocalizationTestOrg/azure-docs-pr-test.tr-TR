---
title: "Azure AD Connect: Bildirim temelli hazırlama ifadelerini | Microsoft Docs"
description: "Merhaba bildirim temelli hazırlama ifadelerini açıklanmaktadır."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: e3ea53c8-3801-4acf-a297-0fb9bb1bf11d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 516bcf1991c608d33aefc19551254d8b2bfc024f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning-expressions"></a>Azure AD Connect eşitleme: bildirim temelli hazırlama ifadeleri anlama
Azure AD Connect eşitleme ilk Forefront Identity Manager 2010'da sunulan bildirim temelli hazırlama üzerinde oluşturur. Tooimplement tanır tam kimlik tümleştirme iş mantığınızı hello gerek toowrite olmadan derlenmiş kod.

Bildirim temelli hazırlama, önemli bir bölümünü özniteliği akışlarında kullanılan hello ifade dilidir. kullanılan hello dili, Microsoft® Visual Basic® for Applications (VBA) bir alt kümesidir. Bu dil Microsoft Office'de kullanılır ve VBScript deneyimi olan kullanıcılar da onu tanımaz. Merhaba bildirim temelli hazırlama ifade dili yalnızca işlevler kullanılarak ve yapılandırılmış bir dil değil. Yöntemleri veya deyimleri yok. İşlevleri yerine içe tooexpress program akışı.

Daha fazla ayrıntı için bkz: [Office 2013 için dil başvurusu uygulamalar için Visual Basic toohello Hoş Geldiniz](https://msdn.microsoft.com/library/gg264383.aspx).

Merhaba öznitelikleri kesin türü belirtilmiş. Bir işlev yalnızca hello doğru türde öznitelikleri kabul eder. Ayrıca, büyük küçük harfe duyarlı değildir. Bir hata oluşturulur veya işlev adları ve öznitelik adları doğru büyük/küçük harf olmalıdır.

## <a name="language-definitions-and-identifiers"></a>Dil tanımları ve tanımlayıcıları
* İşlev bağımsız değişkenleri köşeli adından sonra sahip: FunctionName (1 bağımsız değişkeni, değişken N).
* Öznitelikleri köşeli tarafından tanımlanır: [attributeName]
* Parametreleri yüzde işaretleri tarafından tanımlanır: % ParameterName %
* Dize sabitleri tırnak içine alınmış: Örneğin, "Contoso" (Not: düz tırnak işaretleri kullanmanız gerekir "" tırnak akıllı değil ve "")
* Sayısal değerler teklifleri ve beklenen toobe ondalık ifade edilir. Onaltılık değerler öneki ile & H. Örneğin, 98052 & HFF
* Boole değerleri sabitler ile ifade edilir: True, False.
* Yerleşik sabit ve değişmez değerleri yalnızca kendi adı ile ifade edilir: NULL, CRLF, IgnoreThisFlow

### <a name="functions"></a>İşlevler
Bildirim temelli hazırlama, birçok işlevleri tooenable hello olasılığı tootransform öznitelik değerleri kullanır. Bir işlevden Hello sonuç tooanother işlevinde geçirilen şekilde bu işlevleri iç içe.

`Function1(Function2(Function3()))`

işlevlerin tam listesi Hello hello bulunabilir [işlev başvurusu](active-directory-aadconnectsync-functions-reference.md).

### <a name="parameters"></a>Parametreler
Bir parametre bir bağlayıcı veya PowerShell kullanan bir yönetici tarafından tanımlanır. Parametreler genellikle sistem toosystem farklı değerlere sahip, hello hello etki alanı hello kullanıcının adını, örneğin bulunur. Bu parametreler öznitelik akışları kullanılabilir.

gelen eşitleme kuralları için şu parametreler hello Active Directory Bağlayıcısı sağlanan hello:

| Parametre Adı | Açıklama |
| --- | --- |
| Domain.Netbios |Şu anda alınmakta hello etki alanı örneğin FABRIKAMSALES NetBIOS biçimi |
| Domain.FQDN |Şu anda alınmakta hello etki alanı örneğin sales.fabrikam.com FQDN biçimi |
| Domain.LDAP |Şu anda alınmakta hello etki alanı örneğin DC LDAP biçimi Satışlar, DC = fabrikam, DC = com = |
| Forest.Netbios |NetBIOS adının biçimi şu anda alınmakta hello orman örneğin FABRIKAMCORP |
| Forest.FQDN |Şu anda alınmakta hello orman adı örneğin fabrikam.com FQDN biçimi |
| Forest.LDAP |LDAP adının biçimi şu anda alınmakta hello orman örneğin DC fabrikam, DC = com = |

Merhaba sistemidir hello parametresi kullanılan tooget hello hello bağlayıcı tanıtıcısı şu anda çalıştığı:  
`Connector.ID`

Merhaba hello kullanıcının bulunduğu hello etki alanının NetBIOS adını hello meta veri deposu özniteliği etki alanı dolduran bir örnek aşağıda verilmiştir:  
`domain` <- `%Domain.Netbios%`

### <a name="operators"></a>İşleçler
hello işleçleri aşağıdaki kullanılabilir:

* **Karşılaştırma**: <, < =, <>, =, >, > =
* **Matematik**: +, -, \*, -
* **Dize**: & (Birleştir)
* **Mantıksal**: & & (ve) || (veya)
* **Değerlendirme sırası**:)

İşleçler değerlendirilen sol tooright ve hello aynı değerlendirme öncelik. Diğer bir deyişle, hello \* (çarpanı) (önce - çıkarma) değerlendirilmez. 2\*(5 + 3) olduğunu değil hello aynı 2 olarak\*5 + 3. Merhaba köşeli ayraçlar () kullanılan toochange hello değerlendirme sipariş bırakıldığına tooright değerlendirme sırası uygun değil.

## <a name="multi-valued-attributes"></a>Birden çok değerli öznitelikleri
Merhaba işlevleri hem tek değerli ve birden çok değerli öznitelikleri üzerinde çalışabilir. Birden çok değerli öznitelikler için hello işlevi her değer çalışır ve hello geçerlidir tooevery değer ile aynı işlevi.

Örneğin:  
`Trim([proxyAddresses])`Kırpma hello proxyAddress özniteliğinde her değerin yapın.  
`Word([proxyAddresses],1,"@") & "@contoso.com"`Her değere sahip bir @-sign, hello etki alanı ile Değiştir @contoso.com.  
`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])`Merhaba SIP adresi arayın ve başlangıç değerleri kaldırın.

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba yapılandırma modeli hakkında daha fazla bilgiyi [anlama bildirim temelli hazırlama](active-directory-aadconnectsync-understanding-declarative-provisioning.md).
* Bkz: nasıl bildirim temelli sağlama kullanılan out-of-box içinde olduğu [anlama hello varsayılan yapılandırma](active-directory-aadconnectsync-understanding-default-configuration.md).
* Toomake bir pratik nasıl değiştiğini içinde bildirim temelli hazırlama kullanarak görmek [nasıl toomake değişiklik toohello varsayılan yapılandırması](active-directory-aadconnectsync-change-the-configuration.md).

**Genel bakış konuları**

* [Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme](active-directory-aadconnectsync-whatis.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)

**Başvuru konuları**

* [Azure AD Connect eşitleme: işlevleri başvurusu](active-directory-aadconnectsync-functions-reference.md)

