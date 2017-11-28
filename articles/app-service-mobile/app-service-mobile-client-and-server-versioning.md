---
title: "Mobil uygulamaları ve Mobile Services aaaClient ve sunucu SDK sürüm | Microsoft Docs"
description: "İstemci SDK'ları listesi ve Mobile Services ve Azure mobil uygulamalar sunucusu SDK sürümleriyle uyumluluk"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 35b19672-c9d6-49b5-b405-a6dcd1107cd5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5874b7455ea407ca8c77fb1bd03d97d0767ebb47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a><span data-ttu-id="49da6-103">Mobil uygulamaları ve Mobile Services istemci ve sunucu sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="49da6-103">Client and server versioning in Mobile Apps and Mobile Services</span></span>
<span data-ttu-id="49da6-104">Merhaba en son Azure Mobile Services sürümüdür hello **Mobile Apps** Azure uygulama hizmeti özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="49da6-104">hello latest version of Azure Mobile Services is hello **Mobile Apps** feature of Azure App Service.</span></span>

<span data-ttu-id="49da6-105">Mobil uygulamaları istemci hello ve sunucu SDK başlangıçta temel Mobile Services de, ancak bunlar *değil* birbiriyle uyumlu.</span><span class="sxs-lookup"><span data-stu-id="49da6-105">hello Mobile Apps client and server SDKs are originally based on those in Mobile Services, but they are *not* compatible with each other.</span></span>
<span data-ttu-id="49da6-106">Diğer bir deyişle, kullanmanız gereken bir *Mobile Apps* istemci SDK'sı ile bir *Mobile Apps* sunucusu SDK ve benzer şekilde *Mobile Services*.</span><span class="sxs-lookup"><span data-stu-id="49da6-106">That is, you must use a *Mobile Apps* client SDK with a *Mobile Apps* server SDK and similarly for *Mobile Services*.</span></span> <span data-ttu-id="49da6-107">Bu sözleşme hello istemci ve sunucu SDK'ları, tarafından kullanılan bir özel üstbilgi değeri aracılığıyla zorlanır `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="49da6-107">This contract is enforced through a special header value used by hello client and server SDKs, `ZUMO-API-VERSION`.</span></span>

<span data-ttu-id="49da6-108">Not: her bu belgeyi başvuruyor tooa *Mobile Services* arka uç, onu mutlaka gerekmez Mobile Services üzerinde barındırılan toobe.</span><span class="sxs-lookup"><span data-stu-id="49da6-108">Note: whenever this document refers tooa *Mobile Services* backend, it does not necessarily need toobe hosted on Mobile Services.</span></span> <span data-ttu-id="49da6-109">Şu anda olası toomigrate kod değişiklikleri olmadan uygulama hizmeti üzerinde bir mobil hizmet toorun durumdadır ancak hello hizmet hala kullanıyor *Mobile Services* SDK sürümleri.</span><span class="sxs-lookup"><span data-stu-id="49da6-109">It is now possible toomigrate a mobile service toorun on App Service without any code changes, but hello service would still be using *Mobile Services*  SDK versions.</span></span>

<span data-ttu-id="49da6-110">hakkında daha fazla bilgi toolearn hello makaleye bakın tooApp hizmet kod değişiklikleri olmadan geçirme [mobil hizmeti tooAzure uygulama hizmeti geçirmek].</span><span class="sxs-lookup"><span data-stu-id="49da6-110">toolearn more about migrating tooApp Service without any code changes, see hello article [Migrate a Mobile Service tooAzure App Service].</span></span>

## <a name="header-specification"></a><span data-ttu-id="49da6-111">Üstbilgi belirtimi</span><span class="sxs-lookup"><span data-stu-id="49da6-111">Header specification</span></span>
<span data-ttu-id="49da6-112">başlangıç anahtarı `ZUMO-API-VERSION` hello HTTP üstbilgisi veya hello sorgu dizesi olarak belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="49da6-112">hello key `ZUMO-API-VERSION` may be specified in either hello HTTP header or hello query string.</span></span> <span data-ttu-id="49da6-113">Merhaba değerdir hello formunda bir sürüm dizesi **x.y.z**.</span><span class="sxs-lookup"><span data-stu-id="49da6-113">hello value is a version string in hello form **x.y.z**.</span></span>

<span data-ttu-id="49da6-114">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="49da6-114">For example:</span></span>

<span data-ttu-id="49da6-115">Https://Service.azurewebsites.NET/Tables/TodoItem Al</span><span class="sxs-lookup"><span data-stu-id="49da6-115">GET https://service.azurewebsites.net/tables/TodoItem</span></span>

<span data-ttu-id="49da6-116">ÜSTBİLGİLERİ: ZUMO-API-VERSION: 2.0.0</span><span class="sxs-lookup"><span data-stu-id="49da6-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span></span>

<span data-ttu-id="49da6-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span><span class="sxs-lookup"><span data-stu-id="49da6-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span></span>

## <a name="opting-out-of-version-checking"></a><span data-ttu-id="49da6-118">Sürüm denetimi dışında kullanmama</span><span class="sxs-lookup"><span data-stu-id="49da6-118">Opting out of version checking</span></span>
<span data-ttu-id="49da6-119">Sürüm değerine ayarlayarak denetimini dışında seçebilirsiniz **true** hello uygulama ayarı için **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="49da6-119">You can opt out of version checking by setting a value of **true** for hello app setting **MS_SkipVersionCheck**.</span></span> <span data-ttu-id="49da6-120">Bu, web.config dosyanıza veya hello hello Azure portalında uygulama ayarları bölümü belirtin.</span><span class="sxs-lookup"><span data-stu-id="49da6-120">Specify this either in your web.config or in hello Application Settings section of hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="49da6-121">Mobile Services ve çevrimdışı eşitleme, kimlik doğrulaması ve anında iletme bildirimleri hello alanlarda özellikle mobil uygulamalar arasında davranış değişiklikleri mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="49da6-121">There are a number of behavior changes between Mobile Services and Mobile Apps, particularly in hello areas of offline sync, authentication, and push notifications.</span></span> <span data-ttu-id="49da6-122">Bu davranış değişiklikleri uygulamanızın işlevselliği bozmadığını sonra tam sınama tooensure denetimi sürüm dışında yalnızca tercih.</span><span class="sxs-lookup"><span data-stu-id="49da6-122">You should only opt out of version checking after complete testing tooensure that these behavioral changes do not break your app's functionality.</span></span>
>
>

## <a name="summary-of-compatibility-for-all-versions"></a><span data-ttu-id="49da6-123">Tüm sürümler için Uyumluluk özeti</span><span class="sxs-lookup"><span data-stu-id="49da6-123">Summary of compatibility for all versions</span></span>
<span data-ttu-id="49da6-124">tüm istemci ve sunucu türleri arasında hello uyumluluk aşağıdaki Hello grafik gösterir.</span><span class="sxs-lookup"><span data-stu-id="49da6-124">hello chart below shows hello compatibility between all client and server types.</span></span> <span data-ttu-id="49da6-125">Bir arka uç ya da mobil sınıflandırılır **Hizmetleri** ya da mobil **uygulamaları** kullandığı SDK hello sunucuya göre.</span><span class="sxs-lookup"><span data-stu-id="49da6-125">A backend is classified as either Mobile **Services** or Mobile **Apps** based on hello server SDK that it uses.</span></span>

|  | <span data-ttu-id="49da6-126">**Mobil Hizmetler** Node.js veya .NET</span><span class="sxs-lookup"><span data-stu-id="49da6-126">**Mobile Services** Node.js or .NET</span></span> | <span data-ttu-id="49da6-127">**Mobil uygulamaları** Node.js veya .NET</span><span class="sxs-lookup"><span data-stu-id="49da6-127">**Mobile Apps** Node.js or .NET</span></span> |
| --- | --- | --- |
| <span data-ttu-id="49da6-128">[Mobile Services istemcileri]</span><span class="sxs-lookup"><span data-stu-id="49da6-128">[Mobile Services clients]</span></span> |<span data-ttu-id="49da6-129">Tamam</span><span class="sxs-lookup"><span data-stu-id="49da6-129">Ok</span></span> |<span data-ttu-id="49da6-130">Hata\*</span><span class="sxs-lookup"><span data-stu-id="49da6-130">Error\*</span></span> |
| <span data-ttu-id="49da6-131">[Mobile Apps istemcileri]</span><span class="sxs-lookup"><span data-stu-id="49da6-131">[Mobile Apps clients]</span></span> |<span data-ttu-id="49da6-132">Hata\*</span><span class="sxs-lookup"><span data-stu-id="49da6-132">Error\*</span></span> |<span data-ttu-id="49da6-133">Tamam</span><span class="sxs-lookup"><span data-stu-id="49da6-133">Ok</span></span> |

<span data-ttu-id="49da6-134">\*Bu belirterek denetlenebilir **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="49da6-134">\*This can be controlled by specifying **MS_SkipVersionCheck**.</span></span>

<!-- IMPORTANT!  hello anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: hello fwlink toothis document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <span data-ttu-id="49da6-135"><a name="1.0.0"></a>Mobile Services İstemcisi ve sunucusu</span><span class="sxs-lookup"><span data-stu-id="49da6-135"><a name="1.0.0"></a>Mobile Services client and server</span></span>
<span data-ttu-id="49da6-136">Aşağıdaki hello tablosundaki Hello istemci SDK'ları ile uyumlu **Mobile Services**.</span><span class="sxs-lookup"><span data-stu-id="49da6-136">hello client SDKs in hello table below are compatible with **Mobile Services**.</span></span>

<span data-ttu-id="49da6-137">Not: Mobile Services istemci SDK'ları hello *sağlamadığı* bir üstbilgi değeri göndermek `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="49da6-137">Note: hello Mobile Services client SDKs *do not* send a header value for `ZUMO-API-VERSION`.</span></span> <span data-ttu-id="49da6-138">Bu üst bilgi veya sorgu dizesi değerini Hello hizmet alırsa, açıkça yukarıda açıklandığı gibi out çevirdiniz sürece bir hata döndürülür.</span><span class="sxs-lookup"><span data-stu-id="49da6-138">If hello service receives this header or query string value, an error will be returned, unless you have explicitly opted out as described above.</span></span>

