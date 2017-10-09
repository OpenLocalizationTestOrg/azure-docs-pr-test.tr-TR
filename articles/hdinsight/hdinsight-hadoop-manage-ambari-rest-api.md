---
title: "aaaMonitor ve Hadoop Ambari REST API - Azure Hdınsight ile yönetme | Microsoft Docs"
description: "Bilgi nasıl toouse Ambari toomonitor ve Azure hdınsight'ta Hadoop kümelerini yönetebilirsiniz. Bu belgede nasıl toouse hello Ambari REST API Hdınsight ile dahil kümeleri öğreneceksiniz."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2400530f-92b3-47b7-aa48-875f028765ff
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 1866a77c8e402231bccbcfba7174253aca41339b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-rest-api"></a>Merhaba Ambari REST API kullanarak Hdınsight kümelerini yönetme

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

Nasıl toouse Ambari REST API toomanage hello ve Azure hdınsight'ta Hadoop kümelerini izleme öğrenin.

Apache Ambari hello yönetimi ve Hadoop kümesi kolay toouse web kullanıcı Arabirimi ve REST API'si sağlayarak izlemenin basitleştirir. Ambari hello Linux işletim sistemi kullanan Hdınsight kümelerine dahil edilir. Ambari toomonitor hello küme kullanın ve yapılandırma değişikliklerini yapın.

## <a id="whatis"></a>Ambari nedir

