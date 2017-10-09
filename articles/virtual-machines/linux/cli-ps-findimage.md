---
title: "aaaSelect Linux VM görüntüleri hello Azure CLI ile | Microsoft Docs"
description: "Toouse nasıl hello Azure CLI toodetermine hello yayımcı, teklif, SKU ve sürümü Market VM görüntüleri öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7a858e38-4f17-4e8e-a28a-c7f801101721
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/24/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0b115b8654bc156b5bfadba53a6b002a105acb68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-linux-vm-images-in-hello-azure-marketplace-with-hello-azure-cli"></a><span data-ttu-id="ce934-103">Nasıl hello Azure CLI ile Azure Marketi hello içinde toofind Linux VM görüntüleri</span><span class="sxs-lookup"><span data-stu-id="ce934-103">How toofind Linux VM images in hello Azure Marketplace with hello Azure CLI</span></span>
<span data-ttu-id="ce934-104">Bu konuda nasıl toouse hello Azure CLI 2.0 toofind VM görüntüleri hello Azure Marketi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ce934-104">This topic describes how toouse hello Azure CLI 2.0 toofind VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="ce934-105">Bir Linux VM oluşturduğunuzda, bu bilgileri toospecify bir Market görüntüsü kullanın.</span><span class="sxs-lookup"><span data-stu-id="ce934-105">Use this information toospecify a Marketplace image when you create a Linux VM.</span></span>

<span data-ttu-id="ce934-106">Merhaba son yüklü olduğundan emin olun [Azure CLI 2.0](/cli/azure/install-az-cli2) ve tooan Azure hesabı günlüğe kaydedilir (`az login`).</span><span class="sxs-lookup"><span data-stu-id="ce934-106">Make sure that you installed hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and are logged in tooan Azure account (`az login`).</span></span>

## <a name="terminology"></a><span data-ttu-id="ce934-107">Terminoloji</span><span class="sxs-lookup"><span data-stu-id="ce934-107">Terminology</span></span>

<span data-ttu-id="ce934-108">Market görüntülerini hello CLI ve diğer Azure Araçları tooa hiyerarşi göre tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="ce934-108">Marketplace images are identified in hello CLI and other Azure tools according tooa hierarchy:</span></span>

* <span data-ttu-id="ce934-109">**Yayımcı** -hello hello görüntüyü oluşturan kuruluş.</span><span class="sxs-lookup"><span data-stu-id="ce934-109">**Publisher** - hello organization that created hello image.</span></span> <span data-ttu-id="ce934-110">Örnek: kurallı</span><span class="sxs-lookup"><span data-stu-id="ce934-110">Example: Canonical</span></span>
* <span data-ttu-id="ce934-111">**Teklif** -bir yayımcı tarafından oluşturulan ilgili görüntüler grubudur.</span><span class="sxs-lookup"><span data-stu-id="ce934-111">**Offer** - A group of related images created by a publisher.</span></span> <span data-ttu-id="ce934-112">Örnek: Ubuntu Server</span><span class="sxs-lookup"><span data-stu-id="ce934-112">Example: Ubuntu Server</span></span>
* <span data-ttu-id="ce934-113">**SKU** - bir dağıtım büyük sürümü gibi bir teklif ait bir örnek.</span><span class="sxs-lookup"><span data-stu-id="ce934-113">**SKU** - An instance of an offer, such as a major release of a distribution.</span></span> <span data-ttu-id="ce934-114">Örnek: 16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="ce934-114">Example: 16.04-LTS</span></span>
* <span data-ttu-id="ce934-115">**Sürüm** -hello görüntünün SKU sürüm numarası.</span><span class="sxs-lookup"><span data-stu-id="ce934-115">**Version** - hello version number of an image SKU.</span></span> <span data-ttu-id="ce934-116">Merhaba görüntü belirtirken, hangi hello dağıtım en son sürümünü hello seçer hello sürüm numarasıyla "son" değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce934-116">When specifying hello image, you can replace hello version number with "latest", which selects hello latest version of hello distribution.</span></span>

<span data-ttu-id="ce934-117">toospecify bir Market görüntüsü, genellikle kullandığınız hello görüntü *URN*.</span><span class="sxs-lookup"><span data-stu-id="ce934-117">toospecify a Marketplace image, you typically use hello image *URN*.</span></span> <span data-ttu-id="ce934-118">Merhaba URN hello iki nokta üst üste (:) karakteriyle ayrılmış bu değerleri birleştirir: *yayımcı*:*teklif*:*Sku*:*sürüm*.</span><span class="sxs-lookup"><span data-stu-id="ce934-118">hello URN combines these values, separated by hello colon (:) character: *Publisher*:*Offer*:*Sku*:*Version*.</span></span> 


