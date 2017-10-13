---
title: "Application Insights: programlama dilleri, platformlar ve tümleştirmeler| Microsoft Belgeleri"
description: "Application Insights için programlama dilleri, platformlar ve tümleştirmeler bulunmaktadır"
services: application-insights
documentationcenter: 
author: OlegAnaniev-MSFT
manager: carmonm
ms.assetid: 974db106-54ff-4318-9f8b-f7b3a869e536
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/01/2016
ms.author: bwren
ms.openlocfilehash: d49ad2ff584f42c0e4732a5cff60d23cdf631512
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="developer-analytics-languages-platforms-and-integrations"></a>Geliştirici analizleri: programlama dilleri, platformlar ve tümleştirmeler
Bu öğeler, bildiğimiz [Application Insights](app-insights-overview.md) uygulamalardır. Bunlardan bazıları üçüncü taraflar aracılığıyla sunulur.

## <a name="languages---officially-supported-by-application-insights-team"></a>Application Insights ekibi tarafından resmi olarak desteklenen programlama dilleri
* [C#|VB (.NET)](app-insights-asp-net.md)
* [Java](app-insights-java-get-started.md)
* [JavaScript web sayfaları](app-insights-javascript.md)
* [Node.JS](app-insights-nodejs.md)

## <a name="languages---community-supported"></a>Topluluk tarafından desteklenen programlama dilleri
* [PHP](https://github.com/Microsoft/ApplicationInsights-PHP)
* [Python](https://pypi.python.org/pypi/applicationinsights/0.1.0)
* [Ruby](https://rubygems.org/gems/application_insights)
* [Diğer her şey](#projects)

## <a name="platforms-and-frameworks"></a>Platformlar ve altyapıları
* [Angular](https://www.npmjs.com/package/angular-applicationinsights)
* [ASP.NET](app-insights-asp-net.md)
* [ASP.NET - zaten canlı olan uygulamalar için](app-insights-monitor-performance-live-website-now.md)
* [ASP.NET Core](app-insights-asp-net-core.md)
* [Android](https://github.com/Microsoft/ApplicationInsights-Android) (HockeyApp)
* [Azure Web Apps](app-insights-azure-web-apps.md)
* [Azure Bulut Hizmetleri](app-insights-cloudservices.md)&#151;hem web hem de çalışan rolleri dahil
* [Azure İşlevleri](https://github.com/christopheranderson/azure-functions-app-insights-sample)
* [Docker](app-insights-docker.md)
* [Glimpse](https://azure.microsoft.com/blog/glimpse-application-insights/)
* [iOS](https://github.com/Microsoft/ApplicationInsights-iOS) (HockeyApp)
* [J2EE](app-insights-java-get-started.md)
* [J2EE - zaten canlı olan uygulamalar için](app-insights-java-live.md)
* [Mac OS X uygulaması](https://support.hockeyapp.net/kb/client-integration-ios-mac-os-x-tvos/hockeyapp-for-mac-os-x) (HockeyApp)
* [Node.JS](https://www.npmjs.com/package/applicationinsights)
* [OSX](https://github.com/Microsoft/ApplicationInsights-OSX)
* [Spring](http://joe.blog.freemansoft.com/2015/12/enabling-microsoft-application-insight.html)
* [Evrensel Windows uygulaması](https://support.hockeyapp.net/kb/client-integration-windows-and-windows-phone/how-to-create-an-app-for-uwp) (HockeyApp)
* [WCF](https://github.com/Microsoft/ApplicationInsights-SDK-Labs/blob/master/WCF/readme.md)
* [Windows Phone 8 ve 8.1 uygulaması](https://support.hockeyapp.net/kb/client-integration-windows-and-windows-phone/hockeyapp-for-windows-phone-silverlight-apps-80-and-81) (HockeyApp)
* [Windows Presentation Foundation uygulaması](https://support.hockeyapp.net/kb/client-integration-windows-and-windows-phone/hockeyapp-for-windows-wpf-apps) (HockeyApp)
* [Windows masaüstü uygulamaları, hizmetleri ve çalışan rolleri](app-insights-windows-desktop.md)
* [Diğer her şey](#projects)

## <a name="logging-frameworks"></a>Günlük altyapıları
* [Log4Net, NLog veya System.Diagnostics.Trace](app-insights-diagnostic-search.md)
* [Java, Log4J veya Logback](app-insights-java-trace-logs.md)
* [Semantik Günlük (SLAB)](https://github.com/fidmor89/SLAB_AppInsights) - [Semantik Günlük Uygulama Bloğu](https://msdn.microsoft.com/library/dn440729.aspx) ile tümleşir
* [Bulut tabanlı yük testi](http://blogs.msdn.com/b/visualstudioalm/archive/2015/07/30/getting-application-insights-counters-with-cloud-based-load-testing.aspx)
* [LogStash eklentisi](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-output-applicationinsights)
* [OMS Log Analytics](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/)
* [Logary](https://www.nuget.org/packages/Logary.Targets.AppInsights/)

## <a name="content-management-systems"></a>İçerik Yönetim Sistemleri
* [Concrete](https://github.com/fidmor89/appInsights-Concrete)
* [Drupal](https://github.com/fidmor89/AppInsights-Drupal)
* [Joomla](https://github.com/fidmor89/AppInsights-Joomla)
* [Orchard](https://azure.microsoft.com/blog/integrating-application-insights-into-a-modular-cms-and-a-multi-tenant-public-saas/preview/)
* [SharePoint](app-insights-sharepoint.md)
* [WordPress](https://wordpress.org/plugins/application-insights/)

## <a name="export-and-data-analysis"></a>Dışarı Aktarma ve Veri Analizi
* [Alooma](https://www.alooma.com/blog/application-insights-amazon-redshift)
* [Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx)
* [Akış Analizi](app-insights-export-power-bi.md)

## <a name="projects"></a>Kendi SDK'nizi oluşturun
Programlama diliniz veya platformunuz için henüz bir SDK yoksa belki de bir SDK oluşturmanızın zamanı gelmiştir. [GitHub’da Application Insights SDK projesi](https://github.com/Microsoft/AppInsights-Home) altında listelenen mevcut SDK kodlarını gözden geçirin.
