---
title: "Öğretici: Azure Active Directory Tümleştirme ile AirWatch | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile AirWatch arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e5230d5a36824778a4d9804dadf9f13a0d11a68d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a>Öğretici: Azure Active Directory Tümleştirme AirWatch ile

Bu öğreticide, bilgi nasıl toointegrate AirWatch Azure Active Directory'ye (Azure AD).

AirWatch Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooAirWatch sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooAirWatch (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure AirWatch ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir AirWatch çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden AirWatch ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-airwatch-from-hello-gallery"></a>Merhaba Galerisi'nden AirWatch ekleme
Azure AD'ye tooconfigure hello tümleştirme AirWatch, tooadd AirWatch hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd AirWatch hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **AirWatch**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. Merhaba Sonuçlar panelinde seçin **AirWatch**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı AirWatch ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen AirWatch içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı AirWatch hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** AirWatch içinde.

tooconfigure ve AirWatch ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[AirWatch test kullanıcısı oluşturma](#creating-a-airwatch-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir AirWatch içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma AirWatch uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile AirWatch, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **AirWatch** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. Merhaba üzerinde **AirWatch etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, türü hello değeri olarak`AirWatch`

    > [!NOTE] 
    > Bu değer hello gerçek değil. Bu değer hello gerçek oturum açma URL'si ile güncelleştirin. Kişi [AirWatch istemci destek ekibi](http://www.air-watch.com/company/contact-us/) tooget bu değer. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. Merhaba üzerinde **AirWatch yapılandırma** 'yi tıklatın **yapılandırma AirWatch** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS>
7. Farklı web tarayıcısı penceresinde tooyour AirWatch şirket sitede yönetici olarak oturum açın.

8. Merhaba sol gezinti bölmesinde **hesapları**ve ardından **Yöneticiler**.
   
   ![Yöneticiler](./media/active-directory-saas-airwatch-tutorial/ic791920.png "yöneticileri")

9. Merhaba genişletin **ayarları** menüsüne ve ardından **Dizin Hizmetleri**.
   
   ![Ayarları](./media/active-directory-saas-airwatch-tutorial/ic791921.png "ayarları")

10. Merhaba tıklatın **kullanıcı** sekmede hello **temel DN** metin kutusuna, etki alanı adınızı yazın ve ardından **kaydetmek**.
   
   ![Kullanıcı](./media/active-directory-saas-airwatch-tutorial/ic791922.png "kullanıcı")

11. Merhaba tıklatın **Server** sekmesi.
   
   ![Sunucu](./media/active-directory-saas-airwatch-tutorial/ic791923.png "sunucu")

12. Merhaba aşağıdaki adımları gerçekleştirin:
    
    ![Karşıya yükleme](./media/active-directory-saas-airwatch-tutorial/ic791924.png "karşıya yükle")   
    
    a. Olarak **Directory türü**seçin **hiçbiri**.

    b. Seçin **SAML kimlik doğrulaması için kullanmak**.

    c. tooupload Merhaba indirilen sertifika, tıklatın **karşıya**.

13. Merhaba, **isteği** bölümünde, hello aşağıdaki adımları gerçekleştirin:
    
    ![İstek](./media/active-directory-saas-airwatch-tutorial/ic791925.png "isteği")  

    a. Olarak **bağlama türü isteği**seçin **POST**.

    b. Merhaba hello üzerinde Azure portal'ın **çoklu oturum açma sırasında Airwatch yapılandırma** iletişim sayfası, kopyalama hello **SAML çoklu oturum açma hizmet URL'si** değer ve hello yapıştırma **kimlik sağlayıcısı Tek bir oturum üzerinde URL'si** metin kutusu.

    c. Olarak **NameID biçimi**seçin **e-posta adresi**.

    d. **Kaydet** düğmesine tıklayın.

14. Merhaba tıklatın **kullanıcı** yeniden sekmesinde.
    
    ![Kullanıcı](./media/active-directory-saas-airwatch-tutorial/ic791926.png "kullanıcı")

15. Merhaba, **özniteliği** bölümünde, hello aşağıdaki adımları gerçekleştirin:
    
    ![Öznitelik](./media/active-directory-saas-airwatch-tutorial/ic791927.png "özniteliği")

    a. Merhaba, **nesne tanımlayıcısı** metin kutusuna, türü **http://schemas.microsoft.com/identity/claims/objectidentifier**.

    b. Merhaba, **kullanıcıadı** metin kutusuna, türü **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.

    c. Merhaba, **görünen adı** metin kutusuna, türü **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.

    d. Merhaba, **ad** metin kutusuna, türü **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.

    e. Merhaba, **Soyadı** metin kutusuna, türü **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.

    f. Merhaba, **e-posta** metin kutusuna, türü **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.

    g. **Kaydet** düğmesine tıklayın.

<CE>

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** Britta Simon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-airwatch-test-user"></a>AirWatch test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toolog tooAirWatch bunlar içinde tooAirWatch sağlanması gerekir.

* AirWatch, sağlama el ile bir görev olduğunda.

**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour oturum **AirWatch** yönetici olarak şirket site.
2. Merhaba Gezinti hello sol taraftaki bölmede **hesapları**ve ardından **kullanıcılar**.
   
   ![Kullanıcıların](./media/active-directory-saas-airwatch-tutorial/ic791929.png "kullanıcılar")
3. Merhaba, **kullanıcılar** menüsünde tıklatın **liste görünümü**ve ardından **Ekle \> Kullanıcı Ekle**.
   
   ![Kullanıcı ekleme](./media/active-directory-saas-airwatch-tutorial/ic791930.png "kullanıcı ekleme")
4. Merhaba üzerinde **Ekle / Düzenle kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:

   ![Kullanıcı ekleme](./media/active-directory-saas-airwatch-tutorial/ic791931.png "kullanıcı ekleme")   
   1. Türü hello **kullanıcıadı**, **parola**, **parolayı onayla**, **ad**, **Soyadı**,  **E-posta adresi** geçerli bir Azure hello tooprovision istediğiniz Active Directory hesabı kutularındaki ilgili.
   2. **Kaydet** düğmesine tıklayın.

>[!NOTE]
>API AAD kullanıcı hesaplarının AirWatch tooprovision tarafından sağlanan veya herhangi diğer AirWatch kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.
>  

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooAirWatch vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooAirWatch hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **AirWatch**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Çoklu oturum açma ayarlarınızı tootest istiyorsanız hello erişim paneli açın. Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

