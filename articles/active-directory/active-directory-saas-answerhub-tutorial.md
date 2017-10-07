---
title: "Öğretici: Azure Active Directory Tümleştirme ile AnswerHub | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile AnswerHub arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 818b91d7-01df-4b36-9706-f167c710a73c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 90b530da31abe7e6f18bfa2c5409f8ff1d4f1063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-answerhub"></a>Öğretici: Azure Active Directory Tümleştirme AnswerHub ile

Bu öğreticide, bilgi nasıl toointegrate AnswerHub Azure Active Directory'ye (Azure AD).

AnswerHub Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooAnswerHub sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooAnswerHub (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure AnswerHub ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir AnswerHub çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden AnswerHub ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-answerhub-from-hello-gallery"></a>Merhaba Galerisi'nden AnswerHub ekleme
Azure AD'ye tooconfigure hello tümleştirme AnswerHub, tooadd AnswerHub hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd AnswerHub hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **AnswerHub**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_search.png)

5. Merhaba Sonuçlar panelinde seçin **AnswerHub**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı AnswerHub sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen AnswerHub içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı AnswerHub hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri AnswerHub içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve AnswerHub ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Bir AnswerHub test kullanıcısı oluşturma](#creating-an-answerhub-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir AnswerHub içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma AnswerHub uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile AnswerHub, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **AnswerHub** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_samlbase.png)

3. Merhaba üzerinde **AnswerHub etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company>.answerhub.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company>.answerhub.com`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [AnswerHub istemci destek ekibi](mailto:success@answerhub.com) tooget bu değerleri. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-answerhub-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **AnswerHub yapılandırma** 'yi tıklatın **yapılandırma AnswerHub** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_configure.png) 

7. Farklı web tarayıcısı penceresinde AnswerHub şirket sitenize yönetici olarak oturum açın.
   
    >[!NOTE]
    >AnswerHub yapılandırmada yardıma gereksinim duyarsanız başvurun [AnswerHub'in destek ekibi](mailto:success@answerhub.com.).
   
8. Çok Git**Yönetim**.

9. Merhaba tıklatın **kullanıcı ve grup** sekmesi.

10. Merhaba Gezinti bölmesindeki hello tarafı, sol hello **sosyal ayarları** 'yi tıklatın **SAML Kurulumu**.

11. Tıklatın **IDP Config** sekmesi.

12. Merhaba üzerinde **IDP Config** sekmesinde, hello aşağıdaki adımları gerçekleştirin:

     ![SAML Kurulumu](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Kurulumu")  
  
     a. İçinde **IDP oturum açma URL'si** metin kutusuna, Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.
  
     b. İçinde **IDP oturum kapatma URL'si** metin kutusuna, Yapıştır **Sign-Out URL** Azure portalından kopyaladığınız değeri.
     
     c. İçinde **IDP ad tanımlayıcısı biçimi** metin kutusuna, hello kullanıcı tanımlayıcısı olarak seçili Azure Portalı'nda aynı değeri girin **kullanıcı öznitelikleri** bölümü.
  
     d. Tıklatın **anahtarlar ve Sertifikalar**.

13. Merhaba anahtarlar ve sertifikalar sekmesinde hello aşağıdaki adımları gerçekleştirin:
    
     ![Anahtarlar ve Sertifikalar](./media/active-directory-saas-answerhub-tutorial/ic785173.png "anahtarlar ve sertifikalar")  
 
     a. Not Defteri'nde, kopyalama hello panonuza bunu içerik Azure Portalı'ndan indirilen, base-64 kodlanmış sertifika açın ve ardından toohello yapıştırın **IDP ortak anahtarı (x 509 biçimi)** metin kutusu.
  
     b. **Kaydet** düğmesine tıklayın.

14. Merhaba üzerinde **IDP Config** sekmesini tıklatın, **kaydetmek**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-answerhub-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-answerhub-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-answerhub-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-answerhub-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-an-answerhub-test-user"></a>Bir AnswerHub test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toolog tooAnswerHub bunların AnswerHub sağlanması gerekir.  
AnswerHub Hello durumda sağlama bir el ile bir görevdir.

**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour oturum **AnswerHub** yönetici olarak şirket site.

2. Çok Git**Yönetim**.

3. Merhaba tıklatın **kullanıcıları ve grupları** sekmesi.

4. Merhaba Gezinti bölmesindeki hello tarafı, sol hello **kullanıcıları yönetme** 'yi tıklatın **oluşturma veya içeri aktarma kullanıcı**.
   
   ![Kullanıcıları ve grupları](./media/active-directory-saas-answerhub-tutorial/ic785175.png "kullanıcıları ve grupları")

5. Türü hello **e-posta adresi**, **kullanıcıadı** ve **parola** geçerli bir Azure hello tooprovision istediğiniz Active Directory hesabı ilgili metin kutularına ve 'ıtıklatın **Kaydet**.

>[!NOTE]
>API AAD kullanıcı hesaplarının AnswerHub tooprovision tarafından sağlanan veya herhangi diğer AnswerHub kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooAnswerHub vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooAnswerHub hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **AnswerHub**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba AnswerHub hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour AnswerHub uygulama almanız gerekir.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_203.png

