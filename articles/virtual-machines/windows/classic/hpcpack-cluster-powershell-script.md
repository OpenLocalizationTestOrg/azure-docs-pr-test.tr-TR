---
title: "aaaPowerShell betik toodeploy Windows HPC Kümesi | Microsoft Docs"
description: "PowerShell komut dosyası toodeploy bir Windows HPC Pack 2012 R2 küme Azure sanal makinelerinde çalıştırın."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 286b2be8-2533-40df-b02a-26156b1f1133
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 10ce1e9bc4e98954b955549bd72aaaf6106c69fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a>Yüksek performanslı bilgi işlem (HPC) Windows Küme ile Merhaba HPC Pack Iaas dağıtım komut dosyası oluşturma
Merhaba HPC Pack Iaas dağıtım PowerShell komut dosyası toodeploy tam bir HPC Pack 2012 R2 küme iş yükleri için Azure sanal makinelerinde çalıştırın. Windows Server ve Microsoft HPC Pack çalıştıran bir Active Directory katılmış baş düğümüne Hello küme oluşur ve ek Windows işlem kaynaklarını belirttiğiniz. Linux iş yükleri için toodeploy Azure HPC Pack kümede istiyorsanız, bkz: [hello HPC Pack Iaas dağıtım betiği ile Linux HPC küme oluşturma](../../linux/classic/hpcpack-cluster-powershell-script.md). Azure Resource Manager şablonu toodeploy bir HPC paketi küme de kullanabilirsiniz. Örnekler için bkz: [bir HPC Kümesi oluşturmayı](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) ve [bir özel işlem düğümü görüntüsüyle HPC kümesi oluşturma](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).

> [!IMPORTANT] 
> Bu makalede açıklanan PowerShell betiğini Hello Azure'da hello Klasik dağıtım modeli kullanarak Microsoft HPC Pack 2012 R2 küme oluşturur. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.
> Ayrıca, bu makalede açıklanan hello betik HPC Pack 2016 desteklemez.

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-files"></a>Örnek yapılandırma dosyaları
Hello aşağıdaki örneklerde, kendi değerlerini, abonelik kimliği veya adı ve hello hesabı ve hizmet adlarını değiştirin.

### <a name="example-1"></a>Örnek 1
Merhaba aşağıdaki yapılandırma dosyası bir baş düğüm yerel veritabanlarıyla ve beş işlem düğümlerini hello Windows Server 2012 R2 işletim sistemi çalıştıran bir HPC Pack kümeye dağıtır. Tüm hello bulut Hizmetleri doğrudan hello Batı ABD konumunda oluşturulur. Merhaba baş düğüm hello etki alanı ormanı etki alanı denetleyicisi olarak işlev görür.

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionId>08701940-C02E-452F-B0B1-39D50119F267</SubscriptionId>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%1000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>5</NodeCount>
    <OSVersion>WindowsServer2012R2</OSVersion>
  </ComputeNodes>
