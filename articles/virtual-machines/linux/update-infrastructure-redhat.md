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
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a><span data-ttu-id="9f861-103">Red Hat güncelleştirme altyapısı (RHUI) isteğe bağlı Red Hat Enterprise Linux VM'ler için Azure'da için</span><span class="sxs-lookup"><span data-stu-id="9f861-103">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>
<span data-ttu-id="9f861-104">Sanal makine hello isteğe bağlı Red Hat Enterprise Linux (RHEL) görüntülerde kullanılabilir Azure Marketi oluşturulan kayıtlı tooaccess hello Red Hat güncelleştirme altyapısı (RHUI) Azure'de dağıtılan yok.</span><span class="sxs-lookup"><span data-stu-id="9f861-104">Virtual machines created from hello on-demand Red Hat Enterprise Linux (RHEL) images available in Azure Marketplace are registered tooaccess hello Red Hat Update Infrastructure (RHUI) deployed in Azure.</span></span>  <span data-ttu-id="9f861-105">erişim tooa bölgesel yum depo ve mümkün tooreceive artımlı güncelleştirmeler Hello isteğe bağlı RHEL örneğe sahip.</span><span class="sxs-lookup"><span data-stu-id="9f861-105">hello on-demand RHEL instances have access tooa regional yum repository and able tooreceive incremental updates.</span></span>

<span data-ttu-id="9f861-106">RHUI tarafından yönetilen, hello yum deposu listesi RHEL örneğinizi sağlama işlemi sırasında yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="9f861-106">hello yum repository list, which is managed by RHUI, is configured in your RHEL instance during provisioning.</span></span> <span data-ttu-id="9f861-107">Çalıştıran herhangi bir ek yapılandırma - toodo gerekmeyen `yum update` RHEL örneğinizi hazır tooget hello en son güncelleştirmeleri sonra.</span><span class="sxs-lookup"><span data-stu-id="9f861-107">You don't need toodo any additional configuration - run `yum update` after your RHEL instance is ready tooget hello latest updates.</span></span>

> [!NOTE]
> <span data-ttu-id="9f861-108">Eylül 2016'da güncelleştirilmiş bir Azure RHUI dağıttığımız ve Ocak 2017 biz Merhaba, aşamalı kapatma işlemi başlatıldı eski Azure RHUI.</span><span class="sxs-lookup"><span data-stu-id="9f861-108">In September 2016 we deployed an updated Azure RHUI and in January 2017 we started phased shutdown of hello older Azure RHUI.</span></span> <span data-ttu-id="9f861-109">Hiçbir eylem, hello RHEL resimlerinin (ya da kendi anlık görüntüler) Eylül 2016 veya sonraki - olasılıkla kullanıyorsanız gereklidir.</span><span class="sxs-lookup"><span data-stu-id="9f861-109">If you have been using hello RHEL images (or their snapshots) from September 2016 or later - likely no action is required.</span></span> <span data-ttu-id="9f861-110">Ancak, eski anlık görüntüleri/VMs varsa yapılandırmalarını kesintisiz erişim toohello Azure RHUI güncelleştirilmiş toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="9f861-110">If, however, you have older snapshots/VMs, their configuration needs toobe updated for uninterrupted access toohello Azure RHUI.</span></span>
> 

## <a name="rhui-azure-infrastructure-update"></a><span data-ttu-id="9f861-111">RHUI Azure Altyapı Güncelleştirmesi</span><span class="sxs-lookup"><span data-stu-id="9f861-111">RHUI Azure Infrastructure Update</span></span>
<span data-ttu-id="9f861-112">Eylül 2016 itibariyle Azure Red Hat güncelleştirme altyapısı (RHUI) sunucuları yeni bir dizi vardır.</span><span class="sxs-lookup"><span data-stu-id="9f861-112">As of September 2016, Azure has a new set of Red Hat Update Infrastructure (RHUI) servers.</span></span> <span data-ttu-id="9f861-113">Bu sunucular ile dağıtılan [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) böylece tek bir uç noktası (rhui-1.microsoft.com) bölge bağımsız olarak herhangi bir VM tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9f861-113">These servers are deployed with [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) so that a single endpoint (rhui-1.microsoft.com) can be used by any VM regardless of region.</span></span> <span data-ttu-id="9f861-114">Yeni RHEL Kullandıkça Öde (PAYG) görüntüleri hello Azure Marketi (Eylül 2016 tarihli veya sonraki sürümler) noktası toohello yeni Azure RHUI sunucularında hello ve başka bir eylem gerekli değil.</span><span class="sxs-lookup"><span data-stu-id="9f861-114">hello new RHEL Pay-As-You-Go (PAYG) images in hello Azure Marketplace (versions dated September 2016 or later) point toohello new Azure RHUI servers and do not require any additional action.</span></span>

