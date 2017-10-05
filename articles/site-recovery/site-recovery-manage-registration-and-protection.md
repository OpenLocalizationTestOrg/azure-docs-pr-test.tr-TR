---
title: "Sunucuları kaldırın ve koruma devre dışı bırakma | Microsoft Docs"
description: "Bu makalede Site Recovery kasası sunucularından kaydı ve sanal makineleri ve fiziksel sunucuları için korumayı devre dışı bırakmak için açıklar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: ef1f31d5-285b-4a0f-89b5-0123cd422d80
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: raynew
ms.openlocfilehash: 43f92a35dc9b04584badd1c9f1152470246b5012
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="remove-servers-and-disable-protection"></a>Sunucuları kaldırma ve korumayı devre dışı bırakma

Azure Site Recovery hizmeti, iş sürekliliği ve olağanüstü durum kurtarma (BCDR) stratejinize katkı sağlar. Hizmet, çoğaltma, yük devretme ve sanal makinelerin ve fiziksel sunucuları kurtarma düzenler. Makineler, Azure'a veya bir ikincil şirket içi veri merkezine çoğaltılabilir. Hızlı bir genel bakış için [Azure Site Recovery nedir?](site-recovery-overview.md) konusunu okuyun.

Bu makalede, Azure portalında bir kurtarma Hizmetleri kasası sunucularından kaydı etme ve Site Recovery tarafından korunan makineler için korumayı devre dışı bırakma açıklanmaktadır.

Tüm yorumlarınızı ve sorularınızı bu makalenin alt kısmında veya [Azure Kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)'nda paylaşabilirsiniz.

## <a name="unregister-a-connected-configuration-server"></a>Bağlantılı yapılandırma sunucusu kaydı

VMware Vm'leri veya Windows/Linux fiziksel sunucuları Azure'a çoğaltma durumunda bir kasa bağlı yapılandırma sunucusundan gibi kaydını kaldırabilirsiniz:

1. Makine korumasını devre dışı bırakın. İçinde **korunan öğeler** > **çoğaltılan öğeler**, makine adını sağ tıklayın > **silmek**.
2. Tüm ilkeler ilişkisini kaldırın. İçinde **Site Recovery altyapısı** > **için VMWare ve fiziksel makineler** > **çoğaltma ilkeleri**, ilişkili ilkeye çift tıklayın. Yapılandırma sunucusu sağ tıklayın > **ilişkisini**.
3. Herhangi bir ek şirket içi işlem veya ana hedef sunucuları kaldırın. İçinde **Site Recovery altyapısı** > **için VMWare ve fiziksel makineler** > **yapılandırma sunucularına**, sunucuya sağ tıklayın > **silmek**.
4. Yapılandırma sunucusu silin.
5. Ana hedef sunucu üzerinde çalışan mobilite hizmetini elle kaldırın (Bu ya da ayrı bir olacak sunucu veya yapılandırma sunucusu üzerinde çalışan).
6. Herhangi bir ek işlem sunucusu kaldırın.
7. Yapılandırma sunucusundan kaldırın.
8. Yapılandırma sunucusunda Site Recovery tarafından yüklenen MySQL örneğini kaldırın.
9. Yapılandırma sunucusu kayıt defterinde anahtar silinmeye ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.

## <a name="unregister-a-unconnected-configuration-server"></a>Bağlantısız yapılandırma sunucusu kaydı

VMware Vm'leri veya Windows/Linux fiziksel sunucuları Azure'a çoğaltma durumunda bir kasa bağlantısız yapılandırma sunucusundan gibi kaydını kaldırabilirsiniz:

1. Makine korumasını devre dışı bırakın. İçinde **korunan öğeler** > **çoğaltılan öğeler**, makine adını sağ tıklayın > **silmek**. Seçin **makineyi yönetmeyi Durdur**.
2. Herhangi bir ek şirket içi işlem veya ana hedef sunucuları kaldırın. İçinde **Site Recovery altyapısı** > **için VMWare ve fiziksel makineler** > **yapılandırma sunucularına**, sunucuya sağ tıklayın > **silmek**.
3. Yapılandırma sunucusu silin.
4. Ana hedef sunucu üzerinde çalışan mobilite hizmetini elle kaldırın (Bu ya da ayrı bir olacak sunucu veya yapılandırma sunucusu üzerinde çalışan).
5. Herhangi bir ek işlem sunucusu kaldırın.
6. Yapılandırma sunucusundan kaldırın.
7. Yapılandırma sunucusunda Site Recovery tarafından yüklenen MySQL örneğini kaldırın.
8. Yapılandırma sunucusu kayıt defterinde anahtar silinmeye ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.

