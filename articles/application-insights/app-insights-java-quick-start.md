---
title: "Azure Application Insights ile Hızlı Başlangıç | Microsoft Docs"
description: "Application Insights ile izleme için Java Web Uygulamasını hızlıca ayarlamaya ilişkin yönergeler sağlar"
services: application-insights
keywords: 
author: mrbullwinkle
ms.author: mbullwin
ms.date: 09/10/2017
ms.service: application-insights
ms.custom: mvc
ms.topic: quickstart
manager: carmonm
ms.openlocfilehash: 9246def86fa647213aa3ec12427d829c24fa8034
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/08/2017
---
# <a name="start-monitoring-your-java-web-application"></a>Java Web Uygulamanızı İzlemeye Başlama

Azure Application Insights ile web uygulamanızı kullanılabilirlik, performans ve kullanım bakımından kolayca izleyebilirsiniz. Ayrıca, bir kullanıcının bildirmesini beklemeden uygulamanızdaki hataları hızlıca tanımlayıp tespit edebilirsiniz. Application Insights Java SDK ile MongoDB, MySQL ve Redis dahil olmak üzere yaygın üçüncü taraf paketleri izleyebilirsiniz.

Bu hızlı başlangıç, Application Insights SDK'sını var olan bir Java Dynamic Web Projesine eklerken size kılavuzluk eder.

## <a name="prerequisites"></a>Ön koşullar

Bu hızlı başlangıcı tamamlamak için:

