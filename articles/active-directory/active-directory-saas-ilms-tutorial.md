---
title: "Öğretici: Azure Active Directory Tümleştirme ile iLMS | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile iLMS arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: da0936de23afcd5a4213aa6f699165f9bfa82c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a>Öğretici: Azure Active Directory Tümleştirme iLMS ile

Bu öğreticide, bilgi nasıl toointegrate iLMS Azure Active Directory'ye (Azure AD).

İLMS Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooiLMS sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooiLMS (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure iLMS ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir iLMS çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden iLMS ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-ilms-from-hello-gallery"></a>Merhaba Galerisi'nden iLMS ekleme
Azure AD'ye tooconfigure hello tümleştirme iLMS, tooadd iLMS hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**Merhaba galerisinden tooadd iLMS hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **iLMS**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. Merhaba Sonuçlar panelinde seçin **iLMS**, ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı iLMS sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen iLMS içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı iLMS hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** iLMS içinde.

tooconfigure ve iLMS ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Bir iLMS test kullanıcısı oluşturma](#creating-an-ilms-test-user)**  -toohave bir Britta Simon karşılık gelen her bağlantılı toohello Azure AD gösterimidir iLMS içinde.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma iLMS uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile iLMS, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **iLMS** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. Merhaba üzerinde **iLMS etki alanı ve URL'leri** bölümünde, hello tooconfigure hello uygulamada istiyorsanız aşağıdaki adımları gerçekleştirin **IDP** modu tarafından başlatılan:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, Yapıştır hello **tanımlayıcısı** değer, kopyalama **hizmet sağlayıcısı** iLMS Yönetim Portalı'nda SAML ayarları bölümü.

    b. Merhaba, **yanıt URL'si** metin kutusuna, Yapıştır hello **uç noktası (URL)** değer, kopyalama **hizmet sağlayıcısı** hello aşağıdaki sahip iLMS Yönetim Portalı'nda SAML ayarları bölümü düzeni`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`

    >[!Note]
    >Bu '123456' tanımlayıcısının bir örnek değeridir.

4. Denetleme **Göster Gelişmiş URL ayarları**, tooconfigure hello uygulamada istiyorsanız **SP** modunda başlatılan:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    Merhaba, **oturum açma URL'si** metin kutusuna, Yapıştır hello **uç noktası (URL)** değer, kopyalama **hizmet sağlayıcısı** olarak iLMS Yönetim Portalı'nda SAML ayarları bölümü`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`     

5. tooenable sağlama JIT iLMS uygulama hello SAML onaylar belirli bir biçimde bekler. Bu uygulama için talep aşağıdaki hello yapılandırın. Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz **kullanıcı öznitelikleri** uygulama tümleştirmesi sayfasında bölüm. Ekran aşağıdaki hello bunun bir örneği gösterir.
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/4.png)
    
    Oluşturma **departman, bölge** ve **bölme** öznitelikleri ve iLMS içinde bu özniteliklerin hello ad ekleyin. Yukarıda gösterilen bu öznitelikler gereklidir.    

    > [!NOTE] 
    > Tooenable sahip **Un-recognized kullanıcı hesabı oluşturma** iLMS toomap olarak bu öznitelikler. Merhaba yönergeleri izleyerek [burada](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget hello öznitelikleri yapılandırması hakkında bir fikir.

6. Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği yukarıdaki hello resimde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:
    
    | Öznitelik adı | Öznitelik değeri |
    | ---------------| --------------- |    
    | bölme | User.Department |
    | Bölge | User.State |
    | Bölüm | User.jobtitle |

    a. Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    b. Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.
    
    c. Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.
    
    d. Tıklatın **Tamam**

7. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. Farklı web tarayıcısı penceresinde tooyour içinde oturum **iLMS Yönetici portalı** yönetici olarak.

10. Tıklatın **SSO:SAML** altında **ayarları** sekmesinde tooopen SAML ayarları ve hello aşağıdaki adımları gerçekleştirin:
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/1.png) 

    a. Merhaba genişletin **hizmet sağlayıcısı** bölümü ve kopyalama hello **tanımlayıcısı** ve **uç noktası (URL)** değeri.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/2.png) 

    b. Altında **kimlik sağlayıcısı** 'yi tıklatın **meta verileri içeri aktarma**.
    
    c. Select hello **meta veri** Azure Portalı'ndan ' ndan indirilen dosya **SAML imzalama sertifikası** bölümü.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    d. Tooenable JIT istiyorsanız toocreate sağlama iLMS kaldırmak için hesapları-kullanıcıların tanıyacağı, aşağıdaki adımları izleyin:
        
       - Denetleme **beklemediğiniz tanınan bir kullanıcı hesabı oluşturma**.
       
       ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  İLMS hello özniteliklerle Azure ad'deki harita Hello öznitelikleri. Merhaba özniteliği sütununda hello öznitelikleri adı veya hello varsayılan değeri belirtin.

    e. Çok Git**iş kuralları** sekmesinde ve hello aşağıdaki adımları gerçekleştirin: 
        
       ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/5.png)

       - Denetleme **Un-recognized bölgeler oluşturmak, bölümler ve Departmanlar** toocreate bölgeler, bölümler ve çoklu oturum açma, hello zaman zaten var olmadığından Departmanlar.
        
       - Denetleme **güncelleştirme kullanıcı profili sırasında oturum açma** toospecify hello kullanıcının profilini her çoklu oturum açma ile olup güncelleştirilir. 
        
       - Merhaba, **"Güncelleştirme boş değerler için olmayan zorunlu alanlar, kullanıcı profili"** seçeneği seçiliyse, oturum açma üzerine boş isteğe bağlı profili alanları toocontain boş değerler hesaplanan alanlar hello kullanıcının iLMS profili de neden olabilir.
        
       - Denetleme **hata bildirim e-posta Gönder** ve tooreceive hello hata bildirim e-posta istediğiniz hello kullanıcının hello e-posta girin.

