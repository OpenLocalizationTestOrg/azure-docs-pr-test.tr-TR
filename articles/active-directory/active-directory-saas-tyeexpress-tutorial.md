---
title: "Öğretici: T & E Express Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve T & E Express arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 9a568ace8dbc75fadbf37554996b1b597a813d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a>Öğretici: T & E Express Azure Active Directory Tümleştirme

Bu öğreticide, bilgi nasıl toointegrate T & E Express Azure Active Directory'ye (Azure AD).

T & E Express Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim Systems olan Azure AD & E Express kontrol edebilirsiniz
- Azure AD hesaplarına açan kullanıcıları tooautomatically get Systems & E Express (çoklu oturum açma) etkinleştir
- Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

T & E Express ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir T & E Express çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. T & E Express hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-te-express-from-hello-gallery"></a>T & E Express hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme T & E Express hello galeri tooyour listesinden yönetilen SaaS uygulamaları tooadd T & E Express gerekir.

**tooadd T & E Express hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **Ekle** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **T & E Express**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. Merhaba Sonuçlar panelinde seçin **T & E Express**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma T & "Britta Simon" adlı bir test kullanıcıyı temel alarak E Express ile test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen T & E Express tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir bağlantı bir Azure AD kullanıcı ve kullanıcı arasındaki ilişki hello ilgili kurulan T & E Express gereksinimlerini toobe içinde.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** T & E Express.

tooconfigure ve T & E Express ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[T & E Express test kullanıcısı oluşturma](#creating-a-te-express-test-user)**  -toohave Britta Simon T & E her bağlantılı toohello Azure AD gösterimi olan Express, karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma, T & E Express uygulamanızda yapılandırın.

**T & E Express, Azure AD çoklu oturum açma tooconfigure hello aşağıdaki adımları gerçekleştirin:**

1. Hello üzerinde hello Azure Yönetim Portalı'nda **T & E Express** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. Merhaba üzerinde **T & E Express etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, türü hello değeri olarak:`https://<domain>.tyeexpress.com`

    b. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`

    > [!NOTE] 
    > Lütfen bu hello gerçek değerler olmadığına dikkat edin. Tooupdate hello gerçek tanımlayıcısı ve yanıt URL'si ile bu değerlere sahip. Burada, toouse hello benzersiz değerini hello tanımlayıcı dizesinde öneririz. Kişi [T & E Express desteğini takım](http://www.tyeexpress.com/contacto.aspx) tooget bu değerleri.

5. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. tooconfigure çoklu oturum açma üzerinde **T & E Express** yan, oturum açma toohello T & E express uygulaması SAML olmadan tek yönetici kimlik bilgilerini kullanarak oturum.

9. Merhaba altında **yönetici** sekmesini ve ardından üzerinde **SAML etki alanı** tooOpen hello SAML Ayarları sayfası.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. Select hello **Activar(Activate)** gelen seçeneği **Hayır** çok**SI(Yes)**. Merhaba, **kimlik sağlayıcısı meta verileri** metin kutusuna, Yapıştır hello meta verileri sahip XML donwloaded Azure portalından.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. Tıklatın hello üzerinde **Guardar(Save)** düğmesini toosave hello ayarları. 


### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-te-express-test-user"></a>T & E Express test kullanıcısı oluşturma

T & E Express içine sipariş tooenable Azure AD kullanıcıların toolog bunlar T & E Express sağlanmalıdır.  
T & E Express durumunda, sağlama el ile bir görevdir.

**bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:**

1. Tooyour T & E Express şirket site yönetici olarak oturum açın.

2. Yönetici etiketi altında kullanıcıları tooopen hello kullanıcılar ana sayfasında tıklayın.

    ![Çalışanı ekleyin](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. Merhaba giriş sayfasında, tıklatın  **+**  tooadd hello kullanıcılar.

    ![Çalışanı ekleyin](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. Merhaba formunda sorular gibi tüm hello zorunlu ayrıntılarını girin ve hello Kaydet düğmesine toosave hello Ayrıntılar'ı tıklatın.

    ![Çalışanı ekleyin](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![Çalışanı ekleyin](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, kendi erişim Systems & E Express vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon Systems & E Express, hello aşağıdaki adımları gerçekleştirin:**

1. Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **T & E Express**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba T & hello erişim paneli E Express parçasında tıkladığınızda, otomatik olarak oturum açma tooyour T & E Express uygulaması almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png

