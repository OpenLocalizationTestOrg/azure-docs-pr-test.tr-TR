---
title: "aaaSelf hizmet uygulama erişimi ve Azure Active Directory ile yetkilendirilmiş Yönetimi | Microsoft Docs"
description: "Bu makalede nasıl tooenable Self Servis uygulamaya erişim ve Azure Active Directory ile yetkilendirilmiş yönetimi açıklanmaktadır."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 448a7fe8-a162-475e-9ba2-2e3ab59302bc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: asmalser
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 90bec3bd71796f22a782929b028db0d18c3aa1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-application-access-and-delegated-management-with-azure-active-directory"></a>Self Servis uygulamaya erişim ve Azure Active Directory ile yetkilendirilmiş Yönetimi
Son kullanıcılarınız için Self Servis özellikleri etkinleştirme, kurumsal BT için ortak bir senaryodur. Kullanıcılar, uygulamaları ve best-informed toomake erişimi olan hello kişi çok sayıda kararları hello directory yönetici olmayabilir verin. Uygulamaya kimlerin erişebileceğini genellikle hello en iyi kişi toodecide bir takım lideri veya diğer temsilci olarak atanan yönetici değil. Ancak, hello uygulama kullanan hello kullanıcı ve hello kullanıcı bilir ne toobe mümkün toodo işlerini ihtiyaç duydukları.

> [!IMPORTANT]
> Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı. 

