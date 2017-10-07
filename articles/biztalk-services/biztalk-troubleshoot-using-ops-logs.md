---
title: "İşlem günlükleri kullanarak aaaTroubleshoot BizTalk Services | Microsoft Docs"
description: "BizTalk Services işlem günlükleri kullanarak sorun giderin. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 1081a9c6-58cc-4a76-8ac8-11e5e7a6ea27
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 102779ed6e29784f190c28e4102a7d9670614914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-troubleshoot-using-operation-logs"></a>BizTalk Services: işlem günlükleri kullanarak sorun giderme

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="what-are-hello-operation-logs"></a>Merhaba işlem günlükleri nelerdir
İşlem günlükleri bir özelliktir Yönetim Hizmetleri hello tooview geçmiş günlükleri, BizTalk Services de dahil olmak üzere Azure hizmetlerinizi üzerinde gerçekleştirilen işlemlerinin sağlar ve klasik Azure portalı içinde kullanılabilir. Bu tooview geçmiş verileri sağlar ilgili BizTalk hizmeti aboneliğinizi 180 gün'a kadar toomanagement işlemleri.

> [!NOTE]
> Bu özellik yalnızca günlükleri hello hizmet başlatıldığı gibi yönetim işlemlerini BizTalk Services için desteklenen en fazla, vb. yakalar. Bu tür işlemler bunlar hello Klasik Azure portalı veya hello kullanarak gerçekleştirilen yedeklemiş izlenir [BizTalk hizmeti REST API'leri](http://msdn.microsoft.com/library/azure/dn232347.aspx). Yönetim Hizmetleri kullanılarak izlenen operations tam bir listesi için bkz: [Operations izlenen kullanarak Azure Yönetim Hizmetleri](#bizops).<br/><br/>
> Bu etkinlikler ilgili tooBizTalk (örneğin, ileti. köprüleri vb. tarafından işlenen) hizmeti çalışma zamanı için hello günlüklerini yakalamaz. Bu günlükleri, tooview kullanım hello hello BizTalk Services Portalı'ndan izleme görünümü. Daha fazla bilgi için bkz: [izleme iletileri](http://msdn.microsoft.com/library/azure/hh949805.aspx).
> 
> 

## <a name="view-biztalk-services-operation-logs"></a>İşlem günlükleri BizTalk Services görünümü
1. Hello Klasik Azure portalı, seçin **Yönetim Hizmetleri**ve ardından hello **işlem günlükleri** sekmesi.
2. Merhaba günlükleri abonelik, tarih aralığı, hizmet türüne (örneğin, BizTalk Services), hizmet adı veya hello işleminin (başarılı, başarısız) durumu gibi farklı parametreler göre filtreleyebilirsiniz.
3. Select hello onay işareti tooview hello listesi filtrelenir. Merhaba aşağıdaki resimde gösterilmiştir etkinlikleri ilgili tootestbiztalkservice: ![işlem günlükleri görüntüleme][ViewLogs] 
4. belirli bir işlemi hakkında daha fazla tooview hello satır seçip'ı tıklatın **ayrıntıları** hello altındaki hello görev çubuğundaki.

## <a name="bizops"></a>Azure Yönetim Hizmetleri'ni kullanarak izlenen işlemleri
Merhaba aşağıdaki tabloda hello Azure Yönetimi hizmetlerini kullanarak izlenen hello işlemleri listeler:

| İşlem adı | Görev |
| --- | --- |
| CreateBizTalkService |İşlemi toocreate yeni bir BizTalk hizmeti |
| DeleteBizTalkService |İşlem toodelete BizTalk hizmeti |
| RestartBizTalkService |İşlem toorestart BizTalk hizmeti |
| StartBizTalkService |İşlem toostart BizTalk hizmeti |
| StopBizTalkService |İşlem toostop BizTalk hizmeti |
| DisableBizTalkService |İşlem toodisable BizTalk hizmeti |
| EnableBizTalkService |İşlem tooenable BizTalk hizmeti |
| BackupBizTalkService |BizTalk hizmeti ayarlama işlemi tooback |
| RestoreBizTalkService |İşlem toorestore belirtilen yedekten bir BizTalk hizmeti |
| SuspendBizTalkService |İşlem toosuspend BizTalk hizmeti |
| ResumeBizTalkService |İşlem tooresume BizTalk hizmeti |
| ScaleBizTalkService |Yukarı veya aşağı işlemi tooscale BizTalk hizmeti |
| ConfigUpdateBizTalkService |BizTalk hizmeti işlemi tooupdate hello yapılandırması |
| ServiceUpdateBizTalkService |İşlemi tooupgrade veya indirgeme BizTalk hizmeti tooa farklı bir sürüm |
| PurgeBackupBizTalkService |Merhaba saklama dönemi dışında hello BizTalk hizmeti işlemi toopurge yedekleri |

## <a name="see-also"></a>Ayrıca Bkz.
* [BizTalk hizmeti yedekleme](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [BizTalk hizmeti yedekten geri yükleyin](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [BizTalk Services: Geliştirici, temel, standart ve Premium sürümler grafiği](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [BizTalk Services: Klasik portalı kullanarak Azure hazırlama](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [BizTalk Services: Durum Grafiğini hazırlama](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [BizTalk Services: Pano, İzleyici ve Ölçek sekmeleri](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [BizTalk Services: Azaltma](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [BizTalk Services: Verenin Adı ve Verenin Anahtarı](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [I Başlat'ı kullanarak Azure BizTalk Services SDK'sı nasıl hello](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[ViewLogs]: ./media/biztalk-troubleshoot-using-ops-logs/Operation-Logs.png

