---
title: "aaaCreate PowerShell kullanarak birden çok NIC'yle bir VM'yi (Klasik) | Microsoft Docs"
description: "Bilgi nasıl toocreate ve PowerShell kullanarak birden çok NIC VM'ler yapılandırın."
services: virtual-network, virtual-machines
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a1a3952c-2dcc-4977-bd7a-52d623c1fb07
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 8ef35bd4cfd7e6a527080f1cfc541275ca86f5e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a>Birden çok NIC ile VM (Klasik) oluşturun
Sanal makineler (VM'ler) oluşturma ve birden çok ağ arabirimlerine (NIC'ler) tooeach, VM'lerin ekleyin. Birden çok NIC uygulama sunma ve WAN iyileştirmesi çözümleri gibi birçok ağ sanal Gereçleri gereksinimi var. Birden çok NIC de NIC'ler arasında trafik yalıtımı sağlar.

![VM için multi NIC](./media/virtual-networks-multiple-nics/IC757773.png)

üç NIC ile VM Hello şekil gösterir, her tooa farklı alt bağlı.

> [!IMPORTANT]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır. Microsoft, en yeni dağıtımların Resource Manager kullanmanızı önerir.

* Internet'e yönelik VIP (Klasik dağıtımlar) yalnızca hello "varsayılan" NIC üzerinde desteklenir Merhaba varsayılan NIC yalnızca bir VIP toohello IP'si yok
* Şu anda örnek düzeyinde ortak IP (LPIP) adresleri (Klasik dağıtımlar) birden çok NIC sanal makineleri için desteklenmez.
* Merhaba hello NIC'ler sırasını VM rastgele olur ve ayrıca Azure altyapı güncelleştirmeleri arasında değişebilir hello içinde. Ancak, hello IP adresleri ve karşılık gelen ethernet MAC hello adresleri kalacak aynı hello. Örneğin, varsayın **Eth1** bir Azure Altyapı güncelleştirme ve yeniden başlatma çok değiştirilemedi; IP adresi 10.1.0.100 ve 00-0D-3A-B0-39-0D MAC adresi var.**Eth2**, ancak işlem eşleştirme IP ve MAC hello Kalan aynı hello. Müşteri tarafından başlatılan yeniden başlatma olduğunda hello NIC sipariş kalacak aynı hello.
* Merhaba adresi her NIC'nin her VM için bir alt ağda bulunması gerekir, tek bir birden çok NIC VM her atanabilir içinde adreslerinin aynı alt ağda hello.
* Hello VM boyutu için bir VM oluşturun NIC hello sayısını belirler. Başvuru hello [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ve [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM boyutları makaleleri toodetermine kaç NIC her VM boyutunu destekler. 

## <a name="network-security-groups-nsgs"></a>Ağ güvenlik grupları (Nsg'ler)
Resource Manager dağıtımında, bir VM üzerinde herhangi bir NIC ile ağ güvenlik grubu (birden çok NIC etkin olan bir VM üzerinde herhangi bir NIC içeren NSG), ilişkili olabilir. Bir NIC hello alt ağa bir NSG ile ilişkili olduğu bir alt ağ içinden bir adres atanırsa, ardından hello kuralları hello alt ağın NSG de toothat NIC Uygula Nsg'ler ile toplama tooassociating alt ağlarında bir NSG'yi bir NIC de ilişkilendirebilirsiniz.

Bir alt ağa bir NSG ve içinde bir NIC ile ilişkili ise bu alt ağ ile bir NSG tek tek ilişkilidir, ilişkili hello NSG kuralları uygulanır **akış sırası** toohello trafiğin yönü, içinde veya dışında geçirilen hello göre Merhaba NIC:

* **Gelen trafiği** hello NIC soru, hedefi olan akışlar ilk NIC hello geçirme sonra hello NIC'ın NSG kuralları tetiklemeden önce hello alt ağın NSG kuralları tetikleme hello alt ağ üzerinden.
* **Giden trafik** akar hello hello alt ağa geçirmeden sonra hello alt ağın NSG kuralları tetiklemeden önce hello NIC'ın NSG kuralları tetikleme NIC ilk out hello NIC söz konusu olan kaynağıdır.

Daha fazla bilgi edinmek [ağ güvenlik grupları](virtual-networks-nsg.md) ve nasıl uygulandığını ilişkilendirmeleri toosubnets, sanal makineleri ve NIC göre...

## <a name="how-tooconfigure-a-multi-nic-vm-in-a-classic-deployment"></a>Nasıl tooConfigure klasik bir dağıtımda birden çok NIC VM
Merhaba yönergelerde birden çok NIC 3 NIC içeren VM oluşturmanıza yardımcı olur: varsayılan bir NIC ve iki ek NIC. Merhaba yapılandırma adımları toohello hizmet yapılandırma dosyası parça aşağıdaki göre yapılandırılmış bir VM oluşturacak:

    <VirtualNetworkSite name="MultiNIC-VNet" Location="North Europe">
    <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
    … Skip over hello remainder section …
    </VirtualNetworkSite>


Önkoşullar toorun hello PowerShell komutlarını hello örnekte denemeden önce aşağıdaki hello gerekir.

* Azure aboneliği.
* Yapılandırılmış bir sanal ağ. Bkz: [Virtual Network'e genel bakış](virtual-networks-overview.md) sanal ağlar hakkında daha fazla bilgi.
* Azure PowerShell'in en son sürümünü Hello indirilir ve yüklenir. Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

birden çok NIC, aşağıdaki adımları tek bir PowerShell oturumunda her komutunu girerek tam hello'yle bir VM'yi toocreate:

1. Azure VM görüntü Galeriden bir VM görüntüsü seçin. Görüntüleri sık sık değişen ve bölgeye göre kullanılabilir olduğunu unutmayın. Hello hello aşağıdaki örnekte belirtilen görüntüsü değiştirmek veya değil bölgenizde olması, bu nedenle emin olun ihtiyacınız toospecify hello görüntü.

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. Bir VM yapılandırması oluşturun.

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. Merhaba varsayılan yönetici oturum açma oluşturun.

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. Ek NIC toohello VM yapılandırmasına ekleyin.

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. Merhaba varsayılan NIC için Hello alt ağ ve IP adresi belirtin

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. Merhaba VM sanal ağınızda oluşturun.

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > Hello burada belirttiğiniz VNet (Merhaba önkoşullarını belirtildiği gibi) olması gerekir. Aşağıdaki örnek Hello belirtir adlı bir sanal ağ **MultiNIC VNet**.
    >

## <a name="limitations"></a>Sınırlamalar
birden çok NIC kullanırken aşağıdaki sınırlamalar hello geçerlidir:

* Birden çok NIC içeren VM'ler Azure sanal ağlar (Vnet'ler) içinde oluşturulmalıdır. Non-VNet VM'ler ile birden çok NIC yapılandırılamaz.
* Birden çok NIC veya tek bir NIC gerek toouse tüm sanal makineleri bir kullanılabilirlik kümesi Birden çok NIC VM'ler ve bir kullanılabilirlik kümesi içinde tek NIC VM'ler bileşimi olamaz. Aynı kuralları, bir bulut hizmetinde VM'ler için geçerlidir. Gerekli olmayan birden çok NIC VM'ler için en az iki sahip oldukları her sürece toohave hello NIC'ler, aynı sayıda.
* Birden çok NIC (ve tersi) ile tek bir NIC ile VM yapılandırılamaz, silme ve yeniden oluşturulması dağıtıldıktan sonra.

## <a name="secondary-nics-access-tooother-subnets"></a>İkincil NIC'ler erişim tooother alt
İkincil NIC'ler bir varsayılan ağ geçidi ile değil yapılandırılacak varsayılan olarak, toowhich hello trafik akışını hello son ikincil NIC sınırlı toobe hello içinde olacaktır aynı alt ağ. Merhaba kullanıcıların tooenable ikincil NIC'ler tootalk kendi alt ağı dışından istiyorsanız, bunlar hello yönlendirme tablosu tooconfigure hello ağ geçidi olarak bir giriş aşağıda açıklanan tooadd gerekir.

> [!NOTE]
> Temmuz 2015 tüm NIC'ler için yapılandırılmış bir varsayılan ağ geçidi olabilir önce oluşturulan VM'ler. Bu sanal makineleri yeniden kadar ikincil NIC'ler için hello varsayılan ağ geçidi kaldırılmaz. İşletim sistemlerindeki hello zayıf ana bilgisayar yönlendirme modeli, Linux gibi kullanın Hello giriş ve çıkış trafiği farklı NIC'ler kullanırsanız Internet bağlantısını kesebilirsiniz.
> 

### <a name="configure-windows-vms"></a>Windows sanal makineleri yapılandırma
İki NIC içeren bir Windows VM gibi olduğunu varsayalım:

* Birincil NIC IP adresi: 192.168.1.4
* İkincil NIC IP adresi: 192.168.2.5

Bu VM için Hello IPv4 yol tablosu şöyle olabilir:

    IPv4 Route Table
    ===========================================================================
    Active Routes:
    Network Destination        Netmask          Gateway       Interface  Metric
              0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
            127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
            127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
      127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        168.63.129.16  255.255.255.255      192.168.1.1      192.168.1.4      6
          192.168.1.0    255.255.255.0         On-link       192.168.1.4    261
          192.168.1.4  255.255.255.255         On-link       192.168.1.4    261
        192.168.1.255  255.255.255.255         On-link       192.168.1.4    261
          192.168.2.0    255.255.255.0         On-link       192.168.2.5    261
          192.168.2.5  255.255.255.255         On-link       192.168.2.5    261
        192.168.2.255  255.255.255.255         On-link       192.168.2.5    261
            224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
            224.0.0.0        240.0.0.0         On-link       192.168.1.4    261
            224.0.0.0        240.0.0.0         On-link       192.168.2.5    261
      255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
      255.255.255.255  255.255.255.255         On-link       192.168.1.4    261
      255.255.255.255  255.255.255.255         On-link       192.168.2.5    261
    ===========================================================================

Bu hello varsayılan yol (0.0.0.0) yalnızca kullanılabilir toohello birincil NIC olduğuna dikkat edin Merhaba ikincil için hello alt dışındaki mümkün tooaccess kaynaklar olmaz aşağıda görüldüğü gibi NIC:

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

Varsayılan rota tooadd hello ikincil NIC, aşağıdaki hello adımları izleyin:

1. Merhaba tooidentify hello dizin numarasını aşağıdaki hello komutunu bir komut isteminden çalıştırın ikincil NIC:
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. (Bu örnekte) 27 dizini ile Merhaba tablosunda ikinci girişi Hello dikkat edin.
3. Merhaba Hello komut isteminden çalıştırın **yolu Ekle** komutunu aşağıda gösterildiği gibi. Bu örnekte, hello için hello varsayılan ağ geçidi olarak 192.168.2.1 belirtiyorsanız ikincil NIC:
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. tootest bağlantısı toohello komut istemi geri dönün ve farklı bir alt ağdan hello ikincil NIC gösterilen int eh aşağıdaki örnekte tooping deneyin:
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. Ayrıca, rota tablosu toocheck hello yolu, yeni eklenen aşağıda gösterildiği gibi kontrol edebilirsiniz:
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a>Linux sanal makineleri yapılandırma
Merhaba varsayılan davranışı yönlendirme, zayıf konak kullandığından Linux VM'ler için o hello ikincil NIC'ler öneririz hello içinde yalnızca kısıtlı tootraffic akışları olan aynı alt ağ. Ancak bazı senaryolar hello alt dışında bağlantı istiyorsa, kullanıcıların giriş hello İlkesi tabanlı yönlendirme tooensure etkinleştirmeniz gerekir ve çıkış trafiği kullandığı aynı NIC hello

## <a name="next-steps"></a>Sonraki adımlar
* Dağıtma [MultiNIC VM'ler 2 katmanlı uygulama senaryosunda bir Resource Manager dağıtımında](virtual-network-deploy-multinic-arm-template.md).
* Dağıtma [Klasik dağıtım 2 katmanlı uygulama senaryoda MultiNIC Vm'lerde](virtual-network-deploy-multinic-classic-ps.md).

