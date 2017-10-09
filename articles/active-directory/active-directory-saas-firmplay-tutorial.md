---
title: "Öğretici: Azure Active Directory Tümleştirme FirmPlay - işe alma için çalışan hakları ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile FirmPlay - işe alma için çalışan hakları arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f143e0bb8f2a42de880d77e5f033694ce3f09cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a>Öğretici: Azure Active Directory Tümleştirme ile FirmPlay - işe alma için çalışan hakları

Bu öğreticide, bilgi nasıl toointegrate FirmPlay - işe alma Azure Active Directory (Azure AD) ile çalışan hakları.

FirmPlay - Azure AD ile işe alma için çalışan hakları tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- İşe alma için çalışan hakları erişim tooFirmPlay - olan Azure AD'de kontrol edebilirsiniz
- Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooFirmPlay - işe alma (çoklu oturum açma) için çalışan hakları etkinleştirebilirsiniz
- Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure FirmPlay - işe alma, çalışan hakları ile Azure AD tümleştirme aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- FirmPlay - çoklu oturum açma etkin abonelik işe alma için çalışan hakları


> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.


Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. İşe alma hello galerisinden çalışan hakları FirmPlay - ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-hello-gallery"></a>İşe alma hello galerisinden çalışan hakları FirmPlay - ekleme
tooconfigure hello FirmPlay - Azure AD'ye işe alma için çalışan hakları tümleştirilmesi tooadd FirmPlay - işe alma hello galeri tooyour listesinden yönetilen SaaS uygulamaları için çalışan hakları gerekir.

**tooadd FirmPlay - işe alma hello galerisinden çalışan hakları hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **Ekle** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **FirmPlay - işe alma için çalışan hakları**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. Merhaba Sonuçlar panelinde seçin **FirmPlay - işe alma için çalışan hakları**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma FirmPlay - işe alma "Britta Simon" adlı bir test kullanıcıyı temel alarak çalışan hakları ile test etme.

Tek toowork'ın oturum açma, Azure AD'de FirmPlay - çalışan hakları işe alma için hangi hello karşılık gelen kullanıcı tooa kullanıcıdır tooknow Azure AD gerekiyor. Diğer bir deyişle, bir Azure AD kullanıcısının ve FirmPlay - çalışan hakları işe alma için ilgili kullanıcı hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** FirmPlay - işe alma için çalışan hakları içinde.

tooconfigure ve Azure AD çoklu oturum açmayı test FirmPlay - işe alma, çalışan hakları ile yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[İşe alma test kullanıcısı için çalışan hakları FirmPlay - oluşturma](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)**  -toohave Britta Simon FirmPlay içinde karşılık gelen: çalışan başka bir deyişle işe alma için hakları bağlı her toohello Azure AD gösterimi.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma FirmPlay - çalışan hakları işe alma uygulaması için yapılandırın.

**Azure AD çoklu oturum açma tooconfigure FirmPlay - işe alma, çalışan hakları ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Hello üzerinde hello Azure Yönetim Portalı'nda **FirmPlay - çalışan hakları işe alma için** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. Merhaba üzerinde **FirmPlay - işe alma etki alanı ve URL'ler için çalışan hakları** bölümünde hello **oturum üzerinde URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<your-subdomain>.firmplay.com/`

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > Lütfen bu hello gerçek değer olmadığını unutmayın. Bu değeri hello gerçek ile oturum URL'yi tooupdate sahip. Kişi [FirmPlay - işe alma destek ekibi için çalışan hakları](mailto:engineering@firmplay.com) tooget bu değer. 

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **yeni sertifika oluştur**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. Merhaba üzerinde **yeni sertifika oluştur** iletişim kutusunda, hello Takvim simgesine tıklayın ve bir **sona erme tarihi**. Ardından **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. Merhaba üzerinde **SAML imzalama sertifikası** bölümünde, select **yeni sertifika etkin hale getirin** tıklatıp **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. Merhaba açılır pencere üzerinde **geçiş sertifikası** penceresinde tıklatın **Tamam**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin. 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. Merhaba üzerinde **FirmPlay - işe alma yapılandırması için çalışan hakları** 'yi tıklatın **FirmPlay - çalışan hakları işe alma için yapılandırma** tooopen **oturum açmaYapılandırma**iletişim.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. tooget SSO yapılandırılmış uygulamanızın, kişi [FirmPlay - işe alma destek ekibi için çalışan hakları](mailto:engineering@firmplay.com) ve ile Merhaba aşağıdakileri sağlar: 

    • hello indirilen **sertifika dosyası**

    • hello **SAML çoklu oturum açma hizmet URL'si**

    • hello **SAML varlık kimliği**

    • hello **Sign-Out URL'si**
  

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın. 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a>İşe alma test kullanıcısı için çalışan hakları FirmPlay - oluşturma

Bu bölümde, Britta Simon FirmPlay - işe alma için çalışan hakları adlı bir kullanıcı oluşturun. Lütfen çalışmak [FirmPlay - işe alma destek ekibi için çalışan hakları](mailto:engineering@firmplay.com) tooadd hello kullanıcılar hello FirmPlay - işe alma platform için çalışan hakları.


### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, kendi erişim tooFirmPlay - işe alma için çalışan hakları vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooFirmPlay - işe alma, çalışan hakları hello aşağıdaki adımları gerçekleştirin:**

1. Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **FirmPlay - işe alma için çalışan hakları**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    


### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba FirmPlay - hello erişim paneli, işe alma parçasında çalışan hakları tıkladığınızda otomatik olarak oturum açma tooyour FirmPlay - işe alma uygulaması için çalışan hakları almalısınız.


## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png