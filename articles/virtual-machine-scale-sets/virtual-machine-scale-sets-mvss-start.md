---
title: "sanal makine ölçek hakkında aaaLearn şablonları ayarlama | Microsoft Docs"
description: "Sanal makine ölçek kümeleri için şablon toocreate minimum uygun ölçek kümesi öğrenin"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: b7a1cf6c03b22585e16db9c071d45795c8ae75df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a><span data-ttu-id="c81e8-103">Sanal makine ölçek kümesi şablonları hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="c81e8-103">Learn about virtual machine scale set templates</span></span>
<span data-ttu-id="c81e8-104">[Azure Resource Manager şablonları](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) mükemmel şekilde toodeploy ilgili kaynaklar gruplarıdır.</span><span class="sxs-lookup"><span data-stu-id="c81e8-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way toodeploy groups of related resources.</span></span> <span data-ttu-id="c81e8-105">Bu öğretici serisi toocreate minimum uygun ölçek şablon ayarlama nasıl ve ne gösterilir toomodify bu şablonu toosuit çeşitli senaryoları.</span><span class="sxs-lookup"><span data-stu-id="c81e8-105">This tutorial series shows how toocreate a minimum viable scale set template and how toomodify this template toosuit various scenarios.</span></span> <span data-ttu-id="c81e8-106">Tüm örnekler öğesinden gelen [GitHub deposunu](https://github.com/gatneil/mvss).</span><span class="sxs-lookup"><span data-stu-id="c81e8-106">All examples come from this [GitHub repository](https://github.com/gatneil/mvss).</span></span> 

