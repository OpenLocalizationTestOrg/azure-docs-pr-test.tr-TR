---
title: "Öğretici: Azure Active Directory Tümleştirme Uyarlamalı Suite ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Uyarlamalı Suite arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: af309c27ab74098c1e229c80adb11c96dc2774fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a>Öğretici: Azure Active Directory Tümleştirme Uyarlamalı Suite ile

Bu öğreticide, bilgi nasıl toointegrate Uyarlamalı Suite Azure Active Directory'ye (Azure AD).

Uyarlamalı Suite Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooAdaptive paketi olan Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooAdaptive paketi (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Uyarlamalı Suite ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Uyarlamalı Suite çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Uyarlamalı paketi ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-adaptive-suite-from-hello-gallery"></a>Merhaba Galerisi'nden Uyarlamalı paketi ekleme
Azure AD'ye tooconfigure hello tümleştirme Uyarlamalı paketinin tooadd Uyarlamalı Suite hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd hello Galerisi, Uyarlamalı paketinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Uyarlamalı Suite**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. Merhaba Sonuçlar panelinde seçin **Uyarlamalı Suite**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Uyarlamalı "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Suite ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen Uyarlamalı paketindeki tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı Uyarlamalı paketindeki arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Uyarlamalı paketindeki hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Uyarlamalı Suite ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on) ** -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user) ** -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Uyarlamalı Suite test kullanıcısı oluşturma](#creating-an-adaptive-suite-test-user) ** -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Uyarlamalı paketindeki, karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on) ** -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Uyarlamalı Suite uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma Uyarlamalı Suite ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **Uyarlamalı Suite** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. Merhaba üzerinde **Uyarlamalı Suite etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://login.adaptiveinsights.com:443/samlsso/<unique-id>`

    >[!NOTE]
    > Bu değer hello Uyarlamalı Suite's alabilir **SAML SSO ayarları** sayfası.
    >  

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Uyarlamalı paketi yapılandırma** 'yi tıklatın **yapılandırma Uyarlamalı Suite** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. Farklı web tarayıcısı penceresinde tooyour Uyarlamalı Suite şirket sitede yönetici olarak oturum açın.

8. Çok Git**yönetici**.
   
    ![Yönetici](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "yönetici")

9. Merhaba, **kullanıcılar ve roller** 'yi tıklatın **SAML SSO ayarları yönetme**.
   
    ![SAML SSO ayarlarını Yönet](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "SAML SSO ayarlarını yönet")

10. Merhaba üzerinde **SAML SSO ayarları** sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![SAML SSO ayarları](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO ayarları")

    a. Merhaba, **kimlik sağlayıcı adı** metin kutusuna, yapılandırmanız için bir ad yazın.
    
    b. Yapıştır hello **SAML varlık kimliği** değeri hello Azure portalından kopyalanan **kimlik sağlayıcısı varlık kimliği** metin kutusu.
  
    c. Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** değeri hello Azure portalından kopyalanan **kimlik sağlayıcısı SSO URL** metin kutusu.
  
    d. Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** değeri hello Azure portalından kopyalanan **özel oturum kapatma URL'si** metin kutusu.
  
    e. tooupload indirilen sertifikanızı tıklatın **dosya**.
  
    f. Merhaba, aşağıdakileri seçin:
    * **SAML kullanıcı kimliği**seçin **Uyarlamalı Öngörüler kullanıcının adını**.
    * **SAML kullanıcı kimliği konumu**seçin **NameID, konu kullanıcı kimliği**.
    * **SAML NameID biçimi**seçin **e-posta adresi**.
    * **SAML'yi etkinleştir**seçin **izin SAML SSO ve doğrudan Uyarlamalı Öngörüler oturum açma**.
    
    g. **Kaydet** düğmesine tıklayın.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere ** Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-an-adaptive-suite-test-user"></a>Uyarlamalı Suite test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toolog tooAdaptive Suite'da, bunlar Uyarlamalı paketine sağlanması gerekir.  

* Uyarlamalı Suite Hello durumda sağlama bir el ile bir görevdir.

**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:** 

1. İçinde tooyour oturum **Uyarlamalı Suite** yönetici olarak şirket site.
2. Çok Git**yönetici**.
   
   ![Yönetici](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "yönetici")
3. Merhaba, **kullanıcılar ve roller** 'yi tıklatın **Kullanıcı Ekle**.
   
   ![Kullanıcı ekleme](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "kullanıcı ekleme")
4. Merhaba, **yeni kullanıcı** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
   ![Gönderme](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Gönder")   

   a. Türü hello **adı**, **oturum açma**, **e-posta**, **parola** geçerli bir Azure Active Directory kullanıcı ilgili hello tooprovision istiyor metin kutuları.
  
   b. Seçin bir **rol**.
  
   c. Tıklatın **gönderme**.

>[!NOTE]
>API AAD kullanıcı hesapları Uyarlamalı Suite tooprovision tarafından sağlanan veya herhangi diğer Uyarlamalı Suite kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.
>  

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooAdaptive Suite vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooAdaptive Suite, hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Uyarlamalı Suite**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde Hello amacı olan tootest hello erişim paneli, Microsoft Azure AD çoklu oturum açma yapılandırması kullanılarak.

Merhaba Uyarlamalı Suite hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Uyarlamalı paketi uygulama almanız gerekir.


## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png

