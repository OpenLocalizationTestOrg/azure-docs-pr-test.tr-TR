---
title: "Depolama Gezgini (Önizleme) Azure File storage ile aaaUsing | Microsoft Docs"
description: "Bilgi nasıl toouse Depolama Gezgini (Önizleme) toowork dosya paylaşımları ve dosyaları nasıl öğrenin."
services: storage
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/09/2017
ms.author: cawa
ms.openlocfilehash: 98eb3cde711ae3dbfdb6ffaec23ae24f822370e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a>Depolama Gezgini’ni (Önizleme) Azure Dosya Depolama ile kullanma

Depolama dosya sunan bir hizmet hello kullanılarak bulut paylaşır azure dosyası hello standart sunucu ileti bloğu (SMB) protokolü. SMB 2.1 ve SMB 3.0 desteklenir. Azure File storage, dosya paylaşımları tooAzure üzerinde maliyetli yeniden yazdırmaya gerek duymadan ve hızla kullanan eski uygulamalar geçirebilirsiniz. Dosya depolama tooexpose verileri kullanabileceğiniz genel olarak toohello world veya toostore uygulama verilerini özel olarak. Bu makalede, nasıl toouse Depolama Gezgini (Önizleme) toowork dosya paylaşımları ve dosyaları öğreneceksiniz.

## <a name="prerequisites"></a>Ön koşullar

Bu makaledeki toocomplete hello adımları, hello aşağıdakiler gerekir:

