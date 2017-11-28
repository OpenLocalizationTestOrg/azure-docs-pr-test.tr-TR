---
title: "aaaClaims algılayan uygulamaları - Azure AD uygulaması Proxy | Microsoft Docs"
description: "Nasıl toopublish kullanıcılarınız tarafından güvenli uzaktan erişim için ADFS talep kabul ASP.NET uygulamalarının şirket içi."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7be633225de700226c7c94815eb91b3de2b61cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a><span data-ttu-id="bb810-103">Talep kullanan uygulamalarda uygulama proxy'si ile çalışma</span><span class="sxs-lookup"><span data-stu-id="bb810-103">Working with claims-aware apps in Application Proxy</span></span>
<span data-ttu-id="bb810-104">[Talep kullanan uygulamalar](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) yeniden yönlendirme toohello güvenlik belirteci hizmeti (STS) gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="bb810-104">[Claims-aware apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) perform a redirection toohello Security Token Service (STS).</span></span> <span data-ttu-id="bb810-105">Hello STS bir belirteç karşılığında hello kullanıcıdan kimlik bilgilerini ister ve ardından hello kullanıcı toohello uygulaması yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="bb810-105">hello STS requests credentials from hello user in exchange for a token and then redirects hello user toohello application.</span></span> <span data-ttu-id="bb810-106">Bu yeniden yönlendirmeleri ile birkaç yolu tooenable uygulama proxy'si toowork vardır.</span><span class="sxs-lookup"><span data-stu-id="bb810-106">There are a few ways tooenable Application Proxy toowork with these redirects.</span></span> <span data-ttu-id="bb810-107">Bu makale tooconfigure dağıtımınızı talep kullanan uygulamalar için kullanın.</span><span class="sxs-lookup"><span data-stu-id="bb810-107">Use this article tooconfigure your deployment for claims-aware apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bb810-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bb810-108">Prerequisites</span></span>
<span data-ttu-id="bb810-109">Talep kullanan uygulama hello bu hello STS toois Şirket ağınızın dışında kullanılabilir yönlendiren emin olun.</span><span class="sxs-lookup"><span data-stu-id="bb810-109">Make sure that hello STS that hello claims-aware app redirects toois available outside of your on-premises network.</span></span> <span data-ttu-id="bb810-110">Hello STS kullanılabilir bir proxy üzerinden gösterme veya dışında bağlantılarına izin veren yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb810-110">You can make hello STS available by exposing it through a proxy or by allowing outside connections.</span></span> 

## <a name="publish-your-application"></a><span data-ttu-id="bb810-111">Uygulamanızı yayımlama</span><span class="sxs-lookup"><span data-stu-id="bb810-111">Publish your application</span></span>

