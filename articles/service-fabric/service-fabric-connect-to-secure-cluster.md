---
title: "Güvenli bir şekilde bir Azure Service Fabric kümesine bağlanma | Microsoft Docs"
description: "Service Fabric kümesi istemci erişimi kimlik doğrulaması ve istemcileri ile bir küme arasındaki iletişimin güvenliğini açıklar."
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
ms.openlocfilehash: d6a13ceb8ccd9207ecacc166247535d496d5dec7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-to-a-secure-cluster"></a><span data-ttu-id="c1294-103">Güvenli bir kümeye bağlanma</span><span class="sxs-lookup"><span data-stu-id="c1294-103">Connect to a secure cluster</span></span>

<span data-ttu-id="c1294-104">Bir istemci bir Service Fabric küme düğümüne bağlandığında, istemci kimliği doğrulanmış ve güvenli iletişim sertifika güvenliği veya Azure Active Directory (AAD) kullanılarak oluşturulmuş olabilir.</span><span class="sxs-lookup"><span data-stu-id="c1294-104">When a client connects to a Service Fabric cluster node, the client can be authenticated and secure communication established using certificate security or Azure Active Directory (AAD).</span></span> <span data-ttu-id="c1294-105">Bu kimlik doğrulaması yalnızca yetkili kullanıcılar küme erişebilir ve uygulamaları dağıtılan ve yönetim görevlerini gerçekleştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="c1294-105">This authentication ensures that only authorized users can access the cluster and deployed applications and perform management tasks.</span></span>  <span data-ttu-id="c1294-106">Küme oluştururken sertifika veya AAD güvenlik daha önce kümede etkinleştirilmiş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c1294-106">Certificate or AAD security must have been previously enabled on the cluster when the cluster was created.</span></span>  <span data-ttu-id="c1294-107">Küme güvenlik senaryoları hakkında daha fazla bilgi için bkz: [küme güvenlik](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="c1294-107">For more information on cluster security scenarios, see [Cluster security](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="c1294-108">Sertifikalar ile güvenli bir kümeye bağlanıyorsanız [istemci sertifika ayarlama](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) bilgisayarda kümeye bağlanır.</span><span class="sxs-lookup"><span data-stu-id="c1294-108">If you are connecting to a cluster secured with certificates, [set up the client certificate](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) on the computer that connects to the cluster.</span></span> 

<a id="connectsecureclustercli"></a> 

## <a name="connect-to-a-secure-cluster-using-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="c1294-109">Azure Service Fabric CLI (sfctl) kullanarak güvenli bir kümeye bağlanın</span><span class="sxs-lookup"><span data-stu-id="c1294-109">Connect to a secure cluster using Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="c1294-110">Service Fabric CLI (sfctl) kullanarak güvenli bir kümeye bağlanmak için birkaç farklı yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="c1294-110">There are a few different ways to connect to a secure cluster using the Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="c1294-111">Kimlik doğrulaması için bir istemci sertifikası kullanıyorsanız sertifika bilgilerinin küme düğümlerine dağıtılmış olan bir sertifikayla eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c1294-111">When using a client certificate for authentication, the certificate details must match a certificate deployed to the cluster nodes.</span></span> <span data-ttu-id="c1294-112">Sertifikanızı sertifika yetkilileri (CA) varsa, güvenilen CA'lar ayrıca belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c1294-112">If your certificate has Certificate Authorities (CAs), you need to additionally specify the trusted CAs.</span></span>

<span data-ttu-id="c1294-113">Kullanarak bir küme bağlanabilir `sfctl cluster select` komutu.</span><span class="sxs-lookup"><span data-stu-id="c1294-113">You can connect to a cluster using the `sfctl cluster select` command.</span></span>

<span data-ttu-id="c1294-114">İstemci sertifikaları, bir sertifika ve anahtar çifti olarak ya da tek pem dosyası olarak iki farklı fashions belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="c1294-114">Client certificates can be specified in two different fashions, either as a cert and key pair, or as a single pem file.</span></span> <span data-ttu-id="c1294-115">Parola korumalı için `pem` istenir otomatik olarak parola girmesini dosyaları,.</span><span class="sxs-lookup"><span data-stu-id="c1294-115">For password protected `pem` files, you will be prompted automatically to enter the password.</span></span>

<span data-ttu-id="c1294-116">Pem dosyası olarak istemci sertifikasını belirtmek için dosya yolu belirtin `--pem` bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="c1294-116">To specify the client certificate as a pem file, specify the file path in the `--pem` argument.</span></span> <span data-ttu-id="c1294-117">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c1294-117">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="c1294-118">Pem dosyaları herhangi bir komut çalıştırılmadan önce parola istemeyeceğini parola korumalı.</span><span class="sxs-lookup"><span data-stu-id="c1294-118">Password protected pem files will prompt for password prior to running any command.</span></span>

