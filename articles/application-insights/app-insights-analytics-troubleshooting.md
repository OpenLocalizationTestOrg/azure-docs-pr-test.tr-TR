---
title: Azure Application Insights analizleri aaaTroubleshoot | Microsoft Docs
description: "Application Insights analytics sorunları? Buradan başlayın. "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9bbd5859-3584-4d80-9b6d-d5910fa48baa
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/11/2016
ms.author: bwren
ms.openlocfilehash: e3be2fbc0237440d3b8a736484434a9f276296c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a><span data-ttu-id="a3a30-104">Application Insights Analiz Sorunlarını Giderme</span><span class="sxs-lookup"><span data-stu-id="a3a30-104">Troubleshoot Analytics in Application Insights</span></span>
<span data-ttu-id="a3a30-105">Sorun [uygulama Öngörüler Analytics](app-insights-analytics.md)?</span><span class="sxs-lookup"><span data-stu-id="a3a30-105">Problems with [Application Insights Analytics](app-insights-analytics.md)?</span></span> <span data-ttu-id="a3a30-106">Buradan başlayın.</span><span class="sxs-lookup"><span data-stu-id="a3a30-106">Start here.</span></span> <span data-ttu-id="a3a30-107">Analytics hello güçlü arama Azure Application Insights, aracıdır.</span><span class="sxs-lookup"><span data-stu-id="a3a30-107">Analytics is hello powerful search tool of Azure Application Insights.</span></span>

## <a name="limits"></a><span data-ttu-id="a3a30-108">Sınırlar</span><span class="sxs-lookup"><span data-stu-id="a3a30-108">Limits</span></span>
* <span data-ttu-id="a3a30-109">Şu anda, sorgu sonuçları haftanın son verilerini sınırlı toojust olur.</span><span class="sxs-lookup"><span data-stu-id="a3a30-109">At present, query results are limited toojust over a week of past data.</span></span>
* <span data-ttu-id="a3a30-110">Biz test tarayıcılar: Chrome, sınır ve Internet Explorer'ın en son sürümleri.</span><span class="sxs-lookup"><span data-stu-id="a3a30-110">Browsers we test on: latest editions of Chrome, Edge, and Internet Explorer.</span></span>

## <a name="known-incompatible-browser-extensions"></a><span data-ttu-id="a3a30-111">Bilinen uyumlu tarayıcı uzantıları</span><span class="sxs-lookup"><span data-stu-id="a3a30-111">Known incompatible browser extensions</span></span>
* <span data-ttu-id="a3a30-112">Ghostery</span><span class="sxs-lookup"><span data-stu-id="a3a30-112">Ghostery</span></span>

<span data-ttu-id="a3a30-113">Merhaba uzantıyı devre dışı bırakmak veya farklı bir tarayıcı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a3a30-113">Disable hello extension or use a different browser.</span></span>

## <span data-ttu-id="a3a30-114"><a name="e-a"></a>"Beklenmeyen hata"</span><span class="sxs-lookup"><span data-stu-id="a3a30-114"><a name="e-a"></a> "Unexpected error"</span></span>
![Beklenmeyen hata ekranı](./media/app-insights-analytics-troubleshooting/010.png)

<span data-ttu-id="a3a30-116">İç hata portal çalışma zamanı sırasında – işlenmeyen bir özel durum oluştu.</span><span class="sxs-lookup"><span data-stu-id="a3a30-116">Internal error occurred during portal runtime – unhandled exception.</span></span>

* <span data-ttu-id="a3a30-117">Merhaba tarayıcının önbelleğini temizlemek.</span><span class="sxs-lookup"><span data-stu-id="a3a30-117">Clean hello browser's cache.</span></span> 

## <span data-ttu-id="a3a30-118"><a name="e-b"></a>403... Lütfen tooreload deneyin</span><span class="sxs-lookup"><span data-stu-id="a3a30-118"><a name="e-b"></a>403 ... please try tooreload</span></span>
![403... Lütfen tooreload deneyin](./media/app-insights-analytics-troubleshooting/020.png)

<span data-ttu-id="a3a30-120">Bir kimlik doğrulaması ile ilgili (kimlik doğrulaması veya erişim belirteci oluşturma sırasında) hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="a3a30-120">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="a3a30-121">Merhaba portal çok tarayıcı ayarları değiştirmeden kurtarma yolu yoktur.</span><span class="sxs-lookup"><span data-stu-id="a3a30-121">hello portal may have no way too recover without changing browser settings.</span></span>

