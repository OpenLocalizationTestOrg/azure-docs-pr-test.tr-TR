---
title: aaaMonitor Azure Cosmos DB istekleri ve depolama | Microsoft Docs
description: "Toomonitor Azure Cosmos DB nasıl hesap istekleri ve sunucu hataları gibi performans ölçümleri ve depolama alanı tüketimi gibi kullanım ölçümleri öğrenin."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 4c6a2e6f-6e78-48e3-8dc6-f4498b235a9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: mimig
ms.openlocfilehash: aea029d10717236a573a080dab9d06d87f97f318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-cosmos-db-requests-usage-and-storage"></a>Azure Cosmos DB istekleri, kullanım ve depolama izleme
Azure Cosmos DB hesaplarınızdaki hello izleyebilirsiniz [Azure portal](https://portal.azure.com/). Her Azure Cosmos DB hesap için istekleri ve sunucu hataları ve depolama alanı tüketimi gibi kullanım ölçümleri gibi her iki performans ölçümleri kullanılabilir.

Ölçümleri hello hesabı dikey penceresinde, hello yeni ölçümleri dikey veya Azure İzleyicisi'nde incelenebilir.

## <a name="view-performance-metrics-on-hello-metrics-blade"></a>Merhaba ölçümleri dikey görünüm performans ölçümleri
1. Merhaba, [Azure portal](https://portal.azure.com/), tıklatın **daha Hizmetleri**, çok kaydırma**veritabanları**, tıklatın **Azure Cosmos DB**ve ardından hello hello adına tıklayın Azure Cosmos DB hesabı tooview performans ölçümleri istiyorsunuz.
2. Merhaba kaynak menüde altında **izleme**, tıklatın **ölçümleri**.

Merhaba ölçüm dikey penceresi açılır ve hello koleksiyonu tooreview seçebilirsiniz. Kullanılabilirlik, istekleri, üretilen iş ve depolama ölçümleri gözden geçirin ve bunları toohello Azure Cosmos DB SLA karşılaştırın.

## <a name="view-performance-metrics-by-using-azure-monitoring"></a>Azure Monitoring kullanarak görünüm performans ölçümleri
1. Merhaba, [Azure portal](https://portal.azure.com/), tıklatın **İzleyici** hello atlama çubuğu üzerinde.
2. Merhaba kaynak menüye tıklayın **ölçümleri**.
3. Merhaba, **İzleyicisi - ölçümleri** penceresinde hello **kaynak grubu** açılır menüsünde, select hello kaynak grubu toomonitor istediğiniz hello Azure Cosmos DB hesabıyla ilişkilendirilmiş. 
4. Merhaba, **kaynak** açılır menü, select hello veritabanı hesabı toomonitor.
5. Merhaba listesinde **kullanılabilir ölçümler**, hello ölçümleri toodisplay seçin. Merhaba CTRL düğmesini toomulti Seç kullanın. 

    Ölçümlerinizi hello görüntülenir **çizim** penceresi. 

## <a name="view-performance-metrics-on-hello-account-blade"></a>Merhaba hesabı dikey görünüm performans ölçümleri
1. Merhaba, [Azure portal](https://portal.azure.com/), tıklatın **daha Hizmetleri**, çok kaydırma**veritabanları**, tıklatın **Azure Cosmos DB**ve ardından hello hello adına tıklayın Azure Cosmos DB hesabı tooview performans ölçümleri istiyorsunuz.
2. Merhaba **izleme** Mercek döşeme varsayılan olarak aşağıdaki hello görüntüler:
   
   * Merhaba geçerli gün için toplam istek sayısı.
   * Kullanılan depolama alanı.
   
   Tablonuz görüntülerse **kullanılabilir veri yok** ve veritabanınızda veri oluşturduğumuza inanıyoruz, hello bkz [sorun giderme](#troubleshooting) bölümü.
   
   ![Merhaba istekleri ve hello depolama kullanımını gösteren hello izleme Mercek ekran görüntüsü](./media/monitor-accounts/documentdb-total-requests-and-usage.png)
3. Merhaba üzerinde tıklatarak **istekleri** veya **kullanım kotası** döşeme açılır bir ayrıntılı **ölçüm** dikey.
4. Merhaba **ölçüm** dikey penceresinde hello ölçümleri seçtiğiniz ayrıntılarını gösterir.  Merhaba hello dikey pencerenin üst isteklerinin bir grafik saatlik grafiği, daraltılmış ve toplam istekleri toplama değerlerini gösteren tablo olan ise.  Merhaba ölçüm dikey penceresi de hello listesini hello Geçerli ölçüm dikey penceresinde görüntülenmesini tanımlanan, filtrelenmiş toohello ölçümleri silinmiş uyarıları gösterir (uyarıların sayısı varsa bu şekilde, yalnızca hello Burada sunulan ilgili olanları görürsünüz).   
   
   ![İstekleri içeren hello ölçüm dikey penceresinin ekran görüntüsü kısıtlanan](./media/monitor-accounts/documentdb-metric-blade.png)

## <a name="customize-performance-metric-views-in-hello-portal"></a>Merhaba portalında performans ölçümü görünümlerini özelleştirme
1. belirli bir grafik görüntüler toocustomize hello ölçümleri tıklatın hello grafik tooopen hello içinde **ölçüm** dikey ve ardından **grafiği Düzenle**.  
   ![Vurgulanan grafiği Düzenle de hello ölçüm dikey penceresi denetimleriyle ekran görüntüsü](./media/monitor-accounts/madocdb3.png)
2. Merhaba üzerinde **grafiği Düzenle** dikey penceresinde hello grafik, aynı zamanda bunların zaman aralığını görüntüleme seçenekleri toomodify hello ölçümleri vardır.  
   ![Merhaba grafiği Düzenle dikey penceresi ekran görüntüsü](./media/monitor-accounts/madocdb4.png)
3. Merhaba bölümünde görüntülenen toochange hello ölçümleri seçmeniz yeterlidir veya hello kullanılabilir performans ölçümleri temizleyin ve ardından **Tamam** hello dikey penceresinde hello sonundaki.  
4. toochange hello zaman aralığı, farklı bir aralık seçin (örneğin, **özel**) ve ardından **Tamam** hello dikey penceresinde hello sonundaki.  
   
   ![Ekran görüntüsü hello zaman aralığı hello grafiği Düzenle dikey gösteren parçası nasıl tooenter özel zaman aralığı](./media/monitor-accounts/madocdb5.png)

## <a name="create-side-by-side-charts-in-hello-portal"></a>Merhaba Portalı'nda yan yana grafikleri oluşturma
Hello Azure Portal toocreate yan yana ölçüm grafikleri sağlar.  

1. İlk olarak, toocopy istediğiniz ve seçin hello grafik üzerinde sağ **Özelleştir**.
   
   ![Merhaba toplam istek sayısı hello Özelleştir seçeneği vurgulanmış grafikle ekran görüntüsü](./media/monitor-accounts/madocdb6.png)
2. Tıklatın **kopya** hello menüsü toocopy hello bölümü ve ardından **özelleştirme Bitti**.
   
   ![Merhaba kopya ile Merhaba toplam istek sayısı grafiğinin görüntüsü ve vurgulanan özelleştirme seçenekleri bitti ekranı](./media/monitor-accounts/madocdb7.png)  

Merhaba bölümünde görüntülenen hello ölçümleri ve saat aralığı özelleştirme herhangi diğer ölçüm bir parçası olarak, artık bu bölümü kabul.  Bunu yaparak, iki farklı ölçümleri grafik yan yana hello adresindeki görebilirsiniz aynı anda.  
    ![Ekran görüntüsü hello toplam istek sayısı grafik ve hello saat grafik geçmiş yeni toplam istek sayısı](./media/monitor-accounts/madocdb8.png)  

## <a name="set-up-alerts-in-hello-portal"></a>Merhaba Portal'da uyarılarını ayarlama
1. Hello içinde [Azure portal](https://portal.azure.com/), tıklatın **daha Hizmetleri**, tıklatın **Azure Cosmos DB**ve ardından toosetup kendisi için istediğinizi hello Azure Cosmos DB hesap hello adına tıklayın performans ölçüm uyarıları.
2. Merhaba kaynak menüye tıklayın **uyarı kuralları** tooopen hello uyarı kuralları dikey.  
   ![Bölümü seçili ekran görüntüsü hello uyarı kuralları](./media/monitor-accounts/madocdb10.5.png)
3. Merhaba, **uyarı kuralları** dikey penceresinde tıklatın **uyarı Ekle**.  
   ![Merhaba uyarı Ekle düğmesi vurgulanan hello uyarı kuralları dikey penceresinin ekran görüntüsü](./media/monitor-accounts/madocdb11.png)
4. Merhaba, **uyarı kuralı eklemek** dikey penceresinde belirtin:
   
   * Merhaba uyarı kuralı ayarladığınız Hello adı.
   * Merhaba yeni uyarı kuralı açıklaması.
   * Merhaba ölçüm hello uyarı kuralı.
   * Merhaba koşul, eşik ve süresi belirleyen zaman hello uyarı etkinleştirir. Örneğin, bir sunucu hatası sayısı 5'ten büyük hello son 15 dakika içinde.
   * Merhaba uyarı oluşturulduğunda olup hello Hizmet Yöneticisi ve coadministrators e-posta gönderilir.
   * Uyarı bildirimleri için ek e-posta adresleri.  
     ![Merhaba Ekle bir uyarı kuralı dikey penceresinin ekran görüntüsü](./media/monitor-accounts/madocdb12.png)

## <a name="monitor-azure-cosmos-db-programatically"></a>Azure Cosmos DB programlı şekilde izleme
Hesap düzeyindeki ölçümlerini hello Portalı'nda kullanılabilir Merhaba, hesap depolama gibi kullanım ve toplam istek hello DocumentDB API kullanılabilir değildir. Ancak, kullanım verilerini hello koleksiyonu düzeyinde hello DocumentDB API'lerini kullanarak alabilirsiniz. tooretrieve koleksiyon düzeyinde veri, hello aşağıdaki:

* toouse hello REST API [hello koleksiyonda bir GET gerçekleştirmek](https://msdn.microsoft.com/library/mt489073.aspx). Merhaba koleksiyonu için Hello kota ve kullanım bilgilerini hello x-ms-resource-quota ve x-ms-kaynak kullanım üstbilgileri hello yanıt döndürülür.
* toouse hello .NET SDK'yı kullanmak hello [DocumentClient.ReadDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.readdocumentcollectionasync.aspx) döndürür yöntemi bir [ResourceResponse](https://msdn.microsoft.com/library/dn799209.aspx) gibi bir dizi kullanım özellikleri içeren  **CollectionSizeUsage**, **DatabaseUsage**, **DocumentUsage**ve daha fazlası.

tooaccess ek ölçümler kullanmak hello [Azure İzleyici SDK](https://www.nuget.org/packages/Microsoft.Azure.Insights). Kullanılabilir ölçüm tanımlarını çağırarak alınabilir:

    https://management.azure.com/subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metricDefinitions?api-version=2015-04-08

Biçim aşağıdaki sorguları tooretrieve tek tek ölçümleri kullanım hello:

    https://management.azure.com/subscriptions/{SubecriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metrics?api-version=2015-04-08&$filter=%28name.value%20eq%20%27Total%20Requests%27%29%20and%20timeGrain%20eq%20duration%27PT5M%27%20and%20startTime%20eq%202016-06-03T03%3A26%3A00.0000000Z%20and%20endTime%20eq%202016-06-10T03%3A26%3A00.0000000Z

Daha fazla bilgi için bkz: [alma kaynak ölçümleri'hello Azure İzleyici REST API'si aracılığıyla](https://blogs.msdn.microsoft.com/cloud_solution_architect/2016/02/23/retrieving-resource-metrics-via-the-azure-insights-api/). "Azure Inights" adlandırıldı Not "Azure İzleyicisi".  Bu blog girdisi toohello eski adı gösterir.

## <a name="troubleshooting"></a>Sorun giderme
Görüntü hello bölmeleri, izleme, **kullanılabilir veri yok** ileti ve yakın zamanda yapılan istekleri veya veri toohello veritabanı eklenen, hello döşeme tooreflect hello son kullanımını düzenleyebilirsiniz.

### <a name="edit-a-tile-toorefresh-current-data"></a>Döşeme toorefresh geçerli verileri düzenleme
1. belirli bir bölümünde görüntülenecek toocustomize hello ölçümleri tıklatın hello grafik tooopen hello **ölçüm** dikey ve ardından **grafiği Düzenle**.  
   ![Vurgulanan grafiği Düzenle de hello ölçüm dikey penceresi denetimleriyle ekran görüntüsü](./media/monitor-accounts/madocdb3.png)
2. Merhaba üzerinde **grafiği Düzenle** dikey penceresinde hello **zaman aralığı** 'yi tıklatın **saati aşan**ve ardından **Tamam**.  
   ![Seçili son bir saat hello grafiği Düzenle dikey ekran görüntüsü](./media/monitor-accounts/documentdb-no-available-data-past-hour.png)
3. Kutucuğunuzun, artık geçerli veri ve kullanım gösteren yenilemeniz gerekir.  
   ![Ekran görüntüsü güncelleştirilmiş hello toplam saat döşeme geçmiş istekleri](./media/monitor-accounts/documentdb-no-available-data-fixed.png)

## <a name="next-steps"></a>Sonraki adımlar
Azure Cosmos DB kapasite planlaması, hakkında daha fazla toolearn bkz hello [Azure Cosmos DB kapasite Planlayıcısı hesaplayıcı](https://www.documentdb.com/capacityplanner).

