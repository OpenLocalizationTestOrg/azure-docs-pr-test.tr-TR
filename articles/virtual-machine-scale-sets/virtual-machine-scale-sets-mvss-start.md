---
title: "Sanal makine ölçek kümesi şablonları hakkında bilgi edinin | Microsoft Docs"
description: "Sanal makine ölçek kümeleri için minimum uygun ölçek kümesi şablon oluşturmayı öğrenin"
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
ms.openlocfilehash: 65f02c4675eb752dcc82e9a1d1c7f6c2c193fc32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a><span data-ttu-id="32329-103">Sanal makine ölçek kümesi şablonları hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="32329-103">Learn about virtual machine scale set templates</span></span>
<span data-ttu-id="32329-104">[Azure Resource Manager şablonları](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment), ilgili kaynak gruplarını dağıtmanın harika bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="32329-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way to deploy groups of related resources.</span></span> <span data-ttu-id="32329-105">Bu öğretici serisi minimum uygun ölçek kümesi şablonunun nasıl oluşturulacağını ve çeşitli senaryoları uyacak şekilde bu şablonu nasıl değiştireceğiniz gösterilir.</span><span class="sxs-lookup"><span data-stu-id="32329-105">This tutorial series shows how to create a minimum viable scale set template and how to modify this template to suit various scenarios.</span></span> <span data-ttu-id="32329-106">Tüm örnekler öğesinden gelen [GitHub deposunu](https://github.com/gatneil/mvss).</span><span class="sxs-lookup"><span data-stu-id="32329-106">All examples come from this [GitHub repository](https://github.com/gatneil/mvss).</span></span> 

