---
title: "aaaHow tooconfigure parola tek oturum açma için Galeri olmayan applicationn | Microsoft Docs"
description: "Tooconfigure için özel bir galeri olmayan uygulama güvenliğini nasıl parola tabanlı çoklu oturum açma hello Azure AD uygulama galerisinde listelenmeyen olduğunda"
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
ms.openlocfilehash: e3d0e658f792a0a63110a198811edc66acd6ccf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>Tooconfigure parola nasıl tek bir galeri olmayan uygulaması için oturum açma

Ayrıca toohello seçenekleri bulunan hello Azure AD uygulama galerisinde içinde hello seçeneği tooadd de sahip bir **galeri olmayan uygulama** zaman hello uygulamasıyla listelenmemiş vardır. Bu özelliği kullanarak, kuruluşunuzda zaten herhangi bir uygulama ya da kullanıyor olabileceğiniz herhangi bir üçüncü taraf uygulama zaten hello parçası olmayan bir satıcıdan ekleyebileceğiniz [Azure AD uygulama galerisinde](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).

Bir galeri olmayan uygulama ekledikten sonra daha sonra bu uygulamanın kullandığı hello seçerek hello tek oturum açma yöntemi yapılandırabilirsiniz **çoklu oturum açma** hello kuruluş uygulamasında Gezinti öğede [Azure portalı ](https://portal.azure.com/).

Merhaba çoklu oturum açma yöntemleri kullanılabilir tooyou biri hello [parola tabanlı çoklu oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) seçeneği. Merhaba ile **bir galeri olmayan uygulama eklemek** deneyimi, bir HTML tabanlı kullanıcıadı işleyen herhangi bir uygulama tümleştirebilir ve parola giriş alanı, önceden tümleştirilmiş uygulamaların bizim kümesinde olmasa bile.

Bu çalışır hello yoludur hello parçası olan teknoloji değiştirilene sayfası tarafından bize tooauto sağlayan erişim paneli uzantısı-kullanıcı adı ve parola giriş alanlarının algılamak, belirli bir uygulama Örneğiniz için bunları güvenli bir şekilde saklayın. Kullanıcı adlarını güvenli bir şekilde yeniden yürütme ve parolaları toothose alanları bir kullanıcı hello uygulama erişim Paneli'ne toothat uygulamaya gider.

Bu tooget her türlü uygulama hızlı bir şekilde Azure AD ile tümleştirme kullanmaya ve böylece kullanışlı bir yoludur.

-   Tümleştirme **Merhaba Dünya herhangi bir uygulamada** ile Azure AD kiracınız, HTML kullanıcı adı ve parola giriş alanını işleyen kadar uzun süre

-   Etkinleştirme **kullanıcılarınız için çoklu oturum açmayı** güvenli bir şekilde depolamak ve kullanıcı adları ve parolalar Merhaba uygulaması için yeniden oynatmak tarafından Azure AD ile tümleşik

-   **Giriş otomatik algıla** alanlar için herhangi bir uygulama ve izin toomanually algılamak hello erişim paneli tarayıcı uzantısı kullanarak bu alanlar otomatik algılamayı bulmaz durumda

-   **Destek oturum açma birden çok alan gerektiren uygulamalar** içinde birden fazla yalnızca kullanıcı adı ve parola alanları toosign gerektiren uygulamalar için

-   **Başlangıç etiketleri özelleştirme** hello kullanıcı adı ve parola giriş alanları kullanıcılarınızın üzerinde hello görmek [uygulama erişim Paneli'ne](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) kimlik bilgilerini girmeleri zaman

-   İzin ver, **kullanıcılar** tooprovide kendi kullanıcı adları ve bunlar yazarak el ile Merhaba üzerinde var olan tüm uygulama hesaplar için parolaları [uygulama erişim paneli](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)

-   İzin bir **hello iş grubunun üyesi** toospecify hello kullanıcı adları ve parolalar atanan tooa kullanıcı hello kullanarak [Self Servis uygulamaya erişim](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) özelliği

-   İzin bir **yönetici** toospecify hello kullanıcı adları ve parolalar hello güncelleştirme kimlik bilgileri kullanılarak tooa kullanıcı atanan özellik ne zaman [kullanıcı tooan uygulama atama](#_How_to_configure_1)

-   İzin bir **yönetici** toospecify paylaşılan hello kullanıcı adı veya parola hello güncelleştirme kimlik bilgilerini kullanarak bir grup kişi tarafından kullanılan özellik ne zaman [grubu tooan uygulama atama](#assign-an-application-to-a-group-directly)

Aşağıda nasıl etkinleştirebilirsiniz açıklar [parola tabanlı çoklu oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooany uygulama hello kullanarak Ekle **bir galeri olmayan uygulama eklemek** karşılaşırsınız.

## <a name="overview-of-steps-required"></a>Gerekli adımlara genel bakış

tooconfigure hello Azure AD Galeriden bir uygulama şunları yapmanız gerekir:

-   [Bir galeri olmayan uygulama ekleme](#add-a-non-gallery-application)

-   [Merhaba uygulaması parola çoklu oturum açma için yapılandırma](#configure-the-application-for-password-single-sign-on)

-   [Merhaba uygulama tooa kullanıcısı veya grubu atayın](#assign-the-application-to-a-user-or-a-group)

    -   [Bir kullanıcı tooan uygulama doğrudan atama](#assign-a-user-to-an-application-directly)

    -   [Uygulama tooa grubu doğrudan atama](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a>Bir galeri olmayan uygulama ekleme

tooadd hello Azure AD galeri, bir uygulamadan hello adımları izleyin:

1.  Açık hello [Azure Portal](https://portal.azure.com) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey

6.  tıklatın **olmayan galeri uygulaması.**

7.  Merhaba, uygulamanızın hello adını **adı** metin kutusu. Seçin **ekleyin.**

Kısa bir süre sonra mümkün toosee hello uygulamanın yapılandırma dikey olabilir.

## <a name="configure-hello-application-for-password-single-sign-on"></a>Merhaba uygulaması parola çoklu oturum açma için yapılandırma

tooconfigure çoklu oturum açma bir uygulama için başlangıç adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

  * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Tooconfigure çoklu oturum açma hello uygulamasını seçin.

7.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  Select hello modu **parola tabanlı oturum açma.**

9.  Merhaba girin **oturum açma URL'si**. Bu kullanıcılar kendi kullanıcı adı ve parola toosign içinde için girdiğiniz yere hello URL'dir. Merhaba oturum alanları hello URL'de göründüğünden emin olun.

10. Kullanıcıların toohello uygulama atayın.

11. Ayrıca, ayrıca hello kullanıcı adına kimlik bilgilerini hello satırları hello kullanıcıların seçerek ve tıklayarak sağlayabilirsiniz **güncelleştirme kimlik bilgileri** ve hello kullanıcılar adına hello kullanıcı adı ve parola girme. Aksi takdirde, kullanıcılar istendiğinde tooenter hello kimlik bilgilerinin kendilerini başlatma bağlı olması.

## <a name="assign-a-user-tooan-application-directly"></a>Bir kullanıcı tooan uygulama doğrudan atama

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

## <a name="assign-an-application-tooa-group-directly"></a>Uygulama tooa grubu doğrudan atama

bir veya daha fazla tooassign doğrudan tooan uygulama hello adımları aşağıdaki grupları:

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

10. Merhaba türü **tam grup adı** hello atama ilgilenen hello grubunun **ad veya e-posta adresine göre arama** arama kutusu.

11. Merhaba getirin **grup** hello listesi tooreveal içinde bir **onay kutusunu**. Kullanıcı toohello Hello onay kutusu sonraki toohello grubun profili fotoğraf veya logosu tooadd tıklatın **seçili** listesi.

12. **İsteğe bağlı:** çok isterseniz**birden fazla grubu Ekle**, başka bir tür **tam grup adı** hello içine **ad veya e-posta adresine göre arama** arama kutusu tıklatıp hello onay kutusunu tooadd bu Grup toohello **seçili** listesi.

13. Grupları seçmek bittiğinde hello tıklatın **seçin** düğmesini tooadd bunları kullanıcılar ve gruplar toobe toohello listesi atanan toohello uygulama.

14. **İsteğe bağlı:** hello tıklatın **rolü Seç** hello seçicide **eklemek atama** dikey tooselect rol tooassign toohello gruplar seçtiniz.

15. Merhaba tıklatın **atamak** düğmesini tooassign hello uygulama toohello seçilen grupları.

Seçtiğiniz hello kullanıcılar kısa bir süre mümkün toolaunch bu uygulamalarında değiştirdikten sonra erişim Paneli'ne hello.

## <a name="next-steps"></a>Sonraki adımlar
[Uygulama proxy'si ile çoklu oturum açma tooyour uygulamaları sağlayın](active-directory-application-proxy-sso-using-kcd.md)
