---
title: "Öğretici: Azure Active Directory Tümleştirme daha düz dosyalarla | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile daha düz dosyalar arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f86fe5e3-0e91-40d6-869c-3df6912d27ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 73ca2613b7bbaf9992ecf624ff5defabaa44f7a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-flatter-files"></a>Öğretici: Azure Active Directory Tümleştirme ile daha düz dosyalar

Bu öğreticide, bilgi nasıl toointegrate Azure Active Directory (Azure AD) ile daha düz dosyalar.

Azure AD ile daha düz dosyalar tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişimi olan Azure AD'de denetim tooFlatter dosyaları
- Kullanıcıların tooautomatically etkinleştirebilirsiniz açan tooFlatter dosyalarla (çoklu oturum açma) Azure AD hesaplarına Al
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure daha düz dosyalar ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir daha düz dosyalar çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden daha düz dosya ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-flatter-files-from-hello-gallery"></a>Merhaba Galerisi'nden daha düz dosya ekleme
Azure AD'ye tooconfigure hello tümleştirme daha düz dosya tooadd daha düz dosyalar hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd daha düz hello Galerisi dosyalardan hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **daha düz dosyalar**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_search.png)

5. Merhaba Sonuçlar panelinde seçin **daha düz dosyalar**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı göre daha düz dosyalar ile test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen daha düz dosyalarında tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve daha düz dosyalarında hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri daha düz dosyalarında atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve daha düz dosyalar ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Daha düz dosyalar test kullanıcısı oluşturma](#creating-a-flatter-files-test-user)**  -toohave karşılık gelen Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir daha düz dosyalarında biri.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma daha düz dosyalar uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma daha düz dosyalarla hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **daha düz dosyalar** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_samlbase.png)

3. Merhaba üzerinde **daha düz dosyalar etki alanı ve URL'leri** bölümünde, hello uygulama zaten Azure ile önceden tümleştirilmiş gibi hello kullanıcının tooperform herhangi bir adımı yok.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_url.png)
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **daha düz dosyalar yapılandırma** 'yi tıklatın **yapılandırmak daha düz dosyalar** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_configure.png) 

7. Oturum açma daha düz dosyalar uygulama yönetici olarak tooyour.

8. Tıklatın **PANO**. 
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_05.png)  

9. Tıklatın **ayarları**ve ardından hello hello üzerinde aşağıdaki adımları gerçekleştirin **şirket** sekmesi: 
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_06.png)  
    
    a. Seçin **SAML 2.0 kimlik doğrulaması için kullanmak**.
    
    b. Tıklatın **SAML yapılandırma**.

8. Merhaba üzerinde **SAML Yapılandırması** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin: 
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_08.png)  
   
    a. Merhaba, **etki alanı** metin kutusuna, kayıtlı etki alanınızı yazın.
   
    >[!NOTE]
    >Bir kayıtlı bir etki alanı henüz, kişi yoksa daha düz dosyalarınızı takım aracılığıyla destek [ support@flatterfiles.com ](mailto:support@flatterfiles.com). 
    
    b. İçinde **kimlik sağlayıcısı URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** kopyalanan Azure portalı form.
   
    c.  Base-64 kodlanmış sertifikanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve toohello yapıştırın **kimlik sağlayıcısı sertifikası** metin kutusu.

    d. Tıklatın **güncelleştirme**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-flatter-files-test-user"></a>Daha düz dosyalar test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate Britta Simon daha düz dosyalarında adlı bir kullanıcı var.

**toocreate Britta Simon daha düz dosyalarında adlı bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**

1. Tooyour üzerinde oturum **daha düz dosyalar** yönetici olarak şirket site.

2. Hello Gezinti hello sol taraftaki bölmede **ayarları**ve hello ardından **kullanıcılar** sekmesi.
   
    ![Daha düz dosyalar kullanıcı oluştur](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_09.png)

3. Tıklatın **kullanıcı ekleme**. 

4. Merhaba üzerinde **Kullanıcı Ekle** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
    ![Daha düz dosyalar kullanıcı oluştur](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_10.png)

    a. Merhaba, **ad** metin kutusuna, türü **Britta**.
   
    b. Merhaba, **Soyadı** metin kutusuna, türü **Simon**. 
   
    c. Merhaba, **e-posta adresi** metin kutusuna, hello Azure portal Britta'nın e-posta adresini yazın.
   
    d. Tıklatın **gönderme**.   


### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, Britta Simon etkinleştirme verme tarafından toouse Azure çoklu oturum açma erişim tooFlatter dosyaları.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooFlatter dosyaları hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **daha düz dosyalar**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba erişim paneli daha düz dosyalar döşeme hello tıkladığınızda, otomatik olarak imzalanmış üzerinde daha düz dosyalar uygulama tooyour almanız gerekir.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_203.png

