---
title: "aaaPopulate grupları dinamik olarak temel Azure Active Directory nesne öznitelikleri hakkında | Microsoft Docs"
description: "Nasıl-grup üyeliği de dahil olmak üzere desteklenen ifade kural işleçleri ve parametreleri için toocreate kuralları Gelişmiş."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 04813a42-d40a-48d6-ae96-15b7e5025884
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: curtand
ms.reviewer: rodejo
ms.openlocfilehash: fe22829118ed8f5137a619d93fa6f9bf80835863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="populate-groups-dynamically-based-on-object-attributes"></a>Grupları dinamik olarak nesnesi özniteliklerini temel alarak doldurur
Merhaba Klasik Azure portalı daha karmaşık öznitelik tabanlı gruplara yönelik dinamik üyelikler Azure Active Directory (Azure AD) ile Merhaba özelliği tooenable sağlar.  

Merhaba değişiklik tetikleyecek varsa herhangi bir kullanıcı veya aygıt değişikliği özniteliklerini hello sistem dizin toosee tüm dinamik Grup kurallarında değerlendirildiğinde herhangi bir grup ekler veya kaldırır. Bir kullanıcı veya cihaza bir grupta kuralı uymazsa, bunlar bu grubun bir üyesi olarak eklenir. Bunlar artık hello kural karşılamak varsa, bunlar kaldırılır.

> [!NOTE]
> - Güvenlik gruplarında veya Office 365 gruplarında dinamik üyelik için bir kural ayarlayabilirsiniz.
>
> - Bu özellik, her kullanıcı üye eklenen tooat en az bir dinamik bir grup için bir Azure AD Premium P1 lisansı gerektirir.
>
> - Aygıtların veya kullanıcıların dinamik bir grup oluşturabilirsiniz, ancak kullanıcı ve aygıt nesneleri içeren bir kuralı oluşturulamıyor.

> - Merhaba şu anda olası toocreate kullanıcının özniteliklere sahip bir cihaz grubuna bağlı değil. Cihaz Üyelik kuralları yalnızca başvuru hemen öznitelikleri cihaz nesnelerinin hello dizin olabilir.

## <a name="toocreate-an-advanced-rule"></a>toocreate Gelişmiş bir kuralı
1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com)seçin **Active Directory**ve ardından, kuruluşunuzun dizininde açın.
2. Select hello **grupları** sekmesini ve ardından açık hello grubu tooedit.
3. Select hello **yapılandırma** sekmesi, select hello **Gelişmiş kural** seçeneğini ve ardından hello metin kutusuna kural Gelişmiş hello girin.

## <a name="constructing-hello-body-of-an-advanced-rule"></a>Gelişmiş bir kural gövdesi Hello oluşturma
gruplara yönelik dinamik üyelikler hello için oluşturabileceğiniz hello Gelişmiş üç bölümden oluşur ve bir true veya false sonucu Sonuçlar aslında bir ikili ifade kuralıdır. Merhaba üç bölümden şunlardır:

* Sol parametre
* İkili işleç
* Sağ sabiti

Tam gelişmiş kural benzer toothis arar: (leftParameter işlecin "RightConstant"), açma ve kapama parantezi hello hello tüm ikili deyimi için gerekli olan yerlerde, çift tırnak işareti hello sağ sabiti ve hello sözdizimi için gereklidir Merhaba user.property sol parametresidir. Gelişmiş bir kural birden fazla ikili ifadeler hello tarafından ayrılmış oluşabilir- ve- ya da ve - değil mantıksal işleçler.
Merhaba, doğru şekilde oluşturulmuş bir Gelişmiş kural örnekleri şunlardır:

* (user.department - eq "Satış")- veya (user.department - eq "Pazarlama")
* (user.department - eq "Satış")- ve - değil (user.jobTitle-"SDE" içerir)

Merhaba tam listesi ve desteklenen parametreler ve ifade kural işleçleri için aşağıdaki bölümlere bakın.


Merhaba özelliği hello doğru nesne türü ile eklenmelidir Not: kullanıcı veya aygıt.
Kural aşağıda Hello hello doğrulama başarısız olur: – ne null posta

Merhaba doğru kural olacaktır:

User.Mail – ne null

Merhaba, Gelişmiş kural gövdesi Hello toplam uzunluğu 2048 karakterden uzun olamaz.

