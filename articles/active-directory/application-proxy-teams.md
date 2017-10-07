---
title: "aaaAccess takımlar Azure AD uygulaması Proxy uygulamalarında | Microsoft Docs"
description: "Şirket içi uygulamanızı Microsoft Teams aracılığıyla Azure AD uygulama proxy'si tooaccess kullanın."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 13c36e43ae6349df09272e308ad4f40451cbbeb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a>Şirket içi uygulamalarınızı Microsoft Teams erişme

Azure Active Directory Uygulama proxy'si, tek oturum açma tooon içi uygulamalar, nerede olursa olsun sağlar ve Microsoft Teams işbirliği çabalarınız tek bir yerde kolaylaştırır. Merhaba tümleştirme iki birlikte, kullanıcılarınızın kendi Ekip arkadaşları hiçbir durumda ile üretken olabileceği anlamına gelir. 

Kullanıcılarınızın bulut uygulamaları tootheir takımlar kanalları ekleyebilirsiniz [sekmeleri kullanarak](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), ancak şirket içi barındırılan bu SharePoint sitesi veya tüm kullandıkları planlama aracı ne olur? Uygulama proxy'si hello çözümüdür. Uygulamalar ekleyebilirsiniz uygulama proxy'si tootheir yayımlanan kanalları kullanarak her zaman kullandıkları tooaccess uygulamalarını uzaktan aynı dış URL'ler hello. Ve uygulama proxy'si Azure Active Directory kimlik doğrulaması için çoklu oturum açma deneyimini aynı taşıyan aracılığıyla hello.


## <a name="install-hello-application-proxy-connector-and-publish-your-app"></a>Merhaba uygulama ara sunucusu Bağlayıcısı yükleme ve uygulamanızı yayınlama

Henüz yapmadıysanız [hello bağlayıcı yükleyip kiracınız için uygulama proxy'si yapılandırmanıza](active-directory-application-proxy-enable.md). Ardından, [şirket içi uygulamanızı yayımlamak](application-proxy-publish-azure-portal.md) uzaktan erişim için. Merhaba uygulama yayımlarken hello uygulama tooTeams eklediğinizde, son kullanıcılarınız bu bilgileri gerektiğinden hello dış URL not edin.

Zaten varsa yayımlanan uygulamalarınızı ancak bunların dış URL'ler hatırlama bunları hello aramak [Azure portal](https://portal.azure.com). Oturum açın, sonra çok gidin**Azure Active Directory** > **kurumsal uygulamalar** > **tüm uygulamaları** > uygulamanızı seçin > **Uygulama proxy'si**.

## <a name="add-your-app-tooteams"></a>Uygulama tooTeams Ekle

Uygulama proxy'si aracılığıyla hello uygulama yayımladıktan sonra bunlar, bir sekmede doğrudan kendi takımlar kanalları olarak ekleyebileceğinizi biliyor kullanıcılarınızın olanak tanır. Bunları aşağıdaki üç adımı izleyin vardır:

1. Takımlar tooadd istediğiniz bu uygulamanın kanal ve seçin toohello gidin  **+**  tooadd sekme.

   ![Sekme Ekle seçin](./media/application-proxy-teams/add-tab.png)

2. Seçin **Web sitesi** hello sekmesi seçenekleri.

   ![Web sitesi ekleme](./media/application-proxy-teams/website.png)

3. Merhaba sekmesinde bir ad verin ve hello toohello uygulama proxy'si dış URL'si ayarlayın. 

   ![Sekme adı ve URL yapılandırın](./media/application-proxy-teams/tab-name-url.png)

Bir ekibin üyesi hello sekmesi ekler sonra herkesin hello kanal görüntülersiniz. Access toohello uygulaması olan tüm kullanıcıların tek oturum açma Microsoft Teams için kullandıkları hello kimlik bilgileriyle erişin. Sahip erişim toohello uygulaması olmayan kullanıcılardan takımlar hello sekmesinde görürsünüz, ancak izinleri toohello şirket içi uygulama verin ve Azure portal yayımlanmış sürümü hello uygulama hello kadar engellenir. 

## <a name="next-steps"></a>Sonraki adımlar

- Nasıl çok öğrenin[şirket içi SharePoint siteleri yayımlamak](application-proxy-enable-remote-access-sharepoint.md) uygulama proxy'si ile uygulama.
- Uygulamaları toouse yapılandırma [özel etki alanlarını](active-directory-application-proxy-custom-domains.md) kendi dış URL. 
