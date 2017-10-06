---
title: "Öğretici: Azure Active Directory Tümleştirme ile BlueJeans | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile BlueJeans arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: jeedes
ms.openlocfilehash: 67613303a9f854afbf4619418cc1607d329caf94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a>Öğretici: Azure Active Directory Tümleştirme BlueJeans ile

Bu öğreticide, bilgi nasıl toointegrate BlueJeans Azure Active Directory'ye (Azure AD).

BlueJeans Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooBlueJeans sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooBlueJeans (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure BlueJeans ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir BlueJeans çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden BlueJeans ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-bluejeans-from-hello-gallery"></a>Merhaba Galerisi'nden BlueJeans ekleme
Azure AD'ye tooconfigure hello tümleştirme BlueJeans, tooadd BlueJeans hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd BlueJeans hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **BlueJeans**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_search.png)

5. Merhaba Sonuçlar panelinde seçin **BlueJeans**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı BlueJeans ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen BlueJeans içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı BlueJeans hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri BlueJeans içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve BlueJeans ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[BlueJeans test kullanıcısı oluşturma](#creating-a-bluejeans-test-user)**  -toohave karşılık gelen, Britta Simon BlueJeans içinde kullanıcı bağlantılı toohello Azure AD gösterimidir.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma BlueJeans uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile BlueJeans, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **BlueJeans** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

3. Merhaba üzerinde **BlueJeans etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.BlueJeans.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.BlueJeans.com`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [BlueJeans istemci destek ekibi](https://support.bluejeans.com/contact) tooget bu değerleri. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bluejeans-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **BlueJeans yapılandırma** 'yi tıklatın **yapılandırma BlueJeans** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, değişiklik parola URL'si ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_configure.png) 

7. Farklı web tarayıcısı penceresinde tooyour içinde oturum **BlueJeans** yönetici olarak şirket site.

8. Çok Git**yönetici \> grup ayarları \> güvenlik**.
   
   ![Yönetici](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "yönetici")

9. Merhaba, **güvenlik** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
   ![SAML çoklu oturum açma](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML çoklu oturum açma")   
   
   a. Seçin **SAML çoklu oturum açma**.
  
   b. Seçin **otomatik sağlamayı etkinleştirmek**.

10. Aşağıdaki adımları hello ile geçin:

    ![Sertifika yolu](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "sertifika yolu")
    
    a. Tıklatın **Dosya Seç**ve indirilen hello sertifikasını karşıya yükleyin.
   
    b. Yapıştır **SAML çoklu oturum açma hizmet URL'si** hello içine **oturum açma URL'si** metin kutusu.
   
    c. Yapıştır **değişiklik parola URL'si** hello içine **parola değişikliği URL'si** metin kutusu.
   
    d. Yapıştır **Sign-Out URL** hello içine **oturum kapatma URL'si** metin kutusu.

11. Aşağıdaki adımları hello ile geçin:
    
    ![Değişiklikleri kaydetmek](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Değişiklikleri Kaydet")
    
    a. Merhaba, **kullanıcı kimliği** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
   
    b. Merhaba, **e-posta** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
   
    c. Tıklatın **değişiklikleri kaydetmek**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-bluejeans-test-user"></a>BlueJeans test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toolog tooBlueJeans bunların BlueJeans sağlanması gerekir.  

BlueJeans durumunda sağlama bir el ile bir görevdir.

**bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:**

1. İçinde tooyour oturum **BlueJeans** yönetici olarak şirket site.

2. Çok Git**yönetici \> kullanıcıları yönetme \> Kullanıcı Ekle**.
   
   ![Yönetici](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "yönetici")
   
   >[!IMPORTANT]
   >Merhaba **Kullanıcı Ekle** sekmesi kullanılabilir yalnızca hello içindeki IF **Güvenlik sekmesinde**, **otomatik sağlamayı etkinleştirmek** işaretli değildir. 
   
3. Merhaba, **Kullanıcı Ekle** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Kullanıcı ekleme](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "kullanıcı ekleme")
    
    a. Tür a **BlueJeans kullanıcı adı**, bir **e-posta adresi**, **BlueJeans toplantı kimliği**, **yönetici parolası**, **tam adı** , hello **şirket** , metin kutuları hello tooprovision istediğiniz geçerli bir AAD hesabıyla ilgili.
    
    b. Tıklatın **kullanıcı ekleme**.

>[!NOTE]
>API AAD kullanıcı hesaplarının BlueJeans tooprovision tarafından sağlanan veya herhangi diğer BlueJeans kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz. 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooBlueJeans vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooBlueJeans hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **BlueJeans**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba erişim paneli BlueJeans döşeme hello tıkladığınızda, oturum açma sayfasına BlueJeans uygulamasının almanız gerekir.
Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_203.png

