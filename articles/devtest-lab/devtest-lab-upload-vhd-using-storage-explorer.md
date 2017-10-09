---
title: aaaUpload VHD dosya tooAzure DevTest Labs Microsoft Azure Storage Gezgini kullanma | Microsoft Docs
description: "Microsoft Azure Storage Gezgini kullanarak VHD dosyasını toolab ait depolama hesabı karşıya yükle"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 686691e3676cea4b2d7cd8bf045bc43a792c667e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-microsoft-azure-storage-explorer"></a>Microsoft Azure Storage Gezgini kullanarak VHD dosyasını toolab ait depolama hesabı karşıya yükle

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

Azure DevTest Labs'de VHD dosyaları kullanılan tooprovision sanal makinelerdir kullanılan toocreate özel resimler olabilir. Bu makalede gösterilmektedir nasıl toouse [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooupload VHD dosyası tooa Laboratuvar ait depolama hesabı. VHD dosyasını yüklediğiniz sonra hello [bölüm'sonraki adımlar](#next-steps) nasıl toocreate hello özel bir görüntüden VHD dosyasını karşıya göstermeye bazı makaleleri listeler. Diskleri ve Azure içinde VHD'leri hakkında daha fazla bilgi için bkz: [diskler ve sanal makineler için VHD'ler hakkında](../virtual-machines/linux/about-disks-and-vhds.md)

## <a name="step-by-step-instructions"></a>Adım adım yönergeler

Merhaba, bir VHD karşıya aracılığıyla dosya kullanarak tooDevTest Labs adımları ilerlemesi [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md).

1. [Microsoft Azure Storage Gezgini hello hello en son sürümünü karşıdan yükleyip](http://www.storageexplorer.com).

1. Merhaba hello Azure portal kullanarak hello Laboratuvar ait depolama hesabı adını alın:

    1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
    
    1. Seçin **daha fazla hizmet**ve ardından **DevTest Labs** hello listeden.
    
    1. Merhaba istenen Laboratuvar labs Hello listeden seçin.  
    
    1. Merhaba Laboratuvar'ın dikey penceresinde, seçin **yapılandırma**. 
    
    1. Merhaba Laboratuvar üzerinde **yapılandırma** dikey penceresinde, select **özel görüntülerini (VHD)**.
    
    1. Merhaba üzerinde **özel görüntüleri** dikey penceresinde, seçin **+ Ekle**. 
    
    1. Merhaba üzerinde **özel görüntü** dikey penceresinde, select **VHD**.
    
    1. Merhaba üzerinde **VHD** dikey penceresinde, select **PowerShell kullanarak bir VHD'yi karşıya**.
    
        ![PowerShell kullanarak VHD karşıya yükle][0]
    
    1. Merhaba **PowerShell kullanarak bir görüntüyü karşıya yüklemeden** dikey penceresinde görüntüler çağrısı toohello **Ekle AzureVhd** cmdlet'i. İlk parametre hello (*hedef*) biçimi aşağıdaki hello hello laboratuvarda hello depolama hesabı adını içerir:
    
        https://<Storage-ACCOUNT-Name>.BLOB.Core.Windows.NET/uploads/... 

    1. Sonraki adımlarda kullanılmak üzere hello depolama hesabı adını not edin.
    
1. Tooan Depolama Gezgini'ni kullanarak Azure Abonelik hesabına bağlanın.

    > [!TIP] 
    > 
    > Depolama Gezgini çeşitli bağlantı seçenekleri destekler. Bu bölümde Azure aboneliğinizle ilişkili bağlantı tooa depolama hesabı gösterilmektedir. toosee Depolama Gezgini tarafından desteklenen diğer bağlantı seçenekleri Merhaba, toohello makalesine başvurun [Depolama Gezgini ile çalışmaya başlama](../vs-azure-tools-storage-manage-with-storage-explorer.md).
 
    1. Depolama Gezgini'ni açın.
    
    1. Depolama Gezgini'nde seçin **Azure hesap ayarlarını**. 
    
        ![Azure hesap ayarları][1]
    
    1. Hello sol bölmede oturum açtığınız hello Microsoft hesapları görüntülenir. tooconnect tooanother hesabı, select **Hesap Ekle**, en az bir etkin Azure aboneliği ile ilişkili bir Microsoft hesabıyla hello iletişim kutuları toosign izleyin.
    
        ![Hesap ekleme][2]
    
    1. Başarıyla bir Microsoft hesabıyla oturum açtıktan sonra hello sol bölmesinde bu hesapla ilişkili Azure abonelikleri hello ile doldurur. Select hello hangi toowork istediğiniz ve ardından Azure abonelikleri **Uygula**. (Seçme **tüm abonelikleri** değiştirir hello tüm seçimi veya hello hiçbiri Azure abonelikleri listelenen.)
    
        ![Azure aboneliklerini seçme][3]
    
    1. Hello sol bölmede seçili hello Azure abonelikleriyle ilişkilendirilen hello depolama hesapları gösterilir.
    
        ![Seçili Azure abonelikleri][4]

1. Merhaba Laboratuvar'ın depolama hesabını bulun:

    1. Merhaba Depolama Gezgini sol bölmesinde, bulun ve hello hello Laboratuvar sahip Azure aboneliği için hello düğümünü genişletin.
    
    1. Merhaba aboneliğinin düğümünde genişletin **depolama hesapları**.

    1. Hello Laboratuvar ait depolama hesabı düğüm tooreveal düğümleri genişletin **Blob kapsayıcıları**, **dosya paylaşımları**, **sıraları**, ve **tabloları**.
    
    1. Merhaba genişletin **Blob kapsayıcıları** düğümü.
    
    1. Merhaba yüklemeleri blob kapsayıcı toodisplay hello sağ bölmede içeriğini seçin.
        
        ![Dizin karşıya yükle][5]

1. Depolama Gezgini'ni kullanarak hello VHD dosyasını karşıya yükle:

    1. Merhaba Depolama Gezgini sağ bölmede, hello hello blobları listesini görmelisiniz **yükler** hello Laboratuvar'ın depolama hesabının blob kapsayıcısı. Merhaba blob Düzenleyicisi araç çubuğunda seçin **karşıya yükle** 
        
        ![Düğme karşıya yükle][6]
    
    1. Merhaba gelen **karşıya** açılır menüsünde, select **dosyaları karşıya yükleme...** .
    
    1. Merhaba üzerinde **dosyaları karşıya yükleme** iletişim, select hello üç nokta.
        
        ![Dosya seçin][8]  

    1. Merhaba üzerinde **Select dosyaları tooupload** iletişim kutusunda, Gözat toohello istenen VHD dosyasını seçin ve ardından **açık**.
    
    1. Zaman toohello döndürülen **dosyaları karşıya yükleme** iletişim kutusunda, değişiklik **Blob türü** çok**sayfa blobu**.
    
    1. **Karşıya Yükle**’yi seçin.

        ![Dosya seçin][9]  
    
    1. Depolama Gezgini Hello **etkinlik günlüğü** bölmesi hello karşıdan yükleme durumu (birlikte bağlantılar toocancel hello karşıya yükleme) gösterir. VHD dosyasını karşıya yükleme işleminin hello hello hello VHD dosyasının boyutunu ve bağlantı hızınıza bağlı olarak uzun olabilir. 

        ![Dosya karşıya yükleme durumu][10]  

## <a name="next-steps"></a>Sonraki adımlar

- [Azure DevTest Labs hello Azure portal kullanarak bir VHD dosyasında özel bir görüntü oluşturun](devtest-lab-create-template.md)
- [Azure DevTest Labs PowerShell kullanarak bir VHD dosyasında özel bir görüntü oluşturun](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

[0]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-image-using-psh.png
[1]: ./media/devtest-lab-upload-vhd-using-storage-explorer/settings-icon.png
[2]: ./media/devtest-lab-upload-vhd-using-storage-explorer/add-account-link.png
[3]: ./media/devtest-lab-upload-vhd-using-storage-explorer/subscriptions-list.png
[4]: ./media/devtest-lab-upload-vhd-using-storage-explorer/storage-accounts-list.png
[5]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-dir.png
[6]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-button.png
[7]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-files.png
[8]: ./media/devtest-lab-upload-vhd-using-storage-explorer/select-file.png
[9]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-file.png
[10]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-status.png
