---
title: "Öğretici: Azure Active Directory Tümleştirme SCC yaşam | Microsoft Docs"
description: "Azure Active Directory tooenable ile toouse SCC yaşam döngüsü nasıl tek oturum açma, otomatik sağlama ve daha fazlasını öğrenin!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: c10c313c5fc157ed70d2ccecfb930a8a765f8444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a>Öğretici: Azure Active Directory Tümleştirme ile SCC yaşam döngüsü
Merhaba amacı Bu öğretici, Azure ve SCC yaşam döngüsü tooshow hello tümleştirme ' dir.  

Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

* Geçerli bir Azure aboneliği
* Bir SCC yaşam döngüsü çoklu oturum açma (SSO) abonelik etkin

Bu öğreticiyi tamamladıktan sonra Azure AD kullanıcılarının atamış yaşam döngüsü olacaktır tooSCC mümkün toosingle oturum hello uygulamasına SCC yaşam döngüsü şirket sitenizdeki (servis sağlayıcı tarafından başlatılan oturum açma) hello veya hello kullanarak [giriş Erişim paneli toohello](active-directory-saas-access-panel-introduction.md).

Bu öğreticide gösterilen hello senaryo yapı taşları aşağıdaki Merhaba oluşur:

1. Merhaba uygulama tümleştirmesi SCC yaşam döngüsü için etkinleştirme
2. Çoklu oturum açma (SSO) yapılandırma
3. Kullanıcı hazırlama işleminin yapılandırılması
4. Kullanıcılar atama

![Senaryo](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "senaryosu")

## <a name="enable-hello-application-integration-for-scc-lifecycle"></a>Merhaba uygulama tümleştirmesi SCC yaşam döngüsü için etkinleştirme
Bu bölümde Hello amacı olan toooutline nasıl tooenable hello uygulama tümleştirmesi SCC yaşam döngüsü için.

**tooenable hello uygulama tümleştirmesi SCC yaşam döngüsü için hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol gezinti bölmesinde, Klasik Azure portalı tıklatın **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")
2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.
3. Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.
   
    ![Uygulamaları](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "uygulamalar")
4. Tıklatın **Ekle** hello sayfanın hello sonundaki.
   
    ![Uygulama ekleme](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "uygulama ekleme")
5. Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.
   
    ![Galeriden bir uygulama eklemek](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Galeriden bir uygulama ekleme")
6. Merhaba, **arama kutusu**, türü **SCC yaşam döngüsü**.
   
    ![Uygulama Galerisi](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "uygulama Galerisi")
7. Merhaba sonuçlar bölmesinde seçin **SCC yaşam döngüsü**ve ardından **tam** tooadd Merhaba uygulaması.
   
    ![SCC yaşam döngüsü](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC yaşam döngüsü")
   
## <a name="configure-single-sign-on"></a>Çoklu oturum açmayı yapılandırın

Bu bölümde Hello amacı nasıl hello SAML protokolünü kullanarak Federasyon Azure AD'de hesabıyla tooenable kullanıcılar tooauthenticate tooSCC yaşam döngüsü temel toooutline ' dir.

**tooconfigure çoklu oturum açma, hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Klasik Azure portalı içinde **SCC yaşam döngüsü** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello ** tek oturum yapılandırma üzerinde Aktar ** iletişim.
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "çoklu oturum açmayı yapılandırın")
2. Merhaba üzerinde **nasıl tooSCC yaşam döngüsü üzerindeki kullanıcılar toosign gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "çoklu oturum açmayı yapılandırın")
3. Merhaba üzerinde **uygulama URL'sini Yapılandır** sayfasında hello **oturum üzerinde URL'si** metin kutusuna, türü hello URL kullanılan, kullanıcıların toosign tarafından tooyour üzerinde SCC yaşam döngüsü uygulama deseni takip hello kullanarak "*https:// bs1.SCC.com/lc7/Welcome/Customer/PICTtest.aspx*"ve ardından **sonraki**.
   
    ![Uygulama URL'sini Yapılandır](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "uygulama URL'sini yapılandırın")
4. Merhaba üzerinde **çoklu oturum açma SCC yaşam döngüsü sırasında yapılandırma** sayfasında, **karşıdan meta veri**ve meta veri dosyası, bilgisayarınıza yerel olarak kaydedin.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "çoklu oturum açmayı yapılandırın")
5. Bu meta veri dosyası tooSCC yaşam döngüsü destek ekibi iletin.
   
   >[!NOTE]
   >Çoklu oturum açma hello SCC yaşam döngüsü destek ekibi tarafından etkin toobe sahiptir.
   > 
   > 

6. Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **tam** tooclose hello **tek oturum yapılandırma üzerinde aktar** iletişim.
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "çoklu oturum açmayı yapılandırın")
   
## <a name="configure-user-provisioning"></a>Kullanıcı sağlamayı Yapılandır

SCC yaşam döngüsü içine sipariş tooenable Azure AD kullanıcıların toolog bunların SCC yaşam döngüsü sağlanmalıdır. TooSCC yaşam döngüsü, tooconfigure kullanıcı hazırlama için eylem öğe yok.

Atanan kullanıcı çalıştığında toolog girdiğinde SCC yaşam döngüsü, bir SCC yaşam döngüsü hesap gerekirse, otomatik olarak oluşturulur.

>[!NOTE]
>API AAD kullanıcı hesapları SCC yaşam döngüsü tooprovision tarafından sağlanan veya herhangi diğer SCC yaşam döngüsü kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.
> 
> 

## <a name="assign-users"></a>Kullanıcılar atama
tootest yapılandırmanıza, uygulama erişim tooit atayarak kullanarak tooallow istediğiniz toogrant hello Azure AD kullanıcıları gerekir.

**tooassign kullanıcılar tooSCC yaşam döngüsü, hello aşağıdaki adımları gerçekleştirin:**

1. Hello Klasik Azure portalı, bir test hesabı oluşturun.
2. Hello üzerinde ** SCC yaşam döngüsü ** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.
   
    ![Kullanıcılar atama](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "kullanıcı atama")
3. Test kullanıcınız seçin, **atamak**ve ardından **Evet** tooconfirm, atama.
   
    ![Evet](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Evet")

SSO ayarlarınızı tootest istiyorsanız hello erişim paneli açın. Merhaba erişim paneli hakkında daha fazla ayrıntı için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

