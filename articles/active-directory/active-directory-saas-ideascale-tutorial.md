---
title: "Öğretici: Azure Active Directory Tümleştirme ile IdeaScale | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile IdeaScale arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 10722b137e7565ee165e73994fd5a60b994719bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a>Öğretici: Azure Active Directory Tümleştirme IdeaScale ile

Bu öğreticide, bilgi nasıl toointegrate IdeaScale Azure Active Directory'ye (Azure AD).

IdeaScale Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooIdeaScale sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooIdeaScale (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure IdeaScale ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir IdeaScale çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden IdeaScale ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-ideascale-from-hello-gallery"></a>Merhaba Galerisi'nden IdeaScale ekleme
Azure AD'ye tooconfigure hello tümleştirme IdeaScale, tooadd IdeaScale hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd IdeaScale hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **IdeaScale**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. Merhaba Sonuçlar panelinde seçin **IdeaScale**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı IdeaScale ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen IdeaScale içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı IdeaScale hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri IdeaScale içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve IdeaScale ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Bir IdeaScale test kullanıcısı oluşturma](#creating-an-ideascale-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir IdeaScale içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma IdeaScale uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile IdeaScale, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **IdeaScale** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. Merhaba üzerinde **IdeaScale etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.ideascale.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [IdeaScale istemci destek ekibi](http://support.ideascale.com/) tooget bu değerleri. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **IdeaScale yapılandırma** 'yi tıklatın **yapılandırma IdeaScale** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL ve SAML varlık kimliği** hello gelen **hızlı başvuru bölümünde**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. Farklı web tarayıcısı penceresinde tooyour IdeaScale şirket sitede yönetici olarak oturum açın.

8. Çok Git**topluluk ayarları**.
   
    ![Topluluk ayarları](./media/active-directory-saas-ideascale-tutorial/ic790847.png "topluluk ayarları")

9. Çok Git**güvenlik \> çoklu oturum açma ayarları**.
   
    ![Çoklu oturum açma ayarları](./media/active-directory-saas-ideascale-tutorial/ic790848.png "tek oturum açma ayarları")

10. Olarak **çoklu oturum açma türü**seçin **SAML 2.0**.
   
    ![Oturum açma türü tek](./media/active-directory-saas-ideascale-tutorial/ic790849.png "tek oturum açma türü")

11. Merhaba üzerinde **çoklu oturum açma ayarları** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açma ayarları](./media/active-directory-saas-ideascale-tutorial/ic790850.png "tek oturum açma ayarları")
   
    a. İçinde **SAML IDP varlık kimliği** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.

    b. Azure Portalı'ndan indirilen meta veri dosyasının Hello içeriği Kopyala ve hello yapıştırma **SAML IDP meta veri** metin kutusu.

    c. İçinde **oturum kapatma başarı URL** metin kutusuna, Yapıştır hello değerini **Sign-Out URL** Azure portalından kopyalanan.

    d. Tıklatın **değişiklikleri kaydetmek**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-an-ideascale-test-user"></a>Bir IdeaScale test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toolog IdeaScale bunlar içinde tooIdeaScale sağlanması gerekir. IdeaScale Hello durumda sağlama bir el ile bir görevdir.

**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour oturum **IdeaScale** yönetici olarak şirket site.

2. Çok Git**topluluk ayarları**.
   
    ![Topluluk ayarları](./media/active-directory-saas-ideascale-tutorial/ic790847.png "topluluk ayarları")

3. Çok Git**temel ayarları \> üye yönetim**.

4. Tıklatın **üye ekleme**.
   
    ![Üye yönetim](./media/active-directory-saas-ideascale-tutorial/ic790852.png "üye Yönetimi")

5. Hello yeni üye ekle bölümü, hello aşağıdaki adımları gerçekleştirin:
   
    ![Yeni üye eklemek](./media/active-directory-saas-ideascale-tutorial/ic790853.png "yeni üye ekleme")
   
    a. Merhaba, **e-posta adresleri** metin kutusuna, tooprovision istediğiniz geçerli bir AAD hesabının hello e-posta adresini yazın.
   
    b. Tıklatın **değişiklikleri kaydetmek**. 
   
    >[!NOTE]
    >etkin duruma gelmesi hello Azure Active Directory hesap sahibi bağlantı tooconfirm hello hesabı olan bir e-posta alır.
      
>[!NOTE]
>API AAD kullanıcı hesaplarının IdeaScale tooprovision tarafından sağlanan veya herhangi diğer IdeaScale kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.
 

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooIdeaScale vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooIdeaScale hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **IdeaScale**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme


Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.

Merhaba IdeaScale hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour IdeaScale uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

