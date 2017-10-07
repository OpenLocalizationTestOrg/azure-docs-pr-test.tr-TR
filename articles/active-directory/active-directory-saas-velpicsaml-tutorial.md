---
title: "Öğretici: Azure Active Directory Tümleştirme Velpic SAML ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Velpic SAML arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 613947d8fe95113382a2cdc0f79ce9eda85a0127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a>Öğretici: Azure Active Directory Tümleştirme Velpic SAML ile

Bu öğreticide, bilgi nasıl toointegrate Velpic SAML Azure Active Directory'ye (Azure AD).

Azure AD ile Velpic SAML tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooVelpic SAML sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooVelpic SAML (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Velpic SAML ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Velpic SAML çoklu oturum açma etkin abonelik

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.
- Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Velpic SAML ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-velpic-saml-from-hello-gallery"></a>Merhaba Galerisi'nden Velpic SAML ekleme
Azure AD'ye tooconfigure hello tümleştirme Velpic SAML, tooadd Velpic SAML hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Velpic SAML hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Active Directory][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Uygulamalar][2]
    
3. Tıklatın **Ekle** hello iletişim hello üstte düğmesi.

    ![Uygulamalar][3]

4. Merhaba arama kutusuna yazın **Velpic SAML**.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. Merhaba Sonuçlar panelinde seçin **Velpic SAML**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırmanız ve Velpic SAML ile Azure AD çoklu oturum açmayı test "Britta Simon" adlı bir test kullanıcı tabanlı.

Tek toowork'ın oturum açma hangi hello karşılık gelen Velpic SAML içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Velpic SAML hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Velpic SAML içinde.

tooconfigure ve Velpic SAML ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Velpic SAML test kullanıcısı oluşturma](#creating-a-velpic-saml-test-user)**  -toohave Britta Simon her bağlantılı toohello Azure AD gösterimidir Velpic SAML içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma Velpic SAML uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma Velpic SAML ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Merhaba üzerinde hello Azure Yönetim Portalı'nda **Velpic SAML** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. Hello Hello ayrıntılarını girin **Velpic SAML etki alanı ve URL'leri** bölüm -

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, türü hello değeri olarak:`https://<sub-domain>.velpicsaml.net`

    b. Merhaba, **tanımlayıcısı** metin kutusuna, Yapıştır hello **'Çoklu oturum açma URL'si'** değeri`https://auth.velpic.com/saml/v2/<entity-id>/login`
    
    > [!NOTE]
    > Lütfen başlangıç oturum açma URL'si hello Velpic SAML ekibi tarafından sağlanacak ve tanımlayıcı değeri Velpic SAML tarafında hello SSO eklentisi yapılandırırken kullanılabilecek unutmayın. Velpic SAML uygulama sayfasından değer ve burada Yapıştır toocopy gerekir.

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. Hello Velpic SAML yapılandırma bölümü, oturum açma yapılandırma Velpic SAML tooopen yapılandırma penceresi'ı tıklatın. Merhaba SAML varlık kimliği hızlı başvuru bölümünde hello kopyalayın.

7. Farklı web tarayıcısı penceresinde Velpic SAML şirket sitenize yönetici olarak oturum açın.

8. Tıklayın **Yönet** sekmesinde ve çok Git**tümleştirme** ihtiyaç duyacağınız tooclick üzerinde bölüm **eklentileri** düğmesini toocreate yeni eklenti için oturum açma.

    ![Eklentisi](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. Tıklatın hello üzerinde **'Eklenti ekleme'** düğmesi.
    
    ![Eklentisi](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. Tıklatın hello üzerinde **SAML** döşeme hello eklentisi ekleyin sayfasında.
    
    ![Eklentisi](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. Merhaba yeni SAML eklentisini Hello adını girin ve hello tıklayın **'Ekle'** düğmesi.

    ![Eklentisi](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. Aşağıdaki gibi Hello ayrıntılarını girin:

    ![Eklentisi](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    a. Merhaba, **adı** metin kutusuna, SAML eklentisini hello adını yazın.

    b. Merhaba, **veren URL'si** metin kutusuna, Yapıştır hello **SAML varlık kimliği** hello kopyalanan **yapılandırma oturum açma** hello Azure portalı penceresi.

    c. Merhaba, **sağlayıcısı meta verileri yapılandırma** hello Azure portalından indirdiğiniz meta veri XML dosyasını karşıya yükleyin.

    d. Yalnızca zaman hello etkinleştirerek sağlama tooenable SAML seçebilirsiniz **'Otomatik oluştur yeni kullanıcılar'** onay kutusu. Bir kullanıcı Velpic yok ve bu bayrak etkin değil, Azure hello oturum açma başarısız olur. Merhaba bayrağı etkinleştirilmiş hello kullanıcı otomatik olarak ise Velpic oturum açma hello aynı anda sağlanacak. 

    e. Kopya hello **tek oturum açma URL'si** içinde hello metin kutusu ve Yapıştır Azure portal hello.
    
    f. **Kaydet** düğmesine tıklayın.

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-velpic-saml-test-user"></a>Velpic SAML test kullanıcısı oluşturma

Bu adım yalnızca zaman sağlama kullanıcı Merhaba uygulaması desteklediği genellikle gerekli değildir. Merhaba otomatik kullanıcı sağlamayı etkinleştirilmemişse, el ile kullanıcı oluşturma aşağıda açıklandığı gibi yapılabilir.

Velpic SAML şirket sitenizin yönetici olarak oturum açın ve aşağıdaki adımları gerçekleştirin:
    
1. Yönet sekmesini tıklatın ve tooUsers bölümüne gidin, sonra yeni düğmesi tooadd kullanıcılar'ı tıklatın.

    ![Kullanıcı Ekle](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. Merhaba üzerinde **"Yeni kullanıcı oluştur"** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin.

    ![Kullanıcı](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    a. Merhaba, **ad** metin kutusuna, türü hello Britta Simon adı.

    b. Merhaba, **Soyadı** metin kutusuna, tür hello son adını Britta Simon.

    c. Merhaba, **kullanıcı adı** metin kutusuna, Britta Simon türü hello kullanıcı adı.

    d. Merhaba, **e-posta** metin kutusuna, Britta Simon hesabının hello e-posta adresini yazın.

    e. Merhaba bilgi geri kalanı, gerekirse doldurabilir isteğe bağlıdır.
    
    f. **KAYDET**'e tıklayın.  

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, kendi erişim tooVelpic SAML vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Kullanıcı atama][200] 

**tooassign Britta Simon tooVelpic SAML, hello aşağıdaki adımları gerçekleştirin:**

1. Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Velpic SAML**.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Kullanıcı atama][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Kullanıcı atama][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

1. Velpic SAML döşeme hello erişim paneli hello tıkladığınızda, oturum açma sayfasına Velpic SAML uygulamasının almanız gerekir. Merhaba görmelisiniz **'Günlük oturum Azure AD'** hello oturum açma sayfası düğmesinde.

    ![Eklentisi](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. Tıklatın hello üzerinde **'Günlük oturum Azure AD'** düğmesini toolog Azure AD hesabınızı kullanarak tooVelpic içinde.


## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

