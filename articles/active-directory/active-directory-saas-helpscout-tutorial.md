---
title: "Öğretici: Azure Active Directory Tümleştirme ile Yardım Scout | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Yardım Scout arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeedes
ms.openlocfilehash: 58edd140eb1eb5980796ca743b5f7acd891729a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a>Öğretici: Yardım Scout Azure Active Directory Tümleştirme

Bu öğreticide, nasıl toointegrate yardımcı Azure Active Directory (Azure AD) ile Scout öğrenin.

Azure AD ile Yardım Scout tümleştirme avantajları aşağıdaki hello alın:

- Azure AD'de erişim tooHelp Scout olanların kontrol edebilirsiniz.
- Çoklu oturum açma ve bir kullanıcının Azure AD hesabı kullanarak otomatik olarak, kullanıcılar tooHelp Scout imzalayabilirsiniz.
- Hesaplarınızı tek, merkezi bir konumda, hello Azure portalında yönetebilir.

toolearn yazılım olarak Azure AD ile hizmet (SaaS) uygulama tümleştirmesi hakkında daha fazla bilgi görmek [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooset Yardım Scout ile Azure AD tümleştirme aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Yardım Scout aboneliğiyle, çoklu oturum açık açma 

> [!NOTE]
> Bu öğreticide hello adımları test ederseniz, bunları bir üretim ortamında sınamanızı yok öneririz.

Bu öğreticide hello adımları test etmek için öneriler:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. 

Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Yardım Scout hello Galerisi'nden ekleyin.
2. Ayarlama ve Azure AD çoklu oturum açmayı test edin.

## <a name="add-help-scout-from-hello-gallery"></a>Yardım Scout hello Galerisi'nden ekleme
Merhaba hello galerisinde Yardım Scout Azure AD ile tümleştirilmesi yukarı tooset Yardım Scout tooyour yönetilen SaaS uygulamaları listesi ekleyin.

tooadd Yardım Scout hello galerisinden:

1. Merhaba, [Azure portal](https://portal.azure.com), buna hello soldaki menüden, seçin **Azure Active Directory**. 

    ![Hello Azure Active Directory düğmesi][1]

2. Seçin **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar sayfası][2]
    
3. tooadd yeni bir uygulama seçin **yeni uygulama**.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna **Yardım Scout**. Merhaba arama sonuçlarında seçin **Yardım Scout**ve ardından **Ekle**.

    ![Merhaba sonuçlar listesinde Scout Yardım](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a>Ayarlama ve Azure AD çoklu oturum açmayı test edin

Bu bölümde, ayarladığınız ve Yardım Scout ile Azure AD çoklu oturum açmayı test adlı bir test kullanıcı tabanlı *Britta Simon*.

Tek toowork'ın oturum açma tooknow hello Azure AD karşılık gelen kullanıcı Yardımı Scout Azure AD gerekiyor. Bir Azure AD kullanıcı ve ilgili kullanıcı Yardımı Scout hello arasında bir bağlantı ilişkisi kurulmalıdır.

tooestablish hello ilişkisinde Scout, yardımcı olmak için bağlantı **kullanıcıadı**, hello hello değerini atayın **kullanıcı adı** Azure AD'de.

tooconfigure ve Azure AD çoklu oturum açmayı test Yardım Scout, görevleri aşağıdaki tam hello ile:

1. [Azure AD çoklu oturum açmayı ayarlama](#set-up-azure-ad-single-sign-on). Bu özellik bir kullanıcının toouse ayarlar.
2. [Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user). Testleri Azure AD çoklu oturum açma Britta Simon hello kullanıcıyla.
3. [Yardım Scout test kullanıcısı oluşturma](#create-a-help-scout-test-user). Karşılık gelen Britta Simon, Yardım bağlantılı toohello hello kullanıcı Azure AD gösterimi olan Scout içinde oluşturur.
4. [Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user). Azure AD çoklu oturum açma Britta Simon toouse ayarlar.
5. [Test çoklu oturum açma](#test-single-sign-on). Merhaba yapılandırmayı çalıştığını doğrular.

### <a name="set-up-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı ayarlayın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın ayarlarsınız. Sonra tek oturum açma Yardımı Scout uygulamanızda ayarlayın.

Azure AD çoklu oturum açma Yardımı Scout ile yukarı tooset:

1. Merhaba hello üzerinde Azure portal'ın **Yardım Scout** uygulama tümleştirmesi sayfasında, **çoklu oturum açma**.
 
    ![Oturum açma tek bağlantı ayarlama][4]

2. Merhaba üzerinde **çoklu oturum açma** sayfası için **modu**seçin **SAML tabanlı oturum açma**.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. Altında **Yardım Scout etki alanı ve URL'leri**IDP başlatılan modunda çalışırken, aşağıdaki adımları tam hello tooset Merhaba uygulaması yedeklemek istiyorsanız:

    1. Merhaba, **tanımlayıcısı** kutusuna, desen aşağıdaki hello bir URL girin:`urn:auth0:helpscout:<instancename>`

    2. Merhaba, **yanıt URL'si** kutusuna, desen aşağıdaki hello bir URL girin:`https://helpscout.auth0.com/login/callback?connection=<instancename>`

    ![Scout etki alanı ve URL'leri tek oturum açma bilgileri Yardım](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. SP tarafından başlatılan modunda tooset Merhaba uygulaması yedeklemek istiyorsanız hello seçin **Göster Gelişmiş URL ayarları** onay kutusunu işaretleyin ve ardından aşağıdaki hello:

    * Merhaba, **URL üzerinde oturum** kutusuna, hello biçimini izleyen bir URL girin:`https://secure.helpscout.net/members/login/`

    ![Scout etki alanı ve URL'leri tek oturum açma bilgileri Yardım](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > Merhaba bu URL'leri yalnızca tanıtım değerler. Merhaba değerlerini hello gerçek tanımlayıcı URL'sini ve yanıt URL'si ile güncelleştirin. Bu değerleri tooget başvurun [Yardım Scout destek ekibi](mailto:help@helpscout.com). 

5. Altında **SAML imzalama sertifikası**seçin **meta veri XML**ve ardından hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. **Kaydet**’i seçin.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. tek yukarı tooset hello Yardım Scout tarafında oturum açma, indirilen hello meta veri XML dosyası toohello Gönder [Yardım Scout destek ekibi](mailto:help@helpscout.com). Böylece Hello SAML çoklu oturum açma bağlantısı iki tarafta da düzgün ayarlandığından hello Yardım Scout destek ekibi bu ayar uygulanır.

> [!TIP]
> Bu yönergelerde hello kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulamanızı ayarlama yaparken! Seçerek hello uygulama ekledikten sonra **Active Directory** > **kurumsal uygulamalar**seçin hello **çoklu oturum açma** sekmesi. Merhaba katıştırılmış hello belgelerinde erişebilirsiniz **yapılandırma** kısmına hello sayfanın hello. Daha fazla bilgi için bkz: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde Azure portal hello Britta Simon adlı bir test kullanıcısı oluşturun.

![Bir Azure AD test kullanıcısı oluşturma][100]

toocreate Azure AD'de bir sınama kullanıcısı:

1. Merhaba hello soldaki menüde Azure portal seçin **Azure Active Directory**.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. Kullanıcıların, select toodisplay hello listesini **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    ![Kullanıcıları ve grupları seçin ve ardından tüm kullanıcıları seçin](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. tooopen hello **kullanıcı** iletişim kutusu, hello hello üstündeki **tüm kullanıcılar** sayfasında, **Ekle**.

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. Merhaba, **kullanıcı** iletişim kutusunda, aşağıdaki adımları tam hello:

    1. Merhaba, **adı** kutusuna **BrittaSimon**.

    2. Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresi girin.

    3. Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.

    4. **Oluştur**’u seçin.

        ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a>Yardım Scout test kullanıcısı oluşturma

Merhaba, bu bölümün toocreate Britta Simon Yardım Scout içinde adlı bir kullanıcı nesnesidir. Yardım Scout tam zamanında (JIT) sağlama, varsayılan olarak açıktır destekler.

Bu bölümde, hiçbir eylem ya da görev toocomplete yoktur. Kullanıcı Yardım Scout içinde zaten mevcut değilse tooaccess Yardım Scout çalıştığınızda yeni bir tane oluşturulur.

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, hello kullanıcı Britta Simon toouse Azure AD çoklu oturum açma hello kullanıcı hesabı erişimi tooHelp Scout vererek sağlar.

![Merhaba kullanıcı rolü atayın][200] 

tooassign Britta Simon tooHelp Scout:

1. Hello Azure portal, hello uygulamaları görünümünü açın ve toohello dizini görünümü gidin. Seçin **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Yardım Scout**.

    ![Merhaba Yardım Scout bağlantı hello uygulamalar listesinde](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. Merhaba soldaki menüde seçin **kullanıcılar ve gruplar**.

    ![Merhaba kullanıcılar ve gruplar Bağla][202]

4. **Add (Ekle)** seçeneğini belirleyin. Ardından, hello **eklemek atama** sayfasında, **kullanıcılar ve gruplar**.

    ![Merhaba eklemek atama bölmesi][203]

5. Merhaba üzerinde **kullanıcılar ve gruplar** sayfasında, kullanıcıların, select hello listesinde **Britta Simon**.

6. Merhaba üzerinde **kullanıcılar ve gruplar** sayfasında, **seçin**.

7. Merhaba üzerinde **eklemek atama** sayfasında, **atamak**.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test.

Merhaba erişim panelinde hello Yardım Scout döşeme seçtiğinizde tooyour Yardım Scout uygulama otomatik olarak imzalanmalıdır.

Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi Azure Active Directory ile toointegrate SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_203.png

