---
title: "Azure IOT paketi aaaCustomize bağlı Fabrika | Microsoft Docs"
description: "Merhaba toocustomize hello davranışını Fabrika nasıl bağlı bir açıklama önceden yapılandırılmış çözümü."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: c#
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 53f2fef7a76b5d8e6ad023945a7812dc7fabd12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-how-hello-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a>Merhaba Fabrika çözüm görüntüler veri OPC UA sunucularınızdan nasıl bağlanacağını özelleştirme

## <a name="introduction"></a>Giriş

Merhaba bağlı Fabrika çözüm toplar ve hello OPC UA sunucuları bağlı toohello çözüm verileri görüntüler. Göz atın ve komutları toohello OPC UA sunucuları çözümünüzde gönderir. Merhaba OPC UA hakkında daha fazla bilgi için bkz: [bağlı Fabrika SSS](iot-suite-faq-cf.md).

Merhaba çözümde toplanan veri örnekleri hello genel donanım verimliliği (OEE) ve başlangıç panosunda hello Fabrika, satır ve istasyon düzeylerinde görüntüleyebileceğiniz ana performans göstergelerini (KPI'lar) içerir. Merhaba aşağıdaki ekran görüntüsünde hello OEE KPI için ve değerleri hello gösterir **derleme** istasyon, üzerinde **üretim satırı 1**, hello içinde **Münih** Fabrika:

![Merhaba çözümde OEE ve KPI değerleri örneği][img-oee-kpi]

hello çözüm etkinleştirir, tooview belirli veri öğelerinden bilgilerinden ayrıntılı olarak bilinen OPC UA sunucuları hello *istasyonları*. Merhaba aşağıdaki ekran görüntüsü hello sayının belirli bir istasyondan üretilen öğelerinin çizimleri gösterir:

![Çizimler üretilen öğe sayısı][img-manufactured-items]

Merhaba grafikleri birini tıklatın, daha fazla zaman serisi Öngörüler (TSI) kullanarak hello veri da gözden geçirebilirsiniz:

![Zaman serisi Öngörüler kullanarak verileri keşfedin][img-tsi]

Bu makalede açıklanır:

- Nasıl hello veri kullanılabilir toohello çeşitli görünümleri hello çözümde yapılır.
- Merhaba şekilde hello çözümü nasıl özelleştirebileceğiniz hello verilerini görüntüler.

## <a name="data-sources"></a>Veri kaynakları

Merhaba bağlı Fabrika çözüm hello OPC UA sunucuları bağlı toohello çözüm verileri görüntüler. Merhaba varsayılan yükleme Fabrika benzetimi birkaç OPC UA sunucuları içerir. Kendi OPC UA sunucuları ekleyebilirsiniz, [bir ağ geçidi üzerinden bağlanma] [ lnk-connect-cf] tooyour çözümü.

Bağlı bir OPC UA sunucuya hello panosunda tooyour çözüm gönderebilirsiniz hello veri öğeleri göz atabilirsiniz:

1. Toohello gidin **OPC UA sunucuyu seçin** görünümü:

    ![Toohello seçin OPC UA sunucu görünümü gidin][img-select-server]

1. Bir sunucu seçin ve tıklatın **Bağlan**. Tıklatın **İlerle** zaman hello güvenlik uyarısı görüntülenmez.

    > [!NOTE]
    > Bu uyarı yalnızca bir kez her sunucu için görünür ve hello çözüm Panosu hello sunucu arasında bir güven ilişkisi oluşturur.

1. Sunucu hello Gözat hello veri öğeleri toohello çözüm gönderebilirsiniz artık kullanabilirsiniz. Toohello Çözüm gönderilen öğeleri yeşil bir onay işareti vardır:

    ![Yayımlanan öğeler][img-published]

1. Kullanıyorsanız bir *yönetici* hello çözümde, bir veri öğesi toomake toopublish seçebilirsiniz hello kullanılabilir bağlı Fabrika çözümü. Yönetici olarak, veri öğeleri hello değerini değiştirin ve hello OPC UA server yöntemlerini çağırın.

## <a name="map-hello-data"></a>Merhaba verileri eşleme

Fabrika çözüm eşlemeleri Hello bağlı ve toplamalar hello hello OPC UA sunucu toohello veri öğeleri çeşitli görünümleri hello çözümde yayımlanır. Merhaba çözüm sağladığınızda hello bağlı Fabrika çözüm tooyour Azure hesabı dağıtır. Merhaba bağlı Visual Studio Fabrika çözümü JSON dosyasında bu eşleme bilgilerini depolar. Görüntüleyin ve bu hello bağlı Fabrika Visual Studio çözümü JSON yapılandırma dosyasında değiştirin. Değişikliği yaptıktan sonra hello çözümü yeniden dağıtabilirsiniz.

Merhaba yapılandırma dosyasına kullanabilirsiniz:

- Merhaba varolan sanal oluşturucuları, Üretim satırları ve istasyonları düzenleyin.
- Toohello çözümü bağlantı gerçek OPC UA sunuculardan verileri eşleyin.

tooclone hello bir kopyasını Fabrika Visual Studio çözümü, git komut aşağıdaki kullanım hello bağlı:

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

Merhaba dosya **ContosoTopologyDescription.json** OPC UA sunucu verilerini hello eşleme öğeleri toohello görünümleri hello bağlı Fabrika çözüm panosunda hello tanımlar. Bu yapılandırma dosyası hello bulabilirsiniz **Contoso\Topology** hello klasöründe **WebApp** hello Visual Studio çözümü projesinde.

Merhaba JSON dosyası Merhaba içeriğine hiyerarşisini Fabrika, üretim hattı ve istasyon düğümler düzenlenir. Bu hiyerarşi hello Gezinti hiyerarşisinde hello bağlı Fabrika panosunda tanımlar. Her düğümde hello hiyerarşisinin değerler hello panosunda görüntülenen hello bilgileri belirler. Örneğin, hello JSON dosyası hello Münih Fabrika için değerleri aşağıdaki hello içerir:

```json
"Guid": "73B534AE-7C7E-4877-B826-F1C0EA339F65",
"Name": "Munich",
"Description": "Braking system",
"Location": {
    "City": "Munich",
    "Country": "Germany",
    "Latitude": 48.13641,
    "Longitude": 11.57754
},
"Image": "munich.jpg"
```

Merhaba adını, açıklamasını ve konum bu hello Pano görünümünde görünür:

![Merhaba Pano Münih verileri][img-munich]

Her fabrika, üretim hattı ve istasyon bir görüntü özelliği vardır. Bu JPEG dosyaları hello bulabilirsiniz **Content\img** hello klasöründe **WebApp** projesi. Bu görüntü dosyalar hello bağlı Fabrika panosunda görüntülenir.

Her istasyon OPC UA hello veri öğeleri eşleme hello tanımlayan çeşitli ayrıntılı özellikleri içerir. Bu özellikleri hello aşağıdaki bölümlerde açıklanmıştır:

### <a name="opcuri"></a>OpcUri

Merhaba **OpcUri** hello OPC UA uygulama URI'hello OPC UA sunucu benzersiz olarak tanıtan bir değerdir. Örneğin, hello **OpcUri** hello derleme istasyon Münih 1 satırda üretim hello şuna benzeyen için bir değer: **urn: scada2194:ua:munich:productionline0:assemblystation**.

Merhaba çözüm panosunda hello bağlı hello OPC UA sunucularının URI'ler görüntüleyebilirsiniz:

![OPC UA sunucusu URI görüntülemek][img-server-uris]

### <a name="simulation"></a>Benzetim

Merhaba hello bilgilerinde **benzetimi** belirli toohello hello varsayılan olarak sağlanan OPC UA sunucuları çalıştıran OPC UA benzetimi düğümdür. Gerçek bir OPC UA sunucusu için kullanılmaz.

### <a name="kpi1-and-kpi2"></a>Kpi1 ve kpı2

Bu düğümler hello istasyon verilerden toohello iki KPI değerleri hello panosunda nasıl katkıda açıklanmaktadır. Varsayılan dağıtımında, bu KPI saat başına birim ve saatte kWh değerlerdir. Merhaba çözüm KPI değerlerinde bir istasyonun hello düzeyinde hesaplar ve bunları hello üretim hattı ve Fabrika düzeylerinde toplar.

Her KPI minimum, maksimum ve hedef değer vardır. Her bir KPI değeri bağlı hello Fabrika çözüm tooperform için uyarı eylemleri de tanımlayabilirsiniz. Merhaba aşağıdaki kod parçacığında hello KPI hello derleme istasyon tanımlarında satırdaki üretim Münih 1 gösterir:

```json
"Kpi1": {
  "Minimum": 150,
  "Target": 300,
  "Maximum": 600
},
"Kpi2": {
  "Minimum": 50,
  "Target": 100,
  "Maximum": 200,
  "MinimumAlertActions": [
    {
      "Type": "None"
    }
  ]
}
```

Merhaba aşağıdaki ekran görüntüsünde hello KPI verileri hello panosunda gösterir.

![KPI bilgilerini hello panosunda][lnk-kpi]

### <a name="opcnodes"></a>OpcNodes

Merhaba **OpcNodes** düğümleri tanımlamak hello OPC UA sunucu yayımlanan veri öğeleri hello ve belirtin nasıl tooprocess verileri.

Merhaba **nodeId** değeri tanımlar hello hello OPC UA sunucu gelen belirli OPC UA nodeId. Merhaba ilk düğüm hello derleme istasyon üretim satırının Münih 1 değerine sahip **ns = 2; ı 385 =**. A **nodeId** değeri belirten hello veri öğesi tooread hello OPC UA sunucu ve hello **SymbolicName** bu veriler için bir kolay ad toouse hello panosunda sağlar.

Her düğüm ile ilişkili diğer değerler, aşağıdaki tablonun hello özetlenmiştir:

| Değer | Açıklama |
| ----- | ----------- |
| İlgi Düzeyi  | Merhaba KPI'yı ve OEE değerleri için bu verileri katkıda bulunur. |
| İşlem kodu     | Merhaba verileri nasıl toplanır. |
| Birimler      | Merhaba birimleri toouse hello panosunda.  |
| Görünür    | Toodisplay bu değer olup olmadığını hello Pano. Bazı değerler hesaplamalarında kullanılır ancak görüntülenmez.  |
| Maksimum    | Merhaba panosunda uyarıyı tetikleyen hello en büyük değer. |
| MaximumAlertActions | Bir eylem tootake yanıt tooan uyarısında. Örneğin, bir komut tooa istasyon gönderir. |
| ConstValue | Bir hesaplanmasında kullanılan sabit bir değer. |

## <a name="deploy-hello-changes"></a>Merhaba değişiklikleri dağıtma

Değişiklikleri toohello yapmadan tamamladığınızda **ContosoTopologyDescription.json** gerekir dağıtmanız dosyası hello bağlı Fabrika çözüm tooyour Azure hesabı.

Merhaba **azure-IOT-bağlı-Fabrika** deposu içeren bir **build.ps1** toorebuild kullanın ve hello çözümü dağıtmak PowerShell komut dosyası.

## <a name="next-steps"></a>Sonraki Adımlar

Bağlı hello Fabrika önceden yapılandırılmış çözüm hakkında daha fazla tarafından okuma hello makaleleri aşağıdaki bilgi:

* [Önceden yapılandırılmış bağlı fabrika çözümü yönergeleri][lnk-rm-walkthrough]
* [Bağlı üreteci için bir ağ geçidi dağıtma][lnk-connect-cf]
* [Merhaba azureiotsuite.com sitesindeki izinler][lnk-permissions]
* [Bağlı fabrika hakkında SSS](iot-suite-faq-cf.md)
* [SSS][lnk-faq]


[img-oee-kpi]: ./media/iot-suite-connected-factory-customize/oeenadkpi.png
[img-manufactured-items]: ./media/iot-suite-connected-factory-customize/manufactured.png
[img-tsi]: ./media/iot-suite-connected-factory-customize/tsi.png
[img-select-server]: ./media/iot-suite-connected-factory-customize/selectserver.png
[img-published]: ./media/iot-suite-connected-factory-customize/published.png
[img-munich]: ./media/iot-suite-connected-factory-customize/munich.png
[img-server-uris]: ./media/iot-suite-connected-factory-customize/serveruris.png
[lnk-kpi]: ./media/iot-suite-connected-factory-customize/kpidisplay.png

[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md