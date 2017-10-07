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
# <a name="create-and-manage-windows-vms-in-azure-using-java"></a>Oluşturma ve Java kullanarak azure'da Windows sanal makineleri yönetme

Bir [Azure sanal makine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) çeşitli destekleyici Azure kaynakları gerekir. Bu makalede, oluşturma, yönetme ve Java kullanarak VM kaynakları silme yer almaktadır. Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:

> [!div class="checklist"]
> * Bir Maven projesi oluşturun
> * Bağımlılıkları ekleyin.
> * Kimlik bilgileri oluşturun
> * Kaynak oluşturma
> * Yönetim görevlerini gerçekleştirme
> * Kaynakları silin
> * Merhaba uygulamayı çalıştırın

Bu adımları toodo yaklaşık 20 dakika sürer.

## <a name="create-a-maven-project"></a>Bir Maven projesi oluşturun

1. Zaten yapmadıysanız, yükleme [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
2. Yükleme [Maven](http://maven.apache.org/download.cgi).
3. Yeni bir klasör ve başlangıç projesi oluşturun:
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a>Bağımlılıkları ekleyin.

1. Merhaba altında `testAzureApp` klasörü, açık hello `pom.xml` dosya ve hello yapı yapılandırma çok ekleyin&lt;proje&gt; tooenable hello yapı, uygulamanızın:

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

2. Gerekli tooaccess hello Azure Java SDK'sını hello bağımlılıklar ekleyin.

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

3. Merhaba dosyasını kaydedin.

## <a name="create-credentials"></a>Kimlik bilgileri oluşturun

Bu adım başlamadan önce erişim tooan sahip olduğunuzdan emin olun [Active Directory hizmet asıl](../../azure-resource-manager/resource-group-create-service-principal-portal.md). Ayrıca bir sonraki adımda hello uygulama kimliği, hello kimlik doğrulama anahtarı ve ihtiyacınız hello Kiracı kimliği kaydetmelisiniz.

### <a name="create-hello-authorization-file"></a>Merhaba yetkilendirme dosyası oluşturma

1. Adlı bir dosya oluşturun `azureauth.properties` ve bu özellikler tooit ekleyin:

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

    Değiştir  **&lt;abonelik kimliği&gt;**  , abonelik tanımlayıcısı ile  **&lt;uygulama kimliği&gt;**  hello Active Directory uygulaması ile tanımlayıcı,  **&lt;kimlik doğrulama anahtarı&gt;**  hello uygulama anahtarla ve  **&lt;Kiracı kimliği&gt;**  hello Kiracı tanımlayıcı.

2. Merhaba dosyasını kaydedin.
3. AZURE_AUTH_LOCATION Kabuğu'nda hello tam yolu toohello kimlik doğrulaması dosyasıyla adlı bir ortam değişkeni ayarlayın.

### <a name="create-hello-management-client"></a>Merhaba yönetim istemcisi oluşturma

1. Açık hello `App.java` altında dosya `src\main\java\com\fabrikam` ve bu paket bildirimi hello üstünde olduğundan emin olun:

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. Merhaba paket altında bu deyimine deyimleri içeri aktarın:
   
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

2. toocreate hello Active Directory kimlik bilgileri toomake istekleri gereksinim hello uygulama sınıfı, bu kod toohello ana yöntemi ekleyin:
   
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

## <a name="create-resources"></a>Kaynak oluşturma

### <a name="create-hello-resource-group"></a>Merhaba kaynak grubu oluştur

Tüm kaynaklar içinde bulunması gereken bir [kaynak grubu](../../azure-resource-manager/resource-group-overview.md).

toospecify değerleri Merhaba uygulama ve hello kaynak grubu oluşturmak, bu kod toohello try bloğu hello ana yönteminde ekleyin:

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-hello-availability-set"></a>Merhaba kullanılabilirlik kümesi oluştur

[Kullanılabilirlik kümeleri](tutorial-availability-sets.md) sizin için toomaintain hello sanal makineler, uygulamanız tarafından kullanılan kolaylaştırır.

toocreate hello kullanılabilirlik kümesi, bu kod toohello try bloğu hello ana yönteminde ekleyin:

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-hello-public-ip-address"></a>Merhaba ortak IP adresi oluştur

A [genel IP adresi](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) hello sanal makineyle gerekli toocommunicate değil.

toocreate hello hello sanal makine için genel IP adresi bu kodu toohello try bloğu hello ana yönteminde ekleyin:

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-hello-virtual-network"></a>Merhaba sanal ağ oluşturma

Bir sanal makine bir alt ağda olmalıdır bir [sanal ağ](../../virtual-network/virtual-networks-overview.md).

alt ağ a toocreate ve bir sanal ağ hello ana yönteminde bu kodu toohello try bloğu ekleyin:

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

### <a name="create-hello-network-interface"></a>Merhaba ağ arabirimi oluştur

Bir sanal makine bir ağ arabirimi toocommunicate hello sanal ağda gerekir.

toocreate bir ağ arabirimi, bu kod toohello try bloğu hello ana yönteminde ekleyin:

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

### <a name="create-hello-virtual-machine"></a>Merhaba sanal makine oluşturma

Kaynakları destekleyen tüm hello oluşturduğunuza göre bir sanal makine oluşturabilirsiniz.

toocreate Merhaba sanal makine, bu kod toohello try bloğu hello ana yönteminde ekleyin:

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
> Bu öğretici hello Windows Server işletim sistemi sürümünü çalıştıran bir sanal makine oluşturur. diğer görüntüleri seçme hakkında daha fazla toolearn bkz [erişin ve seçin, Windows PowerShell ve Azure CLI hello Azure sanal makine görüntülerini](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
>

Varolan bir diski bir Market görüntüsü yerine toouse istiyorsanız, bu kodu kullanın: 

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

## <a name="perform-management-tasks"></a>Yönetim görevlerini gerçekleştirme

Bir sanal makine Hello yaşam döngüsü sırasında başlatma, durdurma veya bir sanal makine silme gibi yönetim görevleri toorun isteyebilirsiniz. Ayrıca, toocreate, kod tooautomate yineleyen veya karmaşık görevleri isteyebilirsiniz.

Merhaba VM ile herhangi bir şey toodo gerektiğinde, tooget bir örneği gerekir. Bu kod toohello try bloğu hello main yöntemi ekleyin:

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-hello-vm"></a>Merhaba VM hakkında bilgi edinin

Merhaba sanal makine hakkında tooget bilgi hello ana yönteminde bu kodu toohello try bloğu ekleyin:

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

### <a name="stop-hello-vm"></a>Merhaba VM Durdur

Bir sanal makineyi durdurmak ve tüm ayarları korumak, ancak toobe için sizden ücret veya bir sanal makineyi durdurun ve bunu serbest bırakma devam edin. Bir sanal makine serbest bırakıldığında, kendisiyle ilişkili tüm kaynakları da deallocated ve fatura onun için edilir.

serbest bırakma olmadan toostop hello sanal makine bu kodu toohello try bloğu hello ana yönteminde ekleyin:

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

Toodeallocate hello sanal makine istiyorsanız hello kapalı çağrısı toothis kodu değiştirin:

```java
vm.deallocate();
```

### <a name="start-hello-vm"></a>Merhaba VM Başlat

toostart Merhaba sanal makine, bu kod toohello try bloğu hello ana yönteminde ekleyin:

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="resize-hello-vm"></a>Merhaba VM yeniden boyutlandırma

Dağıtım pek çok görünüşünün sanal makineniz için bir boyut karar verirken dikkate alınmalıdır. Daha fazla bilgi için bkz: [VM boyutları](sizes.md).  

toochange boyutunu hello sanal makine, bu kod toohello try bloğu hello ana yönteminde ekleyin:

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="add-a-data-disk-toohello-vm"></a>Bir veri diski toohello VM ekleme

tooadd bir veri diski toohello 2 GB boyutunda, olan sanal makineye sahip bir LUN 0 ve ReadWrite önbelleğe alma türü, bu kod toohello try bloğu hello ana yönteminde ekleyin:

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter toodelete resources...");
input.nextLine();
```

## <a name="delete-resources"></a>Kaynakları silin

Azure'da kullanılan kaynaklar için ücretlendirildiğinizden, her zaman artık gerekli olmayan iyi bir uygulama toodelete kaynaklarını aşıyor. Toodelete hello sanal makinelerin istediğiniz ve kaynakları destekleyen tüm hello tüm toodo varsa silme hello kaynak grubudur.

1. toodelete hello kaynak grubu, bu kod toohello try bloğu hello ana yönteminde ekleyin:
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. Merhaba App.java dosyasını kaydedin.

## <a name="run-hello-application"></a>Merhaba uygulamayı çalıştırın

Bu konsol uygulaması toorun başlangıç toofinish itibaren tümüyle yaklaşık beş dakika sürer.

1. toorun Merhaba uygulama, bu Maven komutunu kullanın:

    ```
    mvn compile exec:java
    ```

2. Tuşuna önce **Enter** toostart silme kaynakları, birkaç dakika sürebilir hello kaynak tooverify hello oluşturmayı hello Azure portalı. Merhaba dağıtım durumu toosee hello dağıtım bilgilerini'ı tıklatın.


## <a name="next-steps"></a>Sonraki adımlar
* Merhaba kullanma hakkında daha fazla bilgi edinin [Java için Azure kitaplıkları](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).

