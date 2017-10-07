---
title: "Azure RemoteApp görüntüsü dayalı bir Azure VM aaaCreate | Microsoft Docs"
description: "Bilgi nasıl toocreate bir Azure sanal makinesi ile başlatarak Azure RemoteApp için görüntü."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d41583ef-6cd8-4115-8dcb-b2cd5b3d301a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 2d432bcb15be68a2946d91b5f36f41d980726338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a>Bir Azure sanal makineye dayalı bir Azure RemoteApp görüntüsü oluşturma
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Bir Azure sanal makineden (hangi koleksiyonunuzda paylaşmak hello uygulamaları barındıracak) Azure RemoteApp görüntü oluşturabilirsiniz. Toouse tüm hello Azure RemoteApp görüntü gereksinimleri karşılayan toohello Azure VM görüntü Galerisi eklediğimiz sanal makine görüntüsü seçebilir - isterseniz kendi VM için bu VM görüntüsü bir başlangıç noktası olarak kullanabilirsiniz. Yalnızca hello "Windows Server Uzak Masaüstü oturumu ana bilgisayarı" görüntü hello Kitaplığı'nda arayın.

Azure VM temelinde kendi görüntünüzü tabanlı iki adımları toocreate vardır - hello görüntü oluşturma ve hello Azure VM kitaplık tooAzure RemoteApp karşıya yükleyin.

## <a name="create-a-custom-image-based-on-an-azure-vm"></a>Bir Azure VM temelinde özel bir görüntü oluşturun
Bu adımları toocreate bir Azure VM temelinde görüntü kullanın.

1. Bir Azure sanal makine oluşturun. Hello Azure sanal makine görüntüsü Galerisi'nden hello "Windows Server Uzak Masaüstü oturumu ana bilgisayarı" veya "Windows Server Uzak Masaüstü oturumu ana bilgisayarı ile Microsoft Office 365 ProPlus" Merhaba görüntüsü kullanabilirsiniz. Bu görüntü tüm hello Azure RemoteApp şablon görüntüsü gereksinimlerini karşılıyor.
   
    Ayrıntılar için bkz [Windows çalıştıran bir VM oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
2. Toohello VM bağlanmak ve yükleyin ve RemoteApp aracılığıyla tooshare istediğiniz hello uygulamalar yapılandırın. Emin tooperform uygulamalarınız tarafından gerekli ek Windows yapılandırmalara olun.
   
    Ayrıntılar için bkz [nasıl tooLog tooa sanal makine çalıştıran Windows Server üzerinde](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. Merhaba Windows Server Uzak Masaüstü oturumu ana bilgisayarı görüntülerden birini kullanıyorsanız, VM hello RemoteApp pre-reqs. karşılayan sağlayacak bir dahil doğrulama komut dosyası yok toorun komut dosyasını çift tıklatın **Validateremoteappımage** hello masaüstünde. Merhaba betik tarafından raporlanan tüm hataları toohello sonraki adıma devam etmeden önce düzeltilen emin olun.
4. SYSPREP generalize ve hello görüntüsünü yakalayın. Bkz: [nasıl tooCapture bir şablon olarak Windows sanal makine tooUse](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) yönergeler için.

## <a name="import-hello-image-into-hello-azure-remoteapp-image-library"></a>Hello Azure RemoteApp görüntüsü kitaplığa Hello görüntüsü Aktar
Bu adımları tooimport hello yeni görüntüyü Azure RemoteApp kullanın:

1. Merhaba, **şablon görüntüleri** sekmesi:
   
   * Hiçbir mevcut görüntü varsa, tıklatın **karşıya yükleyebilir veya bir şablon görüntüsü içe**.
   * En az bir görüntü zaten varsa, tıklatın  **+**  tooadd yeni bir görüntü.
2. Seçin **sanal makinelerden bir görüntü alma** kitaplığı ve ardından **sonraki**.
3. Merhaba sonraki sayfada özel görüntünüzü hello listeden seçin ve görüntünüzü oluşturduğunuzda listelenen hello adımları uyguladığınız onaylayın. **İleri**’ye tıklayın.
4. Merhaba yeni RemoteApp görüntüsü için bir ad girin ve hello konum seçin ve ardından hello onay işareti toostart hello içeri aktarma işlemi.

> [!NOTE]
> Azure sanal makineleri tooany Azure RemoteApp tarafından desteklenen Azure konumu tarafından desteklenen tüm Azure konumdan görüntüleri içe aktarabilirsiniz. Merhaba konumlara bağlı olarak hello alma too25 dakika sürebilir.
> 
> 

Artık toocreate yeni koleksiyonunuzu ya da hazır bir [bulut](remoteapp-create-cloud-deployment.md) koleksiyonu veya [karma](remoteapp-create-hybrid-deployment.md)gereksinimlerinize bağlı olarak.

