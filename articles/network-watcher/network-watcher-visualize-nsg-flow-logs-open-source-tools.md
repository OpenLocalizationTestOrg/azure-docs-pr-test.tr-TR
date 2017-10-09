---
title: "açık kaynaklı araçları kullanarak aaaVisualize Azure Ağ İzleyicisi NSG akış günlüklerini | Microsoft Docs"
description: "Bu sayfayı toouse kaynak araçları toovisualize NSG akış günlükleri nasıl açılacağını açıklar."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e9b2dcad-4da4-4d6b-aee2-6d0afade0cb8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 47cb529d4a1e00e8c4c0fa6885cbf72aed3e74c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a>Açık kaynaklı Araçları'nı kullanarak Azure Ağ İzleyicisi NSG akış günlükleri Görselleştirme

Ağ güvenlik grubu akış günlükleri kullanılabilir bilgi sağlar; giriş ve çıkış IP trafiği ağ güvenlik grupları anlama. Bu akış günlükleri giden Göster ve gelen akış kuralı başına temelinde hello NIC hello akış, 5 tanımlama grubu ve hakkında bilgi hello akış (kaynak/hedef IP, kaynak/hedef bağlantı noktası, protokol) hello trafiğine izin verilen veya reddedilen varsa uygular.

Bu akış günlükleri zor toomanually ayrıştırma kullanılabilir ve gelen Öngörüler elde edin. Ancak, bu verileri görselleştirin yardımcı olabilecek birçok açık kaynak araçları vardır. Bu makalede bir çözüm toovisualize tooquickly dizin izin ve akış günlüklerinizi bir Kibana Panoda görselleştirebilirsiniz hello esnek yığını kullanarak bu günlükler sağlar.

## <a name="scenario"></a>Senaryo

Bu makalede, biz hello esnek yığını kullanarak toovisualize ağ güvenlik grubu akışı günlüklerini izin veren bir çözümü ayarlama.  Logstash giriş eklentisi hello akış günlükleri doğrudan hello depolama blobu hello akış günlükleri içeren için yapılandırılmış elde eder. Ardından, hello esnek yığını kullanarak hello akış günlükleri dizinlenir ve toocreate Kibana Pano toovisualize hello bilgileri kullanılır.

![senaryo][scenario]

## <a name="steps"></a>Adımlar

### <a name="enable-network-security-group-flow-logging"></a>Ağ güvenlik grubu etkinleştirme akışı günlüğe kaydetme
Bu senaryo için ağ güvenlik grubu akış hesabınızdaki en az bir ağ güvenlik grubu etkin günlüğü olması gerekir. Ağ güvenlik akış günlükleri etkinleştirme ile ilgili yönergeler için aşağıdaki makaleye bakın toohello başvuran [ağ güvenlik grupları için giriş tooflow günlüğü](network-watcher-nsg-flow-logging-overview.md).