<span data-ttu-id="c81e8-107">Hedeflenen toobe basit şablonudur.</span><span class="sxs-lookup"><span data-stu-id="c81e8-107">This template is intended toobe simple.</span></span> <span data-ttu-id="c81e8-108">Ölçek daha kapsamlı örnekleri için şablonlar, hello bakın [Azure hızlı başlangıç şablonlarını GitHub deposunu](https://github.com/Azure/azure-quickstart-templates) ve hello dizesini içeren klasörleri arama `vmss`.</span><span class="sxs-lookup"><span data-stu-id="c81e8-108">For more complete examples of scale set templates, see hello [Azure Quickstart Templates GitHub repository](https://github.com/Azure/azure-quickstart-templates) and search for folders that contain hello string `vmss`.</span></span>

<span data-ttu-id="c81e8-109">Şablonları oluşturma konusunda bilginiz varsa, nasıl toohello "Sonraki adımlar" bölümüne toosee atlayın toomodify bu şablonu.</span><span class="sxs-lookup"><span data-stu-id="c81e8-109">If you are already familiar with creating templates, you can skip toohello "Next steps" section toosee how toomodify this template.</span></span>

## <a name="review-hello-template"></a><span data-ttu-id="c81e8-110">Gözden geçirme hello şablonu</span><span class="sxs-lookup"><span data-stu-id="c81e8-110">Review hello template</span></span>

<span data-ttu-id="c81e8-111">GitHub kullanmak tooreview bizim minimum uygun ölçek kümesi şablon [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="c81e8-111">Use GitHub tooreview our minimum viable scale set template, [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span></span>

<span data-ttu-id="c81e8-112">Bu öğreticide, inceleyeceğiz hello fark (`git diff master minimum-viable-scale-set`) toocreate hello minimum uygun ölçek kümesi şablonu tarafından parça parça.</span><span class="sxs-lookup"><span data-stu-id="c81e8-112">In this tutorial, we examine hello diff (`git diff master minimum-viable-scale-set`) toocreate hello minimum viable scale set template piece by piece.</span></span>

## <a name="define-schema-and-contentversion"></a><span data-ttu-id="c81e8-113">$Schema ve contentVersion tanımlayın</span><span class="sxs-lookup"><span data-stu-id="c81e8-113">Define $schema and contentVersion</span></span>
<span data-ttu-id="c81e8-114">İlk olarak, tanımlarız `$schema` ve `contentVersion` hello şablonunda.</span><span class="sxs-lookup"><span data-stu-id="c81e8-114">First, we define `$schema` and `contentVersion` in hello template.</span></span> <span data-ttu-id="c81e8-115">Merhaba `$schema` öğesi hello şablon dili hello sürümü tanımlar ve Visual Studio söz dizimi vurgulama ve benzer doğrulama özellikleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c81e8-115">hello `$schema` element defines hello version of hello template language and is used for Visual Studio syntax highlighting and similar validation features.</span></span> <span data-ttu-id="c81e8-116">Merhaba `contentVersion` öğesi Azure tarafından kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="c81e8-116">hello `contentVersion` element is not used by Azure.</span></span> <span data-ttu-id="c81e8-117">Bunun yerine, hello şablon sürümü izlemenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="c81e8-117">Instead, it helps you keep track of hello template version.</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a><span data-ttu-id="c81e8-118">parametrelerini tanımlayın</span><span class="sxs-lookup"><span data-stu-id="c81e8-118">Define parameters</span></span>
<span data-ttu-id="c81e8-119">Ardından, iki parametre tanımlarız `adminUsername` ve `adminPassword`.</span><span class="sxs-lookup"><span data-stu-id="c81e8-119">Next, we define two parameters, `adminUsername` and `adminPassword`.</span></span> <span data-ttu-id="c81e8-120">Parametreler hello dağıtım sırasında belirttiğiniz değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="c81e8-120">Parameters are values you specify at hello time of deployment.</span></span> <span data-ttu-id="c81e8-121">Merhaba `adminUsername` parametredir yalnızca bir `string` türü, ancak çünkü `adminPassword` bir parolası türü sunuyoruz `securestring`.</span><span class="sxs-lookup"><span data-stu-id="c81e8-121">hello `adminUsername` parameter is simply a `string` type, but because `adminPassword` is a secret, we give it type `securestring`.</span></span> <span data-ttu-id="c81e8-122">Daha sonra bu parametreler hello ölçek kümesi yapılandırması aktarılır.</span><span class="sxs-lookup"><span data-stu-id="c81e8-122">Later, these parameters are passed into hello scale set configuration.</span></span>

```json
  "parameters": {
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    }
  },
```
## <a name="define-variables"></a><span data-ttu-id="c81e8-123">Değişkenleri tanımlama</span><span class="sxs-lookup"><span data-stu-id="c81e8-123">Define variables</span></span>
<span data-ttu-id="c81e8-124">Resource Manager şablonları aynı zamanda, daha sonra hello şablonda kullanılan değişkenleri toobe tanımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="c81e8-124">Resource Manager templates also let you define variables toobe used later in hello template.</span></span> <span data-ttu-id="c81e8-125">Biz hello JSON nesnesi boş sol şekilde örneğimizde herhangi bir değişkeni kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="c81e8-125">Our example doesn't use any variables, so we've left hello JSON object empty.</span></span>

```json
  "variables": {},
```

## <a name="define-resources"></a><span data-ttu-id="c81e8-126">Kaynakları tanımlayın</span><span class="sxs-lookup"><span data-stu-id="c81e8-126">Define resources</span></span>
<span data-ttu-id="c81e8-127">Sonraki hello kaynakları hello şablon bölümüdür.</span><span class="sxs-lookup"><span data-stu-id="c81e8-127">Next is hello resources section of hello template.</span></span> <span data-ttu-id="c81e8-128">Burada, aslında istediğinizi tanımladığınız toodeploy.</span><span class="sxs-lookup"><span data-stu-id="c81e8-128">Here, you define what you actually want toodeploy.</span></span> <span data-ttu-id="c81e8-129">Farklı `parameters` ve `variables` (JSON nesnelerinin olan), `resources` JSON nesnelerinin JSON listesidir.</span><span class="sxs-lookup"><span data-stu-id="c81e8-129">Unlike `parameters` and `variables` (which are JSON objects), `resources` is a JSON list of JSON objects.</span></span>

```json
   "resources": [
```

<span data-ttu-id="c81e8-130">Tüm kaynak gerektiren `type`, `name`, `apiVersion`, ve `location` özellikleri.</span><span class="sxs-lookup"><span data-stu-id="c81e8-130">All resources require `type`, `name`, `apiVersion`, and `location` properties.</span></span> <span data-ttu-id="c81e8-131">Bu örneğin ilk kaynak türüne sahip `Microsft.Network/virtualNetwork`, adı `myVnet`ve apiVersion `2016-03-30`.</span><span class="sxs-lookup"><span data-stu-id="c81e8-131">This example's first resource has type `Microsft.Network/virtualNetwork`, name `myVnet`, and apiVersion `2016-03-30`.</span></span> <span data-ttu-id="c81e8-132">(toofind hello son API sürümü bir kaynak türü için bkz: Merhaba [Azure REST API belgeleri](https://docs.microsoft.com/rest/api/).)</span><span class="sxs-lookup"><span data-stu-id="c81e8-132">(toofind hello latest API version for a resource type, see hello [Azure REST API documentation](https://docs.microsoft.com/rest/api/).)</span></span>

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a><span data-ttu-id="c81e8-133">Konumu belirtin</span><span class="sxs-lookup"><span data-stu-id="c81e8-133">Specify location</span></span>
<span data-ttu-id="c81e8-134">toospecify hello konumu hello sanal ağ için kullandığımız bir [Resource Manager şablonu işlevi](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="c81e8-134">toospecify hello location for hello virtual network, we use a [Resource Manager template function](../azure-resource-manager/resource-group-template-functions.md).</span></span> <span data-ttu-id="c81e8-135">Bu işlev teklifleri ve bu gibi köşeli ayraçlar içinde alınmalıdır: `"[<template-function>]"`.</span><span class="sxs-lookup"><span data-stu-id="c81e8-135">This function must be enclosed in quotes and square brackets like this: `"[<template-function>]"`.</span></span> <span data-ttu-id="c81e8-136">Bu durumda, hello kullanırız `resourceGroup` işlevi.</span><span class="sxs-lookup"><span data-stu-id="c81e8-136">In this case, we use hello `resourceGroup` function.</span></span> <span data-ttu-id="c81e8-137">İçinde bağımsız değişken almayan ve bu dağıtım için dağıtılan hello kaynak grubu hakkındaki meta verileri içeren bir JSON nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="c81e8-137">It takes in no arguments and returns a JSON object with metadata about hello resource group this deployment is being deployed to.</span></span> <span data-ttu-id="c81e8-138">Merhaba kaynak grubu dağıtım hello aynı anda hello kullanıcı tarafından ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="c81e8-138">hello resource group is set by hello user at hello time of deployment.</span></span> <span data-ttu-id="c81e8-139">Biz sonra bu JSON nesnesinin ile dizine `.location` hello JSON nesnesinde tooget başlangıç konumu.</span><span class="sxs-lookup"><span data-stu-id="c81e8-139">We then index into this JSON object with `.location` tooget hello location from hello JSON object.</span></span>

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a><span data-ttu-id="c81e8-140">Sanal ağ özelliklerini belirtin</span><span class="sxs-lookup"><span data-stu-id="c81e8-140">Specify virtual network properties</span></span>
<span data-ttu-id="c81e8-141">Her bir Resource Manager kaynak kendi sahip `properties` yapılandırmaları belirli toohello kaynak bölümü.</span><span class="sxs-lookup"><span data-stu-id="c81e8-141">Each Resource Manager resource has its own `properties` section for configurations specific toohello resource.</span></span> <span data-ttu-id="c81e8-142">Bu durumda, bu hello sanal ağ hello özel IP adres aralığını kullanarak tek bir alt ağda olması gerektiğini belirtin `10.0.0.0/16`.</span><span class="sxs-lookup"><span data-stu-id="c81e8-142">In this case, we specify that hello virtual network should have one subnet using hello private IP address range `10.0.0.0/16`.</span></span> <span data-ttu-id="c81e8-143">Ölçek kümesi her zaman bir alt ağ içinde yer alır.</span><span class="sxs-lookup"><span data-stu-id="c81e8-143">A scale set is always contained within one subnet.</span></span> <span data-ttu-id="c81e8-144">Alt ağlar yayılamaz.</span><span class="sxs-lookup"><span data-stu-id="c81e8-144">It cannot span subnets.</span></span>

```json
       "properties": {
         "addressSpace": {
           "addressPrefixes": [
             "10.0.0.0/16"
           ]
         },
         "subnets": [
           {
             "name": "mySubnet",
             "properties": {
               "addressPrefix": "10.0.0.0/16"
             }
           }
         ]
       }
     },
```

## <a name="add-dependson-list"></a><span data-ttu-id="c81e8-145">DependsOn listeye ekleyin</span><span class="sxs-lookup"><span data-stu-id="c81e8-145">Add dependsOn list</span></span>
<span data-ttu-id="c81e8-146">Ayrıca toohello gerekli `type`, `name`, `apiVersion`, ve `location` özellikleri, her bir kaynağın isteğe bağlı bir olabilir `dependsOn` dize listesi.</span><span class="sxs-lookup"><span data-stu-id="c81e8-146">In addition toohello required `type`, `name`, `apiVersion`, and `location` properties, each resource can have an optional `dependsOn` list of strings.</span></span> <span data-ttu-id="c81e8-147">Bu liste, bu kaynak dağıtmadan önce bu dağıtım diğer kaynaklardan bitmesi gereken belirtir.</span><span class="sxs-lookup"><span data-stu-id="c81e8-147">This list specifies which other resources from this deployment must finish before deploying this resource.</span></span>

<span data-ttu-id="c81e8-148">Bu durumda, var. yalnızca tek bir öğe hello listesinde hello önceki örnekteki hello sanal ağ</span><span class="sxs-lookup"><span data-stu-id="c81e8-148">In this case, there is only one element in hello list, hello virtual network from hello previous example.</span></span> <span data-ttu-id="c81e8-149">Merhaba ağ tooexist ihtiyaçlarını ayarlanmış tüm sanal makineleri oluşturmadan önce Hello ölçek için Biz bu bağımlılık belirtin.</span><span class="sxs-lookup"><span data-stu-id="c81e8-149">We specify this dependency because hello scale set needs hello network tooexist before creating any VMs.</span></span> <span data-ttu-id="c81e8-150">Bu şekilde hello ölçek kümesi daha önce hello Ağ özelliklerinde belirtilen başlangıç IP adresi aralığından bu VM'ler özel IP adreslerini verin.</span><span class="sxs-lookup"><span data-stu-id="c81e8-150">This way, hello scale set can give these VMs private IP addresses from hello IP address range previously specified in hello network properties.</span></span> <span data-ttu-id="c81e8-151">Merhaba dependsOn listesindeki her bir dizenin Hello biçimi `<type>/<name>`.</span><span class="sxs-lookup"><span data-stu-id="c81e8-151">hello format of each string in hello dependsOn list is `<type>/<name>`.</span></span> <span data-ttu-id="c81e8-152">Kullanım hello aynı `type` ve `name` hello sanal ağ kaynak tanımı'nda önceden kullanılmış.</span><span class="sxs-lookup"><span data-stu-id="c81e8-152">Use hello same `type` and `name` used previously in hello virtual network resource definition.</span></span>

```json
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "apiVersion": "2016-04-30-preview",
       "location": "[resourceGroup().location]",
       "dependsOn": [
         "Microsoft.Network/virtualNetworks/myVnet"
       ],
```
## <a name="specify-scale-set-properties"></a><span data-ttu-id="c81e8-153">Ölçek kümesi özelliklerini belirtin</span><span class="sxs-lookup"><span data-stu-id="c81e8-153">Specify scale set properties</span></span>
<span data-ttu-id="c81e8-154">Ölçek kümeleri hello VM'ler hello ölçek kümesindeki özelleştirmek için birçok özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="c81e8-154">Scale sets have many properties for customizing hello VMs in hello scale set.</span></span> <span data-ttu-id="c81e8-155">Bu özelliklerin tam listesi için bkz: Merhaba [ölçek kümesi REST API belgeleri](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span><span class="sxs-lookup"><span data-stu-id="c81e8-155">For a full list of these properties, see hello [scale set REST API documentation](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span></span> <span data-ttu-id="c81e8-156">Bu öğreticide, biz yalnızca birkaç yaygın olarak kullanılan özellikleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c81e8-156">For this tutorial, we will set only a few commonly used properties.</span></span>
### <a name="supply-vm-size-and-capacity"></a><span data-ttu-id="c81e8-157">VM boyutu ve kapasite sağlayın</span><span class="sxs-lookup"><span data-stu-id="c81e8-157">Supply VM size and capacity</span></span>
<span data-ttu-id="c81e8-158">Merhaba ölçek gereksinimlerini tooknow VM toocreate ("sku adı") hangi boyutunu ve kaç tane böyle VM'ler toocreate ("sku kapasitesi") ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c81e8-158">hello scale set needs tooknow what size of VM toocreate ("sku name") and how many such VMs toocreate ("sku capacity").</span></span> <span data-ttu-id="c81e8-159">Hangi VM boyutları kullanılabilir toosee bkz hello [VM boyutları belgelerine](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span><span class="sxs-lookup"><span data-stu-id="c81e8-159">toosee which VM sizes are available, see hello [VM Sizes documentation](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span></span>

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a><span data-ttu-id="c81e8-160">Güncelleştirmelerin türünü seçin</span><span class="sxs-lookup"><span data-stu-id="c81e8-160">Choose type of updates</span></span>
<span data-ttu-id="c81e8-161">Merhaba ölçek kümesini toohandle hello ölçek kümesinde güncelleştirme biçimini tooknow da gerekir.</span><span class="sxs-lookup"><span data-stu-id="c81e8-161">hello scale set also needs tooknow how toohandle updates on hello scale set.</span></span> <span data-ttu-id="c81e8-162">Şu anda iki seçenek vardır `Manual` ve `Automatic`.</span><span class="sxs-lookup"><span data-stu-id="c81e8-162">Currently, there are two options, `Manual` and `Automatic`.</span></span> <span data-ttu-id="c81e8-163">Merhaba hello iki arasındaki farklar hakkında daha fazla bilgi için üzerinde hello belgelerine bakın. [nasıl tooupgrade bir ölçek kümesi](./virtual-machine-scale-sets-upgrade-scale-set.md).</span><span class="sxs-lookup"><span data-stu-id="c81e8-163">For more information on hello differences between hello two, see hello documentation on [how tooupgrade a scale set](./virtual-machine-scale-sets-upgrade-scale-set.md).</span></span>

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a><span data-ttu-id="c81e8-164">VM işletim sistemini seçin</span><span class="sxs-lookup"><span data-stu-id="c81e8-164">Choose VM operating system</span></span>
<span data-ttu-id="c81e8-165">Merhaba ölçek gereksinimlerine tooknow hangi işletim sistemi tooput hello Vm'lerinde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c81e8-165">hello scale set needs tooknow what operating system tooput on hello VMs.</span></span> <span data-ttu-id="c81e8-166">Burada, hello VM'ler ile tam olarak düzeltme eki bir Ubuntu 16.04 LTS görüntüsü oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="c81e8-166">Here, we create hello VMs with a fully patched Ubuntu 16.04-LTS image.</span></span>

```json
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
               "publisher": "Canonical",
               "offer": "UbuntuServer",
               "sku": "16.04-LTS",
               "version": "latest"
             }
           },
```

### <a name="specify-computernameprefix"></a><span data-ttu-id="c81e8-167">ComputerNamePrefix belirtin</span><span class="sxs-lookup"><span data-stu-id="c81e8-167">Specify computerNamePrefix</span></span>
<span data-ttu-id="c81e8-168">Merhaba ölçek kümesini birden çok VM dağıtır.</span><span class="sxs-lookup"><span data-stu-id="c81e8-168">hello scale set deploys multiple VMs.</span></span> <span data-ttu-id="c81e8-169">Her bir VM adı belirtmek yerine, biz belirtin `computerNamePrefix`.</span><span class="sxs-lookup"><span data-stu-id="c81e8-169">Instead of specifying each VM name, we specify `computerNamePrefix`.</span></span> <span data-ttu-id="c81e8-170">hello form VM adlara sahip olacak şekilde hello ölçek kümesini bir dizin toohello öneki her bir VM ekler `<computerNamePrefix>_<auto-generated-index>`.</span><span class="sxs-lookup"><span data-stu-id="c81e8-170">hello scale set appends an index toohello prefix for each VM, so VM names have hello form `<computerNamePrefix>_<auto-generated-index>`.</span></span>

<span data-ttu-id="c81e8-171">Aşağıdaki kod parçacığında hello hello ölçek kümesindeki tüm VM'ler için tooset hello yönetici kullanıcı adı ve parola önce hello parametrelerinden kullanın.</span><span class="sxs-lookup"><span data-stu-id="c81e8-171">In hello following snippet, we use hello parameters from before tooset hello administrator username and password for all VMs in hello scale set.</span></span> <span data-ttu-id="c81e8-172">Merhaba ile bunu `parameters` şablon işlevi.</span><span class="sxs-lookup"><span data-stu-id="c81e8-172">We do this with hello `parameters` template function.</span></span> <span data-ttu-id="c81e8-173">Bu işlev, bu parametre için değer hello hangi parametresi toorefer tooand çıkarır belirten bir dize olarak alır.</span><span class="sxs-lookup"><span data-stu-id="c81e8-173">This function takes in a string that specifies which parameter toorefer tooand outputs hello value for that parameter.</span></span>

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a><span data-ttu-id="c81e8-174">VM ağ yapılandırması belirtin</span><span class="sxs-lookup"><span data-stu-id="c81e8-174">Specify VM network configuration</span></span>
<span data-ttu-id="c81e8-175">Son olarak, biz hello ölçek kümesindeki hello VM'ler için toospecify hello ağ yapılandırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c81e8-175">Finally, we need toospecify hello network configuration for hello VMs in hello scale set.</span></span> <span data-ttu-id="c81e8-176">Bu durumda, yalnızca daha önce oluşturduğunuz hello alt toospecify hello kimliği ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="c81e8-176">In this case, we only need toospecify hello ID of hello subnet created earlier.</span></span> <span data-ttu-id="c81e8-177">Bu, hello ölçek tooput hello ağ arabirimleri bu alt ağda kümesi bildirir.</span><span class="sxs-lookup"><span data-stu-id="c81e8-177">This tells hello scale set tooput hello network interfaces in this subnet.</span></span>

<span data-ttu-id="c81e8-178">Merhaba sanal ağ hello kullanarak hello alt ağ içeren hello Kimliğini alabilirsiniz `resourceId` şablon işlevi.</span><span class="sxs-lookup"><span data-stu-id="c81e8-178">You can get hello ID of hello virtual network containing hello subnet by using hello `resourceId` template function.</span></span> <span data-ttu-id="c81e8-179">Bu işlev hello türü ve kaynağın adını alır ve bu kaynağın tam tanımlayıcı döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="c81e8-179">This function takes in hello type and name of a resource and returns hello fully qualified identifier of that resource.</span></span> <span data-ttu-id="c81e8-180">Bu kimliği hello biçime sahiptir:`/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span><span class="sxs-lookup"><span data-stu-id="c81e8-180">This ID has hello form: `/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span></span>

<span data-ttu-id="c81e8-181">Ancak, hello sanal ağ hello tanıtıcısı yeterli değildir.</span><span class="sxs-lookup"><span data-stu-id="c81e8-181">However, hello identifier of hello virtual network is not enough.</span></span> <span data-ttu-id="c81e8-182">Ölçek kümesi VM bulunmalıdır hello hello belirli alt belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c81e8-182">You must specify hello specific subnet that hello scale set VMs should be in.</span></span> <span data-ttu-id="c81e8-183">toodo Bu, birleştirme `/subnets/mySubnet` hello sanal ağ toohello kimliği.</span><span class="sxs-lookup"><span data-stu-id="c81e8-183">toodo this, concatenate `/subnets/mySubnet` toohello ID of hello virtual network.</span></span> <span data-ttu-id="c81e8-184">Merhaba, tam olarak nitelenmiş hello hello alt ağ Kimliğini sonucudur.</span><span class="sxs-lookup"><span data-stu-id="c81e8-184">hello result is hello fully qualified ID of hello subnet.</span></span> <span data-ttu-id="c81e8-185">Bu birleştirme hello ile yapmak `concat` dizeleri bir dizi alır ve kendi birleştirme döndüren işlev.</span><span class="sxs-lookup"><span data-stu-id="c81e8-185">Do this concatenation with hello `concat` function, which takes in a series of strings and returns their concatenation.</span></span>

```json
           "networkProfile": {
             "networkInterfaceConfigurations": [
               {
                 "name": "myNic",
                 "properties": {
                   "primary": "true",
                   "ipConfigurations": [
                     {
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
                           "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
                         }
                       }
                     }
                   ]
                 }
               }
             ]
           }
         }
       }
     }
   ]
}

```

## <a name="next-steps"></a><span data-ttu-id="c81e8-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c81e8-186">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
