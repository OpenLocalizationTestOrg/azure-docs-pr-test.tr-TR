---
title: "Öğretici: Azure Active Directory Tümleştirme ile Qualtrics | Microsoft Docs"
description: "Azure Active Directory tooenable ile toouse Qualtrics nasıl tek oturum açma, otomatik sağlama ve daha fazlasını öğrenin!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 941642e74b90bb13a5ce37ce6665cfa32cd86016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a>Öğretici: Azure Active Directory Tümleştirme Qualtrics ile
Merhaba amacı Bu öğretici, Azure ve Qualtrics tooshow hello tümleştirme ' dir.  

Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

* Geçerli bir Azure aboneliği
* Bir Qualtrics çoklu oturum açma (SSO) abonelik etkin

Bu öğreticiyi tamamladıktan sonra tooQualtrics atamış hello Azure AD kullanıcıların mümkün toosingle oturum Qualtrics şirket sitenizin (servis sağlayıcı tarafından başlatılan oturum açma) veya hello kullanarak hello uygulamaya olacaktır [giriş toohello Erişim paneli](active-directory-saas-access-panel-introduction.md).

Bu öğreticide gösterilen hello senaryo yapı taşları aşağıdaki Merhaba oluşur:

1. Merhaba uygulama tümleştirmesi Qualtrics için etkinleştirme
2. Çoklu oturum açma (SSO) yapılandırma
3. Kullanıcı hazırlama işleminin yapılandırılması
4. Kullanıcılar atama

![Senaryo](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "senaryosu")

## <a name="enabling-hello-application-integration-for-qualtrics"></a>Merhaba uygulama tümleştirmesi Qualtrics için etkinleştirme
Bu bölümde Hello amacı olan toooutline nasıl tooenable hello uygulama tümleştirmesi Qualtrics için.

**tooenable hello uygulama tümleştirmesi Qualtrics için hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol gezinti bölmesinde, Klasik Azure portalı tıklatın **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")
2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.
3. Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.
   
   ![Uygulamaları](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "uygulamalar")
4. Tıklatın **Ekle** hello sayfanın hello sonundaki.
   
   ![Uygulama ekleme](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "uygulama ekleme")
5. Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.
   
   ![Galeriden bir uygulama eklemek](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Galeriden bir uygulama ekleme")
6. Merhaba, **arama kutusu**, türü **Qualtrics**.
   
   ![Uygulama Galerisi](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "uygulama Galerisi")
7. Merhaba sonuçlar bölmesinde seçin **Qualtrics**ve ardından **tam** tooadd Merhaba uygulaması.
   
   ![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")
   
## <a name="configure-single-sign-on"></a>Çoklu oturum açmayı yapılandırın

Bu bölümde Hello amacı nasıl tooenable kullanıcılar tooauthenticate tooQualtrics Federasyon kullanarak Azure AD'de hesabıyla hello SAML protokolünü temel toooutline ' dir.

**tooconfigure çoklu oturum açma, hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Klasik Azure portalı içinde **Qualtrics** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **tek oturum yapılandırma üzerinde aktar** iletişim.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "çoklu oturum açmayı yapılandırın")
2. Merhaba üzerinde **nasıl tooQualtrics üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "çoklu oturum açmayı yapılandırın")
3. Hello üzerinde **uygulama URL'sini yapılandırın** sayfasında hello **üzerinde Qualtrics oturum URL'si** metin kutusuna, URL'nizi yazın (örn: "*https://ssotest2ut1.qualtrics.com*") ve ardından **Sonraki**.
   
   ![Uygulama URL'sini Yapılandır](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "uygulama URL'sini yapılandırın")
4. Merhaba üzerinde **çoklu oturum açma sırasında Qualtrics yapılandırma** sayfasında, **karşıdan meta veri**ve hello meta veri dosyası, bilgisayarınıza kaydedin.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "çoklu oturum açmayı yapılandırın")
5. Merhaba meta veri dosyası toohello Qualtrics Destek ekibine gönderin.
   
   >[!NOTE]
   >Merhaba SSO yapılandırma hello Qualtrics destek ekibi tarafından gerçekleştirilen toobe sahiptir. Merhaba Yapılandırma tamamlandıktan hemen sonra bir bildirim alırsınız.
   > 
   > 
6. Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **tam** tooclose hello **tek oturum yapılandırma üzerinde aktar** iletişim.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "çoklu oturum açmayı yapılandırın")
   
## <a name="configure-user-provisioning"></a>Kullanıcı sağlamayı Yapılandır

TooQualtrics sağlama, tooconfigure kullanıcı için eylem öğe yok. Atanmış bir kullanıcı hello erişim paneli kullanılarak Qualtrics toolog çalıştığında Qualtrics hello kullanıcı var olup olmadığını denetler.  

Hiçbir kullanıcı hesabı varsa kullanılabilir henüz, Qualtrics tarafından otomatik olarak oluşturulur.

## <a name="assign-users"></a>Kullanıcılar atama
tootest yapılandırmanıza, uygulama erişim tooit atayarak kullanarak tooallow istediğiniz toogrant hello Azure AD kullanıcıları gerekir.

**tooassign kullanıcılar tooQualtrics hello aşağıdaki adımları gerçekleştirin:**

1. Hello Klasik Azure portalı, bir test hesabı oluşturun.
2. Hello üzerinde **Qualtrics** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.
   
   ![Kullanıcılar atama](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "kullanıcı atama")
3. Test kullanıcınız seçin, **atamak**ve ardından **Evet** tooconfirm, atama.
   
   ![Evet](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Evet")

SSO ayarlarınızı tootest istiyorsanız hello erişim paneli açın. Merhaba erişim paneli hakkında daha fazla ayrıntı için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

