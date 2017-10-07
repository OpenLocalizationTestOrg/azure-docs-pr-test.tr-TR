---
title: "Öğretici: Azure Active Directory Tümleştirme ile TOPdesk - genel | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile TOPdesk - genel arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ef0dd06157ecc3b33814590039f5cbae64e8c916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a>Öğretici: Azure Active Directory Tümleştirme ile TOPdesk - genel

Bu öğreticide, bilgi nasıl toointegrate TOPdesk - Azure Active Directory (Azure AD) ile ortak.

TOPdesk - genel Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Genel erişim tooTOPdesk - olan Azure AD'de kontrol edebilirsiniz.
- Kullanıcıların tooautomatically get açan tooTOPdesk - Azure AD hesaplarına sahip (çoklu oturum açma) ortak etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure TOPdesk ile-Azure AD tümleştirme genel, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- TOPdesk - genel çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Ortak hello galerisinden TOPdesk - ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-topdesk---public-from-hello-gallery"></a>Ortak hello galerisinden TOPdesk - ekleme
TOPdesk - Azure AD'ye ortak tooconfigure hello tümleştirilmesi tooadd TOPdesk - genel hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd TOPdesk - hello galerisinden ortak hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna yazın **TOPdesk - genel**seçin **TOPdesk - genel** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![TOPdesk - genel hello sonuçları listesinde](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma TOPdesk ile test etme - genel "Britta Simon" adlı bir test kullanıcı tabanlı.

Çoklu oturum açma toowork, Azure AD tooknow TOPdesk hangi hello karşılık gelen kullanıcı gereken - Azure AD içinde ortak tooa kullanıcıdır. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı TOPdesk - hello arasında bir bağlantı ilişkisi ortak kurulan toobe gerekir.

TOPdesk içinde-ortak, Ata hello hello değerini **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Azure AD çoklu oturum açma ile TOPdesk - genel test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[TOPdesk - genel test kullanıcısı oluşturma](#create-a-topdesk---public-test-user)**  - toohave Britta Simon TOPdesk içinde karşılık gelen - kullanıcı bağlantılı toohello Azure AD gösterimidir ortak.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma, TOPdesk - genel uygulama yapılandırın.

**Azure AD çoklu oturum açma tooconfigure TOPdesk ile-ortak hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **TOPdesk - genel** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. Merhaba üzerinde **TOPdesk - ortak etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![TOPdesk - ortak etki alanı ve URL'ler tek oturum açma bilgileri](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.topdesk.net`
    
    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.topdesk.net/tas/public/login/verify`

    c. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.topdesk.net/tas/public/login/saml`
     
    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler. Yanıt açıklaması daha sonra öğreticide URL'dir. Kişi [TOPdesk - ortak istemci destek ekibi](https://help.topdesk.com/saas/enterprise/user/) tooget bu değerleri.  

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. Merhaba üzerinde **TOPdesk - genel yapılandırması** 'yi tıklatın **TOPdesk - ortak yapılandırma** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![TOPdesk - genel yapılandırması](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. Tooyour üzerinde oturum **TOPdesk - genel** yönetici olarak şirket site.

8. Merhaba, **TOPdesk** menüsünde tıklatın **ayarları**.
   
    ![Ayarları](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "ayarları")

9. Tıklatın **oturum açma ayarları**.
   
    ![Oturum açma ayarları](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "oturum açma ayarları")

10. Merhaba genişletin **oturum açma ayarları** menüsüne ve ardından **genel**.
   
    ![Genel](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "genel")

11. Merhaba, **ortak** hello bölümünü **SAML oturum açma** yapılandırma bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![Teknik ayarları](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "teknik ayarları")
   
    a. Tıklatın **karşıdan** toodownload hello ortak meta veri dosyası ve bilgisayarınıza yerel olarak kaydedin.
   
    b. İndirilen hello meta veri dosyasını açın ve hello bulun **AssertionConsumerService** düğümü.

    ![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")
   
    c. Kopya hello **AssertionConsumerService** değeri, bu değer hello yapıştırın **yanıt URL'si** metin kutusuna **TOPdesk - ortak etki alanı ve URL'leri** bölümü.      
   
12. bir sertifika dosyası toocreate hello aşağıdaki adımları gerçekleştirin:
    
    ![Sertifika](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "sertifika")
    
    a. Açık hello Azure portalından meta veri dosyası indirilir.
    
    b. Merhaba genişletin **RoleDescriptor** sahip düğümü bir **xsi: type** , **ssas'nin: ApplicationServiceType**.
    
    c. Merhaba Hello değerini kopyalayın **X509Certificate** düğümü.
    
    d. Kopyalanan Kaydet hello **X509Certificate** yerel olarak bilgisayarınızda bir dosyada değeri.

13. Merhaba, **ortak** 'yi tıklatın **Ekle**.
    
    ![SAML oturum açma](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML oturum açma")

14. Merhaba üzerinde **SAML Yapılandırması Yardımcısı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
    
    ![SAML Yapılandırması Yardımcısı](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML Yapılandırması Yardımcısı")
    
    a. tooupload indirilen meta verileriniz dosya Azure portalından altında **Federasyon meta verileri**, tıklatın **Gözat**.

    b. altında sertifikanızı dosya tooupload **sertifika (RSA)**, tıklatın **Gözat**.

    c. aldığınız hello TOPdesk destek ekibinden altında tooupload hello logo dosyası **Logo simgesini**, tıklatın **Gözat**.

    d. Merhaba, **kullanıcı adı özniteliği** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.

    e. Merhaba, **görünen adı** metin kutusuna, yapılandırmanız için bir ad yazın.

    f. **Kaydet** düğmesine tıklayın.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

   ![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    a. Merhaba, **adı** kutusuna **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.

    c. Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-a-topdesk---public-test-user"></a>TOPdesk - genel test kullanıcısı oluşturma

Sipariş tooenable Azure AD kullanıcıların toolog TOPdesk - içine içinde ortak, bunlar sağlanmalıdır TOPdesk - genel.  
TOPdesk - hello durumda ortak, sağlama olduğunu el ile bir görev.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:
1. Tooyour üzerinde oturum **TOPdesk - genel** yönetici olarak şirket site.

2. Hello içinde hello üst menüsünde **TOPdesk \> yeni \> destek dosyalarını \> kişi**.
   
    ![Kişi](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "kişi")

3. Merhaba yeni bir kişiye iletişim kutusunda hello aşağıdaki adımları gerçekleştirin:
   
    ![Yeni bir kişiye](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "yeni bir kişiye")
   
    a. Merhaba Genel sekmesini tıklatın.

    b. Merhaba, **Soyadı** metin kutusuna, Simon gibi hello kullanıcının soyadını yazın
 
    c. Seçin bir **Site** hello hesabı.
 
    d. **Kaydet** düğmesine tıklayın.

> [!NOTE]
> Herhangi bir TOPdesk - genel kullanıcı hesabı oluşturma araçlarını veya TOPdesk - genel tooprovision Azure AD kullanıcı hesapları tarafından sağlanan API'leri kullanabilirsiniz.

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooTOPdesk - genel vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200] 

**tooassign Britta Simon tooTOPdesk - genel hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **TOPdesk - genel**.

    ![Merhaba TOPdesk - ortak bağlantı hello uygulamalar listesinde](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba TOPdesk - tıklattığınızda genel kutucuğu hello erişim paneli, otomatik olarak oturum açma tooyour TOPdesk - genel uygulama almanız gerekir.
Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