<span data-ttu-id="32329-107">Bu şablon, basit olması amaçlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="32329-107">This template is intended to be simple.</span></span> <span data-ttu-id="32329-108">Ölçek daha kapsamlı örnekleri için şablonlar, bakın [Azure hızlı başlangıç şablonlarını GitHub deposunu](https://github.com/Azure/azure-quickstart-templates) ve arama dizesini içeren klasörler için `vmss`.</span><span class="sxs-lookup"><span data-stu-id="32329-108">For more complete examples of scale set templates, see the [Azure Quickstart Templates GitHub repository](https://github.com/Azure/azure-quickstart-templates) and search for folders that contain the string `vmss`.</span></span>

<span data-ttu-id="32329-109">Şablonları oluşturma konusunda bilginiz varsa, bu şablonu nasıl değiştireceğiniz görmek için "Sonraki adımlar" bölümüne atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32329-109">If you are already familiar with creating templates, you can skip to the "Next steps" section to see how to modify this template.</span></span>

## <a name="review-the-template"></a><span data-ttu-id="32329-110">Şablon gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="32329-110">Review the template</span></span>

<span data-ttu-id="32329-111">Bizim minimum uygun ölçek kümesi şablon gözden geçirmek için GitHub kullanın [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="32329-111">Use GitHub to review our minimum viable scale set template, [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span></span>

<span data-ttu-id="32329-112">Bu öğreticide, fark inceleyeceğiz (`git diff master minimum-viable-scale-set`) en düşük uygun ölçek oluşturmak için şablon tarafından parça parça ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="32329-112">In this tutorial, we examine the diff (`git diff master minimum-viable-scale-set`) to create the minimum viable scale set template piece by piece.</span></span>

## <a name="define-schema-and-contentversion"></a><span data-ttu-id="32329-113">$Schema ve contentVersion tanımlayın</span><span class="sxs-lookup"><span data-stu-id="32329-113">Define $schema and contentVersion</span></span>
<span data-ttu-id="32329-114">İlk olarak, tanımlarız `$schema` ve `contentVersion` şablondaki.</span><span class="sxs-lookup"><span data-stu-id="32329-114">First, we define `$schema` and `contentVersion` in the template.</span></span> <span data-ttu-id="32329-115">`$schema` Öğesi şablonu dil sürümünü tanımlar ve Visual Studio söz dizimi vurgulama ve benzer doğrulama özellikleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="32329-115">The `$schema` element defines the version of the template language and is used for Visual Studio syntax highlighting and similar validation features.</span></span> <span data-ttu-id="32329-116">`contentVersion` Öğesi Azure tarafından kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="32329-116">The `contentVersion` element is not used by Azure.</span></span> <span data-ttu-id="32329-117">Bunun yerine, şablonu sürümü izlemenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="32329-117">Instead, it helps you keep track of the template version.</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a><span data-ttu-id="32329-118">parametrelerini tanımlayın</span><span class="sxs-lookup"><span data-stu-id="32329-118">Define parameters</span></span>
<span data-ttu-id="32329-119">Ardından, iki parametre tanımlarız `adminUsername` ve `adminPassword`.</span><span class="sxs-lookup"><span data-stu-id="32329-119">Next, we define two parameters, `adminUsername` and `adminPassword`.</span></span> <span data-ttu-id="32329-120">Parametreleri, dağıtım sırasında belirttiğiniz değerleridir.</span><span class="sxs-lookup"><span data-stu-id="32329-120">Parameters are values you specify at the time of deployment.</span></span> <span data-ttu-id="32329-121">`adminUsername` Parametredir yalnızca bir `string` türü, ancak çünkü `adminPassword` bir parolası türü sunuyoruz `securestring`.</span><span class="sxs-lookup"><span data-stu-id="32329-121">The `adminUsername` parameter is simply a `string` type, but because `adminPassword` is a secret, we give it type `securestring`.</span></span> <span data-ttu-id="32329-122">Daha sonra bu parametreler ölçek kümesi yapılandırmaya geçirilir.</span><span class="sxs-lookup"><span data-stu-id="32329-122">Later, these parameters are passed into the scale set configuration.</span></span>

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
## <a name="define-variables"></a><span data-ttu-id="32329-123">Değişkenleri tanımlama</span><span class="sxs-lookup"><span data-stu-id="32329-123">Define variables</span></span>
<span data-ttu-id="32329-124">Resource Manager şablonları aynı zamanda, daha sonra şablonunda kullanılacak değişkenler tanımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="32329-124">Resource Manager templates also let you define variables to be used later in the template.</span></span> <span data-ttu-id="32329-125">Biz JSON nesnesi boş sol şekilde örneğimizde herhangi bir değişkeni kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="32329-125">Our example doesn't use any variables, so we've left the JSON object empty.</span></span>

```json
  "variables": {},
```

## <a name="define-resources"></a><span data-ttu-id="32329-126">Kaynakları tanımlayın</span><span class="sxs-lookup"><span data-stu-id="32329-126">Define resources</span></span>
<span data-ttu-id="32329-127">Sonraki şablon kaynakları bölümünde bulunur.</span><span class="sxs-lookup"><span data-stu-id="32329-127">Next is the resources section of the template.</span></span> <span data-ttu-id="32329-128">Burada, aslında dağıtmak istediğinizi tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32329-128">Here, you define what you actually want to deploy.</span></span> <span data-ttu-id="32329-129">Farklı `parameters` ve `variables` (JSON nesnelerinin olan), `resources` JSON nesnelerinin JSON listesidir.</span><span class="sxs-lookup"><span data-stu-id="32329-129">Unlike `parameters` and `variables` (which are JSON objects), `resources` is a JSON list of JSON objects.</span></span>

```json
   "resources": [
```

<span data-ttu-id="32329-130">Tüm kaynak gerektiren `type`, `name`, `apiVersion`, ve `location` özellikleri.</span><span class="sxs-lookup"><span data-stu-id="32329-130">All resources require `type`, `name`, `apiVersion`, and `location` properties.</span></span> <span data-ttu-id="32329-131">Bu örneğin ilk kaynak türüne sahip `Microsft.Network/virtualNetwork`, adı `myVnet`ve apiVersion `2016-03-30`.</span><span class="sxs-lookup"><span data-stu-id="32329-131">This example's first resource has type `Microsft.Network/virtualNetwork`, name `myVnet`, and apiVersion `2016-03-30`.</span></span> <span data-ttu-id="32329-132">(Kaynak türü için son API sürümü bulmak için bkz: [Azure REST API belgeleri](https://docs.microsoft.com/rest/api/).)</span><span class="sxs-lookup"><span data-stu-id="32329-132">(To find the latest API version for a resource type, see the [Azure REST API documentation](https://docs.microsoft.com/rest/api/).)</span></span>

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a><span data-ttu-id="32329-133">Konumu belirtin</span><span class="sxs-lookup"><span data-stu-id="32329-133">Specify location</span></span>
<span data-ttu-id="32329-134">Sanal ağ konumunu belirtmek için kullanıyoruz bir [Resource Manager şablonu işlevi](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="32329-134">To specify the location for the virtual network, we use a [Resource Manager template function](../azure-resource-manager/resource-group-template-functions.md).</span></span> <span data-ttu-id="32329-135">Bu işlev teklifleri ve bu gibi köşeli ayraçlar içinde alınmalıdır: `"[<template-function>]"`.</span><span class="sxs-lookup"><span data-stu-id="32329-135">This function must be enclosed in quotes and square brackets like this: `"[<template-function>]"`.</span></span> <span data-ttu-id="32329-136">Bu durumda, kullandığımız `resourceGroup` işlevi.</span><span class="sxs-lookup"><span data-stu-id="32329-136">In this case, we use the `resourceGroup` function.</span></span> <span data-ttu-id="32329-137">İçinde bağımsız değişken almayan ve bu dağıtım dağıtıldığı kaynak grubu hakkındaki meta verileri içeren bir JSON nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="32329-137">It takes in no arguments and returns a JSON object with metadata about the resource group this deployment is being deployed to.</span></span> <span data-ttu-id="32329-138">Kaynak grubu dağıtım zamanında kullanıcı tarafından ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="32329-138">The resource group is set by the user at the time of deployment.</span></span> <span data-ttu-id="32329-139">Biz sonra bu JSON nesnesinin ile dizine `.location` JSON nesnesinden konumunu almak için.</span><span class="sxs-lookup"><span data-stu-id="32329-139">We then index into this JSON object with `.location` to get the location from the JSON object.</span></span>

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a><span data-ttu-id="32329-140">Sanal ağ özelliklerini belirtin</span><span class="sxs-lookup"><span data-stu-id="32329-140">Specify virtual network properties</span></span>
<span data-ttu-id="32329-141">Her bir Resource Manager kaynak kendi sahip `properties` kaynağa özgü yapılandırmalar için bölüm.</span><span class="sxs-lookup"><span data-stu-id="32329-141">Each Resource Manager resource has its own `properties` section for configurations specific to the resource.</span></span> <span data-ttu-id="32329-142">Bu durumda, sanal ağ özel IP adres aralığını kullanarak tek bir alt ağda olması gerektiğini belirtin `10.0.0.0/16`.</span><span class="sxs-lookup"><span data-stu-id="32329-142">In this case, we specify that the virtual network should have one subnet using the private IP address range `10.0.0.0/16`.</span></span> <span data-ttu-id="32329-143">Ölçek kümesi her zaman bir alt ağ içinde yer alır.</span><span class="sxs-lookup"><span data-stu-id="32329-143">A scale set is always contained within one subnet.</span></span> <span data-ttu-id="32329-144">Alt ağlar yayılamaz.</span><span class="sxs-lookup"><span data-stu-id="32329-144">It cannot span subnets.</span></span>

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

## <a name="add-dependson-list"></a><span data-ttu-id="32329-145">DependsOn listeye ekleyin</span><span class="sxs-lookup"><span data-stu-id="32329-145">Add dependsOn list</span></span>
<span data-ttu-id="32329-146">Ek olarak gerekli `type`, `name`, `apiVersion`, ve `location` özellikleri, her bir kaynağın isteğe bağlı bir olabilir `dependsOn` dize listesi.</span><span class="sxs-lookup"><span data-stu-id="32329-146">In addition to the required `type`, `name`, `apiVersion`, and `location` properties, each resource can have an optional `dependsOn` list of strings.</span></span> <span data-ttu-id="32329-147">Bu liste, bu kaynak dağıtmadan önce bu dağıtım diğer kaynaklardan bitmesi gereken belirtir.</span><span class="sxs-lookup"><span data-stu-id="32329-147">This list specifies which other resources from this deployment must finish before deploying this resource.</span></span>

<span data-ttu-id="32329-148">Bu durumda, var. yalnızca tek bir öğe listesinde, önceki örnekten sanal ağ</span><span class="sxs-lookup"><span data-stu-id="32329-148">In this case, there is only one element in the list, the virtual network from the previous example.</span></span> <span data-ttu-id="32329-149">Tüm sanal makineleri oluşturmadan önce mevcut ağa ölçek kümesinin çünkü Biz bu bağımlılık belirtin.</span><span class="sxs-lookup"><span data-stu-id="32329-149">We specify this dependency because the scale set needs the network to exist before creating any VMs.</span></span> <span data-ttu-id="32329-150">Bu şekilde, Ölçek kümesi Ağ Özellikleri'nde daha önce belirtilen IP adresi aralığından bu VM'ler özel IP adreslerini verin.</span><span class="sxs-lookup"><span data-stu-id="32329-150">This way, the scale set can give these VMs private IP addresses from the IP address range previously specified in the network properties.</span></span> <span data-ttu-id="32329-151">DependsOn listedeki her dize biçimi `<type>/<name>`.</span><span class="sxs-lookup"><span data-stu-id="32329-151">The format of each string in the dependsOn list is `<type>/<name>`.</span></span> <span data-ttu-id="32329-152">Aynı `type` ve `name` sanal ağ kaynak tanımı'nda önceden kullanılmış.</span><span class="sxs-lookup"><span data-stu-id="32329-152">Use the same `type` and `name` used previously in the virtual network resource definition.</span></span>

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
## <a name="specify-scale-set-properties"></a><span data-ttu-id="32329-153">Ölçek kümesi özelliklerini belirtin</span><span class="sxs-lookup"><span data-stu-id="32329-153">Specify scale set properties</span></span>
<span data-ttu-id="32329-154">Ölçek kümesi VM ölçek kümesindeki özelleştirmek için birçok özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="32329-154">Scale sets have many properties for customizing the VMs in the scale set.</span></span> <span data-ttu-id="32329-155">Bu özelliklerin tam listesi için bkz: [ölçek kümesi REST API belgeleri](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span><span class="sxs-lookup"><span data-stu-id="32329-155">For a full list of these properties, see the [scale set REST API documentation](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span></span> <span data-ttu-id="32329-156">Bu öğreticide, biz yalnızca birkaç yaygın olarak kullanılan özellikleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="32329-156">For this tutorial, we will set only a few commonly used properties.</span></span>
### <a name="supply-vm-size-and-capacity"></a><span data-ttu-id="32329-157">VM boyutu ve kapasite sağlayın</span><span class="sxs-lookup"><span data-stu-id="32329-157">Supply VM size and capacity</span></span>
<span data-ttu-id="32329-158">Ölçek kümesi boyutu ("sku adı") oluşturmak için VM bilmeniz gerekir ve bu tür kaç VM'ler ("sku kapasitesi") oluşturun.</span><span class="sxs-lookup"><span data-stu-id="32329-158">The scale set needs to know what size of VM to create ("sku name") and how many such VMs to create ("sku capacity").</span></span> <span data-ttu-id="32329-159">Hangi VM boyutları kullanılabilir olduğunu görmek için bkz: [VM boyutları belgelerine](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span><span class="sxs-lookup"><span data-stu-id="32329-159">To see which VM sizes are available, see the [VM Sizes documentation](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span></span>

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a><span data-ttu-id="32329-160">Güncelleştirmelerin türünü seçin</span><span class="sxs-lookup"><span data-stu-id="32329-160">Choose type of updates</span></span>
<span data-ttu-id="32329-161">Ayrıca ölçek ölçek kümesindeki güncelleştirmelerin nasıl ele alınacağını bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="32329-161">The scale set also needs to know how to handle updates on the scale set.</span></span> <span data-ttu-id="32329-162">Şu anda iki seçenek vardır `Manual` ve `Automatic`.</span><span class="sxs-lookup"><span data-stu-id="32329-162">Currently, there are two options, `Manual` and `Automatic`.</span></span> <span data-ttu-id="32329-163">İkisi arasındaki farklar hakkında daha fazla bilgi için belgelere bakın [ölçek kümesini yükseltme](./virtual-machine-scale-sets-upgrade-scale-set.md).</span><span class="sxs-lookup"><span data-stu-id="32329-163">For more information on the differences between the two, see the documentation on [how to upgrade a scale set](./virtual-machine-scale-sets-upgrade-scale-set.md).</span></span>

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a><span data-ttu-id="32329-164">VM işletim sistemini seçin</span><span class="sxs-lookup"><span data-stu-id="32329-164">Choose VM operating system</span></span>
<span data-ttu-id="32329-165">Ölçek sanal makinelerin koymak için hangi işletim sistemi bilmeniz gereksinimlerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="32329-165">The scale set needs to know what operating system to put on the VMs.</span></span> <span data-ttu-id="32329-166">Burada, sanal makineleri bir tam olarak düzeltme eki Ubuntu 16.04 LTS görüntüsüyle oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="32329-166">Here, we create the VMs with a fully patched Ubuntu 16.04-LTS image.</span></span>

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

### <a name="specify-computernameprefix"></a><span data-ttu-id="32329-167">ComputerNamePrefix belirtin</span><span class="sxs-lookup"><span data-stu-id="32329-167">Specify computerNamePrefix</span></span>
<span data-ttu-id="32329-168">Birden çok VM ölçek kümesi dağıtır.</span><span class="sxs-lookup"><span data-stu-id="32329-168">The scale set deploys multiple VMs.</span></span> <span data-ttu-id="32329-169">Her bir VM adı belirtmek yerine, biz belirtin `computerNamePrefix`.</span><span class="sxs-lookup"><span data-stu-id="32329-169">Instead of specifying each VM name, we specify `computerNamePrefix`.</span></span> <span data-ttu-id="32329-170">Formun VM adlara sahip şekilde ölçek kümesini dizin ön eki her bir VM ekler `<computerNamePrefix>_<auto-generated-index>`.</span><span class="sxs-lookup"><span data-stu-id="32329-170">The scale set appends an index to the prefix for each VM, so VM names have the form `<computerNamePrefix>_<auto-generated-index>`.</span></span>

<span data-ttu-id="32329-171">Aşağıdaki kod parçacığında, Ölçek kümesindeki tüm VM'ler için yönetici kullanıcı adı ve parolayı ayarlamak için önce parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="32329-171">In the following snippet, we use the parameters from before to set the administrator username and password for all VMs in the scale set.</span></span> <span data-ttu-id="32329-172">Biz bunu ile `parameters` şablon işlevi.</span><span class="sxs-lookup"><span data-stu-id="32329-172">We do this with the `parameters` template function.</span></span> <span data-ttu-id="32329-173">Bu işlev başvurmak için hangi parametresi belirtir ve bu parametre için değer çıkaran bir dize olarak alır.</span><span class="sxs-lookup"><span data-stu-id="32329-173">This function takes in a string that specifies which parameter to refer to and outputs the value for that parameter.</span></span>

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a><span data-ttu-id="32329-174">VM ağ yapılandırması belirtin</span><span class="sxs-lookup"><span data-stu-id="32329-174">Specify VM network configuration</span></span>
<span data-ttu-id="32329-175">Son olarak, biz ölçek kümesindeki sanal makineleri için ağ yapılandırmasının belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="32329-175">Finally, we need to specify the network configuration for the VMs in the scale set.</span></span> <span data-ttu-id="32329-176">Bu durumda, biz yalnızca daha önce oluşturduğunuz alt ağ kimliği belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="32329-176">In this case, we only need to specify the ID of the subnet created earlier.</span></span> <span data-ttu-id="32329-177">Bu alt ağda ağ arabirimleri yerleştirilecek kümesini söyler.</span><span class="sxs-lookup"><span data-stu-id="32329-177">This tells the scale set to put the network interfaces in this subnet.</span></span>

<span data-ttu-id="32329-178">Alt ağ kullanarak içeren sanal ağ kimliği alabilirsiniz `resourceId` şablon işlevi.</span><span class="sxs-lookup"><span data-stu-id="32329-178">You can get the ID of the virtual network containing the subnet by using the `resourceId` template function.</span></span> <span data-ttu-id="32329-179">Bu işlev türü ve kaynağın adını alır ve bu kaynağın tam tanımlayıcısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="32329-179">This function takes in the type and name of a resource and returns the fully qualified identifier of that resource.</span></span> <span data-ttu-id="32329-180">Bu kimliği biçime sahiptir:`/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span><span class="sxs-lookup"><span data-stu-id="32329-180">This ID has the form: `/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span></span>

<span data-ttu-id="32329-181">Ancak, sanal ağ tanıtıcısı yeterli değildir.</span><span class="sxs-lookup"><span data-stu-id="32329-181">However, the identifier of the virtual network is not enough.</span></span> <span data-ttu-id="32329-182">Ölçek VM'ler kümesi belirli alt bulunmalıdır belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="32329-182">You must specify the specific subnet that the scale set VMs should be in.</span></span> <span data-ttu-id="32329-183">Bunu yapmak için birleştirme `/subnets/mySubnet` sanal ağ kimliği.</span><span class="sxs-lookup"><span data-stu-id="32329-183">To do this, concatenate `/subnets/mySubnet` to the ID of the virtual network.</span></span> <span data-ttu-id="32329-184">Sonuç, alt ağın tam kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="32329-184">The result is the fully qualified ID of the subnet.</span></span> <span data-ttu-id="32329-185">Bu birleştirme ile yapmak `concat` dizeleri bir dizi alır ve kendi birleştirme döndüren işlev.</span><span class="sxs-lookup"><span data-stu-id="32329-185">Do this concatenation with the `concat` function, which takes in a series of strings and returns their concatenation.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="32329-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="32329-186">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
