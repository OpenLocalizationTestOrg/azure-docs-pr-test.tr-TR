---
title: "Active Directory aaaAzure v2.0 uç noktası sınırlamaları ve kısıtlamaları | Microsoft Docs"
description: "Sınırlamalar ve kısıtlamalarla hello Azure AD v2.0 uç noktası için listesi."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: a99289c0-e6ce-410c-94f6-c279387b4f66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: bcbb7239f1d117002d16ac23dca8f1feb13a9161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="should-i-use-hello-v20-endpoint"></a>Merhaba v2.0 uç kullanmalıyım?
Azure Active Directory ile tümleştirme uygulamalar oluştururken, hello v2.0 uç noktası ve kimlik doğrulama protokolleri gereksinimlerinizi karşılayıp karşılamadığını toodecide gerekir. Azure Active Directory'nin özgün uç nokta hala tam olarak desteklenir ve bazı bakımlardan v2.0'den daha fazla özellik zengin değil. Ancak, v2.0 uç hello [önemli avantajlar sunar](active-directory-v2-compare.md) geliştiriciler için.

Geliştiriciler için bu anda Basitleştirilmiş Bizim önerimiz şöyledir:

* Uygulamanızda kişisel Microsoft hesapları desteklemesi gerekiyorsa hello v2.0 uç kullanın. Ancak bunu yapmadan önce bu makalede aşağıdakiler ele hello kısıtlamaları anladığınızdan emin olun.
* Toosupport Microsoft iş ve Okul hesapları yalnızca uygulamanız gerekiyorsa, hello v2.0 uç nokta kullanmayın. Bunun yerine, tooour başvuran [Azure AD Geliştirici Kılavuzu](active-directory-developers-guide.md).

Her zaman sadece toouse hello v2.0 uç gerekir böylece zamanla tooeliminate hello kısıtlamaları burada listelenen hello v2.0 uç büyüyecektir. Hello bu arada, bu makalede hello v2.0 uç sizin için uygun olup olmadığını belirlemek hedeflenen toohelp ' dir. Biz bu makalede tooreflect hello geçerli durumunu hello v2.0 uç tooupdate devam eder. Geri tooreevaluate gereksinimlerinizi v2.0 yetenekleri karşı denetleyin.

Merhaba v2.0 uç kullanmaz var olan bir Azure AD uygulaması varsa, hiçbir gerek toostart sıfırdan yoktur. Hello gelecekteki, biz bir yolu, toouse için var olan Azure AD uygulamalarınız hello v2.0 uç noktası ile sağlar.

## <a name="restrictions-on-app-types"></a>Uygulama türleri kısıtlamalar
Şu anda hello aşağıdaki uygulama türlerini hello v2.0 uç noktası tarafından desteklenmez. Desteklenen uygulama türleri açıklaması için bkz: [hello Azure Active Directory v2.0 uç noktası için uygulama türleri](active-directory-v2-flows.md).

