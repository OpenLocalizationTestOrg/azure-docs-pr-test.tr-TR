---
title: "Sanal ağları - Azure Hdınsight kullanarak aaaConnect tooKafka | Microsoft Docs"
description: "Nasıl toodirectly bağlanmak tooKafka hdınsight'ta bir Azure sanal ağı bilgi edinin. Bir VPN ağ geçidi kullanarak geliştirme istemcilerden ya da şirket içi istemcilerden tooconnect tooKafka nasıl ağ VPN ağ geçidi aygıtı kullanarak öğrenin."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.custom: hdinsightactive
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/01/2017
ms.author: larryfr
ms.openlocfilehash: 03542fe14b9a1d010dffa22a8f8d96b098a1576e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tookafka-on-hdinsight-preview-through-an-azure-virtual-network"></a>Bir Azure sanal ağı (Önizleme) hdınsight'ta tooKafka Bağlan

Toodirectly tooKafka Azure sanal ağları kullanarak hdınsight'ta nasıl bağlanacağını öğrenin. Bu belgede, yapılandırmaları aşağıdaki hello kullanarak tooKafka bağlanmaya ilişkin bilgiler sağlanmaktadır:

* Bir şirket ağında kaynaklardan. Bu bağlantı, yerel ağınızda bir VPN cihazı (yazılım veya donanım) kullanılarak oluşturulur.
* Geliştirme ortamından bir VPN yazılımı istemcisi kullanarak.

## <a name="architecture-and-planning"></a>Mimari ve planlama

Hdınsight doğrudan bağlantı tooKafka hello izin vermiyor genel internet. Bunun yerine, Kafka istemcileri (üreticileri ve tüketicileri) bağlantı yöntemleri aşağıdaki hello birini kullanmanız gerekir:

* Hello Hello istemcisini çalıştıran hdınsight'ta Kafka aynı sanal ağ. Bu yapılandırma hello kullanılır [Hdınsight üzerinde Apache Kafka (Önizleme) ile başlar](hdinsight-apache-kafka-get-started.md) belge. Merhaba doğrudan istemci çalışır hello üzerinde Hdınsight küme düğümü veya başka bir sanal makinede aynı hello ağ.

