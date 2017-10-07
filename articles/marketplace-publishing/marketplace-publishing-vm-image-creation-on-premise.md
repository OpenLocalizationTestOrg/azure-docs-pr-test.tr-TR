---
title: "aaaCreating hello Azure Marketi için şirket içi sanal makine görüntü | Microsoft Docs"
description: "Anlama ve hello adımları toocreate bir şirket içi VM görüntüsü yürütün ve başkaları için toohello Azure Marketi dağıtmak toopurchase."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 26dfbd5a-8685-4b19-987e-c20ca60540ec
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c7a265330f1e494db8d0e981a38ee00d85746bb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-hello-azure-marketplace"></a>Hello Azure Marketi için şirket içi sanal makine görüntü geliştirin
Uzak Masaüstü Protokolü kullanarak, doğrudan hello bulutta Azure sanal sabit diskleri (VHD) geliştirmek öneririz. Ancak, gerekirse, olası toodownload bir VHD olduğunu ve şirket içi altyapısını kullanarak geliştirin.  

Şirket içi geliştirme için hello işletim sistemi oluşturulan hello VHD indirmeniz gerekir VM. Bu adımları adım 3.3, bir parçası olarak yukarıda gerçekleşmesi.  

## <a name="download-a-vhd-image"></a>Bir VHD görüntüsü indirin
### <a name="locate-a-blob-url"></a>Bir blob URL'si bulun
Sipariş toodownload hello VHD, ilk hello blob URL'si hello işletim sistemi diski bulun.

Merhaba blob hello URL'den yeni bulun [Microsoft Azure portal](https://portal.azure.com):

1. Çok Git**Gözat** > **VM'ler**, ve ardından hello VM dağıtılabilir.
2. Altında **yapılandırma**seçin hello **diskleri** döşeme, hangi hello diskleri dikey pencere açılır.
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. Select hello **işletim sistemi diski**, disk özellikleri, hello VHD konumu dahil olmak üzere görüntüler başka bir dikey pencere açılır.
4. Bu blob URL'sini kopyalayın.
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. Şimdi, silmek hello dağıtılan VM hello yedekleme diskleri silmeden. Merhaba VM silme yerine ayrıca durdurabilirsiniz. Merhaba VM çalıştırırken hello işletim sistemi VHD yüklemeyin.
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a>VHD indirme
Merhaba blob URL'si öğrendikten sonra hello kullanarak hello VHD indirebilirsiniz [Azure portal](http://manage.windowsazure.com/) veya PowerShell.  

> [!NOTE]
> Bu kılavuz oluşturma Hello sırasında hello işlevselliği toodownload VHD henüz hello yeni Microsoft Azure Portalı'nda mevcut değil.  
> 
> 

