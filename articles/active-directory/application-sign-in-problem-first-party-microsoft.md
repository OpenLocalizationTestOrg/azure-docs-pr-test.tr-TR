---
title: "tooa Microsoft uygulaması imzalama aaaProblems | Microsoft Docs"
description: "Toofirst taraf Microsoft Azure AD (örneğin, Office 365) kullanarak Applications imzalarken karşılaştığı yaygın sorunlarını giderme"
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
ms.openlocfilehash: 35849ca8dbaa909d17b6d0da572f5c11041a8559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="problems-signing-in-tooa-microsoft-application"></a>Tooa Microsoft uygulaması imzalama sorunları

Microsoft Applications (örneğin, Office 365 Exchange, SharePoint, Yammer, vb.) atanan ve biraz farklı 3 taraf SaaS uygulamaları veya diğer uygulamalar üzerinde çoklu oturum açma için Azure AD ile tümleştirmek yönetilebilir.

Kullanıcı erişim tooa Microsoft yayımlanan uygulama alabilirsiniz üç ana yolu vardır.

-   Merhaba Office 365 veya diğer Ücretli paketlerini uygulamalar için erişim aracılığıyla kullanıcılara verilen **lisans atama** ya da doğrudan tootheir kullanıcı hesabı veya bizim grup tabanlı lisans atama özelliği kullanarak bir grup.

-   Microsoft veya üçüncü taraf yazılımınızla herkes için toouse yayımlar, uygulamalar için kullanıcılara üzerinden erişim izni **kullanıcı izni**. This0 toohello uygulamada Azure AD iş veya Okul hesabıyla oturum açın ve kendi hesaplarına toohave erişim sınırlı toosome veri kümesini izin anlamına gelir.

-   Microsoft ya da bir 3. taraf serbestçe herkes için toouse yayımlar, uygulamalar için kullanıcılar ayrıca aracılığıyla erişimi verilebilir **yönetici izni**. Bu, bir yönetici hello kuruluşunuzdaki herkes tarafından toohello uygulamasında bir genel yönetici hesabıyla oturum açın ve erişim tooeveryone hello kuruluşunuzdaki vermek Merhaba uygulaması kullanılabilir belirledi anlamına gelir.

