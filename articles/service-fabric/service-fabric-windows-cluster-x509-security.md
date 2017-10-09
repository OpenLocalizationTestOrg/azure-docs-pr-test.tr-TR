---
title: "aaaSecure Azure Service Fabric kümesi sertifikaları kullanarak Windows üzerinde | Microsoft Docs"
description: "Bu makalede nasıl toosecure iletişimi hello tek başına veya özel küme de istemcileri ve hello küme arasında açıklanmaktadır."
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
ms.openlocfilehash: f0d411963615349a84edfc8125dec4ee5908f146
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a>X.509 sertifikaları kullanarak Windows'u bir tek başına kümede güvenli
Bu makalede nasıl toosecure hello iletişimine hello çeşitli, tek başına Windows küme düğümlerinin de nasıl toothis küme bağlanan tooauthenticate istemcileri X.509 sertifikaları kullanma açıklanır. Bu, yalnızca yetkili kullanıcılar hello küme erişebilir dağıtılan uygulamalar hello ve yönetim görevlerini gerçekleştirme sağlar.  Merhaba küme oluşturulduğunda sertifika güvenliği hello kümede etkinleştirilmelidir.  

Düğümü düğümü güvenlik, istemci düğümü güvenlik ve rol tabanlı erişim denetimi gibi küme güvenlik üzerinde daha fazla bilgi için bkz: [küme güvenlik senaryoları](service-fabric-cluster-security.md).

## <a name="which-certificates-will-you-need"></a>Hangi sertifikaların ihtiyacınız olacak?
ile toostart [hello tek başına küme paketini indirin](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) kümenizdeki hello düğümlerinin tooone. Size Hello paket, karşıdan bir **ClusterConfig.X509.MultiMachine.json** dosya. Merhaba dosyasını açın ve hello bölümünü gözden **güvenlik** hello altında **özellikleri** bölümü:

