---
title: "aaaConnect güvenli bir şekilde tooan Azure Service Fabric kümesi | Microsoft Docs"
description: "Tooauthenticate istemci erişimi nasıl tooa Service Fabric kümesi ve nasıl açıklar istemcilerle bir küme arasındaki toosecure iletişim."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 759a539e-e5e6-4055-bff5-d38804656e10
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 1b6a87a1fefaddce2043c604ca53751157232170
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="1f911-103">Tooa güvenli kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="1f911-103">Connect tooa secure cluster</span></span>

<span data-ttu-id="1f911-104">İstemci tooa Service Fabric küme düğümü bağlandığında hello istemci kimliği doğrulanmış ve güvenli iletişim sertifika güvenliği veya Azure Active Directory (AAD) kullanılarak oluşturulmuş olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f911-104">When a client connects tooa Service Fabric cluster node, hello client can be authenticated and secure communication established using certificate security or Azure Active Directory (AAD).</span></span> <span data-ttu-id="1f911-105">Bu kimlik doğrulaması yalnızca yetkili kullanıcılar hello küme erişebilir ve uygulamaları dağıtılan ve yönetim görevlerini gerçekleştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="1f911-105">This authentication ensures that only authorized users can access hello cluster and deployed applications and perform management tasks.</span></span>  <span data-ttu-id="1f911-106">Merhaba küme oluşturulduğunda sertifika veya AAD güvenlik önceden hello kümede etkinleştirilmiş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1f911-106">Certificate or AAD security must have been previously enabled on hello cluster when hello cluster was created.</span></span>  <span data-ttu-id="1f911-107">Küme güvenlik senaryoları hakkında daha fazla bilgi için bkz: [küme güvenlik](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="1f911-107">For more information on cluster security scenarios, see [Cluster security](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="1f911-108">Sertifikalar ile güvenlik altına tooa küme bağlanıyorsanız [hello istemci sertifika ayarlama](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) hello bilgisayarda toohello küme bağlanır.</span><span class="sxs-lookup"><span data-stu-id="1f911-108">If you are connecting tooa cluster secured with certificates, [set up hello client certificate](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) on hello computer that connects toohello cluster.</span></span> 

<a id="connectsecureclustercli"></a> 

## <a name="connect-tooa-secure-cluster-using-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="1f911-109">Azure Service Fabric CLI (sfctl) kullanarak tooa güvenli kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="1f911-109">Connect tooa secure cluster using Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="1f911-110">Merhaba Service Fabric CLI (sfctl) kullanan birkaç farklı şekilde tooconnect tooa güvenli kümesi vardır.</span><span class="sxs-lookup"><span data-stu-id="1f911-110">There are a few different ways tooconnect tooa secure cluster using hello Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="1f911-111">Bir istemci sertifikası kimlik doğrulamasını kullanırken, bir sertifika ayrıntıları eşleşmelidir hello sertifika toohello küme düğümleri dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="1f911-111">When using a client certificate for authentication, hello certificate details must match a certificate deployed toohello cluster nodes.</span></span> <span data-ttu-id="1f911-112">Sertifikanızı sertifika yetkilileri (CA) varsa, tooadditionally gerekir hello güvenilen CA'ları belirtin.</span><span class="sxs-lookup"><span data-stu-id="1f911-112">If your certificate has Certificate Authorities (CAs), you need tooadditionally specify hello trusted CAs.</span></span>

<span data-ttu-id="1f911-113">Hello kullanarak tooa küme bağlanabilir `sfctl cluster select` komutu.</span><span class="sxs-lookup"><span data-stu-id="1f911-113">You can connect tooa cluster using hello `sfctl cluster select` command.</span></span>

<span data-ttu-id="1f911-114">İstemci sertifikaları, bir sertifika ve anahtar çifti olarak ya da tek pem dosyası olarak iki farklı fashions belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="1f911-114">Client certificates can be specified in two different fashions, either as a cert and key pair, or as a single pem file.</span></span> <span data-ttu-id="1f911-115">Parola korumalı için `pem` dosyaları olacaktır otomatik olarak tooenter hello parola istenir.</span><span class="sxs-lookup"><span data-stu-id="1f911-115">For password protected `pem` files, you will be prompted automatically tooenter hello password.</span></span>

<span data-ttu-id="1f911-116">pem dosyası olarak toospecify hello istemci sertifikası hello hello dosya yolu belirtin `--pem` bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="1f911-116">toospecify hello client certificate as a pem file, specify hello file path in hello `--pem` argument.</span></span> <span data-ttu-id="1f911-117">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="1f911-117">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="1f911-118">Parola korumalı pem dosyaları için parola önceki toorunning herhangi bir komut isteminde bulunur.</span><span class="sxs-lookup"><span data-stu-id="1f911-118">Password protected pem files will prompt for password prior toorunning any command.</span></span>

<span data-ttu-id="1f911-119">bir sertifika toospecify, anahtar çiftini kullanın hello `--cert` ve `--key` toospecify hello dosya yolları tooeach ilgili dosyasından bağımsız değişkenler.</span><span class="sxs-lookup"><span data-stu-id="1f911-119">toospecify a cert, key pair use hello `--cert` and `--key` arguments toospecify hello file paths tooeach respective file.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

<span data-ttu-id="1f911-120">Bazen kullanılan sertifikaları toosecure test veya geliştirme kümeleri sertifika doğrulaması başarısız.</span><span class="sxs-lookup"><span data-stu-id="1f911-120">Sometimes certificates used toosecure test or dev clusters fail certificate validation.</span></span> <span data-ttu-id="1f911-121">toobypass sertifika doğrulama hello belirtin `--no-verify` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="1f911-121">toobypass certificate verification, specify hello `--no-verify` option.</span></span> <span data-ttu-id="1f911-122">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="1f911-122">For example:</span></span>

> [!WARNING]
> <span data-ttu-id="1f911-123">Merhaba kullanmayın `no-verify` tooproduction Service Fabric kümeleri bağlanırken seçeneği.</span><span class="sxs-lookup"><span data-stu-id="1f911-123">Do not use hello `no-verify` option when connecting tooproduction Service Fabric clusters.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

<span data-ttu-id="1f911-124">Ayrıca, güvenilir CA sertifikaları ya da tek tek sertifikaları yolları toodirectories belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f911-124">In addition, you can specify paths toodirectories of trusted CA certs, or individual certs.</span></span> <span data-ttu-id="1f911-125">toospecify bu yollar kullanın hello `--ca` bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="1f911-125">toospecify these paths, use hello `--ca` argument.</span></span> <span data-ttu-id="1f911-126">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="1f911-126">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

<span data-ttu-id="1f911-127">Bağlandıktan sonra çok gerekir[diğer sfctl komutlarının çalıştırılmasını](service-fabric-cli.md) toointeract hello kümesi ile.</span><span class="sxs-lookup"><span data-stu-id="1f911-127">After you connect, you should be able too[run other sfctl commands](service-fabric-cli.md) toointeract with hello cluster.</span></span>

<a id="connectsecurecluster"></a>

## <a name="connect-tooa-cluster-using-powershell"></a><span data-ttu-id="1f911-128">PowerShell kullanarak tooa kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="1f911-128">Connect tooa cluster using PowerShell</span></span>
<span data-ttu-id="1f911-129">PowerShell aracılığıyla bir kümede işlemleri gerçekleştirmeden önce ilk bağlantı toohello küme oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1f911-129">Before you perform operations on a cluster through PowerShell, first establish a connection toohello cluster.</span></span> <span data-ttu-id="1f911-130">Merhaba küme bağlantısı PowerShell oturumu verilen hello izleyen tüm komutlar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1f911-130">hello cluster connection is used for all subsequent commands in hello given PowerShell session.</span></span>

### <a name="connect-tooan-unsecure-cluster"></a><span data-ttu-id="1f911-131">Tooan güvensiz kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="1f911-131">Connect tooan unsecure cluster</span></span>

<span data-ttu-id="1f911-132">güvenli olmayan tooconnect tooan küme, hello küme uç noktası adresi toohello sağlayın **Connect-ServiceFabricCluster** komutu:</span><span class="sxs-lookup"><span data-stu-id="1f911-132">tooconnect tooan unsecure cluster, provide hello cluster endpoint address toohello **Connect-ServiceFabricCluster** command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="1f911-133">Azure Active Directory'yi kullanarak tooa güvenli kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="1f911-133">Connect tooa secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="1f911-134">Azure Active Directory tooauthorize küme yönetici erişimi kullanan tooconnect tooa güvenli küme hello küme sertifika parmak izi sağlayın ve hello kullan *AzureActiveDirectory* bayrağı.</span><span class="sxs-lookup"><span data-stu-id="1f911-134">tooconnect tooa secure cluster that uses Azure Active Directory tooauthorize cluster administrator access, provide hello cluster certificate thumbprint and use hello *AzureActiveDirectory* flag.</span></span>  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="1f911-135">Bir istemci sertifikası kullanarak tooa güvenli kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="1f911-135">Connect tooa secure cluster using a client certificate</span></span>
<span data-ttu-id="1f911-136">İstemci sertifikaları tooauthorize yönetici erişimi tooconnect tooa güvenli küme PowerShell komutunu aşağıdaki çalışma hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="1f911-136">Run hello following PowerShell command tooconnect tooa secure cluster that uses client certificates tooauthorize administrator access.</span></span> <span data-ttu-id="1f911-137">Merhaba küme sertifika parmak izi ve küme yönetimi için izinler verildiyse hello istemci sertifikasının hello parmak izi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="1f911-137">Provide hello cluster certificate thumbprint and hello thumbprint of hello client certificate that has been granted permissions for cluster management.</span></span> <span data-ttu-id="1f911-138">Merhaba sertifika ayrıntıları hello küme düğümlerinde bir sertifika ile eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f911-138">hello certificate details must match a certificate on hello cluster nodes.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="1f911-139">*ServerCertThumbprint* hello parmak izi hello küme düğümlerinde yüklü hello sunucu sertifikası.</span><span class="sxs-lookup"><span data-stu-id="1f911-139">*ServerCertThumbprint* is hello thumbprint of hello server certificate installed on hello cluster nodes.</span></span> <span data-ttu-id="1f911-140">*FindValue* hello parmak izi hello yönetici istemci sertifikası.</span><span class="sxs-lookup"><span data-stu-id="1f911-140">*FindValue* is hello thumbprint of hello admin client certificate.</span></span>
<span data-ttu-id="1f911-141">Merhaba parametreleri doldurulduğunda, hello komutu aşağıdaki örneğine hello gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="1f911-141">When hello parameters are filled in, hello command looks like hello following example:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-tooa-secure-cluster-using-windows-active-directory"></a><span data-ttu-id="1f911-142">Windows Active Directory kullanarak tooa güvenli kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="1f911-142">Connect tooa secure cluster using Windows Active Directory</span></span>
<span data-ttu-id="1f911-143">Tek başına kümenizi AD güvenlik kullanarak dağıtılmışsa, başlangıç anahtarı "WindowsCredential" ekleyerek toohello kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="1f911-143">If your standalone cluster is deployed using AD security, connect toohello cluster by appending hello switch "WindowsCredential".</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-tooa-cluster-using-hello-fabricclient-apis"></a><span data-ttu-id="1f911-144">Merhaba FabricClient API'lerini kullanarak tooa kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="1f911-144">Connect tooa cluster using hello FabricClient APIs</span></span>
<span data-ttu-id="1f911-145">Merhaba Service Fabric SDK sağlar hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) küme yönetimi için sınıf.</span><span class="sxs-lookup"><span data-stu-id="1f911-145">hello Service Fabric SDK provides hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) class for cluster management.</span></span> <span data-ttu-id="1f911-146">toouse hello FabricClient API'leri hello Microsoft.ServiceFabric NuGet paketi alın.</span><span class="sxs-lookup"><span data-stu-id="1f911-146">toouse hello FabricClient APIs, get hello Microsoft.ServiceFabric NuGet package.</span></span>

