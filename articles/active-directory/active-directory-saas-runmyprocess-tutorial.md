---
title: "Öğretici: Azure Active Directory Tümleştirme ile RunMyProcess | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile RunMyProcess arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f02acda015aeb8d131d8e3ef88bf50c4e8e94750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a>Öğretici: Azure Active Directory Tümleştirme RunMyProcess ile

Bu öğreticide, bilgi nasıl toointegrate RunMyProcess Azure Active Directory'ye (Azure AD).

RunMyProcess Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooRunMyProcess sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooRunMyProcess (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure RunMyProcess ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir RunMyProcess çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz:[deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden RunMyProcess ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-runmyprocess-from-hello-gallery"></a>Merhaba Galerisi'nden RunMyProcess ekleme
Azure AD'ye tooconfigure hello tümleştirme RunMyProcess, tooadd RunMyProcess hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd RunMyProcess hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **RunMyProcess**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_search.png)

5. Merhaba Sonuçlar panelinde seçin **RunMyProcess**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı RunMyProcess sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen RunMyProcess içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı RunMyProcess hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri RunMyProcess içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve RunMyProcess ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[RunMyProcess test kullanıcısı oluşturma](#creating-a-runmyprocess-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir RunMyProcess içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma RunMyProcess uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile RunMyProcess, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **RunMyProcess** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_samlbase.png)

3. Merhaba üzerinde **RunMyProcess etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_url.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://live.runmyprocess.com/live/<tenant id>`

    > [!NOTE] 
    > Merhaba değeri gerçek değil. Güncelleştirme hello değerle hello gerçek oturum açma URL'si. Kişi [RunMyProcess istemci destek ekibi](mailto:support@runmyprocess.com) tooget hello değeri. 

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **RunMyProcess yapılandırma** 'yi tıklatın **yapılandırma RunMyProcess** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_configure.png) 

7. Bir farklı web tarayıcısı penceresinde, bir yönetici olarak oturum açma tooyour RunMyProcess Kiracı.

8. Sol gezinti panelinde tıklatın **hesap** seçip **yapılandırma**.
   
    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_001.png)

9. Çok Git**kimlik doğrulama yöntemini** bölümünde ve aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_002.png)

    a. Olarak **yöntemi**seçin **Samlv2 SSO'su**. 

    b. Merhaba, **SSO yeniden yönlendirme** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.

    c. Merhaba, **oturumu kapatıp yeniden yönlendirme** metin kutusuna, Yapıştır hello değerini **Sign-Out URL**, Azure portalından kopyalanan.

    d. Merhaba, **ad kimliği biçimi** metin kutusuna, tür hello değeri **ad tanımlayıcısı biçimi** olarak **urn: OASIS: adları: tc: SAML:1.1:nameid-biçimi: emailAddress**.

    e. Merhaba hello indirilen sertifika dosyasının içeriğini kopyalayın ve hello yapıştırma **sertifika** metin kutusu. 
 
    f. Tıklatın **kaydetmek** simgesi.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-runmyprocess-test-user"></a>RunMyProcess test kullanıcısı oluşturma

TooRunMyProcess içinde sipariş tooenable Azure AD kullanıcıların toolog bunların RunMyProcess sağlanmalıdır. RunMyProcess Hello durumda sağlama bir el ile bir görevdir.

**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour RunMyProcess şirket site yönetici olarak oturum açın.

2. Tıklatın **hesap** seçip **kullanıcılar** sol gezinti panelinde, ardından **yeni kullanıcı**.
   
    ![Yeni kullanıcı](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "yeni kullanıcı")

3. Merhaba, **kullanıcı ayarları** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![Profil](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "profili") 
  
    a. Türü hello **adı** ve **e-posta** geçerli bir Azure hello tooprovision istediğiniz AD hesabının ilgili metin kutuları. 

    b. Seçin bir **IDE dil**, **dil**, ve **profil**. 

    c. Seçin **Gönder hesap oluşturma e-posta toome**. 

    d. **Kaydet** düğmesine tıklayın.
   
    >[!NOTE]
    >API, kullanıcı hesaplarını RunMyProcess tooprovision Azure Active Directory tarafından sağlanan veya herhangi diğer RunMyProcess kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz. 
    > 

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooRunMyProcess vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooRunMyProcess hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **RunMyProcess**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.

Hello erişim paneli RunMyProcess döşeme hello tıkladığınızda, otomatik olarak oturum açma RunMyProcess uygulama tooyour almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_203.png

