---
title: "birden çok NIC - Azure Resource Manager şablonu ile bir VM aaaCreate | Microsoft Docs"
description: "Bir VM ile birden çok NIC bir Azure Resource Manager şablonu kullanarak oluşturun."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 486f7dd5-cf2f-434c-85d1-b3e85c427def
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5d9ffcbd40c72dc18ae6de38e739eb5e45bf669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a><span data-ttu-id="d8f87-103">Bir şablon kullanarak birden çok NIC ile VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="d8f87-103">Create a VM with multiple NICs using a template</span></span>
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="d8f87-104">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d8f87-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="d8f87-105">Bu makalede, kullanarak yer almaktadır hello yerine çoğu yeni dağıtımlar için Microsoft önerir hello Resource Manager dağıtım modeli [Klasik dağıtım modeli](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d8f87-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="d8f87-106">Merhaba aşağıdaki adımları kullanın adlı bir kaynak grubu *IaaSStory* hello WEB sunucuları ve bir kaynak grubu için adlı *IaaSStory arka uç* hello DB sunucuları için.</span><span class="sxs-lookup"><span data-stu-id="d8f87-106">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8f87-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d8f87-107">Prerequisites</span></span>
<span data-ttu-id="d8f87-108">DB sunucuları hello oluşturabilmeniz için önce toocreate hello gerekir *IaaSStory* hello gereken tüm kaynakların bu senaryo için kaynak grubuyla.</span><span class="sxs-lookup"><span data-stu-id="d8f87-108">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="d8f87-109">Bu kaynaklar toocreate tamamlamak hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d8f87-109">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="d8f87-110">Çok gidin[hello şablon sayfasına](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="d8f87-110">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="d8f87-111">Merhaba şablon sayfasındaki sağ toohello **üst kaynak grubu**, tıklatın **tooAzure dağıtmak**.</span><span class="sxs-lookup"><span data-stu-id="d8f87-111">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="d8f87-112">Gerekirse, hello parametre değerlerini değiştirmek sonra hello Azure Önizleme portalı toodeploy hello kaynak grubunda hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="d8f87-112">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d8f87-113">Depolama hesabı adları benzersiz olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d8f87-113">Make sure your storage account names are unique.</span></span> <span data-ttu-id="d8f87-114">Azure üzerinde yinelenen depolama hesabı adları sahip olamaz.</span><span class="sxs-lookup"><span data-stu-id="d8f87-114">You cannot have duplicate storage account names in Azure.</span></span>
> 

## <a name="understand-hello-deployment-template"></a><span data-ttu-id="d8f87-115">Merhaba dağıtım şablonu anlama</span><span class="sxs-lookup"><span data-stu-id="d8f87-115">Understand hello deployment template</span></span>
<span data-ttu-id="d8f87-116">Bu belgeleri ile sağlanan hello şablonunun dağıtmadan önce ne yaptığını anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d8f87-116">Before you deploy hello template provided with this documentation, make sure you understand what it does.</span></span> <span data-ttu-id="d8f87-117">Aşağıdaki adımları hello hello şablon iyi bir genel bakış sağlar:</span><span class="sxs-lookup"><span data-stu-id="d8f87-117">hello following steps provide a good overview of hello template:</span></span>

1. <span data-ttu-id="d8f87-118">Çok gidin[hello şablon sayfasına](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="d8f87-118">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="d8f87-119">Tıklatın **azuredeploy.json** tooopen hello şablon dosyası.</span><span class="sxs-lookup"><span data-stu-id="d8f87-119">Click **azuredeploy.json** tooopen hello template file.</span></span>
3. <span data-ttu-id="d8f87-120">Bildirim hello *osType* aşağıda listelenen parametre.</span><span class="sxs-lookup"><span data-stu-id="d8f87-120">Notice hello *osType* parameter listed below.</span></span> <span data-ttu-id="d8f87-121">Bu parametre kullanılan tooselect olan hangi VM görüntü toouse hello veritabanı sunucusu, birden çok işletim sistemi için ilgili ayarları.</span><span class="sxs-lookup"><span data-stu-id="d8f87-121">This parameter is used tooselect what VM image toouse for hello database server, along with multiple operating system related settings.</span></span>

    ```json
    "osType": {
      "type": "string",
      "defaultValue": "Windows",
      "allowedValues": [
        "Windows",
        "Ubuntu"
      ],
      "metadata": {
      "description": "Type of OS toouse for VMs: Windows or Ubuntu."
      }
    },
    ```

4. <span data-ttu-id="d8f87-122">Değişkenleri toohello listesini kaydırın ve hello hello tanımını denetleyin **dbVMSetting** değişkenleri, aşağıda listelenen.</span><span class="sxs-lookup"><span data-stu-id="d8f87-122">Scroll down toohello list of variables, and check hello definition for hello **dbVMSetting** variables, listed below.</span></span> <span data-ttu-id="d8f87-123">Hello bulunan hello dizi öğeleri birini aldığı **dbVMSettings** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="d8f87-123">It receives one of hello array elements contained in hello **dbVMSettings** variable.</span></span> <span data-ttu-id="d8f87-124">Yazılım geliştirme ifadeyle bilginiz varsa, hello görüntüleyebilirsiniz **dbVMSettings** değişken karma tablo veya bir sözlük olarak.</span><span class="sxs-lookup"><span data-stu-id="d8f87-124">If you are familiar with software development terminology, you can view hello **dbVMSettings** variable as a hash table, or a dictionary.</span></span>

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. <span data-ttu-id="d8f87-125">Toodeploy Windows hello arka uçta SQL çalıştıran VM'ler karar verdiğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="d8f87-125">Suppose you decide toodeploy Windows VMs running SQL in hello back-end.</span></span> <span data-ttu-id="d8f87-126">Değeri hello **osType** olacaktır *Windows*ve hello **dbVMSetting** değişkeni aşağıda listelenen hello hello ilk değeri temsil eden hello öğesi içerebilir **dbVMSettings** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="d8f87-126">Then hello value for **osType** would be *Windows*, and hello **dbVMSetting** variable would contain hello element listed below, which represents hello first value in hello **dbVMSettings** variable.</span></span>

    ```json
    "Windows": {
      "vmSize": "Standard_DS3",
      "publisher": "MicrosoftSQLServer",
      "offer": "SQL2014SP1-WS2012R2",
      "sku": "Standard",
      "version": "latest",
      "vmName": "DB",
      "osdisk": "osdiskdb",
      "datadisk": "datadiskdb",
      "nicName": "NICDB",
      "ipAddress": "192.168.2.",
      "extensionDeployment": "",
      "avsetName": "ASDB",
      "remotePort": 3389,
      "dbPort": 1433
    },
    ```

6. <span data-ttu-id="d8f87-127">Bildirim hello **vmSize** hello değeri içeren *Standard_DS3*.</span><span class="sxs-lookup"><span data-stu-id="d8f87-127">Notice hello **vmSize** contains hello value *Standard_DS3*.</span></span> <span data-ttu-id="d8f87-128">Yalnızca belirli VM boyutları için birden çok NIC hello kullanımına izin verin.</span><span class="sxs-lookup"><span data-stu-id="d8f87-128">Only certain VM sizes allow for hello use of multiple NICs.</span></span> <span data-ttu-id="d8f87-129">Hangi VM boyutları hello okuyarak birden çok NIC destek doğrulayabilirsiniz [Windows VM boyutları](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ve [Linux VM boyutları](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) makaleleri.</span><span class="sxs-lookup"><span data-stu-id="d8f87-129">You can verify which VM sizes support multiple NICs by reading hello [Windows VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux VM sizes](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) articles.</span></span>

7. <span data-ttu-id="d8f87-130">Çok ilerleyin**kaynakları** ve bildirimi hello ilk öğe.</span><span class="sxs-lookup"><span data-stu-id="d8f87-130">Scroll down too**resources** and notice hello first element.</span></span> <span data-ttu-id="d8f87-131">Bir depolama hesabı açıklar.</span><span class="sxs-lookup"><span data-stu-id="d8f87-131">It describes a storage account.</span></span> <span data-ttu-id="d8f87-132">Bu depolama hesabını her veritabanı VM tarafından kullanılan kullanılan toomaintain hello veri disklerinin olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d8f87-132">This storage account will be used toomaintain hello data disks used by each database VM.</span></span> <span data-ttu-id="d8f87-133">Bu senaryoda, her veritabanı VM normal depolamada depolanan bir işletim sistemi diski ve SSD (premium) depolamada depolanan iki veri diski var.</span><span class="sxs-lookup"><span data-stu-id="d8f87-133">In this scenario, each database VM has an OS disk stored in regular storage, and two data disks stored in SSD (premium) storage.</span></span>

    ```json
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[parameters('prmStorageName')]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "Storage Account - Premium"
      },
      "properties": {
      "accountType": "[parameters('prmStorageType')]"
      }
    },
    ```

8. <span data-ttu-id="d8f87-134">Aşağıda listelenen toohello sonraki kaynak kaydırın.</span><span class="sxs-lookup"><span data-stu-id="d8f87-134">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="d8f87-135">Bu kaynak NIC VM her veritabanında veritabanı erişimi için kullanılan hello temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d8f87-135">This resource represents hello NIC used for database access in each database VM.</span></span> <span data-ttu-id="d8f87-136">Bildirim hello hello kullanımını **kopya** bu kaynak işlevinde.</span><span class="sxs-lookup"><span data-stu-id="d8f87-136">Notice hello use of hello **copy** function in this resource.</span></span> <span data-ttu-id="d8f87-137">Merhaba şablon sağlar, toodeploy istediğiniz gibi hello üzerinde birçok VM tabanlı olarak **dbCount** parametresi.</span><span class="sxs-lookup"><span data-stu-id="d8f87-137">hello template allows you toodeploy as many VMs as you want, based on hello **dbCount** parameter.</span></span> <span data-ttu-id="d8f87-138">Bu nedenle toocreate gerekir hello NIC aynı miktarda her VM için bir tane veritabanı erişimi için.</span><span class="sxs-lookup"><span data-stu-id="d8f87-138">Therefore you need toocreate hello same amount of NICs for database access, one for each VM.</span></span>

    ```json
    {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[concat(variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
    "location": "[variables('location')]",
    "tags": {
      "displayName": "NetworkInterfaces - DB DA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "privateIPAllocationMethod": "Static",
            "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(4))]",
            "subnet": {
              "id": "[variables('backEndSubnetRef')]"
            }
          }
         }
       ] 
     }
    },
    ```

9. <span data-ttu-id="d8f87-139">Aşağıda listelenen toohello sonraki kaynak kaydırın.</span><span class="sxs-lookup"><span data-stu-id="d8f87-139">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="d8f87-140">Bu kaynak NIC her veritabanındaki VM yönetimi için kullanılan hello temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d8f87-140">This resource represents hello NIC used for management in each database VM.</span></span> <span data-ttu-id="d8f87-141">Bir kez daha, bu NIC'ler birini her veritabanı için VM gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8f87-141">Once again, you need one of these NICs for each database VM.</span></span> <span data-ttu-id="d8f87-142">Bildirim hello **networkSecurityGroup** erişim tooRDP/SSH toothis NIC yalnızca izin veren bir NSG bağlama öğesi.</span><span class="sxs-lookup"><span data-stu-id="d8f87-142">Notice hello **networkSecurityGroup** element, linking an NSG that allows access tooRDP/SSH toothis NIC only.</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[concat(variables('dbVMSetting').nicName, '-RA-',copyindex(1))]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "NetworkInterfaces - DB RA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "networkSecurityGroup": {
             "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('remoteAccessNSGName'))]"
             },
             "privateIPAllocationMethod": "Static",
             "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(54))]",
             "subnet": {
              "id": "[variables('backEndSubnetRef')]"
             }
           }
          }
        ]
      }
    },
