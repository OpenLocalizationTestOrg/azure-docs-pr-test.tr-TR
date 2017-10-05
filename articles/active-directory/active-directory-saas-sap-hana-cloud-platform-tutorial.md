---
title: "Öğretici: SAP HANA bulut platformu Azure Active Directory Tümleştirme | Microsoft Docs"
description: "SAP HANA bulut platformu Azure Active Directory ile çoklu oturum açma, otomatik sağlama ve daha fazlasını sağlamak için nasıl kullanılacağını öğrenin!"
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
ms.openlocfilehash: e03bc2410a8d57363c558f723b3bfd0e69b3f4c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a>Öğretici: SAP HANA Cloud Platform ile Azure Active Directory tümleştirme
Bu öğreticinin amacı, Azure ve SAP HANA bulut platformu tümleştirmesini göstermektir.

Bu öğreticide gösterilen senaryo, aşağıdaki öğeleri zaten sahip olduğunuzu varsayar:

* Geçerli bir Azure aboneliği
* SAP HANA bulut platformu hesabı

Bu öğreticiyi tamamladıktan sonra SAP HANA bulut platformu için atanmış Azure AD kullanıcılarının uygulama kullanarak çoklu oturum açabilirsiniz [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).

>[!IMPORTANT]
>Kendi uygulamanızı dağıtmak veya çoklu oturum açma üzerinde test etmek için bir uygulama SAP HANA bulut platformu hesabınızda abone olmak gerekir. Bu öğreticide, bir uygulama hesabında dağıtılır.
> 
> 

Bu öğreticide gösterilen senaryo, aşağıdaki yapı taşlarını oluşur:

1. SAP HANA bulut platformu için uygulama tümleştirmesini etkinleştirme
2. Çoklu oturum açma (SSO) yapılandırma
3. Bir kullanıcıya rol atama
4. Kullanıcılar atama

![Senaryo](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "senaryosu")

## <a name="enabling-the-application-integration-for-sap-hana-cloud-platform"></a>SAP HANA bulut platformu için uygulama tümleştirmesini etkinleştirme
Bu bölümün amacı, SAP HANA bulut platformu için uygulama tümleştirme sağlamak üzere nasıl anahat sağlamaktır.

**SAP HANA bulut platformu için uygulama tümleştirmesini etkinleştirmek için aşağıdaki adımları gerçekleştirin:**

1. Azure yönetim portalında sol gezinti bölmesinde, tıklatın **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")
2. Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.
3. Dizin görünümünde uygulamaları görünümü açmak için **uygulamaları** üst menüde.
   
    ![Uygulamaları](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "uygulamalar")
4. Tıklatın **Ekle** sayfanın sonundaki.
   
    ![Uygulama ekleme](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "uygulama ekleme")
