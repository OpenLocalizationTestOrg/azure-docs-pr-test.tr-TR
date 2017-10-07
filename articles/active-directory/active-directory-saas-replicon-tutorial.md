---
title: "Öğretici: Azure Active Directory Tümleştirme ile Replicon | Microsoft Docs"
description: "Azure Active Directory tooenable ile toouse Replicon nasıl tek oturum açma, otomatik sağlama ve daha fazlasını öğrenin!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 4949eaf959265cfa4f732a2b73317fffe6312a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a>Öğretici: Azure Active Directory Tümleştirme Replicon ile
Merhaba amacı Bu öğretici, Azure ve Replicon tooshow hello tümleştirme ' dir. Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

* Geçerli bir Azure aboneliği
* Replicon Kiracı

Bu öğreticiyi tamamladıktan sonra tooReplicon atamış hello Azure AD kullanıcıların mümkün toosingle oturum Replicon şirket sitenizin (servis sağlayıcı tarafından başlatılan oturum açma) veya hello kullanarak hello uygulamaya olacaktır [giriş toohello erişim Panel](active-directory-saas-access-panel-introduction.md).

Bu öğreticide gösterilen hello senaryo yapı taşları aşağıdaki Merhaba oluşur:

1. Merhaba uygulama tümleştirmesi Replicon için etkinleştirme
2. Çoklu oturum açma (SSO) yapılandırma
3. Kullanıcı hazırlama işleminin yapılandırılması
4. Kullanıcılar atama

![Senaryo](./media/active-directory-saas-replicon-tutorial/IC777798.png "senaryosu")

## <a name="enable-hello-application-integration-for-replicon"></a>Merhaba uygulama tümleştirmesi Replicon için etkinleştirme
Bu bölümde Hello amacı olan toooutline nasıl tooenable hello uygulama tümleştirmesi Replicon için.

**tooenable hello uygulama tümleştirmesi Replicon için hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol gezinti bölmesinde, Klasik Azure portalı tıklatın **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")
2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.
3. Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.
   
    ![Uygulamaları](./media/active-directory-saas-replicon-tutorial/IC700994.png "uygulamalar")
4. Tıklatın **Ekle** hello sayfanın hello sonundaki.
   
    ![Uygulama ekleme](./media/active-directory-saas-replicon-tutorial/IC749321.png "uygulama ekleme")
5. Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.
   
    ![Galeriden bir uygulama eklemek](./media/active-directory-saas-replicon-tutorial/IC749322.png "Galeriden bir uygulama ekleme")
6. Merhaba, **arama kutusu**, türü **Replicon**.
   
    ![Uygulama Galerisi](./media/active-directory-saas-replicon-tutorial/IC777799.png "uygulama Galerisi")
