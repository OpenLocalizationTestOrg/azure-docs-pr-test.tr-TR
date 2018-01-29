---
title: "Azure Application Insights ile Hızlı Başlangıç | Microsoft Docs"
description: "Application Insights ile izleme için Node.js Web Uygulamasını hızlıca ayarlamaya ilişkin yönergeler sağlar"
services: application-insights
keywords: 
author: mrbullwinkle
ms.author: mbullwin
ms.date: 09/10/2017
ms.service: application-insights
ms.custom: mvc
ms.topic: quickstart
manager: carmonm
ms.openlocfilehash: b2c8b8cab312f581a9ceb14179a0a7cab94516d6
ms.sourcegitcommit: d247d29b70bdb3044bff6a78443f275c4a943b11
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/13/2017
---
# <a name="start-monitoring-your-nodejs-web-application"></a>Node.js Web Uygulamanızı İzlemeye Başlama

Azure Application Insights ile web uygulamanızı kullanılabilirlik, performans ve kullanım bakımından kolayca izleyebilirsiniz. Ayrıca, bir kullanıcının bildirmesini beklemeden uygulamanızdaki hataları hızlıca tanımlayıp tespit edebilirsiniz. Sürüm 0.20 SDK yayınından itibaren MongoDB, MySQL ve Redis dahil olmak üzere yaygın üçüncü taraf paketleri izleyebilirsiniz.

Bu hızlı başlangıç, Node.js için Application Insights SDK sürüm 0.22’yi var olan bir Node.js web uygulamasına eklerken size kılavuzluk eder.

## <a name="prerequisites"></a>Ön koşullar

Bu hızlı başlangıcı tamamlamak için:

- Bir Azure Aboneliği ve var olan bir Node.js web uygulaması gerekir.