## <a name="list-popular-images"></a><span data-ttu-id="ce934-119">Liste popüler görüntüleri</span><span class="sxs-lookup"><span data-stu-id="ce934-119">List popular images</span></span>

<span data-ttu-id="ce934-120">Merhaba çalıştırmak [az vm görüntü listesi](/cli/azure/vm/image#list) hello olmadan komutu `--all` seçeneği, popüler VM listesini görüntüleri hello Azure Marketi toosee.</span><span class="sxs-lookup"><span data-stu-id="ce934-120">Run hello [az vm image list](/cli/azure/vm/image#list) command, without hello `--all` option, toosee a list of popular VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="ce934-121">Örneğin, komut toodisplay aşağıdaki hello önbelleğe alınmış popüler görüntüleri listesini tablo biçiminde çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ce934-121">For example, run hello following command toodisplay a cached list of popular images in table format:</span></span>

```azurecli
az vm image list --output table
```

<span data-ttu-id="ce934-122">Merhaba çıktı hello URN içerir (Merhaba hello değerinde *Urn* sütun), hangi toospecify hello görüntü kullanın.</span><span class="sxs-lookup"><span data-stu-id="ce934-122">hello output includes hello URN (hello value in hello *Urn* column), which you use toospecify hello image.</span></span> <span data-ttu-id="ce934-123">Bir VM Bu popüler Market görüntülerden birini oluştururken, alternatif olarak hello URN diğer gibi belirleyebilirsiniz *UbuntuLTS*.</span><span class="sxs-lookup"><span data-stu-id="ce934-123">When creating a VM with one of these popular Marketplace images, you can alternatively specify hello URN alias, such as *UbuntuLTS*.</span></span>

```
You are viewing an offline list of images, use --all tooretrieve an up-to-date list
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
...
```

## <a name="find-specific-images"></a><span data-ttu-id="ce934-124">Belirli görüntüleri bulma</span><span class="sxs-lookup"><span data-stu-id="ce934-124">Find specific images</span></span>

<span data-ttu-id="ce934-125">toofind hello Market, belirli bir VM görüntüsündeki kullanmak hello `az vm image list` hello komutunu `--all` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="ce934-125">toofind a specific VM image in hello Marketplace, use hello `az vm image list` command with hello `--all` option.</span></span> <span data-ttu-id="ce934-126">Merhaba komutunun bu sürümü, bazı zaman toocomplete alır ve genellikle hello listeyi filtrelemek için uzun çıkış döndürebilirsiniz `--publisher` veya başka bir parametre.</span><span class="sxs-lookup"><span data-stu-id="ce934-126">This version of hello command takes some time toocomplete and can return lengthy output, so you usually filter hello list by `--publisher` or another parameter.</span></span> 

<span data-ttu-id="ce934-127">Örneğin, komutu aşağıdaki hello tüm Debian teklifleri görüntüler (Merhaba unutmayın `--all` geçiş, yalnızca ortak görüntülerinin hello yerel önbelleği arar):</span><span class="sxs-lookup"><span data-stu-id="ce934-127">For example, hello following command displays all Debian offers (remember that without hello `--all` switch, it only searches hello local cache of common images):</span></span>

```azurecli
az vm image list --offer Debian --all --output table 

```

<span data-ttu-id="ce934-128">Kısmi çıktı:</span><span class="sxs-lookup"><span data-stu-id="ce934-128">Partial output:</span></span> 
```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  --------------
Debian   credativ     7                  credativ:Debian:7:7.0.201602010                  7.0.201602010
Debian   credativ     7                  credativ:Debian:7:7.0.201603020                  7.0.201603020
Debian   credativ     7                  credativ:Debian:7:7.0.201604050                  7.0.201604050
Debian   credativ     7                  credativ:Debian:7:7.0.201604200                  7.0.201604200
Debian   credativ     7                  credativ:Debian:7:7.0.201606280                  7.0.201606280
Debian   credativ     7                  credativ:Debian:7:7.0.201609120                  7.0.201609120
Debian   credativ     7                  credativ:Debian:7:7.0.201611020                  7.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
Debian   credativ     8                  credativ:Debian:8:8.0.201708040                  8.0.201708040
...
```

<span data-ttu-id="ce934-129">Merhaba ile benzer filtre uygulamak `--location`, `--publisher`, ve `--sku` seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="ce934-129">Apply similar filters with hello `--location`, `--publisher`, and `--sku` options.</span></span> <span data-ttu-id="ce934-130">Kısmi eşleşmeler arama gibi bir filtre bile gerçekleştirebileceğiniz `--offer Deb` toofind tüm Debian görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ce934-130">You can even perform partial matches on a filter, such as searching for `--offer Deb` toofind all Debian images.</span></span>

<span data-ttu-id="ce934-131">Belirli bir konuma hello ile belirtmezseniz `--location` seçeneğini hello değerlerini `westus` varsayılan olarak döndürülür.</span><span class="sxs-lookup"><span data-stu-id="ce934-131">If you don't specify a particular location with hello `--location` option, hello values for `westus` are returned by default.</span></span> <span data-ttu-id="ce934-132">(Çalıştırarak farklı varsayılan konumunu ayarla `az configure --defaults location=<location>`.)</span><span class="sxs-lookup"><span data-stu-id="ce934-132">(Set a different default location by running `az configure --defaults location=<location>`.)</span></span>

<span data-ttu-id="ce934-133">Örneğin, tüm Debian 8 SKU'ları, komutu aşağıdaki hello listeler `westeurope`:</span><span class="sxs-lookup"><span data-stu-id="ce934-133">For example, hello following command lists all Debian 8 SKUs in `westeurope`:</span></span>

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

<span data-ttu-id="ce934-134">Kısmi çıktı:</span><span class="sxs-lookup"><span data-stu-id="ce934-134">Partial output:</span></span>

```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  -------------
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
...
```

## <a name="navigate-hello-images"></a><span data-ttu-id="ce934-135">Merhaba görüntüleri gidin</span><span class="sxs-lookup"><span data-stu-id="ce934-135">Navigate hello images</span></span> 
<span data-ttu-id="ce934-136">Başka bir şekilde toofind görüntünün bir konumda toorun hello olan [az vm görüntü listesi-yayımcılar](/cli/azure/vm/image#list-publishers), [az vm görüntü listesi-teklifleri](/cli/azure/vm/image#list-offers), ve [az vm görüntü listesi-SKU'ları](/cli/azure/vm/image#list-skus) komutları sırayla.</span><span class="sxs-lookup"><span data-stu-id="ce934-136">Another way toofind an image in a location is toorun hello [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers), and [az vm image list-skus](/cli/azure/vm/image#list-skus) commands in sequence.</span></span> <span data-ttu-id="ce934-137">Bu komutları ile bu değerler belirler:</span><span class="sxs-lookup"><span data-stu-id="ce934-137">With these commands, you determine these values:</span></span>

1. <span data-ttu-id="ce934-138">Liste hello görüntü yayımcılar.</span><span class="sxs-lookup"><span data-stu-id="ce934-138">List hello image publishers.</span></span>
2. <span data-ttu-id="ce934-139">Belirli bir yayımcı varsa yayımcının tekliflerini listeleyin.</span><span class="sxs-lookup"><span data-stu-id="ce934-139">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="ce934-140">Belirli bir teklif varsa SKU’larını listeleyin.</span><span class="sxs-lookup"><span data-stu-id="ce934-140">For a given offer, list their SKUs.</span></span>


<span data-ttu-id="ce934-141">Örneğin, hello aşağıdaki komut hello Batı ABD konumu hello görüntü yayımcıları listeler:</span><span class="sxs-lookup"><span data-stu-id="ce934-141">For example, hello following command lists hello image publishers in hello West US location:</span></span>

```azurecli
az vm image list-publishers --location westus --output table
```

<span data-ttu-id="ce934-142">Kısmi çıktı:</span><span class="sxs-lookup"><span data-stu-id="ce934-142">Partial output:</span></span>

```
Location    Name
----------  ----------------------------------------------------
westus      1e
westus      4psa
westus      7isolutions
westus      a10networks
westus      abiquo
westus      accellion
westus      Acronis
westus      Acronis.Backup
westus      actian_matrix
westus      actifio
westus      activeeon
westus      adatao
...
```
<span data-ttu-id="ce934-143">Bu bilgi toofind belirli bir yayımcıdan sunar kullanın.</span><span class="sxs-lookup"><span data-stu-id="ce934-143">Use this information toofind offers from a specific publisher.</span></span> <span data-ttu-id="ce934-144">Canonical hello Batı ABD konumu görüntü Publisher'da ise, örneğin, kendi teklifleri çalıştırarak bulabileceğiniz `azure vm image list-offers`.</span><span class="sxs-lookup"><span data-stu-id="ce934-144">For example, if Canonical is an image publisher in hello West US location, find their offers by running `azure vm image list-offers`.</span></span> <span data-ttu-id="ce934-145">Merhaba konumunu ve örnek aşağıdaki hello olduğu gibi hello yayımcı geçirin:</span><span class="sxs-lookup"><span data-stu-id="ce934-145">Pass hello location and hello publisher as in hello following example:</span></span>

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

<span data-ttu-id="ce934-146">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="ce934-146">Output:</span></span>

```
Location    Name
----------  -------------------------
westus      Ubuntu15.04Snappy
westus      Ubuntu15.04SnappyDocker
westus      UbunturollingSnappy
westus      UbuntuServer
westus      Ubuntu_Core
westus      Ubuntu_Snappy_Core
westus      Ubuntu_Snappy_Core_Docker
```
<span data-ttu-id="ce934-147">Merhaba Batı ABD bölgesinde hello Canonical yayımlar gördüğünüz **UbuntuServer** Azure üzerinde sunar.</span><span class="sxs-lookup"><span data-stu-id="ce934-147">You see that in hello West US region, Canonical publishes hello **UbuntuServer** offer on Azure.</span></span> <span data-ttu-id="ce934-148">Ancak hangi SKU'ları? Bu değerleri tooget çalıştırmak `azure vm image list-skus` ve hello konumu, yayımcı ve bulunan teklif ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="ce934-148">But what SKUs? tooget those values, run `azure vm image list-skus` and set hello location, publisher, and offer that you have discovered:</span></span>

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

<span data-ttu-id="ce934-149">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="ce934-149">Output:</span></span>

```
Location    Name
----------  -----------------
westus      12.04.3-LTS
westus      12.04.4-LTS
westus      12.04.5-DAILY-LTS
westus      12.04.5-LTS
westus      12.10
westus      14.04.0-LTS
westus      14.04.1-LTS
westus      14.04.2-LTS
westus      14.04.3-LTS
westus      14.04.4-LTS
westus      14.04.5-DAILY-LTS
westus      14.04.5-LTS
westus      16.04-beta
westus      16.04-DAILY-LTS
westus      16.04-LTS
westus      16.04.0-LTS
westus      16.10
westus      16.10-DAILY
westus      17.04
westus      17.04-DAILY
westus      17.10-DAILY
```

<span data-ttu-id="ce934-150">Son olarak, hello kullan `az vm image list` komutu toofind hello SKU istediğiniz, örneğin, belirli bir sürümünü **16.04 LTS**:</span><span class="sxs-lookup"><span data-stu-id="ce934-150">Finally, use hello `az vm image list` command toofind a specific version of hello SKU you want, for example, **16.04-LTS**:</span></span>

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

<span data-ttu-id="ce934-151">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="ce934-151">Output:</span></span>

```
Offer         Publisher    Sku        Urn                                               Version
------------  -----------  ---------  ------------------------------------------------  ---------------
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611220  16.04.201611220
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611300  16.04.201611300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612050  16.04.201612050
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612140  16.04.201612140
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612210  16.04.201612210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201701130  16.04.201701130
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702020  16.04.201702020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702200  16.04.201702200
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702210  16.04.201702210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702240  16.04.201702240
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703020  16.04.201703020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703030  16.04.201703030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703070  16.04.201703070
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703270  16.04.201703270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703280  16.04.201703280
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703300  16.04.201703300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705080  16.04.201705080
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705160  16.04.201705160
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706100  16.04.201706100
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706191  16.04.201706191
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707210  16.04.201707210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707270  16.04.201707270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708030  16.04.201708030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708110  16.04.201708110
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708151  16.04.201708151
```
## <a name="next-steps"></a><span data-ttu-id="ce934-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ce934-152">Next steps</span></span>
<span data-ttu-id="ce934-153">Tam olarak hello görüntüsünü seçebilirsiniz artık alma Not hello URN değeri tarafından toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="ce934-153">Now you can choose precisely hello image you want toouse by taking note of hello URN value.</span></span> <span data-ttu-id="ce934-154">Bu değeri hello ile geçirmek `--image` bir VM ile Merhaba oluşturduğunuzda parametresi [az vm oluşturma](/cli/azure/vm#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="ce934-154">Pass this value with hello `--image` parameter when you create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="ce934-155">"Son" Merhaba URN hello sürüm numarası isteğe bağlı olarak değiştirebilirsiniz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ce934-155">Remember that you can optionally replace hello version number in hello URN with "latest".</span></span> <span data-ttu-id="ce934-156">Bu her zaman en son sürümünü hello dağıtım hello sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="ce934-156">This version is always hello latest version of hello distribution.</span></span> <span data-ttu-id="ce934-157">toocreate hello URN bilgileri kullanarak hızlı bir şekilde bir sanal makine bkz [oluşturma ve yönetme Linux VM'ler hello Azure CLI ile](tutorial-manage-vm.md).</span><span class="sxs-lookup"><span data-stu-id="ce934-157">toocreate a virtual machine quickly by using hello URN information, see [Create and Manage Linux VMs with hello Azure CLI](tutorial-manage-vm.md).</span></span>
