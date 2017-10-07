---
title: Azure Data Lake Store Event Hubs'a aaaCapture verilerden | Microsoft Docs
description: "Olay hub'ları kullanmak Azure Data Lake Store toocapture verileri"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: 09b17bd0b47043bd2c83dba72c01a8064f206a0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-store-toocapture-data-from-event-hubs"></a>Olay hub'ları kullanmak Azure Data Lake Store toocapture verileri

Azure Event Hubs tarafından nasıl toouse Azure Data Lake Store toocapture veri alınan öğrenin.

## <a name="prerequisites"></a>Ön koşullar

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).

* **Bir Azure Data Lake Store hesabı**. Yönergeler için toocreate bir, bkz: [Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md).

*  **Bir olay hub'ları ad alanı**. Yönergeler için bkz: [bir olay hub'ları ad alanı oluşturma](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace). Merhaba Data Lake Store hesabı ve hello olay hub'ları ad hello olduğundan emin olun aynı Azure aboneliği.


## <a name="assign-permissions-tooevent-hubs"></a>İzinleri tooEvent hub'ları atayın

Bu bölümde, olay hub'ları toocapture hello verileri istediğiniz bir klasörde hello hesabı oluşturun. Böylece bir Data Lake Store hesabına veri yazabilirsiniz tooEvent hub'ları da izinleri atayın. 

1. Burada Event Hubs toocapture verilerini istediğiniz ve tıklayın hello Data Lake Store hesabını açın **Veri Gezgini**.

    ![Data Lake Store Veri Gezgini](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store Veri Gezgini")

2.  Tıklatın **yeni klasör** ve toocapture hello veri klasörü için bir ad girin.

    ![Data Lake Store içinde yeni bir klasör oluşturun](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Data Lake Store içinde yeni bir klasör oluşturun")

3. Merhaba Data Lake Store hello kökündeki izinleri atayın. 

    a. Tıklatın **Veri Gezgini**hello kökündeki hello Data Lake Store hesabını seçin ve ardından **erişim**.

    ![Data Lake Store kök izinlerini atamak](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Data Lake Store kök izinlerini atama")

    b. Altında **erişim**, tıklatın **Ekle**, tıklatın **kullanıcı veya Grup Seç**, arayın ve sonra `Microsoft.EventHubs`. 

    ![Data Lake Store kök izinlerini atamak](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Data Lake Store kök izinlerini atama")
    
    **Seç**'e tıklayın.

    c. Altında **izinleri atamak**, tıklatın **Select izinleri**. Ayarlama **izinleri** çok**yürütme**. Ayarlama **eklemek** çok**bu klasör ve tüm alt öğeleri**. Ayarlama **olarak eklemek** çok**erişim izni girdisi ve varsayılan izin girdisi**.

    ![Data Lake Store kök izinlerini atamak](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Data Lake Store kök izinlerini atama")

    **Tamam** düğmesine tıklayın.

4. Data Lake Store hesabı altında toocapture verilerin istediğiniz hello klasör izinlerini atayın.

    a. Tıklatın **Veri Gezgini**hello Data Lake Store hesabına başlangıç klasörü seçin ve ardından **erişim**.

    ![Data Lake Store klasör izinlerini atamak](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Data Lake Store klasörün izinlerini atama")

    b. Altında **erişim**, tıklatın **Ekle**, tıklatın **kullanıcı veya Grup Seç**, arayın ve sonra `Microsoft.EventHubs`. 

    ![Data Lake Store klasör izinlerini atamak](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Data Lake Store klasörün izinlerini atama")
    
    **Seç**'e tıklayın.

    c. Altında **izinleri atamak**, tıklatın **Select izinleri**. Ayarlama **izinleri** çok**okuma, yazma,** ve **yürütme**. Ayarlama **eklemek** çok**bu klasör ve tüm alt öğeleri**. Son olarak, ayarlamak **olarak eklemek** çok**erişim izni girdisi ve varsayılan izin girdisi**.

    ![Data Lake Store klasör izinlerini atamak](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Data Lake Store klasörün izinlerini atama")
    
    **Tamam** düğmesine tıklayın. 

## <a name="configure-event-hubs-toocapture-data-toodata-lake-store"></a>Olay hub'ları toocapture veri tooData Lake deposu yapılandırma

Bu bölümde, bir olay hub'ları ad alanı içindeki bir Event Hub oluşturun. Merhaba olay hub'ı toocapture veri tooan Azure Data Lake Store hesabını yapılandırmanız da. Bu bölümde, bir olay hub'ları ad alanı zaten oluşturduğunuzu varsayar.

2. Merhaba gelen **genel bakış** hello olay hub'ları ad alanının bölmesi **+ olay hub'ı**.

    ![Olay hub'ı oluşturma](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "olay hub'ı Oluştur")

3. Tooconfigure olay hub'ları toocapture veri tooData Lake deposu Hello aşağıdaki değerleri belirtin.

    ![Olay hub'ı oluşturma](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "olay hub'ı Oluştur")

    a. Merhaba Event Hub için bir ad sağlayın.
    
    b. Bu öğretici için ayarlanmış **bölüm sayısı** ve **ileti bekletme** toohello varsayılan değerleri.
    
    c. Ayarlama **yakalama** çok**üzerinde**. Set hello **zaman penceresi** (ne sıklıkta toocapture) ve **boyutu penceresi** (veri boyutu toocapture). 
    
    d. İçin **yakalama sağlayıcısı**seçin **Azure Data Lake Store** ve hello seçin hello daha önce oluşturduğunuz Data Lake Store. İçin **Data Lake yolu**, hello hello Data Lake Store hesabı oluşturduğunuz hello klasörün adını girin. Yalnızca tooprovide hello göreli yol toohello klasörü gerekir.

    e. Merhaba bırakın **örnek yakalama dosyası adı biçimlerini** toohello varsayılan değeri. Bu seçenek hello yakalama klasörü altında oluşturulan hello klasör yapısını yönetir.

    f. **Oluştur**'a tıklayın.

## <a name="test-hello-setup"></a>Test hello Kurulumu

Şimdi veri toohello Azure olay hub'ı göndererek hello çözüm test edebilirsiniz. Merhaba yönergeleri izleyin [tooAzure olay hub'ları olayları göndermek](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md). Merhaba veri göndermeye başla sonra belirttiğiniz hello klasör yapısını kullanarak Data Lake Store'da yansıtılan hello veri bakın. Örneğin, bir klasör yapısı hello ekran, Data Lake Store aşağıdaki gösterildiği gibi görürsünüz.

![Data Lake Store'da EventHub veri örneği](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Data Lake Store'da örnek EventHub veri")

> [!NOTE]
> Event Hubs'a gelen iletileri yoksa bile, olay hub'ları yalnızca hello üstbilgileri boş dosyalarıyla Data Lake Store hesabı hello yazar. Merhaba dosyaları hello aynı yazılır hello olay hub'ları oluştururken sağladığınız zaman aralığı.
> 
>

## <a name="analyze-data-in-data-lake-store"></a>Data Lake Store'da verileri analiz etme

Merhaba veri Data Lake Store içinde olduğunda tooprocess ve crunch hello veri analitik işleri çalıştırabilirsiniz. Bkz: [USQL Avro örnek](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) nasıl toodo bu Azure Data Lake Analytics'i kullanarak.
  

## <a name="see-also"></a>Ayrıca bkz.
* [Data Lake Store'da verilerin güvenliğini sağlama](data-lake-store-secure-data.md)
* [Azure Storage Blobları tooData Lake Mağazası'ndan veri kopyalama](data-lake-store-copy-data-azure-storage-blob.md)
