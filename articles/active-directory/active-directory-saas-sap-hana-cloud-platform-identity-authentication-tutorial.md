---
title: "Öğretici: SAP HANA bulut platformu kimlik doğrulama Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Nasıl tooconfigure çoklu oturum açmayı Azure Active Directory arasında ve SAP HANA bulut platformu kimlik doğrulama öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 2142770779ddb745555b47fc85b5457b573f9506
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a>Öğretici: SAP HANA bulut platformu kimlik doğrulama Azure Active Directory Tümleştirme

Bu öğreticide, nasıl toointegrate SAP öğrenin HANA bulut platformu kimlik doğrulaması Azure Active Directory'ye (Azure AD). SAP HANA bulut platformu kimlik doğrulama ana IDP hello gibi Azure AD kullanarak bir proxy IDP tooaccess SAP uygulamaları olarak kullanılır.

SAP HANA bulut platformu kimlik doğrulaması Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Access tooSAP uygulaması olan Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooSAP uygulamaları çoklu oturum açma (SSO) ile Azure AD hesaplarına etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Klasik Azure portalı Yönet

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).


## <a name="prerequisites"></a>Ön koşullar

SAP HANA bulut platformu kimlik doğrulaması ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- A **SAP HANA bulut platformu kimlik doğrulama** SSO abonelik etkin


