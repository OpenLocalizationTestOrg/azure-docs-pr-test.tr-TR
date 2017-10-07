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
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a><span data-ttu-id="72b07-103">Şirket içi uygulamalarınızı Microsoft Teams erişme</span><span class="sxs-lookup"><span data-stu-id="72b07-103">Access your on-premises applications through Microsoft Teams</span></span>

<span data-ttu-id="72b07-104">Azure Active Directory Uygulama proxy'si, tek oturum açma tooon içi uygulamalar, nerede olursa olsun sağlar ve Microsoft Teams işbirliği çabalarınız tek bir yerde kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="72b07-104">Azure Active Directory Application Proxy gives you single sign-on tooon-premises applications no matter where you are, and Microsoft Teams streamlines your collaborative efforts in one place.</span></span> <span data-ttu-id="72b07-105">Merhaba tümleştirme iki birlikte, kullanıcılarınızın kendi Ekip arkadaşları hiçbir durumda ile üretken olabileceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="72b07-105">Integrating hello two together means that your users can be productive with their teammates in any situation.</span></span> 

<span data-ttu-id="72b07-106">Kullanıcılarınızın bulut uygulamaları tootheir takımlar kanalları ekleyebilirsiniz [sekmeleri kullanarak](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), ancak şirket içi barındırılan bu SharePoint sitesi veya tüm kullandıkları planlama aracı ne olur?</span><span class="sxs-lookup"><span data-stu-id="72b07-106">Your users can add cloud apps tootheir Teams channels [using tabs](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), but what happens if that SharePoint site or planning tool they all use is hosted on-premises?</span></span> <span data-ttu-id="72b07-107">Uygulama proxy'si hello çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="72b07-107">Application Proxy is hello solution.</span></span> <span data-ttu-id="72b07-108">Uygulamalar ekleyebilirsiniz uygulama proxy'si tootheir yayımlanan kanalları kullanarak her zaman kullandıkları tooaccess uygulamalarını uzaktan aynı dış URL'ler hello.</span><span class="sxs-lookup"><span data-stu-id="72b07-108">They can add apps published through Application Proxy tootheir channels using hello same external URLs they always use tooaccess their apps remotely.</span></span> <span data-ttu-id="72b07-109">Ve uygulama proxy'si Azure Active Directory kimlik doğrulaması için çoklu oturum açma deneyimini aynı taşıyan aracılığıyla hello.</span><span class="sxs-lookup"><span data-stu-id="72b07-109">And because Application Proxy authenticates through Azure Active Directory, hello same single sign-on experience carries through.</span></span>


## <a name="install-hello-application-proxy-connector-and-publish-your-app"></a><span data-ttu-id="72b07-110">Merhaba uygulama ara sunucusu Bağlayıcısı yükleme ve uygulamanızı yayınlama</span><span class="sxs-lookup"><span data-stu-id="72b07-110">Install hello Application Proxy connector and publish your app</span></span>