### <a name="set-up-hello-elastic-stack"></a>Esnek yığını Hello ayarlayın
Akış günlükleri hello esnek yığını ile NSG bağlanarak, biz Kibana Pano toosearch bize sağlar oluşturabilir, grafik, çözümlemek ve bizim günlüklerinden Öngörüler türetilir.

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
1. Sonraki biz tooconfigure Logstash tooaccess gerekir ve hello akış günlükleri ayrıştırılamadı. Kullanarak bir logstash.conf dosyası oluşturun:

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. Aşağıdaki içerik toohello dosyasına hello ekleyin:

  ```
    input {
      azureblob
        {
            storage_account_name => "mystorageaccount"
            storage_access_key => "storageaccesskey"
            container => "nsgflowlogContainerName"
            codec => "json"
        }
      }

      filter {
        split { field => "[records]" }
        split { field => "[records][properties][flows]"}
        split { field => "[records][properties][flows][flows]"}
        split { field => "[records][properties][flows][flows][flowTuples]"}

     mutate{
      split => { "[records][resourceId]" => "/"}
      add_field => {"Subscription" => "%{[records][resourceId][2]}"
                    "ResourceGroup" => "%{[records][resourceId][4]}"
                    "NetworkSecurityGroup" => "%{[records][resourceId][8]}"}
      convert => {"Subscription" => "string"}
      convert => {"ResourceGroup" => "string"}
      convert => {"NetworkSecurityGroup" => "string"}
      split => { "[records][properties][flows][flows][flowTuples]" => ","}
      add_field => {
                  "unixtimestamp" => "%{[records][properties][flows][flows][flowTuples][0]}"
                  "srcIp" => "%{[records][properties][flows][flows][flowTuples][1]}"
                  "destIp" => "%{[records][properties][flows][flows][flowTuples][2]}"
                  "srcPort" => "%{[records][properties][flows][flows][flowTuples][3]}"
                  "destPort" => "%{[records][properties][flows][flows][flowTuples][4]}"
                  "protocol" => "%{[records][properties][flows][flows][flowTuples][5]}"
                  "trafficflow" => "%{[records][properties][flows][flows][flowTuples][6]}"
                  "traffic" => "%{[records][properties][flows][flows][flowTuples][7]}"
                   }
      convert => {"unixtimestamp" => "integer"}
      convert => {"srcPort" => "integer"}
      convert => {"destPort" => "integer"}        
     }

     date{
       match => ["unixtimestamp" , "UNIX"]
     }
    }

    output {
      stdout { codec => rubydebug }
      elasticsearch {
        hosts => "localhost"
        index => "nsg-flow-logs"
      }
    }  

  ```

Toohello Logstash yükleme hakkında daha ayrıntılı yönergeler için bkz [resmi belge](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)

### <a name="install-hello-logstash-input-plugin-for-azure-blob-storage"></a>Azure blob depolama için Hello Logstash giriş eklentisini yükleme

Bu Logstash eklentisi, toodirectly erişim hello akış günlükleri, belirtilen depolama hesabından izin verir. tooinstall bu eklenti hello varsayılan Logstash yükleme dizininden (Bu örnek /usr/share/logstash/bin) hello komutu çalıştırın:

```
logstash-plugin install logstash-input-azureblob
```

toostart Logstash hello komutu çalıştırın:

```
sudo /etc/init.d/logstash start
```

Bu eklenti hakkında daha fazla bilgi için toodocumentation başvuran [burada](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)

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
1. Bu senaryo için başlangıç dizini düzeni hello akış günlükleri için kullanılan "nsg akış günlüklerini" ' dir. Merhaba dizin düzeni hello "çıktı" bölümünde logstash.conf dosyanızın değişebilir.

1. Tooview hello Kibana Pano uzaktan istiyorsanız, çok erişimine gelen bir NSG kuralı oluşturma**bağlantı noktası 5601**.

### <a name="create-a-kibana-dashboard"></a>Kibana bir pano oluşturun

Bu makalede, bir örnek pano, tooview eğilimleri ve uyarılarınızı ayrıntılarında sağladık.

![Şekil 1][1]

