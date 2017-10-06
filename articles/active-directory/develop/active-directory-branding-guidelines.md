---
title: "aaaBranding uygulamalar için yönergeleri | Microsoft Docs"
description: "Azure Active Directory için kapsamlı bir kılavuz toodeveloper yönelimli kaynakları"
services: active-directory
documentationcenter: dev-center-name
author: skwan
manager: mbaldwin
editor: 
ms.assetid: 72f4e464-1352-4a49-a18f-c37f58e7d5c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: skwan
ms.custom: aaddev
ms.openlocfilehash: e43f884c736a0dcb2e6e51293962ef1e2636ad70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="branding-guidelines-for-applications"></a>Uygulamalar için markalama talimatları
Bu konuda, Azure Active Directory (Azure AD) ile uygulamaları geliştirirken kullanması gereken yönergeleri markalama hello anlatılmaktadır. Bu yönergeleri toouse, iş veya Okul hesabı, Azure AD'de yönetilen veya kişisel hesabıyla oturum açma ve kaydolma tooyour uygulama için istedikleri zaman müşterilerinize doğrudan yardımcı olur.

## <a name="personal-accounts-vs-work-or-school-accounts-from-microsoft"></a>Microsoft iş ve kişisel hesapları veya Okul
Microsoft, iki tür kullanıcı hesaplarının yönetir:

* **Kişisel hesaplar** (eski adıyla Windows Live ID olarak). Bu hesapları arasındaki ilişkiyi hello temsil *tek tek* kullanıcılar, Microsoft ve misiniz kullanılan tooaccess tüketici cihazlarının ve Microsoft Hizmetleri. Bu hesapları kişisel kullanım için tasarlanmıştır.
* **İş veya Okul hesapları.** Bu hesaplar, Azure Active Directory kullanan kuruluşlar adına Microsoft tarafından yönetilir. Bu tooOffice 365 ve Microsoft'a ait diğer iş hizmetlerini kullanılan toosign hesaplarıdır.

İş veya Okul hesapları olan genellikle Microsoft kuruluşlarına (şirket, okul, devlet dairesi) tarafından tooend kullanıcıların (çalışanlar, Öğrenciler, federal çalışan) atanır. Ya da doğrudan hello bulutta hello Azure AD platformu ya da Windows Server Active Directory gibi bir şirket içi Directory'den eşitlenen tooAzure AD içinde yönetilen bu hesaplarıdır. Microsoft, hello *koruyucu* hello iş veya Okul hesapları ancak hello hesapları ait ve hello kuruluşu tarafından denetlenir.

## <a name="referring-tooazure-ad-accounts-in-your-application"></a>Uygulamanızdaki başvuran tooAzure AD hesapları
Microsoft Azure son kullanıcılar toohello veya hello Active Directory marka ve ikisi, aşağıdakileri yapmalısınız açığa çıkarmıyor.

* Kullanıcı oturum açtıktan sonra hello kuruluşunuzun adını ve logosunu mümkün olduğunca kullanmanız gerekir. Bu, "kuruluşunuzun" gibi genel koşulları kullanmaktan daha iyidir.
* Kullanıcılar oturum zaman tootheir hesapları olarak başvurmalıdır "iş veya Okul hesapları" ve kullanım hello Microsoft logosu tooconvey bu hesapları Microsoft tarafından yönetilir. Kullanıcı karışıklığı oluşturan koşulları "Kuruluş hesabı", "iş hesabı" veya "şirket hesabı" gibi kullanmayın.

## <a name="user-account-pictogram"></a>Kullanıcı hesabı piktogram
Bu yönergeleri önceki sürümünde, "mavi rozet" piktogram kullanarak önerilir. Kullanıcı ve geliştirici geri bildirimi doğrultusunda, şimdi hello Microsoft logosu hello kullanımını yerine öneririz. Bu, kullanıcıların Office 365 veya diğer Microsoft iş Hizmetleri toosign tooyour uygulamasında kullandıkları hello hesabı yeniden kullanabilir anlamasına yardımcı olur.

## <a name="signing-up-and-signing-in-with-azure-ad"></a>Kaydolan ve Azure AD ile imzalama
Uygulamanıza kaydolma ve oturum açma için ayrı yollar mevcut ve her iki senaryoları için görsel kılavuz bölümleri aşağıdaki hello sağlayın.

**Uygulamanız (örneğin ücretsiz tootrial veya freemium modeli gibi) son kullanıcı kayıt destekliyorsa**: göstermek bir **oturum açma** kendi iş hesabını veya kişisel hesabıyla uygulamanızla kullanıcıların tooaccess sağlayan düğmeyi. Azure AD uygulamanızı eriştiklerinde ilk kez bir onay istemi hello gösterir.

