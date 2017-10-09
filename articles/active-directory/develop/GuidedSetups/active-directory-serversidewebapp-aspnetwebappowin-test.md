---
title: aaaAzure AD v2 ASP.NET Web sunucusu Getting Started - Test | Microsoft Docs
description: "Microsoft oturum açma Openıd Connect standardını kullanan geleneksel web tarayıcı tabanlı bir uygulama ile ASP.NET çözümünü uygulama"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 99c7525b9146605142180962fc2a61b3c953c064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Kodunuzu test

Tuşuna `F5` toorun projenizi Visual Studio'da. Merhaba tarayıcı açılır ve çok doğrudan*http://localhost: {port}* burada göreceksiniz hello *oturum oturum Microsoft* düğmesi. Bir tane de toosign'ı tıklatın.

Hazır tootest, bir iş, okul (Azure Active Directory) veya (live.com, outlook.com) kişisel hesap toosign içinde kullanım olduğunuzda. 

![Microsoft tarayıcı penceresi ile oturum aç](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Microsoft tarayıcı penceresi ile oturum aç](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a>Beklenen sonuçları
Oturum açma işleminden sonra hello yeniden yönlendirilen toohello giriş sayfası, web sitenizin hello HTTPS uygulama kayıt bilgilerinizi hello Microsoft uygulama kayıt Portalı'nda belirtilen URL olan kullanıcıdır. Bu sayfayı artık gösterir *Hello {User}* ve bir bağlantı toosign genişletme ve bir bağlantı toohello Authorize denetleyicisi bağlantı toosee hello kullanıcının talepleri – oluşturduğunuz.

### <a name="see-users-claims"></a>Kullanıcının talepleri bakın
Merhaba köprü toosee hello kullanıcının talepleri seçin. Bu, toohello denetleyici ve yalnızca kimlik doğrulaması kullanılabilir toousers görünüm sağlar.

#### <a name="expected-results"></a>Beklenen sonuçları
 Merhaba oturum açmış kullanıcı hello temel özelliklerini içeren bir tablo görmeniz gerekir:

| Özellik | Değer | Açıklama|
|---|---|---|
| Ad | {Tam} kullanıcı adı | Merhaba kullanıcı adı ve Soyadı
|Kullanıcı adı | <span>user@domain.com</span>| kullanılan tooidentify hello oturum açmış kullanıcı Hello kullanıcı adı
| Konu| {Konu}|Bir dize toouniquely hello web üzerinden hello kullanıcı oturum açma tanımlayın|
| Kiracı Kimliği| {GUID}| A *GUID* toouniquely hello kullanıcının Azure Active Directory kuruluş temsil eder.|

Ayrıca, kimlik doğrulama isteğine dahil tüm kullanıcı talepleri de dahil olmak üzere bir tablo görürsünüz. Tüm talep bir belirteç kimliği ve açıklama listesi için lütfen bkz [makale](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "listesi, talepleri kimliği belirteci").


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a>Test içeren bir yöntem erişen bir *[Authorize]* özniteliği (isteğe bağlı)
Bu adımda, anonim kullanıcı olarak erişen hello kimliği doğrulanmış denetleyicisi sınayacak:<br/>
Merhaba bağlantı toosign kullanıma hello kullanıcı ve tam hello oturum kapatma işlemini seçin.<br/>
Şimdi, tarayıcıda http://localhost yazın: {port} / tooaccess hello ile korunan denetleyicinizi kimliği doğrulanmış `[Authorize]` özniteliği

#### <a name="expected-results"></a>Beklenen sonuçları
Tooauthenticate toosee hello görünüm gerektiren hello istemi almanız gerekir.

## <a name="additional-information"></a>Ek bilgiler

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a>Tüm web sitenize koruma
tooprotect tüm web sitenizin hello eklemek `AuthorizeAttribute` çok`GlobalFilters` içinde `Global.asax` `Application_Start` yöntemi:

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> **Nasıl tooyour uygulamada yalnızca bir kuruluş toosign toorestrict kullanıcılardan**

> Varsayılan olarak, herhangi bir şirket veya Azure Active Directory ile tümleşik olan kuruluşunuzun iş ve Okul hesaplarını yanı sıra kişisel hesaplar (dahil olmak üzere outlook.com, live.com ve diğerleri) oturum açma tooyour uygulama. 

> Merhaba, uygulama tooaccept oturum açma işlemleri yalnızca bir Azure Active Directory kuruluştan isterseniz, değiştirmek `Tenant` parametresinde *web.config* gelen `Common` hello kuruluşun – toohello Kiracı adı örnek, *contoso.onmicrosoft.com*. Bundan sonra hello değiştirme `ValidateIssuer` bağımsız değişkeni, *OWIN başlangıç sınıfı* çok`true`.

> yalnızca belirli kuruluşların listesi tooallow kullanıcılardan ayarlamak `ValidateIssuer` tootrue ve kullanım hello `ValidIssuers` parametresi toospecify kuruluşların listesi.

> Başka bir seçenek IssuerValidator parametresini kullanarak toovalidate hello verenler tooimplement özel bir yöntem olduğu. Hakkında daha fazla bilgi için `TokenValidationParameters`, lütfen bkz [bu](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "tokenvalidationparameters değerini MSDN makalesine") MSDN makalesi.

