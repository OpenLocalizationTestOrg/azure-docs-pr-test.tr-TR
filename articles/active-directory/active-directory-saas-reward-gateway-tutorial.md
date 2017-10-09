---
title: "Öğretici: Azure Active Directory Tümleştirme ödül ağ geçidi ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve ödül ağ geçidi arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 34336386-998a-4d47-ab55-721d97708e5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 30cdd538471b373468c3d990e4568ddb08081a76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-reward-gateway"></a>Öğretici: Azure Active Directory Tümleştirme ödül ağ geçidi ile

Bu öğreticide, bilgi nasıl toointegrate ödül ağ geçidi Azure Active Directory'ye (Azure AD).

Ödül ağ geçidi Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooReward ağ geçidi sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooReward ağ geçidi (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure ödül ağ geçidi ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir ödül ağ geçidi çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Ödül ağ geçidi hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-reward-gateway-from-hello-gallery"></a>Ödül ağ geçidi hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme ödül ağ geçidinin tooadd hello galeri tooyour yönetilen SaaS uygulamaları listesinden ödül ağ geçidi gerekir.

**tooadd ödül ağ geçidi hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **ödül ağ geçidi**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_search.png)

5. Merhaba Sonuçlar panelinde seçin **ödül ağ geçidi**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ödül "Britta Simon" adlı bir test kullanıcı tabanlı ağ geçidi ile test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen ödül ağ geçidi olarak tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı ödül ağ geçidi hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Ödül ağ geçidi hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve ödül ağ geçidi ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Ödül ağ geçidi test kullanıcısı oluşturma](#creating-a-reward-gateway-test-user)**  -toohave Britta Simon bağlantılı toohello Azure AD kullanıcı gösterimini ödül ağ geçidi olarak, karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma ödül ağ geçidi uygulamanızı yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ödül ağ geçidi ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **ödül ağ geçidi** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_samlbase.png)

3. Merhaba üzerinde **ödül ağ geçidi etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_url.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:
    | |
    |--|
    | `https://<companyname>.rewardgateway.com` |
    | `https://<companyname>.rewardgateway.co.uk/` |
    | `https://<companyname>.rewardgateway.co.nz/` |
    | `https://<companyname>.rewardgateway.com.au/` |

    b. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:
    | |
    |--|
    |  `https://<companyname>.rewardgateway.com/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.co.uk/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.co.nz/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.com.au/Authentication/EndLogin?idp=<Unique Id>` |

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin. Kişi [ödül ağ geçidi destek ekibi](mailto:clientsupport@rewardgateway.com) tooget bu değerleri.
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_400.png)

6. tooconfigure çoklu oturum açma üzerinde **ödül ağ geçidi** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[ödül ağ geçidi destek ekibi](mailto:clientsupport@rewardgateway.com). Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-reward-gateway-test-user"></a>Ödül ağ geçidi test kullanıcısı oluşturma

Bu bölümde, Britta Simon ödül ağ geçidi olarak adlandırılan bir kullanıcı oluşturun. İş ödül ağ geçidiyle [takım Destek](mailto:clientsupport@rewardgateway.com) tooadd hello kullanıcılar hello ödül ağ geçidi Platform.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooReward ağ geçidi vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooReward ağ geçidi hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **ödül ağ geçidi**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba ödül ağ geçidi hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour ödül ağ geçidi uygulaması almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_203.png