### <a name="determine-if-action-is-required"></a><span data-ttu-id="9f861-115">Eylem gerekli olup olmadığını belirler</span><span class="sxs-lookup"><span data-stu-id="9f861-115">Determine if action is required</span></span>
<span data-ttu-id="9f861-116">Azure RHEL PAYG VM'den tooAzure RHUI bağlanırken sorun yaşıyorsanız, aşağıdaki adımları izleyin</span><span class="sxs-lookup"><span data-stu-id="9f861-116">If you are experiencing problems connecting tooAzure RHUI from your Azure RHEL PAYG VM, follow these steps</span></span>
1. <span data-ttu-id="9f861-117">Azure RHUI uç noktası için VM yapılandırmasını inceleyin.</span><span class="sxs-lookup"><span data-stu-id="9f861-117">Inspect VM configuration for Azure RHUI endpoint</span></span>

    <span data-ttu-id="9f861-118">Olup olmadığını denetleyin `/etc/yum.repos.d/rh-cloud.repo` dosyasını içeren başvuru çok`rhui-[1-3].microsoft.com` baseurl içinde `[rhui-microsoft-azure-rhel*]` hello dosyasının bölümü.</span><span class="sxs-lookup"><span data-stu-id="9f861-118">Check if `/etc/yum.repos.d/rh-cloud.repo` file contains reference too`rhui-[1-3].microsoft.com` in baseurl of `[rhui-microsoft-azure-rhel*]` section of hello file.</span></span> <span data-ttu-id="9f861-119">Bu - kullanmakta olduğunuz, yeni Azure RHUI hello.</span><span class="sxs-lookup"><span data-stu-id="9f861-119">If it is - you are using hello new Azure RHUI.</span></span>

    <span data-ttu-id="9f861-120">Varsa, desen aşağıdaki hello ile tooa konumuna işaret eden `mirrorlist.*cds[1-4].cloudapp.net` -hello yapılandırmasını güncelleştirme gereklidir.</span><span class="sxs-lookup"><span data-stu-id="9f861-120">If it pointing tooa location with hello following pattern `mirrorlist.*cds[1-4].cloudapp.net` - hello configuration update is required.</span></span>

    <span data-ttu-id="9f861-121">Merhaba yeni yapılandırma kullanıyorsanız ve hala tooAzure RHUI - bağlanamıyor Microsoft ya da Red Hat destek talebi dosya.</span><span class="sxs-lookup"><span data-stu-id="9f861-121">If you are using hello new configuration and still cannot connect tooAzure RHUI - file a support case with Microsoft or Red Hat.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9f861-122">Erişim tooAzure barındırılan RHUI olduğu sınırlı toohello VM'ler içinde [Microsoft Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="9f861-122">Access tooAzure-hosted RHUI is limited toohello VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
    > 

2. <span data-ttu-id="9f861-123">Merhaba eski Azure RHUI bu denetleme ve tooautomatically güncelleştirme hello yapılandırmasını istediğiniz hala kullanılabilir ise, komutu aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="9f861-123">If hello old Azure RHUI is still available when you do this check and you would like tooautomatically update hello configuration, execute hello following command:</span></span>

    <span data-ttu-id="9f861-124">`sudo yum update RHEL6`veya `sudo yum update RHEL7` hello RHEL ailesi sürümüne bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="9f861-124">`sudo yum update RHEL6` or `sudo yum update RHEL7` depending on hello RHEL family version.</span></span>

