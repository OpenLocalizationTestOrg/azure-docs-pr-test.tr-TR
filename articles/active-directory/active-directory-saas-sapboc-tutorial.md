---
title: "Öğretici: SAP Business nesnesi bulut Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve SAP Business nesnesi bulut arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: a3e9bd93897271531f91bcbc50cd361e8a20551e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a>Öğretici: SAP Business nesnesi bulut Azure Active Directory Tümleştirme

Bu öğreticide, nasıl toointegrate SAP öğrenin iş nesnesi bulut Azure Active Directory'ye (Azure AD).

SAP Business nesnesi bulut Azure AD ile tümleştirdiğinizde avantajları aşağıdaki hello alın:

- Azure AD'de erişim tooSAP iş nesnesi bulut olanların kontrol edebilirsiniz.
- Çoklu oturum açma ve bir kullanıcının Azure AD hesabı kullanarak otomatik olarak, kullanıcılar tooSAP iş nesnesi bulut imzalayabilirsiniz.
- Hesaplarınızı tek, merkezi bir konumda, hello Azure portalında yönetebilir.

toolearn yazılım olarak Azure AD ile hizmet (SaaS) uygulama tümleştirmesi hakkında daha fazla bilgi görmek [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

SAP Business nesnesi bulut ile Azure AD tümleştirme tooset, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- SAP Business nesnesi olan bir buluta, tekli açık oturum

> [!NOTE]
> Bu öğreticide hello adımları test ederseniz, bunları bir üretim ortamında sınamanızı yok öneririz.

Bu öğreticide hello adımları test etmek için öneriler:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. 

Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. SAP Business nesnesi bulut hello Galerisi'nden ekleyin.
2. Ayarlama ve Azure AD çoklu oturum açmayı test edin.

## <a name="add-sap-business-object-cloud-from-hello-gallery"></a>SAP Business nesnesi bulut hello Galerisi'nden ekleme
Itanium tabanlı sistemler için SAP Business nesnesi bulut Azure AD ile Merhaba galerisinde hello tümleştirme tooset SAP Business nesnesi bulut tooyour yönetilen SaaS uygulamaları listesi ekleyin.

SAP Business nesnesi bulut hello galerisinden tooadd:

1. Merhaba, [Azure portal](https://portal.azure.com), buna hello soldaki menüden, seçin **Azure Active Directory**. 

    ![Hello Azure Active Directory düğmesi][1]

2. Seçin **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar sayfası][2]
    
3. tooadd yeni bir uygulama seçin **yeni uygulama**.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna **SAP Business nesnesi bulut**.

    ![Merhaba arama kutusu](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. Merhaba Sonuçlar panelinde seçin **SAP Business nesnesi bulut**ve ardından **Ekle**.

    ![SAP Business nesnesi bulut hello sonuçları listesinde](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a>Ayarlama ve Azure AD çoklu oturum açmayı test edin

Bu bölümde, ayarladığınız ve SAP Business nesnesi bulut ile Azure AD çoklu oturum açmayı test adlı bir test kullanıcı tabanlı *Britta Simon*.

Tek toowork'ın oturum açma tooknow hello Azure AD karşılık gelen kullanıcı SAP Business nesnesi bulutta Azure AD gerekiyor. Bir Azure AD kullanıcısının ve SAP Business nesnesi bulutta hello ilgili kullanıcı arasındaki bağlantıyı ilişkisi kurulmalıdır.

tooestablish hello için bulutta SAP iş nesnesi, ilişki bağlantı **kullanıcıadı**, hello hello değerini atayın **kullanıcı adı** Azure AD'de.

tooconfigure ve Azure AD çoklu oturum açmayı test SAP Business nesnesi bulut, görevleri aşağıdaki tam hello ile:

1. [Azure AD çoklu oturum açmayı ayarlama](#set-up-azure-ad-single-sign-on). Bu özellik bir kullanıcının toouse ayarlar.
2. [Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user). Testleri Azure AD çoklu oturum açma Britta Simon hello kullanıcıyla.
3. [SAP Business nesnesi bulut test kullanıcısı oluşturma](#create-an-sap-business-object-cloud-test-user). Karşılık gelen Britta Simon, SAP iş nesnesi, bağlantılı toohello hello kullanıcı Azure AD gösterimi bulutta oluşturur.
4. [Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user). Azure AD çoklu oturum açma Britta Simon toouse ayarlar.
5. [Test çoklu oturum açma](#test-single-sign-on). Merhaba yapılandırmayı çalıştığını doğrular.

### <a name="set-up-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı ayarlayın

Bu bölümde, üzerinde Azure AD çoklu hello Azure portalında oturum açın. Sonra tek oturum açma SAP Business nesnesi bulut uygulamanızda ayarlayın.

Azure AD çoklu oturum açma SAP Business nesnesi bulut ile yukarı tooset:

1. Merhaba hello üzerinde Azure portal'ın **SAP Business nesnesi bulut** uygulama tümleştirmesi sayfasında, **çoklu oturum açma**.

    ![Çoklu oturum açma seçin][4]

2. Merhaba üzerinde **çoklu oturum açma** sayfası için **modu**seçin **SAML tabanlı oturum açma**.
 
    ![SAML tabanlı oturum açma seçin](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. Altında **SAP Business nesnesi bulut etki alanı ve URL'leri**tam hello adımları izleyin:

    1. Merhaba, **oturum açma URL'si** kutusuna, desen aşağıdaki hello bir URL girin: 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. Merhaba, **tanımlayıcısı** kutusuna, desen aşağıdaki hello bir URL girin:
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![SAP Business nesnesi bulut etki alanı ve URL'leri sayfa URL'leri](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > Merhaba bu URL'leri yalnızca tanıtım değerler. Güncelleştirme hello hello gerçek değerlerle URL ve tanımlayıcıdır URL oturum. tooget hello oturum açma URL'si kişi hello [SAP Business nesnesi bulut istemci destek ekibi](https://www.sap.com/product/analytics/cloud-analytics.support.html). Merhaba yönetici konsolundan hello SAP Business nesnesi bulut meta verileri yükleyerek hello tanımlayıcı URL'sini alabilirsiniz. Bu hello öğreticinin ilerleyen bölümlerinde açıklanmıştır. 

4. Altında **SAML imzalama sertifikası**seçin **meta veri XML**. Daha sonra hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Meta veri XML seçin](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. **Kaydet**’i seçin.

    ![Kaydet'i seçin](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. Farklı web tarayıcısı penceresinde tooyour SAP Business nesnesi bulut şirket sitede yönetici olarak oturum açın.

7. Seçin **menü** > **sistem** > **Yönetim**.
    
    ![Menüsünü, sonra sistem ve yönetim seçin](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. Merhaba üzerinde **güvenlik** sekmesi, select hello **Düzenle** (Kalem) simgesi.
    
    ![Merhaba Güvenlik sekmesinde hello Düzenle simgesini seçin](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. İçin **kimlik doğrulama yöntemini**seçin **SAML çoklu oturum açma (SSO)**.

    ![SAML çoklu oturum açma için hello kimlik doğrulama yöntemini seçin](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. toodownload hello hizmet sağlayıcısı meta verileri (1. adım), select **karşıdan**. Merhaba meta veri dosyasını bulun ve kopyalama hello **Entityıd** değeri. Hello Azure'nın altında portal **SAP Business nesnesi bulut etki alanı ve URL'leri**, hello hello değeri yapıştırın **tanımlayıcısı** kutusu.

    ![Kopyalama ve yapıştırma hello Entityıd değeri](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. tooupload hello hizmet sağlayıcısı meta verileri (2. adım) kaynağından indirdiğiniz hello dosyasında hello Azure portal altında **karşıya kimlik sağlayıcısı meta verileri**seçin **karşıya**.  

    ![Karşıya yükleme karşıya kimlik sağlayıcısı meta verileri altında seçin](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. Merhaba, **kullanıcı özniteliği** listesinde, uygulamanız için toouse istediğinizi seçin hello kullanıcı özniteliği (adım 3). Bu kullanıcı özniteliği toohello kimlik sağlayıcısı eşler. tooenter hello kullanıcının sayfasında, kullanım hello özel bir öznitelik **özel SAML eşleme** seçeneği. Ya da her ikisini seçebilirsiniz **e-posta** veya **kullanıcı kimliği** hello kullanıcı özniteliği olarak. Bizim örneğimizde, biz seçili **e-posta** biz hello kullanıcı tanımlayıcısı talep hello ile eşlenmiş olduğundan **userprincipalname** hello özniteliğinde **kullanıcı öznitelikleri** hello bölümünde Azure portalı. Bu, toohello SAP Business nesnesi bulut uygulaması her başarılı SAML yanıt olarak gönderilen bir benzersiz kullanıcı e-posta, sağlar.

    ![Kullanıcı özniteliğini seçin](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. Merhaba hello kimlik sağlayıcısı (4. adım), tooverify hello hesabıyla **oturum açma kimlik bilgileri (e-posta)** kutusuna, hello kullanıcının e-posta adresi girin. Ardından, seçin **hesabı doğrula**. Merhaba sistem oturum açma kimlik bilgileri toohello kullanıcı hesabı ekler.

    ![E-posta girin ve Doğrula hesabı seçin](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. Select hello **kaydetmek** simgesi.

    ![Kaydet simgesine](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> Bu yönergelerde hello kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulamanızı ayarlama yaparken! Seçerek hello uygulama ekledikten sonra **Active Directory** > **kurumsal uygulamalar**seçin hello **çoklu oturum açma** sekmesi. Merhaba katıştırılmış hello belgelerinde erişebilirsiniz **yapılandırma** kısmına hello sayfanın hello. Daha fazla bilgi için bkz: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Britta Simon hello Azure portal adlı bir test kullanıcısı oluşturursunuz.

toocreate Azure AD'de bir sınama kullanıcısı:

1. Merhaba hello soldaki menüde Azure portal seçin **Azure Active Directory**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. Kullanıcıların, select toodisplay hello listesini **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda **Ekle**.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. Merhaba, **kullanıcı** iletişim kutusunda, aşağıdaki adımları tam hello:
 
    1. Merhaba, **adı** kutusuna **BrittaSimon**.

    2. Merhaba, **kullanıcı adı** kutusuna, hello kullanıcının Britta Simon hello e-posta adresi girin.

    3. Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.

    4. **Oluştur**’u seçin.

        ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Azure AD Kullanıcı oluşturma][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a>SAP Business nesnesi bulut test kullanıcısı oluşturma

TooSAP iş nesnesi bulut oturum önce azure AD kullanıcıları SAP Business nesnesi bulutta sağlanmalıdır. SAP Business nesnesi bulutta sağlama bir el ile bir görevdir.

tooprovision bir kullanıcı hesabı:

1. İçinde tooyour SAP Business nesnesi bulut şirket site yönetici olarak oturum açın.

2. Seçin **menü** > **güvenlik** > **kullanıcılar**.

    ![Çalışanı ekleyin](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. Merhaba üzerinde **kullanıcılar** seçme sayfası, yeni kullanıcı ayrıntılarını tooadd,  **+** . 

    ![Kullanıcılar Sayfası Ekle](./media/active-directory-saas-sapboc-tutorial/user4.png)

    Ardından, hello aşağıdaki adımları tamamlayın:

    1. Merhaba, **kullanıcı kimliği** kutusuna, gibi hello kullanıcının hello kullanıcı Kimliğini girin **Britta**.

    2. Merhaba, **ad** kutusuna, gibi hello ilk hello kullanıcı adını girin **Britta**.

    3. Merhaba, **SOYADI** kutusuna, gibi hello son hello kullanıcı adını girin **Simon**.

    4. Merhaba, **GÖRÜNEN adı** kutusuna, hello kullanıcının tam adını hello gibi girin **Britta Simon**.

    5. Merhaba, **e-posta** kutusuna, hello kullanıcının hello e-posta adresi gibi girin  **brittasimon@contoso.com** .

    6. Merhaba üzerinde **Rollerini Seç** sayfasında hello hello kullanıcı için uygun rolü seçin ve ardından **Tamam**.

      ![Rol seç](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. Select hello **kaydetmek** simgesi.  


### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, hello kullanıcı Britta Simon toouse Azure AD çoklu oturum açma hello kullanıcı hesabı erişimi tooSAP iş nesnesi bulut vererek sağlar.

tooassign Britta Simon tooSAP iş nesnesi bulut:

1. Hello Azure portal, hello uygulamaları görünümünü açın ve toohello dizini görünümü gidin. Seçin **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **SAP Business nesnesi bulut**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. Merhaba soldaki menüde seçin **kullanıcılar ve gruplar**.

    ![Kullanıcıları ve grupları seçin][202] 

4. **Add (Ekle)** seçeneğini belirleyin. Ardından, hello **eklemek atama** sayfasında, **kullanıcılar ve gruplar**.

    ![Merhaba atama Ekle sayfası][203]

5. Merhaba üzerinde **kullanıcılar ve gruplar** sayfasında, kullanıcıların, select hello listesinde **Britta Simon**.

6. Merhaba üzerinde **kullanıcılar ve gruplar** sayfasında, **seçin**.

7. Merhaba üzerinde **eklemek atama** sayfasında, **atamak**.

![Merhaba kullanıcı rolü atayın][200] 
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test.

Merhaba erişim panelinde hello SAP Business nesnesi bulut döşeme seçtiğinizde tooyour SAP Business nesnesi bulut uygulama otomatik olarak imzalanmalıdır.

Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi Azure Active Directory ile toointegrate SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

