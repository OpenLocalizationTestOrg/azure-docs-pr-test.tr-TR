---
title: "Özel geliştirilmiş bir uygulama için belirli alanları aaaHow toofill | Microsoft Docs"
description: "Kılavuzu özel çıkışı toofill ne zaman nasıl alanları üzerinde Azure AD ile özel bir geliştirilmiş uygulama kaydediyorsunuz"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 7e07bc45c58542edb3863db5aad7c845f1a1772e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofill-out-specific-fields-for-a-custom-developed-application"></a>Nasıl toofill özel geliştirilmiş bir uygulama için belirli alanları

Bu makale size hello kullanılabilir tüm alanlar hello uygulama kayıt formunda kısa bir açıklamasını hello [Azure portal](https://portal.azure.com).

## <a name="register-a-new-application"></a>Yeni uygulamayı Kaydet

-   Yeni bir uygulama tooregister gidin toohello [Azure portal](https://portal.azure.com).

-   Merhaba sol gezinti bölmesinden tıklatın **Azure Active Directory.**

-   Seçin **uygulama kayıtlar** tıklatıp **Ekle**.

-   Merhaba uygulama kayıt formu bu açın.

## <a name="fields-in-hello-application-registration-form"></a>Merhaba uygulama kayıt formu alanları


| Alan            | Açıklama                                                                              |
|------------------|------------------------------------------------------------------------------------------|
| Ad             | Merhaba uygulaması Hello adı. En az dört karakter olmalıdır.                |
| Uygulama türü | **Web uygulaması/Web API**: bir web uygulaması, web API veya her ikisini de temsil eden bir uygulama 
| |**Yerel**: bir kullanıcının Cihazınızda veya bilgisayarınızda yüklü bir uygulama           |
| Oturum açma URL'si      | Kullanıcılar, uygulamanızın içinde toouse burada kaydolabilirsiniz hello URL'si                                  |

Merhaba alanları yukarıda doldurduktan sonra Merhaba uygulaması hello Azure portalına kaydedilebilir ve yönlendirilir toohello uygulama sayfası. Merhaba **ayarları** hello uygulama bölmesi düğmesinde toocustomize sizin için daha fazla alan içeriyor hello Ayarları sayfası, uygulamanızı açar. Merhaba tabloda hello Ayarları sayfasında tüm hello alanları açıklar. yalnızca bir alt kümesini, bir web uygulaması veya bir yerel uygulamayı oluşturduğunuz bağlı olarak, bu alanlara görür unutmayın.

| Alan           | Açıklama                                                                                                                                                                                                                                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Uygulama Kimliği  | Bir uygulamayı kaydetme, Azure AD, uygulamanızın bir uygulama kimliği atar Merhaba uygulama kimliği kullanılabilir toouniquely grafik API'si hello gibi tooaccess kaynakları yanı sıra, kimlik doğrulama isteklerini tooAzure AD uygulamanızda tanımlayın.                                                          |
| Uygulama Kimliği URI'si      | Bu genellikle hello formunun benzersiz bir URI olmalıdır **https://&lt;Kiracı\_adı&gt;/&lt;uygulama\_adı&gt;.** Hangi hello belirteci için verilmesi benzersiz tanımlayıcı toospecify hello kaynak olarak bu hello yetkilendirme grant akışı sırasında kullanılır. Verilen hello erişim belirteci hello 'aud' talep haline gelir. |
| Karşıya yeni logo yükle | Bu tooupload logo, uygulamanız için kullanabilirsiniz. Merhaba logosu .bmp, .jpg veya .png biçiminde olmalıdır ve hello dosya boyutu 100 KB'tan daha az olmalıdır. Merhaba boyutlar hello görüntü için merkezi görüntü boyutları 94 x 94 piksel ile 215 x 215 piksel olmalıdır.                                                       |
| Giriş sayfası URL'si   | Uygulama kaydı sırasında belirtilen hello oturum açma URL'si budur.                                                                                                                                                                                                                                              |
| Oturum kapatma URL'si      | Bu hello tek oturum kapatma oturum kapatma URL'si. Merhaba kullanıcı oturumuna Azure AD ile temizlediğinde azure AD kayıtlı herhangi bir uygulama kullanarak bir oturum kapatma isteği toothis URL gönderir.                                                                                                                                       |
| Çoklu kiralanan  | Bu anahtar hello uygulama birden çok kiracılar tarafından kullanılıp kullanılamayacağını belirtir. Genellikle, bu dış kuruluşlar kendi Kiracı kaydetme ve erişim tootheir kuruluşunuzun verilerini verme uygulamanızı kullanabileceğiniz anlamına gelir.                                                                   |
| Yanıt URL'leri      | Merhaba yanıt URL'leri hello burada Azure AD dönüş uygulamanız tarafından istenen herhangi bir belirtece noktalarıdır.                                                                                                                                                                                                          |
| Yeniden yönlendirme URI'ler   | Yerel uygulamalar için burada hello kullanıcının gönderilen toofollowing başarılı yetkilendirme olması budur. Hello azure AD onay hello OAuth 2.0, uygulama malzemeler hello Portalı'nda kayıtlı hello değerlerden birine eşleşen istek URI'si yönlendirin.                                                            |
| Anahtarlar            | Anahtarları tooprogrammatically erişim web API'leri herhangi bir kullanıcı etkileşimi olmadan Azure AD tarafından güvenli hale getirilmiş oluşturabilirsiniz. Merhaba gelen \* \*anahtarları\* \* sayfasında, bir anahtar açıklaması ve hello sona erme tarihini girin ve toogenerate hello anahtarı kaydedin. Mümkün tooaccess olmayacaktır gibi herhangi bir yerde güvenli, emin toosave olun daha sonra.             |

## <a name="next-steps"></a>Sonraki adımlar
[Azure Active Directory ile uygulamaları yönetme](active-directory-enable-sso-scenario.md)