11. Tıklatın **kaydetmek** düğmesini toosave hello ayarları.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
    
### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-an-ilms-test-user"></a>Bir iLMS test kullanıcısı oluşturma

Uygulama, süresi kullanıcı sağlama ve kimlik doğrulama kullanıcılar hello uygulamada otomatik olarak oluşturulduktan sonra hemen destekler. JIT çalışır, hello tıkladıysanız **Un-recognized kullanıcı hesabı oluşturma** iLMS Yönetici portalı SAML yapılandırma ayarı sırasında onay kutusu.

Bir kullanıcı toocreate el ile gerekiyorsa, aşağıdaki adımları izleyin:

1. Tooyour iLMS şirket sitede yönetici olarak oturum açın.

2. Tıklatın **"Kullanıcı kaydetme"** altında **kullanıcılar** tooopen sekmesinde **kullanıcı Kaydet** sayfası. 
   
   ![Çalışanı ekleyin](./media/active-directory-saas-ilms-tutorial/3.png)

3. Merhaba üzerinde **"Kullanıcı kaydetme"** sayfasında, hello aşağıdaki adımları gerçekleştirin.

    ![Çalışanı ekleyin](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    a. Merhaba, **ad** metin kutusuna, tür hello ilk adı Britta.
   
    b. Merhaba, **Soyadı** metin kutusuna, türü hello Soyadı Simon.

    c. Merhaba, **e-posta kimliği** metin kutusuna, Britta Simon hesabının hello e-posta adresini yazın.

    d. Merhaba, **bölge** açılan listesinde, bölge için select hello değer.

    e. Merhaba, **bölme** açılan listesinde, bölme için select hello değer.

    f. Merhaba, **departmanı** açılan listesinde, departman için select hello değer.

    g. **Kaydet** düğmesine tıklayın.

    > [!NOTE] 
    > Seçerek kayıt posta toouser gönderebilirsiniz **kayıt posta Gönder** onay kutusu.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, kendi erişim tooiLMS vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooiLMS hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **iLMS**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba erişim paneli iLMS döşeme hello tıkladığınızda, otomatik olarak oturum açma tooyour iLMS uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

