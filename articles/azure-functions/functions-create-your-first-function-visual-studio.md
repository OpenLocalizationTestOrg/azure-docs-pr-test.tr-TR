---
title: "ilk işlev Visual Studio kullanarak Azure'da aaaCreate | Microsoft Docs"
description: "Oluşturma ve Visual Studio için Azure işlevleri araçları kullanarak basit bir HTTP tetiklenen işlevi tooAzure yayımlama."
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: "azure işlevleri, işlevler, olay işleme, işlem, sunucusuz mimari"
ms.assetid: 82db1177-2295-4e39-bd42-763f6082e796
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 07/05/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 851e5b98dcc2da00334620896a0ea31f566589f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-visual-studio"></a>Visual Studio kullanarak ilk işlevinizi oluşturma

Azure işlevleri sağlayan bir VM oluşturun veya bir web uygulaması yayımlama toofirst gerek kalmadan sunucusuz bir ortamda kodunuzu yürütün.

Bu konuda, nasıl toouse Azure işlevleri toocreate için Visual Studio 2017 araçları hello ve bir "hello world" işlevi yerel olarak test öğrenin. Merhaba işlevi kod tooAzure sonra yayımlar. Bu araçları, Visual Studio 2017 sürüm 15.3 hello Azure geliştirme iş yükü parçası veya sonraki bir sürümü kullanılabilir.

![Visual Studio projesinde Azure İşlevleri kodu](./media/functions-create-your-first-function-visual-studio/functions-vstools-intro.png)

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu öğretici, yükleme:

