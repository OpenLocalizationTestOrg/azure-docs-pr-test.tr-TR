---
title: "Öğretici: Azure Active Directory Tümleştirme ile Intacct | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Intacct arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3500039615166c2f61fb408d85bb82dfaefba134
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a>Öğretici: Azure Active Directory Tümleştirme Intacct ile

Bu öğreticide, bilgi nasıl toointegrate Intacct Azure Active Directory'ye (Azure AD).

Intacct Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooIntacct sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooIntacct (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Intacct ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Intacct çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Intacct ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-intacct-from-hello-gallery"></a>Merhaba Galerisi'nden Intacct ekleme
Azure AD'ye tooconfigure hello tümleştirme Intacct, tooadd Intacct hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Intacct hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Intacct**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. Merhaba Sonuçlar panelinde seçin **Intacct**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Intacct sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen Intacct içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Intacct hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Intacct içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Intacct ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Bir Intacct test kullanıcısı oluşturma](#creating-an-intacct-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Intacct içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Intacct uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Intacct, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Intacct** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. Merhaba üzerinde **Intacct etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > Bu değer gerçek değil. Bu değer hello gerçek yanıt URL'si ile güncelleştirin. Kişi [Intacct destek ekibi](https://us.intacct.com/support) tooget bu değer.

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Intacct yapılandırma** 'yi tıklatın **yapılandırma Intacct** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. Farklı web tarayıcısı penceresinde tooyour Intacct şirket sitede yönetici olarak oturum açın.

8. Merhaba tıklatın **şirket** sekmesini ve ardından **şirket bilgisi**.

    ![Şirket](./media/active-directory-saas-intacct-tutorial/ic790037.png "şirket")

9. Merhaba tıklatın **güvenlik** sekmesini ve ardından **Düzenle**.

    ![Güvenlik](./media/active-directory-saas-intacct-tutorial/ic790038.png "güvenlik")

10. Merhaba, **tek oturum açma (SSO)** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı](./media/active-directory-saas-intacct-tutorial/ic790039.png "çoklu oturum açmayı")

    a. Seçin **etkinleştirmek çoklu oturum açma**.

    b. Olarak **kimlik sağlayıcısı türü**seçin **SAML 2.0**.

    c. İçinde **veren URL'si** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.
   
    d. İçinde **oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.

    e. Açık, **base-64** kodlanmış sertifika Not Defteri'nde, kopyalama hello panonuza bunu içerik ve toohello yapıştırın **sertifika** kutusu.
   
    f. **Kaydet** düğmesine tıklayın.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-an-intacct-test-user"></a>Bir Intacct test kullanıcısı oluşturma

tooset tooIntacct kaydolabilirsiniz şekilde Azure AD kullanıcılarının bunların Intacct sağlanması gerekir. Intacct için sağlama bir el ile bir görevdir.

**tooprovision kullanıcı hesapları, hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour oturum **Intacct** Kiracı.

2. Merhaba tıklatın **şirket** sekmesini ve ardından **kullanıcılar**.

    ![Kullanıcıların](./media/active-directory-saas-intacct-tutorial/ic790041.png "kullanıcılar")
3. Merhaba tıklatın **Ekle** sekmesi.

    ![Ekleme](./media/active-directory-saas-intacct-tutorial/ic790042.png "ekleme")
4. Merhaba, **kullanıcı bilgilerini** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Kullanıcı bilgilerini](./media/active-directory-saas-intacct-tutorial/ic790043.png "kullanıcı bilgileri")

    a. Merhaba girin **kullanıcı kimliği**, hello **Soyadı**, **ad**, hello **e-posta adresi**, hello **başlık**, ve hello **telefon** hello tooprovision istediğiniz bir Azure AD hesabının **kullanıcı bilgilerini** bölümü.

    b. Select hello **yönetici ayrıcalıkları** tooprovision istediğiniz bir Azure AD hesabının.
   
    c. **Kaydet** düğmesine tıklayın. Hello Azure AD hesap sahibi bir e-posta alır ve onu etkinleştirilmeden önce bir bağlantı tooconfirm hesaplarında izler.

>[!NOTE]
>tooprovision Azure AD kullanıcı hesapları, diğer Intacct kullanıcı hesabı oluşturma araçlarını veya Intacct tarafından sağlanan API'leri kullanabilirsiniz.
        
### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooIntacct vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooIntacct hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Intacct**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test.

Merhaba Intacct hello erişim paneli parçasında tıklattığınızda tooyour Intacct uygulama otomatik olarak imzalanmalıdır.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

