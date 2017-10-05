---
title: "Sertifikaları kullanarak Windows Azure Service Fabric kümede güvenli | Microsoft Docs"
description: "Bu makalede, tek başına veya istemciler arasında iyi özel küme ve küme içinde iletişimin güvenliğini sağlamak açıklar."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: fe0ed74c-9af5-44e9-8d62-faf1849af68c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dekapur
ms.openlocfilehash: 71ece1e43cc3c4ac3350cd59633065de06672420
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a>X.509 sertifikaları kullanarak Windows'u bir tek başına kümede güvenli
Bu kümeye bağlanan istemciler X.509 kullanarak kimlik doğrulaması için sertifikaları nasıl bu makalede, tek başına Windows kümeniz çeşitli düğümleri arasındaki iletişimin güvenliğini sağlamak de açıklar. Bu, yalnızca yetkili kullanıcılar kümeye dağıtılan uygulamalar erişmek ve yönetim görevlerini gerçekleştirme sağlar.  Küme oluşturulduğunda sertifika güvenliği kümede etkinleştirilmelidir.  

Düğümü düğümü güvenlik, istemci düğümü güvenlik ve rol tabanlı erişim denetimi gibi küme güvenlik üzerinde daha fazla bilgi için bkz: [küme güvenlik senaryoları](service-fabric-cluster-security.md).

## <a name="which-certificates-will-you-need"></a>Hangi sertifikaların ihtiyacınız olacak?
İle başlamak [tek başına küme paketini karşıdan](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) kümenizdeki düğümlerin birinde. İndirilen paketteki, bulacaksınız bir **ClusterConfig.X509.MultiMachine.json** dosya. Dosyasını açın ve bölümünü gözden **güvenlik** altında **özellikleri** bölümü:

```JSON
"security": {
    "metadata": "The Credential type X509 indicates this is cluster is secured using X509 Certificates. The thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
    "ClusterCredentialType": "X509",
    "ServerCredentialType": "X509",
    "CertificateInformation": {
        "ClusterCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },        
        "ClusterCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ServerCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ServerCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ClientCertificateThumbprints": [
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": false
            },
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ClientCertificateCommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]",
                "CertificateIssuerThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ReverseProxyCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ReverseProxyCertificateCommonNames": {
            "CommonNames": [
                {
                "CertificateCommonName": "[CertificateCommonName]"
                }
            ],
            "X509StoreName": "My"
        }
    }
},
```

Bu bölümde, tek başına Windows kümeniz güvenliğini sağlamak için gereken sertifikaları açıklanmaktadır. Bir küme sertifika belirtiyorsanız değerini ayarlamak **ClusterCredentialType** için  _**X509**_. Dış bağlantıları için sunucu sertifikası belirtiyorsanız ayarlamak **ServerCredentialType** için  _**X509**_. Zorunlu değil, ancak düzgün güvenli bir küme için bu iki sertifikalara sahip olmasını öneririz. Bu değerleri ayarlamak, *X509* sonra da Service Fabric ve karşılık gelen sertifika bir özel durum oluşturur de belirtmeniz gerekir. Bazı senaryolarda, yalnızca belirtmek isteyebilirsiniz _ClientCertificateThumbprints_ veya _ReverseProxyCertificate_. Bu senaryolarda, ayarlanmamış _ClusterCredentialType_ veya _ServerCredentialType_ için _X509_.


