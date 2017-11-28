---
title: "aaaAzure İzleyicisi iş ortağı tümleştirmeler | Microsoft Docs"
description: "Azure monitörün iş ortakları ve onlarla tümleştirme belgelerine nasıl erişebileceğiniz hakkında bilgi edinin."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 01ee13ac-66fc-4edc-8b0c-32f69b986a26
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/16/2017
ms.author: johnkem
ms.openlocfilehash: df3af300bff702c49b1ce66216bc44670ac11938
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-partner-integrations"></a><span data-ttu-id="ee584-103">Azure İzleyicisi iş ortağı tümleştirmeler</span><span class="sxs-lookup"><span data-stu-id="ee584-103">Azure Monitor partner integrations</span></span>
| <span data-ttu-id="ee584-104">İş Ortakları</span><span class="sxs-lookup"><span data-stu-id="ee584-104">Partners</span></span> |  |  |
| --- | --- | --- |
| <span data-ttu-id="ee584-105">[! [Ortak logosu] [alertlogic-logo] <br/> **AlertLogic**][alertlogic-anchor]</span><span class="sxs-lookup"><span data-stu-id="ee584-105">[![Partner Logo][alertlogic-logo]<br/>**AlertLogic**][alertlogic-anchor]</span></span> | <span data-ttu-id="ee584-106">[! [Ortak logosu] [appdynamics-logo] <br/> **AppDynamics**][appdynamics-anchor]</span><span class="sxs-lookup"><span data-stu-id="ee584-106">[![Partner Logo][appdynamics-logo]<br/>**AppDynamics**][appdynamics-anchor]</span></span> | <span data-ttu-id="ee584-107">[! [Ortak logosu] [atlassian-logo] <br/> **Atlassian**][atlassian-anchor]</span><span class="sxs-lookup"><span data-stu-id="ee584-107">[![Partner Logo][atlassian-logo]<br/>**Atlassian**][atlassian-anchor]</span></span> |
| <span data-ttu-id="ee584-108">[! [Ortak logosu] [circonus-logo] <br/> **Circonus**][circonus-anchor]</span><span class="sxs-lookup"><span data-stu-id="ee584-108">[![Partner Logo][circonus-logo]<br/>**Circonus**][circonus-anchor]</span></span> | <span data-ttu-id="ee584-109">[! [Ortak logosu] [cloudhealth-logo] <br/> **CloudHealth**][cloudhealth-anchor]</span><span class="sxs-lookup"><span data-stu-id="ee584-109">[![Partner Logo][cloudhealth-logo]<br/>**CloudHealth**][cloudhealth-anchor]</span></span> | <span data-ttu-id="ee584-110">[! [Ortak logosu] [cloudmonix-logo] <br/> **CloudMonix**][cloudmonix-anchor]</span><span class="sxs-lookup"><span data-stu-id="ee584-110">[![Partner Logo][cloudmonix-logo]<br/>**CloudMonix**][cloudmonix-anchor]</span></span> |
| <span data-ttu-id="ee584-111">[! [Ortak logosu] [cloudyn-logo] <br/> **Cloudyn**][cloudyn-anchor]</span><span class="sxs-lookup"><span data-stu-id="ee584-111">[![Partner Logo][cloudyn-logo]<br/>**Cloudyn**][cloudyn-anchor]</span></span> | <span data-ttu-id="ee584-112">[! [Ortak logosu] [datadog-logo] <br/> **Datadog**][datadog-anchor]</span><span class="sxs-lookup"><span data-stu-id="ee584-112">[![Partner Logo][datadog-logo]<br/>**Datadog**][datadog-anchor]</span></span> | <span data-ttu-id="ee584-113">[! [Ortak logosu] [dynatrace-logo] <br/> **Dynatrace**][dynatrace-anchor]</span><span class="sxs-lookup"><span data-stu-id="ee584-113">[![Partner Logo][dynatrace-logo]<br/>**Dynatrace**][dynatrace-anchor]</span></span> |
| <span data-ttu-id="ee584-114">[! [Ortak logosu] [newrelic-logo] <br/> **NewRelic**][newrelic-anchor]</span><span class="sxs-lookup"><span data-stu-id="ee584-114">[![Partner Logo][newrelic-logo]<br/>**NewRelic**][newrelic-anchor]</span></span> | <span data-ttu-id="ee584-115">[! [Ortak logosu] [opsgenie-logo] <br/> **OpsGenie**][opsgenie-anchor]</span><span class="sxs-lookup"><span data-stu-id="ee584-115">[![Partner Logo][opsgenie-logo]<br/>**OpsGenie**][opsgenie-anchor]</span></span> | <span data-ttu-id="ee584-116">[! [Ortak logosu] [pagerduty-logo] <br/> **PagerDuty**][pagerduty-anchor]</span><span class="sxs-lookup"><span data-stu-id="ee584-116">[![Partner Logo][pagerduty-logo]<br/>**PagerDuty**][pagerduty-anchor]</span></span> |
| <span data-ttu-id="ee584-117">[! [Ortak logosu] [sciencelogic-logo] <br/> **ScienceLogic**][sciencelogic-anchor]</span><span class="sxs-lookup"><span data-stu-id="ee584-117">[![Partner Logo][sciencelogic-logo]<br/>**ScienceLogic**][sciencelogic-anchor]</span></span> | <span data-ttu-id="ee584-118">[! [Ortak logosu] [splunk-logo] <br/> **Splunk**][splunk-anchor]</span><span class="sxs-lookup"><span data-stu-id="ee584-118">[![Partner Logo][splunk-logo]<br/>**Splunk**][splunk-anchor]</span></span> | <span data-ttu-id="ee584-119">[! [Ortak logosu] [sumologic-logo] <br/> **Sumo mantığı**][sumologic-anchor]</span><span class="sxs-lookup"><span data-stu-id="ee584-119">[![Partner Logo][sumologic-logo]<br/>**Sumo Logic**][sumologic-anchor]</span></span> | |