- [Depolama Gezgini (önizleme) indirip yükleme](http://www.storageexplorer.com/)

- [Tooa Azure depolama hesabı veya hizmetine bağlanmak](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a>Dosya Paylaşımı oluşturma

Tüm dosyalar, basitçe dosyaların mantıksal bir gruplandırması olan dosya paylaşımında bulunmalıdır. Bir hesapta sınırsız sayıda dosya paylaşımı olabilir ve her paylaşım sınırsız sayıda dosya depolayabilir.

Aşağıdaki adımları hello nasıl toocreate bir dosya paylaşımı Depolama Gezgini (Önizleme) içinde gösterilmektedir.

1. Depolama Gezgini’ni (Önizleme) açın.

2. Merhaba sol bölmede toocreate hello dosya paylaşımı içinde istediğiniz hello depolama hesabı genişletin

3. Sağ **dosya paylaşımları**ve - hello bağlam menüsünden - seçin **dosya paylaşımı oluştur**.

    ![Dosya Paylaşımı Oluşturma](media/vs-azure-tools-storage-explorer-files/image1.png)

4. Bir metin kutusu altında hello görünür **dosya paylaşımları** klasör. Dosya Paylaşımı için Hello adı girin. Merhaba bkz [adlandırma kuralları paylaşmak](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) bölümünde bir liste için kurallar ve dosya paylaşımları adlandırma kısıtlamaları.

    ![Adlandırma hello paylaşımı](media/vs-azure-tools-storage-explorer-files/image2.png)

5. Tuşuna **Enter** Bitti'yi toocreate Merhaba, dosya paylaşımı veya **Esc** toocancel. Merhaba dosya paylaşımı başarıyla oluşturulduktan sonra uygulamanın altında hello görüntülenecek **dosya paylaşımları** klasörü hello için seçtiğiniz depolama hesabı.

    ![Merhaba yeni paylaşım](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a>Dosya paylaşımının içeriğini görüntüleme

Dosya paylaşımları, dosya ve klasörler içerir (klasörler de dosya içerebilir).

Merhaba aşağıdaki adımları tooview hello bir dosyanın içeriğini Depolama Gezgini (Önizleme) içinde nasıl paylaşmak gösterilmektedir: +

1. Depolama Gezgini’ni (Önizleme) açın.

2. Merhaba sol bölmede, tooview istediğiniz hello dosya paylaşımı içeren hello depolama hesabı'nı genişletin.

3. Merhaba depolama hesabının genişletin **dosya paylaşımları**.

4. Sağ hello dosya paylaşımı, tooview istiyor ve - hello bağlam menüsünden - seçin **açık**. Ayrıca tooview istediğiniz hello dosya paylaşımı çift tıklatabilirsiniz.

    ![Paylaşımı açma](media/vs-azure-tools-storage-explorer-files/image4.png)

5. Merhaba ana bölmede hello dosya paylaşımının içeriğini görüntüler.
    
    ![paylaşımın içeriği hello](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a>Dosya paylaşımını silme

Dosya paylaşımları kolayca oluşturulabilir ve gerektiğinde silinebilir. (toosee toodelete tek tek dosyaların başvurmak nasıl toohello bölüm [bir dosya paylaşımında dosyalar yönetme](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)

Aşağıdaki adımları hello nasıl toodelete bir dosya paylaşımı Depolama Gezgini (Önizleme) içinde gösterilmiştir:

1. Depolama Gezgini’ni (Önizleme) açın.

2. Merhaba sol bölmede, tooview istediğiniz hello dosya paylaşımı içeren hello depolama hesabı'nı genişletin.

3. Merhaba depolama hesabının genişletin **dosya paylaşımları**.

4. Sağ hello dosya paylaşımı, toodelete istiyor ve - hello bağlam menüsünden - seçin **silmek**. Tuşlarına da basabilirsiniz **silmek** toodelete hello şu anda seçili dosya paylaşımı.

    ![Sil](media/vs-azure-tools-storage-explorer-files/image6.png)

5. Seçin **Evet** toohello onay iletişim kutusu.
    
    ![Onay iletişim kutusu](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a>Dosya paylaşımını kopyalama

Depolama Gezgini (Önizleme) toocopy bir dosya paylaşımı toohello Pano sağlar ve bu dosya paylaşımına başka bir depolama hesabı yapıştırın. (toosee toocopy tek tek dosyaların başvurmak nasıl toohello bölüm [bir dosya paylaşımında dosyalar yönetme](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)

Aşağıdaki adımları hello nasıl toocopy bir dosya paylaşımı bir depolama hesabı tooanother gösterilmektedir.

1. Depolama Gezgini’ni (Önizleme) açın.

2. Merhaba sol bölmede, toocopy istediğiniz hello dosya paylaşımı içeren hello depolama hesabı'nı genişletin.

3. Merhaba depolama hesabının genişletin **dosya paylaşımları**.

4. Sağ hello dosya paylaşımı, toocopy istiyor ve - hello bağlam menüsünden - seçin **kopyalama dosya paylaşımı**.

    ![Dosya Paylaşımını Kopyala](media/vs-azure-tools-storage-explorer-files/image8.png)

5. Hangi içine, toopaste hello dosya paylaşmak istediğiniz - hello bağlam menüsünden - seçin hello istenen "hedef" depolama hesabını sağ tıklatıp **Yapıştır dosya paylaşımı**.

    ![Dosya Paylaşımını Yapıştır](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-hello-sas-for-a-file-share"></a>Bir dosya paylaşımı için Hello SAS alma

A [paylaşılan erişim imzası (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) depolama hesabınızda atanmış erişim tooresources sağlar. Başka bir deyişle, bir istemci depolama hesabınızdaki izinleri tooobjects süre ve belirtilen bir izin kümesi ile belirli bir süre için hesap erişim tuşlarınızı tooshare gerek kalmadan sınırlı verebilirsiniz.

Merhaba aşağıdaki adımları göstermek toocreate bir dosya için bir SAS nasıl paylaşmak: +

1. Depolama Gezgini’ni (Önizleme) açın.

2. Hello sol bölmesinde, SAS tooget öğrenmek isterseniz hello dosya paylaşımı içeren hello depolama hesabı'nı genişletin.

3. Merhaba depolama hesabının genişletin **dosya paylaşımları**.

4. Merhaba istenen dosya paylaşımı sağ tıklatın ve - hello bağlam menüsünden - seçin **paylaşılan erişim imzası Al**.

    ![Paylaşılan Erişim İmzası Al](media/vs-azure-tools-storage-explorer-files/image10.png)

5. Merhaba, **paylaşılan erişim imzası** iletişim kutusunda, hello İlkesi, başlangıç ve sona erme tarihleri, saat dilimini belirtin ve erişim düzeyleri hello kaynak için istediğiniz.

    ![SAS iletişim kutusu](media/vs-azure-tools-storage-explorer-files/image11.png)

6. Merhaba SAS seçeneklerini belirtme tamamladığınızda seçin **oluşturma**.

7. İkinci bir **paylaşılan erişim imzası** iletişim listeleri hello hello URL ile birlikte dosya paylaşımı ve tooaccess kullanabileceğiniz QueryStrings hello depolama kaynağı sonra görüntülenir. Seçin **kopya** toocopy toohello Pano istediğiniz sonraki toohello URL.
    
    ![İkinci SAS iletişim kutusu](media/vs-azure-tools-storage-explorer-files/image12.png)

8. İşiniz bittiğinde **Kapat**’ı seçin.

## <a name="manage-access-policies-for-a-file-share"></a>Bir dosya paylaşımı için Erişim İlkelerini yönetme

Merhaba aşağıdaki adımları göstermek nasıl toomanage (ekleme ve kaldırma) erişim ilkeleri bir dosya paylaşımı için: +. Merhaba erişim ilkeleri, SAS üzerinden kişiler tanımlı bir süre boyunca tooaccess hello depolama dosya kaynağı kullanabilir URL'ler oluşturmak için kullanılır.

1. Depolama Gezgini’ni (Önizleme) açın.

2. Hello sol bölmede, erişim ilkeleri toomanage istediğiniz hello dosya paylaşımı içeren hello depolama hesabı'nı genişletin.

3. Merhaba depolama hesabının genişletin **dosya paylaşımları**.

4. Merhaba istenen dosya paylaşımı seçin ve - hello bağlam menüsünden - seçin **erişim ilkelerini Yönet**.

    ![Erişim ilkelerini yönet bağlam menüsü](media/vs-azure-tools-storage-explorer-files/image13.png)

5. Merhaba **erişim ilkeleri** iletişim hello seçili dosya paylaşımı için oluşturulmuş tüm erişim ilkeleri listeler.
    
    ![Erişim İlkeleri](media/vs-azure-tools-storage-explorer-files/image14.png)

6. Merhaba erişim ilkesi yönetim görevi bağlı olarak aşağıdaki adımları izleyin:
    
    - **Yeni bir erişim ilkesi ekleme** - **Ekle**’yi seçin. Oluşturduktan sonra hello **erişim ilkeleri** iletişim yeni eklenen hello görüntüler erişim ilkesi (varsayılan ayarlarla).

    - **Erişim ilkesini düzenleme** - İstediğiniz düzenlemeleri yapıp **Kaydet**’i seçin.

    - **Erişim ilkesini kaldırmak** - seçin **kaldırmak** tooremove istediğiniz sonraki toohello erişim ilkesi.

7. Merhaba daha önce oluşturduğunuz erişim ilkesi kullanarak yeni bir SAS URL'si oluşturun:
    
    ![SAS alma](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![SAS adı ve özellikleri](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a>Bir dosya paylaşımındaki dosyaları yönetme

Bir dosya paylaşımı oluşturduktan sonra bir dosya toothat dosya paylaşımı karşıya yükleme, bir dosya tooyour yerel bilgisayarda indirin, yerel bilgisayarınıza ve daha pek çok dosya açma.

Merhaba aşağıdaki adımları nasıl toomanage hello dosyaları (ve klasörler) içinde bir dosya paylaşımı gösterilmektedir.

1.  Depolama Gezgini’ni (Önizleme) açın.

2.  Merhaba sol bölmede, toomanage istediğiniz hello dosya paylaşımı içeren hello depolama hesabı'nı genişletin.

3.  Merhaba depolama hesabının genişletin **dosya paylaşımları**.

4.  Merhaba dosya paylaşımı tooview istediğiniz çift tıklayın.

5.  Merhaba ana bölmede hello dosya paylaşımının içeriğini görüntüler.

    ![paylaşımın içeriği hello](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  Merhaba ana bölmede hello dosya paylaşımının içeriğini görüntüler.

7.  Tooperform istediğiniz Hello göreve bağlı olarak aşağıdaki adımları izleyin:

    - **Dosyaları tooa dosya paylaşımı karşıya yükle**

        a.  Merhaba ana bölmede ait araç çubuğunda seçin **karşıya**ve ardından **dosya yükleme** hello açılan menüsünden.

        ![Dosyaları karşıya yükleme](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        b. Merhaba, **dosyaları karşıya yükleme** iletişim, select hello üç nokta (**...** ) düğmesini hello hello sağ tarafındaki **dosyaları** metin kutusu tooselect hello dosyaları tooupload istiyor.

        ![Dosya ekleme](media/vs-azure-tools-storage-explorer-files/image19.png)

        c. **Karşıya Yükle**’yi seçin.

    - **Bir klasör tooa dosya paylaşımı karşıya yükle**
        
        a. Merhaba ana bölmede ait araç çubuğunda seçin **karşıya**ve ardından **karşıya yükleme klasörü** hello açılan menüsünden.

        ![Klasörü karşıya yükle menüsü](media/vs-azure-tools-storage-explorer-files/image20.png)

        b. Merhaba, **karşıya yükleme klasörü** iletişim, select hello üç nokta (**...** ) düğmesini hello hello sağ tarafındaki **klasörü** içeriği tooupload istediğiniz metin kutusu tooselect hello klasörü.

        c. İsteğe bağlı olarak, hangi hello seçilen klasörün içeriğini karşıya yükleneceği bir hedef klasör belirtin. Merhaba hedef klasörü yoksa, oluşturulur.

        d. **Karşıya Yükle**’yi seçin.

    - **Bir dosya tooyour yerel bilgisayarda indirin**
        
        a. Toodownload istediğiniz hello dosyasını seçin.
        
        b. Merhaba ana bölmede ait araç çubuğunda seçin **karşıdan**.
        
        c. Merhaba, **toosave hello dosyasını indirdiğiniz belirt** iletişim kutusunda, indirilen hello dosyasına hello konumu belirtin ve hello toogive istediğiniz adı.

        d. **Kaydet**’i seçin.

    - **Bir dosyayı yerel bilgisayarınızda açma**
        
        a.  Tooopen istediğiniz hello dosyasını seçin.
        
        b.  Merhaba ana bölmede ait araç çubuğunda seçin **açık**.
        
        c.  Merhaba dosyası indirilir ve hello dosyanın temel alınan dosya türü ile ilişkili hello uygulama kullanılarak açılır.

    - **Bir dosya toohello Panoya Kopyala**

        a. Toocopy istediğiniz hello dosyasını seçin.

        b. Merhaba ana bölmede ait araç çubuğunda seçin **kopya**.

        c. Hello sol bölmede tooanother dosya paylaşımına gidin ve çift tooview hello ana bölmede içinde.

        d. Merhaba ana bölmede ait araç çubuğunda seçin **Yapıştır** toocreate hello dosyasının bir kopyası.

    - **Dosyayı silme**

        a. Toodelete istediğiniz hello dosyasını seçin.

        b. Merhaba ana bölmede ait araç çubuğunda seçin **silmek**.

        c. Seçin **Evet** toohello onay iletişim kutusu.

## <a name="next-steps"></a>Sonraki adımlar

- Görünüm hello [en son Depolama Gezgini (Önizleme) sürüm notları ve videolar](http://www.storageexplorer.com/).

- Nasıl çok öğrenin[Azure BLOB'ları, tabloları, kuyrukları ve dosyaları kullanan uygulamalar oluşturmak](https://azure.microsoft.com/documentation/services/storage/).
