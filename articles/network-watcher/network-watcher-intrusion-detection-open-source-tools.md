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
# <a name="perform-network-intrusion-detection-with-network-watcher-and-open-source-tools"></a><span data-ttu-id="b58f5-103">Ağ İzleyicisi'ni ve açık kaynaklı araçları ile ağ izinsiz giriş algılama gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="b58f5-103">Perform network intrusion detection with Network Watcher and open source tools</span></span>

<span data-ttu-id="b58f5-104">Paket yakalama ağ izinsiz giriş algılama sistemleri (Kimlikler) uygulama ve ağ güvenlik izleme (NSM) gerçekleştirmek için önemli bir bileşeni var.</span><span class="sxs-lookup"><span data-stu-id="b58f5-104">Packet captures are a key component for implementing network intrusion detection systems (IDS) and performing Network Security Monitoring (NSM).</span></span> <span data-ttu-id="b58f5-105">Paket yakalama işleyen ve olası ağ yetkisiz erişim ve kötü amaçlı etkinliği imzaları Ara birkaç açık kaynak Kimlikleri araç vardır.</span><span class="sxs-lookup"><span data-stu-id="b58f5-105">There are several open source IDS tools that process packet captures and look for signatures of possible network intrusions and malicious activity.</span></span> <span data-ttu-id="b58f5-106">Ağ İzleyicisi tarafından sağlanan hello paket yakalamaları kullanarak, ağınızdaki herhangi bir zararlı yetkisiz ya da güvenlik açıkları için analiz edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b58f5-106">Using hello packet captures provided by Network Watcher, you can analyze your network for any harmful intrusions or vulnerabilities.</span></span>

<span data-ttu-id="b58f5-107">Bu tür bir açık kaynak aracı Suricata, rulesets toomonitor ağ trafiğini kullanan ve şüpheli olaylar gerçekleştiğinde uyarıları tetikler Kimlikleri altyapının değil.</span><span class="sxs-lookup"><span data-stu-id="b58f5-107">One such open source tool is Suricata, an IDS engine that uses rulesets toomonitor network traffic and triggers alerts whenever suspicious events occur.</span></span> <span data-ttu-id="b58f5-108">Suricata yüksek hızda ve verimlilik ağ trafiğini analiz gerçekleştirebilir anlamına çok iş parçacıklı bir altyapı sunar.</span><span class="sxs-lookup"><span data-stu-id="b58f5-108">Suricata offers a multi-threaded engine, meaning it can perform network traffic analysis with increased speed and efficiency.</span></span> <span data-ttu-id="b58f5-109">Suricata ve özelliklerini hakkında daha fazla ayrıntı için https://suricata-ids.org/ adresindeki kendi Web sitesini ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="b58f5-109">For more details about Suricata and its capabilities, visit their website at https://suricata-ids.org/.</span></span>

## <a name="scenario"></a><span data-ttu-id="b58f5-110">Senaryo</span><span class="sxs-lookup"><span data-stu-id="b58f5-110">Scenario</span></span>

<span data-ttu-id="b58f5-111">Bu makalede nasıl ortamı tooperform yukarı tooset izinsiz giriş algılama, Suricata, Ağ İzleyicisi'ni kullanarak ağ ve esnek yığını hello açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b58f5-111">This article explains how tooset up your environment tooperform network intrusion detection using Network Watcher, Suricata, and hello Elastic Stack.</span></span> <span data-ttu-id="b58f5-112">Ağ İzleyicisi Merhaba paket ile kullanılan tooperform ağ izinsiz giriş algılama yakalar sağlar.</span><span class="sxs-lookup"><span data-stu-id="b58f5-112">Network Watcher provides you with hello packet captures used tooperform network intrusion detection.</span></span> <span data-ttu-id="b58f5-113">Suricata işlemler hello paket yakalar ve tetikleyici uyarıları tehditleri verilen kendi ruleset eşleşen paketlere dayalı.</span><span class="sxs-lookup"><span data-stu-id="b58f5-113">Suricata processes hello packet captures and trigger alerts based on packets that match its given ruleset of threats.</span></span> <span data-ttu-id="b58f5-114">Bu uyarılar yerel makinenizde bir günlük dosyasında depolanır.</span><span class="sxs-lookup"><span data-stu-id="b58f5-114">These alerts are stored in a log file on your local machine.</span></span> <span data-ttu-id="b58f5-115">Merhaba esnek yığını kullanarak Suricata tarafından oluşturulan hello günlükleri sıralanabilir ve görsel bir hello günlükleri ve anlamına gelir tooquickly kazanç Öngörüler toopotential ağ güvenlik açıklarını sağlayan bir Kibana Pano toocreate kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b58f5-115">Using hello Elastic Stack, hello logs generated by Suricata can be indexed and used toocreate a Kibana dashboard, providing you with a visual representation of hello logs and a means tooquickly gain insights toopotential network vulnerabilities.</span></span>  