<span data-ttu-id="c1294-119">Bir sertifika belirtmek için anahtar çifti kullanımı `--cert` ve `--key` ilgili her dosya için dosya yolları belirtmek için bağımsız değişkenler.</span><span class="sxs-lookup"><span data-stu-id="c1294-119">To specify a cert, key pair use the `--cert` and `--key` arguments to specify the file paths to each respective file.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

<span data-ttu-id="c1294-120">Bazen test veya geliştirme kümesi güvenliğini sağlamak için kullanılan sertifikalar sertifika doğrulaması başarısız.</span><span class="sxs-lookup"><span data-stu-id="c1294-120">Sometimes certificates used to secure test or dev clusters fail certificate validation.</span></span> <span data-ttu-id="c1294-121">Sertifika doğrulama atlamak üzere belirtin `--no-verify` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="c1294-121">To bypass certificate verification, specify the `--no-verify` option.</span></span> <span data-ttu-id="c1294-122">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c1294-122">For example:</span></span>

> [!WARNING]
> <span data-ttu-id="c1294-123">Kullanmayın `no-verify` Service Fabric kümeleri üretim bağlanırken seçeneği.</span><span class="sxs-lookup"><span data-stu-id="c1294-123">Do not use the `no-verify` option when connecting to production Service Fabric clusters.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

<span data-ttu-id="c1294-124">Ayrıca, güvenilir CA sertifikaları ya da tek tek sertifikaları dizinler için yol belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c1294-124">In addition, you can specify paths to directories of trusted CA certs, or individual certs.</span></span> <span data-ttu-id="c1294-125">Bu yolları belirtmek için kullanın `--ca` bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="c1294-125">To specify these paths, use the `--ca` argument.</span></span> <span data-ttu-id="c1294-126">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c1294-126">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

<span data-ttu-id="c1294-127">Bağlandıktan sonra şunları yapabilirsiniz [diğer sfctl komutlarının çalıştırılmasını](service-fabric-cli.md) kümeyle etkileşim kurmak için.</span><span class="sxs-lookup"><span data-stu-id="c1294-127">After you connect, you should be able to [run other sfctl commands](service-fabric-cli.md) to interact with the cluster.</span></span>

<a id="connectsecurecluster"></a>

## <a name="connect-to-a-cluster-using-powershell"></a><span data-ttu-id="c1294-128">PowerShell kullanarak bir kümeye bağlanın</span><span class="sxs-lookup"><span data-stu-id="c1294-128">Connect to a cluster using PowerShell</span></span>
<span data-ttu-id="c1294-129">PowerShell aracılığıyla bir kümede işlemleri gerçekleştirmeden önce ilk küme bağlantı kurun.</span><span class="sxs-lookup"><span data-stu-id="c1294-129">Before you perform operations on a cluster through PowerShell, first establish a connection to the cluster.</span></span> <span data-ttu-id="c1294-130">Küme bağlantısı verilen PowerShell oturumunda izleyen tüm komutlar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c1294-130">The cluster connection is used for all subsequent commands in the given PowerShell session.</span></span>

### <a name="connect-to-an-unsecure-cluster"></a><span data-ttu-id="c1294-131">Güvenli olmayan bir kümeye bağlanın</span><span class="sxs-lookup"><span data-stu-id="c1294-131">Connect to an unsecure cluster</span></span>

