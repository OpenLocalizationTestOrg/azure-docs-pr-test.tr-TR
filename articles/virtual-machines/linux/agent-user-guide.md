---
title: "aaaAzure Linux VM Aracısı genel bakış | Microsoft Docs"
description: "Bilgi nasıl tooinstall ve Linux Aracısı (waagent) toomanage Azure yapı denetleyicisi ile sanal makinenizin etkileşimi yapılandırın."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: e41de979-6d56-40b0-8916-895bf215ded6
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: szark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4e08c84d9205f4db7aae6fd1568ec1f15fba395c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-and-using-hello-azure-linux-agent"></a>Anlama ve hello Azure Linux Aracısı kullanma
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a>Giriş
Merhaba Microsoft Azure Linux Aracısı, Linux ve FreeBSD sağlama ve hello Azure yapı denetleyicisi VM etkileşim (waagent) yönetir. Linux ve FreeBSD Iaas dağıtımları için işlevselliği aşağıdaki hello sağlar:

> [!NOTE]
> Bkz: Hello Azure Linux Aracısı [Benioku](https://github.com/Azure/WALinuxAgent/blob/master/README.md) ek ayrıntılar için.
> 
> 

* **Görüntü sağlama**
  
  * Kullanıcı hesabı oluşturma
  * SSH kimlik doğrulama türlerini yapılandırma
  * SSH ortak anahtarları ve anahtar çiftleri dağıtımı
  * Ayar hello ana bilgisayar adı
  * Yayımlama hello ana bilgisayar adı toohello platform DNS
  * Raporlama SSH ana anahtar parmak izi toohello platformu
  * Kaynak Disk Yönetimi
  * Biçimlendirme ve hello kaynak diski takma
  * Takas alanı yapılandırma
* **Ağ**
  
  * Platform DHCP sunucularıyla yollar tooimprove uyumluluğu yönetir
  * Merhaba ağ arabirimi adı Hello kararlılığını sağlar
* **Çekirdek**
  
  * Sanal NUMA yapılandırır (çekirdek için devre dışı < 2.6.37)
  * Hyper-V entropi /dev/random için kullanır
  * SCSI zaman aşımı (uzak olabilir) hello kök aygıt için yapılandırır
* **Tanılama**
  
  * Konsol yeniden yönlendirme toohello seri bağlantı noktası
* **SCVMM dağıtımları**
  
  * Algılar ve Linux için hello VMM aracısının System Center Virtual Machine Manager 2012 R2 ortamında çalıştırırken bootstraps
* **VM uzantısı**
  
  * Linux VM (Iaas) tooenable yazılım ve yapılandırma automation'a Microsoft ve iş ortakları tarafından yazılan Bileşen Ekle
  * VM uzantısı başvurusu mantığınız [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)

## <a name="communication"></a>İletişim
Merhaba bilgi akışını hello platform toohello aracısından iki kanallar oluşur:

* Önyükleme zamanında DVD Iaas dağıtımları için eklendi. Bu DVD hello gerçek SSH keypairs dışındaki tüm sağlama bilgilerini içeren bir OVF uyumlu yapılandırma dosyası içerir.
* Bir REST API gösterme TCP uç noktası tooobtain dağıtım ve topoloji yapılandırması kullanılır.

## <a name="requirements"></a>Gereksinimler
Merhaba aşağıdaki sistemleri test edilmiş ve hello Azure Linux Aracısı ile toowork bilinen:

> [!NOTE]
> Bu liste hello resmi hello Microsoft Azure platformu, desteklenen sistemlerinde listesi burada açıklandığı gibi farklı olabilir: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)
> 
> 

* CoreOS
* CentOS 6.3 +
* Red Hat Enterprise Linux 6.7 +
* Debian 7.0 +
* Ubuntu 12.04 +
* openSUSE 12.3 +
* SLES 11 SP3 +
* Oracle Linux 6.4 +

Desteklenen diğer sistemleri:

* FreeBSD 10 + (Azure Linux Aracısı v2.0.10 +)

Merhaba Linux Aracısı sipariş toofunction bazı sistem paketler düzgün bir şekilde bağlıdır:

* Python 2.6 +
* OpenSSL 1.0 +
* OpenSSH 5.3 +
* Dosya sistemi yardımcı programları: sfdisk, fdisk, mkfs, parted
* Parola araçları: chpasswd, sudo
* Araçlar işleme metin: azaltılabilir, grep
* Ağ araçları: IP yönlendirme
* Çekirdek desteği UDF bağlanan dosya sistemlerinin bağlanması için.

