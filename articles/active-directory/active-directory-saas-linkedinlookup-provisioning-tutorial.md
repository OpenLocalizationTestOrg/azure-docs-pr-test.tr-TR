---
title: "Öğretici: Azure Active Directory ile otomatik kullanıcı sağlamayı LinkedIn arama yapılandırma | Microsoft Docs"
description: "Otomatik olarak sağlamak ve kullanıcı hesaplarına LinkedIn arama sağlanmasını için Azure Active Directory yapılandırmayı öğrenin."
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
ms.openlocfilehash: 085a68cfe8f9e08b8722e8613994ee300a015776
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-linkedin-lookup-for-automatic-user-provisioning"></a>Öğretici: LinkedIn arama otomatik kullanıcı sağlamayı için yapılandırma


Bu öğreticinin amacı LinkedIn arama ve Azure AD otomatik olarak sağlamak ve kullanıcı hesaplarına Azure AD'den LinkedIn arama sağlanmasını gerçekleştirmek için gereken adımları Göster sağlamaktır. 

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticide gösterilen senaryo, aşağıdaki öğeleri zaten sahip olduğunuzu varsayar:

*   Azure Active Directory kiracısı
*   Bir LinkedIn arama Kiracı 
*   Bir yönetici hesabıyla LinkedIn aramada LinkedIn hesap Merkezi erişim

> [!NOTE]
> Azure Active Directory LinkedIn kullanarak araması ile tümleşir [SCIM'yi](http://www.simplecloud.info/) protokolü.

## <a name="assigning-users-to-linkedin-lookup"></a>Kullanıcıları LinkedIn arama atama

Azure Active Directory "atamaları" adlı bir kavram hangi kullanıcıların seçili uygulamalara erişim alması belirlemek için kullanır. Otomatik olarak bir kullanıcı hesabı sağlama bağlamında, yalnızca kullanıcıların ve grupların "Azure AD uygulamada atanmış" eşitlenir. 

Yapılandırma ve sağlama hizmeti etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD grupları LinkedIn arama erişmesi gereken kullanıcıları temsil karar vermeniz gerekir. Karar sonra buradaki yönergeleri izleyerek, bu kullanıcılar LinkedIn arama atayabilirsiniz:

[Bir kullanıcı veya grup için bir kuruluş uygulama atama](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-linkedin-lookup"></a>LinkedIn arama kullanıcılara atamak için önemli ipuçları

*   Önerilir tek bir Azure AD kullanıcısının sağlama yapılandırmayı test etmek için LinkedIn arama atanabilir. Ek kullanıcı ve/veya grupları daha sonra atanabilir.

*   Bir kullanıcı için LinkedIn arama atarken seçmelisiniz **kullanıcı** rol ataması iletişim. "Varsayılan erişim" rolü sağlama için çalışmaz.


## <a name="configuring-user-provisioning-to-linkedin-lookup"></a>LinkedIn arama kullanıcı sağlamayı yapılandırma

Bu bölümde, Azure AD API sağlama LinkedIn aramanın SCIM'yi kullanıcı hesabına bağlanma yoluyla size rehberlik eder ve atanmış kullanıcı ve Grup atamasını LinkedIn arama hesaplarında göre kullanıcı oluşturmak, güncelleştirme ve devre dışı bırakmak için sağlama hizmeti yapılandırma Azure AD.

> [!TIP]
> Da tercih edebilirsiniz etkin SAML tabanlı çoklu oturum açma LinkedIn aramasını, yönergeleri izleyerek sağlanan [Azure portal](https://portal.azure.com). Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.


### <a name="to-configure-automatic-user-account-provisioning-to-linkedin-lookup-in-azure-ad"></a>Otomatik olarak bir kullanıcı hesabı LinkedIn arama için Azure AD'de sağlama yapılandırmak için:


LinkedIn erişim belirteci almak için ilk adımdır bakın. Bir kuruluş yöneticisi iseniz, bir erişim belirteci otomatik olarak sağlayabilirsiniz. Hesap Merkezinize gidin **ayarları &gt; genel ayarları** açarak **SCIM'yi Kurulum** paneli.

> [!NOTE]
> Hesap Merkezi'nde yerine doğrudan bir bağlantı aracılığıyla erişiyorsanız aşağıdaki adımları kullanarak ulaşabilirsiniz.

1)  Merkezi hesap için oturum açın.

2)  Seçin **yönetici &gt; yönetici ayarları** .

3)  Tıklatın **Gelişmiş tümleştirmeler** sol kenar çubuğunda. Hesap Merkezi'nde yönlendirilir.

