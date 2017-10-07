---
title: "Azure AD'de aaaUnderstanding hello OAuth2 örtük izin akışı | Microsoft Docs"
description: "Merhaba OAuth2 örtük grant akış, Azure Active Directory'nin uygulaması hakkında daha fazla bilgi ve uygulamanız için uygun olup."
services: active-directory
documentationcenter: dev-center-name
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 90e42ff9-43b0-4b4f-a222-51df847b2a8d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/15/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 3402e6619709e1a5b1e790ffd79dc62139552d9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-oauth2-implicit-grant-flow-in-azure-active-directory-ad"></a>Anlama hello OAuth2 örtük izin akışı içinde Azure Active Directory (AD)
Merhaba OAuth2 örtük verme hello grant listesiyle hello uzun güvenlik sorunlarının hello OAuth2 belirtimi olması için notorious olur. Ve henüz, ADAL JS ve hello bir SPA uygulamaları yazarken öneririz tarafından uygulanan hello yaklaşımdır. Neler sağlar? Tüm sağlasa da, bileşim olduğu: ve ortaya çıkmıştır gibi hello örtük grant tarayıcıdan JavaScript aracılığıyla bir Web API kullanan uygulamalar için pursue hello en iyi yaklaşımdır.

## <a name="what-is-hello-oauth2-implicit-grant"></a>Merhaba OAuth2 örtük grant nedir?
Merhaba quintessential [OAuth2 yetkilendirme kodu verme](https://tools.ietf.org/html/rfc6749#section-1.3.1) iki ayrı uç noktaları kullanan hello yetkilendirme verme olur. Merhaba yetkilendirme uç noktası, bir kimlik doğrulama kodu sonuçları hello kullanıcı etkileşimi aşaması için kullanılır. Merhaba belirteç uç noktası hello istemci tarafından kullanılır ve bir erişim belirteci ve genellikle de bir yenileme belirteci hello kodunu değişimi için. Web uygulamaları hello yetkilendirme sunucusu hello istemci doğrulayabilir, kendi uygulama kimlik bilgilerini toohello belirteç uç noktası, gerekli toopresent demektir.

Merhaba [OAuth2 örtük grant](https://tools.ietf.org/html/rfc6749#section-1.3.2) bir diğer yetkilendirme verir çeşididir. Bir erişim belirteci istemci tooobtain sağlar (ve kullanırken id_token [Openıd Connect](http://openid.net/specs/openid-connect-core-1_0.html)) hello belirteç uç noktası arayarak veya hello istemci kimlik doğrulaması olmadan doğrudan hello yetkilendirme uç noktasından,. Bu değişken JavaScript tabanlı bir Web tarayıcısında çalışan uygulamaları için özel olarak tasarlanmıştır: hello özgün OAuth2 belirtiminde belirteçleri URI parçadaki döndürülür. Merhaba istemcisinde kullanılabilir toohello JavaScript kodu hello belirteci BITS yapıyorsa, ancak yeniden yönlendirmeleri hello sunucu doğru olarak eklenmeyecek güvence altına alır. Tarayıcı yoluyla belirteçleri döndürme doğrudan hello yetkilendirme uç noktasından yönlendirir. Ayrıca, tüm gereksinimleri hello JavaScript uygulama gerekli toocontact hello belirteç uç noktası ise gereklidir kaynak çağrıları çapraz ortadan hello avantajına sahiptir.

Bir önemli hello OAuth2 örtük grant böyle akışlar, yenileme belirteçleri toohello istemci asla geri dönmemek hello olgu özelliğidir. Biz hello sonraki bölümde göreceğiniz gibi gerçekten gerekli değildir ve hatta bir güvenlik sorunu olabilir.

## <a name="suitable-scenarios-for-hello-oauth2-implicit-grant"></a>Merhaba örtük OAuth2 için uygun senaryoları verin
Merhaba OAuth2 belirtimi kendisini bildirir gibi hello örtük grant toosay olan olup tooenable kullanıcı aracısı uygulamaları – bir tarayıcıdan yürütme JavaScript uygulamaları olmuştur. Bu tür uygulamalar özelliğidir tanımlama hello JavaScript kodu sunucu kaynaklarının (genellikle bir Web API) erişmek için ve Merhaba uygulaması UX uygun şekilde güncelleştirmek için kullanılır ' dir. Gmail veya Outlook Web Access gibi uygulamalar düşünün: gelen kutusundan bir ileti seçtiğinizde görselleştirme paneli değiştirir toodisplay hello yeni seçim, başlangıç sayfasının hello rest sırasında yalnızca selamlama iletisine değiştirilmemiş kalır. Bu, geleneksel yeniden yönlendirme tabanlı Web uygulamaları tersine, burada her kullanıcı etkileşimi tam sayfa geri gönderme ve hello yeni sunucu yanıtı tam sayfa işlenmesi ile sonuçlanır olur.

Tek sayfa uygulamaları ya da SPAs hello JavaScript tabanlı yaklaşım tooits aşırı yararlanan uygulamalar olarak adlandırılan: hello fikirdir bu uygulamaların yalnızca bir başlangıç HTML sayfası ve ilişkili JavaScript tarafından yönetilen tüm sonraki etkileşimler ile hizmet olduğunu Web API çağrıları JavaScript aracılığıyla gerçekleştirilir. Ancak, burada hello uygulama çoğunlukla geri gönderme temelli ancak bazen JS çağrıları gerçekleştirir, karma yaklaşım, seyrek olmayan – hello tartışma örtük Akış kullanımı hakkında da olanlar için geçerlidir.

Yeniden yönlendirme tabanlı uygulamalar genellikle yaklaşım JavaScript uygulamaları için de çalışmıyor kendi isteklerini tanımlama bilgileri, ancak yoluyla güvenli hale getirin. Tanımlama bilgileri, yalnızca diğer etki alanlarında doğru JavaScript çağrılarını yönlendirilebilir sırasında bunlar için oluşturulmuş hello etki alanına göre çalışır. Aslında, sık olacaktır hello durum: Microsoft Graph API, Office API, Azure API – tüm bulunan Merhaba uygulaması Burada sunulan hello etki dışında çağırma uygulamaları düşünün. JavaScript uygulamaları için büyüyen bir eğilim toohave hiçbir arka uç, 3 taraf Web API'leri tooimplement % 100 İş işlevlerine bağlı değildir.

Şu anda hello Web API çağrıları tooa korumak için tercih edilen yöntem toouse hello OAuth2 taşıyıcı belirteci, yapılan her çağrı tarafından bir OAuth2 erişim belirteci burada eşlik yaklaşımdır. Merhaba Web API hello gelen erişim belirteci inceler ve bu bulursa, gerekli kapsamları Merhaba, erişim verir toohello istenen işlemi. Merhaba örtük akış JavaScript uygulamaları için kullanışlı bir mekanizma tooobtain erişim belirteçleri için bir Web API, içinde çok sayıda avantaj toocookies saygı sunumu sağlar:

* Belirteçleri güvenle kaynak çağrıları çapraz gerek kalmadan alınabilir – olan belirteçleri dönüş hello yeniden yönlendirme URI'si toowhich zorunlu kaydı belirteçleri değil hatalı yerleştirilen emin garanti altına alır.
* JavaScript uygulamaları, bunlar hedef – sayıda Web API'leri hiçbir kısıtlama olmaksızın etki alanları için ihtiyaç duydukları kadar erişim belirteçleri alabilir
* Yerel depolama tanımlama bilgisi yönetim donuk toohello uygulama iken belirteç önbelleğe alma ve yaşam süresi management üzerinde Tam Denetim verin veya HTML5 özellikleri oturum gibi
* Erişim belirteçleri uygulanmadıkça tooCross site istek sahtekarlığı (CSRF) saldırılarını değil

Merhaba örtük grant akış güvenlik nedenleriyle çoğunlukla yenileme belirteçleri kesmez. Bir yenileme belirteci olarak dar bir şekilde erişim belirteçleri, onu sızmasını durumunda bu nedenle çok daha fazla zarar inflicting çok daha fazla güç verme olarak kapsamlı değildir. Hello örtük akışında belirteçleri hello URL'de teslim edilir, bu nedenle hello riskinin hello yetkilendirme kodu verme daha yüksektir.

Ancak, bir JavaScript uygulaması tüm olanaklarına erişim belirteçleri tekrar tekrar kimlik bilgileri hello kullanıcıya sormadan yenileme için başka bir mekanizma olduğuna dikkat edin. Merhaba uygulama bir gizli IFRAME tooperform yeni belirteç istekleri hello yetkilendirme uç noktası Azure ad karşı kullanabilir: hello tarayıcı hala etkin bir oturumu var olduğu sürece (okuyun: bir oturum tanımlama bilgisi varsa) hello Azure AD etki alanına göre kimlik doğrulama isteği hello Kullanıcı etkileşimi gerek kalmadan başarıyla oluşabilir.

Bu model hello JavaScript uygulama hello yeteneği verir tooindependently erişim belirteçleri yenileyin ve (Merhaba kullanıcı daha önce bunları rıza koşuluyla. yenilerini yeni bir API için bile Al Bu, alma, koruma ve bir yenileme belirteci gibi yüksek değerli yapı koruma hello eklenen yükünü önler. Merhaba sessiz yenileme mümkün kılan hello yapı hello Azure AD oturum tanımlama bilgisi, hello uygulama dışında yönetilir. Başka bir Bu yaklaşımın avantajı, bir kullanıcı Azure AD'den hello tarayıcı sekmeleri birini çalıştıran Azure AD oturum hello uygulamalarından herhangi birini kullanarak kaydolabilirsiniz ' dir. Bu hello Azure AD oturum tanımlama bilgisi hello silinmesine neden olur ve hello JavaScript uygulama otomatik olarak hello kullanıcı oturumu için toorenew belirteçleri hello özelliğini kaybedersiniz.

## <a name="is-hello-implicit-grant-suitable-for-my-app"></a>Merhaba örtük grant Uygulamam için uygun mu?
Merhaba örtük grant diğer verir'den daha fazla riskine neden olur ve hello alanları belgelendiğinden toopay dikkat tooare gerekir. Örneğin, [erişim belirteci kötüye kullanılması, tooImpersonate kaynak sahibi örtük akış içinde] [ OAuth2-Spec-Implicit-Misuse] ve [OAuth 2.0 tehdit modeli ve güvenlik konuları] [ OAuth2-Threat-Model-And-Security-Implications]). Ancak, hello daha yüksek risk büyük ölçüde uzak kaynak tooa tarayıcı tarafından sunulan etkin kod yürütmek tooenable uygulamaları tasarlanmıştır toohello olgu son profilidir. Uygulamasını planlıyorsanız bir SPA mimari arka uç bileşenlerine sahip veya tooinvoke JavaScript aracılığıyla bir Web API düşündüğünüz, hello örtük akış belirteç edinme için önerilir.

Uygulamanızı yerel istemci ise, hello örtük akış harika uygun değil. yerel istemci hello bağlamında hello Azure AD oturum tanımlama bilgisi Hello yokluğu uzun süreli bir oturum sürdürme hello anlamına gelir uygulamanızdan deprives. Uygulamanızın başka bir deyişle, art arda hello yeni kaynaklar için erişim belirteçleri edinirken ister.

Bir arka uç ve arka uç kodu API'den tüketen içeren bir Web uygulaması geliştiriyorsanız hello örtük akış de iyi bir tercihtir değil. Diğer verir çok daha fazla güç sağlar. Örneğin, hello OAuth2 istemci kimlik bilgileri sağlama hello izinleri yansıtacak hello özelliği tooobtain belirteçleri toohello kendisini karşılıklı toouser temsilcilerine olarak atanan uygulama sağlar. Bu bile bir kullanıcının etkin bir oturum vb. ilgilendiğini değil, hello istemci hello özelliği toomaintain programlı erişim tooresources olduğu anlamına gelir. Yalnızca, ancak bu tür verir daha yüksek güvenlik garantileri sağlar. Örneğin, erişim belirteçleri hello kullanıcı tarayıcı üzerinden hiçbir zaman geçiş, şirketlerin hello tarayıcı geçmişinde kaydedilmesini risk ve benzeri. Merhaba istemci uygulaması, ayrıca bir belirteç isterken, güçlü kimlik doğrulaması gerçekleştirebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
* Geliştirici Kaynakları tam bir listesi için toohello bakın hello protokolleri ve OAuth2 yetkilendirme Azure AD tarafından akışları desteği vermek için başvuru bilgileri de dahil olmak üzere [Azure AD Geliştirici Kılavuzu][AAD-Developers-Guide]
* Bkz: [nasıl toointegrate Azure AD ile bir uygulama] [ ACOM-How-To-Integrate] ek derinliğe hello uygulama tümleştirme işlemi için.

<!--Image references-->

<!--Reference style links in use-->
[AAD-Developers-Guide]: active-directory-developers-guide.md
[ACOM-How-And-Why-Apps-Added-To-AAD]: active-directory-how-applications-are-added.md
[ACOM-How-To-Integrate]: active-directory-how-to-integrate.md
[OAuth2-Spec-Implicit-Misuse]: https://tools.ietf.org/html/rfc6749#section-10.16
[OAuth2-Threat-Model-And-Security-Implications]: https://tools.ietf.org/html/rfc6819
