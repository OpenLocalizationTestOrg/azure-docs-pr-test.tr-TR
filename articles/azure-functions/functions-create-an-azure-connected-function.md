---
title: "aaaCreate tooAzure Hizmetleri bağlanan bir işlev | Microsoft Docs"
description: "Azure işlevleri toocreate tooother Azure bağlayan sunucusuz bir uygulama kullanın Hizmetleri."
services: functions
documentationcenter: dev-center-name
author: yochay
manager: manager-alias
editor: 
tags: 
keywords: "azure işlevleri, işlevler, olay işleme, web kancaları, dinamik işlem, sunucusuz mimari"
ms.assetid: ab86065d-6050-46c9-a336-1bfc1fa4b5a1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 9d1f7d3b236f8d2c1a404c76aee410f6d458fb7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-toocreate-a-function-that-connects-tooother-azure-services"></a>Azure işlevleri toocreate tooother Azure bağlanan bir işlev kullanan hizmetler

Bu konu, nasıl Azure Storage bir tabloda toorows toocreate toomessages bir Azure depolama kuyruğu ve kopya hello üzerinde dinler Azure işlevleri işlevinde iletileri gösterir. Kullanılan tooload iletileri hello kuyruğuna tetiklenen Zamanlayıcı işlevdir. İkinci bir işlev hello kuyruktaki iletileri okur ve iletileri toohello tablo yazar. Merhaba kuyruk ve hello tablo sizin için Azure hello bağlama tanımları tabanlı işlevleri tarafından oluşturulur. 

toomake şeyleri daha ilginç, bir işlev JavaScript'te yazılmış ve hello diğer C# kodda yazılır. Bu durum bir işlev uygulamasının nasıl çeşitli dillerde işlevleri olabileceğini gösterir. 

Bu senaryoyu [Kanal 9’daki bir videoda](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player) görebilirsiniz.

## <a name="create-a-function-that-writes-toohello-queue"></a>Toohello sıra Yazar bir işlev oluşturun

