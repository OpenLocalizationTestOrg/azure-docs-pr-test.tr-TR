---
title: "Öğretici: Cisco Spark Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Cisco Spark arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 386c4fd816095e1c61de01dd1dee1bbd00311a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a>Öğretici: Cisco Spark Azure Active Directory Tümleştirme

Bu öğreticide, bilgi toointegrate Cisco Spark nasıl Azure Active Directory (Azure AD) ile.

Cisco Spark Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooCisco Spark sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooCisco Spark (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

Cisco Spark ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Cisco Spark çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Cisco Spark hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-cisco-spark-from-hello-gallery"></a>Cisco Spark hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme Cisco Spark, tooadd Cisco Spark hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Cisco Spark hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Cisco Spark**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. Merhaba Sonuçlar panelinde seçin **Cisco Spark**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Cisco "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Spark ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen Cisco Spark tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve Cisco Spark hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Cisco Spark hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Cisco Spark ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Cisco Spark test kullanıcısı oluşturma](#creating-a-cisco-spark-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Cisco Spark, karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Cisco Spark uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma Cisco Spark ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Cisco Spark** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. Merhaba üzerinde **Cisco Spark etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, URL'yi yazın:`https://web.ciscospark.com/#/signin`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://idbroker.webex.com/<companyname>`

    > [!NOTE] 
    > Bu değer gerçek değil. Bu değer ile Merhaba güncelleştirme gerçek tanımlayıcısı. Kişi [Cisco Spark istemci destek ekibi](https://support.ciscospark.com/) tooget bu değer. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. Cisco Spark uygulama hello SAML onaylar toocontain özel öznitelikler bekler. Bu uygulama için öznitelikler aşağıdaki hello yapılandırın. Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz **kullanıcı öznitelikleri** uygulama tümleştirmesi sayfasında bölüm. Ekran aşağıdaki hello bunun bir örneği gösterir.
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği yukarıdaki hello resimde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:
    
    | Öznitelik adı  | Öznitelik değeri |
    | --------------- | -------------------- |    
    |   Kullanıcı Kimliği    | User.userPrincipalName |   

    a. Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    b. Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.
    
    c. Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.
    
    d. **Tamam**’a tıklayın.

7. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. Çok oturum[Cisco bulut işbirliği Yönetimi](https://admin.ciscospark.com/) tam yönetici kimlik bilgilerinizle.

9. Seçin **ayarları** ve hello altında **kimlik doğrulaması** 'yi tıklatın **Değiştir**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. Seçin **3. taraf kimlik sağlayıcısı tümleştirin. (Gelişmiş)**  ve Git toohello sonraki ekran.

11. Merhaba üzerinde **IDP meta verileri içeri aktarma** sayfasında, ya da sürükle ve bırak hello Azure AD meta veri dosyası hello sayfaya veya hello dosya tarayıcısı seçeneği toolocate kullanabilir ve hello Azure AD meta veri dosyasını karşıya yükleyin. Ardından, seçin **meta veriler (daha güvenli) bir sertifika yetkilisi tarafından imzalanan sertifika gerekli** tıklatıp **sonraki**. 
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. Seçin **SSO Bağlantıyı Sına**ve yeni bir tarayıcı sekmesinde oturum açtığında, Azure AD ile oturum açarak kimlik doğrulaması.

13. Toohello iade **Cisco bulut işbirliği Yönetim** tarayıcı sekmesinde. Merhaba testi başarılı olursa seçin **bu test başarılı oldu. Çoklu oturum açma seçeneği etkinleştirme** tıklatıp **sonraki**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-cisco-spark-test-user"></a>Cisco Spark test kullanıcısı oluşturma

Bu bölümde, Cisco Spark Britta Simon adlı bir kullanıcı oluşturun. Bu bölümde, Cisco Spark Britta Simon adlı bir kullanıcı oluşturun.

1. Toohello Git [Cisco bulut işbirliği Yönetimi](https://admin.ciscospark.com/) tam yönetici kimlik bilgilerinizle.

2. Tıklatın **kullanıcılar** ve ardından **kullanıcıları yönetme**.
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. Merhaba, **yönetmek kullanıcı** penceresinde, seçin **el ile ekleyin veya kullanıcıları değiştirin** tıklatıp **sonraki**.

4. Seçin **adlarını ve e-posta adresi**. Ardından, hello textbox aşağıdaki gibi doldurun:
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    a. Merhaba, **ad** metin kutusuna, türü **Britta**. 
    
    b. Merhaba, **Soyadı** metin kutusuna, türü **Simon**.
    
    c. Merhaba, **e-posta adresi** metin kutusuna, türü  **britta.simon@contoso.com** .

5. Yanı sıra tooadd Britta Simon oturum Hello'ı tıklatın. Ardından **İleri**'ye tıklayın.

6. Merhaba, **Hizmetleri kullanıcıları eklemek** penceresinde tıklatın **kaydetmek** ve ardından **son**.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooCisco Spark vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooCisco Spark, hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Cisco Spark**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.

Merhaba Cisco Spark hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Cisco Spark uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png

