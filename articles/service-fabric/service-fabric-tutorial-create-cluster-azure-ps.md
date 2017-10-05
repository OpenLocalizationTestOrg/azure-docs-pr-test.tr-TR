---
title: "Service Fabric kümesi oluşturma | Microsoft Docs"
description: "PowerShell kullanarak Azure'da bir Windows veya Linux Service Fabric kümesi oluşturmayı öğrenin."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi
ms.openlocfilehash: f62249417552b9cf840bfac3b94c27f63bd7064e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a>PowerShell kullanarak Azure'da güvenli küme oluşturma
Bu öğretici bir Service Fabric kümesi (Windows veya Linux) oluşturmak gösterilmiştir Azure'da çalışan. İşlemi tamamladığınızda, uygulamaları dağıtabileceğiniz bulutta çalıştıran bir kümeye sahip.

Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:

> [!div class="checklist"]
> * PowerShell kullanarak Azure'da güvenli bir Service Fabric kümesi oluştur
> * Küme bir X.509 sertifikası ile güvenli
> * PowerShell kullanarak kümeye bağlanma
> * Bir küme Kaldır

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce:
- Bir Azure aboneliğiniz yoksa, oluşturma bir [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- Yükleme [Service Fabric SDK ve PowerShell Modülü](service-fabric-get-started.md)
- Yükleme [Azure Powershell modülü sürümü 4.1 veya üzeri](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)

Aşağıdaki yordam (tek sanal makine) tek bir düğüm Önizleme Service Fabric kümesi oluşturur. Küme yanı sıra küme oluşturulan ve bir anahtar kasası yerleştirilen otomatik olarak imzalanan bir sertifika tarafından korunmaktadır. Tek düğümlü küme bir sanal makine genişletilemez ve önizleme kümeleri için daha yeni sürümleri yükseltilemez.

Service Fabric kümesi Azure kullanımda çalıştırarak ücrete maliyeti hesaplamak için [Azure fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/).
Service Fabric kümeleri oluşturma hakkında daha fazla bilgi için bkz: [Azure Kaynak Yöneticisi'ni kullanarak bir Service Fabric kümesi oluştur](service-fabric-cluster-creation-via-arm.md).

## <a name="create-the-cluster-using-azure-powershell"></a>Azure PowerShell kullanarak küme oluşturma
1. Azure Resource Manager şablonu ve parametre dosyanın yerel bir kopyasını indirin [Service Fabric için Azure Resource Manager şablonu](https://aka.ms/securepreviewonelineclustertemplate) GitHub depo.  *azuredeploy.JSON* Service Fabric kümesi tanımlayan Azure Resource Manager şablonudur. *azuredeploy.Parameters.JSON* , Küme dağıtımı özelleştirmek bir parametre dosyası.

2. Aşağıdaki parametreleri özelleştirmek *azuredeploy.parameters.json* parametreler dosyası:

   | Parametre       | Açıklama | Önerilen Değer |
   | --------------- | ----------- | --------------- |
   | clusterLocation | Küme dağıtılacağı Azure bölgesi. | *Örneğin, westeurope, eastasia, eastus* |
   | clusterName     | Oluşturmak istediğiniz küme adıdır. | *Örneğin, bobs sfpreviewcluster* |
   | adminUserName   | Küme sanal makinelerde yerel yönetici hesabı. | *Herhangi bir geçerli Windows Server kullanıcı adı* |
   | Admınpassword   | Küme sanal makinelerde yerel yönetici hesabının parolası. | *Geçerli bir Windows Server parola* |
   | clusterCodeVersion | Çalıştırmak üzere Service Fabric sürümü. (255.255.X.255 Önizleme sürümleri). | **255.255.5718.255** |
   | vmInstanceCount | (1 ya da 3-99 olabilir), kümedeki sanal makine sayısı. | **1** | *Önizleme küme için yalnızca bir sanal makine belirtin* |

3. Azure, oturum açma bir PowerShell konsolu açın ve kümede dağıtmak istediğiniz aboneliği seçin:

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. Oluşturma ve Service Fabric tarafından kullanılmak üzere sertifika için bir parola şifreleyebilirsiniz.

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. Küme ve sertifikasını aşağıdaki komutu çalıştırarak oluşturun:

   ```powershell
      New-AzureRmServiceFabricCluster
          -TemplateFile C:\Users\me\Desktop\azuredeploy.json `
          -ParameterFile C:\Users\me\Desktop\azuredeploy.parameters.json `
          -CertificateOutputFolder C:\Users\me\Desktop\ `
          -CertificatePassword $pwd `
          -CertificateSubjectName "mycluster.westeurope.cloudapp.azure.com" `
          -ResourceGroupName myclusterRG
   ```

   >[!NOTE]
   >`-CertificateSubjectName` Parametre Hizala gibi seçtiğiniz bir Azure bölgesine bağlı etki alanının yanı sıra Parametreler dosyasında belirtilen clusterName parametresi: `clustername.eastus.cloudapp.azure.com`.

Yapılandırma tamamlandıktan sonra Azure içinde oluşturulan küme bilgilerini çıkarır. Ayrıca bu parametre için belirtilen yol - CertificateOutputFolder dizinine küme sertifika kopyalar. Service Fabric Explorer erişmek ve kümenizi durumunu görüntülemek için bu sertifika gerekir.

Aşağıdaki URL'ye benzer kümenizi URL'sini not edin: *https://mycluster.westeurope.cloudapp.azure.com:19080*

## <a name="modify-the-certificate--access-service-fabric-explorer"></a>Service Fabric Explorer erişim & sertifika Değiştir ##

1. Sertifika Alma Sihirbazı'nı açmak için sertifikayı çift tıklatın.

2. Varsayılan ayarları kullanır, ancak denetlediğinizden emin olun **bu anahtarı verilebilir olarak işaretle.** onay kutusunu içinde **özel anahtar korumasını** adım. Azure kapsayıcı kayıt defteri için daha sonra Bu öğreticide Service Fabric kümesi kimlik doğrulamasını yapılandırırken sertifika vermek Visual Studio gerekir.

3. Bu gibi durumlarda, Service Fabric Explorer şimdi bir tarayıcıda açabilirsiniz. Bunu yapmak için gidin **ManagementEndpoint** bir web tarayıcısı kullanarak kümenizi URL'sini ve makinenizde kaydedilen sertifikayı seçin.

>[!NOTE]
>Kendinden imzalı bir sertifika kullanıyor gibi Service Fabric Explorer açarken bir sertifika hatası bakın. Kenar içinde tıklattığınızdan sahip *ayrıntıları* ve ardından *Web sayfasına gidin* bağlantı. Chrome'tıklatmak zorunda *Gelişmiş* ve ardından *devam* bağlantı.

>[!NOTE]
>Küme oluşturma başarısız olursa, her zaman zaten dağıtılmış kaynaklar güncelleştirmeleri komutu çalıştırabilirsiniz. Bir sertifika başarısız dağıtımının bir parçası oluşturulmuş olsa bile, yeni bir tane oluşturulur. Küme oluşturma sorunlarını gidermek için bkz: [Azure Kaynak Yöneticisi'ni kullanarak bir Service Fabric kümesi oluştur](service-fabric-cluster-creation-via-arm.md).

## <a name="connect-to-the-secure-cluster"></a>Güvenli kümeye bağlanın
Service Fabric SDK ile birlikte yüklenen Service Fabric PowerShell modülünü kullanarak kümeye bağlanın.  İlk olarak, geçerli kullanıcının, bilgisayarınızdaki kişisel (My) deposuna sertifikası yükleyin.  Aşağıdaki PowerShell komutunu çalıştırın:

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

Şimdi güvenli kümenize bağlanmaya hazırsınız.

**Service Fabric** PowerShell Modülü Service Fabric kümeleri, uygulamaları ve hizmetleri yönetmek için birçok cmdlet'leri sağlar.  Kullanım [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet'ini güvenli kümeye bağlanın. Sertifika parmak izi ve bağlantı uç nokta ayrıntılarını önceki adımdaki çıktı bulunur.

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

Bağlı ve küme sağlıklı olduğundan emin olun kullanarak [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet'i.

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a>Kaynakları temizleme

Küme, küme kaynağının yanı sıra diğer Azure kaynaklarından oluşur. Kümeyi ve kullandığı tüm kaynakları silmenin en basit yolu, kaynak grubunun silinmesidir.

Azure'da oturum açma ve küme kaldırmak istediğiniz abonelik kimliği seçin.  Abonelik Kimliğiniz için oturum açarak bulabileceğiniz [Azure portal](http://portal.azure.com). Kaynak grubu ve kullanarak tüm küme kaynakları silmek [Remove-AzureRMResourceGroup cmdlet'i](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:

> [!div class="checklist"]
> * Service Fabric kümesi oluşturma
> * Küme bir X.509 sertifikası ile güvenli
> * PowerShell kullanarak kümeye bağlanma
> * Bir küme Kaldır

Ardından, var olan bir uygulama dağıtma hakkında bilgi edinmek için aşağıdaki öğreticiyi ilerleyin.
> [!div class="nextstepaction"]
> [Varolan bir .NET uygulama Docker Compose ile dağıtma](service-fabric-host-app-in-a-container.md)