> [!NOTE]
> Dize ve regex işlemlerinin büyük küçük harfe duyarlı.
> Tırnak işareti içeren bir dizeler "kullanarak kaçışlı ' karakter, örneğin, user.department - eq \`"Satış".
> Yalnızca dize türü değerleri için tırnak işareti kullanın ve yalnızca İngilizce tırnak işareti kullanın.
>
>

## <a name="supported-expression-rule-operators"></a>Desteklenen ifade kural işleçleri
Merhaba aşağıdaki tabloda tüm desteklenen hello ifade kural işleçleri ve kural Gelişmiş hello hello gövdesinde kullanılan kendi sözdizimi toobe listelenmektedir:

| işleci | Sözdizimi |
| --- | --- |
| Eşit değildir |-ne |
| eşittir |-eq |
| İle başlayan değil |-notStartsWith |
| İle başlar |-startsWith |
| İçermez |-notContains |
| Contains |-içerir |
| Eşleşmiyor |-notMatch |
| eşleşme |-eşleşmesi |
| İçinde | -içinde |
| İçinde değil | -notIn |

## <a name="operator-precedence"></a>İşleç önceliği

Tüm işleçler alt toohigher öncelikten başına aşağıda listelenmiştir, aynı satır içinde işleci içinde eşit önceliğe-tüm - tüm - veya - ve - değil - eq - ne - startsWith - notStartsWith-- notContains içeren-– notMatch eşleşen-- notIn içinde

Tüm işleçleri ile veya tire öneki olmadan kullanılabilir.

Parantez her zaman gerekli, öncelik gereksinimlerinizi örneğin karşılamadığında tooadd parantez yalnızca gerekir dikkat edin:

   User.Department-eq "Pazarlama" – ve Resource.country-eq "ABD"

eşdeğerdir:

   (user.department-eq "Pazarlama") – ve (Resource.country-eq "ABD")

## <a name="using-hello--in-and--notin-operators"></a>Kullanarak hello - içinde ve - notIn işleçleri

Bir dizi farklı değerlere karşı bir kullanıcı özniteliğinin toocompare hello değeri istiyorsanız kullanabileceğiniz hello - içinde ya da - notIn işleçler. Örneği kullanarak hello - işleci:

    user.department -In [ "50001", "50002", "50003", “50005”, “50006”, “50007”, “50008”, “50016”, “50020”, “50024”, “50038”, “50039”, “51100” ]

Not hello hello "[" ve "]" Merhaba başına ve değer hello listesi sonundaki. Bu durum hello listesinde hello değerlerin user.department eşittir bir hello değerinin tooTrue değerlendirir.

## <a name="query-error-remediation"></a>Sorgu hata düzeltme
Merhaba aşağıdaki tabloda olası hataları listeler ve nasıl toocorrect bunları oluşursa