Bir Node.js web uygulamanız yoksa [Node.js web uygulaması oluşturma hızlı başlangıcı](https://docs.microsoft.com/azure/app-service/app-service-web-get-started-nodejs)’nı izleyerek bir tane oluşturabilirsiniz.
 
Azure aboneliğiniz yoksa başlamadan önce [ücretsiz](https://azure.microsoft.com/free/) bir hesap oluşturun.

## <a name="log-in-to-the-azure-portal"></a>Azure portalında oturum açma

[Azure Portal](https://portal.azure.com/)’da oturum açın.

## <a name="enable-application-insights"></a>Application Insights'ı etkinleştirme

Application Insights, şirket içinde veya bulutta çalışmasından bağımsız olarak İnternet’e bağlı herhangi bir uygulamadan telemetri verilerini toplayabilir. Bu verileri görüntülemeyi başlatmak için aşağıdaki adımları kullanın.

1. **Yeni** > **İzleme + Yönetim** > **Application Insights**’ı seçin.

   ![Application Insights Kaynağı ekleme](./media/app-insights-nodejs-quick-start/001-u.png)

   Bir yapılandırma kutusu görünür; giriş alanlarını doldurmak için aşağıdaki tabloyu kullanın.

    | Ayarlar        | Değer           | Açıklama  |
   | ------------- |:-------------|:-----|
   | **Ad**      | Genel Olarak Benzersiz Değer | İzlemekte olduğunuz uygulamayı tanımlayan ad |
   | **Uygulama Türü** | Node.js Uygulaması | İzlemekte olduğunuz uygulamanın türü |
   | **Kaynak Grubu**     | myResourceGroup      | App Insights verilerini barındıran yeni kaynak grubunun adı |
   | **Konum** | Doğu ABD | Yakınınızda bulunan veya uygulamanızın barındırıldığı konumun yakınında olan bir konum seçin |

2. **Oluştur**'a tıklayın.

## <a name="configure-app-insights-sdk"></a>App Insights SDK’sını Yapılandırma

1. **Genel Bakış** > **Temel Bilgiler**’i seçin > Uygulamanızın **İzleme Anahtarı**’nı kopyalayın.

   ![Yeni App Insights kaynağı formu](./media/app-insights-nodejs-quick-start/003-Black.png)

2. Uygulamanıza Node.js için Application Insights SDK’sı ekleyin. Uygulamanızın kök klasörü çalıştırmasından:

   ```bash
   npm install applicationinsights --save
   ```

3. Uygulamanızın ilk .js dosyasını düzenleyin ve aşağıdaki iki satırı betiğinizin en üst kısmına ekleyin. [Node.js hızlı başlangıç uygulamasını kullanıyorsanız](https://docs.microsoft.com/azure/app-service/app-service-web-get-started-nodejs), index.js dosyasını değiştirin. &lt;instrumentation_key&gt; yerine uygulamanızın izleme anahtarını yazın. 

   ```JavaScript
   const appInsights = require('applicationinsights');
   appInsights.setup('<instrumentation_key>').start();
   ```

4. Uygulamanızı yeniden başlatın.

> [!NOTE]
> Verilerin portalda görünmesi 3-5 dakika sürer. Bu uygulama düşük trafikli bir test uygulaması ise, çoğu ölçümün yalnızca etkin istek veya gerçekleşen işlemler olduğunda yakalandığını aklınızda bulundurun.

## <a name="start-monitoring-in-the-azure-portal"></a>Azure portalında izlemeyi başlatma

1. Artık izleme anahtarınızı aldığınız Application Insights **Genel Bakış** sayfasını yeniden açarak o anda çalışan uygulamanıza ilişkin ayrıntıları görüntüleyebilirsiniz.

   ![Application Insights’a Genel Bakış Menüsü](./media/app-insights-nodejs-quick-start/004-Black.png)

2. Uygulama bileşenleriniz arasındaki bağımlılık ilişkilerinin görsel düzeni için **Uygulama haritası**’na tıklayın. Her bileşen yük, performans, hatalar ve uyarılar gibi KPI'leri gösterir.

   ![Uygulama Eşlemesi](./media/app-insights-nodejs-quick-start/005-Black.png)

3. **Uygulama Analizi** simgesine ![Uygulama Haritası simgesi](./media/app-insights-nodejs-quick-start/006.png) tıklayın.  Bu işlem, Application Insights tarafından toplanan tüm verileri analiz etmeye yönelik zengin bir sorgu dili sağlayan **Application Insights Analizi**’ni açar. Bu örnekte, istek sayısını grafik olarak işleyen bir sorgu oluşturulur. Diğer verileri çözümlemek için kendi sorgularınızı yazabilirsiniz.

   ![Belirli bir süre içindeki kullanıcı isteklerinin analiz grafiği](./media/app-insights-nodejs-quick-start/007-Black.png)

4. **Genel Bakış** sayfasına geri dönüp **Sistem Durumuna Genel Bakış zaman çizelgesi**’ni inceleyin.  Bu pano, gelen istek sayısı, bu isteklerin süresi ve oluşan hatalar dahil olmak üzere uygulamanızın sistem durumu hakkında istatistikler sağlar. 

   ![Sistem Durumuna Genel Bakış zaman çizelgesi grafikleri](./media/app-insights-nodejs-quick-start/008-Black.png)

   **Sayfa Görünümü Yükleme Süresi** grafiğini **istemci tarafı telemetri** verileriyle doldurmak üzere etkinleştirmek için, bu betiği izlemek istediğiniz her sayfaya ekleyin:

   ```HTML
   <!-- 
   To collect end-user usage analytics about your application, 
   insert the following script into each page you want to track.
   Place this code immediately before the closing </head> tag,
   and before any other scripts. Your first data will appear 
   automatically in just a few seconds.
   -->
   <script type="text/javascript">
     var appInsights=window.appInsights||function(config){
       function i(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s="AuthenticatedUserContext",h="start",c="stop",l="Track",a=l+"Event",v=l+"Page",y=u.createElement(o),r,f;y.src=config.url||"https://az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(y);try{t.cookie=u.cookie}catch(p){}for(t.queue=[],t.version="1.0",r=["Event","Exception","Metric","PageView","Trace","Dependency"];r.length;)i("track"+r.pop());return i("set"+s),i("clear"+s),i(h+a),i(c+a),i(h+v),i(c+v),i("flush"),config.disableExceptionTracking||(r="onerror",i("_"+r),f=e[r],e[r]=function(config,i,u,e,o){var s=f&&f(config,i,u,e,o);return s!==!0&&t["_"+r](config,i,u,e,o),s}),t
       }({
           instrumentationKey:"<insert instrumentation key>"
       });
       
       window.appInsights=appInsights;
       appInsights.trackPageView();
   </script>
   ```

5. **Araştır** üst bilgisinin altındaki **Tarayıcı** öğesine tıklayın. Burada, uygulamanızın sayfalarına ait performansla ilgili ölçümleri bulabilirsiniz. **Yeni grafik ekle**’ye tıklayarak ek özel görünümler oluşturabilir veya **Düzenle**’yi seçerek mevcut grafik türlerini, yüksekliğini, renk paletini, gruplandırmaları ve ölçümleri değiştirebilirsiniz.

   ![Sunucu ölçüm grafiği](./media/app-insights-nodejs-quick-start/009-Black.png)

Node.js izleme hakkında daha fazla bilgi için [ek App Insights Node.js belgelerine](app-insights-nodejs.md) bakın.

## <a name="clean-up-resources"></a>Kaynakları temizleme

Sonraki hızlı başlangıçlar veya öğreticilerle devam etmeyi planlıyorsanız, bu hızlı başlangıçta oluşturulan kaynakları silmeyin. Devam etmeyi planlamıyorsanız, Azure portalda bu hızlı başlangıç ile oluşturulan tüm kaynakları silmek için aşağıdaki adımları kullanın.

1. Azure portalında sol taraftaki menüden, **Kaynak grupları**’na tıklayın ve ardından **myResourceGroup**’a tıklayın.
2. Kaynak grubu sayfanızda, **Sil**’e tıklayın, metin kutusuna **myResourceGroup** yazın ve ardından **Sil**’e tıklayın.

## <a name="next-steps"></a>Sonraki adımlar

> [!div class="nextstepaction"]
> [Performans sorunlarını bulma ve tanılama](https://docs.microsoft.com/azure/application-insights/app-insights-analytics)