* Şirket içi ağınıza toohello sanal ağ gibi özel bir ağa bağlayın. Bu yapılandırma istemcileri Kafka ile şirket içi ağ toodirectly çalışmanızı sağlar. tooenable bu yapılandırma, hello aşağıdaki görevleri gerçekleştirin:

    1. Bir sanal ağ oluşturun.
    2. Siteden siteye yapılandırmasını kullanan bir VPN ağ geçidi oluşturun. Bu belgede kullanılan hello yapılandırma tooa VPN ağ geçidi aygıtı, şirket içi ağınıza bağlanır.
    3. Bir DNS sunucusu hello sanal ağ oluşturun.
    4. Her ağ hello DNS sunucusu arasında iletim yapılandırın.
    5. Kafka Hdınsight'ta hello sanal ağınıza yükleyin.

    Merhaba daha fazla bilgi için bkz: [tooKafka bir şirket içi ağ üzerinden bağlanma](#on-premises) bölümü. 

* Makineleri tek tek toohello sanal ağ VPN ağ geçidi ve VPN istemcisi kullanarak bağlanın. tooenable bu yapılandırma, hello aşağıdaki görevleri gerçekleştirin:

    1. Bir sanal ağ oluşturun.
    2. Bir noktadan siteye yapılandırması kullanan bir VPN ağ geçidi oluşturun. Bu yapılandırma Windows istemcilerinde yüklü bir VPN istemcisi sağlar.
    3. Kafka Hdınsight'ta hello sanal ağınıza yükleyin.
    4. Kafka IP reklam için yapılandırın. Bu yapılandırma, IP adresi yerine etki alanı adlarını kullanarak hello istemci tooconnect sağlar.
    5. İndirin ve hello geliştirme sisteminde hello VPN İstemcisi'ni kullanın.

    Merhaba daha fazla bilgi için bkz: [tooKafka bir VPN istemcisi ile bağlantı](#vpnclient) bölümü.

    > [!WARNING]
    > Bu yapılandırma, yalnızca Geliştirme amaçlı sınırlamalar aşağıdaki hello nedeniyle önerilir:
    >
    > * Her bir istemci bir VPN yazılımı istemcisi kullanarak bağlanmanız gerekir. Azure yalnızca Windows tabanlı bir istemci sağlar.
    > * IP ile Kafka toocommunicate adresleme kullanmalısınız hello istemci ad çözümleme istekleri toohello sanal ağ, geçmez. IP iletişimi hello Kafka küme üzerinde ek yapılandırma gerektirir.

Sanal bir ağa Hdınsight kullanma hakkında daha fazla bilgi için bkz: [genişletmek Azure sanal ağları kullanarak Hdınsight](./hdinsight-extend-hadoop-virtual-network.md).

## <a id="on-premises"></a>Bir şirket içi ağdan tooKafka Bağlan

toocreate şirket içi ağınız ile iletişim kuran Kafka küme hello hello adımlarını izleyin [bağlanmak Hdınsight tooyour şirket içi ağ](./connect-on-premises-network.md) belge.

> [!IMPORTANT]
> Merhaba Hdınsight kümesi oluştururken, hello seçin __Kafka__ küme türü.

Bu adımları yapılandırma aşağıdaki hello oluşturun:

* Azure Sanal Ağ
* Siteden siteye VPN ağ geçidi
* Azure depolama hesabı (Hdınsight tarafından kullanılır)
* Hdınsight üzerinde Kafka

Şirket içi, kullanım hello hello adımlarda Kafka istemcisi toohello küme bağlanabilir tooverify [örnek: Python istemci](#python-client) bölümü.

## <a id="vpnclient"></a>Bir VPN istemcisiyle tooKafka Bağlan

Bu bölümde toocreate hello yapılandırma aşağıdaki Hello adımları kullanın:

* Azure Sanal Ağ
* Noktadan siteye VPN ağ geçidi
* Azure depolama hesabı (Hdınsight tarafından kullanılır)
* Hdınsight üzerinde Kafka

1. Merhaba Hello adımları [noktadan siteye bağlantıları için otomatik olarak imzalanan sertifikalar ile çalışma](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) belge. Bu belge hello ağ geçidi için gereken hello sertifikaları oluşturur.

2. PowerShell komut istemini açın ve aşağıdaki kodu toolog tooyour Azure aboneliği içindeki hello kullanın:

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment tooset hello subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. Yapılandırma bilgilerini içeren kod toocreate değişkenler aşağıdaki hello kullan:

    ```powershell
    # Prompt for generic information
    $resourceGroupName = Read-Host "What is hello resource group name?"
    $baseName = Read-Host "What is hello base name? It is used toocreate names for resources, such as 'net-basename' and 'kafka-basename':"
    $location = Read-Host "What Azure Region do you want toocreate hello resources in?"
    $rootCert = Read-Host "What is hello file path toohello root certificate? It is used toosecure hello VPN gateway."

    # Prompt for HDInsight credentials
    $adminCreds = Get-Credential -Message "Enter hello HTTPS user name and password for hello HDInsight cluster" -UserName "admin"
    $sshCreds = Get-Credential -Message "Enter hello SSH user name and password for hello HDInsight cluster" -UserName "sshuser"

    # Names for Azure resources
    $networkName = "net-$baseName"
    $clusterName = "kafka-$baseName"
    $storageName = "store$baseName" # Can't use dashes in storage names
    $defaultContainerName = $clusterName
    $defaultSubnetName = "default"
    $gatewaySubnetName = "GatewaySubnet"
    $gatewayPublicIpName = "GatewayIp"
    $gatewayIpConfigName = "GatewayConfig"
    $vpnRootCertName = "rootcert"
    $vpnName = "VPNGateway"

    # Network settings
    $networkAddressPrefix = "10.0.0.0/16"
    $defaultSubnetPrefix = "10.0.0.0/24"
    $gatewaySubnetPrefix = "10.0.1.0/24"
    $vpnClientAddressPool = "172.16.201.0/24"

    # HDInsight settings
    $HdiWorkerNodes = 4
    $hdiVersion = "3.5"
    $hdiType = "Kafka"
    ```

4. Kullanım hello aşağıdaki kod toocreate hello Azure kaynak grubu ve sanal ağ:

    ```powershell
    # Create hello resource group that contains everything
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello subnet configuration
    $defaultSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -AddressPrefix $defaultSubnetPrefix
    $gatewaySubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -AddressPrefix $gatewaySubnetPrefix

    # Create hello subnet
    New-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AddressPrefix $networkAddressPrefix `
        -Subnet $defaultSubnetConfig, $gatewaySubnetConfig

    # Get hello network & subnet that were created
    $network = Get-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName
    $gatewaySubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -VirtualNetwork $network
    $defaultSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -VirtualNetwork $network

    # Set a dynamic public IP address for hello gateway subnet
    $gatewayPublicIp = New-AzureRmPublicIpAddress -Name $gatewayPublicIpName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AllocationMethod Dynamic
    $gatewayIpConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $gatewayIpConfigName `
        -Subnet $gatewaySubnet `
        -PublicIpAddress $gatewayPublicIp

    # Get hello certificate info
    # Get hello full path in case a relative path was passed
    $rootCertFile = Get-ChildItem $rootCert
    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($rootCertFile)
    $certBase64 = [System.Convert]::ToBase64String($cert.RawData)
    $p2sRootCert = New-AzureRmVpnClientRootCertificate -Name $vpnRootCertName `
        -PublicCertData $certBase64

    # Create hello VPN gateway
    New-AzureRmVirtualNetworkGateway -Name $vpnName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -IpConfigurations $gatewayIpConfig `
        -GatewayType Vpn `
        -VpnType RouteBased `
        -EnableBgp $false `
        -GatewaySku Standard `
        -VpnClientAddressPool $vpnClientAddressPool `
        -VpnClientRootCertificates $p2sRootCert
    ```

    > [!WARNING]
    > Bu işlem toocomplete için birkaç dakika sürebilir.

5. Aşağıdaki kod, toocreate hello Azure depolama hesabı ve blob kapsayıcı hello kullan:

    ```powershell
    # Create hello storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $storageName `
        -Type Standard_GRS `
        -Location $location

    # Get hello storage account keys and create a context
    $defaultStorageKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName `
        -Name $storageName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageName `
        -StorageAccountKey $defaultStorageKey

    # Create hello default storage container
    New-AzureStorageContainer -Name $defaultContainerName `
        -Context $storageContext
    ```

6. Aşağıdaki kod toocreate hello Hdınsight kümesi hello kullan:

    ```powershell
    # Create hello HDInsight cluster
    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $hdiWorkerNodes `
        -ClusterType $hdiType `
        -OSType Linux `
        -Version $hdiVersion `
        -HttpCredential $adminCreds `
        -SshCredential $sshCreds `
        -DefaultStorageAccountName "$storageName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageKey `
        -DefaultStorageContainer $defaultContainerName `
        -VirtualNetworkId $network.Id `
        -SubnetName $defaultSubnet.Id
    ```

  > [!WARNING]
  > Bu işlem yaklaşık 20 dakika toocomplete alır.

8. Cmdlet tooretrieve hello URL hello sanal ağ için hello Windows VPN istemcisi aşağıdaki hello kullan:

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    toodownload hello Windows VPN istemcisi, kullanım hello web tarayıcınızda URİ'si döndürüldü.

### <a name="configure-kafka-for-ip-advertising"></a>Kafka IP reklam için yapılandırma

Varsayılan olarak, Zookeeper hello Kafka aracıların tooclients hello etki alanı adını döndürür. Bu yapılandırma tarafından ad çözümlemesi hello sanal ağ içindeki varlıklar için kullanılamaz olarak VPN yazılımı istemci hello ile çalışmaz. Bu yapılandırma için hello aşağıdaki kullanın adımları tooconfigure Kafka tooadvertise IP adresleri yerine etki alanı adları:

1. Bir web tarayıcısı kullanarak toohttps://CLUSTERNAME.azurehdinsight.net gidin. Değiştir __CLUSTERNAME__ hello Kafka Hdınsight kümesinde hello adı.

    İstendiğinde, hello HTTPS kullanıcı adı ve parola hello küme için kullanın. Merhaba küme Merhaba Ambari Web kullanıcı Arabirimi görüntülenir.

2. Kafka, tooview bilgi seçin __Kafka__ hello soldaki hello listeden.

    ![Hizmet listesi Kafka ile vurgulanan](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. tooview Kafka yapılandırma seçin __yapılandırmalar__ hello üst orta gelen.

    ![Kafka için yapılandırmalar bağlantıları](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. toofind hello __kafka env__ yapılandırması girin `kafka-env` hello içinde __filtre__ hello üst köşedeki alan.

    ![Kafka env için Kafka yapılandırma](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. tooconfigure Kafka tooadvertise IP adresleri, metin toohello hello sonuna aşağıdaki hello eklemek __kafka env şablonu__ alan:

    ```
    # Configure Kafka tooadvertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. Kafka dinlediği tooconfigure hello arabirimine `listeners` hello içinde __filtre__ hello üst köşedeki alan.

7. tüm ağ arabirimlerinde, değişiklik hello hello değerinde Kafka toolisten tooconfigure __dinleyicileri__ çok alan`PLAINTEXT://0.0.0.0:9092`.

8. toosave hello yapılandırma değişikliklerini kullanmak hello __kaydetmek__ düğmesi. Merhaba değişiklikleri açıklayan bir metin iletisi girin. Seçin __Tamam__ hello değişiklikler kaydedildikten sonra.

    ![Kaydet Yapılandırma düğmesi](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. Kafka, yeniden başlatılırken tooprevent hatalarıyla hello __hizmet eylemleri__ düğmesine tıklayın ve ardından __kapatma üzerinde Bakım modu__. Bu işlem Tamam toocomplete seçin.

    ![Hizmet eylemlerle vurgulanmış bakım etkinleştirin](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. toorestart Kafka, hello kullan __yeniden__ düğmesine tıklayın ve ardından __yeniden tüm etkilenen__. Merhaba yeniden onaylayın ve ardından hello __Tamam__ hello işlemi tamamlandıktan sonra düğmesine tıklayın.

    ![Etkilenen yeniden başlatma ile tüm düğmesi vurgulanmış yeniden başlatın](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. toodisable Bakım modu, kullanım hello __hizmet eylemleri__ düğmesine tıklayın ve ardından __Bakım modu devre dışı bırakma__. Seçin **Tamam** toocomplete bu işlemi.

### <a name="connect-toohello-vpn-gateway"></a>Toohello VPN ağ geçidi Bağlan

tooconnect toohello VPN ağ geçidi bir __Windows İstemcisi__, hello kullan __tooAzure bağlanmak__ hello bölümünü [noktadan siteye bağlantı yapılandırma](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) belge.

## <a id="python-client"></a>Örnek: Python istemci

toovalidate bağlantı tooKafka, aşağıdaki adımları toocreate hello kullanın ve Python üretici ve tüketici çalıştırın:

1. Etki alanı adı (FQDN) ve IP adreslerini hello Kafka küme hello düğümler yöntemleri tooretrieve hello tam olarak aşağıdaki hello birini tam:

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

    Bu komut dosyası varsayar `$resourceGroupName` hello sanal ağ içeren hello Azure kaynak grubu hello adıdır.

    Merhaba hello sonraki adımda döndürülen bilgilerini kullanmak için kaydedin.

2. Kullanım hello tooinstall hello aşağıdaki [kafka python](http://kafka-python.readthedocs.io/) istemci:

        pip install kafka-python

3. toosend veri tooKafka, Python kodu aşağıdaki kullanım hello:

  ```python
  from kafka import KafkaProducer
  # Replace hello `ip_address` entries with hello IP address of your worker nodes
  # NOTE: you don't need hello full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    Hello yerine `'kafka_broker'` girişleri hello adresleriyle döndürülen bu bölümdeki 1. adımdaki:

    * Kullanıyorsanız bir __yazılım VPN istemcisi__, hello yerine `kafka_broker` girişleri çalışan düğümlerinizin hello IP adresine sahip.

    * Varsa __ad çözümlemesinin özel bir DNS sunucusu üzerinden etkin__, hello yerine `kafka_broker` girişleri hello hello çalışan düğümleri FQDN'si ile.

    > [!NOTE]
    > Bu kod hello dizesi gönderir `test message` toohello konu `testtopic`. henüz yoksa hello varsayılan yapılandırmasını hdınsight'ta Kafka toocreate hello konudur.

4. tooretrieve hello iletileri Kafka, Python kodu aşağıdaki hello kullan:

   ```python
   from kafka import KafkaConsumer
   # Replace hello `ip_address` entries with hello IP address of your worker nodes
   # Again, you only need one or two, not hello full list.
   # Note: auto_offset_reset='earliest' resets hello starting offset toohello beginning
   #       of hello topic
   consumer = KafkaConsumer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'],auto_offset_reset='earliest')
   consumer.subscribe(['testtopic'])
   for msg in consumer:
     print (msg)
   ```

    Hello yerine `'kafka_broker'` girişleri hello adresleriyle döndürülen bu bölümdeki 1. adımdaki:

    * Kullanıyorsanız bir __yazılım VPN istemcisi__, hello yerine `kafka_broker` girişleri çalışan düğümlerinizin hello IP adresine sahip.

    * Varsa __ad çözümlemesinin özel bir DNS sunucusu üzerinden etkin__, hello yerine `kafka_broker` girişleri hello hello çalışan düğümleri FQDN'si ile.

## <a name="next-steps"></a>Sonraki adımlar

Merhaba Hdınsight bir sanal ağ ile kullanma hakkında daha fazla bilgi için bkz: [genişletmek Azure bir Azure sanal ağı kullanarak Hdınsight](hdinsight-extend-hadoop-virtual-network.md) belge.

Noktadan siteye VPN ağ geçidi ile bir Azure sanal ağı oluşturma konusunda daha fazla bilgi için aşağıdaki belgeleri hello bakın:

* [Hello Azure portal kullanarak bir noktadan siteye bağlantı yapılandırma](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [Azure PowerShell kullanarak bir noktadan siteye bağlantı yapılandırma](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

Hdınsight'ta Kafka ile çalışma hakkında daha fazla bilgi için aşağıdaki belgeleri hello bakın:

* [HDInsight'ta Kafka kullanmaya başlama](hdinsight-apache-kafka-get-started.md)
* [Hdınsight üzerinde Kafka ile yansıtma kullanın](hdinsight-apache-kafka-mirroring.md)
