---
title: "Öğretici: Azure Active Directory Tümleştirme 10.000 ft planına sahip | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve 10.000 ft arasında planlar."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b60c955e-8fa3-4872-a897-c4e81fd7beac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 9aa6fd079da4f931d4dd7277407a07e56091d7c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-10000ft-plans"></a>Öğretici: Azure Active Directory Tümleştirme 10.000 ft planına sahip

Bu öğreticide, bilgi nasıl toointegrate 10.000 ft planları Azure Active Directory (Azure AD) ile.

10.000 ft planları Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim too10, 000 ft planları sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan too10, 000 ft planlarıyla (çoklu oturum açma) Azure AD hesaplarına etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure 10.000 ft planları ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir 10.000 ft planları çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, burada bir aylık deneme alabilirsiniz [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden planları 10.000 ft ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-10000ft-plans-from-hello-gallery"></a>Merhaba Galerisi'nden planları 10.000 ft ekleme
Azure AD'ye tooconfigure hello tümleştirme 10.000 ft planlardan tooadd ihtiyacınız 10.000 ft planları hello galeri tooyour listesinden yönetilen SaaS uygulamaları.

**Merhaba Galerisi'nden tooadd 10.000 ft planları, hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **10.000 ft planları**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_search.png)

5. Merhaba Sonuçlar panelinde seçin **10.000 ft planları**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma 10.000 ft "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı planları ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen 10.000 ft planlarda tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı 10.000 ft hello arasında bir bağlantı ilişkisi planları gerekiyor toobe kuruldu.

10.000 ft planlarda hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve 10.000 ft planları ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Kullanıcı test planları 10.000 ft oluşturma](#creating-a-10000ft-plans-test-user)**  -bir Britta Simon karşılık gelen 10.000 ft içinde planları diğer bir deyişle toohave bağlı toohello Azure AD kullanıcı gösterimi.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma 10.000 ft planları uygulamanızı yapılandırın.

**tooconfigure Azure AD çoklu oturum açma 10.000 ft planına sahip hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **10.000 ft planları** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_samlbase.png)

3. Merhaba üzerinde **10.000 ft planları etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, türü hello URL'si:`https://app.10000ft.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, türü hello URL'si:`https://app.10000ft.com/saml/metadata`

    > [!NOTE] 
    > Merhaba değeri **tanımlayıcısı** özel bir etki alanı varsa farklıdır. Kişi [10.000 ft planları destek ekibi](https://www.10000ft.com/plans/support) tooget bu değer. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Raw)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **10.000 ft planları yapılandırma** 'yi tıklatın **yapılandırma 10.000 ft planları** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_configure.png) 

7. tooconfigure çoklu oturum açma üzerinde **10.000 ft planları** yan, indirilen toosend hello ihtiyacınız **Certificate(Raw), Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** çok[ 10.000 ft planları destek ekibi](https://www.10000ft.com/plans/support).

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-10000ft-plans-test-user"></a>Kullanıcı test planları 10.000 ft oluşturma

Bu bölümde Hello amacı toocreate Britta Simon 10.000 ft planlarda adlı bir kullanıcı var. 10.000 ft planları yalnızca zaman kaynak sağlamayı destekler, varsayılan olarak etkin olduğu. Bu bölümde, eylem öğe yok. Henüz yoksa yeni bir kullanıcı bir girişim tooaccess 10.000 ft planları sırasında oluşturulur. 

> [!NOTE]
> Toocreate kullanıcı el ile gerekiyorsa, toocontact hello gereksinim [10.000 ft planları destek ekibi](https://www.10000ft.com/plans/support).

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim too10, 000 ft planları vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon too10 000ft planları hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **10.000 ft planları**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.  
Merhaba 10.000 planları hello erişim paneli döşeme ft tıkladığınızda, otomatik olarak oturum açma tooyour 10.000 ft planları uygulama almanız gerekir.
 
## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_203.png