* [Visual Studio 2017 sürüm 15.3](https://www.visualstudio.com/vs/preview/), hello dahil olmak üzere **Azure geliştirme** iş yükü.

    ![Visual Studio 2017 hello Azure geliştirme yüküyle yükleyin](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)
    
    >[!NOTE]  
    Yükleme veya tooVisual Studio 2017 sürüm 15.3 yükselttikten sonra Azure işlevleri için toomanually güncelleştirme hello Visual Studio 2017 araçları da gerekebilir. Merhaba hello araçlarından güncelleştirebilirsiniz **Araçları** menüsünün altında **Uzantılar ve güncelleştirmeler...**   >  **Güncelleştirmeleri** > **Visual Studio Marketi'ine** > **Azure işlevleri ve Web Araçları işleri**  >  **Güncelleştirme**. 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

## <a name="create-an-azure-functions-project-in-visual-studio"></a>Visual Studio'da bir Azure İşlevleri projesi oluşturma

[!INCLUDE [Create a project using hello Azure Functions template](../../includes/functions-vstools-create.md)]

Merhaba proje oluşturduğunuza göre ilk işlevinizi oluşturabilirsiniz.

## <a name="create-hello-function"></a>Create Hello işlevi

1. **Çözüm Gezgini**’nde, proje düğümünüze sağ tıklayın ve **Yeni** > **Öğe Ekle**’yi seçin. **Azure İşlevi**’ni seçin ve **Ekle**’ye tıklayın.

2. **HttpTrigger**’ı seçin, **İşlev Adı** yazın, **Erişim Hakları** için **Anonim**’i seçin ve **Oluştur**’a tıklayın. oluşturulan hello işlevi herhangi bir istemciden bir HTTP isteği tarafından erişilir. 

    ![Yeni bir Azure İşlevi oluşturma](./media/functions-create-your-first-function-visual-studio/functions-vstools-add-new-function-2.png)

    Kod dosyası işlevi kodunuzu uygulayan bir sınıf içeren tooyour projesi eklenir. Bu kod adı değeri ve geri kırmak alan bir şablona temel alır. Merhaba **FunctionName** öznitelik işlevinizi hello adını ayarlar. Merhaba **HttpTrigger** öznitelik hello işlevi tetikler selamlama iletisine gösterir. 

    ![İşlev kod dosyası](./media/functions-create-your-first-function-visual-studio/functions-code-page.png)

HTTP ile tetiklenen işlev oluşturduğunuza göre, artık bunu yerel bilgisayarınızda test edebilirsiniz.

## <a name="test-hello-function-locally"></a>Yerel olarak test hello işlevi

Azure İşlevleri Temel Araçları, Azure İşlevleri projenizi yerel geliştirme bilgisayarınızda çalıştırmanıza olanak sağlar. Bu araçları ilk kez Visual Studio'dan bir işlev başlattığınızda hello istendiğinde tooinstall var.  

1. tootest işlevinizi, F5 tuşuna basın. İstenirse, Visual Studio toodownload hello isteğini kabul edin ve Azure işlevleri çekirdek (CLI) Araçları'nı yükleyin.  Böylece Hello araçları HTTP isteklerini işleyebilir tooenable bir güvenlik duvarı özel durumu da gerekebilir.

2. Kopya hello hello Azure işlevleri çalışma zamanı, işlevinden URL'sini çıktı.  

    ![Azure yerel çalışma zamanı](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. Merhaba HTTP isteği Hello URL'sini tarayıcınızın adres çubuğuna yapıştırın. Merhaba sorgu dizesi eklemek `&name=<yourname>` toothis URL ve hello istek yürütülemiyor. Merhaba aşağıdaki hello yanıt hello işlevi tarafından döndürülen hello tarayıcı toohello yerel GET isteğini gösterir: 

    ![Merhaba tarayıcıda işlev localhost yanıtı](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. hata ayıklama, toostop tıklatın hello **durdurmak** hello Visual Studio araç çubuğunda.

Hello işlevi, yerel bilgisayarınızda düzgün çalıştığını doğruladıktan sonra zaman toopublish hello proje tooAzure olur.

## <a name="publish-hello-project-tooazure"></a>Yayımlama Hello proje tooAzure

Projenizi yayımlayabilmeniz için önce Azure aboneliğinizde bir işlev uygulamanızın olması gerekir. Visual Studio'dan bir işlev uygulaması oluşturabilirsiniz.

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a>Azure'da işlevinizi test etme

1. Merhaba işlevi uygulamasının temel URL'si Hello hello yayımlama profili sayfadan kopyalayın. Hello yerine `localhost:port` hello işlevi hello yeni temel URL ile yerel olarak test edilirken kullanılan hello URL'sinin. Önceki gibi emin tooappend hello sorgu dizesi yapmak `&name=<yourname>` toothis URL ve hello istek yürütülemiyor.

    Bu işlev görülüyor, HTTP çağrıları hello URL tetiklenen:

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. Bu yeni URL hello HTTP isteği için tarayıcınızın adres çubuğuna yapıştırın. Merhaba aşağıdaki hello yanıt hello işlevi tarafından döndürülen hello tarayıcı toohello uzak GET isteğini gösterir: 

    ![Merhaba tarayıcıda işlev yanıtı](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)
 
## <a name="next-steps"></a>Sonraki adımlar

Visual Studio toocreate C# işlev uygulaması basit bir HTTP tetiklenen işleviyle kullandınız. 

+ toolearn nasıl tooconfigure proje toosupport Tetikleyicileri ve bağlamaları, diğer türlerini görmek hello [yapılandırma hello proje yerel geliştirme için](functions-develop-vs.md#configure-the-project-for-local-development) bölümüne [Visual Studio için Azure işlevleri Araçları](functions-develop-vs.md).
+ Yerel test ve hello Azure işlevleri çekirdek araçlarını kullanarak hata ayıklama hakkında daha fazla toolearn bkz [koduna ve test Azure işlevleri yerel olarak](functions-run-local.md). 
+ .NET sınıf kitaplıkları işlevleri geliştirme hakkında daha fazla toolearn bkz [Azure işlevlerini kullanarak .NET sınıf kitaplıkları](functions-dotnet-class-library.md). 