```JSON
"security": {
    "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
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

Bu bölümde, tek başına Windows kümeniz güvenliğini sağlamak için gereksinim duyduğunuz hello sertifikaları açıklanmaktadır. Bir küme sertifika belirtiyorsanız hello değerini ayarlamak **ClusterCredentialType** too_**X509**_. Dış bağlantıları için sunucu sertifikası belirtiyorsanız hello ayarlamak **ServerCredentialType** çok_**X509**_. Zorunlu değil, ancak her iki bu sertifikaların düzgün bir şekilde güvenli bir küme için toohave öneririz. Bu değerleri çok ayarlarsanız*X509* sonra karşılık gelen sertifikaları hello veya Service Fabric bir özel durum oluşturur belirtmeniz gerekir. Bazı senaryolarda, yalnızca toospecify hello isteyebilirsiniz _ClientCertificateThumbprints_ veya _ReverseProxyCertificate_. Bu senaryolarda, ayarlanmamış _ClusterCredentialType_ veya _ServerCredentialType_ too_X509_.


> [!NOTE]
> A [parmak izi](https://en.wikipedia.org/wiki/Public_key_fingerprint) hello birincil bir sertifika kimliğidir. Okuma [nasıl tooretrieve bir sertifikanın parmak izini](https://msdn.microsoft.com/library/ms734695.aspx) toofind hello parmak izi oluşturduğunuz hello sertifikaların çıkışı.
> 
> 

Merhaba aşağıdaki tabloda, Küme kurulumu gerekir hello sertifikaları listelenmektedir:

| **CertificateInformation ayarı** | **Açıklama** |
| --- | --- |
| ClusterCertificate |Test ortamı için önerilir. Bu sertifika bir kümede hello düğümler arasında gerekli toosecure hello iletişim yok. İki farklı sertifikaları, birincil ve ikincil bir yükseltme için kullanabilirsiniz. Merhaba sertifikanın parmak izini hello birincil hello ayarlamak **parmak izi** bölümü ve, hello hello ikincil **ThumbprintSecondary** değişkenleri. |
| ClusterCertificateCommonNames |Üretim ortamı için önerilir. Bu sertifika bir kümede hello düğümler arasında gerekli toosecure hello iletişim yok. Bir veya iki küme sertifika ortak adları kullanabilirsiniz. |
| ServerCertificate |Test ortamı için önerilir. Tooconnect toothis küme çalıştığında bu sertifikayı toohello istemci sunulur. Toouse seçebileceğiniz kolaylık sağlamak için aynı sertifika için hello *ClusterCertificate* ve *ServerCertificate*. İki farklı sunucu sertifikaları, birincil ve ikincil bir yükseltme için kullanabilirsiniz. Merhaba sertifikanın parmak izini hello birincil hello ayarlamak **parmak izi** bölümü ve, hello hello ikincil **ThumbprintSecondary** değişkenleri. |
| ServerCertificateCommonNames |Üretim ortamı için önerilir. Tooconnect toothis küme çalıştığında bu sertifikayı toohello istemci sunulur. Toouse seçebileceğiniz kolaylık sağlamak için aynı sertifika için hello *ClusterCertificateCommonNames* ve *ServerCertificateCommonNames*. Bir veya iki sunucu sertifika ortak adları kullanabilirsiniz. |
| ClientCertificateThumbprints |Kimliği doğrulanmış hello istemcilerde tooinstall istediğiniz sertifikaları kümesidir. Bir dizi farklı istemci sertifikalarını tooallow erişim toohello küme istediğiniz hello makinelerde yüklü olabilir. Merhaba sertifikanın parmak izini her hello ayarlamak **CertificateThumbprint** değişkeni. Merhaba ayarlarsanız **IsAdmin** çok*doğru*, sonra hello istemci yüklü bu sertifikayla yönetici hello küme yönetimi etkinliklerini yapabilirsiniz. Merhaba, **IsAdmin** olan *yanlış*, bu sertifikayla hello istemci yalnızca kullanıcı erişim haklarını, salt okunur genellikle izin hello eylemleri gerçekleştirin. Rolleri hakkında daha fazla bilgi için okumaya devam [rol tabanlı erişim denetimi (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac) |
| ClientCertificateCommonNames |Set hello ortak adı hello ilk istemci sertifikası hello için **CertificateCommonName**. Merhaba **CertificateIssuerThumbprint** hello için bu sertifikayı veren hello parmak izi olan. Okuma [sertifikalarla çalışma](https://msdn.microsoft.com/library/ms731899.aspx) tooknow ortak adları ve hello veren hakkında daha fazla bilgi. |
| ReverseProxyCertificate |Test ortamı için önerilir. Bu, olabilir, isteğe bağlı bir sertifikadır toosecure isteyip istemediğinizi belirtilen, [Ters Proxy](service-fabric-reverseproxy.md). Bu sertifika kullanıyorsanız reverseProxyEndpointPort nodeTypes ayarlandığından emin olun. |
| ReverseProxyCertificateCommonNames |Üretim ortamı için önerilir. Bu, olabilir, isteğe bağlı bir sertifikadır toosecure isteyip istemediğinizi belirtilen, [Ters Proxy](service-fabric-reverseproxy.md). Bu sertifika kullanıyorsanız reverseProxyEndpointPort nodeTypes ayarlandığından emin olun. |

Burada hello küme, sunucu ve istemci sertifikaları sağlanan örnek küme yapılandırması İşte. Küme için lütfen unutmayın / sunucu / reverseProxy sertifikalar, parmak izi ve ortak ad verilmez toobe yapılandırılmış birlikte hello için aynı sertifika türü.

 ```JSON
 {
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "2016-09-26",
    "nodes": [{
        "nodeName": "vm0",
        "metadata": "Replace hello localhost below with valid IP address or FQDN",
        "iPAddress": "10.7.0.5",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "iPAddress": "10.7.0.4",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "10.7.0.6",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],
    "properties": {
        "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
        }
        "security": {
            "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
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
Sertifika alma üzerinden veren içeriyorsa, UTC'ye, lütfen hello eski veren sertifika hello sertifika deposunda hello yeni sertifikayı veren sertifika yükledikten sonra en az 2 saat tutmak.

## <a name="acquire-hello-x509-certificates"></a>Merhaba X.509 sertifikaları alma
Merhaba küme içinde toosecure iletişimi, küme düğümleri için tooobtain X.509 sertifikalarını ilk gerekir. Ayrıca, toolimit bağlantı toothis tooauthorized makineleri/kullanıcılar küme, tooobtain ihtiyacınız ve hello istemci makineleri için sertifikaları yükleyin.

Üretim iş yükleri çalıştıran kümeler için kullanmanız gereken bir [sertifika yetkilisi (CA)](https://en.wikipedia.org/wiki/Certificate_authority) X.509 sertifikası toosecure hello küme imzalanmış. Bu sertifikaları edinme hakkında ayrıntılı bilgi için çok gidin[nasıl yapılır: bir sertifika edinin](http://msdn.microsoft.com/library/aa702761.aspx).

Test amaçları için kullandığınız kümeler için otomatik olarak imzalanan bir sertifika toouse seçebilirsiniz.

## <a name="optional-create-a-self-signed-certificate"></a>İsteğe bağlı: otomatik olarak imzalanan bir sertifika oluşturun
Tek yönlü toocreate doğru şekilde güvenli hale getirilebilir otomatik olarak imzalanan bir sertifika olduğundan toouse hello *CertSetup.ps1* hello dizin hello Service Fabric SDK klasöründe betik *C:\Program Files\Microsoft SDKs\Service Fabric\ ClusterSetup\Secure*. Bu dosya toochange hello varsayılan adını hello sertifika Düzenle (Merhaba değeri Ara *CN ServiceFabricDevClusterCert =*). Bu komut dosyası olarak çalıştıracak `.\CertSetup.ps1 -Install`.

Şimdi hello sertifika tooa PFX dosyasını korumalı bir parolayla dışarı aktarın. İlk hello sertifikanın parmak izini hello alın. Merhaba gelen *Başlat* hello çalıştırmak menüsünde *bilgisayar sertifikalarını yönetmek*. Toohello gidin **yerel Bilgisayar\Kişisel** klasörü ve hello sertifika, yalnızca Bul oluşturuldu. Merhaba sertifika tooopen çift tıklayın, select hello *ayrıntıları* sekmesi ve toohello aşağı kaydırın *parmak izi* alan. Merhaba, aşağıdaki PowerShell komutunu hello alanları kaldırdıktan sonra Hello parmak izi değerini kopyalayın.  Değişiklik hello `String` tooa uygun güvenli parola tooprotect ve PowerShell içinde aşağıdaki çalışma başlangıç değeri:

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

toosee hello hello üzerinde yüklü bir sertifika ayrıntılarını makine hello aşağıdaki PowerShell komutunu çalıştırabilirsiniz:

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

Alternatif olarak, bir Azure aboneliğiniz varsa, hello bölümü izleyin [sertifikaları tooKey kasası eklemek](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).

## <a name="install-hello-certificates"></a>Merhaba sertifikaları yükleyin
Sertifikaları olduktan sonra bunları hello küme düğümlerinde yükleyebilirsiniz. Düğümleriniz toohave gereken en son Windows PowerShell hello 3.x yüklü. Küme ve sunucu sertifikaları ve tüm ikincil sertifikaları için her bir düğümde aşağıdaki adımları toorepeat ihtiyacınız olacaktır.

1. Merhaba .pfx dosyaları toohello düğümü kopyalayın.
2. Bir yönetici olarak bir PowerShell penceresi açın ve aşağıdaki komutları hello girin. Hello yerine *$pswd* Bu sertifika toocreate kullanılan hello parolayla. Hello yerine *$PfxFilePath* hello .pfx kopyalanan toothis düğümünün hello tam yoluna sahip.
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. Şimdi hello Network Service hesabı altında çalışır, hello Service Fabric işlem, komut dosyası izleyen hello çalıştırarak kullanabilmesi için bu sertifikayı hello erişim denetimini ayarlayın. Merhaba sertifika ve hello hizmet hesabı için "NETWORK SERVICE" Merhaba parmak izi sağlayın. Bu ' % s'hello ACL'ler hello sertifikanın doğru hello sertifikada açarak denetleyebilirsiniz *Başlat* > *bilgisayar sertifikalarını yönetmek* ve bakarak *tüm görevler*  >  *Özel anahtarları Yönet*.
   
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
   
    # Specify hello user, hello permissions and hello permission type
    $permission = "$($serviceAccount)","FullControl","Allow"
    $accessRule = New-Object -TypeName System.Security.AccessControl.FileSystemAccessRule -ArgumentList $permission
   
    # Location of hello machine related keys
    $keyPath = Join-Path -Path $env:ProgramData -ChildPath "\Microsoft\Crypto\RSA\MachineKeys"
    $keyName = $cert.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
    $keyFullPath = Join-Path -Path $keyPath -ChildPath $keyName
   
    # Get hello current acl of hello private key
    $acl = (Get-Item $keyFullPath).GetAccessControl('Access')
   
    # Add hello new ace toohello acl of hello private key
    $acl.SetAccessRule($accessRule)
   
    # Write back hello new acl
    Set-Acl -Path $keyFullPath -AclObject $acl -ErrorAction Stop
   
    # Observe hello access rights currently assigned toothis certificate.
    get-acl $keyFullPath| fl
    ```
4. Her sunucu sertifikası için yukarıdaki Hello adımları yineleyin. Tooallow erişim toohello küme istediğiniz bu adımları tooinstall hello istemci sertifikalarını hello makinelerde de kullanabilirsiniz.

## <a name="create-hello-secure-cluster"></a>Merhaba güvenli küme oluşturma
Merhaba yapılandırdıktan sonra **güvenlik** hello bölümünü **ClusterConfig.X509.MultiMachine.json** dosyası devam çok[kümenizi oluşturduktan](service-fabric-cluster-creation-for-windows-server.md#createcluster) bölüm tooconfigure düğümleri hello ve hello tek başına bir küme oluşturun. Toouse hello unutmayın **ClusterConfig.X509.MultiMachine.json** hello küme oluşturma sırasında dosya. Örneğin, komutunuzu hello şuna benzeyebilir:

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

Merhaba güvenli olduktan sonra tek başına Windows başarıyla çalışan küme ve kimliği doğrulanmış istemciler tooconnect tooit Merhaba, hello bölümü izleyin kurulumun [Bağlan tooa güvenli küme PowerShell kullanarak](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit. Örneğin:

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

Bu gibi durumlarda, diğer PowerShell komutları toowork sonra Bu kümeyle çalıştırabilirsiniz. Örneğin, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow bu güvenli küme düğümlerinde listesi.


tooremove hello küme hello Service Fabric paketi indirdiğiniz hello kümesinde toohello düğümüne bağlanmak, bir komut satırı açın ve toohello paket klasörüne gidin. Şimdi hello aşağıdaki komutu çalıştırın:

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> Yanlış sertifika yapılandırması hello Küme dağıtımı sırasında yaklaşan engellemek. tooself-güvenlik sorunları tanılamak, lütfen Olay Görüntüleyicisi'ni grubunda bakın *uygulama ve hizmet günlükleri* > *Microsoft Service Fabric*.
> 
> 

