---
title: "Depolama Gezgini (Önizleme) ile aaaManage Azure Blob Storage kaynaklarını | Microsoft Docs"
description: "Azure Blob kapsayıcılar ve Bloblar Depolama Gezgini (Önizleme) ile yönetme"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 2f09e545-ec94-4d89-b96c-14783cc9d7a9
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 503dd061b205875da127378ab48e8d465800fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a>Depolama Gezgini (Önizleme) ile Azure Blob Storage kaynaklarını yönetme
## <a name="overview"></a>Genel Bakış
[Azure Blob Storage](storage/blobs/storage-dotnet-how-to-use-blobs.md) büyük miktarda gelen herhangi bir yere Merhaba Dünya HTTP veya HTTPS üzerinden erişilebilen metin veya ikili veriler gibi yapılandırılmamış veriyi depolamak için bir hizmettir.
Blob Depolama tooexpose verileri kullanabileceğiniz genel olarak toohello world veya toostore uygulama verilerini özel olarak. Bu makalede, bilgi edineceksiniz nasıl toouse Depolama Gezgini (Önizleme) toowork blob kapsayıcılar ve bloblar ile.

## <a name="prerequisites"></a>Ön koşullar
Bu makaledeki toocomplete hello adımları, hello aşağıdakiler gerekir:

