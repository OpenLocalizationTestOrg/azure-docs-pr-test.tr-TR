---
title: "Öğretici: Azure Active Directory Tümleştirme SilkRoad yaşam Suite ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve SilkRoad yaşam Suite arasında."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 07367282ab42b7332f166d64743b4b447aec4935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a>Öğretici: Azure Active Directory Tümleştirme SilkRoad yaşam Suite ile
Bu öğreticinin Hello hedefi olan tooshow, nasıl toointegrate SilkRoad yaşam Suite Azure Active Directory'ye (Azure AD). 

SilkRoad yaşam Suite Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar: 

* Erişim tooSilkRoad yaşam paketine sahip Azure AD'de kontrol edebilirsiniz 
* Azure AD hesaplarına, kullanıcıların tooautomatically get açan tooSilkRoad yaşam Suite çoklu oturum açma (SSO) etkinleştir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar
tooconfigure SilkRoad yaşam Suite ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

* Bir Azure AD aboneliği
* Abonelik SilkRoad yaşam Suite SSO etkin

>[!NOTE]
>tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz. 
> 

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

* Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
* Bir Azure AD deneme ortam yoksa, alabileceğiniz bir [bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticinin Hello hedefi olan tooenable, tootest Azure AD SSO bir sınama ortamında.

Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden SilkRoad yaşam paketi ekleme 
2. Yapılandırma ve Azure AD SSO test etme

## <a name="add-silkroad-life-suite-from-hello-gallery"></a>Merhaba Galerisi'nden SilkRoad yaşam paketi ekleme
Azure AD'ye tooconfigure hello tümleştirme SilkRoad yaşam paketinin tooadd SilkRoad yaşam Suite hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd SilkRoad yaşam hello galeri paketinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**. 
   
    ![Active Directory][1]

2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.

3. Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.
   
    ![Uygulamalar][2]

4. Tıklatın **Ekle** hello sayfanın hello sonundaki.
   
    ![Uygulamalar][3]

5. Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.
   
    ![Uygulamalar][4]

6. Merhaba arama kutusuna yazın **SilkRoad yaşam Suite**.
   
    ![Uygulamalar][5]

7. Merhaba sonuçlar bölmesinde seçin **SilkRoad yaşam Suite**ve ardından **tam** tooadd Merhaba uygulaması.
   
    ![Uygulamalar][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme
Bu bölümde Hello amacı olan tooshow nasıl tooconfigure ve test SilkRoad yaşam Suite ile Azure AD SSO temel alarak "Britta Simon" adlı bir test kullanıcı.

SSO toowork için Azure AD hangi hello karşılık gelen kullanıcı SilkRoad yaşam Suite tooan kullanıcı Azure AD'de tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve SilkRoad yaşam paketindeki hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** SilkRoad yaşam paketindeki.

tooconfigure ve SilkRoad yaşam Suite ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[SilkRoad yaşam Suite test kullanıcısı oluşturma](#creating-a-silkroad-life-suite-test-user)**  -toohave karşılık gelen, Britta Simon SilkRoad yaşam paketindeki, her bağlı toohello Azure AD gösterimidir.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın
Bu bölümde Hello amacı hello Klasik Azure portalı, Azure AD SSO tooenable ve tooconfigure SSO SilkRoad yaşam Suite uygulamanızda ' dir.

**Azure AD çoklu oturum açma tooconfigure SilkRoad yaşam Suite ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Yönetici olarak oturum açma tooyour SilkRoad şirket sitesi. 

  >[!NOTE] 
  > tooobtain erişim toohello Microsoft Azure AD ile Federasyon yapılandırma SilkRoad yaşam Suite kimlik doğrulaması uygulama SilkRoad desteği veya SilkRoad Hizmetleri temsilcinize başvurun.
  > 

2. Çok Git**hizmet sağlayıcısı**ve ardından **Federasyon ayrıntıları**. 
   
    ![Azure AD çoklu oturum açma][10] 

3. Tıklatın **karşıdan Federasyon meta verileri**ve ardından hello meta veri dosyası, bilgisayarınıza kaydedin.
   
    ![Azure AD çoklu oturum açma][11] 

4. Hello hello üzerinde Klasik Azure portalı içinde **SilkRoad yaşam Suite** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **yapılandırma çoklu oturum açma**  iletişim kutusu.
   
    ![Çoklu oturum açmayı yapılandırın][6] 

5. Merhaba üzerinde **nasıl tooSilkRoad yaşam paketi üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Azure AD çoklu oturum açma**ve ardından **sonraki**.
   
    ![Azure AD çoklu oturum açma][7] 

6. Merhaba üzerinde **uygulama ayarlarını yapılandır** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Azure AD çoklu oturum açma][8]   
 1. Merhaba, **oturum üzerinde URL'si** metin kutusuna, kullanıcıların toosign üzerinde tooyour SilkRoad yaşam Suite site tarafından kullanılan türü hello URL'si (örn: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).  
 2. İndirilen açık hello **Silkroad** meta veri dosyası. 
 3. Merhaba bulun **AssertionConsumerService** etiketini ve kopyalama hello **konumu** özniteliği.         
   
    ![Azure AD çoklu oturum açma][21] 
 4. Merhaba değeri hello yapıştırma **yanıt URL'si** metin kutusu.  
 5. **İleri**’ye tıklayın.

6. Merhaba üzerinde **çoklu oturum açma SilkRoad yaşam Suite yapılandırma** sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Azure AD çoklu oturum açma][9]  
 1. İndirme sertifikası'nı tıklatın ve ardından hello dosyayı bilgisayarınıza kaydedin.  
 2. **İleri**’ye tıklayın.

7. İçinde **SilkRoad** uygulama tıklatın **kimlik doğrulaması kaynakları**.
   
    ![Azure AD çoklu oturum açma][12] 

8. Tıklatın **kimlik doğrulaması kaynağı Ekle**. 
   
    ![Azure AD çoklu oturum açma][13] 

9. Merhaba, **kimlik doğrulaması kaynağı Ekle** bölümünde, hello aşağıdaki adımları gerçekleştirin: 
   
    ![Azure AD çoklu oturum açma][14]  
 1. Altında **seçeneği 2 - meta veri dosyası**, tıklatın **Gözat** tooupload hello meta veri dosyası indirilir.  
 2. Tıklatın **kimlik dosya verilerini kullanarak sağlayıcısı oluşturma**.

10. Merhaba, **kimlik doğrulaması kaynakları** 'yi tıklatın **Düzenle**. 
    
     ![Azure AD çoklu oturum açma][15] 

11. Merhaba üzerinde **kimlik doğrulaması kaynağını Düzenle** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin: 
    
     ![Azure AD çoklu oturum açma][16] 
 1. Olarak **etkin**seçin **Evet**.   
 2. Merhaba, **IDP açıklama** metin kutusuna, yapılandırmanız için bir açıklama yazın (örneğin: *Azure AD SSO*).  
 3. Merhaba, **IDP adı** metin kutusuna, belirli tooyour yapılandırma adını yazın (örneğin: *Azure SP*).  
 4. **Kaydet** düğmesine tıklayın.

12. Diğer tüm kimlik doğrulaması kaynakları devre dışı bırakın. 
    
     ![Azure AD çoklu oturum açma][17]

13. Merhaba hello üzerinde Klasik Azure portalı içinde **tek oturum açma onay** sayfasında, **sonraki**.  
    
     ![Azure AD çoklu oturum açma][18]

14. Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.
    
     ![Azure AD çoklu oturum açma][19]

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Britta Simon adlı Klasik Azure portalında bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][20]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.