![Basit web uygulaması senaryosu][1]

<span data-ttu-id="b58f5-117">Her iki açık kaynaklı araçları bir Azure VM tooperform izin vererek bu çözümleme kendi Azure ağ ortamında ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="b58f5-117">Both open source tools can be set up on an Azure VM, allowing you tooperform this analysis within your own Azure network environment.</span></span>

## <a name="steps"></a><span data-ttu-id="b58f5-118">Adımlar</span><span class="sxs-lookup"><span data-stu-id="b58f5-118">Steps</span></span>

### <a name="install-suricata"></a><span data-ttu-id="b58f5-119">Suricata yükleyin</span><span class="sxs-lookup"><span data-stu-id="b58f5-119">Install Suricata</span></span>

<span data-ttu-id="b58f5-120">Tüm diğer yöntemleri yüklemesinin için http://suricata.readthedocs.io/en/latest/install.html ziyaret edin</span><span class="sxs-lookup"><span data-stu-id="b58f5-120">For all other methods of installation, visit http://suricata.readthedocs.io/en/latest/install.html</span></span>

1. <span data-ttu-id="b58f5-121">Vm'nizin Hello komut satırı terminal hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b58f5-121">In hello command-line terminal of your VM run hello following commands:</span></span>

    ```
    sudo add-apt-repository ppa:oisf/suricata-stable
    sudo apt-get update
    sudo sudo apt-get install suricata
    ```

1. <span data-ttu-id="b58f5-122">tooverify hello komutu çalıştırarak kurulumunuzu `suricata -h` toosee hello komutların tam bir listesi.</span><span class="sxs-lookup"><span data-stu-id="b58f5-122">tooverify your installation, run hello command `suricata -h` toosee hello full list of commands.</span></span>

### <a name="download-hello-emerging-threats-ruleset"></a><span data-ttu-id="b58f5-123">Merhaba Gelişmekte olan tehditleri ruleset indirin</span><span class="sxs-lookup"><span data-stu-id="b58f5-123">Download hello Emerging Threats ruleset</span></span>

<span data-ttu-id="b58f5-124">Bu aşamada, biz Suricata toorun için herhangi bir kuralın sahip değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="b58f5-124">At this stage, we do not have any rules for Suricata toorun.</span></span> <span data-ttu-id="b58f5-125">Kendi kurallarınızı toodetect istediğiniz belirli tehditlerin tooyour ağ yok ya da geliştirilmiş kullanımı kural kümeleri sağlayıcıları, Gelişmekte olan tehditleri veya Snort VRT kurallardan gibi bir dizi de yapabilirsiniz oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b58f5-125">You can create your own rules if there are specific threats tooyour network you would like toodetect, or you can also use developed rule sets from a number of providers, such as Emerging Threats, or VRT rules from Snort.</span></span> <span data-ttu-id="b58f5-126">Merhaba serbestçe erişilebilir Gelişmekte olan tehditleri ruleset burada kullanırız:</span><span class="sxs-lookup"><span data-stu-id="b58f5-126">We use hello freely accessible Emerging Threats ruleset here:</span></span>

<span data-ttu-id="b58f5-127">Merhaba kural kümesi indirin ve hello dizinine kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="b58f5-127">Download hello rule set and copy them into hello directory:</span></span>

