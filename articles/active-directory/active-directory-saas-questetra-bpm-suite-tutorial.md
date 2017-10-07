---
title: "Öğretici: Azure Active Directory Tümleştirme Questetra BPM Suite ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Questetra BPM Suite arasında."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 4907e3b5751cd79f994fbd2ebcb7faec4eac34e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a>Öğretici: Azure Active Directory Tümleştirme Questetra BPM Suite ile
Bu öğreticinin Hello hedefi olan tooshow, nasıl toointegrate Questetra BPM Suite Azure Active Directory'ye (Azure AD).  
Questetra BPM Suite Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar: 

* Erişim tooQuestetra BPM paketine sahip Azure AD'de kontrol edebilirsiniz 
* Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooQuestetra (çoklu oturum açma) BPM Suite etkinleştirebilirsiniz
* Hesaplarınızı bir merkezi konumda - hello Klasik Azure portalı Yönet

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar
tooconfigure Questetra BPM Suite ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

* Bir Azure AD aboneliği
* Bir [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.
> 
> 

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

* Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
* Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticinin Hello hedefi olan tooenable, tootest Azure AD çoklu oturum açma bir sınama ortamında.  
Bu öğreticide gösterilen hello senaryo üç ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Questetra BPM paketi ekleme 
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-questetra-bpm-suite-from-hello-gallery"></a>Merhaba Galerisi'nden Questetra BPM paketi ekleme
Azure AD'ye tooconfigure hello tümleştirme Questetra BPM paketinin tooadd Questetra BPM Suite hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Questetra BPM hello galeri paketinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**. 
   
    ![Active Directory][1]

2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.

3. Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.
   
    ![Uygulamalar][2]

4. Tıklatın **Ekle** hello sayfanın hello sonundaki.
   
    ![Uygulamalar][3]

5. Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.
   
    ![Uygulamalar][4]

6. Merhaba arama kutusuna yazın **Questetra BPM Suite**.
   
    ![Uygulamalar][5]

7. Merhaba sonuçlar bölmesinde seçin **Questetra BPM Suite**ve ardından **tam** tooadd Merhaba uygulaması.

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde Hello amacı olan tooshow nasıl tooconfigure ve Questetra BPM Suite ile Azure AD çoklu oturum açmayı test temel alarak "Britta Simon" adlı bir test kullanıcı.

Tek toowork'ın oturum açma, Azure AD hangi hello karşılık gelen kullanıcı Questetra BPM Suite tooan kullanıcı Azure AD'de tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve Questetra BPM paketindeki hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.  
Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Questetra BPM paketindeki.

tooconfigure ve Questetra BPM Suite ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Questetra BPM Suite test kullanıcısı oluşturma](#creating-a-questetra-bpm-suite-test-user)**  -toohave karşılık gelen, Britta Simon Questetra BPM paketindeki, her bağlı toohello Azure AD gösterimidir.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma
Bu bölümde Hello amacı tooenable Azure AD çoklu oturum açma hello Klasik Azure Portalı'nda ve tooconfigure çoklu oturum açma Questetra BPM Suite uygulamanızda ' dir.

**Azure AD çoklu oturum açma tooconfigure Questetra BPM Suite ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Klasik Azure portalı içinde **Questetra BPM Suite** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **yapılandırma çoklu oturum açma**  iletişim kutusu.
   
    ![Çoklu oturum açmayı yapılandırın][8]

2. Merhaba üzerinde **nasıl tooQuestetra BPM paketi üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Azure AD çoklu oturum açma**ve ardından **sonraki**.
   
    ![Azure AD çoklu oturum açma][9]

3. Farklı web tarayıcısı penceresinde oturum açın, **Questetra BPM Suite** yönetici olarak şirket site.

4. Hello içinde hello üst menüsünde **sistem ayarlarını**. 
   
    ![Azure AD çoklu oturum açma][10]

5. tooopen hello **SingleSignOnSAML** sayfasında, **SSO (SAML)**. 
   
    ![Azure AD çoklu oturum açma][11]

6. Merhaba hello üzerinde Klasik Azure portalı içinde **uygulama ayarlarını yapılandır** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin: 
   
    ![Uygulama ayarlarını yapılandırın][13]
   
    a. Üzerinde **Questetra BPM Suite** şirket sitede hello SP bilgi bölümü, kopyalama hello **ACS URL**ve hello yapıştırma **oturum üzerinde URL'si** metin kutusu.
   
    b. Üzerinde **Questetra BPM Suite** şirket sitede hello SP bilgi bölümü, kopyalama hello **varlık kimliği**ve hello yapıştırma **veren URL'si** metin kutusu.
   
    c. Üzerinde **Questetra BPM Suite** şirket sitede hello SP bilgi bölümü, kopyalama hello **ACS URL**ve hello yapıştırma **yanıt URL'si** textbox.
   
    d. **İleri**’ye tıklayın.

7. Merhaba üzerinde **çoklu oturum açma sırasında Questetra BPM paketi yapılandırma** sayfasında, **indirme sertifika**ve yerel olarak bilgisayarınızda hello sertifika dosyasını kaydedin.
   
    ![Çoklu oturum açmayı yapılandırın][14]

8. Üzerinde **Questetra BPM Suite** şirket site, hello aşağıdaki adımları gerçekleştirin: 
   
    ![Çoklu oturum açmayı yapılandırın][15]
   
    a. Seçin **çoklu oturum açmayı etkinleştir**.
   
    b. Merhaba Hello Klasik Azure portalı, kopyalama **veren URL'si** değer ve hello yapıştırma **varlık kimliği** metin kutusu.
   
    c. Merhaba Hello Klasik Azure portalı, kopyalama **çoklu oturum açma hizmet URL'si** değer ve hello yapıştırma **oturum açma sayfası URL'si** metin kutusu.
   
    d. Merhaba Hello Klasik Azure portalı, kopyalama **tek Sign-Out hizmeti URL'si** değer ve hello yapıştırma **oturum kapatma sayfası URL'si** metin kutusu.
   
    e. Merhaba, **NameID biçimi** metin kutusuna, türü **urn: OASIS: adları: tc: SAML:1.1:nameid-biçimi: emailAddress**.

    f. Base-64 kodlanmış dosyayı indirilen sertifikanızı oluşturun. 

    >[!TIP] 
    >Daha fazla ayrıntı için bkz: [nasıl tooconvert bir ikili sertifika bir metin dosyasına](http://youtu.be/PlgrzUZ-Y1o).

    g. Base-64 kodlanmış sertifikanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve hello yapıştırma **doğrulama sertifikası** metin kutusu. 

    h. **Kaydet** düğmesine tıklayın.

1. Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **sonraki**. 
   
    ![Azure AD Connect nedir?][17]

2. Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.  
   
    ![Azure AD Connect nedir?][18]


### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Britta Simon adlı Klasik Azure portalında bir test kullanıcı olur.

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.
   
    ![Azure AD test kullanıcısı oluşturma][100] 

2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.

3. toodisplay hello hello üstte hello menüde kullanıcıların listesini tıklatın **kullanıcılar**.
   
    ![Azure AD test kullanıcısı oluşturma][101] 

4. tooopen hello **Kullanıcı Ekle** hello araç çubuğunda hello altta iletişim tıklatın **Kullanıcı Ekle**. 
   
    ![Azure AD test kullanıcısı oluşturma][102] 

5. Merhaba üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Azure AD test kullanıcısı oluşturma][103]
   
    a. Olarak **kullanıcı türü**seçin **kuruluşunuzdaki yeni kullanıcı**.
   
    b. Merhaba kullanıcı adı olarak **textbox**, türü **BrittaSimon**.
   
    c. İleri'ye tıklayın.

6. Merhaba üzerinde **kullanıcı profili** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin: 
   
    ![Azure AD test kullanıcısı oluşturma][104] 
   
    a. Merhaba, **ad** metin kutusuna, türü **Britta**. 
   
    b. Merhaba, **Soyadı** metin kutusuna, türü, **Simon**.
   
    c. Merhaba, **görünen adı** metin kutusuna, türü **Britta Simon**.
   
    d. Merhaba, **rol** listesinde **kullanıcı**.
   
    e. **İleri**’ye tıklayın.

7. Merhaba üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.
   
    ![Azure AD test kullanıcısı oluşturma][105]  

8. Merhaba üzerinde **Get geçici parola** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Azure AD test kullanıcısı oluşturma][106]   
   
    a. Merhaba Hello değerini yazmak **yeni parola**.
   
    b. **Tamamla**’ya tıklayın.   

