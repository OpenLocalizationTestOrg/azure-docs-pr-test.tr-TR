---
title: "Öğretici: Azure Active Directory Tümleştirme MOVEit Transfer - Azure AD Tümleştirmesi ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile MOVEit Transfer - Azure AD tümleştirme arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 5bbe4f2d952bd45c4d58d55ffc3467b4eb871fd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a>Öğretici: Azure Active Directory Tümleştirme ile MOVEit Transfer - Azure AD tümleştirme

Bu öğreticide, bilgi nasıl toointegrate MOVEit Transfer - Azure Active Directory (Azure AD) ile Azure AD tümleştirme.

MOVEit Transfer - Azure AD tümleştirme Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooMOVEit Transfer - Azure AD tümleştirme sahip Azure AD'de kontrol edebilirsiniz.
- Kullanıcıların tooautomatically get açan tooMOVEit Transfer - Azure AD hesaplarına ile Azure AD tümleştirme (çoklu oturum açma) etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure MOVEit Transfer - Azure AD Tümleştirmesi ile Azure AD tümleştirme aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- MOVEit Transfer - Azure AD tümleştirme çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. MOVEit Transfer - Azure AD tümleştirme hello galerisinden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-moveit-transfer---azure-ad-integration-from-hello-gallery"></a>MOVEit Transfer - Azure AD tümleştirme hello galerisinden ekleme
tooconfigure hello tümleştirme MOVEit aktarım - Azure AD, Azure AD tümleştirmeye tooadd MOVEit Transfer - yönetilen SaaS uygulamalarının Azure AD tümleştirme hello galeri tooyour listeden gerekir.