7. Merhaba sonuçlar bölmesinde seçin **Replicon**ve ardından **tam** tooadd Merhaba uygulaması.
   
    ![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")
   
## <a name="configure-single-sign-on"></a>Çoklu oturum açmayı yapılandırın

Bu bölümde Hello amacı nasıl tooenable kullanıcılar tooauthenticate tooReplicon Federasyon kullanarak Azure AD'de hesabıyla hello SAML protokolünü temel toooutline ' dir.

**tooconfigure çoklu oturum açma, hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Klasik Azure portalı içinde **Replicon** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **tek oturum yapılandırma üzerinde aktar** iletişim.
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-replicon-tutorial/IC777801.png "çoklu oturum açmayı yapılandırın")
2. Merhaba üzerinde **nasıl tooReplicon üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-replicon-tutorial/IC777802.png "çoklu oturum açmayı yapılandırın")
3. Merhaba üzerinde **uygulama URL'sini Yapılandır** sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Uygulama URL'sini Yapılandır](./media/active-directory-saas-replicon-tutorial/IC777803.png "uygulama URL'sini yapılandırın")
  1. Merhaba, **üzerinde Replicon oturum URL'si** metin kutusuna, Replicon Kiracı URL'nizi yazın (örneğin: *https://na2.replicon.com/company/saml2/sp-sso/post*).
  2. Merhaba, **Replicon yanıt URL'si** metin, Replicon yazın **AssertionConsumerService** URL'si (örn: *https://global.replicon.com/! / saml2/şirket/sso/post*).  
      
     >[!NOTE]
     >Hello Replicon meta verilerden hello URL elde edebilirsiniz: **https://global.replicon.com/! /saml2/\<YourCompanyKey\>**.
     > 
     > 
 
  3. **İleri**’ye tıklayın.

4. Hello üzerinde **çoklu oturum açma sırasında Replicon yapılandırmak** sayfası, toodownload meta verileriniz tıklatın **karşıdan meta veri**ve ardından hello meta verileri bilgisayarınıza kaydedin.
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-replicon-tutorial/IC777804.png "çoklu oturum açmayı yapılandırın")
5. Farklı web tarayıcısı penceresinde Replicon şirket sitenize yönetici olarak oturum açın.

6. SAML 2.0 tooconfigure hello aşağıdaki adımları gerçekleştirin:
   
    ![SAML kimlik doğrulamasını etkinleştir](./media/active-directory-saas-replicon-tutorial/IC777805.png "etkinleştirmek SAML kimlik doğrulaması")
  
  1. toodisplay hello **EnableSAML Authentication2** iletişim kutusunda, tooyour URL, şirket anahtarınızı sonra aşağıdaki hello ekleme: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**  
    * Merhaba aşağıdaki hello tam URL hello şeması gösterir:  
   **https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**
   2. Merhaba tıklatın  **+**  tooexpand hello **v20Configuration** bölümü.
   3. Merhaba tıklatın  **+**  tooexpand hello **metaDataConfiguration** bölümü.
   4. Tıklatın **Dosya Seç**, tooselect kimlik sağlayıcısı meta verileri XML dosyasını ve tıklatın **gönderme**.

7. Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **tam** tooclose hello **tek oturum yapılandırma üzerinde aktar** iletişim.
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-replicon-tutorial/IC778418.png "çoklu oturum açmayı yapılandırın")
   
## <a name="configure-user-provisioning"></a>Kullanıcı sağlamayı Yapılandır

Replicon içine sipariş tooenable Azure AD kullanıcıların toolog bunların Replicon sağlanmalıdır.  

Replicon Hello durumda sağlama bir el ile bir görevdir.

**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**

1. Bir web tarayıcısı penceresinde Replicon şirket sitenize yönetici olarak oturum açın.
2. Çok Git**Yönetim \> kullanıcılar**.
   
    ![Kullanıcıların](./media/active-directory-saas-replicon-tutorial/IC777806.png "kullanıcılar")
3. Tıklatın **+ kullanıcı ekleme**.
   
    ![Kullanıcı ekleme](./media/active-directory-saas-replicon-tutorial/IC777807.png "kullanıcı ekleme")
4. Merhaba, **kullanıcı profili** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![Kullanıcı profili](./media/active-directory-saas-replicon-tutorial/IC777808.png "kullanıcı profili")
   
  1. Merhaba, **oturum açma adı** metin kutusuna, türü hello Azure AD e-posta adresini istediğiniz hello Azure AD kullanıcı tooprovision.
  2. Olarak **kimlik doğrulama türü**seçin **SSO**.
  3. Merhaba, **departmanı** metin kutusuna, hello kullanıcının bölüm adını yazın.
  4. Olarak **çalışan türü**seçin **yönetici**.
  5. Tıklatın **kullanıcı profili Kaydet**.

>[!NOTE]
>API AAD kullanıcı hesaplarının Replicon tooprovision tarafından sağlanan veya herhangi diğer Replicon kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.
> 
> 

## <a name="assign-users"></a>Kullanıcılar atama
tootest yapılandırmanıza, uygulama erişim tooit atayarak kullanarak tooallow istediğiniz toogrant hello Azure AD kullanıcıları gerekir.

**tooassign kullanıcılar tooReplicon hello aşağıdaki adımları gerçekleştirin:**

1. Hello Klasik Azure portalı, bir test hesabı oluşturun.

2. Hello üzerinde **Replicon** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.
   
    ![Kullanıcılar atama](./media/active-directory-saas-replicon-tutorial/IC777809.png "kullanıcı atama")

3. Test kullanıcınız seçin, **atamak**ve ardından **Evet** tooconfirm, atama.
   
    ![Evet](./media/active-directory-saas-replicon-tutorial/IC767830.png "Evet")

Çoklu oturum açma ayarlarınızı tootest istiyorsanız hello erişim paneli açın. Merhaba erişim paneli hakkında daha fazla ayrıntı için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

