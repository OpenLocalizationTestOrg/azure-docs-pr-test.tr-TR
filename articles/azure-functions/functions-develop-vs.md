---
title: "Visual Studio kullanarak Azure işlevleri aaaDevelop | Microsoft Docs"
description: "Bilgi nasıl için Visual Studio 2017 Azure işlevleri araçlarını kullanarak toodevelop ve test Azure işlevleri."
services: functions
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: glenga
ms.openlocfilehash: c9baf882bf58068cb9a8930bea337fe51b2a77ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-tools-for-visual-studio"></a>Visual Studio için Azure işlevleri araçları  

Visual Studio 2017 için Azure işlevleri araçları, geliştirme, test ve C# işlevleri tooAzure dağıtmanıza olanak sağlayan Visual Studio için bir uzantısıdır. İlk Azure işlevleri deneyiminizi varsa hakkında daha fazla bilgi edinebilirsiniz [bir giriş tooAzure işlevleri](functions-overview.md).

Hello Azure işlevleri araçları hello aşağıdaki avantajları sağlar: 

* Düzenleme, yapı ve işlevleri yerel geliştirme bilgisayarınızda çalıştırın. 
* Yayımlama Azure işlevlerinizi doğrudan tooAzure proje. 
* Web işleri öznitelikleri toodeclare işlev bağlamaları doğrudan hello tanımları bağlama için ayrı bir function.json Bakımı yerine C# kodu kullanın.
* Geliştirme ve önceden derlenmiş C# işlevleri dağıtın. Önceden derlenmiş işlevleri bir daha iyi soğuk başlangıç daha performans C# betik tabanlı işlevleri sağlar. 
* Visual Studio geliştirme hello yararları tümünün yaparken işlevlerinizi C# kod. 

Bu konu nasıl toouse hello Azure işlevleri araçları Visual Studio 2017 toodevelop için C# işlevlerinizi gösterir. Da bilgi nasıl toopublish, proje tooAzure bir .NET derlemesi olarak.

## <a name="prerequisites"></a>Ön koşullar

