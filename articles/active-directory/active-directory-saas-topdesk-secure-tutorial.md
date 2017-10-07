---
title: "Öğretici: Azure Active Directory Tümleştirme TOPdesk - güvenli ile | Microsoft Docs"
description: "Bilgi nasıl toouse TOPdesk - Azure Active Directory tooenable çoklu oturum açma, otomatik sağlama ve daha fazla ile güvenli!."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 10fe420d1691c2845b89c779486ffd6fcd736432
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a>Öğretici: Azure Active Directory Tümleştirme TOPdesk - güvenli ile
Merhaba amacı Bu öğretici, Azure ve TOPdesk tooshow hello tümleştirme - güvenli.  
Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

* Geçerli bir Azure aboneliği
* TOPdesk - bir abonelik etkin güvenli çoklu oturum açma

Tamamladıktan sonra Bu öğreticide, Azure AD hello kullanıcılar güvenli olacak tooTOPdesk - atadığınız mümkün toosingle oturum hello uygulamaya TOPdesk - güvenli şirket site (servis sağlayıcı tarafından başlatılan oturum açma) konumunda olması ya da hello kullanarak [giriş Erişim paneli toohello](active-directory-saas-access-panel-introduction.md).

Bu öğreticide gösterilen hello senaryo yapı taşları aşağıdaki Merhaba oluşur:

1. Merhaba uygulama tümleştirmesi TOPdesk - güvenli için etkinleştirme
2. Çoklu oturum açmayı yapılandırma
3. Kullanıcı hazırlama işleminin yapılandırılması
4. Kullanıcılar atama

![Senaryo](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "senaryosu")

## <a name="enabling-hello-application-integration-for-topdesk---secure"></a>Merhaba uygulama tümleştirmesi TOPdesk - güvenli için etkinleştirme
Bu bölümde Hello amacı olan toooutline nasıl tooenable hello uygulama tümleştirmesi TOPdesk - güvenli için.

### <a name="tooenable-hello-application-integration-for-topdesk---secure-perform-hello-following-steps"></a>tooenable hello uygulama tümleştirmesi TOPdesk - güvenli için hello aşağıdaki adımları gerçekleştirin:
1. Merhaba hello sol gezinti bölmesinde, Klasik Azure portalı tıklatın **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")

2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.

3. Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.
   
    ![Uygulamaları](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "uygulamalar")

4. Tıklatın **Ekle** hello sayfanın hello sonundaki.
   
    ![Uygulama ekleme](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "uygulama ekleme")

5. Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.
   
    ![Galeriden bir uygulama eklemek](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Galeriden bir uygulama ekleme")

6. Merhaba, **arama kutusu**, türü **TOPdesk - güvenli**.
   
    ![Uygulama Galerisi](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "uygulama Galerisi")

7. Merhaba sonuçlar bölmesinde seçin **TOPdesk - güvenli**ve ardından **tam** tooadd Merhaba uygulaması.
   
    ![TOPdesk - güvenli](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - güvenli")

## <a name="configuring-single-sign-on"></a>Çoklu oturum açmayı yapılandırma
Bu bölümde Hello amacı olan toooutline nasıl tooenable kullanıcılar tooauthenticate tooTOPdesk - SAML Protokolü hello üzerinde temel Federasyon kullanarak Azure AD ile kendi hesaplarını güvenli.  
Yapılandırma tek oturum açma için TOPdesk - güvenli tooupload bir logo simge dosyası gerektirir. tooget hello simge dosyası, kişi hello TOPdesk destek ekibi.

### <a name="tooconfigure-single-sign-on-perform-hello-following-steps"></a>tooconfigure çoklu oturum açma, hello aşağıdaki adımları gerçekleştirin:
1. Tooyour üzerinde oturum **TOPdesk - güvenli** yönetici olarak şirket site.
2. Merhaba, **TOPdesk** menüsünde tıklatın **ayarları**.
   
    ![Ayarları](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "ayarları")

3. Tıklatın **oturum açma ayarları**.
   
    ![Oturum açma ayarları](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "oturum açma ayarları")

4. Merhaba genişletin **oturum açma ayarları** menüsüne ve ardından **genel**.
   
    ![Genel](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "genel")

5. Merhaba, **güvenli** hello bölümünü **SAML oturum açma** yapılandırma bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![Teknik ayarları](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "teknik ayarları")
   
    a. Tıklatın **karşıdan** toodownload hello ortak meta veri dosyası ve bilgisayarınıza yerel olarak kaydedin.
   
    b. Merhaba meta veri dosyasını açın ve ardından hello bulun **AssertionConsumerService** düğümü.
    
    ![Onaylama işlemi tüketici hizmeti](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "onaylama tüketici hizmeti")
   
    c. Kopya hello **AssertionConsumerService** değeri.  
      
    > [!NOTE]
    > Merhaba değerinde hello **uygulama URL'sini Yapılandır** Bu öğreticinin ilerleyen bölümlerinde.
    > 
    > 

6. Farklı web tarayıcısı penceresinde oturum açın, **Klasik Azure portalı** yönetici olarak.

7. Merhaba üzerinde **TOPdesk - güvenli** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello ** tek oturum yapılandırma üzerinde Aktar ** iletişim.
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "çoklu oturum açmayı yapılandırın")

8. Merhaba üzerinde **nasıl bölüştürüleceğini kullanıcılar toosign tooTOPdesk üzerinde-gibi güvenli** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "çoklu oturum açmayı yapılandırın")

