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
# <a name="container-security"></a><span data-ttu-id="f0510-103">Kapsayıcı güvenlik</span><span class="sxs-lookup"><span data-stu-id="f0510-103">Container security</span></span>

<span data-ttu-id="f0510-104">Service Fabric hello kümedeki düğümlere bir Windows veya Linux (sürüm 5.7 veya üstü) yüklü bir Sertifika Hizmetleri bir kapsayıcı tooaccess içinde bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0510-104">Service Fabric provides a mechanism for services inside a container tooaccess a certificate that is installed on hello nodes in a Windows or Linux cluster (version 5.7 or higher).</span></span> <span data-ttu-id="f0510-105">Ayrıca, Service Fabric Windows kapsayıcıları için de gMSA (Grup yönetilen hizmet hesapları) destekler.</span><span class="sxs-lookup"><span data-stu-id="f0510-105">In addition, Service Fabric also supports gMSA (group Managed Service Accounts) for Windows containers.</span></span> 

## <a name="certificate-management-for-containers"></a><span data-ttu-id="f0510-106">Kapsayıcıları için sertifika yönetimi</span><span class="sxs-lookup"><span data-stu-id="f0510-106">Certificate management for containers</span></span>

<span data-ttu-id="f0510-107">Bir sertifika belirterek, kapsayıcı hizmetlerini güvenliğini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0510-107">You can secure your container services by specifying a certificate.</span></span> <span data-ttu-id="f0510-108">Merhaba sertifika hello hello küme düğümlerinde yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f0510-108">hello certificate must be installed on hello nodes of hello cluster.</span></span> <span data-ttu-id="f0510-109">Merhaba sertifika bilgilerini hello altında hello uygulama bildiriminde sağlanan `ContainerHostPolicies` etiketi aşağıdaki kod parçacığında gösterildiği hello olarak:</span><span class="sxs-lookup"><span data-stu-id="f0510-109">hello certificate information is provided in hello application manifest under hello `ContainerHostPolicies` tag as hello following snippet shows:</span></span>

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

<span data-ttu-id="f0510-110">Merhaba uygulama başlatılırken hello çalışma zamanı hello sertifikaları okur ve bir PFX dosyası ve her sertifika için parola oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f0510-110">When starting hello application, hello runtime reads hello certificates and generates a PFX file and password for each certificate.</span></span> <span data-ttu-id="f0510-111">Bu PFX dosyası ve parola, ortam değişkenleri aşağıdaki hello kullanarak hello kapsayıcısı içindeki erişilebilir:</span><span class="sxs-lookup"><span data-stu-id="f0510-111">This PFX file and password are accessible inside hello container using hello following environment variables:</span></span> 

* <span data-ttu-id="f0510-112">**Certificate_ [CodePackageName] _ [CertName] _PFX**</span><span class="sxs-lookup"><span data-stu-id="f0510-112">**Certificate_[CodePackageName]_[CertName]_PFX**</span></span>
* <span data-ttu-id="f0510-113">**Certificate_ [CodePackageName] _ [CertName] _Password**</span><span class="sxs-lookup"><span data-stu-id="f0510-113">**Certificate_[CodePackageName]_[CertName]_Password**</span></span>

<span data-ttu-id="f0510-114">Merhaba kapsayıcı hizmeti ya da işlem hello kapsayıcıya hello PFX dosyasını içeri aktarmak için sorumludur.</span><span class="sxs-lookup"><span data-stu-id="f0510-114">hello container service or process is responsible for importing hello PFX file into hello container.</span></span> <span data-ttu-id="f0510-115">kullanabileceğiniz tooimport hello sertifika `setupentrypoint.sh` komut dosyaları veya özel kod hello kapsayıcı işlemi içinde yürütülür.</span><span class="sxs-lookup"><span data-stu-id="f0510-115">tooimport hello certificate, you can use `setupentrypoint.sh` scripts or executed custom code within hello container process.</span></span> <span data-ttu-id="f0510-116">C# örnek kod hello PFX dosyasını içeri aktarmak için aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="f0510-116">Sample code in C# for importing hello PFX file follows:</span></span>

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
<span data-ttu-id="f0510-117">Bu PFX sertifika kimlik doğrulaması yap hello uygulama veya hizmet ya da diğer hizmetleri ile güvenli commmunication için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f0510-117">This PFX certificate can be used for authenticate hello application or service or secure commmunication with other services.</span></span>


## <a name="set-up-gmsa-for-windows-containers"></a><span data-ttu-id="f0510-118">GMSA Windows kapsayıcıları için ayarlama</span><span class="sxs-lookup"><span data-stu-id="f0510-118">Set up gMSA for Windows containers</span></span>

<span data-ttu-id="f0510-119">gMSA (Grup yönetilen hizmet hesapları), bir kimlik bilgisi belirtimi dosyası yukarı tooset (`credspec`) hello kümedeki tüm düğümlere yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="f0510-119">tooset up gMSA (group Managed Service Accounts), a credential specification file (`credspec`) is placed on all nodes in hello cluster.</span></span> <span data-ttu-id="f0510-120">bir VM uzantısı kullanılarak tüm düğümlerde Hello dosya kopyalanabilir.</span><span class="sxs-lookup"><span data-stu-id="f0510-120">hello file can be copied on all nodes using a VM extension.</span></span>  <span data-ttu-id="f0510-121">Merhaba `credspec` dosya hello gMSA hesabı bilgileri içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0510-121">hello `credspec` file must contain hello gMSA account information.</span></span> <span data-ttu-id="f0510-122">Merhaba hakkında daha fazla bilgi için `credspec` dosya için bkz: [hizmet hesaplarını](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span><span class="sxs-lookup"><span data-stu-id="f0510-122">For more information on hello `credspec` file, see [Service Accounts](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span></span> <span data-ttu-id="f0510-123">Merhaba kimlik bilgisi belirtimi ve hello `Hostname` etiketi hello uygulama bildiriminde belirtilir.</span><span class="sxs-lookup"><span data-stu-id="f0510-123">hello credential specification and hello `Hostname` tag are specified in hello application manifest.</span></span> <span data-ttu-id="f0510-124">Merhaba `Hostname` etiketi altında kapsayıcı çalıştığı hello hello gMSA hesabı adı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="f0510-124">hello `Hostname` tag must match hello gMSA account name that hello container runs under.</span></span>  <span data-ttu-id="f0510-125">Merhaba `Hostname` etiketi hello kapsayıcı tooauthenticate kendisini Kerberos kimlik doğrulaması kullanarak hello etki alanındaki tooother hizmetleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0510-125">hello `Hostname` tag allows hello container tooauthenticate itself tooother services in hello domain using Kerberos authentication.</span></span>  <span data-ttu-id="f0510-126">Merhaba belirtmek için bir örnek `Hostname` ve hello `credspec` hello uygulama bildirimi parçacığını aşağıdaki hello gösterilir:</span><span class="sxs-lookup"><span data-stu-id="f0510-126">A sample for specifying hello `Hostname` and hello `credspec` in hello application manifest is shown in hello following snippet:</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="f0510-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f0510-127">Next steps</span></span>

* [<span data-ttu-id="f0510-128">Bir Windows kapsayıcı tooService Windows Server 2016 doku dağıtma</span><span class="sxs-lookup"><span data-stu-id="f0510-128">Deploy a Windows container tooService Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="f0510-129">Docker kapsayıcısı tooService doku Linux'ta dağıtma</span><span class="sxs-lookup"><span data-stu-id="f0510-129">Deploy a Docker container tooService Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
