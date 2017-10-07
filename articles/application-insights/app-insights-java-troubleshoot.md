---
title: Java web projesinde Application Insights aaaTroubleshoot
description: "Sorun giderme kılavuzu - Application Insights ile canlı Java uygulamalarını izleme."
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: c274c01b1992971fae194c3e510512ca06ab76b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a><span data-ttu-id="45942-103">Java için Application Insights Sorun Giderme, Soru ve Yanıt</span><span class="sxs-lookup"><span data-stu-id="45942-103">Troubleshooting and Q and A for Application Insights for Java</span></span>
<span data-ttu-id="45942-104">Sorular veya sorunlar [Java'da Azure Application Insights][java]?</span><span class="sxs-lookup"><span data-stu-id="45942-104">Questions or problems with [Azure Application Insights in Java][java]?</span></span> <span data-ttu-id="45942-105">Burada, bazı ipuçları verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="45942-105">Here are some tips.</span></span>

## <a name="build-errors"></a><span data-ttu-id="45942-106">Derleme hataları</span><span class="sxs-lookup"><span data-stu-id="45942-106">Build errors</span></span>
<span data-ttu-id="45942-107">**Eclipse'te, ekleme hello olduğunda Application Insights SDK Maven veya Gradle, aracılığıyla derleme veya sağlama toplamı doğrulama hataları alıyorum.**</span><span class="sxs-lookup"><span data-stu-id="45942-107">**In Eclipse, when adding hello Application Insights SDK via Maven or Gradle, I get build or checksum validation errors.**</span></span>

* <span data-ttu-id="45942-108">Varsa hello bağımlılık <version> öğesi bir desen ile joker karakterler kullanarak (örneğin (Maven) `<version>[1.0,)</version>` veya (Gradle) `version:'1.0.+'`), belirli bir sürümü gibi yerine belirtmeyi deneyin `1.0.2`.</span><span class="sxs-lookup"><span data-stu-id="45942-108">If hello dependency <version> element is using a pattern with wildcard characters (e.g. (Maven) `<version>[1.0,)</version>` or (Gradle) `version:'1.0.+'`), try specifying a specific version instead like `1.0.2`.</span></span> <span data-ttu-id="45942-109">Merhaba bkz [sürüm notları](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) hello son sürüm için.</span><span class="sxs-lookup"><span data-stu-id="45942-109">See hello [release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) for hello latest version.</span></span>

## <a name="no-data"></a><span data-ttu-id="45942-110">Veri yok</span><span class="sxs-lookup"><span data-stu-id="45942-110">No data</span></span>
<span data-ttu-id="45942-111">**Application Insights başarıyla eklendi ve Uygulamam çalıştı, ancak hiç veri hello portalında gördüğünüze göre.**</span><span class="sxs-lookup"><span data-stu-id="45942-111">**I added Application Insights successfully and ran my app, but I've never seen data in hello portal.**</span></span>

* <span data-ttu-id="45942-112">Bir dakika bekleyip Yenile'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45942-112">Wait a minute and click Refresh.</span></span> <span data-ttu-id="45942-113">Merhaba grafikler kendilerini düzenli olarak yeniler, ancak aynı zamanda el ile yenileyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45942-113">hello charts refresh themselves periodically, but you can also refresh manually.</span></span> <span data-ttu-id="45942-114">Merhaba yenileme aralığı hello grafiğin zaman aralığı hello bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="45942-114">hello refresh interval depends on hello time range of hello chart.</span></span>
* <span data-ttu-id="45942-115">Merhaba Applicationınsights.xml dosyasını (projenizin kaynaklar klasörüne hello) tanımlanan bir izleme anahtarı olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="45942-115">Check that you have an instrumentation key defined in hello ApplicationInsights.xml file (in hello resources folder in your project)</span></span>
* <span data-ttu-id="45942-116">Olduğunu doğrulayın hiçbir `<DisableTelemetry>true</DisableTelemetry>` hello xml dosyasında düğümü.</span><span class="sxs-lookup"><span data-stu-id="45942-116">Verify that there is no `<DisableTelemetry>true</DisableTelemetry>` node in hello xml file.</span></span>
* <span data-ttu-id="45942-117">Güvenlik Duvarı'nda tooopen TCP bağlantı noktaları 80 ve 443 giden trafiği toodc.services.visualstudio.com için olabilir. Merhaba bkz [güvenlik duvarı özel durumlarını tam listesi](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="45942-117">In your firewall, you might have tooopen TCP ports 80 and 443 for outgoing traffic toodc.services.visualstudio.com. See hello [full list of firewall exceptions](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="45942-118">Merhaba Microsoft Azure Panosu başlatmak, hello hizmet durumu haritası bakın.</span><span class="sxs-lookup"><span data-stu-id="45942-118">In hello Microsoft Azure start board, look at hello service status map.</span></span> <span data-ttu-id="45942-119">Bazı uyarı göstergeleri varsa, bunlar tooOK döndürmüş kapatın ve, Application Insights uygulama dikey penceresini yeniden açın kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="45942-119">If there are some alert indications, wait until they have returned tooOK and then close and re-open your Application Insights application blade.</span></span>
* <span data-ttu-id="45942-120">Ekleyerek toohello IDE konsol penceresinde, günlük özelliğini açın bir `<SDKLogger />` öğesi düğümünde hello kök hello Applicationınsights.xml dosyasını (projenizin kaynaklar klasörüne hello) ve [Hata] başında girişlerini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="45942-120">Turn on logging toohello IDE console window, by adding an `<SDKLogger />` element under hello root node in hello ApplicationInsights.xml file (in hello resources folder in your project), and check for entries prefaced with [Error].</span></span>
* <span data-ttu-id="45942-121">Bu hello Applicationınsights.xml dosyasını başarıyla hello Java SDK'sı tarafından bir "yapılandırma dosyası başarıyla bulundu" deyimi için hello konsolun çıktı iletileri bakarak yüklendi doğru emin olun.</span><span class="sxs-lookup"><span data-stu-id="45942-121">Make sure that hello correct ApplicationInsights.xml file has been successfully loaded by hello Java SDK, by looking at hello console's output messages for a "Configuration file has been successfully found" statement.</span></span>
* <span data-ttu-id="45942-122">Merhaba yapılandırma dosyası bulunamazsa, burada hello yapılandırma dosyası için Aranmakta olan hello çıktı iletileri toosee denetleyin ve Applicationınsights.XML arama konumların birinde bulunan bu hello emin olun.</span><span class="sxs-lookup"><span data-stu-id="45942-122">If hello config file is not found, check hello output messages toosee where hello config file is being searched for, and make sure that hello ApplicationInsights.xml is located in one of those search locations.</span></span> <span data-ttu-id="45942-123">Altın kural, hello uygulama Öngörüler SDK Jar'lar hello yapılandırma dosyası yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45942-123">As a rule of thumb, you can place hello config file near hello Application Insights SDK JARs.</span></span> <span data-ttu-id="45942-124">Örneğin: Tomcat'te bu WEB-INF/lib klasörüne hello anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="45942-124">For example: in Tomcat, this would mean hello WEB-INF/lib folder.</span></span>

#### <a name="i-used-toosee-data-but-it-has-stopped"></a><span data-ttu-id="45942-125">Toosee veri kullanılır, ancak bunu durduruldu</span><span class="sxs-lookup"><span data-stu-id="45942-125">I used toosee data, but it has stopped</span></span>
* <span data-ttu-id="45942-126">Merhaba denetleyin [durum blog](http://blogs.msdn.com/b/applicationinsights-status/).</span><span class="sxs-lookup"><span data-stu-id="45942-126">Check hello [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span></span>
* <span data-ttu-id="45942-127">Veri noktalarının aylık kota ulaşıp?</span><span class="sxs-lookup"><span data-stu-id="45942-127">Have you hit your monthly quota of data points?</span></span> <span data-ttu-id="45942-128">Ayarları/kota ve fiyatlandırma toofind kullanıma açın. Bu durumda, planınızı yükseltmek veya ek kapasite için ödeme yaparsınız.</span><span class="sxs-lookup"><span data-stu-id="45942-128">Open Settings/Quota and Pricing toofind out. If so, you can upgrade your plan, or pay for additional capacity.</span></span> <span data-ttu-id="45942-129">Merhaba bkz [düzeni fiyatlandırma](https://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="45942-129">See hello [pricing scheme](https://azure.microsoft.com/pricing/details/application-insights/).</span></span>

#### <a name="i-dont-see-all-hello-data-im-expecting"></a><span data-ttu-id="45942-130">Tüm hello veri bekleniyor görmüyorum</span><span class="sxs-lookup"><span data-stu-id="45942-130">I don't see all hello data I'm expecting</span></span>
* <span data-ttu-id="45942-131">Açık hello kotalar ve fiyatlandırma dikey ve onay olup [örnekleme](app-insights-sampling.md) içinde bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="45942-131">Open hello Quotas and Pricing blade and check whether [sampling](app-insights-sampling.md) is in operation.</span></span> <span data-ttu-id="45942-132">(% 100 iletim örnekleme işleminde değil anlamına gelir.) Merhaba Application Insights hizmeti kümesi tooaccept uygulamanızdan ulaşan hello telemetri yalnızca bir kısmı olabilir.</span><span class="sxs-lookup"><span data-stu-id="45942-132">(100% transmission means that sampling isn't in operation.) hello Application Insights service can be set tooaccept only a fraction of hello telemetry that arrives from your app.</span></span> <span data-ttu-id="45942-133">Bu telemetrinin aylık kota içinde tutmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="45942-133">This helps you keep within your monthly quota of telemetry.</span></span> 

## <a name="no-usage-data"></a><span data-ttu-id="45942-134">Kullanım verisi yok</span><span class="sxs-lookup"><span data-stu-id="45942-134">No usage data</span></span>
<span data-ttu-id="45942-135">**İstek ve yanıt süreleri, ancak hiçbir sayfa görünümü, tarayıcı hakkındaki verileri veya kullanıcı verileri görüyorum.**</span><span class="sxs-lookup"><span data-stu-id="45942-135">**I see data about requests and response times, but no page view, browser, or user data.**</span></span>

<span data-ttu-id="45942-136">Merhaba sunucudan uygulama toosend telemetrinize başarıyla ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="45942-136">You successfully set up your app toosend telemetry from hello server.</span></span> <span data-ttu-id="45942-137">Sonraki adımınız çok şimdi[web sayfalarını toosend telemetrinize hello web tarayıcısından ayarlamak][usage].</span><span class="sxs-lookup"><span data-stu-id="45942-137">Now your next step is too[set up your web pages toosend telemetry from hello web browser][usage].</span></span>

<span data-ttu-id="45942-138">Alternatif olarak, istemci bir uygulamada ise bir [telefon veya başka bir aygıt][platforms], buradan telemetri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="45942-138">Alternatively, if your client is an app in a [phone or other device][platforms], you can send telemetry from there.</span></span> 

<span data-ttu-id="45942-139">Kullanım hello aynı araçları anahtar tooset hem istemci hem de sunucu telemetri ayarlama.</span><span class="sxs-lookup"><span data-stu-id="45942-139">Use hello same instrumentation key tooset up both your client and server telemetry.</span></span> <span data-ttu-id="45942-140">Merhaba veri, aynı Application Insights kaynağı hello ve istemci ve sunucu mümkün toocorrelate olayları olacak görünür.</span><span class="sxs-lookup"><span data-stu-id="45942-140">hello data will appear in hello same Application Insights resource, and you'll be able toocorrelate events from client and server.</span></span>


## <a name="disabling-telemetry"></a><span data-ttu-id="45942-141">Telemetri devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="45942-141">Disabling telemetry</span></span>
<span data-ttu-id="45942-142">**Telemetri koleksiyonunu nasıl devre dışı bırakabilirim?**</span><span class="sxs-lookup"><span data-stu-id="45942-142">**How can I disable telemetry collection?**</span></span>

<span data-ttu-id="45942-143">Kod:</span><span class="sxs-lookup"><span data-stu-id="45942-143">In code:</span></span>

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

<span data-ttu-id="45942-144">**Veya**</span><span class="sxs-lookup"><span data-stu-id="45942-144">**Or**</span></span> 

<span data-ttu-id="45942-145">Applicationınsights.XML (klasöründe hello kaynakları projenize) güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="45942-145">Update ApplicationInsights.xml (in hello resources folder in your project).</span></span> <span data-ttu-id="45942-146">Merhaba aşağıdaki hello kök düğümü altına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="45942-146">Add hello following under hello root node:</span></span>

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

<span data-ttu-id="45942-147">Merhaba değeri değiştirdiğinizde hello XML yöntemi kullanarak, toorestart hello uygulamaya sahip.</span><span class="sxs-lookup"><span data-stu-id="45942-147">Using hello XML method, you have toorestart hello application when you change hello value.</span></span>

## <a name="changing-hello-target"></a><span data-ttu-id="45942-148">Merhaba hedef değiştirme</span><span class="sxs-lookup"><span data-stu-id="45942-148">Changing hello target</span></span>
<span data-ttu-id="45942-149">**Proje için verileri gönderir hangi Azure kaynak nasıl değiştirebilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="45942-149">**How can I change which Azure resource my project sends data to?**</span></span>

* <span data-ttu-id="45942-150">[Hello hello yeni kaynağın izleme anahtarını alır.][java]</span><span class="sxs-lookup"><span data-stu-id="45942-150">[Get hello instrumentation key of hello new resource.][java]</span></span>
* <span data-ttu-id="45942-151">Eclipse için hello Azure Araç Seti kullanarak Application Insights tooyour proje eklediyseniz, web projenize sağ tıklayın, seçin **Azure**, **yapılandırma Application Insights**ve başlangıç anahtarı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="45942-151">If you added Application Insights tooyour project using hello Azure Toolkit for Eclipse, right click your web project, select **Azure**, **Configure Application Insights**, and change hello key.</span></span>
* <span data-ttu-id="45942-152">Aksi takdirde hello anahtar projeniz hello kaynaklar klasörüne Applicationınsights.XML güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="45942-152">Otherwise, update hello key in ApplicationInsights.xml in hello resources folder in your project.</span></span>

## <a name="debug-data-from-hello-sdk"></a><span data-ttu-id="45942-153">Merhaba SDK verilerden hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="45942-153">Debug data from hello SDK</span></span>

<span data-ttu-id="45942-154">**SDK yapılması hangi hello nasıl bulabilirim?**</span><span class="sxs-lookup"><span data-stu-id="45942-154">**How can I find out what hello SDK is doing?**</span></span>

<span data-ttu-id="45942-155">tooget hello API, neler olduğunu hakkında daha fazla bilgi eklemek `<SDKLogger/>` hello hello Applicationınsights.XML yapılandırma dosyasının kök düğümü altında.</span><span class="sxs-lookup"><span data-stu-id="45942-155">tooget more information about what's happening in hello API, add `<SDKLogger/>` under hello root node of hello ApplicationInsights.xml configuration file.</span></span>

<span data-ttu-id="45942-156">Merhaba Günlükçü toooutput tooa dosya talimatını:</span><span class="sxs-lookup"><span data-stu-id="45942-156">You can also instruct hello logger toooutput tooa file:</span></span>

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

<span data-ttu-id="45942-157">Merhaba dosyaları altında bulunabilir `%temp%\javasdklogs` veya `java.io.tmpdir` Tomcat sunucusunu durumunda.</span><span class="sxs-lookup"><span data-stu-id="45942-157">hello files can be found under `%temp%\javasdklogs` or `java.io.tmpdir` in case of Tomcat server.</span></span>


## <a name="hello-azure-start-screen"></a><span data-ttu-id="45942-158">Hello Azure başlangıç ekranı</span><span class="sxs-lookup"><span data-stu-id="45942-158">hello Azure start screen</span></span>
<span data-ttu-id="45942-159">**Konumundaki arayan [Azure portal hello](https://portal.azure.com). Merhaba harita bir şey Uygulamam hakkında bilgi ver mu?**</span><span class="sxs-lookup"><span data-stu-id="45942-159">**I'm looking at [hello Azure portal](https://portal.azure.com). Does hello map tell me something about my app?**</span></span>

<span data-ttu-id="45942-160">Hayır, hello world hello Azure sunucularının durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="45942-160">No, it shows hello health of Azure servers around hello world.</span></span>

<span data-ttu-id="45942-161">*Hello Azure başlangıç Panosu (giriş ekranı) nasıl veri Uygulamam hakkında bulabilirim?*</span><span class="sxs-lookup"><span data-stu-id="45942-161">*From hello Azure start board (home screen), how do I find data about my app?*</span></span>

<span data-ttu-id="45942-162">Varsayılmıştır [Application Insights için uygulamanızı ayarlayın][java], Gözat'ı tıklatın, Application Insights'ı seçin ve uygulamanız için oluşturulan hello Uygulama kaynağı seçin.</span><span class="sxs-lookup"><span data-stu-id="45942-162">Assuming you [set up your app for Application Insights][java], click Browse, select Application Insights, and select hello app resource you created for your app.</span></span> <span data-ttu-id="45942-163">tooget var. daha hızlı gelecekte, uygulama toohello başlangıç panonuzu sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45942-163">tooget there faster in future, you can pin your app toohello start board.</span></span>

## <a name="intranet-servers"></a><span data-ttu-id="45942-164">İntranet sunucuları</span><span class="sxs-lookup"><span data-stu-id="45942-164">Intranet servers</span></span>
<span data-ttu-id="45942-165">**İntranetimde bulunan bir sunucu izleyebilir mi?**</span><span class="sxs-lookup"><span data-stu-id="45942-165">**Can I monitor a server on my intranet?**</span></span>

<span data-ttu-id="45942-166">Evet, sunucunuzun telemetri toohello Application Insights portalı üzerinden göndermek için sağlanan genel internet hello.</span><span class="sxs-lookup"><span data-stu-id="45942-166">Yes, provided your server can send telemetry toohello Application Insights portal through hello public internet.</span></span> 

<span data-ttu-id="45942-167">Güvenlik Duvarı'nda tooopen TCP bağlantı noktaları 80 ve 443 giden trafiği toodc.services.visualstudio.com ve f5.services.visualstudio.com olabilir.</span><span class="sxs-lookup"><span data-stu-id="45942-167">In your firewall, you might have tooopen TCP ports 80 and 443 for outgoing traffic toodc.services.visualstudio.com and f5.services.visualstudio.com.</span></span>

## <a name="data-retention"></a><span data-ttu-id="45942-168">Veri saklama</span><span class="sxs-lookup"><span data-stu-id="45942-168">Data retention</span></span>
<span data-ttu-id="45942-169">**Ne kadar veri hello Portalı'nda tutulur? Güvenli mi?**</span><span class="sxs-lookup"><span data-stu-id="45942-169">**How long is data retained in hello portal? Is it secure?**</span></span>

<span data-ttu-id="45942-170">Bkz: [veri saklama ve gizlilik][data].</span><span class="sxs-lookup"><span data-stu-id="45942-170">See [Data retention and privacy][data].</span></span>

## <a name="next-steps"></a><span data-ttu-id="45942-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="45942-171">Next steps</span></span>
<span data-ttu-id="45942-172">**Java sunucu Uygulamam için Application Insights'ı ayarlarım. Başka ne yapabilirim?**</span><span class="sxs-lookup"><span data-stu-id="45942-172">**I set up Application Insights for my Java server app. What else can I do?**</span></span>

* <span data-ttu-id="45942-173">[Web sayfalarınıza kullanılabilirliğini izleyin][availability]</span><span class="sxs-lookup"><span data-stu-id="45942-173">[Monitor availability of your web pages][availability]</span></span>
* <span data-ttu-id="45942-174">[Web sayfası kullanımını izleme][usage]</span><span class="sxs-lookup"><span data-stu-id="45942-174">[Monitor web page usage][usage]</span></span>
* <span data-ttu-id="45942-175">[Cihaz uygulamalarınızdaki sorunlarını tanılamak ve kullanımını izleme][platforms]</span><span class="sxs-lookup"><span data-stu-id="45942-175">[Track usage and diagnose issues in your device apps][platforms]</span></span>
* <span data-ttu-id="45942-176">[Kod tootrack kullanımı, uygulamanızın yazma][track]</span><span class="sxs-lookup"><span data-stu-id="45942-176">[Write code tootrack usage of your app][track]</span></span>
* <span data-ttu-id="45942-177">[Tanılama günlüklerini yakalama][javalogs]</span><span class="sxs-lookup"><span data-stu-id="45942-177">[Capture diagnostic logs][javalogs]</span></span>

## <a name="get-help"></a><span data-ttu-id="45942-178">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="45942-178">Get help</span></span>
* [<span data-ttu-id="45942-179">Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="45942-179">Stack Overflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

