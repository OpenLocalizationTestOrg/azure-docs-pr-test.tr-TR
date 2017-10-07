---
title: "Öğretici: Azure Active Directory Tümleştirme ile DocuSign | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile DocuSign arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: e4ef40b8f5af20d811d8d806d2bd7e2039c55052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a>Öğretici: Azure Active Directory Tümleştirme DocuSign ile

Bu öğreticide, bilgi nasıl toointegrate DocuSign Azure Active Directory'ye (Azure AD).

DocuSign Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooDocuSign sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooDocuSign (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure DocuSign ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir DocuSign çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden DocuSign ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-docusign-from-hello-gallery"></a>Merhaba Galerisi'nden DocuSign ekleme
Azure AD'ye tooconfigure hello tümleştirme DocuSign, tooadd DocuSign hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd DocuSign hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **yeni uygulama** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **DocuSign**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. Merhaba Sonuçlar panelinde seçin **DocuSign**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı DocuSign ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen DocuSign içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı DocuSign hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** DocuSign içinde.

tooconfigure ve DocuSign ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[DocuSign test kullanıcısı oluşturma](#creating-a-docusign-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir DocuSign içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma DocuSign uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile DocuSign, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **DocuSign** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base 64)** ve sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. Merhaba üzerinde **DocuSign yapılandırma** bölüm Azure portalının tıklatın **yapılandırma DocuSign** tooopen yapılandırma oturum açma penceresi. Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. Farklı bir web tarayıcısı penceresinde, oturum açma tooyour **DocuSign Yönetici portalı** yönetici olarak.

6. Merhaba Gezinti menüsünde hello sol tıklayın **etki alanları**.
   
    ![Çoklu oturum açmayı yapılandırma][51]

7. Merhaba sağ bölmesinde tıklatın **talep etki alanı**.
   
    ![Çoklu oturum açmayı yapılandırma][52]

8. Merhaba üzerinde **bir etki alanı talep** iletişim kutusunda, hello **etki alanı adı** metin kutusuna, şirket etki alanınızı yazın ve ardından **talep**. Merhaba etki alanını doğrulayın ve hello durumu etkin olduğundan emin olun.
   
    ![Çoklu oturum açmayı yapılandırma][53]

9. Merhaba sol tarafındaki menüde tıklatın **kimlik sağlayıcıları**  
   
    ![Çoklu oturum açmayı yapılandırma][54]
10. Merhaba sağ bölmede **kimlik sağlayıcı Ekle**. 
   
    ![Çoklu oturum açmayı yapılandırma][55]

11. Merhaba üzerinde **kimlik sağlayıcı ayarları** sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açmayı yapılandırma][56]

    a. Merhaba, **adı** metin kutusuna, yapılandırmanızı için benzersiz bir ad yazın. Boşluk kullanmayın.

    b. Yapıştır **SAML varlık kimliği** hello içine **kimlik sağlayıcısı veren** metin kutusu.

    c. Yapıştır **SAML çoklu oturum açma hizmet URL'si** hello içine **kimlik sağlayıcısı oturum açma URL'si** metin kutusu.

    d. Yapıştır **Sign-Out URL** hello içine **kimlik sağlayıcısı oturum kapatma URL'si** metin kutusu.

    e. Seçin **AuthN isteği oturum**.

    f. Olarak **AuthN gönderme isteği tarafından**seçin **POST**.

    g. Olarak **gönderme oturum kapatma isteği tarafından**seçin **almak**.

12. Merhaba, **özel eşleme özniteliği** bölümünde, hello alan seçin, Azure AD talep ile toomap istediğiniz. Bu örnekte, hello **emailaddress** talep hello değeri ile eşleşen **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**. Bu hello varsayılan talep e-posta talebi için Azure AD'den adıdır. 
   
    > [!NOTE]
    > Kullanım hello uygun **kullanıcı tanımlayıcısı** toomap hello Azure AD tooDocuSign kullanıcı eşlemesi kullanıcıdan. Seçin uygun alan hello ve kuruluş ayarlarınızı temel alan hello uygun değeri girin.
          
    ![Çoklu oturum açmayı yapılandırma][57]

13. Merhaba, **kimlik sağlayıcısı sertifikası** 'yi tıklatın **sertifika Ekle**ve Azure AD Portalı'ndan indirilen hello sertifika yükleyin.   
   
    ![Çoklu oturum açmayı yapılandırma][58]

14. **Kaydet** düğmesine tıklayın.

15. Merhaba, **kimlik sağlayıcıları** 'yi tıklatın **Eylemler**ve ardından **uç noktaları**.   
   
    ![Çoklu oturum açmayı yapılandırma][59]
 
16. Merhaba, **uç noktalarını görüntüle SAML 2.0** bölümünde **DocuSign Yönetici portalı**, hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açmayı yapılandırma][60]
   
    a. Kopyalama hello **servis sağlayıcı veren URL'sini**ve hello yapıştırma **tanımlayıcısı** textbox üzerinde **DocuSign etki alanı ve URL'ler** hello Azure portal aşağıdaki hello bölümü Desen: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.
   
    b. Kopyalama hello **hizmet sağlayıcı oturum açma URL'si**ve hello yapıştırma **oturum üzerinde URL'si** textbox üzerinde **DocuSign etki alanı ve URL'leri** hello Azure portal aşağıdaki hello bölümü Desen: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    c.  Tıklatın **Kapat**
    
17. Hello Azure portal, tıklatın **kaydetmek**.
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. Merhaba iletişim Hello üstünde tıklatın **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-docusign-test-user"></a>DocuSign test kullanıcısı oluşturma

Uygulamanızın desteklediği **zaman kullanıcı hazırlama, sadece** ve kimlik doğrulama kullanıcılar hello uygulamada otomatik olarak oluşturulduktan sonra.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, kendi erişim tooDocuSign vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooDocuSign hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **DocuSign**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba DocuSign hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour DocuSign uygulama almanız gerekir.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
* [Kullanıcı sağlamayı Yapılandır](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

