---
title: "Erişim paneli Web sitesine oturum açma sorunu | Microsoft Docs"
description: "Erişim paneli kullanmak için kaydolun çalışılırken karşılaşabileceğiniz sorunları gidermek için yönergeler"
services: active-directory
documentationcenter: 
author: ajamess
manager: mtillman
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviwer: japere
ms.openlocfilehash: 0f50a705d4453970d039c2219aef8e1a411fd533
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/11/2017
---
# <a name="problem-signing-in-to-the-access-panel-website"></a>Erişim paneli Web sitesine oturum açma sorunu

Erişim paneli, Azure AD Yöneticisi erişim verildi görünümü ve başlatma bulut tabanlı uygulamalar Azure Active Directory (Azure AD) bir iş veya Okul hesabı olan bir kullanıcının sağlayan bir web tabanlı portal olmaktır. Azure AD sürümleri olan bir kullanıcı, Self Servis grup ve erişim paneli üzerinden uygulama yönetim özellikleri de kullanabilirsiniz. Erişim paneli Azure Portalı'ndan ayrıdır ve kullanıcıların bir Azure aboneliğine sahip olmasını gerektirmez.

Azure AD'de bir iş veya Okul hesabı varsa kullanıcıların erişim panelinde oturum açabilirsiniz.

-   Kullanıcıların doğrudan Azure AD tarafından doğrulanabilir.

-   Active Directory Federasyon Hizmetleri (AD FS) kullanarak kullanıcıların kimlik doğrulaması.

-   Kullanıcıların Windows Server Active Directory tarafından doğrulanabilir.

Bir kullanıcı Azure veya Office 365 için bir abonelik varsa ve Azure portal ya da bir Office 365 uygulaması kullanarak, erişim paneli sorunsuz bir şekilde gerek kalmadan yeniden oturum açmak için kullandığınız mümkün olacaktır. Kimliği doğrulanmamış kullanıcılar kendi hesabı için Azure AD'de kullanıcı adı ve parola kullanarak oturum açın istenir. Kuruluşun Federasyon yapılandırdıysa, kullanıcı adı yazmaya yeterli olur.

## <a name="general-issues-to-check-first"></a>İlk denetlemek için genel sorunlar 

-   Emin olun kullanıcı olduğundan oturum açma için **URL'yi düzeltin**: <https://myapps.microsoft.com>

-   Kullanıcının tarayıcısının URL ekledi emin olun, **Güvenilen siteler**

-   Kullanıcının hesabı olduğundan emin olun **etkin** için oturum açmalar.

-   Kullanıcının hesabı olduğundan emin olun **kilitli değil.**

-   Kullanıcının emin olun **parola süresi değil veya unutulursa.**

-   Emin olun **çok faktörlü kimlik doğrulaması** kullanıcı erişimini engellemediğinden.

-   Emin olun bir **koşullu erişim ilkesi** veya **kimlik koruması** İlkesi kullanıcı erişimini engellemediğinden.

-   Olduğundan emin olun kullanıcının **kimlik doğrulaması kişi bilgilerini** yürütülebilmesi çok faktörlü kimlik doğrulaması veya koşullu erişim ilkeleri izin güncel değil.

-   Tarayıcınızın tanımlama bilgilerini temizleyip ve yeniden oturum açmaya de deneyin emin olun.

## <a name="meeting-browser-requirements-for-the-access-panel"></a>Erişim paneli toplantı tarayıcı gereksinimleri

Erişim paneli JavaScript destekleyen bir tarayıcı gerektirir ve CSS etkinleştirdi. Parola tabanlı çoklu oturum açma (SSO) erişimi Masası'nda kullanmak için erişim paneli uzantısı kullanıcının tarayıcısında yüklenmesi gerekir. Bir kullanıcı, parola tabanlı SSO için yapılandırılmış bir uygulama seçtiğinde bu uzantıyı otomatik olarak yüklenir.

Parola tabanlı, SSO için son kullanıcının tarayıcılar olabilir:

-   Internet Explorer 8, 9, 10, 11--Windows 7 veya üzeri

-   Edge Windows 10 Anniversary Edition veya daha yenisi 

-   Chrome--Windows 7 veya daha sonra ve MacOS x veya sonraki sürümlerde

-   Firefox 26,0 veya daha sonra--Windows XP SP2 veya sonraki ve Mac OS X 10,6 veya üzeri


## <a name="problems-with-the-users-account"></a>Kullanıcı hesabının sorunları