## <a name="alertlogic-log-manager"></a><span data-ttu-id="ee584-120">AlertLogic Günlük Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="ee584-120">AlertLogic Log Manager</span></span>
<span data-ttu-id="ee584-121">Uyarı mantığı Günlük Yöneticisi güvenlik analizi ve saklama hello Azure etkinlik günlüğü hello Azure İzleyici API aracılığıyla da dahil olmak üzere, VM, uygulama ve Azure platformu günlüklerini toplar.</span><span class="sxs-lookup"><span data-stu-id="ee584-121">Alert Logic Log Manager collects VM, Application, and Azure platform logs for security analysis and retention, including hello Azure Activity Log via hello Azure Monitor API.</span></span>  <span data-ttu-id="ee584-122">Bu bilgi kullanılan toodetect malfeasance ve karşılamak uyumluluk gereksinimlerine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="ee584-122">This information is used toodetect malfeasance and meet compliance requirements.</span></span>

<span data-ttu-id="ee584-123">[Toohello belgelerine gidin.][alertlogic-doc]</span><span class="sxs-lookup"><span data-stu-id="ee584-123">[Go toohello documentation.][alertlogic-doc]</span></span>

## <a name="appdynamics"></a><span data-ttu-id="ee584-124">AppDynamics</span><span class="sxs-lookup"><span data-stu-id="ee584-124">AppDynamics</span></span>
<span data-ttu-id="ee584-125">AppDynamics uygulama performansı Yönetimi (APM) etkinleştirir uygulama sahipleri toorapidly performans sorunlarını gidermek ve Azure ortamında çalışan kendi uygulamalarını hello performansını en iyi duruma getirme.</span><span class="sxs-lookup"><span data-stu-id="ee584-125">AppDynamics Application Performance Management (APM) enables application owners toorapidly troubleshoot performance bottlenecks and optimize hello performance of their applications running in Azure environment.</span></span> <span data-ttu-id="ee584-126">AppDynamics APM sorunsuz bir şekilde Azure Market ile tümleşik ve İzleyici Azure Cloud Services (PaaS) (web ve çalışan rolleri dahil), sanal makineler (Iaas), Uzak Hizmet Algılama (Microsoft Azure Service Bus), Microsoft Azure kuyruk için kullanılabilir Microsoft Azure uzak Hizmetleri (Azure Blob), Azure kuyruk (Microsoft hizmet veri yolu), veri depolama alanı, Microsoft Azure Blob Depolama.</span><span class="sxs-lookup"><span data-stu-id="ee584-126">AppDynamics APM is seamlessly integrated with Azure Marketplace and available for monitor Azure Cloud Services (PaaS) (Including web & worker roles), Virtual Machines (IaaS), Remote Service Detection (Microsoft Azure Service Bus), Microsoft Azure Queue Microsoft Azure Remote Services (Azure Blob), Azure Queue (Microsoft Service Bus), Data Storage, Microsoft Azure Blob Storage.</span></span>

