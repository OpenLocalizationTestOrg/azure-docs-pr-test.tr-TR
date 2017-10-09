---
title: "Service Fabric kapsayıcı güvenlik aaaAzure | Microsoft Docs"
description: "Şimdi toosecure kapsayıcı hizmetlerini öğrenin."
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
ms.openlocfilehash: 88faf4e8f949c2f7743756b6272ca672d9710630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="container-security"></a>Kapsayıcı güvenlik

Service Fabric hello kümedeki düğümlere bir Windows veya Linux (sürüm 5.7 veya üstü) yüklü bir Sertifika Hizmetleri bir kapsayıcı tooaccess içinde bir mekanizma sağlar. Ayrıca, Service Fabric Windows kapsayıcıları için de gMSA (Grup yönetilen hizmet hesapları) destekler. 

## <a name="certificate-management-for-containers"></a>Kapsayıcıları için sertifika yönetimi

Bir sertifika belirterek, kapsayıcı hizmetlerini güvenliğini sağlayabilirsiniz. Merhaba sertifika hello hello küme düğümlerinde yüklü olmalıdır. Merhaba sertifika bilgilerini hello altında hello uygulama bildiriminde sağlanan `ContainerHostPolicies` etiketi aşağıdaki kod parçacığında gösterildiği hello olarak:

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

Merhaba uygulama başlatılırken hello çalışma zamanı hello sertifikaları okur ve bir PFX dosyası ve her sertifika için parola oluşturur. Bu PFX dosyası ve parola, ortam değişkenleri aşağıdaki hello kullanarak hello kapsayıcısı içindeki erişilebilir: 

* **Certificate_ [CodePackageName] _ [CertName] _PFX**
* **Certificate_ [CodePackageName] _ [CertName] _Password**

Merhaba kapsayıcı hizmeti ya da işlem hello kapsayıcıya hello PFX dosyasını içeri aktarmak için sorumludur. kullanabileceğiniz tooimport hello sertifika `setupentrypoint.sh` komut dosyaları veya özel kod hello kapsayıcı işlemi içinde yürütülür. C# örnek kod hello PFX dosyasını içeri aktarmak için aşağıdaki gibidir:

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
Bu PFX sertifika kimlik doğrulaması yap hello uygulama veya hizmet ya da diğer hizmetleri ile güvenli commmunication için kullanılabilir.


## <a name="set-up-gmsa-for-windows-containers"></a>GMSA Windows kapsayıcıları için ayarlama

gMSA (Grup yönetilen hizmet hesapları), bir kimlik bilgisi belirtimi dosyası yukarı tooset (`credspec`) hello kümedeki tüm düğümlere yerleştirilir. bir VM uzantısı kullanılarak tüm düğümlerde Hello dosya kopyalanabilir.  Merhaba `credspec` dosya hello gMSA hesabı bilgileri içermesi gerekir. Merhaba hakkında daha fazla bilgi için `credspec` dosya için bkz: [hizmet hesaplarını](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts). Merhaba kimlik bilgisi belirtimi ve hello `Hostname` etiketi hello uygulama bildiriminde belirtilir. Merhaba `Hostname` etiketi altında kapsayıcı çalıştığı hello hello gMSA hesabı adı eşleşmelidir.  Merhaba `Hostname` etiketi hello kapsayıcı tooauthenticate kendisini Kerberos kimlik doğrulaması kullanarak hello etki alanındaki tooother hizmetleri sağlar.  Merhaba belirtmek için bir örnek `Hostname` ve hello `credspec` hello uygulama bildirimi parçacığını aşağıdaki hello gösterilir:

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a>Sonraki adımlar

* [Bir Windows kapsayıcı tooService Windows Server 2016 doku dağıtma](service-fabric-get-started-containers.md)
* [Docker kapsayıcısı tooService doku Linux'ta dağıtma](service-fabric-get-started-containers-linux.md)
