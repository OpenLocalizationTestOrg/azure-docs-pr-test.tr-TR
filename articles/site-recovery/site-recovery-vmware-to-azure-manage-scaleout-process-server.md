---
title: " Bir genişleme işlem sunucusu Azure Site kurtarma yönetme | Microsoft Docs"
description: "Bu makalede nasıl tooset ayarlama ve bir genişleme işlem sunucusu Azure Site kurtarma yönetme."
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
ms.openlocfilehash: 3d72f9c2c7014a4ff2fa2af168aa55ad1452eae5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-scale-out-process-server"></a>Bir genişleme işlem sunucusu yönetme

Genişleme işlem sunucusu hello Site kurtarma Hizmetleri ve şirket içi altyapınızı arasında veri aktarmak için bir düzenleyici gibi davranır. Bu makalede nasıl ayarlamak, yapılandırabilir ve bir genişleme işlem sunucusu yönetmek açıklanmaktadır.

## <a name="prerequisites"></a>Ön koşullar
Merhaba önerilen donanım, yazılım ve ağ yapılandırma gerekli tooset bir genişleme işlem sunucusu Hello aşağıda verilmiştir.

> [!NOTE]
> [Kapasite planlama](site-recovery-capacity-planner.md) hello genişleme işlem sunucusu bir yapılandırma ile bu paketleri dağıtmak için önemli adım tooensure olan yük gereksinimlerinizi. Daha fazla bilgi edinin [özellikleri için bir genişleme işlem sunucusu ölçeklendirme](#sizing-requirements-for-a-configuration-server).

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-scale-out-process-server-software"></a>Merhaba genişleme işlem sunucusu yazılım indirme
1. Toohello üzerinde Azure portal ve göz atma tooyour kurtarma Hizmetleri kasası oturum açın.
2. Çok Gözat**Site Recovery altyapısı** > **yapılandırma sunucularına** (altında For VMware ve fiziksel makineler).
3. Yapılandırma sunucusu toodrill aşağı hello yapılandırma sunucunun ayrıntıları sayfasına seçin.
4. Merhaba tıklatın **+ işlem sunucusu** düğmesi.
5. Merhaba, **eklemek işlem sunucusu** sayfasında, **dağıtma bir genişleme işlem sunucusu şirket içi** hello seçeneğinden **istediğiniz toodeploy işlem sunucunuzu seçin** aşağı açılır.

  ![Sunucuları Sayfası Ekle](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. Merhaba tıklatın **indirme hello Microsoft Azure Site Recovery birleşik Kurulumu** bağlantı toodownload hello en son sürümünü hello genişleme işlem sunucusu yükleme.

  > [!WARNING]
  Merhaba, genişleme işlem sunucusu sürümü aynı olmalıdır tooor ortamınızda çalışan hello yapılandırma sunucusu sürümden daha düşük. Basit bir yol tooensure sürüm uyumluluğu toouse olan hello tooinstall/güncelleştirme son yapılandırma sunucunuz kullanılan aynı yükleyici BITS.

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a>Yükleme ve bir genişleme işlem sunucusu GUI'den kaydetme
Dağıtımınızı 200 kaynak makinelerden ötesinde çıkışı tooscale varsa veya toplam günlük karmaşıklığı 2 TB'den fazla oranını ek işlem sunucuları toohandle hello trafik hacmi gerekir.

Merhaba denetleyin [boyut işlem sunucuları için öneriler](#size-recommendations-for-the-process-server)ve ardından bu yönergeleri tooset hello işlem sunucusu izleyin. Kaynak makine toouse geçirmek Hello sunucuyu ayarladıktan sonra onu.

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a>Yükleme ve komut satırı kullanarak bir genişleme işlem sunucusu kaydetme

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a>Örnek Kullanım
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a>Genişleme işlem sunucusu Yükleyici komut satırı bağımsız değişkenleri.
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a>Proxy ayarlarını yapılandırma dosyası oluşturma
ProxySettingsFilePath parametresi bir dosya girdi olarak alır. Aşağıdaki biçimlendirmek ve giriş ProxySettingsFilePath parametre olarak geçirmek hello kullanarak dosyası oluşturun.
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a>Genişleme işlem sunucusu için proxy ayarlarını değiştirme
1. Genişleme işlem sunucusu uygulamasına oturum açın.
2. Bir yönetici PowerShell komut penceresi açın.
3. Merhaba aşağıdaki komutu çalıştırın
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. Sonraki toohello dizin taraması **%PROGRAMDATA%\ASR\Agent** ve çalışma hello aşağıdaki komutu
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a>Bir genişleme işlem sunucusu yeniden kaydetme
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* Sonraki bir yönetici komut istemi açın.
* Toohello dizin taraması **%PROGRAMDATA%\ASR\Agent** ve hello komutunu çalıştırın

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a>Bir genişleme işlem sunucusu yükseltme
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a>Bir genişleme işlem sunucusu yetkisini alma
1. Emin olun:
  - Yapılandırma sunucusunun bağlantı durumunu gösterir olarak **bağlı** hello Azure portal'ın
  - İşlem sunucusunun hello yapılandırma sunucusu ile koruyabilmeyi toocommunicate ' dir.
2. Toohello işlem sunucusunda bir yönetici olarak oturum
3. Denetim Masası açın > Program > programları Kaldır
4. Merhaba programları aşağıdaki verilen hello sırayla kaldırın:
  * Microsoft Azure Site kurtarma yapılandırması sunucu/işlem sunucusu
  * Microsoft Azure Site kurtarma yapılandırması sunucu bağımlılıkları
  * Microsoft Azure Kurtarma Hizmetleri Aracısı

Hello Azure portal, hello işlem sunucusu silme tooreflect yukarı too15 dakika sürebilir.

  > [!NOTE]
  Merhaba işlem sunucusu hello yapılandırma sunucusu ile oluşturulamıyor toocommunicate olup olmadığını (Portalı'nda bağlantı durumu kesilir) yeniden toofollow gerekiyor hello adımları toopurge, yapılandırma sunucusu hello.

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a>Bağlantısı kesilmiş bir genişleme işlem sunucusu bir yapılandırma sunucusundan kaydını silme

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a>Bir genişleme işlem sunucusu için gereksinimleri boyutlandırma

| **Ek işlem sunucusu** | **Önbellek disk boyutu** | **Veri değişikliği oranı** | **Korumalı makineler** |
| --- | --- | --- | --- |
|4 Vcpu (2 yuva * 2,5 GHz @ 2 Çekirdek), 8 GB bellek |300 GB |250 GB veya daha az |85 veya daha az makine çoğaltılır. |
|8 Vcpu'lar (2 yuva * @ 2,5 GHz 4 çekirdek), 12 GB bellek |600 GB |250 GB too1 TB |85 150 makineler arasında çoğaltılır. |
|12 Vcpu'lar (2 yuva * 2,5 GHz @ 6 çekirdek) 24 GB bellek |1 TB |1 TB too2 TB |150-225 makineler arasında çoğaltılır. |
