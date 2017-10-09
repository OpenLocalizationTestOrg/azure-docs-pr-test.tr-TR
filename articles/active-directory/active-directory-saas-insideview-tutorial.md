---
title: "Öğretici: Azure Active Directory Tümleştirme ile InsideView | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile InsideView arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c489a7ab-6b1f-4efb-8a66-8bc13bca78c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 979c0c24f3a18a193616061b8c2e78292233a56d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insideview"></a>Öğretici: Azure Active Directory Tümleştirme InsideView ile

Bu öğreticide, bilgi nasıl toointegrate InsideView Azure Active Directory'ye (Azure AD).

InsideView Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooInsideView sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooInsideView (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure InsideView ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir InsideView çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden InsideView ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-insideview-from-hello-gallery"></a>Merhaba Galerisi'nden InsideView ekleme
Merhaba tümleştirilmesi tooconfigure InsideView tooAzure AD içinde tooadd InsideView hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd InsideView hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **InsideView**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_search.png)

5. Merhaba Sonuçlar panelinde seçin **InsideView**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı InsideView ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen InsideView içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı InsideView hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri InsideView içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve InsideView ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[InsideView test kullanıcısı oluşturma](#creating-a-insideview-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir InsideView içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma InsideView uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile InsideView, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **InsideView** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_samlbase.png)

3. Merhaba üzerinde **InsideView etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_url.png)
    
    Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://my.insideview.com/iv/<STS Name>/login.iv`

    > [!NOTE] 
    > Bu değer gerçek değil. Bu değer hello gerçek yanıt URL'si ile güncelleştirin. Kişi [InsideView destek ekibi ](mailto:support@insideview.com) tooget bu değer.
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (ham)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-insideview-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **InsideView yapılandırma** 'yi tıklatın **yapılandırma InsideView** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_configure.png) 

7. Farklı web tarayıcısı penceresinde tooyour InsideView şirket sitede yönetici olarak oturum açın.

8. Merhaba üstte Hello araç çubuğunda **yönetici**, **SingleSignOn ayarları**ve ardından **eklemek SAML**.
   
   ![SAML çoklu oturum açma ayarları](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML çoklu oturum açma ayarları")

9. Merhaba, **yeni bir SAML eklemek** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Yeni bir SAML eklemek](./media/active-directory-saas-insideview-tutorial/ic794136.png "yeni bir SAML ekleme")
   
    a. Merhaba, **STS adını** metin kutusuna, yapılandırmanız için bir ad yazın.

    b. İçinde **SamlP/WS-Fed istenmeyen EndPoint** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.
    
    c. Azure portal, kopyalama hello panonuza bunu içerik gelen yüklediğiniz, base-64 kodlanmış sertifika açın ve ardından toohello yapıştırın **STS sertifikası** metin kutusu.

    d. Merhaba, **Crm kullanıcı kimliği eşleme** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
        
    e. Merhaba, **Crm e-posta eşleme** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.

    f. Merhaba, **ilk adı Crm eşleme** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.
    
    g. Merhaba, **Crm lastName eşleme** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.  

    h. **Kaydet** düğmesine tıklayın.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 
 
### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-insideview-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-insideview-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-insideview-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-insideview-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-insideview-test-user"></a>InsideView test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toolog tooInsideView bunlar içinde tooInsideView sağlanması gerekir. InsideView Hello durumda sağlama bir el ile bir görevdir.

tooget kullanıcılar ve kişiler oluşturulan InsideView, kişi [InsideView destek ekibi](mailto:support@insideview.com).

>[!NOTE]
>API'leri, Azure AD kullanıcı hesapları InsideView tooprovision tarafından sağlanan veya herhangi diğer InsideView kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooInsideView vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooInsideView hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **InsideView**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba InsideView hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour InsideView uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_203.png