* <span data-ttu-id="a3a30-122">Doğrulama [üçüncü taraf tanımlama bilgilerini etkin](#cookies) hello tarayıcıda.</span><span class="sxs-lookup"><span data-stu-id="a3a30-122">Verify [third party cookies are enabled](#cookies) in hello browser.</span></span> 

## <span data-ttu-id="a3a30-123"><a name="authentication"></a>403... güvenlik bölgesi doğrulayın</span><span class="sxs-lookup"><span data-stu-id="a3a30-123"><a name="authentication"></a>403 ... verify security zone</span></span>
![403.. .verify güvenlik bölgesi](./media/app-insights-analytics-troubleshooting/030.png)

<span data-ttu-id="a3a30-125">Bir kimlik doğrulaması ile ilgili (kimlik doğrulaması veya erişim belirteci oluşturma sırasında) hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="a3a30-125">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="a3a30-126">Merhaba portal çok tarayıcı ayarları değiştirmeden kurtarma yolu yoktur.</span><span class="sxs-lookup"><span data-stu-id="a3a30-126">hello portal may have no way too recover without changing browser settings.</span></span>

1. <span data-ttu-id="a3a30-127">Doğrulama [üçüncü taraf tanımlama bilgilerini etkin](#cookies) hello tarayıcıda.</span><span class="sxs-lookup"><span data-stu-id="a3a30-127">Verify [third party cookies are enabled](#cookies) in hello browser.</span></span> 
2. <span data-ttu-id="a3a30-128">Sık kullanılan, yer işareti veya kaydedilen bağlantı tooopen hello Analytics portalı kullandınız mı?</span><span class="sxs-lookup"><span data-stu-id="a3a30-128">Did you use a favorite, bookmark or saved link tooopen hello Analytics portal?</span></span> <span data-ttu-id="a3a30-129">Merhaba bağlantı kaydedildiğinde kullandığınızdan farklı kimlik ile oturum açtığınızı?</span><span class="sxs-lookup"><span data-stu-id="a3a30-129">Are you signed in with different credentials than you used when you saved hello link?</span></span>
3. <span data-ttu-id="a3a30-130">(Tüm pencereleri kapattıktan sonra) içinde-özel/ıncognito tarayıcı penceresi kullanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="a3a30-130">Try using an in-private/incognito browser window (after closing all such windows).</span></span> <span data-ttu-id="a3a30-131">Kimlik bilgilerinizi tooprovide sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="a3a30-131">You'll have tooprovide your credentials.</span></span> 
4. <span data-ttu-id="a3a30-132">Başka bir (normal) tarayıcı penceresi açın ve çok gidin[Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a3a30-132">Open another (ordinary) browser window and go too[Azure](https://portal.azure.com).</span></span> <span data-ttu-id="a3a30-133">Oturumu kapatın. Bağlantı açabilir ve hello doğru kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a3a30-133">Sign out. Then open your link and sign in with hello correct credentials.</span></span>
5. <span data-ttu-id="a3a30-134">Güvenilir bölgeye ayarlar desteklenmez kenarı ve Internet Explorer kullanıcıların da bu hatayı elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3a30-134">Edge and Internet Explorer users can also get this error when trusted zone settings are not supported.</span></span>
   
    <span data-ttu-id="a3a30-135">Her ikisi de doğrulayın [Analytics portalı](https://analytics.applicationinsights.io) ve [Azure Active Directory portalında](https://portal.azure.com) hello olan aynı güvenlik bölgesi:</span><span class="sxs-lookup"><span data-stu-id="a3a30-135">Verify both [Analytics portal](https://analytics.applicationinsights.io) and [Azure Active Directory portal](https://portal.azure.com) are in hello same security zone:</span></span>
   
   * <span data-ttu-id="a3a30-136">Internet Explorer'da açın **Internet Seçenekleri**, **güvenlik**, **Güvenilen siteler**, **siteleri**:</span><span class="sxs-lookup"><span data-stu-id="a3a30-136">In Internet Explorer, open **Internet Options**, **Security**, **Trusted sites**, **Sites**:</span></span>
     
     ![Internet Seçenekleri iletişim kutusunda, bir site ekleme tooTrusted siteler](./media/app-insights-analytics-troubleshooting/033.png)
     
     <span data-ttu-id="a3a30-138">Aşağıdaki URL'lere hello dahil olan hello Web siteleri listesinde o hello emin olun diğerleri de dahildir:</span><span class="sxs-lookup"><span data-stu-id="a3a30-138">In hello Websites list, if any of hello following URLs are included, make sure that hello others are included also:</span></span>
     
     <span data-ttu-id="a3a30-139">https://Analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="a3a30-139">https://analytics.applicationinsights.io</span></span><br/>
     <span data-ttu-id="a3a30-140">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="a3a30-140">https://login.microsoftonline.com</span></span><br/>
     <span data-ttu-id="a3a30-141">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="a3a30-141">https://login.windows.net</span></span>

## <span data-ttu-id="a3a30-142"><a name="e-d"></a>404 ... Kaynak bulunamadı</span><span class="sxs-lookup"><span data-stu-id="a3a30-142"><a name="e-d"></a>404 ... Resource not found</span></span>
![404... kaynak bulunamadı](./media/app-insights-analytics-troubleshooting/040.png)

<span data-ttu-id="a3a30-144">Uygulama kaynağı Application Insights silindi ve artık kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="a3a30-144">Application resource was deleted from Application Insights and isn’t available anymore.</span></span> <span data-ttu-id="a3a30-145">Merhaba URL toohello analitik sayfası kaydedilirse, bu durum oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="a3a30-145">This can happen if you saved hello URL toohello Analytics page.</span></span>

## <span data-ttu-id="a3a30-146"><a name="e-e"></a>403 ... Yok</span><span class="sxs-lookup"><span data-stu-id="a3a30-146"><a name="e-e"></a>403 ... No authorization</span></span>
![403... yetkili değil](./media/app-insights-analytics-troubleshooting/050.png)

<span data-ttu-id="a3a30-148">Bu uygulama izni tooopen analizleri sahip değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3a30-148">You don't have permission tooopen this application in Analytics.</span></span>

* <span data-ttu-id="a3a30-149">Merhaba bağlantı birisinden mı aldınız?</span><span class="sxs-lookup"><span data-stu-id="a3a30-149">Did you get hello link from someone else?</span></span> <span data-ttu-id="a3a30-150">Toomake hello olduğundan emin isteyin [okuyucular veya katkıda bulunanlar bu kaynak grubu için](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="a3a30-150">Ask them toomake sure you are in hello [readers or contributors for this resource group](app-insights-resources-roles-access-control.md).</span></span>
* <span data-ttu-id="a3a30-151">Farklı kimlik bilgileri kullanarak hello bağlantısı kaydettiniz?</span><span class="sxs-lookup"><span data-stu-id="a3a30-151">Did you save hello link using different credentials?</span></span> <span data-ttu-id="a3a30-152">Açık hello [Azure portal](https://portal.azure.com), oturumu kapatın ve ardından hello doğru kimlik bilgilerini sağlayan bu bağlantıyı yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="a3a30-152">Open hello [Azure portal](https://portal.azure.com), sign out, and then try this link again, providing hello correct credentials.</span></span>

## <span data-ttu-id="a3a30-153"><a name="html-storage"></a>403 ... HTML5 depolaması</span><span class="sxs-lookup"><span data-stu-id="a3a30-153"><a name="html-storage"></a>403 ... HTML5 Storage</span></span>
<span data-ttu-id="a3a30-154">HTML5 localStorage ve sessionStorage portalımıza kullanır.</span><span class="sxs-lookup"><span data-stu-id="a3a30-154">Our portal uses HTML5 localStorage and sessionStorage.</span></span>

* <span data-ttu-id="a3a30-155">Chrome: Ayarları, gizlilik, içerik ayarları.</span><span class="sxs-lookup"><span data-stu-id="a3a30-155">Chrome: Settings, privacy, content settings.</span></span>
* <span data-ttu-id="a3a30-156">Internet Explorer: Internet Seçenekleri, Gelişmiş sekmesinde, güvenlik, DOM depolama etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a3a30-156">Internet Explorer: Internet Options, Advanced tab, Security, Enable DOM Storage</span></span>

![403... tooenable HTML5 depolama deneyin](./media/app-insights-analytics-troubleshooting/060.png)

## <span data-ttu-id="a3a30-158"><a name="e-g"></a>404 ... Abonelik bulunamadı</span><span class="sxs-lookup"><span data-stu-id="a3a30-158"><a name="e-g"></a>404 ... Subscription not found</span></span>
![404 ... Abonelik bulunamadı](./media/app-insights-analytics-troubleshooting/070.png)

<span data-ttu-id="a3a30-160">Merhaba URL'si geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a3a30-160">hello URL is invalid.</span></span> 

* <span data-ttu-id="a3a30-161">Açık hello uygulama kaynak [Application Insights portalındaki](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a3a30-161">Open hello app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="a3a30-162">Ardından hello Analytics düğmesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a3a30-162">Then use hello Analytics button.</span></span>

## <span data-ttu-id="a3a30-163"><a name="e-h"></a>404... sayfa yok</span><span class="sxs-lookup"><span data-stu-id="a3a30-163"><a name="e-h"></a>404 ... page doesn't exist</span></span>
![404 ... Sayfa yok](./media/app-insights-analytics-troubleshooting/080.png)

<span data-ttu-id="a3a30-165">Merhaba URL'si geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a3a30-165">hello URL is invalid.</span></span>

* <span data-ttu-id="a3a30-166">Açık hello uygulama kaynak [Application Insights portalındaki](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a3a30-166">Open hello app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="a3a30-167">Ardından hello Analytics düğmesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a3a30-167">Then use hello Analytics button.</span></span>

## <span data-ttu-id="a3a30-168"><a name="cookies"></a>Üçüncü taraf tanımlama bilgilerini etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="a3a30-168"><a name="cookies"></a>Enable third-party cookies</span></span>
  <span data-ttu-id="a3a30-169">Bkz: [nasıl toodisable üçüncü taraf tanımlama bilgilerini](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), ancak çok ihtiyacımız fark**etkinleştirmek** bunları.</span><span class="sxs-lookup"><span data-stu-id="a3a30-169">See [how toodisable third party cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), but notice we need too**enable** them.</span></span>


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

