---
title: "Application Insights tarafından kullanılan aaaIP adresleri | Microsoft Docs"
description: "Application Insights tarafından gerekli sunucu güvenlik duvarı özel durumlar"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 44d989f8-bae9-40ff-bfd5-8343d3e59358
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 8/11/2017
ms.author: bwren
ms.openlocfilehash: 2c101b8da2ba9594fbff607f4f7551cda80c3c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="ip-addresses-used-by-application-insights"></a><span data-ttu-id="1ee4c-103">Application Insights tarafından kullanılan IP adresleri</span><span class="sxs-lookup"><span data-stu-id="1ee4c-103">IP addresses used by Application Insights</span></span>
<span data-ttu-id="1ee4c-104">Merhaba [Azure Application Insights](app-insights-overview.md) hizmeti, IP adreslerinin sayısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="1ee4c-104">hello [Azure Application Insights](app-insights-overview.md) service uses a number of IP addresses.</span></span> <span data-ttu-id="1ee4c-105">İzlemekte olduğunuz hello uygulama güvenlik duvarının arkasında barındırılıyorsa bu adresleri tooknow gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="1ee4c-105">You might need tooknow these addresses if hello app that you are monitoring is hosted behind a firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="1ee4c-106">Bu adresler statik olsa da, toochange gerekir mümkündür atamalarını zaman tootime kaldırın.</span><span class="sxs-lookup"><span data-stu-id="1ee4c-106">Although these addresses are static, it's possible that we will need toochange them from time tootime.</span></span>
> 
> 

## <a name="outgoing-ports"></a><span data-ttu-id="1ee4c-107">Giden bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="1ee4c-107">Outgoing ports</span></span>
<span data-ttu-id="1ee4c-108">Bazı sunucunuzun güvenlik duvarı tooallow hello Application Insights SDK'sı giden bağlantı noktaları ve/veya Durum İzleyicisi toosend veri toohello portal tooopen gerekir:</span><span class="sxs-lookup"><span data-stu-id="1ee4c-108">You need tooopen some outgoing ports in your server's firewall tooallow hello Application Insights SDK and/or Status Monitor toosend data toohello portal:</span></span>