<span data-ttu-id="ee584-127">[Toohello belgelerine gidin.][appdynamics-doc]</span><span class="sxs-lookup"><span data-stu-id="ee584-127">[Go toohello documentation.][appdynamics-doc]</span></span>

## <a name="atlassian-jira"></a><span data-ttu-id="ee584-128">Atlassian JIRA</span><span class="sxs-lookup"><span data-stu-id="ee584-128">Atlassian JIRA</span></span>
<span data-ttu-id="ee584-129">Azure İzleyici uyarılar JIRA bilet oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee584-129">You can create JIRA tickets on Azure Monitor alerts.</span></span>

<span data-ttu-id="ee584-130">[Toohello belgelerine gidin.][atlassian-doc]</span><span class="sxs-lookup"><span data-stu-id="ee584-130">[Go toohello documentation.][atlassian-doc]</span></span>

## <a name="circonus"></a><span data-ttu-id="ee584-131">Circonus</span><span class="sxs-lookup"><span data-stu-id="ee584-131">Circonus</span></span>
<span data-ttu-id="ee584-132">Circonus mikro izleme ve analiz platformu şirket içi veya SaaS dağıtımı üzerinde oluşturulmuş olur.</span><span class="sxs-lookup"><span data-stu-id="ee584-132">Circonus is a microservices monitoring and analytics platform built for on premises or SaaS deployment.</span></span> <span data-ttu-id="ee584-133">Yalnızca tam olarak automatable API merkezli platformu daha ölçeklenebilir ve güvenilir sistemleri daha izler.</span><span class="sxs-lookup"><span data-stu-id="ee584-133">Its fully automatable API-Centric platform is more scalable and reliable than systems it monitors.</span></span> <span data-ttu-id="ee584-134">DevOps Hello gereksinimleri için geliştirilen Circonus yüzdebirlik tabanlı uyarılar, grafikleri, panoları ve iş iyileştirmeyi etkinleştirme makine öğrenme Intelligence sunar.</span><span class="sxs-lookup"><span data-stu-id="ee584-134">Developed for hello requirements of DevOps, Circonus delivers percentile-based alerts, graphs, dashboards, and machine-learning intelligence that enable business optimization.</span></span> <span data-ttu-id="ee584-135">Microsoft Azure bulut kaynaklarınızın ve gerçek zamanlı uygulamalarında Circonus izler.</span><span class="sxs-lookup"><span data-stu-id="ee584-135">Circonus monitors your Microsoft Azure cloud resources and their applications in real time.</span></span> <span data-ttu-id="ee584-136">Circonus toocollect ve izleme ölçümleri kullanabilirsiniz hello değişkenleri toomeasure kaynaklar ve uygulamalar için istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="ee584-136">You can use Circonus toocollect and track metrics for hello variables you want toomeasure for your resources and applications.</span></span> <span data-ttu-id="ee584-137">Circonus ile sistem çapında görünürlük Azure'nın kaynak kullanımı, uygulama performansı ve işletimsel durumunu elde etmek.</span><span class="sxs-lookup"><span data-stu-id="ee584-137">With Circonus, you gain system-wide visibility into Azure’s resource utilization, application performance, and operational health.</span></span>

<span data-ttu-id="ee584-138">[Toohello belgelerine gidin.][circonus-doc]</span><span class="sxs-lookup"><span data-stu-id="ee584-138">[Go toohello documentation.][circonus-doc]</span></span>

## <a name="cloudhealth"></a><span data-ttu-id="ee584-139">CloudHealth</span><span class="sxs-lookup"><span data-stu-id="ee584-139">CloudHealth</span></span>
<span data-ttu-id="ee584-140">Birleştirme ve bulut platformu yerleşik toosave ciddi zaman ve para ile otomatikleştirin.</span><span class="sxs-lookup"><span data-stu-id="ee584-140">Unite and automate your cloud with a platform built toosave serious time and money.</span></span> <span data-ttu-id="ee584-141">Benzersiz görünürlük, sezgisel en iyi duruma getirme ve Kaya kadar sağlam idare yöntemler CloudHealth bulut Yönetimi tanımlayarak.</span><span class="sxs-lookup"><span data-stu-id="ee584-141">With unparalleled visibility, intuitive optimization and rock-solid governance practices, CloudHealth is redefining cloud management.</span></span> <span data-ttu-id="ee584-142">kuruluşların Hello Cloudhealth platformu sağlar ve MSP'ler toomaximize bulut yatırımlarına dönün ve maliyet, kullanım, performans ve güvenlik emin kararları yapın.</span><span class="sxs-lookup"><span data-stu-id="ee584-142">hello Cloudhealth platform enables enterprises and MSPs toomaximize return on cloud investments and make confident decisions around cost, usage, performance and security.</span></span>