3. <span data-ttu-id="9f861-125">Toohello artık bağlanabiliyorsa eski Azure RHUI, izleme hello el ile yapılacak adımlar hello sonraki bölümde açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9f861-125">If you can no longer connect toohello old Azure RHUI, follow hello manual steps described in hello next section.</span></span>

4. <span data-ttu-id="9f861-126">Görüntü/anlık görüntü hello kaynak tooupdate hello yapılandırmasına etkilenen VM emin olun gelen sağlandı.</span><span class="sxs-lookup"><span data-stu-id="9f861-126">Make sure tooupdate hello configuration on hello source image/snapshot affected VM was provisioned from.</span></span>

### <a name="phased-shutdown-of-hello-old-azure-rhui"></a><span data-ttu-id="9f861-127">Aşamalı kapatılması hello eski Azure RHUI</span><span class="sxs-lookup"><span data-stu-id="9f861-127">Phased shutdown of hello old Azure RHUI</span></span>
<span data-ttu-id="9f861-128">Merhaba Hello kapatma sırasında eski Azure biz kısıtlamak RHUI erişim tooit gibi:</span><span class="sxs-lookup"><span data-stu-id="9f861-128">During hello shutdown of hello old Azure RHUI we restrict access tooit as follows:</span></span>

1. <span data-ttu-id="9f861-129">Daha fazla erişim (ACL) tooset tooit zaten bağlanan IP adreslerinin kısıtlayın.</span><span class="sxs-lookup"><span data-stu-id="9f861-129">Further restrict access (ACL) tooset of IP addresses that are already connecting tooit.</span></span> <span data-ttu-id="9f861-130">Olası yan etkileri: kullanarak devam ederseniz eski Azure RHUI hello - yeni VM'ler mümkün tooconnect tooit olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="9f861-130">Possible side-effects: if you continue using hello old Azure RHUI - your new VMs may not be able tooconnect tooit.</span></span> <span data-ttu-id="9f861-131">RHEL VM'ler dinamik IP ile kapatma/ayırması/başlangıç dizisi Git yeni IP alabilirsiniz ve bu nedenle de tooconnect toohello başarısız başlatamadığından eski Azure RHUI</span><span class="sxs-lookup"><span data-stu-id="9f861-131">RHEL VMs with dynamic IPs that go through shutdown/deallocate/start sequence may receive new IP and hence also could start failing tooconnect toohello old Azure RHUI</span></span>

2. <span data-ttu-id="9f861-132">Yansıma içerik teslim sunucuları kapatma.</span><span class="sxs-lookup"><span data-stu-id="9f861-132">Shutdown of mirror content delivery servers.</span></span> <span data-ttu-id="9f861-133">Olası yan etkileri: size daha fazla CDSes kapatmak gibi artık görebilirsiniz `yum update` toohello artık bağlanabildiğinizde hello kadar daha fazla zaman aşımları zaman bakım, noktası eski Azure RHUI.</span><span class="sxs-lookup"><span data-stu-id="9f861-133">Possible side-effects: as we shut down more CDSes you may see longer `yum update` servicing time, more timeouts up until hello point when you can no longer connect toohello old Azure RHUI.</span></span>

### <a name="hello-ips-for-hello-new-rhui-content-delivery-servers-are"></a><span data-ttu-id="9f861-134">Merhaba IP'leri hello yeni RHUI içerik teslim sunucuları için olan</span><span class="sxs-lookup"><span data-stu-id="9f861-134">hello IPs for hello new RHUI content delivery servers are</span></span>
<span data-ttu-id="9f861-135">Ağ yapılandırma toofurther kullanıyorsanız RHEL PAYG Vm'lerden erişimi kısıtlamak, IP'leri aşağıdaki hello için kullanılabilir olduğundan emin olun `yum update` toowork bulunduğunuz hello ortamına bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="9f861-135">If you are using network configuration toofurther restrict access from RHEL PAYG VMs, make sure hello following IPs are allowed for `yum update` toowork depending on hello environment you are in.</span></span> 

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

