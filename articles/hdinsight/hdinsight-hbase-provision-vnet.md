---
title: "aaaCreate HBase kümeleri sanal bir ağa - Azure | Microsoft Docs"
description: "Azure Hdınsight'ta HBase kullanarak başlayın. Azure sanal ağ üzerinde nasıl toocreate Hdınsight HBase kümeleri hakkında bilgi edinin."
keywords: 
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 8de8e446-f818-4e61-8fad-e9d38421e80d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 097338a5a650bb607a9f6f9ddb59bb88d098b56f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a>Azure sanal ağındaki hdınsight'ta HBase kümeleri oluşturma
İçinde nasıl toocreate Azure Hdınsight HBase kümeleri öğrenin bir [Azure Virtual Network][1].

Sanal ağ tümleştirmesinin ile HBase kümeleri aynı sanal ağ, uygulamalarınızın böylece dağıtılan toohello olabilir uygulamalar HBase ile doğrudan iletişim kurabilir. Merhaba yararlar şunlardır:

* Doğrudan bağlantı düğümlerinin hello web uygulama toohello HBase Java uzaktan yordam üzerinden iletişimi sağlayan hello HBase kümesi (RPC) API'larını çağırma.
* Geliştirilmiş performans trafiğinizi zorunluluğunu ortadan kaldırarak birden çok ağ geçitleri ve yük dengeleyicileri üzerine gidin.
* Merhaba özelliği tooprocess hassas bilgileri genel bir uç nokta gösterme olmadan daha güvenli bir şekilde.

### <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce aşağıdaki öğelerindeki hello sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü edinme](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Azure PowerShell içeren bir iş istasyonu**. Bkz: [yükleme ve kullanma Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).

## <a name="create-hbase-cluster-into-virtual-network"></a>Sanal ağda HBase kümesi oluşturma
Bu bölümde, bir Azure sanal ağı kullanarak hello bağımlı Azure depolama hesabıyla Linux tabanlı HBase kümesi oluşturma bir [Azure Resource Manager şablonu](../azure-resource-manager/resource-group-template-deploy.md). Diğer küme oluşturma yöntemleri ve hello ayarlarını anlama, bkz: [Hdınsight kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md). Hdınsight'ta bir şablon toocreate Hadoop kullanma hakkında daha fazla bilgi kümeleri için bkz: [Azure Resource Manager şablonları kullanarak Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-create-windows-clusters-arm-templates.md)

> [!NOTE]
> Bazı özellikler hello şablonuna sabit kodlanmış. Örneğin:
>
> * **Konum**: Doğu ABD 2
> * **Küme sürümü**: 3.5
> * **Çalışan düğüm sayısı küme**: 2
> * **Varsayılan depolama hesabı**: benzersiz bir dize
> * **Sanal ağ adı**: &lt;küme adı >-vnet
> * **Sanal ağ adres alanı**: 10.0.0.0/16
> * **Alt ağ adı**: subnet1
> * **Alt ağ adres aralığı**: 10.0.0.0/24
>
> &lt;Küme adı > merhaba şablon kullanırken sağladığınız hello küme adı ile değiştirilir.
>
>

1. Görüntü tooopen hello hello Azure portal şablonda aşağıdaki hello'ı tıklatın. Merhaba şablon bulunduğu [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Merhaba gelen **özel dağıtım** dikey penceresinde, aşağıdaki özelliklere hello girin:

   * **Abonelik**: Azure aboneliği kullanılan toocreate hello Hdınsight kümesi seçin, bağımlı depolama hesabı hello ve Azure sanal ağı hello.
   * **Kaynak grubu**: seçin **Yeni Oluştur**ve yeni bir kaynak grubu adı belirtin.
   * **Konum**: hello kaynak grubu için bir konum seçin.
   * **ClusterName**: Merhaba Hadoop küme toobe oluşturulan için bir ad girin.
   * **Küme oturum açma adı ve parola**: hello varsayılan oturum açma adı **yönetici**.
   * **SSH kullanıcı adı ve parola**: hello varsayılan kullanıcı adı **sshuser**.  Bunu yeniden adlandırabilirsiniz.
   * **Toohello hüküm ve yukarıda belirtilen hello koşullarını kabul ediyorum**: (seçin)
3. **Satın al**’a tıklayın. Bir küme hakkında toocreate yaklaşık 20 dakika sürer. Merhaba Küme oluşturulduktan sonra hello küme dikey penceresinde hello portal tooopen tıklatabilirsiniz.

