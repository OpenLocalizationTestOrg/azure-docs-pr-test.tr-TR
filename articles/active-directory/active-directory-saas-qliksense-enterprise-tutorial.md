---
title: "Öğretici: Azure Active Directory Tümleştirme Qlik algılama kuruluş ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Qlik algılama kuruluş arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 153edb3f8cd41790d4e9a74f15cfb806e5e9e3b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a>Öğretici: Azure Active Directory Tümleştirme Qlik algılama kuruluş ile

Bu öğreticide, bilgi nasıl toointegrate Qlik algılama kuruluş Azure Active Directory'ye (Azure AD).

Qlik algılama kuruluş Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:

- Erişim tooQlik algılama Kurumsal sahip Azure AD'de kontrol edebilirsiniz.
- Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooQlik algılama Enterprise (çoklu oturum açma) etkinleştirebilirsiniz.
- Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.

Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Ön koşullar

tooconfigure Qlik algılama Kurumsal ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:

- Bir Azure AD aboneliği
- Bir Qlik algılama Kurumsal çoklu oturum açma abonelik etkin

> [!NOTE]
> tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.

Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:

- Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.
- Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Senaryo açıklaması
Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin. Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:

1. Merhaba Galerisi'nden Qlik algılama Kurumsal ekleme
2. Çoklu oturum açmayı yapılandırma ve Azure AD sınama

## <a name="adding-qlik-sense-enterprise-from-hello-gallery"></a>Merhaba Galerisi'nden Qlik algılama Kurumsal ekleme
Azure AD'ye tooconfigure hello tümleştirme Qlik algılama Enterprise tooadd Qlik algılama Kurumsal hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.

**tooadd Qlik algılama Kurumsal hello galerisinden hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi. 

    ![Hello Azure Active Directory düğmesi][1]

2. Çok gidin**kurumsal uygulamalar**. Çok Git**tüm uygulamaları**.

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.

    ![Merhaba yeni uygulama düğmesi][3]

