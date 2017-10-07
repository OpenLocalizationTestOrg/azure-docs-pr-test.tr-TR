---
title: "Öğretici: TINFOIL SECURITY Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile TINFOIL SECURITY arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1a3fa9880d9e026c2d6d6548188df2269ff69139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a>Öğretici: TINFOIL SECURITY Azure Active Directory Tümleştirme

Bu öğreticide, bilgi nasıl toointegrate TINFOIL SECURITY Azure Active Directory'ye (Azure AD).

TINFOIL SECURITY Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooTINFOIL güvenlik sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooTINFOIL güvenlik (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

TINFOIL SECURITY ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir TINFOIL SECURITY çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. TINFOIL SECURITY hello Galerisi'nden ekleme
2. Yapılandırma ve Azure AD çoklu oturum açmayı test etme

## <a name="add-tinfoil-security-from-hello-gallery"></a>TINFOIL SECURITY hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme TINFOIL güvenlik tooadd TINFOIL SECURITY hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**TINFOIL SECURITY hello galerisinden tooadd hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **TINFOIL SECURITY**seçin **TINFOIL SECURITY** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![TINFOIL SECURITY Galeriden](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma TINFOIL "Britta Simon" adlı bir test kullanıcı tabanlı güvenliği ile test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen TINFOIL Security tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve TINFOIL Security hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

TINFOIL güvenlik hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve TINFOIL SECURITY ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[TINFOIL SECURITY test kullanıcısı oluşturma](#create-a-tinfoil-security-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir TINFOIL Security, karşılık gelen.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma TINFOIL SECURITY uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma TINFOIL güvenlik, hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **TINFOIL SECURITY** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![SAML oturum açma tabanlı](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. Merhaba üzerinde **TINFOIL güvenlik etki alanı ve URL'leri** bölümünde, hello uygulama zaten Azure ile önceden tümleştirilmiş gibi hello kullanıcının tooperform herhangi bir adımı yok.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. Merhaba üzerinde **SAML imzalama sertifikası** bölümü, kopyalama hello **parmak İZİ** değeri.

    ![SAML imzalama sertifikası bölümü](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. tooadd hello gerekli öznitelik eşlemelerini hello aşağıdaki adımları gerçekleştirin:
    
    ![Öznitelikleri](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "öznitelikleri")
    
    | Öznitelik adı    |   Öznitelik değeri |
    | ------------------- | -------------------- |
    | Hesap Kimliği | UXXXXXXXXXXXXX |
    
    a. Tıklatın **kullanıcı özniteliği eklemek**.
    
    ![Ekle özniteliği](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "öznitelikleri")
    
    ![Ekle özniteliği](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "öznitelikleri")
    
    b. Merhaba, **öznitelik adı** metin kutusuna, türü **AccountID**.
    
    c. Merhaba, **öznitelik değeri** metin kutusuna, daha sonra hello öğretici alacak Yapıştır hello hesabı kimliği değeri.
    
    d. **Tamam**’a tıklayın.    

6. Tıklatın **kaydetmek** düğmesi.

    ![Kaydet düğmesi](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. Merhaba üzerinde **TINFOIL Güvenlik Yapılandırması** 'yi tıklatın **TINFOIL Güvenlik Yapılandırması** tooopen **yapılandırma oturum açma** penceresi. Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**

    ![TINFOIL güvenlik yapılandırması](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. Farklı web tarayıcısı penceresinde TINFOIL SECURITY şirket sitenize yönetici olarak oturum açın.

9. Merhaba üstte Hello araç çubuğunda **hesabım**.
   
    ![Pano](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Panosu")

10. Tıklatın **güvenlik**.
   
    ![Güvenlik](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "güvenlik")

11. Merhaba üzerinde **çoklu oturum açma** yapılandırma sayfasında, hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açma](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "çoklu oturum açma")
   
    a. Seçin **etkinleştirmek SAML**.
   
    b. Tıklatın **el ile yapılandırma**.
   
    c. İçinde **SAML gönderme URL'sini** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan
   
    d. İçinde **SAML sertifika parmak izi** metin kutusuna, Yapıştır hello değerini **parmak izi** kopyalanan **SAML imzalama sertifikası** bölümü.
  
    e. Kopya **bilgisayarınızı hesap kimliği** değer ve hello değerinde yapıştırma **öznitelik değeri** metin kutusu altında **özniteliği eklemek** Azure portalı bölümünde.
   
    f. **Kaydet** düğmesine tıklayın.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Kullanıcıların ve grupların tüm kullanıcılar -> ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Kullanıcı](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-a-tinfoil-security-test-user"></a>TINFOIL SECURITY test kullanıcısı oluşturma

TINFOIL SECURITY içine sipariş tooenable Azure AD kullanıcıların toolog bunların TINFOIL SECURITY sağlanmalıdır. TINFOIL SECURITY Hello durumda sağlama bir el ile bir görevdir.

**tooget sağlanan, bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba kullanıcı bir kurumsal hesap parçasıysa çok ihtiyacınız[hello TINFOIL SECURITY Destek ekibine başvurun](https://www.tinfoilsecurity.com/contact) tooget hello kullanıcı hesabı oluşturuldu.

2. Merhaba kullanıcı normal bir TINFOIL güvenlik SaaS kullanıcı ise, hello kullanıcı hello kullanıcının sitelerin ortak çalışanı tooany ekleyebilirsiniz. Bu tetikleyicileri bir davet toohello belirtilen işlem toosend e-posta toocreate yeni TINFOIL SECURITY kullanıcı hesabı.

> [!NOTE]
> API'leri, Azure AD kullanıcı hesapları TINFOIL SECURITY tooprovision tarafından sağlanan veya herhangi diğer TINFOIL SECURITY kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.
> 
> 

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooTINFOIL güvenlik vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooTINFOIL güvenlik hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **TINFOIL SECURITY**.

    ![TINFOIL SECURITY seçin](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba TINFOIL SECURITY hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour TINFOIL SECURITY uygulama almanız gerekir. Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