- Oracle JRE 1.6 veya sonraki sürümleri ya da Zulu JRE 1.6 veya sonraki sürümleri yükleme
- [Ücretsiz Java EE Geliştiricileri için Eclipse IDE](http://www.eclipse.org/downloads/) yükleyin. Bu hızlı başlangıçta Eclipse Oxygen (4.7) kullanılır.
- Bir Azure Aboneliği ve var olan bir Java Dynamic Web Projesi gerekir
 
Bir Java Dynamic Web Projeniz yoksa [Java web uygulaması oluşturma hızlı başlangıcı](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-java) ile bir tane oluşturabilirsiniz.

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz](https://azure.microsoft.com/free/) bir hesap oluşturun.

## <a name="log-in-to-the-azure-portal"></a>Azure portalında oturum açma

[Azure Portal](https://portal.azure.com/)’da oturum açın.

## <a name="enable-application-insights"></a>Application Insights'ı etkinleştirme

Application Insights, şirket içinde veya bulutta çalışmasından bağımsız olarak İnternet’e bağlı herhangi bir uygulamadan telemetri verilerini toplayabilir. Bu verileri görüntülemeyi başlatmak için aşağıdaki adımları kullanın.

1. **Yeni** > **İzleme + Yönetim** > **Application Insights**’ı seçin.

   ![Application Insights Kaynağı ekleme](./media/app-insights-java-quick-start/001-j.png)

   Bir yapılandırma kutusu görünür; giriş alanlarını doldurmak için aşağıdaki tabloyu kullanın.

    | Ayarlar        | Değer           | Açıklama  |
   | ------------- |:-------------|:-----|
   | **Ad**      | Genel Olarak Benzersiz Değer | İzlemekte olduğunuz uygulamayı tanımlayan ad |
   | **Uygulama Türü** | Java web uygulaması | İzlemekte olduğunuz uygulamanın türü |
   | **Kaynak Grubu**     | myResourceGroup      | App Insights verilerini barındıran yeni kaynak grubunun adı |
   | **Konum** | Doğu ABD | Yakınınızda bulunan veya uygulamanızın barındırıldığı konumun yakınında olan bir konum seçin |

2. **Oluştur**'a tıklayın.

## <a name="install-app-insights-plugin"></a>App Insights Eklentisini yükleme

1. **Eclipse**’i başlatın > **Yardım**’a tıklayın > **Yeni Yazılım Yükle**’yi seçin.

   ![Yeni App Insights kaynağı formu](./media/app-insights-java-quick-start/000-j.png)

2. "Birlikte Çalış" alanına ```http://dl.microsoft.com/eclipse``` değerini kopyalayın > **Java için Azure Araç Seti**’ni işaretleyin > **Java için Application Insights Eklentisi**’ni seçin > "Gerekli yazılımı bulmak için yükleme sırasında tüm güncelleştirme siteleriyle iletişime geçin" seçeneğinin işaretini kaldırın.

3. Yükleme tamamlandıktan sonra **Eclipse’i Yeniden Başlatmanız** istenir.

## <a name="configure-app-insights-plugin"></a>App Insights Eklentisini Yapılandırma

1. **Eclipse**’i başlatın > **Projenizi** açın > **Proje Gezgini**’nde proje adına sağ tıklayın > **Azure**’u seçin > **Oturum Aç**’a tıklayın.

2. **Etkileşimli** Kimlik Doğrulama Yöntemini seçin > **Oturum Aç**’a tıklayın > Sorulduğunda **Azure kimlik bilgilerinizi** girin > **Azure Aboneliğinizi** seçin.

3. **Proje Gezgini**’nde projenizin adına sağ tıklayın > **Azure**’u seçin > **Application Insights’ı Yapılandır**’a tıklayın.

4. **Application Insights ile telemetriyi etkinleştir**’i işaretleyin > App Insights kaynağını ve Java uygulamanıza bağlamak istediğiniz **İzleme Anahtarı**’nı seçin.

   ![Eclipse Azure Yapılandırma Menüsü](./media/app-insights-java-quick-start/0007-j.png)

> [!NOTE]
> Java için Application Insights SDK’sı canlı ölçümleri yakalama ve görselleştirme özelliğine sahiptir, ancak telemetri koleksiyonunuzu ilk kez etkinleştirdiğinizde verilerin portalda görünmeye başlaması birkaç dakika sürebilir. Bu uygulama düşük trafikli bir test uygulaması ise, çoğu ölçümün yalnızca etkin istek veya işlem olduğunda yakalandığını aklınızda bulundurun.

## <a name="start-monitoring-in-the-azure-portal"></a>Azure portalında izlemeyi başlatın

1. Artık izleme anahtarınızı aldığınız Application Insights **Genel Bakış** sayfasını yeniden açarak o anda çalışan uygulamanıza ilişkin ayrıntıları görüntüleyebilirsiniz.

   ![Application Insights’a Genel Bakış Menüsü](./media/app-insights-java-quick-start/0008-j.png)

2. Uygulama bileşenleriniz arasındaki bağımlılık ilişkilerinin görsel düzeni için **Uygulama haritası**’na tıklayın. Her bileşen yük, performans, hatalar ve uyarılar gibi KPI'leri gösterir.

   ![Uygulama Eşlemesi](./media/app-insights-java-quick-start/005-j.png)

3. **Uygulama Analizi** simgesine ![Uygulama Haritası simgesi](./media/app-insights-java-quick-start/006.png) tıklayın. Bu işlem, Application Insights tarafından toplanan tüm verileri analiz etmeye yönelik zengin bir sorgu dili sağlayan **Application Insights Analizi**’ni açar. Bu örnekte, istek sayısını grafik olarak işleyen bir sorgu oluşturulur. Diğer verileri çözümlemek için kendi sorgularınızı yazabilirsiniz.

   ![Belirli bir süre içindeki kullanıcı isteklerinin analiz grafiği](./media/app-insights-java-quick-start/0010-j.png)

4. **Genel Bakış** sayfasına geri dönüp **Sistem Durumuna Genel Bakış zaman çizelgesi**’ni inceleyin.  Bu pano, gelen istek sayısı, bu isteklerin süresi ve oluşan hatalar dahil olmak üzere uygulamanızın sistem durumu hakkında istatistikler sağlar.

   ![Sistem Durumuna Genel Bakış zaman çizelgesi grafikleri](./media/app-insights-java-quick-start/0009-j.png)

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
        instrumentationKey:"<instrumentation key>"
    });

    window.appInsights=appInsights;
    appInsights.trackPageView();
   </script>
    ```

5. **Canlı Akış**’a tıklayın. Burada, Java web uygulamanızın performansıyla ilgili canlı ölçümleri bulabilirsiniz. **Canlı Ölçüm Akışı**, gelen istek sayısı, bu isteklerin süresi ve oluşan her türlü hata ile ilgili veriler içerir. Ayrıca, işlemci ve bellek gibi önemli performans ölçümlerini gerçek zamanlı olarak izleyebilirsiniz.

   ![Sunucu ölçüm grafikleri](./media/app-insights-java-quick-start/livemetricsjava.png)

Java izleme hakkında daha fazla bilgi için [ek App Insights Java belgelerine](.\app-insights-java-get-started.md) bakın.

## <a name="clean-up-resources"></a>Kaynakları temizleme

Sonraki hızlı başlangıçlar veya öğreticilerle devam etmeyi planlıyorsanız, bu hızlı başlangıçta oluşturulan kaynakları silmeyin. Devam etmeyi planlamıyorsanız, Azure portalda bu hızlı başlangıç ile oluşturulan tüm kaynakları silmek için aşağıdaki adımları kullanın.

1. Azure portalında sol taraftaki menüden, **Kaynak grupları**’na tıklayın ve ardından **myResourceGroup**’a tıklayın.
2. Kaynak grubu sayfanızda, **Sil**’e tıklayın, metin kutusuna **myResourceGroup** yazın ve ardından **Sil**’e tıklayın.

## <a name="next-steps"></a>Sonraki adımlar

> [!div class="nextstepaction"]
> [Performans sorunlarını bulma ve tanılama](https://docs.microsoft.com/azure/application-insights/app-insights-analytics)