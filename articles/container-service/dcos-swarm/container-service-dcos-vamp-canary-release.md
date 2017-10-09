---
title: "Azure DC/OS kümesinde aaaCanary sürüm Vamp ile | Microsoft Docs"
description: "Nasıl toouse toocanary yayın Hizmetleri Vamp ve akıllı trafik bir Azure kapsayıcı hizmeti DC/OS kümesinde filtreleme Uygula"
services: container-service
author: gggina
manager: rasquill
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/17/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: e7b8658a161a7cddcf718e3e1c12a889a330d3d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a>Bir Azure kapsayıcı hizmeti DC/OS kümesinde yalancı yayın mikro Vamp ile

Bu kılavuzda, biz Vamp Azure kapsayıcı hizmeti DC/OS kümesi ile ayarlayın. Biz yalancı hello Vamp demo hizmeti "sava" yayın ve akıllı trafik filtreleme uygulayarak bir uyumsuzluk hello hizmetinin Firefox ile çözün. 

> [!TIP] 
> Bu kılavuzda Vamp bir DC/OS kümesinde çalışır, ancak ayrıca Vamp Kubernetes ile Merhaba orchestrator kullanabilirsiniz.
>

## <a name="about-canary-releases-and-vamp"></a>Yalancı serbest bırakır ve Vamp hakkında


