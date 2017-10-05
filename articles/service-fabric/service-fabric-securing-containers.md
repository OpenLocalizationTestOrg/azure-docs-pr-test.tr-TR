---
title: "Azure Service Fabric kapsayıcı güvenlik | Microsoft Docs"
description: "Şimdi güvenli kapsayıcı hizmetleri öğrenin."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 75faca1e827a0eca6b97adcb2e1c6ca72b3364d6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="container-security"></a>Kapsayıcı güvenlik

Service Fabric kümesindeki düğümlere bir Windows veya Linux (sürüm 5.7 veya üstü) yüklü bir sertifika erişmek için bir kapsayıcı içindeki hizmetler için bir mekanizma sağlar. Ayrıca, Service Fabric Windows kapsayıcıları için de gMSA (Grup yönetilen hizmet hesapları) destekler. 

## <a name="certificate-management-for-containers"></a>Kapsayıcıları için sertifika yönetimi

Bir sertifika belirterek, kapsayıcı hizmetlerini güvenliğini sağlayabilirsiniz. Sertifika, küme düğümlerinde yüklü olmalıdır. Sertifika bilgilerini altında uygulama bildiriminde sağlanan `ContainerHostPolicies` aşağıdaki kod parçacığında gösterildiği gibi etiketi:

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

Uygulama başlatılırken çalışma zamanı sertifikaları okur ve bir PFX dosyası ve her sertifika için parola oluşturur. Bu PFX dosyası ve parola, aşağıdaki ortam değişkenlerini kullanma kapsayıcısı içindeki erişilebilir: 

* **Certificate_ [CodePackageName] _ [CertName] _PFX**
* **Certificate_ [CodePackageName] _ [CertName] _Password**

Kapsayıcı hizmeti veya işlem kapsayıcıya PFX dosyasını içeri aktarmak için sorumludur. Sertifikayı içeri aktarmak için kullanabilirsiniz `setupentrypoint.sh` komut dosyaları veya özel kod kapsayıcı işlemi içinde yürütülür. C# örnek kod PFX dosyasını içeri aktarmak için aşağıdaki gibidir:

```c#
    string certificateFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_PFX");
    string passwordFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_Password");
    X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
    string password = File.ReadAllLines(passwordFilePath, Encoding.Default)[0];
    password = password.Replace("\0", string.Empty);
    X509Certificate2 cert = new X509Certificate2(certificateFilePath, password, X509KeyStorageFlags.MachineKeySet | X509KeyStorageFlags.PersistKeySet);
    store.Open(OpenFlags.ReadWrite);
    store.Add(cert);
    store.Close();
```
Bu PFX sertifika için kullanılabilmesi için uygulama veya hizmet veya diğer hizmetleri ile güvenli commmunication kimlik doğrulaması.


## <a name="set-up-gmsa-for-windows-containers"></a>GMSA Windows kapsayıcıları için ayarlama

Bir kimlik bilgisi belirtimi dosyası gmsa'yı (Grup yönetilen hizmet hesapları) ayarlamak için (`credspec`) kümedeki tüm düğümlere yerleştirilir. Dosya bir VM uzantısı kullanılarak tüm düğümlerde kopyalanabilir.  `credspec` Dosya gMSA hesabı bilgileri içermesi gerekir. Daha fazla bilgi için `credspec` dosya için bkz: [hizmet hesaplarını](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts). Kimlik bilgisi belirtimi ve `Hostname` etiketi, uygulama bildiriminde belirtilir. `Hostname` Etiketi kapsayıcı çalıştığı gMSA hesabı adı eşleşmelidir.  `Hostname` Etiketi Kerberos kimlik doğrulaması kullanarak etki alanındaki diğer hizmetler için kendi kimliğini doğrulamak kapsayıcı sağlar.  Belirtmek için bir örnek `Hostname` ve `credspec` uygulama bildirimi aşağıdaki kod parçacığında gösterilir:

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a>Sonraki adımlar

* [Windows Server 2016 Service Fabric Windows kapsayıcı dağıtma](service-fabric-get-started-containers.md)
* [Service Fabric Linux'ta Docker kapsayıcısı dağıtma](service-fabric-get-started-containers-linux.md)
