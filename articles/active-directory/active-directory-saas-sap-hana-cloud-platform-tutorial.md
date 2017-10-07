---
title: "Öğretici: SAP HANA bulut platformu Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Azure Active Directory tooenable ile toouse SAP HANA bulut platformu nasıl tek oturum açma, otomatik sağlama ve daha fazlasını öğrenin!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bd398225-8bd8-4697-9a44-af6e6679113a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: cc6610969b1c7b08f776e6969a5977fc75eb9ab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a>Öğretici: SAP HANA Cloud Platform ile Azure Active Directory tümleştirme
Merhaba amacı Bu öğretici, Azure ve SAP HANA bulut platformu tooshow hello tümleştirme ' dir.

Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

* Geçerli bir Azure aboneliği
* SAP HANA bulut platformu hesabı

Bu öğreticiyi tamamladıktan sonra Azure AD kullanıcılarının atamış HANA bulut platformu olacaktır tooSAP mümkün toosingle oturum hello kullanarak hello uygulamasına hello [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

>[!IMPORTANT]
>Hesap tootest tek oturum açma, SAP HANA bulut platformunda tooan uygulama abone veya toodeploy kendi uygulamanız gerekir. Bu öğreticide, bir uygulama hello hesabında dağıtılır.
> 
> 

Bu öğreticide gösterilen hello senaryo yapı taşları aşağıdaki Merhaba oluşur:

1. Merhaba uygulama tümleştirmesi SAP HANA bulut platformu için etkinleştirme
2. Çoklu oturum açma (SSO) yapılandırma
3. Bir rol tooa kullanıcı atama
4. Kullanıcılar atama

![Senaryo](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "senaryosu")

## <a name="enabling-hello-application-integration-for-sap-hana-cloud-platform"></a>Merhaba uygulama tümleştirmesi SAP HANA bulut platformu için etkinleştirme
Bu bölümde Hello amacı olan toooutline nasıl tooenable hello uygulama tümleştirmesi için SAP HANA bulut platformu.

**SAP HANA bulut platformu için tooenable hello uygulama tümleştirmesi hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba Sol Gezinti Bölmesi ' hello Azure Yönetim Portalı'ı tıklatın **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")
2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.
3. Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.
   
    ![Uygulamaları](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "uygulamalar")
4. Tıklatın **Ekle** hello sayfanın hello sonundaki.
   
    ![Uygulama ekleme](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "uygulama ekleme")
5. Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.
   
    ![Galeriden bir uygulama eklemek](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Galeriden bir uygulama ekleme")
6. Merhaba, **arama kutusu**, türü **SAP HANA bulut platformu**.
   
    ![Uygulama Galerisi](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "uygulama Galerisi")
7. Merhaba sonuçlar bölmesinde seçin **SAP HANA bulut platformu**ve ardından **tam** tooadd Merhaba uygulaması.
   
    ![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")
   
## <a name="configure-single-sign-on"></a>Çoklu oturum açmayı yapılandırın

Bu bölümde Hello amacı nasıl hello SAML protokolünü kullanarak Federasyon Azure AD'de hesabıyla tooenable kullanıcılar tooauthenticate tooSAP HANA bulut platformu temel toooutline ' dir.

Bu yordam bir parçası, gerekli tooupload base-64 kodlanmış sertifika tooyour SAP HANA bulut platformu Kiracı olur.  

Bu yordama bilmiyorsanız bkz [nasıl tooconvert bir ikili sertifika bir metin dosyasına](http://youtu.be/PlgrzUZ-Y1o)

**tooconfigure çoklu oturum açma, hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Klasik Azure Portalı'nda **SAP HANA bulut platformu** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **yapılandırma çoklu oturum açma**iletişim.
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "çoklu oturum açmayı yapılandırın")
2. Merhaba üzerinde **nasıl kullanıcılar toosign tooSAP HANA bulut platformu üzerinde gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "çoklu oturum açmayı yapılandırın")
3. Farklı web tarayıcısı penceresinde toohello SAP HANA bulut platformu Pilot https://account adresindeki oturum. \<yatay konak\>.ondemand.com/cockpit (örn: *https://account.hanatrial.ondemand.com/cockpit*).
4. Merhaba tıklatın **güven** sekmesi.
   
    ![Güven](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "güven")
5. Güven Yönetimi bölümünde hello aşağıdaki adımları gerçekleştirin:
   
    ![Meta veri alma](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "meta verileri alma")
   
   1. Merhaba tıklatın **yerel hizmet sağlayıcısı** sekmesi.
   2. toodownload hello SAP HANA bulut platformu meta veri dosyası, tıklatın **meta verileri alma**.
6. Merhaba üzerinde hello Azure Active Klasik Portalı'nda **uygulama URL'sini Yapılandır** sayfasında, aşağıdaki adımları hello gerçekleştirmek ve ardından **sonraki**.
   
    ![Uygulama URL'sini Yapılandır](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "uygulama URL'sini yapılandırın")
   
   1. Merhaba, **oturum üzerinde URL'si** metin kutusuna,, kullanıcıların toosign tarafından kullanılan türü hello URL, **SAP HANA bulut platformu** uygulama. SAP HANA bulut platformu uygulamanızda korumalı bir kaynağın hello hesaba özel URL budur. Merhaba URL deseni takip hello üzerinde dayanır: *https://\<applicationName\>\<accountName\>.\< Yatay konak\>.ondemand.com/\<yolu\_için\_korumalı\_kaynak\>*  (örn: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)
      
     >[!NOTE]
     >SAP HANA bulut platformu uygulamanızda hello kullanıcı tooauthenticate gerektirir hello URL budur.
     > 

   2. İndirilen hello SAP HANA bulut platformu meta veri dosyasını açın ve hello bulun **ns3:AssertionConsumerService** etiketi.
   3. Merhaba Hello değerini kopyalayın **konumu** özniteliği ve hello yapıştırma **SAP HANA bulut platformu yanıt URL'si** metin kutusu.

7. Merhaba üzerinde **çoklu oturum açma sırasında SAP HANA bulut platformu yapılandırmak** sayfası, toodownload meta verileriniz tıklatın **karşıdan meta veri**ve hello dosyayı bilgisayarınıza kaydedin.
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "çoklu oturum açmayı yapılandırın")
8. SAP HANA bulut platformu Pilot hello hello üzerinde **yerel hizmet sağlayıcısı** bölümünde, hello aşağıdaki adımları gerçekleştirin:
   
    ![Yönetim güven](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "güven Yönetimi")
   
  1. **Düzenle**’ye tıklayın.
  2. Olarak **yapılandırma türü**seçin **özel**.
  3. Olarak **yerel sağlayıcı adı**, hello varsayılan değeri bırakın.
  4. toogenerate bir **imzalama anahtarı** ve **imzalama sertifikası** anahtar çifti, tıklatın **anahtar çifti oluşturma**.
  5. Olarak **asıl yayma**seçin **devre dışı**.
  6. Olarak **zorla kimlik doğrulama**seçin **devre dışı**.
  7. **Kaydet** düğmesine tıklayın.

9. Merhaba tıklatın **güvenilen kimlik sağlayıcısı** sekmesini ve ardından **güvenilen kimlik sağlayıcısı ekleyin**.
   
    ![Yönetim güven](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "güven Yönetimi")
   
    >[!NOTE]
    >Güvenilen kimlik sağlayıcıları toomanage hello listesi, hello yerel hizmet sağlayıcısı bölüm hello özel yapılandırma türü seçilen toohave gerekir. Varsayılan yapılandırma türü için düzenlenemeyen ve örtük güven toohello SAP ID hizmeti sahip. Hiçbiri için herhangi bir güven ayarı yok.
    > 
    > 

10. Hello tıklatın **genel** sekmesini ve ardından **Gözat** tooupload hello meta veri dosyası indirilir.
    
    ![Yönetim güven](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "güven Yönetimi")
    
    >[!NOTE]
    >Merhaba değerleri Hello meta veri dosyası karşıya yüklemeden sonra **çoklu oturum açma URL'si**, **çoklu oturum kapatma URL'si** ve **imzalama sertifikası** otomatik olarak doldurulur.
    > 
    > 

11. Merhaba tıklatın **öznitelikleri** sekmesi.
12. Merhaba üzerinde **öznitelikleri** sekmesinde, adım aşağıdaki hello gerçekleştirin:
    
    ![Öznitelikleri](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "öznitelikleri") 
  * Tıklatın **Add Assertion-Based özniteliği**ve ardından onaylama tabanlı öznitelikler aşağıdaki hello ekleyin:
       
    | Onaylama işlemi özniteliği | Asıl özniteliği |
    | --- | --- |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/givenName |FirstName |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/surname |Soyadı |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/emailaddress |E-posta 
   
     >[!NOTE]
     >Merhaba öznitelikleri Hello yapılandırmasını nasıl hello uygulamaları HCP üzerinde geliştirilmiş, yani hangi öznitelikleri hello SAML yanıtını bekledikleri ve bu öznitelik hello kodda eriştiklerinde hangi adla (asıl özniteliği) bağlıdır.
     > 
     >  

    1.  Merhaba **varsayılan özniteliği** hello ekran yalnızca gösterim amacıyla kullanılır. Bu gerekli toomake hello senaryosu iş.   
    2.  Merhaba adlarını ve değerlerini **asıl özniteliği** hello gösterildiği ekran bağımlı nasıl Merhaba uygulaması geliştirmiştir. Uygulamanızın farklı eşlemeleri gerektirdiği mümkündür.
     
13. Merhaba hello üzerinde Klasik Azure portalı içinde **çoklu oturum açma sırasında SAP HANA bulut platformu yapılandırma** iletişim kutusunda sayfa, hello tek oturum açma yapılandırması onay seçin ve ardından **tam**.
    
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "çoklu oturum açmayı yapılandırın")

###<a name="assertion-based-groups"></a>Onaylama işlemi tabanlı grupları
İsteğe bağlı bir adım, Azure Active Directory kimlik sağlayıcısı için onaylama tabanlı grupları yapılandırabilirsiniz.

SAP HANA bulut platformunda gruplarını kullanarak toodynamically Ata bir sağlar veya daha fazla kullanıcı tooone ya da daha fazla roller, SAP HANA bulut platformu uygulamalarınızda belirlediği hello SAML özniteliklerinin değerlerini 2.0 onaylama. 

Örneğin, hello onaylama hello özniteliği varsa, "*sözleşme geçici =*", tüm etkilenen kullanıcılar toobe eklenen toohello grubu isteyebilirsiniz"*geçici*". Merhaba grup "*geçici*" SAP HANA bulut platformu hesabınızda dağıtılan bir veya daha fazla uygulamalardan bir veya daha fazla rol içerebilir.
 
Toosimultaneously istediğinizde onaylama tabanlı gruplar kullanılması birçok kullanıcılar tooone veya SAP HANA bulut platformu hesabınızı uygulamaların daha fazla rolü atayın. Tooassign kullanıcılar toospecific rolleri, yalnızca tek veya küçük sayıda istiyorsanız, bunları doğrudan hello atama öneririz "**yetkilerini**" Merhaba SAP HANA bulut platformu Pilot sekmesinde.

## <a name="assign-a-role-tooa-user"></a>Rol tooa kullanıcı atama
SAP HANA bulut platformu içine sipariş tooenable Azure AD kullanıcıların toolog içinde hello SAP HANA bulut platformu toothem rollerinde atamanız gerekir.

**bir rol tooa kullanıcı tooassign hello aşağıdaki adımları gerçekleştirin:**

1. İçinde tooyour oturum **SAP HANA bulut platformu** Pilot.
2. Merhaba aşağıdakileri gerçekleştirin:
   
   ![Yetkilerini](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "yetkileri değiştirme")
   
  1. Tıklatın **yetkilendirme**.
  2. Merhaba tıklatın **kullanıcılar** sekmesi.
  3. Merhaba, **kullanıcı** metin kutusuna, türü hello kullanıcının e-posta adresi.
  4. Tıklatın **atamak** tooassign hello kullanıcı tooa rolü.
  5. **Kaydet** düğmesine tıklayın.

## <a name="assign-users"></a>Kullanıcılar atama
tootest yapılandırmanıza, uygulama erişim tooit atayarak kullanarak tooallow istediğiniz toogrant hello Azure AD kullanıcıları gerekir.

**tooassign kullanıcılar tooSAP HANA bulut platformu hello aşağıdaki adımları gerçekleştirin:**

1. Hello Klasik Azure portalı, bir test hesabı oluşturun.
2. Hello üzerinde **SAP HANA bulut platformu** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.
   
   ![Kullanıcılar atama](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "kullanıcı atama")
3. Test kullanıcınız seçin, **atamak**ve ardından **Evet** tooconfirm, atama.
   
   ![Evet](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Evet")

SSO ayarlarınızı tootest istiyorsanız hello erişim paneli açın. Merhaba erişim paneli hakkında daha fazla ayrıntı için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