## <a name="unregister-a-connected-vmm-server"></a>Bağlı bir VMM sunucusunun kaydı silinemedi

En iyi uygulama, Azure'a bağlıyken VMM sunucusunun kaydı öneririz. Bu ayarları VMM sunucularında (ve diğer eşleştirilmiş bulut VMM sunucularıyla) düzgün temizlendiğinden sağlar. Bağlantı kalıcı bir sorun varsa, bağlantısız bir sunucu yalnızca kaldırmanız gerekir. VMM sunucusu bağlı değilse, el ile ayarlarını temizlemek için bir komut dosyasını çalıştırmak gerekir.

1. Kaldırmak istediğiniz VMM sunucusundaki sanal makineleri çoğaltmak durdurun.
2. Silmek istediğiniz VMM sunucusundaki Bulutlar tarafından kullanılan tüm ağ eşlemeleri silin. İçinde **Site Recovery altyapısı** > **için System Center VMM** > **ağ eşlemesi**, ağ eşlemesi sağ tıklayın > **silmek**.
3. Kaldırmak istediğiniz VMM sunucusundaki Bulutlar ilkelerden çoğaltma ilişkisini kaldırın.  İçinde **Site Recovery altyapısı** > **için System Center VMM** >  **çoğaltma ilkeleri**, ilişkili ilkeye çift tıklayın. Buluta sağ tıklayın > **ilişkisini**.
4. VMM sunucusu veya etkin VMM düğümü silin. İçinde **Site Recovery altyapısı** > **için System Center VMM** > **VMM sunucuları**, sunucuya sağ tıklayın > **silmek**.
5. Sağlayıcı VMM sunucusunda el ile kaldırın. Bir kümeniz varsa, tüm düğümlerden kaldırın.
6. El ile Azure'da çoğaltıyorsanız Microsoft Kurtarma Hizmetleri aracısını silinen bulutlarındaki Hyper-V konakları kaldırın.



### <a name="unregister-an-unconnected-vmm-server"></a>Bağlantısız bir VMM sunucusunun kaydı silinemedi

