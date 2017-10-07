---
title: "aaaDesired durum yapılandırması Azure genel bakış | Microsoft Docs"
description: "PowerShell istenen durum yapılandırması için hello Microsoft Azure uzantısı işleyici kullanarak genel bakış. Önkoşullar, mimari, cmdlet'leri dahil olmak üzere..."
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: bbacbc93-1e7b-4611-a3ec-e3320641f9ba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 01/09/2017
ms.author: zachal
ms.openlocfilehash: b0337a2f1124f35e5e40c1478bd7530427e59d44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-desired-state-configuration-extension-handler"></a>Giriş toohello Azure istenen durum yapılandırması uzantısı işleyicisi
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Hello Azure VM aracısı ve ilişkili uzantıları hello Microsoft Azure altyapı hizmetleri parçasıdır. VM uzantıları hello VM işlevlerini genişletmek ve çeşitli VM yönetim işlemlerini basitleştirmek yazılım bileşenleridir. Örneğin, hello VMAccess uzantısını kullanılan tooreset yöneticinin parola bulunabilir, veya özel komut dosyası hello uzantısı kullanılan tooexecute hello VM üzerinde bir komut dosyası olabilir.

Bu makalede hello PowerShell istenen durum yapılandırması (DSC) uzantısı hello Azure PowerShell SDK'ın bir parçası olarak Azure VM'ler için tanıtılır. Yeni cmdlet'leri tooupload ve PowerShell DSC yapılandırması hello PowerShell DSC uzantısı ile etkin bir Azure VM uygulamak kullanabilirsiniz. Merhaba PowerShell DSC uzantısı çağrılarının PowerShell DSC tooenact hello içine hello VM DSC yapılandırmasını aldı. Bu işlevsellik, hello Azure portal da kullanılabilir.

## <a name="prerequisites"></a>Ön koşullar
**Yerel makine** toointeract ile Merhaba Azure VM uzantısı, Azure PowerShell SDK hello veya her iki hello Azure portal toouse gerekir. 

**Konuk Aracısı** hello hello DSC yapılandırması tarafından yapılandırılan bir Azure VM toobe Windows Management Framework (WMF) 4.0 veya 5.0 destekleyen bir işletim sistemi gerekir. Merhaba tam desteklenen işletim sistemi sürümlerinin listesi hello bulunabilir [DSC uzantısı sürüm geçmişi](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).

## <a name="terms-and-concepts"></a>Terimleri ve kavramları
Bu kılavuz kavramları aşağıdaki hello bilindiğini varsayar:

Yapılandırma - DSC yapılandırma belgesi. 

Düğümü - DSC yapılandırması için hedef. Bu belgede "düğümü" her zaman tooan Azure VM ifade eder.

Yapılandırma verilerini - bir .psd1 dosya ortam verileri içeren bir yapılandırma için

## <a name="architectural-overview"></a>Mimari genel bakış
hello Azure VM Aracısı framework toodeliver Hello Azure DSC uzantısı kullanır, yürürlüğe ve DSC yapılandırmaları Azure Vm'lerinde çalıştırılan hakkında rapor oluşturun. Azure portal parametreleri kümesini hello Azure PowerShell SDK veya hello aracılığıyla sağlanan ve Hello DSC uzantısı en az bir yapılandırma belgesini içeren bir .zip dosyası bekler.

Merhaba uzantısı hello için ilk kez çağrıldığında, bir yükleme işlemi çalıştırır. Bu işlem mantığı aşağıdaki hello kullanarak hello Windows Management Framework (WMF) sürümünü yükler:

1. Hello Azure VM işletim sistemi Windows Server 2016 ise, hiçbir işlem yapılmadı. Windows Server 2016 yüklü PowerShell'in en son sürümünü hello zaten var.
2. Merhaba, `wmfVersion` özelliği belirtildi, hello VM'in işletim sistemiyle uyumlu olmadığı sürece bu hello WMF sürümü yüklenir.
3. Öyle değilse `wmfVersion` özelliği belirtildi, hello son geçerli sürümü hello WMF yüklendi.

Merhaba WMF yeniden başlatma gerektirir. Yeniden başlatmanın ardından hello uzantısı hello belirtilen hello .zip dosyası indirir `modulesUrl` özelliği. Bu konum Azure blob depolama alanına ise, bir SAS belirteci hello belirtilebilir `sasToken` özelliği tooaccess hello dosya. Merhaba .zip indirilir ve açılmış sonra tanımlanan yapılandırması işlevi hello `configurationFunction` toogenerate hello MOF dosyasını çalıştırın. Merhaba uzantısı sonra çalışır `Start-DscConfiguration -Force` üzerinde oluşturulan hello MOF dosyası. Merhaba uzantısı çıkış yakalar ve geri toohello Azure durum kanal yazar. Üzerinde hello bu noktasından DSC LCM'yi izleme ve düzeltme normal olarak işler. 

