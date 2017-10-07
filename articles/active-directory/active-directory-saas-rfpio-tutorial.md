---
title: "Öğretici: Azure Active Directory Tümleştirme ile RFPIO | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile RFPIO arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: e0c692276276edd8f859e73d81cf54d75a65957a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a>Öğretici: Azure Active Directory Tümleştirme RFPIO ile

Bu öğreticide, bilgi nasıl toointegrate RFPIO Azure Active Directory'ye (Azure AD).

RFPIO Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Denetleyebilirsiniz kimlerin erişimi tooRFPIO olan Azure AD içinde.
- Kullanıcıların tooautomatically get açan tooRFPIO (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda--hello Azure portalında yönetebilir.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure RFPIO ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD abonelik.
- RFPIO tek bir oturum üzerinde etkin olmayan abonelik.

> [!NOTE]
> Bu öğreticide, bir üretim ortamı tootest hello adımları kullanmanızı öneririz yok.

Bu öğreticide tootest hello adımları bu önerileri izleyin:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, alabileceğiniz bir [bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. RFPIO hello Galerisi'nden ekleniyor.
2. Yapılandırma ve Azure AD sınama çoklu oturum açmayı.

## <a name="add-rfpio-from-hello-gallery"></a>Merhaba Galerisi'nden RFPIO ekleme
Azure AD'ye tooconfigure hello tümleştirme RFPIO, tooadd RFPIO hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

### <a name="tooadd-rfpio-from-hello-gallery"></a>tooadd RFPIO hello Galeriden

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesinde Merhaba, seçin hello **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Seçin **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. tooadd yeni bir uygulama seçin hello **yeni uygulama** hello iletişim kutusunun üstündeki düğmesinde.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **RFPIO**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. Merhaba Sonuçlar panelinde seçin **RFPIO**ve ardından hello **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı RFPIO sınayın.

Tek toowork'ın oturum açma, Azure AD hangi hello RFPIO karşılık gelen kullanıcı ve bir kullanıcı Azure AD'de arasındaki ilişkidir tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı RFPIO hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba değeri RFPIO içinde atayın **kullanıcı adı** hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve RFPIO ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**--tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**--Britta Simon ile Azure AD çoklu oturum açma tootest.
3. **[RFPIO test kullanıcısı oluşturma](#creating-a-rfpio-test-user)**  --toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir RFPIO içinde karşılık gelen.
4. **[Hello Azure AD test kullanıcısı atayın](#assigning-the-azure-ad-test-user)**--tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#testing-single-sign-on)**  --tooverify hello yapılandırma çalışıyorsa.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma RFPIO uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile RFPIO, hello aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **RFPIO** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. Merhaba üzerinde **RFPIO etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **IDP** modunda başlatılan:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, türü hello URL'si:`https://www.rfpio.com`

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    b. Denetleme **Göster Gelişmiş URL ayarları**.

    c. Merhaba, **geçiş durumunu** metin kutusuna bir dize değeri girin. Kişi [RFPIO destek ekibi](https://www.rfpio.com/contact/) tooget bu değer. 

4. Denetleme **Göster Gelişmiş URL ayarları**. Tooconfigure hello uygulamada istiyorsanız **SP** modu tarafından başlatılan:   

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    Merhaba, **URL üzerinde oturum** metin kutusuna, türü hello URL'si:`https://www.app.rfpio.com`

5. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. Farklı bir web tarayıcısı penceresinde, oturum açma toohello **RFPIO** yönetici olarak Web sitesi.

8. Merhaba alt sol köşe açılan'ı tıklatın.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. Tıklatın hello üzerinde **kuruluş ayarları**. 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. Tıklatın hello üzerinde **özellikler ve tümleştirme**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. Merhaba, **SAML SSO Yapılandırması** tıklatın **Düzenle**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. Bu bölümde aşağıdaki işlemleri gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    a. Merhaba Merhaba içeriğine kopyalama **indirilen meta veri XML** ve hello yapıştırma **kimlik Yapılandırması** alan.

    > [!NOTE]
    >toocopy hello içeriğini indirilen **meta veri XML** kullanım **not defteri ++** veya uygun **XML Düzenleyicisi**. 

    b. Tıklatın **doğrulamak**.

    c. Tıkladığınızda sonra **doğrulama**Çevir, **SAML(Enabled)** tooon.

    d. Tıklatın **gönderme**.

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="create-a-rfpio-test-user"></a>RFPIO test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toolog tooRFPIO bunların RFPIO sağlanması gerekir.  
RFPIO Hello durumda sağlama bir el ile bir görevdir.

**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour RFPIO şirket site yönetici olarak oturum açın.

2. Merhaba alt sol köşe açılan'ı tıklatın.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. Tıklatın hello üzerinde **kuruluş ayarları**. 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. Tıklatın **ekip ÜYELERİNİN**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. Tıklayın **ÜYELER Ekle**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. Merhaba, **eklediğiniz yeni üyeler** bölümü. Aşağıdaki işlemleri gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/app8.png)

    a. ENTER **e-posta adresi** hello içinde **satır başına bir e-posta girin** alan.

    b. Lütfen seçin **rol** gereksinimlerinize göre.

    c. Tıklatın **ÜYELER Ekle**.
        
    > [!NOTE]
    > Hello Azure Active Directory hesap sahibi bir e-posta alır ve onu etkinleştirilmeden önce bir bağlantı tooconfirm hesaplarında izler.

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooRFPIO vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooRFPIO hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **RFPIO**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test.

RFPIO döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma tooyour RFPIO uygulama almanız gerekir.
Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili öğreticiler listesi toointegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

