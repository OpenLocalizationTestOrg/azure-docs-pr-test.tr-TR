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
# <a name="connect-tooa-secure-cluster"></a>Tooa güvenli kümesine bağlanın

İstemci tooa Service Fabric küme düğümü bağlandığında hello istemci kimliği doğrulanmış ve güvenli iletişim sertifika güvenliği veya Azure Active Directory (AAD) kullanılarak oluşturulmuş olabilir. Bu kimlik doğrulaması yalnızca yetkili kullanıcılar hello küme erişebilir ve uygulamaları dağıtılan ve yönetim görevlerini gerçekleştirme sağlar.  Merhaba küme oluşturulduğunda sertifika veya AAD güvenlik önceden hello kümede etkinleştirilmiş olmalıdır.  Küme güvenlik senaryoları hakkında daha fazla bilgi için bkz: [küme güvenlik](service-fabric-cluster-security.md). Sertifikalar ile güvenlik altına tooa küme bağlanıyorsanız [hello istemci sertifika ayarlama](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) hello bilgisayarda toohello küme bağlanır. 

<a id="connectsecureclustercli"></a> 

## <a name="connect-tooa-secure-cluster-using-azure-service-fabric-cli-sfctl"></a>Azure Service Fabric CLI (sfctl) kullanarak tooa güvenli kümesine bağlanın

Merhaba Service Fabric CLI (sfctl) kullanan birkaç farklı şekilde tooconnect tooa güvenli kümesi vardır. Bir istemci sertifikası kimlik doğrulamasını kullanırken, bir sertifika ayrıntıları eşleşmelidir hello sertifika toohello küme düğümleri dağıtılır. Sertifikanızı sertifika yetkilileri (CA) varsa, tooadditionally gerekir hello güvenilen CA'ları belirtin.

Hello kullanarak tooa küme bağlanabilir `sfctl cluster select` komutu.

İstemci sertifikaları, bir sertifika ve anahtar çifti olarak ya da tek pem dosyası olarak iki farklı fashions belirtilebilir. Parola korumalı için `pem` dosyaları olacaktır otomatik olarak tooenter hello parola istenir.

pem dosyası olarak toospecify hello istemci sertifikası hello hello dosya yolu belirtin `--pem` bağımsız değişkeni. Örneğin:

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Parola korumalı pem dosyaları için parola önceki toorunning herhangi bir komut isteminde bulunur.

bir sertifika toospecify, anahtar çiftini kullanın hello `--cert` ve `--key` toospecify hello dosya yolları tooeach ilgili dosyasından bağımsız değişkenler.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

Bazen kullanılan sertifikaları toosecure test veya geliştirme kümeleri sertifika doğrulaması başarısız. toobypass sertifika doğrulama hello belirtin `--no-verify` seçeneği. Örneğin:

> [!WARNING]
> Merhaba kullanmayın `no-verify` tooproduction Service Fabric kümeleri bağlanırken seçeneği.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

Ayrıca, güvenilir CA sertifikaları ya da tek tek sertifikaları yolları toodirectories belirtebilirsiniz. toospecify bu yollar kullanın hello `--ca` bağımsız değişkeni. Örneğin:

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

Bağlandıktan sonra çok gerekir[diğer sfctl komutlarının çalıştırılmasını](service-fabric-cli.md) toointeract hello kümesi ile.

<a id="connectsecurecluster"></a>

## <a name="connect-tooa-cluster-using-powershell"></a>PowerShell kullanarak tooa kümesine bağlanın
PowerShell aracılığıyla bir kümede işlemleri gerçekleştirmeden önce ilk bağlantı toohello küme oluşturun. Merhaba küme bağlantısı PowerShell oturumu verilen hello izleyen tüm komutlar için kullanılır.

### <a name="connect-tooan-unsecure-cluster"></a>Tooan güvensiz kümesine bağlanın

güvenli olmayan tooconnect tooan küme, hello küme uç noktası adresi toohello sağlayın **Connect-ServiceFabricCluster** komutu:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a>Azure Active Directory'yi kullanarak tooa güvenli kümesine bağlanın

Azure Active Directory tooauthorize küme yönetici erişimi kullanan tooconnect tooa güvenli küme hello küme sertifika parmak izi sağlayın ve hello kullan *AzureActiveDirectory* bayrağı.  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Bir istemci sertifikası kullanarak tooa güvenli kümesine bağlanın
İstemci sertifikaları tooauthorize yönetici erişimi tooconnect tooa güvenli küme PowerShell komutunu aşağıdaki çalışma hello kullanır. Merhaba küme sertifika parmak izi ve küme yönetimi için izinler verildiyse hello istemci sertifikasının hello parmak izi sağlayın. Merhaba sertifika ayrıntıları hello küme düğümlerinde bir sertifika ile eşleşmesi gerekir.

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

*ServerCertThumbprint* hello parmak izi hello küme düğümlerinde yüklü hello sunucu sertifikası. *FindValue* hello parmak izi hello yönetici istemci sertifikası.
Merhaba parametreleri doldurulduğunda, hello komutu aşağıdaki örneğine hello gibi görünür: 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-tooa-secure-cluster-using-windows-active-directory"></a>Windows Active Directory kullanarak tooa güvenli kümesine bağlanın
Tek başına kümenizi AD güvenlik kullanarak dağıtılmışsa, başlangıç anahtarı "WindowsCredential" ekleyerek toohello kümesine bağlanın.

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-tooa-cluster-using-hello-fabricclient-apis"></a>Merhaba FabricClient API'lerini kullanarak tooa kümesine bağlanın
Merhaba Service Fabric SDK sağlar hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) küme yönetimi için sınıf. toouse hello FabricClient API'leri hello Microsoft.ServiceFabric NuGet paketi alın.

