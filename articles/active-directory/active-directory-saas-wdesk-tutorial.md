---
title: "Öğretici: Azure Active Directory Tümleştirme ile Wdesk | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Wdesk arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 2c278a5e4f50cc362663efc0f826ff0c0fcf6e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a>Öğretici: Azure Active Directory Tümleştirme Wdesk ile

Bu öğreticide, bilgi nasıl toointegrate Wdesk Azure Active Directory'ye (Azure AD).

Wdesk Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooWdesk sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooWdesk (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz. [Uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Wdesk ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Wdesk çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Wdesk ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-wdesk-from-hello-gallery"></a>Merhaba Galerisi'nden Wdesk ekleme
Azure AD'ye tooconfigure hello tümleştirme Wdesk, tooadd Wdesk hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Wdesk hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Wdesk**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. Merhaba Sonuçlar panelinde seçin **Wdesk**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Wdesk ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen Wdesk içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Wdesk hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Wdesk içinde.

tooconfigure ve Wdesk ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Wdesk test kullanıcısı oluşturma](#creating-a-wdesk-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Wdesk içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Wdesk uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Wdesk, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Wdesk** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. Merhaba üzerinde **Wdesk etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **IDP** başlatılan modu hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`

    b. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`

4. Denetleme **Göster Gelişmiş URL ayarları**. Tooconfigure hello uygulamada istiyorsanız **SP** modunda başlatılan adım aşağıdaki hello gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`
     
    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler. Merhaba SSO yapılandırdığınızda WDesk Portalı'ndan bu değerleri alır. 
  
5. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. Bir farklı web tarayıcısı penceresinde, bir güvenlik yöneticisi olarak oturum açma tooWdesk.

8. Merhaba alt sol tıklayın **yönetici** ve **Hesap Yöneticisi**:
 
     ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. Wdesk Yöneticisi çok gidin**güvenlik**, ardından **SAML** > **SAML ayarları**:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. Altında **genel ayarları**, hello denetleyin **SAML çoklu oturum açmayı etkinleştir**:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. Altında **hizmet sağlayıcı ayrıntıları**, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      a. Kopya hello **oturum açma URL'si** ve yapıştırın **oturum açma URL'si** Azure Portal'daki metin kutusu.
   
      b. Kopya hello **meta veri URL'sini** ve yapıştırın **tanımlayıcısı** Azure Portal'daki metin kutusu.
       
      c. Kopya hello **tüketici url** ve yapıştırın **yanıt URL'si** Azure Portal'daki metin kutusu.
   
      d. Tıklatın **kaydetmek** Azure portal toosave hello değişir.      

12. Tıklatın **IDP ayarlarını yapılandır** tooopen **IDP ayarlarını Düzenle** iletişim. Tıklatın **Dosya Seç** toolocate hello **Metadata.xml** Azure portalından, kaydettiğiniz dosyayı karşıya yükleyin.
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. Tıklatın **değişiklikleri kaydetmek**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-wdesk-test-user"></a>Wdesk test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toolog tooWdesk bunların Wdesk sağlanması gerekir. Wdesk içinde sağlama bir el ile bir görevdir.

**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooWdesk güvenlik yönetici olarak oturum açın.
2. Çok gidin**yönetici** > **Hesap Yöneticisi**.

     ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. Tıklatın **üyeleri** altında **kişiler**.

4. Şimdi **Üye Ekle** tooopen **Üye Ekle** iletişim kutusu. 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. İçinde **kullanıcı** metin kutusuna, kullanıcının gibi hello kullanıcı adı girin  **brittasimon@contoso.com**  tıklatıp **devam** düğmesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  Aşağıda gösterildiği gibi Hello ayrıntılarını girin:
  
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    a. İçinde **e-posta** metin kutusunda, bir kullanıcı gibi hello e-posta girin  **brittasimon@contoso.com** .

    b. İçinde **ad** metin kutusuna, hello ilk gibi kullanıcı adını girin **Britta**.

    c. İçinde **Soyadı** metin kutusuna, hello kullanıcının soyadını gibi girin **Simon**.

7. Tıklatın **Save Member** düğmesi.  

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooWdesk vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooWdesk hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Wdesk**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Wdesk hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Wdesk uygulama almanız gerekir.
Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

