---
title: "Öğretici: Azure Active Directory Tümleştirme almak LMS ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve almak LMS arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: a140a78a3a9474a6372a3ad4fb8251bd2452c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a>Öğretici: Azure Active Directory Tümleştirme almak LMS ile

Bu öğreticide, bilgi nasıl toointegrate Absorb LMS Azure Active Directory'ye (Azure AD).

Almak LMS Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooAbsorb LMS sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooAbsorb LMS (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz. [Uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure almak LMS ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir almak LMS çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden almak LMS ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-absorb-lms-from-hello-gallery"></a>Merhaba Galerisi'nden almak LMS ekleme
Merhaba tümleştirilmesi tooconfigure almak LMS tooAzure AD içinde tooadd Absorb LMS hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Absorb LMS hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Hello arama kutusuna yazın **almak LMS**seçin **almak LMS** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Merhaba sonuçlar listesinde LMS Al](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı LMS almak ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen almak LMS içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı almak LMS hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** almak LMS içinde.

tooconfigure ve almak LMS ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Bir almak LMS test kullanıcısı oluşturma](#create-an-absorb-lms-test-user)**  -toohave Britta Simon kapsamına bağlantılı toohello Azure AD kullanıcı gösterimidir LMS içinde karşılık gelen.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma almak LMS uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma almak LMS ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **almak LMS** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. Merhaba üzerinde **LMS etki alanı almak ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![LMS etki alanı ve URL'leri tek oturum açma bilgilerini al](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.myabsorb.com/Account/SAML`

    b. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.myabsorb.com/Account/SAML`
     
    > [!NOTE] 
    > Bu değerler hello gerçek değildir. Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin. Kişi [almak LMS istemci destek ekibi](https://www.absorblms.com/support) tooget bu değerleri. 

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. Merhaba üzerinde **almak LMS yapılandırma** 'yi tıklatın **almak LMS yapılandırma** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![LMS yapılandırma Al](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. Farklı web tarayıcısı penceresinde tooyour almak LMS şirket sitede yönetici olarak oturum açın.

9. Merhaba tıklatın **hesabı simgesi** hello yönetici arabirimde. 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-absorblms-tutorial/1.png)

10. Tıklatın **Portal ayarları**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. Merhaba tıklatın **kullanıcılar** sekmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-absorblms-tutorial/3.png)

12. Yapılandırma alanları çoklu oturum açma adımları tooaccess hello izleyen hello gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-absorblms-tutorial/4.png)

    a. Select hello uygun **modu**.

    b. Açık hello hello Not Defteri'nde, Azure Portalı'ndan indirilen sertifika kaldırmak hello **---başlangıç sertifika---** ve **---son SERTİFİKAYI---** etiketi ve içeriği kalan hello yapıştırın Merhaba **anahtar** metin kutusu.
    
    c. Merhaba, **ID özelliği**, select hello hello (örneğin kullanıcı adı burada seçilen sonra hello userprinciplename Azure AD'de seçtiyseniz,.) Azure AD kullanıcı tanımlayıcısını hello olarak yapılandırılmış uygun özniteliği

    d. Merhaba, **oturum açma URL'si**, hello yapıştırın **"SAML çoklu oturum açma hizmeti URL'si"** hello kopyalanıp değeri **yapılandırma oturum açma** hello Azure portalı penceresi.

    e. Merhaba, **oturum kapatma URL'si**, hello yapıştırın **"Sign-Out URL"** hello kopyalanıp değeri **yapılandırma oturum açma** hello Azure portalı penceresi.

13. Etkinleştirme **'Yalnızca izin ver SSO oturum açma'**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-absorblms-tutorial/5.png)

14. Tıklatın **"Kaydedin."**

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Merhaba Ekle düğmesi](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.

### <a name="create-an-absorb-lms-test-user"></a>Bir almak LMS test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toolog tooAbsorb LMS'da, bunlar tooAbsorb LMS sağlanması gerekir.  
LMS almak için sağlama bir el ile bir görevdir.

**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour almak LMS şirket site yönetici olarak oturum.

2. Tıklatın **kullanıcılar** sekmesi.

    ![Kişileri davet edin](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. Tıklatın **kullanıcılar** hello altında **kullanıcılar** sekmesi.

    ![Kişileri davet edin](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  Seçin **kullanıcı** gelen **yeni Ekle** açılır.

    ![Kişileri davet edin](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. Merhaba üzerinde **Kullanıcı Ekle** sayfasında, hello aşağıdaki adımları gerçekleştirin:

    ![Kişileri davet edin](./media/active-directory-saas-absorblms-tutorial/user.png)

    a. Merhaba, **ad** metin kutusuna, türü hello ad Britta gibi.

    b. Merhaba, **Soyadı** metin kutusuna, türü hello Soyadı Simon gibi.
    
    c. Merhaba, **kullanıcıadı** metin kutusuna, Britta Simon gibi türü hello kullanıcı adı.

    d. Merhaba, **parola** metin kutusuna, Britta Simon hello parola türünde.

    e. Merhaba, **parolayı onayla** metin kutusuna, türü hello aynı parola.
    
    f. Olarak olun **etkin**.   

6. Tıklatın **"Kaydedin."**
 
### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooAbsorb LMS vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200]

**tooassign Britta Simon tooAbsorb LMS, hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **almak LMS**.

    ![Merhaba almak LMS bağlantı hello uygulamalar listesinde](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Hello almak LMS döşeme hello erişim paneli tıklatın otomatik olarak oturum açma tooyour almak LMS uygulama alırsınız. Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

