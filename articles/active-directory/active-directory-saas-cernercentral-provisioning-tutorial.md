---
title: "Öğretici: Azure Active Directory ile otomatik kullanıcı sağlamayı Cerner Orta yapılandırma | Microsoft Docs"
description: "Nasıl tooconfigure Azure Active Directory tooautomatically sağlamak kullanıcılar tooa kadrosu Cerner Orta öğrenin."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: asmalser-msft
ms.openlocfilehash: e96da98e783d24e7f34ae924824f909eead75f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a>Öğretici: Cerner Orta otomatik kullanıcı sağlamayı için yapılandırma

Bu öğreticinin Hello hedefi Cerner Orta ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooa kullanıcı kadrosu Cerner Orta tooperform gereken adımları hello tooshow ' dir. 


## <a name="prerequisites"></a>Ön koşullar

Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

*   Azure Active Directory kiracısı
*   Cerner Orta Kiracı 

> [!NOTE]
> Azure Active Directory Cerner hello kullanarak orta ile tümleşen [SCIM'yi](http://www.simplecloud.info/) protokolü.

## <a name="assigning-users-toocerner-central"></a>Kullanıcıların tooCerner Orta atama

Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır. Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir. 

Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD grupları tooCerner Orta erişmesi hello kullanıcıları temsil karar vermeniz gerekir. Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooCerner Orta atayabilirsiniz:

[Bir kullanıcı veya grup tooan kuruluş uygulama atama](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toocerner-central"></a>Kullanıcıların tooCerner Orta atamak için önemli ipuçları

*   Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooCerner merkezi tootest hello atanabilir. Ek kullanıcı ve/veya grupları daha sonra atanabilir.

* Tek bir kullanıcı için ilk test tamamlandıktan sonra amaçlanan kullanıcılar tooaccess tam listesini hello herhangi Cerner çözüm (yalnızca Cerner Merkezi) sağlanan toobe tooCerner ait kullanıcı ad listesi atama Cerner Orta önerir.  Diğer Cerner çözümleri hello kullanıcı ad listesi kullanıcılar bu listesi yararlanın.

*   Bir kullanıcı tooCerner Orta atarken hello seçmelisiniz **kullanıcı** hello atama iletişim rolü. Merhaba "Varsayılan erişim" rolüne sahip kullanıcılar sağlamasından hariç tutulur.


## <a name="configuring-user-provisioning-toocerner-central"></a>Kullanıcı tooCerner Orta hazırlama yapılandırma

Bu bölümde, Azure AD tooCerner Orta ait kullanıcı API sağlama Cerner'ın SCIM'yi kullanıcı hesabını kullanarak ad listesi bağlanma yoluyla sırasında size kılavuzluk eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve atanan kullanıcı hesapları Cerner Orta tabanlı devre dışı bırak Azure AD'de kullanıcı ve grup atama üzerinde.

> [!TIP]
> [Azure Portalı'nda (https://portal.azure.com). sağlanan hello yönergeleri izleyerek Cerner Orta için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir. Daha fazla bilgi için bkz: Merhaba [oturum açma Cerner Orta tek Öğreticisi](active-directory-saas-cernercentral-tutorial.md).


### <a name="tooconfigure-automatic-user-account-provisioning-toocerner-central-in-azure-ad"></a>Azure AD'de tooCerner Orta sağlama tooconfigure otomatik olarak bir kullanıcı hesabı:


Sipariş tooprovision kullanıcı hesapları tooCerner Orta, toorequest Cerner Cerner Orta system hesabından gerekir ve Azure AD'nin tooconnect tooCerner'ın SCIM'yi endpoint kullanabileceği bir OAuth taşıyıcı belirteci oluşturmak. Merhaba tümleştirme tooproduction dağıtmadan önce bir Cerner sanal ortamda gerçekleştirilmesi önerilir.

1.  Merhaba ilk adımı hello Cerner yönetme tooensure hello kişiler ve Azure AD tümleştirme sahip gerekli tooaccess hello belgelerine gerekli toocomplete hello yönergeleri olan CernerCare hesap. Gerekirse, her bir geçerli ortamda hello URL'ler toocreate CernerCare hesapları aşağıda kullanın.

   * Korumalı alan: https://sandboxcernercare.com/accounts/create

   * Üretim: https://cernercare.com/accounts/create  

2.  Ardından, bir sistem hesabı için Azure AD oluşturulması gerekir. Merhaba yönergeleri toorequest bir sistem hesabı altında korumalı alan ve üretim ortamları için kullanın.

   * Yönergeler: https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account

   * Korumalı alan: https://sandboxcernercentral.com/system-accounts/

   * Üretim: https://cernercentral.com/system-accounts/

3.  Ardından, OAuth taşıyıcı belirteci her sistem hesapları için oluşturur. toodo Bu, aşağıdaki izleme hello yönergeleri.

   * Yönergeler: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token

   * Korumalı alan: https://sandboxcernercentral.com/system-accounts/

   * Üretim: https://cernercentral.com/system-accounts/

4. Son olarak, her iki Cerner toocomplete hello yapılandırmasında hello korumalı alan ve üretim ortamları için tooacquire kullanıcı ad listesi bölge kimlikleri gerekir. Hakkında bilgi için tooacquire buna ek olarak, bkz: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM. 

5. Artık Azure AD tooprovision kullanıcı hesapları tooCerner yapılandırabilirsiniz. İçinde toohello oturum [Azure portal](https://portal.azure.com)ve toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölüm.

6. Çoklu oturum açma için zaten Cerner Orta yapılandırdıysanız, Cerner hello arama alanı kullanarak orta Örneğiniz için arama yapın. Aksi takdirde seçin **Ekle** arayın ve **Cerner orta** hello uygulama galerisinde. Merhaba Arama sonuçlarından Cerner Orta seçin ve uygulamaların tooyour listesine ekleyin.

7.  Cerner Orta örneğiniz seçin ve ardından hello **sağlama** sekmesi.

8.  Set hello **sağlama modu** çok**otomatik**.

   ![Cerner sağlama Orta](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  Alanlar'ın altında aşağıdaki hello doldurun **yönetici kimlik bilgileri**:

   * Merhaba, **Kiracı URL** alan, "Kullanıcı-ad listesi-bölge-ID" Merhaba bölge kimliği #4. adımda aldığınız değiştirerek bir URL aşağıda hello biçiminde girin.

> Korumalı alan: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/ 

> Üretim: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/ 

   * Merhaba, **gizli belirteci** alanına #3. adımda oluşturulan hello OAuth taşıyıcı belirteci girin ve tıklatın **Bağlantıyı Sına**.

   * Merhaba upperright tarafında portalınızı başarı bildirim görmeniz gerekir.

10. Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve aşağıdaki hello onay kutusunu işaretleyin.

11. **Kaydet** düğmesine tıklayın. 

12. Merhaba, **öznitelik eşlemelerini** bölümünde, hello kullanıcı ve grup öznitelikleri toobe eşitlenmiş Azure AD tooCerner Orta gözden geçirin. Merhaba olarak seçilen öznitelikler **eşleşen** kullanılan toomatch hello kullanıcı hesapları ve grupları Cerner Orta güncelleştirme işlemleri için özellikleridir. Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.

13. tooenable hello Cerner Orta, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello içinde **ayarları** bölümü

14. **Kaydet** düğmesine tıklayın. 

Bu, tüm kullanıcıların hello ilk eşitleme başlatır ve/veya gruplarının tooCerner Orta hello kullanıcılar ve Gruplar bölümünde atanmış. Merhaba ilk eşitleme yaklaşık 20 dakikada hello Azure AD sağlama hizmeti çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır. Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve Cerner Orta uygulama hizmeti sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.

Hello Azure AD tooread sağlama nasıl oturum ile ilgili daha fazla bilgi için bkz: [otomatik olarak bir kullanıcı hesabı sağlama raporlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

## <a name="additional-resources"></a>Ek kaynaklar

* [Cerner Orta: Azure AD kullanarak kimlik verilerini yayımlama](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [Öğretici: Azure Active Directory ile çoklu oturum açma Cerner Orta yapılandırma](active-directory-saas-cernercentral-tutorial.md)
* [Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme](active-directory-enterprise-apps-manage-provisioning.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Sonraki adımlar
* [Tooreview nasıl günlüğe yazacağını öğrenin ve get raporlar etkinlik sağlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).
