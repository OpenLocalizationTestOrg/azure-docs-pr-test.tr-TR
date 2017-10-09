---
title: "Azure App Service'te web uygulamalarını için aaaEnable Tanılama Günlüğü"
description: "Bilgi nasıl tooenable tanılama günlük ve Azure tarafından günlüğe kaydedilen bilgi tooaccess hello nasıl araçları tooyour uygulama, de ekleyin."
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: c9da27b2-47d4-4c33-a3cb-1819955ee43b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2016
ms.author: cephalin
ms.openlocfilehash: 4b2903ff31cc93180552cf51196c33505ffbaf07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-logging-for-web-apps-in-azure-app-service"></a>Azure App Service'te web uygulamalarını için tanılama günlüğünü etkinleştirme
## <a name="overview"></a>Genel Bakış
Azure ayıklama yerleşik tanılama tooassist sağlayan bir [App Service web uygulaması](http://go.microsoft.com/fwlink/?LinkId=529714). Bu makalede, öğreneceksiniz nasıl tooenable tanılama günlük ve Azure tarafından günlüğe kaydedilen bilgi tooaccess hello nasıl araçları tooyour uygulama, de ekleyin.

Bu makalede hello kullanan [Azure Portal](https://portal.azure.com), Azure PowerShell ve tanılama günlükleri ile hello Azure komut satırı arabirimi (Azure CLI) toowork. Visual Studio kullanarak tanılama günlükleri ile çalışma hakkında daha fazla bilgi için bkz: [Visual Studio'da Azure sorun giderme](web-sites-dotnet-troubleshoot-visual-studio.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="whatisdiag"></a>Web sunucusu tanılama ve uygulama tanılama
App Service web apps hello web sunucusu ve hello web uygulamasının içinden bilgileri günlüğe kaydetme için tanılama işlevsellik sağlar. Bu mantıksal olarak ayrılmış **web sunucusu tanılama** ve **uygulama tanılama**.

### <a name="web-server-diagnostics"></a>Web sunucu tanıları
Etkinleştirmek veya tür günlüğe aşağıdaki hello devre dışı bırakabilirsiniz:

* **Hata günlüğü ayrıntılı** -ayrıntılı hata bilgileri (durum kodu 400 veya daha büyük) hatası olduğunu gösteren HTTP durum kodları için. Bu neden hello sunucu hello hata kodunu döndürdü belirlemenize yardımcı olabilecek bilgiler içerebilir.
* **Başarısız istek izleme** -ayrıntılı izleme hello IIS kullanılan bileşenler tooprocess hello isteği ve her bileşenin geçen hello süre dahil olmak üzere, başarısız istekler hakkında bilgi. Döndürülen belirli bir HTTP hata toobe neden olan ayırmak veya tooincrease site performansını çalışıyorsunuz, bu yararlı olabilir.
* **Web sunucusu günlüğe kaydetme** -hello kullanarak HTTP işlemler hakkında bilgi [W3C Genişletilmiş günlük dosyası biçimi](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx). Bu, işlenen istek hello sayısı gibi genel site ölçümleri veya belirli bir IP adresinden kaç isteklerdir belirlerken yararlıdır.

### <a name="application-diagnostics"></a>Uygulama tanılama
Uygulama Tanılama web uygulama tarafından üretilen toocapture bilgileri sağlar. ASP.NET uygulamaları hello kullanabileceğiniz [System.Diagnostics.Trace](http://msdn.microsoft.com/library/36hhw2t6.aspx) sınıfı toolog bilgi toohello uygulama tanılama günlük. Örneğin:

    System.Diagnostics.Trace.TraceError("If you're seeing this, something bad happened");

Çalışma zamanında, sorun giderme Bu günlükleri toohelp alabilirsiniz. Daha fazla bilgi için bkz: [Visual Studio'daki sorun giderme Azure web uygulamaları](web-sites-dotnet-troubleshoot-visual-studio.md).

İçerik tooa web uygulama yayımladığınızda, app Service web apps dağıtım bilgileri de oturum açın. Bu otomatik olarak gerçekleşir ve dağıtım günlüğü için herhangi bir yapılandırma ayarları. Dağıtım günlüğü neden bir dağıtımı başarısız toodetermine sağlar. Örneğin, bir özel dağıtım komut dosyası kullanıyorsanız, dağıtım günlüğü toodetermine hello betik neden başarısız kullanabilirsiniz.

## <a name="enablediag"></a>Nasıl tooenable tanılama
Merhaba tooenable tanılamada [Azure Portal](https://portal.azure.com), web uygulamanız için toohello dikey penceresine gidin ve tıklatın **Ayarları > tanılama günlükleri**.

<!-- todo:cleanup dogfood addresses in screenshot -->
![Günlükleri bölümü](./media/web-sites-enable-diagnostic-log/logspart.png)

Etkinleştirdiğinizde **uygulama tanılama** hello ayrıca tercih **düzeyi**. Bu ayar çok yakalanan toofilter hello bilgilerin sağlar**bilgilendirme**, **uyarı** veya **hata** bilgi. Bu çok ayarı**ayrıntılı** hello uygulama tarafından üretilen tüm bilgileri kaydeder.

> [!NOTE]
> Merhaba web.config değiştirme aksine, uygulama Tanılama'yı etkinleştirme veya tanılama günlük düzeylerini değiştirme dosyası içinde Merhaba uygulaması çalıştıran hello uygulama etki alanı dönüştürülmeyeceği.
>
>

Merhaba, [Klasik portal](https://manage.windowsazure.com) Web uygulaması **yapılandırma** seçebileceğiniz sekmesinde **depolama** veya **dosya sistemi** için **web sunucusu Günlük kaydı**. Seçme **depolama** tooselect bir depolama hesabı ve hello günlüklerine yazılır bir blob kapsayıcı sağlar. İçin tüm diğer günlükler **site tanılama** yalnızca toohello dosya sistemi yazılır.

Merhaba [Klasik portal](https://manage.windowsazure.com) Web uygulaması **yapılandırma** sekmesinde de uygulama tanılama için ek ayarlar vardır:

* **Dosya sistemi** -depoları hello uygulama tanılama bilgileri toohello web app dosya sistemi. Bu dosyalar FTP tarafından erişilen veya Zip arşivini hello Azure PowerShell veya Azure komut satırı arabirimi (Azure CLI) kullanılarak indirilir.
* **Tablo depolama** -depoları hello uygulama tanılama bilgilerini hello belirtilen Azure depolama hesabı ve tablo adı.
* **BLOB Depolama** -depoları hello hello belirtilen Azure depolama hesabı ve blob kapsayıcısında uygulama tanılama bilgileri.
* **Saklama dönemi** -varsayılan olarak, günlükleri otomatik olarak silinir değil **blob depolama**. Seçin **ayarlamak bekletme** ve hello tooautomatically istiyorsanız tookeep günlüklerini silme günlükleri gün sayısını girin.

> [!NOTE]
> Varsa, [depolama hesabınızın erişim anahtarlarını yeniden](../storage/common/storage-create-storage-account.md), hello ilgili günlük kaydı yapılandırması toouse güncelleştirilmiş hello anahtarları sıfırlamanız gerekir. toodo bu:
>
> 1. Merhaba, **yapılandırma** sekmesinde, hello ilgili günlük özelliğini çok belirleyin**devre dışı**. Ayarınız kaydedin.
> 2. Günlük toohello depolama hesabı blob veya tablo yeniden etkinleştirin. Ayarınız kaydedin.
>
>

Dosya sistemi, tablo depolama veya blob depolama herhangi bir bileşimini aynı saat ve ayrı Günlük düzeyi yapılandırmalarının hello etkinleştirilebilir. Örneğin, size toolog hataları ve Uyarıları tooblob depolama uzun vadeli günlük bir çözüm, dosya sistemi günlük ile ayrıntılı bir düzeyde etkinleştirirken isteyebilir.

Tüm üç depolama konumları hello sunarken aynı temel bilgileri günlüğe kaydedilen olayları için **tablo depolama** ve **blob depolama** oturum hello örnek kimliği, iş parçacığı kimliği ve daha gibi ek bilgiler oturum çok daha ayrıntılı zaman damgası (onay biçimi)**dosya sistemi**.

> [!NOTE]
> İçinde depolanan bilgileri **tablo depolama** veya **blob depolama** yalnızca bir depolama istemcisi veya doğrudan bu depolama sistemleri ile çalışabilirsiniz uygulamanın kullanılarak erişilebilir. Örneğin, Visual Studio 2013 kullanılan tooexplore tablo veya blob depolama olabilir bir Depolama Gezgini içerir ve Hdınsight blob storage'da depolanan verilere erişebilir. Ayrıca Azure Storage hello birini kullanarak erişen bir uygulama yazabilirsiniz [Azure SDK'ları](/downloads/#).
>
> [!NOTE]
> Tanılama hello kullanarak Azure Powershell'den de etkinleştirilebilir **kümesi AzureWebsite** cmdlet'i. Azure PowerShell yüklü değil veya toouse yapılandırmadıysanız, Azure aboneliğinize bkz [nasıl tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).
>
>

## <a name="download"></a>Nasıl yapılır: indirme günlükleri
Tanılama bilgileri depolanan toohello web app dosya sistemi, FTP kullanarak doğrudan erişilebilir. Ayrıca Azure PowerShell veya hello Azure komut satırı arabirimi kullanarak Zip arşivini indirilebilir.

Merhaba günlükleri depolanmış hello dizin yapısı aşağıdaki gibidir:

* **Uygulama günlüklerini** -/LogFiles/uygulama /. Bu klasör uygulama günlüğü tarafından üretilen bilgileri içeren bir veya daha fazla metin dosyalarını içerir.
* **Başarısız istek izlemelerin** -/ LogFiles/W3SVC ### /. Bu klasör bir XSL dosyası ve bir veya daha fazla XML dosyalarını içerir. Internet Explorer'da görüntülendiğinde hello hello XSL dosyasını biçimlendirme ve hello XML Merhaba içeriğine filtreleme işlevselliği sağladığından XML dosyaları ile aynı dizinde dosya hello içine hello XSL dosyasını karşıdan emin olun.
* **Ayrıntılı Hata günlüklerini** -/LogFiles/DetailedErrors /. Bu klasör oluşan HTTP hataları için kapsamlı bilgi sağlayan bir veya daha fazla .htm dosyalarını içerir.
* **Web sunucu günlükleri** -/LogFiles/http/RawLogs. Merhaba kullanılarak biçimlendirilmiş bir veya daha fazla metin dosyaları bu klasörde [W3C Genişletilmiş günlük dosyası biçimi](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).
* **Dağıtım günlükleri** -/ LogFiles/Git. Bu klasör Azure web uygulamaları tarafından kullanılan hello iç dağıtım işlemler tarafından oluşturulan günlükleri içeren, aynı zamanda Git dağıtımları için günlüğe kaydeder.

### <a name="ftp"></a>FTP
FTP, ziyaret hello kullanarak tooaccess tanılama bilgilerini **Pano** web uygulamanızın hello [Klasik portal](https://manage.windowsazure.com). Merhaba, **Hızlı Bakış** bölümünde, hello kullan **FTP tanılama günlükleri** bağlantı FTP kullanarak tooaccess hello günlük dosyaları. Merhaba **dağıtım/FTP kullanıcısı** girişi kullanılan tooaccess hello FTP sitesi olmalıdır hello kullanıcı adını listeler.

> [!NOTE]
> Merhaba, **dağıtım/FTP kullanıcısı** girişi ayarlanmamışsa, veya bu kullanıcının parolasını hello unuttuysanız, hello kullanarak yeni bir kullanıcı ve parola oluşturabilirsiniz **sıfırlama dağıtım kimlik bilgileri** hello bağlantıyı**Hızlı Bakış** hello bölümünü **Pano**.
>
>

### <a name="download-with-azure-powershell"></a>Azure PowerShell ile indirme
toodownload hello günlük dosyaları, Azure PowerShell yeni bir örneğini başlatın ve hello aşağıdaki komutu kullanın:

    Save-AzureWebSiteLog -Name webappname

Bu hello tarafından belirtilen hello web uygulaması için hello günlüklerini kaydeder **-adı** adlı parametre tooa dosya **logs.zip** hello geçerli dizinde.

> [!NOTE]
> Azure PowerShell yüklü değil veya toouse yapılandırmadıysanız, Azure aboneliğinize bkz [nasıl tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).
>
>

### <a name="download-with-azure-command-line-interface"></a>Azure komut satırı arabirimi ile indirme
Hello Azure komut satırı arabirimi kullanarak toodownload hello günlük dosyaları yeni komut istemi, PowerShell, Bash veya Terminal oturumu açın ve hello aşağıdaki komutu girin:

    azure site log download webappname

Bu adında 'webappname' tooa dosya adlı hello web uygulaması için hello günlüklerini kaydeder **diagnostics.zip** hello geçerli dizinde.

> [!NOTE]
> Yüklü değilse Azure komut satırı arabirimi (Azure CLI) hello veya toouse yapılandırmadıysanız, Azure aboneliğinizin bkz [nasıl tooUse Azure CLI](../cli-install-nodejs.md).
>
>

## <a name="how-to-view-logs-in-application-insights"></a>Nasıl yapılır: View Application Insights'ta günlüğe kaydeder
Visual Studio Application Insights filtreleme ve günlükleri arama ve hello günlükleri istekleri ve diğer olaylarla ilişkilendirme için araçlar sağlar.

1. Visual Studio'da Hello Application Insights SDK'sı tooyour projeye ekleyin.
   * Çözüm Gezgini'nde, projenize sağ tıklayın ve Application Insights Ekle'ı seçin. Application Insights kaynağı oluşturma dahil adımlarda size kılavuzluk. [Daha fazla bilgi](../application-insights/app-insights-asp-net.md)
2. Merhaba İzleme dinleyicisi paket tooyour projeye ekleyin.
   * Projenize sağ tıklayın ve NuGet paketlerini Yönet'i seçin. Seçin `Microsoft.ApplicationInsights.TraceListener` [daha fazla bilgi edinin](../application-insights/app-insights-asp-net-trace-logs.md)
3. Projenizi karşıya yükleme ve toogenerate günlük verilerini çalıştırın.
4. Merhaba, [Azure Portal](https://portal.azure.com/)tooyour yeni Application Insights kaynağı göz atın ve Aç **arama**. İstek, kullanım ve diğer telemetri ile birlikte günlük verilerinizi görürsünüz. Birkaç telemetri birkaç dakika tooarrive alabilir: Yenile'yi tıklatın. [Daha fazla bilgi](../application-insights/app-insights-diagnostic-search.md)

[Application Insights ile izleme performansı hakkında daha fazla bilgi edinin](../application-insights/app-insights-azure-web-apps.md)

## <a name="streamlogs"></a>Nasıl yapılır: akış günlükleri
Bir uygulama geliştirirken, yararlı toosee günlük kaydı bilgilerini neredeyse gerçek zamanlı genellikle olur. Bu günlük kaydı bilgileri tooyour geliştirme ortamı Azure PowerShell veya hello Azure komut satırı arabirimi kullanarak akış tarafından gerçekleştirilebilir.

> [!NOTE]
> Günlük arabellek bazı türleri hello akış bozuk olayları sonuçlanabilir toohello günlük dosyası yazma. Örneğin, bir kullanıcı bir sayfayı ziyaret ettiğinde oluşan bir uygulama günlük girişi hello karşılık gelen HTTP günlük girişi hello sayfa isteği için önce hello akışında görüntülenebilir.
>
> [!NOTE]
> Günlük akış de akış hello depolanan tooany metin dosyası yazılan bilgilerin **D:\\ev\\LogFiles\\**  klasör.
>
>

### <a name="streaming-with-azure-powershell"></a>Azure PowerShell ile akış
toostream günlük kaydı bilgileri, Azure PowerShell yeni bir örneğini başlatın ve hello aşağıdaki komutu kullanın:

    Get-AzureWebSiteLog -Name webappname -Tail

Bu hello tarafından belirtilen toohello web uygulamasına bağlanır **-Name** parametre ve bilgileri toohello PowerShell penceresinde hello web uygulamasında günlüğü olaylarını ortaya çıktığında akış başlayın. Merhaba /LogFiles directory (d:/home/günlük dosyaları) depolanan .txt, .log veya .htm bitiş toofiles yazılmış herhangi bir bilgi toohello yerel konsol akışı.

hataları gibi toofilter belirli olayları kullanmak hello **-ileti** parametresi. Örneğin:

    Get-AzureWebSiteLog -Name webappname -Tail -Message Error

HTTP gibi toofilter belirli günlük türlerini kullanan hello **-yol** parametresi. Örneğin:

    Get-AzureWebSiteLog -Name webappname -Tail -Path http

toosee kullanılabilir yollar, kullanım hello - ListPath parametre listesi.

> [!NOTE]
> Azure PowerShell yüklü değil veya toouse yapılandırmadıysanız, Azure aboneliğinize bkz [nasıl tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).
>
>

### <a name="streaming-with-azure-command-line-interface"></a>Azure komut satırı arabirimi ile akış
toostream günlük kaydı bilgileri, yeni komut istemi, PowerShell, Bash veya Terminal oturumu açın ve hello aşağıdaki komutu girin:

    azure site log tail webappname

Bu, 'webappname' adlı toohello web uygulamasına bağlanmak ve bilgileri toohello penceresinde hello web uygulamasında günlüğü olaylarını ortaya çıktığında akış başlayın. Merhaba /LogFiles directory (d:/home/günlük dosyaları) depolanan .txt, .log veya .htm bitiş toofiles yazılmış herhangi bir bilgi toohello yerel konsol akışı.

hataları gibi toofilter belirli olayları kullanmak hello **--filtre** parametresi. Örneğin:

    azure site log tail webappname --filter Error

HTTP gibi toofilter belirli günlük türlerini kullanan hello **--yolu** parametresi. Örneğin:

    azure site log tail webappname --path http

> [!NOTE]
> Yüklü değilse Azure komut satırı arabirimi hello veya toouse yapılandırmadıysanız, Azure aboneliğinizin bkz [nasıl tooUse Azure komut satırı arabirimi](../cli-install-nodejs.md).
>
>

## <a name="understandlogs"></a>Nasıl yapılır: Tanılama günlükleri anlama
### <a name="application-diagnostics-logs"></a>Uygulama tanılama günlükleri
Uygulama Tanılama, günlükleri toohello dosya sistemi, table storage depolamak veya blob depolamaya bağlı olarak, .NET uygulamaları için belirli bir biçimde bilgileri depolar. Merhaba temel depolanan verileri kümesidir aynı tüm üç depolama türlerine hello - başlangıç tarihi ve saati hello olayı oluştu, hello olay, hello olay türü (bilgi, uyarı, hata) ve hello olay iletisi üretilen hello işlem kimliği.

**Dosya sistemi**

Günlüğe kaydedilen toohello dosya sistemi veya akış kullanılarak alınan her satırı biçimini izleyen hello olacaktır:

    {Date}  PID[{process id}] {event type/level} {message}

Örneğin, bir hata olayı benzer toohello aşağıdaki görünür:

    2014-01-30T16:36:59  PID[3096] Error       Fatal error on hello page!

Toohello dosya sistemi günlük hello en temel bilgileri yalnızca başlangıç saati, işlem kimliği, olay düzeyi ve ileti sağlama hello üç kullanılabilir yöntemleri sağlar.

**Tablo depolama**

Tootable depolama oturum açarken ek hello olay hakkında daha ayrıntılı bilgi yanı sıra hello tablo depolanan hello veri arama kullanılan toofacilitate özelliklerdir. Merhaba aşağıdaki özellikleri (sütunları) hello tablosunda depolanan her varlık (satır) için kullanılır.

| Özellik adı | Değer/biçimi |
| --- | --- |
| PartitionKey |Tarih/saat yyyyMMddHH biçiminde hello olay |
| RowKey |Bu varlık benzersiz olarak tanımlayan bir GUID değeri |
| zaman damgası |Başlangıç tarihi ve olay hello saat oluştu |
| EventTickCount |Başlangıç tarihi ve olay hello saat, değer çizgisi biçiminde (büyük duyarlık) oluştu |
| ApplicationName |Merhaba web uygulaması adı |
| Düzey |Olay düzeyi (uyarı, bilgi örneğin hata) |
| Olay Kimliği |Bu olayın Hello olay kimliği<p><p>Too0 belirtilmezse varsayılan olarak |
| örnek kimliği |Hatta hello hello web uygulaması örneğini oluştu. |
| PID |İşlem kimliği |
| komutu |Merhaba olay üretilen hello iş parçacığının Hello iş parçacığı kimliği |
| İleti |Olay Ayrıntısı iletisi |

**Blob depolama**

Tooblob depolama günlüğe kaydedildiğinde, verileri virgülle ayrılmış değerler (CSV) biçiminde depolanır. Benzer tootable depolama, ek alanlardır oturum tooprovide hello olay hakkında daha ayrıntılı bilgi. Merhaba aşağıdaki özellikleri hello CSV her satır için kullanılır:

| Özellik adı | Değer/biçimi |
| --- | --- |
| Tarih |Başlangıç tarihi ve olay hello saat oluştu |
| Düzey |Olay düzeyi (uyarı, bilgi örneğin hata) |
| ApplicationName |Merhaba web uygulaması adı |
| örnek kimliği |Olay hello hello web uygulaması örneğini oluştu. |
| EventTickCount |Başlangıç tarihi ve olay hello saat, değer çizgisi biçiminde (büyük duyarlık) oluştu |
| Olay Kimliği |Bu olayın Hello olay kimliği<p><p>Too0 belirtilmezse varsayılan olarak |
| PID |İşlem kimliği |
| komutu |Merhaba olay üretilen hello iş parçacığının Hello iş parçacığı kimliği |
| İleti |Olay Ayrıntısı iletisi |

blob içinde depolanan hello verileri benzer toohello aşağıdaki görünür:

    date,level,applicationName,instanceId,eventTickCount,eventId,pid,tid,message
    2014-01-30T16:36:52,Error,mywebapp,6ee38a,635266966128818593,0,3096,9,An error occurred

> [!NOTE]
> Hello ilk satırı hello günlüğünün bu örnekte belirtildiği şekilde hello sütun üst bilgileri içerir.
>
>

### <a name="failed-request-traces"></a>İstek izlemelerin başarısız oldu
Başarısız istek izlemelerin adlı XML dosyalarında saklanır **fr ### .xml**. toomake bunu daha kolay tooview oturum hello bilgileri, adlandırılmış bir XSL stil **freb.xsl** hello aynı sağlanan XML dosyaları hello gibi dizin. Merhaba XML dosyalarından birini Internet Explorer'da açma hello XSL stil sayfası tooprovide hello izleme bilgilerini biçimlendirilmiş bir görüntüsünü kullanır. Bu benzer toohello aşağıdaki görünür:

![Merhaba tarayıcıda görüntülenen başarısız istek](./media/web-sites-enable-diagnostic-log/tws-failedrequestinbrowser.png)

### <a name="detailed-error-logs"></a>Ayrıntılı hata günlükleri
Ayrıntılı Hata günlüklerini oluşan HTTP hataları daha ayrıntılı bilgi sağlayan HTML belgelerdir. Bunlar yalnızca HTML belgeleri olduğundan, bir web tarayıcısı kullanarak görüntülenebilir.

### <a name="web-server-logs"></a>Web sunucu günlükleri
Merhaba web sunucu günlükleri hello kullanılarak biçimlendirilmiş [W3C Genişletilmiş günlük dosyası biçimi](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx). Bu bilgileri bir metin düzenleyicisi kullanarak okunabilir veya yardımcı programlarını kullanarak Ayrıştırılan [günlük ayrıştırıcısı](http://go.microsoft.com/fwlink/?LinkId=246619).

> [!NOTE]
> Hello Azure web uygulamaları tarafından oluşturulan günlükleri hello desteklemeyen **s-computername**, **s-ip**, veya **cs-version** alanları.
>
>

## <a name="nextsteps"></a> Sonraki adımlar
* [Nasıl tooMonitor Web uygulamaları](http://docs.microsoft.com/en-us/azure/app-service-web/web-sites-monitor)
* [Visual Studio'daki Azure web uygulamaları sorunlarını giderme](web-sites-dotnet-troubleshoot-visual-studio.md)
* [Analiz web uygulama günlüklerini Hdınsight'ta](http://gallery.technet.microsoft.com/scriptcenter/Analyses-Windows-Azure-web-0b27d413)

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
>
>

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)
* Yeni portalı eski portal toohello hello değişikliği Kılavuzu toohello için bkz: [gezinme için başvuru hello Azure portalı](http://go.microsoft.com/fwlink/?LinkId=529715)
