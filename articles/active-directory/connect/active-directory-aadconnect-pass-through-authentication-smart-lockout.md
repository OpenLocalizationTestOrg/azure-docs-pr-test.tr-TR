---
title: "Azure AD Connect: Doğrudan kimlik doğrulaması - akıllı kilitleme | Microsoft Docs"
description: "Bu makalede, şirket içi hesaplarınızı Azure Active Directory (Azure AD) doğrudan kimlik doğrulama hello bulutta yanılma parola saldırılarından nasıl koruduğunu açıklanmaktadır."
services: active-directory
keywords: "Azure AD Connect doğrudan kimlik doğrulama, Active Directory yükleyin gerekli bileşenleri Azure AD, SSO, çoklu oturum açma"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: b02e315c3cc3eae00ca6408d735a416f34c2cdc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a>Azure Active Directory doğrudan kimlik doğrulaması: Akıllı kilitleme

## <a name="overview"></a>Genel Bakış

Azure AD yanılma parola saldırılarına karşı korur ve Office 365 ve SaaS uygulamalarını dışında kilitli orijinal kullanıcıların engeller. Adlı bu özelliği, **akıllı kilitleme**, oturum açma yönteminiz olarak doğrudan kimlik doğrulaması kullandığınızda desteklenir. Akıllı kilitleme tüm kiracılar için varsayılan olarak etkindir ve kullanıcı hesaplarınızı hello zaman koruyorsanız; hiçbir gerek tooturn yoktur üzerinde.

Başarısız oturum açma girişimleri izlemek tarafından ve belirli bir sonra Akıllı kilitleme çalışır **kilitleme eşiği**başlayan bir **kilitleme süresi**. Merhaba saldırgan hello kilitleme süresi sırasında tüm oturum açma denemeleri reddedilir. Merhaba saldırı devam ederse, daha uzun kilitleme süreleri sonucunda hello kilitleme süresi sona erdikten sonra hello sonraki başarısız oturum açma çalışır.

>[!NOTE]
>Merhaba kilitleme eşiği 10 başarısız oturum açma girişimlerinin ve kilitleme süresi 60 saniyedir hello varsayılan varsayılandır.

Akıllı kilitleme, oturum açma işlemleri orijinal kullanıcılar ve saldırganların ve çoğu durumda hello saldırganlar çıkışı yalnızca kilitleri arasında ayırır. Bu işlevsellik, orijinal kullanıcıları kötü amaçlı olarak kilitleme saldırganlar engeller. Oturum açma davranışı, kullanıcıların cihazları & tarayıcılar ve diğer sinyaller toodistinguish orijinal kullanıcılar ve saldırganların arasında geçen kullanırız. Biz sürekli bizim algoritmaları geliştirme.

