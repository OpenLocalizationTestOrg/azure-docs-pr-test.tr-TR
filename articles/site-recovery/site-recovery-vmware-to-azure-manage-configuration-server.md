---
title: " Yapılandırma sunucusu Azure Site kurtarma yönetme | Microsoft Docs"
description: "Bu makalede, ayarlama ve yapılandırma sunucusunu yönetmek açıklar."
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
ms.openlocfilehash: 36da8c7d0f3ace194522e5288f26069cf46d470e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-configuration-server"></a>Yapılandırma sunucusu yönetme

Yapılandırma sunucusu Site kurtarma Hizmetleri ile şirket içi altyapınızı arasında bir düzenleyici gibi davranır. Bu makalede nasıl ayarlamak, yapılandırabilir ve yapılandırma sunucusunu yönetmek açıklanmaktadır.

## <a name="prerequisites"></a>Ön koşullar
En düşük donanım, yazılım ve yapılandırma sunucusu kurmak için gerekli ağ yapılandırması şunlardır:

> [!NOTE]
> [Kapasite planlama](site-recovery-capacity-planner.md) yapılandırmasıyla yapılandırma sunucusu bu paketleri dağıtmak emin olmak için önemli bir adım yük gereksinimlerinizi. Daha fazla bilgi edinin [yapılandırma sunucusu için gereksinimleri boyutlandırma](#sizing-requirements-for-a-configuration-server).

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-the-configuration-server-software"></a>Yapılandırma sunucusu yazılım indirme
1. Azure portalında oturum açın ve kurtarma Hizmetleri Kasası'na göz atın.
2. Gözat **Site Recovery altyapısı** > **yapılandırma sunucularına** (altında VMware ve fiziksel makineler için).

  ![Sunucuları Sayfası Ekle](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. Tıklatın **+ sunucuları** düğmesi.
4. Üzerinde **Sunucu Ekle** sayfasında, kayıt anahtarını indirin için karşıdan yükleme düğmesini tıklatın. Azure Site Recovery hizmeti ile kaydetmek için yapılandırma sunucusu yüklemesi sırasında bu anahtar gerekir.
5. Tıklatın **Microsoft Azure Site Recovery birleşik Kurulumu karşıdan** yapılandırma sunucusunun en son sürümünü indirmek için bağlantı.

  ![Sayfayı Yükle](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  Yapılandırma sunucusunun en son sürümünü, doğrudan indirilebilir [Microsoft Download Center indirme sayfası](http://aka.ms/unifiedsetup)

## <a name="installing-and-registering-a-configuration-server-from-gui"></a>Yükleme ve yapılandırma sunucusu GUI'den kaydetme
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a>Yükleme ve komut satırını kullanarak bir yapılandırma sunucusu kaydetme

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]
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
MySQLCredsFilePath parametresi bir dosya girdi olarak alır. Aşağıdaki biçimi kullanarak dosya oluşturma ve giriş MySQLCredsFilePath parametresi olarak geçirin.
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a>Proxy ayarlarını yapılandırma dosyası oluşturma
ProxySettingsFilePath parametresi bir dosya girdi olarak alır. Aşağıdaki biçimi kullanarak dosya oluşturma ve giriş ProxySettingsFilePath parametresi olarak geçirin.

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a>Yapılandırma sunucusu için proxy ayarlarını değiştirme
1. Yapılandırma sunucusu oturum açın.
2. Kısayol kullanarak cspsconfigtool.exe başlatın.
3. Tıklatın **kasa kayıt** sekmesi.
4. Portaldan yeni bir kasa kayıt dosyasını indirin ve aracı giriş olarak sağlayın.

  ![YAZMAÇ yapılandırma sunucusu](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. Yeni Proxy sunucu bilgileri sağlayın ve tıklatın **kaydetmek** düğmesi.
6. Bir yönetici PowerShell komut penceresi açın.
7. Aşağıdaki komutu çalıştırın
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  Bu yapılandırma sunucusuna bağlı genişleme işlem sunucularınız varsa, gerek [proxy ayarları tüm genişleme işlem sunucularındaki düzeltme](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) dağıtımınızdaki.

## <a name="re-register-a-configuration-server-with-the-same-recovery-services-vault"></a>Aynı kurtarma Hizmetleri kasası ile yapılandırma sunucusunu yeniden kaydedin
  1. Yapılandırma sunucusu oturum açın.
  2. Masaüstünde kısayol kullanarak cspsconfigtool.exe başlatın.
  3. Tıklatın **kasa kayıt** sekmesi.
  4. Yeni bir kayıt dosyası portaldan indirmenizi ve aracı giriş olarak sağlayın.
        ![YAZMAÇ yapılandırma sunucusu](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
  5. Proxy sunucu bilgileri sağlayın ve tıklatın **kaydetmek** düğmesi.  
  6. Bir yönetici PowerShell komut penceresi açın.
  7. Aşağıdaki komutu çalıştırın

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  Bu yapılandırma sunucusuna bağlı genişleme işlem sunucularınız varsa, gerek [tüm genişleme işlem sunucuların yeniden kaydettirin](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) dağıtımınızdaki.

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a>Yapılandırma sunucusu farklı bir kurtarma Hizmetleri kasası ile kaydediliyor.
1. Yapılandırma sunucusu oturum açın.
2. bir yönetici komut isteminden komutunu çalıştırın

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. Kısayol kullanarak cspsconfigtool.exe başlatın.
4. Tıklatın **kasa kayıt** sekmesi.
5. Yeni bir kayıt dosyası portaldan indirmenizi ve aracı giriş olarak sağlayın.

    ![YAZMAÇ yapılandırma sunucusu](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. Proxy sunucu bilgileri sağlayın ve tıklatın **kaydetmek** düğmesi.  
7. Bir yönetici PowerShell komut penceresi açın.
8. Aşağıdaki komutu çalıştırın
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a>Yapılandırma sunucusu yetkisini alma
Yapılandırma sunucusu yetkisini başlamadan önce aşağıdakilerden emin olun.
1. Bu yapılandırma sunucusu altındaki tüm sanal makineler için korumayı devre dışı bırakın.
2. Yapılandırma sunucusundan tüm çoğaltma ilkelerinin ilişkisini kaldırın.
3. Yapılandırma sunucusu ilişkili tüm Vcenter sunucularını/vSphere ana silin.

### <a name="delete-the-configuration-server-from-azure-portal"></a>Yapılandırma sunucusu Azure portalından Sil
1. Azure Portal'da Gözat **Site Recovery altyapısı** > **yapılandırma sunucularına** kasa menüsünden.
2. Yetkisini istediğiniz yapılandırma sunucuya tıklayın.
3. Yapılandırma sunucusunun Ayrıntıları sayfasında Sil düğmesini tıklatın.

  ![Delete yapılandırma sunucusu](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. Tıklatın **Evet** sunucu silme işlemini onaylamak için.

  >[!WARNING]
  Herhangi bir sanal makine, çoğaltma ilkesi veya vCenter sunucuları/vSphere ana bu yapılandırma sunucusu ile ilişkili varsa, sunucu silinemez. Kasa silmeye çalışmadan önce bu varlıkları silin.

### <a name="uninstall-the-configuration-server-software-and-its-dependencies"></a>Yapılandırma sunucusu yazılım ve bağımlılıklarını kaldırma
  > [!TIP]
  Yapılandırma sunucusu Azure Site Recovery ile yeniden yeniden kullanmayı planlıyorsanız, daha sonra adım 4 doğrudan atlayabilirsiniz.

1. Yapılandırma sunucusunda bir yönetici olarak oturum açın.
2. Denetim Masası açın > Program > programları Kaldır
3. Aşağıdaki sırayla programları kaldırın:
  * Microsoft Azure Kurtarma Hizmetleri Aracısı
  * Microsoft Azure Site Recovery Mobility hizmeti/ana hedef sunucu
  * Microsoft Azure Site Recovery sağlayıcısı
  * Microsoft Azure Site kurtarma yapılandırması sunucu/işlem sunucusu
  * Microsoft Azure Site kurtarma yapılandırması sunucu bağımlılıkları
  * MySQL Server 5.5
4. Yönetici komut istemi ve aşağıdaki komutu çalıştırın.
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a>Yapılandırma sunucusu Güvenli Yuva Layer(SSL) sertifikaları yenile
Yapılandırma sunucusu yapılandırma sunucusuna bağlı Mobility hizmeti, işlemi sunucuları ve ana hedef sunucular etkinliklerini düzenler bir yerleşik Web sahiptir. Yapılandırma sunucusunun Web sunucusu, istemcilerin kimliğini doğrulamak için bir SSL sertifikası kullanır. Bu sertifika geçerlilik süresi üç yıl sahiptir ve aşağıdaki yöntemi kullanarak herhangi bir zamanda yenilenebilir:

> [!WARNING]
Sertifika süre sonu yalnızca sürümünde gerçekleştirilebilir 9.4.XXXX. X veya daha yüksek. Tüm Azure Site Recovery bileşenleri (yapılandırma sunucusu, işlem sunucusu, ana hedef sunucusu, Mobility hizmeti) yükseltme sertifikaları yenilemek iş akışı başlamadan önce.

1. Kasanız için Azure Portal'da Gözat > Site Recovery altyapısı > yapılandırma sunucusu.
2. SSL sertifikasını yenilemek gereken yapılandırma sunucusu tıklayın.
3. Yapılandırma sunucusu durumu altında için SSL sertifikası süre sonu tarihi görebilirsiniz.
4. Tıklayarak sertifikayı **sertifikaları yenilemek** aşağıdaki görüntüde gösterildiği gibi eylem:

  ![Delete yapılandırma sunucusu](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a>Güvenli Yuva Katmanı sertifika süre sonu uyarısı

> [!NOTE]
SSL sertifika geçerlilik Mayıs 2016 önce gerçekleşen tüm yüklemeleri için bir yıl ayarlandı. Sertifika süre sonu bildirimleri Azure portalında gösteren görmesini başlattığınız.

1. Yapılandırma sunucusunun SSL sertifikası sonraki iki ay içinde süresi dolacak şekilde olacaksa, Azure portal & (Azure Site Recovery bildirimlerine abone gerekir) e-posta aracılığıyla kullanıcılara bildirme hizmetini başlatır. Size bir bildirim başlığı Kasası'nın kaynak sayfasında görmeye başlayacaksınız.

  ![Sertifika bildirim](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. Sertifika süre sonu hakkında ek ayrıntıları almak için başlığını tıklatın.

  ![Sertifika ayrıntıları](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  Eğer yerine bir **Şimdi Yenile** gördüğünüz düğmesi bir **Şimdi Yükselt** düğmesi. Bu henüz 9.4.xxxx.x veya daha sonraki sürümler için yükseltilmemiş bazı bileşenler, ortamınızdaki gelir.

## <a name="sizing-requirements-for-a-configuration-server"></a>Yapılandırma sunucusu için gereksinimleri boyutlandırma

| **CPU** | **Bellek** | **Önbellek disk boyutu** | **Veri değişikliği oranı** | **Korumalı makineler** |
| --- | --- | --- | --- | --- |
| 8 Vcpu'lar (2 yuva * @ 2,5 GHz 4 çekirdek) |16 GB |300 GB |500 GB veya daha az |100'den az makineler çoğaltılır. |
| 12 Vcpu'lar (2 yuva * 2,5 GHz @ 6 çekirdek) |18 GB |600 GB |1 TB ' 500 GB |100-150 makineler arasında çoğaltılır. |
| 16 Vcpu (2 yuva * 2,5 GHz @ 8 çekirdek) |32 GB |1 TB |1 TB ile 2 TB |150-200 makineler arasında çoğaltılır. |

  >[!TIP]
  Günlük veri dalgalanmasına 2 TB aşıyor veya 200'den fazla sanal makineleri çoğaltmak planlama, çoğaltma trafiği dengelemek için ek işlem sunucusu dağıtmayı önerilir. Sunucularının genişleme işlem dağıtma hakkında daha fazla bilgi edinin.


## <a name="common-issues"></a>Genel sorunlar
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