1. Kaldırmak istediğiniz VMM sunucusundaki sanal makineleri çoğaltmak durdurun.
2. Silmek istediğiniz VMM sunucusundaki Bulutlar tarafından kullanılan tüm ağ eşlemeleri silin. İçinde **Site Recovery altyapısı** > **için System Center VMM** > **ağ eşlemesi**, ağ eşlemesi sağ tıklayın > **silmek**.
3. VMM sunucusu Kimliğini not alın.
4. Kaldırmak istediğiniz VMM sunucusundaki Bulutlar ilkelerden çoğaltma ilişkisini kaldırın.  İçinde **Site Recovery altyapısı** > **için System Center VMM** >  **çoğaltma ilkeleri**, ilişkili ilkeye çift tıklayın. Buluta sağ tıklayın > **ilişkisini**.
5. VMM sunucusu veya etkin düğüm silin. İçinde **Site Recovery altyapısı** > **için System Center VMM** > **VMM sunucuları**, sunucuya sağ tıklayın > **silmek**.
6. İndirme ve çalıştırma [temizleme betiğini](http://aka.ms/asr-cleanup-script-vmm) VMM sunucusunda. PowerShell ile açmak **yönetici olarak çalıştır** seçeneği, varsayılan (LocalMachine) kapsamı yürütme ilkesini değiştirmek için. Komut dosyasında, kaldırmak istediğiniz VMM sunucusunu Kimliğini belirtin. Betik kaydı ve bulut eşleştirme bilgilerini sunucusundan kaldırır.
5. Kaldırmak istediğiniz VMM sunucusundaki Bulutlar ile eşleştirilmiş bulut içeren herhangi bir VMM sunucularında temizleme betiğini çalıştırın.
6. Yüklü sağlayıcı olan tüm diğer pasif VMM küme düğümlerine temizleme betiğini çalıştırın.
7. Sağlayıcı VMM sunucusunda el ile kaldırın. Bir kümeniz varsa, tüm düğümlerden kaldırın.
8. Azure'a çoğaltma, Microsoft Kurtarma Hizmetleri aracısını Hyper-V konakları silinen bulutlarındaki kaldırabilirsiniz

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a>Bir Hyper-V sitesi bir Hyper-V ana bilgisayar kaydı

VMM tarafından yönetilmeyen Hyper-V konaklarının, Hyper-V sitesi toplanır. Bir konak bir Hyper-V sitede aşağıdaki gibi kaldırın:

1. Hyper-V ana bilgisayarda yer alan VM'ler için çoğaltma devre dışı bırakın.
2. Hyper-V sitesi için ilkeler ilişkisini kaldırın. İçinde **Site Recovery altyapısı** > **için Hyper-V sitelerini** >  **çoğaltma ilkeleri**, ilişkili ilkeye çift tıklayın. Sitesi > **ilişkisini**.
3. Hyper-V konakları silin. İçinde **Site Recovery altyapısı** > **için System Center VMM** > **Hyper-V konakları**, sunucuya sağ tıklayın > **silmek**.
4. Tüm konaklar ondan temizlendikten sonra Hyper-V sitesi silin. İçinde **Site Recovery altyapısı** > **için System Center VMM** > **Hyper-V sitelerini**, siteye sağ tıklayın > **silmek**.
5. Aşağıdaki komut dosyasını kaldırdığınız her Hyper-V ana bilgisayarda çalıştırın. Betik sunucu ayarları temizler ve kasadan kaydını siler.


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run the script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove the old Azure Site Recovery Provider related properties. Do you want to continue (Y/N) ?"
            $choice =  Read-Host

            if (!($choice -eq 'Y' -or $choice -eq 'y'))
            {
            "Stopping cleanup."
            return;
            }

            $serviceName = "dra"
            $service = Get-Service -Name $serviceName
            if ($service.Status -eq "Running")
            {
                "Stopping the Azure Site Recovery service..."
                net stop $serviceName
            }

            $asrHivePath = "HKLM:\SOFTWARE\Microsoft\Azure Site Recovery"
            $registrationPath = $asrHivePath + '\Registration'
            $proxySettingsPath = $asrHivePath + '\ProxySettings'
            $draIdvalue = 'DraID'

            if (Test-Path $asrHivePath)
            {
                if (Test-Path $registrationPath)
                {
                    "Removing registration related registry keys."    
                    Remove-Item -Recurse -Path $registrationPath
                }

                if (Test-Path $proxySettingsPath)
            {
                    "Removing proxy settings"
                    Remove-Item -Recurse -Path $proxySettingsPath
                }

                $regNode = Get-ItemProperty -Path $asrHivePath
                if($regNode.DraID -ne $null)
                {            
                    "Removing DraId"
                    Remove-ItemProperty -Path $asrHivePath -Name $draIdValue
                }
                "Registry keys removed."
            }

            # First retrive all the certificates to be deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete the certs
            "Removing all related certificates"
            foreach ($cert in $ASRcerts)
            {
                $store.Remove($cert)
            }
        }catch
        {    
            [system.exception]
            Write-Host "Error occured" -ForegroundColor "Red"
            $error[0]
            Write-Host "FAILED" -ForegroundColor "Red"
        }
        popd``



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a>VMware VM veya fiziksel sunucu için koruma devre dışı bırak

1. İçinde **korunan öğeler** > **çoğaltılan öğeler**, makine adını sağ tıklayın > **silmek**.
2. İçinde **makineyi Kaldır**, aşağıdaki seçeneklerden birini seçin:
    - **(Önerilen) makine için korumayı devre dışı**. Makine çoğaltmasını durdurmak için bu seçeneği kullanın. Site Recovery ayarları otomatik olarak temizlenecek. Yalnızca aşağıdaki durumlarda bu seçenek görürsünüz:
        - **VM birim yeniden boyutlandırılıyor**— sanal makine bir kritik duruma geçer bir birim yeniden boyutlandırdığınızda. Kurtarma noktalarının azure'da korurken devre dışı bırakır koruma için bu seçeneği belirleyin. Makine için korumayı yeniden etkinleştirdiğinizde, yeniden boyutlandırılmış birim için verileri Azure'a aktarılır.
        - **Bir yük devretme yakın zamanda çalıştırdıysanız**— ortamınızı test etmek için bir yük devretme çalıştırdıktan sonra şirket içi makineler yeniden korumaya başlamak için bu seçeneği belirleyin. Her bir sanal makine devre dışı bırakır ve sonra bunlar için korumayı yeniden etkinleştirmeniz gerekir. Bu ayar makineyle devre dışı bırakma Azure içinde çoğaltma sanal makinesi etkilemez. Mobility hizmetinin makineden kaldırmak yok.
    - **Makineyi yönetmeyi Durdur**. Bu seçeneği seçerseniz, makine yalnızca kasadan kaldırılır. Şirket içi makine için koruma ayarları etkilenmeyecek. Makine ayarlarını kaldırın ve makine Azure aboneliğinden kaldırmak için Mobility hizmeti kaldırarak ayarları temizlemek gerekir.

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a>VMM bulutundaki Hyper-V VM için korumayı devre dışı