</IaaSClusterConfig>
```

### <a name="example-2"></a>Örnek 2
Aşağıdaki yapılandırma dosyasına hello var olan bir etki alanı ormanı HPC Pack kümede dağıtır. Merhaba küme yerel veritabanlarıyla 1 baş düğüm vardır ve 12 işlem düğümleri hello uygulanan Bgınfo VM uzantısı ile.
Windows güncelleştirmeleri otomatik yüklemesini tüm hello hello etki alanı ormanda VM'ler devre dışı bırakılmıştır. Tüm hello bulut hizmetlerine doğrudan Doğu Asya konumda oluşturulur. Merhaba işlem düğümleri üç bulut Hizmetleri ve üç depolama hesabı oluşturulur: *MyHPCCN 0001* çok*MyHPCCN 0005* içinde *MyHPCCNService01* ve  *mycnstorage01*; *MyHPCCN-0006* çok*MyHPCCN0010* içinde *MyHPCCNService02* ve *mycnstorage02*; ve  *MyHPCCN-0011* çok*MyHPCCN 0012* içinde *MyHPCCNService03* ve *mycnstorage03*). Merhaba işlem düğümleri, bir işlem düğümünden yakalanan bir görüntüden varolan özel oluşturulur. Merhaba otomatik büyüme ve küçültme hizmeti varsayılan olarak etkin büyür ve küçültme aralıkları.

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>MyDCServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>Large</VMSize>
      </DomainController>
     <NoWindowsAutoUpdate />
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
  </Certificates>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0001%</VMNamePattern>
<ServiceNamePattern>MyHPCCNService%01%</ServiceNamePattern>
<MaxNodeCountPerService>5</MaxNodeCountPerService>
<StorageAccountNamePattern>mycnstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>12</NodeCount>
    <ImageName HPCPackInstalled=”true”>MyHPCComputeNodeImage</ImageName>
    <VMExtensions>
       <VMExtension>
          <ExtensionName>BGInfo</ExtensionName>
          <Publisher>Microsoft.Compute</Publisher>
          <Version>1.*</Version>
       </VMExtension>
    </VMExtensions>
  </ComputeNodes>
  <AutoGrowShrink>
    <CertificateId>1</CertificateId>
  </AutoGrowShrink>
</IaaSClusterConfig>

```

### <a name="example-3"></a>Örnek 3
Aşağıdaki yapılandırma dosyasına hello var olan bir etki alanı ormanı HPC Pack kümede dağıtır. Merhaba küme baş düğüm, 500 GB veri diski, bir veritabanı sunucusuyla hello Windows Server 2012 R2 işletim sistemi ve hello Windows Server 2012 R2 işletim sistemi çalıştıran beş işlem düğümleri çalışan iki Aracısı düğümleri içerir. Merhaba MyHPCCNService hello benzeşim grubunda oluşturulan bulut hizmeti *MyIBAffinityGroup*, ve hello diğer bulut hizmetlerine hello benzeşim grubunda oluşturulan *MyAffinityGroup*. Merhaba HPC iş Scheduler REST API ve HPC web portalı hello baş düğümünde etkinleştirilir.

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>    
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>NewRemoteDB</DBOption>
    <DBVersion>SQLServer2014_Enterprise</DBVersion>
    <DBServer>
      <VMName>MyDBServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>ExtraLarge</VMSize>
      <DataDiskSizeInGB>500</DataDiskSizeInGB>
    </DBServer>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>A8</VMSize>
<NodeCount>5</NodeCount>
<AffinityGroup>MyIBAffinityGroup</AffinityGroup>
  </ComputeNodes>
  <BrokerNodes>
    <VMNamePattern>MyHPCBN-%0000%</VMNamePattern>
    <ServiceName>MyHPCBNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>2</NodeCount>
  </BrokerNodes>
</IaaSClusterConfig>
```



### <a name="example-4"></a>Örnek 4
Aşağıdaki yapılandırma dosyasına hello var olan bir etki alanı ormanı HPC Pack kümede dağıtır. Merhaba küme olan iki baş düğüm yerel veritabanları ile iki Azure düğümü şablonları oluşturulur ve üç boyut Orta Azure düğümleri için Azure düğüm şablonu oluşturulur *AzureTemplate1*. Merhaba baş düğüm yapılandırıldıktan sonra bir komut dosyası hello baş düğüm üzerinde çalışır.

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
<VMSize>ExtraLarge</VMSize>
    <PostConfigScript>c:\MyHNPostActions.ps1</PostConfigScript>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
    <Certificate>
      <Id>2</Id>
      <PfxFile>d:\mytestcert2.pfx</PfxFile>
    </Certificate>    
  </Certificates>
  <AzureBurst>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate1</TemplateName>
      <SubscriptionId>bb9252ba-831f-4c9d-ae14-9a38e6da8ee4</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc1</ServiceName>
      <StorageAccount>myteststorage1</StorageAccount>
      <NodeCount>3</NodeCount>
      <RoleSize>Medium</RoleSize>
    </AzureNodeTemplate>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate2</TemplateName>
      <SubscriptionId>ad4b9f9f-05f2-4c74-a83f-f2eb73000e0b</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc2</ServiceName>
      <StorageAccount>myteststorage2</StorageAccount>
      <Proxy>
        <UsesStaticProxyCount>false</UsesStaticProxyCount>     
        <ProxyRatio>100</ProxyRatio>
        <ProxyRatioBase>400</ProxyRatioBase>
      </Proxy>
      <OSVersion>WindowsServer2012</OSVersion>
    </AzureNodeTemplate>
  </AzureBurst>
</IaaSClusterConfig>
```