```
wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar zxf emerging.rules.tar.gz
sudo cp -r rules /etc/suricata/
```

### <a name="process-packet-captures-with-suricata"></a><span data-ttu-id="b58f5-128">İşlem paket ile Suricata yakalar.</span><span class="sxs-lookup"><span data-stu-id="b58f5-128">Process packet captures with Suricata</span></span>

<span data-ttu-id="b58f5-129">tooprocess paket komutu aşağıdaki hello Çalıştır Suricata kullanarak yakalar:</span><span class="sxs-lookup"><span data-stu-id="b58f5-129">tooprocess packet captures using Suricata, run hello following command:</span></span>

```
sudo suricata -c /etc/suricata/suricata.yaml -r <location_of_pcapfile>
```
<span data-ttu-id="b58f5-130">toocheck hello elde edilen uyarıları, Hello fast.log dosyasını okuyun:</span><span class="sxs-lookup"><span data-stu-id="b58f5-130">toocheck hello resulting alerts, read hello fast.log file:</span></span>
```
tail -f /var/log/suricata/fast.log
```

### <a name="set-up-hello-elastic-stack"></a><span data-ttu-id="b58f5-131">Esnek yığını Hello ayarlayın</span><span class="sxs-lookup"><span data-stu-id="b58f5-131">Set up hello Elastic Stack</span></span>

<span data-ttu-id="b58f5-132">Bizim ağda olup bitenler hakkında değerli bilgiler Suricata üreten hello günlükleri bulunmasına karşın, bu günlük dosyaları hello kolay tooread değil ve anlayın.</span><span class="sxs-lookup"><span data-stu-id="b58f5-132">While hello logs that Suricata produces contain valuable information about what’s happening on our network, these log files aren’t hello easiest tooread and understand.</span></span> <span data-ttu-id="b58f5-133">Suricata hello esnek yığını ile bağlayarak, biz Kibana Pano toosearch bize sağlar oluşturabilir, grafik, analiz ve bizim günlüklerinden Öngörüler türetilir.</span><span class="sxs-lookup"><span data-stu-id="b58f5-133">By connecting Suricata with hello Elastic Stack, we can create a Kibana dashboard what allows us toosearch, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="b58f5-134">Elasticsearch yükleyin</span><span class="sxs-lookup"><span data-stu-id="b58f5-134">Install Elasticsearch</span></span>

1. <span data-ttu-id="b58f5-135">Merhaba esnek yığını sürüm 5.0 ve yukarıdaki Java 8 gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b58f5-135">hello Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="b58f5-136">Merhaba komutu çalıştırmak `java -version` toocheck sürümünüzü.</span><span class="sxs-lookup"><span data-stu-id="b58f5-136">Run hello command `java -version` toocheck your version.</span></span> <span data-ttu-id="b58f5-137">Yükleme, üzerinde toodocumentation bakın java yoksa [Oracle'nın Web sitesi](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="b58f5-137">If you do not have java install, refer toodocumentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="b58f5-138">Sisteminiz için doğru ikili paket Hello yükleyin:</span><span class="sxs-lookup"><span data-stu-id="b58f5-138">Download hello correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="b58f5-139">Diğer yükleme yöntemleri bulunabilir [Elasticsearch yükleme](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span><span class="sxs-lookup"><span data-stu-id="b58f5-139">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="b58f5-140">Elasticsearch hello komutuyla çalıştığını doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="b58f5-140">Verify that Elasticsearch is running with hello command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="b58f5-141">Bir yanıt benzer toothis görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="b58f5-141">You should see a response similar toothis:</span></span>

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

