---
title: "Azure CLI ile Linux VM görüntüleri seçin | Microsoft Docs"
description: "Yayımcı, teklif, SKU ve sürümü Market VM görüntüleri belirlemek için Azure CLI kullanmayı öğrenin."
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
ms.openlocfilehash: e0c27a7ee9e9a7ab1a3b004e070fa556b56a36a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-find-linux-vm-images-in-the-azure-marketplace-with-the-azure-cli"></a><span data-ttu-id="e4643-103">Linux VM görüntüleri Azure CLI ile Azure Marketi bulmak nasıl</span><span class="sxs-lookup"><span data-stu-id="e4643-103">How to find Linux VM images in the Azure Marketplace with the Azure CLI</span></span>
<span data-ttu-id="e4643-104">Bu konuda, Azure Marketi'nde VM görüntüleri bulmak için Azure CLI 2.0 kullanmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="e4643-104">This topic describes how to use the Azure CLI 2.0 to find VM images in the Azure Marketplace.</span></span> <span data-ttu-id="e4643-105">Bir Linux VM oluşturduğunuzda bir Market görüntüsü belirtmek için bu bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="e4643-105">Use this information to specify a Marketplace image when you create a Linux VM.</span></span>

<span data-ttu-id="e4643-106">En son yüklendiğinden emin olmak [Azure CLI 2.0](/cli/azure/install-az-cli2) ve bir Azure hesabına günlüğe kaydedilir (`az login`).</span><span class="sxs-lookup"><span data-stu-id="e4643-106">Make sure that you installed the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and are logged in to an Azure account (`az login`).</span></span>

## <a name="terminology"></a><span data-ttu-id="e4643-107">Terminoloji</span><span class="sxs-lookup"><span data-stu-id="e4643-107">Terminology</span></span>

<span data-ttu-id="e4643-108">Market görüntülerini CLI ve diğer Azure araçlarını bir hiyerarşi göre tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="e4643-108">Marketplace images are identified in the CLI and other Azure tools according to a hierarchy:</span></span>

* <span data-ttu-id="e4643-109">**Yayımcı** -görüntüyü oluşturan kuruluş.</span><span class="sxs-lookup"><span data-stu-id="e4643-109">**Publisher** - The organization that created the image.</span></span> <span data-ttu-id="e4643-110">Örnek: kurallı</span><span class="sxs-lookup"><span data-stu-id="e4643-110">Example: Canonical</span></span>
* <span data-ttu-id="e4643-111">**Teklif** -bir yayımcı tarafından oluşturulan ilgili görüntüler grubudur.</span><span class="sxs-lookup"><span data-stu-id="e4643-111">**Offer** - A group of related images created by a publisher.</span></span> <span data-ttu-id="e4643-112">Örnek: Ubuntu Server</span><span class="sxs-lookup"><span data-stu-id="e4643-112">Example: Ubuntu Server</span></span>
* <span data-ttu-id="e4643-113">**SKU** - bir dağıtım büyük sürümü gibi bir teklif ait bir örnek.</span><span class="sxs-lookup"><span data-stu-id="e4643-113">**SKU** - An instance of an offer, such as a major release of a distribution.</span></span> <span data-ttu-id="e4643-114">Örnek: 16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="e4643-114">Example: 16.04-LTS</span></span>
* <span data-ttu-id="e4643-115">**Sürüm** -SKU görüntü sürüm numarası.</span><span class="sxs-lookup"><span data-stu-id="e4643-115">**Version** - The version number of an image SKU.</span></span> <span data-ttu-id="e4643-116">Görüntü belirtirken, hangi dağıtım en son sürümünü seçer sürüm numarasıyla "son" değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4643-116">When specifying the image, you can replace the version number with "latest", which selects the latest version of the distribution.</span></span>

<span data-ttu-id="e4643-117">Bir Market görüntüsü belirtmek için genellikle görüntünün kullanın *URN*.</span><span class="sxs-lookup"><span data-stu-id="e4643-117">To specify a Marketplace image, you typically use the image *URN*.</span></span> <span data-ttu-id="e4643-118">İki nokta üst üste (:) karakteriyle ayrılmış bu değerleri URN birleştirir: *yayımcı*:*teklif*:*Sku*:*sürüm*.</span><span class="sxs-lookup"><span data-stu-id="e4643-118">The URN combines these values, separated by the colon (:) character: *Publisher*:*Offer*:*Sku*:*Version*.</span></span> 


## <a name="list-popular-images"></a><span data-ttu-id="e4643-119">Liste popüler görüntüleri</span><span class="sxs-lookup"><span data-stu-id="e4643-119">List popular images</span></span>

