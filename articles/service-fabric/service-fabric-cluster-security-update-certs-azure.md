---
title: "Azure Service Fabric kümesi aaaManage sertifikaları | Microsoft Docs"
description: "Service Fabric kümesinden tooor tooadd yeni sertifikalar, geçiş sertifikası ve Kaldır nasıl sertifika açıklar."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 91adc3d3-a4ca-46cf-ac5f-368fb6458d74
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: chackdan
ms.openlocfilehash: 8e57bd95dbb800ecc04cf6988047e3abdc2fe56a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a>Ekleme veya Azure Service Fabric kümesi için sertifikaları kaldırın
Service Fabric'ın X.509 sertifikaları nasıl kullandığı tanımak ve hello ile ilgili bilgi sahibi olmanız önerilir [küme güvenlik senaryoları](service-fabric-cluster-security.md). Anlamanız gerekir hangi küme sertifika ve devam etmeden önce ne için kullanılır.

Yapılandırdığınızda sertifikalar, birincil ve ikincil bir iki küme belirtmenizi Service fabric sağlar, ayrıca tooclient sertifikalarda küme oluşturma sırasında güvenlik sertifika. Çok başvuran[Portalı aracılığıyla azure bir küme oluşturma](service-fabric-cluster-creation-via-portal.md) veya [Azure Resource Manager aracılığıyla azure bir küme oluşturma](service-fabric-cluster-creation-via-arm.md) oluşturma süresi sırasında ayarlama ile ilgili ayrıntılar için. Yalnızca bir küme sertifika belirtirseniz, zaman oluşturabilir, ardından, hello birincil sertifikası olarak kullanılır. Küme oluşturulduktan sonra ikincil olarak yeni bir sertifika ekleyebilirsiniz.

> [!NOTE]
> Güvenli bir küme için her zaman en az bir geçerli (değil iptal edilmiş ve süresi dolan değil) küme sertifika'ni (birincil veya ikincil) dağıtılan gerekir (değilse, hello küme çalışmamaya başlar). süre sonu, tüm geçerli sertifikaların düşmeden önce 90 gün hello sistem, bir uyarı izleme ve ayrıca bir uyarı sistem durumu olayı hello düğümde oluşturur. Şu anda hiçbir e-posta veya var. Bu konuyla ilgili service fabric gönderir herhangi bir bildirim 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-hello-portal"></a>Merhaba portalı kullanarak bir ikincil küme sertifika Ekle

İkincil küme sertifika hello Azure portal eklenemez. Sahip olduğunuz toouse Azure powershell söz konusu. Merhaba işlemi, bu belgenin sonraki bölümlerinde gösterilmiştir.

## <a name="swap-hello-cluster-certificates-using-hello-portal"></a>Merhaba küme sertifikaları Hello portal kullanarak değiştirme

Birincil ve ikincil tooswap hello istiyorsanız bir ikincil küme sertifika başarıyla dağıttıktan sonra toohello güvenlik dikey gidin ve hello bağlam menüsü tooswap hello ikincil sertifikayla hello 'Birincil ile değiştirme' seçeneği seçin Merhaba birincil sertifika.