Kullanıcı hesabında bir sorun nedeniyle erişim Paneli'ne erişim engellenebilir. Aşağıdaki sorun giderme ve kullanıcıların ve hesap ayarları ile sorunları bazı yöntemler şunlardır:

-   [Bir kullanıcı hesabı Azure Active Directory içinde olup olmadığını kontrol edin](#check-if-a-user-account-exists-in-azure-active-directory)

-   [Bir kullanıcının hesap durumunu denetle](#check-a-users-account-status)

-   [Bir kullanıcının parolasını sıfırlama](#reset-a-users-password)

-   [Self servis parola sıfırlamayı etkinleştirme](#enable-self-service-password-reset)

-   [Bir kullanıcının çok faktörlü kimlik doğrulama durumunu denetle](#check-a-users-multi-factor-authentication-status)

-   [Bir kullanıcının kimlik doğrulaması ile ilgili kişi bilgileri](#check-a-users-authentication-contact-info)

-   [Bir kullanıcı grup üyeliklerini denetleyin](#check-a-users-group-memberships)

-   [Bir kullanıcının atanan lisansları denetleme](#check-a-users-assigned-licenses)

-   [Bir kullanıcı bir lisans atama](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a>Bir kullanıcı hesabı Azure Active Directory içinde olup olmadığını kontrol edin

Bir kullanıcı hesabının mevcut olup olmadığını denetlemek için aşağıdaki adımları izleyin:

1.  Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.

3.  Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.

4.  tıklatın **kullanıcılar ve gruplar** Gezinti menüsünde.

5.  tıklatın **tüm kullanıcılar**.

6.  **Arama** ilgilendiğiniz kullanıcı için ve **satıra tıklayın** seçin.

7.  Beklediğiniz ve hiçbir veri eksik gibi göründüğünü emin olmak için kullanıcı nesnesinin özelliklerini denetleyin.

### <a name="check-a-users-account-status"></a>Bir kullanıcının hesap durumunu denetle

Bir kullanıcı hesabı durumunu denetlemek için aşağıdaki adımları izleyin:

1.  Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.

3.  Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.

4.  tıklatın **kullanıcılar ve gruplar** Gezinti menüsünde.

5.  tıklatın **tüm kullanıcılar**.

6.  **Arama** ilgilendiğiniz kullanıcı için ve **satıra tıklayın** seçin.

7.  tıklatın **profil**.

8.  Altında **ayarları** emin **blok oturum** ayarlanır **Hayır**.

### <a name="reset-a-users-password"></a>Bir kullanıcının parolasını sıfırlama

Bir kullanıcının parolasını sıfırlamak için aşağıdaki adımları izleyin:

1.  Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.

3.  Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.

4.  tıklatın **kullanıcılar ve gruplar** Gezinti menüsünde.

5.  tıklatın **tüm kullanıcılar**.

6.  **Arama** ilgilendiğiniz kullanıcı için ve **satıra tıklayın** seçin.

7.  tıklatın **parola sıfırlama** kullanıcı dikey pencerenin üstündeki düğmesi.

8.  tıklatın **parola sıfırlama** düğmesini **parola sıfırlama** görünür dikey.

9.  Kopya **geçici parola** veya **yeni bir parola girin** kullanıcı için.

10. Bu yeni parolayı kullanıcıya iletişim, Azure Active Directory'ye sonraki oturum açma sırasında bu parolayı değiştirmeniz gerekiyor.

### <a name="enable-self-service-password-reset"></a>Self Servis parola sıfırlama etkinleştirme

Self Servis parola sıfırlamayı etkinleştirmek için dağıtım adımları izleyin:

-   [Azure Active Directory parolalarını sıfırlamalarına olanak tanıma](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [Sıfırlama veya Active Directory şirket içi parolalarını değiştirmek kullanıcıları etkinleştir](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a>Bir kullanıcının çok faktörlü kimlik doğrulama durumunu denetle

Bir kullanıcının çok faktörlü kimlik doğrulama durumunu denetlemek için aşağıdaki adımları izleyin:

1.  Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.

3.  Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.

4.  tıklatın **kullanıcılar ve gruplar** Gezinti menüsünde.

5.  tıklatın **tüm kullanıcılar**.

6.  tıklatın **çok faktörlü kimlik doğrulaması** dikey pencerenin üstündeki düğmesi.

7.  Bir kez **multi-Factor Authentication Yönetim Portalı** yüklendiğinde emin olduğunuz üzerinde **kullanıcılar** sekmesi.

8.  Kullanıcı, arama, filtreleme veya sıralama kullanıcı listesinde bulun.

9.  Kullanıcı kullanıcılar listesinden seçin ve **etkinleştirmek**, **devre dışı**, veya **zorla** istediğiniz gibi çok faktörlü kimlik doğrulaması.

   >[!NOTE]
   >Bir kullanıcı ise bir **zorlanmış** durumunda, ayarlayın bunları **devre dışı** geçici olarak kendi hesaba geri izin vermek için. Daha sonra geri oldukları sonra durumlarına değiştirebilirsiniz **etkin** yeniden sonraki oturum açma sırasında kişi bilgileri yeniden kaydetmek için bunları gerektirecek şekilde. Alternatif olarak, içindeki adımları takip edebilirsiniz [bir kullanıcının kimlik doğrulaması ile ilgili kişi bilgileri](#check-a-users-authentication-contact-info) doğrulamak veya onlar için bu veri kümesi için.
   >
   >

### <a name="check-a-users-authentication-contact-info"></a>Bir kullanıcının kimlik doğrulaması ile ilgili kişi bilgileri

Çok faktörlü kimlik doğrulaması, koşullu erişim, kimlik koruması ve parola sıfırlama için kullanılan kullanıcı kimlik doğrulaması kişi bilgilerini denetlemek için aşağıdaki adımları izleyin:

1.  Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.

3.  Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.

4.  tıklatın **kullanıcılar ve gruplar** Gezinti menüsünde.

5.  tıklatın **tüm kullanıcılar**.

6.  **Arama** ilgilendiğiniz kullanıcı için ve **satıra tıklayın** seçin.

7.  tıklatın **profil**.

8.  Ekranı aşağı kaydırarak **kimlik doğrulaması kişi bilgilerini**.

9.  **Gözden geçirme** veri, güncelleştirme ve kullanıcı için gerektiği şekilde kaydedildi.

### <a name="check-a-users-group-memberships"></a>Bir kullanıcı grup üyeliklerini denetleyin

Bir kullanıcı grup üyeliklerini denetlemek için aşağıdaki adımları izleyin:

1.  Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.

3.  Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.

4.  tıklatın **kullanıcılar ve gruplar** Gezinti menüsünde.

5.  tıklatın **tüm kullanıcılar**.

6.  **Arama** ilgilendiğiniz kullanıcı için ve **satıra tıklayın** seçin.

7.  tıklatın **grupları** olduğu kullanıcı grupları görmek için bir üyesidir.

### <a name="check-a-users-assigned-licenses"></a>Bir kullanıcının atanan lisansları denetleme

Bir kullanıcının atanan lisansları denetlemek için aşağıdaki adımları izleyin:

1.  Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.

3.  Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.

4.  tıklatın **kullanıcılar ve gruplar** Gezinti menüsünde.

5.  tıklatın **tüm kullanıcılar**.

6.  **Arama** ilgilendiğiniz kullanıcı için ve **satıra tıklayın** seçin.

7.  tıklatın **lisansları** , şu anda kullanıcı lisansları görmek üzere atanır.

### <a name="assign-a-user-a-license"></a>Bir kullanıcı bir lisans atama 

Bir kullanıcıya bir lisans atamak için aşağıdaki adımları izleyin:

1.  Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.

3.  Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.

4.  tıklatın **kullanıcılar ve gruplar** Gezinti menüsünde.

5.  tıklatın **tüm kullanıcılar**.

6.  **Arama** ilgilendiğiniz kullanıcı için ve **satıra tıklayın** seçin.

7.  tıklatın **lisansları** , şu anda kullanıcı lisansları görmek üzere atanır.

8.  tıklatın **atamak** düğmesi.

9.  Seçin **bir veya daha fazla ürün** mevcut ürünler listesinden.

10. **İsteğe bağlı** tıklatın **atama seçenekleri** ürünleri granularly atanacak öğe. Tıklatın **Tamam** ne zaman bu tamamlandı.

11. Tıklatın **atamak** bu lisans bu kullanıcıya atamak için düğmesi.

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a>Bu sorun giderme adımları sorunu çözmezse

bir destek bileti aşağıdaki bilgilerle varsa açın:

-   Bağıntı hata kimliği

-   UPN (kullanıcı e-posta adresi)

-   Kiracı Kimliği

-   Tarayıcı türü

-   Saat dilimi ve saat/zaman çerçevesine hata oluşuyor

-   Fiddler izlemeleri

## <a name="next-steps"></a>Sonraki adımlar
[Çoklu oturum açma uygulamalarınızı uygulama proxy'si ile sağlayın.](active-directory-application-proxy-sso-using-kcd.md)
