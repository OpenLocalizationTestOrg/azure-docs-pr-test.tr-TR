---
title: "Azure Active Directory B2C: hello başlangıç paketinin özel ilkelerini anlama | Microsoft Docs"
description: "Bir konu Azure Active Directory B2C özel ilkeler hakkında"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 3484e8cc6fa6a9d57c2aa14c0cc9616065892d10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-custom-policies-of-hello-azure-ad-b2c-custom-policy-starter-pack"></a>Hello Azure AD B2C özel İlkesi başlangıç paketinin Hello özel ilkelerini anlama

Bu bölümde hello ile birlikte gelen hello B2C_1A_base ilkesinin tüm hello çekirdek öğeleri listeler **başlangıç paketi** ve kendi ilkelerinizi hello hello devralma aracılığıyla yazmak için de *B2C_1A_base_ Uzantıları İlkesi*.

Bu nedenle, bu daha fazla özellikle odaklanılmaktadır. önceden tanımlanmış hello üzerinde talep türleri, talep dönüştürmeleri, içerik tanımları, Talep sağlayıcı ile bunların teknik profillerini ve çekirdek kullanıcı Yolculuklar hello.

> [!IMPORTANT]
> Microsoft hiçbir açık veya zımni, bundan böyle sağlanan saygı toohello bilgilerle garantide bulunmaz. Değişiklikleri GA süreden önce herhangi bir zamanda GA zaman ya da sonra sunulmasının.

Kendi ilkeleri ve hello B2C_1A_base_extensions İlkesi, bu tanımları geçersiz kılın ve bu ana ilke gerektiği gibi ek olanları sağlayarak genişletir.

Merhaba çekirdek öğeleri hello *B2C_1A_base İlkesi* talep türleri, talep dönüştürmeleri ve içerik tanımlar. Bu öğeleri kendi ilkelerinizi de olduğu gibi hello başvurulan uygulanmadıkça toobe kullanılabilir *B2C_1A_base_extensions İlkesi*.

## <a name="claims-schemas"></a>Talep şemaları

Başka bir talep şemaları, üç bölüme ayrılmıştır:

1.  Düzgün şekilde hello kullanıcı Yolculuklar toowork için gerekli olan hello minimum talepleri listeler ilk bölümü.
2.  Sorgu dizesi parametreleri için gereken talepleri listeler hello ve diğer özel parametreler toobe tooother talep sağlayıcıları, geçirilen ikinci bölümü özellikle login.microsoftonline.com kimlik doğrulaması için. **Lütfen bu talepler değiştirmeyin**.
3.  Ve sonunda hello kullanıcıdan toplanan herhangi bir ek, isteğe bağlı talep listeleyen üçüncü bir bölüm hello dizinde saklanan ve oturum açma sırasında belirteçleri gönderilen. Bu bölümde türü toobe hello kullanıcıdan toplanan ve/veya hello belirteçte gönderilen yeni talep eklenebilir.

> [!IMPORTANT]
> Merhaba talep şema parolaları ve kullanıcı adları gibi belirli talepler kısıtlamaları içerir. Merhaba güven Framework (TF) ilke Azure AD herhangi bir talep sağlayıcısı olarak değerlendirir ve tüm kısıtlamaları hello premium ilkesinde modelled. Bir ilke, daha fazla kısıtlama değiştirilmiş tooadd olması veya başka bir talep sağlayıcı kendi kısıtlamaları olan kimlik bilgisi depolama alanını kullanın.

Merhaba kullanılabilir talep türleri aşağıda listelenmiştir.

### <a name="claims-that-are-required-for-hello-user-journeys"></a>Merhaba kullanıcı Yolculuklar için gerekli olan talepleri

Talepler aşağıdaki hello düzgün kullanıcı Yolculuklar toowork için gereklidir:

