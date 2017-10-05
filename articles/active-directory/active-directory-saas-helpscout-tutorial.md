---
title: "Öğretici: Azure Active Directory Tümleştirme ile Yardım Scout | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory Yardımı Scout arasındaki yapılandırmayı öğrenin."
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
ms.openlocfilehash: 84cee39c28a0f7e6b9878441e504131795673020
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a>Öğretici: Yardım Scout Azure Active Directory Tümleştirme

Bu öğreticide, Azure Active Directory (Azure AD) ile Yardım Scout tümleştirmek öğrenin.

Azure AD ile Yardım Scout tümleştirme aşağıdaki yararları alın:

- Azure AD'de kimlerin erişebileceğini Scout yardımcı olmak için kontrol edebilirsiniz.
- Otomatik olarak yardımcı Scout kullanıcılarınıza, çoklu oturum açma ve bir kullanıcının Azure AD hesabı kullanarak oturum.
- Hesaplarınızı tek, merkezi bir konumda, Azure portalında yönetebilir.

Azure AD ile hizmet (SaaS) uygulaması tümleştirme olarak yazılım hakkında daha fazla bilgi edinmek için [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

Yardım Scout ile Azure AD tümleştirmeyi ayarlamak için aşağıdaki öğeleri gerekir:

- Bir Azure AD aboneliği
- Bir Yardım Scout aboneliğiyle, çoklu oturum açık açma 

> [!NOTE]
> Bu öğreticide adımları test ederseniz, bunları bir üretim ortamında sınamanızı yok öneririz.

Bu öğreticide adımları test etmek için öneriler:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. 

Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:

1. Yardım Scout Galeriden ekleyin.
2. Ayarlama ve Azure AD çoklu oturum açmayı test edin.

## <a name="add-help-scout-from-the-gallery"></a>Galeriden Yardım Scout ekleme
Galeride Yardım Scout Azure AD ile tümleştirmeyi ayarlamak için Yardım Scout yönetilen SaaS uygulamaları listenize ekleyin.

Galeriden Yardım Scout eklemek için:

1. İçinde [Azure portal](https://portal.azure.com), soldaki menüde seçin **Azure Active Directory**. 

    ![Azure Active Directory düğmesi][1]

2. Seçin **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.

    ![Kurumsal uygulamalar sayfası][2]
    
3. Yeni bir uygulama eklemek için seçin **yeni uygulama**.

    ![Yeni Uygulama düğmesi][3]

4. Arama kutusuna **Yardım Scout**. Arama sonuçlarında seçin **Yardım Scout**ve ardından **Ekle**.

    ![Sonuçlar listesinde Scout Yardım](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a>Ayarlama ve Azure AD çoklu oturum açmayı test edin

Bu bölümde, ayarladığınız ve Yardım Scout ile Azure AD çoklu oturum açmayı test adlı bir test kullanıcı tabanlı *Britta Simon*.

Tekli çalışmaya oturum için Azure AD Yardım Scout Azure AD karşılık gelen kullanıcı bilmek ister. Bir Azure AD kullanıcısının Yardım Scout ilgili kullanıcı arasında bir bağlantı ilişkisi kurulmalıdır.

İçin Yardım Scout içinde bağlantı ilişkisi kurmak için **kullanıcıadı**, değeri atayın **kullanıcı adı** Azure AD'de.

Yapılandırma ve Azure AD çoklu oturum açma Yardımı Scout ile test etmek için aşağıdaki görevleri tamamlayın:

1. [Azure AD çoklu oturum açmayı ayarlama](#set-up-azure-ad-single-sign-on). Bir kullanıcı bu özelliği kullanmak için ayarlar.
2. [Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user). Testleri Azure AD çoklu oturum açma Britta Simon kullanıcıyla.
3. [Yardım Scout test kullanıcısı oluşturma](#create-a-help-scout-test-user). Karşılık gelen Britta Simon, kullanıcının Azure AD gösterimini bağlı Yardım Scout oluşturur.
4. [Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user). Çoklu oturum açmayı Britta Azure AD kullanılacak Simon ayarlar.
5. [Test çoklu oturum açma](#test-single-sign-on). Yapılandırma çalıştığını doğrular.

### <a name="set-up-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı ayarlayın

Bu bölümde, Azure AD çoklu oturum açma Azure portalında ayarlarsınız. Sonra tek oturum açma Yardımı Scout uygulamanızda ayarlayın.

Azure AD çoklu oturum açma Yardımı Scout ile ayarlamak için:

1. Azure portalında üzerinde **Yardım Scout** uygulama tümleştirmesi sayfasında, **çoklu oturum açma**.
 
    ![Oturum açma tek bağlantı ayarlama][4]

2. Üzerinde **çoklu oturum açma** sayfası için **modu**seçin **SAML tabanlı oturum açma**.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. Altında **Yardım Scout etki alanı ve URL'leri**, uygulama, aşağıdaki adımları IDP başlatılan modunda, tam ayarlama istiyorsanız:

    1. İçinde **tanımlayıcısı** kutusunda, aşağıdaki desen bir URL girin:`urn:auth0:helpscout:<instancename>`

    2. İçinde **yanıt URL'si** kutusunda, aşağıdaki desen bir URL girin:`https://helpscout.auth0.com/login/callback?connection=<instancename>`

    ![Scout etki alanı ve URL'leri tek oturum açma bilgileri Yardım](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. SP tarafından başlatılan modunda uygulama ayarlamak isteyip istemediğinizi seçin **Göster Gelişmiş URL ayarları** onay kutusunu işaretleyin ve ardından aşağıdakileri yapın:

    * İçinde **URL üzerinde oturum** kutusunda, aşağıdaki biçimde bir URL girin:`https://secure.helpscout.net/members/login/`

    ![Scout etki alanı ve URL'leri tek oturum açma bilgileri Yardım](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > Bu URL'leri yalnızca tanıtım değerler. Yanıt URL'si ve gerçek tanımlayıcı URL'si ile değerlerini güncelleştirin. Bu değerleri almak için başvurun [Yardım Scout destek ekibi](mailto:help@helpscout.com). 

5. Altında **SAML imzalama sertifikası**seçin **meta veri XML**ve meta veri dosyası, bilgisayarınıza kaydedin.

    ![Sertifika indirme bağlantısı](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. **Kaydet**’i seçin.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. Çoklu oturum açma Yardımı Scout tarafında ayarlamak için indirilen meta veri XML dosyasına göndermek [Yardım Scout destek ekibi](mailto:help@helpscout.com). Oturum açma SAML tek bağlantı iki tarafta da düzgün ayarlandığından emin Yardım Scout destek ekibi bu ayar uygulanır.

> [!TIP]
> Bu yönergelerde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulamanızı ayarlama yaparken! Seçerek uygulama ekledikten sonra **Active Directory** > **kurumsal uygulamalar**seçin **çoklu oturum açma** sekmesi. Katıştırılmış belgelerde erişebilirsiniz **yapılandırma** bölümünde, sayfanın sonundaki. Daha fazla bilgi için bkz: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma

Bu bölümde, Azure portalında Britta Simon adlı bir test kullanıcısı oluşturun.

![Bir Azure AD test kullanıcısı oluşturma][100]

Azure AD'de bir test kullanıcı oluşturmak için:

1. Azure portalında soldaki menüde seçin **Azure Active Directory**.

    ![Azure Active Directory düğmesi](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. Kullanıcıların listesini görüntülemek için seçin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

    ![Kullanıcıları ve grupları seçin ve ardından tüm kullanıcıları seçin](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. Açmak için **kullanıcı** en üstündeki iletişim kutusu **tüm kullanıcılar** sayfasında, **Ekle**.

    ![Ekle düğmesi](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları tamamlayın:

    1. İçinde **adı** kutusuna **BrittaSimon**.

    2. İçinde **kullanıcı adı** kutusuna, kullanıcının Britta Simon e-posta adresi girin.

    3. Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.

    4. **Oluştur**’u seçin.

        ![Kullanıcı iletişim kutusu](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a>Yardım Scout test kullanıcısı oluşturma

Bu bölümde nesnesinin Britta Simon Yardım Scout içinde adlı bir kullanıcı oluşturmaktır. Yardım Scout tam zamanında (JIT) sağlama, varsayılan olarak açıktır destekler.

Bu bölümde, eylem veya görevinin tamamlanması için yoktur. Bir kullanıcı Yardımı Scout içinde zaten yoksa, Yardım Scout erişmeyi denediğinde yeni bir tane oluşturulur.

### <a name="assign-the-azure-ad-test-user"></a>Azure AD test kullanıcısı atayın

Bu bölümde, kullanıcı Britta Scout yardımcı olmak için kullanıcı hesabı erişimi verilmesi tarafından Azure AD çoklu oturum açma kullanılacak Simon izin verin.

![Kullanıcı rolü atayın][200] 

Yardım Scout Britta Simon atamak için:

1. Azure Portalı'ndaki uygulamaları görünümünü açın ve dizin görünümüne gidin. Seçin **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Uygulamalar listesinde **Yardım Scout**.

    ![Uygulamalar listesinde Yardım Scout bağlantı](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. Soldaki menüde seçin **kullanıcılar ve gruplar**.

    ![Kullanıcılar ve gruplar bağlantı][202]

4. **Add (Ekle)** seçeneğini belirleyin. Ardından **eklemek atama** sayfasında, **kullanıcılar ve gruplar**.

    ![Ekleme atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** sayfasında, kullanıcıların, seçim listesinde **Britta Simon**.

6. Üzerinde **kullanıcılar ve gruplar** sayfasında, **seçin**.

7. Üzerinde **eklemek atama** sayfasında, **atamak**.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test.

Erişim panelinde Yardım Scout döşeme seçtiğinizde, otomatik olarak yardımcı Scout uygulamanıza oturum açmanız.

Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ek kaynaklar

* [Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi](active-directory-saas-tutorial-list.md)
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

