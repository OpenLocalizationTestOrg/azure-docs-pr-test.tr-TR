---
title: "Öğretici: Azure Active Directory Tümleştirme ile Benefitsolver | Microsoft Docs"
description: "Azure Active Directory tooenable ile toouse Benefitsolver nasıl tek oturum açma, otomatik sağlama ve daha fazlasını öğrenin!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 5bb8511ef9be1e386956188a93e899d6ebe56ed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a>Öğretici: Azure Active Directory Tümleştirme Benefitsolver ile
Merhaba amacı Bu öğretici, Azure ve Benefitsolver tooshow hello tümleştirme ' dir.  

Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

* Geçerli bir Azure aboneliği
* Bir Benefitsolver çoklu oturum açma (SSO) abonelik etkin

Bu öğreticiyi tamamladıktan sonra tooBenefitsolver atamış hello Azure AD kullanıcıların mümkün toosingle oturum hello kullanarak hello uygulamaya olacaktır [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

Bu öğreticide gösterilen hello senaryo yapı taşları aşağıdaki Merhaba oluşur:

1. Merhaba uygulama tümleştirmesi Benefitsolver için etkinleştirme
2. Çoklu oturum açma (SSO) yapılandırma
3. Kullanıcı hazırlama işleminin yapılandırılması
4. Kullanıcılar atama

![Senaryo](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "senaryosu")

## <a name="enabling-hello-application-integration-for-benefitsolver"></a>Merhaba uygulama tümleştirmesi Benefitsolver için etkinleştirme
Bu bölümde Hello amacı olan toooutline nasıl tooenable hello uygulama tümleştirmesi Benefitsolver için.

### <a name="tooenable-hello-application-integration-for-benefitsolver-perform-hello-following-steps"></a>tooenable hello uygulama tümleştirmesi Benefitsolver için hello aşağıdaki adımları gerçekleştirin:
1. Merhaba hello sol gezinti bölmesinde, Klasik Azure portalı tıklatın **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")
2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.
3. Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.
   
   ![Uygulamaları](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "uygulamalar")
4. Tıklatın **Ekle** hello sayfanın hello sonundaki.
   
   ![Uygulama ekleme](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "uygulama ekleme")
5. Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.
   
   ![Galeriden bir uygulama eklemek](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Galeriden bir uygulama ekleme")
6. Merhaba, **arama kutusu**, türü **Benefitsolver**.
   
   ![Uygulama Galerisi](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "uygulama Galerisi")
7. Merhaba sonuçlar bölmesinde seçin **Benefitsolver**ve ardından **tam** tooadd Merhaba uygulaması.
   
   ![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")
   
## <a name="configure-single-sign-on"></a>Çoklu oturum açmayı yapılandırın

Bu bölümde Hello amacı nasıl tooenable kullanıcılar tooauthenticate tooBenefitsolver Federasyon kullanarak Azure AD'de hesabıyla hello SAML protokolünü temel toooutline ' dir.  

Benefitsolver uygulamanızı hello SAML onaylar tooadd özel öznitelik eşlemelerini tooyour gerektiren belirli bir biçimde, bekliyor **saml belirteci öznitelikleri** yapılandırma. 

Ekran aşağıdaki hello bunun bir örneği gösterir.

![Öznitelikleri](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "öznitelikleri")

**tooconfigure çoklu oturum açma, hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Klasik Azure portalı içinde **Benefitsolver** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **tek oturum yapılandırma üzerinde aktar** iletişim kutusu.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "çoklu oturum açmayı yapılandırın")
2. Merhaba üzerinde **nasıl tooBenefitsolver üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "çoklu oturum açmayı yapılandırın")
3. Merhaba üzerinde **uygulama ayarlarını yapılandır** sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
   ![Uygulama ayarlarını yapılandırmak](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "uygulaması ayarlarını yapılandır")
   
   1. Merhaba, **oturum üzerinde URL'si** metin kutusuna, türü **http://azure.benefitsolver.com**.
   2. Merhaba, **yanıt URL'si** metin kutusuna, türü **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.  
   3. **İleri**’ye tıklayın.
4. Hello üzerinde **çoklu oturum açma sırasında Benefitsolver yapılandırma** sayfası, toodownload meta verileriniz tıklatın **karşıdan meta veri**ve hello meta veri dosyası, bilgisayarınıza yerel olarak kaydedin.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "çoklu oturum açmayı yapılandırın")
5. İndirilen hello meta veri dosyası tooyour Benefitsolver Destek ekibine gönderin.
   
   >[!NOTE]
   >Benefitsolver destek ekibinize toodo hello gerçek SSO yapılandırmasına sahip. SSO, aboneliğiniz için etkinleştirildiğinde, bir bildirim alırsınız.
   >

6. Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **tam** tooclose hello **tek oturum yapılandırma üzerinde aktar** iletişim.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "çoklu oturum açmayı yapılandırın")
7. Hello içinde hello üst menüsünde **öznitelikleri** tooopen hello **SAML belirteci öznitelikleri** iletişim.
   
   ![Öznitelikleri](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "öznitelikleri")
8. tooadd hello gerekli öznitelik eşlemelerini hello aşağıdaki adımları gerçekleştirin:
   
   ![Öznitelikleri](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "öznitelikleri")
   
   | Öznitelik adı | Öznitelik değeri |
   | --- | --- |
   | İstemci kimliği |Bu değer tooget Benefitsolver destek ekibinden gerekir. |
   | ClientKey |Bu değer tooget Benefitsolver destek ekibinden gerekir. |
   | LogoutURL |Bu değer tooget Benefitsolver destek ekibinden gerekir. |
   | EmployeeID |Bu değer tooget Benefitsolver destek ekibinden gerekir. |
   
   1. Yukarıdaki hello tablosundaki her veri satırı için tıklatın **kullanıcı özniteliği eklemek**.
   2. Merhaba, **öznitelik adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.
   3. Merhaba, **öznitelik değeri** metin kutusuna, ilgili satır için gösterilen select hello öznitelik değeri.
   4. **Tamamla**’ya tıklayın.
9. Tıklatın **değişiklikleri uygulamak**.

## <a name="configure-user-provisioning"></a>Kullanıcı sağlamayı Yapılandır
Benefitsolver içine sipariş tooenable Azure AD kullanıcıların toolog bunların Benefitsolver sağlanmalıdır.  

Benefitsolver Hello durumda çalışan uygulamanızda Census dosyası sisteminizden HRIS (genellikle her gece) aracılığıyla doldurulmuş verilerdir.  

>[!NOTE]
>API AAD kullanıcı hesaplarının Benefitsolver tooprovision tarafından sağlanan veya herhangi diğer Benefitsolver kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz. 
> 

## <a name="assigning-users"></a>Kullanıcılar atama
tootest yapılandırmanıza, uygulama erişim tooit atayarak kullanarak tooallow istediğiniz toogrant hello Azure AD kullanıcıları gerekir.

### <a name="tooassign-users-toobenefitsolver-perform-hello-following-steps"></a>tooassign kullanıcılar tooBenefitsolver hello aşağıdaki adımları gerçekleştirin:
1. Hello Klasik Azure portalı, bir test hesabı oluşturun.
2. Hello üzerinde ** Benefitsolver ** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.
   
   ![Kullanıcılar atama](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "kullanıcı atama")
3. Test kullanıcınız seçin, **atamak**ve ardından **Evet** tooconfirm, atama.
   
   ![Evet](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Evet")

Çoklu oturum açma ayarlarınızı tootest istiyorsanız hello erişim paneli açın. Merhaba erişim paneli hakkında daha fazla ayrıntı için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

