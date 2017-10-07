---
title: "Öğretici: Salesforce korumalı alan Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Azure Active Directory tooenable ile toouse Salesforce korumalı alan nasıl tek oturum açma, otomatik sağlama ve daha fazlasını öğrenin!."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: deccd6a07b57c8ba56b7e1c3f3ab311813ca017b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a>Öğretici: Azure Active Directory Tümleştirme ile Salesforce korumalı alan

Bu öğreticinin Hello hedefi tooshow hello tümleştirilmesi Azure ve Salesforce korumalı alan ' dir.  

>[!TIP]
>Geri bildirim için bkz: Merhaba [Azure destek sayfası](http://go.microsoft.com/fwlink/?LinkId=521878). 
> 

Kuruluşunuz çeşitli geliştirme gibi amaçlar için farklı ortamlarda birden çok kopyasını özelliği toocreate sınama ve eğitim aşılmasını hello veri ve uygulamaları, Salesforce üretimde olmadan hello sanal verin Kuruluş.  

Daha fazla ayrıntı için bkz: [korumalı alan genel bakış](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)

Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

* Geçerli bir Azure aboneliği
* Bir korumalı alan Salesforce.com'da

Geçerli bir korumalı alan Salesforce.com'da henüz yoksa, toocontact Salesforce gerekir.

Bu öğreticide gösterilen hello senaryo yapı taşları aşağıdaki Merhaba oluşur:

1. Salesforce korumalı alan için etkinleştirme hello uygulama tümleştirmesi
2. Çoklu oturum açma (SSO) yapılandırma
3. Etki alanınızı etkinleştirme
4. Kullanıcı hazırlama işleminin yapılandırılması
5. Kullanıcılar atama

![Senaryo](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "senaryosu")

## <a name="enable-hello-application-integration-for-salesforce-sandbox"></a>Salesforce korumalı alan için Hello uygulama tümleştirmeyi etkinleştir
Bu bölümde Hello amacı olan toooutline nasıl tooenable hello uygulama tümleştirmesi Salesforce korumalı alan için.

**Salesforce korumalı alan için tooenable hello uygulama tümleştirmesi hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello sol gezinti bölmesinde, Klasik Azure portalı tıklatın **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")
2. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.
3. Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.
   
   ![Uygulamaları](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "uygulamalar")
4. tooopen hello **uygulama Galerisi**, tıklatın **uygulama Ekle**ve ardından **my kuruluş toouse için uygulama ekleme**.
   
   ![Neler toodo istiyorsunuz? ] (./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "Neler toodo istiyorsunuz?")
5. Merhaba, **arama kutusu**, türü **Salesforce korumalı alan**.
   
   ![Uygulama Galerisi](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "uygulama Galerisi")
6. Merhaba sonuçlar bölmesinde seçin **Salesforce korumalı alan**ve ardından **tam** tooadd Merhaba uygulaması.
   
   ![Salesforce korumalı alan](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce korumalı alan")
   
## <a name="configur-single-sign-on-sso"></a>Configur çoklu oturum açma (SSO)

Bu bölümde Hello amacı nasıl tooenable kullanıcılar tooauthenticate tooSalesforce Federasyon kullanarak Azure AD'de hesabıyla hello SAML protokolünü temel toooutline ' dir.

**tooconfigure çoklu oturum açma, hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba hello üzerinde Klasik Azure portalı içinde **Salesforce korumalı alan** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **tek oturum yapılandırma üzerinde aktar** iletişim kutusu.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "çoklu oturum açmayı yapılandırın")
2. Merhaba üzerinde **nasıl tooSalesforce Sandbox üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.
   
   ![Salesforce korumalı alan](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce korumalı alan")
3. Merhaba üzerinde **uygulama URL'sini Yapılandır** sayfasında hello **oturum üzerinde URL'si** metin kutusuna, desen aşağıdaki hello kullanarak URL'nizi yazın `http://company.my.salesforce.com`ve ardından **sonraki**.
   
   ![Uygulama URL'sini Yapılandır](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "uygulama URL'sini yapılandırın")
4. Zaten başka bir Salesforce korumalı alan örneği için çoklu oturum açmayı dizininizde yapılandırdıktan sonra hello yapılandırmanız da gerekir **tanımlayıcısı** toohave hello hello aynı değere **URL üzerinde oturum**. 
 * Merhaba **tanımlayıcısı** alan hello denetleyerek bulunabilir **Göster Gelişmiş ayarları** hello onay kutusuna **uygulama URL'sini yapılandırın** hello iletişim sayfası.
5. Merhaba üzerinde **çoklu oturum açma sırasında Salesforce korumalı alan yapılandırmak** sayfasında, **indirme sertifika**ve ardından hello sertifika dosyayı bilgisayarınıza kaydedin.
   
   ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "çoklu oturum açmayı yapılandırın")
6. Farklı web tarayıcısı penceresinde, Salesforce korumalı alan yönetici olarak oturum açın.
7. Hello içinde hello üst menüsünde **Kurulum**.
   
   ![Kurulum](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Kurulumu")
8. Merhaba Gezinti hello sol taraftaki bölmede **güvenlik denetimleri**ve ardından **çoklu oturum açma ayarları**.
   
   ![Çoklu oturum açma ayarları](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "tek oturum açma ayarları")
9. Hello çoklu oturum açma ayarları bölümü, hello aşağıdaki adımları gerçekleştirin:
   
   ![Çoklu oturum açma ayarları](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "tek oturum açma ayarları")  
 1.  Seçin **SAML etkin**. 
 2.  **Yeni**’ye tıklayın.
10. SAML çoklu oturum açma ayarları bölümü Hello üzerinde hello aşağıdaki adımları gerçekleştirin:
    
    ![SAML çoklu oturum açma ayarları](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML çoklu oturum açma ayarları")  
 1. Merhaba adı metin kutusuna hello yapılandırma hello adını yazın (örneğin: *SPSSOWAAD\_Test*). 
 2. Merhaba hello üzerinde Klasik Azure portalı içinde **çoklu oturum açma sırasında Salesforce korumalı alan yapılandırmak** iletişim kutusu sayfası, kopyalama hello **veren URL'si** değer ve hello yapıştırma **veren**metin kutusu.
 3. Merhaba, **varlık kimliği** metin kutusuna, türü **https://test.salesforce.com** bu hello tooyour dizin eklediğiniz ilk Salesforce korumalı alan örneği ise. Salesforce korumalı alan, sonra da hello için bir örneği zaten eklediyseniz **varlık kimliği** hello türü **oturum üzerinde URL'si**, şu biçimde olmalıdır:`http://company.my.salesforce.com`   
 4. Tıklatın **Gözat** tooupload hello sertifika indirilir.  
 5. Olarak **SAML kimlik türü**seçin **onaylamayı içeren hello Federasyon kimliği hello kullanıcı nesnesinden**. 
 6. Olarak **SAML kimlik konumu**seçin **kimliktir hello NameIdentifier öğesinde hello konu deyimi**.
 7. Merhaba hello üzerinde Klasik Azure portalı içinde **çoklu oturum açma sırasında Salesforce korumalı alan yapılandırmak** iletişim kutusu sayfası, kopyalama hello **uzaktan oturum açma URL'si** değer ve hello yapıştırma **kimlik sağlayıcısı Oturum açma URL'si** metin kutusu. 
 8. SAML oturum kapatma SFDC desteklemez.  Geçici bir çözüm olarak Yapıştır 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' hello içine **kimlik sağlayıcısı oturum kapatma URL'si** metin kutusu.
 9. Olarak **hizmet sağlayıcısı tarafından başlatılan bağlama isteği**seçin **HTTP POST**. 
 10. **Kaydet** düğmesine tıklayın.
11. Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **tam** tooclose hello **tek oturum yapılandırma üzerinde aktar** iletişim.
    
    ![Çoklu oturum açma yapılandırma](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "çoklu oturum açmayı yapılandırın")

## <a name="enable-your-domain"></a>Etki alanınızı etkinleştir
Bu bölümde, bir etki alanı zaten oluşturduğunuzu varsayar.  Daha fazla ayrıntı için bkz: [etki alanı adınız tanımlama](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).

**tooenable etki alanınızı hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba sol gezinti bölmesinde **etki alanı yönetimi**ve ardından **My etki alanı.**
   
   ![Etki alanım](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "etki alanım")
   
   >[!NOTE]
   >Lütfen etki alanınızı doğru yapılandırılmış olduğundan emin olun. 
   > 
2. Merhaba, **oturum açma sayfası ayarları** 'yi tıklatın **Düzenle**, sonra **kimlik doğrulama hizmeti**seçin hello önceki gelen oturum açma SAML tek ayar hello hello adı bölümünde ve son olarak tıklatın **kaydetmek**.
   
   ![Etki alanım](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "etki alanım")

Yapılandırılmış bir etki alanınız hemen kullanıcılarınızın hello etki alanı URL'si toologin toohello Salesforce korumalı alan kullanmanız gerekir.  

Merhaba URL tooget hello değeri hello önceki bölümde oluşturduğunuz hello SSO profil'ı tıklatın.

## <a name="configure-user-provisioning"></a>Kullanıcı sağlamayı Yapılandır
Bu bölümde Hello amacı olan toooutline nasıl tooenable Active Directory kullanıcısı kullanıcı sağlamayı tooSalesforce korumalı alan hesapları.

**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**

1. Merhaba üst gezinti çubuğundaki hello Salesforce portalında kullanıcı menünüze adı tooexpand seçin:
   
   ![Ayarlarımı](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "ayarlarım")
2. Kullanıcı menüsünden seçin **My ayarları** tooopen, **My ayarları** sayfası.
3. Merhaba sol bölmede **kişisel** tooexpand kişisel bölüm hello ve ardından **sıfırlama My güvenlik belirteci**:
   
   ![Ayarlarımı](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "ayarlarım")
4. Merhaba üzerinde **sıfırlama My güvenlik belirteci** sayfasında, **güvenlik belirteci sıfırlama** toorequest Salesforce.com güvenlik belirteci içeren bir e-posta.
   
   ![Yeni bir belirteç](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "yeni belirteci")
5. Bir e-posta ile Salesforce.com için e-posta kutunuzu kontrol edin "**salesforce.com.com güvenlik onaylama**" konu olarak.
6. Bu e-posta ve kopyalama hello güvenlik belirteci değerini inceleyin.
7. Merhaba hello üzerinde Klasik Azure portalı içinde **salesforce korumalı alan** uygulama tümleştirme sayfası, tıklatın **kullanıcı sağlamayı Yapılandır** tooopen hello **yapılandırma kullanıcı sağlamayı**iletişim.
   
   ![Kullanıcı sağlamayı Yapılandır](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "kullanıcı sağlamayı Yapılandır")
8. Merhaba üzerinde **, Salesforce korumalı alan kimlik bilgileri tooenable otomatik kullanıcı sağlamayı girin** sayfasında, yapılandırma ayarlarını aşağıdaki hello sağlayın:
   
   ![Salesforce korumalı alan](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce korumalı alan")   
 1. Merhaba, **Salesforce korumalı alan yönetici kullanıcı adı** metin kutusuna, Salesforce korumalı alan hesap hello sahip adı türü **Sistem Yöneticisi** atanan Salesforce.com profilinde.
 2. Merhaba, **Salesforce korumalı alan yönetici parolası** metin kutusuna, bu hesap için hello parolayı girin.
 3. Merhaba, **kullanıcı güvenlik belirteci** metin kutusuna, Yapıştır hello güvenlik belirteci değeri.
 4. Tıklatın **doğrulama** tooverify yapılandırmanızı.
 5. Merhaba tıklatın **sonraki** düğmesini tooopen hello **onay** sayfası.
9. Merhaba üzerinde **onay** sayfasında, **tam** toosave yapılandırmanızı.
   
## <a name="assigning-users"></a>Kullanıcılar atama

tootest yapılandırmanıza, uygulama erişim tooit atayarak kullanarak tooallow istediğiniz toogrant hello Azure AD kullanıcıları gerekir.

**tooassign kullanıcılar tooSalesforce korumalı alan, hello aşağıdaki adımları gerçekleştirin:**

1. Hello Klasik Azure portalı, bir test hesabı oluşturun.
2. Hello üzerinde ** Salesforce korumalı alan ** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.
   
   ![Kullanıcılar atama](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "kullanıcı atama")
3. Test kullanıcınız seçin, **atamak**ve ardından **Evet** tooconfirm, atama.
   
   ![Evet](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Evet")

Şimdi 10 dakika bekleyin ve hello hesap eşitlenmiş tooSalesforce korumalı alan olduğunu doğrulamanız gerekir.

SSO ayarlarınızı tootest istiyorsanız hello erişim paneli açın. Merhaba erişim paneli hakkında daha fazla ayrıntı için bkz: [giriş toohello erişim paneli](https://msdn.microsoft.com/library/dn308586).