| Talep türü | Açıklama |
|-------------|-------------|
| *Kullanıcı Kimliği* | Kullanıcı adı |
| *signInName* | Oturum adı |
| *Tenantıd* | Azure AD B2C Premium hello kullanıcı nesnesinin Kiracı tanımlayıcısını (ID) |
| *objectID* | Azure AD B2C Premium hello kullanıcı nesnesinin nesne tanımlayıcısını (ID) |
| *Parola* | Parola |
| *#newpassword* | |
| *reenterPassword* | |
| *passwordPolicies* | Azure AD B2C Premium toodetermine parola gücünü, sona erme vb. tarafından kullanılan parola ilkeleri. |
| *Sub* | |
| *alternativeSecurityId* | |
| *Identityprovider* | |
| *görünen adı* | |
| *strongAuthenticationPhoneNumber* | Kullanıcının telefon numarası |
| *Verified.strongAuthenticationPhoneNumber* | |
| *E-posta* | Kullanılan toocontact hello kullanıcıya e-posta adresi |
| *signInNamesInfo.emailAddress* | Kullanıcı hello e-posta adresi olarak toosign kullanabilirsiniz |
| *otherMails* | Kullanılan toocontact hello kullanıcıya e-posta adresleri |
| *userPrincipalName* | Hello Azure AD B2C Premium depolandığı şekliyle kullanıcı adı |
| *upnUserName* | Kullanıcı asıl adı oluşturmak için kullanıcı adı |
| *mailNickName* | Hello Azure AD B2C Premium depolandığı şekliyle kullanıcının posta takma adı |
| *newUser* | |
| *yürütülen-SelfAsserted-giriş* | Talep, öznitelikler hello kullanıcıdan toplanan olup olmadığını belirtir |
| *yürütülen-PhoneFactor-giriş* | Talep, yeni bir telefon numarası hello kullanıcıdan toplanan olup olmadığını belirtir |
| *authenticationSource* | Merhaba kullanıcı sosyal kimlik sağlayıcısı, login.microsoftonline.com veya yerel hesap kimlik doğrulamasının yapıldığı belirtir |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a>Sorgu dizesi parametreleri ve diğer özel parametreler için gereken talepleri

Merhaba aşağıdaki talep (bazı sorgu dizesi parametreleri de dahil olmak üzere) özel parametreler tooother talep sağlayıcıları gerekli toopass şunlardır:

| Talep türü | Açıklama |
|-------------|-------------|
| *nux* | Yerel hesap kimlik doğrulaması toologin.microsoftonline.com için geçirilen özel parametresi |
| *NCA* | Yerel hesap kimlik doğrulaması toologin.microsoftonline.com için geçirilen özel parametresi |
| *istemi* | Yerel hesap kimlik doğrulaması toologin.microsoftonline.com için geçirilen özel parametresi |
| *Mkt* | Yerel hesap kimlik doğrulaması toologin.microsoftonline.com için geçirilen özel parametresi |
| *LC* | Yerel hesap kimlik doğrulaması toologin.microsoftonline.com için geçirilen özel parametresi |
| *grant_type* | Yerel hesap kimlik doğrulaması toologin.microsoftonline.com için geçirilen özel parametresi |
| *Kapsam* | Yerel hesap kimlik doğrulaması toologin.microsoftonline.com için geçirilen özel parametresi |
| *client_id* | Yerel hesap kimlik doğrulaması toologin.microsoftonline.com için geçirilen özel parametresi |
| *objectIdFromSession* | Parametresi, nesne kimliği hello hello varsayılan oturum yönetimi sağlayıcısı tooindicate tarafından sağlanan bir SSO oturumundan alınan |
| *isActiveMFASession* | Merhaba kullanıcının etkin bir MFA oturumu sahip parametre hello MFA oturum yönetimi tooindicate tarafından sağlanan |

### <a name="additional-optional-claims-that-can-be-collected"></a>Toplanabilir ek (isteğe bağlı) talepleri

Merhaba aşağıdaki hello kullanıcılardan toplanan ek talep hello dizinde saklanan ve hello belirteçte gönderilen talepleri. Önce özetlendiği gibi ek talep toothis listesi eklenebilir.

| Talep türü | Açıklama |
|-------------|-------------|
| *givenName* | Kullanıcının verilen adı (ilk adı olarak da bilinir) |
| *Soyadı* | Kullanıcının soyadı (Aile adı ve Soyadı olarak da bilinir) |
| *Extension_picture* | Sosyal kullanıcının resim |

## <a name="claim-transformations"></a>Talep dönüştürmeleri

Merhaba kullanılabilir talep dönüştürmeleri, aşağıda listelenmiştir.

| Talep dönüştürme | Açıklama |
|----------------------|-------------|
| *CreateOtherMailsFromEmail* | |
| *CreateRandomUPNUserName* | |
| *CreateUserPrincipalName* | |
| *CreateSubjectClaimFromObjectID* | |
| *CreateSubjectClaimFromAlternativeSecurityId* | |
| *CreateAlternativeSecurityId* | |

## <a name="content-definitions"></a>İçerik tanımları

Bu bölümde zaten hello bildirilen hello içerik tanımları açıklanmaktadır *B2C_1A_base* ilkesi. Bu içerik tanımları başvurulan, geçersiz ve/veya kendi ilkelerinizi de olduğu gibi hello gerektiği şekilde genişletilmiş uygulanmadıkça toobe olan *B2C_1A_base_extensions* ilkesi.

| Talep sağlayıcı | Açıklama |
|-----------------|-------------|
| *Facebook* | |
| *Yerel hesap oturum açma* | |
| *PhoneFactor* | |
| *Azure Active Directory* | |
| *Kendi kendine uygulanan* | |
| *Yerel hesap* | |
| *Oturum yönetimi* | |
| *Trustframework ilke altyapısı* | |
| *TechnicalProfiles* | |
| *Belirteci veren* | |

