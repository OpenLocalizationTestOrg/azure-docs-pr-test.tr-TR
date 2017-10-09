---
title: "aaaAzure olay hub'ları yakalama portal üzerinden etkinleştirme | Microsoft Docs"
description: "Hello Azure portal kullanarak hello olay hub'ları yakalama özelliğini etkinleştirin."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: 27c7528552c497a4d98873a22bd56a991c66247c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-event-hubs-capture-using-hello-azure-portal"></a>Olay hub'ları hello Azure portal kullanarak yakalama etkinleştir

Yakalama hello kullanarak hello olay hub'ı oluşturma zamanında yapılandırabilirsiniz [Azure portal](https://portal.azure.com). Her iki yakalama hello veri tooan Azure yapabilecekleriniz [Blob storage](https://azure.microsoft.com/services/storage/blobs/) kapsayıcı ya da tooan [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) hesabı.

## <a name="capture-data-tooan-azure-storage-account"></a>Yakalama veri tooan Azure depolama hesabı  

Bir olay hub'ı oluşturduğunuzda hello tıklatarak yakalama etkinleştirebilirsiniz **üzerinde** hello düğmesini **Event Hub'ı oluşturma** portal dikey. Ardından bir depolama hesabı ve kapsayıcı tıklayarak belirttiğiniz **Azure Storage** hello içinde **yakalama sağlayıcısı** kutusu. Olay hub'ları yakalama hizmeti için kimlik doğrulaması ile depolama kullandığından, toospecify bir depolama bağlantı dizesi gerekmez. Merhaba kaynak seçici hello kaynak URI'si depolama hesabınız için otomatik olarak seçer. Azure Resource Manager kullanıyorsanız bu URI'yi dize olarak açıkça belirtmeniz gerekir.

Merhaba varsayılan zaman penceresi 5 dakikadır. Hello en düşük değer 1, en fazla 15 hello olur. Merhaba **boyutu** penceresine sahip bir dizi 10-500 MB.

![][1]

## <a name="capture-data-tooan-azure-data-lake-store-account"></a>Veri tooan Azure Data Lake Store hesabı yakalama

toocapture veri tooAzure Data Lake Store, bir Data Lake Store hesabı ve bir olay hub'ı oluşturun:

### <a name="create-an-azure-data-lake-store-account-and-folders"></a>Azure Data Lake Store hesabı ve klasörleri oluşturma

1. Merhaba yönergeleri izleyerek bir Data Lake Store hesabı oluşturma [Azure Data Lake hello Azure portal kullanarak Store ile çalışmaya başlama](../data-lake-store/data-lake-store-get-started-portal.md). 
2. Merhaba hello yönergeleri izleyerek bu hesap altında bir klasör oluşturun [Azure Data Lake Store hesabında klasör oluşturma](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) bölümü.
3. Merhaba Data Lake Store hesabı dikey penceresinde tıklayın **Veri Gezgini**.
4. **Erişim**’e tıklayın.
5. **Ekle**'ye tıklayın.
6. Merhaba, **arama adına veya e-posta** kutusuna **Microsoft.EventHubs** ve bu seçeneği belirleyin. 
7. Merhaba **izinleri** sekmesi görüntülenir. Merhaba izinleri hello aşağıdaki şekilde gösterildiği gibi ayarlayın:

    ![][6]

8. **Tamam** düğmesine tıklayın.
9. Şimdi, toohello hedef klasör gözatma ve hello klasör adını tıklatarak hello kök klasöründe bir klasör oluşturun.
10. **Erişim**’e tıklayın.
11. **Ekle**'ye tıklayın.
12. Merhaba, **arama adına veya e-posta** kutusuna **Microsoft.EventHubs** ve bu seçeneği belirleyin.
13. Merhaba **izinleri** yeniden sekmesi görüntülenir. Merhaba izinleri hello aşağıdaki şekilde gösterildiği gibi ayarlayın:

    ![][5]

### <a name="create-an-event-hub"></a>Olay hub’ı oluşturma

1. Bu hello olay hub'ın hello olmalıdır Not hello Azure Data Lake Store, yeni oluşturduğunuz aynı Azure abonelik. Merhaba tıklatarak oluşturma hello olay hub'ı **üzerinde** altında düğmesini **yakalama** hello içinde **Event Hub'ı oluşturma** portal dikey. 
2. Merhaba, **Event Hub'ı oluşturma** portal dikey penceresinde, seçin **Azure Data Lake Store** hello gelen **yakalama sağlayıcısı** kutusu.
3. İçinde **seçin Data Lake Store**, hello önceden ve hello oluşturduğunuz Data Lake Store hesabı belirtin **Data Lake yolu** alanında, oluşturduğunuz hello yolu toohello veri klasörü girin.

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a>Mevcut bir olay hub'ında Yakalama özelliğini yapılandırma

Event Hubs ad alanlarında mevcut olan olay hub'ları üzerinde Yakalama özelliğini yapılandırabilirsiniz. tooenable bir var olan olay hub'ı veya toochange yakalama ayarlarınızı yakalama, hello ad alanı tooload hello tıklatın **Essentials** dikey penceresinde, kendisi için tooenable istediğiniz veya hello yakalama ayarını hello olay hub'ı tıklatın. Son olarak, hello tıklatın **özellikleri** hello bölümünü dikey penceresini açın ve ardından hello rakamları aşağıdaki gösterildiği gibi hello yakalama ayarları düzenleyin:

### <a name="azure-blob-storage"></a>Azure Blob Depolama

![][2]

### <a name="azure-data-lake-store"></a>Azure Data Lake Store

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a>Sonraki adımlar

Dilerseniz Azure Resource Manager şablonlarını kullanarak da Event Hubs Yakalama özelliğini yapılandırabilirsiniz. Daha fazla bilgi için bkz. [Azure Resource Manager şablonu kullanarak Yakalama özelliğini etkinleştirme](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).
