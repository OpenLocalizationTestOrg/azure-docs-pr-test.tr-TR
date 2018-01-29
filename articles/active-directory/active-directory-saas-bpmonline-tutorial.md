---
title: "Öğretici: Azure Active Directory Tümleştirme ile Bpm'online | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Bpm'online arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 052db91d-ccff-4098-8ae3-2f76eca90539
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/16/2017
ms.author: jeedes
ms.openlocfilehash: 0214fcbdde886bd14d84917e496568027d417096
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bpmonline"></a>Öğretici: Azure Active Directory Tümleştirme Bpm'online ile

Bu öğreticide, Azure Active Directory (Azure AD) ile Bpm'online tümleştirmek öğrenin.

Bpm'online Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:

- Bpm'online erişimi, Azure AD'de kontrol edebilirsiniz.
- Otomatik olarak için Bpm'online (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

Azure AD tümleştirme Bpm'online ile yapılandırmak için aşağıdaki öğeleri gerekir:

- Bir Azure AD aboneliği
- Bir Bpm'online çoklu oturum açma etkin abonelik

> [!NOTE]
> Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:

1. Galeriden Bpm'online ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-bpmonline-from-the-gallery"></a>Galeriden Bpm'online ekleme
Azure AD Bpm'online tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Bpm'online eklemeniz gerekir.

**Galeriden Bpm'online eklemek için aşağıdaki adımları gerçekleştirin:**

1. İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi. 

    ![Azure Active Directory düğmesi][1]

2. Gidin **kurumsal uygulamalar**. Ardından **tüm uygulamaları**.

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.

    ![Yeni Uygulama düğmesi][3]

4. Arama kutusuna **Bpm'online**seçin **Bpm'online** sonuç panelinden ardından **Ekle** uygulama eklemek için düğmeyi.

    ![Sonuçlar listesinde Bpm'online](./media/active-directory-saas-bpmonline-tutorial/tutorial_bpmonline_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve test Azure AD çoklu oturum açma Bpm'online ile "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı

Tekli çalışmaya oturum için Azure AD Bpm'online karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister. Diğer bir deyişle, bir Azure AD kullanıcısının Bpm'online ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.

Bpm'online içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.

Yapılandırma ve Azure AD çoklu oturum açma Bpm'online ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.
3. **[Bpm'online test kullanıcısı oluşturma](#create-a-bpmonline-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Bpm'online sağlamak için.
4. **[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Bpm'online uygulamanızda yapılandırın.

**Azure AD çoklu oturum açma ile Bpm'online yapılandırmak için aşağıdaki adımları gerçekleştirin:**

1. Azure portalında üzerinde **Bpm'online** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-bpmonline-tutorial/tutorial_bpmonline_samlbase.png)

3. Üzerinde **Bpm'online etki alanı ve URL'leri** bölümünde, uygulamada yapılandırmak istiyorsanız aşağıdaki adımları gerçekleştirin **IDP** modu tarafından başlatılan:

    ![Bpm'online etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-bpmonline-tutorial/tutorial_bpmonline_url.png)

    a. İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<client site name>.bpmonline.com/`

    b. İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<client site name>.bpmonline.com/ServiceModel/AuthService.svc/SsoLogin`

4. Denetleme **Göster Gelişmiş URL ayarları** ve uygulamada yapılandırmak istiyorsanız aşağıdaki adımı gerçekleştirin **SP** modunda başlatılan:

    ![Bpm'online etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-bpmonline-tutorial/tutorial_bpmonline_url1.png)

    İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<client site name>.bpmonline.com/`
     
    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu değerler, gerçek tanımlayıcı, yanıt URL'si ve oturum açma URL'si ile güncelleştirin. Kişi [Bpm'online istemci destek ekibi](mailto:support@bpmonline.com) bu değerleri almak için. 

5. Oluşturulacak **meta veri** url, aşağıdaki adımları gerçekleştirin:

    a. Tıklatın **uygulama kayıtlar**.
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bpmonline-tutorial/tutorial_bpmonline_appregistrations.png)
   
    b. Tıklatın **uç noktaları** açmak için **uç noktaları** iletişim kutusu.  
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bpmonline-tutorial/tutorial_bpmonline_endpointicon.png)

    c. Kopyalamak için Kopyala düğmesini tıklatın **FEDERASYON meta veri belgesi** URL'yi kopyalayıp Not Defteri'ne yapıştırın.
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bpmonline-tutorial/tutorial_bpmonline_endpoint.png)
     
    d. Şimdi özellik sayfasına gidin **Bpm'online** ve kopyalama **uygulama kimliği** kullanarak **kopyalama** düğmesine tıklayın ve Not Defteri'ne yapıştırın.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bpmonline-tutorial/tutorial_bpmonline_appid.png)

     e. Oluştur **meta veri URL'sini** şu biçimi kullanarak:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>` 

6. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-bpmonline-tutorial/tutorial_general_400.png)
    
8. Çoklu oturum açma yapılandırmak için **Bpm'online** yan, ihtiyacınız göndermek **meta veri URL'sini** için [Bpm'online destek ekibi](mailto:support@bpmonline.com). Bunlar, her iki tarafta da ayarlamanızı SAML SSO bağlantı sağlamak için bu ayarı ayarlayın.

> [!TIP]
> Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!  Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm. Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.

   ![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**

1. Sol bölmede, Azure portal'ı tıklatın **Azure Active Directory** düğmesi.

    ![Azure Active Directory düğmesi](./media/active-directory-saas-bpmonline-tutorial/create_aaduser_01.png)

2. Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-bpmonline-tutorial/create_aaduser_02.png)

3. Açmak için **kullanıcı** iletişim kutusu, tıklatın **Ekle** en üstündeki **tüm kullanıcılar** iletişim kutusu.

    ![Ekle düğmesi](./media/active-directory-saas-bpmonline-tutorial/create_aaduser_03.png)

4. İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:

    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-bpmonline-tutorial/create_aaduser_04.png)

    a. İçinde **adı** kutusuna **BrittaSimon**.

    b. İçinde **kullanıcı adı** kullanıcı Britta Simon e-posta adresini yazın.

    c. Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-a-bpmonline-test-user"></a>Bpm'online test kullanıcısı oluşturma

Bu bölümde, Bpm'online içinde Britta Simon adlı bir kullanıcı oluşturun. Çalışmak [Bpm'online destek ekibi](mailto:support@bpmonline.com) Bpm'online platform kullanıcıları eklemek için. Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir. 

### <a name="assign-the-azure-ad-test-user"></a>Azure AD test kullanıcısı atayın

Bu bölümde, Britta Bpm'online için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.

![Kullanıcı rolü atayın][200] 

**Bpm'online için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**

1. Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Uygulamalar listesinde **Bpm'online**.

    ![Uygulamalar listesinde Bpm'online bağlantı](./media/active-directory-saas-bpmonline-tutorial/tutorial_bpmonline_app.png)  

3. Soldaki menüde tıklatın **kullanıcılar ve gruplar**.

    !["Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Ekleme atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Erişim paneli Bpm'online parçasında tıklattığınızda, otomatik olarak Bpm'online uygulamanıza açan.
Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bpmonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bpmonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bpmonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bpmonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bpmonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bpmonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bpmonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bpmonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bpmonline-tutorial/tutorial_general_203.png

