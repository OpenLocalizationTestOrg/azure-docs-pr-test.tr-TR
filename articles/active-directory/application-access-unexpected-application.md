---
title: "uygulamaları listem aaaUnexpected uygulamada | Microsoft Docs"
description: "Nasıl toosee kiracınızda tüm uygulamaları ve uygulamaların kurumsal uygulamalar altındaki tüm uygulamalar listenizde görüntülenme anlama"
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
ms.openlocfilehash: 2f974046b655bc36a05f002c56511a8a988cd01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-application-in-my-applications-list"></a>My uygulamalar listesinde beklenmeyen uygulama

Bu makale uygulamaları görüntülenme toounderstand yardımcı, **tüm uygulamaları** altında listesinde **kurumsal uygulamalar**. 

## <a name="how-toosee-all-applications-in-your-tenant"></a>Nasıl toosee kiracınızda bulunan tüm uygulamalar

toosee tüm Kiracı uygulamalarda Merhaba, toouse hello gereksinim **filtre** tooshow kontrol **tüm uygulamaları** hello altında **tüm uygulamaları** listesi. toodo Bu, başlangıç adımları aşağıdaki:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

6.  Hello kullan hello tıklatın **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini**.

7.  Merhaba üzerinde **filtre** dikey penceresinde, kümesi hello **Göster** çok seçenek**tüm uygulamaları.**

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a>Belirli bir uygulama my tüm uygulamalar listesinde neden görünüyor?

Çok filtre zaman**tüm uygulamaları**, hello **tüm uygulamaları** **listesi** her hizmet sorumlusu nesnesi kiracınızda gösterir. Hizmet sorumlusu nesneleri, çeşitli yollarla bu listede görünebilir:

1.  Herhangi bir uygulama hello uygulama Galerisi'nden eklediğinizde dahil olmak üzere:

   1. **Azure AD galeri uygulamaları** – bir tek oturum açma için Azure AD ile önceden tümleştirilmiş uygulama.

   2. **Uygulama proxy'si uygulamalar** – tooprovide güvenli çoklu oturum açma tooexternally istediğiniz şirket içi ortamınızda çalışan bir uygulama.

   3. **Özel geliştirilmiş uygulamaları** – üzerinde toodevelop kuruluşunuz isteyen bir uygulama hello Azure AD uygulama geliştirme platformu, ancak var henüz.

   4. **Galeri olmayan uygulamaları** – kendi uygulamalarınızı Getir! İstediğiniz herhangi bir web bağlantıyı ya da bir kullanıcı adı ve parola alanı işleyen herhangi bir uygulama SAML veya Openıd Connect protokollerini destekler veya çoklu oturum açma için Azure AD ile toointegrate istediğiniz SCIM'yi destekler.

2.  İçin imzalarken veya 3'e, oturum açma<sup>rd</sup> taraf uygulama Azure Active Directory ile tümleşik. Bunun bir örneği [Smartsheet](https://app.smartsheet.com/b/home) veya [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).

3.  İçin imzalama veya bir lisans tooa kullanıcı veya grup tooa birinci taraf uygulama ekleme, ister [Microsoft Office 365](http://products.office.com/).

4.  Hello kullanarak özel geliştirilmiş bir uygulama oluşturarak yeni bir uygulama kaydı eklediğinizde [uygulama kayıt defteri](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).

5.  Hello kullanarak özel geliştirilmiş bir uygulama oluşturarak yeni bir uygulama kaydı eklediğinizde [V2.0 uygulama kayıt portalı](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).

6.  Bir uygulama eklediğinizde Visual Studio'nun kullanarak geliştirirken [ASP.net kimlik doğrulama yöntemleri](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) veya [bağlantılı Hizmetler](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).

7.  Hello kullanarak bir hizmet sorumlusu nesnesi oluştururken [Azure AD PowerShell Modülü](/powershell/azure/install-adv2?view=azureadps-2.0).

8.  Olduğunda, [tooan uygulama onay](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) bir kiracı yönetici toouse veri olarak.

9.  Zaman bir [kullanıcı izin tooan uygulama](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) kiracınızda toouse veri.

10. Kiracınızda verileri depolamak belirli hizmetleri etkinleştirdiğinizde. Bunun bir örneği olan parola hangi modellenir sıfırlama, güvenli bir şekilde İlkesi bir hizmet asıl toostore parolanızı sıfırlayın.

uygulamaları tooyour dizin nasıl eklenir hakkında daha fazla ayrıntı tooget okuma [neden ve nasıl uygulamaları tooAzure AD eklenen](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a>Bu belirli kullanıcının veya grubun atama tooan uygulama tooremove istiyorum

tooremove bir kullanıcı veya grup ataması tooan uygulama adımları hello listelenen hello [bir kuruluş uygulama Azure Active Directory'de bir kullanıcı veya grup atamasını kaldırmak](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) makalesi.

## <a name="i-want-toodisable-all-access-tooan-application-for-every-user"></a>Her kullanıcı için tüm erişim tooan uygulama toodisable istiyorum

toodisable tüm kullanıcı oturum açma işlemleri tooan uygulama hello adımları hello listelenen [kullanıcı oturum açma işlemlerine Azure Active Directory'de bir kurumsal uygulama için devre dışı bırakma](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) makalesi.

## <a name="i-want-toodelete-an-application-entirely"></a>Toodelete uygulamanın tamamen istiyorum

çok**bir uygulamayı silmek**, aşağıdaki hello yönergeleri izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

  * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Toodelete hello uygulamasını seçin.

7.  Merhaba uygulamanın yüklediği sonra tıklayın **silmek** hello üst uygulamanın simgesinden **genel bakış** dikey.

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a>Tüm gelecekteki kullanıcı onayı işlemleri tooany uygulamasını toodisable istiyorum

Tüm dizin önlemek için son kullanıcıların onaylıyorsunuz tooany uygulamasından kullanıcı izni devre dışı bırakılıyor. Yöneticiler hala kullanıcının behalves üzerinde onay. uygulama hakkında daha fazla toolearn onay ve neden olabilir veya bu, okuma toodo istemeyen [anlama kullanıcı ve yönetici onayı](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).

çok**tüm dizininizdeki tüm gelecekteki kullanıcı onayı işlemleri devre dışı**, aşağıdaki hello yönergeleri izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.

5.  Tıklatın **kullanıcı ayarlarını**.

6.  Tüm gelecekteki kullanıcı onayı işlemleri hello ayarı tarafından devre dışı **kullanıcıların kendi verilerini uygulamaları tooaccess izin verebilir** çok geçiş**Hayır** hello tıklatıp **kaydetmek** düğmesi.

## <a name="next-steps"></a>Sonraki adımlar
[Azure Active Directory ile uygulamaları yönetme](active-directory-enable-sso-scenario.md)
