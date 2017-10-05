---
title: "Öğretici: SAP HANA bulut platformu kimlik doğrulama Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve SAP HANA bulut platformu kimlik doğrulama arasında yapılandırmayı öğrenin."
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
ms.openlocfilehash: 7799bf03cc6705f805a48f329a265a3d84bed55f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a>Öğretici: SAP HANA bulut platformu kimlik doğrulama Azure Active Directory Tümleştirme

Bu öğreticide, SAP HANA bulut platformu kimlik doğrulaması Azure Active Directory (Azure AD) ile tümleştirme öğrenin. SAP HANA bulut platformu kimlik doğrulama, bir proxy sunucu olarak IDP ana IDP Azure AD kullanarak SAP uygulamalarına erişmek için kullanılır.

SAP HANA bulut platformu kimlik doğrulaması Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:

- SAP uygulama erişimi, Azure AD'de kontrol edebilirsiniz
- Otomatik olarak uygulamaları çoklu oturum açma (SSO) ile Azure AD hesaplarına SAP açan kullanıcılarınıza etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - Klasik Azure portalı Yönet

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).


## <a name="prerequisites"></a>Ön koşullar

SAP HANA bulut platformu kimlik doğrulaması ile Azure AD tümleştirme yapılandırmak için aşağıdaki öğeleri gerekir:

- Bir Azure AD aboneliği
- A **SAP HANA bulut platformu kimlik doğrulama** SSO abonelik etkin


