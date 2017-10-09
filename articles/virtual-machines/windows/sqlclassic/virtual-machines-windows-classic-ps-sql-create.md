---
title: bir SQL Server sanal makinesi (Klasik) Azure PowerShell'de aaaCreate | Microsoft Docs
description: "Bir Azure VM ile SQL Server sanal makineye Galerisi görüntüleri oluşturmak için adımlar ve PowerShell komut dosyaları sağlar. Bu konuda hello Klasik dağıtım modunu kullanır."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: b73be387-9323-4e08-be53-6e5928e3786e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: b14d5d9bc192fa0a21126395ee20ffd06b3bf47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a>Azure PowerShell (Klasik) kullanarak bir SQL Server sanal makine sağlama

Bu makalede, nasıl toocreate kullanarak SQL Server sanal makine azure'da hello için PowerShell cmdlet'leri adımları sağlar.

> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

Merhaba Resource Manager sürümü bu konu için bkz: [Azure PowerShell Kaynak Yöneticisi'ni kullanarak bir SQL Server sanal makine sağlama](../sql/virtual-machines-windows-ps-sql-create.md).

### <a name="install-and-configure-powershell"></a>PowerShell'i yükleme ve yapılandırma:
1. Bir Azure hesabınız yoksa, [Azure ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/)yi ziyaret edin.
2. [Merhaba en son Azure PowerShell komutlarını yükleyip](/powershell/azure/overview).
3. Windows PowerShell'i başlatın ve tooyour Azure aboneliği ile Merhaba bağlamak **Add-AzureAccount** komutu.

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a>Azure bölgesi hedef belirleme

SQL Server sanal makineniz, belirli bir Azure bölgesinde bulunan bir bulut hizmetinde barındırılan. Merhaba aşağıdaki adımlar, toodetermine bölgeye, depolama hesabı ve hello öğretici hello kalanı için kullanılacak bulut hizmeti yardımcı olur.

1. SQL Server VM'nize toouse toohost istediğiniz hello veri merkezini belirler. PowerShell komutunu aşağıdaki hello kullanılabilir bölge adlarının bir listesini görüntüler.

   ```powershell
   (Get-AzureLocation).Name
   ```

2. Tercih edilen konumunuz tanımladıktan sonra adlı bir değişken ayarlamak **$dcLocation** toothat bölge. Örneğin, aşağıdaki komut kümelerini hello bölge çok hello "Doğu ABD":

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a>Abonelik ve depolama hesabınızı ayarlama

1. Merhaba hello yeni sanal makine için kullanacağınız Azure aboneliği belirler.

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. Hedef Azure aboneliği toohello Ata **$subscr** değişkeni. Sonra geçerli bir Azure aboneliğinizin ayarlayın.

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. Var olan depolama hesapları için denetleyin. Merhaba aşağıdaki betiği seçilen bölgenizde mevcut tüm depolama hesapları görüntüler:

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > İlk yeni bir depolama hesabı gerekiyorsa, bir küçük tüm depolama hesabı adı aşağıdaki örneğine hello olduğu gibi hello yeni AzureStorageAccount komutuyla oluşturun:`New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`

4. Merhaba hedef depolama hesabı adı toohello Ata **$staccount**. Ardından **Set-AzureSubscription** tooset hello aboneliği ve geçerli depolama hesabı.

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a>Bir SQL Server sanal makine görüntüsü seçin

1. Kullanılabilir SQL Server sanal makine görüntüleri hello galerisinden hello listesi öğrenin. Tüm bu görüntüleri bir **ImageFamily** "SQL" ile başlayan özelliği. Merhaba aşağıdaki SQL Server'ın önceden yüklü görüntüler hello görüntü ailesi kullanılabilir tooyou sorgu.

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. Merhaba sanal makine görüntüsü ailesi bulduğunuzda, bu ailesinde birden fazla yayımlanan görüntü olabilir. Kullanım hello aşağıdaki betiği toofind hello son yayımlanan için sanal makine görüntü adı seçilen görüntü ailenize (gibi **Windows Server 2012 R2'de SQL Server 2016 RTM Enterprise**):

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-hello-virtual-machine"></a>Merhaba sanal makine oluşturma

Son olarak, PowerShell ile Merhaba sanal makine oluşturun:

1. Bir bulut oluşturmak hizmet toohost hello yeni VM. Bu da olası toouse var olan bir bulut hizmetini yerine olduğuna dikkat edin. Yeni bir değişken oluşturmak **$svcname** hello bulut hizmeti hello kısa adı.

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. Merhaba sanal makine adı ve bir boyut belirtin. Sanal makine boyutları hakkında daha fazla bilgi için bkz: [Azure için sanal makine boyutlarını](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see hello link toohello other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. Merhaba yerel yönetici hesabı ve parolası belirtin.

   ```powershell
   $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. Komut dosyası toocreate hello sanal makine aşağıdaki hello çalıştırın.

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> Merhaba ek açıklama ve yapılandırma seçenekleri için bkz **komut kümesini yapı** bölümüne [kullanım Azure PowerShell toocreate ve Windows tabanlı sanal makineleri önceden](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="example-powershell-script"></a>Örnek PowerShell komut dosyası

Merhaba aşağıdaki komut dosyası sağlar oluşturur tam bir komut dosyası örneği bir **Windows Server 2012 R2'de SQL Server 2016 RTM Enterprise** sanal makine. Bu komut dosyası kullanırsanız, bu konunun önceki adımlarda hello göre hello ilk değişkenlerini özelleştirmeniz gerekir.

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set hello current subscription and storage account
# Comment out hello New-AzureStorageAccount line if hello account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select hello most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create hello new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create hello VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create hello SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a>İle Uzak Masaüstü Bağlantısı

1. Merhaba RDP dosyalarını hello geçerli kullanıcının belgenin klasör toolaunch bu sanal makineleri toocomplete Kurulum oluşturun:

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. Merhaba belgeleri dizininde hello RDP dosyasını çalıştırın. Merhaba yönetici kullanıcı adı ve parola daha önce sağlanan bağlantı (örneğin, kullanıcı adınızı VMAdmin olduysa, "\VMAdmin" Merhaba kullanıcı belirtin ve hello parola).

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-hello-configuration-of-hello-sql-server-machine-for-remote-access"></a>Uzaktan erişim için SQL Server makinesinde hello tam hello yapılandırması

Toohello makinede Uzak Masaüstü ile oturum sonra SQL Server'ın hello yönergelere göre yapılandırma [bir Azure VM'de SQL Server bağlantısı yapılandırma adımları](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).

## <a name="next-steps"></a>Sonraki adımlar

Hello PowerShell ile sanal makinelerin sağlamaya yönelik ek yönergeler bulabilirsiniz [virtual machines belgeleri](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Çoğu durumda, hello sonraki toomigrate adımdır veritabanları toothis yeni SQL Server VM. Veritabanı geçiş yönergeleri için bkz [veritabanı tooSQL bir Azure VM sunucuda geçiş](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).

Ayrıca hello Azure portal toocreate SQL sanal makineleri kullanmak istiyorsanız bkz [Azure üzerinde bir SQL Server sanal makine sağlama](../sql/virtual-machines-windows-portal-sql-server-provision.md). Merhaba portal size kullanarak VM'ler oluşturur yetenekte hello Klasik modeli bu PowerShell konuda kullanılan yerine önerilen Resource Manager modeli hello bu hello öğretici unutmayın.

Ayrıca toothese kaynakları gözden geçirmenizi öneririz [toorunning Azure Virtual Machines'de SQL Server ilgili diğer konular](../sql/virtual-machines-windows-sql-server-iaas-overview.md).