## <a name="powershell-cmdlets"></a>PowerShell cmdlet'leri
PowerShell cmdlet'leri Azure Resource Manager ile kullanılabilir veya Klasik dağıtım modeli toopackage Merhaba, yayımlama ve DSC uzantısı dağıtımlarını izleme. Merhaba listelenen aşağıdaki cmdlet'leri hello Klasik dağıtım modülleri olsa da, "Azure" "AzureRm" toouse hello Azure Resource Manager modeli ile değiştirilebilir. Örneğin, `Publish-AzureVMDscConfiguration` kullanır hello Klasik dağıtım modeli, burada `Publish-AzureRmVMDscConfiguration` Azure Kaynak Yöneticisi'ni kullanır. 

`Publish-AzureVMDscConfiguration`bir yapılandırma dosyasında alır, bağımlı DSC kaynakları için tarar ve hello yapılandırması ve DSC kaynakları gerekli tooenact hello yapılandırması içeren bir .zip dosyası oluşturur. Hello kullanarak yerel olarak hello paketi oluşturabilirsiniz `-ConfigurationArchivePath` parametresi. Aksi takdirde hello .zip dosyası tooAzure blob depolama yayımlar ve bir SAS belirteci ile güvenliğini sağlar.

Bu cmdlet ile oluşturulan hello .zip dosyası hello hello arşiv klasörü kökünde hello .ps1 yapılandırma komut dosyası vardır. Kaynaklar hello arşiv klasöre yerleştirilen hello modülü klasörünü sahiptir. 

`Set-AzureVMDscExtension`bir VM yapılandırması nesnesine Hello PowerShell DSC uzantısı tarafından gerekli hello ayarları yerleştirir. Merhaba Klasik dağıtım modelinde hello VM değişiklikleri uygulanan tooan Azure VM olmalıdır ile `Update-AzureVM`. 

`Get-AzureVMDscExtension`belirli bir VM'nin Hello DSC uzantı durumunu alır. 

`Get-AzureVMDscExtensionStatus`Merhaba DSC uzantısı işleyici tarafından kamulaştırılmış hello DSC yapılandırması Hello durumunu alır. Bu eylem, bir tek VM veya grup Vm'lere üzerinde gerçekleştirilebilir.

`Remove-AzureVMDscExtension`Merhaba uzantısı işleyici belirli bir sanal makineden kaldırır. Bu cmdlet mu **değil** hello yapılandırmasını kaldırmak, hello WMF kaldırma veya hello sanal makine uygulanan hello ayarlarını değiştirin. Yalnızca hello uzantısı işleyici de kaldırır. 

**ASM ve Azure Resource Manager cmdlet'lerini temel farklılıkları**

* Azure Resource Manager cmdlet'lerini zaman uyumlu. ASM cmdlet'leri zaman uyumsuzdur.
* ResourceGroupName, VMName, ArchiveStorageAccountName, sürüm ve konum tüm gerekli Azure Kaynak Yöneticisi'nde parametreleridir.
* ArchiveResourceGroupName yeni bir isteğe bağlı parametre için Azure Resource Manager ' dir. Merhaba sanal makinenin oluşturulduğu tooa farklı kaynak hello bir gruptan depolama hesabınıza ait olduğunda, bu parametre belirtebilirsiniz.
* Azure Kaynak Yöneticisi'nde ArchiveBlobName ConfigurationArchive çağrılır
* Kapsayıcı adı Azure Kaynak Yöneticisi'nde ArchiveContainerName çağrılır
* Azure Kaynak Yöneticisi'nde ArchiveStorageEndpointSuffix StorageEndpointSuffix çağrılır
* Merhaba otomatik güncelleştirme anahtar tooAzure Resource Manager tooenable otomatik hello uzantısı işleyici toohello en son sürüm olarak ve kullanılabilir olduğunda güncelleştirme eklendi. Bu parametre hello olası toocause sahip Not VM WMF yayımlanan hello yeni bir sürümü olduğunda hello üzerinde yeniden başlatır. 

## <a name="azure-portal-functionality"></a>Azure portal işlevi
Tooa VM göz atın. Ayarlar altında "Uzantıları." Genel tıklatın -> Yeni bir bölme oluşturulur. "Ekle"'yi tıklatın ve PowerShell DSC seçin.

