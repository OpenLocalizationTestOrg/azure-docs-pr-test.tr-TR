---
title: " Yapılandırma sunucusu Azure Site kurtarma yönetme | Microsoft Docs"
description: "Bu makalede nasıl tooset ve yapılandırma sunucusunu yönetebilirsiniz."
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
ms.openlocfilehash: 2852bcd25409121be46a1ebf135ebfcdce6e5de5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-configuration-server"></a>Yapılandırma sunucusu yönetme

Yapılandırma sunucusu hello Site kurtarma Hizmetleri ile şirket içi altyapınızı arasında bir düzenleyici gibi davranır. Bu makalede nasıl ayarlamak, yapılandırabilir ve hello yapılandırma sunucusu yönetmek açıklanmaktadır.

## <a name="prerequisites"></a>Ön koşullar
Merhaba en düşük donanım, yazılım ve ağ yapılandırma gerekli tooset bir yapılandırma sunucusu Hello aşağıda verilmiştir.

> [!NOTE]
> [Kapasite planlama](site-recovery-capacity-planner.md) hello yapılandırma sunucusu bir yapılandırma ile bu paketleri dağıtmak için önemli adım tooensure olan yük gereksinimlerinizi. Daha fazla bilgi edinin [yapılandırma sunucusu için gereksinimleri boyutlandırma](#sizing-requirements-for-a-configuration-server).

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-configuration-server-software"></a>Merhaba yapılandırma sunucusu yazılım indirme
1. Toohello üzerinde Azure portal ve göz atma tooyour kurtarma Hizmetleri kasası oturum açın.
2. Çok Gözat**Site Recovery altyapısı** > **yapılandırma sunucularına** (altında For VMware ve fiziksel makineler).

  ![Sunucuları Sayfası Ekle](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. Merhaba tıklatın **+ sunucuları** düğmesi.
4. Merhaba üzerinde **Sunucu Ekle** sayfasında, hello karşıdan yükleme düğmesini toodownload hello kayıt anahtar'ı tıklatın. Merhaba yapılandırma sunucusu yükleme tooregister sırasında bu anahtar gerekir Azure Site Recovery hizmeti ile.
5. Merhaba tıklatın **indirme hello Microsoft Azure Site Recovery birleşik Kurulumu** bağlantı toodownload hello en son sürümünü hello yapılandırma sunucusu.

  ![Sayfayı Yükle](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  Merhaba yapılandırma sunucusunun en son sürümünü, doğrudan indirilebilir [Microsoft Download Center indirme sayfası](http://aka.ms/unifiedsetup)

## <a name="installing-and-registering-a-configuration-server-from-gui"></a>Yükleme ve yapılandırma sunucusu GUI'den kaydetme
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a>Yükleme ve komut satırını kullanarak bir yapılandırma sunucusu kaydetme

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a>Örnek Kullanım
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a>Yapılandırma sunucusu Yükleyici komut satırı bağımsız değişkenleri.
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a>Bir MySql kimlik bilgileri dosyası oluşturma
MySQLCredsFilePath parametresi bir dosya girdi olarak alır. Aşağıdaki biçimlendirmek ve giriş MySQLCredsFilePath parametre olarak geçirmek hello kullanarak hello dosyası oluşturun.
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a>Proxy ayarlarını yapılandırma dosyası oluşturma
ProxySettingsFilePath parametresi bir dosya girdi olarak alır. Aşağıdaki biçimlendirmek ve giriş ProxySettingsFilePath parametre olarak geçirmek hello kullanarak hello dosyası oluşturun.

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a>Yapılandırma sunucusu için proxy ayarlarını değiştirme
1. Oturum açma tooyour yapılandırma sunucusu.
2. Merhaba kısayolunu kullanarak hello cspsconfigtool.exe başlatın.
3. Merhaba tıklatın **kasa kayıt** sekmesi.
4. Yeni bir kasa kayıt dosyası hello portalından indirin ve giriş toohello aracı olarak sağlayın.

  ![YAZMAÇ yapılandırma sunucusu](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. Merhaba yeni Proxy sunucusu ayrıntılarını sağlayın ve hello tıklatın **kaydetmek** düğmesi.
6. Bir yönetici PowerShell komut penceresi açın.
7. Merhaba aşağıdaki komutu çalıştırın
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  Varsa genişleme işlem sunucuları toothis yapılandırma sunucusu bağlı, çok gerek[hello proxy ayarları tüm hello genişleme işlem sunucularında düzeltme](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) dağıtımınızdaki.

## <a name="re-register-a-configuration-server-with-hello-same-recovery-services-vault"></a>Merhaba yapılandırma sunucusuyla yeniden kaydettirin aynı kurtarma Hizmetleri kasası
  1. Oturum açma tooyour yapılandırma sunucusu.
  2. Merhaba cspsconfigtool.exe masaüstünüzde Hello kısayolunu kullanarak başlatın.
  3. Merhaba tıklatın **kasa kayıt** sekmesi.
  4. Yeni bir kayıt dosyası hello portalından indirin ve giriş toohello aracı olarak sağlayın.
        ![YAZMAÇ yapılandırma sunucusu](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
  5. Merhaba Proxy sunucusu detayları sağlayın ve hello tıklatın **kaydetmek** düğmesi.  
  6. Bir yönetici PowerShell komut penceresi açın.
  7. Merhaba aşağıdaki komutu çalıştırın

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  Varsa genişleme işlem sunucuları toothis yapılandırma sunucusu bağlı, çok gerek[tüm hello genişleme işlem sunucuların yeniden kaydettirin](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) dağıtımınızdaki.

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a>Yapılandırma sunucusu farklı bir kurtarma Hizmetleri kasası ile kaydediliyor.
1. Oturum açma tooyour yapılandırma sunucusu.
2. bir yönetici komut isteminden hello komutunu çalıştırın

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. Merhaba kısayolunu kullanarak hello cspsconfigtool.exe başlatın.
4. Merhaba tıklatın **kasa kayıt** sekmesi.
5. Yeni bir kayıt dosyası hello portalından indirin ve giriş toohello aracı olarak sağlayın.

    ![YAZMAÇ yapılandırma sunucusu](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. Merhaba Proxy sunucusu detayları sağlayın ve hello tıklatın **kaydetmek** düğmesi.  
7. Bir yönetici PowerShell komut penceresi açın.
8. Merhaba aşağıdaki komutu çalıştırın
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a>Yapılandırma sunucusu yetkisini alma
Yapılandırma sunucusu yetkisini başlamadan önce hello aşağıdakilerden emin olun.
1. Bu yapılandırma sunucusu altındaki tüm sanal makineler için korumayı devre dışı bırakın.
2. Merhaba yapılandırma sunucusu gelen tüm çoğaltma ilkelerinin ilişkisini kaldırın.
3. İlişkili toohello yapılandırma sunucusu olan tüm Vcenter sunucularını/vSphere ana bilgisayarları silin.

### <a name="delete-hello-configuration-server-from-azure-portal"></a>Merhaba yapılandırma sunucusu Azure portalından Sil
1. Azure portalında çok Gözat**Site Recovery altyapısı** > **yapılandırma sunucularına** hello kasa menüsünden.
2. Hello yapılandırma toodecommission istediğiniz Server'ı tıklatın.
3. Merhaba yapılandırma sunucunun Ayrıntıları sayfasında hello Sil düğmesini tıklatın.

  ![Delete yapılandırma sunucusu](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. Tıklatın **Evet** hello sunucusunun tooconfirm hello silme.

  >[!WARNING]
  Herhangi bir sanal makine, çoğaltma ilkesi veya vCenter sunucuları/vSphere ana bu yapılandırma sunucusu ile ilişkili varsa, hello sunucu silinemez. Toodelete hello kasası çalışmadan önce bu varlıkları silin.

### <a name="uninstall-hello-configuration-server-software-and-its-dependencies"></a>Merhaba yapılandırma sunucusu yazılım ve bağımlılıklarını kaldırma
  > [!TIP]
  Tooreuse hello yapılandırma sunucusu Azure Site Recovery ile yeniden düşünüyorsanız, daha sonra toostep 4 doğrudan atlayabilirsiniz.

1. Yapılandırma sunucusu toohello üzerinde bir yönetici olarak oturum açın.
2. Denetim Masası açın > Program > programları Kaldır
3. Sıra aşağıdaki hello Hello programlarda kaldırın:
  * Microsoft Azure Kurtarma Hizmetleri Aracısı
  * Microsoft Azure Site Recovery Mobility hizmeti/ana hedef sunucu
  * Microsoft Azure Site Recovery sağlayıcısı
  * Microsoft Azure Site kurtarma yapılandırması sunucu/işlem sunucusu
  * Microsoft Azure Site kurtarma yapılandırması sunucu bağımlılıkları
  * MySQL Server 5.5
4. Komutunu aşağıdaki hello ve yönetici komut isteminden çalıştırın.
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a>Yapılandırma sunucusu Güvenli Yuva Layer(SSL) sertifikaları yenile
Merhaba mobilite hizmeti işlem sunucuları hello etkinliklerini düzenler bir yerleşik Web Hello yapılandırma sunucusu vardır ve ana hedef sunucuları toohello yapılandırma sunucusu bağlı. Merhaba yapılandırma sunucusunun Web sunucusu bir SSL sertifikası tooauthenticate istemcilerine kullanır. Bu sertifika geçerlilik süresi üç yıl sahiptir ve yöntemi aşağıdaki hello kullanarak herhangi bir zamanda yenilenebilir:

> [!WARNING]
Sertifika süre sonu yalnızca sürümünde gerçekleştirilebilir 9.4.XXXX. X veya daha yüksek. Tüm hello Azure Site Recovery bileşenleri (yapılandırma sunucusu, işlem sunucusu, ana hedef sunucusu, Mobility hizmeti) yükseltme hello sertifikaları yenilemek iş akışı başlamadan önce.

1. Üzerinde Azure portal Merhaba, tooyour kasası Gözat > Site Recovery altyapısı > yapılandırma sunucusu.
2. Hello yapılandırma toorenew ihtiyacınız sunucusu için SSL sertifikası hello.
3. Yapılandırma sunucusu durumu Hello altında hello SSL sertifikası süre sonu tarihini hello görebilirsiniz.
4. Merhaba tıklayarak yenileme hello sertifika **sertifikaları yenilemek** hello görüntü aşağıdaki gösterildiği gibi eylem:

  ![Delete yapılandırma sunucusu](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a>Güvenli Yuva Katmanı sertifika süre sonu uyarısı

> [!NOTE]
Merhaba Mayıs 2016 önce gerçekleşen tüm yüklemeleri için SSL sertifikasının geçerlilik ayarlandı tooone yıl. Sertifika süre sonu bildirimleri hello Azure portal gösteren görmesini başlattığınız.

1. Merhaba yapılandırma sunucunun SSL sertifikası sonraki iki ay hello tooexpire olacaksa, Azure portal hello & (abone toobe tooAzure Site Recovery bildirimleri gerekir) e-posta aracılığıyla kullanıcılara bildirme hello hizmetini başlatır. Size bir bildirim başlığı hello kasasının kaynak sayfasında görmeye başlayacaksınız.

  ![Sertifika bildirim](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. Merhaba başlık tooget hello sertifika süre sonu ilgili ek Ayrıntılar'ı tıklatın.

  ![Sertifika ayrıntıları](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  Eğer yerine bir **Şimdi Yenile** gördüğünüz düğmesi bir **Şimdi Yükselt** düğmesi. Bu, henüz yükseltilmiş too9.4.xxxx.x ya da daha yüksek sürüm edilmemiş bazı bileşenler, ortamınızdaki gelir.

## <a name="sizing-requirements-for-a-configuration-server"></a>Yapılandırma sunucusu için gereksinimleri boyutlandırma

| **CPU** | **Bellek** | **Önbellek disk boyutu** | **Veri değişikliği oranı** | **Korumalı makineler** |
| --- | --- | --- | --- | --- |
| 8 Vcpu'lar (2 yuva * @ 2,5 GHz 4 çekirdek) |16 GB |300 GB |500 GB veya daha az |100'den az makineler çoğaltılır. |
| 12 Vcpu'lar (2 yuva * 2,5 GHz @ 6 çekirdek) |18 GB |600 GB |500 GB too1 TB |100-150 makineler arasında çoğaltılır. |
| 16 Vcpu (2 yuva * 2,5 GHz @ 8 çekirdek) |32 GB |1 TB |1 TB too2 TB |150-200 makineler arasında çoğaltılır. |

  >[!TIP]
  Günlük veri dalgalanmasına 2 TB aşıyor veya 200'den fazla sanal makine tooreplicate planlama, toodeploy ek işlem sunucuları tooload hello çoğaltma trafiği dengelemek önerilir. Nasıl toodeploy genişleme işlem sunucular hakkında daha fazla bilgi edinin.


## <a name="common-issues"></a>Genel sorunlar
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
