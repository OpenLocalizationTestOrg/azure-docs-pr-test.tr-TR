---
title: "aaaDeploy Visual Studio kullanarak sanal makine ölçek kümesi | Microsoft Docs"
description: "Visual Studio ve Resource Manager şablonu kullanarak sanal makine ölçek kümeleri dağıtma"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed0786b8-34b2-49a8-85b5-2a628128ead6
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c89a9f2478ccc3d22989aea604a4273bcc46df82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-visual-studio"></a>Nasıl toocreate Visual Studio ile bir sanal makine ölçek kümesi
Bu makalede nasıl toodeploy bir Visual Studio kaynak grubu dağıtımı kullanarak bir Azure sanal makine ölçek kümesi gösterilmektedir.

[Azure sanal makine ölçek kümeleri](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) bir Azure işlem kaynak toodeploy ve Otomatik ölçek benzer sanal makinelerle koleksiyonunu yönetmenize ve Yük Dengeleme. Sağlama ve sanal makine ölçekleme kümeleri kullanarak dağıtın [Azure Resource Manager şablonları](https://github.com/Azure/azure-quickstart-templates). Azure CLI, PowerShell, REST kullanarak Azure Resource Manager şablonları dağıtılabilir ve ayrıca Visual Studio'dan doğrudan. Visual Studio bir Azure kaynak grubu dağıtım projesi bir parçası olarak dağıtılabilir örnek şablonları kümesi sağlar.

Azure kaynak grubu dağıtımları yolu toogroup olan ve bir dizi ilgili Azure kaynaklarını tek dağıtım işleminde yayımlayın. Bunları hakkında daha fazla burada öğrenebilirsiniz: [Visual Studio üzerinden Azure kaynak gruplarını oluşturma ve dağıtma](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

## <a name="pre-requisites"></a>Ön koşullar
Sanal makine ölçek kümeleri Visual Studio'daki dağıtımı başladı tooget hello aşağıdaki gerekir:

* Visual Studio 2013 veya üzeri
* 2.7, 2.8 veya 2.9 Azure SDK

>[!NOTE]
>Bu yönergeler, Visual Studio ile kullandığınız varsayılmıştır [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).

## <a name="creating-a-project"></a>Proje oluşturma
1. Seçerek Visual Studio'da yeni proje oluşturma **dosya | Yeni | Proje**.
   
    ![Yeni dosya][file_new]

2. Altında **Visual C# | Bulut**, seçin **Azure Resource Manager** toocreate bir Azure Resource Manager şablonunu dağıtmak için bir proje.
   
    ![Proje oluşturma][create_project]

3. Şablonları Hello listeden hello Linux veya Windows sanal makine ölçek kümesi şablonu seçin.
   
   ![Şablonu seçin][select_Template]

4. Projeniz oluşturulduktan sonra PowerShell dağıtım betikleri, bir Azure Resource Manager şablonu ve hello sanal makine ölçek kümesi için bir parametre dosyası bakın.
   
    ![Çözüm Gezgini][solution_explorer]

## <a name="customize-your-project"></a>Projenizi özelleştirme
Merhaba şablonu toocustomize düzenleyebilirsiniz artık VM uzantısı özellikleri ekleme veya düzenleme gibi uygulamanızın ihtiyaçları için Yük Dengeleme kuralları. Varsayılan olarak hello sanal makine ölçek kümesi kolay tooadd otomatik ölçeklendirme kurallarını kolaylaştırır yapılandırılmış toodeploy hello AzureDiagnostics uzantısı şablonlarıdır. Ayrıca, bir yük dengeleyici gelen NAT kuralları ile yapılandırılmış bir ortak IP adresi ile dağıtır. 

Hello yük dengeleyici SSH (Linux) veya RDP (Windows) ile toohello VM örnekleri bağlanmanıza olanak sağlar. Merhaba ön uç bağlantı noktası aralığı 50000'den başlar. Linux için bu olması durumunda anlamına gelir, SSH tooport 50000, yönlendirilmiş tooport 22 olan ilk VM hello ölçek kümesi ile Merhaba. Tooport 50001 bağlanma olduğu yönlendirilmiş tooport 22 hello VM vb. ikinci.

 En iyi yolu tooedit şablonlarınızı Visual Studio ile olan toouse hello JSON ana hattı tooorganize hello parametreleri, değişkenler ve kaynakları. Dağıtmadan önce hello bir anlayış şablonunuzda hataları ortaya şema Visual Studio işaret edebilir.

![JSON Gezgini][json_explorer]

## <a name="deploy-hello-project"></a>Merhaba projesini dağıtma
1. Hello Azure Resource Manager şablonu toocreate hello kaynak sanal makine ölçek kümesi dağıtın. Merhaba proje düğümüne sağ tıklayın ve seçin **dağıtma | Yeni dağıtım**.
   
    ![Şablon dağıtma][5deploy_Template]
    
2. Aboneliğinizi hello "Dağıtma tooResource grup" iletişim kutusunda seçin.
   
    ![Şablon dağıtma][6deploy_Template]

3. Buradan, şablonunuza bir Azure kaynak grubu toodeploy oluşturabilirsiniz.
   
    ![Yeni kaynak grubu][new_resource]

4. Bundan sonra öğesini **parametreleri Düzenle** tooyour şablonu geçirilen tooenter parametreleri. Merhaba gerekli toocreate hello dağıtım OS Hello kullanıcı adı ve parola sağlayın. Visual Studio yüklüyse PowerShell araçları yoksa, toocheck önerilir **parolaları kaydetme** tooavoid bir gizli PowerShell komut satırı isteyebilir veya kullanmak [keyvault Destek](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).
   
    ![Parametreleri Düzenle][edit_parameters]

5. Şimdi **dağıtma**. Merhaba **çıkış** penceresi hello dağıtımının ilerleme durumunu gösterir. Merhaba eylemin hello yürütüyor Not **dağıtma AzureResourceGroup.ps1** komut dosyası.
   
   ![Çıktı penceresi][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a>Sanal makine ölçek kümesi keşfetme
Merhaba dağıtım işlemi tamamlandıktan sonra görüntüleyebileceğiniz yeni sanal makine ölçek kümesindeki hello Visual Studio hello **Cloud Explorer** (yenileme hello listesi). Cloud Explorer uygulamaları geliştirirken Visual Studio'da Azure kaynaklarını yönetmenizi sağlar. Ayrıca, sanal makine ölçek kümesi hello görüntüleyebilirsiniz [Azure portal](https://portal.azure.com) ve [Azure kaynak Gezgini](https://resources.azure.com/).

![Bulut Gezgini][cloud_explorer]

 Merhaba portal toovisually yönetmek web tarayıcısı olan Azure altyapınıza Azure kaynak Gezgini kolay bir yolu tooexplore sağlarken hello en iyi yoldur ve Azure kaynaklarını hata ayıklama, bir penceresine vermiş "örnek görüntülemek" Merhaba ve ayrıca PowerShell gösteren Baktığınız hello kaynaklar için komutları.

## <a name="next-steps"></a>Sonraki adımlar
Visual Studio aracılığıyla sanal makine ölçek kümeleri başarıyla dağıttıktan sonra bir kez daha fazla uygulama gereksinimlerinizi proje toosuit özelleştirebilirsiniz. Örneğin, Otomatik ölçek ekleyerek yapılandırın bir **Insights** (örneğin, tek başına VM'ler) altyapısı tooyour şablonu ekleme veya hello özel betik uzantısı kullanarak uygulamaları dağıtma kaynak. İyi örnek şablonları hello bulunabilir [Azure hızlı başlangıç şablonlarını](https://github.com/Azure/azure-quickstart-templates) GitHub deposunu ("vmss" arayın).

[file_new]: ./media/virtual-machine-scale-sets-vs-create/1-FileNew.png
[create_project]: ./media/virtual-machine-scale-sets-vs-create/2-CreateProject.png
[select_Template]: ./media/virtual-machine-scale-sets-vs-create/3b-SelectTemplateLin.png
[solution_explorer]: ./media/virtual-machine-scale-sets-vs-create/4-SolutionExplorer.png
[json_explorer]: ./media/virtual-machine-scale-sets-vs-create/10-JsonExplorer.png
[5deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/5-DeployTemplate.png
[6deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/6-DeployTemplate.png
[new_resource]: ./media/virtual-machine-scale-sets-vs-create/7-NewResourceGroup.png
[edit_parameters]: ./media/virtual-machine-scale-sets-vs-create/8-EditParameter.png
[output_window]: ./media/virtual-machine-scale-sets-vs-create/9-Output.png
[cloud_explorer]: ./media/virtual-machine-scale-sets-vs-create/12-CloudExplorer.png