1. Merhaba Pano dosya indirme [burada](https://aka.ms/networkwatchernsgflowlogdashboard), hello görselleştirme dosya [burada](https://aka.ms/networkwatchernsgflowlogvisualizations)ve kaydedilen hello arama dosyası [burada](https://aka.ms/networkwatchernsgflowlogsearch).

1. Merhaba altında **Yönetim** sekmesini Kibana çok gidin**kaydedilmiş nesneleri** ve tüm üç dosyalarını içeri aktarın. Merhaba öğesinden sonra **Pano** açabilirsiniz sekmesi ve yük hello örneği Panosu.

Ayrıca, kendi Görselleştirme ve kendi ilgi ölçümleri doğru özel panolar oluşturabilirsiniz. Kibana 's Kibana görselleştirmeleri oluşturma hakkında daha fazla okuma [resmi belge](https://www.elastic.co/guide/en/kibana/current/visualize.html).

### <a name="visualize-nsg-flow-logs"></a>NSG akış günlükleri Görselleştirme

Merhaba örnek Pano hello akışı günlüklerinin birkaç görselleştirmeleri sağlar:

1. -Zamanlı karar/yön ile akış hello sayısı hello süre gösteren zaman serisi grafikleri akar. Zaman birimi hello ve hem bu görselleştirmeleri aralığını düzenleyebilirsiniz. Akışlar karar gösterir hello oranını tarafından izin ver veya akış yönünü gelen ve giden trafik hello oranını gösterir tarafından sırasında yapılan kararları reddedin. Bu görsellerle trafiği eğilimleri zamanla inceleyin ve tüm ani veya olağan dışı desenleri arayın.

  ![Şekil 2][2]

1. Hedef/kaynak bağlantı noktası tarafından – tootheir ilgili bağlantı noktaları akışları hello dökümünü gösteren pasta grafikler akar. Bu görünüm ile en sık kullanılan bağlantı noktaları görebilirsiniz. Merhaba pasta grafik içinde belirli bir bağlantı noktasında tıklarsanız, hello Pano hello kalan Bu bağlantı noktasını tooflows filtreleyin.

  ![figure3][3]

1. Akışlar ve erken günlüğü süresi – akış hello sayısı kaydedilir ve hello erken günlük hello tarihi yakalanan gösteren ölçümleri sayısı.

  ![Şekil 4][4]

1. Akışlar NSG ve kural – hello dağıtım her NSG içinde kurallarının yanı sıra, her NSG içinde akışlarının hello dağıtım gösteren bir çubuk grafik. Oluşturulan kuralları trafiğinin çoğu hello ve buradan hangi NSG görebilirsiniz.

  ![figure5][5]

1. İlk 10 kaynak/hedef IP – çubuk hello ilk 10 kaynak ve hedef IP'leri gösteren grafikleri. Bu grafik tooshow fazla veya az üst IP'leri ayarlayabilirsiniz. Buradan, en yaygın olarak IP'leri gerçekleşen hello bkz yanı sıra hello trafiği karar (izin verme veya reddetme) her IP yapılan.

  ![figure6][6]

1. Akış Başlıkları – Bu tablo gösterir, hello her akış başlığın yanı sıra karşılık gelen NGS ve kural içinde bulunan bilgileri.

  ![figure7][7]

Merhaba sorgu çubuğu hello hello Pano üstündeki kullanarak, abonelik kimliği, kaynak grupları, kural veya herhangi bir değişken ilgi gibi hello akışlarının herhangi bir parametre göre hello Pano aşağı filtre uygulayabilirsiniz. Kibana'nın sorgular ve filtreleri hakkında daha fazla bilgi için toohello başvuran [resmi belge](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)

## <a name="conclusion"></a>Sonuç

Merhaba ağ güvenlik grubu akış günlükleri hello esnek yığını ile birleştirerek, biz ile güçlü ve özelleştirilebilir bir yöntem toovisualize bizim ağ trafiğini gündeme. Bu panoları tooquickly kazanç izin ve aşağı, ağ trafiğini yanı sıra filtre hakkında Öngörüler paylaşın ve tüm olası anormallikleri üzerinde araştırın. Kibana kullanarak, bu panoları uyarlamak ve güvenlik, denetleme ve uyumluluk gereksinimlerini belirli görselleştirmeleri toomeet oluşturun.

## <a name="next-steps"></a>Sonraki adımlar

Toovisualize NSG akışınız Power BI ile ziyaret ederek nasıl oturum öğrenin [görselleştirmek NSG akar Power BI ile günlükleri](network-watcher-visualize-nsg-flow-logs-power-bi.md)


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