| <span data-ttu-id="1ee4c-109">Amaç</span><span class="sxs-lookup"><span data-stu-id="1ee4c-109">Purpose</span></span> | <span data-ttu-id="1ee4c-110">URL</span><span class="sxs-lookup"><span data-stu-id="1ee4c-110">URL</span></span> | <span data-ttu-id="1ee4c-111">IP</span><span class="sxs-lookup"><span data-stu-id="1ee4c-111">IP</span></span> | <span data-ttu-id="1ee4c-112">Bağlantı Noktaları</span><span class="sxs-lookup"><span data-stu-id="1ee4c-112">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1ee4c-113">Telemetri</span><span class="sxs-lookup"><span data-stu-id="1ee4c-113">Telemetry</span></span> |<span data-ttu-id="1ee4c-114">DC.Services.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="1ee4c-114">dc.services.visualstudio.com</span></span><br/><span data-ttu-id="1ee4c-115">DC.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="1ee4c-115">dc.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="1ee4c-116">40.114.241.141</span><span class="sxs-lookup"><span data-stu-id="1ee4c-116">40.114.241.141</span></span><br/><span data-ttu-id="1ee4c-117">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="1ee4c-117">104.45.136.42</span></span><br/><span data-ttu-id="1ee4c-118">40.84.189.107</span><span class="sxs-lookup"><span data-stu-id="1ee4c-118">40.84.189.107</span></span><br/><span data-ttu-id="1ee4c-119">168.63.242.221</span><span class="sxs-lookup"><span data-stu-id="1ee4c-119">168.63.242.221</span></span><br/><span data-ttu-id="1ee4c-120">52.167.221.184</span><span class="sxs-lookup"><span data-stu-id="1ee4c-120">52.167.221.184</span></span><br/><span data-ttu-id="1ee4c-121">52.169.64.244</span><span class="sxs-lookup"><span data-stu-id="1ee4c-121">52.169.64.244</span></span> |<span data-ttu-id="1ee4c-122">443</span><span class="sxs-lookup"><span data-stu-id="1ee4c-122">443</span></span> |
| <span data-ttu-id="1ee4c-123">Canlı ölçümleri akış</span><span class="sxs-lookup"><span data-stu-id="1ee4c-123">Live Metrics Stream</span></span> |<span data-ttu-id="1ee4c-124">RT.Services.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="1ee4c-124">rt.services.visualstudio.com</span></span><br/><span data-ttu-id="1ee4c-125">RT.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="1ee4c-125">rt.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="1ee4c-126">23.96.28.38</span><span class="sxs-lookup"><span data-stu-id="1ee4c-126">23.96.28.38</span></span><br/><span data-ttu-id="1ee4c-127">13.92.40.198</span><span class="sxs-lookup"><span data-stu-id="1ee4c-127">13.92.40.198</span></span> |<span data-ttu-id="1ee4c-128">443</span><span class="sxs-lookup"><span data-stu-id="1ee4c-128">443</span></span> |
| <span data-ttu-id="1ee4c-129">İç Telemetri</span><span class="sxs-lookup"><span data-stu-id="1ee4c-129">Internal Telemetry</span></span> |<span data-ttu-id="1ee4c-130">BREEZE.aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="1ee4c-130">breeze.aimon.applicationinsights.io</span></span> |<span data-ttu-id="1ee4c-131">52.161.11.71</span><span class="sxs-lookup"><span data-stu-id="1ee4c-131">52.161.11.71</span></span> |<span data-ttu-id="1ee4c-132">443</span><span class="sxs-lookup"><span data-stu-id="1ee4c-132">443</span></span> |

## <a name="status-monitor"></a><span data-ttu-id="1ee4c-133">Durum İzleyicisi</span><span class="sxs-lookup"><span data-stu-id="1ee4c-133">Status Monitor</span></span>
<span data-ttu-id="1ee4c-134">Durum İzleyicisi'ni yapılandırma - yalnızca değişiklik yaparken gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ee4c-134">Status Monitor Configuration - needed only when making changes.</span></span>

| <span data-ttu-id="1ee4c-135">Amaç</span><span class="sxs-lookup"><span data-stu-id="1ee4c-135">Purpose</span></span> | <span data-ttu-id="1ee4c-136">URL</span><span class="sxs-lookup"><span data-stu-id="1ee4c-136">URL</span></span> | <span data-ttu-id="1ee4c-137">IP</span><span class="sxs-lookup"><span data-stu-id="1ee4c-137">IP</span></span> | <span data-ttu-id="1ee4c-138">Bağlantı Noktaları</span><span class="sxs-lookup"><span data-stu-id="1ee4c-138">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1ee4c-139">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1ee4c-139">Configuration</span></span> |`management.core.windows.net` | |`443` |
| <span data-ttu-id="1ee4c-140">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1ee4c-140">Configuration</span></span> |`management.azure.com` | |`443` |
| <span data-ttu-id="1ee4c-141">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1ee4c-141">Configuration</span></span> |`login.windows.net` | |`443` |
| <span data-ttu-id="1ee4c-142">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1ee4c-142">Configuration</span></span> |`login.microsoftonline.com` | |`443` |
| <span data-ttu-id="1ee4c-143">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1ee4c-143">Configuration</span></span> |`secure.aadcdn.microsoftonline-p.com` | |`443` |
| <span data-ttu-id="1ee4c-144">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1ee4c-144">Configuration</span></span> |`auth.gfx.ms` | |`443` |
| <span data-ttu-id="1ee4c-145">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1ee4c-145">Configuration</span></span> |`login.live.com` | |`443` |
| <span data-ttu-id="1ee4c-146">Yükleme</span><span class="sxs-lookup"><span data-stu-id="1ee4c-146">Installation</span></span> |`packages.nuget.org` | |`443` |

