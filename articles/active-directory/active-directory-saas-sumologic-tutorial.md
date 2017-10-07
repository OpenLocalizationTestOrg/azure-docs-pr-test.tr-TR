---
title: "Öğretici: Azure Active Directory Tümleştirme ile SumoLogic | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile SumoLogic arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 2ef1bd329f5db8899f0b57744e4c0f6eed1c532f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a>Öğretici: Azure Active Directory Tümleştirme SumoLogic ile

Bu öğreticide, bilgi nasıl toointegrate SumoLogic Azure Active Directory'ye (Azure AD).

SumoLogic Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooSumoLogic sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooSumoLogic (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure SumoLogic ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir SumoLogic çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden SumoLogic ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-sumologic-from-hello-gallery"></a>Merhaba Galerisi'nden SumoLogic ekleme
Azure AD'ye tooconfigure hello tümleştirme SumoLogic, tooadd SumoLogic hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd SumoLogic hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **SumoLogic**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_search.png)

5. Merhaba Sonuçlar panelinde seçin **SumoLogic**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı SumoLogic sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen SumoLogic içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı SumoLogic hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri SumoLogic içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve SumoLogic ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[SumoLogic test kullanıcısı oluşturma](#creating-a-sumologic-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir SumoLogic içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma SumoLogic uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile SumoLogic, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **SumoLogic** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_samlbase.png)

3. Merhaba üzerinde **SumoLogic etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenantname>.SumoLogic.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [SumoLogic istemci destek ekibi](https://www.sumologic.com/contact-us/) tooget bu değerleri. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sumologic-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **SumoLogic yapılandırma** 'yi tıklatın **yapılandırma SumoLogic** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_configure.png) 

7. Farklı web tarayıcısı penceresinde tooyour SumoLogic şirket sitede yönetici olarak oturum açın.

8. Çok Git**Yönet \> güvenlik**.
   
    ![Yönetme](./media/active-directory-saas-sumologic-tutorial/ic778556.png "yönetme")

9. Tıklatın **SAML**.
   
    ![Genel güvenlik ayarları](./media/active-directory-saas-sumologic-tutorial/ic778557.png "genel güvenlik ayarları")

10. Merhaba gelen **bir yapılandırma seçin veya yeni bir tane oluşturun** listesinde, seçin **Azure AD**ve ardından **yapılandırma**.
   
    ![SAML 2.0 yapılandırma](./media/active-directory-saas-sumologic-tutorial/ic778558.png "SAML 2.0 yapılandırma")

11. Merhaba üzerinde **yapılandırma SAML 2.0** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
    ![SAML 2.0 yapılandırma](./media/active-directory-saas-sumologic-tutorial/ic778559.png "SAML 2.0 yapılandırma")
   
    a. Merhaba, **yapılandırma adı** metin kutusuna, türü **Azure AD**. 

    b. Seçin **hata ayıklama modu**.

    c. Merhaba, **veren** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği**, Azure portalından kopyalanan. 

    d. Merhaba, **Authn istek URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.

    e. Base-64 kodlanmış sertifikanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve ardından yapıştırın içine tüm sertifika hello **X.509 sertifikası** metin kutusu.

    f. Olarak **e-posta özniteliği**seçin **kullanım SAML konu**.  

    g. Seçin **SP tarafından başlatılan oturum açma yapılandırması**.

    h. Merhaba, **oturum açma yolunu** metin kutusuna, türü **Azure** tıklatıp **kaydetmek**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sumologic-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sumologic-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sumologic-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sumologic-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-sumologic-test-user"></a>SumoLogic test kullanıcısı oluşturma

Sağlanan tooSumoLogic tooSumoLogic içinde sipariş tooenable Azure AD kullanıcıların toolog içinde olmaları gerekir.  

* SumoLogic Hello durumda sağlama bir el ile bir görevdir.

**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour oturum **SumoLogic** Kiracı.

2. Çok Git**Yönet \> kullanıcılar**.
   
    ![Kullanıcıların](./media/active-directory-saas-sumologic-tutorial/ic778561.png "kullanıcılar")

3. **Ekle**'ye tıklayın.
   
    ![Kullanıcıların](./media/active-directory-saas-sumologic-tutorial/ic778562.png "kullanıcılar")

4. Merhaba üzerinde **yeni kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
    ![Yeni kullanıcı](./media/active-directory-saas-sumologic-tutorial/ic778563.png "yeni kullanıcı") 
 
    a. Türü hello ilgili bilgileri hello tooprovision istediğiniz hello Azure AD hesabının **ad**, **Soyadı**, ve **e-posta** metin kutuları.
  
    b. Bir rol seçin.
  
    c. Olarak **durum**seçin **etkin**.
  
    d. **Kaydet** düğmesine tıklayın.

>[!NOTE]
>API AAD kullanıcı hesaplarının SumoLogic tooprovision tarafından sağlanan veya herhangi diğer SumoLogic kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz. 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooSumoLogic vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooSumoLogic hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **SumoLogic**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.

Merhaba SumoLogic hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour SumoLogic uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_203.png

