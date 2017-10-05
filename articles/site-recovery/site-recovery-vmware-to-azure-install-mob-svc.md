---
title: "Mobility hizmetinin (VMware veya fiziksel Azure) yükleme | Microsoft Docs"
description: "Şirket içi bilgisayarları korumak için Mobility hizmeti aracısı yüklemeyi öğrenin."
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
ms.openlocfilehash: 848284f37ae2470a169d8f8a8c9c0bb5b926abe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="install-mobility-service-vmware-or-physical-to-azure"></a>Mobility hizmetinin (VMware veya fiziksel Azure) yükleyin
Azure Site Recovery Mobility hizmeti, bir bilgisayardaki veri yazma yakalar ve bunları işlem sunucusuna gönderir. Azure'a çoğaltmak istediğiniz her bilgisayarda (VMware VM veya fiziksel sunucu) için Mobility hizmetini dağıtın. Mobility hizmeti aşağıdaki yöntemleri kullanarak korumak istediğiniz sunucuları dağıtabilirsiniz:


* [Mobility hizmeti yazılım dağıtım araçları gibi System Center Configuration Manager kullanarak yükleme](site-recovery-install-mobility-service-using-sccm.md)
* [Mobility hizmeti Azure Automation ve istenen durum yapılandırması (Automation DSC) kullanarak yükleme](site-recovery-automate-mobility-service-install.md)
* [Grafik kullanıcı arabirimi (GUI) kullanarak Mobility hizmeti el ile yükleyin](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [Mobility hizmeti el ile bir komut isteminden yükleme](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [Azure Site Recovery anında yüklemesinden tarafından Mobility hizmetini yükleme](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> Mobility hizmeti sürümü 9.7.0.0, Windows sanal makinelerde (VM'ler) başlayarak yükleyici de en son kullanılabilir yükler [Azure VM Aracısı](../virtual-machines/windows/extensions-features.md#azure-vm-agent). Bir bilgisayar üzerinden Azure'a başarısız olduğunda, bilgisayarın tüm VM uzantısı kullanılarak için önkoşul aracı yüklemesi karşılar.

## <a name="prerequisites"></a>Ön koşullar
Sunucunuzda el ile Mobility hizmetini yüklemeden önce önkoşul adımları tamamlayın:
1. Yapılandırma sunucusunda oturum açın ve ardından yönetici olarak bir komut istemi penceresi açın.
2. Bin klasörüne dizini değiştirin ve ardından bir parola dosyası oluşturun:

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. Parola dosyasını güvenli bir konumda depolayın. Mobility hizmeti yüklemesi sırasında dosyasını kullanın.
4. Tüm desteklenen işletim sistemleri için Mobility hizmeti yükleyiciler %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository klasöründe bulunur.

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


## <a name="install-mobility-service-manually-by-using-the-gui"></a>GUI kullanarak Mobility hizmeti el ile yükleyin

>[!IMPORTANT]
> Kullanıyorsanız bir **yapılandırma sunucusu** çoğaltmak için **Azure Iaas sanal makineleri** gelen bir Azure aboneliği/bölge sonra başka bir **komut satırı tabanlı yükleme kullanmak** yöntemi

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a>Mobility hizmeti el ile bir komut isteminden yükleme

### <a name="command-line-installation-on-a-windows-computer"></a>Bir Windows bilgisayarda komut satırı yüklemesi
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a>Linux bilgisayarda komut satırı yükleme
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a>Azure Site Recovery anında yüklemesinden tarafından Mobility hizmetini yükleme
Site RECOVERY'yi kullanarak mobilite hizmetinin göndermeli yüklemesi yapmak için tüm hedef bilgisayarlar aşağıdaki önkoşulları karşılamalıdır.

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
Mobility hizmeti, Azure portalında yükledikten sonra seçin **çoğaltmak** bu sanal makineleri korumaya başlamak için Başlat.

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a>Bir Windows Server bilgisayarında Mobility hizmetini kaldırma
Bir Windows Server bilgisayarında Mobility hizmetini kaldırmak için aşağıdaki yöntemlerden birini kullanın.

### <a name="uninstall-by-using-the-gui"></a>GUI kullanarak kaldırma
1. Denetim Masası'nda seçin **programlar**.
2. Seçin **Microsoft Azure Site Recovery Mobility hizmeti/ana hedef sunucu**ve ardından **kaldırma**.

### <a name="uninstall-at-a-command-prompt"></a>Bir komut isteminde kaldırma
1. Yönetici olarak bir komut istemi penceresi açın.
2. Mobility hizmetini kaldırmak için aşağıdaki komutu çalıştırın:

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a>Bir Linux bilgisayarda Mobility hizmetini kaldırma
1. Linux sunucunuzda olarak oturum açın bir **kök** kullanıcı.
2. Bir terminale için /user/local/ASR gidin.
3. Mobility hizmetini kaldırmak için aşağıdaki komutu çalıştırın:

```
uninstall.sh -Y
```