### <a name="connect-tooan-unsecure-cluster"></a><span data-ttu-id="1f911-147">Tooan güvensiz kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="1f911-147">Connect tooan unsecure cluster</span></span>

<span data-ttu-id="1f911-148">tooconnect tooa uzaktan güvenli olmayan küme, FabricClient örneği oluşturun ve hello küme adresini sağlayın:</span><span class="sxs-lookup"><span data-stu-id="1f911-148">tooconnect tooa remote unsecured cluster, create a FabricClient instance and provide hello cluster address:</span></span>

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

<span data-ttu-id="1f911-149">Bir küme içinde çalışan için kodu, örneğin, güvenilir bir hizmetinde bir FabricClient oluşturmak *olmadan* hello küme adresi belirtme.</span><span class="sxs-lookup"><span data-stu-id="1f911-149">For code that is running from within a cluster, for example, in a Reliable Service, create a FabricClient *without* specifying hello cluster address.</span></span> <span data-ttu-id="1f911-150">FabricClient bağlayan toohello yerel yönetim hello düğüm hello kodu üzerinde ağ geçidi şu anda çalışıyorsa, ek ağ atlama önleme.</span><span class="sxs-lookup"><span data-stu-id="1f911-150">FabricClient connects toohello local management gateway on hello node hello code is currently running on, avoiding an extra network hop.</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="1f911-151">Bir istemci sertifikası kullanarak tooa güvenli kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="1f911-151">Connect tooa secure cluster using a client certificate</span></span>