3. toodisplay hello hello üstte hello menüde kullanıcıların listesini tıklatın **kullanıcılar**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. tooopen hello **Kullanıcı Ekle** hello araç çubuğunda hello altta iletişim tıklatın **Kullanıcı Ekle**. 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. Merhaba üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin: 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.  
 2. Merhaba kullanıcı adı olarak **textbox**, türü **BrittaSimon**. 
 3. **İleri**’ye tıklayın.

6. Merhaba üzerinde **kullanıcı profili** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin: 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. Merhaba, **ad** metin kutusuna, türü **Britta**.    
 2. Merhaba, **Soyadı** metin kutusuna, türü, **Simon**. 
 3. Merhaba, **görünen adı** metin kutusuna, türü **Britta Simon**. 
 4. Merhaba, **rol** listesinde **kullanıcı**.
 5. **İleri**’ye tıklayın.

7. Merhaba üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. Merhaba üzerinde **Get geçici parola** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. Merhaba Hello değerini yazmak **yeni parola**. 
 2. **Tamamla**’ya tıklayın.   

### <a name="create-a-silkroad-life-suite-test-user"></a>SilkRoad yaşam Suite test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate Britta Simon SilkRoad yaşam paketindeki adlı bir kullanıcı var. Britta'nın bir SSO kimliği olmalıdır (bazen tooas başvurulan bir *AuthParam*) Britta'nın eşleşen **emailaddress** Azure AD'de.

**toocreate Britta Simon SilkRoad yaşam paketindeki adlı bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**

- SilkRoad yaşam Suite Destek Ekibi toocreate sahip bir kullanıcıya sor **SSO kimliği** aynı değer hello özniteliği hello **emailaddress** Britta Simon Azure AD'de.

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın
Merhaba amacı, bu bölümde, kendi erişim tooSilkRoad yaşam Suite vererek tooenable Britta Simon toouse Azure SSO olur.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooSilkRoad yaşam Suite hello aşağıdaki adımları gerçekleştirin:**

1. Hello üzerinde Azure Klasik portalı, hello dizin görünümünde tooopen hello uygulamaları Görünüm'e tıklayın **uygulamaları** hello üst menüde.
   
    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **SilkRoad yaşam Suite**.
   
    ![Kullanıcı atama][202] 

3. Hello içinde hello üst menüsünde **kullanıcılar**.
   
    ![Kullanıcı atama][203] 

4. Merhaba kullanıcılar listesinden seçin **Britta Simon**.

5. Merhaba altta Hello araç çubuğunda **atamak**.
   
    ![Kullanıcı atama][205]

### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin
Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.  

Merhaba SilkRoad yaşam Suite hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour SilkRoad yaşam paketi uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek Kaynaklar
* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





