---
title: "Azure Hızlı Başlangıç - Azure portalını kullanarak nesneleri Azure Blob depolama içine/dışına aktarma | Microsoft Docs"
description: "Azure Blob depolamada blobları karşıya yükleme, indirme ve listeleme hakkında bilgi edinin."
services: storage
documentationcenter: storage
author: tamram
manager: jeconnoc
ms.custom: mvc
ms.service: storage
ms.workload: storage
ms.topic: quickstart
ms.date: 12/12/2017
ms.author: tamram
ms.openlocfilehash: f647a5b78ee2fa362c4dea6ee9003ac56e0f7f7d
ms.sourcegitcommit: 562a537ed9b96c9116c504738414e5d8c0fd53b1
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/12/2018
---
# <a name="transfer-objects-tofrom-azure-blob-storage-using-the-azure-portal"></a>Azure portalını kullanarak nesneleri Azure Blob depolama içine/dışına aktarma

Bu hızlı başlangıçta, [Azure portalını](https://portal.azure.com/) kullanarak Azure Depolamada bir kapsayıcı oluşturma ve bu kapsayıcı içinde blok bloblarını karşıya yükleme ve indirme hakkında bilgi edineceksiniz.

## <a name="prerequisites"></a>Ön koşullar

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.

[!INCLUDE [storage-quickstart-tutorial-create-account-portal](../../../includes/storage-quickstart-tutorial-create-account-portal.md)]

## <a name="create-a-container"></a>Bir kapsayıcı oluşturma

Azure portalında bir kapsayıcı oluşturmak için şu adımları izleyin:

1. Azure portalında yeni depolama hesabınıza gidin.
2. Depolama hesabının sol menüsünde **Blob Hizmeti** bölümüne gidip **Blob'lara Göz At**’ı seçin.
3. **Kapsayıcı Ekle** düğmesine tıklayın.
4. Yeni kapsayıcınız için bir ad girin. Kapsayıcı adı küçük harflerden oluşmalı ve bir harf veya rakamla başlamalıdır; yalnızca harf, rakam ve tire (-) karakterini içerebilir. Kapsayıcılar ve blob adları hakkında daha fazla bilgi için bkz. [Kapsayıcıları, Blobları ve Meta Verileri Adlandırma ve Bunlara Başvurma](https://docs.microsoft.com/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata).
5. Kapsayıcıya genel erişim düzeyini ayarlayın. Varsayılan düzey **Özel (anonim erişim yok)** şeklindedir.
6. **Tamam**'a tıklayarak kapsayıcıyı oluşturun.

    ![Azure portalında kapsayıcı oluşturmayı gösteren ekran görüntüsü](media/storage-quickstart-blobs-portal/create-container.png)

## <a name="upload-a-block-blob"></a>Blok blobunu karşıya yükleme

Blok blobları, bir blob oluşturmak üzere birleştirilmiş veri bloklarından oluşur. Blob depolama kullanan çoğu senaryoda blok blobları kullanılır. Blok blobları, bulutta metin ve dosya, görüntü ve video gibi ikili verileri depolamak için idealdir. Bu hızlı başlangıçta blok blobları ile çalışma hakkında bilgi verilmektedir. 

Azure portalında yeni kapsayıcınıza bir blok blobu yüklemek için aşağıdaki adımları izleyin:

1. Azure portalında, önceki bölümde oluşturduğunuz kapsayıcıya gidin.
2. İçerdiği blobların listesini görüntülemek üzere kapsayıcıyı seçin. Bu örnekte yeni bir kapsayıcı oluşturduğunuz için henüz yeni bir kapsayıcı içermez.
3. Kapsayıcıya bir blob yüklemek için **Karşıya Yükle** düğmesine tıklayın.
4. Blok blobu olarak yüklenecek bir dosya bulmak için yerel dosya sisteminize göz atın ve **Karşıya Yükle**’ye tıklayın.
     
    ![Yerel sürücünüzden bir blobu karşıya yüklemeyi gösteren ekran görüntüsü](media/storage-quickstart-blobs-portal/upload-blob.png)

5. Bu şekilde istediğiniz sayıda blobu karşıya yükleyin. Artık yeni blobların kapsayıcı içinde listelendiğini görürsünüz.

    ![Kapsayıcıda blob listesini gösteren ekran görüntüsü](media/storage-quickstart-blobs-portal/list-blobs.png)

## <a name="download-a-block-blob"></a>Blok blobu indirme

Bir blok blobunu tarayıcıda görüntülemek veya yerel dosya sisteminize kaydetmek üzere indirebilirsiniz. Bir blok blobu indirmek için şu adımları izleyin:

1. Önceki bölümde karşıya yüklediğiniz blob listesine gidin. 
2. İndirilecek blobu seçin.
3. **Daha fazla** düğmesine (**...**) sağ tıklayıp **İndir**’i seçin. 

![Azure portalında blob indirmeyi gösteren ekran görüntüsü](media/storage-quickstart-blobs-portal/download-blob.png)

## <a name="clean-up-resources"></a>Kaynakları temizleme

Bu hızlı başlangıçta oluşturduğunuz kaynakları kaldırmak için kapsayıcıyı silmeniz yeterlidir. Kapsayıcıdaki tüm blob'lar da silinir.

Kapsayıcıyı silmek için:

1. Azure portalında, depolama hesabınızdaki kapsayıcı listesine gidin.
2. Silinecek kapsayıcıyı seçin.
3. **Daha fazla** düğmesine (**...**) sağ tıklayıp **Sil**’i seçin.
4. Kapsayıcıyı silmek istediğinizi onaylayın.

    ![Azure portalından kapsayıcı silmeyi gösteren ekran görüntüsü](media/storage-quickstart-blobs-portal/delete-container.png)   

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıçta, dosyaları .NET kullanarak yerel bir disk ve Azure Blob depolama arasında aktarmayı öğrendiniz. Blob depolamayla çalışma hakkında daha fazla bilgi edinmek için, Blob depolama Nasıl yapılır öğreticisiyle devam edin.

> [!div class="nextstepaction"]
> [Blob Depolama İşlemleri Nasıl Yapılır](storage-dotnet-how-to-use-blobs.md)

