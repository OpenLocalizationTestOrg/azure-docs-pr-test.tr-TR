---
title: aaaInstall Mobility hizmetinin (VMware veya fiziksel tooAzure) | Microsoft Docs
description: "Nasıl tooinstall hello Mobility Hizmeti Aracısı tooprotect şirket içi bilgisayarlarınızı öğrenin."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: f7836e6b35d3838bae1eff927838ce4b245b9f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-mobility-service-vmware-or-physical-tooazure"></a>Mobility hizmetinin (VMware veya fiziksel tooAzure) yükleyin
Azure Site Recovery Mobility hizmeti, bir bilgisayardaki veri yazma yakalar ve bunları toohello işlem sunucusuna iletir. Tooreplicate tooAzure istediğiniz Mobility hizmeti tooevery bilgisayar (VMware VM veya fiziksel sunucu) dağıtın. Mobility hizmeti toohello sunucuları hello aşağıdaki yöntemleri kullanarak tooprotect istediğiniz dağıtabilirsiniz:


* [Mobility hizmeti yazılım dağıtım araçları gibi System Center Configuration Manager kullanarak yükleme](site-recovery-install-mobility-service-using-sccm.md)
* [Mobility hizmeti Azure Automation ve istenen durum yapılandırması (Automation DSC) kullanarak yükleme](site-recovery-automate-mobility-service-install.md)
* [Merhaba grafik kullanıcı arabirimi (GUI) kullanarak Mobility hizmeti el ile yükleyin](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [Mobility hizmeti el ile bir komut isteminden yükleme](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [Azure Site Recovery anında yüklemesinden tarafından Mobility hizmetini yükleme](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> Sürüm 9.7.0.0, Windows sanal makinelerde (VM'ler) ile başlayan hello Mobility Hizmeti Yükleyici de hello en son kullanılabilir yükler [Azure VM Aracısı](../virtual-machines/windows/extensions-features.md#azure-vm-agent). Bir bilgisayar tooAzure başarısız olduğunda, hello bilgisayar hello aracı yüklemesi VM uzantıyı kullanmak için önkoşul karşılar.

## <a name="prerequisites"></a>Ön koşullar
Sunucunuzda el ile Mobility hizmetini yüklemeden önce önkoşul adımları tamamlayın:
1. Tooyour yapılandırma sunucusunda oturum açın ve ardından yönetici olarak bir komut istemi penceresi açın.
2. Merhaba dizin toohello bin klasörü değiştirin ve ardından bir parola dosyası oluşturun:

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. Merhaba parola dosyasını güvenli bir konumda depolayın. Merhaba Mobility hizmeti yüklemesi sırasında hello dosyasını kullanın.
4. Tüm desteklenen işletim sistemleri için Mobility hizmeti yükleyiciler hello %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository klasöründe yer alır.

### <a name="mobility-service-installer-to-operating-system-mapping"></a>Mobility hizmeti işletim yükleyici sistem eşlemesi

| Yükleyici dosyası şablonu adı| İşletim sistemi |
|---|--|
|Microsoft ASR\_UA\*Windows\*release.exe | Windows Server 2008 R2 SP1 (64 bit) </br> Windows Server 2012 (64 bit) </br> Windows Server 2012 R2 (64 bit) |
|Microsoft ASR\_UA\*RHEL6 64*release.tar.gz| Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6,8 (yalnızca 64 bit) </br> CentOS 6.4 6.5, 6.6, 6.7, 6,8 (yalnızca 64 bit) |
|Microsoft ASR\_UA\*RHEL7 64\*release.tar.gz | Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (yalnızca 64 bit) </br> CentOS 7.0, 7.1, 7.2 (yalnızca 64 bit)</br> CentOs 7.3 (yalnızca geçiş) |
|Microsoft ASR\_UA\*SLES11 SP3 64\*release.tar.gz| SUSE Linux Enterprise Server 11 SP3 (yalnızca 64 bit)|
|Microsoft ASR\_UA\*SLES11 SP4 64\*release.tar.gz| SUSE Linux Enterprise Server 11 SP4 (yalnızca 64 bit)|
|Microsoft ASR\_UA\*OL6 64\*release.tar.gz | Oracle Enterprise Linux 6.4, 6.5 (yalnızca 64 bit)|
|Microsoft ASR\_UA\*UBUNTU 14.04 64\*release.tar.gz | Ubuntu Linux 14.04 (yalnızca 64 bit)|


## <a name="install-mobility-service-manually-by-using-hello-gui"></a>Merhaba GUI kullanarak Mobility hizmeti el ile yükleyin

>[!IMPORTANT]
> Kullanıyorsanız bir **yapılandırma sunucusu** tooreplicate **Azure Iaas sanal makineleri** bir Azure aboneliği/bölge tooanother sonra gelen **hello komut satırı tabanlı yükleme kullanmak**  yöntemi

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a>Mobility hizmeti el ile bir komut isteminden yükleme

### <a name="command-line-installation-on-a-windows-computer"></a>Bir Windows bilgisayarda komut satırı yüklemesi
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a>Linux bilgisayarda komut satırı yükleme
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a>Azure Site Recovery anında yüklemesinden tarafından Mobility hizmetini yükleme
toodo Site Recovery kullanarak bir itme yüklemesini Mobility hizmeti, tüm hedef bilgisayarlar aşağıdaki önkoşulları hello karşılaması gerekir.

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
Mobility hizmeti, hello Azure portal yükledikten sonra hello seçin **çoğaltmak** düğmesini toostart bu Vm'leri koruma.

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a>Bir Windows Server bilgisayarında Mobility hizmetini kaldırma
Bir Windows Server bilgisayarında yöntemleri toouninstall Mobility hizmeti aşağıdaki hello birini kullanın.

### <a name="uninstall-by-using-hello-gui"></a>Merhaba GUI kullanarak kaldırma
1. Denetim Masası'nda seçin **programlar**.
2. Seçin **Microsoft Azure Site Recovery Mobility hizmeti/ana hedef sunucu**ve ardından **kaldırma**.

### <a name="uninstall-at-a-command-prompt"></a>Bir komut isteminde kaldırma
1. Yönetici olarak bir komut istemi penceresi açın.
2. Mobility hizmeti toouninstall hello aşağıdaki komutu çalıştırın:

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a>Bir Linux bilgisayarda Mobility hizmetini kaldırma
1. Linux sunucunuzda olarak oturum açın bir **kök** kullanıcı.
2. Bir terminale çok/kullanıcı/yerel/ASR gidin.
3. Mobility hizmeti toouninstall hello aşağıdaki komutu çalıştırın:

```
uninstall.sh -Y
```
