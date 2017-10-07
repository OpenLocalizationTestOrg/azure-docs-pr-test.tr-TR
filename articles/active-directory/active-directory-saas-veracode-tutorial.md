---
title: "Öğretici: Azure Active Directory Tümleştirme ile Veracode | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Veracode arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d17307b3864b7df8ee55f569d8f962e2e315b936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a>Öğretici: Azure Active Directory Tümleştirme Veracode ile

Bu öğreticide, bilgi nasıl toointegrate Veracode Azure Active Directory'ye (Azure AD).

Veracode Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooVeracode sahip Azure AD'de kontrol edebilirsiniz.
- Kullanıcıların tooautomatically get açan tooVeracode (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Veracode ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Veracode çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Veracode ekleme
2. Yapılandırma ve Azure AD çoklu oturum açmayı test etme

## <a name="add-veracode-from-hello-gallery"></a>Merhaba Galerisi'nden Veracode ekleme
Azure AD'ye tooconfigure hello tümleştirme Veracode, tooadd Veracode hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Veracode hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna yazın **Veracode**seçin **Veracode** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Merhaba sonuçları listesinde Veracode](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Veracode sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen Veracode içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Veracode hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Veracode içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Veracode ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Veracode test kullanıcısı oluşturma](#create-a-veracode-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Veracode içinde karşılık gelen.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Veracode uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Veracode, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Veracode** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. Merhaba üzerinde **Veracode etki alanı ve URL'leri** bölümü, kullanıcı hello uygulama zaten Azure ile önceden tümleştirilmiş gibi herhangi bir adım tooperform yok. 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. Bu bölümde Hello amacı nasıl tooenable kullanıcılar tooauthenticate tooVeracode Federasyon kullanarak Azure AD'de hesabıyla hello SAML protokolünü temel toooutline ' dir.

    Veracode uygulamanızı hello SAML onaylar tooadd özel öznitelik eşlemelerini tooyour gerektiren belirli bir biçimde, bekliyor **saml belirteci öznitelikleri** yapılandırma. Ekran aşağıdaki hello bunun bir örneği gösterir.
    
    ![Öznitelikleri](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "öznitelikleri")

6. tooadd hello gerekli öznitelik eşlemelerini hello aşağıdaki adımları gerçekleştirin:

    | Öznitelik adı | Öznitelik değeri |
    |--- |--- |
    | FirstName |User.givenName |
    | Soyadı |User.surname |
    | E-posta |User.Mail |
    
    a. Yukarıdaki hello tablosundaki her veri satırı için tıklatın **kullanıcı özniteliği eklemek**.
    
    ![Öznitelikleri](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "öznitelikleri")
    
    ![Öznitelikleri](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "öznitelikleri")
    
    b. Merhaba, **öznitelik adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.
    
    c. Merhaba, **öznitelik değeri** metin kutusuna, ilgili satır için gösterilen select hello öznitelik değeri.
    
    d. **Tamam**’a tıklayın.

7. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. Merhaba üzerinde **Veracode yapılandırma** 'yi tıklatın **yapılandırma Veracode** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML varlık kimliği** hello gelen **hızlı başvuru bölümü.**

    ![Veracode yapılandırma](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. Farklı web tarayıcısı penceresinde Veracode şirket sitenize yönetici olarak oturum açın.

10. Hello içinde hello üst menüsünde **ayarları**ve ardından **yönetici**.
   
    ![Yönetim](./media/active-directory-saas-veracode-tutorial/ic802911.png "Yönetim")

11. Merhaba tıklatın **SAML** sekmesi.

12. Merhaba, **kuruluş SAML ayarları** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![Yönetim](./media/active-directory-saas-veracode-tutorial/ic802912.png "Yönetim")
   
    a.  İçinde **veren** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.
    
    b. Azure Portalı'ndan indirilen sertifikanızı tooupload tıklatın **Dosya Seç**.
   
    c. Seçin **etkinleştirmek kendi kendine kayıt**.

13. Merhaba, **kendi kendine kayıt ayarları** bölümünde, hello aşağıdaki adımları gerçekleştirin ve ardından **kaydetmek**:
   
    ![Yönetim](./media/active-directory-saas-veracode-tutorial/ic802913.png "Yönetim")
   
    a. Olarak **yeni kullanıcı etkinleştirme**seçin **Hayır etkinleştirmesinin**.
   
    b. Olarak **kullanıcı veri güncelleştirmeleri**seçin **tercih Veracode kullanıcı verilerini**.
   
    c. İçin **SAML özniteliği ayrıntılarını**, hello aşağıdakileri seçin:
      * **Kullanıcı rolleri**
      * **İlke Yöneticisi**
      * **Gözden Geçiren**
      * **Güvenlik sağlama**
      * **Executive**
      * **Gönderen**
      * **Oluşturan**
      * **Tüm taraması türleri**
      * **Takım üyelikleri**
      * **Varsayılan takım**

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

   ![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    a. Merhaba, **adı** kutusuna **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.

    c. Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-a-veracode-test-user"></a>Veracode test kullanıcısı oluşturma
Veracode içine sipariş tooenable Azure AD kullanıcıların toolog bunların Veracode sağlanmalıdır. Veracode Hello durumda sağlama otomatik bir görev haline gelmektedir. Sizin için eylem öğe yok. Kullanıcıları otomatik olarak hello ilk tek oturum açma girişimi sırasında gerekirse oluşturulur.

> [!NOTE]
> API'leri, Azure AD kullanıcı hesapları Veracode tooprovision tarafından sağlanan veya herhangi diğer Veracode kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.
> 

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooVeracode vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200] 

**tooassign Britta Simon tooVeracode hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Veracode**.

    ![Merhaba Veracode bağlantı hello uygulamalar listesinde](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Veracode hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Veracode uygulama almanız gerekir.
Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png