## <a name="hockeyapp"></a><span data-ttu-id="1ee4c-147">HockeyApp</span><span class="sxs-lookup"><span data-stu-id="1ee4c-147">HockeyApp</span></span>
| <span data-ttu-id="1ee4c-148">Amaç</span><span class="sxs-lookup"><span data-stu-id="1ee4c-148">Purpose</span></span> | <span data-ttu-id="1ee4c-149">URL</span><span class="sxs-lookup"><span data-stu-id="1ee4c-149">URL</span></span> | <span data-ttu-id="1ee4c-150">IP</span><span class="sxs-lookup"><span data-stu-id="1ee4c-150">IP</span></span> | <span data-ttu-id="1ee4c-151">Bağlantı Noktaları</span><span class="sxs-lookup"><span data-stu-id="1ee4c-151">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1ee4c-152">Çökme verileri</span><span class="sxs-lookup"><span data-stu-id="1ee4c-152">Crash data</span></span> |<span data-ttu-id="1ee4c-153">Gate.hockeyapp.NET</span><span class="sxs-lookup"><span data-stu-id="1ee4c-153">gate.hockeyapp.net</span></span> |<span data-ttu-id="1ee4c-154">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="1ee4c-154">104.45.136.42</span></span> |<span data-ttu-id="1ee4c-155">80, 443</span><span class="sxs-lookup"><span data-stu-id="1ee4c-155">80, 443</span></span> |

## <a name="availability-tests"></a><span data-ttu-id="1ee4c-156">Kullanılabilirlik testleri</span><span class="sxs-lookup"><span data-stu-id="1ee4c-156">Availability tests</span></span>
<span data-ttu-id="1ee4c-157">Bu hello hangi adreslerinden listesidir [kullanılabilirlik web testleri](app-insights-monitor-web-app-availability.md) çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="1ee4c-157">This is hello list of addresses from which [availability web tests](app-insights-monitor-web-app-availability.md) are run.</span></span> <span data-ttu-id="1ee4c-158">İstiyorsanız, uygulamanıza toorun web testleri, ancak bizim kullanılabilirlik test sunucularından gelen trafiği toopermit sahip olacaktır kısıtlı tooserving belirli istemciler, web sunucunuz olur.</span><span class="sxs-lookup"><span data-stu-id="1ee4c-158">If you want toorun web tests on your app, but your web server is restricted tooserving specific clients, then you will have toopermit incoming traffic from our availability test servers.</span></span>

<span data-ttu-id="1ee4c-159">(IP adresleri konuma göre gruplandırılır) Bu adreslerden gelen 80 (http) ve gelen trafiği için 443 (https) bağlantı noktalarını açın:</span><span class="sxs-lookup"><span data-stu-id="1ee4c-159">Open ports 80 (http) and 443 (https) for incoming traffic from these addresses (IP addresses are grouped by location):</span></span>