tootroubleshoot hello Başlarken sorununuzu [genel sorun alanlarından uygulama erişimi tooconsider](#general-problem-areas-with-application-access-to-consider) ve hello okuma [izlenecek yol: adımları tootroubleshoot Microsoft Application erişim](#walkthrough-steps-to-troubleshoot-microsoft-application-access) Merhaba ayrıntıları içine tooget.

## <a name="general-problem-areas-with-application-access-tooconsider"></a>Uygulama erişimi tooconsider genel sorun alanlarından

Merhaba listesini hızla giderek hello izlenecek tooget okuma toostart, ancak burada önerilir hakkında bir fikir varsa, ayrıntılarına geçebilir genel sorunlu alanları aşağıdadır: [izlenecek yol: adımları tootroubleshoot Microsoft Application erişim](#walkthrough-steps-to-troubleshoot-microsoft-application-access).

-   [Merhaba kullanıcının hesabı sorunları](#problems-with-the-users-account)

-   [Grupları sorunları](#problems-with-groups)

-   [Koşullu erişim ilkeleri sorunları](#problems-with-conditional-access-policies)

-   [Uygulama onayı sorunları](#problems-with-application-consent)

## <a name="steps-tootroubleshoot-microsoft-application-access"></a>Adımları tootroubleshoot Microsoft Application erişim

Kullanıcılara tooa Microsoft uygulaması imzaladığınızda aşağıda bazı yaygın sorunlar terimleri içine çalıştırılır.

-   Genel toocheck ilk sorunları

  * Merhaba kullanıcı toohello içinde imzalama emin olun **URL'yi düzeltin** ve bir yerel uygulama URL değil.

  * Merhaba kullanıcının hesabı olduğundan emin olun **kilitli değil.**

  * Merhaba emin olun **kullanıcının hesabı zaten** Azure Active Directory'de. [Bir kullanıcı hesabı Azure Active Directory içinde olup olmadığını kontrol edin](#problems-with-the-users-account)

  * Merhaba kullanıcının hesabı olduğundan emin olun **etkin** için oturum açmalar. [Bir kullanıcının hesap durumunu denetle](#problems-with-the-users-account)

  * Emin hello kullanıcının olun **parola süresi değil veya unutulursa.** [Bir kullanıcının parolasını sıfırlamak](#reset-a-users-password) veya [Self Servis parola sıfırlama etkinleştirme](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)

   * Emin olun **çok faktörlü kimlik doğrulaması** kullanıcı erişimini engellemediğinden. [Bir kullanıcının çok faktörlü kimlik doğrulama durumunu denetleme](#check-a-users-multi-factor-authentication-status) veya [bir kullanıcının kimlik doğrulaması ile ilgili kişi bilgileri](#check-a-users-authentication-contact-info)

   * Emin olun bir **koşullu erişim ilkesi** veya **kimlik koruması** İlkesi kullanıcı erişimini engellemediğinden. [Belirli bir koşullu erişim ilkesini denetleme](#problems-with-conditional-access-policies) veya [belirli bir uygulamanın koşullu erişim ilkesini denetleme](#check-a-specific-applications-conditional-access-policy) veya [belirli koşullu erişim ilkesini devre dışı bırak](#disable-a-specific-conditional-access-policy)

   * Olduğundan emin olun kullanıcının **kimlik doğrulaması kişi bilgilerini** zorlanan toodate tooallow çok faktörlü kimlik doğrulaması veya koşullu erişim ilkeleri toobe olduğu. [Bir kullanıcının çok faktörlü kimlik doğrulama durumunu denetleme](#check-a-users-multi-factor-authentication-status) veya [bir kullanıcının kimlik doğrulaması ile ilgili kişi bilgileri](#check-a-users-authentication-contact-info)

-   İçin **Microsoft** **lisans gerektiren uygulamalar** (Office365) gibi hello genel yukarıdaki sorunları çizgili sonra bazı belirli sorunları toocheck aşağıda verilmiştir:

   * Merhaba kullanıcı sağlayın ya da sahip bir **lisansı atanmış.** [Bir kullanıcının atanan lisansları denetleme](#check-a-users-assigned-licenses) veya [bir grubun atanan lisansları denetleme](#check-a-groups-assigned-licenses)

   * Merhaba lisans ise **tooa atanan** **statik grup**, o hello olun **kullanıcının üyesi olduğu** o grubun. [Bir kullanıcı grup üyeliklerini denetleyin](#check-a-users-group-memberships)

   * Merhaba lisans ise **tooa atanan** **dinamik grup**, o hello olun **dinamik Grup kural doğru olarak ayarlandığında**. [Dinamik bir grubun üyeliğini ölçütlerini denetleyin](#check-a-dynamic-groups-membership-criteria)

   * Merhaba lisans ise **tooa atanan** **dinamik grup**, o hello dinamik grup sahip olduğundan emin olun **işleme tamamlandı** üyeliğine ve o hello **kullanıcı bir üye** (Bu işlem biraz zaman alabilir). [Bir kullanıcı grup üyeliklerini denetleyin](#check-a-users-group-memberships)

   *  Merhaba lisans atandığı emin olun sonra hello lisans olduğundan emin olun **süresi**.

   *  Merhaba lisans olduğundan emin olun **Merhaba uygulaması için** erişmekte olan.

-   İçin **Microsoft** **bir lisans gerektirmeyen uygulamalar**, başka bir şey toocheck şunlardır:

   * Merhaba uygulaması istiyorsa **kullanıcı düzeyinde izinler** (örneğin "Bu kullanıcının posta kutusu erişim"), o hello kullanıcı toohello uygulamada imzaladığı emin olun ve gerçekleştirdiği bir **kullanıcı düzeyinde onay işlemi**  toolet Merhaba uygulaması kendi verilere erişebilir.

   * Merhaba uygulaması istiyorsa **yönetici düzeyi izinler** (örneğin "tüm kullanıcının posta kutularına erişim"), genel yönetici yürüttü emin olun bir **yönetici düzeyi onay işlemi tüm kullanıcılar adına** hello kuruluşunuzdaki.

## <a name="problems-with-hello-users-account"></a>Merhaba kullanıcının hesabı sorunları

Uygulama erişimi toohello uygulama atanmış bir kullanıcı tooa sorun nedeniyle engellenebilir. Aşağıdaki sorun giderme ve kullanıcıların ve hesap ayarları ile sorunları bazı yöntemler şunlardır:

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

  * **Not**: kullanıcı ise bir **zorlanmış** durumunda, ayarladığınız bunları çok**devre dışı** geçici olarak toolet bunları kendi hesaba geri. Bunlar geri olduktan sonra daha sonra durumlarına çok değiştirebilirsiniz**etkin** yeniden toorequire bunları toore kayıt sırasında bir sonraki kişi bilgileri oturum açın. Alternatif olarak, hello hello adımları takip edebilirsiniz [bir kullanıcının kimlik doğrulaması ile ilgili kişi bilgileri](#check-a-users-authentication-contact-info) tooverify ya da bunlar için bu veri kümesi.

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

## <a name="problems-with-groups"></a>Grupları sorunları

Uygulama erişimi toohello uygulama atanmış bir gruba tooa sorun nedeniyle engellenebilir. Aşağıdaki sorun giderme ve gruplar ve grup üyelikleri ile sorunları bazı yöntemler şunlardır:

-   [Bir grubun üyeliğini kontrol edin](#check-a-groups-membership)

-   [Dinamik bir grubun üyeliğini ölçütlerini denetleyin](#check-a-dynamic-groups-membership-criteria)

-   [Bir grubun atanan lisansları denetleme](#check-a-groups-assigned-licenses)

-   [Bir grubun lisansları yeniden işleyin](#reprocess-a-groups-licenses)

-   [Bir gruba bir lisans atama](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a>Bir grubun üyeliğini kontrol edin

toocheck bir grubun üyeliğini, aşağıdaki hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.

5.  tıklatın **tüm grupları**.

6.  **Arama** ilgilendiğiniz hello grubu için ve **hello satıra tıklayın** tooselect.

7.  tıklatın **üyeleri** tooreview hello kullanıcıların listesini atanan toothis grubu.

### <a name="check-a-dynamic-groups-membership-criteria"></a>Dinamik bir grubun üyeliğini ölçütlerini denetleyin 

toocheck dinamik grubun Üyelik ölçütleri hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.

5.  tıklatın **tüm grupları**.

6.  **Arama** ilgilendiğiniz hello grubu için ve **hello satıra tıklayın** tooselect.

7.  tıklatın **dinamik Üyelik kuralları.**

8.  Gözden geçirme hello **basit** veya **Gelişmiş** tanımlanan bu grup için kural ve bu grubun üyesi toobe istediğiniz hello kullanıcının bu ölçütleri karşılayan emin olun.

### <a name="check-a-groups-assigned-licenses"></a>Bir grubun atanan lisansları denetleme

toocheck bir gruba ait atanmış lisansların, aşağıdaki hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.

5.  tıklatın **tüm grupları**.

6.  **Arama** ilgilendiğiniz hello grubu için ve **hello satıra tıklayın** tooselect.

7.  tıklatın **lisansları** toosee hangi lisansları hello grubuna atanmış.

### <a name="reprocess-a-groups-licenses"></a>Bir grubun lisansları yeniden işleyin

tooreprocess bir gruba ait atanmış lisansların, aşağıdaki hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.

5.  tıklatın **tüm grupları**.

6.  **Arama** ilgilendiğiniz hello grubu için ve **hello satıra tıklayın** tooselect.

7.  tıklatın **lisansları** toosee hangi lisansları hello grubuna atanmış.

8.  Merhaba tıklatın **yeniden işleyin** atanan lisansları toothis grubun üyeleri hello düğmesi tooensure güncel. Bu, başlangıç boyutu ve karmaşıklığı hello grubunun bağlı olarak uzun bir süre devam edebilir.

   >[!NOTE]
   >toodo bu daha hızlı ve göz önünde bulundurun geçici olarak bir lisans toohello kullanıcı doğrudan atama. [Bir kullanıcı bir lisans atamak](#problems-with-application-consent).
   >
   >

### <a name="assign-a-group-a-license"></a>Bir gruba bir lisans atama

tooassign bir lisans tooa grubu hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.

5.  tıklatın **tüm grupları**.

6.  **Arama** ilgilendiğiniz hello grubu için ve **hello satıra tıklayın** tooselect.

7.  tıklatın **lisansları** toosee hangi lisansları hello grubuna atanmış.

8.  Merhaba tıklatın **atamak** düğmesi.

9.  Seçin **bir veya daha fazla ürün** mevcut ürünler hello listesinden.

10. **İsteğe bağlı** hello tıklatın **atama seçenekleri** öğesi toogranularly ürünleri atayın. Tıklatın **Tamam** ne zaman bu tamamlandı.

11. Merhaba tıklatın **atamak** bu lisansları toothis Grup tooassign düğmesi. Bu, başlangıç boyutu ve karmaşıklığı hello grubunun bağlı olarak uzun bir süre devam edebilir.

   >[!NOTE]
   >toodo bu daha hızlı ve göz önünde bulundurun geçici olarak bir lisans toohello kullanıcı doğrudan atama. [Bir kullanıcı bir lisans atamak](#problems-with-application-consent).
   > 
   >

## <a name="problems-with-conditional-access-policies"></a>Koşullu erişim ilkeleri sorunları

### <a name="check-a-specific-conditional-access-policy"></a>Belirli bir koşullu erişim ilkesine denetleyin

toocheck veya tek koşullu erişim ilkesini doğrulayın:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  tıklatın **kurumsal uygulamalar** hello Gezinti menüsünde.

5.  Merhaba tıklatın **koşullu erişim** Gezinti öğesi.

6.  inceleyerek ilgilendiğiniz hello İlkesi'ni tıklatın.

7.  Belirli bir koşul, atamaları ya da kullanıcı erişimi engelliyor olabilecek diğer ayarları gözden geçirin.

   >[!NOTE]
   >Bunu değil etkileyen oturum eklentiler toodo Bu, kümesi hello Bu ilke tooensure tootemporarily devre dışı bırak isteyebilir **ilkesini etkinleştir** çok geçiş**yok** hello tıklatıp **kaydetmek** düğmesi .
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a>Belirli bir uygulamanın koşullu erişim ilkesini denetleme

toocheck veya tek bir uygulamanın şu anda yapılandırılmış koşullu erişim ilkesini doğrulayın:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  tıklatın **kurumsal uygulamalar** hello Gezinti menüsünde.

5.  tıklatın **tüm uygulamaları**.

6.  Arama ilgilendiğiniz ya da kullanıcı hello Merhaba uygulaması toosign tooby uygulamada çalışıyor için ad veya uygulama kimliği görüntüler.

     >[!NOTE]
     >Aradığınız Merhaba uygulaması görmüyorsanız, hello tıklatın **filtre** düğmesine tıklayın ve hello listesi hello kapsamını çok genişletin**tüm uygulamaları**. Daha fazla sütun toosee isterseniz, hello tıklatın **sütunları** düğmesini tooadd ek ayrıntılar, uygulamalarınız için.
     >
     >

7.  Merhaba tıklatın **koşullu erişim** Gezinti öğesi.

8.  inceleyerek ilgilendiğiniz hello İlkesi'ni tıklatın.

9.  Belirli bir koşul, atamaları ya da kullanıcı erişimi engelliyor olabilecek diğer ayarları gözden geçirin.

     >[!NOTE]
     >Bunu değil etkileyen oturum eklentiler toodo Bu, kümesi hello Bu ilke tooensure tootemporarily devre dışı bırak isteyebilir **ilkesini etkinleştir** çok geçiş**yok** hello tıklatıp **kaydetmek** düğmesi .
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a>Belirli bir koşullu erişim ilkesine devre dışı bırak

toocheck veya tek koşullu erişim ilkesini doğrulayın:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  tıklatın **kurumsal uygulamalar** hello Gezinti menüsünde.

5.  Merhaba tıklatın **koşullu erişim** Gezinti öğesi.

6.  inceleyerek ilgilendiğiniz hello İlkesi'ni tıklatın.

7.  Hello İlkesi ayarı hello tarafından devre dışı **ilkesini etkinleştir** çok geçiş**Hayır** hello tıklatıp **kaydetmek** düğmesi.

## <a name="problems-with-application-consent"></a>Uygulama onayı sorunları

Merhaba uygun izinlere onay işlemi değil oluştuğu için uygulama erişimi engellenebilir. Aşağıdaki sorun giderme ve uygulama izin sorunları çözmeye bazı yöntemler şunlardır:

-   [Bir kullanıcı düzeyinde onay işlemi gerçekleştirme](#perform-a-user-level-consent-operation)

-   [Herhangi bir uygulama için yönetici düzeyi onay işlemi gerçekleştirme](#perform-administrator-level-consent-operation-for-any-application)

-   [Bir tek kiracılı uygulama için yönetici düzeyi onay gerçekleştirme](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [Çok kiracılı uygulama için yönetici düzeyi onay gerçekleştirme](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a>Bir kullanıcı düzeyinde onay işlemi gerçekleştirme

-   İzinleri isteyen herhangi Open ID Connect özellikli bir uygulama için toohello uygulamanın oturum açma ekranı gezinme hello oturum açmış kullanıcı için kullanıcı düzeyinde izin toohello uygulaması gerçekleştirir.

-   Toodo Bu program aracılığıyla istiyorsanız, bkz: [tek tek kullanıcı izni isteyen](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).

### <a name="perform-administrator-level-consent-operation-for-any-application"></a>Herhangi bir uygulama için yönetici düzeyi onay işlemi gerçekleştirme

-   İçin **yalnızca hello V1 uygulama modeli kullanılarak geliştirilen uygulamaları**, ekleyerek bu yönetici düzeyi onay toooccur zorlayabilirsiniz "**? yönetici komut isteminde =\_onayı**" toohello sonuna bir uygulamanın oturum açma URL'si.

-   İçin **hello V2 uygulama modeli kullanılarak geliştirilen herhangi bir uygulama**, hello altındaki hello yönergeleri izleyerek bu yönetici düzeyi onay toooccur zorunlu kılabilir **bir dizinden hello izinleri iste Yönetici** bölümünü [hello yönetici onayı uç noktası kullanarak](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a>Bir tek kiracılı uygulama için yönetici düzeyi onay gerçekleştirme

-   İçin **tek Kiracı uygulamaları** izinleri (gelenler geliştirdiğiniz veya, kuruluşunuzda sahip), istek gerçekleştirebileceğiniz bir **yönetici düzeyi onay** tüm adına işlemi Genel yönetici olarak oturum açmayı ve üzerinde hello tıklatarak kullanıcıları **izinleri verin** düğmesi hello hello üstündeki **uygulama kayıt defteri -&gt; tüm uygulamalar -&gt; - bir uygulama seçin &gt; Gerekli izinler** dikey.

-   İçin **hello V1 veya V2 uygulama modeli kullanılarak geliştirilen herhangi bir uygulama**, hello altındaki hello yönergeleri izleyerek bu yönetici düzeyi onay toooccur zorunlu kılabilir **isteği hello izinlerinin bir Dizin yönetici** bölümünü [hello yönetici onayı uç noktası kullanarak](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a>Çok kiracılı uygulama için yönetici düzeyi onay gerçekleştirme

-   İçin **çok kiracılı uygulamalara** (bir uygulama bir üçüncü taraf veya Microsoft, geliştirir gibi) bu istek izinlerine gerçekleştirebileceğiniz bir **yönetici düzeyi onay** işlemi. Genel yönetici olarak oturum açın ve üzerinde hello tıklayarak **izinleri verin** düğmesi hello altında **kurumsal uygulamalar -&gt; tüm uygulamalar -&gt; bir uygulama - seçin&gt; İzinleri** dikey (kullanılabilir yakında).

-   Merhaba altındaki hello yönergeleri izleyerek bu yönetici düzeyi onay toooccur zorlayabilir **hello izinleri directory yönetici olarak istek** bölümünü [hello yönetici onayı uç noktasıkullanarak](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

## <a name="next-steps"></a>Sonraki adımlar
[Merhaba yönetici onayı uç noktası kullanma](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