[Yalancı serbest](https://martinfowler.com/bliki/CanaryRelease.html) olan Netflix, Facebook ve Spotify gibi yenilikçi kuruluşlar tarafından benimsenen akıllı Dağıtım stratejisi. Sorunları azaltır, ağ güvenliği tanıtır ve yenilik artırır bulunduğundan, mantıklı bir yaklaşımdır. Bu nedenle neden tüm şirketlerin kullanmadığınız? CI/CD ardışık düzen tooinclude yalancı stratejileri genişletme karmaşıklık ekler ve kapsamlı bir devops bilgi ve deneyimlerine gerektirir. Bile çalışmaya başlamadan önce yeterli tooblock küçük şirket ve kuruluş aynı şekilde olmasıdır. 

[Vamp](http://vamp.io/) bu geçiş tasarlanmış açık kaynak sistemi tooease olduğu ve yalancı serbest özellikleri tercih edilen tooyour kapsayıcı Zamanlayıcı duruma getirin. Yüzde tabanlı sürülmeleri vamp'ın yalancı işlevselliği gider. Trafik filtre ve çok çeşitli koşullar, örneğin tootarget belirli kullanıcılar, IP aralıkları veya cihazlar üzerinde bölebilirsiniz. Vamp izler ve performans ölçümleri, gerçek verilerine dayalı Otomasyon izin vermeyi analiz eder. Otomatik geri alma işlemi hatalarla ayarlayın veya bireysel hizmet çeşitleri yük veya gecikme göre ölçeklendirin.

## <a name="set-up-azure-container-service-with-dcos"></a>Azure kapsayıcı hizmeti DC/OS ile ayarlama



1. [DC/OS kümesi dağıtma](container-service-deployment.md) bir ana ve varsayılan boyutunun iki aracı ile. 

2. [SSH tüneli oluşturma](../container-service-connect.md) tooconnect toohello DC/OS kümesi. Bu makale, toohello küme yerel bağlantı noktası 80 üzerinde tünel varsayar.


## <a name="set-up-vamp"></a>Vamp ayarlayın

Çalışan DC/OS kümesine sahip olduğunuza göre DC/OS kullanıcı Arabirimi (http://localhost:80) hello Vamp yükleyebilirsiniz. 

![DC/OS Kullanıcı Arabirimi](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

Yükleme, iki aşamada yapılır:

1. **Elasticsearch dağıtmak**.

2. Ardından **Vamp dağıtmak** hello Vamp DC/OS universe paketi yükleyerek.

### <a name="deploy-elasticsearch"></a>Elasticsearch dağıtma

Vamp Elasticsearch ölçümleri toplama ve toplama için gerektirir. Merhaba kullanabilirsiniz [magneticio Docker görüntüleri](https://hub.docker.com/r/magneticio/elastic/) toodeploy uyumlu Vamp Elasticsearch yığını.

1. Hello DC/OS kullanıcı Arabirimi, çok Git**Hizmetleri** tıklatıp **hizmeti Dağıt**.

2. Seçin **JSON modu** hello gelen **yeni hizmeti Dağıt** açılır.

  ![JSON modu seçin](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. JSON aşağıdaki hello yapıştırın. Bu yapılandırma, 1 GB RAM ve temel sistem durumu denetimi hello Elasticsearch bağlantı noktası ile Merhaba kapsayıcı çalıştırır.
  
  ```JSON
  {
    "id": "elasticsearch",
    "instances": 1,
    "cpus": 0.2,
    "mem": 1024.0,
    "container": {
      "docker": {
        "image": "magneticio/elastic:2.2",
        "network": "HOST",
        "forcePullImage": true
      }
    },
    "healthChecks": [
      {
        "protocol": "TCP",
        "gracePeriodSeconds": 30,
        "intervalSeconds": 10,
        "timeoutSeconds": 5,
        "port": 9200,
        "maxConsecutiveFailures": 0
      }
    ]
  }
  ```
  

3. Tıklatın **dağıtmak**.

  DC/OS hello Elasticsearch kapsayıcı dağıtır. Merhaba üzerinde ilerleme durumunu izleyebilirsiniz **Hizmetleri** sayfası.  

  ![e dağıtabilir? Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a>Vamp dağıtma

Olarak Elasticsearch raporları bir kez **çalıştıran**, hello Vamp DC/OS Universe paket ekleyebilirsiniz. 

1. Çok Git**Universe** arayın ve **vamp**. 
  ![DC/OS universe üzerinde vamp](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)

2. Tıklatın **yükleme** sonraki toohello vamp paketi ve seçin **gelişmiş yükleme**.

3. Aşağı kaydırın ve elasticsearch url aşağıdaki hello girin: `http://elasticsearch.marathon.mesos:9200`. 

  ![Elasticsearch URL'sini girin](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. Tıklatın **gözden geçirin ve yükleyin**, ardından **yükleme** toostart hello dağıtım.  

  DC/OS gerekli tüm Vamp bileşenlerini dağıtır. Merhaba üzerinde ilerleme durumunu izleyebilirsiniz **Hizmetleri** sayfası.
  
  ![Vamp universe paketi olarak dağıtma](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. Dağıtım tamamlandıktan sonra hello Vamp UI erişebilirsiniz:

  ![DC/OS vamp hizmeti](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![UI vamp](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a>İlk hizmetiniz dağıtma

Bu Vamp çalışır durumda artık şeması hizmetinden dağıtın. 

En basit biçimiyle içinde bir [Vamp şeması](http://vamp.io/documentation/using-vamp/blueprints/) hello uç noktaları (ağ geçidi), kümeler ve Hizmetleri toodeploy açıklar. Kullanan kümeler toogroup farklı türevleri aynı hizmet mantıksal gruplar halinde yalancı serbest bırakma veya bir hello vamp / B testi.  

Bu senaryo adlı örnek bir tek yapılı uygulama kullanır [ **sava**](https://github.com/magneticio/sava), sürüm 1.0 olduğu. Merhaba monolith Docker Hub magneticio/sava:1.0.0 altında olan bir Docker kapsayıcısı paketlenmiştir. Merhaba uygulama normalde bağlantı noktası 8080 üzerinde çalışır, ancak altında bağlantı noktası 9050 bu durumda tooexpose istiyor. Basit şeması kullanarak Vamp aracılığıyla Hello uygulamasını dağıtın.

1. Çok Git**dağıtımları**.

2. **Ekle**'ye tıklayın.

3. Aşağıdaki hello yapıştırma seçeneğiyle şeması YAML. Bu şeması sizi bir sonraki adımda değiştirmek yalnızca bir hizmet değişken ile tek bir küme içerir:

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster toocreate
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. **Kaydet** düğmesine tıklayın. Vamp hello dağıtım başlatır.

Merhaba dağıtım üzerinde hello listelenen **dağıtımları** sayfası. Merhaba dağıtım toomonitor durumunu tıklatın.

![UI Sava dağıtma - vamp](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![Kullanıcı arabiriminde Vamp Sava hizmeti](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

İki ağ geçidi oluşturulur, hangi hello üzerinde listelenen **ağ geçitleri** sayfa:

* hizmetini (bağlantı noktası 9050) çalıştıran bir kararlı endpoint tooaccess hello 
* bir Vamp yönetilen iç ağ geçidi (daha sonra bu ağ geçidi hakkında daha fazla). 

![UI - sava ağ geçitleri vamp](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

Hello sava hizmeti şimdi dağıtıldığını, ancak hello Azure yük dengeleyici tooforward trafiği tooit henüz bilmiyor, dışarıdan erişemezler. tooaccess hello hizmeti, güncelleştirme hello Azure ağ yapılandırması.


## <a name="update-hello-azure-network-configuration"></a>Hello Azure ağ yapılandırmasını güncelleştirin

Dağıtılan hello sava düğümlerde hizmetini kararlı bir uç nokta bağlantı noktası 9050 gösterme hello DC/OS Aracısı, vamp. Dış hello DC/OS kümesi tooaccess hello hizmetinden değişiklikleri toohello Azure ağ yapılandırması, küme dağıtımınızda aşağıdaki hello olun: 

1. **Hello Azure yük dengeleyici yapılandırma** hello aracılar için (Merhaba adlı kaynak **dcos-aracı-lb-xxxx**) durum araştırması ve bağlantı noktası 9050 toohello sava örneklerinde kuralı tooforward trafiği ile. 

2. **Güncelleştirme hello ağ güvenlik grubu** hello ortak aracılar için (Merhaba adlı kaynak **XXXX-aracı-genel-nsg-XXXX**) bağlantı noktası 9050 tooallow trafiğine.

Azure portal, bkz: kullanarak bu görevleri için ayrıntılı adımlar toocomplete hello [etkinleştirmek genel erişim tooan Azure kapsayıcı hizmeti uygulama](container-service-enable-public-access.md). Bağlantı noktasını 9050 tüm bağlantı noktası ayarlarını belirtin.


Her şeyi oluşturulduktan sonra toohello Git **genel bakış** dikey penceresinde hello DC/OS Aracısı Yük Dengeleyici (Merhaba adlı kaynak **dcos-aracı-lb-xxxx**). Hello bulur **genel IP adresi**ve hello adresi tooaccess sava 9050 numaralı bağlantı noktasını kullanın.

![Azure portal - get genel IP adresi](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![Sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a>Yalancı yayın çalıştırın

Üretime toocanary yayın istediğiniz bir uygulamanın yeni sürümü bu olduğunu varsayalım. Magneticio/sava:1.1.0 kapsayıcılı olması ve hazır toogo şunlardır. Vamp dağıtımı çalıştıran yeni hizmetleri toohello kolayca eklemenize olanak sağlar. "Birleştirilmiş" hizmetlerin hello varolan Hizmetleri hello kümedeki yanında dağıtılan ve Ağırlık % 0 olarak atanmış. Merhaba trafik dağılımı ayarlamak kadar hiçbir trafik yeni birleştirilmiş yönlendirilmiş tooa hizmetidir. Merhaba ağırlık kaydırıcı hello Vamp UI içinde artımlı ayarlamalar (yalancı sürüm) ya da anlık bir geri alma için izin verme hello dağıtım üzerinde tam denetim verir.

### <a name="merge-a-new-service-variant"></a>Yeni bir hizmet değişken birleştirme

toomerge hello yeni sava 1.1 hizmetiyle dağıtımı çalıştıran hello:

1. Hello Vamp UI, tıklatın **planlar**.

2. Tıklatın **Ekle** ve Yapıştır aşağıdaki hello'şeması YAML: yeni bir hizmet değişken (sava: 1.1.0) toodeploy hello var olan küme (sava_cluster) içinde bu şeması açıklar.

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster tooupdate
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint tooupdate
  ```
  
3. **Kaydet** düğmesine tıklayın. Merhaba şeması depolanır ve üzerinde hello listelenen **planlar** sayfası.

4. Açık hello Eylem menüsünde tıklatın ve hello sava: 1.1 şeması **birleştirilecek**.

  ![UI - planlar vamp](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. Select hello **sava** dağıtım ve tıklatın **birleştirme**.

  ![UI vamp - şeması toodeployment birleştirme](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

Vamp dağıtır hello şeması sava: hello 1.0.0 yanında açıklanan hello yeni sava: 1.1.0 hizmeti değişken **sava_cluster** hello dağıtımı çalıştıran biri. 

![UI - güncelleştirilmiş sava dağıtım vamp](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

Merhaba **sava_cluster/sava/webport** ağ geçidi (Merhaba küme uç noktası) da güncelleştirilmiş, dağıtılan sava: 1.1.0 rota toohello yeni ekleme. Bu noktada, hiçbir trafik burada yönlendirilen (Merhaba **ağırlık** too0% ayarlanır).

![UI - küme ağ geçidi vamp](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a>Yalancı sürüm

Her iki sava sürümleriyle dağıtılan hello aynı küme, hello taşıyarak aralarındaki trafik hello dağıtımını Ayarla **ağırlık** kaydırıcı.

1. Tıklatın ![Vamp UI - Düzenle](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) sonraki çok**ağırlık**.

2. Merhaba ağırlık dağıtım too50%/50% ayarlayın ve tıklatın **kaydetmek**.

  ![UI - ağ geçidi ağırlık kaydırıcı vamp](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. Tooyour tarayıcı geri dönün ve birkaç kere hello sava sayfayı yenileyin. Merhaba sava uygulamayı şimdi sava: 1.0 sayfa sava: 1.1 sayfa arasında geçiş yapar.

  ![değişen sava1.0 ve sava1.1 Hizmetleri](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > Bu değişim hello sayfasının en iyi hello "Incognito" veya "Anonim" modu tarayıcınızın hello statik varlıklarını önbelleğe alma nedeniyle çalışır.
  >

### <a name="filter-traffic"></a>Trafik filtre

Dağıtımdan sonra bir uyumsuzluk sava: 1.1.0 nedenleri Firefox tarayıcılarda sorunları görüntülemek içinde bulunan varsayalım. Vamp toofilter gelen trafiği ayarlayın ve kararlı sava: 1.0.0 bilinen toohello tüm Firefox kullanıcıları geri doğrudan. Başka bir herkes tooenjoy hello hello yararları devam ederken çözümler Firefox kullanıcılar için kesintiyi hello instantly Bu filtre sava: 1.1.0 geliştirildi.

Kullanır vamp **koşullar** toofilter trafiği bir ağ geçidi yollar arasında. Trafik ilk filtre ve according toohello uygulanan koşullar tooeach rota yönlendirilmiş. Tüm kalan trafik toohello ağ geçidi ağırlığı ayarı göre dağıtılır.

Bir koşul toofilter tüm Firefox kullanıcıları oluşturun ve bunları toohello eski sava: 1.0.0 doğrudan:

1. Merhaba sava/sava_cluster/webport üzerinde **ağ geçitleri** sayfasında, ![Vamp UI - Düzenle](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd bir **KOŞULU** toohello rota sava/sava_cluster/sava:1.0.0/webport. 

2. Merhaba koşulu girin **kullanıcı aracısı Firefox ==** tıklatıp ![Vamp UI - Kaydet](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).

  Vamp %0 varsayılan gücü ile Merhaba koşulu ekler. trafiği filtreleyerek toostart, tooadjust hello koşul gücü gerekir.

3. Tıklatın ![Vamp UI - Düzenle](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **gücü** uygulanan toohello koşulu.
 
4. Set hello **gücü** too100% tıklatıp ![Vamp UI - Kaydet](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.

  Vamp şimdi hello koşul (tüm Firefox kullanıcılar) toosava:1.0.0 eşleşen tüm trafik gönderir.

  ![UI vamp - koşul toogateway Uygula](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. Son olarak, tüm kalan trafik (tüm Firefox olmayan kullanıcılar) toohello yeni sava: 1.1.0 hello ağ geçidi ağırlık toosend ayarlayın. Tıklatın ![Vamp UI - Düzenle](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) sonraki çok**ağırlık** ve yönlendirilmiş toohello rota sava/sava_cluster/sava:1.1.0/webport % 100 olacak şekilde hello ağırlık dağıtımı ayarlayın.

  Merhaba koşul tarafından filtrelenmiş olmayan tüm trafiği yönlendirilmiş toohello yeni sava: 1.1.0 sunulmuştur.

6. Eylem toosee hello filtre iki farklı tarayıcılar (bir Firefox ve başka bir tarayıcı) açın ve hello sava hizmet hem de erişebilirsiniz. Diğer tüm tarayıcılar yönlendirilmiş toosava:1.1.0 çalışırken tüm Firefox istekleri toosava:1.0.0, gönderilir.

  ![UI - filtre trafiği vamp](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a>Özetle

Bu makalede Hızlı Giriş tooVamp bir DC/OS kümesinde oluştu. Yeni başlayanlar Vamp var ve, Azure kapsayıcı hizmeti DC/OS üzerinde çalışan küme, hizmet Vamp şeması ile dağıtılmış ve kullanıma sunulan hello uç noktasında (ağ geçidi) erişilen.

Biz de güçlü özelliklerinden bazıları Vamp üzerinde işlemdeki: çalışan dağıtım ve artımlı olarak giriş ve ardından trafik tooresolve bilinen bir uyumsuzluk filtreleme bir yeni hizmet değişken toohello birleştirme.


## <a name="next-steps"></a>Sonraki adımlar

* Merhaba aracılığıyla Vamp eylemleri yönetme hakkında bilgi edinin [Vamp REST API](http://vamp.io/documentation/api/api-reference/).

* Node.js içinde Vamp Otomasyon betikleri oluşturmak ve bunları olarak çalıştırma [Vamp iş akışları](http://vamp.io/documentation/tutorials/create-a-workflow/).

* Bkz: ek [VAMP öğreticileri](http://vamp.io/documentation/tutorials/overview/).

