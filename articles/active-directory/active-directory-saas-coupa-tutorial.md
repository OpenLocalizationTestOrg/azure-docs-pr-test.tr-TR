---
title: "Öğretici: Azure Active Directory Tümleştirme ile Coupa | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Coupa arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2017
ms.author: jeedes
ms.openlocfilehash: 30149f181d8b0ebdc1ae6820da5d561f3a942fa3
ms.sourcegitcommit: aaba209b9cea87cb983e6f498e7a820616a77471
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/12/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a>Öğretici: Azure Active Directory Tümleştirme Coupa ile

Bu öğreticide, Azure Active Directory (Azure AD) ile Coupa tümleştirmek öğrenin.

Coupa Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:

- Coupa erişimi, Azure AD'de kontrol edebilirsiniz.
- Otomatik olarak için Coupa (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

Azure AD tümleştirme Coupa ile yapılandırmak için aşağıdaki öğeleri gerekir:

- Bir Azure AD aboneliği
- Bir Coupa çoklu oturum açma abonelik etkin

> [!NOTE]
> Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:

1. Galeriden Coupa ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-coupa-from-the-gallery"></a>Galeriden Coupa ekleme
Azure AD Coupa tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Coupa eklemeniz gerekir.

**Galeriden Coupa eklemek için aşağıdaki adımları gerçekleştirin:**

1. İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi. 

    ![Azure Active Directory düğmesi][1]

2. Gidin **kurumsal uygulamalar**. Ardından **tüm uygulamaları**.

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.

    ![Yeni Uygulama düğmesi][3]

4. Arama kutusuna **Coupa**seçin **Coupa** sonuç panelinden ardından **Ekle** uygulama eklemek için düğmeyi.

    ![Sonuçlar listesinde Coupa](./media/active-directory-saas-coupa-tutorial/tutorial_coupa_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Coupa sınayın.

Tekli çalışmaya oturum için Azure AD Coupa karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister. Diğer bir deyişle, bir Azure AD kullanıcısının Coupa ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.

Coupa içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.

Yapılandırma ve Azure AD çoklu oturum açma Coupa ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.
3. **[Coupa test kullanıcısı oluşturma](#create-a-coupa-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Coupa sağlamak için.
4. **[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Coupa uygulamanızda yapılandırın.

**Azure AD çoklu oturum açma ile Coupa yapılandırmak için aşağıdaki adımları gerçekleştirin:**

1. Azure portalında üzerinde **Coupa** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-coupa-tutorial/tutorial_coupa_samlbase.png)

3. Üzerinde **Coupa etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:

    ![Coupa etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-coupa-tutorial/tutorial_coupa_url.png)

    a. İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`http://<companyname>.Coupa.com`

    b. İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`<companyname>.coupahost.com`

    c. İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.coupahost.com/sp/ACS.saml2`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu değerler, gerçek oturum açma URL'si tanımlayıcısı ve yanıt URL'si ile güncelleştirin. Kişi [Coupa istemci destek ekibi](https://success.coupa.com/Support/Contact_Us?) bu değerleri almak için. öğreticide daha sonra açıklanan meta verilerden yanıt URL değeri alırsınız.

4. Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.

    ![Sertifika indirme bağlantısı](./media/active-directory-saas-coupa-tutorial/tutorial_coupa_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-coupa-tutorial/tutorial_general_400.png)

6. Coupa şirket sitenize yönetici olarak oturum açma.

7. Git **Kurulum \> güvenlik denetimi**.
   
   ![Güvenlik denetimleri](./media/active-directory-saas-coupa-tutorial/ic791900.png "güvenlik denetimleri")

8. İçinde **Coupa kimlik bilgilerini kullanarak oturum** bölümünde, aşağıdaki adımları gerçekleştirin:

    ![Coupa SP meta veri](./media/active-directory-saas-coupa-tutorial/ic791901.png "Coupa SP meta verileri")
    
    a. Seçin **SAML kullanarak oturum**.
    
    b. Bilgisayarınıza Coupa meta veri dosyası indirmek için tıklayın **karşıdan yükleme ve SP meta verileri içeri aktarma**. meta veri açıp kopyalama **AssertionConsumerService dizin/URL** değeri, değerin içine yapıştırma **yanıt URL'si** metin kutusuna **Coupa etki alanı ve URL'leri** bölümü. 
    
    c. Tıklatın **Gözat** Azure portalından indirdiğiniz meta veriler karşıya yüklemek için.
    
    d. **Kaydet** düğmesine tıklayın.

> [!TIP]
> Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!  Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm. Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.

   ![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**

1. Sol bölmede, Azure portal'ı tıklatın **Azure Active Directory** düğmesi.

    ![Azure Active Directory düğmesi](./media/active-directory-saas-coupa-tutorial/create_aaduser_01.png)

2. Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-coupa-tutorial/create_aaduser_02.png)

3. Açmak için **kullanıcı** iletişim kutusu, tıklatın **Ekle** en üstündeki **tüm kullanıcılar** iletişim kutusu.

    ![Ekle düğmesi](./media/active-directory-saas-coupa-tutorial/create_aaduser_03.png)

4. İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:

    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-coupa-tutorial/create_aaduser_04.png)

    a. İçinde **adı** kutusuna **BrittaSimon**.

    b. İçinde **kullanıcı adı** kullanıcı Britta Simon e-posta adresini yazın.

    c. Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-a-coupa-test-user"></a>Coupa test kullanıcısı oluşturma

Azure AD kullanıcıların Coupa oturum etkinleştirmek için bunların Coupa sağlanmalıdır.  

* Coupa söz konusu olduğunda, sağlama bir el ile bir görevdir.

**Kullanıcı sağlamayı yapılandırmak için aşağıdaki adımları gerçekleştirin:**

1. Oturum, **Coupa** yönetici olarak şirket site.

2. Üstteki menüde tıklatın **Kurulum**ve ardından **kullanıcılar**.
   
   ![Kullanıcıların](./media/active-directory-saas-coupa-tutorial/ic791908.png "kullanıcılar")

3. **Oluştur**'a tıklayın.
   
   ![Kullanıcılar oluşturma](./media/active-directory-saas-coupa-tutorial/ic791909.png "kullanıcıları oluşturun")

4. İçinde **kullanıcı oluşturma** bölümünde, aşağıdaki adımları gerçekleştirin:
   
   ![Kullanıcı ayrıntılarını](./media/active-directory-saas-coupa-tutorial/ic791910.png "kullanıcı ayrıntıları")
   
   a. Tür **oturum açma**, **ad**, **Soyadı**, **tek oturum açma kimliği**, **e-posta** özniteliklerini bir Geçerli bir Azure Active Directory hesabı ilgili metin kutularına içine sağlamak istiyorsunuz.

   b. **Oluştur**'a tıklayın.   
   
   >[!NOTE]
   >Azure Active Directory hesap sahibi etkin duruma gelmesi hesabı onaylamak için bir bağlantı içeren bir e-posta alırsınız. 
   > 

>[!NOTE]
>API sağlama AAD kullanıcı hesaplarına Coupa tarafından sağlanan veya herhangi diğer Coupa kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz. 

### <a name="assign-the-azure-ad-test-user"></a>Azure AD test kullanıcısı atayın

Bu bölümde, Britta Coupa için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.

![Kullanıcı rolü atayın][200] 

**Coupa için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**

1. Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Uygulamalar listesinde **Coupa**.

    ![Uygulamalar listesinde Coupa bağlantı](./media/active-directory-saas-coupa-tutorial/tutorial_coupa_app.png)  

3. Soldaki menüde tıklatın **kullanıcılar ve gruplar**.

    !["Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Ekleme atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Erişim paneli Coupa parçasında tıklattığınızda, otomatik olarak Coupa uygulamanıza açan.
Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_203.png