<span data-ttu-id="c1294-132">Güvenli olmayan bir kümeye bağlanmak için küme uç nokta adresine sağlamak **Connect-ServiceFabricCluster** komutu:</span><span class="sxs-lookup"><span data-stu-id="c1294-132">To connect to an unsecure cluster, provide the cluster endpoint address to the **Connect-ServiceFabricCluster** command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-to-a-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="c1294-133">Azure Active Directory'yi kullanarak güvenli bir kümeye bağlanın</span><span class="sxs-lookup"><span data-stu-id="c1294-133">Connect to a secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="c1294-134">Küme Yöneticisi erişim yetkisi vermek için Azure Active Directory kullanan güvenli bir kümeye bağlanmak için küme sertifika parmak izini verin ve kullanmak *AzureActiveDirectory* bayrağı.</span><span class="sxs-lookup"><span data-stu-id="c1294-134">To connect to a secure cluster that uses Azure Active Directory to authorize cluster administrator access, provide the cluster certificate thumbprint and use the *AzureActiveDirectory* flag.</span></span>  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="c1294-135">Bir istemci sertifikası ile güvenli bir kümeye bağlanın</span><span class="sxs-lookup"><span data-stu-id="c1294-135">Connect to a secure cluster using a client certificate</span></span>
<span data-ttu-id="c1294-136">Yönetici erişim yetkisi vermek için istemci sertifikalarını kullanan güvenli bir kümeye bağlanmak için aşağıdaki PowerShell komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c1294-136">Run the following PowerShell command to connect to a secure cluster that uses client certificates to authorize administrator access.</span></span> <span data-ttu-id="c1294-137">Küme sertifika parmak izi ve küme yönetimi için izinleri verildi istemci sertifikası parmak izi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="c1294-137">Provide the cluster certificate thumbprint and the thumbprint of the client certificate that has been granted permissions for cluster management.</span></span> <span data-ttu-id="c1294-138">Sertifika ayrıntılarını küme düğümlerinde bir sertifika ile eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c1294-138">The certificate details must match a certificate on the cluster nodes.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="c1294-139">*ServerCertThumbprint* küme düğümlerinde yüklü sunucu sertifikasının parmak izi.</span><span class="sxs-lookup"><span data-stu-id="c1294-139">*ServerCertThumbprint* is the thumbprint of the server certificate installed on the cluster nodes.</span></span> <span data-ttu-id="c1294-140">*FindValue* yönetici istemci sertifikasının parmak izi.</span><span class="sxs-lookup"><span data-stu-id="c1294-140">*FindValue* is the thumbprint of the admin client certificate.</span></span>
<span data-ttu-id="c1294-141">Parametreleri doldurulduğunda, komut aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="c1294-141">When the parameters are filled in, the command looks like the following example:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-to-a-secure-cluster-using-windows-active-directory"></a><span data-ttu-id="c1294-142">Windows Active Directory kullanarak güvenli bir kümeye bağlanın</span><span class="sxs-lookup"><span data-stu-id="c1294-142">Connect to a secure cluster using Windows Active Directory</span></span>
<span data-ttu-id="c1294-143">Tek başına kümenizi AD güvenlik kullanarak dağıtılmışsa, anahtar "WindowsCredential" ekleyerek kümeye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="c1294-143">If your standalone cluster is deployed using AD security, connect to the cluster by appending the switch "WindowsCredential".</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-to-a-cluster-using-the-fabricclient-apis"></a><span data-ttu-id="c1294-144">FabricClient API'lerini kullanarak bir kümeye bağlanın</span><span class="sxs-lookup"><span data-stu-id="c1294-144">Connect to a cluster using the FabricClient APIs</span></span>
<span data-ttu-id="c1294-145">Service Fabric SDK sağlar [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) küme yönetimi için sınıf.</span><span class="sxs-lookup"><span data-stu-id="c1294-145">The Service Fabric SDK provides the [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) class for cluster management.</span></span> <span data-ttu-id="c1294-146">FabricClient API'ları kullanmak için Microsoft.ServiceFabric NuGet paketi alın.</span><span class="sxs-lookup"><span data-stu-id="c1294-146">To use the FabricClient APIs, get the Microsoft.ServiceFabric NuGet package.</span></span>

### <a name="connect-to-an-unsecure-cluster"></a><span data-ttu-id="c1294-147">Güvenli olmayan bir kümeye bağlanın</span><span class="sxs-lookup"><span data-stu-id="c1294-147">Connect to an unsecure cluster</span></span>

<span data-ttu-id="c1294-148">Uzak güvenli olmayan bir kümeye bağlanmak için bir FabricClient örneği oluşturun ve küme adresini sağlayın:</span><span class="sxs-lookup"><span data-stu-id="c1294-148">To connect to a remote unsecured cluster, create a FabricClient instance and provide the cluster address:</span></span>

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

<span data-ttu-id="c1294-149">Bir küme içinde çalışan için kodu, örneğin, güvenilir bir hizmetinde bir FabricClient oluşturmak *olmadan* küme adresini belirtme.</span><span class="sxs-lookup"><span data-stu-id="c1294-149">For code that is running from within a cluster, for example, in a Reliable Service, create a FabricClient *without* specifying the cluster address.</span></span> <span data-ttu-id="c1294-150">Kod, üzerinde çalışmakta olan düğüm üzerinde yerel yönetim ağ geçidi ek ağ atlama önleme FabricClient bağlanır.</span><span class="sxs-lookup"><span data-stu-id="c1294-150">FabricClient connects to the local management gateway on the node the code is currently running on, avoiding an extra network hop.</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="c1294-151">Bir istemci sertifikası ile güvenli bir kümeye bağlanın</span><span class="sxs-lookup"><span data-stu-id="c1294-151">Connect to a secure cluster using a client certificate</span></span>