```

10. <span data-ttu-id="d8f87-143">Aşağıda listelenen toohello sonraki kaynak kaydırın.</span><span class="sxs-lookup"><span data-stu-id="d8f87-143">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="d8f87-144">Bu kaynak, tüm veritabanı VM'ler tarafından paylaşılan bir kullanılabilirlik kümesi toobe temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d8f87-144">This resource represents an availability set toobe shared by all database VMs.</span></span> <span data-ttu-id="d8f87-145">Bu şekilde, her zaman olacağını bir VM bakım sırasında çalışan ayarlamak hello içinde garanti.</span><span class="sxs-lookup"><span data-stu-id="d8f87-145">That way, you guarantee that there will always be one VM in hello set running during maintenance.</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/availabilitySets",
      "name": "[variables('dbVMSetting').avsetName]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "AvailabilitySet - DB"
      }
    },
    ```

11. <span data-ttu-id="d8f87-146">Toohello sonraki kaynak kaydırın.</span><span class="sxs-lookup"><span data-stu-id="d8f87-146">Scroll down toohello next resource.</span></span> <span data-ttu-id="d8f87-147">Bu kaynak hello veritabanı VM'ler, hello ilk birkaç satırı aşağıda listelenen görülen temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d8f87-147">This resource represents hello database VMs, as seen in hello first few lines listed below.</span></span> <span data-ttu-id="d8f87-148">Bildirim hello hello kullanımını **kopya** yeniden işlev, birden çok VM oluşturduğunuz sağlama dayalı hello üzerinde **dbCount** parametresi.</span><span class="sxs-lookup"><span data-stu-id="d8f87-148">Notice hello use of hello **copy** function again, ensuring that multiple VMs are created based on hello **dbCount** parameter.</span></span> <span data-ttu-id="d8f87-149">Ayrıca hello fark **dependsOn** koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="d8f87-149">Also notice hello **dependsOn** collection.</span></span> <span data-ttu-id="d8f87-150">VM, hello kullanılabilirlik kümesi ve hello depolama hesabı ile birlikte dağıtılan hello önce oluşturulan gerekli toobe olan iki NIC listeler.</span><span class="sxs-lookup"><span data-stu-id="d8f87-150">It lists two NICs being necessary toobe created before hello VM is deployed, along with hello availability set, and hello storage account.</span></span>

    ```json
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('dbVMSetting').vmName,copyindex(1))]",
    "location": "[variables('location')]",
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-RA-', copyindex(1))]",
      "[concat('Microsoft.Compute/availabilitySets/', variables('dbVMSetting').avsetName)]",
      "[concat('Microsoft.Storage/storageAccounts/', parameters('prmStorageName'))]"
    ],
    "tags": {
      "displayName": "VMs - DB"
    },
    "copy": {
      "name": "dbvmcount",
      "count": "[parameters('dbCount')]"
    },
    ```