Tooa depolama kuyruğu bağlanmadan önce toocreate hello ileti sırası yükleyen işlevi gerekir. Bu JavaScript işlevi 10 saniyede bir ileti toohello sırası yazan Zamanlayıcı tetikleyicisi kullanır. Zaten bir Azure hesabınız yoksa, hello denetleyin [deneyin Azure işlevleri](https://functions.azure.com/try) deneyimi veya [ücretsiz Azure hesabınızı oluşturmak](https://azure.microsoft.com/free/).

1. Toohello Azure portalına gidin ve işlev uygulamanızı bulun.

2. **Yeni İşlev** > **TimerTrigger-JavaScript** seçeneğine tıklayın. 

3. Ad hello işlevi **FunctionsBindingsDemo1**, cron ifade değeri girin `0/10 * * * * *` için **zamanlama**ve ardından **oluşturma**.
   
    ![Zamanlayıcı ile tetiklenen işlev ekleme](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    10 saniyede bir çalışan zamanlayıcı tetiklemeli bir işlev oluşturdunuz.

5. Merhaba üzerinde **geliştirme** sekmesini tıklatın, **günlükleri** ve hello günlüğü'nde hello etkinlik görüntüleyin. 10 saniyede bir yazılmış bir günlük girişi göreceksiniz.
   
    ![Görünüm hello günlük tooverify hello işlevi çalışır](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a>İleti kuyruğu çıktı bağlaması ekleme

1. Merhaba üzerinde **tümleştir** sekmesinde, seçin **yeni çıktı** > **Azure kuyruk depolama** > **seçin**.

    ![Tetikleyici zamanlayıcı işlevi ekleme](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. Girin `myQueueItem` için **ileti parametre adı** ve `functions-bindings` için **sıra adı**, var olan seçin **depolama hesabı bağlantısı** veya tıklatın**yeni** bir depolama hesabı bağlantı ve ardından toocreate **kaydetmek**.  

    ![Merhaba çıkış bağlama toohello depolama kuyruğu oluşturma](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. Merhaba edilene **geliştirme** sekmesinde, aşağıdaki kod toohello işlevi hello Ekle:
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. Merhaba bulun *varsa* deyimi yaklaşık hello işlevinin 9 satır ve INSERT hello aşağıdaki kod bu deyim sonra.
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    Bu kod oluşturur bir **myQueueItem** ve ayarlar kendi **zaman** özelliği toohello geçerli zaman damgası. Ardından hello yeni kuyruk öğesi toohello bağlamın ekler **myQueueItem** bağlama.

3. **Kaydet ve Çalıştır**’a tıklayın.

## <a name="view-storage-updates-by-using-storage-explorer"></a>Depolama Gezgini'ni kullanarak depolama güncelleştirmelerini görüntüleme
İşlevinizi oluşturduğunuz hello kuyrukta iletileri görüntüleyerek çalışıp çalışmadığını doğrulayabilirsiniz.  Visual Studio'da bulut Gezgini'ni kullanarak tooyour depolama kuyruğu bağlanabilir. Ancak, hello portal kolay tooconnect tooyour depolama hesabı Microsoft Azure Storage Gezgini kullanarak kolaylaştırır.

1. Merhaba, **tümleştir** sekmesini ve ardından sıranız bağlama çıktı > **belgelerine**, ardından depolama hesabınız için bağlantı dizesi hello Göster ve kopyalama hello değeri. Bu değer tooconnect tooyour depolama hesabı kullanın.

    ![Azure Depolama Gezgini’ni İndir](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. Henüz yapmadıysanız [Microsoft Azure Depolama Gezgini](http://storageexplorer.com)’ni indirip yükleyin. 
 
3. Depolama Gezgini'nde hello tıklayın Bağlan tooAzure depolama simgesi, hello alanında hello bağlantı dizesini yapıştırın ve hello Sihirbazı tamamlayın.

    ![Depolama Gezgini ile bağlantı ekleme](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. Altında **yerel ve bağlı**, genişletin **depolama hesapları** > depolama hesabınız > **sıraları** > **işlevleri bağlamaları**ve iletileri toohello sıraya yazılan doğrulayın.

    ![Merhaba sıradaki iletiler görünümü](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    Merhaba sıra yok veya boş bırakılırsa, da büyük olasılıkla işlev bağlama veya kod ile ilgili bir sorun yoktur.

## <a name="create-a-function-that-reads-from-hello-queue"></a>Merhaba kuyruktaki iletileri okur bir işlev oluşturun

Toohello sıraya eklenen iletileri sahip olduğunuza göre yazma hello kalıcı olarak tooan Azure depolama tablosu iletileri ve hello kuyruktaki iletileri okur başka bir işlev oluşturabilirsiniz.

1. **Yeni İşlev** > **QueueTrigger-CSharp** seçeneğine tıklayın. 
 
2. Ad hello işlevi `FunctionsBindingsDemo2`, girin **işlevleri bağlamaları** hello içinde **sıra adı** alan, mevcut bir depolama hesabını seçin veya oluşturun ve ardından **oluşturma**.

    ![Çıkış kuyruğu zamanlayıcı işlevi ekleme](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. (İsteğe bağlı) Merhaba yeni işlev önce Depolama Gezgini hello yeni kuyruk görüntüleyerek çalıştığını doğrulayabilirsiniz. Ayrıca Visual Studio’daki Bulut Gezgini’ni kullanabilirsiniz.  

4. (İsteğe bağlı) Merhaba yenileme **işlevleri bağlamaları** sıraya ve öğeler hello sıradan kaldırıldı dikkat edin. Merhaba işlevi ilişkili toohello hello kaldırma oluşur **işlevleri bağlamaları** sıraya giriş tetikleyici ve hello işlevi hello sıra okuduğu. 
 
## <a name="add-a-table-output-binding"></a>Tablo çıktı bağlaması ekleme

1. FunctionsBindingsDemo2 içinde **Tümleştir** > **Yeni Çıkış** > **Azure Tablo Depolama** > **Seç** seçeneklerine tıklayın.

    ![Bağlama tooan Azure Storage tablo ekleme](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. **Tablo adı** için `functionbindings` ve **Tablo parametre adı** için `myTable` girin, bir **Depolama hesabı bağlantısı** seçin ya da yeni bir tane oluşturun ve ardından **Kaydet**’e tıklayın.

    ![Merhaba depolama tablo bağlaması yapılandırma](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. Merhaba, **geliştirme** sekmesinde, hello varolan işlev kodu hello şununla değiştirin:
   
    ```cs
    
    using System;
    
    public static void Run(QItem myQueueItem, ICollector<TableItem> myTable, TraceWriter log)
    {    
        TableItem myItem = new TableItem
        {
            PartitionKey = "key",
            RowKey = Guid.NewGuid().ToString(),
            Time = DateTime.Now.ToString("hh.mm.ss.ffffff"),
            Msg = myQueueItem.Msg,
            OriginalTime = myQueueItem.Time    
        };
        
        // Add hello item toohello table binding collection.
        myTable.Add(myItem);
    
        log.Verbose($"C# Queue trigger function processed: {myItem.RowKey} | {myItem.Msg} | {myItem.Time}");
    }
    
    public class TableItem
    {
        public string PartitionKey {get; set;}
        public string RowKey {get; set;}
        public string Time {get; set;}
        public string Msg {get; set;}
        public string OriginalTime {get; set;}
    }
    
    public class QItem
    {
        public string Msg { get; set;}
        public string Time { get; set;}
    }
    ```
    Merhaba **Tableıtem** sınıfı hello depolama tablosunda bir satırı temsil eder ve hello öğesi toohello ekleyin `myTable` koleksiyonu **Tableıtem** nesneleri. Merhaba ayarlamalısınız **PartitionKey** ve **RowKey** özellikleri toobe mümkün tooinsert hello tabloya.

4. **Kaydet** düğmesine tıklayın.  Son olarak, Depolama Gezgini veya Visual Studio Cloud Explorer hello tablo görüntüleyerek hello işlevi works doğrulayabilirsiniz.

5. (İsteğe bağlı) Depolama Gezgini'nde, depolama hesabınızı içinde **tabloları** > **functionsbindings** ve satır toohello tablo eklendiğini doğrulayın. Yapabileceğiniz aynı Visual Studio Cloud Explorer'da hello.

    ![Merhaba tablosundaki satırları görünümü](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    Merhaba tablo yok veya boş bırakılırsa, da büyük olasılıkla işlev bağlama veya kod ile ilgili bir sorun yoktur. 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a>Sonraki adımlar
Azure işlevleri hakkında daha fazla bilgi için aşağıdaki konularda hello bakın:

* [Azure İşlevleri geliştirici başvurusu](functions-reference.md)  
  İşlevleri kodlamak ve tetikleyicileri ve bağlamaları tanımlamak için programcı başvurusu
* [Azure İşlevlerini test etme](functions-test-a-function.md)  
  İşlevlerinizi test etmek için çeşitli araçları ve teknikleri açıklar.
* [Nasıl tooscale Azure işlevleri](functions-scale.md)  
  Merhaba tüketim barındırma planı ve nasıl toochoose hello doğru planın dahil olmak üzere Azure işlevlerinde kullanılabilen hizmet planlarını açıklanır. 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

