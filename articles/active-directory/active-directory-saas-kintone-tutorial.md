---
title: "Öğretici: Azure Active Directory Tümleştirme ile Kintone | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Kintone arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 4f61fb95c643743504699b175beeff06e01c95c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a>Öğretici: Azure Active Directory Tümleştirme Kintone ile

Bu öğreticide, bilgi nasıl toointegrate Kintone Azure Active Directory'ye (Azure AD).

Kintone Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooKintone sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooKintone (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Kintone ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Kintone çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Kintone ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-kintone-from-hello-gallery"></a>Merhaba Galerisi'nden Kintone ekleme
Azure AD'ye tooconfigure hello tümleştirme Kintone, tooadd Kintone hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Kintone hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Kintone**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_search.png)

5. Merhaba Sonuçlar panelinde seçin **Kintone**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Kintone sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen Kintone içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Kintone hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Kintone içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Kintone ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Kintone test kullanıcısı oluşturma](#creating-a-kintone-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Kintone içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Kintone uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Kintone, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Kintone** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_samlbase.png)

3. Merhaba üzerinde **Kintone etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.kintone.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [Kintone istemci destek ekibi](https://www.kintone.com/contact/) tooget bu değerleri. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kintone-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Kintone yapılandırma** 'yi tıklatın **yapılandırma Kintone** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_configure.png) 

7. Farklı web tarayıcısı penceresinde oturum açın, **Kintone** yönetici olarak şirket site.

8. Tıklatın **ayarları**.
   
    ![Ayarları](./media/active-directory-saas-kintone-tutorial/ic785879.png "ayarları")

9. Tıklatın **kullanıcılar ve sistem yönetimini**.
   
    ![Kullanıcılar ve sistem yönetimini](./media/active-directory-saas-kintone-tutorial/ic785880.png "kullanıcılar ve Sistem Yönetimi")

10. Altında **Sistem Yönetimi \> güvenlik** tıklatın **oturum açma**.
   
    ![Oturum açma](./media/active-directory-saas-kintone-tutorial/ic785881.png "oturum açma")

11. Tıklatın **etkinleştirmek SAML kimlik doğrulaması**.
   
    ![SAML kimlik doğrulaması](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML kimlik doğrulaması")

12. Hello SAML kimlik doğrulaması bölümü, hello aşağıdaki adımları gerçekleştirin:
    
    ![SAML kimlik doğrulaması](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML kimlik doğrulaması")
    
    a. Merhaba, **oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.
   
    b. Merhaba, **oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL** Azure portalından kopyalanan.
    
    c. Tıklatın **Gözat** tooupload indirilen sertifikanızı.
    
    d. **Kaydet** düğmesine tıklayın.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kintone-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kintone-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kintone-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kintone-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-kintone-test-user"></a>Kintone test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toolog tooKintone bunların Kintone sağlanması gerekir.  
Kintone Hello durumda sağlama bir el ile bir görevdir.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:

1. İçinde tooyour oturum **Kintone** yönetici olarak şirket site.

2. Tıklatın **ayarı**.
   
    ![Ayarları](./media/active-directory-saas-kintone-tutorial/ic785879.png "ayarları")

3. Tıklatın **kullanıcılar ve sistem yönetimini**.
   
    ![Kullanıcı & Sistem Yönetimi](./media/active-directory-saas-kintone-tutorial/ic785880.png "kullanıcı & Sistem Yönetimi")

4. Altında **kullanıcı yönetimi**, tıklatın **Departmanlar k & ullanıcıların**.
   
    ![K & ullanıcıların departmanı](./media/active-directory-saas-kintone-tutorial/ic785888.png "departmanı ve kullanıcılar")

5. Tıklatın **yeni kullanıcı**.
   
    ![Yeni kullanıcılar](./media/active-directory-saas-kintone-tutorial/ic785889.png "yeni kullanıcılar")

6. Merhaba, **yeni kullanıcı** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![Yeni kullanıcılar](./media/active-directory-saas-kintone-tutorial/ic785890.png "yeni kullanıcılar")
   
    a. Tür a **görünen adı**, **oturum açma adı**, **yeni parola**, **parolayı onaylayın**, **e-posta adresi**, ve ilgili diğer ayrıntıları hello tooprovision istediğiniz geçerli bir AAD hesabının metin kutuları.
 
    b. **Kaydet** düğmesine tıklayın.

> [!NOTE]
> API AAD kullanıcı hesaplarının Kintone tooprovision tarafından sağlanan veya herhangi diğer Kintone kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooKintone vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooKintone hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Kintone**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.

Merhaba Kintone hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Kintone uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_203.png