Merhaba öğreticiyi tamamladıktan sonra toodelete hello küme isteyebilirsiniz. HDInsight ile, verileriniz Azure Storage’da depolanır, böylece kullanılmadığında bir kümeyi güvenle silebilirsiniz. Ayrıca, kullanılmıyorken dahi HDInsight kümesi için sizden ücret kesilir. Merhaba ücretleri hello küme için hello ücretleri depolama birkaç katı olduğundan, bunlar kullanımda olmadığında ekonomik toodelete kümeleri mantıklıdır. Bir küme silme hello yönergeler için bkz: [kullanarak yönetmek Hadoop kümeleri hdınsight'ta Azure portalına hello](hdinsight-administer-use-management-portal.md#delete-clusters).

Yeni, HBase kümesi ile çalışma toobegin bulunan hello yordamları kullanabilirsiniz [hdınsight'ta Hadoop ile HBase kullanmaya başlamanıza](hdinsight-hbase-tutorial-get-started.md).

## <a name="connect-toohello-hbase-cluster-using-hbase-java-rpc-apis"></a>Toohello HBase kümesi HBase Java RPC API'lerini kullanarak bağlan
1. Bir hizmet (Iaas) sanal makineye bir altyapı oluşturmanızı hello aynı Azure sanal ağı ve hello aynı alt ağ. Yeni bir Iaas sanal makine oluşturma ile ilgili yönergeler için bkz: [bir sanal makine çalıştıran Windows Server oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md). Bu belgedeki Hello adımları izleyerek, hello ağ yapılandırması için değerleri aşağıdaki hello kullanmanız gerekir:

   * **Sanal ağ**: &lt;küme adı >-vnet
   * **Alt ağ**: subnet1

   > [!IMPORTANT]
   > Değiştir &lt;küme adı > merhaba adıyla önceki adımlarda hello Hdınsight kümesi oluştururken kullandığınız.
   >
   >

   Bu değerleri kullanarak hello sanal makinenin hello aynı yerleştirildiğinden sanal ağ ve alt hello Hdınsight kümesi olarak. Bu yapılandırma veren toodirectly birbirleri ile iletişim kurar. Bir Hdınsight kümesini boş kenar düğümüne bir şekilde toocreate yoktur. Merhaba kenar düğümüne kullanılan toomanage hello kümesi olabilir.  Daha fazla bilgi için bkz: [Hdınsight'ta boş kenar düğümünü kullanmak](hdinsight-apps-use-edge-node.md).

2. Java uygulama tooconnect tooHBase uzaktan kullanılırken hello tam etki alanı adı (FQDN) kullanmanız gerekir. toodetermine bunu hello bağlantıya özgü DNS soneki hello HBase kümesi almanız gerekir. toodo: yöntemler aşağıdaki hello birini kullanabilirsiniz

   * Bir Web tarayıcısı toomake Ambari çağrısı kullanın:

     Toohttps göz atın: / /&lt;ClusterName >.azurehdinsight.net/api/v1/clusters/&lt;ClusterName > / barındıran? minimal_response = true. Bir JSON dosyası hello DNS sonekleri etkinleştirir.
   * Merhaba Ambari Web sitesi kullanın:

     1. Çok Gözat https://&lt;ClusterName >. azurehdinsight.net.
     2. Tıklatın **ana** hello üst menüsünde.
   * Curl toomake REST çağrılarını kullanın:

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     Merhaba "host_name" girişini bulun, Hello JavaScript nesne gösterimi (JSON) veri döndürdü. Merhaba düğümler hello küme için FQDN hello içerir. Örneğin:

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     Merhaba hello küme adı ile başlayan hello etki alanı adı hello DNS soneki bölümüdür. Örneğin, mycluster.b1.cloudapp.net.
   * Azure PowerShell kullanma

     Azure PowerShell komut dosyası tooregister hello aşağıdaki kullanım hello **Get-ClusterDetail** kullanılan tooreturn hello DNS soneki olabilir işlevi:

    ```powershell
        function Get-ClusterDetail(
            [String]
            [Parameter( Position=0, Mandatory=$true )]
            $ClusterDnsName,
            [String]
            [Parameter( Position=1, Mandatory=$true )]
            $Username,
            [String]
            [Parameter( Position=2, Mandatory=$true )]
            $Password,
            [String]
            [Parameter( Position=3, Mandatory=$true )]
            $PropertyName
            )
        {
        <#
            .SYNOPSIS
            Displays information toofacilitate an HDInsight cluster-to-cluster scenario within hello same virtual network.
            .Description
            This command shows hello following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run hello HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows hello FQDN suffix of hosts in hello cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows hello value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run hello HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows hello FQDN suffix of hosts in hello cluster.
        #>

            $DnsSuffix = ".azurehdinsight.net"

            $ClusterFQDN = $ClusterDnsName + $DnsSuffix
            $webclient = new-object System.Net.WebClient
            $webclient.Credentials = new-object System.Net.NetworkCredential($Username, $Password)

            if($PropertyName -eq "ZookeeperQuorum")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.quorum"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.quorum'
            }
            if($PropertyName -eq "ZookeeperClientPort")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.property.clientPort"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.property.clientPort'
            }
            if($PropertyName -eq "HBaseRestServers")
            {
                $Url1 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.rest.port"
                $Response1 = $webclient.DownloadString($Url1)
                $JsonObject1 = $Response1 | ConvertFrom-Json
                $PortNumber = $JsonObject1.items[0].properties.'hbase.rest.port'

                $Url2 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/hbase/components/hbrest"
                $Response2 = $webclient.DownloadString($Url2)
                $JsonObject2 = $Response2 | ConvertFrom-Json
                foreach ($host_component in $JsonObject2.host_components)
                {
                    $ConnectionString = $host_component.HostRoles.host_name + ":" + $PortNumber
                    Write-host $ConnectionString
                }
            }
            if($PropertyName -eq "FQDNSuffix")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/YARN/components/RESOURCEMANAGER"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                $FQDN = $JsonObject.host_components[0].HostRoles.host_name
                $pos = $FQDN.IndexOf(".")
                $Suffix = $FQDN.Substring($pos + 1)
                Write-host $Suffix
            }
        }
    ```

     Çalışan hello Azure PowerShell Betiği sonra kullanım hello şu komutu tooreturn hello DNS soneki hello kullanarak **Get-ClusterDetail** işlevi. Bu komutu kullanırken Hdınsight HBase küme adı, yönetici adı ve yönetici parolasını belirtin.

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     Bu komut hello DNS soneki döndürür. Örneğin, **yourclustername.b4.internal.cloudapp.net**.


<!--
3.    Change hello primary DNS suffix configuration of hello virtual machine. This enables hello virtual machine tooautomatically resolve hello host name of hello HBase cluster without explicit specification of hello suffix. For example, hello *workernode0* host name will be correctly resolved tooworkernode0 of hello HBase cluster.

    toomake hello configuration change:

    1. RDP into hello virtual machine.
    2. Open **Local Group Policy Editor**. hello executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** toohello value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot hello virtual machine.
-->

sanal makine hello tooverify HBase kümesi hello ile iletişim kurmak, hello komutunu `ping headnode0.<dns suffix>` hello sanal makineden. Örneğin, ping headnode0.mycluster.b1.cloudapp.net.

toouse bu bilgileri bir Java uygulamasında hello adımları izleyebilirsiniz [Hdınsight (Hadoop) ile HBase kullanan Maven kullanmak toobuild Java uygulamaları](hdinsight-hbase-build-java-maven.md) toocreate bir uygulama. toohave Merhaba uygulaması tooa uzak HBase sunucusuna bağlanma, hello Değiştir **hbase-site.xml** Zookeeper Bu örnek toouse hello FQDN dosyasında. Örneğin:

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> Azure sanal ağlar, ad çözümleme hakkında daha fazla bilgi için nasıl dahil toouse kendi DNS sunucusu bkz [adı çözümleme (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).
>
>

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, nasıl öğrenilen toocreate bir HBase kümesi. toolearn daha bakın:

* [Hdınsight kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Hdınsight'ta boş kenar düğümleri kullanın](hdinsight-apps-use-edge-node.md)
* [HDInsight’ta HBase çoğaltmayı yapılandırma](hdinsight-hbase-replication.md)
* [Hdınsight'ta Hadoop kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md)
* [Hdınsight'ta Hadoop ile HBase kullanmaya başlamanıza](hdinsight-hbase-tutorial-get-started.md)
* [Hdınsight'ta HBase ile twitter düşüncelerini çözümleme](hdinsight-hbase-analyze-twitter-sentiment.md)
* [Sanal ağ genel bakış][vnet-overview]

[1]: http://azure.microsoft.com/services/virtual-network/
[2]: http://technet.microsoft.com/library/ee176961.aspx
[3]: http://technet.microsoft.com/library/hh847889.aspx

[hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[vnet-overview]: ../virtual-network/virtual-networks-overview.md
[vm-create]: ../virtual-machines/virtual-machines-windows-hero-tutorial.md

[azure-portal]: https://portal.azure.com
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx


[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter


[powershell-install]: /powershell/azureps-cmdlets-docs


[hdinsight-customize-cluster]: hdinsight-hadoop-customize-cluster.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: ../hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-hbase-replication-dns]: hdinsight-hbase-geo-replication-configure-DNS.md

[img-dns-surffix]: ./media/hdinsight-hbase-provision-vnet/DNSSuffix.png
[img-primary-dns-suffix]: ./media/hdinsight-hbase-provision-vnet/PrimaryDNSSuffix.png
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Hello yeni HBase kümesi ayrıntılarını sağlayın"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Betik eylemi toocustomize bir HBase kümesi kullanın"

[azure-preview-portal]: https://portal.azure.com