### <a name="manual-update-procedure-toouse-hello-new-azure-rhui-servers"></a><span data-ttu-id="9f861-136">El ile güncelleştirme yordamı toouse hello yeni Azure RHUI sunucuları</span><span class="sxs-lookup"><span data-stu-id="9f861-136">Manual update procedure toouse hello new Azure RHUI servers</span></span>
<span data-ttu-id="9f861-137">Yükleme (curl) aracılığıyla hello ortak anahtarı imza</span><span class="sxs-lookup"><span data-stu-id="9f861-137">Download (via curl) hello public key signature</span></span>

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

<span data-ttu-id="9f861-138">İndirilen hello anahtarını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="9f861-138">Verify hello downloaded key</span></span>

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="9f861-139">Merhaba çıktısını denetleyin, doğrulayın `keyid` ve `user ID packet`:</span><span class="sxs-lookup"><span data-stu-id="9f861-139">Check hello output, verify `keyid` and `user ID packet`:</span></span>

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

<span data-ttu-id="9f861-140">Merhaba ortak anahtarı yükleyin</span><span class="sxs-lookup"><span data-stu-id="9f861-140">Install hello public key</span></span>

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="9f861-141">Karşıdan yükle, doğrulamak ve istemci RPM yüklemek</span><span class="sxs-lookup"><span data-stu-id="9f861-141">Download, Verify, and Install Client RPM</span></span>

<span data-ttu-id="9f861-142">İndirin: RHEL 6</span><span class="sxs-lookup"><span data-stu-id="9f861-142">Download: For RHEL 6</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

<span data-ttu-id="9f861-143">RHEL 7</span><span class="sxs-lookup"><span data-stu-id="9f861-143">For RHEL 7</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

<span data-ttu-id="9f861-144">Doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="9f861-144">Verify:</span></span>

```bash
rpm -Kv azureclient.rpm
```

<span data-ttu-id="9f861-145">Bu imza çıktısında denetleyin hello Tamam paketidir</span><span class="sxs-lookup"><span data-stu-id="9f861-145">Check in output that signature of hello package is OK</span></span>

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

<span data-ttu-id="9f861-146">Merhaba RPM yükleyin</span><span class="sxs-lookup"><span data-stu-id="9f861-146">Install hello RPM</span></span>

```bash
sudo rpm -U azureclient.rpm
```

<span data-ttu-id="9f861-147">Tamamlandıktan sonra Azure RHUI form hello VM erişebildiğinizden emin olun</span><span class="sxs-lookup"><span data-stu-id="9f861-147">Upon completion, verify that you can access Azure RHUI form hello VM</span></span>

### <a name="all-in-one-script-for-automating-hello-preceding-task"></a><span data-ttu-id="9f861-148">Görev önceki hello otomatikleştirmek için hepsi bir arada komut dosyası</span><span class="sxs-lookup"><span data-stu-id="9f861-148">All-in-one script for automating hello preceding task</span></span>
<span data-ttu-id="9f861-149">Etkilenen VM'ler toohello yeni Azure RHUI sunucuların güncelleştirme gerekli tooautomate hello görev olarak komut dosyası izleyen hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="9f861-149">Use hello following script as needed tooautomate hello task of updating affected VMs toohello new Azure RHUI servers.</span></span>

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

