---
title: "oturum açma aaaSingle Yönetim'hello Azure Active Directory kurumsal uygulamalar için | Microsoft Docs"
description: "Azure Active Directory kullanarak kurumsal uygulamaları için toomanage çoklu oturum açma nasıl hello öğrenin"
services: active-directory
documentationcenter: 
author: asmalser
manager: femila
editor: 
ms.assetid: bcc954d3-ddbe-4ec2-96cc-3df996cbc899
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: asmalser
ms.openlocfilehash: b0a8e622ab10517b7b69f786406b6e9b9f2e7eaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-single-sign-on-for-enterprise-apps"></a>Kurumsal uygulamaları için çoklu oturum açmayı yönetme
> [!div class="op_single_selector"]
> * [Azure portal](active-directory-enterprise-apps-manage-sso.md)
> * [Klasik Azure Portalı](active-directory-sso-integrate-saas-apps.md)
> 

Bu makalede nasıl toouse hello [Azure portal](https://portal.azure.com) kurumsal uygulamalar için toomanage çoklu oturum açma ayarları. Kurumsal uygulamalar dağıtılan ve kuruluşunuzda kullanılan uygulamalardır. Bu makale özellikle hello eklenen tooapps geçerlidir [Azure Active Directory Uygulama galerisinde](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery). 

## <a name="finding-your-apps-in-hello-portal"></a>Uygulamalarınızı hello Portalı'nda bulma
Çoklu oturum açma için ayarlanan tüm kurumsal uygulamaları görüntülenebilir ve hello Azure portal yönetilebilir. Merhaba uygulamaları hello bulunabilir **daha Hizmetleri** &gt; **kurumsal uygulamalar** hello portalı bölümü. 

![Kurumsal uygulamalar dikey penceresi][1]

Seçin **tüm uygulamaları** tooview yapılandırılmış tüm uygulamaların listesi. Bir uygulamayı seçerek hello kaynak dikey burada bu uygulama için raporlar görüntülenebilir ve çeşitli ayarları yönetilebilmesi için bu uygulama için yükler.

toomanage çoklu oturum açma ayarları, seçin **çoklu oturum açma**.

![Uygulama kaynağı dikey][2]

## <a name="single-sign-on-modes"></a>Çoklu oturum açma modları
Merhaba **çoklu oturum açma** dikey başlıyorsa bir **modu** yapılandırılmış hello tek oturum açma modu toobe sağlayan menüsü. Merhaba mevcut Seçenekler şunlardır:

* **SAML tabanlı oturum açma** -bu seçenek Azure hello SAML 2.0 protokolü kullanılarak Active Directory'ye Merhaba uygulaması tam Federasyon çoklu oturum açma destekliyorsa kullanılabilir.
* **Parola tabanlı oturum açma** -bu seçenek Azure AD parola form bu uygulama için doldurma destekliyorsa kullanılabilir.
* **Bağlantılı oturum** -"Varolan çoklu oturum açma" eski adıyla, bu seçenek, Yöneticiler'i sağlar, kullanıcının Azure AD erişim paneli veya Office 365 uygulama Başlatıcı bağlantı toothis uygulamada tooplace.

Bu modları hakkında daha fazla bilgi için bkz: [nasıl çoklu oturum açmayı Azure Active Directory iş](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

## <a name="saml-based-sign-on"></a>SAML tabanlı oturum açma
Merhaba **SAML tabanlı oturum açma** seçeneği, dört bölümlerde bölünmüş bir dikey pencere görüntüler:

### <a name="domains-and-urls"></a>Etki alanları ve URL'ler
Merhaba uygulamanın etki alanı ve URL'ler ile ilgili tüm ayrıntıları tooyour Azure AD dizini burada eklenen budur. Tüm isteğe bağlı girişleri hello seçerek görüntülenebilir ancak toomake tek oturum açma iş uygulama doğrudan Merhaba ekranında görüntülenen tüm girişleri gerekli **Göster Gelişmiş URL ayarları** onay kutusu. desteklenen girişleri Hello tam listesini içerir:

* **Oturum üzerinde URL'si** – toosign bileşenini toothis uygulama hello kullanıcı gider burada. Bir kullanıcı toothis URL gittiğinde hello hizmet sağlayıcısı gerekli hello Merhaba uygulaması yapılandırılmış tooperform hizmet sağlayıcısı tarafından başlatılan tek oturum açma, ise yeniden yönlendirme tooAzure AD tooauthenticate ve oturum kullanıcı hello. Bu alan doldurulursa, Azure AD bu URL toolaunch hello uygulamadan Office 365 ve Azure AD erişim paneli hello kullanır. Bu alan atlanmış sonra Azure AD kimlik sağlayıcısı yerine gerçekleştirir-zaman hello uygulama hello Azure AD erişim paneli, Office 365 veya Azure AD hello tek başlatıldıktan üzerinde başlatılan oturum oturum açma URL'si.
* **Tanımlayıcı** -bu URI benzersizce Merhaba uygulaması hangi tek oturum açma yapılandırılan için. Bu Azure AD hello SAML belirteci İzleyici parametresinin hello gibi geri tooapplication gönderir ve hello uygulamasıdır beklenen toovalidate hello değerdir. Bu değer, hello uygulama tarafından sağlanan herhangi bir SAML meta veri hello varlık kimliği olarak görünür.
* **Yanıt URL'si** -hello yanıt URL'si olan burada hello uygulama tooreceive hello SAML belirteci bekler. Bu da başvurulan tooas hello onaylama tüketici Hizmeti'ni (ACS) URL'dir. Bunlar girdikten sonra sonraki tooproceed toohello sonraki ekran'ı tıklatın. Bu ekran hangi gereksinimlerini toobe tooaccept Azure AD'den bir SAML belirtecine yapılandırdığınız hello uygulama yan tooenable üzerinde hakkında bilgi sağlar.
* **Geçiş durumunu** -hello geçiş durumunda, burada kimlik doğrulama tamamlandıktan sonra kullanıcı tooredirect hello hello uygulamaya bildirmek yardımcı olabilecek isteğe bağlı bir parametre. Bazı uygulamalar bu alan farklı kullanır ancak genellikle hello hello uygulama, geçerli bir URL değerdir (Merhaba uygulamanın çoklu oturum açma Ayrıntılar için belgelere bakın). Merhaba özelliği tooset hello geçiş durumunu benzersiz toohello yeni Azure portalına olan yeni bir özelliktir.

### <a name="user-attributes"></a>Kullanıcı öznitelikleri
Burada admins görüntüleyebilir ve Azure AD kullanıcılar her toohello uygulama sorunlarını hello SAML belirtecinde gönderilen Düzenle hello öznitelikleri oturum budur.

yalnızca desteklenen düzenlenebilir özniteliği hello hello **kullanıcı tanımlayıcısı** özniteliği. Bu özniteliğin değeri Hello hello hello uygulamadaki her bir kullanıcı olarak tanıtan Azure ad alanıdır. Merhaba uygulama hello "e-posta adresi" Merhaba kullanıcı adı ve benzersiz tanımlayıcı kullanarak dağıtılmışsa, örneğin, ardından hello değeri toohello "user.mail" alan Azure AD içinde ayarlanabilir.

### <a name="saml-signing-certificate"></a>SAML imzalama sertifikası
Bu bölümde Azure AD toohello uygulama her zaman hello kullanıcının kimliğini doğrular verilen toosign hello SAML belirteçlerini kullanır hello sertifika hello ayrıntılarını gösterir. Merhaba sona erme tarihi gibi Denetlenmekte, hello geçerli sertifika toobe hello özelliklerini sağlar.

### <a name="application-configuration"></a>Uygulama yapılandırması
Merhaba son bölümü hello belgelerine ve/veya denetimleri gerekli tooconfigure hello uygulama kendisini toouse Azure Active Directory kimlik sağlayıcısı olarak sağlar.

Merhaba **uygulama Yapılandır** uçarak çıkış menü hello uygulama yapılandırmak için yeni kısa, katıştırılmış yönergeler sağlar. Başka bir yeni özellik benzersiz toohello yeni Azure portalına budur.

> [!NOTE]
> Merhaba Salesforce.com uygulama embedded belgeler tam bir örnek için bkz. Ek uygulamalar için belge sürekli olarak ekleniyor.
> 
> 

![Katıştırılmış belgeleri][3]

## <a name="password-based-sign-on"></a>Parola tabanlı oturum açma
Merhaba uygulaması için destekleniyorsa, seçerek hello parola tabanlı SSO modu ve seçerek **kaydetmek** anında toodo yapılandırır parola tabanlı SSO. Parola tabanlı SSO dağıtma hakkında daha fazla bilgi için bkz: [nasıl çoklu oturum açmayı Azure Active Directory iş](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

![Parola tabanlı oturum açma][4]

## <a name="linked-sign-on"></a>Bağlantılı oturum açma
Bağlantılı hello SSO modu seçme Hello uygulama için destekleniyorsa, bu uygulamasını hello Azure AD erişim paneli veya Office 365 tooredirect toowhen kullanıcılar'ı tıklatın, istediğiniz tooenter hello URL da sağlar. Bağlantılı SSO (eski adıyla "mevcut SSO") hakkında daha fazla bilgi için bkz: [nasıl çoklu oturum açmayı Azure Active Directory iş](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

![Bağlantılı oturum açma][5]

##<a name="feedback"></a>Geri Bildirim

Hello kullanarak gibi Azure AD deneyimi geliştirilmiş umuyoruz. Gelen hello geribildirim unutmayın! Geri bildirim ve fikir geliştirme için hello sonrası **Yönetici portalı** bölümünü bizim [geri bildirim Forumunda](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).  Biz, her gün harika yeni hizmetler oluşturma hakkında heyecan ve kılavuz tooshape kullanabilir ve sonraki geliştirmemiz ne tanımlayın.

[1]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade.PNG
[2]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-sso-blade.PNG
[3]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-embedded-docs.PNG
[4]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-password-sso.PNG
[5]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-linked-sso.PNG
