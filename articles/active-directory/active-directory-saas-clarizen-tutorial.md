---
title: "Öğretici: Azure Active Directory Tümleştirme ile Clarizen | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Clarizen arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: f24ccda3b90e5df9a203a444dfda905043b30276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a>Öğretici: Azure Active Directory Tümleştirme Clarizen ile

Bu öğreticide, bilgi nasıl toointegrate Clarizen ile Azure Active Directory (Azure AD). Yararları hello Bu tümleştirme sağlar:

- Erişim tooClarizen sahip Azure AD'de denetleyebilirsiniz.
- Azure AD hesaplarına sahip (çoklu oturum açma) tooClarizen içinde otomatik olarak imzalanmış, kullanıcıların toobe etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda, hello Azure portalında yönetebilir.

Bu öğreticide Hello senaryo iki ana görevden oluşur:

1. Clarizen hello Galerisi'nden ekleyin.
2. Yapılandırma ve Azure AD çoklu oturum açmayı sınayın.

Azure AD ile hizmet (SaaS) uygulaması tümleştirme olarak yazılım hakkında daha fazla bilgi istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar
tooconfigure Clarizen ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Çoklu oturum açma için etkinleştirilen Clarizen abonelik

Bu öğreticide tootest hello adımları bu önerileri izleyin:

- Azure AD çoklu oturum açma bir test ortamında test edin. Bu gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD test ortamı yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="add-clarizen-from-hello-gallery"></a>Merhaba Galerisi'nden Clarizen ekleme
Azure AD'ye Clarizen tooconfigure hello tümleştirilmesi hello galeri tooyour listesinden yönetilen SaaS uygulamaları Clarizen ekleyin.