<span data-ttu-id="ee584-143">[Daha fazla bilgi edinin.][cloudhealth-doc]</span><span class="sxs-lookup"><span data-stu-id="ee584-143">[Learn More.][cloudhealth-doc]</span></span>

## <a name="cloudmonix"></a><span data-ttu-id="ee584-144">CloudMonix</span><span class="sxs-lookup"><span data-stu-id="ee584-144">CloudMonix</span></span>
<span data-ttu-id="ee584-145">CloudMonix izleme, otomasyon ve Microsoft Azure platformu için kendini onarma hizmetleri sunar.</span><span class="sxs-lookup"><span data-stu-id="ee584-145">CloudMonix offers monitoring, automation and self-healing services for Microsoft Azure platform.</span></span>

<span data-ttu-id="ee584-146">[Toohello belgelerine gidin.][cloudmonix-doc]</span><span class="sxs-lookup"><span data-stu-id="ee584-146">[Go toohello documentation.][cloudmonix-doc]</span></span>

## <a name="cloudyn"></a><span data-ttu-id="ee584-147">Cloudyn</span><span class="sxs-lookup"><span data-stu-id="ee584-147">Cloudyn</span></span>
<span data-ttu-id="ee584-148">Cloudyn yönetir ve birden çok platform en iyi duruma getirir, karma bulut dağıtımlarını toohelp kuruluşların tam olarak kendi bulut olası unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ee584-148">Cloudyn manages and optimizes multi-platform, hybrid cloud deployments toohelp enterprises fully realize their cloud potential.</span></span> <span data-ttu-id="ee584-149">Kullanım, performans ve maliyet Öngörüler ve tıklatılabilir önerileri için akıllı en iyi duruma getirme ve bulut yönetimi ile birlikte, görünürlük Hello SaaS çözümü sunar.</span><span class="sxs-lookup"><span data-stu-id="ee584-149">hello SaaS solution delivers visibility into usage, performance and cost, coupled with insights and actionable recommendations for smart optimization and cloud governance.</span></span> <span data-ttu-id="ee584-150">Cloudyn doğru geri ödeme ve hiyerarşik maliyet ayırma Yönetimi aracılığıyla sorumluluk sağlar.</span><span class="sxs-lookup"><span data-stu-id="ee584-150">Cloudyn enables accountability through accurate chargeback and hierarchical cost allocation management.</span></span> <span data-ttu-id="ee584-151">Cloudyn Azure izleme ile sipariş tooprovide öngörü tümleşiktir ve işlem yapılabilir önerileri toooptimize Azure dağıtımınız sipariş.</span><span class="sxs-lookup"><span data-stu-id="ee584-151">Cloudyn is integrated with Azure Monitoring in order tooprovide insights and actionable recommendations in order toooptimize your Azure deployment.</span></span>

<span data-ttu-id="ee584-152">[Toohello belgelerine gidin.][cloudyn-doc]</span><span class="sxs-lookup"><span data-stu-id="ee584-152">[Go toohello documentation.][cloudyn-doc]</span></span>

## <a name="datadog"></a><span data-ttu-id="ee584-153">Datadog</span><span class="sxs-lookup"><span data-stu-id="ee584-153">Datadog</span></span>
<span data-ttu-id="ee584-154">Datadog bulut ölçekli uygulamalar için izleme hello dünyanın en önde gelen veri araya getiren sunucuları, veritabanları, Araçlar olduğu ve toopresent tüm yığın birleşik bir görünümünü Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="ee584-154">Datadog is hello world’s leading monitoring service for cloud-scale applications, bringing together data from servers, databases, tools, and services toopresent a unified view of your entire stack.</span></span> <span data-ttu-id="ee584-155">Bu özellikler geliştirme ve Ops takımlar toowork birliğine dayalı olarak sağlayan bir SaaS tabanlı veri analizi platformu tooavoid kapalı kalma süresi, performans sorunlarını gidermek ve o geliştirme emin olun ve dağıtımı döngüleri bitiş saati üzerinde sağlanır.</span><span class="sxs-lookup"><span data-stu-id="ee584-155">These capabilities are provided on a SaaS-based data analytics platform that enables Dev and Ops teams toowork collaboratively tooavoid downtime, resolve performance problems, and ensure that development and deployment cycles finish on time.</span></span> <span data-ttu-id="ee584-156">Datadog ve Azure tümleştirerek toplamak ve ölçümleri, altyapınız genelinde görüntüleyebilir, VM ölçümleri uygulama düzeyi ölçümlerini ile ilişkilendirmek ve dilim ve özellikleri ve özel etiketler herhangi bir bileşimini kullanarak ölçümlerinizi inin.</span><span class="sxs-lookup"><span data-stu-id="ee584-156">By integrating Datadog and Azure, you can collect and view metrics from across your infrastructure, correlate VM metrics with application-level metrics, and slice and dice your metrics using any combination of properties and custom tags.</span></span>

