---
title: "aaaConnect Hdınsight tooyour şirket içi ağ - Azure Hdınsight | Microsoft Docs"
description: "Tooyour şirket içi ağ bağlanmak ve nasıl toocreate bir Hdınsight kümesi bir Azure sanal ağında öğrenin. Nasıl tooconfigure ad çözümlemesi Hdınsight ve şirket içi ağınız arasında özel bir DNS sunucusu kullanılarak öğrenin."
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a3adf0e3df7726d8e6566d723700506baaf89a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-hdinsight-tooyour-on-premise-network"></a>Hdınsight tooyour şirket içi ağa bağlan

Nasıl tooconnect Hdınsight tooyour ağ Azure sanal ağlar ve VPN ağ geçidi kullanarak şirket içi öğrenin. Bu belge planlama bilgilerini sağlar:

* Bir Azure sanal tooyour bağlayan ağ içinde Hdınsight kullanarak ağ şirket içi.

* DNS ad çözümlemesi hello sanal ağ ve şirket içi ağınız arasında yapılandırma.

* Ağ güvenlik grupları toorestrict Internet erişimi tooHDInsight yapılandırma.

* Merhaba sanal ağda Hdınsight tarafından sağlanan bağlantı noktaları.

## <a name="create-hello-virtual-network-configuration"></a>Merhaba sanal ağ yapılandırması oluştur

> [!IMPORTANT]
> Bağlama hakkında adım adım kılavuz arıyorsanız, Hdınsight tooyour şirket içi bir Azure sanal ağı kullanarak ağ'yı, hello bkz [bağlanmak Hdınsight tooyour şirket içi ağ](connect-on-premises-network.md) belge.

Kullanım hello aşağıdaki belgeler toolearn nasıl toocreate bir Azure sanal bağlı tooyour ağ ağ içi:
    