>[!NOTE] 
>Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.
>

Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
- Bir Azure AD deneme ortam yoksa, alabileceğiniz bir [bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.

Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:

1. Galeriden SAP HANA bulut platformu kimlik doğrulama ekleme
2. Yapılandırma ve Azure AD SSO test etme

Teknik ayrıntılara girmeden önce bakmak oluşturacağız kavramları anlamanız önemlidir. SAP HANA bulut platformu kimlik doğrulaması ve Azure Active Directory Federasyon, uygulamalar veya SAP uygulamaları ve Hizmetleri SAP HANA bulut platformu kimlik doğrulama tarafından korunan ile AAD (olarak bir IDP) tarafından korunan hizmetler arasında SSO uygulanmasını sağlar.

Şu anda, SAP HANA bulut platformu kimlik doğrulama SAP uygulamaları için bir Proxy Kimlik sağlayıcısı gibi davranır. Azure Active Directory sırayla bu kurulumunda başında kimlik sağlayıcısı gibi davranır. 

Aşağıdaki diyagram bu gösterir:    

![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

Bu kurulum ile SAP HANA bulut platformu kimlik doğrulama kiracınızı Azure Active Directory'de güvenilir bir uygulama olarak yapılandırılır. 

Daha sonra tüm SAP uygulamalar ve hizmetler bu şekilde korumak istediğiniz SAP HANA bulut platformu kimlik doğrulama yönetim konsolunda yapılandırılan!

Başka bir deyişle, SAP uygulamaları ve hizmetlerine erişim izni verme için yetkilendirme (yetkilendirme Azure Active Directory'de yapılandırma) aksine Kurulum SAP HANA bulut platformu kimlik doğrulama yerinde yapması gerekmez.

SAP HANA bulut platformu kimlik doğrulaması Azure Active Directory Marketi üzerinden bir uygulama olarak yapılandırarak, gerekli bireysel talepler yapılandırmayı dikkatli gerekmez / SAML onaylar ve dönüşümleri gerekli SAP uygulamaları için geçerli bir kimlik doğrulama belirteci üretmek.

>[!NOTE] 
>Şu anda Web SSO her iki taraf tarafından yalnızca test edilmiştir. Uygulama API veya API API iletişimi için gerekli akışları çalışması gerekir, ancak, henüz test edilmemiştir. Bunlar bir sonraki etkinliklere bir parçası olarak test edilir.
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-the-gallery"></a>SAP HANA bulut platformu kimlik doğrulama Galerisi'nden ekleme
SAP HANA bulut platformu kimlik doğrulama tümleştirme Azure AD'ye yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden SAP HANA bulut platformu kimlik doğrulama eklemeniz gerekir.

**SAP HANA bulut platformu kimlik doğrulama Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**

1. İçinde [ **Azure Yönetim Portalı**](https://portal.azure.com), sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Gidin **kurumsal uygulamalar**. Ardından **tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **Ekle** iletişim kutusunun üst kısmında düğmesi.

    ![Uygulamalar][3]

4. Arama kutusuna **SAP HANA bulut platformu kimlik doğrulama**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. Sonuçlar panelinde seçin **SAP HANA bulut platformu kimlik doğrulama**ve ardından **Ekle** uygulama eklemek için düğmesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme
Bu bölümde, yapılandırma ve SAP HANA bulut Platform kimliği "Britta Simon" adlı bir test kullanıcı tabanlı kimlik doğrulaması ile Azure AD SSO test etme.

Çalışmak SSO için Azure AD karşılık gelen kullanıcı SAP HANA bulut platformu kimlik doğrulama için bir kullanıcı Azure AD'de nedir bilmesi gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının SAP HANA bulut platformu kimlik doğrulama ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.

Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** SAP HANA bulut platformu kimlik doğrulama içinde.

Yapılandırmak ve SAP HANA bulut platformu kimlik doğrulaması ile Azure AD SSO sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.
3. **[SAP HANA bulut platformu kimlik doğrulama test kullanıcısı oluşturma](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)**  - Britta Simon, karşılık gelen her, Azure AD gösterimine bağlı SAP HANA bulut platformu kimlik doğrulama sağlamak için.
4. **[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.

### <a name="configuring-azure-ad-sso"></a>Azure AD SSO yapılandırma

Bu bölümde, Azure Yönetim Portalı'nda Azure AD SSO'yu etkinleştirmek ve çoklu oturum açma, SAP HANA bulut platformu kimlik doğrulama uygulamanızda yapılandırın.

SAP HANA bulut platformu kimlik doğrulama uygulaması SAML onaylar belirli bir biçimde bekliyor. Bu öznitelik değerlerini yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm. Aşağıdaki ekran görüntüsünde bunun bir örneği gösterir.

![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

**SAP HANA bulut platformu kimlik doğrulaması ile Azure AD SSO yapılandırmak için aşağıdaki adımları gerçekleştirin:**

1. Azure Yönetim Portalı'nda üzerinde **SAP HANA bulut platformu kimlik doğrulama** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.
 
    ![Çoklu oturum açmayı yapılandırın][5]

3. İçinde **kullanıcı öznitelikleri** bölümünde **çoklu oturum açma** SAP uygulamanız bir öznitelik örneğin "firstName" görüyorsa iletişim. SAML belirteci öznitelikleri iletişim kutusunda, "ad" özniteliğini ekleyin.
 1. Tıklatın **Ekle özniteliği** açmak için **özniteliği eklemek** iletişim.
 
    ![Çoklu oturum açmayı yapılandırın][6]

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. İçinde **öznitelik adı** metin kutusuna, öznitelik adı "ad" yazın.
 3. Gelen **öznitelik değeri** listesinde, öznitelik değeri "user.givenname" seçin.
 4. **Tamam**’a tıklayın.

4. Üzerinde **SAP HANA bulut Platform kimliği kimlik doğrulaması etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. İçinde **oturum üzerinde URL'si** metin kutusuna, oturum SAP uygulama için URL'yi yazın.
 2. İçinde **tanımlayıcısı** metin kutusuna, desen aşağıdaki değeri yazın:`<entity-id>.accounts.ondemand.com` 
    * Bu değer bilmiyorsanız, lütfen SAP HANA bulut platformu kimlik doğrulama belgeleri izleyin [Kiracı SAML 2.0 yapılandırma](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).

5. Üzerinde **SAP HANA bulut Platform kimliği kimlik doğrulama Yapılandırması** 'yi tıklatın **SAP HANA bulut platformu kimlik doğrulama** açmak için **yapılandırma oturum açma** iletişim. Ardından, tıklatın **SAML XML meta verilerini** ve dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. Uygulamanız için yapılandırılmış SSO almak için SAP HANA bulut Platform kimlik kimlik doğrulama yönetim konsoluna gidin. URL aşağıdaki deseni vardır:`https://<tenant-id>.accounts.ondemand.com/admin`
 * Ardından, SAP HANA bulut platformu kimlik doğrulama için belgeleri takip [SAP HANA bulut platformu kimlik doğrulaması sırasında Kurumsal kimlik sağlayıcısı yapılandırma Microsoft Azure AD](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html). 

7. Azure Yönetim Portalı'nda tıklatın **kaydetmek** düğmesi.
8. Yalnızca ekleyin ve başka bir SAP uygulama için SSO'yu etkinleştirmek isterseniz, aşağıdaki adımları devam edin. "Ekleme SAP HANA bulut platformu kimlik doğrulama galerisinden" bölümü altındaki adımları yineleyin SAP HANA bulut platformu kimlik doğrulama başka bir örneği eklemek için.
9. Azure Yönetim Portalı'nda üzerinde **SAP HANA bulut platformu kimlik doğrulama** uygulama tümleştirme sayfasını tıklatın **bağlantılı oturum açma**.

    ![Bağlantılı oturum açma özelliğini yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. Yapılandırmayı kaydedin.

>[!NOTE] 
>Yeni uygulama önceki SAP uygulaması için SSO yapılandırma özelliğinden yararlanır. Lütfen, aynı Kurumsal kimlik sağlayıcıları SAP HANA bulut Platform kimliği kimlik doğrulama yönetim konsolunda kullandığınızdan emin olun.
>

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümün amacı, Britta Simon adlı yeni Portalı'nda bir test kullanıcı oluşturmaktır.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**

1. İçinde **Azure Yönetim Portalı**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. Git **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** kullanıcıların listesini görüntülemek için.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. İçinde **adı** metin kutusuna, türü **BrittaSimon**.
  2. İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.
  3. Seçin **Göster parola** ve değerini yazma **parola**.
  4. **Oluştur**'a tıklayın. 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a>SAP HANA bulut platformu kimlik doğrulama test kullanıcısı oluşturma

SAP HANA bulut Platform kimliği kimlik doğrulamasını bir kullanıcı oluşturmanız gerekmez. Azure AD kullanıcı deposunda kullanıcılar SSO işlevini kullanabilirsiniz.

SAP HANA bulut platformu kimlik doğrulama Kimlik Federasyonu seçeneğini destekler. Bu seçenek, Kurumsal kimlik sağlayıcısı tarafından kimliği doğrulanmış kullanıcılar kullanıcı deposu, SAP HANA bulut platformu kimlik doğrulama içinde olup olmadığını denetlemek için uygulamanın sağlar. 

Varsayılan ayar, Kimlik Federasyonu seçenek devre dışıdır. Kimlik Federasyonu etkinleştirilirse, SAP HANA bulut platformu kimlik doğrulama içeri aktarılan kullanıcıların uygulamaya erişmek kullanabilirsiniz. 

SAP HANA bulut platformu kimlik doğrulaması ile Kimlik Federasyonu etkinleştirme etkinleştirmek veya SAP HANA bulut platformu kimlik doğrulaması ile Kimlik Federasyonu devre dışı bırakma hakkında daha fazla bilgi için bkz: [Kimlik Federasyonu ile kullanıcı deposu, SAP HANA bulut platformu kimlik doğrulama yapılandırın.](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).

### <a name="assign-the-azure-ad-test-user"></a>Azure AD test kullanıcısı atayın

Bu bölümde, SAP HANA bulut platformu kimlik doğrulama için kendi erişim vererek, Azure çoklu oturum açma kullanılacak Britta Simon etkinleştirin.

![Kullanıcı atama][200] 

**SAP HANA bulut platformu kimlik doğrulama için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**

1. Azure Yönetim Portalı'nda uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Uygulamalar listesinde **SAP HANA bulut platformu kimlik doğrulama**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. Soldaki menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    

### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, erişim paneli kullanarak Azure AD SSO yapılandırmanızı sınayın.

Erişim paneli SAP HANA bulut platformu kimlik doğrulama parçasında tıklattığınızda, otomatik olarak SAP HANA bulut platformu kimlik doğrulama uygulamanız açan.


## <a name="additional-resources"></a>Ek kaynaklar

* [Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi](active-directory-saas-tutorial-list.md)
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