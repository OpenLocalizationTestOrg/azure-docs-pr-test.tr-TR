---
title: PowerShell ile bir Windows VM aaaCreate | Microsoft Docs
description: "Azure PowerShell ve hello Klasik dağıtım modeli kullanarak Windows sanal makine oluşturun."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 42c0d4be-573c-45d1-b9b0-9327537702f7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 5339f458c1f08f6e1752a53191f19402fab8ea25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-hello-classic-deployment-model"></a>PowerShell ve hello Klasik dağıtım modeliyle bir Windows sanal makine oluşturma
> [!div class="op_single_selector"]
> * [Azure portal - Windows](tutorial.md)
> * [PowerShell - Windows](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Nasıl çok öğrenin[hello Resource Manager modelini kullanarak bu adımları uygulamadan](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Bu adımlar nasıl toocustomize Azure PowerShell kümesi oluşturmak ve bir yapı bloğu yaklaşımını kullanarak Windows tabanlı bir Azure sanal makine önceden komutları gösterir. Bu işlem kullanabilirsiniz tooquickly yeni bir Windows tabanlı sanal makine için bir komut kümesi oluşturun ve var olan bir dağıtıma genişletin veya birden çok komut ayarlar, hızlı bir şekilde toocreate yapı bir özel geliştirme ve test veya BT Uzmanı ortamı.

Bir doldurma-arada boşlukları yaklaşım Azure PowerShell komut kümelerini oluşturmak için aşağıdaki adımları izleyin. Bu yaklaşım, yeni tooPowerShell olan veya yalnızca tooknow hangi değerleri toospecify başarılı yapılandırmasını istiyorsanız yararlı olabilir. Gelişmiş PowerShell kullanıcıları hello komutları alabilir ve hello değişkenleri ("$" ile başlayan hello satırlar) için kendi değerlerinizi yerleştirin.

Henüz yapmadıysanız, hello yönergeleri kullanın [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) , yerel bilgisayarınızda Azure PowerShell tooinstall. Sonra bir Windows PowerShell komut istemi açın.

## <a name="step-1-add-your-account"></a>1. adım: hesabınızı ekleme
1. Merhaba PowerShell isteminde **Add-AzureAccount** tıklatıp **Enter**. 
2. Azure aboneliğinizle ilişkili hello e-posta adresini yazın ve tıklatın **devam**. 
3. Merhaba hesabınızın parolasını yazın. 
4. Tıklatın **oturum**.

## <a name="step-2-set-your-subscription-and-storage-account"></a>2. adım: aboneliğiniz ve depolama hesabı ayarlama
Azure aboneliği ve depolama hesabı hello Windows PowerShell komut isteminde şu komutları çalıştırarak ayarlayın. Merhaba < ve > karakterleri dahil olmak üzere hello tırnak içindeki her şeyi hello doğru adlarıyla değiştirin.

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

Merhaba hello çıktısını varlığıyla SubscriptionName özelliği hello hello doğru abonelik adı alabilirsiniz **Get-AzureSubscription** komutu. Merhaba hello çıktısını Label özelliğinin hello hello doğru depolama hesabı adı alabilirsiniz **Get-AzureStorageAccount** hello çalıştırdıktan sonra komut **Select-AzureSubscription** komutu.

## <a name="step-3-determine-hello-imagefamily"></a>3. adım: Merhaba ImageFamily belirleme
Ardından, toodetermine hello ImageFamily veya etiket değeri hello belirli görüntü karşılık gelen toohello için toocreate istediğiniz Azure sanal makine gerekir. Bu komut kullanılabilir ImageFamily değerlerle hello listesini elde edebilirsiniz.

    Get-AzureVMImage | select ImageFamily -Unique

Windows tabanlı bilgisayarlar için ImageFamily değeri bazı örnekleri şunlardır:

* Windows Server 2012 R2 Datacenter
* Windows Server 2008 R2 SP1
* Windows Server 2016 Technical Preview 4
* Windows Server 2012'de SQL Server 2012 SP1 Enterprise

Aradığınız hello görüntü bulursanız, hello metin düzenleyici seçim veya hello PowerShell Tümleşik komut dosyası ortamı (ISE) yeni bir örneğini açın. Merhaba aşağıdaki hello yeni metin dosyası veya hello hello ImageFamily değerini değiştirerek PowerShell ISE kopyalayın.

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

Bazı durumlarda, hello etiket özelliği hello ImageFamily değeri yerine hello görüntü adı kullanılıyor. Merhaba ImageFamily özelliğini kullanarak aradığınız hello görüntü bulamadıysanız, bu komutla kendi etiket özelliği tarafından hello yansımaları listeler.

    Get-AzureVMImage | select Label -Unique

Bu komutla hello sağ görüntü bulursanız, seçim veya hello PowerShell ISE hello metin düzenleyicisi yeni bir örneğini açın. Merhaba aşağıdaki hello yeni metin dosyası veya hello hello etiket değeri değiştirerek PowerShell ISE kopyalayın.

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a>4. adım: komut kümesi oluşturma
Kümesi, yeni bir metin dosyası veya hello işe hello değişken değerleri doldurma ve merhaba < ve > karakterleri kaldırma içine hello uygun blokları kümesi kopyalama komutunuzu Hello kalan oluşturun. Merhaba iki bkz [örnekler](#examples) hello hello son sonucunun hakkında bir fikir için bu makalenin sonunda.

(Gerekli) bu iki komut blokları birini seçerek, komutunu başlatın.

Seçenek 1: bir sanal makine adı ve bir boyut belirtin.

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

Seçenek 2: bir ad, boyutu ve kullanılabilirlik kümesi adı belirtin.

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

D, DS veya G-serisi sanal makineler için Hello InstanceSize değerleri için bkz: [sanal makine ve bulut hizmeti boyutları Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).

> [!NOTE]
> Bir Kuruluş Sözleşmesi Yazılım Güvencesi ile varsa ve Windows Server hello tootake avantajlarından düşündüğünüz [karma kullanımı avantajı](https://azure.microsoft.com/pricing/hybrid-use-benefit/), ekleme **- LicenseType değeri** parametresi toohello  **AzureVMConfig yeni** hello değere geçirme cmdlet'ini **Windows_Server** hello tipik kullanım örneği.  Görüntüyü karşıya yüklediğiniz kullandığınızdan emin olun; Merhaba galeri standart bir görüntüden hello karma kullanma avantajı ile kullanamazsınız.
> 
> 

İsteğe bağlı olarak, bir tek başına Windows bilgisayar için hello yerel yönetici hesabı ve parolası belirtin.

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

Güçlü bir parola seçin. toocheck kendi gücü bkz [parola denetleyicisi: güçlü parolalar kullanarak](https://www.microsoft.com/security/pc-security/password-checker.aspx).

İsteğe bağlı olarak, tooadd hello Windows bilgisayar tooan var olan Active Directory etki alanı, hello yerel yönetici hesabı ve parola, hello etki alanı ve hello adı ve etki alanı hesabının parolasını belirtin.

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="<FQDN of hello domain that hello machine is joining>"
    $domacctdomain="<domain of hello account that has permission tooadd hello machine toohello domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

Merhaba sözdizimi hello için Windows tabanlı sanal makinelere ilişkin ek öncesi yapılandırma seçenekleri için bkz **Windows** ve **WindowsDomain** parametre kümelerine [ Ekleme AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).

İsteğe bağlı olarak, sanal makine hello statik DIP bilinen belirli bir IP adresi atayın.

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

Belirli bir IP adresi ile kullanılabilir olduğunu doğrulayabilirsiniz:

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

İsteğe bağlı olarak, bir Azure sanal ağında hello sanal makine tooa belirli alt atayın.

    $vm1 | Set-AzureSubnet -SubnetNames "<name of hello subnet>"

İsteğe bağlı olarak, tek bir veri diski toohello sanal makine ekleyin.

    $disksize=<size of hello disk in GB>
    $disklabel="<hello label on hello disk>"
    $lun=<Logical Unit Number (LUN) of hello disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

Bir Active Directory etki alanı denetleyicisi için $hcaching çok ayarlamak "None".

İsteğe bağlı olarak hello sanal makine tooan varolan yük dengeli kümesi için dış trafiğin ekleyin.

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of hello internal port>
    $pubport=<port number of hello external port>
    $endpointname="<name of hello endpoint>"
    $lbsetname="<name of hello existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

Son olarak, hello sanal makine oluşturmak için bu gerekli komutu blokları birini seçin.

Seçenek 1: var olan bir bulut hizmetinde hello sanal makine oluşturun.

    New-AzureVM –ServiceName "<short name of hello cloud service>" -VMs $vm1

Merhaba kısa hello bulut hizmeti adını hello bulut hizmetlerinin listesi hello Azure portal veya Merhaba, kaynak grupları listesinde hello Azure portalında görünür hello adıdır.

Seçenek 2: hello sanal makineyi bir bulut hizmetini ve sanal ağ oluşturun.

    $svcname="<short name of hello cloud service>"
    $vnetname="<name of hello virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a>5. adım: komut kümesini çalıştırın
Metin Düzenleyicisi'nde oluşturulan hello Azure PowerShell komut kümesini gözden geçirin veya birden çok adım 4 komutlarından bloklarını oluşan PowerShell ISE hello. Tüm gerekli hello değişkenleri belirttiniz ve hello doğru değerlerin olduğundan emin olun. Ayrıca tüm merhaba < ve > karakterleri kaldırdığınız emin olun.

Bir metin düzenleyicisi kullanıyorsanız, copy hello komutu toohello Pano ayarlayın ve, Windows PowerShell komut istemini açın sağ tıklayın. Bu PowerShell komutlarını bir dizi olarak hello komut kümesini vermek ve Azure sanal makine oluşturun. Alternatif olarak, hello PowerShell ISE set hello komutunu çalıştırın.

Bu sanal makineyi yeniden veya benzer bir oluşturacaksanız, şunları yapabilirsiniz:

* Bu komut bir PowerShell komut dosyası (*.ps1) ayarlanmış kaydedin.
* Farklı Kaydet hello bir Azure Otomasyonu runbook olarak ayarla bu komutu **Automation hesapları** hello Azure portalı bölümü.

## <a id="examples"></a>Örnekler
Aşağıda, Windows tabanlı Azure sanal makineler oluşturma toobuild Azure PowerShell komut kümelerini yukarıdaki hello adımları kullanarak, iki örnek verilmiştir.

### <a name="example-1"></a>Örnek 1
Bir PowerShell gereksinim toocreate hello ilk sanal makine bir Active Directory etki alanı denetleyicisi için komut kümesinin:

* Merhaba Windows Server 2012 R2 Datacenter görüntüsü kullanır.
* Merhaba adı AZDC1 vardır.
* Bir tek başına bilgisayardır.
* Bir ek veri diski 20 GB sahiptir.
* Merhaba statik IP adresi 192.168.244.4 vardır.
* Merhaba AZDatacenter sanal ağın Hello arka uç alt ağda değil.
* Hello Azure TailspinToys bulut hizmetidir.

Okunabilirlik için her bloğu arasında boş satırlar ile bu sanal makine hello karşılık gelen Azure PowerShell komut kümesini toocreate aşağıdadır.

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

    $vm1 | Set-AzureSubnet -SubnetNames "BackEnd"

    $vm1 | Set-AzureStaticVNetIP -IPAddress 192.168.244.4

    $disksize=20
    $disklabel="DCData"
    $lun=0
    $hcaching="None"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

### <a name="example-2"></a>Örnek 2
Bir PowerShell gereken komut kümesini toocreate bir sanal makine için bir iş sunucu:

* Merhaba Windows Server 2012 R2 Datacenter görüntüsü kullanır.
* Merhaba adı LOB1 vardır.
* Merhaba corp.contoso.com etki alanının bir üyesidir.
* Bir ek veri diski 200 GB sahiptir.
* Merhaba AZDatacenter sanal ağın Hello ön uç alt ağda değil.
* Hello Azure TailspinToys bulut hizmetidir.

Bu sanal makine hello karşılık gelen Azure PowerShell komut kümesini toocreate aşağıdadır.

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="corp.contoso.com"
    $domacctdomain="CORP"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "FrontEnd"

    $disksize=200
    $disklabel="LOBData"
    $lun=0
    $hcaching="ReadWrite"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname


## <a name="next-steps"></a>Sonraki adımlar
127 GB'den büyük bir işletim sistemi diski gerekiyorsa, yapabilecekleriniz [hello OS sürücüyü genişletin](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