5. Üzerinde **ne yapmak istiyorsunuz** iletişim kutusunda, tıklatın **Galeriden bir uygulama eklemek**.
   
    ![Galeriden bir uygulama eklemek](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Galeriden bir uygulama ekleme")
6. İçinde **arama kutusu**, türü **SAP HANA bulut platformu**.
   
    ![Uygulama Galerisi](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "uygulama Galerisi")
7. Sonuçlar bölmesinde seçin **SAP HANA bulut platformu**ve ardından **tam** uygulama eklemek için.
   
    ![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")
   
## <a name="configure-single-sign-on"></a>Çoklu oturum açmayı yapılandırın

Bu bölümün amacı kullanıcıların SAP HANA bulut platformu için kendi hesabıyla SAML protokolünü temel Federasyon kullanarak Azure AD kimlik doğrulaması sağlamak nasıl anahat sağlamaktır.

Bu yordam bir parçası olarak, SAP HANA bulut platformu kiracınız base-64 kodlanmış sertifika yüklemek için gerekli değildir.  

Bu yordama bilmiyorsanız bkz [ikili bir sertifika bir metin dosyasına dönüştürme](http://youtu.be/PlgrzUZ-Y1o)

**Çoklu oturum açma yapılandırmak için aşağıdaki adımları gerçekleştirin:**

1. Azure Klasik portalında üzerinde **SAP HANA bulut platformu** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma özelliğini yapılandırın** açmak için **tek oturum yapılandırma üzerinde aktar** iletişim kutusu.
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "çoklu oturum açmayı yapılandırın")
2. Üzerinde **SAP HANA bulut platformu için oturum açmasını nasıl istiyorsunuz** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "çoklu oturum açmayı yapılandırın")
3. Farklı web tarayıcısı penceresinde https://account SAP HANA bulut platformu Pilot için oturum açma. \<yatay konak\>.ondemand.com/cockpit (örn: *https://account.hanatrial.ondemand.com/cockpit*).
4. Tıklatın **güven** sekmesi.
   
    ![Güven](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "güven")
5. Güven Yönetimi bölümünde, aşağıdaki adımları gerçekleştirin:
   
    ![Meta veri alma](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "meta verileri alma")
   
   1. Tıklatın **yerel hizmet sağlayıcısı** sekmesi.
   2. SAP HANA bulut platformu meta veri dosyası indirmek için tıklayın **meta verileri alma**.
6. Azure Active Klasik Portalı'nda üzerinde **uygulama URL'sini Yapılandır** sayfasında, aşağıdaki adımları uygulayın ve ardından **sonraki**.
   
    ![Uygulama URL'sini Yapılandır](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "uygulama URL'sini yapılandırın")
   
   1. İçinde **oturum üzerinde URL'si** metin kutusuna, türü URL kullanılan kullanıcılarınız tarafından oturumu açmak için **SAP HANA bulut platformu** uygulama. SAP HANA bulut platformu uygulamanızda korumalı bir kaynağın hesap özgü URL'sidir. URL aşağıdaki desenine dayanır: *https://\<applicationName\>\<accountName\>.\< Yatay konak\>.ondemand.com/\<yolu\_için\_korumalı\_kaynak\>*  (örn: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)
      
     >[!NOTE]
     >Bu kullanıcının kimlik doğrulamasını gerektirir, SAP HANA bulut platformu uygulamanızda URL'dir.
     > 

   2. İndirilen SAP HANA bulut platformu meta veri dosyasını açın ve ardından bulun **ns3:AssertionConsumerService** etiketi.
   3. Değerini kopyalayın **konumu** özniteliği ve ardından yapıştırın **SAP HANA bulut platformu yanıt URL'si** metin kutusu.

7. Üzerinde **çoklu oturum açma sırasında SAP HANA bulut platformu yapılandırmak** meta verileriniz, indirme sayfasında, tıklatın **karşıdan meta veri**ve ardından dosyayı bilgisayarınıza kaydedin.
   
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "çoklu oturum açmayı yapılandırın")
8. SAP HANA bulut platformu Pilot üzerinde içinde **yerel hizmet sağlayıcısı** bölümünde, aşağıdaki adımları gerçekleştirin:
   
    ![Yönetim güven](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "güven Yönetimi")
   
  1. **Düzenle**’ye tıklayın.
  2. Olarak **yapılandırma türü**seçin **özel**.
  3. Olarak **yerel sağlayıcı adı**, varsayılan değeri bırakın.
  4. Oluşturmak için bir **imzalama anahtarı** ve **imzalama sertifikası** anahtar çifti, tıklatın **anahtar çifti oluşturma**.
  5. Olarak **asıl yayma**seçin **devre dışı**.
  6. Olarak **zorla kimlik doğrulama**seçin **devre dışı**.
  7. **Kaydet** düğmesine tıklayın.

9. Tıklatın **güvenilen kimlik sağlayıcısı** sekmesini ve ardından **güvenilen kimlik sağlayıcısı ekleyin**.
   
    ![Yönetim güven](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "güven Yönetimi")
   
    >[!NOTE]
    >Güvenilen kimlik sağlayıcıları listesini yönetmek için özel yapılandırma türü yerel hizmet sağlayıcısı bölümünde seçmiş olmanız gerekir. Varsayılan yapılandırma türü için düzenlenemeyen ve örtük güven SAP kimliği hizmetine sahip. Hiçbiri için herhangi bir güven ayarı yok.
    > 
    > 

10. Tıklatın **genel** sekmesini ve ardından **Gözat** indirilen meta veri dosyasını karşıya yüklemek için.
    
    ![Yönetim güven](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "güven Yönetimi")
    
    >[!NOTE]
    >Meta veri dosyası, değerlerini karşıya sonra **çoklu oturum açma URL'si**, **çoklu oturum kapatma URL'si** ve **imzalama sertifikası** otomatik olarak doldurulur.
    > 
    > 

11. **Öznitelikler** sekmesine tıklayın.
12. Üzerinde **öznitelikleri** sekmesinde, aşağıdaki adımı gerçekleştirin:
    
    ![Öznitelikleri](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "öznitelikleri") 
  * Tıklatın **Add Assertion-Based özniteliği**ve ardından aşağıdaki onaylama tabanlı öznitelikleri ekleyin:
       
    | Onaylama işlemi özniteliği | Asıl özniteliği |
    | --- | --- |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/givenName |FirstName |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/surname |Soyadı |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/emailaddress |E-posta 
   
     >[!NOTE]
     >Öznitelikleri yapılandırma nasıl HCP üzerinde uygulamaları geliştirilmiş, yani hangi öznitelikleri SAML yanıtta bekledikleri ve kod bu öznitelikte eriştiklerinde hangi adla (asıl özniteliği) bağlıdır.
     > 
     >  

    1.  **Varsayılan özniteliği** ekran görüntüsünde yalnızca gösterim amacıyla kullanılır. İş senaryosu yapmak için gerekli değildir.   
    2.  Adları ve değerleri için **asıl özniteliği** ekran görüntüsünde gösterilen uygulama nasıl geliştirilen bağlıdır. Uygulamanızın farklı eşlemeleri gerektirdiği mümkündür.
     
13. Azure Klasik portalında üzerinde **çoklu oturum açma sırasında SAP HANA bulut platformu yapılandırma** iletişim kutusunda sayfa, tek oturum açma yapılandırması onay seçin ve ardından **tam**.
    
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "çoklu oturum açmayı yapılandırın")

