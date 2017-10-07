---
title: "aaaMicrosoft Doğrulayıcı Azure ve Microsoft hesaplarının oturum açma - telefon | Microsoft Docs"
description: "Telefon toosign tooyour parolanızı yazmak yerine Microsoft hesabı kullanın. Bu makalede, bu özellik hakkında sık sorulan sorular yanıtlanmaktadır."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/12/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: a4911ff580b3ffa078299ad706d099330b75a2e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-with-your-phone-not-your-password"></a>Telefonunuz oturum, parolanızı değil oturum

Merhaba Microsoft Authenticator uygulama parolanızı girdikten sonra iki aşamalı doğrulama gerçekleştirerek hesaplarınızın güvenliğini sağlamanıza yardımcı olur. Ancak bunu hello kişisel Microsoft hesabınızın parolasını tamamen değiştirebilir olduğunu biliyor muydunuz? 

Bu özellik, iOS ve Android cihazlarda kullanılabilir ve kişisel Microsoft hesaplarıyla çalışır. 

## <a name="how-it-works"></a>Nasıl çalışır?

Tooyour Microsoft hesabı oturum açtığınızda, birçoğu için iki aşamalı doğrulamayı hello Microsoft Authenticator uygulamasını kullanın. Parolanızı yazın ve sonra Git toohello uygulama tooeither bir bildirim onaylamak veya bir doğrulama kodu alın. Telefon oturum açma ile Merhaba parola atlayın ve tüm kimlik doğrulama telefonunuza yapın. Telefon oturum açma iki aşamalı doğrulamayı bir tür olduğundan, tooprovide bildiğiniz bir şey ve kimlik bilgilerinizi tooverify sahip bir şey hala gerekir. Merhaba telefon hala elinizde hello şeydir ve telefonunuzun PIN veya biyometrik anahtarı bildiğiniz hello şeydir. 

## <a name="how-tooget-started"></a>Tooget nasıl başlatılacağını

tooyour kişisel Microsoft hesabı, telefon ile toosign şu adımları izleyin: 

1. Telefon oturum açma hesabınızın etkinleştirin. 

  - Henüz, yükleme ve kişisel Microsoft hesabınızı hello toohello adımları göre ekleme hello Microsoft Authenticator uygulaması yoksa [Microsoft Authenticator sayfasına](microsoft-authenticator-app-how-to.md). İyi toogo olacak şekilde yeni eklenen hesapları otomatik olarak etkinleştirilir.

  - İki aşamalı doğrulama için Microsoft Authenticator zaten kullanıyorsanız, hello uygulama giriş sayfasından hesabınızı seçin ve Seç **etkinleştirme telefon oturum açma** hello açılan menüsünden.

  >[!NOTE] 
  >tooprotect hesabınızı biz bir PIN veya biyometrik kilit aygıtınızda gerektirir. Telefonunuz kilidi tutarsanız, telefon oturum açma etkinleştirmeden önce tooset kilit kurmak isteyen bir istek yukarı hello uygulama açılır. 

3. Çoğu sayfaları normalde girdiğiniz Microsoft hesabı parolanızı belirten bir bağlantı sahip **bir uygulama kullanın**. Bu bağlantıyı toosign telefonunuz oturum seçin. 

4. Microsoft bir bildirim tooyour telefon gönderir. Merhaba bildirim toosign tooyour hesabındaki onaylayın.   

## <a name="faq"></a>SSS 

### <a name="how-is-signing-in-with-my-phone-more-secure-than-typing-a-password"></a>Nasıl daha güvenli bir parola yazarak daha telefonum oturum imzalama?  

Günümüzde çoğu kişi tooweb siteleri veya uygulamaları bir kullanıcı adı ve parola kullanarak oturum açın.  Ne yazık ki, parolaları genellikle kaybolduğunda, çalındığında veya saldırganlar tarafından tahmin. Merhaba Microsoft Authenticator uygulama toosign ayarladığınızda, biz telefonunuzda hesabınızın kilidini açmak bir anahtar oluşturun. Biz bu hello PIN anahtarıyla korumak veya biyometrik telefonunuzda zaten kullanın.  Telefonunuz oturum oturum açtığınızda kimliğinizi güvenli bir şekilde iki Etkenler – hello kullanılan tooprove ise bu anahtar telefon kendisi ve yeteneği toounlock onu. 

kullanılan hello benzer toohello anahtarları Windows Hello ve hello FIDO Alliance UAF belirtimleri kullanılan anahtardır. Yalnızca verileri değil, biyografisi tooprotect hello anahtarı yerel olarak kullanılan ve hiçbir zaman gönderilen veya hello bulutta, depolanan. 
 
### <a name="where-can-i-use-my-phone-tooreplace-my-password-and-where-would-i-still-need-hello-password"></a>Burada my telefon tooreplace parolamı kullanabilir miyim ve burada hala hello parola ihtiyacım?  

