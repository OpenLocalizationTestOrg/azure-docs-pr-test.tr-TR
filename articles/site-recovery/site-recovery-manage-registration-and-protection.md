---
title: "aaaRemove sunucuları ve koruma devre dışı bırakma | Microsoft Docs"
description: "Bu makalede nasıl toounregister sunucuları bir Site kurtarma kasası ve sanal makineleri ve fiziksel sunucuları için toodisable korumayı açıklar."
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
ms.openlocfilehash: 95f20433f782c93685ad4bae93c6bc0e2d2f2356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-servers-and-disable-protection"></a>Sunucuları kaldırma ve korumayı devre dışı bırakma

Hello Azure Site Recovery hizmeti tooyour iş devamlılığı ve olağanüstü durum kurtarma (BCDR) stratejinize katkı sağlar. Çoğaltma, yük devretme ve sanal makinelerin ve fiziksel sunucuları kurtarma Hello hizmet düzenler. Makineler çoğaltılmış tooAzure veya tooa ikincil şirket içi veri merkezi olabilir. Hızlı bir genel bakış için [Azure Site Recovery nedir?](site-recovery-overview.md) konusunu okuyun.

Bu makalede nasıl hello Azure portal toounregister sunucularından bir kurtarma Hizmetleri kasası ve nasıl toodisable koruma makineler için Site Recovery tarafından korunan açıklanır.

Tüm yorumlarınızı ve sorularınızı bu makalenin veya hello hello altındaki sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="unregister-a-connected-configuration-server"></a>Bağlantılı yapılandırma sunucusu kaydı

VMware Vm'leri veya Windows/Linux fiziksel sunucuları tooAzure çoğaltma durumunda bir kasa bağlı yapılandırma sunucusundan gibi kaydını kaldırabilirsiniz:

1. Makine korumasını devre dışı bırakın. İçinde **korunan öğeler** > **çoğaltılan öğeler**, sağ hello makine > **silmek**.
2. Tüm ilkeler ilişkisini kaldırın. İçinde **Site Recovery altyapısı** > **için VMWare ve fiziksel makineler** > **çoğaltma ilkeleri**, hello çift tıklatın ilişkili ilke. Sağ hello yapılandırma sunucusu > **ilişkisini**.
3. Herhangi bir ek şirket içi işlem veya ana hedef sunucuları kaldırın. İçinde **Site Recovery altyapısı** > **için VMWare ve fiziksel makineler** > **yapılandırma sunucularına**, sağ hello sunucu > **Silmek**.
4. Merhaba yapılandırma sunucusu silin.
5. Merhaba ana hedef sunucu üzerinde çalışan hello mobilite hizmetini elle kaldırın (Bu ya da ayrı bir olacak sunucu veya hello yapılandırma sunucusu üzerinde çalışan).
6. Herhangi bir ek işlem sunucusu kaldırın.
7. Merhaba yapılandırma sunucusundan kaldırın.
8. Merhaba yapılandırma sunucusunda Site Recovery tarafından yüklenen MySQL hello örneğini kaldırın.
9. Merhaba yapılandırma sunucusu Hello kayıt defterinde hello anahtarını silmek ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.

## <a name="unregister-a-unconnected-configuration-server"></a>Bağlantısız yapılandırma sunucusu kaydı

VMware Vm'leri veya Windows/Linux fiziksel sunucuları tooAzure çoğaltma durumunda bir kasa bağlantısız yapılandırma sunucusundan gibi kaydını kaldırabilirsiniz:

1. Makine korumasını devre dışı bırakın. İçinde **korunan öğeler** > **çoğaltılan öğeler**, sağ hello makine > **silmek**. Seçin **hello makineyi yönetmeyi Durdur**.
2. Herhangi bir ek şirket içi işlem veya ana hedef sunucuları kaldırın. İçinde **Site Recovery altyapısı** > **için VMWare ve fiziksel makineler** > **yapılandırma sunucularına**, sağ hello sunucu > **Silmek**.
3. Merhaba yapılandırma sunucusu silin.
4. Merhaba ana hedef sunucu üzerinde çalışan hello mobilite hizmetini elle kaldırın (Bu ya da ayrı bir olacak sunucu veya hello yapılandırma sunucusu üzerinde çalışan).
5. Herhangi bir ek işlem sunucusu kaldırın.
6. Merhaba yapılandırma sunucusundan kaldırın.
7. Merhaba yapılandırma sunucusunda Site Recovery tarafından yüklenen MySQL hello örneğini kaldırın.
8. Merhaba yapılandırma sunucusu Hello kayıt defterinde hello anahtarını silmek ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.