<span data-ttu-id="ee584-157">[Toohello belgelerine gidin.][datadog-doc]</span><span class="sxs-lookup"><span data-stu-id="ee584-157">[Go toohello documentation.][datadog-doc]</span></span>

## <a name="dynatrace"></a><span data-ttu-id="ee584-158">Dynatrace</span><span class="sxs-lookup"><span data-stu-id="ee584-158">Dynatrace</span></span>
<span data-ttu-id="ee584-159">Merhaba Dynatrace OneAgent hello Azure uzantısı mekanizması Azure Vm'leri ve uygulama hizmetleri ile tümleşir.</span><span class="sxs-lookup"><span data-stu-id="ee584-159">hello Dynatrace OneAgent integrates with Azure VMs and App Services via hello Azure extension mechanism.</span></span> <span data-ttu-id="ee584-160">Bu şekilde Dynatrace OneAgent konakları, ağ ve Hizmetleri hakkında performans ölçümleri toplayabilir.</span><span class="sxs-lookup"><span data-stu-id="ee584-160">This way Dynatrace OneAgent can gather performance metrics about hosts, network, and services.</span></span> <span data-ttu-id="ee584-161">Ölçümleri yalnızca görüntüleme yanı sıra Dynatrace ortamları uçtan uca, hello istemci tarafı toohello veritabanı katmanı hareketleri gösteren visualizes.</span><span class="sxs-lookup"><span data-stu-id="ee584-161">Besides just displaying metrics Dynatrace visualizes environments end-to-end, showing transactions from hello client side toohello database layer.</span></span> <span data-ttu-id="ee584-162">AI tabanlı bağıntı sorun ve tam olarak tümleşik kök nedeni-kod ve veritabanı düzeyi Öngörüler yöntemi dahil olmak üzere analizi, olun sorun giderme ve performansı en iyi duruma getirme çok daha kolay.</span><span class="sxs-lookup"><span data-stu-id="ee584-162">AI-based correlation of problems and fully integrated root-cause-analysis, including method level insights into code and database, make troubleshooting and performance optimizations much easier.</span></span>

<span data-ttu-id="ee584-163">[Toohello belgelerine gidin.][dynatrace-doc]</span><span class="sxs-lookup"><span data-stu-id="ee584-163">[Go toohello documentation.][dynatrace-doc]</span></span>

## <a name="newrelic"></a><span data-ttu-id="ee584-164">NewRelic</span><span class="sxs-lookup"><span data-stu-id="ee584-164">NewRelic</span></span>
<span data-ttu-id="ee584-165">[Daha fazla bilgi edinin.][newrelic-doc]</span><span class="sxs-lookup"><span data-stu-id="ee584-165">[Learn more.][newrelic-doc]</span></span>

## <a name="opsgenie"></a><span data-ttu-id="ee584-166">OpsGenie</span><span class="sxs-lookup"><span data-stu-id="ee584-166">OpsGenie</span></span>
<span data-ttu-id="ee584-167">OpsGenie Azure tarafından oluşturulan hello uyarılar için bir dağıtıcı olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="ee584-167">OpsGenie acts as a dispatcher for hello alerts generated by Azure.</span></span> <span data-ttu-id="ee584-168">OpsGenie belirler hello doğru kişilerin toonotify çağrısı zamanlamaları ve çözümler, bunları bildirerek göre e-posta, metin iletisi (SMS), telefon aramaları kullanarak, anında iletme bildirimleri.</span><span class="sxs-lookup"><span data-stu-id="ee584-168">OpsGenie determines hello right people toonotify based on on-call schedules and escalations, by notifying them using email, text messages (SMS), phone calls, push notifications.</span></span> <span data-ttu-id="ee584-169">Yalnızca, Azure algılanan sorunlar için uyarılar oluşturur ve hello doğru kişilerin bunlar üzerinde çalıştığınız OpsGenie sağlar.</span><span class="sxs-lookup"><span data-stu-id="ee584-169">Simply, Azure generates alerts for detected problems, and OpsGenie ensures hello right people are working on them.</span></span>