![Sertifika değiştirme][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-hello-portal"></a>Merhaba portalı kullanarak bir küme sertifikayı Kaldır

Güvenli bir küme için (dağıtılan en az bir geçerli değil iptal edilmiş ve süresi dolan değil) sertifika (birincil veya ikincil) her zaman gerekir aksi durumda, hello küme çalışmayı durdurur.

tooremove küme güvenlik, Bul toohello güvenlik dikey ve select hello 'Delete' seçeneği hello bağlam menüsünden hello ikincil sertifika kullanılmasını ikincil bir sertifika.

Maksadınızı tooswap gerekir, birincil olarak işaretlenmiş tooremove hello sertifika ise ile ilk ikincil hello ve hello ikincil hello yükseltme tamamlandıktan sonra silin.

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a>Resource Manager Powershell kullanarak bir ikincil sertifika Ekle

Bu adımları, Kaynak Yöneticisi'ni nasıl çalıştığını iyi ve en az bir Resource Manager şablonu kullanarak bir Service Fabric kümesi dağıttıysanız ve hello kümesi kullanışlı tooset kullanılan hello şablonuna sahip varsayalım. JSON kullanarak rahat olduğu da varsayılır.

> [!NOTE]
> Örnek bir şablon ve toofollow boyunca veya bir başlangıç noktası olarak kullanabileceğiniz parametreler arıyorsanız sonra buradan indirin [git deposuna](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample). 
> 
> 

### <a name="edit-your-resource-manager-template"></a>Kaynak Yöneticisi şablonunuzu düzenleyin

Aşağıdaki boyunca kolaylığı için örnek 5-VM-1-NodeTypes-Secure_Step2.JSON biz yapmadan tüm hello düzenlemeleri içerir. Merhaba örnek şu adreste [git deposuna](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).

**Tüm hello adımları toofollow emin olun**

**1. adım:** , küme toodeploy kullanılan hello Resource Manager şablonu açın. (Merhaba örnek deposuna yukarıda hello yüklediyseniz 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy güvenli bir küme kullanın ve bu şablonu açın).

**2. adım:** Ekle **iki yeni parametreler** "secCertificateThumbprint" ve "secCertificateUrlValue" türü "dize" toohello parametresi bölümü. Aşağıdaki kod parçacığını hello kopyalayın ve toohello şablonu ekleyin. Bağlı olarak Hello kaynak şablonunuzun zaten bu tanımlanan sahip, bu durumda toohello sonraki adım taşıma. 
 
```JSON
   "secCertificateThumbprint": {
      "type": "string",
      "metadata": {
        "description": "Certificate Thumbprint"
      }
    },
    "secCertificateUrlValue": {
      "type": "string",
      "metadata": {
        "description": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

**3. adım:** toohello değişiklik yapma **Microsoft.ServiceFabric/clusters** kaynak - şablonunuzda hello "Microsoft.ServiceFabric/clusters" kaynak tanımı bulun. Bu tanım özellikleri altında "Sertifika" JSON bulacaksınız hello JSON parçacığı aşağıdaki gibi görünmelidir etiketi:

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

Yeni bir etiket "thumbprintSecondary" ekleyin ve "[parameters('secCertificateThumbprint')]" bir değer verin.  

Merhaba kaynak tanımı hello aşağıdaki gibi görünmelidir artık bunu (kaynağınız hello şablonu bağlı olarak, tam olarak hello gibi aşağıdaki parçacığı olmayabilir). 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

Çok istiyorsanız**rollover hello cert**, ikincil olarak birincil ve taşıma hello geçerli birincil olarak hello yeni sertifika belirtin. Bu, geçerli birincil sertifika toohello yeni sertifikanızı tek bir dağıtım adımda hello geçişi sonuçlanır.

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


**4. adım:** değişiklik yapma çok**tüm** hello **Microsoft.Compute/virtualMachineScaleSets** kaynak tanımları - hello Microsoft.Compute/virtualMachineScaleSets kaynak bulun tanımı. Kaydırma toohello "publisher": "Microsoft.Azure.ServiceFabric" altında "virtualMachineProfile".

Merhaba service fabric yayımcı ayarlarında, şöyle bir şey görmeniz gerekir.

![Json_Pub_Setting1][Json_Pub_Setting1]

Merhaba yeni sertifika girişleri tooit Ekle

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

Merhaba özellikleri artık aşağıdaki gibi görünmelidir

![Json_Pub_Setting2][Json_Pub_Setting2]

Çok istiyorsanız**rollover hello cert**, ikincil olarak birincil ve taşıma hello geçerli birincil olarak hello yeni sertifika belirtin. Bu, geçerli sertifika toohello yeni sertifikanızı tek bir dağıtım adımda hello geçişi sonuçlanır. 


```JSON
               "certificate": {
                   "thumbprint": "[parameters('secCertificateThumbprint')]",
                   "x509StoreName": "[parameters('certificateStoreValue')]"
                     },
               "certificateSecondary": {
                    "thumbprint": "[parameters('certificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```
Merhaba özellikleri artık aşağıdaki gibi görünmelidir

![Json_Pub_Setting3][Json_Pub_Setting3]


**5. adım:** çok değişiklik**tüm** hello **Microsoft.Compute/virtualMachineScaleSets** kaynak tanımları - hello Microsoft.Compute/virtualMachineScaleSets kaynak bulun tanımı. Toohello "vaultCertificates" kaydırma:, "OSProfile" altında. Bu gibi görünmelidir.


![Json_Pub_Setting4][Json_Pub_Setting4]

Merhaba secCertificateUrlValue tooit ekleyin. Aşağıdaki kod parçacığında hello kullan:

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
Json kaynaklanan hello aşağıdakine benzer görünmelidir.
![Json_Pub_Setting5][Json_Pub_Setting5]


> [!NOTE]
> 4 ve 5 tüm hello Nodetypes/Microsoft.Compute/virtualMachineScaleSets kaynak tanımlarında şablonunuzda yinelenen olduğundan emin olun. Bunlardan birini kaçırılması durumunda hello sertifika üzerinde bu VMSS yüklenmemiş ve (, bu hello küme güvenlik için kullanabilirsiniz. geçerli sertifika şunun; giderek hello küme de dahil olmak üzere kümenizdeki öngörülemeyen sonuçlara gerekir Bu nedenle çift, devam etmeden önce lütfen denetleyin.
> 
> 


### <a name="edit-your-template-file-tooreflect-hello-new-parameters-you-added-above"></a>Yukarıda eklediğiniz şablon dosyası tooreflect hello yeni parametrelerinizi Düzenle
Merhaba hello örnekten kullanıyorsanız [git deposuna](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow bunların, hello örnek 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON içinde toomake değişiklikleri başlatabilirsiniz. 

Resource Manager şablonu parametreniz dosya düzenleme, hello iki yeni parametrelerini secCertificateThumbprint ve secCertificateUrlValue ekleyin. 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-hello-template-tooazure"></a>Merhaba şablonu tooAzure dağıtma

- Artık hazır toodeploy şablonu tooAzure şunlardır. Bir Azure PS sürüm 1 + komut istemi açın.
- Tooyour Azure hesabı oturum ve hello belirli azure aboneliğini seçin. Bu, bir azure aboneliği daha erişim toomore sahip çok kişi için önemli bir adımdır.

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

Test hello şablon önceki toodeploying onu. Kullanım hello kümenizi halen dağıtılmış durumda aynı kaynak grubu.

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

Merhaba şablonu tooyour kaynak grubuna dağıtın. Kullanım hello kümenizi halen dağıtılmış durumda aynı kaynak grubu. Merhaba New-AzureRmResourceGroupDeployment komutunu çalıştırın. Merhaba varsayılan değer olduğundan toospecify hello modu gerekmez **artımlı**.

> [!NOTE]
> Mod tooComplete ayarlarsanız, şablonunuzda olmayan kaynakları yanlışlıkla silebilirsiniz. Bu nedenle bu senaryoda kullanmayın.
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

Örneği burada verilmiştir bir doldurulmuş hello aynı powershell.

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

Merhaba dağıtım tamamlandıktan sonra küme tooyour kullanarak bağlanan yeni bir sertifika hello ve bazı sorgular gerçekleştirebilir. Mümkün toodo varsa. Ardından hello eski sertifika silebilirsiniz. 

Kendinden imzalı bir sertifika kullanıyorsanız, tooimport unutmayın, yerel TrustedPeople sertifika deposuna bunları.

```powershell
######## Set up hello certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
Hızlı başvuru için hello komutu tooconnect tooa güvenli küme İşte 

```powershell
$ClusterName= "chackosecure5.westus.cloudapp.azure.com:19000"
$CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7SD1D630F8F3" 

Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
    -X509Credential `
    -ServerCertThumbprint $CertThumbprint  `
    -FindType FindByThumbprint `
    -FindValue $CertThumbprint `
    -StoreLocation CurrentUser `
    -StoreName My
```
Hızlı başvuru için işte hello komutu tooget küme durumu

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-toohello-cluster"></a>Uygulama sertifikaları toohello kümesini dağıtma.

Adım 5'te bir keyvault toohello düğümleri dağıtılan toohave hello sertifikalarının yukarıda özetlendiği gibi aynı adımları hello kullanabilirsiniz. yalnızca tanımlanır ve farklı parametrelerini kullanın.


## <a name="adding-or-removing-client-certificates"></a>Ekleme veya istemci sertifikaları kaldırma

Toplama toohello küme sertifikalarda istemci sertifikaları tooperform yönetim işlemlerini service fabric kümesi ekleyebilirsiniz.

İstemci sertifikalarını - yönetici iki tür ekleyebilirsiniz veya salt okunur. Bunlar ardından kullanılan toocontrol erişim toohello yönetici işlemleri ve sorgu işlemleri hello kümede olabilir. Varsayılan olarak, hello küme sertifikaları toohello izin verilen yönetici sertifikalar listesine eklenir.

istemci sertifikalarını herhangi bir sayıda belirtebilirsiniz. Bir yapılandırma güncelleştirme toohello service fabric kümesi her eklendiği/silindiği sonuçları


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a>İstemci sertifikalarını - yönetici ekleme veya salt okunur Portalı aracılığıyla

1. Toohello güvenlik dikey gidin ve seçin hello '+ kimlik doğrulama' hello güvenlik dikey üstünde düğmesi.
2. Merhaba 'Kimlik doğrulama türü' - 'Salt okunur istemci' veya 'Yönetici istemci' Hello 'Kimlik doğrulama Ekle' dikey penceresinde, seçin
3. Şimdi hello yetkilendirme yöntemi seçin. Bu, bu sertifikayı hello konu adı veya hello parmak izini kullanarak görünmelidir olup olmadığını tooService doku gösterir. Genel olarak, bu konu adı iyi güvenlik uygulaması toouse hello yetkilendirme yöntemi değil. 

![İstemci sertifikası ekleme][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-hello-portal"></a>İstemci sertifikalarını - yönetici veya salt okunur kullanarak silinmesini hello portalı

tooremove küme güvenlik, Bul toohello güvenlik dikey ve select hello 'Delete' seçeneği hello bağlam menüsünden hello belirli sertifika kullanılmasını ikincil bir sertifika.



## <a name="next-steps"></a>Sonraki adımlar
Küme yönetimi hakkında daha fazla bilgi için bu makaleler okuyun:

* [Service Fabric kümesi yükseltme işlemi ve sizden beklentileri](service-fabric-cluster-upgrade.md)
* [İstemciler için rol tabanlı erişim Kurulumu](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