## <a name="unregister-a-connected-vmm-server"></a>Bağlı bir VMM sunucusunun kaydı silinemedi

En iyi uygulama, bu tooAzure bağlandığında hello VMM sunucusunun kaydı öneririz. Bu ayarları hello VMM sunucularında (ve diğer eşleştirilmiş bulut VMM sunucularıyla) düzgün temizlendiğinden sağlar. Bağlantı kalıcı bir sorun varsa, bağlantısız bir sunucu yalnızca kaldırmanız gerekir. Merhaba VMM sunucusu bağlı değil, gerekir toomanually betik tooclean ayarlarını çalıştırın.

1. Merhaba tooremove istediğiniz VMM sunucusu üzerinde bulutlarındaki sanal makineleri çoğaltmak durdurun.
2. Merhaba toodelete istediğiniz VMM sunucusunu bulutlarda tarafından kullanılan tüm ağ eşlemeleri silin. İçinde **Site Recovery altyapısı** > **için System Center VMM** > **ağ eşlemesi**, hello ağ eşlemesi sağ tıklayın >  **Silme**.
3. Merhaba tooremove istediğiniz VMM sunucusunu bulutlarda ilkelerden çoğaltma ilişkisini kaldırın.  İçinde **Site Recovery altyapısı** > **için System Center VMM** >  **çoğaltma ilkeleri**, ilişkili hello ilkeye çift tıklayın. Merhaba buluta sağ tıklayın > **ilişkisini**.
4. Merhaba VMM sunucusu veya etkin VMM düğümü silin. İçinde **Site Recovery altyapısı** > **için System Center VMM** > **VMM sunucuları**, sağ hello server >  **Silme**.
5. Merhaba sağlayıcısı hello VMM sunucusunda el ile kaldırın. Bir kümeniz varsa, tüm düğümlerden kaldırın.
6. TooAzure çoğaltıyorsanız el ile silinmiş hello bulutlarındaki Hyper-V konakları hello Microsoft Kurtarma Hizmetleri Aracısı'nı kaldırın.



### <a name="unregister-an-unconnected-vmm-server"></a>Bağlantısız bir VMM sunucusunun kaydı silinemedi

