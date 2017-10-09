---
title: "oturum açtıktan sonra bir uygulamanın sayfasında aaaError | Microsoft Docs"
description: "Bir hata Hello uygulama kendisini yayar zaman nasıl tooresolve sorunları Azure AD ile oturum açın"
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
ms.openlocfilehash: 317b6f8e6417520ead80ae4e26c591ba6b134683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a>Oturum açtıktan sonra bir uygulamanın sayfada hata

Bu senaryoda, Azure AD hello kullanıcı oturumu, ancak Merhaba uygulaması hello kullanıcı toosuccessfully bitiş hello oturum akışı sağlanmıyor hata görüntüleme. Bu senaryoda, Merhaba uygulaması hello yanıt sorunu Azure AD tarafından kabul etmiyor.

Merhaba uygulaması Azure AD'den hello yanıt neden kabul etmediğiniz bazı olası nedenleri vardır. Merhaba uygulamasında Hello hatası yeterince Temizle tooknow değilse ne sonra hello yanıtta eksik:

-   Merhaba uygulaması hello Azure AD Galerisi, hello makaledeki tüm hello adımları takip doğrulayıp [nasıl toodebug SAML tabanlı tek oturum açma tooapplications Azure Active Directory'de](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).

-   Gibi bir araç kullanın [Fiddler](http://www.telerik.com/fiddler) toocapture SAML istek, SAML yanıtını ve SAML belirteci.

-   Merhaba SAML yanıtını, eksik olana hello uygulama satıcı tooknow ile paylaşır.

## <a name="missing-attributes-in-hello-saml-response"></a>Merhaba SAML yanıtını eksik öznitelikleri

tooadd hello Azure AD yapılandırma toobe hello Azure AD yanıt olarak gönderilen bir öznitelikte hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

   * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Tooconfigure çoklu oturum açma hello uygulamasını seçin.

7.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  tıklatın **görüntüleme ve düzenleme diğer tüm kullanıcı özniteliklerini altında** hello **kullanıcı öznitelikleri** bölüm tooedit hello kullanıcı oturum açtığında gönderilen toobe toohello hello SAML belirteci uygulamada öznitelikleri.

   bir öznitelik tooadd:

   * tıklatın **Ekle özniteliği**. Merhaba girin **adı** ve hello select hello **değeri** gelen hello açılır.

   * Tıklatın **kaydedin.** Yeni bir öznitelik hello hello tablosundaki bakın.

9.  Merhaba yapılandırmayı kaydedin.

Bir sonraki defa Hello toohello uygulamada oturum açtığında Azure AD hello yeni öznitelik hello SAML yanıtını gönderir.

## <a name="hello-application-expects-a-different-user-identifier-value-or-format"></a>Merhaba uygulaması farklı kullanıcı tanımlayıcısı value veya format bekliyor

Merhaba oturum açma toohello uygulama hello SAML yanıtını rolleri gibi öznitelikleri eksik veya Merhaba uygulaması hello Entityıd özniteliği için farklı bir biçim bekleniyordu nedeniyle başarısız oluyor.

## <a name="add-an-attribute-in-hello-azure-ad-application-configuration"></a>Bir öznitelik hello Azure AD uygulama yapılandırmasında ekleyin:

toochange hello kullanıcı tanımlayıcısı değeri hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

   * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Tooconfigure çoklu oturum açma hello uygulamasını seçin.

7.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  Merhaba altında **kullanıcı öznitelikleri**, select hello hello kullanıcılarınız için benzersiz tanımlayıcı **kullanıcı tanımlayıcısı** açılır.

## <a name="change-entityid-user-identifier-format"></a>Entityıd (kullanıcı tanımlayıcısı) biçimini değiştirme

Merhaba uygulaması hello Entityıd özniteliği için başka bir biçime görüyorsa. Ardından, Azure AD hello yanıtta toohello uygulama kullanıcı kimlik doğrulamasından sonra gönderir mümkün tooselect hello Entityıd (kullanıcı tanımlayıcısı) biçimi olmayacaktır.

Merhaba NameID özniteliği (kullanıcı tanımlayıcısı) için Azure AD select hello biçimi seçili hello değere göre veya hello SAML AuthRequest hello uygulama tarafından istenen biçim hello. Daha fazla bilgi için hello makalesine bakın [tek oturum açma SAML Protokolü](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) NameIDPolicy altında hello bölüm.

## <a name="hello-application-expects-a-different-signature-method-for-hello-saml-response"></a>Merhaba uygulaması farklı imza yöntemi hello SAML yanıtını için bekliyor

Merhaba SAML belirtecine hangi kısımlarının Azure Active Directory tarafından dijital olarak imzalanmış toochange. Merhaba adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

  * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Tooconfigure çoklu oturum açma hello uygulamasını seçin.

7.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  tıklatın **Göster gelişmiş sertifika imzalama ayarları** hello altında **SAML imzalama sertifikası** bölümü.

9.  Select hello uygun **imzalama seçeneği** hello uygulama tarafından beklenen:

  * Oturum SAML yanıtını

  * Oturum açma SAML yanıtını ve onaylama

  * Oturum SAML onayı

Bir sonraki defa Hello toohello uygulamada oturum açtığında, Azure AD oturum seçili hello SAML yanıtını parçası hello.

## <a name="hello-application-expects-hello-signing-algorithm-toobe-sha-1"></a>Merhaba uygulaması algoritması toobe SHA-1 imzalama hello bekliyor

Varsayılan olarak, Azure AD çoğu güvenlik algoritması hello kullanarak hello SAML belirteci imzalar. Merhaba oturum algoritma tooSHA-1 değiştirme hello uygulama tarafından gerekli kılınmadıkça hiçbir önerilmez.

toochange imzalama algoritmasını Merhaba, hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

   * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Tooconfigure çoklu oturum açma hello uygulamasını seçin.

7.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  tıklatın **Göster gelişmiş sertifika imzalama ayarları** hello altında **SAML imzalama sertifikası** bölümü.

9.  SHA-1, hello seçin **imzalama algoritması**.

Sonraki kullanıcı işaretlerini toohello uygulamada Merhaba, SAML belirteci SHA-1 algoritmasını kullanarak Azure AD oturum hello.

## <a name="next-steps"></a>Sonraki adımlar
[Nasıl toodebug SAML tabanlı tek oturum açma tooapplications Azure Active Directory'de](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