```
AU : Sydney
13.70.83.252
13.75.150.96
13.75.153.9
13.75.158.185
BR : Sao Paulo
191.232.32.122
191.232.172.45
191.232.176.218
191.232.191.225
CH : Zurich
94.245.66.43
94.245.66.44
94.245.66.45
94.245.66.48
FR : Paris
94.245.72.44
94.245.72.45
94.245.72.46
94.245.72.49
94.245.72.52
94.245.72.53
HK : Hong Kong
13.75.121.122
23.99.115.153
23.99.123.38
23.102.232.186
52.175.38.49
52.175.39.103
IE : Dublin
13.74.184.101
13.74.185.160
40.69.200.198
52.164.224.46
52.169.12.203
52.169.14.11
52.169.237.149
52.178.183.105
JP : Kawaguchi
52.243.33.33
52.243.33.141
52.243.35.253
52.243.41.117
NL : Amsterdam
52.174.166.113
52.174.178.96
52.174.31.140
52.174.35.14
52.178.104.23
52.178.109.190
52.178.111.139
52.233.166.221
RU : Moscow
94.245.82.32
94.245.82.33
94.245.82.37
94.245.82.38
SE : Stockholm
94.245.78.40
94.245.78.41
94.245.78.42
94.245.78.45
SG : Singapore
52.187.29.7
52.187.179.17
52.187.76.248
52.187.43.24
52.163.57.91
52.187.30.120
US : CA-San Jose
104.45.228.236
104.45.237.251
13.64.152.110
13.64.156.54
13.64.232.251
13.64.236.105
13.91.94.59
40.118.131.182
40.83.189.192
40.83.215.122
US : FL-Miami
65.54.78.49
65.54.78.50
65.54.78.51
65.54.78.54
65.54.78.57
65.54.78.58
65.54.78.59
65.54.78.60
US : IL-Chicago
23.96.247.139
23.96.249.113
52.162.124.242
52.162.126.139
52.162.241.147
52.162.246.222
52.162.247.136
52.237.153.231
52.237.154.216
52.237.156.14
52.237.157.218
52.237.157.37
US : TX-San Antonio
104.210.145.106
13.84.176.24
13.84.49.16
13.85.11.137
13.85.26.248
13.85.69.145
52.171.136.162
52.171.141.253
52.171.57.172
52.171.58.140
US : VA-Ashburn
13.82.218.95
13.90.96.71
13.90.98.52
13.92.137.70
40.85.187.235
40.87.61.61
52.168.8.247
52.170.38.79
52.170.80.61
52.179.9.26

```  

