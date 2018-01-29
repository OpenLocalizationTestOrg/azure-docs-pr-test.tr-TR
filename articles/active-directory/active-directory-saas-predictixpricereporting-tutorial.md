---
title: "Öğretici: Azure Active Directory Tümleştirme Predictix Fiyat Raporlama ile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve fiyat Predictix raporlama arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 691d0c43-3aa1-4220-9e46-e7a88db234ad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: e8efedf016f007707d08ecca92f93a6844eadbd6
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-price-reporting"></a>Öğretici: Azure Active Directory Tümleştirme Predictix Fiyat Raporlama ile

Bu öğreticide, Azure Active Directory (Azure AD) ile tümleştirme Predictix Fiyat Raporlama öğrenin.

Azure AD ile tümleştirme Predictix Fiyat Raporlama ile aşağıdaki avantajları sağlar:

- Fiyat Predictix raporlama erişimi, Azure AD'de kontrol edebilirsiniz.
- Azure AD hesaplarına otomatik olarak Predictix fiyat raporlama için (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

Azure AD tümleştirme Predictix Fiyat Raporlama ile yapılandırmak için aşağıdaki öğeleri gerekir:

- Bir Azure AD aboneliği
- Bir fiyat Predictix raporlama çoklu oturum açma abonelik etkin

> [!NOTE]
> Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:

1. Fiyat Predictix raporlama Galeriden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-predictix-price-reporting-from-the-gallery"></a>Fiyat Predictix raporlama Galeriden ekleme
Azure AD Predictix Fiyat Raporlama tümleştirilmesi yapılandırmak için fiyat Predictix raporlama Galeriden yönetilen SaaS uygulamaları listenize eklemeniz gerekir.

**Fiyat Predictix raporlama Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**

1. İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi. 

    ![Azure Active Directory düğmesi][1]

2. Gidin **kurumsal uygulamalar**. Ardından **tüm uygulamaları**.

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.

    ![Yeni Uygulama düğmesi][3]

4. Arama kutusuna yazın **Predictix Fiyat Raporlama**seçin **Predictix Fiyat Raporlama** sonuç panelinden ardından **Ekle** uygulama eklemek için düğmeyi.

    ![Fiyat Predictix raporlama sonuçlar listesinde](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı fiyat Predictix Raporlama ile test etme.

Tekli çalışmaya oturum için Azure AD ne karşılık gelen Predictix Fiyat Raporlama bir kullanıcı için Azure AD içinde olduğu bilmek ister. Diğer bir deyişle, bir Azure AD kullanıcısının ile ilgili fiyat Predictix raporlama kullanıcı arasında bir bağlantı ilişki kurulması gerekir.

Fiyat Predictix raporlamada değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.

Yapılandırma ve Azure AD çoklu oturum açma Predictix Fiyat Raporlama ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.
3. **[Fiyat Predictix raporlama test kullanıcısı oluşturma](#create-a-predictix-price-reporting-test-user)**  - Predictix fiyat kullanıcı Azure AD gösterimini bağlantılı raporlama Britta Simon, karşılık gelen sağlamak için.
4. **[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Predictix Fiyat Raporlama uygulamanızda yapılandırın.

**Azure AD çoklu oturum açma Predictix Fiyat Raporlama ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**

1. Azure portalında üzerinde **Predictix Fiyat Raporlama** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_samlbase.png)

3. Üzerinde **Predictix fiyat raporlama etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:

    ![Predictix fiyat raporlama etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_url.png)

    a. İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname-pricing>.predictix.com/sso/request`

    b. İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:
    | |
    |--|
    | `https://<companyname-pricing>.predictix.com` |
    | `https://<companyname-pricing>.dev.predictix.com` |

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin. Kişi [Predictix fiyat raporlama istemcisi destek ekibi](http://www.infor.com/company/customer-center/) bu değerleri almak için. 
 
4. Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.

    ![Sertifika indirme bağlantısı](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_400.png)

6. Üzerinde **Predictix Fiyat Raporlama yapılandırma** 'yi tıklatın **Predictix fiyat bildirimini Yapılandır** açmak için **yapılandırma oturum açma** penceresi. Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**

    ![Predictix Fiyat Raporlama yapılandırma](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_configure.png) 

7. Çoklu oturum açma yapılandırmak için **Predictix Fiyat Raporlama** yan, indirilen göndermek için ihtiyacınız **sertifika (Base64)**, **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** için [Predictix Fiyat Raporlama destek ekibi](http://www.infor.com/company/customer-center/). Bunlar, her iki tarafta da ayarlamanızı SAML SSO bağlantı sağlamak için bu ayarı ayarlayın.

> [!TIP]
> Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!  Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm. Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.

   ![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**

1. Sol bölmede, Azure portal'ı tıklatın **Azure Active Directory** düğmesi.

    ![Azure Active Directory düğmesi](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_01.png)

2. Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_02.png)

3. Açmak için **kullanıcı** iletişim kutusu, tıklatın **Ekle** en üstündeki **tüm kullanıcılar** iletişim kutusu.

    ![Ekle düğmesi](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_03.png)

4. İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:

    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_04.png)

    a. İçinde **adı** kutusuna **BrittaSimon**.

    b. İçinde **kullanıcı adı** kullanıcı Britta Simon e-posta adresini yazın.

    c. Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-a-predictix-price-reporting-test-user"></a>Fiyat Predictix raporlama test kullanıcısı oluşturma

Bu bölümde, fiyat Predictix raporlamada Britta Simon adlı bir kullanıcı oluşturun. Çalışmak [Predictix Fiyat Raporlama destek ekibi](http://www.infor.com/company/customer-center/) Predictix Fiyat Raporlama platform kullanıcıları eklemek için.

### <a name="assign-the-azure-ad-test-user"></a>Azure AD test kullanıcısı atayın

Bu bölümde, Britta Predictix fiyat raporlama için erişim izni verme, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.

![Kullanıcı rolü atayın][200] 

**Fiyat Predictix Raporlama ile Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**

1. Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Uygulamalar listesinde **Predictix Fiyat Raporlama**.

    ![Uygulamalar listesinde fiyat Predictix raporlama bağlantı](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_app.png)  

3. Soldaki menüde tıklatın **kullanıcılar ve gruplar**.

    !["Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Ekleme atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Erişim paneli Predictix Fiyat Raporlama parçasında tıklattığınızda, otomatik olarak Predictix Fiyat Raporlama uygulamanıza açan.

## <a name="additional-resources"></a>Ek kaynaklar

* [Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_203.png

