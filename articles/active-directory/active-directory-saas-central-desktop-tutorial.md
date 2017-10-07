---
title: "Öğretici: Azure Active Directory Tümleştirme Merkezi Masaüstü ile | Microsoft Docs"
description: "Azure Active Directory tooenable ile toouse Merkezi Masaüstü nasıl tek oturum açma, otomatik sağlama ve daha fazlasını öğrenin!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 93036ae801c446ce476288c00579931ba10a843b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a>Öğretici: Azure Active Directory Tümleştirme ile Merkezi Masaüstü
Merhaba amacı Bu öğretici, Azure ve Merkezi Masaüstü tooshow hello tümleştirme ' dir. Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

* Geçerli bir Azure aboneliği
* Merkezi bir masaüstü çoklu oturum açma etkin Abonelik / Merkezi Masaüstü Kiracı

Bu öğreticide gösterilen hello senaryo yapı taşları aşağıdaki Merhaba oluşur:

* Merhaba uygulama tümleştirmesi Merkezi Masaüstü için etkinleştirme
* Çoklu oturum açma (SSO) yapılandırma
* Kullanıcı hazırlama işleminin yapılandırılması
* Kullanıcılar atama

![Senaryo](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "senaryosu")

## <a name="enable-hello-application-integration-for-central-desktop"></a>Merhaba uygulama tümleştirmesi Merkezi Masaüstü için etkinleştirmek
Bu bölümde Hello amacı olan toooutline nasıl tooenable hello uygulama tümleştirmesi Merkezi Masaüstü için.

**Merkezi Masaüstü tooenable hello uygulama tümleştirmesi hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol gezinti bölmesinde, Klasik Azure portalı tıklatın **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")
2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.
3. Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.
   
   ![Uygulamaları](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "uygulamalar")
4. Tıklatın **Ekle** hello sayfanın hello sonundaki.
   
   ![Uygulama ekleme](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "uygulama ekleme")
5. Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.
   
   ![Galeriden bir uygulama eklemek](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Galeriden bir uygulama ekleme")
6. Merhaba, **arama kutusu**, türü **Merkezi Masaüstü**.
   
   ![Uygulama Galerisi](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "uygulama Galerisi")
7. Merhaba sonuçlar bölmesinde seçin **Merkezi Masaüstü**ve ardından **tam** tooadd Merhaba uygulaması.
   
   ![Merkezi Masaüstü](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Merkezi Masaüstü")
   
## <a name="configure-single-sign-on"></a>Çoklu oturum açmayı yapılandırın

Bu bölümde Hello amacı nasıl hello SAML protokolünü kullanarak Federasyon Azure AD'de hesabıyla tooenable kullanıcılar tooauthenticate tooCentral Masaüstü temel toooutline ' dir.

Bu yordam bir parçası, gerekli tooupload base-64 kodlanmış sertifika tooyour Merkezi Masaüstü Kiracı olur.  
Bu yordama bilmiyorsanız bkz [nasıl tooconvert bir ikili sertifika bir metin dosyasına](http://youtu.be/PlgrzUZ-Y1o).

**tooconfigure çoklu oturum açma, hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Klasik Azure portalı içinde **Merkezi Masaüstü** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello ** tek oturum yapılandırma üzerinde Aktar ** iletişim.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "çoklu oturum açmayı yapılandırın")
2. Merhaba üzerinde **nasıl tooCentral Masaüstü üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "çoklu oturum açmayı yapılandırın")
3. Merhaba üzerinde **uygulama URL'sini Yapılandır** sayfasında, aşağıdaki adımları hello gerçekleştirmek ve ardından **sonraki**: 
   
   1. Merhaba, **Merkezi Masaüstü Oturum açma URL'si** metin kutusuna, Merkezi Masaüstü kiracınızın türü hello URL'si (örn: *http://contoso.centraldesktop.com*).
   2. Merkezi Masaüstü AssertionConsumerService URL'nizi Hello Merkezi Masaüstü yanıt URL'si metin kutusuna yazın (örneğin: https://contoso.centraldesktop.com/saml2-assertion.php).
   
   >[!NOTE]
   >Merhaba değer hello Merkezi Masaüstü meta verileri alabilir (örn: *http://contoso.centraldesktop.com*).
   >  
   
   ![Uygulama URL'sini Yapılandır](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "uygulama URL'sini yapılandırın")
4. Merhaba üzerinde **çoklu oturum açma sırasında Merkezi Masaüstü yapılandırma** sayfası, toodownload, sertifikanızı tıklatın **indirme sertifika**ve hello sertifika dosyayı bilgisayarınıza kaydedin.
   
  ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "çoklu oturum açmayı yapılandırın")
5. İçinde tooyour oturum **Merkezi Masaüstü** Kiracı.
6. Çok Git**ayarları**, tıklatın **Gelişmiş**ve ardından **çoklu oturum açma**.
   
  ![Kurulum - Gelişmiş](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Kurulum - Gelişmiş")
7. Merhaba üzerinde **tek oturum açma ayarları** sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
  ![Çoklu oturum açma ayarları](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "tek oturum açma ayarları")
   
  1. Seçin **etkinleştir SAML v2 çoklu oturum açma**.
  2. Hello hello üzerinde Klasik Azure Portalı'nda **çoklu oturum açma sırasında Merkezi Masaüstü yapılandırma** sayfası, kopyalama hello **veren URL'si** değer ve hello yapıştırma **SSO URL** metin kutusu.
  3. Merhaba hello üzerinde Klasik Azure Portalı'nda **çoklu oturum açma sırasında Merkezi Masaüstü yapılandırma** sayfası, kopyalama hello **uzaktan oturum açma URL'si** değer ve hello yapıştırma **SSO oturum açma URL'si**metin kutusu.
  4. Merhaba hello üzerinde Klasik Azure Portalı'nda **çoklu oturum açma sırasında Merkezi Masaüstü yapılandırma** sayfası, kopyalama hello **tek Sign-Out hizmeti URL'si** değer ve hello yapıştırma **SSO oturum kapatma URL'si** metin kutusu.
8. Merhaba, **ileti imzası doğrulama yöntemi** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
   ![İleti imzası doğrulama yöntemi](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "ileti imzası doğrulama yöntemi")
   
  1. Seçin **sertifika**.
  2. Merhaba gelen **SSO sertifika** listesinde **RSH SHA256**.
  3. İndirilen hello sertifikadan kopyalama hello hello metin dosyasının içeriğini bir metin dosyası oluşturun ve hello yapıştırın **SSO sertifika** alan.  
     >[!TIP]
     >Daha fazla ayrıntı için bkz: [nasıl tooconvert bir ikili sertifika bir metin dosyasına](http://youtu.be/PlgrzUZ-Y1o)
      >  
   4. Seçin **bir bağlantı tooyour SAMLv2 oturum açma sayfasını görüntülemek**.
9. Tıklatın **güncelleştirme**.
10. Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **tam** tooclose hello **tek oturum yapılandırma üzerinde aktar** iletişim.
    
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "çoklu oturum açmayı yapılandırın")
    
## <a name="configure-user-provisioning"></a>Kullanıcı sağlamayı Yapılandır

AAD kullanıcılar toobe mümkün toosign için bunların sağlanan toohello Merkezi Masaüstü uygulaması olması gerekir. Bu bölümde, nasıl Merkezi Masaüstü toocreate AAD kullanıcı hesapları açıklanmaktadır.

**tooprovision kullanıcı hesapları tooCentral Masaüstü:**
1. İçinde tooyour Merkezi Masaüstü Kiracı oturum açın.
2. Çok Git**kişiler \> iç üyeleri**.
3. Tıklatın **iç üye eklemek**.
   
  ![Kişiler](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "kişiler")
4. Merhaba, **yeni üyeler e-posta adresi** metin kutusuna, tooprovision istediğiniz ve ardından bir AAD hesabıyla yazın **sonraki**.
   
  ![E-posta adreslerini yeni üyeler](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "e-posta adreslerini yeni üyeler")
5. Tıklatın **Ekle iç üyeleri**.
   
  ![İç üye ekleme](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "iç üye ekleme")
   
   >[!NOTE]
   >eklediğiniz hello kullanıcılar tooclick tooactivate hello hesabına ihtiyaç duydukları onay bağlantısı içeren bir e-posta alır.
   > 

>[!NOTE]
>API AAD kullanıcı hesaplarını Merkezi Masaüstü tooprovision tarafından sağlanan veya herhangi diğer Merkezi Masaüstü kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz
>  

## <a name="assign-users"></a>Kullanıcılar atama
tootest yapılandırmanıza, uygulama erişim tooit atayarak kullanarak tooallow istediğiniz toogrant hello Azure AD kullanıcıları gerekir.

**tooassign kullanıcılar tooCentral Masaüstü hello aşağıdaki adımları gerçekleştirin:**

1. Hello Klasik Azure portalı, bir test hesabı oluşturun.
2. Hello üzerinde **Merkezi Masaüstü** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.
   
   ![Kullanıcılar atama](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "kullanıcı atama")
3. Test kullanıcınız seçin, **atamak**ve ardından **Evet** tooconfirm, atama.
   
   ![Evet](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Evet")

Çoklu oturum açma ayarlarınızı tootest istiyorsanız hello erişim paneli açın. Merhaba erişim paneli hakkında daha fazla ayrıntı için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

