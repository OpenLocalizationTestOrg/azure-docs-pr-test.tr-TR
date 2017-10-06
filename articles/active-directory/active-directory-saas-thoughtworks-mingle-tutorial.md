---
title: "Öğretici: Azure Active Directory Tümleştirme Thoughtworks Mingle ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory arasındaki Thoughtworks Mingle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c17f8e13d2db3de7d228d9b27128d134f98d6cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a>Öğretici: Azure Active Directory Tümleştirme Thoughtworks Mingle ile

Bu öğreticide, bilgi toointegrate Thoughtworks Azure Active Directory (Azure AD) ile Mingle nasıl.

Azure AD ile tümleştirme Thoughtworks Mingle ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooThoughtworks Mingle sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooThoughtworks Mingle (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Thoughtworks Mingle ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Thoughtworks Mingle çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Thoughtworks Mingle hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-thoughtworks-mingle-from-hello-gallery"></a>Thoughtworks Mingle hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme Thoughtworks Mingle, tooadd Thoughtworks Mingle hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Thoughtworks Mingle hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna yazın **Thoughtworks Mingle**seçin **Thoughtworks Mingle** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Thoughtworks Mingle hello sonuçları listesinde](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Thoughtworks Mingle ile test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen Thoughtworks Mingle içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı Thoughtworks Mingle arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Thoughtworks Mingle içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Thoughtworks Mingle ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Thoughtworks Mingle test kullanıcısı oluşturma](#create-a-thoughtworks-mingle-test-user)**  -toohave Britta Simon Thoughtworks bağlantılı toohello Azure AD kullanıcı gösterimi olan Mingle içinde karşılık gelen.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Thoughtworks Mingle uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma Thoughtworks Mingle ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Thoughtworks Mingle** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. Merhaba üzerinde **Thoughtworks Mingle etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Thoughtworks Mingle etki alanı ve URL'leri tek oturum açma bilgilerini](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.mingle.thoughtworks.com`

    > [!NOTE] 
    > Merhaba değeri gerçek değil. Güncelleştirme hello değerle hello gerçek oturum açma URL'si. Kişi [Thoughtworks Mingle istemci destek ekibi](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) tooget hello değeri. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. İçinde tooyour oturum **Thoughtworks Mingle** yönetici olarak şirket site.

7. Merhaba tıklatın **yönetici** sekmesini ve ardından **SSO Config**.
   
    ![Yönetici sekmesine](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO yapılandırma")

8. Merhaba, **SSO Config** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![SSO Config](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO yapılandırma")
    
    a. tooupload hello meta veri dosyası, tıklatın **dosya**. 

    b. Tıklatın **değişiklikleri kaydetmek**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Merhaba Ekle düğmesi](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-a-thoughtworks-mingle-test-user"></a>Thoughtworks Mingle test kullanıcısı oluşturma

Sağlanan toohello Thoughtworks Mingle uygulama Azure Active Directory kullanıcı adlarını kullanarak Azure AD kullanıcıların toobe mümkün toosign için olmaları gerekir. Thoughtworks Mingle, Hello durumda sağlama bir el ile bir görevdir.

**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour Thoughtworks Mingle şirket site yönetici olarak oturum açın.

2. tıklatın **profil**.
   
    ![İlk projenizi](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "ilk projenizi")

3. Merhaba tıklatın **yönetici** sekmesini ve ardından **kullanıcılar**.
   
    ![Kullanıcıların](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "kullanıcılar")

4. Tıklatın **yeni kullanıcı**.
   
    ![Yeni kullanıcı](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "yeni kullanıcı")

5. Merhaba üzerinde **yeni kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Yeni kullanıcı iletişim kutusu](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "yeni kullanıcı")  
 
    a. Türü hello **oturum açma adı**, **görünen adı**, **Seç parola**, **parolayı onayla** geçerli bir Azure AD hesabının tooprovision metin kutuları Hello ilgili. 

    b. Olarak **kullanıcı türü**seçin **tam kullanıcı**.

    c. Tıklatın **bu profili oluşturma**.

>[!NOTE]
>API AAD kullanıcı hesaplarının Thoughtworks Mingle tooprovision tarafından sağlanan veya herhangi diğer Thoughtworks Mingle kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.
> 

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooThoughtworks Mingle vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200] 

**tooassign Britta Simon tooThoughtworks Mingle, hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Thoughtworks Mingle**.

    ![Merhaba Thoughtworks Mingle bağlantıyı hello uygulamalar listesi](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.

Merhaba Thoughtworks Mingle parçasında hello erişim paneli tıkladığınızda, otomatik olarak oturum açma tooyour Thoughtworks Mingle uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png