1. İçinde **korunan öğeler** > **çoğaltılan öğeler**, makine adını sağ tıklayın > **silmek**.
2. İçinde **makineyi Kaldır**, aşağıdaki seçeneklerden birini seçin:

    - **(Önerilen) makine için korumayı devre dışı**. Makine çoğaltmasını durdurmak için bu seçeneği kullanın. Site Recovery ayarları otomatik olarak temizlenecek.
    - **Makineyi yönetmeyi Durdur**. Bu seçeneği seçerseniz, makine yalnızca kasadan kaldırılır. Şirket içi makine için koruma ayarları etkilenmeyecek. Makine ayarlarını kaldırın ve makine Azure aboneliğinden kaldırmak için ayarları el ile temizlemek aşağıdaki yönergeleri kullanarak gerekir. Sanal makine ve sabit diskleri silmek için seçerseniz, bunlar hedef konumundan kaldırılması olduğunu unutmayın.

### <a name="clean-up-protection-settings---replication-to-a-secondary-vmm-site"></a>Koruma ayarlarını - ikincil VMM sitesi için çoğaltma Temizle

Seçtiyseniz **makineyi yönetmeyi Durdur** ve birincil sanal makine ayarlarını temizlemek için birincil sunucuda bu komut dosyasını çalıştırın, ikincil bir siteye çoğaltmak. VMM konsolundan VMM PowerShell konsolunu açmak için PowerShell düğmesini tıklatın. SQLVM1, sanal makine adı ile değiştirin.

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. İkincil VMM sunucusunda ikincil sanal makinenin ayarlarını temizlemek için bu komut dosyasını çalıştırın:

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. Böylece ikincil VM yeniden VMM konsolunda algılanan ikincil VMM sunucusunda Hyper-V ana bilgisayar sunucusunda sanal makineleri yenileyin.
4. VMM sunucusundaki çoğaltma ayarlarını yukarıdaki adımları temizleyin. Sanal makine için çoğaltma durdurmak istiyorsanız, aşağıdaki komut dosyasını birincil ve ikincil VM'ler çalıştırın. SQLVM1, sanal makine adı ile değiştirin.

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-to-azure"></a>Koruma ayarlarını - Azure'a çoğaltma için temizleme

1. Seçtiyseniz **makineyi yönetmeyi Durdur** ve kaynak VMM sunucusunda bu komut dosyası çalıştırma Azure PowerShell kullanarak VMM konsolundan çoğaltır.
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. Yukarıdaki adımları VMM sunucusundaki çoğaltma ayarları temizleyin. Hyper-V ana bilgisayar sunucusunda çalışan sanal makine için çoğaltma durdurmak için bu komut dosyasını çalıştırın. SQLVM1 adıyla bir sanal makine ve host01.contoso.com Hyper-V konak sunucusu adını değiştirin.

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a>Bir Hyper-V sitesindeki bir Hyper-V sanal makine için korumayı devre dışı bırakın

Azure için Hyper-V sanal makinelerini çoğaltıyorsanız olmadan bir VMM sunucusu, bu yordamı kullanın.

1. İçinde **korunan öğeler** > **çoğaltılan öğeler**, makine adını sağ tıklayın > **silmek**.
2. İçinde **makineyi Kaldır**, aşağıdaki seçenekleri seçebilirsiniz:

   - **(Önerilen) makine için korumayı devre dışı**. Makine çoğaltmasını durdurmak için bu seçeneği kullanın. Site Recovery ayarları otomatik olarak temizlenecek.
   - **Makineyi yönetmeyi Durdur**. Bu seçeneği seçerseniz, makine kasadan yalnızca kaldırılır. Şirket içi makine için koruma ayarları etkilenmeyecek. Makine ayarlarını kaldırın ve sanal makineyi Azure aboneliğinden kaldırmak için ayarları el ile temizlenmesi gerekir. Sanal makine ve sabit diskleri silmek için seçerseniz hedef konumundan kaldırılacak.
3. Seçtiyseniz **makineyi yönetmeyi Durdur**, sanal makine için çoğaltmayı kaldırmak için kaynak Hyper-V ana bilgisayarı sunucusunda, bu komut dosyasını çalıştırın. SQLVM1, sanal makine adı ile değiştirin.

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
