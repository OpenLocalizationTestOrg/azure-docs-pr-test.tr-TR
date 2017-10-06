---
title: "Öğretici: Azure Active Directory Tümleştirme ile FreshDesk | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile FreshDesk arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 577a5eb6d9b1bc03030a2b47f63d375869c903bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a>Öğretici: Azure Active Directory Tümleştirme FreshDesk ile

Bu öğreticide, bilgi nasıl toointegrate FreshDesk Azure Active Directory'ye (Azure AD).

FreshDesk Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooFreshDesk sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooFreshDesk (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure FreshDesk ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir FreshDesk çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden FreshDesk ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-freshdesk-from-hello-gallery"></a>Merhaba Galerisi'nden FreshDesk ekleme
Azure AD'ye tooconfigure hello tümleştirme FreshDesk, tooadd FreshDesk hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd FreshDesk hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **Ekle** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **FreshDesk**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. Merhaba Sonuçlar panelinde seçin **FreshDesk**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı FreshDesk sınayın.

Tek toowork'ın oturum açma hangi hello karşılık gelen FreshDesk içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı FreshDesk hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** FreshDesk içinde.

tooconfigure ve FreshDesk ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[FreshDesk test kullanıcısı oluşturma](#creating-a-freshdesk-test-user)**  -toohave karşılık gelen her bağlantılı toohello Azure AD gösterimidir FreshDesk içinde Britta Simon biri.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma FreshDesk uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma ile FreshDesk, hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba üzerinde hello Azure Yönetim Portalı'nda **FreshDesk** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. Merhaba üzerinde **FreshDesk etki alanı ve URL'leri** bölümünde, lütfen hello girin **oturum açma URL'si** olarak: `https://<tenant-name>.freshdesk.com` veya başka bir değer Freshdesk önerdiği.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > Lütfen bu gerçek değer olmadığını unutmayın. Değerin gerçek oturum açma URL'si ile güncelleştirmeniz gerekir. Kişi [FreshDesk istemci destek ekibi](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) bu değeri alınamıyor.  

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika** ve hello sertifika bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. Merhaba üzerinde **FreshDesk yapılandırma** 'yi tıklatın **yapılandırma FreshDesk** tooopen yapılandırma oturum açma penceresi. Hello hello SAML çoklu oturum açma hizmet URL'si ve Sign-Out URL'sini kopyalayın **hızlı başvuru** bölümü.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. Farklı web tarayıcısı penceresinde Freshdesk şirket sitenize yönetici olarak oturum açın.

8. Hello içinde hello üst menüsünde **yönetici**.
   
   ![Yönetici](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "yönetici")

9. Merhaba, **genel ayarları** sekmesini tıklatın, **güvenlik**.
   
   ![Güvenlik](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "güvenlik")

10. Merhaba, **güvenlik** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![Çoklu oturum açmayı](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "çoklu oturum açmayı")
   
    a. İçin **çoklu oturum açma (SSO)**seçin **üzerinde**.

    b. Seçin **SAML SSO**.

    c. Türü hello **SAML çoklu oturum açma hizmet URL'si** hello Azure portalından kopyalandığından **SAML oturum açma URL'si** metin kutusu.

    d. Türü hello **Sign-Out URL** hello Azure portalından kopyalandığından **oturum kapatma URL'si** metin kutusu.

    e. Kopya hello **parmak izi** değer Azure Portalı'ndan indirilen hello sertifikasından ve hello yapıştırma **güvenlik sertifika parmak izi** metin kutusu.  
 
    >[!TIP]
    >Daha fazla ayrıntı için bkz: [nasıl tooretrieve bir sertifikanın parmak izi değeri](http://youtu.be/YKQF266SAxI). 
    
    f. **Kaydet** düğmesine tıklayın.


### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-freshdesk-test-user"></a>FreshDesk test kullanıcısı oluşturma

FreshDesk içine sipariş tooenable Azure AD kullanıcıların toolog bunların FreshDesk sağlanmalıdır.  
FreshDesk Hello durumda sağlama bir el ile bir görevdir.

**bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:**

1. İçinde tooyour oturum **Freshdesk** Kiracı.
2. Hello içinde hello üst menüsünde **yönetici**.
   
   ![Yönetici](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "yönetici")

3. Merhaba, **genel ayarları** sekmesini tıklatın, **aracıları**.
   
   ![Aracıları](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "aracıları")

4. Tıklatın **yeni aracı**.
   
    ![Yeni aracı](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "yeni aracı")

5. Merhaba aracı bilgileri iletişim kutusunda hello aşağıdaki adımları gerçekleştirin:
   
   ![Aracı bilgilerini](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "aracısı bilgileri")
   
   a. Merhaba, **tam adı** metin kutusuna, tür hello tooprovision istediğiniz hello Azure AD hesabının adını.

   b. Merhaba, **e-posta** metin kutusuna, türü hello Azure AD e-posta adresini istediğiniz hello Azure AD hesabının tooprovision.

   c. Merhaba, **başlık** metin kutusuna, tooprovision istediğiniz hello Azure AD hesabının türü hello başlığı.

   d. Seçin **aracıları rolü**ve ardından **atamak**.
       
   e. **Kaydet** düğmesine tıklayın.     
   
    >[!NOTE]
    >Hello Azure AD hesap sahibi etkinleştirilmeden önce bir bağlantı tooconfirm hello hesabını içeren bir e-posta alırsınız. 
    > 
    
    >[!NOTE]
    >API AAD kullanıcı hesaplarının Freshdesk tooprovision tarafından sağlanan veya herhangi diğer Freshdesk kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz. tooFreshDesk.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, kendi erişim tooBox vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooFreshDesk hello aşağıdaki adımları gerçekleştirin:**

1. Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **FreshDesk**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba FreshDesk hello erişim paneli parçasında tıkladığınızda, oturum açma sayfası tooget açan tooyour FreshDesk uygulama almanız gerekir.

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

