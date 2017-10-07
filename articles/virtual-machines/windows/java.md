---
title: "aaaCreate ve bir Azure sanal makine Java kullanarak yönetme | Microsoft Docs"
description: "Java ve Azure Resource Manager toodeploy bir sanal makine ve tüm destekleyici kaynakları kullanın."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 31ac8d59f92ecff887e64906940933dd6fd50815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-java"></a><span data-ttu-id="3286d-103">Oluşturma ve Java kullanarak azure'da Windows sanal makineleri yönetme</span><span class="sxs-lookup"><span data-stu-id="3286d-103">Create and manage Windows VMs in Azure using Java</span></span>

<span data-ttu-id="3286d-104">Bir [Azure sanal makine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) çeşitli destekleyici Azure kaynakları gerekir.</span><span class="sxs-lookup"><span data-stu-id="3286d-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="3286d-105">Bu makalede, oluşturma, yönetme ve Java kullanarak VM kaynakları silme yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="3286d-105">This article covers creating, managing, and deleting VM resources using Java.</span></span> <span data-ttu-id="3286d-106">Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3286d-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3286d-107">Bir Maven projesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="3286d-107">Create a Maven project</span></span>
> * <span data-ttu-id="3286d-108">Bağımlılıkları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3286d-108">Add dependencies</span></span>
> * <span data-ttu-id="3286d-109">Kimlik bilgileri oluşturun</span><span class="sxs-lookup"><span data-stu-id="3286d-109">Create credentials</span></span>
> * <span data-ttu-id="3286d-110">Kaynak oluşturma</span><span class="sxs-lookup"><span data-stu-id="3286d-110">Create resources</span></span>
> * <span data-ttu-id="3286d-111">Yönetim görevlerini gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="3286d-111">Perform management tasks</span></span>
> * <span data-ttu-id="3286d-112">Kaynakları silin</span><span class="sxs-lookup"><span data-stu-id="3286d-112">Delete resources</span></span>
> * <span data-ttu-id="3286d-113">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="3286d-113">Run hello application</span></span>

<span data-ttu-id="3286d-114">Bu adımları toodo yaklaşık 20 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="3286d-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="3286d-115">Bir Maven projesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="3286d-115">Create a Maven project</span></span>

