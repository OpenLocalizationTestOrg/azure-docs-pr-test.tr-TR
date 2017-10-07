---
title: "aaaCreate çoklu VM ortamları ve Azure Resource Manager şablonları ile PaaS kaynaklarına | Microsoft Docs"
description: "Bilgi nasıl toocreate çoklu VM ortamları ve PaaS kaynaklardan Azure DevTest Labs içinde bir Azure Resource Manager şablonu"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: tarcher
ms.openlocfilehash: ab8628f6cb5a666435258efb93921ec69ad3a13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-multi-vm-environments-and-paas-resources-with-azure-resource-manager-templates"></a>Çoklu VM ortamları ve PaaS kaynaklarına Azure Resource Manager şablonları ile oluşturma

Merhaba [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) tooeasily sağlayan [oluşturun ve VM tooa Laboratuvar ekleme](https://docs.microsoft.com/en-us/azure/devtest-lab/devtest-lab-add-vm). Bu da aynı anda bir VM oluşturmak için çalışır. Ancak, birden çok VM Hello ortamı içeriyorsa, her VM tek tek toobe vardır. Çok katmanlı Web uygulaması veya bir SharePoint grubu gibi senaryolar için bir tek adımda birden çok VM hello oluşturulması için gereken tooallow mekanizmadır. Azure Resource Manager şablonları kullanarak şimdi hello altyapısı ve Azure çözümünüzü yapılandırmasını tanımlayın ve sürekli olarak tutarlı bir durumda birden çok VM dağıtın. Bu özellik, hello aşağıdaki avantajları sağlar:

- Azure Resource Manager şablonları doğrudan, kaynak denetim deposundan (GitHub veya Team Services Git) yüklenir.
- Yapılandırdıktan sonra kullanıcılarınızın bir ortam hello diğer türleri ile ne yapabileceklerini olarak Azure portalında bir Azure Resource Manager şablonu seçerek oluşturabilirsiniz [VM tabanları](./devtest-lab-comparing-vm-base-image-types.md).
- Azure PaaS kaynaklarına ek tooIaaS VM'ler Azure Resource Manager şablonunda bir ortamdan sağlanabilir.
- ortamlar Hello maliyetini toplama tooindividual tabanları diğer türleri tarafından oluşturulan VM'ler hello laboratuvarda izlenebilir.
- PaaS kaynaklarına oluşturulur ve maliyet izlemesi görüntülenir; Ancak, VM otomatik kapatma tooPaaS kaynakların geçerli değildir.
- Kullanıcınız tek Laboratuvar VM'ler için sahip oldukları gibi hello ortamlar için aynı VM ilke denetimi.

Birçok hello hakkında daha fazla bilgi [Resource Manager şablonlarını kullanmanın yararları](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#the-benefits-of-using-resource-manager) toodeploy, güncelleştirme ya da tüm Laboratuvar kaynaklarınızı tek bir işlemde silin.

> [!NOTE]
> Daha fazla Laboratuvar VM'ler temel toocreate bir Resource Manager şablonunu kullandığınızda, bazı farklar tookeep göz önünde Multi-VMs veya tek sanal makineleri oluştururken olup olmadığı. Bir sanal makinenin kullanmak Azure Resource Manager şablonu Bu farklılıklar daha ayrıntılı açıklanır.
>
>

## <a name="configure-azure-resource-manager-template-repositories"></a>Azure Resource Manager şablonu depoları yapılandırın

Merhaba biri olarak altyapı olarak kodu ve kod olarak yapılandırma, ortam şablonları en iyi yöntemlerle kaynak denetiminde yönetilmelidir. Azure DevTest Labs, bu yöntem izler ve tüm Azure Resource Manager şablonları doğrudan, GitHub veya VSTS Git havuzların yükler. Sonuç olarak, Resource Manager şablonları hello test ortamı toohello üretim ortamı'ndan hello tüm yayın döngüsü boyunca kullanılabilir.

Bir depoda Azure Resource Manager şablonlarınızı birkaç kuralları toofollow tooorganize vardır:

- Merhaba ana şablon dosyası adlı `azuredeploy.json`. 

    ![Anahtar Azure Resource Manager şablon dosyaları](./media/devtest-lab-create-environment-from-arm/master-template.png)

- Bir parametre dosyasında tanımlanan toouse parametre değerlerini istiyorsanız hello parametre dosyası adlandırılmalıdır `azuredeploy.parameters.json`.
- Merhaba parametreleri kullanabilirsiniz `_artifactsLocation` ve `_artifactsLocationSasToken` DevTest Labs tooautomatically yönetmenize izin vererek tooconstruct hello parametersLink URI değeri, iç içe şablonları. Bkz: [nasıl Azure DevTest Labs yapar iç içe geçmiş Resource Manager şablonu dağıtımları test ortamlarında daha kolay](https://blogs.msdn.microsoft.com/devtestlab/2017/05/23/how-azure-devtest-labs-makes-nested-arm-template-deployments-easier-for-testing-environments/) daha fazla bilgi için.
- Meta veri tanımlanan toospecify hello şablon görünen ad ve açıklama olabilir. Bu meta veriler adındaki bir dosyada olmalıdır `metadata.json`. Merhaba aşağıdaki örnek meta veri dosyası adı ve açıklaması toospecify hello görüntülenme gösterilmektedir: 

```json
{
 
"itemDisplayName": "<your template name>",
 
"description": "<description of hello template>"
 
}
```

Merhaba aşağıdaki adımlar, hello Azure portal kullanarak bir depo tooyour laboratuvarı eklerken size kılavuzluk. 

1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Seçin **daha Hizmetleri**ve ardından **DevTest Labs** hello listeden.
1. Merhaba istenen Laboratuvar labs Hello listeden seçin.   
1. Merhaba Laboratuvar'ın dikey penceresinde, seçin **yapılandırma ve ilkeleri**.

    ![Yapılandırma ve ilkeleri](./media/devtest-lab-create-environment-from-arm/configuration-and-policies-menu.png)

1. Merhaba gelen **yapılandırma ve ilkeleri** ayarları listesinde **depoları**. Merhaba **depoları** toohello Laboratuvar eklenen hello depoları dikey penceresinde listelenir. Adlı depo `Public Repo` tüm Laboratuvarları için otomatik olarak oluşturulur ve toohello bağlayan [DevTest Labs GitHub deposuna](https://github.com/Azure/azure-devtestlab) kullanımınız için birden fazla VM yapılar içerir.

    ![Ortak depodaki](./media/devtest-lab-create-environment-from-arm/public-repo.png)

1. Seçin **Ekle +** tooadd Azure Resource Manager şablonu deponuz.
1. Ne zaman ikinci hello **depoları** dikey penceresi açılır ve hello gerekli bilgileri aşağıdaki gibi girin:
    - **Ad** -hello laboratuvarında kullanılan hello depo adını girin.
    - **Git kopyalama URL'si** -GitHub ya da Visual Studio Team Services hello GIT HTTPS kopya URL'si girin.  
    - **Şube** -hello şube adı tooaccess, Azure Resource Manager şablonu tanımlarını girin. 
    - **Kişisel erişim belirteci** -hello kişisel erişim belirteci kullanılır toosecurely deponuz erişim. Visual Studio Team Services, belirtecinden tooget seçin  **&lt;adınız >> Profilim > Güvenlik > Genel erişim belirteci**. tooget belirtecinizi github'dan seçin seçerek ve ardından, avatar **ayarlar > Genel erişim belirteci**. 
    - **Klasör yolları** - hello iki giriş alanları, birini kullanarak bir eğik çizgiyle - / - başlatır hello klasör yolu girin ve yapı tanımlarınızı göreli tooyour Git kopya URI tooeither olduğu (ilk giriş alanı) veya Azure Resource Manager şablonu tanımları.   
    
        ![Ortak depodaki](./media/devtest-lab-create-environment-from-arm/repo-values.png)

1. Tüm gerekli hello alanları girilir ve hello geçemediğinden sonra seçeneğini **kaydetmek**.

Merhaba sonraki bölümde bir Azure Resource Manager şablonu ortamları oluşturmada size yol gösterir.

## <a name="create-an-environment-from-an-azure-resource-manager-template"></a>Bir Azure Resource Manager şablonu bir ortam oluşturmak

Bir Azure Resource Manager şablonu deposu hello laboratuvarda yapılandırıldıktan sonra Laboratuvar kullanıcılarınızın Azure portal ile Merhaba aşağıdaki adımları kullanarak bir ortam oluşturabilirsiniz:

1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Seçin **daha Hizmetleri**ve ardından **DevTest Labs** hello listeden.
1. Merhaba istenen Laboratuvar labs Hello listeden seçin.   
1. Merhaba Laboratuvar'ın dikey penceresinde, seçin **Ekle +**.
1. Merhaba **bir temel seçin** dikey penceresinde görüntüler hello taban görüntüleri ilk listelenen hello Azure Resource Manager şablonları ile kullanabilirsiniz. Select hello Azure Resource Manager şablonu istenen.

    ![Bir temel seçin](./media/devtest-lab-create-environment-from-arm/choose-a-base.png)
  
1. Merhaba üzerinde **Ekle** dikey penceresinde hello girin **ortam adı** değeri. Merhaba ortamı hello Laboratuvar görüntülenen tooyour kullanıcılar nedir adıdır. Merhaba kalan giriş alanları hello Azure Resource Manager şablonunda tanımlanır. Varsayılan değerleri hello şablonu veya hello tanımlı değilse `azuredeploy.parameter.json` dosya varsa, varsayılan değerleri, bu girdi alanlarında görüntülenir. Tür parametreleri için *güvenli dize*, hello laboratuar ortamında 's depolanan hello gizlilikler kullanabilir [kişisel gizli depolama](https://azure.microsoft.com/en-us/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store).

    ![Ekle dikey penceresi](./media/devtest-lab-create-environment-from-arm/add.png)

    > [!NOTE]
    > -Belirtilmiş olsa bile - boş değerler olarak görüntülenen birkaç parametre değerleri vardır. Bu nedenle, kullanıcıların bir Azure Resource Manager şablonunda bu değerleri tooparameters atarsanız, DevTest Labs hello değerleri görüntülemez; Bunun yerine boş giriş alanlarının nerede hello Laboratuvar kullanıcıların tooenter gerekir hello ortamı oluştururken bir değer gösteriliyor.
    > 
    > - GEN BENZERSİZ
    > - GEN - BENZERSİZ-[N]
    > - GEN SSH-PUB-ANAHTAR
    > - GEN-PAROLA 
 
1. Seçin **Ekle** toocreate hello ortamı. Merhaba ortamı başlatır hello görüntüleme hello durumundaki hemen sağlama **My sanal makineleri** listesi. Yeni bir kaynak grubu, hello Azure Resource Manager şablonunda tanımlanan tüm hello kaynakları hello Laboratuvar tooprovision tarafından otomatik olarak oluşturulur.
1. Merhaba ortamı oluşturulduktan sonra hello hello ortamı seçin **My sanal makineleri** listesinde tooopen hello kaynak grubu dikey ve hello Ortamı'nda sağlanan hello kaynakların tümünü göz atın.
    
    ![Sanal makineler listem](./media/devtest-lab-create-environment-from-arm/all-environment-resources.png)
   
   Merhaba ortamı tooview yalnızca hello hello Ortamı'nda sağlanan VM'lerin listesini genişletebilirsiniz.
    
    ![Sanal makineler listem](./media/devtest-lab-create-environment-from-arm/my-vm-list.png)

1. Veri diskleri, değişen otomatik kapatma süresi ve daha fazlasını ekleme yapıları, uygulama gibi hello ortamları tooview hello kullanılabilir eylemler - birini tıklatın.

    ![Ortam Eylemler](./media/devtest-lab-create-environment-from-arm/environment-actions.png)

## <a name="next-steps"></a>Sonraki adımlar
* Bir VM oluşturulduktan sonra seçerek toohello VM bağlanabilir **Bağlan** hello VM'in dikey.
* Kaynakları görüntülemek ve bir ortamda hello hello ortam seçerek yönetmek **My sanal makineleri** Laboratuvarınızı listesinde. 
* Merhaba keşfedin [Azure hızlı başlangıç Şablon Galerisinden Azure Resource Manager şablonları](https://github.com/Azure/azure-quickstart-templates)
