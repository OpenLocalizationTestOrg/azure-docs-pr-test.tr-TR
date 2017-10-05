---
title: Talep kullanan uygulamalar - Azure AD uygulama proxy'si | Microsoft Docs
description: "Kullanıcılarınız tarafından güvenli uzaktan erişim için ADFS talep kabul şirket içi ASP.NET uygulamaları yayımlamak nasıl."
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
ms.openlocfilehash: 5784222608b01509fc4ff84b1a8792cbcfea89e6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a><span data-ttu-id="ce51d-103">Talep kullanan uygulamalarda uygulama proxy'si ile çalışma</span><span class="sxs-lookup"><span data-stu-id="ce51d-103">Working with claims-aware apps in Application Proxy</span></span>
<span data-ttu-id="ce51d-104">[Talep kullanan uygulamalar](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) yeniden yönlendirmesi için güvenlik belirteci hizmeti (STS) gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="ce51d-104">[Claims-aware apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) perform a redirection to the Security Token Service (STS).</span></span> <span data-ttu-id="ce51d-105">STS bir belirteç karşılığında kullanıcı kimlik bilgilerini ister ve ardından kullanıcının uygulamaya yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="ce51d-105">The STS requests credentials from the user in exchange for a token and then redirects the user to the application.</span></span> <span data-ttu-id="ce51d-106">Bu yeniden yönlendirmeleri ile çalışmak uygulama proxy'si etkinleştirmek için birkaç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="ce51d-106">There are a few ways to enable Application Proxy to work with these redirects.</span></span> <span data-ttu-id="ce51d-107">Dağıtımınızı talep kullanan uygulamalar için yapılandırmak için bu makaleyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="ce51d-107">Use this article to configure your deployment for claims-aware apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ce51d-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ce51d-108">Prerequisites</span></span>
<span data-ttu-id="ce51d-109">Talep kullanan uygulama yönlendirir STS Şirket ağınızın dışında kullanılabilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ce51d-109">Make sure that the STS that the claims-aware app redirects to is available outside of your on-premises network.</span></span> <span data-ttu-id="ce51d-110">STS kullanılabilir bir proxy üzerinden gösterme ya da dış bağlantılara izin yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce51d-110">You can make the STS available by exposing it through a proxy or by allowing outside connections.</span></span> 

## <a name="publish-your-application"></a><span data-ttu-id="ce51d-111">Uygulamanızı yayımlama</span><span class="sxs-lookup"><span data-stu-id="ce51d-111">Publish your application</span></span>

