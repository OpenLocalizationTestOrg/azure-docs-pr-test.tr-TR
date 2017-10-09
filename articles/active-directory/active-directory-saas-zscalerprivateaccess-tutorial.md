---
title: "Öğretici: Azure Active Directory Tümleştirme ile Zscaler özel erişim (ZPA) | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Zscaler özel erişim (ZPA) arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 83711115-1c4f-4dd7-907b-3da24b37c89e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 0370cff60c8ac15bd1919acccc924da1e50dc45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-private-access-zpa"></a>Öğretici: Azure Active Directory Tümleştirme ile Zscaler özel erişim (ZPA)

Bu öğreticide, bilgi nasıl toointegrate Zscaler özel erişim (ZPA) Azure Active Directory'ye (Azure AD).

Zscaler özel erişim (ZPA) Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooZscaler özel erişim (ZPA) sahip Azure AD'de kontrol edebilirsiniz
- Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooZscaler özel erişim (ZPA) (çoklu oturum açma) etkinleştirebilirsiniz
- Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

Azure AD Tümleştirmesi ile Zscaler özel erişim (ZPA) tooconfigure, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Zscaler özel erişim (ZPA) çoklu oturum açma etkin abonelik


> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.


Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Zscaler özel erişim (ZPA) ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama


## <a name="adding-zscaler-private-access-zpa-from-hello-gallery"></a>Merhaba Galerisi'nden Zscaler özel erişim (ZPA) ekleme
Azure AD'ye tooconfigure hello tümleştirmesi, Zscaler özel erişim (ZPA), tooadd Zscaler özel erişim (ZPA) hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Zscaler özel erişim (ZPA) hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **Ekle** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Zscaler özel erişim (ZPA)**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_001.png)

5. Merhaba Sonuçlar panelinde seçin **Zscaler özel erişim (ZPA)**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ile Zscaler özel erişim ("Britta Simon" adlı bir test kullanıcı tabanlı ZPA) test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen içinde Zscaler özel erişim (ZPA) tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı içinde Zscaler özel erişim (ZPA) arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** içinde Zscaler özel erişim (ZPA).

tooconfigure ve test ile Zscaler özel erişim (ZPA) Azure AD çoklu oturum açma, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Zscaler özel erişim (ZPA) test kullanıcısı oluşturma](#creating-a-zscaler-private-access-(zpa)-test-user)**  -toohave Britta Simon içinde Zscaler özel erişim (her bağlantılı toohello Azure AD gösterimi olan ZPA), karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma Zscaler özel erişim (ZPA) uygulamanızda yapılandırın.

**tooconfigure ile Zscaler özel erişim (ZPA), Azure AD çoklu oturum açma hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba üzerinde hello Azure Yönetim Portalı'nda **Zscaler özel erişim (ZPA)** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_300.png)
    
3. Merhaba üzerinde **Zscaler özel erişim (ZPA) etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_01.png)

    a. Merhaba, **oturum üzerinde URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, türü:`https://samlsp.private.zscaler.com/auth/metadata`

    > [!NOTE] 
    > Lütfen bu hello gerçek değerler olmadığına dikkat edin. Bu değerlerle hello gerçek oturum açma URL'si ve tanımlayıcı tooupdate sahip. Burada, toouse hello benzersiz değer URL'nin hello tanımlayıcı öneririz. Kişi [Zscaler özel erişim (ZPA) destek ekibi](https://help.zscaler.com/zpa-submit-ticket) tooget bu değerleri.

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **yeni sertifika oluştur**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_400.png)   

5. Merhaba üzerinde **yeni sertifika oluştur** iletişim kutusunda, hello Takvim simgesine tıklayın ve bir **sona erme tarihi**. Ardından **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_500.png)

6. Merhaba üzerinde **SAML imzalama sertifikası** bölümünde, select **yeni sertifika etkin hale getirin** tıklatıp **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_02.png)

7. Merhaba açılır pencere üzerinde **geçiş sertifikası** penceresinde tıklatın **Tamam**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_600.png)

8. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_03.png) 

9. Farklı web tarayıcısı penceresinde Zscaler özel erişim (ZPA) şirket sitenize yönetici olarak oturum açın.

10. Çok gidin**yönetici** ve ardından **IDP yapılandırma**.

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_04.png)

11. Merhaba, **IDP yapılandırma** 'yi tıklatın **yeni IDP Yapılandırması Ekle**.

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_05.png)

12. Merhaba, **yeni IDP yapılandırma** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_06.png)

    a. Tıklatın **Dosya Seç** ve indirilen meta veri dosyasını karşıya yükleyin.

    b. Tıklatın **kaydetmek** düğmesi.
    


### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_01.png) 

2. Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_02.png) 

3. Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın. 



### <a name="creating-a-zscaler-private-access-zpa-test-user"></a>Zscaler özel erişim (ZPA) test kullanıcısı oluşturma

Bu bölümde, Britta Simon Zscaler özel erişim (ZPA içinde) adlı bir kullanıcı oluşturun. Lütfen çalışmak [Zscaler özel erişim (ZPA) destek ekibi](https://help.zscaler.com/zpa-submit-ticket) tooadd hello kullanıcılar hello Zscaler özel erişim (ZPA) Platform.


### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, kendi özel erişim (ZPA) erişim tooZscaler vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooZscaler özel erişim (ZPA), hello aşağıdaki adımları gerçekleştirin:**

1. Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Zscaler özel erişim (ZPA)**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_50.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    


### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Zscaler özel erişim (ZPA) hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Zscaler özel erişim (ZPA) uygulama almanız gerekir.


## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_203.png