---
title: "Visual Studio kullanarak bir Service Fabric kümesi ayarlama | Microsoft Docs"
description: "Visual Studio'da bir Azure kaynak grubu projesi tarafından oluşturulan Azure Resource Manager şablonu kullanarak bir Service Fabric kümesini ayarlamak açıklar"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: adegeo
editor: 
ms.assetid: bd2c0511-36c9-4828-8dc3-69e4b6a70567
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/21/2017
ms.author: mikhegn
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: c43145b96cdbdfaa7e1893e50d027321fe4c0510
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a>Visual Studio kullanarak bir Service Fabric kümesi ayarlayın
Bu makalede, Visual Studio ve Azure Resource Manager şablonu kullanarak bir Azure Service Fabric kümesini ayarlamak açıklar. Şablonu oluşturmak için Visual Studio Azure kaynak grubu projesi kullanacağız. Şablonu oluşturduktan sonra Visual Studio'dan doğrudan Azure dağıtılabilir. Ayrıca bir komut dosyasından veya sürekli tümleştirme (CI) tesis parçası olarak kullanılabilir.

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a>Bir Azure kaynak grubu projesi kullanarak bir Service Fabric kümesi şablonu oluşturma
Başlamak için Visual Studio'yu açın ve bir Azure kaynak grubu projesi oluşturun (içinde kullanılabilir **bulut** klasörü):

![Seçili Azure kaynak grubu projesi ile yeni proje iletişim kutusu][1]

Bu proje için yeni bir Visual Studio çözümü oluşturun veya varolan bir çözümü ekleyin.

> [!NOTE]
> Azure kaynak grubu projesi bulut düğümü altında görmüyorsanız Azure yüklü SDK'sı yok. Web Platformu yükleyicisi başlatın ([Şimdi Yükle](http://www.microsoft.com/web/downloads/platform.aspx) henüz yapmadıysanız), "Azure SDK'sı için .NET için" araması yapın ve Visual Studio sürümünüzle uyumlu sürümünü yükleyin.
> 
> 

Tamam düğmesine basın sonra Visual Studio oluşturmak istediğiniz Resource Manager şablonu seçmenizi ister:

![Azure şablonu iletişim kutusu seçili Service Fabric kümesi şablonla seçin][2]

Service Fabric kümesi şablonunu seçin ve Tamam düğmesine tekrar basın. Proje ve Resource Manager şablonu şimdi oluşturuldu.

## <a name="prepare-the-template-for-deployment"></a>Şablon dağıtımı için hazırlama
Kümeyi oluşturmak için şablon dağıtılmadan önce gerekli şablon parametreleri için değerler sağlamanız gerekir. Bu parametre değerlerini okuma `ServiceFabricCluster.parameters.json` dosyasını, `Templates` kaynak grubu projesi klasörü. Dosyasını açın ve aşağıdaki değerleri girin:

| Parametre adı | Açıklama |
| --- | --- |
| adminUserName |Yönetici hesabı adı için Service Fabric makineler (düğümler). |
| certificateThumbprint |Sertifikanın parmak izi, küme güvenliğini sağlar. |
| sourceVaultResourceId |*Kaynak kimliği* küme korur sertifikanın depolandığı anahtar kasasının. |
| certificateUrlValue |Küme güvenlik sertifikası URL'si. |

Visual Studio Service Fabric Resource Manager şablonu bir sertifika tarafından korunan güvenli bir küme oluşturur. Bu sertifika son üç şablon parametreleri ile tanımlanan (`certificateThumbprint`, `sourceVaultValue`, ve `certificateUrlValue`), ve bunu bulunmalıdır bir **Azure anahtar kasası**. Küme güvenlik sertifikasının nasıl oluşturulacağı hakkında daha fazla bilgi için bkz: [Service Fabric kümesi güvenlik senaryoları](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) makalesi.

