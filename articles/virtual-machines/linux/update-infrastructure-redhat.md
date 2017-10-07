---
title: "aaaRed Hat güncelleştirme altyapısı (RHUI) | Microsoft Docs"
description: "Microsoft Azure isteğe bağlı Red Hat Enterprise Linux örneklerinin Red Hat güncelleştirme altyapısı (RHUI) hakkında bilgi edinin"
services: virtual-machines-linux
documentationcenter: 
author: BorisB2015
manager: timlt
editor: 
ms.assetid: f495f1b4-ae24-46b9-8d26-c617ce3daf3a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/13/2017
ms.author: borisb
ms.openlocfilehash: cc244857104b25e4e61862c518db77e915e137ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a>Red Hat güncelleştirme altyapısı (RHUI) isteğe bağlı Red Hat Enterprise Linux VM'ler için Azure'da için
Sanal makine hello isteğe bağlı Red Hat Enterprise Linux (RHEL) görüntülerde kullanılabilir Azure Marketi oluşturulan kayıtlı tooaccess hello Red Hat güncelleştirme altyapısı (RHUI) Azure'de dağıtılan yok.  erişim tooa bölgesel yum depo ve mümkün tooreceive artımlı güncelleştirmeler Hello isteğe bağlı RHEL örneğe sahip.

RHUI tarafından yönetilen, hello yum deposu listesi RHEL örneğinizi sağlama işlemi sırasında yapılandırılır. Çalıştıran herhangi bir ek yapılandırma - toodo gerekmeyen `yum update` RHEL örneğinizi hazır tooget hello en son güncelleştirmeleri sonra.

> [!NOTE]
> Eylül 2016'da güncelleştirilmiş bir Azure RHUI dağıttığımız ve Ocak 2017 biz Merhaba, aşamalı kapatma işlemi başlatıldı eski Azure RHUI. Hiçbir eylem, hello RHEL resimlerinin (ya da kendi anlık görüntüler) Eylül 2016 veya sonraki - olasılıkla kullanıyorsanız gereklidir. Ancak, eski anlık görüntüleri/VMs varsa yapılandırmalarını kesintisiz erişim toohello Azure RHUI güncelleştirilmiş toobe gerekir.
> 

## <a name="rhui-azure-infrastructure-update"></a>RHUI Azure Altyapı Güncelleştirmesi
Eylül 2016 itibariyle Azure Red Hat güncelleştirme altyapısı (RHUI) sunucuları yeni bir dizi vardır. Bu sunucular ile dağıtılan [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) böylece tek bir uç noktası (rhui-1.microsoft.com) bölge bağımsız olarak herhangi bir VM tarafından kullanılabilir. Yeni RHEL Kullandıkça Öde (PAYG) görüntüleri hello Azure Marketi (Eylül 2016 tarihli veya sonraki sürümler) noktası toohello yeni Azure RHUI sunucularında hello ve başka bir eylem gerekli değil.

### <a name="determine-if-action-is-required"></a>Eylem gerekli olup olmadığını belirler
Azure RHEL PAYG VM'den tooAzure RHUI bağlanırken sorun yaşıyorsanız, aşağıdaki adımları izleyin
1. Azure RHUI uç noktası için VM yapılandırmasını inceleyin.

    Olup olmadığını denetleyin `/etc/yum.repos.d/rh-cloud.repo` dosyasını içeren başvuru çok`rhui-[1-3].microsoft.com` baseurl içinde `[rhui-microsoft-azure-rhel*]` hello dosyasının bölümü. Bu - kullanmakta olduğunuz, yeni Azure RHUI hello.

    Varsa, desen aşağıdaki hello ile tooa konumuna işaret eden `mirrorlist.*cds[1-4].cloudapp.net` -hello yapılandırmasını güncelleştirme gereklidir.

    Merhaba yeni yapılandırma kullanıyorsanız ve hala tooAzure RHUI - bağlanamıyor Microsoft ya da Red Hat destek talebi dosya.

    > [!NOTE]
    > Erişim tooAzure barındırılan RHUI olduğu sınırlı toohello VM'ler içinde [Microsoft Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/details.aspx?id=41653).
    > 

2. Merhaba eski Azure RHUI bu denetleme ve tooautomatically güncelleştirme hello yapılandırmasını istediğiniz hala kullanılabilir ise, komutu aşağıdaki hello yürütün:

    `sudo yum update RHEL6`veya `sudo yum update RHEL7` hello RHEL ailesi sürümüne bağlı olarak.

3. Toohello artık bağlanabiliyorsa eski Azure RHUI, izleme hello el ile yapılacak adımlar hello sonraki bölümde açıklanmaktadır.

