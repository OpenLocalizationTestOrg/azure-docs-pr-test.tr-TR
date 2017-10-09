---
title: "aaaExtend Hdınsight sanal ağ - Azure ile | Microsoft Docs"
description: "Toouse Azure Virtual Network tooconnect Hdınsight tooother nasıl bulut kaynakları veya kaynakları, veri merkezinizdeki öğrenin"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 37b9b600-d7f8-4cb1-a04a-0b3a827c6dcc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: ba80be4d9f280c6c62fa8acc996ef5f921acdbbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a>Bir Azure sanal ağı kullanarak Azure Hdınsight genişletme

Bilgi nasıl toouse Hdınsight ile bir [Azure Virtual Network](../virtual-network/virtual-networks-overview.md). Bir Azure sanal ağı kullanarak aşağıdaki senaryolar hello sağlar:

* TooHDInsight doğrudan bir şirket içi ağ üzerinden bağlanılıyor.

* Hdınsight toodata bağlanan bir Azure sanal ağında depolar.

* Doğrudan internet üzerinde herkese açık şekilde kullanılamayan Hadoop hizmetlerine erişimi hello. Örneğin, Kafka API'leri veya hello HBase Java API.

> [!WARNING]
> Merhaba bu belgedeki bilgiler, TCP/IP ağ bilinmesini gerektirir. TCP/IP ağ ile bilmiyorsanız tooproduction ağlar değişiklikler yapmadan önce olan bir kullanıcıyla ortak.

## <a name="planning"></a>Planlama

Merhaba, bir sanal ağdaki tooinstall Hdınsight planlarken yanıt hello sorular şunlardır:

