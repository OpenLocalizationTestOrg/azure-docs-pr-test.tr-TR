---
title: "Öğretici: Azure Active Directory Tümleştirme ile LinkedIn öğrenme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve LinkedIn öğrenme arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 14610a25132ed0ccf5892cad6ccc4e1ef03ff280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a>Öğretici: Azure Active Directory Tümleştirme ile LinkedIn öğrenme

Bu öğreticide, bilgi nasıl toointegrate LinkedIn öğrenme Azure Active Directory'ye (Azure AD).

LinkedIn öğrenme Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooLinkedIn sahip Azure AD'de denetleyebilirsiniz öğrenme
- Oturum açma, kullanıcıların tooautomatically get tooLinkedIn etkinleştirebilirsiniz (çoklu oturum açma) Azure AD hesaplarına sahip öğrenme
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure LinkedIn öğrenme ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir LinkedIn öğrenme çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. LinkedIn öğrenme hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-linkedin-learning-from-hello-gallery"></a>LinkedIn öğrenme hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme LinkedIn öğrenme tooadd LinkedIn öğrenme hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd LinkedIn öğrenme hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **Ekle** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **LinkedIn öğrenme**. Sonuçları panelinden tıklatın **LinkedIn öğrenme** tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma LinkedIn "Britta Simon" adlı bir test kullanıcı tabanlı Learning ile test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen LinkedIn learning'de tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı LinkedIn öğrenme hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** LinkedIn learning'de.

tooconfigure ve LinkedIn Learning ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Bir LinkedIn öğrenme test kullanıcısı oluşturma](#creating-a-linkedin-learning-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma LinkedIn öğrenme uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma LinkedIn Learning ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **LinkedIn öğrenme** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. Bir farklı web tarayıcısı penceresinde, bir yönetici olarak oturum açma tooyour LinkedIn öğrenme Kiracı.

4. İçinde **hesap Merkezi'nde**, tıklatın **genel ayarları** altında **ayarları**. Ayrıca, seçin **öğrenme - varsayılan** hello aşağı açılan listeden.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. Tıklatın **veya burayı tıklatın tooload ve kopyalama tek tek alanların hello formundan** kopyalayıp **varlık kimliği** ve **onaylama tüketici erişim (ACS) URL'si**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. Azure Portal'da altında **LinkedIn öğrenme etki alanı ve URL'leri**, hello tooconfigure SSO istiyorsanız aşağıdaki adımları gerçekleştirin içinde **IDP başlatılan** modu

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, hello girin **varlık kimliği** LinkedIn portalından kopyalandığından 

    b. Merhaba, **yanıt URL'si** metin kutusuna, hello girin **onaylama tüketici erişim (ACS) Url** LinkedIn portalından kopyalandığından

7. Tooconfigure SSO istiyorsanız içinde **SP tarafından başlatılan**, ardından hello yapılandırma bölümündeki Gelişmiş URL Göster ayarı seçeneğini tıklatın ve desen aşağıdaki hello ile hello oturum açma URL'si yapılandırın:

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. LinkedIn öğrenme uygulamanızı hello SAML onaylar, tooadd özel öznitelik eşlemelerini tooyour SAML belirteci öznitelikleri yapılandırma gerektiren belirli bir biçimde, bekliyor. Ekran aşağıdaki hello bunun bir örneği gösterir. Merhaba varsayılan değerini **kullanıcı tanımlayıcısı** olan **user.userprincipalname** ancak LinkedIn öğrenme hello kullanıcının e-posta adresiyle eşleşen bu toobe bekliyor. Bunun için kullanabileceğiniz **user.mail** özniteliği hello listeden veya kuruluş yapılandırmanızı temel alarak hello uygun öznitelik değeri kullanın. 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. İçinde **kullanıcı öznitelikleri** 'yi tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** ve hello özniteliklerini ayarlayın. Merhaba kullanıcının ihtiyacı tooadd dört talep adlı **e-posta**, **departmanı**, **firstname**, ve **lastname** ve hello değeri ile eşleşen toobe **user.mail**, **user.department**, **user.givenname**, ve **user.surname** sırasıyla

    | Öznitelik adı | Öznitelik değeri |
    | --- | --- |
    | E-posta| User.Mail |    
    | Bölüm| User.Department |
    | FirstName| User.givenName |
    | Soyadı| User.surname |
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    a. Tıklatın **özniteliği eklemek** tooopen hello özniteliği iletişim.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    b. Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.
    
    c. Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.
    
    d. Tıklatın **Tamam**

10. Merhaba hello üzerinde aşağıdaki adımları gerçekleştirin **adı** öznitelik -

    a. Tıklatın hello özniteliği tooopen hello üzerinde **öznitelik Düzenle** penceresi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    b. Hello Hello URL değeri Sil **ad alanı**.
    
    c. Tıklatın **Tamam** toosave hello ayarı.

11. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. **Kaydet** düğmesine tıklayın.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. Çok Git**LinkedIn yönetici ayarları** bölümü. Merhaba karşıya yükleme XML dosyası seçeneğini tıklatarak hello Azure portal ' yüklenen hello XML dosyasını karşıya yükleyin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. Tıklatın **üzerinde** tooenable SSO. SSO durumu değişir **bağlı** çok**bağlandı**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın. 

### <a name="creating-a-linkedin-learning-test-user"></a>Bir LinkedIn öğrenme test kullanıcısı oluşturma

Bağlantılı öğrenme uygulama destekler. Yalnızca zaman kullanıcı sağlama ve kimlik doğrulamasından sonra kullanıcılar hello uygulamada otomatik olarak oluşturulur. Merhaba yönetici ayarları sayfasında hello LinkedIn öğrenme portal Çevir hello anahtar **otomatik olarak ata lisansları** zaman sağlama sadece tooactive tooenable ve bu ayrıca atamak lisans toohello kullanıcı.
   
   ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, Azure çoklu oturum açma Britta Simon toouse erişim tooLinkedIn vererek etkinleştirmeniz öğrenme.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooLinkedIn öğrenme, hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **LinkedIn öğrenme**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba LinkedIn öğrenme hello erişim paneli parçasında tıklattığınızda hello Azure oturum açma sayfasına almanız gerekir ve üzerinde başarılı oturum açma sonra bunu LinkedIn öğrenme uygulamanıza almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png