<span data-ttu-id="1f911-152">Merhaba kümedeki Hello düğümler geçerli sertifikaların ortak adı olması gerekir veya DNS adının SAN'hello [RemoteCommonNames özelliği](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) ayarlamak [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="1f911-152">hello nodes in hello cluster must have valid certificates whose common name or DNS name in SAN appears in hello [RemoteCommonNames property](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) set on [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span></span> <span data-ttu-id="1f911-153">Bu işlem aşağıdaki hello istemci hello küme düğümleri arasında karşılıklı kimlik doğrulamasını etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="1f911-153">Following this process enables mutual authentication between hello client and hello cluster nodes.</span></span>

```csharp
using System.Fabric;
using System.Security.Cryptography.X509Certificates;

string clientCertThumb = "71DE04467C9ED0544D021098BCD44C71E183414E";
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string CommonName = "www.clustername.westus.azure.com";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var xc = GetCredentials(clientCertThumb, serverCertThumb, CommonName);
var fc = new FabricClient(xc, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

static X509Credentials GetCredentials(string clientCertThumb, string serverCertThumb, string name)
{
    X509Credentials xc = new X509Credentials();
    xc.StoreLocation = StoreLocation.CurrentUser;
    xc.StoreName = "My";
    xc.FindType = X509FindType.FindByThumbprint;
    xc.FindValue = clientCertThumb;
    xc.RemoteCommonNames.Add(name);
    xc.RemoteCertThumbprints.Add(serverCertThumb);
    xc.ProtectionLevel = ProtectionLevel.EncryptAndSign;
    return xc;
}
```