1. Merhaba tooremove istediğiniz VMM sunucusu üzerinde bulutlarındaki sanal makineleri çoğaltmak durdurun.
2. Toodelete istediğiniz hello VMM sunucusundaki Bulutlar tarafından kullanılan tüm ağ eşlemeleri silin. İçinde **Site Recovery altyapısı** > **için System Center VMM** > **ağ eşlemesi**, hello ağ eşlemesi sağ tıklayın >  **Silme**.
3. Merhaba VMM sunucusu Hello Kimliğini not alın.
4. Merhaba tooremove istediğiniz VMM sunucusunu bulutlarda ilkelerden çoğaltma ilişkisini kaldırın.  İçinde **Site Recovery altyapısı** > **için System Center VMM** >  **çoğaltma ilkeleri**, ilişkili hello ilkeye çift tıklayın. Merhaba buluta sağ tıklayın > **ilişkisini**.
5. Merhaba VMM sunucusu veya etkin düğüm silin. İçinde **Site Recovery altyapısı** > **için System Center VMM** > **VMM sunucuları**, sağ hello server >  **Silme**.
6. İndirme ve çalıştırma hello [temizleme betiğini](http://aka.ms/asr-cleanup-script-vmm) hello VMM sunucusunda. PowerShell ile Merhaba açmak **yönetici olarak çalıştır** seçeneği, toochange hello yürütme İlkesi hello varsayılan (LocalMachine) kapsam için. Merhaba komut dosyasında hello tooremove istediğiniz VMM sunucusunu hello Kimliğini belirtin. Merhaba betik kaydı ve bulut eşleştirme bilgilerini hello sunucusundan kaldırır.
5. Merhaba tooremove istediğiniz VMM sunucusu üzerinde Bulutları ile eşleştirilmiş bulut içeren herhangi bir VMM sunucularında Hello temizleme betiğini çalıştırın.
6. Merhaba sağlayıcısı yüklü olan tüm diğer pasif VMM küme düğümlerine Hello temizleme betiğini çalıştırın.
7. Merhaba sağlayıcısı hello VMM sunucusunda el ile kaldırın. Bir kümeniz varsa, tüm düğümlerden kaldırın.
8. TooAzure çoğaltma, hello Microsoft Kurtarma Hizmetleri aracısını silinmiş hello bulutlarındaki Hyper-V konakları kaldırırsanız.

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a>Bir Hyper-V sitesi bir Hyper-V ana bilgisayar kaydı

VMM tarafından yönetilmeyen Hyper-V konaklarının, Hyper-V sitesi toplanır. Bir konak bir Hyper-V sitede aşağıdaki gibi kaldırın:

1. Hyper-V hello ana bilgisayarda yer alan VM'ler için çoğaltma devre dışı bırakın.
2. Merhaba Hyper-V sitesi için ilkeler ilişkisini kaldırın. İçinde **Site Recovery altyapısı** > **için Hyper-V sitelerini** >  **çoğaltma ilkeleri**, ilişkili hello ilkeye çift tıklayın. Sağ hello site > **ilişkisini**.
3. Hyper-V konakları silin. İçinde **Site Recovery altyapısı** > **için System Center VMM** > **Hyper-V konakları**, sağ hello server >  **Silme**.
4. Tüm konaklar ondan temizlendikten sonra hello Hyper-V sitesi silin. İçinde **Site Recovery altyapısı** > **için System Center VMM** > **Hyper-V sitelerini**, sağ hello site >  **Silme**.
5. Komut dosyası kaldırdığınız her Hyper-V ana bilgisayarda aşağıdaki hello çalıştırın. Merhaba betik hello sunucusundaki ayarları temizler ve hello kasasından kaydını siler.


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run hello script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove hello old Azure Site Recovery Provider related properties. Do you want toocontinue (Y/N) ?"
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
                "Stopping hello Azure Site Recovery service..."
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

            # First retrive all hello certificates toobe deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete hello certs
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

1. İçinde **korunan öğeler** > **çoğaltılan öğeler**, sağ hello makine > **silmek**.
2. İçinde **makineyi Kaldır**, aşağıdaki seçeneklerden birini seçin:
    - **(Önerilen) hello makine için korumayı devre dışı**. Bu seçenek toostop Hello makinenin çoğaltıldığını kullanın. Site Recovery ayarları otomatik olarak temizlenecek. Aşağıdaki durumlarda hello bu seçeneği yalnızca görürsünüz:
        - **Merhaba VM birim yeniden boyutlandırılıyor**— sanal bir birim hello yeniden boyutlandırdığınızda makine kritik duruma geçer. Kurtarma noktalarının azure'da korurken bu seçeneği toodisables koruma seçin. Merhaba makine için korumayı yeniden etkinleştirdiğinizde, hello veri hello yeniden boyutlandırılmış birim için aktarılan tooAzure olur.
        - **Bir yük devretme yakın zamanda çalıştırdıysanız**— ortamınızın bir yük devretme tootest çalıştırdıktan sonra şirket içi makineleri yeniden koruma bu seçeneği toostart seçin. Her bir sanal makine devre dışı bırakır ve ardından tooenable koruma için yeniden gereksinim duyarsınız. Bu ayar devre dışı bırakma hello makineyle azure'da hello çoğaltma sanal makine etkilemez. Merhaba Mobility hizmeti hello makineden kaldırmak yok.
    - **Merhaba makineyi yönetmeyi Durdur**. Bu seçeneği belirlerseniz, hello makine yalnızca hello kasadan kaldırılır. Şirket içi hello makine için koruma ayarları etkilenmeyecek. tooremove ayarları hello makinesindeki ve tooremove hello hello Azure aboneliği makineden hello Mobility hizmeti kaldırarak tooclean hello ayarlarının gerekir.

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a>VMM bulutundaki Hyper-V VM için korumayı devre dışı

1. İçinde **korunan öğeler** > **çoğaltılan öğeler**, sağ hello makine > **silmek**.
2. İçinde **makineyi Kaldır**, aşağıdaki seçeneklerden birini seçin:

    - **(Önerilen) hello makine için korumayı devre dışı**. Bu seçenek toostop Hello makinenin çoğaltıldığını kullanın. Site Recovery ayarları otomatik olarak temizlenecek.
    - **Merhaba makineyi yönetmeyi Durdur**. Bu seçeneği belirlerseniz, hello makine yalnızca hello kasadan kaldırılır. Şirket içi hello makine için koruma ayarları etkilenmeyecek. tooremove ayarları hello makinesindeki ve tooremove hello hello Azure aboneliği makineden, tooclean hello ayarlarının yukarı el ile aşağıdaki hello yönergeleri kullanarak gerekir. Toodelete hello sanal makine ve sabit disk seçin, bunlar hello hedef konumundan kaldırılması olduğunu unutmayın.

### <a name="clean-up-protection-settings---replication-tooa-secondary-vmm-site"></a>Koruma ayarlarını - çoğaltma tooa ikincil VMM sitesi Temizle

Seçtiyseniz **hello makineyi yönetmeyi Durdur** ve tooa ikincil site, çoğaltma çalıştırdığınız bu betiği hello birincil sunucu tooclean hello ayarlarını hello birincil sanal makine için. Merhaba VMM konsolunda hello PowerShell düğmesi tooopen hello VMM PowerShell Konsolu'nu tıklatın. SQLVM1 sanal makineniz hello adıyla değiştirin.

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. Bu komut dosyası tooclean hello ayarlarını hello ikincil sanal makinenin Hello ikincil VMM sunucusunda çalıştırın:

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. Böylece Hello ikincil VM yeniden hello VMM konsolunda algılanan hello ikincil VMM sunucusunda hello Hyper-V konak sunucusunda hello sanal makineleri yenileyin.
4. Yukarıdaki adımları Hello hello çoğaltma ayarları hello VMM sunucusunda temizlenir. Merhaba sanal makinesi, aşağıdaki komut dosyası hello çalıştırmak için toostop çoğaltma istiyorsanız, birincil ve ikincil VM'ler hello. SQLVM1 sanal makineniz hello adıyla değiştirin.

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-tooazure"></a>Koruma ayarlarını - çoğaltma tooAzure Temizle

1. Seçtiyseniz **hello makineyi yönetmeyi Durdur** ve çoğaltma tooAzure, hello VMM konsolundan PowerShell kullanarak hello kaynak VMM sunucusunda, bu komut dosyasını çalıştırın.
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. Yukarıdaki adımları Hello hello VMM sunucusundaki hello çoğaltma ayarları temizleyin. toostop çoğaltma hello Hyper-V ana bilgisayar sunucusunda çalışan hello sanal makine için bu komut dosyasını çalıştırın. SQLVM1 hello adıyla bir sanal makine ve host01.contoso.com hello hello Hyper-V konak sunucusu adını değiştirin.

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a>Bir Hyper-V sitesindeki bir Hyper-V sanal makine için korumayı devre dışı bırakın

Bir VMM Sunucu olmadan Hyper-V sanal makineleri tooAzure çoğaltma yapıyorsanız bu yordamı kullanın.

1. İçinde **korunan öğeler** > **çoğaltılan öğeler**, sağ hello makine > **silmek**.
2. İçinde **makineyi Kaldır**, aşağıdaki seçenekleri şu hello seçebilirsiniz:

   - **(Önerilen) hello makine için korumayı devre dışı**. Bu seçenek toostop Hello makinenin çoğaltıldığını kullanın. Site Recovery ayarları otomatik olarak temizlenecek.
   - **Merhaba makineyi yönetmeyi Durdur**. Bu seçeneği belirlerseniz hello makine hello kasadan yalnızca kaldırılacak. Şirket içi hello makine için koruma ayarları etkilenmeyecek. tooremove ayarları hello makinesindeki ve hello Azure aboneliği tooremove hello sanal makineden, tooclean hello ayarlarını yukarı el ile yapmanız gerekir. Toodelete hello sanal makine ve kendi sabit diskleri seçerseniz hello hedef konumundan kaldırılacak.
3. Seçtiyseniz **hello makineyi yönetmeyi Durdur**, tooremove çoğaltma hello sanal makine için bu betiği hello kaynak Hyper-V ana bilgisayar sunucusunda çalıştırın. SQLVM1 sanal makineniz hello adıyla değiştirin.

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
