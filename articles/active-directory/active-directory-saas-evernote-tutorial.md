---
title: "Öğretici: Azure Active Directory Tümleştirme ile Evernote | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Evernote arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 4d7017e571ed12a0b155aa188c6b0ecb3c9898a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a>Öğretici: Azure Active Directory Tümleştirme Evernote ile

Bu öğreticide, bilgi nasıl toointegrate Evernote Azure Active Directory'ye (Azure AD).

Evernote Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooEvernote sahip Azure AD'de kontrol edebilirsiniz.
- Kullanıcıların tooautomatically get açan tooEvernote (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Evernote ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Evernote çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Evernote ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-evernote-from-hello-gallery"></a>Merhaba Galerisi'nden Evernote ekleme
Azure AD'ye tooconfigure hello tümleştirme Evernote, tooadd Evernote hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Evernote hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna yazın **Evernote**seçin **Evernote** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Merhaba sonuçları listesinde Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Evernote sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen Evernote içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Evernote hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Evernote içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Evernote ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Bir Evernote test kullanıcısı oluşturma](#create-an-evernote-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Evernote içinde karşılık gelen.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Evernote uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Evernote, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Evernote** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. Merhaba üzerinde **Evernote etki alanı ve URL'leri** bölümünde, hello tooconfigure hello IDP uygulamada başlatılan modu istiyorsanız aşağıdaki adımları gerçekleştirin:

    ![Evernote etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url.png)

    Merhaba, **tanımlayıcısı** metin kutusuna, türü hello URL'si:`https://www.evernote.com/saml2`

4. Denetleme **Göster Gelişmiş URL ayarları** ve adım tooconfigure hello uygulamada istiyorsanız aşağıdaki hello gerçekleştirmek **SP** modunda başlatılan:

    ![Evernote etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url1.png)

    Merhaba, **URL üzerinde oturum** metin kutusuna, türü hello URL'si:`https://www.evernote.com/Login.action`   

5. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

6. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

7. Merhaba üzerinde **Evernote yapılandırma** 'yi tıklatın **yapılandırma Evernote** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Evernote yapılandırma](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

8. Farklı web tarayıcısı penceresinde Evernote şirket sitenize yönetici olarak oturum açın.

9. Çok Git**'Yönetici Konsolu'**

    ![Yönetim Konsolu](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

10. Merhaba gelen **'Yönetici Konsolu'**, çok Git**'Security'** seçip **' çoklu oturum açma '**

    ![SSO ayarı](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

11. Hello aşağıdaki değerleri yapılandırın:

    ![Sertifika ayarları](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)
    
    a.  **SSO etkinleştir:** SSO varsayılan olarak etkindir (tıklatın **devre dışı çoklu oturum açma** tooremove hello SSO gereksinim)

    b. Yapıştır **SAML çoklu oturum açma hizmet URL'si** hello hello Azure portal ' kopyaladığınız değeri **SAML HTTP istek URL'si** metin kutusu.

    c. "Sertifika başlayın" ve "Son SERTİFİKAYI" gibi bir not defteri ve kopyalama hello içerik Azure AD'den hello indirilen sertifika açın ve hello yapıştırma **X.509 sertifikası** metin kutusu. 

    d.Click **Değişiklikleri Kaydet**

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

   ![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-evernote-tutorial/create_aaduser_01.png)

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-evernote-tutorial/create_aaduser_02.png)

3. tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-evernote-tutorial/create_aaduser_03.png)

4. Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-evernote-tutorial/create_aaduser_04.png)

    a. Merhaba, **adı** kutusuna **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.

    c. Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-an-evernote-test-user"></a>Bir Evernote test kullanıcısı oluşturma

Evernote içine sipariş tooenable Azure AD kullanıcıların toolog bunların Evernote sağlanmalıdır.  
Evernote Hello durumda sağlama bir el ile bir görevdir.

**bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:**

1. İçinde tooyour Evernote şirket site yönetici olarak oturum açın.

2. Merhaba tıklatın **'Yönetici Konsolu'**.

    ![Yönetim Konsolu](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. Merhaba gelen **'Yönetici Konsolu'**, çok Git**'kullanıcıları eklemek'**.

    ![Ekleme testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. **Ekip üyeleri ekleme** hello içinde **e-posta** metin kutusu, kullanıcı hesabı hello e-posta adresini yazın ve'ı tıklatın **davet edin.**

    ![Ekleme testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. Davet gönderildikten sonra hello Azure Active Directory hesap sahibinin e-posta tooaccept hello davetiye alır.

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooEvernote vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200] 

**tooassign Britta Simon tooEvernote hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Evernote**.

    ![Merhaba Evernote bağlantı hello uygulamalar listesinde](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png)  

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Evernote hello erişim paneli parçasında tıkladığınızda, oturum açma Evernote uygulama tooyour almanız gerekir. Bir kuruluş hesabı ancak gerek toolog sonra kişisel hesabınızla oturum. 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_203.png