## <a name="installation"></a>Yükleme
Bir RPM ya da bir DEB paketi dağıtımınızı ait paket depodan kullanarak yükleme hello Azure Linux Aracısı yükseltme ve yükleme hello tercih edilen yöntemdir. Tüm hello [dağıtım sağlayıcıları destekli](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) hello Azure Linux Aracısı paketi depoları ve görüntüleri tümleştirin.

Merhaba toohello belgelerine başvurun [Azure Linux Aracısı bağlantıların github'da](https://github.com/Azure/WALinuxAgent) kaynak veya toocustom konumu veya ön yükleme gibi gelişmiş yükleme seçenekleri için.

## <a name="command-line-options"></a>Komut satırı seçenekleri
### <a name="flags"></a>Bayrakları
* ayrıntılı: Belirtilen komut dosyasının ayrıntı düzeyini artırın
* Zorla: Bazı komutlar için etkileşimli Onayı Atla

### <a name="commands"></a>Komutlar
* Yardım: desteklenen hello komutları ve bayrakları listeler.
* deprovision: tooclean hello sistem deneyin ve yeniden sağlama için uygun yapın. Bu işlem hello aşağıdaki silindi:
  
  * (Provisioning.RegenerateSshHostKeyPair hello yapılandırma dosyasındaki ' y' ise) tüm SSH konak anahtarları
  * /Etc/resolv.conf ad sunucusu yapılandırma
  * Kök paroladan (Provisioning.DeleteRootPassword hello yapılandırma dosyasındaki ' y' ise) eşitleme
  * Önbelleğe alınan DHCP istemci kiraları
  * Sıfırlama ana bilgisayar adı toolocalhost.localdomain

> [!WARNING]
> Sağlama kaldırma, hello görüntü tüm hassas bilgilerin temizlenmiş ve yeniden dağıtım için uygun olacağını garanti etmez.
> 
> 

* deprovision + kullanıcı: altında - deprovision (yukarıda) her şeyi gerçekleştirir ve ayrıca (/var/lib/waagent elde edilen) hello son sağlanan kullanıcının hesabını siler ve veri ilişkilendirilmiş. Bu parametre, yakalanan ve yeniden kullanılabilir, böylece Azure üzerinde önceden sağlama bir görüntü XML'deki sağlamada olur.
* Sürüm: görüntüler hello waagent sürümü
* serialconsole: kaz toomark ttyS0 yapılandırır (Merhaba ilk seri bağlantı noktası) hello önyükleme konsolu olarak. Bu çekirdek önyükleme günlüklerini toothe seri bağlantı noktasına gönderilen ve hata ayıklama için kullanılabilir hale sağlar.
* arka plan programı: arka plan programı toomanage etkileşim hello platform olarak waagent çalıştırın. Bu değişken hello waagent init komut dosyasında belirtilen toowaagent değeri.
* Başlat: waagent arka plan işlemi olarak çalıştır

## <a name="configuration"></a>Yapılandırma
Bir yapılandırma dosyası (/ etc/waagent.conf) denetimleri hello waagent eylemler. Örnek bir yapılandırma dosyası aşağıda verilmiştir:

    Provisioning.Enabled=y
    Provisioning.DeleteRootPassword=n
    Provisioning.RegenerateSshHostKeyPair=y
    Provisioning.SshHostKeyPairType=rsa
    Provisioning.MonitorHostName=y
    Provisioning.DecodeCustomData=n
    Provisioning.ExecuteCustomData=n
    Provisioning.PasswordCryptId=6
    Provisioning.PasswordCryptSaltLength=10
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.MountOptions=None
    ResourceDisk.EnableSwap=n
    ResourceDisk.SwapSizeMB=0
    LBProbeResponder=y
    Logs.Verbose=n
    OS.RootDeviceScsiTimeout=300
    OS.OpensslPath=None
    HttpProxy.Host=None
    HttpProxy.Port=None

Merhaba çeşitli yapılandırma seçenekleri aşağıda ayrıntılı olarak açıklanmıştır. Yapılandırma seçenekleri üç tür içindedir; Boolean, String veya tamsayı. Merhaba Boolean yapılandırma seçenekleri "y" veya "n" belirtilebilir. özel anahtar sözcüğü "Hiçbiri" bazı dize türü için yapılandırma girdileri ayrıntılı olarak aşağıdaki kullanılabilir hello.

**Provisioning.Enabled:**  
Tür: Boolean  
Varsayılan: y

Bu hello kullanıcı tooenable izin verir veya hello Aracısı işlevleri sağlama hello devre dışı bırakın. "Y" veya "n" değerler geçerlidir. Sağlama devre dışıysa, SSH ana bilgisayar ve kullanıcı anahtarları hello görüntüsündeki korunur ve hello Azure sağlama API belirtilen herhangi bir yapılandırma yok sayılır.

> [!NOTE]
> Merhaba `Provisioning.Enabled` parametre Varsayılanları çok "n" Ubuntu bulut görüntülerde, bulut init sağlamak için kullanın.
> 
> 

**Provisioning.DeleteRootPassword:**  
Tür: Boolean  
Varsayılan: n

Sağlama işlemi sırasında kümesi, hello kök dosyasında parolasını hello/etc/gölge silinmesi durumunda hello.

**Provisioning.RegenerateSshHostKeyPair:**  
Tür: Boolean  
Varsayılan: y

Merhaba işlemden/etc/ssh/sağlama sırasında kümesi, tüm SSH ana anahtar çifti (ecdsa, dsa ve rsa) silinmişse. Ve tek bir yeni anahtar çifti oluşturulur.

Merhaba şifreleme türü hello yeni anahtar çifti için Provisioning.SshHostKeyPairType girişi hello tarafından yapılandırılabilir. Merhaba SSH arka plan programı (örneğin, bir yeniden başlatma sırasında) yeniden başlatıldığında bazı dağıtımları eksik herhangi bir şifreleme türü için anahtar çiftleri SSH yeniden oluşturacağını unutmayın.

**Provisioning.SshHostKeyPairType:**  
Türü: Dize  
Varsayılan: rsa

Bu hello SSH arka plan hello sanal makine tarafından desteklenen tooan şifreleme algoritması türü ayarlayabilirsiniz. genellikle desteklenen hello "rsa", "dsa" ve "ecdsa" değerlerdir. "Putty.exe" Windows "ecdsa" desteklemediğini unutmayın. Bu nedenle, Windows tooconnect tooa Linux dağıtım üzerinde toouse putty.exe düşünüyorsanız, lütfen "rsa" veya "dsa" kullanın.

**Provisioning.MonitorHostName:**  
Tür: Boolean  
Varsayılan: y

Ayarlama, waagent hello Linux sanal makine ana bilgisayar adı değişiklikleri (Merhaba "hostname" komutu tarafından döndürülen gibi) izleyen ve otomatik olarak hello görüntü tooreflect hello değişikliği hello ağ yapılandırmasını güncelleştirin durumunda. Toohello DNS sunucuları sipariş toopush hello adını değiştirmek için ağ hello sanal makine yeniden başlatılır. Bu kısaca Internet bağlantısı kaybedilmesine neden olur.

**Provisioning.DecodeCustomData**  
Tür: Boolean  
Varsayılan: n

Ayarlama, waagent CustomData Base64 gelen kod çözme varsa.

**Provisioning.ExecuteCustomData**  
Tür: Boolean  
Varsayılan: n

Ayarlama, waagent CustomData sağladıktan sonra yürütecek varsa.

**Provisioning.PasswordCryptId**  
Türü: dize  
Varsayılan: 6

Parola karmasını oluştururken crypt tarafından kullanılan algoritma.  
 1 - MD5  
 2a - Blowfish  
 5 - SHA-256  
 6 - SHA-512  

**Provisioning.PasswordCryptSaltLength**  
Türü: dize  
Varsayılan: 10

Parola Karması oluşturulurken kullanılan rastgele salt uzunluğu.

**ResourceDisk.Format:**  
Tür: Boolean  
Varsayılan: y

Ayarlama, hello platform tarafından sağlanan hello kaynak disk biçimlendirilmiş ve olması hello filesystem türü "ResourceDisk.Filesystem" Merhaba kullanıcı tarafından istenen "ntfs" dışında bir şey ise waagent tarafından oluşturulmuş durumunda. Linux (83) türünde tek bir bölüm hello diskte kullanıma sunulacaktır. Başarıyla bağlanabiliyorsa'nın bu bölüm biçimlendirilmez unutmayın.

**ResourceDisk.Filesystem:**  
Türü: Dize  
Varsayılan: ext4

Bu hello kaynak disk hello filesystem türünü belirtir. Desteklenen değerler Linux dağıtım göre farklılık gösterir. Merhaba dize X, ardından mkfs ise. X hello Linux görüntüde mevcut olması. SLES 11 görüntüleri genellikle 'ext3' kullanmanız gerekir. FreeBSD görüntüleri 'ufs2' burada kullanmanız gerekir.

**ResourceDisk.MountPoint:**  
Türü: Dize  
Varsayılan: / mnt/kaynak 

Bu hello kaynak disk bağlı hello yolunu belirtir. Bu hello kaynak diski Not bir *geçici* disk ve hello VM deprovisioned olduğunda boşaltılabilir.

**ResourceDisk.MountOptions**  
Türü: Dize  
Varsayılan: yok

Disk bağlama seçenekleri geçirilen toobe toohello mount -o komutu belirtir. Değer, virgülle ayrılmış listesi ex budur. 'nodev, nosuid'. Mount(8) Ayrıntılar için bkz.

**ResourceDisk.EnableSwap:**  
Tür: Boolean  
Varsayılan: n

Varsa bir takas dosyası ayarı (/ swapfile) hello kaynak disk üzerinde oluşturulur ve toohello sistem takas alanı eklenir.

**ResourceDisk.SwapSizeMB:**  
Türü: tamsayı  
Varsayılan: 0

Merhaba hello takas dosyası megabayt cinsinden büyüklüğü.

**Logs.Verbose:**  
Tür: Boolean  
Varsayılan: n

Kümesi, günlük ayrıntı boosted durumunda. Waagent too/var/log/waagent.log günlüğe kaydeder ve hello sistem logrotate işlevselliği toorotate günlüklerini yararlanır.

**İŞLETİM SİSTEMİ. EnableRDMA**  
Tür: Boolean  
Varsayılan: n

Ayarlama, hello aracı tooinstall denemek ve donanım temel hello hello bellenimini hello sürümüyle eşleşen bir RDMA çekirdek sürücüsü yüklemek durumunda.

**İŞLETİM SİSTEMİ. RootDeviceScsiTimeout:**  
Türü: tamsayı  
Varsayılan: 300

Bu, hello SCSI zaman aşımı saniye hello işletim sistemi diski ve veri sürücülerinde yapılandırır. Aksi durumda ayarlamak, hello sistem varsayılan değerler kullanılır.

**İŞLETİM SİSTEMİ. OpensslPath:**  
Türü: Dize  
Varsayılan: yok

Bu, kullanılan toospecify hello openssl ikili toouse şifreleme işlemleri için alternatif bir yol olabilir.

**HttpProxy.Host, HttpProxy.Port**  
Türü: Dize  
Varsayılan: yok

Ayarlama, hello Aracısı bu proxy kullanıp kullanmayacağını sunucu tooaccess hello Internet. 

## <a name="ubuntu-cloud-images"></a>Ubuntu bulut görüntüleri
Ubuntu bulut görüntüleri kullanma Not [bulut init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform tarafından yönetilmesi birçok yapılandırma görevleri hello Azure Linux Aracısı.  Lütfen aşağıdaki farkları hello dikkat edin:

* **Provisioning.Enabled** Varsayılanları "Çok Ubuntu bulut görüntülerinde görevleri sağlama bulut init tooperform kullanan n".
* yapılandırma parametreleri aşağıdaki hello Ubuntu bulut görüntüleri'de, disk ve takas bulut init toomanage hello kaynak alanı kullanmak üzerinde hiçbir etkisi yoktur:
  
  * **ResourceDisk.Format**
  * **ResourceDisk.Filesystem**
  * **ResourceDisk.MountPoint**
  * **ResourceDisk.EnableSwap**
  * **ResourceDisk.SwapSizeMB**
* Lütfen kaynakları tooconfigure hello kaynak disk bağlama noktası aşağıdaki hello bakın ve sağlama işlemi sırasında değiştirme alanı Ubuntu bulut görüntülerinde:
  
  * [Ubuntu Wiki: Takas bölümlerini yapılandırma](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [Bir Azure sanal makinesine özel veri injecting](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