## <a name="optional-change-the-cluster-name"></a>İsteğe bağlı: küme adını değiştirin
Her Service Fabric kümesi bir adı vardır. Azure'da bir Fabric kümesi oluşturduğunuzda, küme adı (Azure bölgesi ile birlikte) küme için etki alanı adı sistemi (DNS) ad belirler. Örneğin, küme adı, `myBigCluster`ve yeni küme barındıracak kaynak grubu konumu (Azure bölgesi) Doğu ABD, DNS adı kümenin `myBigCluster.eastus.cloudapp.azure.com`.

Varsayılan olarak küme adını otomatik olarak oluşturulur ve "Küme" öneki rastgele bir sonek ekleyerek benzersiz yapılan. Bu, çok şablon parçası olarak kullanmak üzere kolaylaştırır bir **sürekli tümleştirme** (CI) sistem. Sizin için anlamlı bir kümeniz için belirli bir ad kullanmak istiyorsanız, değeri ayarlayın `clusterName` Resource Manager şablonu dosyasındaki değişken (`ServiceFabricCluster.json`) için seçtiğiniz ad. Bu, o dosyasında tanımlanan ilk değişkenidir.

## <a name="optional-add-public-application-ports"></a>İsteğe bağlı: genel uygulama bağlantı noktaları ekleme
Dağıtmadan önce küme için genel uygulama bağlantı noktalarını değiştirmek isteyebilirsiniz. Varsayılan olarak, şablon yalnızca iki ortak TCP bağlantı noktalarını (80 ve 8081) açar. Daha fazla bilgi için uygulamalarınızı gerekiyorsa, Azure yük dengeleyici tanımını şablondaki değiştirin. Tanımı ana şablon dosyasında depolanır (`ServiceFabricCluster.json`). Bu dosyayı açın ve arama `loadBalancedAppPort`. Her bağlantı noktası üç yapılar ile ilişkilidir:

1. Bağlantı noktası TCP bağlantı noktası değerini tanımlayan Şablon değişkeni:
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. A *araştırma* tanımlayan ne sıklıkta ve ne kadar Azure yük dengeleyici üzerinden başka bir başarısız olmadan önce belirli bir Service Fabric düğüm kullanmayı dener. Araştırmalar yük dengeleyici kaynak bir parçasıdır. İlk varsayılan uygulama bağlantı noktası için araştırma tanımı aşağıda verilmiştir:
   
    ```json
    {
        "name": "AppPortProbe1",
        "properties": {
            "intervalInSeconds": 5,
            "numberOfProbes": 2,
            "port": "[variables('loadBalancedAppPort1')]",
            "protocol": "Tcp"
        }
    }
    ```
3. A *Yük Dengeleme kuralı* , bağlar, birlikte bağlantı noktası ve hangi etkinleştirir Yük Dengeleme Service Fabric küme düğümleri kümesi boyunca araştırma:
   
    ```json
    {
        "name": "AppPortLBRule1",
        "properties": {
            "backendAddressPool": {
                "id": "[variables('lbPoolID0')]"
            },
            "backendPort": "[variables('loadBalancedAppPort1')]",
            "enableFloatingIP": false,
            "frontendIPConfiguration": {
                "id": "[variables('lbIPConfig0')]"
            },
            "frontendPort": "[variables('loadBalancedAppPort1')]",
            "idleTimeoutInMinutes": 5,
            "probe": {
                "id": "[concat(variables('lbID0'),'/probes/AppPortProbe1')]"
            },
            "protocol": "Tcp"
        }
    }
    ```
   Kümeye dağıtmayı planladığınız uygulamalar daha fazla bağlantı noktası gerekiyorsa, bunları oluşturma ek araştırma ve Yük Dengeleme kuralı tanımlarına göre ekleyebilirsiniz. Azure yük dengeleyici ile Resource Manager şablonları ile çalışma konusunda daha fazla bilgi için bkz: [bir şablonu kullanarak bir iç yük dengeleyici oluşturmaya başlamak](../load-balancer/load-balancer-get-started-ilb-arm-template.md).