12. <span data-ttu-id="d8f87-151">Aşağı kaydırın hello VM kaynak toohello **networkProfile** aşağıda listelenen öğesi.</span><span class="sxs-lookup"><span data-stu-id="d8f87-151">Scroll down in hello VM resource toohello **networkProfile** element, as listed below.</span></span> <span data-ttu-id="d8f87-152">Her VM için başvuru olan iki NIC olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d8f87-152">Notice that there are two NICs being reference for each VM.</span></span> <span data-ttu-id="d8f87-153">Bir VM için birden çok NIC oluşturduğunuzda, hello ayarlamalısınız **birincil** hello NIC'ler birinin özelliği çok*true*, ve rest çok hello*false*.</span><span class="sxs-lookup"><span data-stu-id="d8f87-153">When you create multiple NICs for a VM, you must set hello **primary** property of one of hello NICs too*true*, and hello rest too*false*.</span></span>

    ```json
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-DA-',copyindex(1)))]",
          "properties": { "primary": true }
        },
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-RA-',copyindex(1)))]",
          "properties": { "primary": false }
        }
      ]
    }
    ```

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a><span data-ttu-id="d8f87-154">Kullanarak Hello ARM şablonu dağıtma toodeploy tıklatın</span><span class="sxs-lookup"><span data-stu-id="d8f87-154">Deploy hello ARM template by using click toodeploy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d8f87-155">Merhaba izlediğinizden emin olun [ön koşullar](#Pre-requisites) hello yönergeleri izleyerek önce adımları.</span><span class="sxs-lookup"><span data-stu-id="d8f87-155">Make sure you follow hello [pre-requisites](#Pre-requisites) steps before following hello instructions below.</span></span>
> 

