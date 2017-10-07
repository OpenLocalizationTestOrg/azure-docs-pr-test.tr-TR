---
title: "Azure Hizmetleri - platformlar arası CLI aaaCreate uyarıları | Microsoft Docs"
description: "Belirttiğiniz hello koşullar karşılandığında tetikleyici e-postalar, bildirimler, Web siteleri URL'leri (Web kancaları) ya da Otomasyon çağırın."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 5c6a2d27-7dcc-4f89-8752-9bb31b05ff35
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: robb
ms.openlocfilehash: e53701e5377a415038a69fbd32f1e5fc5fe99be9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a>Ölçüm uyarılar için Azure services - Azure İzleyicisi'nde, platformlar arası CLI oluşturabilir.
> [!div class="op_single_selector"]
> * [Portal](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Genel Bakış
Bu makale size nasıl tooset kullanarak Azure ölçüm uyarıları hello platformlar arası komut satırı arabirimi (CLI) gösterir.

> [!NOTE]
> Azure İzleyicisi "Azure Öngörüler" olarak adlandırılmıştı için hello yeni 25 Eylül 2016'ya kadar adıdır. Ancak, başlangıç ad alanları ve bu nedenle aşağıdaki hello komutları hala hello "ınsights" içeriyor.
>
>

İzleme ölçümlerini ya da olayları, Azure hizmetlerinizi göre bir uyarı alabilirsiniz.

* **Ölçüm değerleri** - hello belirtilen ölçüm hello değeri herhangi bir yönde atadığınız bir eşik kestiği olduğunda uyarı tetikler. Diğer bir deyişle, her ikisi de tetikler hello koşul karşılanır ilk ve ardından daha sonra ne zaman, koşul artık karşılanıp zaman.    
* **Etkinlik günlüğü olaylarını** -bir uyarıyı tetiklemek *her* olay veya yalnızca belirli bir olaylar oluşur. Etkinlik günlüğü Uyarıları hakkında daha fazla toolearn [burayı tıklatın](monitoring-activity-log-alerts.md)

Tetikler olduğunda bir uyarı ölçüm toodo hello aşağıdaki yapılandırabilirsiniz:

* e-posta bildirimleri toohello hizmet yöneticisini ve ortak Yöneticiler Gönder
* e-posta, belirttiğiniz tooadditional e-postalar gönderin.
* bir Web kancası çağırın
* bir Azure runbook'tan (yalnızca Azure portal şu anda hello) yürütülmesini Başlat

Yapılandırma ve kullanma ölçüm uyarı kuralları hakkında bilgi alın

* [Azure portal](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [komut satırı arabirimi (CLI)](insights-alerts-command-line-interface.md)
* [Azure monitör REST API'si](https://msdn.microsoft.com/library/azure/dn931945.aspx)

Bir komut yazarak komutlar için Yardım her zaman alabilir ve koyma - hello sonunda yardımcı olur. Örneğin:

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-hello-cli"></a>Merhaba CLI kullanarak uyarı kuralları oluşturma
1. Merhaba önkoşulları ve oturum açma tooAzure gerçekleştirin. Bkz: [Azure İzleyici CLI örnekleri](insights-cli-samples.md). Kısacası, hello CLI yükleyin ve bu komutları çalıştırın. Bunlar, oturum açmış almak için hangi aboneliğe ve toorun Azure İzleyici komutları hazırlama göster.

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. toolist var olan bir kaynak grubu üzerinde kurallarıyla form aşağıdaki hello **uyarıları kural listesi azure Öngörüler** *[Seçenekler] &lt;kaynak grubu&gt;*

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. bir kural toocreate toohave birkaç önemli bilgi parçasından önce gerekir.
  * Merhaba **kaynak kimliği** hello kaynak için bir uyarı tooset istiyor
  * Merhaba **ölçüm tanımlarını** kaynağı için kullanılabilir

     Tek yönlü tooget hello kaynak kimliği toouse hello Azure portal ' dir. Merhaba kaynak zaten oluşturulmuş olduğu varsayılarak, hello Portalı'nda seçin. Merhaba sonraki dikey penceresinde, ardından *özellikleri* hello altında *ayarları* bölümü. Merhaba *kaynak kimliği* hello sonraki dikey penceresinde bir alandır. Başka bir yoldur toouse hello [Azure kaynak Gezgini](https://resources.azure.com/).

     Bir web uygulaması için bir örnek kaynak kimliği

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     tooget hello kullanılabilir Ölçümler ve bu ölçümleri hello önceki kaynak Örneğin, CLI komutu aşağıdaki kullanım hello için birim listesi:  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     *PT1M* hello ayrıntı hello kullanılabilir ölçüm (1 dakikalık aralıklarla) kalıyor. Farklı ayrıntı kullanarak farklı ölçüm seçenekler sunar.
4. toocreate bir ölçüm tabanlı uyarı kuralı, hello form aşağıdaki komutu kullanın:

    **Uyarı kuralı ölçüm kümesi azure Öngörüler** *[Seçenekler] &lt;ruleName&gt; &lt;konumu&gt; &lt;resourceGroup&gt; &lt;pencereboyutu&gt; &lt;işleci&gt; &lt;eşik&gt; &lt;uç noktası Targetresourceıd&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*

    bir web sitesi kaynakta bir uyarı örnek ayarlar aşağıdaki hello. 5 dakikada bir ve yeniden zaman 5 dakika boyunca hiçbir trafik aldığı için herhangi bir trafik tutarlı bir şekilde aldığı zaman hello uyarı tetikler.

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. Ölçüm bir uyarı oluşturulduğunda toocreate Web kancası veya gönderme e-posta, hello e-posta ve/veya Web kancalarını önce oluşturun. Merhaba kural hemen oluşturmak daha sonra. Web kancası veya e-posta kuralları hello CLI kullanarak önceden oluşturulmuş ilişkilendiremezsiniz.

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. Uyarılarınızı düzgün bir şekilde tek bir kuralı bakarak oluşturulduğunu doğrulayabilirsiniz.

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. toodelete kuralları, bir komut hello formunun kullanın:

    **Uyarı kuralı silme Öngörüler** [Seçenekler] &lt;resourceGroup&gt; &lt;ruleName&gt;

    Bu komutlar, bu makalede daha önce oluşturduğunuz hello kuralları silin.

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a>Sonraki adımlar
* [Azure izleme genel bir bakış elde](monitoring-overview.md) hello toplamak ve izlemek bilgi türlerini de dahil olmak üzere.
* Daha fazla bilgi edinmek [Web kancalarını uyarıları yapılandırma](insights-webhooks-alerts.md).
* Daha fazla bilgi edinmek [etkinlik günlüğü olayları uyarıları yapılandırma](monitoring-activity-log-alerts.md).
* Daha fazla bilgi edinmek [Azure Automation Runbook](../automation/automation-starting-a-runbook.md).
* Alma bir [tanılama günlüklerinin toplanması genel bakış](monitoring-overview-of-diagnostic-logs.md) toocollect ayrıntılı hizmetinizi yüksek sıklıkta ölçümleri.
* Alma bir [ölçümleri toplama genel bakış](insights-how-to-customize-monitoring.md) toomake hizmetinizi kullanılabilir ve yanıt verebilir durumda olduğundan emin.