### <a name="connect-tooa-secure-cluster-interactively-using-azure-active-directory"></a><span data-ttu-id="1f911-154">Etkileşimli olarak Azure Active Directory'yi kullanarak tooa güvenli kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="1f911-154">Connect tooa secure cluster interactively using Azure Active Directory</span></span>

<span data-ttu-id="1f911-155">Örnek kullanan Azure Active Directory istemci kimliği ve sunucu sertifikası sunucu kimliği için aşağıdaki hello.</span><span class="sxs-lookup"><span data-stu-id="1f911-155">hello following example uses Azure Active Directory for client identity and server certificate for server identity.</span></span>

<span data-ttu-id="1f911-156">Bir iletişim kutusu penceresinin otomatik olarak etkileşimli oturum açma için toohello küme bağlandıktan sonra açılır.</span><span class="sxs-lookup"><span data-stu-id="1f911-156">A dialog window automatically pops up for interactive sign-in upon connecting toohello cluster.</span></span>

```csharp
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);

var fc = new FabricClient(claimsCredentials, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}
```

### <a name="connect-tooa-secure-cluster-non-interactively-using-azure-active-directory"></a><span data-ttu-id="1f911-157">Tooa güvenli küme etkileşimsiz Azure Active Directory'yi kullanarak bağlan</span><span class="sxs-lookup"><span data-stu-id="1f911-157">Connect tooa secure cluster non-interactively using Azure Active Directory</span></span>