## <a name="technical-profiles"></a>Teknik profilleri

Bu bölümde hello talep sağlayıcısı başına zaten tanımlanmış hello teknik profilleri gösterilmektedir *B2C_1A_base* ilkesi. Daha fazla başvurulan, geçersiz ve/veya kendi ilkelerinizi de olduğu gibi hello gerektiği şekilde genişletilmiş uygulanmadıkça toobe Bu teknik profillerdir *B2C_1A_base_extensions* ilkesi.

### <a name="technical-profiles-for-facebook"></a>Facebook için teknik profilleri

| Teknik profili | Açıklama |
|-------------------|-------------|
| *Facebook OAUTH* | |

### <a name="technical-profiles-for-local-account-signin"></a>Yerel hesap oturum açma için teknik profilleri

| Teknik profili | Açıklama |
|-------------------|-------------|
| *Oturum açma etkileşimsiz* | |

### <a name="technical-profiles-for-phone-factor"></a>Telefon faktörü için teknik profilleri

| Teknik profili | Açıklama |
|-------------------|-------------|
| *PhoneFactor giriş* | |
| *PhoneFactor InputOrVerify* | |
| *PhoneFactor doğrulayın* | |

### <a name="technical-profiles-for-azure-active-directory"></a>Azure Active Directory için teknik profilleri

| Teknik profili | Açıklama |
|-------------------|-------------|
| *AAD-genel* | Teknik profili tarafından dahil hello diğer AAD xxx teknik profilleri |
| *AAD UserWriteUsingAlternativeSecurityId* | Sosyal oturum açma teknik profili |
| *AAD UserReadUsingAlternativeSecurityId* | Sosyal oturum açma teknik profili |
| *AAD UserReadUsingAlternativeSecurityId NoError* | Sosyal oturum açma teknik profili |
| *AAD UserWritePasswordUsingLogonEmail* | Yerel hesaplar için teknik profili |
| *AAD UserReadUsingEmailAddress* | Yerel hesaplar için teknik profili |
| *AAD UserWriteProfileUsingObjectId* | ObjectID kullanarak kullanıcı kaydını güncelleştirmek için teknik profili |
| *AAD UserWritePhoneNumberUsingObjectId* | ObjectID kullanarak kullanıcı kaydını güncelleştirmek için teknik profili |
| *AAD UserWritePasswordUsingObjectId* | ObjectID kullanarak kullanıcı kaydını güncelleştirmek için teknik profili |
| *AAD UserReadUsingObjectId* | Kullanıcı kimlik doğrulaması yaptıktan sonra teknik kullanılan tooread veri profilidir |

### <a name="technical-profiles-for-self-asserted"></a>Kendi kendine uygulanan için teknik profilleri

| Teknik profili | Açıklama |
|-------------------|-------------|
| *SelfAsserted sosyal* | |
| *SelfAsserted ProfileUpdate* | |

### <a name="technical-profiles-for-local-account"></a>Yerel hesap için teknik profilleri

| Teknik profili | Açıklama |
|-------------------|-------------|
| *LocalAccountSignUpWithLogonEmail* | |

### <a name="technical-profiles-for-session-management"></a>Oturum yönetimi için teknik profilleri

| Teknik profili | Açıklama |
|-------------------|-------------|
| *SM sekmeyi* | |
| *SM AAD* | |
| *SM SocialSignup* | Profil adı yukarı kullanılan toodisambiguate AAD oturum oturum arasında olması ve oturum açın |
| *SM SocialLogin* | |
| *SM MFA* | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a>Trustframework ilke altyapısı TechnicalProfiles için teknik profilleri

Hiçbir teknik profilleri Merhaba şu anda tanımlanmış **Trustframework ilke altyapısı TechnicalProfiles** Talep sağlayıcı.

### <a name="technical-profiles-for-token-issuer"></a>Belirteç Verenin için teknik profilleri

| Teknik profili | Açıklama |
|-------------------|-------------|
| *JwtIssuer* | |

## <a name="user-journeys"></a>Kullanıcı Yolculuklar

Bu bölümde zaten hello bildirilen hello kullanıcı Yolculuklar gösterilmektedir *B2C_1A_base* ilkesi. Bu kullanıcı Yolculuklar daha fazla başvurulan, geçersiz ve/veya kendi ilkelerinizi de olduğu gibi hello gerektiği şekilde genişletilmiş uygulanmadıkça toobe olan *B2C_1A_base_extensions* ilkesi.

| Kullanıcı gezisine | Açıklama |
|--------------|-------------|
| *Kaydolma* | |
| *Oturum açma* | |
| *SignUpOrSignIn* | |
| *EditProfile* | |
| *PasswordReset* | |
