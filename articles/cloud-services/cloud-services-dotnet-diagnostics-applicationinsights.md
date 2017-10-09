---
title: aaaTroubleshoot bulut Application Insights kullanarak Hizmetleri | Microsoft Docs
description: "Application Insights tooprocess Azure Tanılama verileri kullanarak tootroubleshoot bulut hizmeti nasıl sorunlar hakkında bilgi edinin."
services: cloud-services
documentationcenter: .net
author: sbtron
manager: timlt
editor: tysonn
ms.assetid: e93f387b-ef29-4731-ae41-0676722accb6
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: saurabh
ms.openlocfilehash: 972924d9e6d1fe33d5c19b006d482de52ffb0ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-services-using-application-insights"></a>Bulut Hizmetleri Application Insights kullanarak sorun giderme
İle [Azure SDK 2.8](https://azure.microsoft.com/downloads/) ve Azure tanılama uzantısını 1.5, bulut hizmetiniz için Azure Tanılama verileri gönderebilir doğrudan tooApplication Öngörüler. Hello Azure tanılama tarafından toplanan günlüklerini&mdash;uygulama günlükleri, Windows olay günlükleri, ETW günlükleri ve performans sayaçları dahil olmak üzere&mdash;tooApplication Öngörüler gönderilebilir. Ardından bu bilgileri hello Application Insights portalında UI görselleştirebilirsiniz. Daha sonra hello Application Insights SDK'sı tooget Öngörüler ölçümleri ve uygulamanın yanı sıra hello sistem ve Azure tanılama gelen altyapı düzeyinde veri alınması günlükleri kullanabilirsiniz.

## <a name="configure-azure-diagnostics-toosend-data-tooapplication-insights"></a>Azure tanılama toosend veri tooApplication Öngörüler yapılandırın
Bu adımları tooset, bulut hizmeti projesi toosend Azure Tanılama verileri tooApplication Öngörüler yukarı izleyin.

1. Visual Studio Çözüm Gezgini'nde, bir role sağ tıklayın ve seçin **özellikleri** tooopen hello rol Tasarımcısı.

    ![Çözüm Gezgini rolü özellikleri][1]

2. Merhaba, **tanılama** hello rol Tasarımcısı, select hello bölümünü **tanılama veri tooApplication Öngörüler Gönder** seçeneği.

    ![Rol Tasarımcısı tanılama veri tooapplication Öngörüler Gönder][2]

3. Açılır hello iletişim kutusunda, toosend hello Azure Tanılama verileri istediğiniz hello Application Insights kaynağı seçin. Merhaba iletişim kutusu tooselect aboneliğiniz mevcut bir Application Insights kaynağı izin verir veya toomanually Application Insights kaynağı için bir izleme anahtarını belirtin. Application Insights kaynağı oluşturma hakkında daha fazla bilgi için bkz: [yeni bir Application Insights kaynağı oluşturma](../application-insights/app-insights-create-new-resource.md).

    ![Uygulama ınsights kaynağını seçin][3]

    Merhaba Application Insights kaynağı ekledikten sonra bu kaynak için hello izleme anahtarını hello ada sahip bir hizmet yapılandırma ayarı olarak depolanır **appınsıghts_ınstrumentatıonkey**. Her bir hizmet yapılandırması veya ortamı için bu yapılandırma ayarı değiştirebilirsiniz. toodo hello bu nedenle, farklı bir yapılandırma seçin **hizmet yapılandırmasını** listesi ve bu yapılandırma için yeni bir izleme anahtarını belirtin.

    ![Hizmet yapılandırmasını seçin][4]

    Merhaba **appınsıghts_ınstrumentatıonkey** yapılandırma ayarı, Visual Studio tooconfigure hello tanılama uzantısını hello uygun bilgilerle Application Insights kaynağı yayımlama sırasında tarafından kullanılır. Merhaba yapılandırma ayarı farklı hizmet yapılandırması için farklı izleme anahtarı tanımlamanın uygun bir yoludur. Visual Studio bu ayarı çevirin ve hello tanılama uzantı genel yapılandırması hello sırasında yerleştirme işlemi yayımlayın. PowerShell ile Merhaba tanılama uzantısını yapılandırma toosimplify hello işlemi, Visual Studio'dan hello paket çıktı hello genel yapılandırması XML hello uygun Application Insights izleme anahtarı ile de içerir. Merhaba ortak yapılandırma dosyaları hello Uzantıları klasöründe oluşturulur ve hello desenler izleyen *PaaSDiagnostics.&lt; RoleName&gt;. PubConfig.xml*. Tüm PowerShell tabanlı dağıtımların bu deseni toomap her yapılandırma tooa rolünü kullanabilirsiniz.

4) hello Azure Tanılama Aracı tooApplication Öngörüler, toplanan tüm performans sayaçları ve hata düzeyi günlükleri tooconfigure Azure tanılama toosend etkinleştirmek hello **tanılama veri tooApplication Öngörüler Gönder** seçeneği. 

    Toofurther istiyorsanız tooApplication Öngörüler hangi verilerin gönderileceğini yapılandırın, hello el ile düzenlemeniz gerekir *diagnostics.wadcfgx* her rol için dosya. Bkz: [yapılandırma Azure tanılama toosend veri tooApplication Insights](#configure-azure-diagnostics-to-send-data-to-application-insights) toolearn hello yapılandırmasını el ile güncelleştirme hakkında daha fazla bilgi.

Hello bulut hizmeti yapılandırılmış toosend Azure Tanılama verileri tooapplication Öngörüler olduğunda, onu tooAzure normalde hello Azure tanılama uzantısını etkinleştirildiğinden emin dağıtabilirsiniz. Daha fazla bilgi için bkz: [Visual Studio kullanarak bir bulut hizmeti yayımlama](../vs-azure-tools-publishing-a-cloud-service.md).  

## <a name="viewing-azure-diagnostics-data-in-application-insights"></a>Application Insights'ta Azure Tanılama verileri görüntüleme
Hello Azure tanılama telemetri hello Application Insights kaynağı, bulut hizmeti için yapılandırılmış görünür.

Azure tanılama günlük türleri bu yolla tooApplication Öngörüler kavramları eşlenir:

* Performans sayaçları, Application ınsights'ta özel ölçümleri olarak görüntülenir.
* Windows olay günlüklerini, izlemeleri ve Application Insights özel olaylar olarak gösterilir.
* Uygulama günlükleri, ETW günlükleri ve herhangi bir tanılama altyapısı günlük izlemelerini Application ınsights'ta olarak gösterilir.

tooview Azure tanılama verilerini Application ınsights'ta hello aşağıdakilerden birini yapın:

* Kullanım [ölçüm Gezgini](../application-insights/app-insights-metrics-explorer.md) toovisualize tüm özel performans sayaçlarını veya Windows olay günlüğü olaylarını farklı türdeki sayar.

    ![Ölçümleri Explorer'da özel ölçümleri][5]

* Kullanım [arama](../application-insights/app-insights-diagnostic-search.md) toosearch Azure tanılama tarafından gönderilen hello izleme günlükleri arasında. İşlenmeyen bir özel durum hello rol toocrash ve Geri Dönüşüm neden olursa, örneğin, hello özel durum hakkında bilgi hello görüntülenir *uygulama* kanalı *Windows olay günlüğü*. Merhaba özel durum toohelp Bul hello hello sorunun nedenini hello tam yığın izlemesi almak ve Windows olay günlüğü hatası hello arama toolook kullanın.

    ![Arama izlemeleri][6]

## <a name="next-steps"></a>Sonraki Adımlar
* [Merhaba Application Insights SDK'sı tooyour bulut hizmeti eklemek](../application-insights/app-insights-cloudservices.md) toosend veri istekleri, özel durumlar, bağımlılıklar ve uygulamanızdan herhangi özel telemetri hakkında. Hello Azure Tanılama verileri, uygulama ve sistem, tam görünümünü almak bu bilgileri bir araya geldiğinde tümünde aynı uygulama Insight kaynak hello.  

<!--Image references-->
[1]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/solution-explorer-properties.png
[2]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-sendtoappinsights.png
[3]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/select-appinsights-resource.png
[4]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-appinsights-serviceconfig.png
[5]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/metrics-explorer-custom-metrics.png
[6]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/search-windowseventlog-error.png
