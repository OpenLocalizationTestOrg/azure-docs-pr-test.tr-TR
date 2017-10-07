---
title: "aaaConfigure SaaS uygulamaları için Azure Active Directory B2B işbirliği | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği için PowerShell ve kod örnekleri"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c3f22f81567c04ac23ef2316c09de718ecb15d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a>SaaS uygulamaları B2B işbirliği için yapılandırma

Azure AD ile tümleştirmek çoğu uygulamaları ile Azure Active Directory (Azure AD) B2B işbirliği çalışır. Bu bölümde, Azure AD B2B ile kullanmak için bazı yaygın SaaS uygulamaları yapılandırmaya yönelik yönergeler size rehberlik eder.

Uygulamaya özgü yönergeleri göz önünde bulundurmanız önce bazı kurallar altın şunlardır:

* Merhaba uygulamalarının çoğu için Kullanıcı Kurulumu el ile toohappen gerekir. Diğer bir deyişle, kullanıcılar da hello uygulamada el ile oluşturulması gerekir.

* Dropbox gibi otomatik kurulum destekleyen uygulamalar için ayrı davetleri hello uygulamalardan oluşturulur. Kullanıcıların her davet emin tooaccept olması gerekir.

* Merhaba kullanıcı öznitelikleri, tüm sorunları Konuk kullanıcılar karıştırılmış kullanıcı profili diski (UPD) ile toomitigate için her zaman kümesindeki **kullanıcı tanımlayıcısı** çok**user.mail**.


## <a name="dropbox-business"></a>Dropbox iş

kendi kuruluş hesabı kullanarak tooenable kullanıcılar toosign güvenlik onaylama işlemi biçimlendirme dili (SAML) kimlik sağlayıcısı Dropbox iş toouse Azure AD el ile yapılandırmanız gerekir. Bu nedenle, Dropbox iş yapılandırılmış toodo olmadıysa sor veya aksi takdirde Azure AD kullanarak kullanıcıların toosign izin olamaz.

1. Azure AD, select INTO tooadd hello Dropbox iş uygulama **kurumsal uygulamalar** hello sol bölmesinde ve ardından **Ekle**.

  ![Merhaba Kurumsal uygulamaları sayfasındaki Hello "Ekle" düğmesi](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. Merhaba, **bir uygulama eklemek** penceresinde girin **dropbox** hello arama kutusuna ve ardından **iş için Dropbox** hello sonuçları listesinde.

  ![Merhaba "dropbox" için arama uygulama sayfası ekleme](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. Merhaba üzerinde **çoklu oturum açma** sayfasında, **çoklu oturum açma** hello sol bölmesinde ve ardından girin **user.mail** hello içinde **kullanıcı tanımlayıcısı** bir kutu. (Bunu UPN varsayılan olarak ayarlanır.)

  ![Merhaba uygulama için çoklu oturum açmayı yapılandırma](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. Dropbox yapılandırması için toodownload hello sertifika toouse seçin **yapılandırma DropBox**ve ardından **SAML çoklu oturum üzerinde hizmet URL'si** hello listesinde.

  ![Dropbox yapılandırması için Hello sertifika yükleme](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. Oturum açma tooDropbox hello ile oturum açma URL'si hello **çoklu oturum açma** sayfası.

  ![Merhaba Dropbox oturum açma sayfası](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. Başlangıç menüsünden seçin **Yönetici Konsolu**.

  ![Merhaba Dropbox menüsünde Hello "Yönetici Konsolu" bağlantısı](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. Merhaba, **kimlik doğrulaması** iletişim kutusunda **daha fazla**, hello sertifikasını karşıya yükleyin ve ardından hello **URL'de oturum** kutusunda, hello SAML çoklu oturum açma URL'sini girin.

  ![Merhaba hello "Daha fazla" bağlantısına daraltılmış kimlik doğrulama iletişim kutusu](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![kimlik doğrulama iletişim kutusu Hello "Oturum açma URL'si" Merhaba genişletilmiş](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. tooconfigure otomatik kullanıcı hello Azure portal, Kurulum'da seçin **sağlama** hello sol bölmesinde seçin **otomatik** hello içinde **sağlama modu** kutusuna ve ardından seçin **Yetkilendirmek**.

  ![Otomatik kullanıcı sağlamayı hello Azure portalını yapılandırma](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

Konuk veya üye kullanıcı hello Dropbox uygulamada ayarlanan sonra Dropbox'tan ayrı bir davet alırsınız. toouse Dropbox çoklu oturum açma davetlilerin bir bağlantıya tıklayarak hello daveti kabul etmelisiniz.

## <a name="box"></a>Box
SAML Protokolü hello üzerinde temel Federasyon kullanarak kullanıcıların tooauthenticate kutusunu Konuk kullanıcılar kendi Azure AD hesabı ile etkinleştirebilirsiniz. Bu yordamda, meta veri tooBox.com karşıya yükleyin.

1. Merhaba kutusunu uygulama hello Kurumsal uygulamalardan ekleyin.

2. Çoklu oturum açma sırasının hello yapılandırın:

  ![Kutusunu çoklu oturum açmayı yapılandırın](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 a. Merhaba, **URL üzerinde oturum** kutusunda, hello Azure portal kutusunu, hello oturum açma URL'si uygun şekilde ayarlandığından emin olun. Bu hello Box.com kiracınızın URL'dir. Merhaba adlandırma kuralına uymalı *https://.box.com*.  
 Merhaba **tanımlayıcısı** toothis uygulanmaz uygulama, ancak bu zorunlu bir alan görünmeye.

 b. Merhaba, **kullanıcı tanımlayıcısı** kutusuna **user.mail** (için SSO Konuk hesapları için).

 c. Altında **SAML imzalama sertifikası**, tıklatın **yeni sertifika oluştur**.

 d. Box.com Kiracı toouse Azure AD kimlik sağlayıcısı olarak, yapılandırma toobegin hello meta veri dosyasını indirin ve tooyour yerel sürücüye kaydedin.

 e. Çoklu oturum açma, yapılandıran hello meta veri dosyası toohello kutusunu destek ekibi, iletin.

3. Merhaba sol bölmesinde, Azure AD otomatik kullanıcı kurulumu seçin **sağlama**ve ardından **Authorize**.

  ![Azure AD tooconnect tooBox yetkilendirmek](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

Dropbox davetlilerin gibi kutusunu davetlilerin hello Box uygulamasına kendi davetini almak gerekir.

## <a name="next-steps"></a>Sonraki adımlar

Azure AD B2B işbirliği makalelerini aşağıdaki hello bakın:

* [Azure AD B2B işbirliği nedir?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B işbirliği kullanıcı özellikleri](active-directory-b2b-user-properties.md)
* [B2B işbirliği kullanıcı tooa rolü ekleme](active-directory-b2b-add-guest-to-role.md)
* [B2B işbirliği davetleri temsilci seçme](active-directory-b2b-delegate-invitations.md)
* [Dinamik gruplar ve B2B işbirliği](active-directory-b2b-dynamic-groups.md)
* [B2B işbirliği kodu ve PowerShell örnekleri](active-directory-b2b-code-samples.md)
* [B2B işbirliği kullanıcı belirteçleri](active-directory-b2b-user-token.md)
* [B2B işbirliği kullanıcı taleplerini eşleme](active-directory-b2b-claims-mapping.md)
* [Office 365 dış paylaşım](active-directory-b2b-o365-external-user.md)
* [B2B işbirliği geçerli sınırlamalar](active-directory-b2b-current-limitations.md)