### <span data-ttu-id="49da6-139"><a name="MobileServicesClients"></a>Mobil *Hizmetleri* istemci SDK'ları</span><span class="sxs-lookup"><span data-stu-id="49da6-139"><a name="MobileServicesClients"></a> Mobile *Services* client SDKs</span></span>
| <span data-ttu-id="49da6-140">İstemci Platformu</span><span class="sxs-lookup"><span data-stu-id="49da6-140">Client platform</span></span> | <span data-ttu-id="49da6-141">Sürüm</span><span class="sxs-lookup"><span data-stu-id="49da6-141">Version</span></span> | <span data-ttu-id="49da6-142">Version üstbilgi değeri</span><span class="sxs-lookup"><span data-stu-id="49da6-142">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="49da6-143">Yönetilen istemci (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="49da6-143">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="49da6-144">1.3.2</span><span class="sxs-lookup"><span data-stu-id="49da6-144">1.3.2</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |<span data-ttu-id="49da6-145">yok</span><span class="sxs-lookup"><span data-stu-id="49da6-145">n/a</span></span> |
| <span data-ttu-id="49da6-146">iOS</span><span class="sxs-lookup"><span data-stu-id="49da6-146">iOS</span></span> |[<span data-ttu-id="49da6-147">2.2.2</span><span class="sxs-lookup"><span data-stu-id="49da6-147">2.2.2</span></span>](http://aka.ms/gc6fex) |<span data-ttu-id="49da6-148">yok</span><span class="sxs-lookup"><span data-stu-id="49da6-148">n/a</span></span> |
| <span data-ttu-id="49da6-149">Android</span><span class="sxs-lookup"><span data-stu-id="49da6-149">Android</span></span> |[<span data-ttu-id="49da6-150">2.0.3</span><span class="sxs-lookup"><span data-stu-id="49da6-150">2.0.3</span></span>](https://go.microsoft.com/fwLink/?LinkID=280126) |<span data-ttu-id="49da6-151">yok</span><span class="sxs-lookup"><span data-stu-id="49da6-151">n/a</span></span> |
| <span data-ttu-id="49da6-152">HTML</span><span class="sxs-lookup"><span data-stu-id="49da6-152">HTML</span></span> |[<span data-ttu-id="49da6-153">1.2.7</span><span class="sxs-lookup"><span data-stu-id="49da6-153">1.2.7</span></span>](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |<span data-ttu-id="49da6-154">yok</span><span class="sxs-lookup"><span data-stu-id="49da6-154">n/a</span></span> |

### <a name="mobile-services-server-sdks"></a><span data-ttu-id="49da6-155">Mobil *Hizmetleri* sunucusu SDK</span><span class="sxs-lookup"><span data-stu-id="49da6-155">Mobile *Services* server SDKs</span></span>
| <span data-ttu-id="49da6-156">Sunucu platformu</span><span class="sxs-lookup"><span data-stu-id="49da6-156">Server platform</span></span> | <span data-ttu-id="49da6-157">Sürüm</span><span class="sxs-lookup"><span data-stu-id="49da6-157">Version</span></span> | <span data-ttu-id="49da6-158">Kabul edilen sürüm üst bilgisi</span><span class="sxs-lookup"><span data-stu-id="49da6-158">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="49da6-159">.NET</span><span class="sxs-lookup"><span data-stu-id="49da6-159">.NET</span></span> |[<span data-ttu-id="49da6-160">WindowsAzure.MobileServices.Backend.* sürüm 1.0.x</span><span class="sxs-lookup"><span data-stu-id="49da6-160">WindowsAzure.MobileServices.Backend.* Version 1.0.x</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |<span data-ttu-id="49da6-161">** Hiçbir sürüm üst bilgisi **</span><span class="sxs-lookup"><span data-stu-id="49da6-161">**No version header **</span></span> |
| <span data-ttu-id="49da6-162">Node.js</span><span class="sxs-lookup"><span data-stu-id="49da6-162">Node.js</span></span> |<span data-ttu-id="49da6-163">(yakında)</span><span class="sxs-lookup"><span data-stu-id="49da6-163">(coming soon)</span></span> |<span data-ttu-id="49da6-164">**Hiçbir sürüm üst bilgisi**</span><span class="sxs-lookup"><span data-stu-id="49da6-164">**No version header**</span></span> |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a><span data-ttu-id="49da6-165">Mobile Services arka uçlarını davranışı</span><span class="sxs-lookup"><span data-stu-id="49da6-165">Behavior of Mobile Services backends</span></span>
| <span data-ttu-id="49da6-166">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="49da6-166">ZUMO-API-VERSION</span></span> | <span data-ttu-id="49da6-167">MS_SkipVersionCheck değeri</span><span class="sxs-lookup"><span data-stu-id="49da6-167">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="49da6-168">Yanıt</span><span class="sxs-lookup"><span data-stu-id="49da6-168">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="49da6-169">Belirtilmemiş.</span><span class="sxs-lookup"><span data-stu-id="49da6-169">Not specified</span></span> |<span data-ttu-id="49da6-170">Herhangi biri</span><span class="sxs-lookup"><span data-stu-id="49da6-170">Any</span></span> |<span data-ttu-id="49da6-171">200 - TAMAM</span><span class="sxs-lookup"><span data-stu-id="49da6-171">200 - OK</span></span> |
| <span data-ttu-id="49da6-172">Herhangi bir değer</span><span class="sxs-lookup"><span data-stu-id="49da6-172">Any value</span></span> |<span data-ttu-id="49da6-173">True</span><span class="sxs-lookup"><span data-stu-id="49da6-173">True</span></span> |<span data-ttu-id="49da6-174">200 - TAMAM</span><span class="sxs-lookup"><span data-stu-id="49da6-174">200 - OK</span></span> |
| <span data-ttu-id="49da6-175">Herhangi bir değer</span><span class="sxs-lookup"><span data-stu-id="49da6-175">Any value</span></span> |<span data-ttu-id="49da6-176">Belirtilen false/değil</span><span class="sxs-lookup"><span data-stu-id="49da6-176">False/Not Specified</span></span> |<span data-ttu-id="49da6-177">400 - Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="49da6-177">400 - Bad Request</span></span> |

## <span data-ttu-id="49da6-178"><a name="2.0.0"></a>Azure Mobile Apps istemci ve sunucu</span><span class="sxs-lookup"><span data-stu-id="49da6-178"><a name="2.0.0"></a>Azure Mobile Apps client and server</span></span>
### <span data-ttu-id="49da6-179"><a name="MobileAppsClients"></a>Mobil *uygulamaları* istemci SDK'ları</span><span class="sxs-lookup"><span data-stu-id="49da6-179"><a name="MobileAppsClients"></a> Mobile *Apps* client SDKs</span></span>
<span data-ttu-id="49da6-180">Sürüm denetimi sunulmuştur hello istemci SDK sürümleri aşağıdaki hello ile başlatma için **Azure Mobile Apps**:</span><span class="sxs-lookup"><span data-stu-id="49da6-180">Version checking was introduced starting with hello following versions of hello client SDK for **Azure Mobile Apps**:</span></span>

| <span data-ttu-id="49da6-181">İstemci Platformu</span><span class="sxs-lookup"><span data-stu-id="49da6-181">Client platform</span></span> | <span data-ttu-id="49da6-182">Sürüm</span><span class="sxs-lookup"><span data-stu-id="49da6-182">Version</span></span> | <span data-ttu-id="49da6-183">Version üstbilgi değeri</span><span class="sxs-lookup"><span data-stu-id="49da6-183">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="49da6-184">Yönetilen istemci (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="49da6-184">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="49da6-185">2.0.0</span><span class="sxs-lookup"><span data-stu-id="49da6-185">2.0.0</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |<span data-ttu-id="49da6-186">2.0.0</span><span class="sxs-lookup"><span data-stu-id="49da6-186">2.0.0</span></span> |
| <span data-ttu-id="49da6-187">iOS</span><span class="sxs-lookup"><span data-stu-id="49da6-187">iOS</span></span> |[<span data-ttu-id="49da6-188">3.0.0</span><span class="sxs-lookup"><span data-stu-id="49da6-188">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=529823) |<span data-ttu-id="49da6-189">2.0.0</span><span class="sxs-lookup"><span data-stu-id="49da6-189">2.0.0</span></span> |
| <span data-ttu-id="49da6-190">Android</span><span class="sxs-lookup"><span data-stu-id="49da6-190">Android</span></span> |[<span data-ttu-id="49da6-191">3.0.0</span><span class="sxs-lookup"><span data-stu-id="49da6-191">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |<span data-ttu-id="49da6-192">3.0.0</span><span class="sxs-lookup"><span data-stu-id="49da6-192">3.0.0</span></span> |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a><span data-ttu-id="49da6-193">Mobil *uygulamaları* sunucusu SDK</span><span class="sxs-lookup"><span data-stu-id="49da6-193">Mobile *Apps* server SDKs</span></span>
<span data-ttu-id="49da6-194">Sürüm denetimi server SDK sürümleri aşağıdaki eklenmiştir:</span><span class="sxs-lookup"><span data-stu-id="49da6-194">Version checking is included in following server SDK versions:</span></span>

| <span data-ttu-id="49da6-195">Sunucu platformu</span><span class="sxs-lookup"><span data-stu-id="49da6-195">Server platform</span></span> | <span data-ttu-id="49da6-196">SDK</span><span class="sxs-lookup"><span data-stu-id="49da6-196">SDK</span></span> | <span data-ttu-id="49da6-197">Kabul edilen sürüm üst bilgisi</span><span class="sxs-lookup"><span data-stu-id="49da6-197">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="49da6-198">.NET</span><span class="sxs-lookup"><span data-stu-id="49da6-198">.NET</span></span> |[<span data-ttu-id="49da6-199">Microsoft.Azure.Mobile.Server</span><span class="sxs-lookup"><span data-stu-id="49da6-199">Microsoft.Azure.Mobile.Server</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |<span data-ttu-id="49da6-200">2.0.0</span><span class="sxs-lookup"><span data-stu-id="49da6-200">2.0.0</span></span> |
| <span data-ttu-id="49da6-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="49da6-201">Node.js</span></span> |[<span data-ttu-id="49da6-202">Azure-mobile-uygulamalar)</span><span class="sxs-lookup"><span data-stu-id="49da6-202">azure-mobile-apps)</span></span>](https://www.npmjs.com/package/azure-mobile-apps) |<span data-ttu-id="49da6-203">2.0.0</span><span class="sxs-lookup"><span data-stu-id="49da6-203">2.0.0</span></span> |

### <a name="behavior-of-mobile-apps-backends"></a><span data-ttu-id="49da6-204">Mobile Apps arka uçlarını davranışı</span><span class="sxs-lookup"><span data-stu-id="49da6-204">Behavior of Mobile Apps backends</span></span>
| <span data-ttu-id="49da6-205">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="49da6-205">ZUMO-API-VERSION</span></span> | <span data-ttu-id="49da6-206">MS_SkipVersionCheck değeri</span><span class="sxs-lookup"><span data-stu-id="49da6-206">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="49da6-207">Yanıt</span><span class="sxs-lookup"><span data-stu-id="49da6-207">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="49da6-208">x.y.z ya da Null</span><span class="sxs-lookup"><span data-stu-id="49da6-208">x.y.z or Null</span></span> |<span data-ttu-id="49da6-209">True</span><span class="sxs-lookup"><span data-stu-id="49da6-209">True</span></span> |<span data-ttu-id="49da6-210">200 - TAMAM</span><span class="sxs-lookup"><span data-stu-id="49da6-210">200 - OK</span></span> |
| <span data-ttu-id="49da6-211">Null</span><span class="sxs-lookup"><span data-stu-id="49da6-211">Null</span></span> |<span data-ttu-id="49da6-212">Belirtilen false/değil</span><span class="sxs-lookup"><span data-stu-id="49da6-212">False/Not Specified</span></span> |<span data-ttu-id="49da6-213">400 - Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="49da6-213">400 - Bad Request</span></span> |
| <span data-ttu-id="49da6-214">1.x.y</span><span class="sxs-lookup"><span data-stu-id="49da6-214">1.x.y</span></span> |<span data-ttu-id="49da6-215">Belirtilen false/değil</span><span class="sxs-lookup"><span data-stu-id="49da6-215">False/Not Specified</span></span> |<span data-ttu-id="49da6-216">400 - Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="49da6-216">400 - Bad Request</span></span> |
| <span data-ttu-id="49da6-217">2.0.0-2.x.y</span><span class="sxs-lookup"><span data-stu-id="49da6-217">2.0.0-2.x.y</span></span> |<span data-ttu-id="49da6-218">Belirtilen false/değil</span><span class="sxs-lookup"><span data-stu-id="49da6-218">False/Not Specified</span></span> |<span data-ttu-id="49da6-219">200 - TAMAM</span><span class="sxs-lookup"><span data-stu-id="49da6-219">200 - OK</span></span> |
| <span data-ttu-id="49da6-220">3.0.0-3.x.y</span><span class="sxs-lookup"><span data-stu-id="49da6-220">3.0.0-3.x.y</span></span> |<span data-ttu-id="49da6-221">Belirtilen false/değil</span><span class="sxs-lookup"><span data-stu-id="49da6-221">False/Not Specified</span></span> |<span data-ttu-id="49da6-222">400 - Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="49da6-222">400 - Bad Request</span></span> |

## <a name="next-steps"></a><span data-ttu-id="49da6-223">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="49da6-223">Next Steps</span></span>
* <span data-ttu-id="49da6-224">[mobil hizmeti tooAzure uygulama hizmeti geçirmek]</span><span class="sxs-lookup"><span data-stu-id="49da6-224">[Migrate a Mobile Service tooAzure App Service]</span></span>

[Mobile Services istemcileri]: #MobileServicesClients
[Mobile Apps istemcileri]: #MobileAppsClients


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[mobil hizmeti tooAzure uygulama hizmeti geçirmek]: app-service-mobile-migrating-from-mobile-services.md