1. Merhaba, [Azure portal](https://portal.azure.com), buna hello sol bölmesinde, hello tıklatın **Azure Active Directory** simgesi.

    ![Azure Active Directory simgesi][1]

2. Tıklatın **kurumsal uygulamalar**. Ardından **tüm uygulamaları**.

    !["Kurumsal uygulamalar" ve "Tüm uygulamalar" ı tıklatarak][2]

3. Merhaba tıklatın **Ekle** hello hello iletişim kutusunun üstündeki düğmesini.

    ![Merhaba "Ekle" düğmesi][3]

4. Merhaba arama kutusuna yazın **Clarizen**.

    ![Merhaba arama kutusuna "Clarizen"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. Merhaba sonuçlar bölmesinde seçin **Clarizen**ve ardından **Ekle** tooadd Merhaba uygulaması.

    ![Merhaba sonuçlar bölmesinde Clarizen seçme](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme
Aşağıdaki bölümlerde hello, yapılandırmak ve Azure AD çoklu oturum açma hello test kullanıcıya Britta Simon bağlı Clarizen test.

Tek toowork'ın oturum açma hangi hello karşılık gelen Clarizen içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Clarizen hello arasında bir bağlantı ilişkisi kurulan toobe gerekir. Merhaba değerini atayarak bu bağlantı ilişkisini kurmak **kullanıcı adı** hello değeri olarak Azure AD'de **kullanıcıadı** Clarizen içinde.

tooconfigure ve Azure AD çoklu oturum açmayı test Clarizen, yapı taşları aşağıdaki tam hello ile:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  Britta Simon ile Azure AD çoklu oturum açma tootest.
3. **[Clarizen test kullanıcısı oluşturma](#create-a-clarizen-test-user)**  toohave Britta Simon her bağlantılı toohello Azure AD gösterimidir Clarizen içinde karşılık gelen.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın
Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Clarizen uygulamanızda yapılandırın.

1. Hello hello üzerinde Azure portal'ın **Clarizen** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    !["Çoklu oturum açma" a tıklayarak][4]

2. Merhaba, **çoklu oturum açma** iletişim kutusu için **modu**seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.

    !["SAML tabanlı oturum açma" seçme](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. Merhaba, **Clarizen etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Tanımlayıcı ve yanıt URL'si için kutuları](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    a. Merhaba, **tanımlayıcısı** kutusunda türü hello değeri olarak: **Clarizen**

    b. Merhaba, **yanıt URL'si** desen aşağıdaki hello kullanarak bir URL yazın: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**

    > [!NOTE]
    > Bunlar hello gerçek değerleri değildir. Toouse hello gerçek tanımlayıcısına sahip ve URL yanıtlayın. Burada tanımlayıcı hello gibi hello benzersiz bir dize değerini kullanmak öneririz. tooget hello gerçek değerler, kişi hello [Clarizen destek ekibi](https://success.clarizen.com/hc/en-us/requests/new).

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **yeni sertifika oluştur**.

    !["Yeni Sertifika Oluştur" a tıklayarak](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. Merhaba, **yeni sertifika oluştur** iletişim kutusunda, hello takvim simgesini tıklatın ve bir sona erme tarihi seçin. Daha sonra **Kaydet**'e tıklayın.

    ![Seçme ve sona erme tarihi kaydetme](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. Merhaba, **SAML imzalama sertifikası** bölümünde, select **yeni sertifika etkin hale getirin**ve ardından **kaydetmek**.

    ![Merhaba yeni sertifika etkin hale getirme için Hello onay kutusu seçme](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. Merhaba, **geçiş sertifikası** iletişim kutusu, tıklatın **Tamam**.

    !["Tamam" toomake hello sertifika etkin istediğiniz tooconfirm tıklatarak](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. Merhaba, **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    !["Sertifika (Base64)" toostart hello Yükle'yi tıklatarak](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. Merhaba, **Clarizen yapılandırma** 'yi tıklatın **yapılandırma Clarizen** tooopen hello **yapılandırma oturum açma** penceresi.

    !["Clarizen Yapılandır" a tıklayarak](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    !["Oturum açma yapılandırma" penceresinde, dosyaları ve URL'leri dahil](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. Farklı web tarayıcısı penceresinde tooyour Clarizen şirket sitede yönetici olarak oturum açın.

11. Kullanıcı adınıza tıklayın ve ardından **ayarları**.

    ![Kullanıcı adınızı "Ayarlar"'ı tıklatarak](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "ayarları")

12. Merhaba tıklatın **genel ayarları** sekmesi. Ardından, sonraki çok**şirket dışı kimlik doğrulaması**, tıklatın **Düzenle**.

    !["Genel ayarları" sekmesini](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "genel ayarları")

13. Merhaba, **şirket dışı kimlik doğrulaması** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:

    !["Federe kimlik doğrulaması" iletişim kutusu](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "şirket dışı kimlik doğrulaması")

    a. Seçin **etkinleştir federe kimlik doğrulaması**.

    b. Tıklatın **karşıya** tooupload indirilen sertifikanızı.

    c. Merhaba, **oturum açma URL'si** kutusuna, hello değerini girin **SAML çoklu oturum açma hizmet URL'si** hello Azure AD uygulama yapılandırma penceresinden.

    d. Merhaba, **Sign-out URL** kutusuna, hello değerini girin **Sign-Out URL** hello Azure AD uygulama yapılandırma penceresinden.

    e. Seçin **POST kullanmak**.

    f. **Kaydet** düğmesine tıklayın.

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Hello Azure portal, Britta Simon adlı bir test kullanıcısı oluşturun.

![Hello Azure AD test kullanıcı adı ve e-posta adresi][100]

1. Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** simgesi.

    ![Azure Active Directory simgesi](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. Tıklatın **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. Merhaba iletişim kutusunun Hello üstünde tıklatın **Ekle** tooopen hello **kullanıcı** iletişim kutusu.

    ![Merhaba "Ekle" düğmesi](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:

    !["Kullanıcı" iletişim kutusu adı, e-posta adresi ve parola ile doldurulur](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    a. Merhaba, **adı** kutusuna **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** kutusunda hello Britta Simon hesap türü hello e-posta adresi.

    c. Seçin **Göster parola** ve hello değerini yazmak **parola**.

    d. **Oluştur**'a tıklayın.

### <a name="create-a-clarizen-test-user"></a>Clarizen test kullanıcısı oluşturma
tooenable Azure AD kullanıcıların toosign tooClarizen içinde kullanıcı hesapları hazırlamanız gerekir. Clarizen Hello durumda sağlama bir el ile bir görevdir.

1. İçinde tooyour Clarizen şirket site yönetici olarak oturum açın.

2. Tıklatın **kişiler**.

    !["Kişiler" tıklatarak](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "kişiler")

3. Tıklatın **davet kullanıcı**.

    !["Kullanıcı davet" düğmesine](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "kullanıcıları davet et")

4. Merhaba, **kişileri davet** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:

    !["Kişileri davet edin" iletişim kutusu](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "kişileri davet edin")

    a. Merhaba, **e-posta** kutusunda hello Britta Simon hesap türü hello e-posta adresi.

    b. Tıklatın **davet**.

    > [!NOTE]
    > Hello Azure Active Directory hesap sahibi bir e-posta almak ve bunu etkinleştirilmeden önce bağlantı tooconfirm hesaplarında izleyin.

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın
Her erişim tooClarizen vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Atanan test kullanıcısı][200]

1. Hello Azure portal, hello uygulamaları görünümü Aç, toohello dizin görünümü göz atın, tıklatın **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.

    !["Kurumsal uygulamalar" ve "Tüm uygulamalar" ı tıklatarak][201]

2. Merhaba uygulamalar listesinde **Clarizen**.

    ![Merhaba listesinde Clarizen seçme](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. Merhaba sol bölmede **kullanıcılar ve gruplar**.

    !["Kullanıcılar ve Gruplar" a tıklayarak][202]

4. Merhaba tıklatın **Ekle** düğmesi. Ardından hello **eklemek atama** iletişim kutusunda **kullanıcılar ve gruplar**.

    ![Hello "Ekle" düğmesi ve hello "Atama Ekle" iletişim kutusu][203]

5. Merhaba, **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcılar hello listesinde.

6. Merhaba, **kullanıcılar ve gruplar** iletişim kutusunda, hello **seçin** düğmesi.

7. Merhaba, **eklemek atama** iletişim hello kutusunda, **atamak** düğmesi.

### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin
Azure AD çoklu oturum açma yapılandırmanızı hello erişim paneli kullanarak sınayın.

Merhaba Clarizen hello erişim paneli parçasında tıklattığınızda tooyour Clarizen uygulama otomatik olarak imzalanmalıdır.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi Azure Active Directory ile toointegrate SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
