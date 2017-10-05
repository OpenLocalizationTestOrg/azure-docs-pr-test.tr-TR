---
title: "Oluşturma ve Java kullanarak Azure sanal makinesi yönetme | Microsoft Docs"
description: "Bir sanal makine ve tüm destekleyici kaynakları dağıtmak için Java ve Azure Resource Manager'ı kullanın."
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
ms.openlocfilehash: b9e739a07c5863577285fb3a221b372b385c6762
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-java"></a><span data-ttu-id="46641-103">Oluşturma ve Java kullanarak azure'da Windows sanal makineleri yönetme</span><span class="sxs-lookup"><span data-stu-id="46641-103">Create and manage Windows VMs in Azure using Java</span></span>

<span data-ttu-id="46641-104">Bir [Azure sanal makine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) çeşitli destekleyici Azure kaynakları gerekir.</span><span class="sxs-lookup"><span data-stu-id="46641-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="46641-105">Bu makalede, oluşturma, yönetme ve Java kullanarak VM kaynakları silme yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="46641-105">This article covers creating, managing, and deleting VM resources using Java.</span></span> <span data-ttu-id="46641-106">Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="46641-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="46641-107">Bir Maven projesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="46641-107">Create a Maven project</span></span>
> * <span data-ttu-id="46641-108">Bağımlılıkları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="46641-108">Add dependencies</span></span>
> * <span data-ttu-id="46641-109">Kimlik bilgileri oluşturun</span><span class="sxs-lookup"><span data-stu-id="46641-109">Create credentials</span></span>
> * <span data-ttu-id="46641-110">Kaynak oluşturma</span><span class="sxs-lookup"><span data-stu-id="46641-110">Create resources</span></span>
> * <span data-ttu-id="46641-111">Yönetim görevlerini gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="46641-111">Perform management tasks</span></span>
> * <span data-ttu-id="46641-112">Kaynakları silin</span><span class="sxs-lookup"><span data-stu-id="46641-112">Delete resources</span></span>
> * <span data-ttu-id="46641-113">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="46641-113">Run the application</span></span>

<span data-ttu-id="46641-114">Bu adımların tamamlanması yaklaşık 20 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="46641-114">It takes about 20 minutes to do these steps.</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="46641-115">Bir Maven projesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="46641-115">Create a Maven project</span></span>