1. <span data-ttu-id="ce51d-112">Uygulamanızı bölümünde açıklanan yönergeleri göre yayımlamak [uygulama proxy'si ile uygulama yayımlama](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ce51d-112">Publish your application according to the instructions described in [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>
2. <span data-ttu-id="ce51d-113">Seçin ve Portalı'nda uygulama sayfası gidin **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="ce51d-113">Navigate to the application page in the portal and select **Single sign-on**.</span></span>
3. <span data-ttu-id="ce51d-114">Seçerseniz **Azure Active Directory** olarak, **ön kimlik doğrulama yöntemi**seçin **Azure AD çoklu oturum açma devre dışı özelliğini** olarak, **iç Kimlik doğrulama yöntemini**.</span><span class="sxs-lookup"><span data-stu-id="ce51d-114">If you chose **Azure Active Directory** as your **Preauthentication Method**, select **Azure AD single sign-on disabled** as your **Internal Authentication Method**.</span></span> <span data-ttu-id="ce51d-115">Seçerseniz **geçiş** olarak, **ön kimlik doğrulama yöntemi**, değişikliği gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ce51d-115">If you chose **Passthrough** as your **Preauthentication Method**, you don't need to change anything.</span></span>

## <a name="configure-adfs"></a><span data-ttu-id="ce51d-116">ADFS yapılandırın</span><span class="sxs-lookup"><span data-stu-id="ce51d-116">Configure ADFS</span></span>

<span data-ttu-id="ce51d-117">İki yoldan biriyle talep kullanan uygulamalar için ADFS yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce51d-117">You can configure ADFS for claims-aware apps in one of two ways.</span></span> <span data-ttu-id="ce51d-118">İlk özel etki alanlarını kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="ce51d-118">The first is by using custom domains.</span></span> <span data-ttu-id="ce51d-119">WS-Federasyon ile saniyedir.</span><span class="sxs-lookup"><span data-stu-id="ce51d-119">The second is with WS-Federation.</span></span> 

### <a name="option-1-custom-domains"></a><span data-ttu-id="ce51d-120">Seçenek 1: Özel etki alanları</span><span class="sxs-lookup"><span data-stu-id="ce51d-120">Option 1: Custom domains</span></span>

<span data-ttu-id="ce51d-121">Tüm iç URL'leri uygulamalarınız için tam olarak nitelenmiş etki alanı adlarını (FQDN) sonra yapılandırabileceğiniz [özel etki alanlarını](active-directory-application-proxy-custom-domains.md) uygulamalarınız için.</span><span class="sxs-lookup"><span data-stu-id="ce51d-121">If all the internal URLs for your applications are fully qualified domain names (FQDNs), then you can configure [custom domains](active-directory-application-proxy-custom-domains.md) for your applications.</span></span> <span data-ttu-id="ce51d-122">Özel etki alanlarını iç URL'ler ile aynı olan dış URL'ler oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="ce51d-122">Use the custom domains to create external URLs that are the same as the internal URLs.</span></span> <span data-ttu-id="ce51d-123">Ardından, dış URL'ler iç URL'nizde eşleştiğinde, kullanıcılarınızın şirket içi veya uzak olup STS yeniden yönlendirme çalışır.</span><span class="sxs-lookup"><span data-stu-id="ce51d-123">When your external URLs match your internal URLs, then the STS redirections work whether your users are on-premises or remote.</span></span> 

### <a name="option-2-ws-federation"></a><span data-ttu-id="ce51d-124">Seçenek 2: WS-Federasyon</span><span class="sxs-lookup"><span data-stu-id="ce51d-124">Option 2: WS-Federation</span></span>

1. <span data-ttu-id="ce51d-125">ADFS Yönetimi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="ce51d-125">Open ADFS Management.</span></span>
2. <span data-ttu-id="ce51d-126">Git **bağlı olan taraf güvenleri**uygulama ara sunucusu ile yayımlıyorsa uygulama sağ tıklatın ve seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="ce51d-126">Go to **Relying Party Trusts**, right-click on the app you are publishing with Application Proxy, and choose **Properties**.</span></span>  

   ![Bağlı olan taraf güvenleri sağ uygulama adı - ekran görüntüsü](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. <span data-ttu-id="ce51d-128">Üzerinde **uç noktaları** sekmesinde, altında **uç nokta türü**seçin **WS-Federasyon**.</span><span class="sxs-lookup"><span data-stu-id="ce51d-128">On the **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.</span></span>
4. <span data-ttu-id="ce51d-129">Altında **güvenilen URL**, girdiğiniz uygulama proxy'si ile yapılandırılabilir.%nd;a;%nd;a;%nişlem URL'si girin **dış URL** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ce51d-129">Under **Trusted URL**, enter the URL you entered in the Application Proxy under **External URL** and click **OK**.</span></span>  

   ![Bir uç nokta - ekleyin güvenilen URL değeri - ekran görüntüsü Ayarla](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a><span data-ttu-id="ce51d-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ce51d-131">Next steps</span></span>
* <span data-ttu-id="ce51d-132">[Çoklu oturum açmayı etkinleştir](application-proxy-sso-overview.md) talep kullanan olmayan uygulamalar için</span><span class="sxs-lookup"><span data-stu-id="ce51d-132">[Enable single-sign on](application-proxy-sso-overview.md) for applications that aren't claims-aware</span></span>
* [<span data-ttu-id="ce51d-133">Proxy uygulamaları ile etkileşim kurmak yerel istemci uygulamaları etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="ce51d-133">Enable native client apps to interact with proxy applications</span></span>](active-directory-application-proxy-native-client.md)