<span data-ttu-id="d8f87-156">Merhaba örnek şablonunda kullanılabilir hello genel depo yukarıda açıklanan hello varsayılan kullanılan değerler toogenerate hello senaryosu içeren bir parametre dosyası kullanır.</span><span class="sxs-lookup"><span data-stu-id="d8f87-156">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="d8f87-157">toodeploy tıklatın toodeploy, bu şablonu kullanarak izleyin [bu bağlantıyı](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), sağ toohello **arka uç kaynak grubu (belgelere bakın)** tıklatın **tooAzure dağıtmak**, Değiştir Varsayılan parametre değerlerini gerekirse hello ve hello hello Portalı'ndaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="d8f87-157">toodeploy this template using click toodeploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), toohello right of **Backend resource group (see documentation)** click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

<span data-ttu-id="d8f87-158">Aşağıdaki Hello şekilde hello yeni kaynak grubu Merhaba içeriğine dağıtımdan sonra gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d8f87-158">hello figure below shows hello contents of hello new resource group, after deployment.</span></span>

![Arka uç kaynak grubu](./media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="d8f87-160">PowerShell kullanarak Hello şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="d8f87-160">Deploy hello template by using PowerShell</span></span>
<span data-ttu-id="d8f87-161">PowerShell kullanarak yüklediğiniz toodeploy hello şablon PowerShell'i yükleme ve hello hello adımları izleyerek yapılandırma [PowerShell'i yükleme ve yapılandırma](/powershell/azure/overview) makalesi ve hello aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="d8f87-161">toodeploy hello template you downloaded by using PowerShell, install and configure PowerShell by completing hello steps in hello [Install and configure PowerShell](/powershell/azure/overview) article and then complete hello following steps:</span></span>

