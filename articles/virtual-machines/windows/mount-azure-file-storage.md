---
title: Azure dosya depolama biriminden bir Azure Windows VM aaaMount | Microsoft Docs
description: "Azure dosya depolama ile Merhaba bulutta dosya depolamak ve bir Azure sanal makineden (VM) bulut dosya paylaşımına bağlayın."
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 965f1c1b3f0d07fec6d86f9312a05e02e8ce7fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a>Azure dosya paylaşımları Windows VM ile birlikte kullanmak 

Azure dosya paylaşımları, VM'den bir şekilde toostore ve erişim dosyaları olarak kullanabilirsiniz. Örneğin, bir komut dosyası veya tüm sanal makineleri tooshare istediğiniz uygulama yapılandırma dosyası depolayabilirsiniz. Bu konuda, dosya paylaşımı toocreate ve bağlama Azure nasıl ve ne gösteriyoruz tooupload ve yükleme dosyaları.

## <a name="connect-tooa-file-share-from-a-vm"></a>Bir sanal makineden tooa dosya paylaşımına bağlanmak

Bu bölümde, zaten bir dosya paylaşımı için tooconnect istediğinizi varsayar. Bir toocreate gerekirse bkz [bir dosya paylaşımı oluşturmak](#create-a-file-share) bu konuda daha sonra.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba sol menüsünde **depolama hesapları**.
3. Depolama hesabınızı seçin.
4. Merhaba, **genel bakış** sayfasında **Hizmetleri**seçin **dosyaları**.
5. Bir dosya paylaşımı seçin.
6. Tıklatın **Bağlan** tooopen hello bağlama hello dosya paylaşımından Windows veya Linux için komut satırı söz dizimi görülmektedir bir sayfa.
7. Merhaba komutun Hello sözdizimi vurgulayın ve Not Defteri veya nedenini bildirmeden bir yerde başka kolayca erişebilirsiniz bir yere yapıştırın. 
8. Merhaba sözdizimi tooremove hello başında Düzenle ** > ** ve değiştirme *[sürücü harfi]* hello sürücü harfine sahip (örneğin, **Y:**) burada istediğinizi toomount hello dosya paylaşımı.
8. Tooyour VM bağlanabilir ve bir komut istemi açın.
9. Merhaba yapıştırma seçeneğiyle bağlantı sözdizimi düzenlenmesi ve isabet **Enter**.
10. Merhaba bağlantıyı oluştururken hello iletisi alıyorum **hello komutu başarıyla tamamlandı.**
11. Merhaba sürücü harfi tooswitch toothat sürücüye yazarak Hello bağlantısını denetleyin ve ardından **dir** toosee Merhaba içeriğine hello dosya paylaşımı.



## <a name="create-a-file-share"></a>Dosya paylaşımı oluşturma 
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba sol menüsünde **depolama hesapları**.
3. Depolama hesabınızı seçin.
4. Merhaba, **genel bakış** sayfasında **Hizmetleri**seçin **dosyaları**.
5. Merhaba dosya hizmeti sayfasında tıklatın **+ dosya paylaşımı** ilk dosya paylaşımı toocreate. \
6. Merhaba dosya paylaşımı adı girin. Dosya Paylaşımı adları küçük harf, rakam ve tek tire kullanabilirsiniz. Merhaba adı bir tire ile başlatamıyor ve birden çok kullanamazsınız art arda kısa çizgi. 
7. Bir sınırı ne kadar büyük hello dosya doldurun, too5120 GB olabilir.
8. Tıklatın **Tamam** toodeploy hello dosya paylaşımı.
   
## <a name="upload-files"></a>Dosyaları karşıya yükleme
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba sol menüsünde **depolama hesapları**.
3. Depolama hesabınızı seçin.
4. Merhaba, **genel bakış** sayfasında **Hizmetleri**seçin **dosyaları**.
5. Bir dosya paylaşımı seçin.
6. Tıklatın **karşıya** tooopen hello **dosyaları karşıya yükleme** sayfası.
7. Başlangıç klasörü simgesi toobrowse üzerinde yerel dosya sistemine dosya tooupload için tıklatın.   
8. Tıklatın **karşıya** tooupload hello dosya toohello dosya paylaşımı.

## <a name="download-files"></a>Dosyaları indirme
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba sol menüsünde **depolama hesapları**.
3. Depolama hesabınızı seçin.
4. Merhaba, **genel bakış** sayfasında **Hizmetleri**seçin **dosyaları**.
5. Bir dosya paylaşımı seçin.
6. Merhaba dosyasını sağ tıklatın ve seçin **karşıdan** toodownload, tooyour yerel makine.
   

## <a name="next-steps"></a>Sonraki adımlar

Ayrıca, oluşturun ve PowerShell kullanarak dosya paylaşımlarını yönetin. Daha fazla bilgi için bkz: [Windows Azure File storage ile çalışmaya başlama](../../storage/files/storage-dotnet-how-to-use-files.md).