9. Merhaba üzerinde **uygulama URL'sini Yapılandır** sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Uygulama URL'sini Yapılandır](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "uygulama URL'sini yapılandırın")
   
    a. Merhaba, **TOPdesk - URL üzerinde güvenli oturum** metin kutusuna, TOPdesk - güvenli uygulama, kullanıcıların toosign tarafından kullanılan türü hello URL'si (örn: "*https://qssolutions.topdesk.net*").
   
    b. Merhaba, **TOPdesk – ortak yanıt URL'si** metin kutusuna, Yapıştır hello **TOPdesk - güvenli AssertionConsumerService URL** (örn: "*https://qssolutions.topdesk.net/tas/public/login/saml*")
   
    c. **İleri**’ye tıklayın.

10. Merhaba üzerinde **çoklu oturum açma sırasında TOPdesk - güvenli yapılandırma** sayfası, toodownload, meta veri dosyası tıklatın **karşıdan meta veri**ve yerel olarak bilgisayarınızda hello dosyasını kaydedin.
    
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "çoklu oturum açmayı yapılandırın")

11. bir sertifika dosyası toocreate hello aşağıdaki adımları gerçekleştirin:
    
    ![Sertifika](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "sertifika")
    
    a. Açık hello indirilen meta veri dosyası.
    b. Merhaba genişletin **RoleDescriptor** sahip düğümü bir **xsi: type** , **ssas'nin: ApplicationServiceType**.
    c. Merhaba Hello değerini kopyalayın **X509Certificate** düğümü.
    d. Kopyalanan Kaydet hello **X509Certificate** yerel olarak bilgisayarınızda bir dosyada değeri.

12. Üzerinde TOPdesk - şirket sitede hello güvenli **TOPdesk** menüsünde tıklatın **ayarları**.
    
    ![Ayarları](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "ayarları")

13. Tıklatın **oturum açma ayarları**.
    
    ![Oturum açma ayarları](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "oturum açma ayarları")

14. Merhaba genişletin **oturum açma ayarları** menüsüne ve ardından **genel**.
    
    ![Genel](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "genel")

15. Merhaba, **ortak** 'yi tıklatın **Ekle**.
    
    ![Ekleme](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "ekleme")

16. Merhaba üzerinde **SAML Yapılandırması Yardımcısı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
    
    ![SAML Yapılandırması Yardımcısı](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Yapılandırması Yardımcısı")
    
    a. indirilen, meta veri dosyası, altında tooupload **Federasyon meta verileri**, tıklatın **Gözat**.

    b. altında sertifikanızı dosya tooupload **sertifika (RSA)**, tıklatın **Gözat**.

    c. aldığınız hello TOPdesk destek ekibinden altında tooupload hello logo dosyası **Logo simgesini**, tıklatın **Gözat**.

    d. Merhaba, **kullanıcı adı özniteliği** metin kutusuna, türü **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.

    e. Merhaba, **görünen adı** metin kutusuna, yapılandırmanız için bir ad yazın.

    f. **Kaydet** düğmesine tıklayın.

17. Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **tam** tooclose hello **tek oturum yapılandırma üzerinde aktar** iletişim.
    
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "çoklu oturum açmayı yapılandırın")

## <a name="configuring-user-provisioning"></a>Kullanıcı hazırlama işleminin yapılandırılması
Sipariş tooenable Azure AD kullanıcıların toolog TOPdesk - içine içinde güvenli, bunların TOPdesk - güvenli sağlanmalıdır.  
Merhaba TOPdesk - durumda sağlama el ile bir görev güvenlidir.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:
1. Tooyour üzerinde oturum **TOPdesk - güvenli** yönetici olarak şirket site.
2. Hello içinde hello üst menüsünde **TOPdesk \> yeni \> destek dosyalarını \> işleci**.
   
    ![İşleç](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "işleci")

3. Merhaba üzerinde **New işleci** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
    ![New işleci](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New işleci")
   
    a. Merhaba Genel sekmesini tıklatın.
   
    b. Merhaba, **Soyadı** hello textbox **genel** bölümü, tür hello son adını tooprovision istediğiniz geçerli bir Azure Active Directory hesabı.
   
    c. Seçin bir **Site** hello hello hesap için **konumu** bölümü.
   
    d. Merhaba, **oturum açma adı** hello textbox **TOPdesk oturum açma** bölümünde, kullanıcı oturum açma adını yazın.
   
    e. **Kaydet** düğmesine tıklayın.

> [!NOTE]
> Tüm diğer TOPdesk - güvenli kullanıcı hesabı oluşturma araçlarını veya TOPdesk tarafından - API'lerinden güvenli tooprovision AAD kullanıcı hesaplarını kullanabilirsiniz.
> 
> 

## <a name="assigning-users"></a>Kullanıcılar atama
tootest yapılandırmanıza, uygulama erişim tooit atayarak kullanarak tooallow istediğiniz toogrant hello Azure AD kullanıcıları gerekir.

### <a name="tooassign-users-tootopdesk---secure-perform-hello-following-steps"></a>tooassign kullanıcılar tooTOPdesk - güvenli, hello aşağıdaki adımları gerçekleştirin:
1. Hello Klasik Azure portalı, bir test hesabı oluşturun.
2. Hello üzerinde ** TOPdesk - güvenli ** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.
   
    ![Kullanıcılar atama](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "kullanıcı atama")

3. Test kullanıcınız seçin, **atamak**ve ardından **Evet** tooconfirm, atama.
   
    ![Evet](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Evet")

Çoklu oturum açma ayarlarınızı tootest istiyorsanız hello erişim paneli açın. Merhaba erişim paneli hakkında daha fazla ayrıntı için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