<span data-ttu-id="ee584-170">[Toohello belgelerine gidin.][opsgenie-doc]</span><span class="sxs-lookup"><span data-stu-id="ee584-170">[Go toohello documentation.][opsgenie-doc]</span></span>

## <a name="pagerduty"></a><span data-ttu-id="ee584-171">PagerDuty</span><span class="sxs-lookup"><span data-stu-id="ee584-171">PagerDuty</span></span>
<span data-ttu-id="ee584-172">PagerDuty, Olay yönetimi çözümü, baştaki hello Azure uyarılar için birinci sınıf destek ölçümleri sağlamıştır.</span><span class="sxs-lookup"><span data-stu-id="ee584-172">PagerDuty, hello leading incident management solution, has provided first-class support for Azure Alerts on metrics.</span></span> <span data-ttu-id="ee584-173">Bugün, PagerDuty artık bildirimleri Azure izleme uyarıları, otomatik ölçeklendirme bildirimleri ve denetim günlüğü olaylarını toplama toonotifications platform düzeyi ölçümlerini Azure Hizmetleri için üzerinde destekler.</span><span class="sxs-lookup"><span data-stu-id="ee584-173">Today, PagerDuty now supports notifications on Azure Monitor Alerts, Autoscale Notifications, and Audit Log Events, in addition toonotifications on platform-level metrics for Azure services.</span></span> <span data-ttu-id="ee584-174">Bu geliştirmeler hello çekirdek Azure platformu artırılmış görünürlük kullanıcılar etkinleştirilirken bir gerçek zamanlı yanıtı için PagerDuty'nın Olay yönetimi özelliklerinden tam anlamıyla tootake verin.</span><span class="sxs-lookup"><span data-stu-id="ee584-174">These enhancements give users increased visibility into hello core Azure Platform while enabling them tootake full advantage of PagerDuty’s incident management capabilities for real-time response.</span></span> <span data-ttu-id="ee584-175">Bizim genişletilmiş Azure tümleştirme kancalarını, hızlı ve kolay kurulum ve özelleştirme için izin verme aracılığıyla mümkün hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="ee584-175">Our expanded Azure integration is made possible via webhooks, allowing for quick and easy set-up and customization.</span></span>

<span data-ttu-id="ee584-176">[Toohello belgelerine gidin.][pagerduty-doc]</span><span class="sxs-lookup"><span data-stu-id="ee584-176">[Go toohello documentation.][pagerduty-doc]</span></span>

## <a name="sciencelogic"></a><span data-ttu-id="ee584-177">ScienceLogic</span><span class="sxs-lookup"><span data-stu-id="ee584-177">ScienceLogic</span></span>
<span data-ttu-id="ee584-178">ScienceLogic hello herhangi teknolojisi, herhangi bir yerden yönetmek için yeni nesil BT hizmeti güvence platformu sunar.</span><span class="sxs-lookup"><span data-stu-id="ee584-178">ScienceLogic delivers hello next generation IT service assurance platform for managing any technology, anywhere.</span></span>  <span data-ttu-id="ee584-179">Bir platform ScienceLogic hello ölçek, güvenlik, otomasyon ve BT kaynaklarını, hizmetleri ve sabit hızda olan uygulamaları yönetme esnekliği gerekli toosimplify hello sürekli genişleyen görev sunar.</span><span class="sxs-lookup"><span data-stu-id="ee584-179">In one platform, ScienceLogic delivers hello scale, security, automation, and resiliency necessary toosimplify hello ever-expanding task of managing IT resources, services, and applications that are in constant motion.</span></span>  <span data-ttu-id="ee584-180">Merhaba ScienceLogic platformu, Microsoft Azure ile Azure API toointerface kullanır.</span><span class="sxs-lookup"><span data-stu-id="ee584-180">hello ScienceLogic platform uses Azure APIs toointerface with Microsoft Azure.</span></span>  <span data-ttu-id="ee584-181">Ne zaman bir şey çalışmıyor ve daha hızlı düzeltebilirsiniz bilmesi ScienceLogic, Azure hizmetlerinizi ve kaynaklarınızı gerçek zamanlı görünürlük sağlar.</span><span class="sxs-lookup"><span data-stu-id="ee584-181">ScienceLogic gives you real-time visibility into your Azure services and resources so you know when something’s not working and can fix it faster.</span></span> <span data-ttu-id="ee584-182">Ayrıca, diğer Bulut ve veri merkezi Sistemlerinizle ve hizmetlerinizi yanı sıra Azure yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee584-182">You can also manage Azure alongside your other clouds and data center systems and services.</span></span>