Parola doğrulama isteklerini, şirket içi Active Directory (AD) üzerine doğrudan kimlik doğrulama ileten olduğundan, kullanıcılarınızın AD hesapları kilitleme tooprevent saldırganların gerekir. Kendi AD hesap kilitleme ilkeleri olduğundan (özellikle [ **hesap kilitleme eşiği** ](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) ve [ **hesap kilitleme sayaç sonra sıfırlamailkeleri** ](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), Azure AD tooconfigure kilitleme eşiği gerekir ve kilitleme süresi değerleri uygun şekilde saldırıları hello bulutta kullanıma toofilter şirket içi düşmeden önce AD.

>[!NOTE]
>Merhaba akıllı kilitleme özelliğini ücretsiz ve _üzerinde_ tüm müşteriler için varsayılan olarak. Ancak, Azure AD kilitleme eşiği ve grafik API'sini kullanarak kilitleme süresi değerleri değiştirme Kiracı toohave en az bir Azure AD Premium P2 lisansınızı gerekir. Bir Azure AD Premium P2 lisansı gerekmez _kullanıcı başına_ tooget hello akıllı kilitleme özelliğini doğrudan kimlik doğrulamasına sahip.

Kullanıcılarınızın AD hesapları şirket içi olduğunu tooensure iyi korumalı, tooensure gerekir:

1.  Azure AD kilitleme eşiği _daha az_ Reklamın hesap kilitleme eşiği değerinden. AD'ın hesap kilitleme eşiği en az iki ya da Azure AD kilitleme eşiği üç kez şekilde hello değerleri ayarlamanızı öneririz.
2.  Azure AD kilitleme süresi (saniye cinsinden gösterilir) _uzun_ Reklamın sıfırlama hesap kilitleme sayaç (dakika cinsinden gösterilir) sonra daha.

## <a name="verify-your-ad-account-lockout-policies"></a>AD hesap kilitleme ilkeleri doğrulayın

Aşağıdaki yönergeler tooverify hello AD hesap kilitleme ilkeleri kullanın:

1.  Merhaba Grup İlkesi yönetim aracını açın.
2.  Örneğin, uygulanan tooall kullanıcılar olan hello Grup İlkesi hello varsayılan etki alanı ilkesi düzenleyin.
3.  TooComputer Yapılandırması\İlkeler\Windows Ayarları\Güvenlik Ayarları\Hesap İlkeleri\Hesap kilitleme ilkesi gidin.
4.  Hesap kilitleme eşiği ve hesap kilitleme sayaç sonra sıfırlama değerleri doğrulayın.

![AD ve hesap kilitleme ilkeleri](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-hello-graph-api-toomanage-your-tenants-smart-lockout-values"></a>Merhaba grafik API'si toomanage, kiracının akıllı kilitleme değerlerini kullanın

>[!IMPORTANT]
>Azure AD kilitleme eşiği ve grafik API'sini kullanarak kilitleme süresi değerleri değiştirerek bir Azure AD Premium P2 özelliğidir. Bu ayrıca, toobe kiracınızın genel yönetici gerekir.

Kullanabileceğiniz [Graph Explorer'a](https://developer.microsoft.com/graph/graph-explorer) tooread, ayarlayın ve Azure AD akıllı kilitleme değerlerini güncelleştirin. Ancak, bu işlemlerin program aracılığıyla da yapabilirsiniz.

### <a name="read-smart-lockout-values"></a>Okuma akıllı kilitleme değerleri

Bu adımları tooread, kiracının akıllı kilitleme değerleri izleyin:

1. Graph Explorer'a kiracınızın genel yönetici olarak oturum açın. İstenirse, hello için erişim izni ver izinleri istedi.
2. "İzinlerini değiştirme"'i tıklatın ve hello "Directory.ReadWrite.All" izni seçin.
3. Merhaba grafik API'si istek gibi yapılandırma: kümesi versiyonunu çok "BETA" istek türü çok "GET" ve URL çok`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.
4. "Sorgu Çalıştır" toosee, kiracının akıllı kilitleme değerler'i tıklatın. Önce kiracının değerleri ayarlamadıysanız boş bakın.

### <a name="set-smart-lockout-values"></a>Akıllı kilitleme değerlerini Ayarla

Bu adımları tooset, kiracının akıllı kilitleme değerlerini (Merhaba yalnızca ilk kez) izleyin:

1. Graph Explorer'a kiracınızın genel yönetici olarak oturum açın. İstenirse, hello için erişim izni ver izinleri istedi.
2. "İzinlerini değiştirme"'i tıklatın ve hello "Directory.ReadWrite.All" izni seçin.
3. Merhaba grafik API'si istek gibi yapılandırma: kümesi versiyonunu çok "BETA" istek türü çok "POST" ve URL çok`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.
4. JSON istek hello "İstek gövdesi" alanına aşağıdaki hello kopyalayıp yeniden açın. Merhaba akıllı kilitleme değerlerini uygun şekilde değiştirin ve kullanmak için rastgele bir GUID `templateId`.
5. "Sorgu Çalıştır" tooset, kiracının akıllı kilitleme değerler'i tıklatın.

```
{
  "templateId": "5cf42378-d67d-4f36-ba46-e8b86229381d",
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "300"
    },
    {
      "name": "LockoutThreshold",
      "value": "5"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

>[!NOTE]
>Bunları kullanmıyorsanız hello bırakabilirsiniz **BannedPasswordList** ve **EnableBannedPasswordCheck** değerler boş olarak ("") ve "false" sırasıyla.

Doğru kullanarak, kiracının akıllı kilitleme değerleri ayarladığınızdan emin olun [adımları](#read-smart-lockout-values).

### <a name="update-smart-lockout-values"></a>Akıllı kilitleme değerleri güncelleştirin

(Önceden daha önce ayarlamış olmanız ise) bu adımları tooupdate, kiracının akıllı kilitleme değerleri izleyin:

1. Graph Explorer'a kiracınızın genel yönetici olarak oturum açın. İstenirse, hello için erişim izni ver izinleri istedi.
2. "İzinlerini değiştirme"'i tıklatın ve hello "Directory.ReadWrite.All" izni seçin.
3. [Bu adımları tooread, kiracının akıllı kilitleme değerlerini izleyin](#read-smart-lockout-values). Kopya hello `id` "PasswordRuleSettings" olarak "görünen adı" Merhaba öğesinin değeri (GUID).
4. Hello grafik API'si istek gibi yapılandırma: sürümü çok Ayarla "BETA" çok istek türü "Düzeltme Eki" ve URL çok`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` -kullanmak için adım 3 GUID hello `<id>`.
5. JSON istek hello "İstek gövdesi" alanına aşağıdaki hello kopyalayıp yeniden açın. Merhaba akıllı kilitleme değerleri uygun şekilde değiştirin.
6. "Sorgu Çalıştır" tooupdate, kiracının akıllı kilitleme değerler'i tıklatın.

```
{
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "30"
    },
    {
      "name": "LockoutThreshold",
      "value": "4"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

Doğru kullanarak, kiracının akıllı kilitleme değerleri güncelleştirilmiş doğrulamak [adımları](#read-smart-lockout-values).

## <a name="next-steps"></a>Sonraki adımlar
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - yeni özellik istekleri dosyalama için.