### <a name="creating-a-questetra-bpm-suite-test-user"></a>Questetra BPM Suite test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate Britta Simon Questetra BPM paketindeki adlı bir kullanıcı var.

**toocreate Britta Simon Questetra BPM paketindeki adlı bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**

1. Yönetici olarak oturum açma tooyour Questetra BPM Suite şirket sitesi.
2. Çok Git**sistem ayarlarını > kullanıcı listesi > Yeni kullanıcı**. 
3. Merhaba yeni kullanıcı iletişim kutusundaki hello aşağıdaki adımları gerçekleştirin: 
   
    ![Test kullanıcısı oluşturma][300] 
   
    a. Merhaba, **adı** metin kutusuna, Azure AD'de Britta'nin kullanıcı adını yazın.
   
    b. Merhaba, **e-posta** metin kutusuna, Azure AD'de Britta'nin kullanıcı adını yazın.
   
    c. Merhaba, **parola** metin kutusuna, bir parola yazın.

4. Tıklatın **yeni kullanıcı Ekle**.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama
Merhaba amacı, bu bölümde, kendi erişim tooQuestetra BPM Suite vererek tooenabling Britta Simon toouse Azure çoklu oturum açma olur.

![Azure AD Connect nedir?][200]

**tooassign Britta Simon tooQuestetra BPM Suite hello aşağıdaki adımları gerçekleştirin:**

1. Hello üzerinde Azure Klasik portalı, hello dizin görünümünde tooopen hello uygulamaları Görünüm'e tıklayın **uygulamaları** hello üst menüde.
   
    ![Azure AD Connect nedir?][201]
2. Merhaba uygulamalar listesinde **Questetra BPM Suite**.
   
    ![Azure AD Connect nedir?][205]
3. Hello içinde hello üst menüsünde **kullanıcılar**.
   
    ![Azure AD Connect nedir?][202]
4. Merhaba kullanıcılar listesinden seçin **Britta Simon**.
   
    ![Azure AD Connect nedir?][203]
5. Merhaba altta Hello araç çubuğunda **atamak**.
   
    ![Azure AD Connect nedir?][204]

### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme
Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.  
Merhaba Questetra BPM Suite hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Questetra BPM paketi uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek Kaynaklar
* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
