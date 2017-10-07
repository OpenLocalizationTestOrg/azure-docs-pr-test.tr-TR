---
title: "Öğretici: Azure Active Directory Tümleştirme ArcGIS Online ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ArcGIS Online arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: f3dd55d798cf3256fb2758e011f33946baa405ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a>Öğretici: Azure Active Directory Tümleştirme ArcGIS Online ile

Bu öğreticide, bilgi nasıl toointegrate ArcGIS çevrimiçi Azure Active Directory'ye (Azure AD).

ArcGIS çevrimiçi Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooArcGIS çevrimiçi olan Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooArcGIS çevrimiçi (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with ArcGIS Online, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Ön koşullar

tooconfigure ArcGIS Online ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir ArcGIS çevrimiçi çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. ArcGIS çevrimiçi hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-arcgis-online-from-hello-gallery"></a>ArcGIS çevrimiçi hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme ArcGIS Online hello galeri tooyour yönetilen SaaS uygulamaları listesinden ArcGIS çevrimiçi tooadd gerekir.

**tooadd ArcGIS çevrimiçi hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **yeni uygulama** hello iletişim tooadd yeni uygulamanın hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **ArcGIS çevrimiçi**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. Merhaba Sonuçlar panelinde seçin **ArcGIS çevrimiçi**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ArcGIS "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Online ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen ArcGIS çevrimiçi tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve ArcGIS çevrimiçi hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** ArcGIS çevrimiçi.

tooconfigure ve ArcGIS Online ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on) ** -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user) ** -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[ArcGIS çevrimiçi bir test kullanıcısı oluşturma](#creating-an-arcgis-online-test-user) ** -toohave Britta Simon ArcGIS bağlantılı toohello Azure AD kullanıcı gösterimi olan Online'da, karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on) ** -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma ArcGIS çevrimiçi uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ArcGIS Online ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **ArcGIS çevrimiçi** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. Merhaba üzerinde **ArcGIS çevrimiçi etki alanı ve URL'leri** bölümünde, adım aşağıdaki hello gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, desen aşağıdaki hello kullanarak türü hello değeri:`https://<company>.maps.arcgis.com`

    > [!NOTE] 
    > Bu değer hello gerçek değil. Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si. Kişi [ArcGIS çevrimiçi istemci destek ekibi](http://support.esri.com/) tooget bu değer. 

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. Farklı web tarayıcısı penceresinde ArcGIS şirket sitenize yönetici olarak oturum açın.

7. Tıklatın **ayarları düzenleme**.

    ![Ayarları Düzenle](./media/active-directory-saas-arcgis-tutorial/ic784742.png "ayarlarını Düzenle")

8. Tıklatın **güvenlik**.

    ![Güvenlik](./media/active-directory-saas-arcgis-tutorial/ic784743.png "güvenlik")

9. Altında **Kurumsal oturum açma bilgileri**, tıklatın **AYARLANMIŞ kimlik sağlayıcı**.

    ![Kurumsal oturum açma bilgileri](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Kurumsal oturum açmalar")

10. Merhaba üzerinde **ayarlanmış kimlik sağlayıcı** yapılandırma sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Kimlik sağlayıcısı ayarlamak](./media/active-directory-saas-arcgis-tutorial/ic784745.png "ayarlamak kimlik sağlayıcısı")
   
    a. Merhaba, **adı** metin kutusuna, kuruluşunuzun adını yazın.

    b. İçin **hello Kurumsal kimlik sağlayıcısı meta verileri sağlanan kullanarak**seçin **dosya**.

    c. tooupload, indirilen meta veri dosyası tıklatın **dosya**.

    d. Tıklatın **KÜMESİ kimlik SAĞLAYICISI**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere ** Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** Britta Simon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-an-arcgis-online-test-user"></a>ArcGIS çevrimiçi bir test kullanıcısı oluşturma

İçine ArcGIS çevrimiçi sipariş tooenable Azure AD kullanıcıların toolog bunlar ArcGIS çevrimiçi sağlanmalıdır.  
ArcGIS Online Hello durumda sağlama bir el ile bir görevdir.

**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour oturum **ArcGIS** Kiracı.

2. Tıklatın **üye davet et**.
   
    ![Üye davet](./media/active-directory-saas-arcgis-tutorial/ic784747.png "üye davet")

3. Seçin **üye otomatik olarak bir e-posta göndermeden eklemek**ve ardından **sonraki**.
   
    ![Üyeler otomatik olarak Ekle](./media/active-directory-saas-arcgis-tutorial/ic784748.png "üyeleri otomatik olarak Ekle")

4. Merhaba üzerinde **üyeleri** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
     ![Ekleme ve gözden](./media/active-directory-saas-arcgis-tutorial/ic784749.png "ekleme ve gözden geçirme")
    
     a. Merhaba girin **e-posta**, **ad**, ve **Soyadı** tooprovision istediğiniz geçerli bir AAD hesabının.
  
     b. Tıklatın **ekleme ve gözden geçirme**.
5. Girdiğiniz ve ardından hello verileri gözden **ADD MEMBERS**.
   
    ![Üye Ekle](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Üye Ekle")
        
    > [!NOTE]
    > Hello Azure Active Directory hesap sahibi bir e-posta almak ve bunu etkinleştirilmeden önce bağlantı tooconfirm hesaplarında izleyin.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, çevrimiçi erişim tooArcGIS vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign çevrimiçi Britta Simon tooArcGIS hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **ArcGIS çevrimiçi**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba ArcGIS çevrimiçi hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour ArcGIS çevrimiçi uygulama almanız gerekir.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