Merhaba portal giriş gerekir.
**Yapılandırma modülleri veya komut dosyası**: Bu alan zorunludur. Bir yapılandırma betiğini içeren bir .ps1 dosyası ya da bir .ps1 yapılandırma betiğini hello kökündeki ve hello .zip içinde modülü klasörlerdeki tüm bağımlı kaynaklarla bir .zip dosyası gerektirir. Merhaba ile oluşturulan `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` hello Azure PowerShell SDK'sını dahil cmdlet'i. Merhaba .zip dosyası tarafından bir SAS belirteci güvenli, kullanıcı blob depolama alanına yüklenir. 

**Yapılandırma verileri PSD1 dosyası**: Bu alan isteğe bağlıdır. Yapılandırmanızı .psd1 yapılandırma veri dosyası gerektiriyorsa, bu alan tooselect kullanın ve tooyour kullanıcı blob depolama burada onu güvenli bir SAS belirteci tarafından karşıya yükleyin. 

**Yapılandırma, modül adı**: .ps1 dosyaları birden çok yapılandırma işlevleri sahip olabilir. Ardından hello yapılandırma .ps1 betiği Hello adını girin bir '\' ve hello yapılandırma işlevinin hello adı. Örneğin, hello adı "configuration.ps1".ps1 komut dosyanız varsa ve "IisInstall" Merhaba yapılandırmadır girersiniz:`configuration.ps1\IisInstall`

**Yapılandırma değişkenleri**: hello yapılandırma işlevi bağımsız değişken alıyorsa, bunları burada hello biçiminde girin `argumentName1=value1,argumentName2=value2`. Bu biçim PowerShell cmdlet'lerini veya Resource Manager şablonları ile yapılandırma bağımsız değişkenleri nasıl kabul daha farklı bir biçim olduğuna dikkat edin. 

## <a name="getting-started"></a>Başlarken
Hello Azure DSC uzantısı DSC yapılandırma belgelerde alır ve Azure Vm'lerinde enacts. Bir yapılandırma basit bir örnek aşağıda verilmiştir. Yerel olarak, "IisInstall.ps1" kaydedin:

```powershell
configuration IISInstall 
{ 
    node "localhost"
    { 
        WindowsFeature IIS 
        { 
            Ensure = "Present" 
            Name = "Web-Server"                       
        } 
    } 
}
```

VM üzerinde hello adımları yer hello IisInstall.ps1 komut dosyası izleyen hello belirtilen, hello yapılandırma yürütün ve geri durumu rapor.
###<a name="classic-model"></a>Klasik modeli
```powershell
#Azure PowerShell cmdlets are required
Import-Module Azure

#Use an existing Azure Virtual Machine, 'DscDemo1'
$demoVM = Get-AzureVM DscDemo1

#Publish hello configuration script into user storage.
Publish-AzureVMDscConfiguration -ConfigurationPath ".\IisInstall.ps1" -StorageContext $storageContext -Verbose -Force

#Set hello VM toorun hello DSC configuration
Set-AzureVMDscExtension -VM $demoVM -ConfigurationArchive "IisInstall.ps1.zip" -StorageContext $storageContext -ConfigurationName "IisInstall" -Verbose

#Update hello configuration of an Azure Virtual Machine
$demoVM | Update-AzureVM -Verbose

#check on status
Get-AzureVMDscExtensionStatus -VM $demovm -Verbose
```
###<a name="azure-resource-manager-model"></a>Azure Resource Manager modeli

```powershell
$resourceGroup = "dscVmDemo"
$location = "westus"
$vmName = "myVM"
$storageName = "demostorage"
#Publish hello configuration script into user storage
Publish-AzureRmVMDscConfiguration -ConfigurationPath .\iisInstall.ps1 -ResourceGroupName $resourceGroup -StorageAccountName $storageName -force
#Set hello VM toorun hello DSC configuration
Set-AzureRmVmDscExtension -Version 2.21 -ResourceGroupName $resourceGroup -VMName $vmName -ArchiveStorageAccountName $storageName -ArchiveBlobName iisInstall.ps1.zip -AutoUpdate:$true -ConfigurationName "IISInstall"

```

## <a name="logging"></a>Günlüğe kaydetme
Günlükleri yerleştirilir:

C:\WindowsAzure\Logs\Plugins\Microsoft.PowerShell.DSC\[sürüm numarası]

## <a name="next-steps"></a>Sonraki adımlar
PowerShell DSC hakkında daha fazla bilgi için [hello PowerShell Belge Merkezi ziyaret](https://msdn.microsoft.com/powershell/dsc/overview). 

Merhaba inceleyin [hello DSC uzantısı için Azure Resource Manager şablonu](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

PowerShell DSC ile yönetebileceğiniz toofind işlevsellikler [hello PowerShell Galerisi Gözat](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) daha fazla DSC kaynakları için.

Yapılandırmaları hassas parametreleri geçirme hakkında daha fazla bilgi için bkz: [yönetmek hello DSC uzantısı işleyici ile güvenli kimlik bilgileri](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

