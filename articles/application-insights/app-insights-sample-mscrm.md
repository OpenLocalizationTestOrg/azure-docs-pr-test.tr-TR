---
title: Microsoft Dynamics CRM ve Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: a9593d5f198e05db80451a599428a296ed02e781
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a><span data-ttu-id="a8ef9-104">İzlenecek yol: Telemetri Microsoft Dynamics CRM Online Application Insights kullanarak etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="a8ef9-104">Walkthrough: Enabling Telemetry for Microsoft Dynamics CRM Online using Application Insights</span></span>
<span data-ttu-id="a8ef9-105">Bu makalede, telemetri verilerini alma gösterilmektedir [Microsoft Dynamics CRM Online](https://www.dynamics.com/) kullanarak [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="a8ef9-105">This article shows you how to get telemetry data from [Microsoft Dynamics CRM Online](https://www.dynamics.com/) using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span></span> <span data-ttu-id="a8ef9-106">Biz uygulamanıza Application Insights komut dosyası ekleme tamamlandı işlemini veri ve veri görselleştirme yakalama yol.</span><span class="sxs-lookup"><span data-stu-id="a8ef9-106">We’ll walk through the complete process of adding Application Insights script to your application, capturing data, and data visualization.</span></span>

> [!NOTE]
> <span data-ttu-id="a8ef9-107">[Örnek çözümü Gözat](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="a8ef9-107">[Browse the sample solution](https://dynamicsandappinsights.codeplex.com/).</span></span>
> 
> 

## <a name="add-application-insights-to-new-or-existing-crm-online-instance"></a><span data-ttu-id="a8ef9-108">Yeni veya mevcut CRM Online örneğine Application Insights ekleyin</span><span class="sxs-lookup"><span data-stu-id="a8ef9-108">Add Application Insights to new or existing CRM Online instance</span></span>
<span data-ttu-id="a8ef9-109">Uygulamanızı izlemek üzere uygulamanıza Application Insights SDK ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a8ef9-109">To monitor your application, you add an Application Insights SDK to your application.</span></span> <span data-ttu-id="a8ef9-110">SDK'sı telemetri gönderir [Application Insights portalındaki](https://portal.azure.com), burada bizim güçlü analizi ve tanılama araçları kullanabilir, veya verileri depolama alanına verin.</span><span class="sxs-lookup"><span data-stu-id="a8ef9-110">The SDK sends telemetry to the [Application Insights portal](https://portal.azure.com), where you can use our powerful analysis and diagnostic tools, or export the data to storage.</span></span>

### <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="a8ef9-111">Application Insights kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8ef9-111">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="a8ef9-112">Alma [Microsoft Azure hesap](http://azure.com/pricing).</span><span class="sxs-lookup"><span data-stu-id="a8ef9-112">Get [an account in Microsoft Azure](http://azure.com/pricing).</span></span> 
2. <span data-ttu-id="a8ef9-113">Oturum [Azure portal](https://portal.azure.com) ve yeni bir Application Insights kaynağı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a8ef9-113">Sign into the [Azure portal](https://portal.azure.com) and add a new Application Insights resource.</span></span> <span data-ttu-id="a8ef9-114">Verilerinizi nereye işlenen ve görüntülenen budur.</span><span class="sxs-lookup"><span data-stu-id="a8ef9-114">This is where your data will be processed and displayed.</span></span>
   
    ![Tıklatın +, geliştirici Hizmetleri, Application Insights.](./media/app-insights-sample-mscrm/01.png)
   
    <span data-ttu-id="a8ef9-116">Uygulama türü olarak ASP.NET’i seçin.</span><span class="sxs-lookup"><span data-stu-id="a8ef9-116">Choose ASP.NET as the application type.</span></span>
3. <span data-ttu-id="a8ef9-117">Başlarken sayfasını açın ve Aç "İzleyici ve istemci tarafı tanılamak".</span><span class="sxs-lookup"><span data-stu-id="a8ef9-117">Open the Getting Started page and open "Monitor and diagnose client side".</span></span>
   
    ![Kod parçacığı web sayfanıza eklemek için](./media/app-insights-sample-mscrm/03.png)

<span data-ttu-id="a8ef9-119">**Kod sayfası açık tutmak** başka bir tarayıcı penceresi sonraki adımda yaparken.</span><span class="sxs-lookup"><span data-stu-id="a8ef9-119">**Keep the code page open** while you do the next step in another browser window.</span></span> <span data-ttu-id="a8ef9-120">Kod yakında gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8ef9-120">You'll need the code soon.</span></span> 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a><span data-ttu-id="a8ef9-121">Microsoft Dynamics CRM JavaScript web kaynak oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8ef9-121">Create a JavaScript web resource in Microsoft Dynamics CRM</span></span>
1. <span data-ttu-id="a8ef9-122">Oturum açma ve CRM Online örneği yönetici ayrıcalıklarıyla açın.</span><span class="sxs-lookup"><span data-stu-id="a8ef9-122">Open your CRM Online instance and login with administrator privileges.</span></span>
2. <span data-ttu-id="a8ef9-123">Açık Microsoft Dynamics CRM ayarları, özelleştirmeleri, sistem özelleştirme</span><span class="sxs-lookup"><span data-stu-id="a8ef9-123">Open Microsoft Dynamics CRM Settings, Customizations, Customize the System</span></span>
   
    ![Microsoft Dynamics CRM ayarları](./media/app-insights-sample-mscrm/04.png)
   
    ![Ayarlar > özelleştirmeleri](./media/app-insights-sample-mscrm/05.png)

    ![Sistem seçeneği özelleştirme](./media/app-insights-sample-mscrm/06.png)

1. <span data-ttu-id="a8ef9-127">Bir JavaScript kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a8ef9-127">Create a JavaScript resource.</span></span>
   
    ![Yeni Web kaynağı iletişim kutusu](./media/app-insights-sample-mscrm/07.png)
   
    <span data-ttu-id="a8ef9-129">Select bir ad verin **komut dosyası (JScript)** ve metin düzenleyicisini açın.</span><span class="sxs-lookup"><span data-stu-id="a8ef9-129">Give it a name, select **Script (JScript)** and open the text editor.</span></span>
   
    ![Metin Düzenleyicisi'ni açın](./media/app-insights-sample-mscrm/08.png)
2. <span data-ttu-id="a8ef9-131">Kodu Application Insights kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="a8ef9-131">Copy the code from Application Insights.</span></span> <span data-ttu-id="a8ef9-132">Kopyalanırken komut dosyası etiketlerini yoksay emin olun.</span><span class="sxs-lookup"><span data-stu-id="a8ef9-132">While copying make sure to ignore script tags.</span></span> <span data-ttu-id="a8ef9-133">Ekran görüntüsünün altında bakın:</span><span class="sxs-lookup"><span data-stu-id="a8ef9-133">Refer below screenshot:</span></span>
   
    ![İzleme anahtarı ayarlayın](./media/app-insights-sample-mscrm/09.png)
   
    <span data-ttu-id="a8ef9-135">Kodu uygulama ınsights kaynağınızı tanımlayan izleme anahtarını içerir.</span><span class="sxs-lookup"><span data-stu-id="a8ef9-135">The code includes the instrumentation key that identifies your Application insights resource.</span></span>
3. <span data-ttu-id="a8ef9-136">Kaydedin ve yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="a8ef9-136">Save and publish.</span></span>
   
    ![Kaydedin ve yayımlayın](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a><span data-ttu-id="a8ef9-138">Gereç formlar</span><span class="sxs-lookup"><span data-stu-id="a8ef9-138">Instrument Forms</span></span>
1. <span data-ttu-id="a8ef9-139">Microsoft CRM Online içinde hesap formunu açın</span><span class="sxs-lookup"><span data-stu-id="a8ef9-139">In Microsoft CRM Online, open the Account form</span></span>
   
    ![Hesap formu](./media/app-insights-sample-mscrm/11.png)
2. <span data-ttu-id="a8ef9-141">Form özelliklerini açın</span><span class="sxs-lookup"><span data-stu-id="a8ef9-141">Open the form Properties</span></span>
   
    ![Form Özellikleri](./media/app-insights-sample-mscrm/12.png)
3. <span data-ttu-id="a8ef9-143">Oluşturduğunuz JavaScript web kaynağı ekleyin</span><span class="sxs-lookup"><span data-stu-id="a8ef9-143">Add the JavaScript web resource that you created</span></span>
   
    ![Menü ekleme](./media/app-insights-sample-mscrm/13.png)
   
    ![Web kaynağı ekleyin](./media/app-insights-sample-mscrm/14.png)
4. <span data-ttu-id="a8ef9-146">Kaydet ve formu özelleştirmelerinizi yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="a8ef9-146">Save and publish your form customizations.</span></span>

## <a name="metrics-captured"></a><span data-ttu-id="a8ef9-147">Yakalanan ölçümleri</span><span class="sxs-lookup"><span data-stu-id="a8ef9-147">Metrics captured</span></span>
<span data-ttu-id="a8ef9-148">Şimdi form için telemetri yakalamayı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="a8ef9-148">You have now set up telemetry capture for the form.</span></span> <span data-ttu-id="a8ef9-149">Kullanıldığında, verileri Application Insights kaynağınıza gönderilir.</span><span class="sxs-lookup"><span data-stu-id="a8ef9-149">Whenever it is used, data will be sent to your Application Insights resource.</span></span>

<span data-ttu-id="a8ef9-150">Göreceğiniz veri örnekleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a8ef9-150">Here are samples of the data that you'll see.</span></span>

#### <a name="application-health"></a><span data-ttu-id="a8ef9-151">Uygulama durumu</span><span class="sxs-lookup"><span data-stu-id="a8ef9-151">Application health</span></span>
![Örnek sayfa yükleme süresi](./media/app-insights-sample-mscrm/15.png)

![Örnek sayfa görünümleri grafik](./media/app-insights-sample-mscrm/16.png)

<span data-ttu-id="a8ef9-154">Tarayıcı özel durumlar:</span><span class="sxs-lookup"><span data-stu-id="a8ef9-154">Browser exceptions:</span></span>

![Tarayıcı özel durumlar grafik](./media/app-insights-sample-mscrm/17.png)

<span data-ttu-id="a8ef9-156">Daha fazla ayrıntı almak için grafiği tıklatın:</span><span class="sxs-lookup"><span data-stu-id="a8ef9-156">Click the chart to get more detail:</span></span>

![Özel durumlar listesi](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a><span data-ttu-id="a8ef9-158">Kullanım</span><span class="sxs-lookup"><span data-stu-id="a8ef9-158">Usage</span></span>
![Kullanıcıları, oturumlar ve sayfa görünümleri](./media/app-insights-sample-mscrm/19.png)

![Sesion grafikleri](./media/app-insights-sample-mscrm/20.png)

![Tarayıcı sürümleri](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a><span data-ttu-id="a8ef9-162">Tarayıcılar</span><span class="sxs-lookup"><span data-stu-id="a8ef9-162">Browsers</span></span>
![Sayfa yükleme süresi dökümü](./media/app-insights-sample-mscrm/22.png)

![Tarayıcı sürümü göre oturum sayısı](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a><span data-ttu-id="a8ef9-165">Coğrafi konum</span><span class="sxs-lookup"><span data-stu-id="a8ef9-165">Geolocation</span></span>
![Ülkeye göre oturum sayısı](./media/app-insights-sample-mscrm/24.png)

![Oturumların ve kullanıcıların ülkeye göre](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a><span data-ttu-id="a8ef9-168">İç sayfa görünümü isteği</span><span class="sxs-lookup"><span data-stu-id="a8ef9-168">Inside page view request</span></span>
![Sayfa görünümü özeti](./media/app-insights-sample-mscrm/26.png)

![Sayfa görünümü etkinliklerine arama](./media/app-insights-sample-mscrm/27.png)

![Benzer sayfa görünümleri](./media/app-insights-sample-mscrm/28.png)

![Sayfa görünümü özellikleri](./media/app-insights-sample-mscrm/29.png)

![Oturum başına sayfa](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a><span data-ttu-id="a8ef9-174">Örnek kod</span><span class="sxs-lookup"><span data-stu-id="a8ef9-174">Sample code</span></span>
<span data-ttu-id="a8ef9-175">[Örnek kod Gözat](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="a8ef9-175">[Browse the sample code](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="power-bi"></a><span data-ttu-id="a8ef9-176">Power BI</span><span class="sxs-lookup"><span data-stu-id="a8ef9-176">Power BI</span></span>
<span data-ttu-id="a8ef9-177">Bunu bile daha derin çözümleme yapabilirsiniz, [Microsoft Power BI için verileri dışa](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="a8ef9-177">You can do even deeper analysis if you [export the data to Microsoft Power BI](app-insights-export-power-bi.md).</span></span>

## <a name="sample-microsoft-dynamics-crm-solution"></a><span data-ttu-id="a8ef9-178">Örnek Microsoft Dynamics CRM çözümü</span><span class="sxs-lookup"><span data-stu-id="a8ef9-178">Sample Microsoft Dynamics CRM Solution</span></span>
<span data-ttu-id="a8ef9-179">[Microsoft Dynamics CRM uygulanan örnek çözümü işte](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="a8ef9-179">[Here is the sample solution implemented in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="learn-more"></a><span data-ttu-id="a8ef9-180">Daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="a8ef9-180">Learn more</span></span>
* [<span data-ttu-id="a8ef9-181">Application Insights nedir?</span><span class="sxs-lookup"><span data-stu-id="a8ef9-181">What is Application Insights?</span></span>](app-insights-overview.md)
* [<span data-ttu-id="a8ef9-182">Web sayfaları için Application Insights</span><span class="sxs-lookup"><span data-stu-id="a8ef9-182">Application Insights for web pages</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="a8ef9-183">Daha fazla örnekleri ve izlenecek yollar</span><span class="sxs-lookup"><span data-stu-id="a8ef9-183">More samples and walkthroughs</span></span>](app-insights-code-samples.md)
