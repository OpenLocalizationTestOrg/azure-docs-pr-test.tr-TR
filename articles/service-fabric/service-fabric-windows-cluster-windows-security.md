---
title: "Windows güvenliği kullanarak Windows üzerinde çalışan küme a aaaSecure | Microsoft Docs"
description: "Tek başına bir tooconfigure düğümü düğümü ve istemci düğüm güvenlik nasıl küme Windows güvenliği kullanarak Windows üzerinde çalışan öğrenin."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ce3bf686-ffc4-452f-b15a-3c812aa9e672
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: 44f3011eb630357f342052a48d6c852b17dccec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a>Windows tek başına bir kümede Windows güvenliği kullanarak güvenli hale getirme
erişim tooa Service Fabric kümesi tooprevent yetkisiz, hello küme güvenlik altına almanız gerekir. Merhaba küme üretim iş yükleri çalıştığında güvenlik özellikle önemlidir. Bu makalede nasıl hello Windows güvenliği kullanarak tooconfigure düğümü düğümü ve istemci düğüm güvenlik *ClusterConfig.JSON* dosya.  Merhaba işleme toohello karşılık gelen güvenlik adımında yapılandırma [Windows üzerinde çalışan tek başına küme oluşturmak](service-fabric-cluster-creation-for-windows-server.md). Service Fabric Windows güvenliği nasıl kullandığı hakkında daha fazla bilgi için bkz: [küme güvenlik senaryoları](service-fabric-cluster-security.md).

> [!NOTE]
> Bir güvenlik seçim tooanother'den hiçbir Küme yükseltme olduğundan hello seçimi düğümü düğümü güvenlik dikkatle düşünmelisiniz. toochange hello güvenlik seçimi toorebuild hello tam küme sahip.
>
>

