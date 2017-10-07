---
title: "aaaGet otomatik ölçek ile özel bir ölçü Azure tarafından başlatılan | Microsoft Docs"
description: "Bilgi nasıl tooscale kaynağınız özel ölçüm Azure tarafından."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: d3e268ec322698d0d367361cd9c156b21e0fb6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a><span data-ttu-id="1f511-103">Otomatik ölçek ile özel bir ölçü Azure tarafından kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="1f511-103">Get started with auto scale by custom metric in Azure</span></span>
<span data-ttu-id="1f511-104">Bu makalede nasıl tooscale kaynağınız Azure portal'ın özel bir ölçü tarafından.</span><span class="sxs-lookup"><span data-stu-id="1f511-104">This article describes how tooscale your resource by a custom metric in Azure portal.</span></span>

<span data-ttu-id="1f511-105">Azure İzleyici otomatik ölçek tooVirtual makine ölçek kümeleri (VMSS), bulut Hizmetleri, uygulama hizmeti planları ve uygulama hizmeti ortamları yalnızca geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1f511-105">Azure Monitor auto scale applies only tooVirtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="1f511-106">Sağlar kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="1f511-106">Lets get started</span></span>
<span data-ttu-id="1f511-107">Bu makalede, application ınsights ile yapılandırılmış bir web uygulaması olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="1f511-107">This article assumes that you have a web app with application insights configured.</span></span> <span data-ttu-id="1f511-108">Zaten yoksa, şunları yapabilirsiniz [ASP.NET Web siteniz için Application Insights'ı ayarlama][1]</span><span class="sxs-lookup"><span data-stu-id="1f511-108">If you don't have one already, you can [set up Application Insights for your ASP.NET website][1]</span></span>

- <span data-ttu-id="1f511-109">Açık [Azure portalı][2]</span><span class="sxs-lookup"><span data-stu-id="1f511-109">Open [Azure portal][2]</span></span>
- <span data-ttu-id="1f511-110">Merhaba sol gezinti bölmesindeki Azure İzleyici simgeyi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1f511-110">Click on Azure Monitor icon in hello left navigation pane.</span></span>
  <span data-ttu-id="1f511-111">![Azure izleyicisini Başlat][3]</span><span class="sxs-lookup"><span data-stu-id="1f511-111">![Launch Azure Monitor][3]</span></span>
- <span data-ttu-id="1f511-112">Otomatik ölçeklendirme için Otomatik ölçek geçerli otomatik ölçeklendirme durumunun yanı sıra uygulanabilir tüm hello kaynaklarını tooview ayarı tıklatıldığında ![Azure İzleyicisi'nde otomatik ölçek Bul][4]</span><span class="sxs-lookup"><span data-stu-id="1f511-112">Click on Autoscale setting tooview all hello resources for which auto scale is applicable, along with its current autoscale status ![Discover auto scale in Azure monitor][4]</span></span>
- <span data-ttu-id="1f511-113">Azure İzleyicisi'nde 'Otomatik ölçeklendirme' dikey penceresini açın ve tooscale istediğiniz bir kaynak seçin</span><span class="sxs-lookup"><span data-stu-id="1f511-113">Open 'Autoscale' blade in Azure Monitor and select a resource you want tooscale</span></span>
> <span data-ttu-id="1f511-114">Not: app ınsights yapılandırılmış olan bir web uygulaması ile ilişkili bir uygulama hizmeti planı hello adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="1f511-114">Note: hello steps below use an app service plan associated with a web app that has app insights configured.</span></span>
- <span data-ttu-id="1f511-115">Merhaba ölçek ayarı dikey penceresinde hello kaynağın hello geçerli örnek sayısı 1 olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="1f511-115">In hello scale setting blade for hello resource, notice that hello current instance count is 1.</span></span> <span data-ttu-id="1f511-116">'Etkinleştir otomatik 'ölçeklendirme'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1f511-116">Click on 'Enable autoscale'.</span></span>
  <span data-ttu-id="1f511-117">![Yeni web uygulaması için ölçek ayarı][5]</span><span class="sxs-lookup"><span data-stu-id="1f511-117">![Scale setting for new web app][5]</span></span>
- <span data-ttu-id="1f511-118">Merhaba ölçek ayarlama ve hello tıklayın için "Kural Ekle" bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="1f511-118">Provide a name for hello scale setting, and hello click on "Add a rule".</span></span> <span data-ttu-id="1f511-119">Bir bağlam hello sağ taraftaki bölmede olarak açılır hello ölçek kuralı seçeneklerini dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="1f511-119">Notice hello scale rule options that opens as a context pane in hello right hand side.</span></span> <span data-ttu-id="1f511-120">Varsayılan olarak, örneğinizi sayısı 1 ile Merhaba CPU percetage hello kaynağının % 70 aşarsa hello seçeneği tooscale ayarlar.</span><span class="sxs-lookup"><span data-stu-id="1f511-120">By default, it sets hello option tooscale your instance count by 1 if hello CPU percetage of hello resource exceeds 70%.</span></span> <span data-ttu-id="1f511-121">Merhaba ölçüm Kaynağı Değiştir hello üstünde çok "Application Insights", select app ınsights kaynağı hello 'Resource' açılır ve temel seçip hello özel ölçüm tooscale istediğiniz hello.</span><span class="sxs-lookup"><span data-stu-id="1f511-121">Change hello metric source at hello top too"Application Insights", select hello app insights resource in hello 'Resource' dropdown and then select hello custom metric based on which you want tooscale.</span></span>
  <span data-ttu-id="1f511-122">![Özel bir ölçü ölçeklendirin][6]</span><span class="sxs-lookup"><span data-stu-id="1f511-122">![Scale by custom metric][6]</span></span>
- <span data-ttu-id="1f511-123">Yukarıdaki benzer toohello adımı içinde ölçeklendirmek ve hello özel ölçüm eşiğin altına ise hello ölçek sayısı 1 ile azaltmak ölçek kuralı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1f511-123">Similar toohello step above, add a scale rule that will scale in and decrease hello scale count by 1 if hello custom metric is below a threshold.</span></span>
  <span data-ttu-id="1f511-124">![CPU üzerinde göre ölçeklendirin][7]</span><span class="sxs-lookup"><span data-stu-id="1f511-124">![Scale based on cpu][7]</span></span>
- <span data-ttu-id="1f511-125">Merhaba sınırları örneği ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1f511-125">Set hello you instance limits.</span></span> <span data-ttu-id="1f511-126">Merhaba özel ölçüm dalgalanmaları bağlı olarak 2-5 örnekleri arasında tooscale isterseniz, örneğin, 'minimum' çok '2', 'en fazla' çok ayarlayın '5' ve 'default' çok '2'</span><span class="sxs-lookup"><span data-stu-id="1f511-126">For example, if you want tooscale between 2-5 instances depending on hello custom metric fluctuations, set 'minimum' too'2', 'maximum' too'5' and 'default' too'2'</span></span>
> <span data-ttu-id="1f511-127">Not: hello kaynak ölçümleri okunurken bir sorun oluştu ve hello geçerli kapasitesi hello varsayılan kapasitenin altında olduğunda durumunda, ardından tooensure hello hello kaynak kullanılabilirliğini otomatik ölçeklendirme toohello varsayılan değerini ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="1f511-127">Note: In case there is a problem reading hello resource metrics and hello current capacity is below hello default capacity, then tooensure hello availability of hello resource, Autoscale will scale out toohello default value.</span></span> <span data-ttu-id="1f511-128">Merhaba geçerli kapasite zaten varsayılan kapasitesinden yüksek ise, otomatik ölçeklendirme, ölçekleme sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="1f511-128">If hello current capacity is already higher than default capacity, Autoscale will not scale in.</span></span>
- <span data-ttu-id="1f511-129">'Kaydet' tıklayın</span><span class="sxs-lookup"><span data-stu-id="1f511-129">Click on 'Save'</span></span>

<span data-ttu-id="1f511-130">Tebrikler.</span><span class="sxs-lookup"><span data-stu-id="1f511-130">Congratulations.</span></span> <span data-ttu-id="1f511-131">Şimdi başarıyla ölçek ayarı tooauto oluşturulan artık web uygulamanız özel bir ölçü ölçekleme.</span><span class="sxs-lookup"><span data-stu-id="1f511-131">You now now succesfully created your scale setting tooauto scale your web app based on a custom metric.</span></span>

> <span data-ttu-id="1f511-132">Not: hello aynı VMSS veya Bulut hizmet rolü ile başlatılan geçerli tooget adımlardır.</span><span class="sxs-lookup"><span data-stu-id="1f511-132">Note: hello same steps are applicable tooget started with a VMSS or cloud service role.</span></span>

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