<span data-ttu-id="b58f5-142">Toohello sayfa yükleme esnek arama hakkında daha ayrıntılı yönergeler için bkz [yükleme](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span><span class="sxs-lookup"><span data-stu-id="b58f5-142">For further instructions on installing Elastic search, refer toohello page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="b58f5-143">Logstash yükleyin</span><span class="sxs-lookup"><span data-stu-id="b58f5-143">Install Logstash</span></span>

1. <span data-ttu-id="b58f5-144">tooinstall Logstash hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b58f5-144">tooinstall Logstash run hello following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="b58f5-145">Ardından tooconfigure Logstash tooread eve.json dosyasının hello çıktısından gerekir.</span><span class="sxs-lookup"><span data-stu-id="b58f5-145">Next we need tooconfigure Logstash tooread from hello output of eve.json file.</span></span> <span data-ttu-id="b58f5-146">Kullanarak bir logstash.conf dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="b58f5-146">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="b58f5-147">Aşağıdaki içerik toohello dosyasına hello ekleyin (Bu hello yol toohello eve.json dosyası doğru olduğundan emin olun):</span><span class="sxs-lookup"><span data-stu-id="b58f5-147">Add hello following content toohello file (make sure that hello path toohello eve.json file is correct):</span></span>

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

1. <span data-ttu-id="b58f5-148">Böylece Logstash hello dosya işleyebilen emin toogive hello doğru izinleri toohello eve.json dosya olun.</span><span class="sxs-lookup"><span data-stu-id="b58f5-148">Make sure toogive hello correct permissions toohello eve.json file so that Logstash can ingest hello file.</span></span>
    
    ```
    sudo chmod 775 /var/log/suricata/eve.json
    ```

1. <span data-ttu-id="b58f5-149">toostart Logstash hello komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b58f5-149">toostart Logstash run hello command:</span></span>

    ```
    sudo /etc/init.d/logstash start
    ```

<span data-ttu-id="b58f5-150">Toohello Logstash yükleme hakkında daha ayrıntılı yönergeler için bkz [resmi belge](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="b58f5-150">For further instructions on installing Logstash, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="b58f5-151">Kibana yükleyin</span><span class="sxs-lookup"><span data-stu-id="b58f5-151">Install Kibana</span></span>

1. <span data-ttu-id="b58f5-152">Aşağıdaki komutları tooinstall Kibana hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b58f5-152">Run hello following commands tooinstall Kibana:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
    tar xzvf kibana-5.2.0-linux-x86_64.tar.gz

    ```
1. <span data-ttu-id="b58f5-153">toorun Kibana hello komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="b58f5-153">toorun Kibana use hello commands:</span></span>

    ```
    cd kibana-5.2.0-linux-x86_64/
    ./bin/kibana
    ```

1. <span data-ttu-id="b58f5-154">tooview Kibana web arabirimi, çok gidin`http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="b58f5-154">tooview your Kibana web interface, navigate too`http://localhost:5601`</span></span>
1. <span data-ttu-id="b58f5-155">Bu senaryo için Suricata günlüklerini hello için kullanılan hello dizin Düzen olan "logstash-*"</span><span class="sxs-lookup"><span data-stu-id="b58f5-155">For this scenario, hello index pattern used for hello Suricata logs is "logstash-*"</span></span>

1. <span data-ttu-id="b58f5-156">Tooview hello Kibana Pano uzaktan istiyorsanız, çok erişimine gelen bir NSG kuralı oluşturma**bağlantı noktası 5601**.</span><span class="sxs-lookup"><span data-stu-id="b58f5-156">If you want tooview hello Kibana dashboard remotely, create an inbound NSG rule allowing access too**port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="b58f5-157">Kibana bir pano oluşturun</span><span class="sxs-lookup"><span data-stu-id="b58f5-157">Create a Kibana dashboard</span></span>

<span data-ttu-id="b58f5-158">Bu makalede, bir örnek pano, tooview eğilimleri ve uyarılarınızı ayrıntılarında sağladık.</span><span class="sxs-lookup"><span data-stu-id="b58f5-158">For this article, we have provided a sample dashboard for you tooview trends and details in your alerts.</span></span>

1. <span data-ttu-id="b58f5-159">Merhaba Pano dosya indirme [burada](https://aka.ms/networkwatchersuricatadashboard), hello görselleştirme dosya [burada](https://aka.ms/networkwatchersuricatavisualization)ve kaydedilen hello arama dosyası [burada](https://aka.ms/networkwatchersuricatasavedsearch).</span><span class="sxs-lookup"><span data-stu-id="b58f5-159">Download hello dashboard file [here](https://aka.ms/networkwatchersuricatadashboard), hello visualization file [here](https://aka.ms/networkwatchersuricatavisualization), and hello saved search file [here](https://aka.ms/networkwatchersuricatasavedsearch).</span></span>

1. <span data-ttu-id="b58f5-160">Merhaba altında **Yönetim** sekmesini Kibana çok gidin**kaydedilmiş nesneleri** ve tüm üç dosyalarını içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="b58f5-160">Under hello **Management** tab of Kibana, navigate too**Saved Objects** and import all three files.</span></span> <span data-ttu-id="b58f5-161">Merhaba öğesinden sonra **Pano** açabilirsiniz sekmesi ve yük hello örneği Panosu.</span><span class="sxs-lookup"><span data-stu-id="b58f5-161">Then from hello **Dashboard** tab you can open and load hello sample dashboard.</span></span>

<span data-ttu-id="b58f5-162">Ayrıca, kendi Görselleştirme ve kendi ilgi ölçümleri doğru özel panolar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b58f5-162">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="b58f5-163">Kibana 's Kibana görselleştirmeleri oluşturma hakkında daha fazla okuma [resmi belge](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span><span class="sxs-lookup"><span data-stu-id="b58f5-163">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

![kibana Panosu][2]

### <a name="visualize-ids-alert-logs"></a><span data-ttu-id="b58f5-165">Kimlikleri uyarı günlükleri Görselleştirme</span><span class="sxs-lookup"><span data-stu-id="b58f5-165">Visualize IDS alert logs</span></span>

<span data-ttu-id="b58f5-166">Merhaba örnek Pano hello Suricata uyarı günlüklerinin birkaç görselleştirmeleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="b58f5-166">hello sample dashboard provides several visualizations of hello Suricata alert logs:</span></span>

1. <span data-ttu-id="b58f5-167">Uyarıları GeoIP – hello dağıtım coğrafi konum (IP tarafından belirlenir) göre kaynak kendi ülkeye göre uyarıları gösteren bir harita göre</span><span class="sxs-lookup"><span data-stu-id="b58f5-167">Alerts by GeoIP – a map showing hello distribution of alerts by their country of origin based on geographic location (determined by IP)</span></span>

    ![coğrafi IP][3]

1. <span data-ttu-id="b58f5-169">10 uyarılar – hello 10 en sık tetiklenen uyarıların bir özeti ve bunların açıklaması top.</span><span class="sxs-lookup"><span data-stu-id="b58f5-169">Top 10 Alerts – a summary of hello 10 most frequent triggered alerts and their description.</span></span> <span data-ttu-id="b58f5-170">Bir bireysel uyarı tıklatarak hello Pano toohello bilgileri toothat belirli uyarı ilgili filtreler.</span><span class="sxs-lookup"><span data-stu-id="b58f5-170">Clicking an individual alert filters down hello dashboard toohello information pertaining toothat specific alert.</span></span>

    ![Görüntü 4][4]

1. <span data-ttu-id="b58f5-172">Uyarılar – sayısı hello hello ruleset tarafından tetiklenen uyarıların toplam sayısı</span><span class="sxs-lookup"><span data-stu-id="b58f5-172">Number of Alerts – hello total count of alerts triggered by hello ruleset</span></span>

    ![Görüntü 5][5]

1. <span data-ttu-id="b58f5-174">İlk 20 kaynak/hedef IP/bağlantı noktaları - pasta grafikler gösteren üst 20 IP'leri hello ve Uyarıları bağlantı noktaları üzerinde tetiklenen.</span><span class="sxs-lookup"><span data-stu-id="b58f5-174">Top 20 Source/Destination IPs/Ports - pie charts showing hello top 20 IPs and ports that alerts were triggered on.</span></span> <span data-ttu-id="b58f5-175">Belirli IP/bağlantı noktaları toosee üzerinde kaç tane ve hangi aşağı filtreleyebilirsiniz tür uyarılar tetiklendiğinde.</span><span class="sxs-lookup"><span data-stu-id="b58f5-175">You can filter down on specific IPs/ports toosee how many and what kind of alerts are being triggered.</span></span>

    ![Görüntü 6][6]

1. <span data-ttu-id="b58f5-177">Uyarı Özeti – her bireysel uyarı belirli ayrıntılarını özetleyen bir tablo.</span><span class="sxs-lookup"><span data-stu-id="b58f5-177">Alert Summary – a table summarizing specific details of each individual alert.</span></span> <span data-ttu-id="b58f5-178">Bu tablo tooshow diğer parametreleri her uyarı için ilgi özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b58f5-178">You can customize this table tooshow other parameters of interest for each alert.</span></span>

    ![Görüntü 7][7]

<span data-ttu-id="b58f5-180">Özel görsel ve panolar oluşturma hakkında daha fazla belgeler için bkz: [Kibana'nin resmi belge](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span><span class="sxs-lookup"><span data-stu-id="b58f5-180">For more documentation on creating custom visualizations and dashboards, see [Kibana’s official documentation](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span></span>

## <a name="conclusion"></a><span data-ttu-id="b58f5-181">Sonuç</span><span class="sxs-lookup"><span data-stu-id="b58f5-181">Conclusion</span></span>

<span data-ttu-id="b58f5-182">Ağ İzleyicisi'ni ve açık kaynak Kimlikleri araçları Suricata gibi ağ izinsiz giriş algılama çeşitli tehditler için gerçekleştirebileceğiniz sağlanan paket birleştirerek yakalar.</span><span class="sxs-lookup"><span data-stu-id="b58f5-182">By combining packet captures provided by Network Watcher and open source IDS tools such as Suricata, you can perform network intrusion detection for a wide range of threats.</span></span> <span data-ttu-id="b58f5-183">Bu panoları, tooquickly eğilimleri ve ağınızdaki, daha fazla bilgi de derinliklerine uyarılar kötü amaçlı kullanıcı aracıları veya açık bağlantı noktaları gibi veri toodiscover kök nedeni hello uygulamasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="b58f5-183">These dashboards allow you tooquickly spot trends and anomalies within your network, as well dig into hello data toodiscover root causes of alerts such as malicious user agents or vulnerable ports.</span></span> <span data-ttu-id="b58f5-184">Ayıklanan bu verilerle korunmasına nasıl yardımcı tooreact tooand ağınıza zararlı yetkisiz erişim girişimlerini hakkında bilinçli kararlar almanıza ve kuralları tooprevent gelecekteki yetkisiz tooyour ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b58f5-184">With this extracted data, you can make informed decisions on how tooreact tooand protect your network from any harmful intrusion attempts, and create rules tooprevent future intrusions tooyour network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b58f5-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b58f5-185">Next steps</span></span>

<span data-ttu-id="b58f5-186">Tootrigger paket göre uyarıları ziyaret ederek nasıl yakalar öğrenin [paket yakalama toodo öngörülü ağ ile Azure işlevleri izleme kullanın](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="b58f5-186">Learn how tootrigger packet captures based on alerts by visiting [Use packet capture toodo proactive network monitoring with Azure Functions](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="b58f5-187">Toovisualize NSG akışınız Power BI ile ziyaret ederek nasıl oturum öğrenin [görselleştirmek NSG akar Power BI ile günlükleri](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="b58f5-187">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>



<!-- images -->
[1]: ./media/network-watcher-intrusion-detection-open-source-tools/figure1.png
[2]: ./media/network-watcher-intrusion-detection-open-source-tools/figure2.png
[3]: ./media/network-watcher-intrusion-detection-open-source-tools/figure3.png
[4]: ./media/network-watcher-intrusion-detection-open-source-tools/figure4.png
[5]: ./media/network-watcher-intrusion-detection-open-source-tools/figure5.png
[6]: ./media/network-watcher-intrusion-detection-open-source-tools/figure6.png
[7]: ./media/network-watcher-intrusion-detection-open-source-tools/figure7.png