1. <span data-ttu-id="bb810-112">Açıklanan toohello yönergeleri göre uygulamanızı yayımlamak [uygulama proxy'si ile uygulama yayımlama](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bb810-112">Publish your application according toohello instructions described in [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>
2. <span data-ttu-id="bb810-113">Merhaba seçin ve Portalı'nda uygulama sayfası toohello gidin **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="bb810-113">Navigate toohello application page in hello portal and select **Single sign-on**.</span></span>
3. <span data-ttu-id="bb810-114">Seçerseniz **Azure Active Directory** olarak, **ön kimlik doğrulama yöntemi**seçin **Azure AD çoklu oturum açma devre dışı özelliğini** olarak, **iç Kimlik doğrulama yöntemini**.</span><span class="sxs-lookup"><span data-stu-id="bb810-114">If you chose **Azure Active Directory** as your **Preauthentication Method**, select **Azure AD single sign-on disabled** as your **Internal Authentication Method**.</span></span> <span data-ttu-id="bb810-115">Seçerseniz **geçiş** olarak, **ön kimlik doğrulama yöntemi**, toochange herhangi bir şey gerekmez.</span><span class="sxs-lookup"><span data-stu-id="bb810-115">If you chose **Passthrough** as your **Preauthentication Method**, you don't need toochange anything.</span></span>

## <a name="configure-adfs"></a><span data-ttu-id="bb810-116">ADFS yapılandırın</span><span class="sxs-lookup"><span data-stu-id="bb810-116">Configure ADFS</span></span>

<span data-ttu-id="bb810-117">İki yoldan biriyle talep kullanan uygulamalar için ADFS yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb810-117">You can configure ADFS for claims-aware apps in one of two ways.</span></span> <span data-ttu-id="bb810-118">Merhaba, özel etki alanlarını kullanarak önce gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="bb810-118">hello first is by using custom domains.</span></span> <span data-ttu-id="bb810-119">Merhaba, WS-Federasyon ile ikinci olur.</span><span class="sxs-lookup"><span data-stu-id="bb810-119">hello second is with WS-Federation.</span></span> 

### <a name="option-1-custom-domains"></a><span data-ttu-id="bb810-120">Seçenek 1: Özel etki alanları</span><span class="sxs-lookup"><span data-stu-id="bb810-120">Option 1: Custom domains</span></span>

<span data-ttu-id="bb810-121">Uygulamalarınızı tam için tüm dahili URL Merhaba, etki alanı adları (FQDN), sonra yapılandırabileceğiniz [özel etki alanlarını](active-directory-application-proxy-custom-domains.md) uygulamalarınız için.</span><span class="sxs-lookup"><span data-stu-id="bb810-121">If all hello internal URLs for your applications are fully qualified domain names (FQDNs), then you can configure [custom domains](active-directory-application-proxy-custom-domains.md) for your applications.</span></span> <span data-ttu-id="bb810-122">İç URL'leri hello aynı hello kullan hello özel etki alanlarını toocreate harici URL.</span><span class="sxs-lookup"><span data-stu-id="bb810-122">Use hello custom domains toocreate external URLs that are hello same as hello internal URLs.</span></span> <span data-ttu-id="bb810-123">Ardından, dış URL'ler iç URL'nizde eşleştiğinde, kullanıcılarınızın şirket içi veya uzak olup hello STS yeniden yönlendirme çalışır.</span><span class="sxs-lookup"><span data-stu-id="bb810-123">When your external URLs match your internal URLs, then hello STS redirections work whether your users are on-premises or remote.</span></span> 

### <a name="option-2-ws-federation"></a><span data-ttu-id="bb810-124">Seçenek 2: WS-Federasyon</span><span class="sxs-lookup"><span data-stu-id="bb810-124">Option 2: WS-Federation</span></span>

1. <span data-ttu-id="bb810-125">ADFS Yönetimi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="bb810-125">Open ADFS Management.</span></span>
2. <span data-ttu-id="bb810-126">Çok Git**bağlı olan taraf güvenleri**uygulama ara sunucusu ile yayımlıyorsa hello uygulama sağ tıklatın ve seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="bb810-126">Go too**Relying Party Trusts**, right-click on hello app you are publishing with Application Proxy, and choose **Properties**.</span></span>  

   ![Bağlı olan taraf güvenleri sağ uygulama adı - ekran görüntüsü](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. <span data-ttu-id="bb810-128">Merhaba üzerinde **uç noktaları** sekmesinde, altında **uç nokta türü**seçin **WS-Federasyon**.</span><span class="sxs-lookup"><span data-stu-id="bb810-128">On hello **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.</span></span>
4. <span data-ttu-id="bb810-129">Altında **güvenilen URL**, uygulama proxy'si altında hello girilen hello URL'sini girin **dış URL** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="bb810-129">Under **Trusted URL**, enter hello URL you entered in hello Application Proxy under **External URL** and click **OK**.</span></span>  

   ![Bir uç nokta - ekleyin güvenilen URL değeri - ekran görüntüsü Ayarla](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a><span data-ttu-id="bb810-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bb810-131">Next steps</span></span>
* <span data-ttu-id="bb810-132">[Çoklu oturum açmayı etkinleştir](application-proxy-sso-overview.md) talep kullanan olmayan uygulamalar için</span><span class="sxs-lookup"><span data-stu-id="bb810-132">[Enable single-sign on](application-proxy-sso-overview.md) for applications that aren't claims-aware</span></span>
* [<span data-ttu-id="bb810-133">Yerel istemci uygulamaları toointeract proxy uygulamalarla etkinleştir</span><span class="sxs-lookup"><span data-stu-id="bb810-133">Enable native client apps toointeract with proxy applications</span></span>](active-directory-application-proxy-native-client.md)


