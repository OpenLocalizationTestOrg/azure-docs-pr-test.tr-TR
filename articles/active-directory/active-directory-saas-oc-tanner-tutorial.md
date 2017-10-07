---
title: "Öğretici: Azure Active Directory Tümleştirme O.C. ile Etikan - AppreciateHub | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile O.C. arasında Etikan - AppreciateHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: 45052cf56e35746d7df5910162e40e3bbcad1aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oc-tanner---appreciatehub"></a>Öğretici: Azure Active Directory Tümleştirme O.C. ile Etikan - AppreciateHub

Bu öğreticide, bilgi nasıl toointegrate O.C. Etikan - AppreciateHub Azure ile Active Directory (Azure AD).

O.C. tümleştirme Etikan - Azure AD ile AppreciateHub ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooO.C sahip Azure AD'de kontrol edebilirsiniz. Etikan - AppreciateHub
- Oturum açma, kullanıcıların tooautomatically get tooO.C etkinleştirebilirsiniz. Etikan - Azure AD hesaplarına sahip AppreciateHub (çoklu oturum açma)
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure O.C. ile Azure AD tümleştirme Etikan - AppreciateHub, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- BİR O.C. Etikan - abonelik etkin AppreciateHub çoklu oturum açma

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. O.C. ekleme Etikan - AppreciateHub hello Galeriden
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-oc-tanner---appreciatehub-from-hello-gallery"></a>O.C. ekleme Etikan - AppreciateHub hello Galeriden
tooconfigure hello O.C. tümleştirilmesi Etikan - Azure AD'ye AppreciateHub tooadd O.C. gerekir Etikan - AppreciateHub hello galeri tooyour listesinden yönetilen SaaS uygulamaları.

**tooadd O.C. Etikan - AppreciateHub hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **O.C. Etikan - AppreciateHub**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_search.png)

5. Merhaba Sonuçlar panelinde seçin **O.C. Etikan - AppreciateHub**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma O.C. ile test etme Etikan - AppreciateHub "Britta Simon" adlı bir test kullanıcı tabanlı.

Tek toowork'ın oturum açma Azure AD tooknow O.C. hangi hello karşılık gelen kullanıcı gerekiyor Etikan - AppreciateHub tooa Azure AD'de kullanıcıdır. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı O.C. hello arasında bir bağlantı ilişkisi Etikan - AppreciateHub kurulan toobe gerekir.

İçinde O.C. Etikan - AppreciateHub, Ata hello hello değerini **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Azure AD çoklu oturum açma O.C. ile test Etikan - AppreciateHub, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Bir O.C. oluşturma Etikan - AppreciateHub test kullanıcısı](#creating-a-oc-tanner---appreciatehub-test-user)**  -toohave Britta Simon O.C. içinde karşılık gelen Etikan - bağlantılı toohello Azure AD kullanıcı gösterimi olan AppreciateHub.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirme ve çoklu oturum açma, O.C. yapılandırma Etikan - AppreciateHub uygulama.

**tooconfigure Azure AD çoklu oturum açma O.C. ile Etikan - AppreciateHub, hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **O.C. Etikan - AppreciateHub** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_samlbase.png)

3. Merhaba üzerinde **O.C. Etikan - AppreciateHub etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_url.png)

    a. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`

    > [!NOTE] 
    > Bu değer gerçek değil. Bu değer hello gerçek yanıt URL'si ile güncelleştirin. Kişi [O.C. Etikan - AppreciateHub destek ekibi](mailto:sso@octanner.com) tooget bu değer.

    b. Bağlantı aşağıdaki hello kullanarak açık hello meta veri dosyası: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).
   
    c. Merhaba bulun **md:AssertionConsumerService** düğümü. 
   
    d. Merhaba Hello değerini kopyalayın **konumu** özniteliği. 
   
    ![Uygulama ayarlarını yapılandırın][12]
   
    e. Merhaba, **oturum üzerinde URL'si** hello önceki adımda elde hello değerini aşan bir metin kutusu.

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_400.png)

6. tooconfigure çoklu oturum açma üzerinde **O.C. Etikan - AppreciateHub** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[O.C. Etikan - AppreciateHub destek ekibi](mailto:sso@octanner.com).

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a>Bir O.C. oluşturma Etikan - AppreciateHub test kullanıcısı

Hello amacı, bu bölümde toocreate içinde O.C. Britta Simon adlı bir kullanıcı değil Etikan - AppreciateHub.

**toocreate bir kullanıcı Britta Simon O.C. denir. Etikan - AppreciateHub, hello aşağıdaki adımları gerçekleştirin:**

Sorun, [O.C. Etikan - AppreciateHub destek ekibi](mailto:sso@octanner.com) toocreate nameID özniteliği hello Azure AD'de aynı değeri Britta Simon hello kullanıcı adı olarak sahip bir kullanıcı.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooO.C vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin. Etikan - AppreciateHub.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooO.C. Etikan - AppreciateHub, hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **O.C. Etikan - AppreciateHub**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.  
Merhaba O.C. tıkladığınızda Etikan - AppreciateHub parçasında Merhaba erişim paneli, otomatik olarak oturum açma O.C. tooyour almanız gerekir Etikan - AppreciateHub uygulama.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png

[100]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png