## <a name="data-access-api"></a><span data-ttu-id="1ee4c-160">Veri erişimi API’si</span><span class="sxs-lookup"><span data-stu-id="1ee4c-160">Data access API</span></span>
| <span data-ttu-id="1ee4c-161">Amaç</span><span class="sxs-lookup"><span data-stu-id="1ee4c-161">Purpose</span></span> | <span data-ttu-id="1ee4c-162">URI</span><span class="sxs-lookup"><span data-stu-id="1ee4c-162">URI</span></span> | <span data-ttu-id="1ee4c-163">IP</span><span class="sxs-lookup"><span data-stu-id="1ee4c-163">IP</span></span> | <span data-ttu-id="1ee4c-164">Bağlantı Noktaları</span><span class="sxs-lookup"><span data-stu-id="1ee4c-164">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1ee4c-165">API</span><span class="sxs-lookup"><span data-stu-id="1ee4c-165">API</span></span> |<span data-ttu-id="1ee4c-166">api.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="1ee4c-166">api.applicationinsights.io</span></span><br/><span data-ttu-id="1ee4c-167">api1.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="1ee4c-167">api1.applicationinsights.io</span></span><br/><span data-ttu-id="1ee4c-168">api2.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="1ee4c-168">api2.applicationinsights.io</span></span><br/><span data-ttu-id="1ee4c-169">api3.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="1ee4c-169">api3.applicationinsights.io</span></span><br/><span data-ttu-id="1ee4c-170">api4.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="1ee4c-170">api4.applicationinsights.io</span></span><br/><span data-ttu-id="1ee4c-171">api5.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="1ee4c-171">api5.applicationinsights.io</span></span> |<span data-ttu-id="1ee4c-172">13.82.26.252</span><span class="sxs-lookup"><span data-stu-id="1ee4c-172">13.82.26.252</span></span><br/><span data-ttu-id="1ee4c-173">40.76.213.73</span><span class="sxs-lookup"><span data-stu-id="1ee4c-173">40.76.213.73</span></span> |<span data-ttu-id="1ee4c-174">80,443</span><span class="sxs-lookup"><span data-stu-id="1ee4c-174">80,443</span></span> |
| <span data-ttu-id="1ee4c-175">API belgeleri</span><span class="sxs-lookup"><span data-stu-id="1ee4c-175">API docs</span></span> |<span data-ttu-id="1ee4c-176">dev.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="1ee4c-176">dev.applicationinsights.io</span></span><br/><span data-ttu-id="1ee4c-177">dev.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="1ee4c-177">dev.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="1ee4c-178">dev.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="1ee4c-178">dev.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="1ee4c-179">www.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="1ee4c-179">www.applicationinsights.io</span></span><br/><span data-ttu-id="1ee4c-180">www.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="1ee4c-180">www.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="1ee4c-181">www.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="1ee4c-181">www.aisvc.visualstudio.com</span></span> |<span data-ttu-id="1ee4c-182">13.82.24.149</span><span class="sxs-lookup"><span data-stu-id="1ee4c-182">13.82.24.149</span></span><br/><span data-ttu-id="1ee4c-183">40.114.82.10</span><span class="sxs-lookup"><span data-stu-id="1ee4c-183">40.114.82.10</span></span> |<span data-ttu-id="1ee4c-184">80,443</span><span class="sxs-lookup"><span data-stu-id="1ee4c-184">80,443</span></span> |
| <span data-ttu-id="1ee4c-185">İç API</span><span class="sxs-lookup"><span data-stu-id="1ee4c-185">Internal API</span></span> |<span data-ttu-id="1ee4c-186">aigs.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="1ee4c-186">aigs.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="1ee4c-187">aigs1.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="1ee4c-187">aigs1.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="1ee4c-188">aigs2.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="1ee4c-188">aigs2.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="1ee4c-189">aigs3.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="1ee4c-189">aigs3.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="1ee4c-190">aigs4.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="1ee4c-190">aigs4.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="1ee4c-191">aigs5.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="1ee4c-191">aigs5.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="1ee4c-192">aigs6.aisvc.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="1ee4c-192">aigs6.aisvc.visualstudio.com</span></span> |<span data-ttu-id="1ee4c-193">dinamik</span><span class="sxs-lookup"><span data-stu-id="1ee4c-193">dynamic</span></span>|<span data-ttu-id="1ee4c-194">443</span><span class="sxs-lookup"><span data-stu-id="1ee4c-194">443</span></span> |

## <a name="application-insights-analytics"></a><span data-ttu-id="1ee4c-195">Uygulama Öngörüler analizi</span><span class="sxs-lookup"><span data-stu-id="1ee4c-195">Application Insights Analytics</span></span>