>[!NOTE] 
>tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.
>

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
- Bir Azure AD deneme ortam yoksa, alabileceğiniz bir [bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.

Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. SAP HANA bulut platformu kimlik doğrulama hello Galerisi'nden ekleme
2. Yapılandırma ve Azure AD SSO test etme

Merhaba teknik ayrıntılara girmeden önce önemli toounderstand hello kavramları toolook adresindeki oluşturacağız olur. Merhaba SAP HANA bulut platformu kimlik doğrulaması ve Azure Active Directory Federasyon tooimplement SSO uygulamalar veya SAP uygulamaları ve Hizmetleri SAP HANA bulut Platform kimliği tarafından korunan ile AAD (olarak bir IDP) tarafından korunan hizmetler arasında sağlar Kimlik doğrulaması.

Şu anda, SAP HANA bulut platformu kimlik doğrulama bir Proxy Kimlik sağlayıcısı tooSAP uygulamalar olarak davranır. Azure Active Directory kimlik sağlayıcısı bu kurulumunda önde gelen hello sırayla görür. 

Aşağıdaki diyagramda hello bunu göstermektedir:    

![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

Bu kurulum ile SAP HANA bulut platformu kimlik doğrulama kiracınızı Azure Active Directory'de güvenilir bir uygulama olarak yapılandırılır. 

Daha sonra tüm SAP uygulamaları ve Hizmetleri bu şekilde aracılığıyla tooprotect istediğiniz hello SAP HANA bulut platformu kimlik doğrulama yönetim konsolunda yapılandırılan!

Bu erişim izni verme tooSAP uygulamalar için yetkilendirme anlamına gelir ve böyle bir kurulum (olarak Azure Active Directory'de karşılıklı tooconfiguring yetkilendirme) için SAP HANA bulut platformu kimlik doğrulama gereksinimlerini tootake yerine Hizmetleri.

SAP HANA bulut platformu kimlik doğrulama hello Azure Active Directory Marketi üzerinden bir uygulama olarak yapılandırarak, gerekli bireysel talepler yapılandırma care of tootake gerekmeyen / SAML onaylar ve dönüşümleri gerekli tooproduce bir SAP uygulamaları için geçerli bir kimlik doğrulama belirteci.

>[!NOTE] 
>Şu anda Web SSO her iki taraf tarafından yalnızca test edilmiştir. Uygulama API veya API API iletişimi için gerekli akışları çalışması gerekir, ancak, henüz test edilmemiştir. Bunlar bir sonraki etkinliklere bir parçası olarak test edilir.
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-hello-gallery"></a>SAP HANA bulut platformu kimlik doğrulama hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme SAP HANA bulut platformu kimlik doğrulama, hello galeri tooyour yönetilen SaaS uygulamaları listesinden tooadd SAP HANA bulut platformu kimlik doğrulaması gerekir.

**SAP HANA bulut platformu kimlik doğrulama hello galerisinden tooadd hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, [ **Azure Yönetim Portalı**](https://portal.azure.com), üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **Ekle** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **SAP HANA bulut platformu kimlik doğrulama**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. Merhaba Sonuçlar panelinde seçin **SAP HANA bulut platformu kimlik doğrulama**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme
Bu bölümde, yapılandırma ve SAP HANA bulut Platform kimliği "Britta Simon" adlı bir test kullanıcı tabanlı kimlik doğrulaması ile Azure AD SSO test etme.

SSO toowork için hangi hello karşılık gelen SAP HANA bulut platformu kimlik doğrulama içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve SAP HANA bulut platformu kimlik doğrulama hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** SAP HANA bulut platformu kimlik doğrulama içinde.

tooconfigure ve SAP HANA bulut platformu kimlik doğrulaması ile Azure AD SSO test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[SAP HANA bulut platformu kimlik doğrulama test kullanıcısı oluşturma](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)**  -toohave Britta Simon her bağlantılı toohello Azure AD gösterimidir SAP HANA bulut platformu kimlik doğrulama olarak, karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-sso"></a>Azure AD SSO yapılandırma

Bu bölümdeki hello Azure Yönetim Portalı'nda Azure AD SSO'yu etkinleştirmek ve çoklu oturum açma, SAP HANA bulut platformu kimlik doğrulama uygulamanızda yapılandırın.

SAP HANA bulut platformu kimlik doğrulama uygulaması hello SAML onaylar belirli bir biçimde bekliyor. Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm. Ekran aşağıdaki hello bunun bir örneği gösterir.

![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

**SAP HANA bulut platformu kimlik doğrulaması ile Azure AD SSO tooconfigure hello aşağıdaki adımları gerçekleştirin:**

1. Hello üzerinde hello Azure Yönetim Portalı'nda **SAP HANA bulut platformu kimlik doğrulama** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın][5]

3. Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** SAP uygulamanız bir öznitelik örneğin "firstName" görüyorsa iletişim. Merhaba SAML belirteci öznitelikleri iletişim kutusunda hello "firstName" özniteliğini ekleyin.
 1. Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.
 
    ![Çoklu oturum açmayı yapılandırın][6]

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. Merhaba, **öznitelik adı** metin kutusuna, türü hello öznitelik adı "ad".
 3. Merhaba gelen **öznitelik değeri** listesinde, select hello öznitelik değeri "user.givenname".
 4. **Tamam**’a tıklayın.

4. Merhaba üzerinde **SAP HANA bulut Platform kimliği kimlik doğrulaması etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. Merhaba, **oturum üzerinde URL'si** metin kutusuna, hello oturum hello SAP uygulama için URL'yi yazın.
 2. Merhaba, **tanımlayıcısı** metin kutusuna, düzeni izleyen türü başlangıç değeri:`<entity-id>.accounts.ondemand.com` 
    * Bu değer bilmiyorsanız, lütfen hello SAP HANA bulut platformu kimlik doğrulama belgeleri izleyin [Kiracı SAML 2.0 yapılandırma](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).

5. Merhaba üzerinde **SAP HANA bulut Platform kimliği kimlik doğrulama Yapılandırması** 'yi tıklatın **SAP HANA bulut platformu kimlik doğrulama** tooopen **oturum açmayapılandırma** iletişim. Ardından, tıklatın **SAML XML meta verilerini** ve hello dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. Uygulamanız için yapılandırılmış SSO tooget tooSAP HANA bulut Platform kimliği kimlik doğrulama yönetim konsolunda gidin. Merhaba URL deseni takip hello sahiptir:`https://<tenant-id>.accounts.ondemand.com/admin`
 * Ardından hello belgelerine SAP HANA bulut platformu kimlik doğrulama üzerinde çok izleyin[SAP HANA bulut platformu kimlik doğrulaması sırasında Kurumsal kimlik sağlayıcısı yapılandırma Microsoft Azure AD](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html). 

7. Hello Azure Yönetim Portalı'nda tıklatın **kaydetmek** düğmesi.
8. Yalnızca tooadd isterseniz ve SSO'yu etkinleştirmek için başka bir SAP uygulama adımları izleyerek hello devam edin. SAP HANA bulut platformu kimlik doğrulama başka bir kopyası hello bölüm "Ekleme SAP HANA bulut platformu kimlik doğrulama hello galerisinden" tooadd altındaki adımları yineleyin.
9. Merhaba üzerinde hello Azure Yönetim Portalı'nda **SAP HANA bulut platformu kimlik doğrulama** uygulama tümleştirme sayfasını tıklatın **bağlantılı oturum açma**.

    ![Bağlantılı oturum açma özelliğini yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. Ardından, hello yapılandırmayı kaydedin.

>[!NOTE] 
>Merhaba yeni uygulama hello önceki SAP uygulamasının hello SSO yapılandırmasını özelliğinden yararlanır. Lütfen emin olun kullanım hello hello SAP HANA bulut Platform kimliği kimlik doğrulama yönetim konsolunu aynı Kurumsal kimlik sağlayıcıları.
>

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Merhaba amacı, bu bölümde toocreate bir sınama kullanıcısı Britta Simon adlı hello yeni Portalı'nda ' dir.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.
  2. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.
  3. Seçin **Göster parola** ve hello hello değerini yazma **parola**.
  4. **Oluştur**'a tıklayın. 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a>SAP HANA bulut platformu kimlik doğrulama test kullanıcısı oluşturma

SAP HANA bulut platformu kimlik doğrulaması bir kullanıcı toocreate gerek yoktur. Hello Azure AD kullanıcı deposunda kullanıcılar hello SSO işlevini kullanabilirsiniz.

SAP HANA bulut platformu kimlik doğrulama hello Kimlik Federasyonu seçeneğini destekler. Merhaba Kurumsal kimlik sağlayıcısı tarafından kimliği doğrulanmış hello kullanıcılar hello kullanıcı deposu, SAP HANA bulut platformu kimlik doğrulama, yoksa bu seçenek hello uygulama toocheck sağlar. 

Merhaba varsayılan ayarı hello Kimlik Federasyonu seçeneği devre dışı bırakılır. Kimlik Federasyonu etkinleştirilirse, SAP HANA bulut platformu kimlik doğrulama içeri aktarılan yalnızca hello mümkün tooaccess Merhaba uygulaması kullanıcılardır. 

Nasıl tooenable veya devre dışı bırak SAP HANA bulut platformu kimlik doğrulaması ile Kimlik Federasyonu bakın SAP HANA bulut platformu kimlik doğrulaması ile Kimlik Federasyonu etkinleştirme hakkında daha fazla bilgi için [Kimlik Federasyonu yapılandırma Merhaba kullanıcı deposu, SAP HANA bulut platformu kimlik doğrulama ile. ](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, kendi erişim tooSAP HANA bulut platformu kimlik doğrulama vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooSAP HANA bulut platformu kimlik doğrulama, hello aşağıdaki adımları gerçekleştirin:**

1. Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **SAP HANA bulut platformu kimlik doğrulama**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    

### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, Azure AD SSO yapılandırmanızı hello erişim paneli kullanarak sınayın.

Merhaba SAP HANA bulut platformu kimlik doğrulama hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour SAP HANA bulut platformu kimlik doğrulama uygulaması almanız gerekir.


## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png