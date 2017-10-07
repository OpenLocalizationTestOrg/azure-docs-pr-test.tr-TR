---
title: "Azure Active Directory B2C: Yerleşik ilkeleri | Microsoft Docs"
description: "Bir konu Azure Active Directory B2C hello Genişletilebilir ilke çerçevesini ve nasıl toocreate çeşitli ilke türleri"
services: active-directory-b2c
documentationcenter: 
author: sama
manager: mbaldwin
editor: PatAltimore
ms.assetid: 0d453e72-7f70-4aa2-953d-938d2814d5a9
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: sama
ms.openlocfilehash: 24bb85eba30f888c6ea7d0401e05235e8eb6ea79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a>Azure Active Directory B2C: Yerleşik ilkeleri


Azure Active Directory (Azure AD) B2C Hello Genişletilebilir ilke çerçevesini hello çekirdek hello hizmet gücünü ' dir. İlkeleri tam olarak açıklayan tüketici kimlik deneyimi gibi kaydolma, oturum açma ve profil düzenleme. Örneğin, bir kayıt ilkesi toocontrol davranışları hello aşağıdaki ayarları yapılandırarak sağlar:

* Tüketiciler toosign Merhaba uygulaması için kullanabileceğiniz türü (facebook sosyal hesapları) veya e-posta adresleri gibi yerel hesap
* Öznitelikler (örneğin, ad, posta kodu ve ayakkabı boyutu) toobe hello tüketiciden kayıt sırasında toplanan
* Azure çok faktörlü kimlik doğrulaması
* Merhaba görünümüne tüm kayıt sayfaları
* Çalıştırma hello İlkesi tamamlandığında uygulama hello (hangi bir belirteç talep olarak bildirimleri) bilgilerini alır

Kiracınızda farklı türlerde birden çok ilke oluşturup, bunları gerektiği gibi uygulamalarınızda kullanabilirsiniz. İlkeler, uygulamalar arasında yeniden kullanılabilir. Bu esneklik, geliştiricilerin toodefine sağlar ve tüketici kimlik deneyimi ile en az veya herhangi bir değişiklik tootheir kodu değiştirin.

İlkeleri basit Geliştirici arabirimi aracılığıyla kullanılabilir. Uygulamanız (bir ilke parametre hello istekte geçirme) standart bir HTTP kimlik doğrulaması isteği kullanarak bir ilke tetikler ve yanıt olarak özelleştirilmiş bir belirteç alır. Örneğin, bir kayıt ilkesi çağırma istekleri ve oturum açma ilke çağırmak istekleri arasındaki tek fark hello hello "p" sorgu dizesi parametresi kullanılır hello ilkesi adı şudur:

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siup                                       // Your sign-up policy

```

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siin                                       // Your sign-in policy

```

Hello ilkesi çerçevesi hakkında daha fazla bilgi için bkz: [bu blog gönderisine Azure AD B2C üzerinde hello Enterprise Mobility and Security Blog hakkında](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).

## <a name="create-a-sign-up-or-sign-in-policy"></a>Bir kayıt veya oturum açma ilkesi oluşturma

Bu ilke, her iki tüketici kaydolma ve oturum açma deneyimlerini tek bir yapılandırmasına sahip işler. Tüketiciler, yoldan hello sağ (kaydolma veya oturum açma) hello bağlam bağlı olarak gerektiriyordu. Ayrıca, Merhaba uygulaması başarılı oturum ups veya oturum açma işlemleri almaz belirteçleri Merhaba içeriğine anlatır.  Hello kaydolma veya oturum açma ilkesi için bir kod örneğidir [kullanılabilir burada](active-directory-b2c-devquickstarts-web-dotnet-susi.md).  Kayıt İlkesi ve oturum açma ilkesi bu ilkeyi kullanmak maskelenmesi önerilen olur.  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a>Kayıt ilkesi oluşturma

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a>Bir oturum açma ilkesi oluşturma

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a>İlke düzenleme profil oluşturma

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a>Bir parola sıfırlama ilkesi oluşturma

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a>Sık sorulan sorular

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a>Bir kayıt veya oturum açma ilkesi bir parola sıfırlama İlkesi ile nasıl bağlanır?
Bir oturum açma veya kaydolma ilkesiyle (yerel hesaplar için) oluşturduğunuzda, gördüğünüz bir **unuttunuz parola?** hello deneyimi'nın ilk sayfasında hello bağlantı. Bu bağlantıyı tıklatarak otomatik olarak tetikleyici bir parola sıfırlama İlkesi değil. 

Bunun yerine, hata kodu hello  **`AADB2C90118`**  tooyour uygulamasına döndürülür. Uygulamanızın, belirli parolası sıfırlama ilkesini harekete geçirerek, bu hata kodu toohandle gerekir. Daha fazla bilgi için bir [ilkeleri bağlama hello yaklaşımı gösteren örnek](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a>Bir kayıt veya oturum açma ilkesi veya bir kayıt ilkesi ve bir oturum açma ilkesi kullanmalıyım?
Bir kayıt ilkesi ve bir oturum açma ilkesi bir kayıt veya oturum açma ilkesi kullanmanızı öneririz.  

Hello kaydolma veya oturum açma ilkesi hello oturum açma ilkesinden daha fazla özellik içerir. Ayrıca toouse sayfası kullanıcı arabirimini özelleştirme sağlar ve yerelleştirme için daha iyi destek vardır. 

oturum açma Hello İlkesi ilkelerinizi toolocalize gerekmiyorsa, yalnızca markalama için ikincil özelleştirme özellikleri gerekir ve parola istediğiniz önerilir yerleşik sıfırlama.

## <a name="next-steps"></a>Sonraki adımlar
* [Belirteç, oturum ve tek oturum açma yapılandırması](active-directory-b2c-token-session-sso.md)
* [E-posta doğrulama tüketici kaydolma sırasında devre dışı bırak](active-directory-b2c-reference-disable-ev.md)

