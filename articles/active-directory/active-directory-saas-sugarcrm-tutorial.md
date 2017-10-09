---
title: "Öğretici: Azure Active Directory Tümleştirme Sugar CRM ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Sugar CRM arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 108d2f8125e410743ee7bc48883a1d0b00602615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sugar-crm"></a>Öğretici: Sugar CRM Azure Active Directory Tümleştirme

Bu öğreticide, bilgi nasıl toointegrate Sugar CRM Azure Active Directory'ye (Azure AD).

Sugar CRM Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooSugar CRM sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooSugar CRM (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

Sugar CRM ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Sugar CRM çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Sugar CRM hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-sugar-crm-from-hello-gallery"></a>Sugar CRM hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme Sugar CRM tooadd Sugar CRM hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Sugar CRM hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Sugar CRM**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_search.png)

5. Merhaba Sonuçlar panelinde seçin **Sugar CRM**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Sugar "Britta Simon" adlı bir test kullanıcı tabanlı CRM ile test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen Sugar CRM'deki tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Sugar CRM hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Sugar CRM hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Sugar CRM ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Sugar CRM test kullanıcısı oluşturma](#creating-a-sugar-crm-test-user)**  -toohave karşılık gelen, Britta Simon Sugar CRM'deki bağlantılı toohello Azure AD kullanıcı gösterimidir.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Sugar CRM uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma Sugar CRM ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Sugar CRM** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_samlbase.png)

3. Merhaba üzerinde **Sugar CRM etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_url.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:
    | |
    |--|
    | `https://<companyname>.sugarondemand.com` |
    | `https://<companyname>.trial.sugarcrm` |

    > [!NOTE] 
    > Merhaba değeri gerçek değil. Güncelleştirme hello değerle hello gerçek oturum açma URL'si. Kişi [Sugar CRM istemci destek ekibi](https://support.sugarcrm.com/) tooget hello değeri. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **Sugar CRM Yapılandırma** 'yi tıklatın **yapılandırma Sugar CRM** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_configure.png) 

7. Farklı web tarayıcısı penceresinde tooyour Sugar CRM şirket sitede yönetici olarak oturum açın.

8. Çok Git**yönetici**.
   
    ![Yönetici](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "yönetici")

9. Merhaba, **Yönetim** 'yi tıklatın **parola yönetimi**.
   
    ![Yönetim](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Yönetim")

10. Seçin **SAML kimlik doğrulamasını etkinleştirme**.
   
    ![Yönetim](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Yönetim")

11. Merhaba, **SAML kimlik doğrulaması** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![SAML kimlik doğrulaması](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "SAML kimlik doğrulaması")  
 
    a. Merhaba, **oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.
  
    b. Merhaba, **SLO URL** metin kutusuna, Yapıştır hello değerini **Sign-Out URL**, Azure portalından kopyalanan.
  
    c. Base-64 kodlanmış sertifikanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve ardından yapıştırın içine tüm sertifika hello **X.509 sertifikası** metin kutusu.
  
    d. **Kaydet** düğmesine tıklayın.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-sugar-crm-test-user"></a>Sugar CRM test kullanıcısı oluşturma

Sağlanan tooSugar CRM tooSugar CRM, sipariş tooenable Azure AD kullanıcıların toolog içinde olmaları gerekir.

Sugar CRM Hello durumda sağlama bir el ile bir görevdir.

**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour oturum **Sugar CRM** yönetici olarak şirket site.

2. Çok Git**yönetici**.
   
    ![Yönetici](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "yönetici")

3. Merhaba, **Yönetim** 'yi tıklatın **kullanıcı yönetimi**.
   
    ![Yönetim](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Yönetim")

4. Çok Git**kullanıcılar \> yeni kullanıcı oluştur**.
   
    ![Yeni kullanıcı oluşturmak](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "yeni kullanıcı oluşturun")

5. Merhaba üzerinde **kullanıcı profili** sekmesinde, hello aşağıdaki adımları gerçekleştirin:
   
    ![Yeni kullanıcı](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "yeni kullanıcı")

    a. Türü hello **kullanıcı adı**, **Soyadı**, ve **e-posta adresi** hello halinde geçerli bir Azure Active Directory kullanıcı, metin kutuları ilgili.
  
6. Olarak **durum**seçin **etkin**.

7. Merhaba parola sekmesinde hello aşağıdaki adımları gerçekleştirin:
   
    ![Yeni kullanıcı](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "yeni kullanıcı")

    a. Merhaba türü hello parolanıza textbox ilgili.

    b. **Kaydet** düğmesine tıklayın.

>[!NOTE]
>API AAD kullanıcı hesaplarının Sugar CRM tooprovision tarafından sağlanan veya herhangi diğer Sugar CRM kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz. 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooSugar CRM vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooSugar, CRM hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Sugar CRM**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.

Merhaba Sugar CRM hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Sugar CRM uygulaması almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_203.png

