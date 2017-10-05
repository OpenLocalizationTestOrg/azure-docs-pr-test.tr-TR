---
title: "Öğretici: Azure Active Directory Tümleştirme ile Benefitsolver | Microsoft Docs"
description: "Çoklu oturum açma, otomatik sağlama ve daha fazla etkinleştirmek için Azure Active Directory ile Benefitsolver kullanmayı öğrenin!"
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
ms.openlocfilehash: 8a13dd5ebd872f86247158379b28bc291a9c9d83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a>Öğretici: Azure Active Directory Tümleştirme Benefitsolver ile
Bu öğreticinin amacı, Azure ve Benefitsolver tümleştirmesini göstermektir.  

Bu öğreticide gösterilen senaryo, aşağıdaki öğeleri zaten sahip olduğunuzu varsayar:

* Geçerli bir Azure aboneliği
* Bir Benefitsolver çoklu oturum açma (SSO) abonelik etkin

Bu öğreticiyi tamamladıktan sonra Benefitsolver için atanmış Azure AD kullanıcılarının uygulama kullanarak çoklu oturum açabilirsiniz [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).

Bu öğreticide gösterilen senaryo, aşağıdaki yapı taşlarını oluşur:

1. Uygulama tümleştirmesi Benefitsolver için etkinleştirme
2. Çoklu oturum açma (SSO) yapılandırma
3. Kullanıcı hazırlama işleminin yapılandırılması
4. Kullanıcılar atama

![Senaryo](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "senaryosu")

## <a name="enabling-the-application-integration-for-benefitsolver"></a>Uygulama tümleştirmesi Benefitsolver için etkinleştirme
Bu bölümün amacı Benefitsolver için uygulama tümleştirme sağlamak üzere nasıl anahat sağlamaktır.

### <a name="to-enable-the-application-integration-for-benefitsolver-perform-the-following-steps"></a>Benefitsolver uygulama tümleştirmesini etkinleştirmek için aşağıdaki adımları gerçekleştirin:
1. Azure Klasik portalında, sol gezinti bölmesinde tıklatın **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")
2. Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.
3. Dizin görünümünde uygulamaları görünümü açmak için **uygulamaları** üst menüde.
   
   ![Uygulamaları](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "uygulamalar")
4. Tıklatın **Ekle** sayfanın sonundaki.
   
   ![Uygulama ekleme](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "uygulama ekleme")
5. Üzerinde **ne yapmak istiyorsunuz** iletişim kutusunda, tıklatın **Galeriden bir uygulama eklemek**.
   
   ![Galeriden bir uygulama eklemek](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Galeriden bir uygulama ekleme")
6. İçinde **arama kutusu**, türü **Benefitsolver**.
   
   ![Uygulama Galerisi](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "uygulama Galerisi")
7. Sonuçlar bölmesinde seçin **Benefitsolver**ve ardından **tam** uygulama eklemek için.
   
   ![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")
   
## <a name="configure-single-sign-on"></a>Çoklu oturum açmayı yapılandırın

Bu bölümün amacı kullanıcıların Benefitsolver için kendi hesabıyla SAML protokolünü temel Federasyon kullanarak Azure AD kimlik doğrulaması sağlamak nasıl anahat sağlamaktır.  

Özel öznitelik eşlemelerini eklemenizi gerektirir belirli bir biçimde SAML onaylar Benefitsolver uygulamanızı bekler, **saml belirteci öznitelikleri** yapılandırma. 

Aşağıdaki ekran görüntüsünde bunun bir örneği gösterir.

![Öznitelikleri](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "öznitelikleri")

**Çoklu oturum açma yapılandırmak için aşağıdaki adımları gerçekleştirin:**

1. Azure Klasik portalında üzerinde **Benefitsolver** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma özelliğini yapılandırın** açmak için **tek oturum yapılandırma üzerinde aktar** iletişim.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "çoklu oturum açmayı yapılandırın")
2. Üzerinde **Benefitsolver için oturum açmasını nasıl istiyorsunuz** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "çoklu oturum açmayı yapılandırın")
3. Üzerinde **uygulama ayarlarını yapılandır** sayfasında, aşağıdaki adımları gerçekleştirin:
   
   ![Uygulama ayarlarını yapılandırmak](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "uygulaması ayarlarını yapılandır")
   
   1. İçinde **oturum üzerinde URL'si** metin kutusuna, türü **http://azure.benefitsolver.com**.
   2. İçinde **yanıt URL'si** metin kutusuna, türü **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.  
   3. **İleri**’ye tıklayın.