<span data-ttu-id="d8f87-162">Merhaba çalıştırmak  **`New-AzureRmResourceGroup`**  kullanarak bir kaynak grubu cmdlet toocreate hello şablonu.</span><span class="sxs-lookup"><span data-stu-id="d8f87-162">Run hello **`New-AzureRmResourceGroup`** cmdlet toocreate a resource group using hello template.</span></span>

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

<span data-ttu-id="d8f87-163">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="d8f87-163">Expected output:</span></span>

    ResourceGroupName : IaaSStory-Backend
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    Permissions       :
                        Actions  NotActions
                        =======  ==========
                        *
        Resources         :
                        Name                 Type                                 Location
                        ===================  ===================================  ========
                        ASDB                 Microsoft.Compute/availabilitySets   westus  
                        DB1                  Microsoft.Compute/virtualMachines    westus  
                        DB2                  Microsoft.Compute/virtualMachines    westus  
                        NICDB-DA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-DA-2           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-2           Microsoft.Network/networkInterfaces  westus  
                        wtestvnetstorageprm  Microsoft.Storage/storageAccounts    westus  
    ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="d8f87-164">Hello Azure CLI kullanarak Hello şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="d8f87-164">Deploy hello template by using hello Azure CLI</span></span>
<span data-ttu-id="d8f87-165">hello Azure CLI kullanarak toodeploy hello şablon hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="d8f87-165">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="d8f87-166">Azure CLI hiç kullanmadıysanız bkz [hello Azure CLI yükleyip](../cli-install-nodejs.md) ve sonra Azure hesabınızı ve aboneliğinizi toohello noktaya hello talimatlarını izleyin.</span><span class="sxs-lookup"><span data-stu-id="d8f87-166">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="d8f87-167">Merhaba çalıştırmak  **`azure config mode`**  aşağıda gösterildiği gibi komut tooswitch tooResource Yöneticisi modu.</span><span class="sxs-lookup"><span data-stu-id="d8f87-167">Run hello **`azure config mode`** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="d8f87-168">Çıktı aşağıdaki Hello beklenen:</span><span class="sxs-lookup"><span data-stu-id="d8f87-168">hello expected output follows:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="d8f87-169">Açık hello [parametre dosyası](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json)içeriğini seçin ve tooa dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d8f87-169">Open hello [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), select its contents, and save it tooa file in your computer.</span></span> <span data-ttu-id="d8f87-170">Bu örnekte, hello parametreler dosyası çok kaydettik*parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="d8f87-170">For this example, we saved hello parameters file too*parameters.json*.</span></span>
4. <span data-ttu-id="d8f87-171">Merhaba çalıştırmak  **`azure group deployment create`**  cmdlet toodeploy hello hello şablonu ve parametre kullanarak yeni Vnet'i, yukarıda indirdiğiniz ve değiştirdiğiniz dosyaları.</span><span class="sxs-lookup"><span data-stu-id="d8f87-171">Run hello **`azure group deployment create`** cmdlet toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="d8f87-172">Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d8f87-172">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    <span data-ttu-id="d8f87-173">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="d8f87-173">Expected output:</span></span>
   
        info:    Executing command group create
        + Getting resource group IaaSStory-Backend
        + Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