Self Servis uygulamaya erişim özelliğidir [Azure Active Directory Premium](https://azure.microsoft.com/trial/get-started-active-directory/) P1 ve P2 directory yöneticileri izin veren lisans:

* "Daha fazla uygulama Al" kullanarak tooapplications döşeme hello kullanıcılara toorequest erişimi etkinleştirmek [Azure AD erişim paneli](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)
* Hangi uygulamaların kullanıcıların erişim istemek ayarlama
* Bir onay kullanıcılar toobe mümkün tooself Ata erişim tooan uygulamanız için gerekli olup olmadığını ayarlayın
* Merhaba isteklerinin onaylanması ve her uygulama için erişim yöneten ayarlama

Federe veya parola tabanlı çoklu oturum açma hello destekleyen tüm önceden tümleştirilmiş ve özel uygulamalar için bu özelliği bugün desteklenen [Azure Active Directory Uygulama galerisinde](https://azure.microsoft.com/marketplace/active-directory/all/), Salesforce, Dropbox gibi uygulamalar dahil olmak üzere Google Apps ve daha fazlası.
Bu makalede nasıl yapılır:

* İsteğe bağlı onay iş akışı yapılandırma dahil olmak üzere son kullanıcılar için Self Servis uygulama erişimi yapılandırma 
* Erişim yönetimi, kuruluşunuzda belirli uygulamaları toohello en uygun kişiler için temsilci seçme ve toouse hello Azure AD erişim paneli tooapprove erişim isteklerini etkinleştirmek, doğrudan erişimi tooselected kullanıcılar atayın veya (isteğe bağlı olarak) ayarlama parola tabanlı çoklu oturum açma yapılandırıldığında, uygulama erişimi için kimlik bilgileri

## <a name="configuring-self-service-application-access"></a>Self Servis uygulama erişimi yapılandırma
tooenable Self Servis uygulamaya erişim hangi uygulamaların eklenebilir veya, son kullanıcılarınız tarafından istenen bu yönergeleri izleyin ve yapılandırılır.

1. Merhaba içine oturum [Klasik Azure portalı](https://manage.windowsazure.com/).

2.   Merhaba altında **Active Directory** bölümünde, dizininizi seçin ve ardından hello **uygulamaları** sekmesi. 

3. Select hello **Ekle** button ve hello Galerisi seçeneği tooselect ve bir uygulama ekleyin.

4. Uygulamanızı eklendikten sonra hello uygulaması hızlı başlangıç sayfası alırsınız. Tıklatın **yapılandırma çoklu oturum açma**hello istenen tek oturum açma modunu seçin ve hello yapılandırmayı kaydedin. 

5. Ardından, hello'ı seçin **yapılandırma** sekmesini tooenable kullanıcılar toorequest erişim toothis uygulamadan hello Azure AD erişim paneli ayarlamak **Self Servis uygulamaya erişim izin** çok**Evet**.
  
  ![][1]

6. toooptionally erişim istekleri için bir onay iş akışı yapılandırma kümesi **erişim vermeden önce onay gerektiren** çok**Evet**. Bir veya daha fazla onaylayanlar hello kullanarak seçilebilir sonra **onaylayanlar** düğmesi.

  Onaylayan bir Azure AD hesapla hello kuruluştaki herhangi bir kullanıcı olabilir ve lisans, hesap sağlama için sorumlu olabilir veya başka bir iş sürecini erişim tooan uygulama vermeden önce kuruluşunuzun gerektirir. Merhaba onaylayan bile hello Grup sahibi bir veya daha fazla hesap grupları paylaşılan ve hello kullanıcılar tooone paylaşılan bir hesap erişim bu grupları toogive, atayabilirsiniz olabilir. 

  Hiçbir onay gerekiyorsa, kullanıcılar Anında hello uygulama eklenen tootheir Azure AD erişim paneli alır. Merhaba uygulaması için ayarlarsanız, [otomatik kullanıcı sağlamayı](active-directory-saas-app-provisioning.md), veya ayarlandığına ["kullanıcı tarafından yönetilen" parola SSO modu](active-directory-appssoaccess-whatis.md#password-based-single-sign-on), hello kullanıcı hesabı ve hello parolayı bilmeniz bir kullanıcı zaten sahip olmalıdır.

7. Merhaba uygulaması yapılandırılmış toouse yüklediyse parola tabanlı çoklu oturum açma, hello onaylayan tooset hello SSO kimlik her kullanıcı adına izin vermek için bir seçenek daha sonra da kullanılabilir. Daha fazla bilgi için üzerinde hello bölümüne bakın. [erişim yönetimi için temsilci](#delegated-application-access-management).

8. Son olarak, hello **Self-Assigned kullanıcılar için grubu** hello verilen veya erişimi toohello uygulama atanan kullanılan toostore hello kullanıcıları hello grup adını gösterir. Merhaba erişim onaylayan, bu grubun hello sahibi olur. Gösterilen hello grup adı yoksa, otomatik olarak oluşturulur. İsteğe bağlı olarak hello grup adı, varolan bir grubu toohello adını ayarlanabilir.

9. toosave hello yapılandırma tıklatın **kaydetmek** Merhaba ekranında hello sonundaki. Artık kullanıcıların toorequest erişim toothis hello erişim paneli uygulamadan yapabilirsiniz.

10. tootry hello son kullanıcı deneyimi, oturum https://myapps.microsoft.com, tercihen uygulama onaylayan değil farklı bir hesap kullanarak, kuruluşunuzun Azure AD erişim paneli açın. 

11. Merhaba altında **uygulamaları** sekmesini ve ardından hello **daha fazla uygulama alın** döşeme. Bu kutucuğu tüm hello özelliği toosearch ve hello soldaki uygulama kategoriye göre filtre ile Merhaba dizinde Self Servis uygulamaya erişim için etkinleştirilmiş hello uygulamaları Galerisi görüntüler. 

12. Bir uygulama üzerinde tıklatarak hello istek işlem başlatır. Onay işlemi gereklidir sonra Merhaba uygulaması hemen eklenecek hello altında **uygulamaları** sekmesinden kısa bir onay sonra. Onay gerekiyorsa, bunu belirten bir iletişim kutusu görürsünüz ve toohello onaylayanlar bir e-posta gönderilir. Hello imzalanmalıdır erişim paneli onaylayan olmayan toosee bu istek işlemi.

13. Merhaba e-posta hello onaylayan toosign hello Azure AD erişim paneline yönlendirir ve hello isteğini onaylayın. Merhaba istek onaylandıktan (ve tanımladığınız herhangi bir özel işlem hello onaylayan tarafından gerçekleştirilmiş sonra) hello kullanıcı altında göründüğünü Merhaba uygulaması görür kendi **uygulamaları** burada kullanıcılar oturum açabilir içine sekmesi.

## <a name="delegated-application-access-management"></a>Temsilci uygulamaya erişim yönetimi
Uygulama erişimi onaylayıcı, kuruluşunuzdaki hello en uygun kişi tooapprove olan herhangi bir kullanıcı olması veya erişim toohello uygulama söz konusu reddedin. Bu kullanıcının lisans, hesap sağlama için sorumlu olabilir veya erişim tooan uygulama vermeden önce kuruluşunuzun başka bir iş sürecini gerektirir.

Yukarıda açıklanan Self Servis uygulamaya erişim yapılandırırken herhangi onaylayanlar bkz ek atanan uygulama **uygulamalarını yönet** oldukları uygulamaları gösterir hello Azure AD erişim paneli parçasında Merhaba access Yöneticisi. Bir uygulamaya tıklamak çeşitli seçeneklere sahip bir ekran gösterir.

![][2]

### <a name="approve-requests"></a>İsteği onaylama
Hello **isteklerini onaylama** döşemesi sağlayan onaylayanlar herhangi bekleyen onayları belirli toothat uygulama ve burada hello istekleri yeniden yönlendirmeleri toohello onayları sekmesini onaylanabilir veya reddedildi toosee. Her bir istek hangi toodo yönlendiren oluşturulduğunda hello onaylayan de otomatik e-postaları alır.

### <a name="add-users"></a>Kullanıcıları ekleme
Merhaba **Kullanıcı Ekle** döşeme toodirectly grant seçili kullanıcıların erişim toohello uygulama onaylayanlar sağlar. Bu kutucuğu tıklatıldığında, hello onaylayan bir iletişim kutusu tooview ve kullanıcılar için arama kendi dizininde veren görür. Bu kullanıcının Azure AD erişim panelleri veya Office 365 gösterildikten hello uygulamada bir kullanıcı sonuçları ekleniyor. Sağlama işlemi herhangi bir el ile kullanıcı gerekiyorsa, mümkün toosign hello uygulama hello kullanıcı önce altındadır sonra hello onaylayan erişim vermeden önce bu işlemi gerçekleştirmeniz gerekir.  

### <a name="manage-users"></a>Kullanıcıları yönetme
Merhaba **kullanıcıları yönetme** döşeme verir onaylayanlar toodirectly güncelleştirme veya hangi kullanıcıların erişimi kaldırma toohello uygulama. 

### <a name="configure-password-sso-credentials-if-applicable"></a>Parola SSO kimlik bilgilerini (varsa) yapılandırın
Merhaba **yapılandırma** kutucuğu yalnızca gösterilen Merhaba uygulaması tarafından hello BT yöneticisi toouse parola tabanlı çoklu oturum açma yapılandırıldığından ve hello Yöneticisi verilen hello onaylayan hello özelliği tooset parola SSO kimlik daha önce açıklandığı gibi. Nasıl hello kimlik yayılan tooassigned kullanıcılar için bu onay kutusu seçildiğinde, hello onaylayan çeşitli seçenekler sunulur:

![][3]

* **Kullanıcıların kendi parolalarını oturum oturum** – ne kendi kullanıcı adları ve parolalar hello uygulama için ve istendiğinde tooenter olduğundan bu modda, atanan hello kullanıcıları bilgilendirin bunları ilk oturum açma toohello uygulamasına bağlıdır. Merhaba senaryo toohello parola SSO çalışması hello burada karşılık gelen [kullanıcıların kimlik bilgilerini yönetme](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).
* **Kullanıcılar, yönetebilirim ayrı hesaplar kullanarak otomatik olarak oturumunuz** – bu modda hello atanan kullanıcılar gerekli tooenter olmayan ya da uygulamaya özgü kimlik bilgilerini hello uygulamasına imzalarken bildirin. Bunun yerine, hello onaylayan hello kimlik bilgilerini her kullanıcı için erişim hello kullanarak atadıktan sonra Ayarlar **Kullanıcı Ekle** döşeme. Merhaba kullanıcı Merhaba uygulaması kullanıcıların erişim panelinde ya da Office 365 tıkladığında, bunlar otomatik olarak hello onaylayan tarafından ayarlanmış hello kimlik bilgilerini kullanarak oturum açtınız. Merhaba senaryo toohello parola SSO çalışması hello burada karşılık gelen [yöneticileri kimlik bilgilerini yönetir](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).
* **Kullanıcılar, yönetebilirim tek bir hesap kullanarak otomatik olarak oturumunuz** -tüm atanan kullanıcılar tek bir paylaşılan hesabı kullanarak erişim izni toobe gerektiğinde özel bir durum bu uygun toouse durumdur. Merhaba en yaygın kullanımı bu özellik için burada bir kuruluşun tek "Şirket" hesabı varsa ve birden çok kullanıcı toomake güncelleştirmeleri toothat hesabınızın olması gerekir sosyal medya uygulamalarla durumdur. Merhaba senaryo da toohello parola SSO çalışması hello burada karşılık gelen [yöneticileri kimlik bilgilerini yönetir](active-directory-appssoaccess-whatis.md#password-based-single-sign-on). Ancak, bu seçeneği belirledikten sonra hello onaylayan istendiğinde tooenter hello kullanıcı adı ve parolasını hello tek paylaşılan olacaktır. Tamamlandığında, tüm atanan kullanıcılar hello uygulamada kendi Azure AD erişim panelleri veya Office 365 tıklayarak, bu hesabı kullanarak oturum açtınız.

## <a name="additional-resources"></a>Ek Kaynaklar
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)

<!--Image references-->
[1]: ./media/active-directory-self-service-application-access/ssaa_admin.PNG
[2]: ./media/active-directory-self-service-application-access/ssaa_ap_manage_app.PNG
[3]: ./media/active-directory-self-service-application-access/ssaa_ap_manage_app_config.PNG
