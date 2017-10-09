---
title: "Azure Active Directory B2C: Çok faktörlü kimlik doğrulaması | Microsoft Docs"
description: "Tooenable tüketiciye yönelik uygulamalar çok faktörlü kimlik doğrulaması Azure Active Directory B2C tarafından güvenliği nasıl"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 53ef86c4-1586-45dc-9952-dbbd62f68afc
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 29beb1e6ab5d8ab5a65f9c5c068d9e71c60418dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-enable-multi-factor-authentication-in-your-consumer-facing-applications"></a>Azure Active Directory B2C: Tüketiciye yönelik uygulamalarınızda çok faktörlü kimlik doğrulamasını etkinleştir
Azure Active Directory (Azure AD) B2C ile doğrudan tümleşir [Azure çok faktörlü kimlik doğrulaması](../multi-factor-authentication/multi-factor-authentication.md) böylece tüketiciye yönelik uygulamalarınızda güvenlik toosign yukarı ve oturum açma deneyimlerini ikinci bir katmanı ekleyebilirsiniz. Ve tek satırlık bir kod yazmak zorunda kalmadan bunu yapabilirsiniz. Şu anda telefon çağrısı ve metin iletisi doğrulama destekler. Kaydolma ve oturum açma ilkeleri oluşturduysanız, çok faktörlü kimlik doğrulaması yine etkinleştirebilirsiniz.

> [!NOTE]
> Varolan ilkeleri yalnızca düzenleyerek kaydolma ve oturum açma ilkeleri oluşturduğunuzda, çok faktörlü kimlik doğrulaması de etkinleştirilebilir.
> 
> 

Bu özellik hello aşağıdaki gibi senaryoları işlemek uygulamaları yardımcı olur:

* Çok faktörlü kimlik doğrulaması tooaccess bir uygulama gerekmez, ancak tooaccess gerektiren başka bir. Örneğin, hello tüketici uygulamaya Otomatik Sigorta sosyal veya yerel bir hesap ile oturum açabilirsiniz, ancak hello ev sigorta uygulamaya erişmeyi hello aynı kayıtlı önce hello telefon numarasını doğrulamanız gerekir dizin.
* Çok faktörlü kimlik doğrulaması tooaccess bir uygulamanın genel gerektirmez, ancak tooaccess hello hassas bölümleri içindeki gerektirir. Örneğin, hello tüketici tooa sosyal veya yerel hesabı ve onay hesap bakiyesini uygulamayla bankacılık oturum açabilirsiniz, ancak bir kablo aktarımı denemeden önce hello telefon numarasını doğrulamanız gerekir.

## <a name="modify-your-sign-up-policy-tooenable-multi-factor-authentication"></a>Kayıt İlkesi tooenable çok faktörlü kimlik doğrulaması değiştirme
1. [Bu adımları toonavigate toohello B2C özellikleri dikey hello Azure portalı üzerinde izleyin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. **Kaydolma ilkeleri**’ne tıklayın.
3. Kayıt İlkesi (örneğin, "B2C_1_SiUp") tooopen'ı tıklatın.
4. Tıklatın **çok faktörlü kimlik doğrulaması** ve hello **durumu** çok**ON**. **Tamam** düğmesine tıklayın.
5. Tıklatın **kaydetmek** hello dikey penceresinde hello üstünde.

Hello İlkesi tooverify hello tüketici deneyimi hello "Şimdi Çalıştır" özelliğini kullanabilirsiniz. Merhaba aşağıdakileri doğrulayın:

Merhaba çok faktörlü kimlik doğrulama adımı oluşmadan önce bir tüketici hesabı dizininizde oluşturulan. Merhaba adımı sırasında hello tüketici kendi telefon numarası ve doğrulamak tooprovide istedi. Doğrulama başarılı olursa, bağlı olduğu hello telefon numarası toohello tüketici hesabı daha sonra kullanmak için. Hello tüketici iptal eder ya da bırakır olsa bile, isterse bir telefon numarası yeniden sırasında hello sonraki oturum açma (multi-Factor Authentication etkinleştirildiğinde) tooverify sorulan.

## <a name="modify-your-sign-in-policy-tooenable-multi-factor-authentication"></a>Multi-Factor Authentication, oturum açma ilkesi tooenable değiştirme
1. [Bu adımları toonavigate toohello B2C özellikleri dikey hello Azure portalı üzerinde izleyin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Tıklatın **oturum açma ilkeleri**.
3. Oturum açma (örneğin, "B2C_1_SiIn") ilkesi tooopen'ı tıklatın. Tıklatın **Düzenle** hello dikey penceresinde hello üstünde.
4. Tıklatın **çok faktörlü kimlik doğrulaması** ve hello **durumu** çok**ON**. **Tamam** düğmesine tıklayın.
5. Tıklatın **kaydetmek** hello dikey penceresinde hello üstünde.

Hello İlkesi tooverify hello tüketici deneyimi hello "Şimdi Çalıştır" özelliğini kullanabilirsiniz. Merhaba aşağıdakileri doğrulayın:

Doğrulanmış telefon numarası bağlıysa hello Tüketici (bir sosyal veya yerel hesabı kullanarak), oturum açtığında toohello tüketici hesabı buldukça, tooverify istedi. Telefon numarası bağlıysa, hello tüketici tooprovide bir sorular ve onu doğrulayın. Başarılı doğrulamayı, bağlı olduğu hello telefon numarası toohello tüketici hesabı daha sonra kullanmak için.

## <a name="multi-factor-authentication-on-other-policies"></a>Diğer ilkeler çok faktörlü kimlik doğrulaması
Kaydolma ve oturum açma için ilkeler yukarıda açıklandığı gibi aynı zamanda olası tooenable çok faktörlü kimlik doğrulaması kaydolma olan veya ilkeleri ilkeler oturum açma ve parola sıfırlama. En kısa sürede ilkelerini düzenleme profilinde kullanıma sunulacaktır.

