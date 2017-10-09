---
title: "Azure Ağ İzleyicisi'ni ve açık kaynaklı araçları ile aaaPerform ağ izinsiz giriş algılama | Microsoft Docs"
description: "Bu makalede nasıl toouse Azure Ağ İzleyicisi'ni ve açık kaynaklı araçları tooperform izinsiz giriş algılama ağ açıklanır"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0f043f08-19e1-4125-98b0-3e335ba69681
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b5a909b827ab32ad6b2fd8e2911a944fd940249e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="perform-network-intrusion-detection-with-network-watcher-and-open-source-tools"></a>Ağ İzleyicisi'ni ve açık kaynaklı araçları ile ağ izinsiz giriş algılama gerçekleştirme

Paket yakalama ağ izinsiz giriş algılama sistemleri (Kimlikler) uygulama ve ağ güvenlik izleme (NSM) gerçekleştirmek için önemli bir bileşeni var. Paket yakalama işleyen ve olası ağ yetkisiz erişim ve kötü amaçlı etkinliği imzaları Ara birkaç açık kaynak Kimlikleri araç vardır. Ağ İzleyicisi tarafından sağlanan hello paket yakalamaları kullanarak, ağınızdaki herhangi bir zararlı yetkisiz ya da güvenlik açıkları için analiz edebilirsiniz.

Bu tür bir açık kaynak aracı Suricata, rulesets toomonitor ağ trafiğini kullanan ve şüpheli olaylar gerçekleştiğinde uyarıları tetikler Kimlikleri altyapının değil. Suricata yüksek hızda ve verimlilik ağ trafiğini analiz gerçekleştirebilir anlamına çok iş parçacıklı bir altyapı sunar. Suricata ve özelliklerini hakkında daha fazla ayrıntı için https://suricata-ids.org/ adresindeki kendi Web sitesini ziyaret edin.

## <a name="scenario"></a>Senaryo

Bu makalede nasıl ortamı tooperform yukarı tooset izinsiz giriş algılama, Suricata, Ağ İzleyicisi'ni kullanarak ağ ve esnek yığını hello açıklanmaktadır. Ağ İzleyicisi Merhaba paket ile kullanılan tooperform ağ izinsiz giriş algılama yakalar sağlar. Suricata işlemler hello paket yakalar ve tetikleyici uyarıları tehditleri verilen kendi ruleset eşleşen paketlere dayalı. Bu uyarılar yerel makinenizde bir günlük dosyasında depolanır. Merhaba esnek yığını kullanarak Suricata tarafından oluşturulan hello günlükleri sıralanabilir ve görsel bir hello günlükleri ve anlamına gelir tooquickly kazanç Öngörüler toopotential ağ güvenlik açıklarını sağlayan bir Kibana Pano toocreate kullanılır.  

![Basit web uygulaması senaryosu][1]

Her iki açık kaynaklı araçları bir Azure VM tooperform izin vererek bu çözümleme kendi Azure ağ ortamında ayarlanabilir.

## <a name="steps"></a>Adımlar

### <a name="install-suricata"></a>Suricata yükleyin

Tüm diğer yöntemleri yüklemesinin için http://suricata.readthedocs.io/en/latest/install.html ziyaret edin

1. Vm'nizin Hello komut satırı terminal hello aşağıdaki komutları çalıştırın:

    ```
    sudo add-apt-repository ppa:oisf/suricata-stable
    sudo apt-get update
    sudo sudo apt-get install suricata
    ```

1. tooverify hello komutu çalıştırarak kurulumunuzu `suricata -h` toosee hello komutların tam bir listesi.

### <a name="download-hello-emerging-threats-ruleset"></a>Merhaba Gelişmekte olan tehditleri ruleset indirin

Bu aşamada, biz Suricata toorun için herhangi bir kuralın sahip değilsiniz. Kendi kurallarınızı toodetect istediğiniz belirli tehditlerin tooyour ağ yok ya da geliştirilmiş kullanımı kural kümeleri sağlayıcıları, Gelişmekte olan tehditleri veya Snort VRT kurallardan gibi bir dizi de yapabilirsiniz oluşturabilirsiniz. Merhaba serbestçe erişilebilir Gelişmekte olan tehditleri ruleset burada kullanırız:

Merhaba kural kümesi indirin ve hello dizinine kopyalayın:

```
wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar zxf emerging.rules.tar.gz
sudo cp -r rules /etc/suricata/
```

### <a name="process-packet-captures-with-suricata"></a>İşlem paket ile Suricata yakalar.

tooprocess paket komutu aşağıdaki hello Çalıştır Suricata kullanarak yakalar:

```
sudo suricata -c /etc/suricata/suricata.yaml -r <location_of_pcapfile>
```
toocheck hello elde edilen uyarıları, Hello fast.log dosyasını okuyun:
```
tail -f /var/log/suricata/fast.log
```

### <a name="set-up-hello-elastic-stack"></a>Esnek yığını Hello ayarlayın

