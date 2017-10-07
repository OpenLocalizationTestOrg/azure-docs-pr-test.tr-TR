---
title: "aaaApp kayıt portalı Yardım konuları | Microsoft Docs"
description: "Çeşitli özelliklerin hello Microsoft uygulama kayıt Portalı'nda açıklaması."
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: f0507c28-9464-4d3e-bd53-de9053fd5278
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: 3eb17b629577446a336152799497e7d980fb825d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="app-registration-reference"></a>Uygulama Kayıt başvurusu
Bu belgede bağlamı ve hello Microsoft uygulama kayıt portalı bulunan çeşitli özelliklerin açıklamaları sağlanmaktadır [https://apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).

## <a name="my-applications"></a>Uygulamalarım
Bu listedeki tüm uygulamalarınızın hello Azure AD v2.0 uç noktası ile kullanılması için kaydedilen içerir.  Bu uygulamalar Microsoft hesabı ve Azure Active Directory'den iş/Okul hesapları hem kişisel hesapları olan kullanıcıların hello özelliği toosign sahip.  toolearn hello Azure AD v2.0 uç hakkında daha fazla bilgi görmek bizim [v2.0 genel bakış](active-directory-appmodel-v2-overview.md).  Bu uygulamalar ayrıca hello Microsoft hesabı kimlik doğrulama uç noktası ile kullanılan toointegrate olarak `https://login.live.com`.

## <a name="live-sdk-applications"></a>Canlı SDK uygulamaları
Bu listedeki tüm uygulamalarınızın yalnızca Microsoft hesabı ile kullanmak için kayıtlı içerir.  Azure Active Directory doğabilecek ile kullanmak için etkinleştirilmemiş.  Merhaba MSA Geliştirici portalında ile önceden kaydedilmiş tüm uygulamaları bulabileceğiniz budur `https://account.live.com/developers/applications`.  Daha önce sırasında gerçekleştirilen tüm işlevleri `https://account.live.com/developers/applications` şimdi bu yeni portalında gerçekleştirilen `https://apps.dev.microsoft.com`.  Daha fazla Microsoft hesabı uygulamalarınızı hakkında sorularınız varsa lütfen bizimle iletişime geçin.

## <a name="application-secrets"></a>Uygulama parolaları
Uygulama parolaları olan uygulama tooperform güvenilir izin kimlik bilgilerini [istemci kimlik doğrulaması](http://tools.ietf.org/html/rfc6749#section-2.3) Azure AD ile.  OAuth ve Openıd Connect içinde bir uygulama parolaları olan yaygın olarak başvurulan tooas bir `client_secret`.  Merhaba v2.0 protokolü, bir web adreslenebilir konumdaki güvenlik belirtecini alır herhangi bir uygulama (kullanarak bir `https` düzeni) bir uygulama gizli tooidentify kendisini tooAzure AD güvenlik belirtecini kullanım bağlı kullanmanız gerekir.  Ayrıca, bir uygulama gizli tooperform istemci kimlik doğrulaması, toodiscourage kullanarak bir cihazdaki recieves belirteçleri Yasak, herhangi bir yerel istemci gizli güvenli olmayan ortamlarda depolanmasını hello.

Her uygulama verilen herhangi bir noktada iki geçerli uygulama parolaları içerebilir.  İki gizli tutarak, uygulamanızın tüm ortamı genelinde hello ablilty tooperform düzenli anahtar geçişi sahip.  Uygulama tooa yeni gizli hello tamamen geçirdikten sonra hello eski parola silin ve yeni bir sağlama.

Şu anda uygulama parolaları yalnızca iki tür hello uygulama kayıt Portalı'nda izin verilir.  Seçme **yeni bir parola oluşturmak** oluşturur ve uygulamanızda kullanabilirsiniz hello ilgili veri deposundaki bir paylaşılan gizlilik depolar.  Seçme **oluştur yeni bir anahtar çifti** indirmiş ve istemci kimlik doğrulaması tooAzure AD için kullanılan yeni bir ortak/özel anahtar çifti oluşturur.

## <a name="profile"></a>Profil
Merhaba uygulama kayıt portalı Hello profil bölümü olabilir toocustomize hello oturum sayfasında uygulamanız için kullanılır.  Şu anda hello oturum açma sayfasının uygulama logosu, hizmet URL'si ve gizlilik bildirimini koşulları değiştirebilirsiniz.  Merhaba logosu bir saydam 48 x 48 veya 50 x 50 piksel boyutunda, 15 KB bir GIF, PNG veya JPEG dosyası olmalıdır ya da daha küçük.  Merhaba değerleri ve oturum açma sayfası kaynaklanan görüntüleme hello değiştirmeyi deneyin!

## <a name="live-sdk-support"></a>Canlı SDK'sı desteği
"Live SDK desteği" etkinleştirdiğinizde, oluşturduğunuz gizli hello Azure AD ve Microsoft Account veri sağlanacak herhangi bir uygulama depolar.  Bu, uygulama toointegrate hello Microsoft Account hizmetini (login.live.com) ile doğrudan izin verir.  Microsoft Account doğrudan (karşılıklı toousing hello Azure AD v2.0 uç noktası) kullanarak bir uygulama toobuild istiyorsanız, Live SDK desteği etkin olduğundan emin olun.

Live SDK desteğini devre dışı bırakma, hello uygulama gizli anahtarı yalnızca hello Azure AD veri deposuna yazılır güvence altına alır.  Hello Azure AD veri deposu toomeet izin Kurumsal düzeyde düzenlemeleri FISMA uyumluluk gibi belirli standartları içerir.  Live SDK desteğini etkinleştirirseniz, uygulamanızın bazı Bu standartlar ile uyumluluğu elde.

Her zaman sadece toouse hello Azure AD v2.0 uç planlıyorsanız, Canlı SDK'sı desteği güvenli bir şekilde devre dışı bırakabilirsiniz.

