---
title: "Öğretici: Azure Active Directory Tümleştirme ile Coupa | Microsoft Docs"
description: "Azure Active Directory tooenable ile toouse Coupa nasıl tek oturum açma, otomatik sağlama ve daha fazlasını öğrenin!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 87e98573718d27d408c886466a374a987f58faa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a>Öğretici: Azure Active Directory Tümleştirme Coupa ile
Merhaba amacı Bu öğretici, Azure ve Coupa tooshow hello tümleştirme ' dir.  
Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

* Geçerli bir Azure aboneliği
* Bir Coupa çoklu oturum açma (SSO) abonelik etkin

Bu öğreticiyi tamamladıktan sonra tooCoupa atamış hello Azure AD kullanıcıların mümkün toosingle oturum hello kullanarak hello uygulamaya olacaktır [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

Bu öğreticide gösterilen hello senaryo yapı taşları aşağıdaki Merhaba oluşur:

* Merhaba uygulama tümleştirmesi Coupa için etkinleştirme
* Çoklu oturum açmayı yapılandırma
* Kullanıcı hazırlama işleminin yapılandırılması
* Kullanıcılar atama

![Senaryo](./media/active-directory-saas-coupa-tutorial/IC791897.png "senaryosu")

## <a name="enable-hello-application-integration-for-coupa"></a>Merhaba uygulama tümleştirmesi Coupa için etkinleştirme
Bu bölümde Hello amacı olan toooutline nasıl tooenable hello uygulama tümleştirmesi Coupa için.

**tooenable hello uygulama tümleştirmesi Coupa için hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol gezinti bölmesinde, Klasik Azure portalı tıklatın **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")
2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.
3. Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.
   
   ![Uygulamaları](./media/active-directory-saas-coupa-tutorial/IC700994.png "uygulamalar")
4. Tıklatın **Ekle** hello sayfanın hello sonundaki.
   
   ![Uygulama ekleme](./media/active-directory-saas-coupa-tutorial/IC749321.png "uygulama ekleme")
5. Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.
   
   ![Galeriden bir uygulama eklemek](./media/active-directory-saas-coupa-tutorial/IC749322.png "Galeriden bir uygulama ekleme")
6. Merhaba, **arama kutusu**, türü **Coupa**.
   
   ![Uygulama Galerisi](./media/active-directory-saas-coupa-tutorial/IC791898.png "uygulama Galerisi")
7. Merhaba sonuçlar bölmesinde seçin **Coupa**ve ardından **tam** tooadd Merhaba uygulaması.
   
   ![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")
   
## <a name="configure-single-sign-on"></a>Çoklu oturum açmayı yapılandırın

Bu bölümde Hello amacı nasıl tooenable kullanıcılar tooauthenticate tooCoupa Federasyon kullanarak Azure AD'de hesabıyla hello SAML protokolünü temel toooutline ' dir.  

Coupa için çoklu oturum açmayı yapılandırma tooretrieve bir sertifika parmak izi değerinden gerektirir. Bu yordama bilmiyorsanız bkz [nasıl tooretrieve bir sertifikanın parmak izi değeri](http://youtu.be/YKQF266SAxI).

**tooconfigure çoklu oturum açma, hello aşağıdaki adımları gerçekleştirin:**

1. Üzerinde tooyour Coupa şirket site yönetici olarak oturum açın.
2. Çok Git**Kurulum \> güvenlik denetimi**.
   
   ![Güvenlik denetimleri](./media/active-directory-saas-coupa-tutorial/IC791900.png "güvenlik denetimleri")
3. toodownload hello Coupa meta veri dosyası tooyour bilgisayar, **indirin ve SP meta veri içe**.
   
   ![Coupa SP meta veri](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP meta verileri")
4. Farklı bir tarayıcı penceresinde toohello Klasik Azure portalı üzerinde oturum açın.
5. Merhaba üzerinde **Coupa** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **tek oturum yapılandırma üzerinde aktar** iletişim.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-coupa-tutorial/IC791902.png "çoklu oturum açmayı yapılandırın")
6. Merhaba üzerinde **nasıl tooCoupa üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-coupa-tutorial/IC791903.png "çoklu oturum açmayı yapılandırın")
7. Merhaba üzerinde **uygulama URL'sini Yapılandır** sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
   ![Uygulama URL'sini Yapılandır](./media/active-directory-saas-coupa-tutorial/IC791904.png "uygulama URL'sini yapılandırın")   
   1. Merhaba, **oturum üzerinde URL'si** metin kutusuna, tooyour Coupa uygulama üzerinde kullanıcıların toosign tarafından kullanılan türü URL'si (örn: "*http://company.Coupa.com*").
   2. İndirilen Coupa meta veri dosyanızı açın ve ardından hello kopyalayın **AssertionConsumerService dizin/URL**.
   3. Merhaba, **Coupa yanıt URL'si** metin kutusuna, Yapıştır hello **AssertionConsumerService dizin/URL** değeri.
   4. **İleri**’ye tıklayın.
8. Merhaba üzerinde **çoklu oturum açma sırasında Coupa yapılandırma** sayfası, toodownload, meta veri dosyası tıklatın **karşıdan meta veri**ve yerel olarak bilgisayarınızda hello dosyasını kaydedin.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-coupa-tutorial/IC791905.png "çoklu oturum açmayı yapılandırın")
9. Merhaba Coupa şirket sitesinde çok Git**Kurulum \> güvenlik denetimi**.
   
   ![Güvenlik denetimleri](./media/active-directory-saas-coupa-tutorial/IC791900.png "güvenlik denetimleri")
10. Merhaba, **Coupa kimlik bilgilerini kullanarak oturum** bölümünde, hello aşağıdaki adımları gerçekleştirin:  

   ![Coupa kimlik bilgilerini kullanarak oturum](./media/active-directory-saas-coupa-tutorial/IC791906.png "Coupa kimlik bilgilerini kullanarak oturum açın") 
   1. Seçin **SAML kullanarak oturum**.
   2. Tıklatın **Gözat** tooupload indirilen, Azure Active meta veri dosyası.
   3. **Kaydet** düğmesine tıklayın.
11. Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **tam** tooclose hello **tek oturum yapılandırma üzerinde aktar** iletişim.
    
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-coupa-tutorial/IC791907.png "çoklu oturum açmayı yapılandırın")
    
## <a name="configure-user-provisioning"></a>Kullanıcı sağlamayı Yapılandır

Coupa içine sipariş tooenable Azure AD kullanıcıların toolog bunların Coupa sağlanmalıdır.  

* Coupa Hello durumda sağlama bir el ile bir görevdir.

**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour oturum **Coupa** yönetici olarak şirket site.
2. Hello içinde hello üst menüsünde **Kurulum**ve ardından **kullanıcılar**.
   
   ![Kullanıcıların](./media/active-directory-saas-coupa-tutorial/IC791908.png "kullanıcılar")
3. **Oluştur**'a tıklayın.
   
   ![Kullanıcılar oluşturma](./media/active-directory-saas-coupa-tutorial/IC791909.png "kullanıcıları oluşturun")
4. Merhaba, **kullanıcı oluşturma** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
   ![Kullanıcı ayrıntılarını](./media/active-directory-saas-coupa-tutorial/IC791910.png "kullanıcı ayrıntıları")
   
   1. Türü hello **oturum açma**, **ad**, **Soyadı**, **tek oturum açma kimliği**, **e-posta** özniteliklerini bir Geçerli Azure Active Directory hesabı hello tooprovision istediğiniz metin kutuları ilgili.
   2. **Oluştur**'a tıklayın.   
   >[!NOTE]
   >etkin duruma gelmesi hello Azure Active Directory hesap sahibi bağlantı tooconfirm hello hesabı olan bir e-posta alırsınız. 
   > 

>[!NOTE]
>API AAD kullanıcı hesaplarının Coupa tooprovision tarafından sağlanan veya herhangi diğer Coupa kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz. 
> 

## <a name="assign-users"></a>Kullanıcılar atama
tootest yapılandırmanıza, uygulama erişim tooit atayarak kullanarak tooallow istediğiniz toogrant hello Azure AD kullanıcıları gerekir.

**tooassign kullanıcılar tooCoupa hello aşağıdaki adımları gerçekleştirin:**

1. Hello Klasik Azure portalı, bir test hesabı oluşturun.
2. Hello üzerinde ** Coupa ** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.
   
   ![Kullanıcılar atama](./media/active-directory-saas-coupa-tutorial/IC791911.png "kullanıcı atama")
3. Test kullanıcınız seçin, **atamak**ve ardından **Evet** tooconfirm, atama.
   
   ![Evet](./media/active-directory-saas-coupa-tutorial/IC767830.png "Evet")

Çoklu oturum açma ayarlarınızı tootest istiyorsanız hello erişim paneli açın. Merhaba erişim paneli hakkında daha fazla ayrıntı için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

