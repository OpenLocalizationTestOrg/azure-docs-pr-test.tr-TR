---
title: "Öğretici: Azure Active Directory Tümleştirme ile Onit | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Onit arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bc479a28-8fcd-493f-ac53-681975a5149c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 9e12449e5bf7f169b3cadfaa12438ac5d52ed8f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-onit"></a>Öğretici: Azure Active Directory Tümleştirme Onit ile

Bu öğreticide, bilgi nasıl toointegrate Onit Azure Active Directory'ye (Azure AD).

Onit Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooOnit sahip Azure AD'de kontrol edebilirsiniz.
- Kullanıcıların tooautomatically get açan tooOnit (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Onit ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Onit çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması

Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Onit ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-onit-from-hello-gallery"></a>Merhaba Galerisi'nden Onit ekleme
Azure AD'ye tooconfigure hello tümleştirme Onit, tooadd Onit hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Onit hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna yazın **Onit**seçin **Onit** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Merhaba sonuçları listesinde Onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Onit ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen Onit içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Onit hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Onit içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Onit ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Bir Onit test kullanıcısı oluşturma](#create-an-onit-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Onit içinde karşılık gelen.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Onit uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile Onit, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **Onit** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-onit-tutorial/tutorial_onit_samlbase.png)

3. Merhaba üzerinde **Onit etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Onit etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-onit-tutorial/tutorial_onit_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<sub-domain>.onit.com`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<sub-domain>.onit.com`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı. Kişi [Onit istemci destek ekibi](https://www.onit.com/support) tooget bu değerleri. 
 
4. Merhaba üzerinde **SAML imzalama sertifikası** bölümü, kopyalama hello **parmak İZİ** sertifika değeri.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-onit-tutorial/tutorial_onit_certificate.png) 

5. Onit uygulama hello SAML onaylar belirli bir biçimde bekler. Lütfen bu uygulama için talep aşağıdaki hello yapılandırın. Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz **"Atrribute"** hello uygulama sekmesinde. Ekran aşağıdaki hello bunun bir örneği gösterir. 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-onit-tutorial/tutorial_onit_attribute.png) 

6. Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği hello görüntüde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:
    
    | Öznitelik adı | Öznitelik değeri |
    | ------------------- | -------------------- |
    | E-posta | User.Mail |
    
    a. Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-onit-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-onit-tutorial/tutorial_attribute_05.png)

    b. Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.

    c. Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.

    d. Merhaba bırakın **Namespace** boş.
    
    e. **Tamam**’a tıklayın.

7. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-onit-tutorial/tutorial_general_400.png)

8. Merhaba üzerinde **Onit yapılandırma** 'yi tıklatın **yapılandırma Onit** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **Sign-Out URL, SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![Onit yapılandırma](./media/active-directory-saas-onit-tutorial/tutorial_onit_configure.png)

9. Farklı web tarayıcısı penceresinde Onit şirket sitenize yönetici olarak oturum açın.

10. Hello içinde hello üst menüsünde **Yönetim**.
   
   ![Yönetim](./media/active-directory-saas-onit-tutorial/IC791174.png "Yönetim")
11. Tıklatın **düzenleme Corporation**.
   
   ![Düzen Corporation](./media/active-directory-saas-onit-tutorial/IC791175.png "düzenleme Corporation")
   
12. Merhaba tıklatın **güvenlik** sekmesi.
    
    ![Düzen şirket bilgileri](./media/active-directory-saas-onit-tutorial/IC791176.png "düzenleme şirket bilgileri")

13. Merhaba üzerinde **güvenlik** sekmesinde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açma](./media/active-directory-saas-onit-tutorial/IC791177.png "çoklu oturum açma")

    a. Olarak **kimlik doğrulama stratejisi**seçin **çoklu oturum açma ve parola**.
    
    b. İçinde **IDP hedef URL** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.

    c. İçinde **IDP oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL**, Azure portalından kopyalanan.

    d. İçinde **IDP sertifika parmak izi (SHA1)** metin kutusuna, Yapıştır hello **parmak izi** Azure portalından kopyaladığınız sertifika değeri.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

   ![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-onit-tutorial/create_aaduser_01.png)

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-onit-tutorial/create_aaduser_02.png)

3. tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-onit-tutorial/create_aaduser_03.png)

4. Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-onit-tutorial/create_aaduser_04.png)

    a. Merhaba, **adı** kutusuna **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.

    c. Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-an-onit-test-user"></a>Bir Onit test kullanıcısı oluşturma

Onit içine sipariş tooenable Azure AD kullanıcıların toolog bunların Onit sağlanmalıdır.  

Onit Hello durumda sağlama bir el ile bir görevdir.

**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**

1. Tooyour üzerinde oturum **Onit** yönetici olarak şirket site.
2. Tıklatın **kullanıcı ekleme**.
   
   ![Yönetim](./media/active-directory-saas-onit-tutorial/IC791180.png "Yönetim")
3. Merhaba üzerinde **Kullanıcı Ekle** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
   ![Kullanıcı ekleme](./media/active-directory-saas-onit-tutorial/IC791181.png "kullanıcı ekleme")
   
  1. Türü hello **adı** ve hello **e-posta adresi** geçerli bir Azure hello tooprovision istediğiniz AD hesabının ilgili metin kutuları.
  2. **Oluştur**'a tıklayın.    
   
 > [!NOTE]
 > Hello Azure Active Directory hesap sahibi bir e-posta alır ve onu etkinleştirilmeden önce bir bağlantı tooconfirm hesaplarında izler.

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooOnit vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200] 

**tooassign Britta Simon tooOnit hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Onit**.

    ![Merhaba Onit bağlantı hello uygulamalar listesinde](./media/active-directory-saas-onit-tutorial/tutorial_onit_app.png)  

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Onit hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Onit uygulama almanız gerekir.
Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-onit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-onit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-onit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-onit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-onit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-onit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-onit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-onit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-onit-tutorial/tutorial_general_203.png