<span data-ttu-id="c1294-152">Kümedeki düğümler geçerli sertifikaların ortak adı olması gerekir veya SAN DNS adıyla görünür [RemoteCommonNames özelliği](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) ayarlamak [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="c1294-152">The nodes in the cluster must have valid certificates whose common name or DNS name in SAN appears in the [RemoteCommonNames property](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) set on [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span></span> <span data-ttu-id="c1294-153">Bu işlem aşağıdaki istemci ve küme düğümleri arasında karşılıklı kimlik doğrulamasını etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="c1294-153">Following this process enables mutual authentication between the client and the cluster nodes.</span></span>

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

### <a name="connect-to-a-secure-cluster-interactively-using-azure-active-directory"></a><span data-ttu-id="c1294-154">Etkileşimli olarak Azure Active Directory'yi kullanarak güvenli bir kümeye bağlanın</span><span class="sxs-lookup"><span data-stu-id="c1294-154">Connect to a secure cluster interactively using Azure Active Directory</span></span>

<span data-ttu-id="c1294-155">Aşağıdaki örnek, Azure Active Directory istemci kimliği ve sunucu sertifikası sunucu kimliği için kullanır.</span><span class="sxs-lookup"><span data-stu-id="c1294-155">The following example uses Azure Active Directory for client identity and server certificate for server identity.</span></span>

<span data-ttu-id="c1294-156">Bir iletişim kutusu penceresinin otomatik olarak etkileşimli oturum açma için kümeye bağlandıktan sonra açılır.</span><span class="sxs-lookup"><span data-stu-id="c1294-156">A dialog window automatically pops up for interactive sign-in upon connecting to the cluster.</span></span>

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

### <a name="connect-to-a-secure-cluster-non-interactively-using-azure-active-directory"></a><span data-ttu-id="c1294-157">Etkileşimsiz Azure Active Directory'yi kullanarak güvenli bir kümeye bağlanın</span><span class="sxs-lookup"><span data-stu-id="c1294-157">Connect to a secure cluster non-interactively using Azure Active Directory</span></span>

<span data-ttu-id="c1294-158">Aşağıdaki örnek Microsoft.IdentityModel.Clients.activedirectory tarafından üzerinde sürüm kullanır: 2.19.208020213.</span><span class="sxs-lookup"><span data-stu-id="c1294-158">The following example relies on Microsoft.IdentityModel.Clients.ActiveDirectory, Version: 2.19.208020213.</span></span>

<span data-ttu-id="c1294-159">AAD belirteci edinme hakkında daha fazla bilgi için bkz: [Microsoft.IdentityModel.Clients.activedirectory tarafından](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span><span class="sxs-lookup"><span data-stu-id="c1294-159">For more information on AAD token acquisition, see [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span></span>

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

### <a name="connect-to-a-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a><span data-ttu-id="c1294-160">Azure Active Directory'yi kullanarak önceki meta veri bilgisi olmadan güvenli bir kümeye bağlanın</span><span class="sxs-lookup"><span data-stu-id="c1294-160">Connect to a secure cluster without prior metadata knowledge using Azure Active Directory</span></span>

<span data-ttu-id="c1294-161">Aşağıdaki örnek, etkileşimli olmayan belirteç edinme kullanır, ancak aynı yaklaşımı özel etkileşimli belirteç edinme deneyim oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c1294-161">The following example uses non-interactive token acquisition, but the same approach can be used to build a custom interactive token acquisition experience.</span></span> <span data-ttu-id="c1294-162">Belirteç alımı için gereken Azure Active Directory meta veri kümesi yapılandırmasından okuyun.</span><span class="sxs-lookup"><span data-stu-id="c1294-162">The Azure Active Directory metadata needed for token acquisition is read from cluster configuration.</span></span>

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

## <a name="connect-to-a-secure-cluster-using-service-fabric-explorer"></a><span data-ttu-id="c1294-163">Service Fabric Explorer kullanarak güvenli bir kümeye bağlanın</span><span class="sxs-lookup"><span data-stu-id="c1294-163">Connect to a secure cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="c1294-164">Ulaşmaya [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) verilmiş bir küme için tarayıcınızı noktası:</span><span class="sxs-lookup"><span data-stu-id="c1294-164">To reach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) for a given cluster, point your browser to:</span></span>

`http://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="c1294-165">Tam URL Azure Portalı'nın küme essentials bölmesinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c1294-165">The full URL is also available in the cluster essentials pane of the Azure portal.</span></span>

### <a name="connect-to-a-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="c1294-166">Azure Active Directory'yi kullanarak güvenli bir kümeye bağlanın</span><span class="sxs-lookup"><span data-stu-id="c1294-166">Connect to a secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="c1294-167">AAD ile güvenli bir kümeye bağlanmak için tarayıcınızı noktası:</span><span class="sxs-lookup"><span data-stu-id="c1294-167">To connect to a cluster that is secured with AAD, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="c1294-168">Otomatik olarak sorulur AAD oturum oturum.</span><span class="sxs-lookup"><span data-stu-id="c1294-168">You are automatically be prompted to log in with AAD.</span></span>

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="c1294-169">Bir istemci sertifikası ile güvenli bir kümeye bağlanın</span><span class="sxs-lookup"><span data-stu-id="c1294-169">Connect to a secure cluster using a client certificate</span></span>

<span data-ttu-id="c1294-170">Sertifikaları güvenli bir kümeye bağlanmak için tarayıcınızı noktası:</span><span class="sxs-lookup"><span data-stu-id="c1294-170">To connect to a cluster that is secured with certificates, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="c1294-171">Otomatik olarak sorulur bir istemci sertifikası seçin.</span><span class="sxs-lookup"><span data-stu-id="c1294-171">You are automatically be prompted to select a client certificate.</span></span>

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-the-remote-computer"></a><span data-ttu-id="c1294-172">Uzak bilgisayarda bir istemci sertifikası ayarlama</span><span class="sxs-lookup"><span data-stu-id="c1294-172">Set up a client certificate on the remote computer</span></span>
<span data-ttu-id="c1294-173">Bir küme ve sunucu sertifikası ve istemci erişimi için başka bir küme güvenliğini sağlamak için en az iki sertifika kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c1294-173">At least two certificates should be used for securing the cluster, one for the cluster and server certificate and another for client access.</span></span>  <span data-ttu-id="c1294-174">Ayrıca ek ikincil sertifikalar ve istemci erişim sertifikalarını kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="c1294-174">We recommend that you also use additional secondary certificates and client access certificates.</span></span>  <span data-ttu-id="c1294-175">İstemci ve sertifika güvenliği kullanarak bir küme düğümünü arasındaki iletişimin güvenliğini sağlamak için önce istemci sertifikası edinin ve yükleyin gerekir.</span><span class="sxs-lookup"><span data-stu-id="c1294-175">To secure the communication between a client and a cluster node using certificate security, you first need to obtain and install the client certificate.</span></span> <span data-ttu-id="c1294-176">Kişisel (My) deposuna yerel bilgisayar veya geçerli kullanıcı sertifika yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="c1294-176">The certificate can be installed into the Personal (My) store of the local computer or the current user.</span></span>  <span data-ttu-id="c1294-177">İstemci küme doğrulanabilmesi Ayrıca sunucu sertifikasının parmak izi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c1294-177">You also need the thumbprint of the server certificate so that the client can authenticate the cluster.</span></span>

<span data-ttu-id="c1294-178">İstemci sertifikası kümeye erişmek bilgisayarda ayarlamak için aşağıdaki PowerShell cmdlet'ini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c1294-178">Run the following PowerShell cmdlet to set up the client certificate on the computer from which you access the cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

<span data-ttu-id="c1294-179">Kendinden imzalı bir sertifika ise, güvenli bir kümeye bağlanmak için bu sertifikayı kullanmadan önce makinenizin "güvenilir kişiler" deposuna içeri aktarmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c1294-179">If it is a self-signed certificate, you need to import it to your machine's "trusted people" store before you can use this certificate to connect to a secure cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a><span data-ttu-id="c1294-180">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c1294-180">Next steps</span></span>

* [<span data-ttu-id="c1294-181">Service Fabric kümesi yükseltme işlemi ve sizden beklentileri</span><span class="sxs-lookup"><span data-stu-id="c1294-181">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="c1294-182">Visual Studio'da, Service Fabric uygulamaları yönetme</span><span class="sxs-lookup"><span data-stu-id="c1294-182">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="c1294-183">Service Fabric sistem durumu modeli giriş</span><span class="sxs-lookup"><span data-stu-id="c1294-183">Service Fabric Health model introduction</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="c1294-184">Uygulama güvenliği ve farklı çalıştır</span><span class="sxs-lookup"><span data-stu-id="c1294-184">Application Security and RunAs</span></span>](service-fabric-application-runas-security.md)
* [<span data-ttu-id="c1294-185">Service Fabric CLI ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c1294-185">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
