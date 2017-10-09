---
title: "Öğretici: Azure Active Directory Tümleştirme LinkedIn yükseltmesine ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory arasındaki LinkedIn Yükselt."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 189bd72c230be7dc0c0b934f94ea01e84af9ad23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a>Öğretici: Azure Active Directory Tümleştirme LinkedIn yükseltmesine ile

Bu öğreticide, bilgi toointegrate LinkedIn yükseltmesine nasıl Azure Active Directory (Azure AD) ile.

LinkedIn yükseltmesine Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooLinkedIn yükseltme sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooLinkedIn yükseltme (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure LinkedIn yükseltmesine ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir LinkedIn yükseltmesine çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. LinkedIn yükseltmesine hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-linkedin-elevate-from-hello-gallery"></a>LinkedIn yükseltmesine hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme LinkedIn yükseltmesine, tooadd LinkedIn yükseltmesine hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd LinkedIn yükseltmesine hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **Ekle** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **LinkedIn yükseltmesine**. Sonuçları panelinden tıklatın **LinkedIn yükseltmesine** tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı LinkedIn yükseltmesine ile test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen LinkedIn yükseltmesine de tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı LinkedIn yükseltmesine arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** LinkedIn yükseltmesine içinde.

tooconfigure ve LinkedIn yükseltmesine ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Bir LinkedIn yükseltmesine test kullanıcısı oluşturma](#creating-a-linkedin-elevate-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma LinkedIn yükseltmesine uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma LinkedIn yükseltmesine ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Merhaba üzerinde hello Azure Yönetim Portalı'nda **LinkedIn yükseltmesine** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. Bir farklı web tarayıcısı penceresinde, bir yönetici olarak oturum açma tooyour LinkedIn yükseltmesine Kiracı.

4. İçinde **hesap Merkezi'nde**, tıklatın **genel ayarları** altında **ayarları**. Ayrıca, seçin **yükseltme - AAD Test yükseltmesine** hello aşağı açılan listeden.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. Tıklayın **veya burayı tıklatın tooload ve kopyalama tek tek alanların hello formundan** kopyalayıp **varlık kimliği** ve **onaylama tüketici erişim (ACS) URL'si**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. Azure Portal'da altında **LinkedIn yükseltme etki alanı ve URL'leri**, hello tooconfigure SSO istiyorsanız aşağıdaki adımları gerçekleştirin içinde **IDP başlatılan** modu

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, hello girin **varlık kimliği** LinkedIn portalından kopyalandığından 

    b. Merhaba, **yanıt URL'si** metin kutusuna, hello girin **onaylama tüketici erişim (ACS) Url** LinkedIn portalından kopyalandığından

7. Tooconfigure SSO istiyorsanız içinde **SP tarafından başlatılan**, sonra hello yapılandırma bölümündeki Gelişmiş URL Göster ayarı seçeneğini tıklatın ve hello oturum URL deseni takip hello ile yapılandırın:

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. LinkedIn yükseltmesine uygulamanızı hello SAML onaylar, tooadd özel öznitelik eşlemelerini tooyour SAML belirteci öznitelikleri yapılandırma gerektiren belirli bir biçimde, bekliyor. Ekran aşağıdaki hello bunun bir örneği gösterir. Merhaba varsayılan değerini **kullanıcı tanımlayıcısı** olan **user.userprincipalname** ancak LinkedIn yükseltmesine hello kullanıcının e-posta adresiyle eşleşen bu toobe bekliyor. Bunun için kullanabileceğiniz **user.mail** özniteliği hello listeden veya kuruluş yapılandırmanızı temel alarak hello uygun öznitelik değeri kullanın. 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. İçinde **kullanıcı öznitelikleri** 'yi tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** ve hello özniteliklerini ayarlayın. Adlı başka bir talep tooadd gerek **departmanı** ve hello değeri gereken çok eşlenen toobe**user.department**.

    | Öznitelik adı | Öznitelik değeri |
    | --- | --- |    
    | Bölüm| User.Department |

      ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      a. Aşağıdaki - gösterildiği gibi hello departmanı özniteliği Ekle'ye tıklayın Ekle özniteliği tooopen hello özniteliği ayrıntılar sayfası

      ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      b. Tıklayın **Tamam** toosave hello özniteliği.

      c. Değişiklik hello hello özniteliğin adını **emailaddress** çok**e-posta**.


10. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. **Kaydet** düğmesine tıklayın.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. Çok Git**LinkedIn yönetici ayarları** bölümü. Yalnızca XML karşıya dosya seçeneği hello üzerinde tıklayarak hello Azure portal ' yüklenen hello XML dosyasını karşıya yükleyin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. Tıklatın **üzerinde** tooenable SSO. SSO durum değişecektir **bağlı** çok**bağlandı**

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın. 

### <a name="creating-a-linkedin-elevate-test-user"></a>Bir LinkedIn yükseltmesine test kullanıcısı oluşturma

Bağlantılı yükseltmesine uygulama zaman kullanıcı sağlama ve kimlik doğrulama kullanıcılar hello uygulamada otomatik olarak oluşturulacak sonra hemen destekler. Merhaba yönetici ayarları sayfasında hello LinkedIn yükseltmesine portal Çevir hello anahtar **otomatik olarak ata lisansları** zaman sağlama sadece tooactive tooenable ve bu ayrıca atamak lisans toohello kullanıcı.

   ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, kendi erişim tooLinkedIn yükseltme vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooLinkedIn yükseltme, hello aşağıdaki adımları gerçekleştirin:**

1. Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **LinkedIn yükseltmesine**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba LinkedIn yükseltmesine döşemeyi hello erişim paneli tıklattığınızda hello Azure oturum açma sayfasına almanız gerekir ve üzerinde başarılı oturum açma sonra bunu LinkedIn yükseltmesine uygulamanıza almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [Öğretici: LinkedIn yükseltmesine otomatik kullanıcı hazırlama Azure Active Directory ile yapılandırma](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_203.png