[Apache Ambari](http://ambari.apache.org) web kullanılan tooprovision olması, yönetmek ve Hadoop kümelerini izleme kullanıcı Arabirimi sağlar. Geliştiriciler tümleştirebilir Bu yetenekler uygulamalarına hello kullanarak [Ambari REST API'leri](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

Ambari, Linux tabanlı Hdınsight kümeleri ile varsayılan olarak sağlanır.

## <a name="how-toouse-hello-ambari-rest-api"></a>Nasıl toouse hello Ambari REST API

> [!IMPORTANT]
> Merhaba bilgileri ve bu belgedeki örneklerde Linux işletim sistemi kullanan bir Hdınsight kümesi gerektirir. Daha fazla bilgi için bkz: [Hdınsight kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md).

Bu belgedeki örneklerde Hello hello Uluç Kabuğu (bash) ve PowerShell için sağlanır. örnekler GNU ile test edilmiş hello bash 4.3.11 bash, ancak diğer UNIX Kabukları ile çalışması gerekir. Merhaba PowerShell örnekleri PowerShell 5.0 ile test edilmiş, ancak PowerShell 3.0 veya üstünü çalışması gerekir.

Merhaba kullanıyorsanız __Uluç Kabuk__ (Bash) hello aşağıdaki yüklü olması gerekir:

* [cURL](http://curl.haxx.se/): cURL REST API'leri ile kullanılan toowork hello komut satırından olabilir bir yardımcı olan. Bu belgede, hello Ambari REST API ile kullanılan toocommunicate değil.

Bash veya PowerShell kullanarak olup olmadığını oluşturmuş olmanız da gerekir [jq](https://stedolan.github.io/jq/) yüklü. Jq JSON belgeleri ile çalışmaya yönelik bir yardımcı programdır. İçinde kullanılan **tüm** Bash örnekler, hello ve **bir** hello PowerShell örnekler.

### <a name="base-uri-for-ambari-rest-api"></a>Temel Ambari Rest API için URI

Merhaba hello Hdınsight Ambari REST API için ana URI olan https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, burada **CLUSTERNAME** hello kümenizin adıdır.

> [!IMPORTANT]
> Hello Hello küme adı tam olarak nitelenmiş sırasında etki alanı adı (FQDN) bölümü hello URI (CLUSTERNAME.azurehdinsight.net) büyük/küçük harfe duyarlıdır, diğer oluşum hello URI içindeki büyük/küçük harfe duyarlıdır. Örneğin, kümenizi adlı `MyCluster`, geçerli URI'ler hello aşağıda verilmiştir:
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> URI'ler hello hello adı ikinci oluşum hello değil çünkü bir hata döndürür hello aşağıdaki durumu düzeltin.
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a>Kimlik Doğrulaması

Hdınsight üzerinde tooAmbari bağlanırken HTTPS gerektirir. Merhaba yönetici hesabı adını kullan (Merhaba varsayılandır **yönetici**) ve küme oluşturma sırasında sağlanan parola.

## <a name="examples-authentication-and-parsing-json"></a>Örnekler: Kimlik doğrulaması ve JSON ayrıştırma

Örnek hello nasıl toomake hello bir GET isteği temel Ambari REST API gösterir:

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> Bu belgedeki Hello Bash örneklerde varsayımlar aşağıdaki hello olun:
>
> * Merhaba oturum açma için hello küme adıdır hello varsayılan değerini `admin`.
> * `$PASSWORD`Merhaba Hdınsight oturum açma komut Hello parolasını içerir. Bu değer kullanılarak ayarlanır `PASSWORD='mypassword'`.
> * `$CLUSTERNAME`Merhaba hello küme adını içerir. Bu değer kullanılarak ayarlanır`set CLUSTERNAME='clustername'`

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> Bu belgedeki Hello PowerShell örnekleri varsayımlar aşağıdaki hello olun:
>
> * `$creds`hello Yöneticisi oturum açma ve hello küme parolasını içeren bir kimlik bilgisi nesnesidir. Bu değer kullanılarak ayarlanır `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` ve istendiğinde hello kimlik bilgileri sağlama.
> * `$clusterName`Merhaba hello küme adını içeren bir dizedir. Bu değer kullanılarak ayarlanır `$clusterName="clustername"`.

Örneklerin her ikisi de bilgi benzer toohello aşağıdaki örneğine ile başlayan bir JSON belgesi döndürün:

```json
{
"href" : "http://10.0.0.10:8080/api/v1/clusters/CLUSTERNAME",
"Clusters" : {
    "cluster_id" : 2,
    "cluster_name" : "CLUSTERNAME",
    "health_report" : {
    "Host/stale_config" : 0,
    "Host/maintenance_state" : 0,
    "Host/host_state/HEALTHY" : 7,
    "Host/host_state/UNHEALTHY" : 0,
    "Host/host_state/HEARTBEAT_LOST" : 0,
    "Host/host_state/INIT" : 0,
    "Host/host_status/HEALTHY" : 7,
    "Host/host_status/UNHEALTHY" : 0,
    "Host/host_status/UNKNOWN" : 0,
    "Host/host_status/ALERT" : 0
    ...
```

### <a name="parsing-json-data"></a>JSON verilerini ayrıştırma

Merhaba aşağıdaki örnek kullanır `jq` tooparse hello JSON yanıt belge ve yalnızca hello görüntülemek `health_report` hello sonuçlarından bilgi.

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

PowerShell 3.0 ve üstü sağlar hello `ConvertFrom-Json` hello JSON belgesi ile daha kolay toowork powershell'den bir nesne dönüştürür cmdlet'i. Merhaba aşağıdaki örnek kullanır `ConvertFrom-Json` toodisplay yalnızca hello `health_report` hello sonuçlarından bilgi.

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> Ancak bu belgenin kullanımı çoğu örneklerde `ConvertFrom-Json` toodisplay öğeleri hello yanıt belgeden hello [güncelleştirme Ambari yapılandırma](#example-update-ambari-configuration) örnek jq kullanır. Bu örnek tooconstruct Jq kullanılan hello JSON yanıt belgeden yeni bir şablon.

Merhaba REST API tam başvuru için bkz: [Ambari API Başvurusu V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

## <a name="example-get-hello-fqdn-of-cluster-nodes"></a>Örnek: Merhaba küme düğümlerinin FQDN Al

Hdınsight ile çalışırken, bir küme düğümü tooknow hello tam etki alanı adı (FQDN) gerekebilir. Merhaba FQDN hello için çeşitli örnekler aşağıdaki hello kullanarak hello kümedeki düğümlerin kolayca alabilir:

* **Tüm düğümler**

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" \
    | jq '.items[].Hosts.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.Hosts.host_name
    ```

* **Baş düğümler**

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HDFS/components/NAMENODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/NAMENODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* **Çalışan düğümü**

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/DATANODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/DATANODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* **Zookeeper düğümleri**

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

## <a name="example-get-hello-internal-ip-address-of-cluster-nodes"></a>Örnek: küme düğümlerinin hello iç IP adresi al

> [!IMPORTANT]
> Internet üzerinden erişilebilir değil hello doğrudan bu bölümdeki hello örnekleri tarafından döndürülen hello IP adresleridir. Yalnızca hello hello Hdınsight kümesi içeren Azure sanal ağ içinde erişilebilir.
>
> Hdınsight ve sanal ağlarla çalışma hakkında daha fazla bilgi için bkz: [özel bir Azure Virtual Network kullanarak genişletme Hdınsight yetenekleri](hdinsight-extend-hadoop-virtual-network.md).

toofind başlangıç IP adresi, küme düğümleri hello iç tam etki alanı adını (FQDN) hello bilmeniz gerekir. Merhaba FQDN olduktan sonra başlangıç IP adresi hello konağının sonra alabilirsiniz. Merhaba aşağıdaki örneklerde önce tüm hello konak düğümleri FQDN'sini hello için Ambari sorgu ve ardından Ambari başlangıç IP adresi her konak için sorgular.

```bash
for HOSTNAME in $(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" | jq -r '.items[].Hosts.host_name')
do
    IP=$(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts/$HOSTNAME" | jq -r '.Hosts.ip')
  echo "$HOSTNAME <--> $IP"
done
```

```powershell
$uri = "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts"
$resp = Invoke-WebRequest -Uri $uri -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
foreach($item in $respObj.items) {
    $hostName = [string]$item.Hosts.host_name
    $hostInfoResp = Invoke-WebRequest -Uri "$uri/$hostName" `
        -Credential $creds
    $hostInfoObj = ConvertFrom-Json $hostInfoResp 
    $hostIp = $hostInfoObj.Hosts.ip
    "$hostName <--> $hostIp"
}
```

## <a name="example-get-hello-default-storage"></a>Örnek: Merhaba varsayılan depolama Al

Bir Hdınsight kümesi oluştururken hello varsayılan depolama alanı olarak bir Azure depolama hesabı veya Data Lake Store hello küme için kullanmanız gerekir. Merhaba Küme oluşturulduktan sonra bu bilgileri Ambari tooretrieve kullanabilirsiniz. Örneğin, tooread/yazma veri toohello kapsayıcı Hdınsight dışında istiyorsanız.

Merhaba aşağıdaki örneklerde hello varsayılan depolama yapılandırması hello kümeden Al:

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
| jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'
```

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties.'fs.defaultFS'
```

> [!IMPORTANT]
> Bu örnekler hello ilk uygulanan yapılandırma toohello sunucu dönüşü (`service_config_version=1`) bu bilgileri içerir. Küme oluşturulduktan sonra değiştiren bir değer almak, toolist hello yapılandırma sürümlerini gerekir ve hello en son almak.

Merhaba dönüş değeri örnek Merhaba, benzer tooone şöyledir:

* `wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net`-Bu değer bu hello küme varsayılan depolama için bir Azure Storage hesabı kullanarak gösterir. Merhaba `ACCOUNTNAME` hello hello depolama hesabının adını bir değerdir. Merhaba `CONTAINER` bölümüdür hello blob kapsayıcısının hello depolama hesabındaki hello adı. Merhaba, hello hello kümesi için HDFS uyumlu depolama hello kökündeki kapsayıcıdır.

* `adl://home`-Bu değer bu hello küme varsayılan depolama için bir Azure Data Lake Store kullandığını belirtir.

    toofind hello Data Lake Store hesap adını, örnek hello kullan:

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.hostname'
    ```

    Merhaba dönüş değeri çok benzer`ACCOUNTNAME.azuredatalakestore.net`, burada `ACCOUNTNAME` hello Data Lake Store hesabı hello adıdır.

    toofind hello dizini hello küme, örnek kullanım hello için hello depolama alanını içeren bir Data Lake Store içinde:

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.mountpoint'
    ```

    Merhaba dönüş değeri çok benzer`/clusters/CLUSTERNAME/`. Bu değer, hello Data Lake Store hesabı içinde bir yoludur. Bu yol hello hello hello küme için HDFS uyumlu bir dosya sistemi köküdür. 

> [!NOTE]
> Merhaba `Get-AzureRmHDInsightCluster` tarafından sağlanan cmdlet [Azure PowerShell](/powershell/azure/overview) döndürür hello küme için depolama bilgilerini de hello.


## <a name="example-get-configuration"></a>Örnek: Get yapılandırma

1. Kümeniz için uygun olan hello yapılandırmalarını alma.

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    Bu örnek hello geçerli yapılandırmasını içeren bir JSON belgesi döndürür (Merhaba tarafından tanımlanan *etiketi* değeri) hello kümeye yüklü hello bileşenleri için. Merhaba aşağıdaki bir Spark kümesi türünden döndürülen hello verilerden bir alıntı örnektir.
   
   ```json
   "spark-metrics-properties" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-fairscheduler" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-sparkconf" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   }
   ```

2. İlgilendiğiniz hello bileşeni için Hello yapılandırma alın. Örneğin, aşağıdaki Hello yerine `INITIAL` hello önceki isteğinden döndürülen hello etiket değeri.

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    Bu örnek hello hello geçerli yapılandırmasını içeren bir JSON belgesi döndürür `core-site` bileşeni.

## <a name="example-update-configuration"></a>Örnek: Güncelleştirme yapılandırma

1. Ambari hello "istenen yapılandırma" depolar hello geçerli yapılandırmasını alın:

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    Bu örnek hello geçerli yapılandırmasını içeren bir JSON belgesi döndürür (Merhaba tarafından tanımlanan *etiketi* değeri) hello kümeye yüklü hello bileşenleri için. Merhaba aşağıdaki bir Spark kümesi türünden döndürülen hello verilerden bir alıntı örnektir.
   
    ```json
    "spark-metrics-properties" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-fairscheduler" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-sparkconf" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    }
    ```
   
    Bu listeden hello bileşenin toocopy hello adı gerekir (örneğin, **spark\_thrift\_sparkconf** ve hello **etiketi** değeri.

2. Merhaba bileşeni ve etiket için Hello yapılandırma komutları aşağıdaki hello kullanarak Al:
   
    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=spark-thrift-sparkconf&tag=INITIAL" \
    | jq --arg newtag $(echo version$(date +%s%N)) '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    ```powershell
    $epoch = Get-Date -Year 1970 -Month 1 -Day 1 -Hour 0 -Minute 0 -Second 0
    $now = Get-Date
    $unixTimeStamp = [math]::truncate($now.ToUniversalTime().Subtract($epoch).TotalMilliSeconds)
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=spark-thrift-sparkconf&tag=INITIAL" `
        -Credential $creds
    $resp.Content | jq --arg newtag "version$unixTimeStamp" '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    > [!NOTE]
    > Değiştir **spark thrift sparkconf** ve **ilk** hello bileşeni ve tooretrieve hello yapılandırması için istediğiniz etiketi.
   
    Jq Hdınsight'ta yeni bir yapılandırma şablonuna alınan kullanılan tooturn hello verilerdir. Özellikle, bu örnekler hello aşağıdaki eylemleri gerçekleştirin:
   
    * Merhaba dizesi "Sürüm" ve depolanan hello tarihi içeren benzersiz bir değer oluşturur `newtag`.

    * Merhaba yeni istenen yapılandırma için bir kök belge oluşturur.

    * Alır hello Merhaba içeriğine `.items[]` dizi ve altında hello ekler **desired_config** öğesi.

    * Siler hello `href`, `version`, ve `Config` öğeleri, bu öğeleri gerekli toosubmit yeni bir yapılandırma değildir.

    * Ekler bir `tag` değerini bir öğesiyle `version#################`. Merhaba sayısal bölümü üzerinde hello geçerli tarih temel alır. Her yapılandırma benzersiz bir etiketi olması gerekiyor.
     
    Merhaba veri toohello son olarak, kaydedilen `newconfig.json` belge. Merhaba belge yapısı aşağıdaki örneğine benzer toohello görünmelidir:
     
     ```json
    {
        "Clusters": {
            "desired_config": {
            "tag": "version1459260185774265400",
            "type": "spark-thrift-sparkconf",
            "properties": {
                ....
            },
            "properties_attributes": {
                ....
            }
        }
    }
    ```

3. Açık hello `newconfig.json` hello belge ve değiştirebilir ve ekleyebilir değerlerde `properties` nesnesi. Merhaba aşağıdaki örnek değişiklikleri hello değerini `"spark.yarn.am.memory"` gelen `"1g"` çok`"3g"`. Ayrıca ekler `"spark.kryoserializer.buffer.max"` değerini `"256m"`.
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    Yapmayı değişiklikleri tamamladıktan sonra hello dosyasını kaydedin.

4. Aşağıdaki komutları toosubmit güncelleştirilmiş hello yapılandırma tooAmbari hello kullanın.
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" -X PUT -d @newconfig.json "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
    ```

    ```powershell
    $newConfig = Get-Content .\newconfig.json
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body $newConfig
    $resp.Content
    ```
   
    Bu komutlar hello Merhaba içeriğine gönderme **newconfig.json** dosya toohello küme hello yeni istenen yapılandırması gibi. Merhaba isteği bir JSON belgesi döndürür. Merhaba **versionTag** bu belgedeki öğe gönderildi ve hello hello sürüm eşleşmelidir **yapılandırmalar** nesne, istenen hello yapılandırma değişiklikleri içerir.

### <a name="example-restart-a-service-component"></a>Örnek: bir hizmet bileşeni yeniden başlatın

Bu noktada, hello Ambari web kullanıcı Arabirimi bakarsanız, hello Spark hizmeti hello Yeni yapılandırmanın etkili olması için önce yeniden toobe gerektiğini belirtir. Aşağıdaki adımları toorestart hello hizmet hello kullanın.

1. Merhaba Spark hizmeti tooenable Bakım modu aşağıdaki hello kullan:

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}'
    $resp.Content
    ```
   
    Bu komutlar, bakım modunu açar bir JSON belgesi toohello sunucu gönderin. Merhaba hizmeti artık isteği aşağıdaki hello kullanarak bakım modunda olduğunu doğrulayabilirsiniz:
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK" \
    | jq .ServiceInfo.maintenance_state
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK2" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.ServiceInfo.maintenance_state
    ```
   
    Merhaba dönüş değeri olan `ON`.

2. Ardından, tooturn hello hizmet dışı aşağıdaki hello kullanın:

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}'
    $resp.Content
    ```
    
    Merhaba yanıt benzer toohello örneği aşağıdaki gibidir:
   
    ```json
    {
        "href" : "http://10.0.0.18:8080/api/v1/clusters/CLUSTERNAME/requests/29",
        "Requests" : {
            "id" : 29,
            "status" : "Accepted"
        }
    }
    ```
    
    > [!IMPORTANT]
    > Merhaba `href` bu URI tarafından döndürülen değer hello küme düğümü hello iç IP adresini kullanıyor. toouse dış hello kümeden değiştirmek hello '10.0.0.18:8080' bölümü hello hello küme FQDN'si ile. 
    
    komutları aşağıdaki hello hello isteği hello durumunu alabilir:

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/requests/29" \
    | jq .Requests.request_status
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/requests/29" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.Requests.request_status
    ```

    Yanıtın `COMPLETED` bu hello isteğini tamamladı gösterir.

3. Merhaba önceki istek tamamlandığında toostart hello hizmeti aşağıdaki hello kullanın.
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```
   
    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}'
    ```
    Merhaba hizmeti şimdi hello yeni yapılandırma kullanıyor.

4. Son olarak, Bakım Modu kapalı tooturn aşağıdaki hello kullanın.
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}'
    ```

## <a name="next-steps"></a>Sonraki adımlar

Merhaba REST API tam başvuru için bkz: [Ambari API Başvurusu V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

