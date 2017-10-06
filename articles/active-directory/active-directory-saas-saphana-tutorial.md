---
title: "Öğretici: SAP HANA Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve SAP HANA arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 5ff6bfde0b1d7ab14025a4bc45199f9f826affd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a>Öğretici: SAP HANA Azure Active Directory Tümleştirme

Bu öğreticide, nasıl toointegrate SAP öğrenin HANA Azure Active Directory'ye (Azure AD).

SAP HANA Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooSAP HANA sahip Azure AD'de kontrol edebilirsiniz
- Kullanıcıların tooautomatically get açan tooSAP HANA (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

SAP HANA ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir SAP HANA çoklu oturum açma abonelik etkin
- Çalışan HANA örneği üzerinde herhangi bir ortak Iaas, şirket içi ya da Azure VM'ler veya Azure SAP büyük örnekleri
- Merhaba XSA Yönetim Web arabirimi yanı sıra HANA Studio hello HANA örnek üzerinde yüklü.

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamında, SAP HANA kullanarak önermiyoruz. Merhaba tümleştirme ilk geliştirme veya hazırlama ortamı hello uygulamasının ve kullanım hello üretim ortamında test edin.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. SAP HANA hello Galerisi'nden ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-sap-hana-from-hello-gallery"></a>SAP HANA hello Galerisi'nden ekleme
Azure AD'ye tooconfigure hello tümleştirme, SAP HANA tooadd SAP HANA hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**SAP HANA hello galerisinden tooadd hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Merhaba arama kutusuna yazın **SAP HANA**seçin **SAP HANA** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması. 

    ![Merhaba yeni uygulama](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Çoklu oturum açmayı yapılandırma ve Azure AD sınama
Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı SAP HANA ile test etme

Tek toowork'ın oturum açma hangi hello karşılık gelen SAP HANA içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve SAP HANA hello ilgili kullanıcı arasındaki bağlantıyı ilişki kurulan toobe gerekir.

SAP HANA içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve SAP HANA ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[SAP HANA test kullanıcısı oluşturma](#creating-a-sap-hana-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir SAP HANA içinde karşılık gelen.
4. **[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırma

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma, SAP HANA uygulamanızda yapılandırın.

**tooconfigure Azure AD çoklu oturum açma SAP HANA ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Hello hello üzerinde Azure portal'ın **SAP HANA** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açmayı yapılandırın][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. Merhaba üzerinde **SAP HANA etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    a. Merhaba, **tanımlayıcısı** metin kutusuna, türü olarak:`HA100` 

    b. Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin. Kişi [SAP HANA istemci destek ekibi](https://cloudplatform.sap.com/contact.html) tooget bu değerleri. 

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    >Sertifika etkin değilse, ardından active hello tıklayarak "Yapma yeni sertifika etkin" onay kutusunu hello Azure AD kolaylaştırır. 

5. SAP HANA uygulama hello SAML onaylar belirli bir biçimde bekler. Ekran aşağıdaki hello bunun bir örneği gösterir. Burada size hello eşledikten **kullanıcı tanımlayıcısı** ile **ExtractMailPrefix()** işlevinin **user.mail**. Bu e-posta benzersiz kullanıcı kimliği hello hello kullanıcının hello önek değeri verir Bu toohello SAP HANA uygulama her başarılı yanıt olarak gönderilir.

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim:

    a. Merhaba, **kullanıcı tanımlayıcısı** açılır listesinden, **ExtractMailPrefix**.
    
    b. Merhaba, **posta** açılır listesinden, **user.mail**.

7. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. tooconfigure çoklu oturum açma üzerinde **SAP HANA** tarafı, oturum açma tooyour **HANA XSA Web Konsolu** toohello giderek ilgili HTTPS uç noktası.

    > [!Note]
    > Merhaba varsayılan yapılandırmasında bir kimliği doğrulanmış SAP HANA veritabanına kullanıcı toocomplete hello oturum açma işleminin hello kimlik bilgileri gerektiren hello isteği tooa oturum açma ekranı hello URL yönlendirir. oturum açan hello kullanıcı hello ayrıcalıkları gerekli tooperform SAML yönetim görevlerini olması gerekir.

9. Hello XSA Web arabirimi, çok gidin**SAML kimlik sağlayıcısı** tıklatıp buradan hello **"+"** -düğmesini hello bölmesinin Merhaba ekranında toodisplay hello kimlik sağlayıcısı bilgisi Ekle üzerinde ve gerçekleştirin Aşağıdaki adımları hello:

    ![Kimlik sağlayıcısı ekleyin](./media/active-directory-saas-saphana-tutorial/sap1.png)

    a. Merhaba, **kimlik sağlayıcısı bilgisi Ekle** bölmesinde, Yapıştır hello hello hello Azure Portalı'ndan indirilen meta veri XML içeriğini **meta veri** metin kutusu.

    ![Kimlik sağlayıcı ayarları ekleme](./media/active-directory-saas-saphana-tutorial/sap2.png)

    b. Merhaba hello XML belgesinin içeriğini geçerliyse, işlem ayrıştırma hello hello gerekli bilgileri tooinsert hello ayıklar. **konu, varlık kimliği ve sertifikayı veren** hello genel veri alanlarında ekran alanı ve hello URL alanlarında hello Hedef ekran alanı, örneğin,  **taban URL ve SingleSignOn URL (*)**.

    ![Kimlik sağlayıcı ayarları ekleme](./media/active-directory-saas-saphana-tutorial/sap3.png)

    c. Merhaba adı kutusuna hello genel veri alanı ekranında, hello yeni SAML SSO kimlik sağlayıcısı için bir ad girin.

    > [!Note]
    > Merhaba SAML IDP Hello adı zorunludur ve benzersiz olmalıdır; SAML SAP HANA XS uygulamaları toouse hello kimlik doğrulama yöntemi olarak Örneğin, Itanium tabanlı sistemler için hello kimlik doğrulaması ekran alanı hello XS yapı Yönetim Aracı'nda seçerseniz hello görüntülenir, kullanılabilir SAML IDPs listesinde görüntülenir.

10. Merhaba yeni SAML kimlik sağlayıcısı Hello ayrıntılarını kaydedin. Seçin **kaydetmek** toosave hello hello SAML kimlik sağlayıcısı ayrıntılarını ve hello yeni SAML IDP toohello listesi bilinen SAML IDPs ekleyin.

    ![Kaydet düğmesi](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. Merhaba hello sistem özelliklerini içinde HANA Studio'da **yapılandırma** sekmesinde, yalnızca ayarlarına göre filtre **saml** ve hello ayarlamak **assertion_timeout** gelen**10 sn** çok**120 saniye**.

    ![assertion_timeout ayarı](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Azure AD Kullanıcı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.
    
    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.
 
    ![Merhaba Ekle düğmesi](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:
 
    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    a. Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.

    b. Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.

    c. Seçin **Göster parola** ve hello hello değerini yazma **parola**.

    d. **Oluştur**'a tıklayın.
 
### <a name="creating-a-sap-hana-test-user"></a>SAP HANA test kullanıcısı oluşturma

tooenable Azure AD kullanıcıların toolog tooSAP HANA'da, bunlar SAP HANA sağlanması gerekir.
SAP HANA tam zamanı sağlama, varsayılan olarak etkin olduğu destekler.

Bir kullanıcı toocreate el ile gerekiyorsa, hello aşağıdaki adımları gerçekleştirin:

>[!Note]
>Merhaba kullanıcı tarafından kullanılan hello Dış kimlik doğrulama değiştirebilirsiniz.
Dış kullanıcılar, örneğin Kerberos sistem bir dış sistem kullanılarak doğrulanır. Dış kimlikler hakkında ayrıntılı bilgi için kişi, [etki alanı yöneticisi](https://cloudplatform.sap.com/contact.html).

1. Açık hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) bir Yöneticiyseniz ve etkinleştir DB kullanıcı SAML SSO için hello gibi.

    ![Kullanıcı oluştur](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. Değer çizgilerinin hello görünmez onay kutusunu toohello sol üst **SAML** ve hello Yapılandır bağlantısını izleyin.

3. Tıklatın **Ekle** tooadd SAML IDP hello ve tıklayın **Tamam** hello uygun SAML IDP seçme.

4. Merhaba eklemek **Dış kimlik** (örneğin. Burada BrittaSimon) veya seçin **"Tüm"** tıklatıp **Tamam**.

    >[!Note]
    >"Tüm" onay kutusu işaretli sonra HANA hello kullanıcı adı gerekiyor tooexactly eşleşme hello hello UPN hello etki alanı soneki önce hello kullanıcı adını (yani BrittaSimon@contoso.com HANA BrittaSimon olur).

5. Test amacıyla, tüm Ata **"XS"** rolleri toohello kullanıcı.

    ![rol atama](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > Bu, kullanım örnekleri için yalnızca uygun izinleri vermeniz gerekir.

6. Merhaba kullanıcı kaydedin.

### <a name="assigning-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atama

Bu bölümde, erişim tooSAP HANA vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200] 

**tooassign Britta Simon tooSAP HANA, hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **SAP HANA**.

    ![Kullanıcı atama](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202] 

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="testing-single-sign-on"></a>Çoklu oturum açmayı test etme

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba SAP HANA hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour SAP HANA uygulama almanız gerekir.
Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png