<span data-ttu-id="1f911-158">Merhaba aşağıdaki örnek dayanır Microsoft.IdentityModel.Clients.activedirectory tarafından üzerinde sürüm: 2.19.208020213.</span><span class="sxs-lookup"><span data-stu-id="1f911-158">hello following example relies on Microsoft.IdentityModel.Clients.ActiveDirectory, Version: 2.19.208020213.</span></span>

<span data-ttu-id="1f911-159">AAD belirteci edinme hakkında daha fazla bilgi için bkz: [Microsoft.IdentityModel.Clients.activedirectory tarafından](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span><span class="sxs-lookup"><span data-stu-id="1f911-159">For more information on AAD token acquisition, see [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span></span>

```csharp
string tenantId = "C15CFCEA-02C1-40DC-8466-FBD0EE0B05D2";
string clientApplicationId = "118473C2-7619-46E3-A8E4-6DA8D5F56E12";
string webApplicationId = "53E6948C-0897-4DA6-B26A-EE2A38A690B4";

string token = GetAccessToken(
    tenantId,
    webApplicationId,
    clientApplicationId,
    "urn:ietf:wg:oauth:2.0:oob");

string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);
claimsCredentials.LocalClaims = token;

var fc = new FabricClient(claimsCredentials, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

...

static string GetAccessToken(
    string tenantId,
    string resource,
    string clientId,
    string redirectUri)
{
    string authorityFormat = @"https://login.microsoftonline.com/{0}";
    string authority = string.Format(CultureInfo.InvariantCulture, authorityFormat, tenantId);
    var authContext = new AuthenticationContext(authority);

    var authResult = authContext.AcquireToken(
        resource,
        clientId,
        new UserCredential("TestAdmin@clustenametenant.onmicrosoft.com", "TestPassword"));
    return authResult.AccessToken;
}

```

### <a name="connect-tooa-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a><span data-ttu-id="1f911-160">Azure Active Directory'yi kullanarak önceki meta veri bilgisi olmadan tooa güvenli kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="1f911-160">Connect tooa secure cluster without prior metadata knowledge using Azure Active Directory</span></span>

<span data-ttu-id="1f911-161">Hello aşağıdaki örnek etkileşimli olmayan belirteç edinme, kullanır, ancak hello aynı yaklaşımı kullanılan toobuild özel etkileşimli belirteç edinme deneyimi olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f911-161">hello following example uses non-interactive token acquisition, but hello same approach can be used toobuild a custom interactive token acquisition experience.</span></span> <span data-ttu-id="1f911-162">belirteç alımı için gereken hello Azure Active Directory meta veri kümesi yapılandırmasından okuyun.</span><span class="sxs-lookup"><span data-stu-id="1f911-162">hello Azure Active Directory metadata needed for token acquisition is read from cluster configuration.</span></span>

```csharp
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);

var fc = new FabricClient(claimsCredentials, connection);

fc.ClaimsRetrieval += (o, e) =>
{
    return GetAccessToken(e.AzureActiveDirectoryMetadata);
};

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

...

static string GetAccessToken(AzureActiveDirectoryMetadata aad)
{
    var authContext = new AuthenticationContext(aad.Authority);

    var authResult = authContext.AcquireToken(
        aad.ClusterApplication,
        aad.ClientApplication,
        new UserCredential("TestAdmin@clustenametenant.onmicrosoft.com", "TestPassword"));
    return authResult.AccessToken;
}

```

<a id="connectsecureclustersfx"></a>

## <a name="connect-tooa-secure-cluster-using-service-fabric-explorer"></a><span data-ttu-id="1f911-163">Service Fabric Explorer kullanarak tooa güvenli kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="1f911-163">Connect tooa secure cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="1f911-164">tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) verilmiş bir küme için tarayıcınızı noktası:</span><span class="sxs-lookup"><span data-stu-id="1f911-164">tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) for a given cluster, point your browser to:</span></span>

`http://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="1f911-165">Merhaba tam URL hello küme essentials bölmesinde hello Azure portalında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1f911-165">hello full URL is also available in hello cluster essentials pane of hello Azure portal.</span></span>

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="1f911-166">Azure Active Directory'yi kullanarak tooa güvenli kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="1f911-166">Connect tooa secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="1f911-167">AAD ile güvenli tooconnect tooa küme tarayıcınıza noktası:</span><span class="sxs-lookup"><span data-stu-id="1f911-167">tooconnect tooa cluster that is secured with AAD, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="1f911-168">Otomatik olarak olması AAD oturum istendiğinde toolog.</span><span class="sxs-lookup"><span data-stu-id="1f911-168">You are automatically be prompted toolog in with AAD.</span></span>

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="1f911-169">Bir istemci sertifikası kullanarak tooa güvenli kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="1f911-169">Connect tooa secure cluster using a client certificate</span></span>

<span data-ttu-id="1f911-170">Sertifikalar ile güvenli tooconnect tooa küme tarayıcınıza noktası:</span><span class="sxs-lookup"><span data-stu-id="1f911-170">tooconnect tooa cluster that is secured with certificates, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="1f911-171">Otomatik olarak olması istendiğinde tooselect bir istemci sertifikası.</span><span class="sxs-lookup"><span data-stu-id="1f911-171">You are automatically be prompted tooselect a client certificate.</span></span>

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-hello-remote-computer"></a><span data-ttu-id="1f911-172">Bir istemci sertifikası hello uzak bilgisayarda ayarlama</span><span class="sxs-lookup"><span data-stu-id="1f911-172">Set up a client certificate on hello remote computer</span></span>
<span data-ttu-id="1f911-173">En az iki sertifika hello küme, hello küme ve sunucu sertifikası için bir ve istemci erişimi için başka bir güvenliğini sağlamak için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1f911-173">At least two certificates should be used for securing hello cluster, one for hello cluster and server certificate and another for client access.</span></span>  <span data-ttu-id="1f911-174">Ayrıca ek ikincil sertifikalar ve istemci erişim sertifikalarını kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="1f911-174">We recommend that you also use additional secondary certificates and client access certificates.</span></span>  <span data-ttu-id="1f911-175">bir istemci arasında kullanarak bir küme düğümü toosecure hello iletişimi sertifika güvenlik, ilk tooobtain gerekir ve hello istemci sertifikası yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1f911-175">toosecure hello communication between a client and a cluster node using certificate security, you first need tooobtain and install hello client certificate.</span></span> <span data-ttu-id="1f911-176">Merhaba sertifika hello kişisel (My) deposuna hello yerel bilgisayar veya hello geçerli kullanıcı yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="1f911-176">hello certificate can be installed into hello Personal (My) store of hello local computer or hello current user.</span></span>  <span data-ttu-id="1f911-177">Merhaba istemci hello küme doğrulanabilmesi hello sertifikanın parmak izini hello sunucu da gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f911-177">You also need hello thumbprint of hello server certificate so that hello client can authenticate hello cluster.</span></span>

<span data-ttu-id="1f911-178">PowerShell cmdlet tooset hello istemci sertifika hello kümeye erişmek hello bilgisayarda aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1f911-178">Run hello following PowerShell cmdlet tooset up hello client certificate on hello computer from which you access hello cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

<span data-ttu-id="1f911-179">Kendinden imzalı bir sertifika varsa, bu sertifika tooconnect tooa güvenli küme kullanmadan önce onu tooyour makinenin "güvenilir kişiler" saklayın tooimport gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f911-179">If it is a self-signed certificate, you need tooimport it tooyour machine's "trusted people" store before you can use this certificate tooconnect tooa secure cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a><span data-ttu-id="1f911-180">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1f911-180">Next steps</span></span>

* [<span data-ttu-id="1f911-181">Service Fabric kümesi yükseltme işlemi ve sizden beklentileri</span><span class="sxs-lookup"><span data-stu-id="1f911-181">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="1f911-182">Visual Studio'da, Service Fabric uygulamaları yönetme</span><span class="sxs-lookup"><span data-stu-id="1f911-182">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="1f911-183">Service Fabric sistem durumu modeli giriş</span><span class="sxs-lookup"><span data-stu-id="1f911-183">Service Fabric Health model introduction</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="1f911-184">Uygulama güvenliği ve farklı çalıştır</span><span class="sxs-lookup"><span data-stu-id="1f911-184">Application Security and RunAs</span></span>](service-fabric-application-runas-security.md)
* [<span data-ttu-id="1f911-185">Service Fabric CLI ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="1f911-185">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