<span data-ttu-id="ee584-183">[Daha fazla bilgi edinin.][sciencelogic-doc]</span><span class="sxs-lookup"><span data-stu-id="ee584-183">[Learn more.][sciencelogic-doc]</span></span>

## <a name="azure-monitor-add-on-for-splunk"></a><span data-ttu-id="ee584-184">Splunk için Azure İzleyici eklentisi</span><span class="sxs-lookup"><span data-stu-id="ee584-184">Azure Monitor Add-on for Splunk</span></span>
<span data-ttu-id="ee584-185">Merhaba Splunk için Azure İzleyici eklentisi olan [hello Splunkbase burada bulunan](https://splunkbase.splunk.com/app/3534/).</span><span class="sxs-lookup"><span data-stu-id="ee584-185">hello Azure Monitor Add-on for Splunk is [available in hello Splunkbase here](https://splunkbase.splunk.com/app/3534/).</span></span>

<span data-ttu-id="ee584-186">[Toohello belgelerine gidin.][splunk-doc]</span><span class="sxs-lookup"><span data-stu-id="ee584-186">[Go toohello documentation.][splunk-doc]</span></span>

## <a name="sumo-logic"></a><span data-ttu-id="ee584-187">Sumo mantığı</span><span class="sxs-lookup"><span data-stu-id="ee584-187">Sumo Logic</span></span>
<span data-ttu-id="ee584-188">Sumo mantığı bir güvenli, bulut yerel makine veri analizi, gerçek zamanlı, sürekli Intelligence hello tüm uygulama yaşam döngüsü ve yığın üzerinde yapılandırılmış, yarı yapılandırılmış ve yapılandırılmamış verileri teslim etmek hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="ee584-188">Sumo Logic is a secure, cloud-native, machine data analytics service, delivering real-time, continuous intelligence from structured, semi-structured, and unstructured data across hello entire application lifecycle and stack.</span></span> <span data-ttu-id="ee584-189">Merhaba dünya genelindeki 1000'den fazla müşteriler Sumo mantığına hello analizi ve toobuild, çalıştırmak ve modern uygulamalarını ve altyapıları bulut güvenli Öngörüler için kullanır.</span><span class="sxs-lookup"><span data-stu-id="ee584-189">More than 1,000 customers around hello globe rely on Sumo Logic for hello analytics and insights toobuild, run, and secure their modern applications and cloud infrastructures.</span></span> <span data-ttu-id="ee584-190">Sumo mantığı ile müşteriler çok kiracılı, hizmet modeli avantajı tooaccelerate kendi shift toocontinuous yenilik rekabet avantajı, iş değerini ve büyüme artırma kazanır.</span><span class="sxs-lookup"><span data-stu-id="ee584-190">With Sumo Logic, customers gain a multi-tenant, service-model advantage tooaccelerate their shift toocontinuous innovation, increasing competitive advantage, business value, and growth.</span></span>

<span data-ttu-id="ee584-191">[Daha fazla bilgi edinin.][sumologic-doc]</span><span class="sxs-lookup"><span data-stu-id="ee584-191">[Learn more.][sumologic-doc]</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee584-192">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="ee584-192">Next Steps</span></span>
* [<span data-ttu-id="ee584-193">Azure İzleyicisi hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="ee584-193">Learn more about Azure Monitor</span></span>](monitoring-overview.md)
* [<span data-ttu-id="ee584-194">Merhaba REST API kullanarak erişim ölçümleri</span><span class="sxs-lookup"><span data-stu-id="ee584-194">Access metrics using hello REST API</span></span>](monitoring-rest-api-walkthrough.md)
* [<span data-ttu-id="ee584-195">Akış hello etkinlik günlüğü tooa üçüncü taraf hizmeti</span><span class="sxs-lookup"><span data-stu-id="ee584-195">Stream hello Activity Log tooa third party service</span></span>](monitoring-stream-activity-logs-event-hubs.md)
* [<span data-ttu-id="ee584-196">Tanılama günlüklerini tooa üçüncü taraf hizmeti akışı</span><span class="sxs-lookup"><span data-stu-id="ee584-196">Stream Diagnostic Logs tooa third party service</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

<!--Partner Anchors-->
[alertlogic-anchor]: #alertlogic-log-manager "AlertLogic"
[appdynamics-anchor]: #appdynamics "AppDynamics"
[atlassian-anchor]: #atlassian-jira "Atlassian"
[circonus-anchor]: #circonus "Circonus"
[cloudhealth-anchor]: #cloudhealth "CloudHealth"
[cloudmonix-anchor]: #cloudmonix "CloudMonix"
[cloudyn-anchor]: #cloudyn "Cloudyn"
[datadog-anchor]: #datadog "Datadog"
[dynatrace-anchor]: #dynatrace "Dynatrace"
[newrelic-anchor]: #newrelic "NewRelic"
[opsgenie-anchor]: #opsgenie "OpsGenie"
[pagerduty-anchor]: #pagerduty "PagerDuty"
[sciencelogic-anchor]: #sciencelogic "ScienceLogic"
[splunk-anchor]: #azure-monitor-add-on-for-splunk "Splunk"
[sumologic-anchor]: #sumo-logic "Sumo mantığı"

<!--Icon references-->
[alertlogic-logo]: ./media/partner-logos/alertlogic.png
[appdynamics-logo]: ./media/partner-logos/appdynamics.png
[atlassian-logo]: ./media/partner-logos/atlassian.png
[circonus-logo]: ./media/partner-logos/circonus.png
[cloudhealth-logo]: ./media/partner-logos/cloudhealth.png
[cloudmonix-logo]: ./media/partner-logos/cloudmonix.png
[cloudyn-logo]: ./media/partner-logos/cloudyn.png
[datadog-logo]: ./media/partner-logos/datadog.png
[dynatrace-logo]: ./media/partner-logos/dynatrace.png
[newrelic-logo]: ./media/partner-logos/newrelic.png
[opsgenie-logo]: ./media/partner-logos/opsgenie.png
[pagerduty-logo]: ./media/partner-logos/pagerduty.png
[sciencelogic-logo]: ./media/partner-logos/sciencelogic.png
[splunk-logo]: ./media/partner-logos/splunk.png
[sumologic-logo]: ./media/partner-logos/sumologic.png

<!--Partner Documentation-->
[alertlogic-doc]: https://docs.alertlogic.com/userGuides/log-manager-collection-sources.htm "AlertLogic belgeleri."
[appdynamics-doc]: https://www.appdynamics.com/net/azure/ "AppDynamics belgeleri."
[atlassian-doc]: https://azure.microsoft.com/blog/automated-notifications-from-azure-monitor-for-atlassian-jira/
[circonus-doc]: https://support.circonus.com/support/solutions/articles/24000013515-azure-integration 
[cloudhealth-doc]: https://www.cloudhealthtech.com/azure
[cloudmonix-doc]: http://cloudmonix.com/features/azure-management/ "CloudMonix giriş."
[cloudyn-doc]: https://www.cloudyn.com/azure-monitoring "Cloudyn giriş."
[datadog-doc]: http://docs.datadoghq.com/integrations/azure/ "Datadog belgeleri."
[dynatrace-doc]: https://help.dynatrace.com/infrastructure-monitoring/paas/how-do-i-monitor-microsoft-azure-web-apps/ "Dynatrace belgeleri."
[newrelic-doc]: https://newrelic.com/azure "NewRelic belgeleri."
[opsgenie-doc]: https://www.opsgenie.com/docs/integrations/azure-integration "OpsGenie belgeleri."
[pagerduty-doc]: https://www.pagerduty.com/docs/guides/azure-integration-guide/ "PagerDuty belgeleri."
[sciencelogic-doc]: https://www.sciencelogic.com/product/technologies/microsoft/azure "ScienceLogic belgeleri."
[splunk-doc]: https://github.com/Microsoft/AzureMonitorAddonForSplunk/wiki/Azure-Monitor-Addon-For-Splunk "Splunk belgeleri."
[sumologic-doc]: https://www.sumologic.com/azure "SumoLogic belgeleri."