| <span data-ttu-id="1ee4c-196">Amaç</span><span class="sxs-lookup"><span data-stu-id="1ee4c-196">Purpose</span></span> | <span data-ttu-id="1ee4c-197">URI</span><span class="sxs-lookup"><span data-stu-id="1ee4c-197">URI</span></span> | <span data-ttu-id="1ee4c-198">IP</span><span class="sxs-lookup"><span data-stu-id="1ee4c-198">IP</span></span> | <span data-ttu-id="1ee4c-199">Bağlantı Noktaları</span><span class="sxs-lookup"><span data-stu-id="1ee4c-199">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1ee4c-200">Analytics portalı</span><span class="sxs-lookup"><span data-stu-id="1ee4c-200">Analytics Portal</span></span> | <span data-ttu-id="1ee4c-201">Analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="1ee4c-201">analytics.applicationinsights.io</span></span> | <span data-ttu-id="1ee4c-202">dinamik</span><span class="sxs-lookup"><span data-stu-id="1ee4c-202">dynamic</span></span> | <span data-ttu-id="1ee4c-203">80,443</span><span class="sxs-lookup"><span data-stu-id="1ee4c-203">80,443</span></span> |
| <span data-ttu-id="1ee4c-204">CDN</span><span class="sxs-lookup"><span data-stu-id="1ee4c-204">CDN</span></span> | <span data-ttu-id="1ee4c-205">applicationanalytics.azureedge.NET</span><span class="sxs-lookup"><span data-stu-id="1ee4c-205">applicationanalytics.azureedge.net</span></span> | <span data-ttu-id="1ee4c-206">dinamik</span><span class="sxs-lookup"><span data-stu-id="1ee4c-206">dynamic</span></span> | <span data-ttu-id="1ee4c-207">80,443</span><span class="sxs-lookup"><span data-stu-id="1ee4c-207">80,443</span></span> |
| <span data-ttu-id="1ee4c-208">Medya CDN</span><span class="sxs-lookup"><span data-stu-id="1ee4c-208">Media CDN</span></span> | <span data-ttu-id="1ee4c-209">applicationanalyticsmedia.azureedge.NET</span><span class="sxs-lookup"><span data-stu-id="1ee4c-209">applicationanalyticsmedia.azureedge.net</span></span> | <span data-ttu-id="1ee4c-210">dinamik</span><span class="sxs-lookup"><span data-stu-id="1ee4c-210">dynamic</span></span> | <span data-ttu-id="1ee4c-211">80,443</span><span class="sxs-lookup"><span data-stu-id="1ee4c-211">80,443</span></span> |

<span data-ttu-id="1ee4c-212">Not: *. Application Insights ekibi tarafından applicationinsights.io etki alanına ait.</span><span class="sxs-lookup"><span data-stu-id="1ee4c-212">Note: *.applicationinsights.io domain is owned by Application Insights team.</span></span>

## <a name="application-insights-azure-portal-extension"></a><span data-ttu-id="1ee4c-213">Application Insights Azure portalı uzantısı</span><span class="sxs-lookup"><span data-stu-id="1ee4c-213">Application Insights Azure Portal Extension</span></span>

| <span data-ttu-id="1ee4c-214">Amaç</span><span class="sxs-lookup"><span data-stu-id="1ee4c-214">Purpose</span></span> | <span data-ttu-id="1ee4c-215">URI</span><span class="sxs-lookup"><span data-stu-id="1ee4c-215">URI</span></span> | <span data-ttu-id="1ee4c-216">IP</span><span class="sxs-lookup"><span data-stu-id="1ee4c-216">IP</span></span> | <span data-ttu-id="1ee4c-217">Bağlantı Noktaları</span><span class="sxs-lookup"><span data-stu-id="1ee4c-217">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1ee4c-218">Uygulama Öngörüler uzantısı</span><span class="sxs-lookup"><span data-stu-id="1ee4c-218">Application Insights Extension</span></span> | <span data-ttu-id="1ee4c-219">stamp2.app.insightsportal.VisualStudio.com</span><span class="sxs-lookup"><span data-stu-id="1ee4c-219">stamp2.app.insightsportal.visualstudio.com</span></span> | <span data-ttu-id="1ee4c-220">dinamik</span><span class="sxs-lookup"><span data-stu-id="1ee4c-220">dynamic</span></span> | <span data-ttu-id="1ee4c-221">80,443</span><span class="sxs-lookup"><span data-stu-id="1ee4c-221">80,443</span></span> |
| <span data-ttu-id="1ee4c-222">Uygulama Insights uzantısını CDN</span><span class="sxs-lookup"><span data-stu-id="1ee4c-222">Application Insights Extension CDN</span></span> | <span data-ttu-id="1ee4c-223">insightsportal prod2 cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="1ee4c-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="1ee4c-224">prod2 asiae cdn.aisvc.visualstudio.com insightsportal</span><span class="sxs-lookup"><span data-stu-id="1ee4c-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="1ee4c-225">insightsportal cdn aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="1ee4c-225">insightsportal-cdn-aimon.applicationinsights.io</span></span> | <span data-ttu-id="1ee4c-226">dinamik</span><span class="sxs-lookup"><span data-stu-id="1ee4c-226">dynamic</span></span> | <span data-ttu-id="1ee4c-227">80,443</span><span class="sxs-lookup"><span data-stu-id="1ee4c-227">80,443</span></span> |

