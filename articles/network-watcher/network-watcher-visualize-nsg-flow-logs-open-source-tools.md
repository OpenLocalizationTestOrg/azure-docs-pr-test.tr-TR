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
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a><span data-ttu-id="5fca8-103">Açık kaynaklı Araçları'nı kullanarak Azure Ağ İzleyicisi NSG akış günlükleri Görselleştirme</span><span class="sxs-lookup"><span data-stu-id="5fca8-103">Visualize Azure Network Watcher NSG flow logs using open source tools</span></span>

<span data-ttu-id="5fca8-104">Ağ güvenlik grubu akış günlükleri kullanılabilir bilgi sağlar; giriş ve çıkış IP trafiği ağ güvenlik grupları anlama.</span><span class="sxs-lookup"><span data-stu-id="5fca8-104">Network Security Group flow logs provide information that can be used understand ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="5fca8-105">Bu akış günlükleri giden Göster ve gelen akış kuralı başına temelinde hello NIC hello akış, 5 tanımlama grubu ve hakkında bilgi hello akış (kaynak/hedef IP, kaynak/hedef bağlantı noktası, protokol) hello trafiğine izin verilen veya reddedilen varsa uygular.</span><span class="sxs-lookup"><span data-stu-id="5fca8-105">These flow logs show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5 tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="5fca8-106">Bu akış günlükleri zor toomanually ayrıştırma kullanılabilir ve gelen Öngörüler elde edin.</span><span class="sxs-lookup"><span data-stu-id="5fca8-106">These flow logs can be difficult toomanually parse and gain insights from.</span></span> <span data-ttu-id="5fca8-107">Ancak, bu verileri görselleştirin yardımcı olabilecek birçok açık kaynak araçları vardır.</span><span class="sxs-lookup"><span data-stu-id="5fca8-107">However, there are several open source tools that can help visualize this data.</span></span> <span data-ttu-id="5fca8-108">Bu makalede bir çözüm toovisualize tooquickly dizin izin ve akış günlüklerinizi bir Kibana Panoda görselleştirebilirsiniz hello esnek yığını kullanarak bu günlükler sağlar.</span><span class="sxs-lookup"><span data-stu-id="5fca8-108">This article will provide a solution toovisualize these logs using hello Elastic Stack, which will allow you tooquickly index and visualize your flow logs on a Kibana dashboard.</span></span>

## <a name="scenario"></a><span data-ttu-id="5fca8-109">Senaryo</span><span class="sxs-lookup"><span data-stu-id="5fca8-109">Scenario</span></span>

<span data-ttu-id="5fca8-110">Bu makalede, biz hello esnek yığını kullanarak toovisualize ağ güvenlik grubu akışı günlüklerini izin veren bir çözümü ayarlama.</span><span class="sxs-lookup"><span data-stu-id="5fca8-110">In this article, we will set up a solution that will allow you toovisualize Network Security Group flow logs using hello Elastic Stack.</span></span>  <span data-ttu-id="5fca8-111">Logstash giriş eklentisi hello akış günlükleri doğrudan hello depolama blobu hello akış günlükleri içeren için yapılandırılmış elde eder.</span><span class="sxs-lookup"><span data-stu-id="5fca8-111">A Logstash input plugin will obtain hello flow logs directly from hello storage blob configured for containing hello flow logs.</span></span> <span data-ttu-id="5fca8-112">Ardından, hello esnek yığını kullanarak hello akış günlükleri dizinlenir ve toocreate Kibana Pano toovisualize hello bilgileri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5fca8-112">Then, using hello Elastic Stack, hello flow logs will be indexed and used toocreate a Kibana dashboard toovisualize hello information.</span></span>

![senaryo][scenario]

## <a name="steps"></a><span data-ttu-id="5fca8-114">Adımlar</span><span class="sxs-lookup"><span data-stu-id="5fca8-114">Steps</span></span>