1. <span data-ttu-id="3286d-116">Zaten yapmadıysanız, yükleme [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="3286d-116">If you haven't already done so, install [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
2. <span data-ttu-id="3286d-117">Yükleme [Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="3286d-117">Install [Maven](http://maven.apache.org/download.cgi).</span></span>
3. <span data-ttu-id="3286d-118">Yeni bir klasör ve başlangıç projesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="3286d-118">Create a new folder and hello project:</span></span>
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a><span data-ttu-id="3286d-119">Bağımlılıkları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3286d-119">Add dependencies</span></span>

1. <span data-ttu-id="3286d-120">Merhaba altında `testAzureApp` klasörü, açık hello `pom.xml` dosya ve hello yapı yapılandırma çok ekleyin&lt;proje&gt; tooenable hello yapı, uygulamanızın:</span><span class="sxs-lookup"><span data-stu-id="3286d-120">Under hello `testAzureApp` folder, open hello `pom.xml` file and add hello build configuration too&lt;project&gt; tooenable hello building of your application:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <configuration>
                <mainClass>com.fabrikam.testAzureApp.App</mainClass>
            </configuration>
        </plugin>
      </plugins>
    </build>
    ```

2. <span data-ttu-id="3286d-121">Gerekli tooaccess hello Azure Java SDK'sını hello bağımlılıklar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3286d-121">Add hello dependencies that are needed tooaccess hello Azure Java SDK.</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-compute</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-resources</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-network</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.squareup.okio</groupId>
      <artifactId>okio</artifactId>
      <version>1.13.0</version>
    </dependency>
    <dependency> 
      <groupId>com.nimbusds</groupId>
      <artifactId>nimbus-jose-jwt</artifactId>
      <version>3.6</version>
    </dependency>
    <dependency>
      <groupId>net.minidev</groupId>
      <artifactId>json-smart</artifactId>
      <version>1.0.6.3</version>
    </dependency>
    <dependency>
      <groupId>javax.mail</groupId>
      <artifactId>mail</artifactId>
      <version>1.4.5</version>
    </dependency>
    ```

3. <span data-ttu-id="3286d-122">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3286d-122">Save hello file.</span></span>

## <a name="create-credentials"></a><span data-ttu-id="3286d-123">Kimlik bilgileri oluşturun</span><span class="sxs-lookup"><span data-stu-id="3286d-123">Create credentials</span></span>

<span data-ttu-id="3286d-124">Bu adım başlamadan önce erişim tooan sahip olduğunuzdan emin olun [Active Directory hizmet asıl](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3286d-124">Before you start this step, make sure that you have access tooan [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="3286d-125">Ayrıca bir sonraki adımda hello uygulama kimliği, hello kimlik doğrulama anahtarı ve ihtiyacınız hello Kiracı kimliği kaydetmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="3286d-125">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="3286d-126">Merhaba yetkilendirme dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="3286d-126">Create hello authorization file</span></span>

1. <span data-ttu-id="3286d-127">Adlı bir dosya oluşturun `azureauth.properties` ve bu özellikler tooit ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3286d-127">Create a file named `azureauth.properties` and add these properties tooit:</span></span>

    ```
    subscription=<subscription-id>
    client=<application-id>
    key=<authentication-key>
    tenant=<tenant-id>
    managementURI=https://management.core.windows.net/
    baseURL=https://management.azure.com/
    authURL=https://login.windows.net/
    graphURL=https://graph.windows.net/
    ```

    <span data-ttu-id="3286d-128">Değiştir  **&lt;abonelik kimliği&gt;**  , abonelik tanımlayıcısı ile  **&lt;uygulama kimliği&gt;**  hello Active Directory uygulaması ile tanımlayıcı,  **&lt;kimlik doğrulama anahtarı&gt;**  hello uygulama anahtarla ve  **&lt;Kiracı kimliği&gt;**  hello Kiracı tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="3286d-128">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

2. <span data-ttu-id="3286d-129">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3286d-129">Save hello file.</span></span>
3. <span data-ttu-id="3286d-130">AZURE_AUTH_LOCATION Kabuğu'nda hello tam yolu toohello kimlik doğrulaması dosyasıyla adlı bir ortam değişkeni ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3286d-130">Set an environment variable named AZURE_AUTH_LOCATION in your shell with hello full path toohello authentication file.</span></span>

### <a name="create-hello-management-client"></a><span data-ttu-id="3286d-131">Merhaba yönetim istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="3286d-131">Create hello management client</span></span>

1. <span data-ttu-id="3286d-132">Açık hello `App.java` altında dosya `src\main\java\com\fabrikam` ve bu paket bildirimi hello üstünde olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="3286d-132">Open hello `App.java` file under `src\main\java\com\fabrikam` and make sure this package statement is at hello top:</span></span>

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. <span data-ttu-id="3286d-133">Merhaba paket altında bu deyimine deyimleri içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="3286d-133">Under hello package statement, add these import statements:</span></span>
   
    ```java
    import com.microsoft.azure.management.Azure;
    import com.microsoft.azure.management.compute.AvailabilitySet;
    import com.microsoft.azure.management.compute.AvailabilitySetSkuTypes;
    import com.microsoft.azure.management.compute.CachingTypes;
    import com.microsoft.azure.management.compute.InstanceViewStatus;
    import com.microsoft.azure.management.compute.DiskInstanceView;
    import com.microsoft.azure.management.compute.VirtualMachine;
    import com.microsoft.azure.management.compute.VirtualMachineSizeTypes;
    import com.microsoft.azure.management.network.PublicIPAddress;
    import com.microsoft.azure.management.network.Network;
    import com.microsoft.azure.management.network.NetworkInterface;
    import com.microsoft.azure.management.resources.ResourceGroup;
    import com.microsoft.azure.management.resources.fluentcore.arm.Region;
    import com.microsoft.azure.management.resources.fluentcore.model.Creatable;
    import com.microsoft.rest.LogLevel;
    import java.io.File;
    import java.util.Scanner;
    ```

2. <span data-ttu-id="3286d-134">toocreate hello Active Directory kimlik bilgileri toomake istekleri gereksinim hello uygulama sınıfı, bu kod toohello ana yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3286d-134">toocreate hello Active Directory credentials that you need toomake requests, add this code toohello main method of hello App class:</span></span>
   
    ```java
    try {    
        final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
        Azure azure = Azure.configure()
            .withLogLevel(LogLevel.BASIC)
            .authenticate(credFile)
            .withDefaultSubscription();
    } catch (Exception e) {
        System.out.println(e.getMessage());
        e.printStackTrace();
    }

    ```

## <a name="create-resources"></a><span data-ttu-id="3286d-135">Kaynak oluşturma</span><span class="sxs-lookup"><span data-stu-id="3286d-135">Create resources</span></span>

### <a name="create-hello-resource-group"></a><span data-ttu-id="3286d-136">Merhaba kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="3286d-136">Create hello resource group</span></span>

<span data-ttu-id="3286d-137">Tüm kaynaklar içinde bulunması gereken bir [kaynak grubu](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3286d-137">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="3286d-138">toospecify değerleri Merhaba uygulama ve hello kaynak grubu oluşturmak, bu kod toohello try bloğu hello ana yönteminde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3286d-138">toospecify values for hello application and create hello resource group, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-hello-availability-set"></a><span data-ttu-id="3286d-139">Merhaba kullanılabilirlik kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="3286d-139">Create hello availability set</span></span>

<span data-ttu-id="3286d-140">[Kullanılabilirlik kümeleri](tutorial-availability-sets.md) sizin için toomaintain hello sanal makineler, uygulamanız tarafından kullanılan kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="3286d-140">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

<span data-ttu-id="3286d-141">toocreate hello kullanılabilirlik kümesi, bu kod toohello try bloğu hello ana yönteminde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3286d-141">toocreate hello availability set, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-hello-public-ip-address"></a><span data-ttu-id="3286d-142">Merhaba ortak IP adresi oluştur</span><span class="sxs-lookup"><span data-stu-id="3286d-142">Create hello public IP address</span></span>

<span data-ttu-id="3286d-143">A [genel IP adresi](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) hello sanal makineyle gerekli toocommunicate değil.</span><span class="sxs-lookup"><span data-stu-id="3286d-143">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

<span data-ttu-id="3286d-144">toocreate hello hello sanal makine için genel IP adresi bu kodu toohello try bloğu hello ana yönteminde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3286d-144">toocreate hello public IP address for hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-hello-virtual-network"></a><span data-ttu-id="3286d-145">Merhaba sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="3286d-145">Create hello virtual network</span></span>

<span data-ttu-id="3286d-146">Bir sanal makine bir alt ağda olmalıdır bir [sanal ağ](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3286d-146">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="3286d-147">alt ağ a toocreate ve bir sanal ağ hello ana yönteminde bu kodu toohello try bloğu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3286d-147">toocreate a subnet and a virtual network, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating virtual network...");
Network network = azure.networks()
    .define("myVN")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withAddressSpace("10.0.0.0/16")
    .withSubnet("mySubnet","10.0.0.0/24")
    .create();
```

### <a name="create-hello-network-interface"></a><span data-ttu-id="3286d-148">Merhaba ağ arabirimi oluştur</span><span class="sxs-lookup"><span data-stu-id="3286d-148">Create hello network interface</span></span>

<span data-ttu-id="3286d-149">Bir sanal makine bir ağ arabirimi toocommunicate hello sanal ağda gerekir.</span><span class="sxs-lookup"><span data-stu-id="3286d-149">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

<span data-ttu-id="3286d-150">toocreate bir ağ arabirimi, bu kod toohello try bloğu hello ana yönteminde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3286d-150">toocreate a network interface, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating network interface...");
NetworkInterface networkInterface = azure.networkInterfaces()
    .define("myNIC")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withExistingPrimaryNetwork(network)
    .withSubnet("mySubnet")
    .withPrimaryPrivateIPAddressDynamic()
    .withExistingPrimaryPublicIPAddress(publicIPAddress)
    .create();
```

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="3286d-151">Merhaba sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="3286d-151">Create hello virtual machine</span></span>

<span data-ttu-id="3286d-152">Kaynakları destekleyen tüm hello oluşturduğunuza göre bir sanal makine oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3286d-152">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="3286d-153">toocreate Merhaba sanal makine, bu kod toohello try bloğu hello ana yönteminde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3286d-153">toocreate hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating virtual machine...");
VirtualMachine virtualMachine = azure.virtualMachines()
    .define("myVM")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withExistingPrimaryNetworkInterface(networkInterface)
    .withLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .withAdminUsername("azureuser")
    .withAdminPassword("Azure12345678")
    .withComputerName("myVM")
    .withExistingAvailabilitySet(availabilitySet)
    .withSize("Standard_DS1")
    .create();
Scanner input = new Scanner(System.in);
System.out.println("Press enter tooget information about hello VM...");
input.nextLine();
```

> [!NOTE]
> <span data-ttu-id="3286d-154">Bu öğretici hello Windows Server işletim sistemi sürümünü çalıştıran bir sanal makine oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3286d-154">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="3286d-155">diğer görüntüleri seçme hakkında daha fazla toolearn bkz [erişin ve seçin, Windows PowerShell ve Azure CLI hello Azure sanal makine görüntülerini](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3286d-155">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="3286d-156">Varolan bir diski bir Market görüntüsü yerine toouse istiyorsanız, bu kodu kullanın:</span><span class="sxs-lookup"><span data-stu-id="3286d-156">If you want toouse an existing disk instead of a marketplace image, use this code:</span></span> 

```java
ManagedDisk managedDisk = azure.disks.define("myosdisk") 
    .withRegion(Region.US_EAST) 
    .withExistingResourceGroup("myResourceGroup") 
    .withWindowsFromVhd("https://mystorage.blob.core.windows.net/vhds/myosdisk.vhd") 
    .withSizeInGB(128) 
    .withSku(DiskSkuTypes.PremiumLRS) 
    .create(); 

azure.virtualMachines.define("myVM") 
    .withRegion(Region.US_EAST) 
    .withExistingResourceGroup("myResourceGroup") 
    .withExistingPrimaryNetworkInterface(networkInterface) 
    .withSpecializedOSDisk(managedDisk, OperatingSystemTypes.Windows) 
    .withExistingAvailabilitySet(availabilitySet) 
    .withSize(VirtualMachineSizeTypes.StandardDS1) 
    .create(); 
``` 

## <a name="perform-management-tasks"></a><span data-ttu-id="3286d-157">Yönetim görevlerini gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="3286d-157">Perform management tasks</span></span>

<span data-ttu-id="3286d-158">Bir sanal makine Hello yaşam döngüsü sırasında başlatma, durdurma veya bir sanal makine silme gibi yönetim görevleri toorun isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3286d-158">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="3286d-159">Ayrıca, toocreate, kod tooautomate yineleyen veya karmaşık görevleri isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3286d-159">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

<span data-ttu-id="3286d-160">Merhaba VM ile herhangi bir şey toodo gerektiğinde, tooget bir örneği gerekir.</span><span class="sxs-lookup"><span data-stu-id="3286d-160">When you need toodo anything with hello VM, you need tooget an instance of it.</span></span> <span data-ttu-id="3286d-161">Bu kod toohello try bloğu hello main yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3286d-161">Add this code toohello try block of hello main method:</span></span>

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="3286d-162">Merhaba VM hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="3286d-162">Get information about hello VM</span></span>

<span data-ttu-id="3286d-163">Merhaba sanal makine hakkında tooget bilgi hello ana yönteminde bu kodu toohello try bloğu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3286d-163">tooget information about hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("hardwareProfile");
System.out.println("    vmSize: " + vm.size());
System.out.println("storageProfile");
System.out.println("  imageReference");
System.out.println("    publisher: " + vm.storageProfile().imageReference().publisher());
System.out.println("    offer: " + vm.storageProfile().imageReference().offer());
System.out.println("    sku: " + vm.storageProfile().imageReference().sku());
System.out.println("    version: " + vm.storageProfile().imageReference().version());
System.out.println("  osDisk");
System.out.println("    osType: " + vm.storageProfile().osDisk().osType());
System.out.println("    name: " + vm.storageProfile().osDisk().name());
System.out.println("    createOption: " + vm.storageProfile().osDisk().createOption());
System.out.println("    caching: " + vm.storageProfile().osDisk().caching());
System.out.println("osProfile");
System.out.println("    computerName: " + vm.osProfile().computerName());
System.out.println("    adminUserName: " + vm.osProfile().adminUsername());
System.out.println("    provisionVMAgent: " + vm.osProfile().windowsConfiguration().provisionVMAgent());
System.out.println("    enableAutomaticUpdates: " + vm.osProfile().windowsConfiguration().enableAutomaticUpdates());
System.out.println("networkProfile");
System.out.println("    networkInterface: " + vm.primaryNetworkInterfaceId());
System.out.println("vmAgent");
System.out.println("  vmAgentVersion: " + vm.instanceView().vmAgent().vmAgentVersion());
System.out.println("    statuses");
for(InstanceViewStatus status : vm.instanceView().vmAgent().statuses()) {
    System.out.println("    code: " + status.code());
    System.out.println("    displayStatus: " + status.displayStatus());
    System.out.println("    message: " + status.message());
    System.out.println("    time: " + status.time());
}
System.out.println("disks");
for(DiskInstanceView disk : vm.instanceView().disks()) {
    System.out.println("  name: " + disk.name());
    System.out.println("  statuses");
    for(InstanceViewStatus status : disk.statuses()) {
        System.out.println("    code: " + status.code());
        System.out.println("    displayStatus: " + status.displayStatus());
        System.out.println("    time: " + status.time());
    }
}
System.out.println("VM general status");
System.out.println("  provisioningStatus: " + vm.provisioningState());
System.out.println("  id: " + vm.id());
System.out.println("  name: " + vm.name());
System.out.println("  type: " + vm.type());
System.out.println("VM instance status");
for(InstanceViewStatus status : vm.instanceView().statuses()) {
    System.out.println("  code: " + status.code());
    System.out.println("  displayStatus: " + status.displayStatus());
}
System.out.println("Press enter toocontinue...");
input.nextLine();   
```

### <a name="stop-hello-vm"></a><span data-ttu-id="3286d-164">Merhaba VM Durdur</span><span class="sxs-lookup"><span data-stu-id="3286d-164">Stop hello VM</span></span>

<span data-ttu-id="3286d-165">Bir sanal makineyi durdurmak ve tüm ayarları korumak, ancak toobe için sizden ücret veya bir sanal makineyi durdurun ve bunu serbest bırakma devam edin.</span><span class="sxs-lookup"><span data-stu-id="3286d-165">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="3286d-166">Bir sanal makine serbest bırakıldığında, kendisiyle ilişkili tüm kaynakları da deallocated ve fatura onun için edilir.</span><span class="sxs-lookup"><span data-stu-id="3286d-166">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="3286d-167">serbest bırakma olmadan toostop hello sanal makine bu kodu toohello try bloğu hello ana yönteminde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3286d-167">toostop hello virtual machine without deallocating it, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

<span data-ttu-id="3286d-168">Toodeallocate hello sanal makine istiyorsanız hello kapalı çağrısı toothis kodu değiştirin:</span><span class="sxs-lookup"><span data-stu-id="3286d-168">If you want toodeallocate hello virtual machine, change hello PowerOff call toothis code:</span></span>

```java
vm.deallocate();
```

### <a name="start-hello-vm"></a><span data-ttu-id="3286d-169">Merhaba VM Başlat</span><span class="sxs-lookup"><span data-stu-id="3286d-169">Start hello VM</span></span>

<span data-ttu-id="3286d-170">toostart Merhaba sanal makine, bu kod toohello try bloğu hello ana yönteminde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3286d-170">toostart hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="resize-hello-vm"></a><span data-ttu-id="3286d-171">Merhaba VM yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="3286d-171">Resize hello VM</span></span>

<span data-ttu-id="3286d-172">Dağıtım pek çok görünüşünün sanal makineniz için bir boyut karar verirken dikkate alınmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3286d-172">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="3286d-173">Daha fazla bilgi için bkz: [VM boyutları](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="3286d-173">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="3286d-174">toochange boyutunu hello sanal makine, bu kod toohello try bloğu hello ana yönteminde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3286d-174">toochange size of hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="3286d-175">Bir veri diski toohello VM ekleme</span><span class="sxs-lookup"><span data-stu-id="3286d-175">Add a data disk toohello VM</span></span>

<span data-ttu-id="3286d-176">tooadd bir veri diski toohello 2 GB boyutunda, olan sanal makineye sahip bir LUN 0 ve ReadWrite önbelleğe alma türü, bu kod toohello try bloğu hello ana yönteminde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3286d-176">tooadd a data disk toohello virtual machine that is 2 GB in size, has a LUN of 0, and a caching type of ReadWrite, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter toodelete resources...");
input.nextLine();
```

## <a name="delete-resources"></a><span data-ttu-id="3286d-177">Kaynakları silin</span><span class="sxs-lookup"><span data-stu-id="3286d-177">Delete resources</span></span>

<span data-ttu-id="3286d-178">Azure'da kullanılan kaynaklar için ücretlendirildiğinizden, her zaman artık gerekli olmayan iyi bir uygulama toodelete kaynaklarını aşıyor.</span><span class="sxs-lookup"><span data-stu-id="3286d-178">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="3286d-179">Toodelete hello sanal makinelerin istediğiniz ve kaynakları destekleyen tüm hello tüm toodo varsa silme hello kaynak grubudur.</span><span class="sxs-lookup"><span data-stu-id="3286d-179">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

1. <span data-ttu-id="3286d-180">toodelete hello kaynak grubu, bu kod toohello try bloğu hello ana yönteminde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3286d-180">toodelete hello resource group, add this code toohello try block in hello main method:</span></span>
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. <span data-ttu-id="3286d-181">Merhaba App.java dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3286d-181">Save hello App.java file.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="3286d-182">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="3286d-182">Run hello application</span></span>

<span data-ttu-id="3286d-183">Bu konsol uygulaması toorun başlangıç toofinish itibaren tümüyle yaklaşık beş dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="3286d-183">It should take about five minutes for this console application toorun completely from start toofinish.</span></span>

1. <span data-ttu-id="3286d-184">toorun Merhaba uygulama, bu Maven komutunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="3286d-184">toorun hello application, use this Maven command:</span></span>

    ```
    mvn compile exec:java
    ```

2. <span data-ttu-id="3286d-185">Tuşuna önce **Enter** toostart silme kaynakları, birkaç dakika sürebilir hello kaynak tooverify hello oluşturmayı hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="3286d-185">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="3286d-186">Merhaba dağıtım durumu toosee hello dağıtım bilgilerini'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3286d-186">Click hello deployment status toosee information about hello deployment.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3286d-187">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3286d-187">Next steps</span></span>
* <span data-ttu-id="3286d-188">Merhaba kullanma hakkında daha fazla bilgi edinin [Java için Azure kitaplıkları](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span><span class="sxs-lookup"><span data-stu-id="3286d-188">Learn more about using hello [Azure libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span></span>