> [!NOTE]
> A [parmak izi](https://en.wikipedia.org/wiki/Public_key_fingerprint) bir sertifika birincil kimliğidir. Okuma [bir sertifikanın parmak izini alma](https://msdn.microsoft.com/library/ms734695.aspx) oluşturduğunuz sertifika parmak izi bulunamıyor.
> 
> 

Aşağıdaki tabloda, Küme kurulumu gerekir sertifikaları listelenmektedir:

| **CertificateInformation ayarı** | **Açıklama** |
| --- | --- |
| ClusterCertificate |Test ortamı için önerilir. Bu sertifika, bir küme düğümlerinde arasındaki iletişimin güvenliğini sağlamak için gereklidir. İki farklı sertifikaları, birincil ve ikincil bir yükseltme için kullanabilirsiniz. Sertifikanın parmak izi birincil ayarlamak **parmak izi** bölümü ve, ikincil **ThumbprintSecondary** değişkenleri. |
| ClusterCertificateCommonNames |Üretim ortamı için önerilir. Bu sertifika, bir küme düğümlerinde arasındaki iletişimin güvenliğini sağlamak için gereklidir. Bir veya iki küme sertifika ortak adları kullanabilirsiniz. |
| ServerCertificate |Test ortamı için önerilir. Bu kümeye bağlanmaya çalıştığında bu sertifikayı istemciye sunulur. Kolaylık olması için için aynı sertifika kullanmayı tercih edebileceğiniz *ClusterCertificate* ve *ServerCertificate*. İki farklı sunucu sertifikaları, birincil ve ikincil bir yükseltme için kullanabilirsiniz. Sertifikanın parmak izi birincil ayarlamak **parmak izi** bölümü ve, ikincil **ThumbprintSecondary** değişkenleri. |
| ServerCertificateCommonNames |Üretim ortamı için önerilir. Bu kümeye bağlanmaya çalıştığında bu sertifikayı istemciye sunulur. Kolaylık olması için için aynı sertifika kullanmayı tercih edebileceğiniz *ClusterCertificateCommonNames* ve *ServerCertificateCommonNames*. Bir veya iki sunucu sertifika ortak adları kullanabilirsiniz. |
| ClientCertificateThumbprints |Kimliği doğrulanmış istemcilerde yüklemek istediğiniz sertifika kümesidir. Bir dizi farklı istemci sertifikaları, küme erişmesine izin vermek istediğiniz makinelerde yüklü olabilir. Her sertifikanın parmak izini ayarlamak **CertificateThumbprint** değişkeni. Ayarlarsanız **IsAdmin** için *doğru*, sonra istemcinin yüklü bu sertifikayla yönetici küme yönetimi etkinliklerini yapabilirsiniz. Varsa **IsAdmin** olan *yanlış*, istemcinin bu sertifikayla yalnızca kullanıcı erişim haklarını, salt okunur genellikle için izin verilen eylemleri gerçekleştirebilirsiniz. Rolleri hakkında daha fazla bilgi için okumaya devam [rol tabanlı erişim denetimi (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac) |
| ClientCertificateCommonNames |İlk istemci sertifikası için ortak adı ayarlama **CertificateCommonName**. **CertificateIssuerThumbprint** bu sertifikayı verenin parmak izi olan. Okuma [sertifikalarla çalışma](https://msdn.microsoft.com/library/ms731899.aspx) ortak adları ve veren hakkında daha fazla bilgi edinmek için. |
| ReverseProxyCertificate |Test ortamı için önerilir. Bu, olabilir, isteğe bağlı bir sertifikadır güvenli isteyip istemediğinizi belirtilen, [Ters Proxy](service-fabric-reverseproxy.md). Bu sertifika kullanıyorsanız reverseProxyEndpointPort nodeTypes ayarlandığından emin olun. |
| ReverseProxyCertificateCommonNames |Üretim ortamı için önerilir. Bu, olabilir, isteğe bağlı bir sertifikadır güvenli isteyip istemediğinizi belirtilen, [Ters Proxy](service-fabric-reverseproxy.md). Bu sertifika kullanıyorsanız reverseProxyEndpointPort nodeTypes ayarlandığından emin olun. |

Burada küme, sunucu ve istemci sertifikaları sağlanan örnek küme yapılandırması İşte. Küme için lütfen unutmayın / sunucu / reverseProxy sertifikalar, parmak izi ve ortak adı için aynı sertifika türü birlikte yapılandırılması izin verilmez.

 ```JSON
 {
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "2016-09-26",
    "nodes": [{
        "nodeName": "vm0",
        "metadata": "Replace the localhost below with valid IP address or FQDN",
        "iPAddress": "10.7.0.5",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "metadata": "Replace the localhost with valid IP address or FQDN",
        "iPAddress": "10.7.0.4",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "10.7.0.6",
        "metadata": "Replace the localhost with valid IP address or FQDN",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],
    "properties": {
        "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
        }
        "security": {
            "metadata": "The Credential type X509 indicates this is cluster is secured using X509 Certificates. The thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
            "ClusterCredentialType": "X509",
            "ServerCredentialType": "X509",
            "CertificateInformation": {
                "ClusterCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myClusterCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ServerCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myServerCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ClientCertificateThumbprints": [{
                    "CertificateThumbprint": "c4 c18 8e aa a8 58 77 98 65 f8 61 4a 0d da 4c 13 c5 a1 37 6e",
                    "IsAdmin": false
                }, {
                    "CertificateThumbprint": "71 de 04 46 7c 9e d0 54 4d 02 10 98 bc d4 4c 71 e1 83 41 4e",
                    "IsAdmin": true
                }]
            }
        },
        "reliabilityLevel": "Bronze",
        "nodeTypes": [{
            "name": "NodeType0",
            "clientConnectionEndpointPort": "19000",
            "clusterConnectionEndpointPort": "19001",
            "leaseDriverEndpointPort": "19002",
            "serviceConnectionEndpointPort": "19003",
            "httpGatewayEndpointPort": "19080",
            "applicationPorts": {
                "startPort": "20001",
                "endPort": "20031"
            },
            "ephemeralPorts": {
                "startPort": "20032",
                "endPort": "20062"
            },
            "isPrimary": true
        }
         ],
        "fabricSettings": [{
            "name": "Setup",
            "parameters": [{
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
            }, {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
            }]
        }]
    }
}
 ```

## <a name="certificate-roll-over"></a>Sertifika geçir
Sertifika ortak adı yerine parmak izi kullanırken, sertifika alma üzerinden küme yapılandırması yükseltme gerektirmez.
Sertifika alma üzerinden içeriyorsa veren geçir, lütfen tutma cert eski veren cert depolamak yeni sertifikayı veren sertifika yükledikten sonra en az 2 saat.

## <a name="acquire-the-x509-certificates"></a>X.509 sertifikaları alma
Küme içindeki iletişimin güvenliğini sağlamak için ilk X.509 sertifikaları için Küme düğümlerinizi edinmeniz gerekir. Ayrıca, yetkili makineler/kullanıcıların bu kümeye bağlantı sınırlamak için elde edilir ve istemci makineleri için sertifikaları yüklemek gerekecektir.

Üretim iş yükleri çalıştıran kümeler için kullanmanız gereken bir [sertifika yetkilisi (CA)](https://en.wikipedia.org/wiki/Certificate_authority) küme güvenli hale getirmek için X.509 sertifikası imzalanmış. Bu sertifikaları edinme hakkında ayrıntılar için Git [nasıl yapılır: bir sertifika edinin](http://msdn.microsoft.com/library/aa702761.aspx).

Test amaçları için kullandığınız kümeler için otomatik olarak imzalanan bir sertifika kullanmayı da tercih edebilirsiniz.

## <a name="optional-create-a-self-signed-certificate"></a>İsteğe bağlı: otomatik olarak imzalanan bir sertifika oluşturun
Doğru bir şekilde güvenli hale getirilebilir otomatik olarak imzalanan bir sertifika oluşturmak için bir yol kullanmaktır *CertSetup.ps1* betik dizinindeki Service Fabric SDK klasöründeki *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\ Güvenli*. Sertifikayı varsayılan adını değiştirmek için bu dosyayı düzenlemek (değeri Ara *CN ServiceFabricDevClusterCert =*). Bu komut dosyası olarak çalıştıracak `.\CertSetup.ps1 -Install`.

Şimdi Sertifika PFX dosyasını korumalı bir parola ile dışa aktarın. İlk sertifikanın parmak izini edinin. Gelen *Başlat* çalıştırmak menüsünde *bilgisayar sertifikalarını yönetmek*. Gidin **yerel Bilgisayar\Kişisel** klasörü ve yeni sertifikayı oluşturan bulma. Açmak için seçin sertifikayı çift tıklatın *ayrıntıları* sekmesinde ve ekranı aşağı kaydırarak *parmak izi* alan. Parmak izi değeri, aşağıdaki PowerShell komutunu alanları kaldırdıktan sonra kopyalayın.  Değişiklik `String` koruyun ve PowerShell içinde aşağıdaki çalıştırmak için uygun bir güvenli parola değerine:

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

Makinede yüklü bir sertifika ayrıntılarını görmek için aşağıdaki PowerShell komutunu çalıştırabilirsiniz:

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

Alternatif olarak, bir Azure aboneliğiniz varsa, bölümü izleyin [sertifikaları anahtar Kasası'na eklemek](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).

## <a name="install-the-certificates"></a>Sertifika Yükleme
Sertifikaları olduktan sonra küme düğümleri üzerinde yükleyebilirsiniz. Düğümleriniz en son Windows PowerShell gerek 3.x yüklü. Küme ve sunucu sertifikaları ve tüm ikincil sertifikaları için her bir düğümde aşağıdaki adımları yinelemeniz gerekecek.

1. .Pfx dosyaları düğüme kopyalayın.
2. Bir yönetici olarak bir PowerShell penceresi açın ve aşağıdaki komutları yazın. Değiştir *$pswd* bu sertifikayı oluşturmak için kullanılan parola ile. Değiştir *$PfxFilePath* .pfx tam yoluna sahip bu düğüme kopyalanır.
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. Şimdi ağ hizmeti hesabı altında çalışır, Service Fabric işlem, aşağıdaki komut dosyası çalıştırarak kullanabilmesi için bu sertifikaya erişim denetimini ayarlayın. Hizmet hesabı "NETWORK SERVICE" ve sertifika parmak izini verin. Sertifikada açarak sertifika ACL'lerin doğru olduğundan emin olun *Başlat* > *bilgisayar sertifikalarını yönetmek* ve bakarak *tüm görevler*  >  *Özel anahtarları Yönet*.
   
    ```powershell
    param
    (
    [Parameter(Position=1, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$pfxThumbPrint,
   
    [Parameter(Position=2, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$serviceAccount
    )
   
    $cert = Get-ChildItem -Path cert:\LocalMachine\My | Where-Object -FilterScript { $PSItem.ThumbPrint -eq $pfxThumbPrint; }
   
    # Specify the user, the permissions and the permission type
    $permission = "$($serviceAccount)","FullControl","Allow"
    $accessRule = New-Object -TypeName System.Security.AccessControl.FileSystemAccessRule -ArgumentList $permission
   
    # Location of the machine related keys
    $keyPath = Join-Path -Path $env:ProgramData -ChildPath "\Microsoft\Crypto\RSA\MachineKeys"
    $keyName = $cert.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
    $keyFullPath = Join-Path -Path $keyPath -ChildPath $keyName
   
    # Get the current acl of the private key
    $acl = (Get-Item $keyFullPath).GetAccessControl('Access')
   
    # Add the new ace to the acl of the private key
    $acl.SetAccessRule($accessRule)
   
    # Write back the new acl
    Set-Acl -Path $keyFullPath -AclObject $acl -ErrorAction Stop
   
    # Observe the access rights currently assigned to this certificate.
    get-acl $keyFullPath| fl
    ```
4. Her sunucu sertifikası için yukarıdaki adımları yineleyin. Küme erişmesine izin vermek istediğiniz makinelere istemci sertifikalarını yüklemek için aşağıdaki adımları da kullanabilirsiniz.

## <a name="create-the-secure-cluster"></a>Güvenli küme oluşturma
Yapılandırdıktan sonra **güvenlik** bölümünü **ClusterConfig.X509.MultiMachine.json** dosyası devam etmek için [kümenizi oluşturduktan](service-fabric-cluster-creation-for-windows-server.md#createcluster) düğümleri yapılandırma bölümü ve tek başına küme oluşturun. Kullanmayı unutmayın **ClusterConfig.X509.MultiMachine.json** küme oluşturma sırasında dosya. Örneğin, komutunuzu aşağıdakine benzeyebilir:

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

Güvenli tek başına Windows başarıyla çalışan küme ve buna bağlanmak için kimliği doğrulanmış istemciler ayarladıktan sonra bölümü izleyin [PowerShell kullanarak güvenli bir kümeye Bağlan](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) bağlanmak için. Örneğin:

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

Ardından, bu küme ile çalışmak için diğer PowerShell komutları çalıştırabilirsiniz. Örneğin, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) güvenli bu kümede düğümler listesi göstermek için.


Küme kaldırmak için Service Fabric paketi indirdiğiniz küme düğümünde bağlanmak, bir komut satırı açın ve paket klasörüne gidin. Şimdi aşağıdaki komutu çalıştırın:

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> Yanlış sertifika yapılandırması Küme dağıtımı sırasında yaklaşan engellemek. Kendi kendine güvenlik sorunları tanılamak için lütfen Olay Görüntüleyicisi'ni grubunda bakın *uygulama ve hizmet günlükleri* > *Microsoft Service Fabric*.
> 
> 

