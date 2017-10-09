---
title: "Öğretici: Azure Active Directory ile otomatik kullanıcı sağlamayı kayma yapılandırma | Microsoft Docs"
description: "Nasıl tooSlack tooconfigure, Azure Active Directory tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesapları öğrenin."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: asmalser-msft
ms.reviewer: asmalser
ms.openlocfilehash: d0a565bbe0bd7e229b9dd99b1ebbaf67d93a2206
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a>Öğretici: Kayma otomatik kullanıcı sağlamayı için yapılandırma


Merhaba Bu öğreticinin amacı olan kayma ve Azure tooperform gereken adımları hello tooshow AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooSlack. 

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

*   Bir Azure Active Active directory kiracısı
*   Bir boşluk ile Merhaba Kiracı [planı artı](https://aadsyncfabric.slack.com/pricing) veya daha iyi etkin 
*   Kayma takım yönetici izinlerine sahip bir kullanıcı hesabı 

Not: Azure AD tümleştirme sağlama kullanır üzerinde hello hello [Slack'e SCIM'yi API](https://api.slack.com/scim) kullanılabilir tooSlack takımlar temelinde hello planı artı ya da daha iyi olduğu.

## <a name="assigning-users-tooslack"></a>Kullanıcıların tooSlack atama

Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır. Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir. 

Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya tooyour Slack uygulamasına erişmesi Azure AD temsil hello kullanıcılar gruplarında toodecide gerekir. Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour Slack uygulama atayabilirsiniz:

[Bir kullanıcı veya grup tooan kuruluş uygulama atama](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-tooslack"></a>Kullanıcıların tooSlack atamak için önemli ipuçları

*   Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooSlack tootest hello atanabilir. Ek kullanıcı ve/veya grupları daha sonra atanabilir.

*   Bir kullanıcı tooSlack atarken hello seçmelisiniz **kullanıcı** veya hello atama iletişim kutusunda "Grubu" rolü. Merhaba "Varsayılan erişim" rolü sağlama için çalışmaz.


## <a name="configuring-user-provisioning-tooslack"></a>Kullanıcı tooSlack hazırlama yapılandırma 

Bu bölümde, Azure AD tooSlack kullanıcının kullanıcı hesabı API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve Azure AD'de kullanıcı ve grup atama göre kayma atanan kullanıcı hesaplarında devre dışı bırakın.

**İpucu:** tooenabled SAML tabanlı çoklu oturum açma (Azure Portalı'nda) sağlanan hello yönergeleri izleyerek kayma için tercih edebilirsiniz [https://portal.azure.com]. Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.


### <a name="tooconfigure-automatic-user-account-provisioning-tooslack-in-azure-ad"></a>Azure AD'de tooSlack sağlama tooconfigure otomatik olarak bir kullanıcı hesabı:


1)  Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.

2) Çoklu oturum açma için zaten kayma yapılandırdıysanız, hello arama alanı kullanarak kayma Örneğiniz için arama yapın. Aksi takdirde seçin **Ekle** arayın ve **Slack'e** hello uygulama galerisinde. Kayma hello Arama sonuçlarından seçin ve uygulamaların tooyour listesine ekleyin.

3)  Kayma örneğiniz seçin ve ardından hello **sağlama** sekmesi.

4)  Set hello **sağlama modu** çok**otomatik**.

![Sağlama boşluk](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  Merhaba altında **yönetici kimlik bilgileri** 'yi tıklatın **Authorize**. Bu, yeni bir tarayıcı penceresinde bir Slack yetkilendirme iletişim kutusunu açar. 

6) Merhaba yeni pencerede kayma takım yönetim hesabınızı kullanarak oturum açın. Hello elde edilen yetkilendirme iletişim kutusunda, select hello tooenable sağlamayı istiyor ve ardından Slack ekip **Authorize**. Bir kez tamamlanan, dönüş toohello Azure portal toocomplete hello yapılandırma sağlama.

![Yetkilendirme iletişim](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour Slack uygulama bağlanabilir. Merhaba bağlantı başarısız olursa Slack hesabınızın Team yönetici izinlerine sahip olduğundan emin olun ve hello "Yetkilendir" adım yeniden deneyin.

8) Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve aşağıdaki hello onay kutusunu işaretleyin.

9) **Kaydet** düğmesine tıklayın. 

10) Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooSlack**.

11) Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooSlack eşitleneceğini hello kullanıcı öznitelikleri gözden geçirin. Seçilen öznitelikler hello Not **eşleşen** özellikleri, Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları kayma içinde güncelleştirme işlemleri için olacaktır. Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.

12) tooenable hello kayma, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello içinde **ayarları** bölümü

13) **Kaydet** düğmesine tıklayın. 

Bu, herhangi bir kullanıcı ve/veya hello kullanıcılar tooSlack ve Gruplar bölümü atanan gruplarını hello ilk eşitleme başlatır. Merhaba ilk eşitleme yaklaşık her 10 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform gerektiğine dikkat edin. Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve Slack uygulamanızdan hizmet sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.

## <a name="optional-configuring-group-object-provisioning-tooslack"></a>[İsteğe bağlı] Grup nesnesi tooSlack sağlama yapılandırma 

İsteğe bağlı olarak, Azure AD tooSlack Grup nesnelerle hello sağlamayı etkinleştirebilirsiniz. Bu "kullanıcı gruplarını atamasını" farklıdır, bu hello gerçek Grup nesnesi ayrıca tooits üyeleri Azure AD tooSlack çoğaltılır. Örneğin, Azure AD içinde "My grubu" adlı bir grup varsa, "My grubu" adlı bir identitical grubu kayma içinde oluşturulur.

### <a name="tooenable-provisioning-of-group-objects"></a>tooenable group nesnelerini sağlama:

1) Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory grupları tooSlack**.

2) Merhaba eşleme özniteliği dikey penceresinde, etkin tooYes ayarlayın.

3) Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooSlack eşitleneceğini hello grup öznitelikleri gözden geçirin. Seçilen öznitelikler hello Not **eşleşen** özellikler kullanılan toomatch hello gruplarında kayma güncelleştirme işlemleri için olacaktır. 

4) **Kaydet** düğmesine tıklayın.

Merhaba, tüm Grup atanmış nesneleri tooSlack bu sonucu **kullanıcılar ve gruplar** tam olarak Azure AD tooSlack eşitlenmekte olan bölüm. Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve Slack uygulamanızdan hizmet sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.


## <a name="additional-resources"></a>Ek Kaynaklar

* [Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme](active-directory-enterprise-apps-manage-provisioning.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