4. Görüntü/anlık görüntü hello kaynak tooupdate hello yapılandırmasına etkilenen VM emin olun gelen sağlandı.

### <a name="phased-shutdown-of-hello-old-azure-rhui"></a>Aşamalı kapatılması hello eski Azure RHUI
Merhaba Hello kapatma sırasında eski Azure biz kısıtlamak RHUI erişim tooit gibi:

1. Daha fazla erişim (ACL) tooset tooit zaten bağlanan IP adreslerinin kısıtlayın. Olası yan etkileri: kullanarak devam ederseniz eski Azure RHUI hello - yeni VM'ler mümkün tooconnect tooit olmayabilir. RHEL VM'ler dinamik IP ile kapatma/ayırması/başlangıç dizisi Git yeni IP alabilirsiniz ve bu nedenle de tooconnect toohello başarısız başlatamadığından eski Azure RHUI

2. Yansıma içerik teslim sunucuları kapatma. Olası yan etkileri: size daha fazla CDSes kapatmak gibi artık görebilirsiniz `yum update` toohello artık bağlanabildiğinizde hello kadar daha fazla zaman aşımları zaman bakım, noktası eski Azure RHUI.

### <a name="hello-ips-for-hello-new-rhui-content-delivery-servers-are"></a>Merhaba IP'leri hello yeni RHUI içerik teslim sunucuları için olan
Ağ yapılandırma toofurther kullanıyorsanız RHEL PAYG Vm'lerden erişimi kısıtlamak, IP'leri aşağıdaki hello için kullanılabilir olduğundan emin olun `yum update` toowork bulunduğunuz hello ortamına bağlı olarak. 

```
# Azure Global
13.91.47.76
40.85.190.91
52.187.75.218
52.174.163.213

# Azure US Government
13.72.186.193

# Azure Germany
51.5.243.77
51.4.228.145
```

### <a name="manual-update-procedure-toouse-hello-new-azure-rhui-servers"></a>El ile güncelleştirme yordamı toouse hello yeni Azure RHUI sunucuları
Yükleme (curl) aracılığıyla hello ortak anahtarı imza

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

İndirilen hello anahtarını doğrulayın

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

Merhaba çıktısını denetleyin, doğrulayın `keyid` ve `user ID packet`:

```bash
Version: GnuPG v1.4.7 (GNU/Linux)
:public key packet:
        version 4, algo 1, created 1446074508, expires 0
        pkey[0]: [2048 bits]
        pkey[1]: [17 bits]
        keyid: EB3E94ADBE1229CF
:user ID packet: "Microsoft (Release signing) <gpgsecurity@microsoft.com>"
:signature packet: algo 1, keyid EB3E94ADBE1229CF
        version 4, created 1446074508, md5len 0, sigclass 0x13
        digest algo 2, begin of digest 1a 9b
        hashed subpkt 2 len 4 (sig created 2015-10-28)
        hashed subpkt 27 len 1 (key flags: 03)
        hashed subpkt 11 len 5 (pref-sym-algos: 9 8 7 3 2)
        hashed subpkt 21 len 3 (pref-hash-algos: 2 8 3)
        hashed subpkt 22 len 2 (pref-zip-algos: 2 1)
        hashed subpkt 30 len 1 (features: 01)
        hashed subpkt 23 len 1 (key server preferences: 80)
        subpkt 16 len 8 (issuer key ID EB3E94ADBE1229CF)
        data: [2047 bits]
```

Merhaba ortak anahtarı yükleyin

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

Karşıdan yükle, doğrulamak ve istemci RPM yüklemek

İndirin: RHEL 6

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

RHEL 7

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

Doğrulayın:

```bash
rpm -Kv azureclient.rpm
```

Bu imza çıktısında denetleyin hello Tamam paketidir

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

Merhaba RPM yükleyin

```bash
sudo rpm -U azureclient.rpm
```

Tamamlandıktan sonra Azure RHUI form hello VM erişebildiğinizden emin olun

### <a name="all-in-one-script-for-automating-hello-preceding-task"></a>Görev önceki hello otomatikleştirmek için hepsi bir arada komut dosyası
Etkilenen VM'ler toohello yeni Azure RHUI sunucuların güncelleştirme gerekli tooautomate hello görev olarak komut dosyası izleyen hello kullanın.

```sh
# Download key
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 

# Validate key
if ! gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release | grep -q "keyid: EB3E94ADBE1229CF"; then
    echo "Keyfile azure.asc NOT valid. Exiting."
    exit 1
fi

# Install Key
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release

# Download RPM package
if grep -q "release 7" /etc/redhat-release; then
    ver=7
elif  grep -q "release 6" /etc/redhat-release; then
    ver=6
else
    echo "Version not supported, exiting"
    exit 1
fi

url=https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel$ver/rhui-azure-rhel$ver-2.0-2.noarch.rpm
curl -o azureclient.rpm "$url"

# Verify package
if ! rpm -Kv azureclient.rpm | grep -q "key ID be1229cf: OK"; then
    echo "RPM failed validation ($url)"
    exit 1
fi

# Install package
sudo rpm -U azureclient.rpm
```