## <a name="troubleshooting"></a>Sorun giderme
* **"Sanal ağ yok" hatası** -hello betik toodeploy birden fazla küme Azure içinde eşzamanlı olarak bir abonelik altında çalıştırırsanız, bir veya daha fazla dağıtım hello hatasıyla başarısız olabilir "VNet *VNet\_adı* değil Mevcut".
  Bu hata oluşursa hello betiği başarısız hello dağıtım için yeniden çalıştırın.
* **Hello Azure sanal ağı ' hello Internet sorun erişme** - hello dağıtım komut dosyası kullanarak yeni bir etki alanı denetleyicisi ile bir küme oluşturun veya el ile bir baş düğüm VM toodomain denetleyicisini yükseltip, sorunlarla karşılaşabilirsiniz Merhaba VM'ler toohello Internet bağlanılıyor. Bu sorun bir iletici DNS sunucusu hello etki alanı denetleyicisi üzerinde otomatik olarak yapılandırılır ve bu iletici DNS sunucusu düzgün sorunu çözmezse ortaya çıkabilir.
  
    Bu soruna geçici bir çözüm toowork toohello etki alanı denetleyicisi ve her iki Kaldır hello ileticisi yapılandırma ayarı oturum veya geçerli iletici DNS sunucusunu yapılandırın. Bu ayar, Sunucu Yöneticisi'ni tıklatın tooconfigure **Araçları** >
    **DNS** tooopen DNS Yöneticisi'ni çift tıklayın ve ardından **İleticiler**.
* **RDMA ağ yoğun Vm'lerden erişirken sorun** - Windows Server işlem eklemek veya Aracısı düğümü bir RDMA özellikli kullanarak VM'ler boyut A8 veya A9 gibi bu sanal makineleri toohello RDMA uygulama ağ bağlantısı sorunları karşılaşabilirsiniz. Bu sorun bir toohello küme hello VM'ler eklendiğinde hello HpcVmDrivers uzantısı düzgün yüklenmemiş varsa nedenidir. Örneğin, uzantı durumu yükleme hello takılmış olabilir.
  
    toowork hello VM'ler hello uzantısında ilk onay hello durumunu bu soruna geçici bir çözüm. Merhaba uzantısı düzgün yüklenmemiş, hello düğümleri hello HPC kümesinden kaldırmayı deneyin ve hello düğümleri tekrar ekleyin. Örneğin, işlem düğümü VM'ler hello baş düğümünde hello Ekle HpcIaaSNode.ps1 komut dosyası çalıştırarak ekleyebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
* Bir test iş yükü hello kümede çalıştırmayı deneyin. HPC Pack Merhaba bir örnek için bkz: [Başlangıç Kılavuzu](https://technet.microsoft.com/library/jj884144).
* Eğitmen tooscript hello Küme dağıtımı ve HPC iş yükünü çalıştırmak için bkz: [Azure toorun Excel ve SOA iş yükleri bir HPC paketi küme kullanmaya başlama](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* HPC paketi araçları toostart deneyin, durdurmak, ekleyin ve oluşturduğunuz kümeden işlem düğümleri kaldırma. Bkz: [bir HPC Pack Yönet işlem düğümleri küme Azure'da](hpcpack-cluster-node-manage.md).
* toosubmit işleri toohello yerel bir bilgisayardan kümesi tooget bkz [bir şirket içi bilgisayar tooan HPC Pack işlerden gönderme HPC küme Azure'da](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