* Mevcut sanal ağda tooinstall Hdınsight gerekiyor mu? Veya yeni bir ağ oluşturmak?

    Varolan bir sanal ağı kullanıyorsanız, Hdınsight yükleyebilmek için önce toomodify hello ağ yapılandırması gerekebilir. Daha fazla bilgi için bkz: Merhaba [Hdınsight tooan var olan sanal ağ ekleme](#existingvnet) bölümü.

* Hdınsight tooanother sanal ağ içeren tooconnect hello sanal ağ veya şirket içi ağınıza istiyor musunuz?

    tooeasily iş ağlar kaynaklarla toocreate özel DNS ve gerekir DNS iletmeyi yapılandırın. Merhaba daha fazla bilgi için bkz: [birden çok ağları bağlama](#multinet) bölümü.

* Toorestrict/yeniden yönlendirme istiyorsunuz gelen veya giden trafiği tooHDInsight?

    Hdınsight hello Azure veri merkezinde belirli IP adresleri ile iletişim sınırsız gerekir. Güvenlik duvarları üzerinden istemci iletişimi için izin verilmelidir çeşitli bağlantı noktaları da vardır. Daha fazla bilgi için bkz: Merhaba [ağ trafiğini denetleme](#networktraffic) bölümü.

## <a id="existingvnet"></a>Hdınsight tooan var olan sanal ağ ekleme

Merhaba adımları Bu bölümde toodiscover kullanma tooadd Azure sanal ağı var olan yeni bir Hdınsight tooan.

> [!NOTE]
> Bir sanal ağ var olan bir Hdınsight kümesine eklenemiyor.

1. Merhaba sanal ağ için bir Klasik veya Resource Manager dağıtım modeli kullanıyor musunuz?

    Hdınsight 3.4 ve büyük bir Resource Manager sanal ağ gerektirir. Hdınsight'ın önceki sürümlerini Klasik sanal ağ gereklidir.

    Ardından, varolan ağınızda bir Klasik sanal ağı ise, Resource Manager sanal ağ oluşturma ve hello iki bağlantı gerekir. [Klasik sanal ağlar toonew sanal ağlara bağlanma](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

    Birleştirilmiş sonra hello Resource Manager ağında yüklü Hdınsight hello Klasik ağ kaynakları ile etkileşim kurabilir.

2. Zorlamalı tünel kullanıyor musunuz? Zorlamalı tünel, giden Internet trafiği tooa aygıt İnceleme için zorlayan bir alt ağ ayarı ve günlüğe kaydetme olur. Hdınsight zorlamalı tünel desteklemez. Bir alt ağ Hdınsight yüklemeden önce zorlamalı tünel kaldırmak veya Hdınsight için yeni bir alt ağ oluşturun.

3. Ağ güvenlik grupları, kullanıcı tanımlı yollar veya sanal ağ uygulamaları toorestrict trafiği içine veya dışına hello sanal ağ kullanıyorsunuz?

    Yönetilen bir hizmet olarak Hdınsight Kısıtlanmamış erişim tooseveral IP adreslerini hello Azure veri merkezinde gerektirir. Bu IP adresleri ile tooallow iletişim herhangi bir mevcut ağ güvenlik grupları veya kullanıcı tanımlı yollar güncelleştirin.

    Hdınsight çeşitli bağlantı noktaları kullanan birden çok hizmetleri barındırır. Trafik toothese bağlantı noktalarını engellemez. Bağlantı noktaları tooallow sanal gereç güvenlik duvarları üzerinden bir listesi için bkz: hello [güvenlik](#security) bölümü.

    toofind var olan güvenlik yapılandırmanızı Azure PowerShell veya Azure CLI komutları aşağıdaki kullanım hello:

    * Ağ güvenlik grupları

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        Daha fazla bilgi için bkz: Merhaba [ağ güvenlik grupları sorun giderme](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) belge.

        > [!IMPORTANT]
        > Ağ güvenlik grubu kural kuralı önceliği temelinde sırayla uygulanır. Merhaba trafik desenle eşleşen hello ilk kural uygulanır ve hiçbir diğerlerinin bu trafiği için uygulanır. Sipariş en fazla izne sahip tooleast izin veren kuralları. Daha fazla bilgi için bkz: Merhaba [filtre ağ güvenlik grupları ile ağ trafiği](../virtual-network/virtual-networks-nsg.md) belge.

    * Kullanıcı tanımlı yollar

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        Merhaba daha fazla bilgi için bkz: [sorun giderme yolları](../virtual-network/virtual-network-routes-troubleshoot-portal.md) belge.

4. Hdınsight kümesi oluşturma ve yapılandırma sırasında hello Azure sanal ağı seçin. Belgeleri toounderstand hello küme oluşturma işlemi aşağıdaki hello Hello adımları kullanın:

    * [Hello Azure portal kullanarak Hdınsight oluşturma](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [Azure PowerShell kullanarak HDInsight oluşturma](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [Azure CLI 1.0 kullanarak Hdınsight oluşturma](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [Bir Azure Resource Manager şablonu kullanarak Hdınsight oluşturma](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > Hdınsight ekleme bir isteğe bağlı yapılandırma adımı tooa sanal ağ oluşturur. Merhaba küme yapılandırma emin tooselect hello sanal ağ olabilir.

## <a id="multinet"></a>Birden çok ağları bağlama

Hello büyük sınama birden fazla ağ yapılandırması ile Merhaba ağlar arasında ad çözümleme ' dir.

Azure ad çözümlemesi için sanal bir ağa yüklü olan Azure hizmetleri sağlar. Bu yerleşik ad çözümlemesi bir tam etki alanı adı (FQDN) kullanarak kaynaklarına aşağıdaki Hdınsight tooconnect toohello sağlar:

* Kullanılabilir herhangi bir kaynağa Internet hello. Örneğin, microsoft.com, google.com.

* İçinde aynı Azure sanal ağ, hello kullanarak hello olan herhangi bir kaynağa __iç DNS ad__ hello kaynağının. Örneğin, hello varsayılan ad çözümlemesi kullanırken hello örnek iç DNS adları atanan tooHDInsight çalışan düğümleri şunlardır:

    * wn0 hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net
    * wn2 hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net

    Bu her iki düğüm iç DNS adları kullanarak birbirine ve diğer düğümlere, hdınsight'ta ile doğrudan iletişim kurabilir.

Merhaba varsayılan ad çözümlemesini yapar __değil__ Hdınsight tooresolve kaynakların hello adları birleştirilmiş toohello sanal ağı olan ağlarda izin verin. Örneğin, ortak toojoin şirket içi toohello sanal ağ ağ. Yalnızca hello varsayılan ad çözümlemesi ile Hdınsight adıyla hello şirket içi ağınızdaki kaynaklara erişemez. Şirket içi ağınızdaki kaynaklara adıyla hello sanal ağ kaynaklarına erişemez, Hello ters de geçerlidir.

> [!WARNING]
> Merhaba özel DNS sunucusu oluşturmak ve hello sanal ağ toouse yapılandırmanız gerekir, oluşturmadan önce hello Hdınsight kümesi.

tooenable ad çözümlemesi hello sanal ağ ve birleştirilmiş ağlarda bulunan kaynaklar arasında hello aşağıdaki eylemleri gerçekleştirmeniz gerekir:

1. Özel bir DNS sunucusu hello tooinstall Hdınsight planlama burada Azure sanal ağ oluşturun.

2. Merhaba sanal ağ toouse hello özel DNS sunucusunu yapılandırın.

3. Azure sanal ağınızın DNS soneki atanan hello bulur. Bu değeri çok benzer`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`. Merhaba hello DNS soneki bulma hakkında daha fazla bilgi için bkz: [örnek: özel DNS](#example-dns) bölümü.

4. İletme hello DNS sunucuları arasında yapılandırın. Merhaba yapılandırma uzak ağ hello türüne bağlıdır.

    * Merhaba uzak ağ bir şirket içi ağ ise, DNS aşağıdaki gibi yapılandırın:
        
        * __Özel DNS__ (Merhaba sanal ağındaki):

            * Merhaba DNS sonekini hello sanal ağ toohello Azure özyinelemeli çözümleyici (168.63.129.16) istekleri ilet. Azure hello sanal ağ içindeki kaynaklar için istekleri işleyen

            * Tüm diğer istekleri toohello şirket içi DNS sunucusu iletin. Merhaba DNS diğer tüm ad çözümleme isteklerini Internet kaynakların Microsoft.com gibi bile istekleri işleyen şirket içi.

        * __Şirket içi DNS__: iletmek hello sanal ağ DNS soneki toohello özel DNS sunucusu için istek. Merhaba özel DNS sunucusu, daha sonra toohello Azure özyinelemeli çözümleyici iletir.

        Bu yapılandırma yolları isteklerinde hello DNS sonekinde hello sanal ağ toohello özel DNS sunucusunun etki alanı adları tam. (Hatta genel internet adresleri için) tüm diğer isteklerden hello şirket içi DNS sunucusu tarafından işlenir.

    * Merhaba uzak ağ başka bir Azure sanal ağ ise, DNS aşağıdaki gibi yapılandırın:

        * __Özel DNS__ (her sanal ağındaki):

            * Merhaba DNS sonekini hello sanal ağlar için istekleri toohello özel DNS sunucularını iletilir. Merhaba DNS her sanal ağ içindeki alt ağ içindeki kaynakların çözümlemek için sorumludur.

            * Tüm diğer istekleri toohello Azure özyinelemeli çözümleyici iletin. Merhaba özyinelemeli çözümleyici yerel çözme ve Internet kaynakların sorumludur.

        Merhaba DNS sunucusu her ağ için DNS soneki göre diğer istekleri toohello iletir. Diğer istekleri hello Azure özyinelemeli çözümleyici kullanarak çözümlenir.

    Her yapılandırma örneği için bkz: Merhaba [örnek: özel DNS](#example-dns) bölümü.

Daha fazla bilgi için bkz: Merhaba [VM'ler ve rol örnekleri için ad çözümlemesi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) belge.

## <a name="directly-connect-toohadoop-services"></a>TooHadoop Hizmetleri doğrudan bağlanın

Hdınsight üzerinde çoğu belgelerine hello erişim toohello küme sahip olduğunuzu varsayar Internet. Https://CLUSTERNAME.azurehdinsight.net toohello kümesine bağlayabilirsiniz örneğin. Bu adres Nsg'ler kullandınız veya Udr'ler toorestrict erişimden hello Internet kullanılabilir değilse hello ortak ağ geçidi, kullanır.

tooconnect tooAmbari ve diğer web sayfalarını hello sanal ağ üzerinden hello aşağıdaki adımları kullanın:

1. Merhaba Hdınsight küme düğümlerinin toodiscover hello iç tam etki alanı adları (FQDN) aşağıdaki yöntemleri hello birini kullanın:

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

    Verilen düğüm listesi Merhaba, hello FQDN Merhaba baş düğümler bulmak ve hello FQDN'ler tooconnect tooAmbari ve diğer web Hizmetleri kullanın. Örneğin, `http://<headnode-fqdn>:8080` tooaccess Ambari.

    > [!IMPORTANT]
    > Merhaba baş düğümler üzerinde barındırılan bazı hizmetler aynı anda yalnızca bir düğümde etkin olur. Bir hizmet bir baş düğüm üzerindeki erişmeyi deneyin ve bir 404 hatası döndürürse toohello diğer baş düğüm geçin.

2. toodetermine hello düğümünü ve bir hizmet, kullanılabilir bağlantı noktası bkz hello [hdınsight'ta Hadoop Hizmetleri tarafından kullanılan bağlantı noktaları](./hdinsight-hadoop-port-settings-for-services.md) belge.

## <a id="networktraffic"></a>Ağ trafiğini denetleme

Bir Azure sanal ağlarda ağ trafiğini, yöntemler aşağıdaki hello kullanılarak denetlenebilir:

* **Ağ güvenlik grupları** (NSG) toofilter gelen ve giden trafik toohello ağ izin verin. Daha fazla bilgi için bkz: Merhaba [filtre ağ güvenlik grupları ile ağ trafiği](../virtual-network/virtual-networks-nsg.md) belge.

    > [!WARNING]
    > Hdınsight giden trafiği kısıtlama desteklemez.

* **Kullanıcı tanımlı yollar** (UDR) nasıl hello ağ kaynakları arasında trafiği akan tanımlayın. Daha fazla bilgi için bkz: Merhaba [kullanıcı tanımlı yollar ve IP iletimini](../virtual-network/virtual-networks-udr-overview.md) belge.

* **Ağ sanal Gereçleri** çoğaltmak güvenlik duvarları ve yönlendiriciler gibi cihazların Merhaba işlevselliği. Daha fazla bilgi için bkz: Merhaba [ağ uygulamaları](https://azure.microsoft.com/solutions/network-appliances) belge.

Yönetilen bir hizmet olarak Hdınsight Kısıtlanmamış erişim tooAzure sistem durumu ve yönetim Hizmetleri'nde hello Azure bulut gerektirir. Nsg'ler ve Udr'ler kullanırken Hdınsight hizmetlerin hala Hdınsight ile iletişim kurabildiğinden emin olmalısınız.

Hdınsight, çeşitli bağlantı noktaları üzerinde hizmetleri sunar. Bir sanal gereç Güvenlik Duvarı'nı kullanırken, bu hizmetler için kullanılan bağlantı noktaları hello üzerinde trafiğe izin vermelidir. Daha fazla bilgi için hello [gerekli bağlantı noktalarını] bölümüne bakın.

### <a id="hdinsight-ip"></a>Hdınsight ile ağ güvenlik gruplarını ve kullanıcı tanımlı yollar

Kullanmayı planlıyorsanız, **ağ güvenlik grubu** veya **kullanıcı tanımlı yollar** toocontrol ağ trafiğini, Eylemler Hdınsight'ı yüklemeden önce aşağıdaki hello gerçekleştirin:

1. Merhaba toouse Hdınsight için planlama Azure bölgesi tanımlayın.

2. Hdınsight tarafından gerekli hello IP adreslerini belirleyin. Daha fazla bilgi için bkz: Merhaba [Hdınsight tarafından gerekli IP adreslerini](#hdinsight-ip) bölüm.

3. Oluşturma veya hello ağ güvenlik grupları veya kullanıcı tanımlı yollar tooinstall Hdınsight planlama hello alt ağ için değiştirme içine.

    * __Ağ güvenlik grupları__: izin __gelen__ bağlantı noktasında trafik __443__ hello IP adreslerinden.
    * __Kullanıcı tanımlı yollar__: bir rota tooeach IP adresi oluşturma ve ayarlama hello __sonraki atlama türü__ too__Internet__.

Ağ güvenlik grupları veya kullanıcı tanımlı yollar hakkında daha fazla bilgi için belge aşağıdaki hello bakın:

* [Ağ güvenlik grubu](../virtual-network/virtual-networks-nsg.md)

* [Kullanıcı tanımlı yollar](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a>Zorlamalı tünel oluşturma

Zorlamalı tünel kullanıcı tanımlı yönlendirme yapılandırması bir alt ağdaki tüm trafiği zorunlu tooa belirli ağ veya şirket içi ağınız gibi konuma olduğu. Hdınsight mu __değil__ destek zorlamalı tünel.

## <a id="hdinsight-ip"></a>Gerekli IP adresi

> [!IMPORTANT]
> Azure sistem durumu hello ve Yönetim Hizmetleri Hdınsight ile mümkün toocommunicate olması gerekir. Ağ güvenlik grupları veya kullanıcı tanımlı yollar kullanıyorsanız, bu hizmetleri tooreach Hdınsight için IP adresleri hello trafiğinden izin verin.
>
> Ağ güvenlik grupları veya kullanıcı tanımlı yollar toocontrol trafik kullanmıyorsanız, bu bölüm göz ardı edebilirsiniz.

Ağ güvenlik grupları veya kullanıcı tanımlı yollar kullanıyorsanız, hello Azure sistem durumu ve Yönetim Hizmetleri tooreach Hdınsight gelen trafiğe izin vermelidir. İzin verilmiş olmalıdır adımları toofind hello IP adreslerini aşağıdaki hello kullan:

1. Her zaman IP adreslerini aşağıdaki hello gelen trafiğe izin vermeniz gerekir:

    | IP adresi | İzin verilen bağlantı noktası | Yön |
    | ---- | ----- | ----- |
    | 168.61.49.99 | 443 | Gelen |
    | 23.99.5.239 | 443 | Gelen |
    | 168.61.48.131 | 443 | Gelen |
    | 138.91.141.162 | 443 | Gelen |

2. Hdınsight kümenize bölgeleri aşağıdaki hello birinde ise, hello bölge için listelenen hello IP adreslerinden gelen trafiğe izin vermelidir:

    > [!IMPORTANT]
    > Merhaba, kullanmakta olduğunuz Azure bölgesi listede yoksa, yalnızca hello dört IP adresleri adım 1'deki kullanın.

    | Ülke | Bölge | İzin verilen IP adresi | İzin verilen bağlantı noktası | Yön |
    | ---- | ---- | ---- | ---- | ----- |
    | Asya | Doğu Asya | 23.102.235.122</br>52.175.38.134 | 443 | Gelen |
    | &nbsp; | Güneydoğu Asya | 13.76.245.160</br>13.76.136.249 | 443 | Gelen |
    | Avustralya | Avustralya Doğu | 104.210.84.115</br>13.75.152.195 | 443 | Gelen |
    | &nbsp; | Avustralya Güneydoğu | 13.77.2.56</br>13.77.2.94 | 443 | Gelen |
    | Brezilya | Güney Brezilya | 191.235.84.104</br>191.235.87.113 | 443 | Gelen |
    | Kanada | Doğu Kanada | 52.229.127.96</br>52.229.123.172 | 443 | Gelen |
    | &nbsp; | Orta Kanada | 52.228.37.66</br>52.228.45.222 | 443 | Gelen |
    | Çin | Çin Kuzey | 42.159.96.170</br>139.217.2.219 | 443 | Gelen |
    | &nbsp; | Çin Doğu | 42.159.198.178</br>42.159.234.157 | 443 | Gelen |
    | Avrupa | Kuzey Avrupa | 52.164.210.96</br>13.74.153.132 | 443 | Gelen |
    | &nbsp; | Batı Avrupa| 52.166.243.90</br>52.174.36.244 | 443 | Gelen |
    | Almanya | Almanya Orta | 51.4.146.68</br>51.4.146.80 | 443 | Gelen |
    | &nbsp; | Almanya Kuzeydoğu | 51.5.150.132</br>51.5.144.101 | 443 | Gelen |
    | Hindistan | Orta Hindistan | 52.172.153.209</br>52.172.152.49 | 443 | Gelen |
    | Japonya | Japonya Doğu | 13.78.125.90</br>13.78.89.60 | 443 | Gelen |
    | &nbsp; | Japonya Batı | 40.74.125.69</br>138.91.29.150 | 443 | Gelen |
    | Kore | Kore Orta | 52.231.39.142</br>52.231.36.209 | 433 | Gelen |
    | &nbsp; | Kore Güney | 52.231.203.16</br>52.231.205.214 | 443 | Gelen
    | Birleşik Krallık | Birleşik Krallık Batı | 51.141.13.110</br>51.141.7.20 | 443 | Gelen |
    | &nbsp; | Birleşik Krallık Güney | 51.140.47.39</br>51.140.52.16 | 443 | Gelen |
    | Amerika Birleşik Devletleri | Orta ABD | 13.67.223.215</br>40.86.83.253 | 443 | Gelen |
    | &nbsp; | Orta Kuzey ABD | 157.56.8.38</br>157.55.213.99 | 443 | Gelen |
    | &nbsp; | Batı Orta ABD | 52.161.23.15</br>52.161.10.167 | 443 | Gelen |
    | &nbsp; | Batı ABD 2 | 52.175.211.210</br>52.175.222.222 | 443 | Gelen |

    Merhaba hello IP hakkında bilgi için Azure kamu toouse adresleri için bkz: [Azure Kamu Intelligence + analiz](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) belge.

3. Sanal ağınız ile özel bir DNS sunucusu kullanıyorsanız, erişimden de izin vermeniz gerekir __168.63.129.16__. Azure'nın özyinelemeli çözümleyici adresidir. Daha fazla bilgi için bkz: Merhaba [VM'ler ve rol için ad çözümlemesi örnekleri](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) belge.

Daha fazla bilgi için bkz: Merhaba [ağ trafiğini denetleme](#networktraffic) bölümü.

## <a id="hdinsight-ports"></a>Gerekli bağlantı noktaları

Bir ağı kullanmayı planlıyorsanız, **sanal gereç Güvenlik Duvarı** toosecure hello sanal ağ, size izin vermelidir giden trafiği bağlantı noktaları aşağıdaki hello üzerinde:

* 53
* 443
* 1433
* 11000-11999
* 14000-14999

Merhaba belirli hizmetleri için bağlantı noktalarının listesi için bkz [hdınsight'ta Hadoop Hizmetleri tarafından kullanılan bağlantı noktaları](hdinsight-hadoop-port-settings-for-services.md) belge.

Sanal gereçler için güvenlik duvarı kuralları hakkında daha fazla bilgi için bkz: Merhaba [sanal gereç senaryo](../virtual-network/virtual-network-scenario-udr-gw-nva.md) belge.

## <a id="hdinsight-nsg"></a>Örnek: ağ güvenlik grupları Hdınsight ile

Bu bölümdeki Hello örnekler, nasıl Azure Yönetim Hizmetleri ile Merhaba Hdınsight toocommunicate izin toocreate ağ güvenlik grubu kuralları gösterir. Merhaba örnekler kullanmadan önce hello IP adreslerini toomatch Merhaba olanları hello kullanmakta olduğunuz Azure bölgesini ayarlayın. Bu bilgileri hello bulabilirsiniz [Hdınsight ağ güvenlik gruplarını ve kullanıcı tanımlı yollar ile](#hdinsight-ip) bölümü.

### <a name="azure-resource-management-template"></a>Azure kaynak yönetimi şablonu

Merhaba aşağıdaki kaynak yönetimi şablon gelen trafiği sınırlar, ancak Hdınsight tarafından gerekli hello IP adreslerinden gelen trafiğe izin veren bir sanal ağ oluşturur. Bu şablon, hello sanal ağında ayrıca bir Hdınsight kümesi oluşturur.

* [Güvenli bir Azure sanal ağ ve bir Hdınsight Hadoop kümesi dağıtma](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> Bu örnek toomatch hello kullanmakta olduğunuz Azure bölgesi kullanılan hello IP adreslerini değiştirin. Bu bilgileri hello bulabilirsiniz [Hdınsight ağ güvenlik gruplarını ve kullanıcı tanımlı yollar ile](#hdinsight-ip) bölümü.

### <a name="azure-powershell"></a>Azure PowerShell

PowerShell komut dosyası toocreate gelen trafiği kısıtlar ve hello trafiğinden hello Kuzey Avrupa bölge için IP adreslerini sağlayan bir sanal ağ aşağıdaki hello kullanın.

> [!IMPORTANT]
> Bu örnek toomatch hello kullanmakta olduğunuz Azure bölgesi kullanılan hello IP adreslerini değiştirin. Bu bilgileri hello bulabilirsiniz [Hdınsight ağ güvenlik gruplarını ve kullanıcı tanımlı yollar ile](#hdinsight-ip) bölümü.

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with hello resource group hello virtual network is in"
$subnetName = "Replace with hello name of hello subnet that you plan toouse for HDInsight"
# Get hello Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get hello region hello Virtual network is in.
$location = $vnet.Location
# Get hello subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for hello HDInsight health and management services.
$nsg = New-AzureRmNetworkSecurityGroup `
    -Name "hdisecure" `
    -ResourceGroupName $resourceGroupName `
    -Location $location `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -name "hdirule1" `
        -Description "HDI health and management address 52.164.210.96" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "52.164.210.96" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 300 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 13.74.153.132" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "13.74.153.132" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 301 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.49.99" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.49.99" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 302 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 23.99.5.239" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "23.99.5.239" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 303 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.48.131" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.48.131" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 304 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 138.91.141.162" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "138.91.141.162" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 305 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "blockeverything" `
        -Description "Block everything else" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "*" `
        -SourceAddressPrefix "Internet" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Deny `
        -Priority 500 `
        -Direction Inbound
# Set hello changes toohello security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply hello NSG toohello subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> Bu örnek nasıl tooadd kuralları tooallow gelen gerekli hello IP adreslerindeki trafiği gösterir. Bir kural toorestrict içermiyor gelen diğer kaynaklardan erişim.
>
> Aşağıdaki örneğine hello nasıl tooenable SSH erişim Internet hello gösterir:
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a>Azure CLI

Aşağıdaki adımları toocreate gelen trafik sınırlar, ancak Hdınsight tarafından gerekli hello IP adreslerinden gelen trafiğe izin veren bir sanal ağ hello kullanın.

1. Yeni bir ağ güvenlik grubu adlı komut toocreate aşağıdaki kullanım hello `hdisecure`. Değiştir **RESOURCEGROUPNAME** hello Azure sanal ağı içeren hello kaynak grubu ile. Değiştir **konumu** hello konum (bölge) içinde bu hello grup oluşturuldu.

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    Merhaba Grup oluşturulduktan sonra hello yeni grubu hakkında bilgi alabilir.

2. Bağlantı noktası 443 üzerinden hello Azure Hdınsight sistem durumu ve yönetim hizmeti öğesinden gelen iletişime izin tooadd kuralları toohello yeni ağ güvenlik grubu aşağıdaki hello kullanın. Değiştir **RESOURCEGROUPNAME** hello Azure sanal ağı içeren hello kaynak grubunun hello ada sahip.

    > [!IMPORTANT]
    > Bu örnek toomatch hello kullanmakta olduğunuz Azure bölgesi kullanılan hello IP adreslerini değiştirin. Bu bilgileri hello bulabilirsiniz [Hdınsight ağ güvenlik gruplarını ve kullanıcı tanımlı yollar ile](#hdinsight-ip) bölümü.

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. tooretrieve bu ağ güvenlik grubu için benzersiz tanımlayıcı Merhaba, hello aşağıdaki komutu kullanın:

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    Bu komut metnini izleyen bir değer benzer toohello döndürür:

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    Beklenen hello sonuç alamazsanız kimliği etrafında çift tırnak hello komutunu kullanın.

4. Kullanım hello aşağıdaki tooapply hello ağ güvenlik grubu tooa alt komutu. Hello yerine __GUID__ ve __RESOURCEGROUPNAME__ hello olanları değerlerle hello önceki adımdaki döndürdü. Değiştir __vnetname ADLI__ ve __SUBNETNAME__ hello sanal ağ adı ve alt ağ adıyla toocreate istiyor.

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    Bu komut tamamlandıktan sonra sanal ağ hello Hdınsight yükleyebilirsiniz.

> [!IMPORTANT]
> Bu adımları yalnızca access toohello Hdınsight sistem durumu ve yönetim hizmetine hello Azure bulut açın. Tüm diğer erişim toohello Hdınsight kümeden dış hello sanal ağ engellendi. tooenable erişim hello sanal ağ dışından, ek ağ güvenlik grubu kuralları eklemeniz gerekir.
>
> Aşağıdaki örneğine hello nasıl tooenable SSH erişim Internet hello gösterir:
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <a id="example-dns"></a>Örnek: DNS yapılandırması

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a>Sanal bir ağa bağlı şirket içi ağ arasındaki ad çözümlemesi

Bu örnek varsayımlar aşağıdaki hello yapar:

* Bir Azure sanal bir VPN ağ geçidi kullanarak bağlı tooan şirket içi ağ ağ var.

* Merhaba özel DNS sunucusu hello sanal ağındaki hello işletim sistemi olarak Linux veya UNIX çalışıyor.

* [Bağlama](https://www.isc.org/downloads/bind/) hello özel DNS sunucusuna yüklenir.

Merhaba özel DNS sunucusunda hello sanal ağ içinde:

1. Sanal ağ hello Azure PowerShell veya Azure CLI toofind hello DNS sonekini kullanın:

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. Merhaba özel DNS sunucusunda hello sanal ağ için metin hello Merhaba içeriğine aşağıdaki hello kullanın `/etc/bind/named.conf.local` dosyası:

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    Hello yerine `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` hello sanal ağınızın DNS soneki ile değer.

    Bu yapılandırma tüm DNS isteklerine hello sanal ağ toohello Azure özyinelemeli çözümleyici hello DNS soneki için yönlendirir.

2. Merhaba özel DNS sunucusunda hello sanal ağ için metin hello Merhaba içeriğine aşağıdaki hello kullanın `/etc/bind/named.conf.options` dosyası:

    ```
    // Clients tooaccept requests from
    // TODO: Add hello IP range of hello joined network toothis list
    acl goodclients {
        10.0.0.0/16; # IP address range of hello virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent toohello following
            forwarders {
                192.168.0.1; # Replace with hello IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * Hello yerine `10.0.0.0/16` hello IP adres aralığını, sanal ağınızın değerle. Bu giriş, ad çözümleme istekleri adreslerini bu aralıkta sağlar.

    * Merhaba şirket içi ağ toohello Hello IP adres aralığı Ekle `acl goodclients { ... }` bölümü.  Giriş ad çözümleme isteklerinin kaynaklardan hello şirket ağında sağlar.
    
    * Merhaba değeri değiştirin `192.168.0.1` hello şirket içi DNS sunucunuzun IP adresine sahip. Bu giriş, tüm diğer DNS isteklerini toohello şirket DNS sunucularına yönlendirir.

3. toouse hello yapılandırma, bağlama yeniden başlatın. Örneğin, `sudo service bind9 restart`.

4. Bir koşullu ileticisi toohello şirket içi DNS sunucusu ekleyin. Adım 1 toohello özel DNS sunucusundan hello DNS soneki için Hello koşullu ileticisi toosend istekleri yapılandırın.

    > [!NOTE]
    > DNS yazılımınızın nasıl özellikleri için Hello belgelerine tooadd koşullu ileticisi.

Bu adımları tamamladıktan sonra tam etki alanı adları (FQDN) kullanarak ya da ağ tooresources bağlanabilir. Bu gibi durumlarda, Hdınsight şimdi hello sanal ağınıza yükleyebilirsiniz.

### <a name="name-resolution-between-two-connected-virtual-networks"></a>İki bağlı sanal ağlar arasındaki ad çözümlemesi

Bu örnek varsayımlar aşağıdaki hello yapar:

* İki Azure sanal veya eşliği ya da, bir VPN ağ geçidi kullanarak bağlanan ağ var.

* Her iki ağ Hello özel DNS sunucusu, Linux veya UNIX hello işletim sistemi olarak çalışıyor.

* [Bağlama](https://www.isc.org/downloads/bind/) hello özel DNS sunucularında yüklü.

1. Her iki sanal ağlar Azure PowerShell veya Azure CLI toofind hello DNS sonekini kullanın:

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. Metin hello Merhaba içeriğine aşağıdaki kullanım hello `/etc/bind/named.config.local` hello özel DNS sunucusunda dosya. Merhaba özel DNS sunucusunda hem de sanal ağlarda bu değişikliği yapın.

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello IP address of hello DNS server in hello other virtual network
    };
    ```

    Hello yerine `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` hello hello DNS soneki değeri __diğer__ sanal ağ. Bu girdi hello uzak ağ toohello hello DNS soneki için istekleri yönlendirir özel ağındaki DNS, o.

3. Metin hello Merhaba içeriğine aşağıdaki hello Hello özel DNS sunucularında hem de sanal ağlarda kullanmak `/etc/bind/named.conf.options` dosyası:

    ```
    // Clients tooaccept requests from
    acl goodclients {
        10.1.0.0/16; # hello IP address range of one virtual network
        10.0.0.0/16; # hello IP address range of hello other virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            forwarders {
            168.63.129.16;   # Azure recursive resolver         
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * Hello yerine `10.0.0.0/16` ve `10.1.0.0/16` değerleri ile başlangıç IP adresi aralıkları, sanal ağların. Bu girdi her ağ kaynaklarında hello DNS sunucularının toomake isteklere izin verir.

    Merhaba sanal ağların (örneğin, microsoft.com) DNS soneklerini hello olmayan tüm istekler hello Azure özyinelemeli çözümleyici tarafından işlenir.

4. toouse hello yapılandırma, bağlama yeniden başlatın. Örneğin, `sudo service bind9 restart` hem DNS sunucularında.

Bu adımları tamamladıktan sonra tam etki alanı adları (FQDN) kullanarak hello sanal ağ içinde tooresources bağlanabilir. Bu gibi durumlarda, Hdınsight şimdi hello sanal ağınıza yükleyebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

* Hdınsight tooconnect tooan şirket içi ağ yapılandırma uçtan uca örneği için bkz: [bağlanmak Hdınsight tooan şirket içi ağ](./connect-on-premises-network.md).

* Azure sanal ağlar hakkında daha fazla bilgi için bkz: Merhaba [Azure Virtual Network'e genel bakış](../virtual-network/virtual-networks-overview.md).

* Ağ güvenlik grupları hakkında daha fazla bilgi için bkz: [ağ güvenlik grupları](../virtual-network/virtual-networks-nsg.md).

* Kullanıcı tanımlı yollar hakkında daha fazla bilgi için bkz: [kullanıcı tanımlı yollar ve IP iletimini](../virtual-network/virtual-networks-udr-overview.md).