* [Hello Azure portalını kullanma](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [Azure PowerShell’i kullanma](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [Azure CLI’yi kullanma](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a>Ad çözümlemesini yapılandırma

tooallow Hdınsight ve ada göre birleştirilmiş hello ağ toocommunicate kaynaklarında hello aşağıdaki eylemleri gerçekleştirmeniz gerekir:

* Özel bir DNS sunucusu hello Azure sanal ağ oluşturun.

* Merhaba sanal ağ toouse hello özel DNS sunucusu hello varsayılan Azure özyinelemeli çözümleyici yerine yapılandırın.

* Merhaba özel DNS sunucusu ve şirket içi DNS sunucunuz arasında iletim yapılandırın.

Bu yapılandırma davranışı aşağıdaki hello sağlar:

* Merhaba DNS sonekine sahip tam etki alanı adları için istekleri __hello sanal ağ için__ toohello özel DNS sunucusu iletilir. Merhaba özel DNS sunucusu, daha sonra bu istekleri toohello başlangıç IP adresi döndürür Azure özyinelemeli çözümleyici iletir.

* Tüm diğer isteklerden toohello şirket DNS sunucusuna iletilir. Microsoft.com gibi ortak Internet kaynakların bile istekleri toohello şirket içi DNS sunucusu ad çözümlemesi için iletilir.

Diyagram aşağıdaki hello çizgiler hello sanal ağın DNS soneki hello bitiş kaynaklara yönelik isteklerin ' dir. Mavi satırlar hello şirket içi ağ veya üzerinde kaynaklara yönelik isteklerin genel internet hello gelir.

![Bu belgede kullanılan hello yapılandırmasında DNS isteklerine nasıl çözüleceğini diyagramı](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a>Özel bir DNS sunucusu oluştur

> [!IMPORTANT]
> Oluşturma ve Hdınsight hello sanal ağınıza yüklemeden önce hello DNS sunucusu yapılandırmanız gerekir.

toocreate hello kullanan bir Linux VM [bağlamak](https://www.isc.org/downloads/bind/) DNS yazılım, aşağıdaki adımları kullanın hello:

> [!NOTE]
> Merhaba aşağıdaki adımları kullanın hello [Azure portal](https://portal.azure.com) toocreate bir Azure sanal makine. Diğer yolları toocreate bir sanal makine için hello bkz [VM Oluştur - Azure CLI](../virtual-machines/linux/quick-create-cli.md) ve [VM Oluştur - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) belgeleri.

1. Merhaba gelen [Azure portal](https://portal.azure.com)seçin  __+__ , __işlem__, ve __Ubuntu Server 16.04 LTS__.

    ![Ubuntu sanal makine oluşturma](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. Merhaba gelen __Temelleri__ bölümünde, aşağıdaki bilgilerle hello girin:

    * __Ad__: Bu sanal makineyi tanımlayan bir kolay ad. Örneğin, __DNSProxy__.
    * __Kullanıcı adı__: hello SSH hesabı hello adı.
    * __SSH ortak anahtarını__ veya __parola__: Merhaba hello SSH hesabı için kimlik doğrulama yöntemi. Daha güvenli olarak ortak anahtarları kullanmanızı öneririz. Daha fazla bilgi için bkz: Merhaba [Linux VM'ler için SSH anahtarları oluşturma ve kullanma](../virtual-machines/linux/mac-create-ssh-keys.md) belge.
    * __Kaynak grubu__: seçin __var olanı kullan__ve ardından daha önce oluşturduğunuz hello sanal ağ içeren hello kaynak grubunu seçin.
    * __Konum__: Merhaba hello sanal ağ ile aynı konumda seçin.

    ![Sanal makine temel yapılandırma](./media/connect-on-premises-network/vm-basics.png)

    Merhaba diğer girişler varsayılan değerleri bırakın ve ardından __Tamam__.

3. Merhaba gelen __bir boyutu seçin__ bölümünde, select hello VM boyutu. Bu öğretici için en küçük hello seçin ve seçeneği en düşük maliyeti. toocontinue, kullanım hello __seçin__ düğmesi.

4. Merhaba gelen __ayarları__ bölümünde, aşağıdaki bilgilerle hello girin:

    * __Sanal ağ__: Merhaba daha önce oluşturduğunuz sanal ağ seçin.

    * __Alt ağ__: hello sanal ağ için hello varsayılan alt ağ seçin. Yapmak __değil__ hello hello VPN ağ geçidi tarafından kullanılan alt ağ seçin.

    * __Tanılama depolama hesabı__: mevcut bir depolama hesabını seçin veya yeni bir tane oluşturun.

    ![Sanal ağ ayarları](./media/connect-on-premises-network/virtual-network-settings.png)

    Bırakın hello diğer girişler hello varsayılan değerinde sonra seçin __Tamam__ toocontinue.

5. Merhaba gelen __satın alma__ bölümü, select hello __satın alma__ düğmesini toocreate hello sanal makine.

6. Merhaba sanal makine oluşturulduktan sonra kendi __genel bakış__ bölümünde görüntülenir. Merhaba hello soldaki listesinden __özellikleri__. Merhaba Kaydet __genel IP adresi__ ve __özel IP adresi__ değerleri. Merhaba sonraki bölümde kullanılır.

    ![Ortak ve özel IP adresleri](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a>Yükleme ve bağlama (DNS yazılım) yapılandırma

1. SSH tooconnect toohello kullanmak __genel IP adresi__ hello sanal makinenin. Aşağıdaki örnek hello 40.68.254.142 tooa sanal makinenin bağlanır:

    ```bash
    ssh sshuser@40.68.254.142
    ```

    Değiştir `sshuser` hello SSH kullanıcı hesabı ile Merhaba kümesi oluştururken belirttiğiniz.

    > [!NOTE]
    > Yolları tooobtain hello çeşitli vardır `ssh` yardımcı programı. Linux, Unix ve macOS üzerinde hello işletim sisteminin bir parçası sağlanır. Windows kullanıyorsanız, aşağıdaki seçenekleri şu hello birini göz önünde bulundurun:
    >
    > * [Azure bulut Kabuğu](../cloud-shell/quickstart.md)
    > * [Windows 10 Ubuntu bash](https://msdn.microsoft.com/commandline/wsl/about)
    > * [Git (https://git-scm.com/)](https://git-scm.com/)
    > * [OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. tooinstall bağlama hello SSH oturumundan komutları aşağıdaki hello kullan:

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. tooconfigure bağlama tooforward ad çözümleme istekleri tooyour şirket içi DNS sunucusu kullanın metin hello Merhaba içeriğine aşağıdaki hello `/etc/bind/named.conf.options` dosyası:

        acl goodclients {
            10.0.0.0/16; # Replace with hello IP address range of hello virtual network
            10.1.0.0/16; # Replace with hello IP address range of hello on-premises network
            localhost;
            localnets;
        };

        options {
                directory "/var/cache/bind";

                recursion yes;

                allow-query { goodclients; };

                forwarders {
                192.168.0.1; # Replace with hello IP address of hello on-premises DNS server
                };

                dnssec-validation auto;

                auth-nxdomain no;    # conform tooRFC1035
                listen-on { any; };
        };

    > [!IMPORTANT]
    > Hello başlangıç değerleri değiştirin `goodclients` hello IP adres aralığı bir bölümle hello sanal ağ ve şirket içi ağ. Bu bölümde, bu DNS sunucusu gelen istekleri kabul hello adreslerini tanımlar.
    >
    > Hello yerine `192.168.0.1` hello girişi `forwarders` hello IP adresine sahip bir bölüm şirket içi DNS sunucunuzun. Bu giriş yolları DNS isteklerini tooyour çözümlemesi için DNS sunucusu şirket içi.

    tooedit bu dosya, komutu aşağıdaki kullanım hello:

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    toosave hello dosya, kullanım __Ctrl + X__, __Y__ve ardından __Enter__.

4. Merhaba SSH oturumundan hello aşağıdaki komutu kullanın:

    ```bash
    hostname -f
    ```

    Bu komut metnini izleyen bir değer benzer toohello döndürür:

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    Merhaba `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` metindir hello __DNS soneki__ bu sanal ağ için. Bu değer daha sonra kullanılmak üzere kaydedin.

5. tooconfigure bağlama tooresolve DNS adlarını hello sanal ağ içindeki kaynakların kullanmak metin hello Merhaba içeriğine aşağıdaki hello `/etc/bind/named.conf.local` dosyası:

        // Replace hello following with hello DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # hello Azure recursive resolver
        };

    > [!IMPORTANT]
    > Merhaba değiştirmelisiniz `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` daha önce hello DNS soneki.

    tooedit bu dosya, komutu aşağıdaki kullanım hello:

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    toosave hello dosya, kullanım __Ctrl + X__, __Y__ve ardından __Enter__.

6. toostart bağlama hello aşağıdaki komutu kullanın:

    ```bash
    sudo service bind9 restart
    ```

7. bağlama tooverify kaynakların şirket içi ağınızda, aşağıdaki komutları kullanın hello hello adları çözümleyebilirsiniz:

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > Değiştir `dns.mynetwork.net` , şirket içi ağınıza bir kaynak hello tam etki alanı adı (FQDN).
    >
    > Değiştir `10.0.0.4` hello ile __iç IP adresi__ özel DNS sunucunuzun hello sanal ağ.

    Merhaba yanıt metni aşağıdaki benzer toohello görüntülenir:

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-hello-virtual-network-toouse-hello-custom-dns-server"></a>Merhaba sanal ağ toouse hello özel DNS sunucusunu yapılandırma

tooconfigure hello sanal ağ toouse hello özel DNS sunucusu hello Azure özyinelemeli çözümleyici yerine hello aşağıdaki adımları kullanın:

1. Merhaba, [Azure portal](https://portal.azure.com)hello sanal ağ seçin ve ardından __DNS sunucuları__.

2. Seçin __özel__ve hello girin __iç IP adresi__ hello özel DNS sunucusunun. Son olarak, seçin __kaydetmek__.

    ![Merhaba ağ Hello özel DNS sunucusunu ayarlayın](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-hello-on-premises-dns-server"></a>Merhaba şirket içi DNS sunucusunu yapılandırma

Merhaba önceki bölümde hello özel DNS sunucusu tooforward istekleri toohello şirket içi DNS sunucusu yapılandırılmış. Ardından, hello şirket içi DNS sunucusu tooforward istekleri toohello özel DNS sunucusu yapılandırmanız gerekir.

Belirli adımları için tooconfigure DNS sunucunuzun, DNS sunucusu yazılımınızı için hello belgelere. Merhaba adımları arayın tooconfigure bir __koşullu ileticisi__.

Koşullu iletme, yalnızca belirli bir DNS soneki isteklerini iletir. Bu durumda, iletici hello DNS soneki hello sanal ağ için yapılandırmanız gerekir. Bu soneki isteklerinde hello özel DNS sunucusunun IP adresini toohello iletilmesi gereken. 

Merhaba aşağıdaki hello iletici yapılandırması örneği metindir **bağlamak** DNS yazılım:

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello custom DNS server's internal IP address
    };

DNS kullanma hakkında bilgi için **Windows Server 2016**, hello bkz [Ekle DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) belgelerine...

Merhaba şirket içi DNS sunucusunu yapılandırdıktan sonra kullanabileceğiniz `nslookup` hello şirket içi ağ tooverify hello sanal ağ adları, çözebilirsiniz. Aşağıdaki örnek hello 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

Kullanan şirket içi DNS sunucusunda 196.168.0.4 hello Bu örnek tooresolve hello hello özel DNS sunucusunun adı. Başlangıç IP adresi hello şirket içi DNS sunucusu için hello değiştirin. Hello yerine `dnsproxy` hello tam olarak nitelenmiş etki alanı adıyla hello özel DNS sunucusunun adresi.

## <a name="optional-control-network-traffic"></a>İsteğe bağlı: Denetim ağ trafiği

Ağ güvenlik grubu (NSG) veya kullanıcı tanımlı yolları (UDR) toocontrol ağ trafiğini kullanabilirsiniz. Nsg'ler izin toofilter gelen ve giden trafiği ve izin verin veya hello trafiği reddedin. Udr'ler nasıl hello sanal ağınızdaki kaynaklara arasında trafiği akan toocontrol izin, Internet hello ve şirket içi ağ hello.

> [!WARNING]
> Hdınsight hello Azure bulut, belirli IP adreslerinden gelen erişim ve sınırsız giden erişim gerektirir. Nsg'ler veya Udr'ler toocontrol trafiği kullanırken hello aşağıdaki adımları gerçekleştirmeniz gerekir:
>
> 1. Merhaba IP adresleri sanal ağınızı içeren hello konumunu bulun. Konuma göre gerekli IP'leri listesi için bkz: [gerekli IP adreslerini](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).
>
> 2. Merhaba IP adreslerinden gelen trafiğe izin verin.
>
>    * __NSG__: izin __gelen__ bağlantı noktasında trafik __443__ hello gelen __Internet__.
>    * __UDR__: kümesi hello __sonraki atlama__ hello rota too__Internet__ türü.

Hello Azure PowerShell veya hello Azure CLI toocreate Nsg'leri kullanarak bir örnek için bkz: [genişletmek Hdınsight Azure sanal ağlar ile](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) belge.

## <a name="create-hello-hdinsight-cluster"></a>Merhaba Hdınsight kümesi oluşturma

> [!WARNING]
> Hdınsight hello sanal ağında yüklemeden önce hello özel DNS sunucusu yapılandırmanız gerekir.

Kullanım hello adımları hello [hello Azure portal kullanarak bir Hdınsight kümesi oluşturmayı](./hdinsight-hadoop-create-linux-clusters-portal.md) belge toocreate Hdınsight kümesi.

> [!WARNING]
> * Küme oluşturma sırasında sanal ağınızı içeren hello konumu seçmelisiniz.
>
> * Merhaba, __Gelişmiş ayarları__ bölümü yapılandırmasına, hello sanal ağ ve daha önce oluşturduğunuz alt seçmeniz gerekir.

## <a name="connecting-toohdinsight"></a>TooHDInsight bağlanma

Hdınsight üzerinde çoğu belgelerine hello erişim toohello küme sahip olduğunuzu varsayar Internet. Https://CLUSTERNAME.azurehdinsight.net toohello kümesine bağlayabilirsiniz örneğin. Bu adres Nsg'ler kullandınız veya Udr'ler toorestrict erişimden hello Internet kullanılabilir değilse hello ortak ağ geçidi, kullanır.

toodirectly tooHDInsight hello sanal ağ üzerinden bağlanmasına, hello aşağıdaki adımları kullanın:

1. toodiscover hello iç tam etki alanı adları hello Hdınsight küme düğümlerinin yöntemler aşağıdaki hello birini kullanın:

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

2. bir hizmet, kullanılabilir toodetermine hello bağlantı noktasına bkz hello [hdınsight'ta Hadoop Hizmetleri tarafından kullanılan bağlantı noktaları](./hdinsight-hadoop-port-settings-for-services.md) belge.

    > [!IMPORTANT]
    > Merhaba baş düğümler üzerinde barındırılan bazı hizmetler aynı anda yalnızca bir düğümde etkin olur. Bir hizmet bir baş düğüm üzerindeki erişmeyi deneyin ve başarısız olursa, diğer baş düğüm toohello geçin.
    >
    > Örneğin, Ambari yalnızca aynı anda bir baş düğüm üzerinde etkindir. Ambari bir baş düğüm üzerinde erişmeyi deneyin ve üzerinde çalıştırıldığı sonra 404 hatası döndürürse diğer baş düğüm hello.

## <a name="next-steps"></a>Sonraki adımlar

* Sanal bir ağa Hdınsight kullanma hakkında daha fazla bilgi için bkz: [genişletmek Azure sanal ağları kullanarak Hdınsight](./hdinsight-extend-hadoop-virtual-network.md).

* Azure sanal ağlar hakkında daha fazla bilgi için bkz: Merhaba [Azure Virtual Network'e genel bakış](../virtual-network/virtual-networks-overview.md).

* Ağ güvenlik grupları hakkında daha fazla bilgi için bkz: [ağ güvenlik grupları](../virtual-network/virtual-networks-nsg.md).

* Kullanıcı tanımlı yollar hakkında daha fazla bilgi için bkz: [kullanıcı tanımlı yollar ve IP iletimini](../virtual-network/virtual-networks-udr-overview.md).
