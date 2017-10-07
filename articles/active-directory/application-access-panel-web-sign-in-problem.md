---
title: "Web sitesi toohello erişim paneli imzalama aaaProblem | Microsoft Docs"
description: "Erişim paneli toouse toosign çalışırken karşılaşabileceğiniz Kılavuzu tootroubleshoot sorunlar hello"
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
ms.reviwer: japere
ms.openlocfilehash: 1037f7c5fbaa9425760ad5739b383c716d5fc3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-signing-in-toohello-access-panel-website"></a>Toohello erişim paneli Web sitesinde oturum açarken bir sorunla

Merhaba erişim paneli, hangi etkinleştirir bir iş veya Okul sahip bir kullanıcı hesabı Azure Active Directory (Azure AD) tooview ve başlatma bulut tabanlı uygulamalarda o hello Azure AD yönetici web tabanlı bir portal erişim verildi ' dir. Azure AD sürümleri olan bir kullanıcı, Self Servis grup ve hello erişim paneli üzerinden uygulama yönetim özellikleri de kullanabilirsiniz. Merhaba erişim paneli hello Azure portal ' ayrıdır ve kullanıcıların toohave bir Azure aboneliği gerektirmez.

Kullanıcılar, Azure AD'de bir iş veya Okul hesabı varsa toohello erişim paneli oturum açabilir.

-   Kullanıcıların doğrudan Azure AD tarafından doğrulanabilir.

-   Active Directory Federasyon Hizmetleri (AD FS) kullanarak kullanıcıların kimlik doğrulaması.

-   Kullanıcıların Windows Server Active Directory tarafından doğrulanabilir.

Bir kullanıcı Azure veya Office 365 için bir abonelik varsa ve hello Azure portal ya da bir Office 365 uygulaması kullanarak, mümkün toouse olacak toosign içinde yeniden gerek kalmadan erişim paneli sorunsuz bir şekilde hello. Kimliği doğrulanmamış kullanıcıların kendi hesabı için Azure AD içinde hello kullanıcı adı ve parola kullanarak, istendiğinde toosign olması. Merhaba kuruluş Federasyon yapılandırdıysa, hello kullanıcı adı yazmaya yeterli olur.

## <a name="general-issues-toocheck-first"></a>Genel toocheck ilk sorunları 

-   Merhaba kullanıcı toohello içinde imzalama emin olun **URL'yi düzeltin**: <https://myapps.microsoft.com>

-   Merhaba kullanıcının tarayıcısının hello URL tooits eklenmiş emin **Güvenilen siteler**

-   Merhaba kullanıcının hesabı olduğundan emin olun **etkin** için oturum açmalar.

-   Merhaba kullanıcının hesabı olduğundan emin olun **kilitli değil.**

-   Emin hello kullanıcının olun **parola süresi değil veya unutulursa.**

-   Emin olun **çok faktörlü kimlik doğrulaması** kullanıcı erişimini engellemediğinden.

-   Emin olun bir **koşullu erişim ilkesi** veya **kimlik koruması** İlkesi kullanıcı erişimini engellemediğinden.

-   Olduğundan emin olun kullanıcının **kimlik doğrulaması kişi bilgilerini** zorlanan toodate tooallow çok faktörlü kimlik doğrulaması veya koşullu erişim ilkeleri toobe olduğu.

-   Tarayıcınızın tanımlama bilgilerini temizleyip ve toosign olarak yeniden deneniyor yapma emin tooalso deneyin.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Merhaba erişim paneli toplantı tarayıcı gereksinimleri

JavaScript destekleyen bir tarayıcı Hello erişim paneli gerektirir ve CSS etkinleştirdi. toouse parola tabanlı çoklu oturum açma (SSO) hello erişim paneli, hello erişim paneli uzantısı içinde hello kullanıcının tarayıcısında yüklenmesi gerekir. Bir kullanıcı, parola tabanlı SSO için yapılandırılmış bir uygulama seçtiğinde bu uzantıyı otomatik olarak yüklenir.

Parola tabanlı, SSO için hello son kullanıcının tarayıcılar olabilir:

-   Internet Explorer 8, 9, 10, 11--Windows 7 veya üzeri

-   Edge Windows 10 Anniversary Edition veya daha yenisi 

-   Chrome--Windows 7 veya daha sonra ve MacOS x veya sonraki sürümlerde

-   Firefox 26,0 veya daha sonra--Windows XP SP2 veya sonraki ve Mac OS X 10,6 veya üzeri


## <a name="problems-with-hello-users-account"></a>Merhaba kullanıcının hesabı sorunları

Erişim paneli hello kullanıcının hesabı tooa sorun nedeniyle engellenmiş toohello erişin. Aşağıdaki sorun giderme ve kullanıcıların ve hesap ayarları ile sorunları bazı yöntemler şunlardır:

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

bir kullanıcı hesabı varsa, toocheck hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.

5.  tıklatın **tüm kullanıcılar**.

6.  **Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.

7.  Merhaba kullanıcı nesnesi toobe beklediğiniz ve hiçbir veri eksik gibi göründüğünü emin Hello özelliklerini denetleyin.

### <a name="check-a-users-account-status"></a>Bir kullanıcının hesap durumunu denetle

toocheck bir kullanıcıya ait hesap durumu, hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.

5.  tıklatın **tüm kullanıcılar**.

6.  **Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.

7.  tıklatın **profil**.

8.  Altında **ayarları** emin **blok oturum** çok ayarlanır**Hayır**.

