---
title: "aaaInstall eğilim mikro derin güvenlik bir VM'de | Microsoft Docs"
description: "Bu makalede nasıl tooinstall ve eğilim mikro güvenlik Azure hello Klasik dağıtım modelinde oluşturulan VM yapılandırın."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e991b635-f1e2-483f-b7ca-9d53e7c22e2a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: iainfou
ms.openlocfilehash: dc5492db07a37a2296df5da673183a14c6d5b1f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a>Nasıl tooinstall ve bir Windows VM bir hizmet olarak eğilimi mikro derin güvenliği yapılandırma
> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

Bu makale size nasıl gösterir tooinstall ve eğilim mikro derin güvenlik bir yeni veya var olan Windows Server çalıştıran sanal makine (VM) bir hizmet olarak yapılandırın. Bir hizmet olarak derin güvenlik kötü amaçlı yazılımdan koruma, bir güvenlik duvarı, bir yetkisiz erişim önleme sisteminin ve bütünlüğü izleme içerir.

Merhaba istemcisi bir güvenlik uzantısı hello VM Aracısı aracılığıyla olarak yüklenir. Yeni bir sanal makine üzerinde VM Aracısı'hello Azure portal tarafından otomatik olarak oluşturulan hello olarak hello derin güvenlik aracısı yükleyin.

Mevcut bir VM'yi Hello Klasik portal, hello Azure CLI veya PowerShell kullanılarak oluşturulan VM Aracısı sahip olmayabilir. Merhaba VM aracısı yüklü olmayan mevcut sanal makineyi için toodownload gerekir ve ilk yükleyin. Bu makalede her iki durumlarda kapsar.

Geçerli bir eğilim mikro abonelikten bir şirket içi çözüm varsa, kullanabilirsiniz toohelp Azure sanal makinelerinizi koruma. Bir müşteri henüz değilseniz, deneme aboneliği için kaydolabilirsiniz. Bu çözüm hakkında daha fazla bilgi için bkz: hello eğilimi mikro blog gönderisi [Microsoft Azure VM Aracısı uzantısı için ayrıntılı güvenlik](http://go.microsoft.com/fwlink/p/?LinkId=403945).

## <a name="install-hello-deep-security-agent-on-a-new-vm"></a>Merhaba derin güvenlik aracısı yeni bir VM'e yükleyin

Merhaba [Azure portal](http://portal.azure.com) , hello görüntüden kullandığınızda hello eğilimi mikro güvenlik uzantısı yüklemenize olanak tanıyan **Market** toocreate hello sanal makine. Tek bir sanal makine oluşturuyorsanız, hello portal eğilimi mikro kolay bir yolu tooadd korumadan kullanmaktır.

Bir giriş hello kullanarak **Market** yardımcı olan bir Sihirbazı'nı Ayarla hello sanal makineyi açar. Merhaba kullandığınız **ayarları** dikey penceresinde, hello üçüncü Pano hello sihirbazının tooinstall hello eğilimi mikro güvenlik uzantısı.  Genel yönergeler için bkz: [Windows hello Azure portalı çalıştıran bir sanal makine oluşturma](tutorial.md).

Toohello ulaştıklarında **ayarları** dikey penceresinde hello Sihirbazı, adımları hello:

1. Tıklatın **uzantıları**, ardından **uzantısı Ekle** hello sonraki bölmesinde.

   ![Merhaba uzantı eklemeye başlayın][1]

2. Seçin **derin güvenlik aracısı** hello içinde **yeni kaynak** bölmesi. Merhaba derin güvenlik aracısı bölmesinde **oluşturma**.

   ![Derin güvenlik aracısı tanımlama][2]

3. Merhaba girin **Kiracı tanımlayıcı** ve **Kiracı etkinleştirme parola** hello uzantısı. İsteğe bağlı olarak, girebilirsiniz bir **güvenlik ilkesi tanımlayıcısı**. Ardından **Tamam** tooadd hello istemci.

   ![Uzantı ayrıntılarını sağlayın][3]

## <a name="install-hello-deep-security-agent-on-an-existing-vm"></a>Var olan bir VM Hello derin güvenlik Aracısı yükleme
Mevcut bir VM'yi tooinstall hello aracısını, aşağıdaki öğelerindeki hello gerekir:

* Hello Azure PowerShell modülü, sürüm 0.8.2 veya daha yeni, yerel bilgisayarınızda yüklü. Hello kullanarak yüklediyseniz Azure PowerShell hello sürümü kontrol edebilirsiniz **Get-Module azure | Tablo Biçimlendir sürüm** komutu. Yönergeler ve bir bağlantı toohello en son sürüm için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview). Azure aboneliği tooyour kullanarak oturum `Add-AzureAccount`.
* Merhaba VM Aracısı hello hedef sanal makinede yüklü.

İlk olarak, VM aracısının yüklü olduğundan bu hello doğrulayın. Merhaba bulut hizmeti adı ve sanal makine adı girin ve ardından komutlar bir yönetici düzeyi Azure PowerShell komut isteminde aşağıdaki hello çalıştırın. Merhaba < ve > karakterleri dahil olmak üzere hello tırnak içindeki her şeyi değiştirin.

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

Merhaba bulut hizmeti ve sanal makine adını bilmiyorsanız, çalıştırmak **Get-AzureVM** bilgiyi tüm geçerli aboneliğinizde sanal makineler hello toodisplay.

Merhaba, **write-host** komutu döndürür **doğru**, VM aracısının yüklü hello. Döndürürse **False**, hello yönergeler ve hello Azure blog gönderisi indirme bağlantısı toohello bkz [VM aracısı ve uzantılar - 2. parça](http://go.microsoft.com/fwlink/p/?LinkId=403947).

Merhaba VM Aracısı yüklüyse, bu komutları çalıştırın.

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a>Sonraki adımlar
Merhaba Aracısı toostart yüklendiğinde çalıştıran birkaç dakika sürer. Derin bir güvenlik yöneticisi tarafından yönetilecek şekilde bundan sonra hello sanal makine üzerinde derin güvenlik tooactivate gerekir. Merhaba makaleler ek yönergeler için bkz:

* Bu çözümle ilgili eğilim'ın makale [Instant-On Cloud Security Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)
* A [örnek Windows PowerShell komut dosyası](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure hello sanal makine
* [Yönergeler](http://go.microsoft.com/fwlink/?LinkId=404099) hello örnek

## <a name="additional-resources"></a>Ek kaynaklar
[Nasıl tooa sanal makineye Windows Server çalıştıran toolog]

[Azure VM uzantıları ve özellikleri]

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
[Nasıl tooa sanal makineye Windows Server çalıştıran toolog]:connect-logon.md
[Azure VM uzantıları ve özellikleri]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409
