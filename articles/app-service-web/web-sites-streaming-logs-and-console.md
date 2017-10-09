---
title: "aaaStreaming günlükleri ve konsol"
description: "Akış günlükleri ve konsoluna genel bakış"
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: 3e50a287-781b-4c6a-8c53-eec261889d7a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/12/2016
ms.author: byvinyal
ms.openlocfilehash: bb4b8ce5358da12041e164dfff8f43790dd67924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-logs-and-hello-console"></a>Akış günlükleri ve hello konsol
## <a name="streaming-logs"></a>Akış günlükleri
Merhaba **Azure portal** izleme olayları görüntülemenize olanak sağlayan bir tümleşik akış Günlük Görüntüleyici sağlar, **uygulama hizmeti** gerçek zamanlı uygulamaları.  

Bu özelliği ayarlama birkaç basit adımı gerektirir:

* Kodunuzda izlemeleri yazma
* Uygulamayı etkinleştir **tanılama günlüklerini** uygulamanız için
* Görünüm hello hello yerleşik akıştan **akış günlükleri** hello kullanıcı Arabiriminde **Azure portal**.

### <a name="how-toowrite-traces-in-your-code"></a>Kodunuzda toowrite nasıl izlediğini
Kodunuzda izlemeleri yazarken kolaydır.  C# kod aşağıdaki hello yazma olarak kadar kolaydır:

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

Merhaba izleme sınıfı hello System.Diagnostics ad alanında yaşar.

Bir node.js uygulamasında bu kod yazabilirsiniz tooachieve hello aynı sonucu:

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-tooenable-and-view-hello-streaming-logs"></a>Akış günlükleri nasıl tooenable ve görünüm hello
![][BrowseSitesScreenshot]Tanılama bir uygulama başına temelinde etkinleştirilir. Bu özelliği tooenable istediğiniz toohello site göz atarak başlayın.  

![][DiagnosticsLogs]Ayarlar menüsünden toohello kaydırarak **izleme** bölümünde ve tıklayın **(1) tanılama günlükleri**. Ardından **(2) etkinleştir** **uygulama günlüğü (dosya sistemi)** veya **uygulama günlüğü (blob)** hello **düzeyi** seçeneği hello değiştirmenize olanak sağlar izlemeler toocapture önem derecesi. Yalnızca tooget hello özelliğiyle tanıdık çalışıyorsanız, hello çok düzeyi**ayrıntılı** tooensure tüm izleme deyimleri toplanır.

' I tıklatın **KAYDETMEK** hello hello dikey ve en üstündeki hazır tooview günlükleri demektir.

> [!NOTE]
> Merhaba yüksek hello **önem düzeyi** daha fazla kaynaklardır tüketilen toolog ve daha fazla izlemeleri üretilmektedir hello hello. Emin olun **önem düzeyi** üretim veya yüksek trafiğe sahip site için yapılandırılmış toohello doğru ayrıntı değil. 
> 
> 

![][StreamingLogsScreenshot]tooview hello **akış günlükleri** gelen hello Azure portalı içinde tıklayın **(1) günlük akışı** hello içinde de **izleme** hello ayarları menüsünün bölümünde. Uygulamanızı etkin olarak izleme deyimleri yazma sonra hello görmeniz gerekir **(2) akış günlükleri UI** yakın gerçek zamanlı.

## <a name="console"></a>Konsol
Merhaba **Azure portal** konsol erişimi tooyour uygulaması sağlar. Uygulamanızın dosya sistemini inceleyin ve powershell/cmd komut dosyalarını çalıştır. Konsol komutları yürütülürken zaman, çalışan uygulama kodu olarak aynı izinleri ayarlama hello tarafından bağlıdır. Erişim tooprotected dizinleri ve yükseltilmiş izinleri gerektiren çalışan komutlar engellenir.  

![][ConsoleScreenshot]Çok ayarları menüsünden aşağı kaydırın**geliştirme araçları** bölümünde ve tıklayın **(1) konsol** ve hello **(2) konsol** toohello sağ kullanıcı arabirimini açar.

tooget ile Merhaba tanıdık **konsol**, temel komutları gibi deneyin:

`````````````````````````
dir
`````````````````````````

`````````````````````````
cd
`````````````````````````

<!-- Images. -->
[DiagnosticsLogs]: ./media/web-sites-streaming-logs-and-console/diagnostic-logs.png
[BrowseSitesScreenshot]: ./media/web-sites-streaming-logs-and-console/browse-sites.png
[StreamingLogsScreenshot]: ./media/web-sites-streaming-logs-and-console/streaming-logs.png
[ConsoleScreenshot]: ./media/web-sites-streaming-logs-and-console/console.png