###<a name="assertion-based-groups"></a>Onaylama işlemi tabanlı grupları
İsteğe bağlı bir adım, Azure Active Directory kimlik sağlayıcısı için onaylama tabanlı grupları yapılandırabilirsiniz.

SAP HANA bulut platformunda gruplarını kullanarak dinamik olarak bir veya daha fazla kullanıcı, SAP HANA bulut platformu uygulamalarınızda SAML 2.0 onaylama özniteliklerinin değerlerini tarafından belirlenen bir veya daha fazla rol atamanıza olanak sağlar. 

Onaylama işlemi öznitelik içeriyorsa, örneğin, "*sözleşme geçici =*", etkilenen tüm kullanıcılar grubuna eklenecek isteyebilirler"*geçici*". Grup "*geçici*" SAP HANA bulut platformu hesabınızda dağıtılan bir veya daha fazla uygulamalardan bir veya daha fazla rol içerebilir.
 
Aynı anda çok sayıda kullanıcı uygulamalarının SAP HANA bulut platformu hesabınızda bir veya daha fazla rol atamak istiyorsanız onaylama tabanlı grupları kullanın. Yalnızca tek veya küçük kullanıcı sayısı çok belirli rollere atamak istiyorsanız, bunları doğrudan atama öneririz "**yetkilerini**" SAP HANA bulut platformu Pilot sekmesinde.

## <a name="assign-a-role-to-a-user"></a>Bir kullanıcıya rol atama
SAP HANA bulut platformuna oturum Azure AD kullanıcıları etkinleştirmek için SAP HANA bulut platformu rollerinde onlara atamanız gerekir.

**Bir kullanıcıya rol atamak için aşağıdaki adımları gerçekleştirin:**

1. Oturum, **SAP HANA bulut platformu** Pilot.
2. Aşağıdakileri gerçekleştirin:
   
   ![Yetkilerini](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "yetkileri değiştirme")
   
  1. Tıklatın **yetkilendirme**.
  2. Tıklatın **kullanıcılar** sekmesi.
  3. İçinde **kullanıcı** metin kutusuna, kullanıcının e-posta adresini yazın.
  4. Tıklatın **atamak** kullanıcı role atamak için.
  5. **Kaydet** düğmesine tıklayın.

## <a name="assign-users"></a>Kullanıcılar atama
Yapılandırmanızı test etmek için uygulama erişimi atayarak kullanarak izin vermek istediğiniz Azure AD kullanıcılarının vermeniz gerekir.

**SAP HANA bulut platformu için kullanıcılara atamak için aşağıdaki adımları gerçekleştirin:**

1. Klasik Azure portalında bir test hesabı oluşturun.
2. Üzerinde **SAP HANA bulut platformu** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.
   
   ![Kullanıcılar atama](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "kullanıcı atama")
3. Test kullanıcınız seçin, **atamak**ve ardından **Evet** , atama onaylamak için.
   
   ![Evet](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Evet")

SSO ayarlarınızı test etmek isterseniz, erişim paneli açın. Erişim paneli hakkında daha fazla ayrıntı için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).