4. Üzerinde **çoklu oturum açma sırasında Benefitsolver yapılandırma** meta verileriniz, indirme sayfasında, tıklatın **karşıdan meta veri**ve meta veri dosyası, bilgisayarınıza yerel olarak kaydedin.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "çoklu oturum açmayı yapılandırın")
5. İndirilen meta veri dosyası Benefitsolver destek ekibinize gönderin.
   
   >[!NOTE]
   >Gerçek SSO yapılandırmasını yapmak Benefitsolver destek ekibinize sahiptir. SSO, aboneliğiniz için etkinleştirildiğinde, bir bildirim alırsınız.
   >

6. Klasik Azure portalı, çoklu oturum açma yapılandırması onay seçin ve ardından **tam** kapatmak için **tek oturum yapılandırma üzerinde aktar** iletişim.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "çoklu oturum açmayı yapılandırın")
7. Üstteki menüde tıklatın **öznitelikleri** açmak için **SAML belirteci öznitelikleri** iletişim.
   
   ![Öznitelikleri](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "öznitelikleri")
8. Gerekli öznitelik eşlemelerini eklemek için aşağıdaki adımları gerçekleştirin:
   
   ![Öznitelikleri](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "öznitelikleri")
   
   | Öznitelik adı | Öznitelik değeri |
   | --- | --- |
   | İstemci kimliği |Bu değer, Benefitsolver destek ekibinden edinmeniz gerekir. |
   | ClientKey |Bu değer, Benefitsolver destek ekibinden edinmeniz gerekir. |
   | LogoutURL |Bu değer, Benefitsolver destek ekibinden edinmeniz gerekir. |
   | EmployeeID |Bu değer, Benefitsolver destek ekibinden edinmeniz gerekir. |
   
   1. Her veri satırının için yukarıdaki tabloda **kullanıcı özniteliği eklemek**.
   2. İçinde **öznitelik adı** metin kutusuna, ilgili satır için gösterilen öznitelik adı yazın.
   3. İçinde **öznitelik değeri** metin kutusuna, ilgili satır için gösterilen öznitelik değerini seçin.
   4. **Tamamla**’ya tıklayın.
9. Tıklatın **değişiklikleri uygulamak**.

## <a name="configure-user-provisioning"></a>Kullanıcı sağlamayı Yapılandır
Azure AD kullanıcıların Benefitsolver oturum etkinleştirmek için bunların Benefitsolver sağlanmalıdır.  

Benefitsolver söz konusu olduğunda, çalışan uygulamanızda Census dosyası sisteminizden HRIS (genellikle her gece) aracılığıyla doldurulmuş verilerdir.  

>[!NOTE]
>API sağlama AAD kullanıcı hesaplarına Benefitsolver tarafından sağlanan veya herhangi diğer Benefitsolver kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz. 
> 

## <a name="assigning-users"></a>Kullanıcılar atama
Yapılandırmanızı test etmek için uygulama erişimi atayarak kullanarak izin vermek istediğiniz Azure AD kullanıcılarının vermeniz gerekir.

### <a name="to-assign-users-to-benefitsolver-perform-the-following-steps"></a>Kullanıcılar için Benefitsolver atamak için aşağıdaki adımları gerçekleştirin:
1. Klasik Azure portalında bir test hesabı oluşturun.
2. Üzerinde ** Benefitsolver ** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.
   
   ![Kullanıcılar atama](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "kullanıcı atama")
3. Test kullanıcınız seçin, **atamak**ve ardından **Evet** , atama onaylamak için.
   
   ![Evet](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Evet")

Çoklu oturum açma ayarlarınızı test etmek isterseniz, erişim paneli açın. Erişim paneli hakkında daha fazla ayrıntı için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).

