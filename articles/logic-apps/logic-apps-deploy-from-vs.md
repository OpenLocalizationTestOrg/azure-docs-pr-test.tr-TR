---
title: "aaaCreate, derleme ve logic apps Visual Studio - Azure mantıksal uygulamaları dağıtma | Microsoft Docs"
description: "Tasarlama, derleme ve Azure mantıksal uygulamaları dağıtmak için Visual Studio projeleri oluşturma."
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e484e5ce-77e9-4fa9-bcbe-f851b4eb42a6
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 2/14/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 5154cb05f9a48e9f0f2381a6953947217f7bb114
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a>Tasarım, derleme ve Visual Studio'daki Azure mantıksal uygulamaları dağıtma

Merhaba rağmen [Azure portal](https://portal.azure.com/) toocreate sizin için harika bir yol sunar ve Azure mantıksal uygulamaları yönetmek için Visual Studio tasarlamayı, derlemeyi ve mantıksal uygulamalarınızı dağıtma için kullanabilirsiniz. Visual Studio hello mantığı Uygulama Tasarımcısı gibi zengin araçları sizin için toocreate logic apps sağlar, dağıtım ve Otomasyon şablonları yapılandırın ve tooany ortamı dağıtın. 

Azure Logic Apps ile başlatılan tooget öğrenin [nasıl toocreate ilk mantıksal uygulamanızı hello Azure portal](logic-apps-create-a-logic-app.md).

## <a name="installation-steps"></a>Yükleme adımları

tooinstall ve Visual Studio Araçları Azure mantıksal uygulamaları için yapılandırmak için aşağıdaki adımları izleyin.

### <a name="prerequisites"></a>Ön koşullar

* [Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) veya Visual Studio 2015
* [En son Azure SDK'sı](https://azure.microsoft.com/downloads/) (2.9.1 veya üzeri)
* [Azure PowerShell](https://github.com/Azure/azure-powershell#installation)
* Merhaba katıştırılmış Tasarımcısı kullanırken erişim toohello web

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a>Azure mantıksal uygulamaları için Visual Studio araçlarını yükleme

Merhaba önkoşulları yüklendikten sonra:

1. Visual Studio'yu açın. Merhaba üzerinde **Araçları** menüsünde, select **Uzantılar ve güncelleştirmeler**.
2. Merhaba genişletin **çevrimiçi** çevrimiçi arama yapabilmeniz için kategori.
3. Göz atın veya arayın **Logic Apps** bulana kadar **Visual Studio için Azure Logic Apps Araçları**.
4. toodownload ve yükleme hello uzantısı,'ı **karşıdan**.
5. Yüklendikten sonra Visual Studio'yu yeniden başlatın.

> [!NOTE]
> Ayrıca indirebilirsiniz [Azure Logic Apps araçları Visual Studio 2017 için](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) ve hello [Visual Studio 2015 için Azure Logic Apps Araçları](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) hello Visual Studio Market'te doğrudan.

Yükleme işlemini tamamlandığınızda hello Azure kaynak grubu projesi mantığı uygulama tasarımcı ile birlikte kullanabilirsiniz.

## <a name="create-your-project"></a>Projenizi oluşturma

1. Merhaba üzerinde **dosya** menüsünde çok Git**yeni**seçip **proje**. Veya tooadd çözüm, Git çok varolan, proje tooan**Ekle**seçip **yeni proje**.

    ![Dosya menüsü](./media/logic-apps-deploy-from-vs/filemenu.png)

2. Merhaba, **yeni proje** penceresinde Bul **bulut**seçip **Azure kaynak grubu**. Projenizi adlandırın ve tıklatın **Tamam**.

    ![Yeni Proje Ekle](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. Select hello **mantıksal uygulama** boş mantığı uygulama dağıtım şablonu toouse sizin için oluşturduğu şablonu. Şablonunuzu seçtikten sonra tıklayın **Tamam**.

    ![Mantıksal uygulama şablonu seçin](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    Şimdi mantıksal uygulama projesi tooyour çözümünüzü ekledik. 
    Hello Çözüm Gezgini, dağıtım dosyanızı görüntülenmesi gerekir.

    ![Dağıtım dosyası](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a>Mantıksal uygulamanızı mantığı Uygulama Tasarımcısı ile oluşturma

Bir mantıksal uygulama içeren bir Azure kaynak grubu projesi sahip olduğunuzda, iş akışınızı Visual Studio toocreate hello mantığı Uygulama Tasarımcısı açabilirsiniz. 

> [!NOTE]
> internet bağlantısı çok bağlayıcıları kullanılabilir özellikler ve veri için sorgu Hello Tasarımcısı gerektirir. Örneğin, hello Dynamics CRM Online bağlayıcısını kullanırsanız, hello Tasarımcısı varsayılan özellikleri ve CRM örneği tooshow kullanılabilir özel sorgular.

1. Sağ tıklayın, `<template>.json` dosyasını bulun ve seçin **mantığı Uygulama Tasarımcısı ile Aç**. (`Ctrl+L`)

2. Azure abonelik, kaynak grubunu ve konumu, dağıtım şablonu seçin.

    > [!NOTE]
    > Bir mantıksal uygulama tasarlama API bağlantı kaynaklarını özellikleri sorgu tasarımı sırasında oluşturur. Visual Studio tasarım sırasında bu bağlantılar, seçili kaynak grubu toocreate kullanır. tooview veya herhangi bir API bağlantısı değiştirmek, toohello Azure portalına gidin ve göz **API bağlantıları**.

    ![Abonelik Seçici](./media/logic-apps-deploy-from-vs/designer_picker.png)

    Merhaba Tasarımcısı kullanır hello tanımı hello `<template>.json` dosya oluşturma işlemi için.

4. Oluşturun ve mantıksal uygulamanızı tasarlayın. Dağıtım şablonu, yaptığınız değişikliklerle güncelleştirilir.

    ![Visual Studio'da mantığı Uygulama Tasarımcısı](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

Visual Studio ekler `Microsoft.Web/connections` kaynakları çok, kaynak dosya için herhangi bir bağlantısı toofunction mantıksal uygulamanız gerekir. Bu bağlantı özellikleri ayarlanabilir dağıttığınızda ve içinde dağıttıktan sonra yönetilen **API bağlantıları** hello Azure Portalı'nda.

### <a name="switch-toojson-code-view"></a>TooJSON kod görünümüne geçin

tooshow hello mantıksal uygulamanızı seçin hello için JSON gösterimi **kod görünümü** hello Designer hello altındaki sekmesi.

tooswitch toohello tam kaynak JSON yeniden, hello sağ `<template>.json` dosyasını bulun ve seçin **açık**.

### <a name="add-references-for-dependent-resources-toovisual-studio-deployment-templates"></a>Bağımlı kaynaklarla tooVisual Studio dağıtım şablonları için başvuruları ekleme

Mantıksal uygulama tooreference bağımlı kaynaklarınızı istediğinizde kullanabilirsiniz [Azure Resource Manager şablonu işlevleri](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) mantığı uygulama dağıtım şablonunuzda. Örneğin, mantıksal uygulama tooreference mantıksal uygulamanızı toodeploy istediğiniz bir Azure işlevi veya tümleştirme hesap isteyebilirsiniz. Mantıksal Uygulama Tasarımcısı hello şekilde dağıtım şablonunuzu toouse parametrelerinde nasıl işlediğini doğru hakkında aşağıdaki yönergeleri izleyin. 

Bu türden tetikleyiciler ve Eylemler mantığı uygulama parametreleri kullanabilirsiniz:

*   Alt iş akışı
*   İşlev uygulaması
*   APIM çağrısı
*   API bağlantı çalışma zamanı URL'si
*   API bağlantı yolu

Ve şablon işlevleri parametreleri, değişkenleri, ResourceId, concat vb. gibi kullanabilirsiniz. Örneğin, işte hello Azure işlevi kaynak kimliği nasıl değiştirebilirsiniz:

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

Ve burada parametreleri kullanabilirsiniz:

```
"MyFunction": {
    "type": "Function",
    "inputs": {
        "body":{},
        "function":{
            "id":"[resourceid('Microsoft.Web/sites/functions','functionApp',parameters('functionName'))]"
        }
    },
    "runAfter":{}
}
```
Başka bir örnek olarak Service Bus Gönder ileti işlemi hello Parametreleştirme:

```
"Send_message": {
    "type": "ApiConnection",
        "inputs": {
            "host": {
                "connection": {
                    "name": "@parameters('$connections')['servicebus']['connectionId']"
                }
            },
            "method": "post",
            "path": "[concat('/@{encodeURIComponent(''', parameters('queueuname'), ''')}/messages')]",
            "body": {
                "ContentData": "@{base64(triggerBody())}"
            },
            "queries": {
                "systemProperties": "None"
            }
        },
        "runAfter": {}
    }
```
> [!NOTE] 
> host.runtimeUrl isteğe bağlıdır ve varsa, şablondan kaldırılabilir.
> 


> [!NOTE] 
> Örneğin parametrelerini kullandığınızda hello mantığı Uygulama Tasarımcısı toowork için varsayılan değer sağlamalısınız:
> 
> ```
> "parameters": {
>     "IntegrationAccount": {
>     "type":"string",
>     "minLength":1,
>     "defaultValue":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.Logic/integrationAccounts/<integrationAccountName>"
>     }
> },
> ```

### <a name="save-your-logic-app"></a>Mantıksal uygulamanızı kaydetme

toosave mantığı uygulamanızı dilediğiniz zaman, Git çok**dosya** > **kaydetmek**. (`Ctrl+S`) 

Uygulamanızı kaydederken mantıksal uygulamanızı herhangi bir hata varsa, hello Visual Studio göründükleri **çıkışları** penceresi.

## <a name="deploy-your-logic-app-from-visual-studio"></a>Mantıksal uygulamanızı Visual Studio'dan dağıtma

Uygulamanızı yapılandırdıktan sonra yalnızca birkaç adımda Visual Studio doğrudan dağıtabilirsiniz. 

1. Çözüm Gezgini'nde, projenize sağ tıklayın ve çok Git**dağıtma** > **yeni dağıtım...**

    ![Yeni dağıtım](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. İstendiğinde, tooyour Azure aboneliği oturum açın. 

3. Şimdi mantıksal uygulamanızı toodeploy istediğiniz yere hello kaynak grubu için hello ayrıntıları seçmeniz gerekir. İşiniz bittiğinde seçin **dağıtma**.

    > [!NOTE]
    > Merhaba doğru şablonu ve parametre dosyası hello kaynak grubu için seçtiğinizden emin olun. Örneğin, toodeploy tooa üretim ortamına istiyorsanız hello üretim parametreler dosyası seçin.

    ![Tooresource grubunu dağıtma](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    Merhaba dağıtım durumu görünür hello **çıkış** penceresi. 
    Tooselect olabilir **Azure sağlama** hello içinde **Göster çıktı** listesi.

    ![Dağıtım durumu çıktı](./media/logic-apps-deploy-from-vs/output.png)

Hello gelecekteki, mantıksal uygulamanızı kaynak denetiminde düzenleyin ve Visual Studio toodeploy yeni sürümlerini kullanın.

> [!NOTE]
> Hello Azure portal hello tanımında doğrudan değiştirirseniz, sonraki Visual Studio'dan dağıttığınızda bu değişikliklerin üzerine yazılır. 

## <a name="add-your-logic-app-tooan-existing-resource-group-project"></a>Mantıksal uygulama tooan mevcut kaynak grubu projenizi ekleme

Varolan bir kaynak grubu projesi varsa, logic app toothat projenizi hello JSON ana hattı penceresinde ekleyebilirsiniz. Daha önce oluşturduğunuz hello uygulama yanında başka bir mantıksal uygulama da ekleyebilirsiniz.

1. Açık hello `<template>.json` dosya.

2. JSON ana hattı penceresinin tooopen hello Git çok**Görünüm** > **diğer pencereler** > **JSON ana hattı**.

3. tooadd bir kaynak toohello şablon dosyası tıklatın **kaynak ekleme** hello JSON ana hattı penceresinin hello üstünde. Veya hello JSON ana hattı penceresinde sağ **kaynakları**seçip **yeni kaynak ekleme**.

    ![JSON ana hattı penceresinin](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. Merhaba, **kaynak ekleme** iletişim kutusu bulun ve seçin, **mantıksal uygulama**. Mantıksal uygulamanızı adlandırın ve seçin **Ekle**.

    ![Kaynak Ekle](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a>Sonraki Adımlar

* [Logic apps Visual Studio Cloud Explorer ile yönetme](logic-apps-manage-from-vs.md)
* [Sık rastlanan örnekleri ve senaryoları inceleyin](logic-apps-examples-and-scenarios.md)
* [Tooautomate iş Azure Logic Apps ile nasıl işlediği öğrenin](http://channel9.msdn.com/Events/Build/2016/T694)
* [Bilgi nasıl toointegrate sistemlerinizi Azure Logic Apps ile](http://channel9.msdn.com/Events/Build/2016/P462)