## <a name="application-insights-sdks"></a><span data-ttu-id="1ee4c-228">Uygulama Insights SDK'ları</span><span class="sxs-lookup"><span data-stu-id="1ee4c-228">Application Insights SDKs</span></span>

| <span data-ttu-id="1ee4c-229">Amaç</span><span class="sxs-lookup"><span data-stu-id="1ee4c-229">Purpose</span></span> | <span data-ttu-id="1ee4c-230">URI</span><span class="sxs-lookup"><span data-stu-id="1ee4c-230">URI</span></span> | <span data-ttu-id="1ee4c-231">IP</span><span class="sxs-lookup"><span data-stu-id="1ee4c-231">IP</span></span> | <span data-ttu-id="1ee4c-232">Bağlantı Noktaları</span><span class="sxs-lookup"><span data-stu-id="1ee4c-232">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1ee4c-233">Application Insights JS SDK CDN</span><span class="sxs-lookup"><span data-stu-id="1ee4c-233">Application Insights JS SDK CDN</span></span> | <span data-ttu-id="1ee4c-234">az416426.VO.msecnd.NET</span><span class="sxs-lookup"><span data-stu-id="1ee4c-234">az416426.vo.msecnd.net</span></span> | <span data-ttu-id="1ee4c-235">dinamik</span><span class="sxs-lookup"><span data-stu-id="1ee4c-235">dynamic</span></span> | <span data-ttu-id="1ee4c-236">80,443</span><span class="sxs-lookup"><span data-stu-id="1ee4c-236">80,443</span></span> |
| <span data-ttu-id="1ee4c-237">Uygulama Öngörüler Java SDK'sı</span><span class="sxs-lookup"><span data-stu-id="1ee4c-237">Application Insights Java SDK</span></span> | <span data-ttu-id="1ee4c-238">aijavasdk.BLOB.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="1ee4c-238">aijavasdk.blob.core.windows.net</span></span> | <span data-ttu-id="1ee4c-239">dinamik</span><span class="sxs-lookup"><span data-stu-id="1ee4c-239">dynamic</span></span> | <span data-ttu-id="1ee4c-240">80,443</span><span class="sxs-lookup"><span data-stu-id="1ee4c-240">80,443</span></span> |

## <a name="profiler"></a><span data-ttu-id="1ee4c-241">Profil Oluşturucu</span><span class="sxs-lookup"><span data-stu-id="1ee4c-241">Profiler</span></span>

| <span data-ttu-id="1ee4c-242">Amaç</span><span class="sxs-lookup"><span data-stu-id="1ee4c-242">Purpose</span></span> | <span data-ttu-id="1ee4c-243">URI</span><span class="sxs-lookup"><span data-stu-id="1ee4c-243">URI</span></span> | <span data-ttu-id="1ee4c-244">IP</span><span class="sxs-lookup"><span data-stu-id="1ee4c-244">IP</span></span> | <span data-ttu-id="1ee4c-245">Bağlantı Noktaları</span><span class="sxs-lookup"><span data-stu-id="1ee4c-245">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1ee4c-246">Aracı</span><span class="sxs-lookup"><span data-stu-id="1ee4c-246">Agent</span></span> | <span data-ttu-id="1ee4c-247">Agent.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="1ee4c-247">agent.azureserviceprofiler.net</span></span><br/><span data-ttu-id="1ee4c-248">*. agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="1ee4c-248">*.agent.azureserviceprofiler.net</span></span> | <span data-ttu-id="1ee4c-249">dinamik</span><span class="sxs-lookup"><span data-stu-id="1ee4c-249">dynamic</span></span> | <span data-ttu-id="1ee4c-250">443</span><span class="sxs-lookup"><span data-stu-id="1ee4c-250">443</span></span>
| <span data-ttu-id="1ee4c-251">Portal</span><span class="sxs-lookup"><span data-stu-id="1ee4c-251">Portal</span></span> | <span data-ttu-id="1ee4c-252">Gateway.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="1ee4c-252">gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="1ee4c-253">dinamik</span><span class="sxs-lookup"><span data-stu-id="1ee4c-253">dynamic</span></span> | <span data-ttu-id="1ee4c-254">443</span><span class="sxs-lookup"><span data-stu-id="1ee4c-254">443</span></span>
| <span data-ttu-id="1ee4c-255">Depolama</span><span class="sxs-lookup"><span data-stu-id="1ee4c-255">Storage</span></span> | <span data-ttu-id="1ee4c-256">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="1ee4c-256">*.core.windows.net</span></span> | <span data-ttu-id="1ee4c-257">dinamik</span><span class="sxs-lookup"><span data-stu-id="1ee4c-257">dynamic</span></span> | <span data-ttu-id="1ee4c-258">443</span><span class="sxs-lookup"><span data-stu-id="1ee4c-258">443</span></span>

