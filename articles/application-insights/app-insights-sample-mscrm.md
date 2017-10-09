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
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a>İzlenecek yol: Telemetri Microsoft Dynamics CRM Online Application Insights kullanarak etkinleştirme
Bu makale size nasıl gösterir tooget telemetri verilerini [Microsoft Dynamics CRM Online](https://www.dynamics.com/) kullanarak [Azure Application Insights](https://azure.microsoft.com/services/application-insights/). Biz Application Insights betik tooyour uygulama ekleyerek, veri ve veri görselleştirme yakalama hello tam işleminde size kılavuzluk.

> [!NOTE]
> [Merhaba örnek çözümü Gözat](https://dynamicsandappinsights.codeplex.com/).
> 
> 

## <a name="add-application-insights-toonew-or-existing-crm-online-instance"></a>Application Insights toonew veya mevcut CRM Online örneği ekleme
toomonitor uygulamanıza Application Insights SDK'sı tooyour uygulama ekleyin. Merhaba SDK telemetri toohello gönderir [Application Insights portalındaki](https://portal.azure.com), burada bizim güçlü analizi ve tanılama araçları kullanabilir, veya hello veri toostorage verin.

### <a name="create-an-application-insights-resource-in-azure"></a>Application Insights kaynağı oluşturma
1. Alma [Microsoft Azure hesap](http://azure.com/pricing). 
2. Merhaba içine oturum [Azure portal](https://portal.azure.com) ve yeni bir Application Insights kaynağı ekleyin. Verilerinizi nereye işlenen ve görüntülenen budur.
   
    ![Tıklatın +, geliştirici Hizmetleri, Application Insights.](./media/app-insights-sample-mscrm/01.png)
   
    ASP.NET hello uygulama türü olarak seçin.
3. Merhaba Başlarken sayfasını açın ve Aç "İzleyici ve istemci tarafı tanılamak".
   
    ![Kod parçacığı web sayfanıza eklemek için](./media/app-insights-sample-mscrm/03.png)

**Merhaba kod sayfası açık tutmak getirin** sonraki adıma başka bir tarayıcı penceresinde hello sırada. Merhaba kod yakında gerekir. 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a>Microsoft Dynamics CRM JavaScript web kaynak oluşturma
1. Oturum açma ve CRM Online örneği yönetici ayrıcalıklarıyla açın.
2. Microsoft Dynamics CRM, özelleştirmeleri, Özelleştir hello sistem ayarları
   
    ![Microsoft Dynamics CRM ayarları](./media/app-insights-sample-mscrm/04.png)
   
    ![Ayarlar > özelleştirmeleri](./media/app-insights-sample-mscrm/05.png)

    ![Merhaba sistemi seçeneği özelleştirme](./media/app-insights-sample-mscrm/06.png)

1. Bir JavaScript kaynağı oluşturun.
   
    ![Yeni Web kaynağı iletişim kutusu](./media/app-insights-sample-mscrm/07.png)
   
    Select bir ad verin **komut dosyası (JScript)** ve açık hello metin düzenleyici.
   
    ![Açık hello metin düzenleyicisi](./media/app-insights-sample-mscrm/08.png)
2. Merhaba kodu Application Insights kopyalayın. Kopyalanırken emin tooignore komut dosyası etiketlerini olun. Ekran görüntüsünün altında bakın:
   
    ![İzleme anahtarı ayarlayın](./media/app-insights-sample-mscrm/09.png)
   
    Merhaba kodu uygulama ınsights kaynağınızı tanımlayan hello izleme anahtarını içerir.
3. Kaydedin ve yayımlayın.
   
    ![Kaydedin ve yayımlayın](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a>Gereç formlar
1. Microsoft CRM Online içinde hello hesap formunu açın
   
    ![Hesap formu](./media/app-insights-sample-mscrm/11.png)
2. Merhaba form özelliklerini açın
   
    ![Form Özellikleri](./media/app-insights-sample-mscrm/12.png)
3. Merhaba, oluşturduğunuz JavaScript web kaynağı ekleme
   
    ![Menü ekleme](./media/app-insights-sample-mscrm/13.png)
   
    ![Merhaba web kaynağı ekleyin](./media/app-insights-sample-mscrm/14.png)
4. Kaydet ve formu özelleştirmelerinizi yayımlayın.

## <a name="metrics-captured"></a>Yakalanan ölçümleri
Şimdi hello form için telemetri yakalamayı oluşturdunuz. Kullanıldığında, veri tooyour Application Insights kaynağı gönderilir.

Göreceğiniz hello veri örnekleri aşağıda verilmiştir.

#### <a name="application-health"></a>Uygulama durumu
![Örnek sayfa yükleme süresi](./media/app-insights-sample-mscrm/15.png)

![Örnek sayfa görünümleri grafik](./media/app-insights-sample-mscrm/16.png)

Tarayıcı özel durumlar:

![Tarayıcı özel durumlar grafik](./media/app-insights-sample-mscrm/17.png)

Daha fazla ayrıntı Hello grafik tooget tıklatın:

![Özel durumlar listesi](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a>Kullanım
![Kullanıcıları, oturumlar ve sayfa görünümleri](./media/app-insights-sample-mscrm/19.png)

![Sesion grafikleri](./media/app-insights-sample-mscrm/20.png)

![Tarayıcı sürümleri](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a>Tarayıcılar
![Sayfa yükleme süresi dökümü](./media/app-insights-sample-mscrm/22.png)

![Tarayıcı sürümü göre oturum sayısı](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a>Coğrafi konum
![Ülkeye göre oturum sayısı](./media/app-insights-sample-mscrm/24.png)

![Oturumların ve kullanıcıların ülkeye göre](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a>İç sayfa görünümü isteği
![Sayfa görünümü özeti](./media/app-insights-sample-mscrm/26.png)

![Sayfa görünümü etkinliklerine arama](./media/app-insights-sample-mscrm/27.png)

![Benzer sayfa görünümleri](./media/app-insights-sample-mscrm/28.png)

![Sayfa görünümü özellikleri](./media/app-insights-sample-mscrm/29.png)

![Oturum başına sayfa](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a>Örnek kod
[Merhaba örnek kod Gözat](https://dynamicsandappinsights.codeplex.com/).

## <a name="power-bi"></a>Power BI
Bunu bile daha derin çözümleme yapabilirsiniz, [hello veri tooMicrosoft Power BI verme](app-insights-export-power-bi.md).

## <a name="sample-microsoft-dynamics-crm-solution"></a>Örnek Microsoft Dynamics CRM çözümü
[Microsoft Dynamics CRM uygulanan hello örnek çözümü işte](https://dynamicsandappinsights.codeplex.com/).

## <a name="learn-more"></a>Daha fazla bilgi edinin
* [Application Insights nedir?](app-insights-overview.md)
* [Web sayfaları için Application Insights](app-insights-javascript.md)
* [Daha fazla örnekleri ve izlenecek yollar](app-insights-code-samples.md)
