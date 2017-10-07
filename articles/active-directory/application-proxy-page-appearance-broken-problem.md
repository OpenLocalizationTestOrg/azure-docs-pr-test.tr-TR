---
title: "aaaApplication sayfası için uygulama proxy'si uygulama doğru görüntülemiyor | Microsoft Docs"
description: "Azure AD ile tümleşik Hello sayfa doğru bir uygulama Proxy uygulamada değil görüntülenirken Kılavuzu"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: f4abaa4e94c512868f2085affe59cac443784a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a><span data-ttu-id="ca8cc-103">Uygulama sayfası için uygulama proxy'si uygulama düzgün görüntülenmez</span><span class="sxs-lookup"><span data-stu-id="ca8cc-103">Application page does not display correctly for an Application Proxy application</span></span>

<span data-ttu-id="ca8cc-104">Bu makale yardımcı, Azure Active Directory Uygulama proxy'si uygulamalarıyla tootroubleshoot sorunları toohello sayfasına gidin, ancak başlangıç sayfasında bir şey doğru görünmüyor.</span><span class="sxs-lookup"><span data-stu-id="ca8cc-104">This article help you tootroubleshoot issues with Azure Active Directory Application Proxy applications when you navigate toohello page, but something on hello page doesn't look correct.</span></span>

## <a name="overview"></a><span data-ttu-id="ca8cc-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ca8cc-105">Overview</span></span>
<span data-ttu-id="ca8cc-106">Bir uygulama proxy'si uygulama yayımladığınızda, yalnızca, kök altındaki sayfalar Merhaba uygulaması erişirken erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="ca8cc-106">When you publish an Application Proxy app, only pages under your root are accessible when accessing hello application.</span></span> <span data-ttu-id="ca8cc-107">Merhaba sayfa doğru görüntülemiyorsa hello kök İç URL hello uygulama için kullanılan bazı sayfası kaynakları eksik olabilir.</span><span class="sxs-lookup"><span data-stu-id="ca8cc-107">If hello page isn’t displaying correctly, hello root internal URL used for hello application may be missing some page resources.</span></span> <span data-ttu-id="ca8cc-108">tooresolve, yayımlanan emin olun *tüm* hello hello sayfa için kaynaklar, uygulamanızın bir parçası olarak.</span><span class="sxs-lookup"><span data-stu-id="ca8cc-108">tooresolve, make sure you have published *all* hello resources for hello page as part of your application.</span></span>

<span data-ttu-id="ca8cc-109">Bu durum, hello sorunundan Ağ İzleyicisi'ni açarak doğrulayabilirsiniz (Fiddler veya F12 gibi araçlar Internet Explorer/kenar) hello sayfa yüklenirken ve 404 hatalarını aranıyor.</span><span class="sxs-lookup"><span data-stu-id="ca8cc-109">You can verify this is hello issue by opening your network tracker (such as Fiddler, or F12 tools in Internet Explorer/Edge), loading hello page, and looking for 404 errors.</span></span> <span data-ttu-id="ca8cc-110">Bu, şu anda bulunamıyor ve yayımlanan toobe hala gerekebilir hello sayfaları gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca8cc-110">That indicates hello pages that currently cannot be found and may still need toobe published.</span></span>

<span data-ttu-id="ca8cc-111">Bu durumda bir örnek olarak, bir iç URL'sini kullanarak giderleri uygulama yayımlandı varsayalım <http://myapps/expenses>, ancak hello uygulamanın kullandığı hello stil <http://myapps/style.css>.</span><span class="sxs-lookup"><span data-stu-id="ca8cc-111">As an example of this case, assume you have published an expenses application using an internal URL of <http://myapps/expenses>, but hello app uses hello stylesheet <http://myapps/style.css>.</span></span> <span data-ttu-id="ca8cc-112">Bu durumda, Hello giderleri uygulama yüklenirken throw şekilde çalışırken tooload style.css 404 hatası hello stil sayfası, uygulamanızda yayınlanmadı.</span><span class="sxs-lookup"><span data-stu-id="ca8cc-112">In this case, hello stylesheet is not published in your application, so loading hello expenses app throw a 404 error while trying tooload style.css.</span></span> <span data-ttu-id="ca8cc-113">Bu örnekte, hello sorunun bir iç URL'si ile Merhaba uygulaması yayımlama tarafından çözülmüş <http://myapp/> yerine.</span><span class="sxs-lookup"><span data-stu-id="ca8cc-113">In this example, hello problem would be resolved by publishing hello application with an internal URL of <http://myapp/> instead.</span></span>

## <a name="problems-with-publishing-as-one-application"></a><span data-ttu-id="ca8cc-114">Bir uygulama yayımlama sorunları</span><span class="sxs-lookup"><span data-stu-id="ca8cc-114">Problems with publishing as one application</span></span>

<span data-ttu-id="ca8cc-115">Olası toopublish değilse içindeki tüm kaynakların aynı uygulama Merhaba, aralarında bağlantıları etkinleştirmek ve birden çok uygulama toopublish gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca8cc-115">If it is not possible toopublish all resources within hello same application, you need toopublish multiple applications and enable links between them.</span></span>

<span data-ttu-id="ca8cc-116">toodo bu nedenle, hello kullanmanızı öneririz [özel etki alanlarını](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) çözümü.</span><span class="sxs-lookup"><span data-stu-id="ca8cc-116">toodo so, we recommend using hello [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution.</span></span> <span data-ttu-id="ca8cc-117">Ancak, bu çözüm hello sertifika etki alanınız için sahip olduğunuz ve uygulamalarınızı tam etki alanı adlarını (FQDN) kullanmak gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ca8cc-117">However, this solution requires that you own hello certificate for your domain and your applications use fully qualified domain names (FQDNs).</span></span> <span data-ttu-id="ca8cc-118">Diğer seçenekler için bkz: Merhaba [bağlantıların belgelerine sorun giderme](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span><span class="sxs-lookup"><span data-stu-id="ca8cc-118">For other options, see hello [troubleshoot broken links documentation](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca8cc-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ca8cc-119">Next steps</span></span>
[<span data-ttu-id="ca8cc-120">Azure AD uygulama proxy'si ile uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="ca8cc-120">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
