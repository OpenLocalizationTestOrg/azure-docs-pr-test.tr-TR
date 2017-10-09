---
title: "Öğretici: Salesforce korumalı alan Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Salesforce korumalı alan arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7539f08356568a17ebfcee2764bbbefa129b0553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a>Öğretici: Azure Active Directory Tümleştirme ile Salesforce korumalı alan

Bu öğreticide, bilgi nasıl toointegrate Salesforce korumalı alan Azure Active Directory'ye (Azure AD).

Salesforce korumalı alan Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Korumalı alan erişimi tooSalesforce sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooSalesforce Sandbox (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

Salesforce korumalı alan ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Salesforce korumalı alan çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Salesforce korumalı alan hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-salesforce-sandbox-from-hello-gallery"></a>Salesforce korumalı alan hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme Salesforce korumalı alan, hello galeri tooyour yönetilen SaaS uygulamaları listesinden tooadd Salesforce korumalı alan gerekir.

**Salesforce korumalı alan hello galerisinden tooadd hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **yeni uygulama** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Salesforce korumalı alan**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. Merhaba Sonuçlar panelinde seçin **Salesforce korumalı alan**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırmanız ve Salesforce korumalı alan Azure AD çoklu oturum açma testiyle "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı

Tek toowork'ın oturum açma hangi hello karşılık gelen Salesforce korumalı alanı içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Salesforce korumalı alan hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Salesforce korumalı alanı içinde.

tooconfigure ve Salesforce korumalı alan ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Salesforce korumalı alan test kullanıcısı oluşturma](#creating-a-salesforce-sandbox-test-user)**  -toohave Britta Simon bağlantılı toohello Azure AD kullanıcı gösterimini Salesforce korumalı alanı içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Salesforce korumalı alan uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma Salesforce korumalı alan ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Salesforce korumalı alan** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. Merhaba üzerinde **Salesforce korumalı alan etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     Merhaba, **oturum açma URL'si** metin kutusuna, desen aşağıdaki hello kullanarak türü hello değeri:`https://<subdomain>.my.salesforce.com`

    > [!NOTE] 
    > Bu değer hello gerçek değil. Bu değer hello gerçek oturum açma URL'si ile güncelleştirin. Kişi [Salesforce korumalı alan istemci destek ekibi](https://help.salesforce.com/support) tooget bu değer.


4. Zaten başka bir Salesforce korumalı alan örneği için çoklu oturum açmayı dizininizde yapılandırdıktan sonra hello yapılandırmanız da gerekir **tanımlayıcısı** toohave hello hello aynı değere **URL üzerinde oturum**. 
    
    >[!Note]
    >Merhaba **tanımlayıcısı** alan hello denetleyerek bulunabilir **Göster Gelişmiş ayarları** hello onay kutusuna **uygulama URL'sini yapılandırın** hello iletişim sayfası 


5. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. Merhaba üzerinde **Salesforce korumalı alan yapılandırma** 'yi tıklatın **yapılandırma Salesforce korumalı alan** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS>
8. Tarayıcınızda yeni bir sekme açın ve oturum tooyour Salesforce korumalı alan yönetici hesabı.

9. Hello içinde hello üst menüsünde **Kurulum**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. Merhaba Gezinti hello sol taraftaki bölmede **güvenlik denetimleri**ve ardından **çoklu oturum açma ayarları**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. Hello çoklu oturum açma ayarları bölümü, hello aşağıdaki adımları gerçekleştirin: ![yapılandırma çoklu oturum açma](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)
     
     a.  Seçin **SAML etkin**. 

     b.  **Yeni**’ye tıklayın.

12. SAML çoklu oturum açma ayarları bölümü Hello üzerinde hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    a.In hello adı metin kutusuna, tür hello hello yapılandırma adını (örneğin: *SPSSOWAAD\_Test*). 

    b. Yapıştır **SMAL varlık kimliği** hello değerine **veren** metin kutusu.

    c. Merhaba, **varlık kimliği** metin kutusuna, türü **https://test.salesforce.com** tooyour directory eklediğiniz ilk Salesforce korumalı alan örneği hello ise. Salesforce korumalı alan, sonra da hello için bir örneği zaten eklediyseniz **varlık kimliği** hello türü **oturum üzerinde URL'si**, şu biçimde olmalıdır:`http://company.my.salesforce.com`  
 
    d. Tıklatın **Gözat** tooupload hello sertifika indirilir.  

    e. Olarak **SAML kimlik türü**seçin **onaylamayı içeren hello Federasyon kimliği hello kullanıcı nesnesinden**.
 
    f. Olarak **SAML kimlik konumu**seçin **kimliktir hello NameIdentifier öğesinde hello konu deyimi**.

    g. Yapıştır **çoklu oturum açma hizmet URL'si** hello içine **kimlik sağlayıcısı oturum açma URL'si** metin kutusu. 

    h. SAML oturum kapatma SFDC desteklemez.  Geçici bir çözüm olarak Yapıştır 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' hello içine **kimlik sağlayıcısı oturum kapatma URL'si** metin kutusu.

    ı. Olarak **hizmet sağlayıcısı tarafından başlatılan bağlama isteği**seçin **HTTP POST**. 

    j. **Kaydet** düğmesine tıklayın.

### <a name="enable-your-domain"></a>Etki alanınızı etkinleştir
Bu bölümde, bir etki alanı zaten oluşturduğunuzu varsayar.  Daha fazla bilgi için bkz: [etki alanı adınız tanımlama](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).

**tooenable etki alanınızı hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba sol gezinti bölmesinde **etki alanı yönetimi**ve ardından **My etki alanı.**
   
     ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   >Lütfen etki alanınızı doğru yapılandırılmış olduğundan emin olun. 

2. Merhaba, **oturum açma sayfası ayarları** 'yi tıklatın **Düzenle**, sonra **kimlik doğrulama hizmeti**seçin hello önceki gelen oturum açma SAML tek ayar hello hello adı bölümünde ve son olarak tıklatın **kaydetmek**.
   
   ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

Yapılandırılmış bir etki alanınız hemen kullanıcılarınızın hello etki alanı URL'si toologin toohello Salesforce korumalı alan kullanmanız gerekir.  

Merhaba URL tooget hello değeri hello önceki bölümde oluşturduğunuz hello SSO profil'ı tıklatın.    

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. Kullanıcıların toodisplay hello listesini Git çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. Merhaba iletişim Hello üstünde tıklatın **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-salesforce-sandbox-test-user"></a>Salesforce korumalı alan test kullanıcısı oluşturma

Bu bölümde, Britta Simon adlı bir kullanıcı Salesforce korumalı alanda oluşturulur. Salesforce korumalı alan yeni saat sağlama, varsayılan olarak etkin olduğu destekler.
Bu bölümde, eylem öğe yok. Salesforce korumalı alanda bir kullanıcı zaten mevcut değilse tooaccess Salesforce korumalı alan çalıştığında yeni bir tane oluşturulur.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooSalesforce Sandbox vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooSalesforce korumalı alan, hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Salesforce korumalı alan**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

SSO ayarlarınızı tootest istiyorsanız hello erişim paneli açın. Merhaba erişim paneli hakkında daha fazla ayrıntı için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
* [Kullanıcı sağlamayı Yapılandır](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

