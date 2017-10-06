---
title: "Öğretici: Azure Active Directory ile otomatik kullanıcı sağlamayı LinkedIn satış Gezgini yapılandırma | Microsoft Docs"
description: "Nasıl tooLinkedIn satış Gezgini tooconfigure, Azure Active Directory tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesapları öğrenin."
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
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 322c5271535994c13a9fafadbf74f356cdfe865d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-linkedin-sales-navigator-for-automatic-user-provisioning"></a>Öğretici: LinkedIn satış Gezgini otomatik kullanıcı sağlamayı için yapılandırma


Bu öğreticinin Hello hedefi LinkedIn satış Gezgini ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooLinkedIn satış Gezgini tooperform gereken adımları hello tooshow ' dir. 

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

*   Azure Active Directory kiracısı
*   Bir LinkedIn satış Gezgini Kiracı 
*   Bir yönetici hesabıyla LinkedIn satış Gezgininde erişim toohello LinkedIn hesap Merkezi

> [!NOTE]
> Azure Active Directory hello kullanarak LinkedIn satış Gezgini ile tümleşir [SCIM'yi](http://www.simplecloud.info/) protokolü.

## <a name="assigning-users-toolinkedin-sales-navigator"></a>Kullanıcıların tooLinkedIn satış Gezgini atama

Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır. Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir. 

Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD tooLinkedIn satış Gezgini erişmesi hello kullanıcıları temsil gruplarında toodecide gerekir. Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooLinkedIn satış Gezgini atayabilirsiniz:

[Bir kullanıcı veya grup tooan kuruluş uygulama atama](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolinkedin-sales-navigator"></a>Kullanıcıların tooLinkedIn satış Gezgini atamak için önemli ipuçları

*   Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooLinkedIn satış Gezgini tootest hello atanabilir. Ek kullanıcı ve/veya grupları daha sonra atanabilir.

*   Bir kullanıcı tooLinkedIn satış Gezgini atarken hello seçmelisiniz **kullanıcı** hello atama iletişim rolü. Merhaba "Varsayılan erişim" rolü sağlama için çalışmaz.


## <a name="configuring-user-provisioning-toolinkedin-sales-navigator"></a>Kullanıcı tooLinkedIn satış Gezgini hazırlama yapılandırma

Bu bölümde, API sağlama, Azure AD tooLinkedIn satış Gezgini'nın SCIM'yi kullanıcı hesabı konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve LinkedIn satış kullanıcıyı temel alarak Gezgininde atanan kullanıcı hesapları devre dışı bırak ve Azure AD'de Grup ataması.

> [!TIP]
> Sağlanan hello yönergeleri izleyerek LinkedIn satış Gezgini için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com). Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.


### <a name="tooconfigure-automatic-user-account-provisioning-toolinkedin-sales-navigator-in-azure-ad"></a>Azure AD'de tooLinkedIn satış Gezgini sağlama tooconfigure otomatik olarak bir kullanıcı hesabı:


Merhaba ilk adımı tooretrieve LinkedIn erişim belirteci değil. Bir kuruluş yöneticisi iseniz, bir erişim belirteci otomatik olarak sağlayabilirsiniz. Hesap Merkezinize çok Git**ayarları &gt; genel ayarları** ve açık hello **SCIM'yi Kurulum** paneli.

> [!NOTE]
> Merhaba hesap Merkezi'nde yerine doğrudan bir bağlantı aracılığıyla erişiyorsanız aşağıdaki adımları hello kullanarak ulaşabilirsiniz.

1)  TooAccount Merkezi'nde oturum açın.

2)  Seçin **yönetici &gt; yönetici ayarları** .

3)  Tıklatın **Gelişmiş tümleştirmeler** hello sol kenar üzerinde. Yönlendirilmiş toohello hesap Merkezi'nde var.

4)  Tıklatın **+ Ekle yeni SCIM'yi yapılandırma** ve her alanı doldurarak hello yordamı izleyin.

> Autoassign lisansları etkin değil, yalnızca kullanıcı verilerini eşitlenip anlamına gelir.

![LinkedIn satış Gezgini sağlama](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_1.PNG)

> Autolicense atama etkinleştirildiğinde, toonote uygulama örneği ve lisans türü gerekir. İlk gelen üzerinde atanmış lisansların, tüm hello lisansları duruma kadar temel ilk hizmet.

![LinkedIn satış Gezgini sağlama](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_2.PNG)

5)  Tıklatın **belirteç Oluştur**. Erişim belirteci ekranınıza hello altında görmelisiniz **erişim belirteci** alan.

6)  Erişim belirteci tooyour Pano veya bilgisayar hello sayfadan ayrılmadan önce kaydedin.

7) Ardından, toohello içinde oturum [Azure portal](https://portal.azure.com)ve toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölüm.

8) Çoklu oturum açma için zaten LinkedIn satış Gezgini yapılandırdıysanız, LinkedIn satış hello arama alanı kullanarak Gezgini Örneğiniz için arama yapın. Aksi takdirde seçin **Ekle** arayın ve **LinkedIn satış Gezgini** hello uygulama galerisinde. Merhaba Arama sonuçlarından LinkedIn satış Gezgini seçin ve uygulamaların tooyour listesine ekleyin.

9)  LinkedIn satış Gezgini örneğiniz seçin ve ardından hello **sağlama** sekmesi.

10) Set hello **sağlama modu** çok**otomatik**.

![LinkedIn satış Gezgini sağlama](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_3.PNG)

11)  Alanlar'ın altında aşağıdaki hello doldurun **yönetici kimlik bilgileri** :

* Merhaba, **Kiracı URL** alanında, https://api.linkedin.com girin.

* Merhaba, **gizli belirteci** alan, 1. adımda oluşturulan hello erişim belirtecini girin ve tıklatın **Bağlantıyı Sına** .

* Merhaba upperright tarafında portalınızı başarı bildirim görmeniz gerekir.

12) Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve aşağıdaki hello onay kutusunu işaretleyin.

13) **Kaydet** düğmesine tıklayın. 

14) Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooLinkedIn satış Gezgini eşitleneceğini hello kullanıcı ve grup öznitelikleri gözden geçirin. Seçilen öznitelikler hello Not **eşleşen** özellikler kullanılan toomatch hello kullanıcı hesapları ve grupları LinkedIn satış Gezgininde güncelleştirme işlemleri için olacaktır. Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.

![LinkedIn satış Gezgini sağlama](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_4.PNG)

15) tooenable hello LinkedIn satış Gezgini, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello içinde **ayarları** bölümü

16) **Kaydet** düğmesine tıklayın. 

Bu, herhangi bir kullanıcı ve/veya tooLinkedIn satış Gezgini hello kullanıcılar ve Gruplar bölümünde atanan gruplarını hello ilk eşitleme başlatır. Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform gerektiğine dikkat edin. Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve LinkedIn satış Gezgini uygulamanızdan hizmet sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.


## <a name="additional-resources"></a>Ek Kaynaklar

* [Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme](active-directory-enterprise-apps-manage-provisioning.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