Bugün, oturum açma hello telefon özelliği yalnızca web uygulamaları ve kişisel Microsoft hesapları, iOS veya kişisel bir Microsoft hesabı kullanmanız Android uygulamalarını ve Windows 10 kişisel bir Microsoft hesabı kullanan uygulamalar tarafından desteklenen Hizmetleri ile çalışır. Bu web siteleri veya uygulamaları tooone içinde oturum genellikle gireceğiniz parolanızı hello sayfasında olduğunda belirten bir bağlantı **bir uygulama kullanın**. 

Telefon oturum açma kullanılan toounlock bir Windows bilgisayarı, XBOX veya Office uygulamaları gibi Microsoft uygulamalarına Masaüstü sürümlerini şu anda olamaz. 
 
### <a name="does-this-replace-two-step-verification-should-i-turn-it-off"></a>Bu, iki aşamalı doğrulamayı yerini almaz? I kapatmak?   

Bazen. Telefon oturum açma hello kapsamı genişletme üzerinde çalışıyoruz, ancak şimdilik vardır hala desteklemeyen hello Microsoft ekosistemi yerlerde. Bu yerde biz yine iki aşamalı doğrulamayı güvenli oturum açma için kullanıyorsunuz. Bu nedenle, Hayır, iki basamaklı doğrulamayı kapatmak hesabınız için etkinleştirmeniz gerekir. 
 
### <a name="okay-if-i-keep-two-step-verification-turned-on-for-my-account-do-i-have-tooapprove-two-notifications"></a>İki aşamalı doğrulamayı hesabımın açık tutarsanız, Tamam, tooapprove iki bildirim var mı?

Hayır, olmaz. Tooyour telefonunuza bir Microsoft hesabıyla oturum iki aşamalı doğrulamayı sayılır. Parolanızı yazmaya yerine sonra bir bildirim onaylama, kimliğinizi öğrenerek kanıtlamak nasıl toounlock telefonunuzu ve bildirim onaylama. Biz ikinci bir bildirim tooapprove göndermez.

### <a name="what-if-i-lose-my-phone-or-dont-have-it-with-me-how-can-i-access-my-account"></a>Ne telefonum kaybeder veya sahip değilseniz, benimle, nasıl Hesabımı erişebilir mi?  

Her zaman tıklayabilirsiniz **bir parolasını kullanmanız** hello oturum açma sayfası tooswitch üzerinde toousing parolanızı yedekleyin. İki aşamalı doğrulama kullanırsanız, yine ikinci yöntem tooverify oturum açma işleminiz gerektiğini göz önünde bulundurun. İşte bu nedenle kesinlikle toomake hesabınıza fazladan, güncel güvenlik bilgileri sahip olduğunuzdan emin öneririz. Https://account.live.com/proofs/manage adresinden güvenlik bilgilerinizi yönetebilirsiniz. 
 
### <a name="how-do-i-stop-using-this-feature-and-go-back-tooentering-my-password"></a>Nasıl bu özelliği kullanmayı açıp tooentering parolamı dön?

Tıklatın **bir parolasını kullanmanız** oturum açtığınızda. Biz en son tercih ettiğiniz unutmayın ve varsayılan hello tarafından oturum açtığınızda sunar. Telefonunuz oturum hiç toogo geri toosigning istiyorsanız, **bir uygulama kullanın**. 
 
### <a name="can-i-use-hello-app-toosign-in-tooall-my-accounts-with-microsoft"></a>Microsoft ile Merhaba uygulama toosign tooall içinde my hesapları kullanabilirim?   
Bu işlevsellik şu anda yalnızca kişisel Microsoft hesapları için kullanılabilir. 
 
### <a name="can-i-sign-into-my-pc-with-my-phone"></a>Bilgisayarımda telefonum ile oturum açarak?  
Bilgisayarınıza için oturum Windows Hello Windows 10 imzalama, yüz, parmak izi veya bir PIN kullanmanızı öneririz.   
 
### <a name="can-i-sign-in-with-my-windows-phone"></a>My Windows Phone oturum oturum?  
Şu anda Biz bu işlevselliği hello Microsoft Authenticator üzerinde Windows Phone için geliştirdiğiniz değil. 

## <a name="next-steps"></a>Sonraki adımlar
Merhaba Microsoft Authenticator uygulamasını yüklemediyseniz atın. Merhaba uygulama için kullanılabilir [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), ve telefon oturum açma için hello Microsoft Authenticator uygulaması üzerinde kullanılabilir [Android](http://go.microsoft.com/fwlink/?Linkid=825072) ve [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).

Genel hello uygulaması hakkında sorularınız varsa, hello bakalım [Microsoft Doğrulayıcı SSS](microsoft-authenticator-app-faq.md)