## <a name="deploy-the-template-by-using-visual-studio"></a>Visual Studio kullanarak şablonu dağıtma
Tüm gerekli parametre değerleri kaydettikten sonra`ServiceFabricCluster.param.dev.json` dosyası, şablonu dağıtmak ve Service Fabric kümesi oluşturmak hazır. Visual Studio Çözüm Gezgini kaynak grubu projesindeki sağ tıklatın ve seçin **dağıtma | Yeni dağıtım...** . Gerekirse, Visual Studio gösterir, **kaynak grubuna Dağıt** iletişim kutusu, Azure için kimlik doğrulaması isteyen:

![Kaynak grubu iletişim için dağıtma][3]

İletişim kutusu, küme için var olan bir Resource Manager kaynak grubu seçmenize olanak sağlar ve yeni bir tane oluşturmak için seçeneği sunar. Normalde bir Service Fabric kümesi için farklı bir kaynak grubu kullanacak şekilde mantıklıdır.

Dağıt düğmesi isabet sonra Visual Studio şablon parametre değerlerini onaylamanızı ister. İsabet **kaydetmek** düğmesi. Bir parametre kalıcı bir değere sahip değil: küme yönetici hesabı parolası. Visual Studio için bir tane istediğinde bir parola değeri sağlamanız gerekir.

> [!NOTE]
> Azure SDK 2.9 ile başlayarak, Visual Studio okuma parolalardan destekler **Azure anahtar kasası** dağıtımı sırasında. Şablon parametreleri iletişim kutusunda dikkat `adminPassword` parametresi metin kutusu sağda little "anahtar" simgesi vardır. Bu simge, küme yönetici parolası olarak var olan bir anahtar kasası gizli seçmenizi sağlar. Yalnızca ilk etkinleştirme, anahtar kasanızı Gelişmiş erişim ilkelerindeki şablon dağıtımı için Azure Resource Manager erişim için emin olun. 
> 
> 

Visual Studio çıktı penceresinde dağıtım işleminin ilerleme durumunu izleyebilirsiniz. Şablon dağıtımı tamamlandıktan sonra yeni küme kullanıma hazır!

> [!NOTE]
> PowerShell hiçbir zaman Azure şimdi kullanmakta olduğunuz makineden yönetmek için kullanıldıysa, küçük bir temizlik yapmanız gerekir.
> 
> 1. PowerShell komut dosyasını çalıştırarak etkinleştirme [ `Set-ExecutionPolicy` ](https://technet.microsoft.com/library/hh849812.aspx) komutu. Geliştirme makineler için "sınırsız" ilke genellikle kabul edilebilir.
> 2. Tanılama veri koleksiyonunu Azure PowerShell komutlarındaki izin verir ve çalıştırmak karar [ `Enable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619303.aspx) veya [ `Disable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619236.aspx) gerektiği. Bu gereksiz istemleri şablon dağıtımı sırasında kaçının.
> 
> 

Herhangi bir hata varsa, Git [Azure portal](https://portal.azure.com/) ve için dağıttığınız kaynak grubunu açın. Tıklatın **tüm ayarları**, ardından **dağıtımları** ayarlar dikey penceresinde. Başarısız bir kaynak grubu dağıtım ayrıntılı tanılama bilgisi var. bırakır.

> [!NOTE]
> Service Fabric kümeleri belirli sayıda düğümleri kullanılabilirliği sürdürmek ve "çekirdek koruma olarak." başvurulan durumunu - korumak için yukarı olması gerekir Bu nedenle, ilk yapmadığınız sürece tüm kümesindeki makineleri kapatmaya güvenli değil bir [tam yedekleme, durumunun](service-fabric-reliable-services-backup-restore.md).
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* [Azure portalını kullanarak Service Fabric kümesi ayarlama hakkında bilgi edinin](service-fabric-cluster-creation-via-portal.md)
* [Visual Studio kullanarak Service Fabric uygulamaları yönetmeyi ve dağıtmayı öğrenin](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