1. <span data-ttu-id="46641-116">Zaten yapmadıysanız, yükleme [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="46641-116">If you haven't already done so, install [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
2. <span data-ttu-id="46641-117">Yükleme [Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="46641-117">Install [Maven](http://maven.apache.org/download.cgi).</span></span>
3. <span data-ttu-id="46641-118">Yeni bir klasör ve projeyi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="46641-118">Create a new folder and the project:</span></span>
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a><span data-ttu-id="46641-119">Bağımlılıkları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="46641-119">Add dependencies</span></span>

1. <span data-ttu-id="46641-120">Altında `testAzureApp` klasörü, açık `pom.xml` dosya ve derleme yapılandırmasını eklemek &lt;proje&gt; uygulamanızın oluşturulmasını etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="46641-120">Under the `testAzureApp` folder, open the `pom.xml` file and add the build configuration to &lt;project&gt; to enable the building of your application:</span></span>

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

2. <span data-ttu-id="46641-121">Azure Java SDK'sını erişmek için gerekli bağımlılıkları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="46641-121">Add the dependencies that are needed to access the Azure Java SDK.</span></span>

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

3. <span data-ttu-id="46641-122">Dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="46641-122">Save the file.</span></span>

## <a name="create-credentials"></a><span data-ttu-id="46641-123">Kimlik bilgileri oluşturun</span><span class="sxs-lookup"><span data-stu-id="46641-123">Create credentials</span></span>

<span data-ttu-id="46641-124">Bu adım başlamadan önce erişimi olduğundan emin olun bir [Active Directory hizmet asıl](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="46641-124">Before you start this step, make sure that you have access to an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="46641-125">Uygulama kimliği, kimlik doğrulama anahtarı ve ihtiyacınız Kiracı kimliği bir sonraki adımda kaydetmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="46641-125">You should also record the application ID, the authentication key, and the tenant ID that you need in a later step.</span></span>

### <a name="create-the-authorization-file"></a><span data-ttu-id="46641-126">Yetkilendirme dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="46641-126">Create the authorization file</span></span>

1. <span data-ttu-id="46641-127">Adlı bir dosya oluşturun `azureauth.properties` ve bu özellikleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46641-127">Create a file named `azureauth.properties` and add these properties to it:</span></span>

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

    <span data-ttu-id="46641-128">Değiştir  **&lt;abonelik kimliği&gt;**  , abonelik tanımlayıcısı ile  **&lt;uygulama kimliği&gt;**  Active Directory Uygulama tanımlayıcısı ile  **&lt;kimlik doğrulama anahtarı&gt;**  uygulama anahtarla ve  **&lt;Kiracı kimliği&gt;**  , Kiracı tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="46641-128">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with the Active Directory application identifier, **&lt;authentication-key&gt;** with the application key, and **&lt;tenant-id&gt;** with the tenant identifier.</span></span>

2. <span data-ttu-id="46641-129">Dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="46641-129">Save the file.</span></span>
3. <span data-ttu-id="46641-130">Kimlik doğrulama dosyasının tam yolu ile Kabuk AZURE_AUTH_LOCATION adlı bir ortam değişkeni ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="46641-130">Set an environment variable named AZURE_AUTH_LOCATION in your shell with the full path to the authentication file.</span></span>

### <a name="create-the-management-client"></a><span data-ttu-id="46641-131">Yönetim istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="46641-131">Create the management client</span></span>

1. <span data-ttu-id="46641-132">Açık `App.java` altında dosya `src\main\java\com\fabrikam` ve bu paket bildirimi en üstte olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="46641-132">Open the `App.java` file under `src\main\java\com\fabrikam` and make sure this package statement is at the top:</span></span>

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. <span data-ttu-id="46641-133">Paket altında bu deyimine deyimleri içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="46641-133">Under the package statement, add these import statements:</span></span>
   
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

2. <span data-ttu-id="46641-134">İstekleri yapmanız gereken Active Directory kimlik bilgileri oluşturmak için bu kodu uygulama sınıfı ana yöntemine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46641-134">To create the Active Directory credentials that you need to make requests, add this code to the main method of the App class:</span></span>
   
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

## <a name="create-resources"></a><span data-ttu-id="46641-135">Kaynak oluşturma</span><span class="sxs-lookup"><span data-stu-id="46641-135">Create resources</span></span>

### <a name="create-the-resource-group"></a><span data-ttu-id="46641-136">Kaynak grubunu oluşturma</span><span class="sxs-lookup"><span data-stu-id="46641-136">Create the resource group</span></span>

<span data-ttu-id="46641-137">Tüm kaynaklar içinde bulunması gereken bir [kaynak grubu](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="46641-137">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="46641-138">Uygulama için değerleri belirtin ve kaynak grubu oluşturmak için ana yöntem try bloğunda bu kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46641-138">To specify values for the application and create the resource group, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-the-availability-set"></a><span data-ttu-id="46641-139">Kullanılabilirlik kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="46641-139">Create the availability set</span></span>

<span data-ttu-id="46641-140">[Kullanılabilirlik kümeleri](tutorial-availability-sets.md) uygulamanız tarafından kullanılan sanal makinelerin bakımını kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="46641-140">[Availability sets](tutorial-availability-sets.md) make it easier for you to maintain the virtual machines used by your application.</span></span>

<span data-ttu-id="46641-141">Kullanılabilirlik kümesi oluşturmak için ana yöntem try bloğunda bu kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46641-141">To create the availability set, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-the-public-ip-address"></a><span data-ttu-id="46641-142">Ortak IP adresi oluştur</span><span class="sxs-lookup"><span data-stu-id="46641-142">Create the public IP address</span></span>

<span data-ttu-id="46641-143">A [genel IP adresi](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) sanal makineyle iletişim kurmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="46641-143">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed to communicate with the virtual machine.</span></span>

<span data-ttu-id="46641-144">Sanal makine için genel IP adresi oluşturmak için ana yöntem try bloğunda bu kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46641-144">To create the public IP address for the virtual machine, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-the-virtual-network"></a><span data-ttu-id="46641-145">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="46641-145">Create the virtual network</span></span>

<span data-ttu-id="46641-146">Bir sanal makine bir alt ağda olmalıdır bir [sanal ağ](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="46641-146">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="46641-147">Bir alt ağ ve sanal ağ oluşturmak için ana yöntem try bloğunda bu kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46641-147">To create a subnet and a virtual network, add this code to the try block in the main method:</span></span>

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

### <a name="create-the-network-interface"></a><span data-ttu-id="46641-148">Ağ arabirimi oluştur</span><span class="sxs-lookup"><span data-stu-id="46641-148">Create the network interface</span></span>

<span data-ttu-id="46641-149">Bir sanal makinenin sanal ağ iletişim kurmak için bir ağ arabirimi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="46641-149">A virtual machine needs a network interface to communicate on the virtual network.</span></span>

<span data-ttu-id="46641-150">Bir ağ arabirimi oluşturmak için ana yöntem try bloğunda bu kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46641-150">To create a network interface, add this code to the try block in the main method:</span></span>

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

### <a name="create-the-virtual-machine"></a><span data-ttu-id="46641-151">Sanal makineyi oluşturma</span><span class="sxs-lookup"><span data-stu-id="46641-151">Create the virtual machine</span></span>

<span data-ttu-id="46641-152">Tüm destekleyici kaynakları oluşturduğunuza göre bir sanal makine oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46641-152">Now that you created all the supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="46641-153">Sanal makine oluşturmak için ana yöntem try bloğunda bu kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46641-153">To create the virtual machine, add this code to the try block in the main method:</span></span>

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
System.out.println("Press enter to get information about the VM...");
input.nextLine();
```

> [!NOTE]
> <span data-ttu-id="46641-154">Bu öğretici, Windows Server işletim sistemi sürümünü çalıştıran bir sanal makine oluşturur.</span><span class="sxs-lookup"><span data-stu-id="46641-154">This tutorial creates a virtual machine running a version of the Windows Server operating system.</span></span> <span data-ttu-id="46641-155">Diğer görüntüleri seçme hakkında daha fazla bilgi için bkz: [erişin ve seçin, Windows PowerShell ve Azure CLI Azure sanal makine görüntülerini](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="46641-155">To learn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and the Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="46641-156">Varolan bir diski bir Market görüntüsü yerine kullanmak istiyorsanız, bu kodu kullanın:</span><span class="sxs-lookup"><span data-stu-id="46641-156">If you want to use an existing disk instead of a marketplace image, use this code:</span></span> 

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

## <a name="perform-management-tasks"></a><span data-ttu-id="46641-157">Yönetim görevlerini gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="46641-157">Perform management tasks</span></span>

<span data-ttu-id="46641-158">Bir sanal makine yaşam döngüsü sırasında başlatma, durdurma veya bir sanal makine silme gibi yönetim görevleri çalıştırmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46641-158">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="46641-159">Ayrıca, yinelenen veya karmaşık görevleri otomatikleştirmek için kod oluşturmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46641-159">Additionally, you may want to create code to automate repetitive or complex tasks.</span></span>

<span data-ttu-id="46641-160">VM ile herhangi bir şey yapmanız gerektiğinde bir örneğini almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="46641-160">When you need to do anything with the VM, you need to get an instance of it.</span></span> <span data-ttu-id="46641-161">Bu kod main yöntemini deneyin bloğunu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46641-161">Add this code to the try block of the main method:</span></span>

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-the-vm"></a><span data-ttu-id="46641-162">VM hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="46641-162">Get information about the VM</span></span>

<span data-ttu-id="46641-163">Sanal makine hakkında bilgi almak için ana yöntem try bloğunda bu kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46641-163">To get information about the virtual machine, add this code to the try block in the main method:</span></span>

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
System.out.println("Press enter to continue...");
input.nextLine();   
```

### <a name="stop-the-vm"></a><span data-ttu-id="46641-164">VM’yi durdurma</span><span class="sxs-lookup"><span data-stu-id="46641-164">Stop the VM</span></span>

<span data-ttu-id="46641-165">Bir sanal makineyi durdurun ve tüm ayarları korumak ancak bunun için sizden ücret devam ya da sanal makineyi durdurun ve bunu serbest bırakma.</span><span class="sxs-lookup"><span data-stu-id="46641-165">You can stop a virtual machine and keep all its settings, but continue to be charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="46641-166">Bir sanal makine serbest bırakıldığında, kendisiyle ilişkili tüm kaynakları da deallocated ve fatura onun için edilir.</span><span class="sxs-lookup"><span data-stu-id="46641-166">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="46641-167">Serbest bırakma olmadan sanal makineyi durdurmak için ana yöntem try bloğunda bu kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46641-167">To stop the virtual machine without deallocating it, add this code to the try block in the main method:</span></span>

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter to continue...");
input.nextLine();
```

<span data-ttu-id="46641-168">Sanal makine ayırması istiyorsanız, bu kod kapalı çağrısı değiştirin:</span><span class="sxs-lookup"><span data-stu-id="46641-168">If you want to deallocate the virtual machine, change the PowerOff call to this code:</span></span>

```java
vm.deallocate();
```

### <a name="start-the-vm"></a><span data-ttu-id="46641-169">VM Başlat</span><span class="sxs-lookup"><span data-stu-id="46641-169">Start the VM</span></span>

<span data-ttu-id="46641-170">Sanal makineyi başlatmak için ana yöntem try bloğunda bu kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46641-170">To start the virtual machine, add this code to the try block in the main method:</span></span>

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter to continue...");
input.nextLine();
```

### <a name="resize-the-vm"></a><span data-ttu-id="46641-171">VM'yi yeniden boyutlandırın</span><span class="sxs-lookup"><span data-stu-id="46641-171">Resize the VM</span></span>

<span data-ttu-id="46641-172">Dağıtım pek çok görünüşünün sanal makineniz için bir boyut karar verirken dikkate alınmalıdır.</span><span class="sxs-lookup"><span data-stu-id="46641-172">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="46641-173">Daha fazla bilgi için bkz: [VM boyutları](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="46641-173">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="46641-174">Sanal makine boyutunu değiştirmek için ana yöntem try bloğunda bu kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46641-174">To change size of the virtual machine, add this code to the try block in the main method:</span></span>

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter to continue...");
input.nextLine();
```

### <a name="add-a-data-disk-to-the-vm"></a><span data-ttu-id="46641-175">VM için bir veri diski Ekle</span><span class="sxs-lookup"><span data-stu-id="46641-175">Add a data disk to the VM</span></span>

<span data-ttu-id="46641-176">Bir veri diski boyutu 2 GB ise, bir LUN 0 ve ReadWrite önbelleğe alma türü sahip sanal makine eklemek için ana yöntem try bloğunda bu kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46641-176">To add a data disk to the virtual machine that is 2 GB in size, has a LUN of 0, and a caching type of ReadWrite, add this code to the try block in the main method:</span></span>

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter to delete resources...");
input.nextLine();
```

## <a name="delete-resources"></a><span data-ttu-id="46641-177">Kaynakları silin</span><span class="sxs-lookup"><span data-stu-id="46641-177">Delete resources</span></span>

<span data-ttu-id="46641-178">Azure'da kullanılan kaynaklar için ücretlendirildiğinizden, her zaman artık gerekli olmayan kaynakları silmek için iyi bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="46641-178">Because you are charged for resources used in Azure, it is always good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="46641-179">Sanal makineler ve destekleyici tüm kaynakları silmek istiyorsanız, tüm yapmanız gereken olan kaynak grubunu silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46641-179">If you want to delete the virtual machines and all the supporting resources, all you have to do is delete the resource group.</span></span>

1. <span data-ttu-id="46641-180">Kaynak grubunu silmek için ana yöntem try bloğunda bu kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46641-180">To delete the resource group, add this code to the try block in the main method:</span></span>
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. <span data-ttu-id="46641-181">App.java dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="46641-181">Save the App.java file.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="46641-182">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="46641-182">Run the application</span></span>

<span data-ttu-id="46641-183">Tamamlamak için bu konsol uygulamasını tamamen çalıştırın yaklaşık beş dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="46641-183">It should take about five minutes for this console application to run completely from start to finish.</span></span>

1. <span data-ttu-id="46641-184">Uygulamayı çalıştırmak için bu Maven komutunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="46641-184">To run the application, use this Maven command:</span></span>

    ```
    mvn compile exec:java
    ```

2. <span data-ttu-id="46641-185">Tuşuna önce **Enter** kaynakları silme başlatmak için Azure portalında kaynakların oluşturulmasını doğrulamak için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="46641-185">Before you press **Enter** to start deleting resources, you could take a few minutes to verify the creation of the resources in the Azure portal.</span></span> <span data-ttu-id="46641-186">Dağıtım hakkında bilgi için dağıtım durumunu tıklatın.</span><span class="sxs-lookup"><span data-stu-id="46641-186">Click the deployment status to see information about the deployment.</span></span>


## <a name="next-steps"></a><span data-ttu-id="46641-187">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="46641-187">Next steps</span></span>
* <span data-ttu-id="46641-188">Kullanma hakkında daha fazla bilgi edinin [Java için Azure kitaplıkları](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span><span class="sxs-lookup"><span data-stu-id="46641-188">Learn more about using the [Azure libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span></span>

