---
title: Azure Depolama Gezgini ile Blob depolama biriminden aaaMove veri tooand | Microsoft Docs
description: "Azure Storage Gezgini kullanarak Azure Blob depolama alanından veri tooand Taşı"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 10bd283f-0875-4c67-af63-6492270b7656
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 38d3bc009950c97d8474b0acceaf74814638dac0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azure-storage-explorer"></a>Azure Storage Gezgini kullanarak Azure Blob depolama alanından veri tooand Taşı
Azure Storage Gezgini, Windows, macOS ve Linux Azure Storage verilerle toowork sağlayan Microsoft ücretsiz bir araçtır. Bu konuda açıklanmaktadır nasıl toouse, tooupload ve indirme verileri Azure blob depolama. Merhaba aracı adresinden yüklenebilir [Microsoft Azure Storage Gezgini](http://storageexplorer.com/).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> Tarafından sağlanan hello kodlarıyla ayarlanan VM kullanıyorsanız [veri bilimi sanal makinelerle](machine-learning-data-science-virtual-machines.md), sonra da Azure Storage Gezgini hello VM üzerinde zaten yüklü.
> 
> [!NOTE]
> Bir tam giriş tooAzure blob depolama çok başvuran[Azure Blob Temelleri](../storage/blobs/storage-dotnet-how-to-use-blobs.md) ve [Azure Blob hizmeti](https://msdn.microsoft.com/library/azure/dd179376.aspx).   
> 
> 

## <a name="prerequisites"></a>Ön koşullar
Bu belge, Azure aboneliği bir depolama hesabı ve o hesap için karşılık gelen depolama anahtar hello sahip olduğunuzu varsayar. Karşıya yükleme/veri yüklemeden önce Azure depolama hesabı adı ve hesap anahtarınızın bilmeniz gerekir. 

* bir Azure aboneliği yukarı tooset bkz [ücretsiz bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).
* Bir depolama hesabı oluşturma hakkında yönergeler ve hesabı ve anahtarı bilgilerini almak için bkz: [Azure storage hesapları hakkında](../storage/common/storage-create-storage-account.md). Bu anahtar tooconnect toohello hesap hello Azure Storage Gezgini aracıyla gerektiği depolama hesabınız için Not hello erişim tuşu olun.
* Hello Azure Storage Gezgini aracı adresinden yüklenebilir [Microsoft Azure Storage Gezgini](http://storageexplorer.com/). Sırasında Hello Varsayılanları kabul edin.

<a id="explorer"></a>

## <a name="use-azure-storage-explorer"></a>Azure Depolama Gezgini'ni kullanın
adımları belge nasıl aşağıdaki hello Azure Storage Gezgini kullanarak tooupload/indirme verileri. 

1. Microsoft Azure Storage Gezgini başlatın.
2. Merhaba yukarı toobring **tooyour hesabında oturum...**  seçin **Azure hesap ayarlarını** simgesine ve sonra **Hesap Ekle** ve kimlik bilgilerini girin. ![Bir Azure depolama hesabı ekleme](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/add-an-azure-store-account.png)
3. Merhaba yukarı toobring **tooAzure depolama bağlanmak** seçin hello **tooAzure depolama birimini bağlayın** simgesi. ![TooAzure depolama birimini bağlayın](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-1.png)
4. Merhaba erişim anahtarı üzerinde hello Azure storage hesabınızdan girin **tooAzure depolama bağlanmak** Sihirbazı'nı ve ardından **sonraki**. ![TooAzure depolama birimini bağlayın](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-2.png)
5. Hello depolama hesabı adı girin **hesap adı** kutusuna ve ardından **sonraki**. ![Harici depolama ekleme](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/attach-external-storage.png)
6. eklenen hello depolama hesabı listelenmiş olmalıdır. toocreate depolama hesabındaki bir blob kapsayıcısını sağ hello **Blob kapsayıcıları** bu hesap, select düğümünde **Blob kapsayıcısı oluşturmak**ve bir ad girin.
7. tooupload veri tooa kapsayıcısı, select hello hedef kapsayıcı ve tıklatın hello **karşıya** düğmesini.![ Depolama hesapları](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/storage-accounts.png)
8. Tıklatın hello üzerinde **...**  hello sağında toohello **dosyaları** kutusunda, bir veya birden çok dosya tooupload hello dosya sisteminden seçin ve'ı tıklatın **karşıya** hello dosyaları karşıya yükleme toobegin.![ Dosyaları karşıya yükleme](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/upload-files-to-blob.png)
9. Merhaba seçerek toodownload veri blob hello karşılık gelen kapsayıcı toodownload ve tıklatın **karşıdan**. ![Dosyaları indirme](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/download-files-from-blob.png)

