---
title: "Öğretici: Azure Active Directory Tümleştirme ile LinkedInSalesNavigator | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile LinkedInSalesNavigator arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7a9fa8f3-d611-4ffe-8d50-04e9586b24da
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 443d302d40d7af16aba5114e00963f23ea8d12d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-sales-navigator"></a>Öğretici: Azure Active Directory Tümleştirme ile LinkedIn satış Gezgini

Bu öğreticide, bilgi nasıl toointegrate LinkedIn satış Gezgini Azure Active Directory'ye (Azure AD).

LinkedIn satış Gezgini Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooLinkedIn satış Gezgini sahip Azure AD'de kontrol edebilirsiniz
- Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooLinkedIn satış Gezgini (çoklu oturum açma) etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow isterseniz, Gözat [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure LinkedIn satış Gezgini ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir LinkedIn satış Gezgini çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmaktan kaçının.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. LinkedIn satış Gezgini hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-linkedin-sales-navigator-from-hello-gallery"></a>LinkedIn satış Gezgini hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme LinkedIn satış Gezgini, tooadd LinkedIn satış Gezgini hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd LinkedIn satış Gezgini hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **yeni uygulama** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **LinkedIn satış Gezgini**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_search.png)

5. Merhaba Sonuçlar panelinde seçin **LinkedIn satış Gezgini**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma LinkedIn satış "Britta Simon" adlı bir test kullanıcı tabanlı Gezgini ile test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen LinkedIn satış Gezgininde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve LinkedIn satış Gezgininde hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** LinkedIn satış Gezgininde.

tooconfigure ve Azure AD çoklu oturum açma LinkedIn satış Gezgini ile test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on) ** -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user) ** -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Bir LinkedIn satış Gezgini test kullanıcısı oluşturma](#creating-a-linkedin-sales-navigator-test-user) ** -toohave karşılık gelen, Britta Simon LinkedIn satış Gezgininde, hello kullanıcı bağlantılı toohello Azure AD gösterimidir.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on) ** -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma LinkedIn satış Gezgini uygulamanızda yapılandırın.

**Azure AD çoklu oturum açma tooconfigure LinkedIn satış Gezgini ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **LinkedIn satış Gezgini** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim, **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_samlbase.png)

3. Farklı bir web tarayıcısı penceresinde, oturum açma tooyour **LinkedIn satış Gezgini** yönetici olarak Web sitesi.

4. İçinde **hesap Merkezi'nde**, tıklatın **genel ayarları** altında **ayarları**. Ayrıca, seçin **satış Gezgini** hello aşağı açılan listeden.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_01.png)

5. Tıklatın **veya burayı tıklatın tooload ve kopyalama tek tek alanların hello formundan** kopyalayıp **varlık kimliği** ve **onaylama tüketici erişim (ACS) Url**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_031.png)

6. Azure Portal'da altında **LinkedIn satış Gezgini etki alanı ve URL'leri** bölümünde, hello tooconfigure hello uygulamada istiyorsanız aşağıdaki adımları gerçekleştirin **IDP** modunda başlatılır.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url1.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, hello girin **varlık kimliği** LinkedIn portalından kopyalandığından 

    b. Merhaba, **yanıt URL'si** metin kutusuna, hello girin **onaylama tüketici erişim (ACS) Url** LinkedIn portalından kopyalandığından

7. Denetleyin **Göster Gelişmiş URL ayarları**, tooconfigure hello uygulamada istiyorsanız **SP** modunda başlatılır.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url2.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, desen aşağıdaki hello kullanarak türü hello değeri:`https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`

8. **LinkedIn satış Gezgini** uygulama tooadd özel öznitelik eşlemelerini tooyour SAML belirteci öznitelikleri yapılandırma gerektiren belirli bir biçimde, hello SAML onaylar bekler. Aşağıdaki ekran görüntüsü hello bir örneği gösterir. Merhaba varsayılan değerini **kullanıcı tanımlayıcısı** olan **user.userprincipalname** ancak LinkedIn satış Gezgini, hello kullanıcının e-posta adresiyle eşleşen toobe bekliyor. Kullanabileceğiniz **user.mail** özniteliği hello listeden veya kuruluş yapılandırmanızı temel alarak hello uygun öznitelik değeri kullanın. 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/updateusermail.png)
    
9. İçinde **kullanıcı öznitelikleri** 'yi tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** ve hello özniteliklerini ayarlayın. Merhaba kullanıcının ihtiyacı tooadd dört talep adlı **e-posta**, **departmanı**, **firstname**, ve **lastname** ve hello değeri ile eşleşen toobe **user.mail**, **user.department**, **user.givenname**, ve **user.surname** sırasıyla

    | Öznitelik adı | Öznitelik değeri |
    | --- | --- |    
    | E-posta| User.Mail |
    | Bölüm| User.Department |
    | FirstName| User.givenName |
    | Soyadı| User.surname |
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/userattribute.png)
    
    a. Tıklayın **özniteliği eklemek** tooopen hello özniteliği iletişim.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_04.png)
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_05.png)
   
    b. Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.
    
    c. Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.
    
    d. Tıklatın **Tamam**

10. Merhaba hello üzerinde aşağıdaki adımları gerçekleştirin **adı** öznitelik -

    a. Tıklatın hello özniteliği tooopen hello üzerinde **öznitelik Düzenle** penceresi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/url_update.png)

    b. Hello Hello URL değeri Sil **ad alanı**.
    
    c. Tıklatın **Tamam** toosave hello ayarı.

11. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_certificate.png) 

12. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_400.png)

13. Çok Git**LinkedIn yönetici ayarları** bölümü. Tıklatın **karşıya yükleme XML dosyası** tooupload hello hello Azure portal ' indirmiş meta veri XML dosyası.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_metadata_03.png)

14. Tıklatın **üzerinde** tooenable SSO. SSO durumu değişir **bağlı** çok**bağlandı**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_05.png)


> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere ** Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_01.png) 

2. Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_02.png) 

3. Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-linkedin-sales-navigator-test-user"></a>Bir LinkedIn satış Gezgini test kullanıcısı oluşturma

Bağlantılı satış Gezgin uygulaması sadece kullanıcı zamanı (JIT) sağlama ve kimlik doğrulama kullanıcılar hello uygulamada otomatik olarak oluşturulduktan sonra destekler. Etkinleştirme **otomatik olarak lisansları atama** tooassign lisans toohello kullanıcı.
   
   ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooLinkedIn satış Gezgini vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooLinkedIn satış Gezgini hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **LinkedIn satış Gezgini**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba LinkedIn satış Gezgini hello erişim paneli parçasında tıklattığınızda yeniden yönlendirilen tooOrganizational sayfa tooprovide sahip olduğu kişisel LinkedIn hesap bilgilerinizi olmalıdır. Kişisel hesabınızı LinkedIn iş hesabınızla bağlar. Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_203.png