**Merhaba geçerli aracılığıyla Hello işletim sistemi VHD karşıdan [Azure portalı](http://manage.windowsazure.com/)**

1. Siz bunu zaten yapmadıysanız toohello Azure portalında oturum açın.
2. Merhaba tıklatın **depolama** sekmesi.
3. VHD hangi hello içinde depolanan hello depolama hesabı seçin.
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. Bu depolama hesabı özellikleri görüntüler. Select hello **kapsayıcıları** sekmesi.
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. Hangi hello VHD depolanan hello kapsayıcısı seçin. Varsayılan olarak, hello Portalı'ndan oluşturduğunuzda hello VHD VHD'ler kapsayıcısında depolanır.
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. Merhaba URL toohello bir kaydettiğiniz karşılaştırarak Hello doğru işletim sistemi VHD seçin.
7. **İndir**’e tıklayın.
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a>PowerShell kullanarak bir VHD'yi indirin
Ayrıca toousing Merhaba Azure portal, hello kullanabilirsiniz [Kaydet AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet toodownload hello işletim sistemi VHD.

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
Örneğin, kaydetme AzureVhd-kaynak "https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd" - LocalFilePath "C:\Users\Administrator\Desktop\baseimagevm.vhd" - depolama anahtarı<String>

> [!NOTE]
> **Kaydet-AzureVhd** de sahip bir **NumberOfThreads** olabilir seçeneği tooincrease paralellik toomake hello en iyi kullanılabilir bant genişliği kullanımını hello indirme için kullanılır.
> 
> 

## <a name="upload-vhds-tooan-azure-storage-account"></a>VHD'ler tooan Azure depolama hesabı karşıya yükle
VHD'ler şirket içi hazırlanmış, bunları bir depolama alanına Azure'da hesap tooupload gerekir. Bu adım, VHD oluşturma şirket içi sonra ancak VM görüntüsü için sertifika alma önce gerçekleşir.

### <a name="create-a-storage-account-and-container"></a>Bir depolama hesabı ve kapsayıcı oluşturma
VHD'ler hello Amerika Birleşik Devletleri'nde bir bölgede depolama hesaba yüklenebilmesi öneririz. Tüm VHD'leri tek bir SKU için tek bir depolama hesabına içindeki tek bir kapsayıcıda yerleştirilmelidir.

toocreate bir depolama hesabı, kullanabileceğiniz hello [Microsoft Azure portal](https://portal.azure.com/), PowerShell veya hello Linux komut satırı aracı.  

**Merhaba Microsoft Azure Portalı'ndan bir depolama hesabı oluşturma**

1. **Yeni**’ye tıklayın.
2. Seçin **depolama**.
3. Merhaba depolama hesabı adı girin ve ardından bir konum seçin.
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. **Oluştur**'a tıklayın.
5. Depolama hesabı oluşturuldu hello Hello dikey penceresi açık olması gerekir. Aksi takdirde, seçin **Gözat** > **depolama hesapları**. Dikey penceresinde Hello üzerinde depolama hesabı, oluşturulan hello depolama hesabı seçin.
6. Seçin **kapsayıcıları**.
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. Merhaba kapsayıcılara dikey penceresinde, seçin **Ekle**ve ardından bir kapsayıcı adı ve hello kapsayıcısı izinlerine girin. Seçin **özel** kapsayıcı izinleri.

> [!TIP]
> Bir kapsayıcı toopublish planlama SKU başına oluşturmanızı öneririz.
> 
> 

  ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a>PowerShell kullanarak bir depolama hesabı oluşturma
PowerShell kullanarak oluşturduğunuz bir depolama hesabı hello kullanarak [yeni AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet'i.

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

Ardından hello kullanarak bu depolama hesabı içindeki bir kapsayıcı oluşturabilirsiniz [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet'i.

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> Bu komutları o hello geçerli depolama hesabı bağlamını PowerShell'de ayarlamak varsayalım.   Çok başvuran[Azure PowerShell ayarı](marketplace-publishing-powershell-setup.md) PowerShell kurulumu hakkında daha fazla ayrıntı için.  
> 
> ### <a name="create-a-storage-account-by-using-hello-command-line-tool-for-mac-and-linux"></a>Mac ve Linux için hello komut satırı aracını kullanarak bir depolama hesabı oluşturma
> Gelen [Linux komut satırı aracı](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), aşağıdaki gibi bir depolama hesabı oluşturun.
> 
> 

        azure storage account create mystorageaccount --location "West US"

Şu şekilde bir kapsayıcı oluşturun.

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a>VHD’yi karşıya yükleme
Merhaba depolama hesabı ve kapsayıcı oluşturduktan sonra hazırlanan Vhd'lerinizi karşıya yükleyebilirsiniz. PowerShell, hello Linux komut satırı aracını veya diğer Azure Depolama Yönetimi araçlarını kullanabilirsiniz.

### <a name="upload-a-vhd-via-powershell"></a>Bir VHD PowerShell aracılığıyla karşıya yükleme
Kullanım hello [Ekle AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet'i.

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-hello-command-line-tool-for-mac-and-linux"></a>Mac ve Linux için hello komut satırı aracını kullanarak bir VHD'yi karşıya yükle
Merhaba ile [Linux komut satırı aracı](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), hello aşağıdakileri kullanın: azure vm görüntüsü oluşturma <image name> --konum <Location of hello data center> --OS Linux<LocationOfLocalVHD>

## <a name="see-also"></a>Ayrıca bkz.
* [Merhaba Market için bir sanal makine görüntüsü oluşturma](marketplace-publishing-vm-image-creation.md)
* [Azure PowerShell ayarlama](marketplace-publishing-powershell-setup.md)