## <a name="configure-windows-security-using-gmsa"></a>GMSA kullanarak Windows güvenliği yapılandırma  
Merhaba örnek *ClusterConfig.gMSA.Windows.MultiMachine.JSON* yapılandırma dosyasını karşıdan ile Merhaba [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. zip](http://go.microsoft.com/fwlink/?LinkId=730690) tek başına küme paketi içeren Windows güvenliği kullanarak yapılandırmak için bir şablon [Grup yönetilen hizmet hesabı (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):  

```  
"security": {  
            "WindowsIdentities": {  
                "ClustergMSAIdentity": "accountname@fqdn"  
                "ClusterSPN": "fqdn"  
                "ClientIdentities": [  
                    {  
                        "Identity": "domain\\username",  
                        "IsAdmin": true  
                    }  
                ]  
            }  
        }  
```  
  
| **Yapılandırma ayarı** | **Açıklama** |  
| --- | --- |  
| WindowsIdentities |Merhaba küme ve istemci kimliklerini içerir. |  
| ClustergMSAIdentity |Düğümü düğümü güvenliğini yapılandırır. Bir grup yönetilen hizmet hesabı. |  
| ClusterSPN |GMSA hesabının tam olarak nitelenmiş etki alanı SPN|  
| ClientIdentities |İstemcisi düğümü güvenliğini yapılandırır. İstemci kullanıcı hesapları dizisi. |  
| Kimlik |Merhaba istemci kimliği, bir etki alanı kullanıcısı. |  
| IsAdmin |TRUE, hello etki alanı kullanıcısı yönetici istemci erişimi, kullanıcı istemci erişimi için false belirtir. |  
  
[Düğüm toonode güvenlik](service-fabric-cluster-security.md#node-to-node-security) ayarlayarak yapılandırılmış **ClustergMSAIdentity** toorun gMSA altında service fabric gerektiği zaman. Sipariş toobuild güven ilişkilerini düğümler arasında bunlar birbirinden haberdar olmanız gerekir. Bu iki farklı yolla gerçekleştirilebilir: hello hello kümedeki tüm düğümleri içeren Grup yönetilen hizmet hesabı veya hello kümedeki tüm düğümleri içerir hello etki alanı makine grubu belirtin. Hello kullanarak önerilir [Grup yönetilen hizmet hesabı (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) yaklaşım, özellikle büyük kümeler (10'dan fazla düğüm) veya büyük olasılıkla toogrow ya da küçültmek kümeleri.  
Bu yaklaşım, kendisi için küme yöneticileri erişim hakları tooadd verilmiş ve üye kaldırma bir etki alanı grubu hello oluşturulmasını gerektirmez. Bu hesaplar, otomatik parola yönetimi için de yararlıdır. Daha fazla bilgi için bkz: [Grup yönetilen hizmet hesapları ile çalışmaya başlama](http://technet.microsoft.com/library/jj128431.aspx).  
 
[İstemci toonode güvenlik](service-fabric-cluster-security.md#client-to-node-security) kullanılarak yapılandırılmış **ClientIdentities**. Bir istemci ve hello kümesi arasında sipariş tooestablish güven içinde güven hangi istemci kimlikleri hello küme tooknow yapılandırmanız gerekir. Bu iki farklı şekillerde yapılabilir: bağlanmak veya belirtmek hello etki alanı grubu kullanıcıları hello bağlanabilmesi için etki alanı düğümü kullanıcıları belirtin. Service Fabric bağlı tooa Service Fabric kümesi istemciler için iki farklı erişim denetim türlerini destekler: Yönetici ve kullanıcı. Erişim denetimi Küme Yöneticisi toolimit erişim toocertain türü küme işlemleri farklı hello küme daha güvenli hale getirme kullanıcı grupları için hello hello yeteneği sağlar.  Yöneticiler tam erişim toomanagement özellikleri (okuma/yazma özellikleri dahil) sahiptir. Kullanıcıların varsayılan olarak, yalnızca okuma erişimi toomanagement özellikleri (örneğin, sorgu özellikleri) ve hello özelliği tooresolve uygulamaları ve hizmetleri vardır. Erişim denetimleri hakkında daha fazla bilgi için bkz: [Service Fabric istemciler için rol tabanlı erişim denetimi](service-fabric-cluster-security-roles.md).  
 
Örnek Hello **güvenlik** bölüm Windows güvenliği kullanarak gMSA yapılandırır ve bu hello makineleri belirtir *ServiceFabric.clusterA.contoso.com* gMSA hello küme ve, parçası olan *CONTOSO\usera* yönetici istemci erişimi vardır:  
  
```  
"security": {  
    "WindowsIdentities": {  
        "ClustergMSAIdentity" : "ServiceFabric.clusterA.contoso.com",  
        "ClusterSPN" : "clusterA.contoso.com",  
        "ClientIdentities": [{  
            "Identity": "CONTOSO\\usera",  
            "IsAdmin": true  
        }]  
    }  
}  
```  
  
## <a name="configure-windows-security-using-a-machine-group"></a>Makine grubu kullanarak Windows güvenliği yapılandırma  
Merhaba örnek *ClusterConfig.Windows.MultiMachine.JSON* yapılandırma dosyasını karşıdan ile Merhaba [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. zip](http://go.microsoft.com/fwlink/?LinkId=730690) tek başına küme paketi, Windows güvenliği yapılandırmak için bir şablonu içerir.  Windows güvenliği hello yapılandırılmış **özellikleri** bölümü: 

```
"security": {
            "ClusterCredentialType": "Windows",
            "ServerCredentialType": "Windows",
            "WindowsIdentities": {
                "ClusterIdentity" : "[domain\machinegroup]",
                "ClientIdentities": [{
                    "Identity": "[domain\username]",
                    "IsAdmin": true
                }]
            }
        }
```

| **Yapılandırma ayarı** | **Açıklama** |
| --- | --- |
| ClusterCredentialType |**ClusterCredentialType** çok ayarlanır*Windows* ClusterIdentity bir Active Directory makine grubu adını belirtir. |  
| ServerCredentialType |Çok ayarlamak*Windows* tooenable istemciler için Windows Güvenlik.<br /><br />Bu, hello istemcileri hello küme hello kümenin kendisi ve bir Active Directory etki alanı içinde çalıştığını gösterir. |  
| WindowsIdentities |Merhaba küme ve istemci kimliklerini içerir. |  
| ClusterIdentity |Makine grubu adı, domain\machinegroup, tooconfigure düğümü düğümü güvenlik kullanın. |  
| ClientIdentities |İstemcisi düğümü güvenliğini yapılandırır. İstemci kullanıcı hesapları dizisi. |  
| Kimlik |Merhaba etki alanı kullanıcısı, hello istemci kimliği için etki alanı\kullanıcı adı ekleyin. |  
| IsAdmin |Etki alanı kullanıcısı hello kümesi tootrue toospecify yönetici istemci erişimi ya da kullanıcı istemci erişimi için yanlış sahiptir. |  

[Düğüm toonode güvenlik](service-fabric-cluster-security.md#node-to-node-security) ayarı kullanılarak yapılandırılır **ClusterIdentity** toouse bir Active Directory etki alanı içindeki bir makine grubun istiyorsanız. Daha fazla bilgi için bkz: [Active Directory'de bir makine grubu oluştur](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).

[İstemcisi düğümü güvenlik](service-fabric-cluster-security.md#client-to-node-security) kullanılarak yapılandırılan **ClientIdentities**. tooestablish güven bir istemci ve hello kümesi arasında küme hello kimlikleri güvenebileceği hello küme tooknow hello istemci yapılandırmanız gerekir. İki farklı yolla güven kurabilir:

- Bağlanabilir hello etki alanı grubu kullanıcıları belirtin.
- Bağlanabilir hello etki alanı düğümü kullanıcıları belirtin.

Service Fabric bağlı tooa Service Fabric kümesi istemciler için iki farklı erişim denetim türlerini destekler: Yönetici ve kullanıcı. Erişim denetimi, hangi hello küme daha güvenli hale getirir hello küme yönetici toolimit erişim toocertain türleri için farklı kullanıcı grupları, küme işlemlerinin sağlar.  Yöneticiler tam erişim toomanagement özellikleri (okuma/yazma özellikleri dahil) sahiptir. Kullanıcıların varsayılan olarak, yalnızca okuma erişimi toomanagement özellikleri (örneğin, sorgu özellikleri) ve hello özelliği tooresolve uygulamaları ve hizmetleri vardır.  

Örnek Hello **güvenlik** bölüm Windows güvenliği yapılandırır, o hello makineleri belirtir *ServiceFabric/clusterA.contoso.com* hello kümesinin parçası olan ve bu belirtir *CONTOSO\usera* yönetici istemci erişimi vardır:

```
"security": {
    "ClusterCredentialType": "Windows",
    "ServerCredentialType": "Windows",
    "WindowsIdentities": {
        "ClusterIdentity" : "ServiceFabric/clusterA.contoso.com",
        "ClientIdentities": [{
            "Identity": "CONTOSO\\usera",
            "IsAdmin": true
        }]
    }
},
```

> [!NOTE]
> Service Fabric bir etki alanı denetleyicisinde dağıtılmalıdır değil. ClusterConfig.json başlangıç IP adresi hello etki alanı denetleyicisinin makine grubu kullanırken içermez ve Grup yönetilen hizmet hesabı (gMSA) olduğundan emin olun.
>
>

## <a name="next-steps"></a>Sonraki adımlar
Windows güvenliği hello yapılandırdıktan sonra *ClusterConfig.JSON* dosya, hello küme oluşturma işlemine devam [Windows üzerinde çalışan tek başına küme oluşturmak](service-fabric-cluster-creation-for-windows-server.md).

Düğümü düğümü nasıl güvenlik, istemci düğümü güvenlik ve rol tabanlı erişim denetimi, bkz: hakkında daha fazla bilgi için [küme güvenlik senaryoları](service-fabric-cluster-security.md).

Bkz: [Bağlan tooa güvenli küme](service-fabric-connect-to-secure-cluster.md) PowerShell veya FabricClient kullanarak bağlanma örnekler.
