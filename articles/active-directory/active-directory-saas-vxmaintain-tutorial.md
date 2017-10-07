---
title: "Öğretici: Azure Active Directory ile vxMaintain tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile vxMaintain arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 937ea276d898986fc5a953c96fddabdc8940309f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a>Öğretici: Azure Active Directory vxMaintain ile tümleştirme

Bu öğreticide, bilgi nasıl toointegrate vxMaintain Azure Active Directory'ye (Azure AD).

Bu tümleştirme birkaç önemli avantaj sağlar. Şunları yapabilirsiniz:

- ToovxMaintain erişim denetimi olan Azure AD'de.
- Kullanıcıların tooautomatically oturum açma toovxMaintain çoklu oturum açma (SSO) ile Azure AD hesaplarına kullanarak etkinleştirin.
- Hesaplarınızı tek bir merkezi konumda yönetme: Azure portal hello.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla toolearn bkz [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure vxMaintain ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- VxMaintain abonelik SSO'su etkin

> [!NOTE]
> Bu öğreticide hello adımları test ettiğinizde, bir üretim ortamında kullanmayın öneririz.

Bu öğreticide tootest hello adımları bu önerileri izleyin:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. 

Bu öğretici özetlenmektedir hello senaryo iki ana yapı taşlarını oluşur:

* Merhaba Galerisi'nden vxMaintain ekleme
* Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="add-vxmaintain-from-hello-gallery"></a>Merhaba Galerisi'nden vxMaintain ekleme
Azure AD ile vxMaintain tooconfigure hello tümleştirilmesi, tooadd vxMaintain hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

Merhaba galerisinden tooadd vxMaintain hello aşağıdaki:

1. Merhaba, [Azure portal](https://portal.azure.com), buna hello sol bölmesinde, seçin hello **Azure Active Directory** düğmesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Seçin **kurumsal uygulamalar** > **tüm uygulamaları**.

    ![Merhaba "Kurumsal uygulamalar" bölmesi][2]
    
3. bir uygulamada hello tooadd **tüm uygulamaları** iletişim kutusunda **yeni uygulama**.

    !["Yeni uygulamayı" Merhaba düğmesi][3]

4. Merhaba arama kutusuna yazın **vxMaintain**.

    ![Merhaba "Modu tek oturum açma" açılan liste](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. Merhaba sonuçları listesinden seçmek **vxMaintain**ve ardından **Ekle**.

    ![Merhaba vxMaintain bağlantı](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme
Bu bölümde, yapılandırma ve Azure AD SSO "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı vxMaintain kullanarak test etme

SSO toowork için Azure AD tooknow hello vxMaintain karşılık gelen toohello Azure AD kullanıcısının gerekir. Diğer bir deyişle, hello Azure AD kullanıcısının hello karşılık gelen vxMaintain kullanıcı arasında bir bağlantı ilişkisi oluşturmanız gerekir.

tooestablish hello bağlantı ilişkisi, Ata hello vxMaintain **kullanıcı adı** değeri hello Azure AD olarak **kullanıcıadı** değeri.

tooconfigure ve test vxMaintain, yapı taşları aşağıdaki tam hello kullanarak Azure AD SSO.

### <a name="configure-azure-ad-sso"></a>Azure AD SSO yapılandırın

Bu bölümde, hello Azure portalında Azure AD SSO'yu etkinleştirmek hem hello aşağıdakileri yaparak vxMaintain uygulamanızda SSO yapılandırın:

1. Merhaba hello üzerinde Azure portal'ın **vxMaintain** uygulama tümleştirmesi sayfasında, **çoklu oturum açma**.

    ![komutu "çoklu oturum açmayı" Merhaba][4]

2. Merhaba içinde SSO tooenable **tek oturum açma modu** aşağı açılan listesinden, **SAML tabanlı oturum açma**.
 
    ![Merhaba "SAML tabanlı oturum açma" komutu](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. Altında **vxMaintain etki alanı ve URL'leri**, aşağıdaki hello:

    ![Merhaba vxMaintain etki alanı ve URL'ler bölümü](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    a. Merhaba, **tanımlayıcısı** kutusuna sözdizimi aşağıdaki hello sahip bir URL yazın:`https://<company name>.verisae.com`

    b. Merhaba, **yanıt URL'si** kutusuna sözdizimi aşağıdaki hello sahip bir URL yazın:`https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`

    > [!NOTE] 
    > Merhaba önceki değerleri gerçek değildir. Merhaba gerçek tanımlayıcısı ile güncelleştirin ve URL yanıt. tooobtain hello değerleri, kişi hello [vxMaintain destek ekibi](http://www.verisae.com/contact-us).
 
4. Altında **SAML imzalama sertifikası**seçin **meta veri XML**ve ardından hello meta veri dosya tooyour bilgisayara kaydedin.

    ![Merhaba "SAML imzalama sertifikası" bölümü](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. **Kaydet**’i seçin.

    ![Merhaba Kaydet düğmesi](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. tooconfigure **vxMaintain** SSO, indirilen gönderme hello **meta veri XML** toohello dosya [vxMaintain destek ekibi](http://www.verisae.com/contact-us).

> [!TIP]
> Merhaba uygulama ayarlama gibi hello yönergeleri önceki hello kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com). Hello hello uygulama ekledikten sonra **Active Directory** > **kurumsal uygulamalar** bölümü, select hello **çoklu oturum açma** sekmesini ve ardından erişim hello Merhaba belgelerinden katıştırılmış **yapılandırma** bölümü. 
>
>toolearn hello embedded belgeler özelliği hakkında daha fazla bilgi görmek [Kurumsal uygulamaları için çoklu oturum açmayı yönetme](https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde, test kullanıcı Britta Simon hello Azure portal hello aşağıdakileri yaparak oluşturun:

![Hello Azure AD test kullanıcısı][100]

1. Merhaba, **Azure portal**, buna hello sol bölmesinde, seçin hello **Azure Active Directory** düğmesi.

    ![Merhaba "Azure Active Directory" düğmesi](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. Kullanıcıların, listesini toodisplay Git çok**kullanıcılar ve gruplar** > **tüm kullanıcılar**.
    
    ![Merhaba "Tüm kullanıcılar" bağlantı](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)  
    Merhaba **tüm kullanıcılar** iletişim kutusu açılır. 

3. tooopen hello **kullanıcı** iletişim kutusunda **Ekle**.
 
    ![Merhaba Ekle düğmesi](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. Merhaba, **kullanıcı** iletişim kutusunda, aşağıdaki hello:
 
    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** kutusuna **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** kutusunda, test kullanıcısının Britta Simon hello e-posta adresini yazın.

    c. Select hello **Göster parola** onay kutusunu ve ardından hello oluşturulan Not hello değeri **parola** kutusu.

    d. **Oluştur**’u seçin.
 
### <a name="create-a-vxmaintain-test-user"></a>VxMaintain test kullanıcısı oluşturma

Bu bölümde, test kullanıcı Britta Simon vxMaintain oluşturun. Merhaba vxMaintain Platform tooadd kullanıcıların çalışması ile [vxMaintain destek ekibi](http://www.verisae.com/contact-us). SSO kullanmadan önce oluşturup hello kullanıcıları etkinleştirin.

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, test kullanıcısı Britta Simon toouse Azure SSO erişimi toovxMaintain vererek etkinleştirin. toodo, bu nedenle, hello aşağıdaki:

![Test kullanıcısı hello görünen ad listesinde][200] 

1. Hello Azure portal'ın **uygulamaları** görüntülemek için çok gidin**Directory** Görünüm > **kurumsal uygulamalar** > **tüm uygulamaları**.

    ![Merhaba "Tüm uygulamaları" bağlantı][201] 

2. Merhaba, **uygulamaları** listesinde **vxMaintain**.

    ![Merhaba vxMaintain bağlantı](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. Merhaba sol bölmesinde seçin **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202] 

4. Seçin **Ekle** ve ardından hello **eklemek atama** bölmesinde, **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][203]

5. Merhaba, **kullanıcılar ve gruplar** iletişim kutusunda hello **kullanıcılar** listesinden, **Britta Simon**seçip hello **seçin** düğmesi.

7. Merhaba, **eklemek atama** iletişim kutusunda **atamak**.
    
### <a name="test-your-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı test edin

Bu bölümde, hello erişim paneli kullanarak Azure AD SSO yapılandırmanızı sınayın.

Seçme hello **vxMaintain** hello erişim paneli parçasında oturumunuzu tooyour vxMaintain uygulamada otomatik olarak.

Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="next-steps"></a>Sonraki adımlar

* [Azure Active Directory ile SaaS uygulamalarını tümleştirme öğreticiler listesi](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png