**Uygulamanızı yalnızca yöneticileri onayı izinleri gerektiriyorsa ya da uygulamanızı kuruluş lisanslama gerektiriyorsa**: kullanıcı oturum açma yönetici alımdaki ayırın. Merhaba **"Bu uygulamayı Al" düğmesini** admins toosign yeniden yönlendirme sonra kullanıcılar kuruluşlarındaki adına toogrant izin isteyin. Bu sahip Merhaba, son kullanıcıların onay istekleri tooyour uygulama gizleme avantaj.

## <a name="visual-guidance-for-app-acquisition"></a>Uygulama alım için görsel kılavuz
"Hello uygulamayı Al" bağlantı hello kullanıcı toohello Azure AD erişime yönlendirme gerekir (yetkilendirme) sayfası, tooallow bir kuruluşun Yöneticisi tooauthorize uygulama toohave Microsoft tarafından barındırılan tootheir kuruluşunuzun verilere erişebilir. Toorequest erişim hello tartışılır nasıl Ayrıntılar [Azure Active Directory Tümleştirme uygulamalarla](active-directory-integrating-applications.md) makalesi.

Yöneticileri tooyour uygulama kabul edildikten sonra tooadd seçebilirsiniz, tootheir kullanıcıların Office 365 uygulama Başlatıcı deneyimi (Merhaba waffle'ndan ve erişilebilir [https://portal.office.com/myapps](https://portal.office.com/myapps)). Bu özellik tooadvertise isterseniz, "Bu uygulama tooyour kuruluş Ekle" ve böyle bir düğme Göster gibi koşulları kullanabilirsiniz:

![Uygulama türleri ve senaryolar](./media/active-directory-branding-guidelines/add-to-my-org.png)

Ancak, düğmeleri kalmak yerine açıklayıcı metin yazma öneririz. Örneğin:

> *Office 365 veya Microsoft'un diğer iş hizmeti zaten kullanıyorsanız, yalnızca < your_app_name > erişim tooyour kuruluşunuzun verilerini verebilirsiniz. Bu, kullanıcıların tooaccess < your_app_name > var olan kullanıcılar iş hesaplarını olanak tanır.*
> 
> 

## <a name="visual-guidance-for-sign-in"></a>Oturum açma için görsel kılavuz
Uygulamanızı Azure AD ile toointegrate kullandığınız toohello Protokolü karşılık gelen kullanıcılar toohello oturum açma uç noktası yönlendiren düğmesinin işareti görüntülemelidir. bölümden hello ne bu düğme gibi görünmelidir ayrıntılar sağlar.

### <a name="pictogram-and-sign-in-with-microsoft"></a>Piktogram ve "Microsoft ile oturum"
Azure AD uygulamanızı destekleyebilir diğer kimlik sağlayıcılardan arasında benzersiz olarak temsil eden hello ilişkilendirme hello Microsoft logosu hello "Sign in ile Microsoft" hüküm ve kullanıcının. "Oturum in ile Microsoft" yeterli alan yoksa, bu çok "oturum açın" Tamam tooshorten var.

![Uygulama türleri ve senaryolar](./media/active-directory-branding-guidelines/sign-in-with-microsoft-light.png)

![Uygulama türleri ve senaryolar](./media/active-directory-branding-guidelines/sign-in-light.png)

Koyu Renk düzenini hello düğmeleri için de kullanabilirsiniz.

![Uygulama türleri ve senaryolar](./media/active-directory-branding-guidelines/sign-in-with-microsoft-dark.png)

![Uygulama türleri ve senaryolar](./media/active-directory-branding-guidelines/sign-in-dark.png)

## <a name="branding-dos-and-donts"></a>Marka yapılması ve yapılmaması gerekenler
**YAPMAK** "iş veya Okul hesabı kullan" hello "Sign in ile Microsoft" düğmesine tooprovide ek açıklama toohelp son kullanıcılar ile birlikte tanıması bunu kullanıp kullanmayacağınızı. **Verme** "Kuruluş hesabı", "iş hesabı" veya "şirket hesabı." gibi diğer kullanım koşulları

**Verme** "Office 365 ID" veya "Azure kimliği" kullanın. Office 365 de hello Azure AD kimlik doğrulaması için kullanmayan bir Microsoft sunan bir tüketici adıdır.

**Verme** hello Microsoft logosu alter.

**Verme** son kullanıcılar toohello Azure veya Active Directory markalar kullanıma sunar. Ancak Tamam toouse geliştiriciler, BT uzmanları ve Yöneticiler bu koşulları.

## <a name="navigation-dos-and-donts"></a>Gezinti yapılması ve yapılmaması gerekenler
**YAPMAK** kullanıcılar toosign için bir yol sağlar ve geçiş tooanother kullanıcı hesabı. Kişiler, genellikle çoğu kişi Microsoft/Facebook/Google/Twitter tek bir kişisel hesabından olmakla birlikte, birden fazla kuruluşla ilişkilendirilir. Çoklu oturum açmış kullanıcı desteği yakında geliyor.