## <a name="rhui-overview"></a><span data-ttu-id="9f861-150">RHUI genel bakış</span><span class="sxs-lookup"><span data-stu-id="9f861-150">RHUI overview</span></span>
<span data-ttu-id="9f861-151">[Red Hat güncelleştirme altyapısını](https://access.redhat.com/products/red-hat-update-infrastructure) Red Hat sertifikalı bulut sağlayıcıları tarafından barındırılan Red Hat Enterprise Linux bulut örnekleri için yüksek oranda ölçeklenebilir bir çözüm toomanage yum depo içeriğini sunar.</span><span class="sxs-lookup"><span data-stu-id="9f861-151">[Red Hat Update Infrastructure](https://access.redhat.com/products/red-hat-update-infrastructure) offers a highly scalable solution toomanage yum repository content for Red Hat Enterprise Linux cloud instances that are hosted by Red Hat-certified cloud providers.</span></span> <span data-ttu-id="9f861-152">Merhaba Yukarı Akış Pulp projesini temel alan, RHUI bulut sağlayıcıları toolocally yansıtma Red Hat barındırılan depo içeriğini sağlar, kendi içerikle özel depoları oluşturmak ve bu depoları kullanılabilir tooa büyük grubunu yük dengeli son kullanıcılara yapın İçerik teslim sistemi.</span><span class="sxs-lookup"><span data-stu-id="9f861-152">Based on hello upstream Pulp project, RHUI allows cloud providers toolocally mirror Red Hat-hosted repository content, create custom repositories with their own content, and make those repositories available tooa large group of end users through a load-balanced content delivery system.</span></span>

## <a name="regions-where-rhui-is-available"></a><span data-ttu-id="9f861-153">RHUI kullanılabilir olduğu bölgeleri</span><span class="sxs-lookup"><span data-stu-id="9f861-153">Regions where RHUI is available</span></span>
<span data-ttu-id="9f861-154">RHUI RHEL isteğe bağlı görüntüleri kullanılabildiği tüm bölgelerde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9f861-154">RHUI is available in all regions where RHEL on-demand images are available.</span></span> <span data-ttu-id="9f861-155">Şu anda üzerinde hello listelenen tüm genel bölgeler içeren [Azure durum Panosu](https://azure.microsoft.com/status/) sayfa, Azure ABD devlet kurumları ve Azure Almanya bölgeleri.</span><span class="sxs-lookup"><span data-stu-id="9f861-155">It currently includes all public regions listed on hello [Azure status dashboard](https://azure.microsoft.com/status/) page, Azure US Government and Azure Germany regions.</span></span> <span data-ttu-id="9f861-156">RHUI erişim RHEL isteğe bağlı görüntülerden sağlanan VM'ler için kendi fiyatına dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="9f861-156">RHUI access for VMs provisioned from RHEL on-demand images is included in their price.</span></span> <span data-ttu-id="9f861-157">Biz hello gelecekteki RHEL isteğe bağlı kullanılabilirlik genişletin gibi ek bölge/Ulusal bulut kullanılabilirlik güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="9f861-157">Additional regional/national cloud availability will be updated as we expand RHEL on-demand availability in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="9f861-158">Erişim tooAzure barındırılan RHUI olduğu sınırlı toohello VM'ler içinde [Microsoft Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="9f861-158">Access tooAzure-hosted RHUI is limited toohello VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
> 
> 

## <a name="get-updates-from-another-update-repository"></a><span data-ttu-id="9f861-159">Başka bir güncelleştirme depodan güncelleştirmeleri al</span><span class="sxs-lookup"><span data-stu-id="9f861-159">Get updates from another update repository</span></span>
<span data-ttu-id="9f861-160">İlk tooget güncelleştirmeleri (yerine Azure barındırılan RHUI) farklı güncelleştirme depodan gerekiyorsa, RHUI, örneklerden toounregister gerekir.</span><span class="sxs-lookup"><span data-stu-id="9f861-160">If you need tooget updates from a different update repository (instead of Azure-hosted RHUI), first you need toounregister your instances from RHUI.</span></span> <span data-ttu-id="9f861-161">Yeniden kayıt toore gerekiyor (Red Hat uydu veya Red Hat müşteri portalı CDN gibi) hello istenen güncelleştirme altyapısıyla bunları.</span><span class="sxs-lookup"><span data-stu-id="9f861-161">Then you need toore-register them with hello desired update infrastructure (such as Red Hat Satellite or Red Hat Customer Portal CDN).</span></span> <span data-ttu-id="9f861-162">Bu hizmetler için Red Hat abonelikleri ve kayıt için uygun [Red Hat bulut erişimi azure'da](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="9f861-162">You will need appropriate Red Hat subscriptions for these services and registration for [Red Hat Cloud Access in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span></span>

<span data-ttu-id="9f861-163">toounregister RHUI ve yeniden kaydedin tooyour güncelleştirme Altyapısı şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="9f861-163">toounregister RHUI and reregister tooyour update infrastructure follow these steps:</span></span>

1. <span data-ttu-id="9f861-164">/Etc/yum.repos.d/RH-cloud.repo düzenleyin ve tüm değiştirin `enabled=1` çok`enabled=0`.</span><span class="sxs-lookup"><span data-stu-id="9f861-164">Edit /etc/yum.repos.d/rh-cloud.repo and change all `enabled=1` too`enabled=0`.</span></span> <span data-ttu-id="9f861-165">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="9f861-165">For example:</span></span>
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. <span data-ttu-id="9f861-166">/Etc/yum/pluginconf.d/rhnplugin.conf düzenler ve değiştirirseniz `enabled=0` çok`enabled=1`.</span><span class="sxs-lookup"><span data-stu-id="9f861-166">Edit /etc/yum/pluginconf.d/rhnplugin.conf and change `enabled=0` too`enabled=1`.</span></span>
3. <span data-ttu-id="9f861-167">Red Hat müşteri portalı gibi hello istenen altyapısı ile sonra kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9f861-167">Then register with hello desired infrastructure, such as Red Hat Customer Portal.</span></span> <span data-ttu-id="9f861-168">Red Hat çözüm Kılavuzu izleyin [nasıl tooregister ve sistem toohello Red Hat müşteri portalı abone](https://access.redhat.com/solutions/253273).</span><span class="sxs-lookup"><span data-stu-id="9f861-168">Follow Red Hat solution guide on [how tooregister and subscribe a system toohello Red Hat Customer Portal](https://access.redhat.com/solutions/253273).</span></span>

> [!NOTE]
> <span data-ttu-id="9f861-169">Erişim toohello Azure barındırılan RHUI hello RHEL Kullandıkça Öde (PAYG) görüntüsü fiyatına dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="9f861-169">Access toohello Azure-hosted RHUI is included in hello RHEL Pay-As-You-Go (PAYG) image price.</span></span> <span data-ttu-id="9f861-170">Hello Azure barındırılan RHUI PAYG RHEL VM'den kaydını hello sanal makine Getir bilgisayarınızı-kendi-lisans (KLG) türüne VM dönüştürmez.</span><span class="sxs-lookup"><span data-stu-id="9f861-170">Unregistering a PAYG RHEL VM from hello Azure-hosted RHUI does not convert hello virtual machine into Bring-Your-Own-License (BYOL) type VM.</span></span> <span data-ttu-id="9f861-171">Kayıt, aynı VM hello başka bir güncelleştirme kaynağı ile çift ücretlerinin yansıtılmasını: ilk Red Hat aboneliği için ikinci kez saat Azure RHEL yazılım ücret ve hello için.</span><span class="sxs-lookup"><span data-stu-id="9f861-171">If you register hello same VM with another source of updates you may be incurring double charges: first time for Azure RHEL software fee, and hello second time for Red Hat subscription(s).</span></span> 
> 
> <span data-ttu-id="9f861-172">Toouse tutarlı bir şekilde gerekiyorsa Azure barındırılan RHUI dışında bir güncelleştirme altyapısı düşünün oluşturma ve açıklandığı gibi kendi (KLG-türü) görüntüleri dağıtma [oluşturma ve karşıya Red Hat tabanlı sanal makine için Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) makalesi.</span><span class="sxs-lookup"><span data-stu-id="9f861-172">If you consistently need toouse an update infrastructure other than Azure-hosted RHUI consider creating and deploying your own (BYOL-type) images as described in [Create and Upload Red Hat-based virtual machine for Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article.</span></span>
> 

## <a name="next-steps"></a><span data-ttu-id="9f861-173">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9f861-173">Next steps</span></span>
<span data-ttu-id="9f861-174">toocreate bir Red Hat Enterprise Linux VM Azure Market Kullandıkça Öde görüntü ve Dengeleme Azure barındırılan RHUI Git çok[Azure Marketi](https://azure.microsoft.com/marketplace/partners/redhat/).</span><span class="sxs-lookup"><span data-stu-id="9f861-174">toocreate a Red Hat Enterprise Linux VM from Azure Marketplace Pay-As-You-Go image and leverage Azure-hosted RHUI go too[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span></span> <span data-ttu-id="9f861-175">Mümkün toouse olacaktır `yum update` herhangi bir ek ayar olmadan RHEL Örneğinizde.</span><span class="sxs-lookup"><span data-stu-id="9f861-175">You will be able toouse `yum update` in your RHEL instance without any additional setup.</span></span>

