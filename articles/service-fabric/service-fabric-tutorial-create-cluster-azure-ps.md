---
title: "aaaCreate Service Fabric küme Azure'da | Microsoft Docs"
description: "Nasıl toocreate bir Windows veya Linux Service Fabric kümesi Azure PowerShell'i kullanma hakkında bilgi edinin."
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
ms.openlocfilehash: e697e2a2e99f67cb02422efdb368c664c9fd5a97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a>PowerShell kullanarak Azure'da güvenli küme oluşturma
Bu öğretici nasıl toocreate Service Fabric kümesi (Windows veya Linux) çalıştığından gösterir azure'da. İşlemi tamamladığınızda, uygulamaları dağıtabileceğiniz hello bulutta çalıştıran bir kümeye sahip.

Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:

> [!div class="checklist"]
> * PowerShell kullanarak Azure'da güvenli bir Service Fabric kümesi oluştur
> * Bir X.509 sertifikası ile güvenli hello kümesi
> * PowerShell kullanarak toohello kümesine bağlanın
> * Bir küme Kaldır

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce:
- Bir Azure aboneliğiniz yoksa, oluşturma bir [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- Merhaba yüklemek [Service Fabric SDK ve PowerShell Modülü](service-fabric-get-started.md)
- Merhaba yüklemek [Azure Powershell modülü sürümü 4.1 veya üzeri](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)

Aşağıdaki yordamı hello (tek sanal makine) tek bir düğüm Önizleme Service Fabric kümesi oluşturur. Merhaba küme hello küme yanı sıra oluşturulan ve bir anahtar kasası yerleştirilen otomatik olarak imzalanan bir sertifika tarafından korunmaktadır. Tek düğümlü küme bir sanal makine genişletilemez ve önizleme kümeleri yükseltilmiş toonewer sürümleri kaldırılamıyor.

Azure kullanım hello Service Fabric kümesi çalıştırarak ücrete toocalculate maliyet [Azure fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/).
Service Fabric kümeleri oluşturma hakkında daha fazla bilgi için bkz: [Azure Kaynak Yöneticisi'ni kullanarak bir Service Fabric kümesi oluştur](service-fabric-cluster-creation-via-arm.md).

## <a name="create-hello-cluster-using-azure-powershell"></a>Azure PowerShell kullanarak hello kümesi oluşturma
1. Hello hello Azure Resource Manager şablonu ve hello parametre dosyası yerel bir kopyasını indirin [Service Fabric için Azure Resource Manager şablonu](https://aka.ms/securepreviewonelineclustertemplate) GitHub depo.  *azuredeploy.JSON* tanımlayan bir Service Fabric kümesi hello Azure Resource Manager şablonudur. *azuredeploy.Parameters.JSON* toocustomize hello Küme dağıtımı sizin için bir parametre dosyası olduğunu.

2. Merhaba parametrelerinde aşağıdaki hello özelleştirme *azuredeploy.parameters.json* parametreler dosyası:

   | Parametre       | Açıklama | Önerilen Değer |
   | --------------- | ----------- | --------------- |
   | clusterLocation | Hello Azure bölgesi toowhich toodeploy hello küme. | *Örneğin, westeurope, eastasia, eastus* |
   | clusterName     | Ad hello kümesinin toocreate istiyor. | *Örneğin, bobs sfpreviewcluster* |
   | adminUserName   | Merhaba küme sanal makinelerde Hello yerel yönetici hesabı. | *Herhangi bir geçerli Windows Server kullanıcı adı* |
   | Admınpassword   | Hello hello küme sanal makinelerde yerel yönetici hesabının parolası. | *Geçerli bir Windows Server parola* |
   | clusterCodeVersion | Merhaba Service Fabric sürümü toorun. (255.255.X.255 Önizleme sürümleri). | **255.255.5718.255** |
   | vmInstanceCount | sanal makineler (1 ya da 3-99 olabilir) kümenizdeki Hello sayısı. | **1** | *Önizleme küme için yalnızca bir sanal makine belirtin* |

3. Bir PowerShell konsol, oturum açma tooAzure açın ve toodeploy hello küme istediğiniz hello aboneliği seçin:

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. Oluşturma ve Service Fabric tarafından kullanılan hello sertifika toobe için bir parola şifreleyebilirsiniz.

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. Merhaba küme ve sertifikasını hello aşağıdaki komutu çalıştırarak oluşturun:

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
   >Merhaba `-CertificateSubjectName` parametre Hizala hello Parametreler dosyasında belirtilen hello clusterName parametresiyle, de etki alanına bağlı toohello Azure bölgesi hello gibi gibi seçtiğiniz: `clustername.eastus.cloudapp.azure.com`.

Merhaba Yapılandırma tamamlandıktan sonra Azure içinde oluşturulan hello küme bilgilerini çıkarır. Ayrıca, bu parametre için belirtilen hello yolunda hello küme sertifika toohello - CertificateOutputFolder dizin kopyalar. Bu sertifika tooaccess kümenizi Service Fabric Explorer ve görünüm hello durumunu gerekir.

Benzer toohello olabilir, kümeniz hello URL'sini not edin URL aşağıdaki: *https://mycluster.westeurope.cloudapp.azure.com:19080*

## <a name="modify-hello-certificate--access-service-fabric-explorer"></a>Service Fabric Explorer erişim & Hello sertifika Değiştir ##

1. Merhaba sertifika tooopen hello Sertifika Alma Sihirbazı'nı çift tıklatın.

2. Varsayılan ayarları kullanır, ancak emin toocheck hello olun **bu anahtarı verilebilir olarak işaretle.** onay kutusuna hello **özel anahtar korumasını** adım. Visual Studio, Azure kapsayıcı kayıt defteri tooService doku küme kimlik doğrulaması daha sonra Bu öğreticide yapılandırırken tooexport hello sertifika gerekir.

3. Bu gibi durumlarda, Service Fabric Explorer şimdi bir tarayıcıda açabilirsiniz. toodo, bu nedenle, toohello gidin **ManagementEndpoint** bir web tarayıcısı ve makinenizde kaydedilmiş select hello sertifika kullanarak, kümeniz için URL.

>[!NOTE]
>Kendinden imzalı bir sertifika kullanıyor gibi Service Fabric Explorer açarken bir sertifika hatası bakın. Edge'de, tooclick sahip *ayrıntıları* ve ardından hello *toohello Web sayfasındaki Git* bağlantı. Chrome'tooclick sahip *Gelişmiş* ve ardından hello *devam* bağlantı.

>[!NOTE]
>Merhaba küme oluşturma işlemi başarısız olursa, her zaman önceden dağıtılan hello kaynak güncelleştirmeleri hello komutu çalıştırabilirsiniz. Bir sertifika başarısız hello dağıtımının bir parçası oluşturulmuş olsa bile, yeni bir tane oluşturulur. tootroubleshoot küme oluşturma, bkz: [Azure Kaynak Yöneticisi'ni kullanarak bir Service Fabric kümesi oluştur](service-fabric-cluster-creation-via-arm.md).

## <a name="connect-toohello-secure-cluster"></a>Toohello güvenli kümesine bağlanın
Service Fabric SDK Hello ile yüklü hello Service Fabric PowerShell modülünü kullanarak toohello kümesine bağlanın.  Önce bilgisayarınızdaki geçerli kullanıcının hello hello (My) kişisel deposuna hello sertifikası yükleyin.  Merhaba aşağıdaki PowerShell komutunu çalıştırın:

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

Hazır tooconnect tooyour güvenli küme sunulmuştur.

Merhaba **Service Fabric** PowerShell Modülü Service Fabric kümeleri, uygulamaları ve hizmetleri yönetmek için birçok cmdlet'leri sağlar.  Kullanım hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet tooconnect toohello güvenli küme. Sertifika parmak izi hello ve bağlantı uç nokta ayrıntılarını bir önceki adımda hello çıktısı bulunur.

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

Bağlı ve hello küme hello kullanarak sağlıklı olduğundan emin olun [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet'i.

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a>Kaynakları temizleme

Bir küme diğer Azure kaynaklarını toohello küme kaynağı kendisi ayrıca oluşur. Merhaba en basit yolu toodelete hello küme içereceği tükettiği tüm hello kaynakları ise toodelete hello kaynak grubu.

İçinde tooAzure oturum ve hello abonelik kimliği tooremove hello kümenin istediğinizi seçin.  Abonelik Kimliğinizi toohello içinde oturum açarak bulabilirsiniz [Azure portal](http://portal.azure.com). Merhaba kaynak grubu ve hello kullanarak tüm hello küme kaynakları silmek [Remove-AzureRMResourceGroup cmdlet'i](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).

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
> * Bir X.509 sertifikası ile güvenli hello kümesi
> * PowerShell kullanarak toohello kümesine bağlanın
> * Bir küme Kaldır

Ardından, öğretici toolearn nasıl aşağıdaki toohello ilerletmek toodeploy varolan bir uygulama.
> [!div class="nextstepaction"]
> [Varolan bir .NET uygulama Docker Compose ile dağıtma](service-fabric-host-app-in-a-container.md)