## <a name="rhui-overview"></a>RHUI genel bakış
[Red Hat güncelleştirme altyapısını](https://access.redhat.com/products/red-hat-update-infrastructure) Red Hat sertifikalı bulut sağlayıcıları tarafından barındırılan Red Hat Enterprise Linux bulut örnekleri için yüksek oranda ölçeklenebilir bir çözüm toomanage yum depo içeriğini sunar. Merhaba Yukarı Akış Pulp projesini temel alan, RHUI bulut sağlayıcıları toolocally yansıtma Red Hat barındırılan depo içeriğini sağlar, kendi içerikle özel depoları oluşturmak ve bu depoları kullanılabilir tooa büyük grubunu yük dengeli son kullanıcılara yapın İçerik teslim sistemi.

## <a name="regions-where-rhui-is-available"></a>RHUI kullanılabilir olduğu bölgeleri
RHUI RHEL isteğe bağlı görüntüleri kullanılabildiği tüm bölgelerde kullanılabilir. Şu anda üzerinde hello listelenen tüm genel bölgeler içeren [Azure durum Panosu](https://azure.microsoft.com/status/) sayfa, Azure ABD devlet kurumları ve Azure Almanya bölgeleri. RHUI erişim RHEL isteğe bağlı görüntülerden sağlanan VM'ler için kendi fiyatına dahil edilir. Biz hello gelecekteki RHEL isteğe bağlı kullanılabilirlik genişletin gibi ek bölge/Ulusal bulut kullanılabilirlik güncelleştirilir.

> [!NOTE]
> Erişim tooAzure barındırılan RHUI olduğu sınırlı toohello VM'ler içinde [Microsoft Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/details.aspx?id=41653).
> 
> 

## <a name="get-updates-from-another-update-repository"></a>Başka bir güncelleştirme depodan güncelleştirmeleri al
İlk tooget güncelleştirmeleri (yerine Azure barındırılan RHUI) farklı güncelleştirme depodan gerekiyorsa, RHUI, örneklerden toounregister gerekir. Yeniden kayıt toore gerekiyor (Red Hat uydu veya Red Hat müşteri portalı CDN gibi) hello istenen güncelleştirme altyapısıyla bunları. Bu hizmetler için Red Hat abonelikleri ve kayıt için uygun [Red Hat bulut erişimi azure'da](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).

toounregister RHUI ve yeniden kaydedin tooyour güncelleştirme Altyapısı şu adımları izleyin:

1. /Etc/yum.repos.d/RH-cloud.repo düzenleyin ve tüm değiştirin `enabled=1` çok`enabled=0`. Örneğin:
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. /Etc/yum/pluginconf.d/rhnplugin.conf düzenler ve değiştirirseniz `enabled=0` çok`enabled=1`.
3. Red Hat müşteri portalı gibi hello istenen altyapısı ile sonra kaydedin. Red Hat çözüm Kılavuzu izleyin [nasıl tooregister ve sistem toohello Red Hat müşteri portalı abone](https://access.redhat.com/solutions/253273).

> [!NOTE]
> Erişim toohello Azure barındırılan RHUI hello RHEL Kullandıkça Öde (PAYG) görüntüsü fiyatına dahil edilir. Hello Azure barındırılan RHUI PAYG RHEL VM'den kaydını hello sanal makine Getir bilgisayarınızı-kendi-lisans (KLG) türüne VM dönüştürmez. Kayıt, aynı VM hello başka bir güncelleştirme kaynağı ile çift ücretlerinin yansıtılmasını: ilk Red Hat aboneliği için ikinci kez saat Azure RHEL yazılım ücret ve hello için. 
> 
> Toouse tutarlı bir şekilde gerekiyorsa Azure barındırılan RHUI dışında bir güncelleştirme altyapısı düşünün oluşturma ve açıklandığı gibi kendi (KLG-türü) görüntüleri dağıtma [oluşturma ve karşıya Red Hat tabanlı sanal makine için Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) makalesi.
> 

## <a name="next-steps"></a>Sonraki adımlar
toocreate bir Red Hat Enterprise Linux VM Azure Market Kullandıkça Öde görüntü ve Dengeleme Azure barındırılan RHUI Git çok[Azure Marketi](https://azure.microsoft.com/marketplace/partners/redhat/). Mümkün toouse olacaktır `yum update` herhangi bir ek ayar olmadan RHEL Örneğinizde.