4. Hello arama kutusuna yazın **Qlik algılama Kurumsal**seçin **Qlik algılama Kurumsal** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.

    ![Merhaba sonuçları listesinde Qlik algılama Enterprise](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Yapılandırma ve Azure AD çoklu oturum açmayı test etme

Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Qlik algılama "Britta Simon" adlı bir test kullanıcı tabanlı kuruluş ile test etme.

Tek toowork'ın oturum açma hangi hello karşılık gelen Qlik algılama kuruluştaki tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir. Diğer bir deyişle, bir Azure AD kullanıcısının ve Qlik algılama kuruluştaki hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.

Merhaba hello değeri Qlik algılama kuruluşta atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.

tooconfigure ve Qlik algılama kuruluş ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:

1. **[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.
2. **[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.
3. **[Qlik algılama Kurumsal test kullanıcısı oluşturma](#create-a-qlik-sense-enterprise-test-user)**  -toohave karşılık gelen, Britta Simon Qlik algılama kuruluşta, kullanıcı bağlantılı toohello Azure AD gösterimidir.
4. **[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.
5. **[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD çoklu oturum açmayı yapılandırın

Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Qlik algılama Kurumsal uygulamanızda yapılandırın.

**Azure AD çoklu oturum açma tooconfigure Qlik algılama kuruluş ile Merhaba aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Azure portal'ın **Qlik algılama Kurumsal** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. Merhaba üzerinde **Qlik algılama kuruluş etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:

    ![Qlik algılama kuruluş etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    a. Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`
    
    > [!NOTE]
    > Sondaki eğik çizgi bu URI hello sonunda hello unutmayın. Gerekli değildir.
    
    b. Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > Bu değerler gerçek değildir. Bu değerleri ile Merhaba gerçek oturum açma URL'si ve tanımlayıcı, daha sonra Bu öğreticide veya kişi açıklanacak güncelleştirme [Qlik algılama Kurumsal İstemci destek ekibi](https://www.qlik.com/us/services/support) tooget bu değerleri. 

4. Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. Tıklatın **kaydetmek** düğmesi.

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. Böylece bu tooQlik algılama sunucu yükleyebilirsiniz hello Federasyon meta veri XML dosyasını hazırlayın.
   
    > [!NOTE]
    > Merhaba IDP meta veri toohello Qlik algılama sunucu karşıya yüklemeden önce hello dosyasının düzenlenen toobe tooremove bilgi tooensure düzgün çalışmasını Azure AD arasında gerekir ve Qlik algılama sunucu.
    
    ![QlikSense][qs24]
   
    a. Bir metin düzenleyicisinde Azure portalından indirmiş hello FederationMetaData.xml dosyasını açın.
   
    b. Merhaba değeri için arama **RoleDescriptor**.  Dört girdi (açma ve kapatma öğesi etiketleri iki çiftleri) vardır.
   
    c. Merhaba RoleDescriptor etiketleri ve tüm bilgileri arasında hello dosyadan silin.
   
    d. Merhaba dosyasını kaydedin ve yakındaki bu belgenin sonraki bölümlerinde kullanmak için saklayın.

7. Sanal proxy yapılandırmaları oluşturabilirsiniz bir kullanıcı olarak toohello Qlik algılama Qlik Yönetim Konsolu (QMC) gidin.

8. Hello QMC, üzerinde hello tıklatın **sanal proxy'leri** menü öğesi.
   
    ![QlikSense][qs6] 

9. Merhaba ekranında Hello altındaki hello tıklatın **Yeni Oluştur** düğmesi.
   
    ![QlikSense][qs7]

10. Merhaba sanal proxy düzenleme ekranı görüntülenir.  Merhaba üzerinde Merhaba ekranında sağ tarafında yapılandırma seçenekleri görünür yapmak için bir menü ' dir.
   
    ![QlikSense][qs9]

11. Kimlik menü seçeneğini işaretli hello ile Merhaba hello Azure sanal proxy yapılandırması için tanımlayıcı bilgileri girin.
    
    ![QlikSense][qs8]  
    
    a. Merhaba **açıklama** hello sanal proxy yapılandırması için bir kolay ad alanıdır.  Bir değer için bir açıklama girin.
    
    b. Merhaba **önek** alan Azure AD çoklu oturum açma ile tooQlik algılama bağlamak için hello sanal proxy uç nokta tanımlar.  Bu sanal proxy için bir benzersiz önek adı girin.
    
    c. **Oturum etkin olmama zaman aşımı (dakika)** hello zaman aşımı değeri bu sanal proxy üzerinden bağlantıları için.
    
    d. Merhaba **oturum tanımlama bilgisi üstbilgisi adı** olan kullanıcı Qlik algılama oturumu alır başarılı kimlik doğrulamasından sonra hello için oturum tanımlayıcısı hello hello tanımlama bilgisi adı depolama.  Bu ad benzersiz olmalıdır.

12. Merhaba kimlik doğrulaması menü seçeneği toomake üzerinde görünür tıklatın.  Merhaba kimlik doğrulama ekranı görüntülenir.
    
    ![QlikSense][qs10]
    
    a. Merhaba **anonim erişim modu** açılan belirler anonim kullanıcılar hello sanal proxy üzerinden Qlik algılama erişimi.  Anonim kullanıcı Hello varsayılan seçenektir.
    
    b. Merhaba **kimlik doğrulama yöntemini** açılan belirler hello kimlik doğrulama düzeni hello sanal proxy kullanır.  SAML hello aşağı açılan listeden seçin.  Daha fazla seçenek sonuç olarak görünür.
    
    c. Merhaba, **SAML konak URI alan**, giriş hello hostname kullanıcılar bu SAML sanal proxy üzerinden tooaccess Qlik algılama girin.  Merhaba ana hello Qlik algılama sunucu hello URI'sini adıdır.
    
    d. Merhaba, **SAML varlık kimliği**, hello girilen hello SAML konak URI alanı için aynı değeri girin.
    
    e. Merhaba **SAML IDP meta veri** önceki hello düzenlenebilir hello dosyası **Düzenle Federasyon meta verilerini Azure AD yapılandırma** bölümü.  **Merhaba IDP meta veriler karşıya yüklemeden önce hello dosyasının düzenlenen toobe gerekir** tooremove bilgi tooensure düzgün çalışmasını Azure AD arasında ve Qlik algılama sunucu.  **Lütfen yukarıdaki toohello yönergeleri hello dosyanın henüz toobe düzenlenebilir bakın.**  Merhaba dosyayı düzenlerseniz hello Gözat düğmesi ve select hello düzenlenen meta veri dosyası tooupload toohello sanal proxy yapılandırması tıklatın.
    
    f. Merhaba temsil eden hello SAML öznitelik için Hello öznitelik adı veya şema başvurusu girin **UserID** Azure AD toohello Qlik algılama sunucusuna gönderir.  Şema başvurusu bilgileri hello Azure uygulaması ekranlar post yapılandırmada kullanılabilir.  toouse hello name özniteliği girin `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
    
    g. Merhaba Hello değeri girin **kullanıcı dizini** , olacaktır ekli toousers tooQlik algılama sunucusu aracılığıyla Azure AD kimlik doğrulaması sırasında.  Sabit kodlanmış değerler arasına, tarafından **köşeli ayraçlar []**.  Bu metin kutusunda toouse hello Azure AD SAML onayı gönderilen bir öznitelik girin hello hello özniteliğin adını **olmadan** köşeli ayraç.
    
    h. Merhaba **SAML imzalama algoritmasını** kümeleri hello hello sanal proxy yapılandırması için imzalama hizmet sağlayıcısı (Server'daki bu servis talebi Qlik algılama) sertifikası.  Qlik algılama sunucusu Microsoft Gelişmiş RSA ve AES şifreleme sağlayıcısı kullanılarak oluşturulan güvenilen bir sertifika kullanıyorsa, hello SAML imzalama algoritmasını çok değiştirmek**SHA-256**.
    
    ı. Merhaba SAML özniteliği eşleme bölümüne güvenlik kuralları kullanmak için grupları gönderilen toobe tooQlik algılama gibi ek özellikleri sağlar.

13. Tıklatın hello üzerinde **yük DENGELEME** menü seçeneği toomake onu görünür.  Merhaba Yük Dengeleme ekranı görüntülenir.
    
    ![QlikSense][qs11]

14. Merhaba üzerinde tıklatın **Ekle yeni sunucu düğümü** düğmesini tıklatın, select altyapısı düğüm veya düğümler Qlik algılama amacıyla oturumları toofor dengelemesini gönderir ve Başlangıç'ı tıklatın **Ekle** düğmesi.
    
    ![QlikSense][qs12]

15. Merhaba Gelişmiş menü seçeneği toomake üzerinde görünür tıklatın. Merhaba Gelişmiş ekranı görüntülenir.
    
    ![QlikSense][qs13]
    
    Merhaba konak beyaz liste toohello Qlik algılama sunucusuna bağlanırken kabul ana bilgisayar adlarını tanımlar.  **Kullanıcıların tooQlik algılama sunucusu bağlanırken belirteceği hello ana bilgisayar adı girin.** Merhaba ana bilgisayar adı olan hello SAML konak URI hello https:// olmadan hello gibi aynı değeri.

16. Merhaba tıklatın **Uygula** düğmesi.
    
    ![QlikSense][qs14]

17. Bağlantılı toohello sanal proxy başlatılacak proxy'leri bildiren Tamam tooaccept hello uyarı iletisi tıklayın.
    
    ![QlikSense][qs15]

18. Merhaba sağ tarafında Merhaba ekranında, hello ilişkili öğeler menüsü görüntülenir.  Tıklatın hello üzerinde **proxy'leri** menü seçeneği.
    
    ![QlikSense][qs16]

19. Merhaba proxy ekranı görüntülenir.  Merhaba tıklatın **bağlantı** hello alt toolink sırasında bir proxy toohello sanal proxy düğmesi.
    
    ![QlikSense][qs17]

20. Bu sanal proxy bağlantı desteklemek ve hello tıklatın select hello proxy düğümü **bağlantı** düğmesi.  Bağladıktan sonra hello proxy ilişkili proxy'leri altında listelenir.
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. Sonra yaklaşık beş tooten saniye, hello yenileme QMC iletisi görünür.  Merhaba tıklatın **yenileme QMC** düğmesi.
    
    ![QlikSense][qs20]

22. Merhaba QMC yenilendiğinde hello üzerinde tıklatın **sanal proxy'leri** menü öğesi. Merhaba yeni SAML sanal proxy giriş Merhaba ekranında hello tablosundaki listelenir.  Merhaba sanal proxy girişini tek tıklatın.
    
    ![QlikSense][qs51]

23. Merhaba ekranında Hello altındaki hello karşıdan SP meta verileri düğmesi etkinleşir.  Merhaba tıklatın **karşıdan SP meta veri** düğmesini toosave hello meta veri tooa dosyası.
    
    ![QlikSense][qs52]

24. Açık hello sp meta veri dosyası.  Merhaba gözlemlemek **Entityıd** girişi ve hello **AssertionConsumerService** girişi.  Bu değerler eşdeğer toohello **tanımlayıcısı** ve hello **URL üzerinde oturum** hello Azure AD uygulama yapılandırmasında. Bu değerleri hello yapıştırmak **Qlik algılama kuruluş etki alanı ve URL'leri** hello Azure AD uygulaması Yapılandırma Sihirbazı'nda değiştirmelisiniz sonra bunlar, eşleşen değil, hello Azure AD uygulama yapılandırma bölümünde.
    
    ![QlikSense][qs53]

> [!TIP]
> Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!  Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına. Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Bir Azure AD test kullanıcısı oluşturma
Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.

![Bir Azure AD test kullanıcısı oluşturma][100]

**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.

   ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.

   !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.

   ![Merhaba Ekle düğmesi](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:

   ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   a. Merhaba, **adı** kutusuna **BrittaSimon**.

   b. Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.

   c. Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.

   d. **Oluştur**'a tıklayın.
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a>Qlik algılama Kurumsal test kullanıcısı oluşturma

Bu bölümde, Britta Simon Qlik algılama kuruluşta adlı bir kullanıcı oluşturun. Çalışmak [Qlik algılama Kurumsal İstemci destek ekibi](https://www.qlik.com/us/services/support) hello Qlik algılama Kurumsal platformunda hello kullanıcıları eklemek için. Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir. 

### <a name="assign-hello-azure-ad-test-user"></a>Hello Azure AD test kullanıcısı atayın

Bu bölümde, erişim tooQlik algılama Kurumsal vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.

![Merhaba kullanıcı rolü atayın][200] 

**tooassign Britta Simon tooQlik algılama Kurumsal hello aşağıdaki adımları gerçekleştirin:**

1. Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.

    ![Kullanıcı atama][201] 

2. Merhaba uygulamalar listesinde **Qlik algılama Kurumsal**.

    ![Merhaba Qlik algılama Kurumsal bağlantı hello uygulamalar listesinde](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. Tıklatın **Ekle** düğmesi. Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.

    ![Merhaba eklemek atama bölmesi][203]

5. Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.

6. Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.

7. Tıklatın **atamak** düğmesini **eklemek atama** iletişim.
    
### <a name="test-single-sign-on"></a>Çoklu oturum açmayı test edin

Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.

Merhaba Qlik algılama Kurumsal hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Qlik algılama Kurumsal uygulama almanız gerekir. 

## <a name="additional-resources"></a>Ek kaynaklar

* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

