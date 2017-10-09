---
title: aaaMicrosoft Dynamics CRM ve Azure Application Insights | Microsoft Docs
description: "Telemetri Microsoft Dynamics CRM Application Insights kullanarak Online'dan alın. Kurulum, verileri, Görselleştirme ve dışarı aktarma alma kılavuz."
services: application-insights
documentationcenter: 
author: mazharmicrosoft
manager: carmonm
ms.assetid: 04c66338-687e-49e5-9975-be935f98f156
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: bwren
ms.openlocfilehash: a39398060d6553fb18a26c101f085b7d87443636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a><span data-ttu-id="18f97-104">İzlenecek yol: Telemetri Microsoft Dynamics CRM Online Application Insights kullanarak etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="18f97-104">Walkthrough: Enabling Telemetry for Microsoft Dynamics CRM Online using Application Insights</span></span>
<span data-ttu-id="18f97-105">Bu makale size nasıl gösterir tooget telemetri verilerini [Microsoft Dynamics CRM Online](https://www.dynamics.com/) kullanarak [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="18f97-105">This article shows you how tooget telemetry data from [Microsoft Dynamics CRM Online](https://www.dynamics.com/) using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span></span> <span data-ttu-id="18f97-106">Biz Application Insights betik tooyour uygulama ekleyerek, veri ve veri görselleştirme yakalama hello tam işleminde size kılavuzluk.</span><span class="sxs-lookup"><span data-stu-id="18f97-106">We’ll walk through hello complete process of adding Application Insights script tooyour application, capturing data, and data visualization.</span></span>

> [!NOTE]
> <span data-ttu-id="18f97-107">[Merhaba örnek çözümü Gözat](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="18f97-107">[Browse hello sample solution](https://dynamicsandappinsights.codeplex.com/).</span></span>
> 
> 

## <a name="add-application-insights-toonew-or-existing-crm-online-instance"></a><span data-ttu-id="18f97-108">Application Insights toonew veya mevcut CRM Online örneği ekleme</span><span class="sxs-lookup"><span data-stu-id="18f97-108">Add Application Insights toonew or existing CRM Online instance</span></span>
<span data-ttu-id="18f97-109">toomonitor uygulamanıza Application Insights SDK'sı tooyour uygulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="18f97-109">toomonitor your application, you add an Application Insights SDK tooyour application.</span></span> <span data-ttu-id="18f97-110">Merhaba SDK telemetri toohello gönderir [Application Insights portalındaki](https://portal.azure.com), burada bizim güçlü analizi ve tanılama araçları kullanabilir, veya hello veri toostorage verin.</span><span class="sxs-lookup"><span data-stu-id="18f97-110">hello SDK sends telemetry toohello [Application Insights portal](https://portal.azure.com), where you can use our powerful analysis and diagnostic tools, or export hello data toostorage.</span></span>

### <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="18f97-111">Application Insights kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="18f97-111">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="18f97-112">Alma [Microsoft Azure hesap](http://azure.com/pricing).</span><span class="sxs-lookup"><span data-stu-id="18f97-112">Get [an account in Microsoft Azure](http://azure.com/pricing).</span></span> 
2. <span data-ttu-id="18f97-113">Merhaba içine oturum [Azure portal](https://portal.azure.com) ve yeni bir Application Insights kaynağı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="18f97-113">Sign into hello [Azure portal](https://portal.azure.com) and add a new Application Insights resource.</span></span> <span data-ttu-id="18f97-114">Verilerinizi nereye işlenen ve görüntülenen budur.</span><span class="sxs-lookup"><span data-stu-id="18f97-114">This is where your data will be processed and displayed.</span></span>
   
    ![Tıklatın +, geliştirici Hizmetleri, Application Insights.](./media/app-insights-sample-mscrm/01.png)
   
    <span data-ttu-id="18f97-116">ASP.NET hello uygulama türü olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="18f97-116">Choose ASP.NET as hello application type.</span></span>
3. <span data-ttu-id="18f97-117">Merhaba Başlarken sayfasını açın ve Aç "İzleyici ve istemci tarafı tanılamak".</span><span class="sxs-lookup"><span data-stu-id="18f97-117">Open hello Getting Started page and open "Monitor and diagnose client side".</span></span>
   
    ![Kod parçacığı web sayfanıza eklemek için](./media/app-insights-sample-mscrm/03.png)

<span data-ttu-id="18f97-119">**Merhaba kod sayfası açık tutmak getirin** sonraki adıma başka bir tarayıcı penceresinde hello sırada.</span><span class="sxs-lookup"><span data-stu-id="18f97-119">**Keep hello code page open** while you do hello next step in another browser window.</span></span> <span data-ttu-id="18f97-120">Merhaba kod yakında gerekir.</span><span class="sxs-lookup"><span data-stu-id="18f97-120">You'll need hello code soon.</span></span> 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a><span data-ttu-id="18f97-121">Microsoft Dynamics CRM JavaScript web kaynak oluşturma</span><span class="sxs-lookup"><span data-stu-id="18f97-121">Create a JavaScript web resource in Microsoft Dynamics CRM</span></span>
1. <span data-ttu-id="18f97-122">Oturum açma ve CRM Online örneği yönetici ayrıcalıklarıyla açın.</span><span class="sxs-lookup"><span data-stu-id="18f97-122">Open your CRM Online instance and login with administrator privileges.</span></span>
2. <span data-ttu-id="18f97-123">Microsoft Dynamics CRM, özelleştirmeleri, Özelleştir hello sistem ayarları</span><span class="sxs-lookup"><span data-stu-id="18f97-123">Open Microsoft Dynamics CRM Settings, Customizations, Customize hello System</span></span>
   
    ![Microsoft Dynamics CRM ayarları](./media/app-insights-sample-mscrm/04.png)
   
    ![Ayarlar > özelleştirmeleri](./media/app-insights-sample-mscrm/05.png)

    ![Merhaba sistemi seçeneği özelleştirme](./media/app-insights-sample-mscrm/06.png)

1. <span data-ttu-id="18f97-127">Bir JavaScript kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="18f97-127">Create a JavaScript resource.</span></span>
   
    ![Yeni Web kaynağı iletişim kutusu](./media/app-insights-sample-mscrm/07.png)
   
    <span data-ttu-id="18f97-129">Select bir ad verin **komut dosyası (JScript)** ve açık hello metin düzenleyici.</span><span class="sxs-lookup"><span data-stu-id="18f97-129">Give it a name, select **Script (JScript)** and open hello text editor.</span></span>
   
    ![Açık hello metin düzenleyicisi](./media/app-insights-sample-mscrm/08.png)
2. <span data-ttu-id="18f97-131">Merhaba kodu Application Insights kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="18f97-131">Copy hello code from Application Insights.</span></span> <span data-ttu-id="18f97-132">Kopyalanırken emin tooignore komut dosyası etiketlerini olun.</span><span class="sxs-lookup"><span data-stu-id="18f97-132">While copying make sure tooignore script tags.</span></span> <span data-ttu-id="18f97-133">Ekran görüntüsünün altında bakın:</span><span class="sxs-lookup"><span data-stu-id="18f97-133">Refer below screenshot:</span></span>
   
    ![İzleme anahtarı ayarlayın](./media/app-insights-sample-mscrm/09.png)
   
    <span data-ttu-id="18f97-135">Merhaba kodu uygulama ınsights kaynağınızı tanımlayan hello izleme anahtarını içerir.</span><span class="sxs-lookup"><span data-stu-id="18f97-135">hello code includes hello instrumentation key that identifies your Application insights resource.</span></span>
3. <span data-ttu-id="18f97-136">Kaydedin ve yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="18f97-136">Save and publish.</span></span>
   
    ![Kaydedin ve yayımlayın](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a><span data-ttu-id="18f97-138">Gereç formlar</span><span class="sxs-lookup"><span data-stu-id="18f97-138">Instrument Forms</span></span>
1. <span data-ttu-id="18f97-139">Microsoft CRM Online içinde hello hesap formunu açın</span><span class="sxs-lookup"><span data-stu-id="18f97-139">In Microsoft CRM Online, open hello Account form</span></span>
   
    ![Hesap formu](./media/app-insights-sample-mscrm/11.png)
2. <span data-ttu-id="18f97-141">Merhaba form özelliklerini açın</span><span class="sxs-lookup"><span data-stu-id="18f97-141">Open hello form Properties</span></span>
   
    ![Form Özellikleri](./media/app-insights-sample-mscrm/12.png)
3. <span data-ttu-id="18f97-143">Merhaba, oluşturduğunuz JavaScript web kaynağı ekleme</span><span class="sxs-lookup"><span data-stu-id="18f97-143">Add hello JavaScript web resource that you created</span></span>
   
    ![Menü ekleme](./media/app-insights-sample-mscrm/13.png)
   
    ![Merhaba web kaynağı ekleyin](./media/app-insights-sample-mscrm/14.png)
4. <span data-ttu-id="18f97-146">Kaydet ve formu özelleştirmelerinizi yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="18f97-146">Save and publish your form customizations.</span></span>

## <a name="metrics-captured"></a><span data-ttu-id="18f97-147">Yakalanan ölçümleri</span><span class="sxs-lookup"><span data-stu-id="18f97-147">Metrics captured</span></span>
<span data-ttu-id="18f97-148">Şimdi hello form için telemetri yakalamayı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="18f97-148">You have now set up telemetry capture for hello form.</span></span> <span data-ttu-id="18f97-149">Kullanıldığında, veri tooyour Application Insights kaynağı gönderilir.</span><span class="sxs-lookup"><span data-stu-id="18f97-149">Whenever it is used, data will be sent tooyour Application Insights resource.</span></span>

<span data-ttu-id="18f97-150">Göreceğiniz hello veri örnekleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="18f97-150">Here are samples of hello data that you'll see.</span></span>

#### <a name="application-health"></a><span data-ttu-id="18f97-151">Uygulama durumu</span><span class="sxs-lookup"><span data-stu-id="18f97-151">Application health</span></span>
![Örnek sayfa yükleme süresi](./media/app-insights-sample-mscrm/15.png)

![Örnek sayfa görünümleri grafik](./media/app-insights-sample-mscrm/16.png)

<span data-ttu-id="18f97-154">Tarayıcı özel durumlar:</span><span class="sxs-lookup"><span data-stu-id="18f97-154">Browser exceptions:</span></span>

![Tarayıcı özel durumlar grafik](./media/app-insights-sample-mscrm/17.png)

<span data-ttu-id="18f97-156">Daha fazla ayrıntı Hello grafik tooget tıklatın:</span><span class="sxs-lookup"><span data-stu-id="18f97-156">Click hello chart tooget more detail:</span></span>

![Özel durumlar listesi](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a><span data-ttu-id="18f97-158">Kullanım</span><span class="sxs-lookup"><span data-stu-id="18f97-158">Usage</span></span>
![Kullanıcıları, oturumlar ve sayfa görünümleri](./media/app-insights-sample-mscrm/19.png)

![Sesion grafikleri](./media/app-insights-sample-mscrm/20.png)

![Tarayıcı sürümleri](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a><span data-ttu-id="18f97-162">Tarayıcılar</span><span class="sxs-lookup"><span data-stu-id="18f97-162">Browsers</span></span>
![Sayfa yükleme süresi dökümü](./media/app-insights-sample-mscrm/22.png)

![Tarayıcı sürümü göre oturum sayısı](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a><span data-ttu-id="18f97-165">Coğrafi konum</span><span class="sxs-lookup"><span data-stu-id="18f97-165">Geolocation</span></span>
![Ülkeye göre oturum sayısı](./media/app-insights-sample-mscrm/24.png)

![Oturumların ve kullanıcıların ülkeye göre](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a><span data-ttu-id="18f97-168">İç sayfa görünümü isteği</span><span class="sxs-lookup"><span data-stu-id="18f97-168">Inside page view request</span></span>
![Sayfa görünümü özeti](./media/app-insights-sample-mscrm/26.png)

![Sayfa görünümü etkinliklerine arama](./media/app-insights-sample-mscrm/27.png)

![Benzer sayfa görünümleri](./media/app-insights-sample-mscrm/28.png)

![Sayfa görünümü özellikleri](./media/app-insights-sample-mscrm/29.png)

![Oturum başına sayfa](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a><span data-ttu-id="18f97-174">Örnek kod</span><span class="sxs-lookup"><span data-stu-id="18f97-174">Sample code</span></span>
<span data-ttu-id="18f97-175">[Merhaba örnek kod Gözat](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="18f97-175">[Browse hello sample code](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="power-bi"></a><span data-ttu-id="18f97-176">Power BI</span><span class="sxs-lookup"><span data-stu-id="18f97-176">Power BI</span></span>
<span data-ttu-id="18f97-177">Bunu bile daha derin çözümleme yapabilirsiniz, [hello veri tooMicrosoft Power BI verme](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="18f97-177">You can do even deeper analysis if you [export hello data tooMicrosoft Power BI](app-insights-export-power-bi.md).</span></span>

## <a name="sample-microsoft-dynamics-crm-solution"></a><span data-ttu-id="18f97-178">Örnek Microsoft Dynamics CRM çözümü</span><span class="sxs-lookup"><span data-stu-id="18f97-178">Sample Microsoft Dynamics CRM Solution</span></span>
<span data-ttu-id="18f97-179">[Microsoft Dynamics CRM uygulanan hello örnek çözümü işte](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="18f97-179">[Here is hello sample solution implemented in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="learn-more"></a><span data-ttu-id="18f97-180">Daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="18f97-180">Learn more</span></span>
* [<span data-ttu-id="18f97-181">Application Insights nedir?</span><span class="sxs-lookup"><span data-stu-id="18f97-181">What is Application Insights?</span></span>](app-insights-overview.md)
* [<span data-ttu-id="18f97-182">Web sayfaları için Application Insights</span><span class="sxs-lookup"><span data-stu-id="18f97-182">Application Insights for web pages</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="18f97-183">Daha fazla örnekleri ve izlenecek yollar</span><span class="sxs-lookup"><span data-stu-id="18f97-183">More samples and walkthroughs</span></span>](app-insights-code-samples.md)