Azure işlevleri araçları hello Azure geliştirme iş yükünü dahil [Visual Studio 2017 sürüm 15.3](https://www.visualstudio.com/vs/), veya sonraki bir sürümü. Merhaba eklediğinizden emin olun **Azure geliştirme** Visual Studio 2017 sürüm 15.3 yüklemenizdeki iş yükü:

![Visual Studio 2017 hello Azure geliştirme yüküyle yükleyin](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)

toocreate ve işlevleri dağıtmak, ayrıca gerekir:

* Etkin bir Azure aboneliği. Bir Azure aboneliğiniz yoksa [serbest hesapları](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) kullanılabilir.

* Bir Azure depolama hesabı. toocreate bir depolama hesabı bkz [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account).  
## <a name="create-an-azure-functions-project"></a>Azure işlevleri projesi oluşturma 

[!INCLUDE [Create a project using hello Azure Functions](../../includes/functions-vstools-create.md)]


## <a name="configure-hello-project-for-local-development"></a>Merhaba projeyi yerel geliştirme için yapılandırın

Hello Azure işlevleri şablonunu kullanarak yeni bir proje oluşturduğunuzda, aşağıdaki dosyaları hello içeren boş C# projesinde alın:

* **Host.JSON**: yapılandırmanıza olanak hello işlevleri ana bilgisayar. Bu ayarlar hem de yerel olarak ve Azure içinde çalışırken geçerlidir. Daha fazla bilgi için bkz: [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) başvurusu makalesinde.
    
* **Local.Settings.JSON**: işlevleri yerel olarak çalıştırırken kullanılan ayarları bulundurur. Bu ayarlar, Azure tarafından kullanılmaz, hello tarafından kullanılan [Azure işlevleri çekirdek Araçları](functions-run-local.md). Bağlantı dizeleri tooother Azure gibi bu dosya toospecify ayarları kullanmak Hizmetleri. Yeni bir anahtar toohello ekleme **değerleri** dizi projenizdeki işlevleri gerektirdiği her bağlantı için. Daha fazla bilgi için bkz: [yerel ayarları dosyasına](functions-run-local.md#local-settings-file) hello Azure işlevleri çekirdek araçları konu başlığı.

Merhaba işlevleri çalışma zamanı bir Azure Storage hesabı dahili olarak kullanır. Tüm HTTP ve Web kancalarını dışında türleri tetiklemek için hello ayarlamalısınız **Values.AzureWebJobsStorage** anahtar tooa geçerli Azure depolama hesabı bağlantı dizesi.

[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

 tooset hello depolama hesabı bağlantı dizesi:

1. Visual Studio'da açın **Cloud Explorer**, genişletin **depolama hesabı** > **depolama hesabınız**seçeneğini belirleyip **özellikleri**ve kopyalama hello **birincil bağlantı dizesi** değeri.   

2. Projenizdeki hello local.settings.json proje dosyasını açın ve ayarlayın hello hello değerini **AzureWebJobsStorage** anahtar kopyaladığınız toohello bağlantı dizesi.

3. Merhaba önceki adım tooadd benzersiz anahtarlar toohello yineleyin **değerleri** dizi işlevlerinizi tarafından gereken diğer bağlantılar için.  

## <a name="create-a-function"></a>İşlev oluşturma

Önceden derlenmiş işlevlerde hello işlevi tarafından kullanılan hello bağlamaları hello kodda öznitelikleri uygulama tarafından tanımlanır. İşlevlerinizi sağlanan hello şablonlardan hello Azure işlevleri araçları toocreate kullandığınızda, bu öznitelikler için uygulanır. 

1. **Çözüm Gezgini**’nde, proje düğümünüze sağ tıklayın ve **Yeni** > **Öğe Ekle**’yi seçin. Seçin **Azure işlevi**, bir **adı** hello sınıfı ve tıklatın **Ekle**.

2. Tetikleyici seçin, hello bağlama özelliklerini ayarlama ve tıklatın **oluşturma**. bir kuyruk depolama oluşturma işlevi tetiklendiğinde hello aşağıdaki örnek hello ayarlarını gösterir. 

    ![](./media/functions-develop-vs/functions-vstools-create-queuetrigger.png)
    
    Adlı bir bağlantı dizesi anahtar **QueueStorage** sağlanır, hello local.settings.json dosyasında tanımlanmış. 
 
3. İncelemek hello yeni eklenen sınıfı. Statik bkz **çalıştırmak** ile Merhaba öznitelikli yöntemi, **FunctionName** özniteliği. Bu öznitelik, hello yöntemi hello işlevi için hello giriş noktası olarak gösterir. 

    Örneğin, C# sınıfı aşağıdaki hello temel bir sıra tetiklenen depolama işlevini temsil eder:

    ````csharp
    using System;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Host;
    
    namespace FunctionApp1
    {
        public static class Function1
        {
            [FunctionName("QueueTriggerCSharp")]        
            public static void Run([QueueTrigger("myqueue-items", Connection = "QueueStorage")]string myQueueItem, TraceWriter log)
            {
                log.Info($"C# Queue trigger function processed: {myQueueItem}");
            }
        }
    } 
    ````
 
    Bağlama özgü öznitelik uygulanan tooeach bağlama sağlanan parametresi toohello giriş noktası yöntemidir. Merhaba özniteliği hello bağlama bilgileri parametre olarak alır. Merhaba önceki örnekte hello ilk parametresine sahip bir **QueueTrigger** tetiklenen sıra işlevini belirten uygulanan, öznitelik. Merhaba kuyruk adı ve bağlantı dizesi ayarı adı parametre olarak geçirilir.  

## <a name="testing-functions"></a>İşlevleri test etme

Azure İşlevleri Temel Araçları, Azure İşlevleri projenizi yerel geliştirme bilgisayarınızda çalıştırmanıza olanak sağlar. Bu araçları ilk kez Visual Studio'dan bir işlev başlattığınızda hello istendiğinde tooinstall var.  

tootest işlevinizi, F5 tuşuna basın. İstenirse, Visual Studio toodownload hello isteğini kabul edin ve Azure işlevleri çekirdek (CLI) Araçları'nı yükleyin.  Böylece Hello araçları HTTP isteklerini işleyebilir tooenable bir güvenlik duvarı özel durumu da gerekebilir.

Çalışan hello proje ile dağıtılan işlevi test edersiniz gibi kodunuzu test edebilirsiniz. Daha fazla bilgi için bkz: [Azure işlevleri, kodunuzu test etmek için stratejileri](functions-test-a-function.md). Hata ayıklama modunda çalışırken, kesme noktaları Visual Studio'da beklendiği gibi ulaşıldığından. 

Merhaba nasıl tootest bir sıra işlevi tetiklenen bir örnek için bkz: [tetiklenen sıra işlevi hızlı başlangıç Öğreticisi](functions-create-storage-queue-triggered-function.md#test-the-function).  

hello Azure işlevleri çekirdek araçlarını kullanma hakkında daha fazla toolearn bkz [kod ve yerel olarak Azure işlevlerini test](functions-run-local.md).

## <a name="publish-tooazure"></a>TooAzure yayımlama

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

>[!NOTE]  
>Merhaba local.settings.json eklediğiniz herhangi bir ayarı de toohello işlev uygulaması Azure'da eklenmesi gerekir. Bu ayarlar otomatik olarak eklenmez. Gerekli ayarları tooyour işlev uygulaması şu yollardan biriyle ekleyebilirsiniz:
>
>* [Hello Azure portal kullanarak](functions-how-to-use-azure-function-app-settings.md#settings).
>* [Hello kullanarak `--publish-local-settings` seçeneği yayımlama hello Azure işlevleri çekirdek Araçları](functions-run-local.md#publish).
>* [Hello Azure CLI kullanarak](/cli/azure/functionapp/config/appsettings#set). 

## <a name="next-steps"></a>Sonraki adımlar

Azure işlevleri araçları hakkında daha fazla bilgi için bkz: hello ortak Sorular bölümünü hello [Azure işlevleri için Visual Studio 2017 Araçları](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) blog postası.

toolearn hello Azure işlevleri çekirdek araçları hakkında daha fazla bilgi görmek [kod ve yerel olarak Azure işlevlerini test](functions-run-local.md).  
.NET sınıf kitaplıkları işlevleri geliştirme hakkında daha fazla toolearn bkz [Azure işlevlerini kullanarak .NET sınıf kitaplıkları](functions-dotnet-class-library.md). Bu konu ayrıca nasıl toouse öznitelikleri toodeclare hello bağlamaları Azure işlevleri tarafından desteklenen çeşitli örnekler sağlar.    