4)  Tıklatın **+ Ekle yeni SCIM'yi yapılandırma** ve her alanı doldurarak yordamı izleyin.

> Autoassign lisansları etkin değil, yalnızca kullanıcı verilerini eşitlenip anlamına gelir.

![LinkedIn sağlama arama](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_1.PNG)

> Autolicense atama etkinleştirildiğinde, uygulama örneği ve lisans türü Not gerekir. İlk gelen üzerinde atanmış lisansların, tüm lisanslar duruma kadar temel ilk hizmet.

![LinkedIn sağlama arama](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_2.PNG)

5)  Tıklatın **belirteç Oluştur**. Erişim belirteci görüntü altında görmelisiniz **erişim belirteci** alan.

6)  Erişim belirteci sayfadan ayrılmadan önce Pano veya bilgisayara kaydedin.

7) Ardından, oturum [Azure portal](https://portal.azure.com)ve **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.

8) Çoklu oturum açma için zaten LinkedIn arama yapılandırdıysanız, LinkedIn arama alanı kullanarak araması Örneğiniz için arama yapın. Aksi takdirde seçin **Ekle** arayın ve **LinkedIn arama** uygulama galerisinde. Arama sonuçlarından LinkedIn arama seçin ve uygulamaları listenize ekleyin.

9)  LinkedIn arama örneğiniz seçin ve ardından **sağlama** sekmesi.

10) Ayarlama **sağlama modunda** için **otomatik**.

![LinkedIn sağlama arama](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_3.PNG)

11)  Altında aşağıdaki alanları doldurun **yönetici kimlik bilgileri** :

* İçinde **Kiracı URL** alanında, https://api.linkedin.com girin.

* İçinde **gizli belirteci** alan, 1. adımda oluşturulan erişim belirteci girin ve tıklayın **Bağlantıyı Sına** .

* Portalınızı upperright tarafında bir başarı bildirimi görmelisiniz.

12) Bir kişi veya sağlama hata bildirimleri alması gereken Grup e-posta adresini girin **bildirim e-posta** alan ve aşağıdaki onay kutusunu işaretleyin.

13) **Kaydet** düğmesine tıklayın. 

14) İçinde **öznitelik eşlemelerini** bölümünde, Azure AD'den LinkedIn arama eşitleneceğini kullanıcı ve grup öznitelikleri gözden geçirin. Seçilen öznitelikler olarak Not **eşleşen** özellikleri, kullanıcı hesapları ve grupları LinkedIn aramada güncelleştirme işlemleri için eşleştirmek için kullanılır. Değişiklikleri kaydetmek için Kaydet düğmesini seçin.

![LinkedIn sağlama arama](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_4.PNG)

15) Azure AD hizmeti LinkedIn arama için sağlama etkinleştirmek için değiştirmek **sağlama durumu** için **üzerinde** içinde **ayarları** bölümü

16) **Kaydet** düğmesine tıklayın. 

Bu, herhangi bir kullanıcı ve/veya grupları kullanıcıları ve grupları bölümünde LinkedIn arama atanan ilk eşitleme başlatır. İlk eşitlemeyi gerçekleştirmek için yaklaşık 20 dakikada çalıştığı sürece oluşan sonraki eşitlemeler uzun sürer unutmayın. Kullanabileceğiniz **eşitleme ayrıntıları** bölüm ilerlemeyi izlemek ve LinkedIn arama uygulamanızı sağlama hizmeti tarafından gerçekleştirilen tüm eylemler açıklanmaktadır etkinlik raporları sağlamak için bağlantıları izleyin.


## <a name="additional-resources"></a>Ek Kaynaklar

* [Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme](active-directory-enterprise-apps-manage-provisioning.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