## <a name="snapshot-debugger"></a><span data-ttu-id="1ee4c-259">Anlık Görüntü Hata Ayıklayıcı</span><span class="sxs-lookup"><span data-stu-id="1ee4c-259">Snapshot Debugger</span></span>

| <span data-ttu-id="1ee4c-260">Amaç</span><span class="sxs-lookup"><span data-stu-id="1ee4c-260">Purpose</span></span> | <span data-ttu-id="1ee4c-261">URI</span><span class="sxs-lookup"><span data-stu-id="1ee4c-261">URI</span></span> | <span data-ttu-id="1ee4c-262">IP</span><span class="sxs-lookup"><span data-stu-id="1ee4c-262">IP</span></span> | <span data-ttu-id="1ee4c-263">Bağlantı Noktaları</span><span class="sxs-lookup"><span data-stu-id="1ee4c-263">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1ee4c-264">Aracı</span><span class="sxs-lookup"><span data-stu-id="1ee4c-264">Agent</span></span> | <span data-ttu-id="1ee4c-265">ppe.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="1ee4c-265">ppe.azureserviceprofiler.net</span></span><br/><span data-ttu-id="1ee4c-266">*. ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="1ee4c-266">*.ppe.azureserviceprofiler.net</span></span> | <span data-ttu-id="1ee4c-267">dinamik</span><span class="sxs-lookup"><span data-stu-id="1ee4c-267">dynamic</span></span> | <span data-ttu-id="1ee4c-268">443</span><span class="sxs-lookup"><span data-stu-id="1ee4c-268">443</span></span>
| <span data-ttu-id="1ee4c-269">Portal</span><span class="sxs-lookup"><span data-stu-id="1ee4c-269">Portal</span></span> | <span data-ttu-id="1ee4c-270">ppe.Gateway.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="1ee4c-270">ppe.gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="1ee4c-271">dinamik</span><span class="sxs-lookup"><span data-stu-id="1ee4c-271">dynamic</span></span> | <span data-ttu-id="1ee4c-272">443</span><span class="sxs-lookup"><span data-stu-id="1ee4c-272">443</span></span>
| <span data-ttu-id="1ee4c-273">Depolama</span><span class="sxs-lookup"><span data-stu-id="1ee4c-273">Storage</span></span> | <span data-ttu-id="1ee4c-274">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="1ee4c-274">*.core.windows.net</span></span> | <span data-ttu-id="1ee4c-275">dinamik</span><span class="sxs-lookup"><span data-stu-id="1ee4c-275">dynamic</span></span> | <span data-ttu-id="1ee4c-276">443</span><span class="sxs-lookup"><span data-stu-id="1ee4c-276">443</span></span>