<span data-ttu-id="72b07-111">Henüz yapmadıysanız [hello bağlayıcı yükleyip kiracınız için uygulama proxy'si yapılandırmanıza](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="72b07-111">If you haven't already, [configure Application Proxy for your tenant and install hello connector](active-directory-application-proxy-enable.md).</span></span> <span data-ttu-id="72b07-112">Ardından, [şirket içi uygulamanızı yayımlamak](application-proxy-publish-azure-portal.md) uzaktan erişim için.</span><span class="sxs-lookup"><span data-stu-id="72b07-112">Then, [publish your on-premises application](application-proxy-publish-azure-portal.md) for remote access.</span></span> <span data-ttu-id="72b07-113">Merhaba uygulama yayımlarken hello uygulama tooTeams eklediğinizde, son kullanıcılarınız bu bilgileri gerektiğinden hello dış URL not edin.</span><span class="sxs-lookup"><span data-stu-id="72b07-113">When you're publishing hello app, make note of hello external URL because your end users need that information when they add hello app tooTeams.</span></span>

<span data-ttu-id="72b07-114">Zaten varsa yayımlanan uygulamalarınızı ancak bunların dış URL'ler hatırlama bunları hello aramak [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="72b07-114">If you already have your apps published but don't remember their external URLs, look them up in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="72b07-115">Oturum açın, sonra çok gidin**Azure Active Directory** > **kurumsal uygulamalar** > **tüm uygulamaları** > uygulamanızı seçin > **Uygulama proxy'si**.</span><span class="sxs-lookup"><span data-stu-id="72b07-115">Sign in, then navigate too**Azure Active Directory** > **Enterprise applications** > **All applications** > select your app > **Application proxy**.</span></span>

## <a name="add-your-app-tooteams"></a><span data-ttu-id="72b07-116">Uygulama tooTeams Ekle</span><span class="sxs-lookup"><span data-stu-id="72b07-116">Add your app tooTeams</span></span>

<span data-ttu-id="72b07-117">Uygulama proxy'si aracılığıyla hello uygulama yayımladıktan sonra bunlar, bir sekmede doğrudan kendi takımlar kanalları olarak ekleyebileceğinizi biliyor kullanıcılarınızın olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="72b07-117">Once you publish hello app through Application Proxy, let your users know that they can add it as a tab directly in their Teams channels.</span></span> <span data-ttu-id="72b07-118">Bunları aşağıdaki üç adımı izleyin vardır:</span><span class="sxs-lookup"><span data-stu-id="72b07-118">Have them follow these three steps:</span></span>

1. <span data-ttu-id="72b07-119">Takımlar tooadd istediğiniz bu uygulamanın kanal ve seçin toohello gidin  **+**  tooadd sekme.</span><span class="sxs-lookup"><span data-stu-id="72b07-119">Navigate toohello Teams channel where you want tooadd this app and select **+** tooadd a tab.</span></span>

   ![Sekme Ekle seçin](./media/application-proxy-teams/add-tab.png)

2. <span data-ttu-id="72b07-121">Seçin **Web sitesi** hello sekmesi seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="72b07-121">Select **Website** from hello tab options.</span></span>

   ![Web sitesi ekleme](./media/application-proxy-teams/website.png)

3. <span data-ttu-id="72b07-123">Merhaba sekmesinde bir ad verin ve hello toohello uygulama proxy'si dış URL'si ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="72b07-123">Give hello tab a name and set hello URL toohello Application Proxy external URL.</span></span> 

   ![Sekme adı ve URL yapılandırın](./media/application-proxy-teams/tab-name-url.png)

<span data-ttu-id="72b07-125">Bir ekibin üyesi hello sekmesi ekler sonra herkesin hello kanal görüntülersiniz.</span><span class="sxs-lookup"><span data-stu-id="72b07-125">Once one member of a team adds hello tab, it shows up for everyone in hello channel.</span></span> <span data-ttu-id="72b07-126">Access toohello uygulaması olan tüm kullanıcıların tek oturum açma Microsoft Teams için kullandıkları hello kimlik bilgileriyle erişin.</span><span class="sxs-lookup"><span data-stu-id="72b07-126">Any users who have access toohello app get single sign-on access with hello credentials they use for Microsoft Teams.</span></span> <span data-ttu-id="72b07-127">Sahip erişim toohello uygulaması olmayan kullanıcılardan takımlar hello sekmesinde görürsünüz, ancak izinleri toohello şirket içi uygulama verin ve Azure portal yayımlanmış sürümü hello uygulama hello kadar engellenir.</span><span class="sxs-lookup"><span data-stu-id="72b07-127">Any users who don't have access toohello app will see hello tab in Teams, but are blocked until you give them permissions toohello on-premises app and hello Azure portal published version of hello app.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="72b07-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="72b07-128">Next steps</span></span>

- <span data-ttu-id="72b07-129">Nasıl çok öğrenin[şirket içi SharePoint siteleri yayımlamak](application-proxy-enable-remote-access-sharepoint.md) uygulama proxy'si ile uygulama.</span><span class="sxs-lookup"><span data-stu-id="72b07-129">Learn how too[publish on-premises SharePoint sites](application-proxy-enable-remote-access-sharepoint.md) with Application Proxy.</span></span>
- <span data-ttu-id="72b07-130">Uygulamaları toouse yapılandırma [özel etki alanlarını](active-directory-application-proxy-custom-domains.md) kendi dış URL.</span><span class="sxs-lookup"><span data-stu-id="72b07-130">Configure your apps toouse [custom domains](active-directory-application-proxy-custom-domains.md) for their external URL.</span></span> 