* [Depolama Gezgini (önizleme) indirip yükleme](http://www.storageexplorer.com)
* [Tooa Azure depolama hesabı veya hizmetine bağlanmak](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a>Bir blob kapsayıcı oluşturun
Tüm BLOB'lar BLOB'ları yalnızca mantıksal bir gruplandırması olan bir blob kapsayıcısında bulunmalıdır. Bir hesapta sınırsız sayıda kapsayıcı olabilir ve her kapsayıcı sınırsız sayıda BLOB depolayabilirsiniz.

Merhaba aşağıdaki adımları göstermek nasıl toocreate bir blob kapsayıcısına Depolama Gezgini (Önizleme).

1. Depolama Gezgini’ni (Önizleme) açın.
2. Merhaba sol bölmede toocreate hello blob kapsayıcısı içinde istediğiniz hello depolama hesabı'nı genişletin.
3. Sağ **Blob kapsayıcıları**ve - hello bağlam menüsünden - seçin **Blob kapsayıcısı oluşturmak**.

   ![BLOB kapsayıcıları bağlam menüsü oluşturma][0]
4. Bir metin kutusu altında hello görünür **Blob kapsayıcıları** klasör. Blob kapsayıcısı için Hello ad girin. Merhaba bkz [kapsayıcı adlandırma kurallarını](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) bölümünde bir liste için kurallar ve blob kapsayıcı adlandırma kısıtlamaları.

   ![BLOB kapsayıcıları metin kutusu oluşturma][1]
5. Tuşuna **Enter** toocreate hello blob kapsayıcısı, tamamlandığında veya **Esc** toocancel. Merhaba blob kapsayıcısı başarıyla oluşturulduktan sonra uygulamanın altında hello görüntülenecek **Blob kapsayıcıları** klasörü hello için seçtiğiniz depolama hesabı.

   ![Blob kapsayıcısı oluşturuldu][2]

## <a name="view-a-blob-containers-contents"></a>Bir blob kapsayıcının içeriğini görüntüleme
BLOB kapsayıcıları, blobları ve (Ayrıca BLOB içerebilir) klasörleri içerir.

Merhaba aşağıdaki adımları göstermek nasıl Depolama Gezgini (Önizleme) bir blob kapsayıcısına tooview Merhaba içeriğine:

1. Depolama Gezgini’ni (Önizleme) açın.
2. Merhaba sol bölmede, tooview istediğiniz hello blob kapsayıcısı içeren hello depolama hesabı'nı genişletin.
3. Merhaba depolama hesabının genişletin **Blob kapsayıcıları**.
4. Sağ hello blob kapsayıcısı, tooview istiyor ve - hello bağlam menüsünden - seçin **açık Blob kapsayıcı Düzenleyicisi**.
   Ayrıca tooview istediğiniz hello blob kapsayıcısı çift tıklatabilirsiniz.

   ![Açık blob kapsayıcı Düzenleyicisi bağlam menüsü][19]
5. Merhaba ana bölmede hello blob kapsayıcısının içeriğini görüntüler.

   ![BLOB kapsayıcı Düzenleyicisi][3]

## <a name="delete-a-blob-container"></a>Bir blob kapsayıcısından silin
BLOB kapsayıcıları kolayca oluşturulur ve gerektiğinde silinir. (nasıl toodelete tek BLOB, toosee toohello bölümüne başvurun [blob kapsayıcısı içinde BLOB'ları yönetme](#managing-blobs-in-a-blob-container).)

Merhaba aşağıdaki adımları göstermek nasıl toodelete bir blob kapsayıcısına Depolama Gezgini (Önizleme):

1. Depolama Gezgini’ni (Önizleme) açın.
2. Merhaba sol bölmede, tooview istediğiniz hello blob kapsayıcısı içeren hello depolama hesabı'nı genişletin.
3. Merhaba depolama hesabının genişletin **Blob kapsayıcıları**.
4. Sağ hello blob kapsayıcısı, toodelete istiyor ve - hello bağlam menüsünden - seçin **silmek**.
   Tuşlarına da basabilirsiniz **silmek** toodelete hello şu anda seçili blob kapsayıcısı.

   ![BLOB kapsayıcı bağlam menüsü Sil][4]
5. Seçin **Evet** toohello onay iletişim kutusu.

   ![BLOB kapsayıcı onay Sil][5]

## <a name="copy-a-blob-container"></a>Bir blob kapsayıcısını kopyalayın
Depolama Gezgini (Önizleme) toocopy bir blob kapsayıcı toohello Pano ve kapsayıcı içinde başka bir depolama hesabı blob sonra Yapıştır sağlar. (nasıl toocopy tek BLOB, toosee toohello bölümüne başvurun [blob kapsayıcısı içinde BLOB'ları yönetme](#managing-blobs-in-a-blob-container).)

Aşağıdaki adımları hello nasıl toocopy bir blob kapsayıcısından bir depolama hesabı tooanother gösterilmektedir.

1. Depolama Gezgini’ni (Önizleme) açın.
2. Merhaba sol bölmede, toocopy istediğiniz hello blob kapsayıcısı içeren hello depolama hesabı'nı genişletin.
3. Merhaba depolama hesabının genişletin **Blob kapsayıcıları**.
4. Sağ hello blob kapsayıcısı, toocopy istiyor ve - hello bağlam menüsünden - seçin **kopyalama Blob kapsayıcısı**.

   ![Kopya blob kapsayıcı bağlam menüsü][6]
5. Hangi içine, toopaste hello blob kapsayıcısı istediğiniz - hello bağlam menüsünden - seçin hello istenen "hedef" depolama hesabını sağ tıklatıp **Yapıştır Blob kapsayıcısı**.

   ![Yapıştır blob kapsayıcı bağlam menüsü][7]

## <a name="get-hello-sas-for-a-blob-container"></a>Blob kapsayıcısı için Hello SAS alma
A [paylaşılan erişim imzası (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) depolama hesabınızda atanmış erişim tooresources sağlar.
Başka bir deyişle, bir istemci depolama hesabınızdaki izinleri tooobjects süre ve belirtilen bir izin kümesi ile belirli bir süre için hesap erişim tuşlarınızı paylaşmak zorunda kalmadan sınırlı verebilirsiniz.

Merhaba aşağıdaki adımları göstermek nasıl toocreate bir blob kapsayıcı için bir SAS:

1. Depolama Gezgini’ni (Önizleme) açın.
2. Hello sol bölmesinde, SAS tooget öğrenmek isterseniz hello blob kapsayıcısı içeren hello depolama hesabı'nı genişletin.
3. Merhaba depolama hesabının genişletin **Blob kapsayıcıları**.
4. Merhaba istenen blob kapsayıcısına sağ tıklayın ve - hello bağlam menüsünden - seçin **paylaşılan erişim imzası Al**.

   ![SAS bağlam menüsü Al][8]
5. Merhaba, **paylaşılan erişim imzası** iletişim kutusunda, hello İlkesi, başlangıç ve sona erme tarihleri, saat dilimini belirtin ve erişim düzeyleri hello kaynak için istediğiniz.

   ![SAS seçenekleri Al][9]
6. Merhaba SAS seçeneklerini belirtme tamamladığınızda seçin **oluşturma**.
7. İkinci bir **paylaşılan erişim imzası** iletişim listeleri hello hello URL yanı sıra blob kapsayıcısı ve tooaccess kullanabileceğiniz QueryStrings hello depolama kaynağı sonra görüntülenir.
   Seçin **kopya** toocopy toohello Pano istediğiniz sonraki toohello URL.

   ![SAS URL'leri Kopyala][10]
8. İşiniz bittiğinde **Kapat**’ı seçin.

## <a name="manage-access-policies-for-a-blob-container"></a>Blob kapsayıcısı için erişim ilkelerini yönetme
Merhaba aşağıdaki adımları göstermek nasıl toomanage (ekleme ve kaldırma) erişim ilkeleri blob kapsayıcısı için:

1. Depolama Gezgini’ni (Önizleme) açın.
2. Merhaba sol bölmede hello depolama hesabı erişim ilkeleri toomanage istediğiniz hello blob kapsayıcısı içeren genişletin.
3. Merhaba depolama hesabının genişletin **Blob kapsayıcıları**.
4. Merhaba istenen blob kapsayıcısı seçip - hello bağlam menüsünden - **erişim ilkelerini Yönet**.

   ![Erişim ilkelerini yönet bağlam menüsü][11]
5. Merhaba **erişim ilkeleri** iletişim hello seçili blob kapsayıcısı için oluşturulmuş tüm erişim ilkeleri listeler.

   ![Erişim ilkesi seçenekleri][12]        
6. Merhaba erişim ilkesi yönetim görevi bağlı olarak aşağıdaki adımları izleyin:

   * **Yeni bir erişim ilkesi ekleme** - **Ekle**’yi seçin. Oluşturduktan sonra hello **erişim ilkeleri** iletişim yeni eklenen hello görüntüler erişim ilkesi (varsayılan ayarlarla).
   * **Bir erişim ilkesi Düzenle** - istenen tüm düzenlemeleri yapın ve seçin **kaydetmek**.
   * **Erişim ilkesini kaldırmak** - seçin **kaldırmak** tooremove istediğiniz sonraki toohello erişim ilkesi.

## <a name="set-hello-public-access-level-for-a-blob-container"></a>Blob kapsayıcısı için Hello genel erişim düzeyini ayarlama
Varsayılan olarak, her blob kapsayıcısı çok ayarlanır "Genel erişim yok".

Merhaba aşağıdaki adımları nasıl toospecify genel erişim gösteren bir blob kapsayıcısı için düzeyi.

1. Depolama Gezgini’ni (Önizleme) açın.
2. Merhaba sol bölmede hello depolama hesabı erişim ilkeleri toomanage istediğiniz hello blob kapsayıcısı içeren genişletin.
3. Merhaba depolama hesabının genişletin **Blob kapsayıcıları**.
4. Merhaba istenen blob kapsayıcısı seçip - hello bağlam menüsünden - **genel erişim düzeyi ayarlanan**.

   ![Genel erişim düzeyi bağlam menüsü Ayarla][13]
5. Merhaba, **kapsayıcısı genel erişim düzeyi ayarlanan** iletişim kutusunda, istenen hello erişim düzeyini belirtin.

   ![Genel erişim düzeyi seçeneklerini ayarlama][14]
6. **Uygula**’yı seçin.

## <a name="managing-blobs-in-a-blob-container"></a>Blob kapsayıcısı içinde BLOB'ları yönetme
Bir blob kapsayıcısını oluşturduktan sonra bir blob toothat blob kapsayıcı karşıya yükleme, bir blob tooyour yerel bilgisayarda indirin, yerel bilgisayarınıza ve çok daha fazlasını bir blob açın.

Aşağıdaki adımları hello nasıl toomanage hello BLOB'lar (ve klasörler) bir blob kapsayıcısına gösterilmektedir.

1. Depolama Gezgini’ni (Önizleme) açın.
2. Merhaba sol bölmede, toomanage istediğiniz hello blob kapsayıcısı içeren hello depolama hesabı'nı genişletin.
3. Merhaba depolama hesabının genişletin **Blob kapsayıcıları**.
4. Merhaba blob kapsayıcısı tooview istediğiniz çift tıklayın.
5. Merhaba ana bölmede hello blob kapsayıcısının içeriğini görüntüler.

   ![Görünüm blob kapsayıcısı][3]
6. Merhaba ana bölmede hello blob kapsayıcısının içeriğini görüntüler.
7. Tooperform istediğiniz Hello göreve bağlı olarak aşağıdaki adımları izleyin:

   * **Dosyaları tooa blob kapsayıcısı karşıya yükle**

     1. Merhaba ana bölmede ait araç çubuğunda seçin **karşıya**ve ardından **dosya yükleme** hello açılan menüsünden.

        ![Dosya menüsü karşıya yükle][15]
     2. Merhaba, **dosyaları karşıya yükleme** iletişim, select hello üç nokta (**...** ) düğmesini hello hello sağ tarafındaki **dosyaları** metin kutusu tooselect hello dosyaları tooupload istiyor.

        ![Karşıya yükleme seçenekleri dosyaları][16]
     3. Merhaba türünü belirtin **Blob türü**. Merhaba makale [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) çeşitli blob türü hello hello arasındaki farklar açıklanmaktadır.
     4. İsteğe bağlı olarak, içine hello seçili dosyaları karşıya yükleneceği bir hedef klasör belirtin. Merhaba hedef klasörü yoksa, oluşturulur.
     5. **Karşıya Yükle**’yi seçin.
   * **Bir klasör tooa blob kapsayıcı karşıya yükle**

     1. Merhaba ana bölmede ait araç çubuğunda seçin **karşıya**ve ardından **karşıya yükleme klasörü** hello açılan menüsünden.

        ![Klasörü karşıya yükle menüsü][17]
     2. Merhaba, **karşıya yükleme klasörü** iletişim, select hello üç nokta (**...** ) düğmesini hello hello sağ tarafındaki **klasörü** içeriği tooupload istediğiniz metin kutusu tooselect hello klasörü.

        ![Klasör Seçenekleri karşıya yükle][18]
     3. Merhaba türünü belirtin **Blob türü**. Merhaba makale [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) çeşitli blob türü hello hello arasındaki farklar açıklanmaktadır.
     4. İsteğe bağlı olarak, hangi hello seçilen klasörün içeriğini karşıya yükleneceği bir hedef klasör belirtin. Merhaba hedef klasörü yoksa, oluşturulur.
     5. **Karşıya Yükle**’yi seçin.
   * **Bir blob tooyour yerel bilgisayarda indirin**

     1. Merhaba blob toodownload istediğiniz seçin.
     2. Merhaba ana bölmede ait araç çubuğunda seçin **karşıdan**.
     3. Merhaba, **toosave hello blob indirdiğiniz belirt** iletişim kutusunda, indirilen hello blob hello konumu belirtin ve hello toogive istediğiniz adı.  
     4. **Kaydet**’i seçin.
   * **Yerel bilgisayarınızda bir blob açın**

     1. Merhaba blob tooopen istediğiniz seçin.
     2. Merhaba ana bölmede ait araç çubuğunda seçin **açık**.
     3. Merhaba blob indirilir ve hello blob'un temel alınan dosya türü ile ilişkili hello uygulama kullanılarak açılır.
   * **Bir blob toohello Panoya Kopyala**

     1. Merhaba blob toocopy istediğiniz seçin.
     2. Merhaba ana bölmede ait araç çubuğunda seçin **kopya**.
     3. Merhaba sol bölmede tooanother blob kapsayıcısı gidin ve çift tooview hello ana bölmede içinde.
     4. Merhaba ana bölmede ait araç çubuğunda seçin **Yapıştır** toocreate hello blob kopyalama.
   * **Bir blob Sil**

     1. Merhaba blob toodelete istediğiniz seçin.
     2. Merhaba ana bölmede ait araç çubuğunda seçin **silmek**.
     3. Seçin **Evet** toohello onay iletişim kutusu.

## <a name="next-steps"></a>Sonraki adımlar
* Görünüm hello [en son Depolama Gezgini (Önizleme) sürüm notları ve videolar](http://www.storageexplorer.com).
* Nasıl çok öğrenin[Azure BLOB'ları, tabloları, kuyrukları ve dosyaları kullanan uygulamalar oluşturmak](https://azure.microsoft.com/documentation/services/storage/).

[0]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-create-context-menu.png
[1]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create.png
[2]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create-done.png
[3]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-editor.png
[4]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-context-menu.png
[5]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-confirmation.png
[6]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-copy-context-menu.png
[7]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-paste-context-menu.png
[8]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-context-menu.png
[9]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-options.png
[10]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-urls.png
[11]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-context-menu.png
[12]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-options.png
[13]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-context-menu.png
[14]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-options.png
[15]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-menu.png
[16]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-options.png
[17]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-menu.png
[18]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-options.png
[19]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-open-editor-context-menu.png
