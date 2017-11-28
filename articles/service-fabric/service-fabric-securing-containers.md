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
# <a name="container-security"></a><span data-ttu-id="25e70-103">Kapsayıcı güvenlik</span><span class="sxs-lookup"><span data-stu-id="25e70-103">Container security</span></span>

<span data-ttu-id="25e70-104">Service Fabric kümesindeki düğümlere bir Windows veya Linux (sürüm 5.7 veya üstü) yüklü bir sertifika erişmek için bir kapsayıcı içindeki hizmetler için bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="25e70-104">Service Fabric provides a mechanism for services inside a container to access a certificate that is installed on the nodes in a Windows or Linux cluster (version 5.7 or higher).</span></span> <span data-ttu-id="25e70-105">Ayrıca, Service Fabric Windows kapsayıcıları için de gMSA (Grup yönetilen hizmet hesapları) destekler.</span><span class="sxs-lookup"><span data-stu-id="25e70-105">In addition, Service Fabric also supports gMSA (group Managed Service Accounts) for Windows containers.</span></span> 

## <a name="certificate-management-for-containers"></a><span data-ttu-id="25e70-106">Kapsayıcıları için sertifika yönetimi</span><span class="sxs-lookup"><span data-stu-id="25e70-106">Certificate management for containers</span></span>

<span data-ttu-id="25e70-107">Bir sertifika belirterek, kapsayıcı hizmetlerini güvenliğini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="25e70-107">You can secure your container services by specifying a certificate.</span></span> <span data-ttu-id="25e70-108">Sertifika, küme düğümlerinde yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="25e70-108">The certificate must be installed on the nodes of the cluster.</span></span> <span data-ttu-id="25e70-109">Sertifika bilgilerini altında uygulama bildiriminde sağlanan `ContainerHostPolicies` aşağıdaki kod parçacığında gösterildiği gibi etiketi:</span><span class="sxs-lookup"><span data-stu-id="25e70-109">The certificate information is provided in the application manifest under the `ContainerHostPolicies` tag as the following snippet shows:</span></span>

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

<span data-ttu-id="25e70-110">Uygulama başlatılırken çalışma zamanı sertifikaları okur ve bir PFX dosyası ve her sertifika için parola oluşturur.</span><span class="sxs-lookup"><span data-stu-id="25e70-110">When starting the application, the runtime reads the certificates and generates a PFX file and password for each certificate.</span></span> <span data-ttu-id="25e70-111">Bu PFX dosyası ve parola, aşağıdaki ortam değişkenlerini kullanma kapsayıcısı içindeki erişilebilir:</span><span class="sxs-lookup"><span data-stu-id="25e70-111">This PFX file and password are accessible inside the container using the following environment variables:</span></span> 

* <span data-ttu-id="25e70-112">**Certificate_ [CodePackageName] _ [CertName] _PFX**</span><span class="sxs-lookup"><span data-stu-id="25e70-112">**Certificate_[CodePackageName]_[CertName]_PFX**</span></span>
* <span data-ttu-id="25e70-113">**Certificate_ [CodePackageName] _ [CertName] _Password**</span><span class="sxs-lookup"><span data-stu-id="25e70-113">**Certificate_[CodePackageName]_[CertName]_Password**</span></span>

<span data-ttu-id="25e70-114">Kapsayıcı hizmeti veya işlem kapsayıcıya PFX dosyasını içeri aktarmak için sorumludur.</span><span class="sxs-lookup"><span data-stu-id="25e70-114">The container service or process is responsible for importing the PFX file into the container.</span></span> <span data-ttu-id="25e70-115">Sertifikayı içeri aktarmak için kullanabilirsiniz `setupentrypoint.sh` komut dosyaları veya özel kod kapsayıcı işlemi içinde yürütülür.</span><span class="sxs-lookup"><span data-stu-id="25e70-115">To import the certificate, you can use `setupentrypoint.sh` scripts or executed custom code within the container process.</span></span> <span data-ttu-id="25e70-116">C# örnek kod PFX dosyasını içeri aktarmak için aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="25e70-116">Sample code in C# for importing the PFX file follows:</span></span>

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
<span data-ttu-id="25e70-117">Bu PFX sertifika için kullanılabilmesi için uygulama veya hizmet veya diğer hizmetleri ile güvenli commmunication kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="25e70-117">This PFX certificate can be used for authenticate the application or service or secure commmunication with other services.</span></span>


## <a name="set-up-gmsa-for-windows-containers"></a><span data-ttu-id="25e70-118">GMSA Windows kapsayıcıları için ayarlama</span><span class="sxs-lookup"><span data-stu-id="25e70-118">Set up gMSA for Windows containers</span></span>

<span data-ttu-id="25e70-119">Bir kimlik bilgisi belirtimi dosyası gmsa'yı (Grup yönetilen hizmet hesapları) ayarlamak için (`credspec`) kümedeki tüm düğümlere yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="25e70-119">To set up gMSA (group Managed Service Accounts), a credential specification file (`credspec`) is placed on all nodes in the cluster.</span></span> <span data-ttu-id="25e70-120">Dosya bir VM uzantısı kullanılarak tüm düğümlerde kopyalanabilir.</span><span class="sxs-lookup"><span data-stu-id="25e70-120">The file can be copied on all nodes using a VM extension.</span></span>  <span data-ttu-id="25e70-121">`credspec` Dosya gMSA hesabı bilgileri içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="25e70-121">The `credspec` file must contain the gMSA account information.</span></span> <span data-ttu-id="25e70-122">Daha fazla bilgi için `credspec` dosya için bkz: [hizmet hesaplarını](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span><span class="sxs-lookup"><span data-stu-id="25e70-122">For more information on the `credspec` file, see [Service Accounts](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span></span> <span data-ttu-id="25e70-123">Kimlik bilgisi belirtimi ve `Hostname` etiketi, uygulama bildiriminde belirtilir.</span><span class="sxs-lookup"><span data-stu-id="25e70-123">The credential specification and the `Hostname` tag are specified in the application manifest.</span></span> <span data-ttu-id="25e70-124">`Hostname` Etiketi kapsayıcı çalıştığı gMSA hesabı adı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="25e70-124">The `Hostname` tag must match the gMSA account name that the container runs under.</span></span>  <span data-ttu-id="25e70-125">`Hostname` Etiketi Kerberos kimlik doğrulaması kullanarak etki alanındaki diğer hizmetler için kendi kimliğini doğrulamak kapsayıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="25e70-125">The `Hostname` tag allows the container to authenticate itself to other services in the domain using Kerberos authentication.</span></span>  <span data-ttu-id="25e70-126">Belirtmek için bir örnek `Hostname` ve `credspec` uygulama bildirimi aşağıdaki kod parçacığında gösterilir:</span><span class="sxs-lookup"><span data-stu-id="25e70-126">A sample for specifying the `Hostname` and the `credspec` in the application manifest is shown in the following snippet:</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="25e70-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="25e70-127">Next steps</span></span>

* [<span data-ttu-id="25e70-128">Windows Server 2016 Service Fabric Windows kapsayıcı dağıtma</span><span class="sxs-lookup"><span data-stu-id="25e70-128">Deploy a Windows container to Service Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="25e70-129">Service Fabric Linux'ta Docker kapsayıcısı dağıtma</span><span class="sxs-lookup"><span data-stu-id="25e70-129">Deploy a Docker container to Service Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
