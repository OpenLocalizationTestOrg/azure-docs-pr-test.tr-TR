---
title: "Öğretici: Azure Active Directory Tümleştirme Jitbit Yardım Masası ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Jitbit Yardım Masası arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f6c837bbb910c1e84f7ed9da676c5ab40f75338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a>Öğretici: Azure Active Directory Tümleştirme Jitbit Yardım Masası ile

Bu öğreticide, bilgi nasıl toointegrate Jitbit Yardım Masası Azure Active Directory'ye (Azure AD).

Jitbit Yardım Masası Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooJitbit Yardım Masası sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooJitbit Yardım Masası (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Jitbit Yardım Masası ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Jitbit Yardım Masası çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Jitbit Yardım Masası ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-jitbit-helpdesk-from-hello-gallery"></a>Merhaba Galerisi'nden Jitbit Yardım Masası ekleme
Azure AD'ye tooconfigure hello tümleştirme Jitbit Yardım Masası, tooadd Jitbit Yardım Masası hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Jitbit Yardım Masası hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Jitbit Yardım Masası**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. Merhaba Sonuçlar panelinde seçin **Jitbit Yardım Masası**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırmanız ve Jitbit Yardım Masası ile Azure AD çoklu oturum açmayı test "Britta Simon" adlı bir test kullanıcı tabanlı.

Tek toowork'ın oturum açma hangi hello karşılık gelen Jitbit Yardım Masası içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Jitbit Yardım Masası hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Jitbit Yardım Masası içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Jitbit Yardım Masası ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Jitbit Yardım Masası test kullanıcısı oluşturma](#creating-a-jitbit-helpdesk-test-user)**  -toohave Britta Simon bağlantılı toohello Azure AD kullanıcı gösterimini Jitbit Yardım Masası'nda, karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Jitbit Yardım Masası uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma Jitbit Yardım Masası ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Jitbit Yardım Masası** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. Merhaba üzerinde **Jitbit Yardım Masası etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın: 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > Bu değer gerçek değil. Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si. Kişi [Jitbit Yardım Masası istemci destek ekibi](https://www.jitbit.com/support/) tooget bu değer. 
    
    b.  Merhaba, **tanımlayıcısı** metin kutusuna, şu URL'yi yazın:`https://www.jitbit.com/web-helpdesk/`

    
 


4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Jitbit Yardım Masası yapılandırma** 'yi tıklatın **yapılandırma Jitbit Yardım Masası** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. Farklı web tarayıcısı penceresinde Jitbit Yardım Masası şirket sitenize yönetici olarak oturum açın.

8. Merhaba üstte Hello araç çubuğunda **Yönetim**.
   
    ![Yönetim](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Yönetim")

9. Tıklatın **genel ayarları**.
   
    ![Kullanıcılar, şirketler ve izinleri](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "kullanıcıları, şirketler ve izinleri")

10. Merhaba, **kimlik doğrulama ayarlarını** yapılandırma bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![Kimlik doğrulama ayarlarını](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "kimlik doğrulama ayarları")
    
    a. Seçin **SAML 2.0 tek etkinleştirmek oturum**, çoklu oturum açma (SSO), ile kullanarak toosign **OneLogin**.

    b. Merhaba, **uç nokta URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.

    c. Açık, **base-64** kodlanmış sertifika Not Defteri'nde, kopyalama hello panonuza bunu içerik ve toohello yapıştırın **X.509 sertifikası** metin kutusu

    d. Tıklatın **değişiklikleri kaydetmek**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, tür adı olarak **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a>Jitbit Yardım Masası test kullanıcısı oluşturma

Jitbit Yardım Masası uygulamasına sipariş tooenable Azure AD kullanıcıların toolog bunlar Jitbit Yardım Masası sağlanmalıdır.  Jitbit Yardım Masası Hello durumda sağlama bir el ile bir görevdir.

**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour oturum **Jitbit Yardım Masası** Kiracı.

2. Hello içinde hello üst menüsünde **Yönetim**.
   
    ![Yönetim](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Yönetim")

3. Tıklatın **kullanıcıları, şirketler ve izinleri**.
   
    ![Kullanıcılar, şirketler ve izinleri](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "kullanıcıları, şirketler ve izinleri")

4. Tıklatın **Kullanıcı Ekle**.
   
    ![Kullanıcı Ekle](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Kullanıcı Ekle")
   
5. Hello Oluştur bölümünde, tooprovision gibi istediğiniz hello Azure AD hesabının hello veri türü:

    ![Oluşturma](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "oluşturma")
   
   a. Merhaba, **kullanıcıadı** metin kutusuna, türü **BrittaSimon**, hello Azure portal olduğu gibi hello kullanıcı adı.

   b. Merhaba, **e-posta** hello kullanıcının e-posta metin kutusuna, ister  **BrittaSimon@contoso.com** .

   c. Merhaba, **ad** metin kutusuna, tür ilk gibi hello kullanıcı adını **Britta**.

   d. Merhaba, **Soyadı** metin kutusuna, türü hello kullanıcının soyadını gibi **Simon**.
   
   e. **Oluştur**'a tıklayın.

>[!NOTE]
>API'leri, Azure AD kullanıcı hesapları Jitbit Yardım Masası tooprovision tarafından sağlanan veya herhangi diğer Jitbit Yardım Masası kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.
> 
        

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooJitbit Yardım Masası vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooJitbit Yardım Masası, hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Jitbit Yardım Masası**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Jitbit Yardım Masası döşeme hello erişim paneli hello tıkladığınızda, oturum açma sayfasına Jitbit Yardım Masası uygulamasının almanız gerekir.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png

