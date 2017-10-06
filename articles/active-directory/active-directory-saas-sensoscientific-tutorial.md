---
title: "Öğretici: Azure Active Directory Tümleştirme SensoScientific kablosuz sıcaklık izleme sistemi | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile SensoScientific kablosuz sıcaklık izleme sistemi arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: 4eabf7fc6457c217fd5c0c2539ab88c8110055e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a>Öğretici: Azure Active Directory Tümleştirme ile SensoScientific kablosuz sıcaklık sistem izleme

Bu öğreticide, bilgi nasıl toointegrate SensoScientific kablosuz sıcaklık izleme sistemi Azure Active Directory'ye (Azure AD).

SensoScientific kablosuz sıcaklık sistem izleme Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooSensoScientific kablosuz sıcaklık sistem izleme sahip Azure AD'de kontrol edebilirsiniz
- Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooSensoScientific kablosuz sıcaklık sistem izleme (çoklu oturum açma) etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure SensoScientific kablosuz sıcaklık izleme sistemi ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir SensoScientific kablosuz sıcaklık sistem izleme çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden SensoScientific kablosuz sıcaklık sistem izleme ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-hello-gallery"></a>Merhaba Galerisi'nden SensoScientific kablosuz sıcaklık sistem izleme ekleme
Azure AD'ye tooconfigure hello tümleştirme SensoScientific kablosuz Sıcaklık İzleme sisteminin tooadd SensoScientific kablosuz sıcaklık sistem izleme hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd SensoScientific kablosuz sıcaklık izleme sistemi hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **SensoScientific kablosuz sıcaklık sistem izleme**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

5. Merhaba Sonuçlar panelinde seçin **SensoScientific kablosuz sıcaklık sistem izleme**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma SensoScientific kablosuz Sıcaklık "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı sistem izleme ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen SensoScientific kablosuz Sıcaklık İzleme sisteminde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve izleme SensoScientific kablosuz sıcaklık sistemindeki hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** SensoScientific kablosuz Sıcaklık İzleme sistem.

tooconfigure ve SensoScientific kablosuz sıcaklık sistem izleme ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[SensoScientific kablosuz sıcaklık sistem izleme test kullanıcısı oluşturma](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)**  -toohave Britta Simon SensoScientific kablosuz sıcaklık izleme sistemi içinde karşılık gelen bağlı toohello Azure AD gösterimi Kullanıcı.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma SensoScientific kablosuz sıcaklık sistem izleme uygulamanızda yapılandırın.

**Azure AD çoklu oturum açma tooconfigure SensoScientific kablosuz sıcaklık sistemi, izleme hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **SensoScientific kablosuz sıcaklık sistem izleme** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

3. Merhaba üzerinde **SensoScientific kablosuz sıcaklık sistem etki alanı izleme ve URL'leri** bölümünde, herhangi bir adım hello uygulaması olarak zaten önceden tümleştirilmiştir Azure ile hiçbir gerek tooperform:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **SensoScientific kablosuz Sıcaklık İzleme Sistem Yapılandırması** 'yi tıklatın **SensoScientific kablosuz Sıcaklık İzleme sistem yapılandırma** tooopen  **Oturum açma özelliğini yapılandırın** penceresi. Kopya hello **Sign-Out URL, SAML varlık kimliği** ve **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

7. Üzerinde tooyour SensoScientific kablosuz sıcaklık sistem izleme uygulama yönetici olarak oturum açın.

8. Merhaba Gezinti menüsünde hello üstte tıklatın **yapılandırma** ve Git **yapılandırma** altında **çoklu oturum açma** tooopen hello tek oturum açma ayarları.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

9. İçinde **tek oturum açma ayarları** form hello aşağıdaki adımları gerçekleştirin:
 
    a. Seçin **verenin adı** Azure AD olarak.
    
    b. Yapıştır hello **SAML varlık kimliği** veren URL'si metin kutusuna Azure portalından kopyalanan.
    
    c. Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** çoklu oturum açma hizmet URL'si metin kutusuna Azure portalından kopyalanan.

    d. Yapıştır hello **Sign-Out URL** tek Sign-Out hizmeti URL'si metin kutusuna Azure portalından kopyalanan.

    e. Azure portalından indirdiğiniz ve burada karşıya hello sertifika göz atın.
    
    f. **Kaydet** düğmesine tıklayın.
  
> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler](https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a>SensoScientific kablosuz sıcaklık sistem izleme test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toolog tooSensoScientific kablosuz sıcaklık izleme sistemi, bunlar SensoScientific kablosuz sıcaklık izleme sistemine sağlanması gerekir. Çalışmak [SensoScientific kablosuz sıcaklık sistem izleme destek ekibi](https://www.sensoscientific.com/contact-us/) hello SensoScientific kablosuz sıcaklık sistem izleme platformunda hello kullanıcıları eklemek için. Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir. 

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooSensoScientific kablosuz sıcaklık sistem izleme vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooSensoScientific izleme kablosuz sıcaklık sistem hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **SensoScientific kablosuz sıcaklık sistem izleme**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin. Merhaba SensoScientific kablosuz sıcaklık sistem izleme kutucuğa tıklayın hello erişim paneli, otomatik olarak oturum açma tooyour SensoScientific kablosuz sıcaklık sistem izleme uygulama olacaktır. Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_203.png