### <a name="standalone-web-apis"></a>Tek başına Web API'leri
Merhaba v2.0 uç kullanabileceğine[güvenli bir Web API OAuth 2.0 ile derleme](active-directory-v2-flows.md#web-apis). Ancak, bu Web API belirteçleri, aynı uygulama kimliği hello olan bir uygulamadan alabilirsiniz Farklı bir uygulama kimliği sahip bir istemciden bir Web API erişemiyor Merhaba istemci olmaz mümkün toorequest olması veya izinleri tooyour Web API alın.

toobuild sahip bir istemciden gelen belirteçleri hello aynı uygulama kimliği, kabul eden bir Web API'sini nasıl görürüm toosee hello v2.0 uç noktası Web API örnekleri bizim [Başlarken](active-directory-appmodel-v2-overview.md#getting-started) bölümü.

## <a name="restrictions-on-app-registrations"></a>Uygulama kayıtlar kısıtlamalar
Şu anda toointegrate hello v2.0 uç noktası ile istediğiniz her uygulama için bir uygulama kaydı hello yeni oluşturmalısınız [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList). Var olan Azure AD veya Microsoft hesabı uygulamaları hello v2.0 uç noktası ile uyumlu değil. Merhaba uygulama kayıt portalı dışındaki herhangi bir portal kaydedilmiş uygulamaları hello v2.0 uç noktası ile uyumlu değildir. Hello gelecekteki, tooprovide şekilde toouse v2.0 uygulama olarak mevcut bir uygulama planlayın. Şu anda, yine de yoktur hello v2.0 uç noktası ile var olan bir uygulama toowork için geçiş yol yok.

Ayrıca, hello oluşturduğunuz uygulama kayıtlar [uygulama kayıt portalı](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) uyarılar aşağıdaki hello vardır:

* Yalnızca iki uygulama sırrı uygulama kimliği izin verilen
* Kişisel bir Microsoft hesabı olan bir kullanıcı tarafından kaydedilen bir uygulama kaydı görüntülenebilir ve yalnızca bir tek Geliştirici hesabı tarafından yönetilebilir. Birden çok geliştiriciler arasında paylaşılamaz.  Tooshare isterseniz, uygulama kaydı birden çok geliştiriciler arasında hello kayıt portalı bir Azure AD hesapla içine imzalayarak hello uygulaması oluşturabilirsiniz.
* Merhaba yeniden yönlendirme izin URI hello biçimi birkaç kısıtlamalar vardır. Yeniden yönlendirme URI'ler hakkında daha fazla bilgi için hello sonraki bölümüne bakın.

## <a name="restrictions-on-redirect-uris"></a>Yeniden yönlendirme URI'ler kısıtlamalar
Şu anda hello uygulama kayıt portalı kayıtlı uygulamalar sınırlı kısıtlı tooa yeniden yönlendirme URI'si değerler kümesidir. web uygulamaları ve Hizmetleri için URI hello düzeniyle başlamalıdır yeniden yönlendirme hello `https`, ve tüm yeniden yönlendirme URI'si değerler tek bir DNS etki alanı paylaşması gerekir. Örneğin, bu yeniden yönlendirme URI'ler biri sahip bir web uygulaması kaydedilemiyor:

`https://login-east.contoso.com`  
`https://login-west.contoso.com`

Merhaba kayıt sistem hello tam DNS adını hello varolan yeniden yönlendirme URI'si toohello DNS adını hello yeniden yönlendirme eklemekte olduğunuz URI karşılaştırır. Aşağıdakilerden hello aşağıdaki koşullar doğruysa hello isteği tooadd hello DNS adı başarısız olur:  

* Merhaba tam DNS adını hello yeni yeniden yönlendirme URI'si hello varolan yeniden yönlendirme URI'si hello DNS adı eşleşmiyor.
* Merhaba yeni yeniden yönlendirme URI'si Hello tam DNS adı bir alt etki alanı hello varolan yeniden yönlendirme URI'si değil.

Örneğin, Hello uygulamanın bu yeniden yönlendirme URI'si varsa:

`https://login.contoso.com`

Bu gibi tooit ekleyebilirsiniz:

`https://login.contoso.com/new`

Bu durumda, hello DNS adı tam olarak eşleşir. Ya da şunu yapabilirsiniz:

`https://new.login.contoso.com`

Bu durumda, login.contoso.com tooa DNS alt etki başvuran. Oturum açma east.contoso.com ve oturum açma-west.contoso.com URI'ler yeniden yönlendirme olarak bir uygulama toohave istiyorsanız, bu URI şu sırayla yeniden yönlendirme eklemeniz gerekir:

`https://contoso.com`  
`https://login-east.contoso.com`  
`https://login-west.contoso.com`  

Merhaba iki hello alt etki alanlarına olduklarından ilk yeniden yönlendirme URI'si, ikinci ekleyebilirsiniz contoso.com. Bu sınırlama gelecek sürümde kaldırılacak.

Merhaba uygulama kayıt portalı uygulamasında bir tooregister nasıl görürüm toolearn [nasıl tooregister hello v2.0 uç noktası ile uygulama](active-directory-v2-app-registration.md).

## <a name="restrictions-on-services-and-apis"></a>Hizmetleri ve API üzerindeki kısıtlamaları
Şu anda hello v2.0 uç oturum açma için hello uygulama kayıt portalı kayıtlı ve hello listesinde iner herhangi bir uygulama destekler [kimlik doğrulaması akışı desteklenen](active-directory-v2-flows.md). Ancak, bu uygulamaları çok sınırlı bir kaynak kümesi için OAuth 2.0 erişim belirteçleri elde edebilirsiniz. Merhaba v2.0 uç noktası sorunlarını belirteçleri yalnızca erişim:

* Merhaba belirteci istenen hello uygulama. Merhaba mantıksal uygulama birkaç farklı bileşenler veya katmanları oluşuyorsa uygulama kendisi için bir erişim belirteci alması. toosee bu senaryo, eylemde kullanıma bizim [Başlarken](active-directory-appmodel-v2-overview.md#getting-started) öğreticileri.
* Merhaba Outlook posta, Takvim ve kişiler REST API'leri, her biri https://outlook.office.com bulunur. toolearn nasıl toowrite bu API'leri erişen bir uygulama bkz hello [Office Başlarken](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2) öğreticileri.
* Microsoft Graph API. Hakkında daha fazla bilgiyi [Microsoft Graph](https://graph.microsoft.io) ve kullanılabilir tooyou hello verileri.

Şu anda başka bir hizmetler desteklenir. Daha fazla Microsoft Online Services hello gelecekteki, ayrıca toosupport kendi özel olarak geliştirilmiş Web API'leri ve Hizmetleri için eklenir.

## <a name="restrictions-on-libraries-and-sdks"></a>Kitaplıklar ve SDK'ları üzerindeki kısıtlamaları
Şu anda hello v2.0 uç noktası için kitaplık desteği sınırlıdır. Bir üretim uygulamasında toouse hello v2.0 uç istiyorsanız, bu seçenekler vardır:

* Bir web uygulaması oluşturuyorsanız, Microsoft, genel olarak kullanılabilir sunucu tarafı Ara tooperform oturum açma ve belirteç doğrulama güvenli bir şekilde kullanabilirsiniz. Bunlar, ASP.NET ve Node.js Passport eklenti hello için hello Open ID Connect OWIN ara yazılımı içerir. Microsoft Ara kullanmak kod örnekleri için bkz: bizim [Başlarken](active-directory-appmodel-v2-overview.md#getting-started) bölümü.
* Masaüstü ve mobil uygulama geliştiriyorsanız, önizlememiz Microsoft kimlik doğrulama kitaplıkları (MSAL) birini kullanabilirsiniz.  Güvenli toouse olacak şekilde Bu kitaplıklar üretim desteklenen bir önizlemede bulunan üretim uygulamaları bunları. Merhaba hello koşulları hakkında daha fazla Önizleme ve kullanılabilir kitaplıklarında hello okuyabilir bizim [kimlik doğrulama kitaplıkları başvuru](active-directory-v2-libraries.md).
* Microsoft kitaplıkları tarafından kapsanmayan platformları için doğrudan uygulama kodunuzda protokolü ileti alma ve gönderme tarafından hello v2.0 uç noktası ile tümleştirebilirsiniz. Merhaba v2.0 Openıd Connect ve OAuth protokollerini [açıkça belgelenmiş](active-directory-v2-protocols.md) toohelp bu tür bir tümleştirme gerçekleştirin.
* Son olarak, açık kaynaklı açmak ID Connect ve OAuth kitaplıkları toointegrate hello v2.0 uç noktası ile kullanabilirsiniz. Merhaba v2.0 protokol önemli bir değişiklik yapılmadan birçok açık kaynak Protokolü kitaplıkları ile uyumlu olmalıdır. Bu tür kitaplıklarının Hello kullanılabilirlik dile ve platforma göre değişir. Merhaba [Open ID Connect](http://openid.net/connect/) ve [OAuth 2.0](http://oauth.net/2/) Web siteleri korumak popüler uygulamaları listesi. Daha fazla bilgi için bkz: [Azure Active Directory v2.0 ve kimlik doğrulama kitaplıkları](active-directory-v2-libraries.md)ve açık kaynak istemci kitaplıkları ve hello v2.0 uç noktası ile test örnekleri hello listesi.

## <a name="restrictions-on-protocols"></a>Protokolleri kısıtlamalar
Merhaba v2.0 uç SAML veya WS-Federasyon desteklemiyor; yalnızca, Open ID Connect ve OAuth 2.0 de destekler.  Tüm özellikleri ve yetenekleri OAuth kurallarının hello v2.0 uç eklenmiştir. Şu anda bu protokolü özellikleri ve yetenekleri olan *kullanılamaz* hello v2.0 uç noktada:

* Merhaba v2.0 uç noktası tarafından verilen kimlik belirteçlerini içermez bir `email` hello kullanıcı tooview izni e-postasını alma olsa bile hello kullanıcı için talep.
* Merhaba Openıd Connect kullanıcı bilgisi endpoint hello v2.0 uç uygulanmadı. Ancak, büyük olasılıkla bu uç noktada alacağı tüm kullanıcı profil verileri kullanılabilir Microsoft Graph hello `/me` uç noktası.
* Merhaba v2.0 uç veren rol veya Grup Talep Kimliği belirteçleri desteklemez.
* Merhaba [OAuth 2.0 kaynak sahibi parolası kimlik bilgilerini verme](https://tools.ietf.org/html/rfc6749#section-4.3) hello v2.0 uç noktası tarafından desteklenmiyor.

Addtion içinde hello SAML herhangi bir biçimi veya WS-Federasyon protokolleri hello v2.0 uç desteklemez.

toobetter hello v2.0 uç okuyun, desteklenen protokol işlevselliği hello kapsamını anlamanız bizim [Openıd Connect ve OAuth 2.0 protokolü başvurusu](active-directory-v2-protocols.md).

## <a name="restrictions-for-work-and-school-accounts"></a>İş ve Okul hesapları için kısıtlamalar
Windows uygulamalarında Active Directory Authentication Library (ADAL) kullandıysanız, hello güvenlik onaylama işlemi biçimlendirme dili (SAML) onaylama grant kullanan Windows tümleşik kimlik doğrulaması, avantajlarından gerçekleştirilecek. Bu verme ile Federasyon kullanıcıları, Azure AD kiracılar sessizce kimliğini kendi şirket içi Active Directory örneği ile kimlik bilgileri girmeden. Şu anda hello SAML onaylama grant hello v2.0 uç üzerinde desteklenmiyor.