<span data-ttu-id="e4643-120">Çalıştırma [az vm görüntü listesi](/cli/azure/vm/image#list) olmadan komutu `--all` Azure Marketi popüler VM görüntüleri listesini görmek için seçeneği.</span><span class="sxs-lookup"><span data-stu-id="e4643-120">Run the [az vm image list](/cli/azure/vm/image#list) command, without the `--all` option, to see a list of popular VM images in the Azure Marketplace.</span></span> <span data-ttu-id="e4643-121">Örneğin, tablo biçiminde popüler görüntüleri önbelleğe alınmış bir listesini görüntülemek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e4643-121">For example, run the following command to display a cached list of popular images in table format:</span></span>

```azurecli
az vm image list --output table
```

<span data-ttu-id="e4643-122">Çıktı URN içerir (değeri *Urn* sütun), görüntüyü belirtmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="e4643-122">The output includes the URN (the value in the *Urn* column), which you use to specify the image.</span></span> <span data-ttu-id="e4643-123">Bir VM Bu popüler Market görüntülerden birini oluştururken, alternatif olarak, URN diğer adı gibi belirleyebilirsiniz *UbuntuLTS*.</span><span class="sxs-lookup"><span data-stu-id="e4643-123">When creating a VM with one of these popular Marketplace images, you can alternatively specify the URN alias, such as *UbuntuLTS*.</span></span>

```
You are viewing an offline list of images, use --all to retrieve an up-to-date list
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

## <a name="find-specific-images"></a><span data-ttu-id="e4643-124">Belirli görüntüleri bulma</span><span class="sxs-lookup"><span data-stu-id="e4643-124">Find specific images</span></span>

<span data-ttu-id="e4643-125">Belirli bir VM görüntüsü markette bulmak için `az vm image list` komutunu `--all` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="e4643-125">To find a specific VM image in the Marketplace, use the `az vm image list` command with the `--all` option.</span></span> <span data-ttu-id="e4643-126">Komutun bu sürümü tamamlamak ve biraz zaman alabilir genellikle listeyi filtrelemek için uzun output dönüş `--publisher` veya başka bir parametre.</span><span class="sxs-lookup"><span data-stu-id="e4643-126">This version of the command takes some time to complete and can return lengthy output, so you usually filter the list by `--publisher` or another parameter.</span></span> 

<span data-ttu-id="e4643-127">Örneğin, aşağıdaki komut tüm Debian teklifleri görüntüler (olmadan unutmamanız `--all` geçiş, yalnızca yerel önbelleğe ortak görüntülerinin arar):</span><span class="sxs-lookup"><span data-stu-id="e4643-127">For example, the following command displays all Debian offers (remember that without the `--all` switch, it only searches the local cache of common images):</span></span>

```azurecli
az vm image list --offer Debian --all --output table 

```

<span data-ttu-id="e4643-128">Kısmi çıktı:</span><span class="sxs-lookup"><span data-stu-id="e4643-128">Partial output:</span></span> 
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

<span data-ttu-id="e4643-129">Benzer filtreleri ile uygulama `--location`, `--publisher`, ve `--sku` seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="e4643-129">Apply similar filters with the `--location`, `--publisher`, and `--sku` options.</span></span> <span data-ttu-id="e4643-130">Kısmi eşleşmeler arama gibi bir filtre bile gerçekleştirebileceğiniz `--offer Deb` tüm Debian görüntüleri bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="e4643-130">You can even perform partial matches on a filter, such as searching for `--offer Deb` to find all Debian images.</span></span>

<span data-ttu-id="e4643-131">Belirli bir konumla belirtmezseniz `--location` seçeneğini değerlerini `westus` varsayılan olarak döndürülür.</span><span class="sxs-lookup"><span data-stu-id="e4643-131">If you don't specify a particular location with the `--location` option, the values for `westus` are returned by default.</span></span> <span data-ttu-id="e4643-132">(Çalıştırarak farklı varsayılan konumunu ayarla `az configure --defaults location=<location>`.)</span><span class="sxs-lookup"><span data-stu-id="e4643-132">(Set a different default location by running `az configure --defaults location=<location>`.)</span></span>

<span data-ttu-id="e4643-133">Örneğin, aşağıdaki komut, tüm Debian 8 SKU listeler `westeurope`:</span><span class="sxs-lookup"><span data-stu-id="e4643-133">For example, the following command lists all Debian 8 SKUs in `westeurope`:</span></span>

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

<span data-ttu-id="e4643-134">Kısmi çıktı:</span><span class="sxs-lookup"><span data-stu-id="e4643-134">Partial output:</span></span>

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

## <a name="navigate-the-images"></a><span data-ttu-id="e4643-135">Görüntüleri gidin</span><span class="sxs-lookup"><span data-stu-id="e4643-135">Navigate the images</span></span> 
<span data-ttu-id="e4643-136">Görüntüyü bir konumda bulmak için başka bir yolu çalıştırmaktır [az vm görüntü listesi-yayımcılar](/cli/azure/vm/image#list-publishers), [az vm görüntü listesi-teklifleri](/cli/azure/vm/image#list-offers), ve [az vm görüntü listesi-SKU'ları](/cli/azure/vm/image#list-skus) komutları sırayla.</span><span class="sxs-lookup"><span data-stu-id="e4643-136">Another way to find an image in a location is to run the [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers), and [az vm image list-skus](/cli/azure/vm/image#list-skus) commands in sequence.</span></span> <span data-ttu-id="e4643-137">Bu komutları ile bu değerler belirler:</span><span class="sxs-lookup"><span data-stu-id="e4643-137">With these commands, you determine these values:</span></span>

1. <span data-ttu-id="e4643-138">Görüntü yayımcılarını listeleyin.</span><span class="sxs-lookup"><span data-stu-id="e4643-138">List the image publishers.</span></span>
2. <span data-ttu-id="e4643-139">Belirli bir yayımcı varsa yayımcının tekliflerini listeleyin.</span><span class="sxs-lookup"><span data-stu-id="e4643-139">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="e4643-140">Belirli bir teklif varsa SKU’larını listeleyin.</span><span class="sxs-lookup"><span data-stu-id="e4643-140">For a given offer, list their SKUs.</span></span>


<span data-ttu-id="e4643-141">Örneğin, aşağıdaki komut, Batı ABD konumunda görüntü yayımcılar listeler:</span><span class="sxs-lookup"><span data-stu-id="e4643-141">For example, the following command lists the image publishers in the West US location:</span></span>

```azurecli
az vm image list-publishers --location westus --output table
```

<span data-ttu-id="e4643-142">Kısmi çıktı:</span><span class="sxs-lookup"><span data-stu-id="e4643-142">Partial output:</span></span>

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
<span data-ttu-id="e4643-143">Belirli bir yayımcıdan teklifleri bulmak için bu bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="e4643-143">Use this information to find offers from a specific publisher.</span></span> <span data-ttu-id="e4643-144">Canonical Batı ABD konumunda bir görüntü yayımcı ise, örneğin, kendi teklifleri çalıştırarak bulabileceğiniz `azure vm image list-offers`.</span><span class="sxs-lookup"><span data-stu-id="e4643-144">For example, if Canonical is an image publisher in the West US location, find their offers by running `azure vm image list-offers`.</span></span> <span data-ttu-id="e4643-145">Konum ve yayıncıya aşağıdaki örnekteki gibi geçirin:</span><span class="sxs-lookup"><span data-stu-id="e4643-145">Pass the location and the publisher as in the following example:</span></span>

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

<span data-ttu-id="e4643-146">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="e4643-146">Output:</span></span>

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
<span data-ttu-id="e4643-147">Batı ABD bölgesi Canonical yayımlar gördüğünüz **UbuntuServer** Azure üzerinde sunar.</span><span class="sxs-lookup"><span data-stu-id="e4643-147">You see that in the West US region, Canonical publishes the **UbuntuServer** offer on Azure.</span></span> <span data-ttu-id="e4643-148">Peki bunların SKU’su ne?</span><span class="sxs-lookup"><span data-stu-id="e4643-148">But what SKUs?</span></span> <span data-ttu-id="e4643-149">Bu değerleri almak için şunu çalıştırın `azure vm image list-skus` ve konumu, yayımcı ve bulunan teklif ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="e4643-149">To get those values, run `azure vm image list-skus` and set the location, publisher, and offer that you have discovered:</span></span>

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

<span data-ttu-id="e4643-150">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="e4643-150">Output:</span></span>

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

<span data-ttu-id="e4643-151">Son olarak, `az vm image list` istediğiniz, örneğin, belirli bir SKU sürümünü bulmak için komutu **16.04 LTS**:</span><span class="sxs-lookup"><span data-stu-id="e4643-151">Finally, use the `az vm image list` command to find a specific version of the SKU you want, for example, **16.04-LTS**:</span></span>

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

<span data-ttu-id="e4643-152">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="e4643-152">Output:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="e4643-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e4643-153">Next steps</span></span>
<span data-ttu-id="e4643-154">Artık tam olarak URN değeri not gerçekleştirerek kullanmak istediğiniz görüntü seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4643-154">Now you can choose precisely the image you want to use by taking note of the URN value.</span></span> <span data-ttu-id="e4643-155">Bu değer ile geçirmek `--image` bir VM ile oluşturduğunuzda parametresi [az vm oluşturma](/cli/azure/vm#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="e4643-155">Pass this value with the `--image` parameter when you create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="e4643-156">"Son" URN sürüm numarası isteğe bağlı olarak değiştirebilirsiniz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e4643-156">Remember that you can optionally replace the version number in the URN with "latest".</span></span> <span data-ttu-id="e4643-157">Bu her zaman en son sürümünü dağıtım sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="e4643-157">This version is always the latest version of the distribution.</span></span> <span data-ttu-id="e4643-158">URN bilgileri kullanarak hızlı bir şekilde bir sanal makine oluşturmak için bkz: [oluşturma ve yönetme Linux VM'ler Azure CLI ile](tutorial-manage-vm.md).</span><span class="sxs-lookup"><span data-stu-id="e4643-158">To create a virtual machine quickly by using the URN information, see [Create and Manage Linux VMs with the Azure CLI](tutorial-manage-vm.md).</span></span>
