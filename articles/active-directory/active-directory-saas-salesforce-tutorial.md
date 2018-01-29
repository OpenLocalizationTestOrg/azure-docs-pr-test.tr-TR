---
title: "Öğretici: Azure Active Directory Tümleştirme Salesforce ile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve Salesforce arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/15/2017
ms.author: jeedes
ms.openlocfilehash: ed127afbca5135ade21f6ac53d18d46e88939fd9
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a>Öğretici: Salesforce Azure Active Directory Tümleştirme

Bu öğreticide, Azure Active Directory (Azure AD) ile Salesforce tümleştirmek öğrenin.

Salesforce Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:

- Salesforce erişimi, Azure AD'de kontrol edebilirsiniz.
- Otomatik olarak Salesforce (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

Azure AD tümleştirme Salesforce ile yapılandırmak için aşağıdaki öğeleri gerekir:

- Bir Azure AD aboneliği
- Bir Salesforce çoklu oturum açma abonelik etkin

> [!NOTE]
> Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:

1. Salesforce Galeriden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-salesforce-from-the-gallery"></a>Salesforce Galeriden ekleme
Azure AD Salesforce tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Salesforce eklemeniz gerekir.

**Salesforce Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**

1. İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi. 

    ![Azure Active Directory düğmesi][1]

2. Gidin **kurumsal uygulamalar**. Ardından **tüm uygulamaları**.

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.

    ![Yeni Uygulama düğmesi][3]

4. Arama kutusuna **Salesforce**seçin **Salesforce** sonuç panelinden ardından **Ekle** uygulama eklemek için düğmeyi.

    ![Sonuçlar listesinde Salesforce](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Salesforce sınayın.

Tekli çalışmaya oturum için Azure AD Salesforce karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister. Diğer bir deyişle, bir Azure AD kullanıcısının Salesforce ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.

Salesforce içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.

Yapılandırma ve Azure AD çoklu oturum açma Salesforce ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.
3. **[Salesforce test kullanıcısı oluşturma](#create-a-salesforce-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Salesforce sağlamak için.
4. **[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Salesforce uygulamanızda yapılandırın.

**Azure AD çoklu oturum açma ile Salesforce yapılandırmak için aşağıdaki adımları gerçekleştirin:**

1. Azure portalında üzerinde **Salesforce** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. Üzerinde **Salesforce etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:

    ![Salesforce etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)
    
    a. İçinde **oturum açma URL'si** metin kutusuna, şu biçimi kullanarak değeri yazın:
    
    Kurumsal hesap:`https://<subdomain>.my.salesforce.com`

    Geliştirici hesabı:`https://<subdomain>-dev-ed.my.salesforce.com`
    
    b. İçinde **tanımlayıcısı** metin kutusuna, şu biçimi kullanarak değeri yazın:
    
    Kurumsal hesap:`https://<subdomain>.my.salesforce.com`

    Geliştirici hesabı:`https://<subdomain>-dev-ed.my.salesforce.com`
    
    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu değerleri tanımlayıcısı ve gerçek oturum açma URL'si ile güncelleştirin. Kişi [Salesforce istemci destek ekibi](https://help.salesforce.com/support) bu değerleri almak için.

4. Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika** ve sertifika dosyayı bilgisayarınıza kaydedin.

    ![Sertifika indirme bağlantısı](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. Üzerinde **Salesforce yapılandırma** 'yi tıklatın **yapılandırma Salesforce** açmak için **yapılandırma oturum açma** penceresi. Kopya **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**

    ![Salesforce yapılandırma](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 

7. Tarayıcı ve günlüğüne Salesforce yönetici hesabınız için yeni bir sekme açın.

8. Tıklayın **Kurulum** altında **ayarlar simgesine** sayfanın sağ üst köşesinde üzerinde.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/configure1.png)

9. Ekranı aşağı kaydırarak **ayarları** Gezinti bölmesinde **kimlik** ilgili bölümü genişletin. Ardından **çoklu oturum açma ayarları**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

10. Üzerinde **çoklu oturum açma ayarları** sayfasında, **Düzenle** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)
    
    > [!NOTE]
    > Salesforce hesabınız için çoklu oturum açma ayarlarını etkinleştirmek erişemiyorsanız başvurmanız gerekebilir [Salesforce istemci destek ekibi](https://help.salesforce.com/support). 

11. Seçin **SAML etkin**ve ardından **kaydetmek**.

      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
12. SAML çoklu oturum açma ayarlarınızı yapılandırmak için tıklatın **yeni**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

13. Üzerinde **SAML çoklu oturum açma ayarını Düzenle** sayfasında, aşağıdaki yapılandırmaları yapın:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    a. İçin **adı** alanına, bu yapılandırma için bir kolay ad yazın. İçin bir değer sağlama **adı** otomatik olarak doldurulması **API adı** metin kutusu.

    b. İçinde **veren** alan, değerini yapıştırın **SAML varlık kimliği**, hangi Azure portalından kopyalanır.

    c. İçinde **varlık kimliği textbox**, şu biçimi kullanarak Salesforce etki alanı adınızı yazın:
      
      * Kurumsal hesap:`https://<subdomain>.my.salesforce.com`
      * Geliştirici hesabı:`https://<subdomain>-dev-ed.my.salesforce.com`
      
    d. Karşıya yüklemek için **kimlik sağlayıcısı sertifikası**, tıklatın **Dosya Seç** göz atın ve Azure portalından indirdiğiniz sertifika dosyasını seçin.

    e. Olarak **SAML kimlik türü**, aşağıdaki seçeneklerden birini seçin:
    
      * Seçin **onaylamayı kullanıcının Salesforce kullanıcı adını içeren**, kullanıcının Salesforce kullanıcıadı SAML onayı geçirilirse

      * Seçin **onaylamayı içeren kullanıcı nesnesinden Federasyon kimliği**, Federasyon kimliği kullanıcı nesnesinden SAML onayı geçirilirse

      * Seçin **onaylamayı içeren kullanıcı nesnesi kullanım Kimliğinden**, kullanıcı kimliği kullanıcı nesnesinden SAML onayı geçirilirse

    f. İçin **SAML kimlik konumu**seçin **kimliktir konu deyimi NameIdentifier öğesinde**.

    g. İçin **hizmet sağlayıcısı tarafından başlatılan bağlama isteği**seçin **HTTP yeniden yönlendirme**.

    h. İçinde **kimlik sağlayıcısı oturum açma URL'si** metin değerini yapıştırın **çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan
    
    ı. Son olarak, tıklatın **kaydetmek** , SAML çoklu oturum açma ayarları uygulamak için.

14. Salesforce sol gezinti bölmesinde üzerinde tıklatın **şirket ayarları** ilgili bölümü genişletin ve ardından **My etki alanı**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

15. Ekranı aşağı kaydırarak **kimlik doğrulama Yapılandırması** bölüm ve'ı tıklatın **Düzenle** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

16. İçinde **kimlik doğrulama Yapılandırması** bölümünde, onay **oturum açma sayfasına** olarak **kimlik doğrulaması Servie** SAML SSO yapılandırma ve ardından  **Kaydet**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > Birden fazla kimlik doğrulama hizmeti seçili ise, kullanıcıların bunlar çoklu oturum açma Salesforce ortamınıza başlatma sırasında oturum açmak istiyor hangi kimlik doğrulama hizmeti seçmeniz istenir. Bunu olmasını istemiyorsanız sonra yapmanız gerekenler **diğer tüm kimlik doğrulama hizmetleri işaretlemeden bırakın**.

> [!TIP]
> Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!  Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm. Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.

   ![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**

1. Sol bölmede, Azure portal'ı tıklatın **Azure Active Directory** düğmesi.

    ![Azure Active Directory düğmesi](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png)

2. Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png)

3. Açmak için **kullanıcı** iletişim kutusu, tıklatın **Ekle** en üstündeki **tüm kullanıcılar** iletişim kutusu.

    ![Ekle düğmesi](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png)

4. İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:

    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png)

    a. İçinde **adı** kutusuna **BrittaSimon**.

    b. İçinde **kullanıcı adı** kullanıcı Britta Simon e-posta adresini yazın.

    c. Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-a-salesforce-test-user"></a>Salesforce test kullanıcısı oluşturma

Bu bölümde, Britta Simon adlı bir kullanıcı Salesforce'ta oluşturulur. Salesforce yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.
Bu bölümde, eylem öğe yok. Bir kullanıcı zaten Salesforce'ta yoksa, Salesforce erişmeyi denediğinde yeni bir tane oluşturulur.

### <a name="assign-the-azure-ad-test-user"></a>Azure AD test kullanıcısı atayın

Bu bölümde, Britta Salesforce erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.

![Kullanıcı rolü atayın][200] 

**Salesforce Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**

1. Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Uygulamalar listesinde **Salesforce**.

    ![Uygulamalar listesinde Salesforce bağlantı](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png)  

3. Soldaki menüde tıklatın **kullanıcılar ve gruplar**.

    !["Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Ekleme atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Erişim paneli Salesforce parçasında tıklattığınızda, otomatik olarak Salesforce uygulamanıza açan.
Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

