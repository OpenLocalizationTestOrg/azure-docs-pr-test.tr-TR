---
title: "Azure Active Directory etki alanı Hizmetleri: Yönetim Kılavuzu | Microsoft Docs"
description: "Azure PowerShell ve hello Klasik dağıtım modeli kullanarak bir Windows sanal makine tooa yönetilen etki alanına katılın."
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9143b843-7327-43c3-baab-6e24a18db25e
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 21bc5930d84c5368a120f9d81f09320e2a0168fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain-using-powershell"></a>PowerShell kullanarak bir Windows Server sanal makine tooa yönetilen etki alanına katılma
> [!div class="op_single_selector"]
> * [Klasik Azure portalı - Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell - Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır. Azure AD etki alanı Hizmetleri hello Resource Manager modeli şu anda desteklemiyor.
>
>

Bu adımlar nasıl toocustomize Azure PowerShell kümesi oluşturmak ve bir yapı bloğu yaklaşımını kullanarak Windows tabanlı bir Azure sanal makine önceden komutları gösterir. Bu adımları Windows tabanlı bir Azure sanal makine oluşturun ve tooan Azure AD etki alanı Hizmetleri yönetilen etki alanına katılması yardımcı olur.

Bir doldurma-arada boşlukları yaklaşım Azure PowerShell komut kümelerini oluşturmak için aşağıdaki adımları izleyin. Bu yaklaşım, yeni tooPowerShell olduğunuz veya başarılı bir yapılandırma için hangi değerlerin toospecify tooknow istiyorsanız yararlı olabilir. Gelişmiş PowerShell kullanıcıları hello komutları alabilir ve hello değişkenleri ("$" ile başlayan hello satırlar) için kendi değerlerinizi yerleştirin.

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

## <a name="step-3-step-by-step-walkthrough---provision-hello-virtual-machine-and-join-it-toohello-managed-domain"></a>3. adım: Adım adım - hello sanal makine sağlama ve toohello yönetilen etki alanına katılma
Okunabilirlik için her bloğu arasında boş satırlar ile bu sanal makine hello karşılık gelen Azure PowerShell komut kümesini toocreate aşağıdadır.

Sağlanan hello Windows sanal makine toobe hakkındaki bilgileri belirtin.

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

D, DS veya G-serisi sanal makineler için Hello InstanceSize değerleri için bkz: [sanal makine ve bulut hizmeti boyutları Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).

Merhaba yönetilen etki alanı hakkında bilgi sağlar.

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

Merhaba hello bulut hizmeti adını belirtin.

    $svcname="Contoso100-test"

VM birleştirilmelidir hello sanal ağ toowhich hello Hello adını belirtin. Bu hello AAD DS yönetilen etki alanı bu sanal ağda kullanılabilir olduğundan emin olun.

    $vnetname="MyPreviewVnet"

Merhaba VM görüntü kullanılan toobe tooprovision hello VM seçin.

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

Merhaba VM - kümesi VM adı, yapılandırma kullanılan örnek boyutu & görüntü toobe.

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

Merhaba VM için yerel yönetici kimlik bilgilerini edinin. Güçlü bir yerel yönetici parolası seçin.

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

Too'AAD DC Yöneticiler grubu toojoin VM toohello yönetilen etki alanına ait bir kullanıcı hesabı için kimlik bilgilerini edinin. Örneğimizde örneği belirttiğimiz 'Kemal için' hello etki alanı adı - hello kullanıcı adı olarak belirtmeyin.

    $domainadmincred=Get-Credential –Message "Now type hello name (DO NOT INCLUDE hello DOMAIN) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

Merhaba VM yapılandırma - etki alanı katılma gereksinim & gerekli kimlik bilgilerini belirtin.

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

Merhaba VM için bir alt ağ olarak ayarlayın.

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

İsteğe bağlı: Noktası toohello IP adresi hello etki alanı. Merhaba sanal ağ için DNS sunucularını hello Azure AD etki alanı Hizmetleri yönetilen etki alanı toobe hello hello IP adreslerini ayarlarsanız, bu adım gerekli değildir.

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

Şimdi, sağlama hello etki alanı Windows VM katılmış.

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-tooprovision-a-windows-vm-and-automatically-join-it-tooan-aad-domain-services-managed-domain"></a>Bir Windows VM tooprovision komut dosyası ve otomatik olarak tooan AAD etki alanı Hizmetleri yönetilen etki alanına katılın
Bu PowerShell komut kümesini iş sunucu için bir sanal makine oluşturur:

* Merhaba Windows Server 2012 R2 Datacenter görüntüsü kullanır.
* Ek çok küçük bir sanal makine bulunuyor.
* Merhaba adı Contoso100 test vardır.
* Otomatik olarak etki alanına katılmış toohello contoso100 yönetilen etki alanıdır.
* Toohello eklenen hello aynı sanal ağ yönetilen etki alanı.

İşte tam örnek komut dosyası toocreate hello Windows sanal makine hello ve otomatik olarak toohello Azure AD etki alanı Hizmetleri yönetilen etki alanına katılın.

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

    $domainadmincred=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a>İlgili İçerik
* [Azure AD etki alanı Hizmetleri - başlangıç kılavuzu](active-directory-ds-getting-started.md)
* [Azure AD Domain Services tarafından yönetilen etki alanını yönetme](active-directory-ds-admin-guide-administer-domain.md)
