---
title: "aaaHow tooconfigure federe bir galeri olmayan uygulama için çoklu oturum açmayı | Microsoft Docs"
description: "Azure AD ile toointegrate istediğiniz özel bir galeri olmayan uygulama için çoklu oturum açmayı tooconfigure nasıl Federasyon"
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
ms.openlocfilehash: f4a37cb500c075d0ce917ad8f13411f2ce208c56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a>Nasıl bir galeri olmayan uygulama için çoklu oturum açmayı tooconfigure Federasyon

Galeri olmayan uygulama tooconfigure toohave Azure AD premium gerekir ve Merhaba uygulaması SAML 2.0 destekler. Azure AD sürümleri hakkında daha fazla bilgi için ziyaret [Azure AD fiyatlandırma](https://azure.microsoft.com/pricing/details/active-directory/).

## <a name="overview-of-steps-required"></a>Gerekli adımlara genel bakış
Bir yüksek düzeyde genel bakış hello adımları federe gerekli tooconfigure tek oturum açma için Galeri olmayan aşağıdadır (örneğin, özel) uygulama.

-   [Azure AD (oturum açma URL'si, tanımlayıcı, yanıt URL'si) Hello uygulamanın meta veri değerlerini yapılandırın](#_Configuring_single_sign-on)

-   [Kullanıcı tanımlayıcısı seçin ve kullanıcı öznitelikleri gönderilen toobe toohello uygulaması ekleyin](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Azure AD meta verileri ve sertifika alma](#download-the-azure-ad-metadata-or-certificate)

-   [Merhaba uygulaması (oturum açma URL'si, veren, oturum kapatma URL'si ve sertifika) Azure AD meta veri değerlerini yapılandırın](#_Configuring_single_sign-on)

-   [Kullanıcıların toohello uygulama atama](#_Assign_users_to_the_application)

## <a name="configuring-single-sign-on-toonon-gallery-applications"></a>Çoklu oturum açma toonon-galeri uygulamaları yapılandırma

tooconfigure çoklu oturum açma hello Azure AD Galerisi'nde olmayan bir uygulama için başlangıç adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey.

6.  tıklatın **olmayan galeri uygulama** hello içinde **kendi uygulama Ekle** bölümü

7.  Merhaba Merhaba uygulaması hello adını **adı** metin kutusu.

8.  Tıklatın **Ekle** button, tooadd Merhaba uygulaması.

9.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

10. Seçin **SAML tabanlı oturum açma** hello içinde **modu** açılır.

11. Merhaba gerekli değerleri girin **etki alanı ve URL'ler.** Bu değerleri hello uygulama satıcısından almanız gerekir.

   1. IDP tarafından başlatılan SSO'yu olarak tooconfigure hello uygulama hello yanıt URL'si ve hello tanımlayıcısı girin.

   2. **İsteğe bağlı:** tooconfigure hello uygulama SP tarafından başlatılan SSO'yu olarak hello oturum URL'yi, gerekli bir değerdir.

12. Merhaba, **kullanıcı öznitelikleri**, select hello hello kullanıcılarınız için benzersiz tanımlayıcı **kullanıcı tanımlayıcısı** açılır.

13. **İsteğe bağlı:** tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** tooedit Merhaba, kullanıcı oturum açtığında gönderilen toobe toohello hello SAML belirteci uygulamada öznitelikleri.

   bir öznitelik tooadd:

   1. tıklatın **Ekle özniteliği**. Merhaba girin **adı** ve hello select hello **değeri** gelen hello açılır.

   2. Tıklatın **kaydedin.** Yeni bir öznitelik hello hello tablosundaki bakın.

14. tıklatın **yapılandırma &lt;uygulama adı&gt;**  tooaccess belgelerine nasıl tooconfigure çoklu oturum açma hello uygulamada. Ayrıca, Azure AD URL'leri ve hello uygulama için gerekli sertifika sahiptir.

15. [Kullanıcıların toohello uygulama atayın.](#assign-users-to-the-application)

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Kullanıcı tanımlayıcısı seçin ve kullanıcı öznitelikleri gönderilen toobe toohello uygulaması ekleyin

tooselect kullanıcı tanımlayıcısı Merhaba veya kullanıcı öznitelikleri ekleme, hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

  * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Çoklu oturum açma yapılandırdığınız hello uygulaması'nı seçin.

7.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  Merhaba altında **kullanıcı öznitelikleri** bölümünde, select hello hello kullanıcılarınız için benzersiz tanımlayıcı **kullanıcı tanımlayıcısı** açılır. Merhaba seçeneği hello uygulama tooauthenticate hello kullanıcı toomatch hello beklenen değer gerekiyor.

 >[! Azure AD seçili hello değere göre hello NameID özniteliği (kullanıcı tanımlayıcısı) için hello biçimini seçin veya hello SAML AuthRequest hello uygulama tarafından istenen biçim hello unutmayın}. Daha fazla bilgi için hello makalesine bakın [tek oturum açma SAML Protokolü](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) NameIDPolicy altında hello bölüm.
 >
 >

9.  tooadd kullanıcı öznitelikleri, tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** tooedit Merhaba, kullanıcı oturum açtığında gönderilen toobe toohello hello SAML belirteci uygulamada öznitelikleri.

   bir öznitelik tooadd:

   1. tıklatın **Ekle özniteliği**. Merhaba girin **adı** ve hello select hello **değeri** gelen hello açılır.

   2. Tıklatın **kaydedin.** Yeni bir öznitelik hello hello tablosundaki bakın.

## <a name="download-hello-azure-ad-metadata-or-certificate"></a>Hello Azure AD meta verileri veya sertifika yükleme

toodownload hello uygulama meta verileri veya sertifika Azure AD'den hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

   * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Çoklu oturum açma yapılandırdığınız hello uygulaması'nı seçin.

7.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  Çok Git**SAML imzalama sertifikası** bölümünde ve ardından **karşıdan** sütun değeri. Çoklu oturum açma yapılandırma hangi hello uygulama gerektirir bağlı olarak, meta veri XML hello veya sertifika hello ya da hello seçeneği toodownload bakın.

Azure AD, URL tooget hello meta verilerinin sağlamaz. Merhaba meta veriler yalnızca bir XML dosyası olarak alınabilir.

## <a name="assign-users-toohello-application"></a>Kullanıcıların toohello uygulama atama

tooassign bir veya daha fazla kullanıcı tooan uygulama, doğrudan başlangıç adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

  * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Tooassign kullanıcı toofrom hello listesini hello uygulamasını seçin.

7.  Merhaba uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  Hello tıklatın **Ekle** hello üstünde düğmesi **kullanıcılar ve gruplar** listesi tooopen hello **eklemek atama** dikey.

9.  Merhaba tıklatın **kullanıcılar ve gruplar** hello seçicisini **eklemek atama** dikey.

10. Merhaba türü **tam adı** veya **e-posta adresi** hello atama ilgilenen hello kullanıcının **ad veya e-posta adresine göre arama** arama kutusu.

11. Merhaba getirin **kullanıcı** hello listesi tooreveal içinde bir **onay kutusunu**. Kullanıcı toohello Hello onay kutusu sonraki toohello kullanıcının profili fotoğraf veya logosu tooadd tıklatın **seçili** listesi.

12. **İsteğe bağlı:** çok isterseniz**birden fazla kullanıcı ekleme**, başka bir tür **tam adı** veya **e-posta adresi** hello içine **ada göre ara veya e-posta adresi** arama kutusu ve bu kullanıcı toohello hello onay kutusunu tooadd tıklatın **seçili** listesi.

13. Kullanıcıların seçerek bittiğinde hello tıklatın **seçin** düğmesini tooadd bunları kullanıcılar ve gruplar toobe toohello listesi atanan toohello uygulama.

14. **İsteğe bağlı:** hello tıklatın **rolü Seç** hello seçicide **eklemek atama** dikey tooselect rol seçtiğiniz tooassign toohello kullanıcılar.

15. Merhaba tıklatın **atamak** düğmesini tooassign hello uygulama toohello seçilen kullanıcılar.

Bir kısa süre sonra seçtiğiniz hello kullanıcıların hello çözüm Açıklama bölümünde açıklanan yöntemleri kullanarak bu uygulamaları hello mümkün toolaunch olması.

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a>Gönderilen tooan uygulama Hello SAML talepler özelleştiriliyor

toolearn tooyour uygulama toocustomize hello SAML öznitelik taleplerini gönderilen nasıl bkz [talep eşleme Azure Active Directory'de](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) daha fazla bilgi için.

## <a name="next-steps"></a>Sonraki adımlar
[Uygulama proxy'si ile çoklu oturum açma tooyour uygulamaları sağlayın](active-directory-application-proxy-sso-using-kcd.md)