### <a name="enable-network-security-group-flow-logging"></a><span data-ttu-id="5fca8-115">Ağ güvenlik grubu etkinleştirme akışı günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="5fca8-115">Enable Network Security Group flow logging</span></span>
<span data-ttu-id="5fca8-116">Bu senaryo için ağ güvenlik grubu akış hesabınızdaki en az bir ağ güvenlik grubu etkin günlüğü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5fca8-116">For this scenario, you must have Network Security Group Flow Logging enabled on at least one Network Security Group in your account.</span></span> <span data-ttu-id="5fca8-117">Ağ güvenlik akış günlükleri etkinleştirme ile ilgili yönergeler için aşağıdaki makaleye bakın toohello başvuran [ağ güvenlik grupları için giriş tooflow günlüğü](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5fca8-117">For instructions on enabling Network Security Flow Logs, refer toohello following article [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>


### <a name="set-up-hello-elastic-stack"></a><span data-ttu-id="5fca8-118">Esnek yığını Hello ayarlayın</span><span class="sxs-lookup"><span data-stu-id="5fca8-118">Set up hello Elastic Stack</span></span>
<span data-ttu-id="5fca8-119">Akış günlükleri hello esnek yığını ile NSG bağlanarak, biz Kibana Pano toosearch bize sağlar oluşturabilir, grafik, çözümlemek ve bizim günlüklerinden Öngörüler türetilir.</span><span class="sxs-lookup"><span data-stu-id="5fca8-119">By connecting NSG flow logs with hello Elastic Stack, we can create a Kibana dashboard what allows us toosearch, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="5fca8-120">Elasticsearch yükleyin</span><span class="sxs-lookup"><span data-stu-id="5fca8-120">Install Elasticsearch</span></span>

1. <span data-ttu-id="5fca8-121">Merhaba esnek yığını sürüm 5.0 ve yukarıdaki Java 8 gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5fca8-121">hello Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="5fca8-122">Merhaba komutu çalıştırmak `java -version` toocheck sürümünüzü.</span><span class="sxs-lookup"><span data-stu-id="5fca8-122">Run hello command `java -version` toocheck your version.</span></span> <span data-ttu-id="5fca8-123">Yükleme, üzerinde toodocumentation bakın java yoksa [Oracle'nın Web sitesi](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="5fca8-123">If you do not have java install, refer toodocumentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="5fca8-124">Sisteminiz için doğru ikili paket Hello yükleyin:</span><span class="sxs-lookup"><span data-stu-id="5fca8-124">Download hello correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="5fca8-125">Diğer yükleme yöntemleri bulunabilir [Elasticsearch yükleme](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span><span class="sxs-lookup"><span data-stu-id="5fca8-125">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="5fca8-126">Elasticsearch hello komutuyla çalıştığını doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="5fca8-126">Verify that Elasticsearch is running with hello command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="5fca8-127">Bir yanıt benzer toothis görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="5fca8-127">You should see a response similar toothis:</span></span>

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

<span data-ttu-id="5fca8-128">Toohello sayfa yükleme esnek arama hakkında daha ayrıntılı yönergeler için bkz [yükleme](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span><span class="sxs-lookup"><span data-stu-id="5fca8-128">For further instructions on installing Elastic search, refer toohello page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="5fca8-129">Logstash yükleyin</span><span class="sxs-lookup"><span data-stu-id="5fca8-129">Install Logstash</span></span>

1. <span data-ttu-id="5fca8-130">tooinstall Logstash hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5fca8-130">tooinstall Logstash run hello following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="5fca8-131">Sonraki biz tooconfigure Logstash tooaccess gerekir ve hello akış günlükleri ayrıştırılamadı.</span><span class="sxs-lookup"><span data-stu-id="5fca8-131">Next we need tooconfigure Logstash tooaccess and parse hello flow logs.</span></span> <span data-ttu-id="5fca8-132">Kullanarak bir logstash.conf dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="5fca8-132">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="5fca8-133">Aşağıdaki içerik toohello dosyasına hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5fca8-133">Add hello following content toohello file:</span></span>

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

<span data-ttu-id="5fca8-134">Toohello Logstash yükleme hakkında daha ayrıntılı yönergeler için bkz [resmi belge](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="5fca8-134">For further instructions on installing Logstash, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-hello-logstash-input-plugin-for-azure-blob-storage"></a><span data-ttu-id="5fca8-135">Azure blob depolama için Hello Logstash giriş eklentisini yükleme</span><span class="sxs-lookup"><span data-stu-id="5fca8-135">Install hello Logstash input plugin for Azure blob storage</span></span>

<span data-ttu-id="5fca8-136">Bu Logstash eklentisi, toodirectly erişim hello akış günlükleri, belirtilen depolama hesabından izin verir.</span><span class="sxs-lookup"><span data-stu-id="5fca8-136">This Logstash plugin will allow you toodirectly access hello flow logs from their designated storage account.</span></span> <span data-ttu-id="5fca8-137">tooinstall bu eklenti hello varsayılan Logstash yükleme dizininden (Bu örnek /usr/share/logstash/bin) hello komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5fca8-137">tooinstall this plugin, from hello default Logstash installation directory (in this case /usr/share/logstash/bin) run hello command:</span></span>

```
logstash-plugin install logstash-input-azureblob
```

<span data-ttu-id="5fca8-138">toostart Logstash hello komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5fca8-138">toostart Logstash run hello command:</span></span>

```
sudo /etc/init.d/logstash start
```

<span data-ttu-id="5fca8-139">Bu eklenti hakkında daha fazla bilgi için toodocumentation başvuran [burada](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span><span class="sxs-lookup"><span data-stu-id="5fca8-139">For more information about this plugin, refer toodocumentation [here](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="5fca8-140">Kibana yükleyin</span><span class="sxs-lookup"><span data-stu-id="5fca8-140">Install Kibana</span></span>

1. <span data-ttu-id="5fca8-141">Aşağıdaki komutları tooinstall Kibana hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5fca8-141">Run hello following commands tooinstall Kibana:</span></span>

  ```
  curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
  tar xzvf kibana-5.2.0-linux-x86_64.tar.gz
  ```

1. <span data-ttu-id="5fca8-142">toorun Kibana hello komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="5fca8-142">toorun Kibana use hello commands:</span></span>

  ```
  cd kibana-5.2.0-linux-x86_64/
  ./bin/kibana
  ```

1. <span data-ttu-id="5fca8-143">tooview Kibana web arabirimi, çok gidin`http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="5fca8-143">tooview your Kibana web interface, navigate too`http://localhost:5601`</span></span>
1. <span data-ttu-id="5fca8-144">Bu senaryo için başlangıç dizini düzeni hello akış günlükleri için kullanılan "nsg akış günlüklerini" ' dir.</span><span class="sxs-lookup"><span data-stu-id="5fca8-144">For this scenario, hello index pattern used for hello flow logs is "nsg-flow-logs".</span></span> <span data-ttu-id="5fca8-145">Merhaba dizin düzeni hello "çıktı" bölümünde logstash.conf dosyanızın değişebilir.</span><span class="sxs-lookup"><span data-stu-id="5fca8-145">You may change hello index pattern in hello "output" section of your logstash.conf file.</span></span>

1. <span data-ttu-id="5fca8-146">Tooview hello Kibana Pano uzaktan istiyorsanız, çok erişimine gelen bir NSG kuralı oluşturma**bağlantı noktası 5601**.</span><span class="sxs-lookup"><span data-stu-id="5fca8-146">If you want tooview hello Kibana dashboard remotely, create an inbound NSG rule allowing access too**port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="5fca8-147">Kibana bir pano oluşturun</span><span class="sxs-lookup"><span data-stu-id="5fca8-147">Create a Kibana dashboard</span></span>

<span data-ttu-id="5fca8-148">Bu makalede, bir örnek pano, tooview eğilimleri ve uyarılarınızı ayrıntılarında sağladık.</span><span class="sxs-lookup"><span data-stu-id="5fca8-148">For this article, we have provided a sample dashboard for you tooview trends and details in your alerts.</span></span>

![Şekil 1][1]

1. <span data-ttu-id="5fca8-150">Merhaba Pano dosya indirme [burada](https://aka.ms/networkwatchernsgflowlogdashboard), hello görselleştirme dosya [burada](https://aka.ms/networkwatchernsgflowlogvisualizations)ve kaydedilen hello arama dosyası [burada](https://aka.ms/networkwatchernsgflowlogsearch).</span><span class="sxs-lookup"><span data-stu-id="5fca8-150">Download hello dashboard file [here](https://aka.ms/networkwatchernsgflowlogdashboard), hello visualization file [here](https://aka.ms/networkwatchernsgflowlogvisualizations), and hello saved search file [here](https://aka.ms/networkwatchernsgflowlogsearch).</span></span>

1. <span data-ttu-id="5fca8-151">Merhaba altında **Yönetim** sekmesini Kibana çok gidin**kaydedilmiş nesneleri** ve tüm üç dosyalarını içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="5fca8-151">Under hello **Management** tab of Kibana, navigate too**Saved Objects** and import all three files.</span></span> <span data-ttu-id="5fca8-152">Merhaba öğesinden sonra **Pano** açabilirsiniz sekmesi ve yük hello örneği Panosu.</span><span class="sxs-lookup"><span data-stu-id="5fca8-152">Then from hello **Dashboard** tab you can open and load hello sample dashboard.</span></span>

<span data-ttu-id="5fca8-153">Ayrıca, kendi Görselleştirme ve kendi ilgi ölçümleri doğru özel panolar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5fca8-153">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="5fca8-154">Kibana 's Kibana görselleştirmeleri oluşturma hakkında daha fazla okuma [resmi belge](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span><span class="sxs-lookup"><span data-stu-id="5fca8-154">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

### <a name="visualize-nsg-flow-logs"></a><span data-ttu-id="5fca8-155">NSG akış günlükleri Görselleştirme</span><span class="sxs-lookup"><span data-stu-id="5fca8-155">Visualize NSG flow logs</span></span>

<span data-ttu-id="5fca8-156">Merhaba örnek Pano hello akışı günlüklerinin birkaç görselleştirmeleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="5fca8-156">hello sample dashboard provides several visualizations of hello flow logs:</span></span>

1. <span data-ttu-id="5fca8-157">-Zamanlı karar/yön ile akış hello sayısı hello süre gösteren zaman serisi grafikleri akar.</span><span class="sxs-lookup"><span data-stu-id="5fca8-157">Flows by Decision/Direction Over Time - time series graphs showing hello number of flows over hello time period.</span></span> <span data-ttu-id="5fca8-158">Zaman birimi hello ve hem bu görselleştirmeleri aralığını düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5fca8-158">You can edit hello unit of time and span of both these visualizations.</span></span> <span data-ttu-id="5fca8-159">Akışlar karar gösterir hello oranını tarafından izin ver veya akış yönünü gelen ve giden trafik hello oranını gösterir tarafından sırasında yapılan kararları reddedin.</span><span class="sxs-lookup"><span data-stu-id="5fca8-159">Flows by Decision shows hello proportion of allow or deny decisions made, while Flows by Direction shows hello proportion of inbound and outbound traffic.</span></span> <span data-ttu-id="5fca8-160">Bu görsellerle trafiği eğilimleri zamanla inceleyin ve tüm ani veya olağan dışı desenleri arayın.</span><span class="sxs-lookup"><span data-stu-id="5fca8-160">With these visuals you can examine traffic trends over time and look for any spikes or unusual patterns.</span></span>

  ![Şekil 2][2]

1. <span data-ttu-id="5fca8-162">Hedef/kaynak bağlantı noktası tarafından – tootheir ilgili bağlantı noktaları akışları hello dökümünü gösteren pasta grafikler akar.</span><span class="sxs-lookup"><span data-stu-id="5fca8-162">Flows by Destination/Source Port – pie charts showing hello breakdown of flows tootheir respective ports.</span></span> <span data-ttu-id="5fca8-163">Bu görünüm ile en sık kullanılan bağlantı noktaları görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5fca8-163">With this view you can see your most commonly used ports.</span></span> <span data-ttu-id="5fca8-164">Merhaba pasta grafik içinde belirli bir bağlantı noktasında tıklarsanız, hello Pano hello kalan Bu bağlantı noktasını tooflows filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="5fca8-164">If you click on a specific port within hello pie chart, hello rest of hello dashboard will filter down tooflows of that port.</span></span>

  ![figure3][3]

1. <span data-ttu-id="5fca8-166">Akışlar ve erken günlüğü süresi – akış hello sayısı kaydedilir ve hello erken günlük hello tarihi yakalanan gösteren ölçümleri sayısı.</span><span class="sxs-lookup"><span data-stu-id="5fca8-166">Number of Flows and Earliest Log Time – metrics showing you hello number of flows recorded and hello date of hello earliest log captured.</span></span>

  ![Şekil 4][4]

1. <span data-ttu-id="5fca8-168">Akışlar NSG ve kural – hello dağıtım her NSG içinde kurallarının yanı sıra, her NSG içinde akışlarının hello dağıtım gösteren bir çubuk grafik.</span><span class="sxs-lookup"><span data-stu-id="5fca8-168">Flows by NSG and Rule – a bar graph showing you hello distribution of flows within each NSG, as well as hello distribution of rules within each NSG.</span></span> <span data-ttu-id="5fca8-169">Oluşturulan kuralları trafiğinin çoğu hello ve buradan hangi NSG görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5fca8-169">From here you can see which NSG and rules generated hello most traffic.</span></span>

  ![figure5][5]

1. <span data-ttu-id="5fca8-171">İlk 10 kaynak/hedef IP – çubuk hello ilk 10 kaynak ve hedef IP'leri gösteren grafikleri.</span><span class="sxs-lookup"><span data-stu-id="5fca8-171">Top 10 Source/Destination IPs – bar charts showing hello top 10 source and destination IPs.</span></span> <span data-ttu-id="5fca8-172">Bu grafik tooshow fazla veya az üst IP'leri ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5fca8-172">You can adjust these charts tooshow more or less top IPs.</span></span> <span data-ttu-id="5fca8-173">Buradan, en yaygın olarak IP'leri gerçekleşen hello bkz yanı sıra hello trafiği karar (izin verme veya reddetme) her IP yapılan.</span><span class="sxs-lookup"><span data-stu-id="5fca8-173">From here you can see hello most commonly occurring IPs as well as hello traffic decision (allow or deny) being made towards each IP.</span></span>

  ![figure6][6]

1. <span data-ttu-id="5fca8-175">Akış Başlıkları – Bu tablo gösterir, hello her akış başlığın yanı sıra karşılık gelen NGS ve kural içinde bulunan bilgileri.</span><span class="sxs-lookup"><span data-stu-id="5fca8-175">Flow Tuples – this table shows you hello information contained within each flow tuple, as well as its corresponding NGS and rule.</span></span>

  ![figure7][7]

<span data-ttu-id="5fca8-177">Merhaba sorgu çubuğu hello hello Pano üstündeki kullanarak, abonelik kimliği, kaynak grupları, kural veya herhangi bir değişken ilgi gibi hello akışlarının herhangi bir parametre göre hello Pano aşağı filtre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5fca8-177">Using hello query bar at hello top of hello dashboard, you can filter down hello dashboard based on any parameter of hello flows, such as subscription ID, resource groups, rule, or any other variable of interest.</span></span> <span data-ttu-id="5fca8-178">Kibana'nın sorgular ve filtreleri hakkında daha fazla bilgi için toohello başvuran [resmi belge](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span><span class="sxs-lookup"><span data-stu-id="5fca8-178">For more about Kibana's queries and filters, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span></span>

## <a name="conclusion"></a><span data-ttu-id="5fca8-179">Sonuç</span><span class="sxs-lookup"><span data-stu-id="5fca8-179">Conclusion</span></span>

<span data-ttu-id="5fca8-180">Merhaba ağ güvenlik grubu akış günlükleri hello esnek yığını ile birleştirerek, biz ile güçlü ve özelleştirilebilir bir yöntem toovisualize bizim ağ trafiğini gündeme.</span><span class="sxs-lookup"><span data-stu-id="5fca8-180">By combining hello Network Security Group flow logs with hello Elastic Stack, we have come up with powerful and customizable way toovisualize our network traffic.</span></span> <span data-ttu-id="5fca8-181">Bu panoları tooquickly kazanç izin ve aşağı, ağ trafiğini yanı sıra filtre hakkında Öngörüler paylaşın ve tüm olası anormallikleri üzerinde araştırın.</span><span class="sxs-lookup"><span data-stu-id="5fca8-181">These dashboards allow you tooquickly gain and share insights about your network traffic, as well as filter down and investigate on any potential anomalies.</span></span> <span data-ttu-id="5fca8-182">Kibana kullanarak, bu panoları uyarlamak ve güvenlik, denetleme ve uyumluluk gereksinimlerini belirli görselleştirmeleri toomeet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5fca8-182">Using Kibana, you can tailor these dashboards and create specific visualizations toomeet any security, audit, and compliance needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5fca8-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5fca8-183">Next steps</span></span>

<span data-ttu-id="5fca8-184">Toovisualize NSG akışınız Power BI ile ziyaret ederek nasıl oturum öğrenin [görselleştirmek NSG akar Power BI ile günlükleri](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="5fca8-184">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