### <a name="reset-a-users-password"></a>Bir kullanıcının parolasını sıfırlama

tooreset bir kullanıcının parolasını, aşağıdaki hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.

5.  tıklatın **tüm kullanıcılar**.

6.  **Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.

7.  Merhaba tıklatın **parola sıfırlama** hello kullanıcı dikey penceresinde hello üstündeki düğmesi.

8.  Merhaba tıklatın **parola sıfırlama** hello düğmesinde **parola sıfırlama** görünür dikey.

9.  Kopya hello **geçici parola** veya **yeni bir parola girin** hello kullanıcı için.

10. Bu yeni parola toohello kullanıcı iletişim, bu parolayı sırasında bir sonraki oturum tooAzure Active Directory gerekli toochange olabilir.

### <a name="enable-self-service-password-reset"></a>Self Servis parola sıfırlama etkinleştirme

tooenable Self Servis parola sıfırlama, hello dağıtım adımları izleyin:

-   [Azure Active Directory parolalarını kullanıcılar tooreset etkinleştir](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [Kullanıcıların tooreset etkinleştirmek veya Active Directory şirket içi parolalarını değiştirme](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a>Bir kullanıcının çok faktörlü kimlik doğrulama durumunu denetle

toocheck kullanıcı çok faktörlü kimlik doğrulama durumu, aşağıdaki hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.

5.  tıklatın **tüm kullanıcılar**.

6.  Merhaba tıklatın **çok faktörlü kimlik doğrulaması** hello dikey penceresinde hello üstündeki düğmesi.

7.  Bir kez hello **multi-Factor Authentication Yönetim Portalı** yüklendiğinde hello üzerinde olduğundan olun **kullanıcılar** sekmesi.

8.  Merhaba kullanıcı arama, filtreleme veya sıralama hello kullanıcı listesinde bulun.

9.  Kullanıcıların hello listesinden seçim hello kullanıcı ve **etkinleştirmek**, **devre dışı**, veya **zorla** istediğiniz gibi çok faktörlü kimlik doğrulaması.

   >[!NOTE]
   >Bir kullanıcı ise bir **zorlanmış** durumunda, ayarladığınız bunları çok**devre dışı** geçici olarak toolet bunları kendi hesaba geri. Bunlar geri olduktan sonra daha sonra durumlarına çok değiştirebilirsiniz**etkin** yeniden toorequire bunları toore kayıt sırasında bir sonraki kişi bilgileri oturum açın. Alternatif olarak, hello hello adımları takip edebilirsiniz [bir kullanıcının kimlik doğrulaması ile ilgili kişi bilgileri](#check-a-users-authentication-contact-info) tooverify ya da bunlar için bu veri kümesi.
   >
   >

### <a name="check-a-users-authentication-contact-info"></a>Bir kullanıcının kimlik doğrulaması ile ilgili kişi bilgileri

bir kullanıcının kimlik doğrulamasını başvurun çok faktörlü kimlik doğrulaması, koşullu erişim, kimlik koruması ve parola sıfırlamak için kullanılan bilgileri toocheck hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.

5.  tıklatın **tüm kullanıcılar**.

6.  **Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.

7.  tıklatın **profil**.

8.  Çok ilerleyin**kimlik doğrulaması kişi bilgilerini**.

9.  **Gözden geçirme** hello veri, hello kullanıcı ve güncelleştirme için gerektiği şekilde kaydedildi.

### <a name="check-a-users-group-memberships"></a>Bir kullanıcı grup üyeliklerini denetleyin

toocheck bir kullanıcıya ait grup üyeliklerini, hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.

5.  tıklatın **tüm kullanıcılar**.

6.  **Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.

7.  tıklatın **grupları** hello kullanıcı grupları toosee bir üyesidir.

### <a name="check-a-users-assigned-licenses"></a>Bir kullanıcının atanan lisansları denetleme

toocheck bir kullanıcıya ait atanmış lisansların, aşağıdaki hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.

5.  tıklatın **tüm kullanıcılar**.

6.  **Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.

7.  tıklatın **lisansları** toosee lisansları hello kullanıcı şu anda atanmış.

### <a name="assign-a-user-a-license"></a>Bir kullanıcı bir lisans atama 

tooassign lisans tooa kullanıcı hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.

5.  tıklatın **tüm kullanıcılar**.

6.  **Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.

7.  tıklatın **lisansları** toosee lisansları hello kullanıcı şu anda atanmış.

8.  Merhaba tıklatın **atamak** düğmesi.

9.  Seçin **bir veya daha fazla ürün** mevcut ürünler hello listesinden.

10. **İsteğe bağlı** hello tıklatın **atama seçenekleri** öğesi toogranularly ürünleri atayın. Tıklatın **Tamam** ne zaman bu tamamlandı.

11. Merhaba tıklatın **atamak** tooassign bu lisansları toothis kullanıcı düğmesi.

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>Bu sorun giderme adımları hello sorunu çözmezse

bir destek bileti varsa aşağıdaki bilgilerle hello ile açın:

-   Bağıntı hata kimliği

-   UPN (kullanıcı e-posta adresi)

-   Kiracı Kimliği

-   Tarayıcı türü

-   Saat dilimi ve saat/zaman çerçevesine hata oluşuyor

-   Fiddler izlemeleri

## <a name="next-steps"></a>Sonraki adımlar
[Uygulama proxy'si ile çoklu oturum açma tooyour uygulamaları sağlayın](active-directory-application-proxy-sso-using-kcd.md)