### <a name="connect-tooan-unsecure-cluster"></a>Tooan güvensiz kümesine bağlanın

tooconnect tooa uzaktan güvenli olmayan küme, FabricClient örneği oluşturun ve hello küme adresini sağlayın:

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

Bir küme içinde çalışan için kodu, örneğin, güvenilir bir hizmetinde bir FabricClient oluşturmak *olmadan* hello küme adresi belirtme. FabricClient bağlayan toohello yerel yönetim hello düğüm hello kodu üzerinde ağ geçidi şu anda çalışıyorsa, ek ağ atlama önleme.

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Bir istemci sertifikası kullanarak tooa güvenli kümesine bağlanın

Merhaba kümedeki Hello düğümler geçerli sertifikaların ortak adı olması gerekir veya DNS adının SAN'hello [RemoteCommonNames özelliği](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) ayarlamak [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient). Bu işlem aşağıdaki hello istemci hello küme düğümleri arasında karşılıklı kimlik doğrulamasını etkinleştirir.

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

### <a name="connect-tooa-secure-cluster-interactively-using-azure-active-directory"></a>Etkileşimli olarak Azure Active Directory'yi kullanarak tooa güvenli kümesine bağlanın

Örnek kullanan Azure Active Directory istemci kimliği ve sunucu sertifikası sunucu kimliği için aşağıdaki hello.

Bir iletişim kutusu penceresinin otomatik olarak etkileşimli oturum açma için toohello küme bağlandıktan sonra açılır.

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

### <a name="connect-tooa-secure-cluster-non-interactively-using-azure-active-directory"></a>Tooa güvenli küme etkileşimsiz Azure Active Directory'yi kullanarak bağlan

Merhaba aşağıdaki örnek dayanır Microsoft.IdentityModel.Clients.activedirectory tarafından üzerinde sürüm: 2.19.208020213.

AAD belirteci edinme hakkında daha fazla bilgi için bkz: [Microsoft.IdentityModel.Clients.activedirectory tarafından](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).

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

### <a name="connect-tooa-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a>Azure Active Directory'yi kullanarak önceki meta veri bilgisi olmadan tooa güvenli kümesine bağlanın

Hello aşağıdaki örnek etkileşimli olmayan belirteç edinme, kullanır, ancak hello aynı yaklaşımı kullanılan toobuild özel etkileşimli belirteç edinme deneyimi olabilir. belirteç alımı için gereken hello Azure Active Directory meta veri kümesi yapılandırmasından okuyun.

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

## <a name="connect-tooa-secure-cluster-using-service-fabric-explorer"></a>Service Fabric Explorer kullanarak tooa güvenli kümesine bağlanın
tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) verilmiş bir küme için tarayıcınızı noktası:

`http://<your-cluster-endpoint>:19080/Explorer`

Merhaba tam URL hello küme essentials bölmesinde hello Azure portalında kullanılabilir.

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a>Azure Active Directory'yi kullanarak tooa güvenli kümesine bağlanın

AAD ile güvenli tooconnect tooa küme tarayıcınıza noktası:

`https://<your-cluster-endpoint>:19080/Explorer`

Otomatik olarak olması AAD oturum istendiğinde toolog.

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Bir istemci sertifikası kullanarak tooa güvenli kümesine bağlanın

Sertifikalar ile güvenli tooconnect tooa küme tarayıcınıza noktası:

`https://<your-cluster-endpoint>:19080/Explorer`

Otomatik olarak olması istendiğinde tooselect bir istemci sertifikası.

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-hello-remote-computer"></a>Bir istemci sertifikası hello uzak bilgisayarda ayarlama
En az iki sertifika hello küme, hello küme ve sunucu sertifikası için bir ve istemci erişimi için başka bir güvenliğini sağlamak için kullanılmalıdır.  Ayrıca ek ikincil sertifikalar ve istemci erişim sertifikalarını kullanmanızı öneririz.  bir istemci arasında kullanarak bir küme düğümü toosecure hello iletişimi sertifika güvenlik, ilk tooobtain gerekir ve hello istemci sertifikası yükleyin. Merhaba sertifika hello kişisel (My) deposuna hello yerel bilgisayar veya hello geçerli kullanıcı yüklenebilir.  Merhaba istemci hello küme doğrulanabilmesi hello sertifikanın parmak izini hello sunucu da gerekir.

PowerShell cmdlet tooset hello istemci sertifika hello kümeye erişmek hello bilgisayarda aşağıdaki hello çalıştırın.

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

Kendinden imzalı bir sertifika varsa, bu sertifika tooconnect tooa güvenli küme kullanmadan önce onu tooyour makinenin "güvenilir kişiler" saklayın tooimport gerekir.

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a>Sonraki adımlar

* [Service Fabric kümesi yükseltme işlemi ve sizden beklentileri](service-fabric-cluster-upgrade.md)
* [Visual Studio'da, Service Fabric uygulamaları yönetme](service-fabric-manage-application-in-visual-studio.md)
* [Service Fabric sistem durumu modeli giriş](service-fabric-health-introduction.md)
* [Uygulama güvenliği ve farklı çalıştır](service-fabric-application-runas-security.md)
* [Service Fabric CLI ile çalışmaya başlama](service-fabric-cli.md)