Bizim ağda olup bitenler hakkında değerli bilgiler Suricata üreten hello günlükleri bulunmasına karşın, bu günlük dosyaları hello kolay tooread değil ve anlayın. Suricata hello esnek yığını ile bağlayarak, biz Kibana Pano toosearch bize sağlar oluşturabilir, grafik, analiz ve bizim günlüklerinden Öngörüler türetilir.

#### <a name="install-elasticsearch"></a>Elasticsearch yükleyin

1. Merhaba esnek yığını sürüm 5.0 ve yukarıdaki Java 8 gerektirir. Merhaba komutu çalıştırmak `java -version` toocheck sürümünüzü. Yükleme, üzerinde toodocumentation bakın java yoksa [Oracle'nın Web sitesi](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)
1. Sisteminiz için doğru ikili paket Hello yükleyin:

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    Diğer yükleme yöntemleri bulunabilir [Elasticsearch yükleme](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)

1. Elasticsearch hello komutuyla çalıştığını doğrulayın:

    ```
    curl http://127.0.0.1:9200
    ```

    Bir yanıt benzer toothis görmeniz gerekir:

    ```
    {
    "name" : "Angela Del Toro",
    "cluster_name" : "elasticsearch",
    "version" : {
        "number" : "5.2.0",
        "build_hash" : "8ff36d139e16f8720f2947ef62c8167a888992fe",
        "build_timestamp" : "2016-01-27T13:32:39Z",
        "build_snapshot" : false,
        "lucene_version" : "6.1.0"
    },
    "tagline" : "You Know, for Search"
    }
    ```

Toohello sayfa yükleme esnek arama hakkında daha ayrıntılı yönergeler için bkz [yükleme](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)

### <a name="install-logstash"></a>Logstash yükleyin

1. tooinstall Logstash hello aşağıdaki komutları çalıştırın:

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. Ardından tooconfigure Logstash tooread eve.json dosyasının hello çıktısından gerekir. Kullanarak bir logstash.conf dosyası oluşturun:

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. Aşağıdaki içerik toohello dosyasına hello ekleyin (Bu hello yol toohello eve.json dosyası doğru olduğundan emin olun):

    ```ruby
    input {
    file {
        path => ["/var/log/suricata/eve.json"]
        codec =>  "json"
        type => "SuricataIDPS"
    }

    }

    filter {
    if [type] == "SuricataIDPS" {
        date {
        match => [ "timestamp", "ISO8601" ]
        }
        ruby {
        code => "
            if event.get('[event_type]') == 'fileinfo'
            event.set('[fileinfo][type]', event.get('[fileinfo][magic]').to_s.split(',')[0])
            end
        "
        }

        ruby{
        code => "
            if event.get('[event_type]') == 'alert'
            sp = event.get('[alert][signature]').to_s.split(' group ')
            if (sp.length == 2) and /\A\d+\z/.match(sp[1])
                event.set('[alert][signature]', sp[0])
            end
            end
            "
        }
    }

    if [src_ip]  {
        geoip {
        source => "src_ip"
        target => "geoip"
        #database => "/opt/logstash/vendor/geoip/GeoLiteCity.dat"
        add_field => [ "[geoip][coordinates]", "%{[geoip][longitude]}" ]
        add_field => [ "[geoip][coordinates]", "%{[geoip][latitude]}"  ]
        }
        mutate {
        convert => [ "[geoip][coordinates]", "float" ]
        }
        if ![geoip.ip] {
        if [dest_ip]  {
            geoip {
            source => "dest_ip"
            target => "geoip"
            #database => "/opt/logstash/vendor/geoip/GeoLiteCity.dat"
            add_field => [ "[geoip][coordinates]", "%{[geoip][longitude]}" ]
            add_field => [ "[geoip][coordinates]", "%{[geoip][latitude]}"  ]
            }
            mutate {
            convert => [ "[geoip][coordinates]", "float" ]
            }
        }
        }
    }
    }

    output {
    elasticsearch {
        hosts => "localhost"
    }
    }
    ```

1. Böylece Logstash hello dosya işleyebilen emin toogive hello doğru izinleri toohello eve.json dosya olun.
    
    ```
    sudo chmod 775 /var/log/suricata/eve.json
    ```

1. toostart Logstash hello komutu çalıştırın:

    ```
    sudo /etc/init.d/logstash start
    ```

Toohello Logstash yükleme hakkında daha ayrıntılı yönergeler için bkz [resmi belge](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)

### <a name="install-kibana"></a>Kibana yükleyin

1. Aşağıdaki komutları tooinstall Kibana hello çalıştırın:

    ```
    curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
    tar xzvf kibana-5.2.0-linux-x86_64.tar.gz

    ```
1. toorun Kibana hello komutları kullanın:

    ```
    cd kibana-5.2.0-linux-x86_64/
    ./bin/kibana
    ```

1. tooview Kibana web arabirimi, çok gidin`http://localhost:5601`
1. Bu senaryo için Suricata günlüklerini hello için kullanılan hello dizin Düzen olan "logstash-*"

1. Tooview hello Kibana Pano uzaktan istiyorsanız, çok erişimine gelen bir NSG kuralı oluşturma**bağlantı noktası 5601**.

### <a name="create-a-kibana-dashboard"></a>Kibana bir pano oluşturun

Bu makalede, bir örnek pano, tooview eğilimleri ve uyarılarınızı ayrıntılarında sağladık.

1. Merhaba Pano dosya indirme [burada](https://aka.ms/networkwatchersuricatadashboard), hello görselleştirme dosya [burada](https://aka.ms/networkwatchersuricatavisualization)ve kaydedilen hello arama dosyası [burada](https://aka.ms/networkwatchersuricatasavedsearch).

1. Merhaba altında **Yönetim** sekmesini Kibana çok gidin**kaydedilmiş nesneleri** ve tüm üç dosyalarını içeri aktarın. Merhaba öğesinden sonra **Pano** açabilirsiniz sekmesi ve yük hello örneği Panosu.

Ayrıca, kendi Görselleştirme ve kendi ilgi ölçümleri doğru özel panolar oluşturabilirsiniz. Kibana 's Kibana görselleştirmeleri oluşturma hakkında daha fazla okuma [resmi belge](https://www.elastic.co/guide/en/kibana/current/visualize.html).

![kibana Panosu][2]

### <a name="visualize-ids-alert-logs"></a>Kimlikleri uyarı günlükleri Görselleştirme

Merhaba örnek Pano hello Suricata uyarı günlüklerinin birkaç görselleştirmeleri sağlar:

1. Uyarıları GeoIP – hello dağıtım coğrafi konum (IP tarafından belirlenir) göre kaynak kendi ülkeye göre uyarıları gösteren bir harita göre

    ![coğrafi IP][3]

1. 10 uyarılar – hello 10 en sık tetiklenen uyarıların bir özeti ve bunların açıklaması top. Bir bireysel uyarı tıklatarak hello Pano toohello bilgileri toothat belirli uyarı ilgili filtreler.

    ![Görüntü 4][4]

1. Uyarılar – sayısı hello hello ruleset tarafından tetiklenen uyarıların toplam sayısı

    ![Görüntü 5][5]

1. İlk 20 kaynak/hedef IP/bağlantı noktaları - pasta grafikler gösteren üst 20 IP'leri hello ve Uyarıları bağlantı noktaları üzerinde tetiklenen. Belirli IP/bağlantı noktaları toosee üzerinde kaç tane ve hangi aşağı filtreleyebilirsiniz tür uyarılar tetiklendiğinde.

    ![Görüntü 6][6]

1. Uyarı Özeti – her bireysel uyarı belirli ayrıntılarını özetleyen bir tablo. Bu tablo tooshow diğer parametreleri her uyarı için ilgi özelleştirebilirsiniz.

    ![Görüntü 7][7]

Özel görsel ve panolar oluşturma hakkında daha fazla belgeler için bkz: [Kibana'nin resmi belge](https://www.elastic.co/guide/en/kibana/current/introduction.html).

## <a name="conclusion"></a>Sonuç

Ağ İzleyicisi'ni ve açık kaynak Kimlikleri araçları Suricata gibi ağ izinsiz giriş algılama çeşitli tehditler için gerçekleştirebileceğiniz sağlanan paket birleştirerek yakalar. Bu panoları, tooquickly eğilimleri ve ağınızdaki, daha fazla bilgi de derinliklerine uyarılar kötü amaçlı kullanıcı aracıları veya açık bağlantı noktaları gibi veri toodiscover kök nedeni hello uygulamasına izin verir. Ayıklanan bu verilerle korunmasına nasıl yardımcı tooreact tooand ağınıza zararlı yetkisiz erişim girişimlerini hakkında bilinçli kararlar almanıza ve kuralları tooprevent gelecekteki yetkisiz tooyour ağ oluşturun.

## <a name="next-steps"></a>Sonraki adımlar

Tootrigger paket göre uyarıları ziyaret ederek nasıl yakalar öğrenin [paket yakalama toodo öngörülü ağ ile Azure işlevleri izleme kullanın](network-watcher-alert-triggered-packet-capture.md)

Toovisualize NSG akışınız Power BI ile ziyaret ederek nasıl oturum öğrenin [görselleştirmek NSG akar Power BI ile günlükleri](network-watcher-visualize-nsg-flow-logs-power-bi.md)



<!-- images -->
[1]: ./media/network-watcher-intrusion-detection-open-source-tools/figure1.png
[2]: ./media/network-watcher-intrusion-detection-open-source-tools/figure2.png
[3]: ./media/network-watcher-intrusion-detection-open-source-tools/figure3.png
[4]: ./media/network-watcher-intrusion-detection-open-source-tools/figure4.png
[5]: ./media/network-watcher-intrusion-detection-open-source-tools/figure5.png
[6]: ./media/network-watcher-intrusion-detection-open-source-tools/figure6.png
[7]: ./media/network-watcher-intrusion-detection-open-source-tools/figure7.png
