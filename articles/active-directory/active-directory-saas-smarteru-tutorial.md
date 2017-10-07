---
title: "Öğretici: Azure Active Directory Tümleştirme ile SmarterU | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile SmarterU arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 95fe3212-d052-4ac8-87eb-ac5305227e85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: a3b81b557c47e31f09e61bcf75dd23f370e642e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-smarteru"></a>Öğretici: Azure Active Directory Tümleştirme SmarterU ile

Bu öğreticide, bilgi nasıl toointegrate SmarterU Azure Active Directory'ye (Azure AD).

SmarterU Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooSmarterU sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooSmarterU (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure SmarterU ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir SmarterU çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden SmarterU ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-smarteru-from-hello-gallery"></a>Merhaba Galerisi'nden SmarterU ekleme
Azure AD'ye tooconfigure hello tümleştirme SmarterU, tooadd SmarterU hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd SmarterU hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **SmarterU**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_search.png)

5. Merhaba Sonuçlar panelinde seçin **SmarterU**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı SmarterU ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen SmarterU içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı SmarterU hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri SmarterU içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve SmarterU ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[SmarterU test kullanıcısı oluşturma](#creating-a-smarteru-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir SmarterU içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma SmarterU uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile SmarterU, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **SmarterU** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_samlbase.png)

3. Merhaba üzerinde **SmarterU etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin: 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_url.png)

    Merhaba, **tanımlayıcısı** metin kutusuna, türü hello URL'si:`https://www.smarteru.com/`

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smarteru-tutorial/tutorial_general_400.png)

6. Farklı web tarayıcısı penceresinde tooyour SmarterU şirket sitede yönetici olarak oturum açın.

7. Merhaba üstte Hello araç çubuğunda **hesap ayarlarını**.
   
    ![Hesap ayarları](./media/active-directory-saas-smarteru-tutorial/IC777326.png "hesap ayarları")

8. Merhaba hesap yapılandırma sayfasında hello aşağıdaki adımları gerçekleştirin:
   
    ![Dış yetkilendirme](./media/active-directory-saas-smarteru-tutorial/IC777327.png "dış yetkilendirme") 
 
      a. Seçin **etkinleştirmek dış yetkilendirme**.
  
      b. Merhaba, **ana oturum açma denetimi** bölümü, select hello **SmarterU** sekmesi.
  
      c. Merhaba, **kullanıcı varsayılan oturum açma** bölümü, select hello **SmarterU** sekmesi.
  
      d. Seçin **etkinleştirmek Okta**.
  
      e. Merhaba hello indirilen meta veri dosyasının içeriğini kopyalayın ve hello yapıştırma **Okta meta veri** metin kutusu.
  
      f. **Kaydet** düğmesine tıklayın.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smarteru-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smarteru-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smarteru-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smarteru-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-smarteru-test-user"></a>SmarterU test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toolog tooSmarterU bunların SmarterU sağlanması gerekir.

SmarterU, sağlama el ile bir görev olduğunda.

**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour oturum **SmarterU** Kiracı.

2. Çok Git**kullanıcılar**.

3. Merhaba kullanıcı bölümünde hello aşağıdaki adımları gerçekleştirin:
   
    ![Yeni kullanıcı](./media/active-directory-saas-smarteru-tutorial/IC777329.png "yeni kullanıcı")  

    a. Tıklatın **+ kullanıcı**.
    
    b. Türü hello ilişkili öznitelik değerlerini hello Azure AD kullanıcı hesabının kutularındaki aşağıdaki hello: **birincil e-posta**, **çalışan kimliği**, **parola**,  **Parolayı doğrulayın**, **verilen ad**, **Soyadı**.
    
    c. Tıklatın **etkin**. 
    
    d. **Kaydet** düğmesine tıklayın.

>[!NOTE]
>API AAD kullanıcı hesaplarının SmarterU tooprovision tarafından sağlanan veya herhangi diğer SmarterU kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooSmarterU vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooSmarterU hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **SmarterU**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.
 
Merhaba SmarterU hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour SmarterU uygulama almanız gerekir.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md). 


## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_203.png