**tooadd MOVEit Transfer - Azure AD tümleştirme hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna yazın **MOVEit Transfer - Azure AD tümleştirme**seçin **MOVEit Transfer - Azure AD tümleştirme** sonuç panelinden ardından **Ekle** düğmesini tooadd hello uygulama.

    ![MOVEit Transfer - Azure AD tümleştirme hello sonuçları listesinde](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma MOVEit Transfer - "Britta Simon" adlı bir test kullanıcı tabanlı Azure AD Tümleştirmesi ile test etme.

Çoklu oturum açma toowork, Azure AD tooknow MOVEit aktarımı hangi hello karşılık gelen kullanıcı gereken - Azure AD içinde Azure AD tümleştirme tooa kullanıcıdır. Diğer bir deyişle, bir bağlantı ilişkisi Azure AD kullanıcısının hello ilgili kullanıcı MOVEit transfer - Azure AD tümleştirme kurulan toobe gerekir.

Merhaba hello değeri MOVEit Transfer - Azure AD tümleştirme atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Azure AD çoklu oturum açmayı test MOVEit Transfer - Azure AD Tümleştirmesi ile yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[MOVEit Transfer - Azure AD tümleştirme test kullanıcısı oluşturma](#create-a-moveit-transfer---azure-ad-integration-test-user)**  kullanıcı bağlantılı toohello Azure AD gösterimidir - toohave Britta Simon MOVEit transfer, karşılık gelen - Azure AD tümleştirme.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma, MOVEit Transfer - Azure AD tümleştirme uygulaması yapılandırın.

**tooconfigure Azure AD çoklu oturum açma MOVEit Transfer - Azure AD Tümleştirmesi ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **MOVEit Transfer - Azure AD tümleştirme** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. Merhaba üzerinde **MOVEit aktarım - Azure AD tümleştirme etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://contoso.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://contoso.com/<tenatid>`

    c. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`    
     
    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler. Bu değerleri daha sonra da başvurabilir **servis sağlayıcı meta verileri URL'sini** bölüm veya kişi [MOVEit Transfer - Azure AD tümleştirme istemci destek ekibi](https://community.ipswitch.com/s/support) tooget bu değerleri.

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. Üzerinde tooyour MOVEit aktarımı Kiracı yönetici olarak oturum açın.

7. Merhaba sol gezinti bölmesinde tıklatın **ayarları**.

    ![Ayarları bölümü üzerinde uygulama yan](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. Tıklatın **tek oturum açma** altındaki bağlantı **kullanıcı kimlik doğrulama -> güvenlik ilkelerini**.

    ![Güvenlik ilkeleri üzerinde uygulama yan](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. Merhaba meta veri URL'sini bağlantı toodownload hello meta veri belgesi'ı tıklatın.

    ![Hizmet sağlayıcısı meta veri URL'si](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * Doğrulayın **Entityıd** eşleşen **tanımlayıcısı** hello içinde **MOVEit aktarım - Azure AD tümleştirme etki alanı ve URL'leri** bölümü.
    * Doğrulayın **AssertionConsumerService** konumu URL ile eşleşip **yanıt URL'si** hello içinde **MOVEit aktarım - Azure AD tümleştirme etki alanı ve URL'leri** bölümü.
    
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. Tıklatın **kimlik sağlayıcı Ekle** tooadd yeni bir Federasyon kimlik sağlayıcısı düğmesine tıklayın.

    ![Kimlik sağlayıcısı ekleyin](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. Tıklatın **Gözat...**  tooselect hello Azure Portalı'ndan indirilen meta veri dosyası ve ardından **kimlik sağlayıcı Ekle** tooupload hello indirilen dosya.

    ![SAML kimlik sağlayıcısı](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. Seçin "**Evet**" olarak **etkin** hello içinde **federe kimlik sağlayıcı ayarları Düzenle...**  sayfasında ve tıklayın **kaydetmek**.

    ![Federe kimlik sağlayıcı ayarları](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. Merhaba, **federe kimlik sağlayıcısı kullanıcı ayarlarını Düzenle** sayfasında, hello aşağıdaki eylemleri gerçekleştirin:
    
    ![Federe kimlik sağlayıcı ayarları Düzenle](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    a. Seçin **SAML NameID** olarak **oturum açma adı**.
    
    b. Seçin **diğer** olarak **tam adı** ve hello **öznitelik adı** textbox hello değeri koyun: `http://schemas.microsoft.com/identity/claims/displayname`.
    
    c. Seçin **diğer** olarak **e-posta** ve hello **öznitelik adı** textbox hello değeri koyun: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
    
    d. Seçin **Evet** olarak **oturum açma hesabı otomatik olarak oluşturma**.
    
    e. Tıklatın **kaydetmek** düğmesi.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

   ![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    a. Merhaba, **adı** kutusuna **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.

    c. Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a>MOVEit Transfer - Azure AD tümleştirme test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate Britta Simon MOVEit Transfer - Azure AD tümleştirme adlı bir kullanıcı var. MOVEit Transfer - Azure AD tümleştirme yalnızca zaman sağlama, hangi etkinleştirdiğiniz destekler. Bu bölümde, eylem öğe yok. Yeni bir kullanıcı bir girişim tooaccess MOVEit Transfer - henüz yoksa Azure AD tümleştirme sırasında oluşturulur.

>[!NOTE]
>Toocreate kullanıcı el ile gerekiyorsa, toocontact hello gereksinim [MOVEit Transfer - Azure AD tümleştirme istemci destek ekibi](https://community.ipswitch.com/s/support).

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooMOVEit Transfer - Azure AD tümleştirme vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200] 

**tooassign Britta Simon tooMOVEit Transfer - Azure AD tümleştirme hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **MOVEit Transfer - Azure AD tümleştirme**.

    ![Merhaba MOVEit Transfer - Azure AD tümleştirme bağlantı hello uygulamalar listesinde](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.

Merhaba MOVEit Transfer - Azure AD tümleştirme kutucuğuna tıkladığınızda hello erişim paneli, otomatik olarak oturum açma tooyour MOVEit Transfer - Azure AD tümleştirme uygulaması almanız gerekir. 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