| Sorgu ayrıştırma hatası | Hata kullanımı | Düzeltilmiş kullanımı |
| --- | --- | --- |
| Hata: özniteliği desteklenmiyor. |(user.invalidProperty - eq "Value") |(user.department - eq "value")<br/>Özellik hello birinden eşleşmelidir [özellikleri listesi desteklenen](#supported-properties). |
| Hata: Öznitelikte işleci desteklenmiyor. |(user.accountEnabled-true içerir) |(user.accountEnabled - eq true)<br/>Özellik olduğu boolean türü. Desteklenen hello işleçleri kullanın (-eq veya - ne) listesinin hello Boole türünden üzerinde. |
| Hata: Sorgu derleme hatası oluştu. |(user.department - eq "Satış")- ve (user.department - eq "Pazarlama") (user.userPrincipalName-eşleşen "*@domain.ext") |(user.department - eq "Satış")- ve (user.department - eq "Pazarlama")<br/>Mantıksal işleç, listeden bir desteklenen hello özellikleri yukarıdaki eşleşmelidir. (user.userPrincipalName-eşleşen ". *@domain.ext") veya (user.userPrincipalName-eşleşen "@domain.ext$") normal ifadede hata. |
| Hata: İkili ifade doğru biçimde değil. |(user.department-eq "Satış") (user.department - eq "Satış") (user.department-eq "Satış") |(user.accountEnabled - eq true)- ve (user.userPrincipalName-içeren "alias@domain")<br/>Sorgu birden çok hata içeriyor. Parantez doğru yerde içinde değil. |
| Hata: Dinamik üyelikleri ayarı sırasında bilinmeyen bir hata oluştu. |(user.accountEnabled - eq "True" ve user.userPrincipalName-içeren "alias@domain") |(user.accountEnabled - eq true)- ve (user.userPrincipalName-içeren "alias@domain")<br/>Sorgu birden çok hata içeriyor. Parantez doğru yerde içinde değil. |

## <a name="supported-properties"></a>Desteklenen özellikler
Merhaba, Gelişmiş kuralınız kullanabileceğiniz tüm hello kullanıcı özellikleri şunlardır:

### <a name="properties-of-type-boolean"></a>Boolean özelliklerini türü
İzin verilen işleçleri

* -eq
* -ne

| Özellikler | İzin verilen değerler | Kullanım |
| --- | --- | --- |
| accountEnabled |doğru false |user.accountEnabled - eq true |
| dirSyncEnabled |doğru false |user.dirSyncEnabled - eq true |

### <a name="properties-of-type-string"></a>Dize türünde özellikleri
İzin verilen işleçleri

* -eq
* -ne
* -notStartsWith
* -StartsWith
* -içerir
* -notContains
* -eşleşmesi
* -notMatch
* -içinde
* -notIn

| Özellikler | İzin verilen değerler | Kullanım |
| --- | --- | --- |
| city |Herhangi bir dize değeri veya $null |(user.city - eq "value") |
| Ülke |Herhangi bir dize değeri veya $null |(Resource.country - eq "value") |
| Şirket adı | Herhangi bir dize değeri veya $null | (user.companyName - eq "value") |
| Bölüm |Herhangi bir dize değeri veya $null |(user.department - eq "value") |
| Görünen adı |Herhangi bir dize değeri |(user.displayName - eq "value") |
| facsimileTelephoneNumber |Herhangi bir dize değeri veya $null |(user.facsimileTelephoneNumber - eq "value") |
| givenName |Herhangi bir dize değeri veya $null |(user.givenName - eq "value") |
| İş Unvanı |Herhangi bir dize değeri veya $null |(user.jobTitle - eq "value") |
| Posta |Herhangi bir dize değeri veya $null (Merhaba kullanıcının SMTP adresi) |(user.mail - eq "value") |
| mailNickName |Herhangi bir dize değeri (Merhaba kullanıcı diğer adı posta) |(user.mailNickName - eq "value") |
| Mobil |Herhangi bir dize değeri veya $null |(user.mobile - eq "value") |
| objectID |Merhaba kullanıcı nesnesinin GUID |(user.objectId - eq "1111111-1111-1111-1111-111111111111") |
| onPremisesSecurityIdentifier | Gelen eşitlenmiş olan kullanıcılar için şirket içi güvenlik tanımlayıcısı (SID) toohello bulut şirket içi. |(user.onPremisesSecurityIdentifier - eq "S-1-1-11-1111111111-1111111111-1111111111-1111111") |
| passwordPolicies |Hiçbiri DisableStrongPassword DisablePasswordExpiration DisablePasswordExpiration, DisableStrongPassword |(user.passwordPolicies - eq "DisableStrongPassword") |
| physicalDeliveryOfficeName |Herhangi bir dize değeri veya $null |(user.physicalDeliveryOfficeName - eq "value") |
| posta kodu |Herhangi bir dize değeri veya $null |(user.postalCode - eq "value") |
| preferredLanguage |ISO 639-1 kodu |(user.preferredLanguage - eq "en-US") |
| sipProxyAddress |Herhangi bir dize değeri veya $null |(user.sipProxyAddress - eq "value") |
| durum |Herhangi bir dize değeri veya $null |(user.state - eq "value") |
| StreetAddress |Herhangi bir dize değeri veya $null |(user.streetAddress - eq "value") |
| Soyadı |Herhangi bir dize değeri veya $null |(user.surname - eq "value") |
| telephoneNumber |Herhangi bir dize değeri veya $null |(user.telephoneNumber - eq "value") |
| usageLocation |İki harflerin ülke kodu |(user.usageLocation - eq "ABD") |
| userPrincipalName |Herhangi bir dize değeri |(user.userPrincipalName - eq "alias@domain") |
| UserType |üye Konuk $null |(user.userType - eq "Üye") |

### <a name="properties-of-type-string-collection"></a>Türü dize koleksiyonunun özellikleri
İzin verilen işleçleri

* -içerir
* -notContains

| Özellikler | İzin verilen değerler | Kullanım |
| --- | --- | --- |
| otherMails |Herhangi bir dize değeri |(user.otherMails-içeren "alias@domain") |
| proxyAddresses |SMTP: alias@domain smtp:alias@domain |(user.proxyAddresses-içeren "SMTP: alias@domain") |

## <a name="multi-value-properties"></a>Birden çok değerli özellikleri
İzin verilen işleçleri

* -herhangi (Merhaba koleksiyonda en az bir öğe hello koşul eşleştiğinde memnun)
* -(tüm hello koleksiyondaki tüm öğeleri hello koşul eşleştiğinde memnun)

| Özellikler | Değerler | Kullanım |
| --- | --- | --- |
| assignedPlans |Aşağıdaki dize özelliklere hello hello koleksiyondaki her nesneyi sunar: capabilityStatus, hizmet, servicePlanId |user.assignedPlans-tüm (assignedPlan.servicePlanId - eq "efb87545-963c-4e0d-99df-69c6916d9eb0"- ve assignedPlan.capabilityStatus - eq "Etkin") |

Çoklu değer özelliklerdir hello nesne koleksiyonları aynı türde. Kullanabileceğiniz - hello tümünün veya bir koşul tooone öğelerini hello koleksiyonunda sırasıyla tüm ve - tüm işleçleri tooapply. Örneğin:

assignedPlans toohello kullanıcı atanan tüm hizmet planları listeleyen birden çok değerli bir özelliktir. Merhaba ifade aşağıda da etkin durumda olan hello Exchange Online (planı 2) hizmet planı olan kullanıcılar seçer:

```
user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled")
```

(Merhaba GUID tanımlayıcısı hello Exchange Online (planı 2) hizmet planı tanımlar.)

> [!NOTE]
> Tooidentify tüm kullanıcıların kendisi için istiyorsanız kullanışlıdır bir Office 365 (veya diğer Microsoft çevrimiçi hizmet) özelliği etkinleştirildi, örnek tootarget için bunları ilkeleri belirli bir dizi.

Merhaba ifadesini hello ("SCO" hizmet adı tarafından tanımlanan) Intune hizmeti ile ilişkili herhangi bir hizmet planının olan tüm kullanıcıları seçer:
```
user.assignedPlans -any (assignedPlan.service -eq "SCO" -and assignedPlan.capabilityStatus -eq "Enabled")
```

## <a name="use-of-null-values"></a>Null değerleri kullanımı

toospecify bir null değer bir kuralı, "null" ya da $null kullanabilirsiniz. Örnek:

   User.Mail – ne null user.mail – ne için $null eşdeğerdir

## <a name="extension-attributes-and-custom-attributes"></a>Uzantı öznitelikleri ve özel öznitelikler
Uzantı öznitelikleri ve özel öznitelikler dinamik üyelik kurallarında desteklenir.

Uzantı öznitelikleri AD şirket içi penceresi sunucusundan eşitlenen ve "X 1-15 burada eşittir ExtensionAttributeX" Merhaba biçimi uygulayın.
Bir uzantı özniteliği kullanan bir kural, bir örnek olabilir

(user.extensionAttribute15 - eq "Pazarlama")

Özel öznitelikler, şirket içi Windows Server AD veya bir bağlı SaaS uygulama ve hello hello biçimine eşitlenen "user.extension_[GUID]\__ [öznitelik]", [GUID] hello uygulamanın benzersiz tanımlayıcısı aad'de hello olduğu, oluşturulan hello özniteliğinde AAD ve [öznitelik] oluşturulduğu hello özniteliğinin hello adı aynıdır.
Özel bir öznitelik kullanan bir kural örneğidir

User.extension_c272a57b722d4eb29bfe327874ae79cb__OfficeNumber  

Merhaba özel öznitelik adı hello dizininde bir kullanıcı sorgulanarak bulunabilir özniteliği grafik Gezgini'ni kullanarak ve hello öznitelik adı için arama.

## <a name="direct-reports-rule"></a>"Doğrudan raporları" kuralı
Yöneticinin tüm doğrudan raporları içeren bir grup oluşturabilirsiniz. Hello Yöneticisi'nin doğrudan raporları hello gelecekteki değiştirdiğinizde, hello grubun üyeliği otomatik olarak ayarlanır.

> [!NOTE]
> 1. Merhaba kural toowork için emin hello olun **Manager kimliği** özelliği ayarlanmış doğru kiracınızda kullanıcıları. Bir kullanıcı için geçerli değer hello denetleyebilirsiniz kendi **Profil sekmesi**.
> 2. Bu kural yalnızca destekler **doğrudan** raporlar. Şu anda olası toocreate iç içe geçmiş bir hiyerarşi, örneğin doğrudan raporlar ve bunların raporları içeren bir grubu için bir grup değil.

**tooconfigure hello grubu**

1. 1-5 bölümünden adımlarını [toocreate hello Gelişmiş kural](#to-create-the-advanced-rule)seçip bir **üyelik türü** , **dinamik kullanıcı**.
2. Merhaba üzerinde **dinamik Üyelik kuralları** dikey penceresinde hello kural sözdizimi aşağıdaki hello ile girin:

    *"{ObectID_of_manager}" için doğrudan raporları*

    Geçerli bir kural örneği:
```
                    Direct Reports for "62e19b97-8b3d-4d4a-a106-4ce66896a863"
```
    where “62e19b97-8b3d-4d4a-a106-4ce66896a863” is hello objectID of hello manager. hello object ID can be found on manager's **Profile tab**.
3. Hello kural kaydedildikten sonra hello tüm kullanıcılarla toohello Grup Yöneticisi kimlik değeri eklenecek belirtilmiş.

## <a name="using-attributes-toocreate-rules-for-device-objects"></a>İçin cihaz nesnelerinin öznitelikleri toocreate kurallarını kullanma
Bir gruptaki üyelik için cihaz nesnelerinin seçen bir kural oluşturabilirsiniz. cihaz öznitelikleri aşağıdaki hello kullanılabilir:

| Özellikler              | İzin verilen değerler                  | Kullanım                                                       |
|-------------------------|---------------------------------|-------------------------------------------------------------|
| accountEnabled          | doğru false                      | (device.accountEnabled - eq true)                            |
| Görünen adı             | Herhangi bir dize değeri                | (device.displayName - eq "Ramiz Iphone")                       |
| deviceOSType            | Herhangi bir dize değeri                | (device.deviceOSType - eq "IOS")                             |
| DeviceOSVersion         | Herhangi bir dize değeri                | (cihazı. OSVersion - eq "9.1")                                |
| deviceCategory          | Herhangi bir dize değeri                | (device.deviceCategory - eq "")                              |
| DeviceManufacturer      | Herhangi bir dize değeri                | (device.deviceManufacturer - eq "Microsoft")                 |
| DeviceModel             | Herhangi bir dize değeri                | (device.deviceModel - eq "IPhone 7 +")                        |
| deviceOwnership         | Herhangi bir dize değeri                | (device.deviceOwnership - eq "")                             |
| domainName              | Herhangi bir dize değeri                | (device.domainName - eq "contoso.com")                       |
| enrollmentProfileName   | Herhangi bir dize değeri                | (device.enrollmentProfileName - eq "")                       |
| isRooted                | doğru false                      | (device.deviceOSType - eq true)                              |
| managementType          | Herhangi bir dize değeri                | (device.managementType - eq "")                              |
| Kuruluş birimi      | Herhangi bir dize değeri                | (device.organizationalUnit - eq "")                          |
| deviceId                | Geçerli bir cihaz kimliği                | (device.deviceId - eq "d4fe7726-5966-431c-b3b8-cddc8fdb717d") |
| objectID                | Geçerli bir AAD objectID            | (device.objectId - eq "76ad43c9-32c5-45e8-a272-7b58b58f596d") |

> [!NOTE]
> Bu cihaz kurallarını hello "Basit kuralı" açılır hello Klasik Azure portalı kullanılarak oluşturulamaz.
>
>

## <a name="next-steps"></a>Sonraki adımlar
Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.

* [Gruplara yönelik dinamik üyelikler sorunlarını giderme](active-directory-accessmanagement-troubleshooting.md)
* [Azure Active Directory grupları ile erişim tooresources yönetme](active-directory-manage-groups.md)
* [Grup ayarlarını yapılandırmak için Azure Active Directory cmdlet'leri](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)
