---
title: "aaaManage DNS bölgeleri Azure DNS - Azure portalı | Microsoft Docs"
description: "DNS bölgelerini hello Azure portal kullanarak yönetebilirsiniz. Bu makalede nasıl tooupdate, silme ve Azure DNS üzerinde DNS bölgeleri oluşturma"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/18/2017
ms.author: gwallace
ms.openlocfilehash: 0d8ce302bb7126dfe8077a6f3e33418e16fcea64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-hello-azure-portal"></a>Azure portal toomanage DNS bölgelerini nasıl hello

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)

Bu makale size nasıl toomanage hello Azure portal kullanarak DNS bölgeleri gösterir. DNS bölgelerini hello platformlar arası kullanarak da yönetebilirsiniz [Azure CLI](dns-operations-dnszones-cli.md) veya Azure hello [PowerShell](dns-operations-dnszones.md).

## <a name="create-a-dns-zone"></a>DNS bölgesi oluşturma

1. Toohello Azure portalında oturum açın
2. Hello Hub menüsünde ve tıklayın **yeni > Ağ iletişimi >** ve ardından **DNS bölgesi** tooopen hello oluşturmak DNS bölge dikey.

    ![DNS bölgesi](./media/dns-operations-dnszones-portal/openzone650.png)

4. Merhaba üzerinde **oluşturma DNS bölgesi** dikey penceresinde hello aşağıdaki değerleri girin ve ardından **oluşturma**:


   | **Ayar** | **Değer** | **Ayrıntılar** |
   |---|---|---|
   |**Ad**|contoso.com|Merhaba DNS bölgesinin Hello adı|
   |**Abonelik**|[Aboneliğiniz]|Bir abonelik toocreate hello DNS bölgesini seçin.|
   |**Kaynak grubu**|**Yeni oluştur:** contosoDNSRG|Bir kaynak grubu oluşturun. Merhaba kaynak grubu adı, seçtiğiniz hello abonelik içinde benzersiz olmalıdır. Merhaba okuyun, kaynak grupları hakkında daha fazla toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) genel bakış makalesi.|
   |**Konum**|Batı ABD||

> [!NOTE]
> Merhaba kaynak grubu hello kaynak grubu toohello konumunu gösterir ve hello DNS bölgesi üzerinde hiçbir etkisi olmaz. Merhaba DNS bölgesi konumunu her zaman "Genel" ve gösterilmiyor.

## <a name="list-dns-zones"></a>Liste DNS bölgeleri

İçinde Azure portal Merhaba, çok gidin**daha fazla hizmet** > **ağ** > **DNS bölgeleri**. Her DNS bölgesinin kendi kaynağı, kayıt kümesi sayısı gibi bilgiler ve ad sunucuları bu görünümden görüntülenebilir ' dir. Merhaba sütun **ad sunucuları** hello varsayılan görünüm tooadd tıklatın erişilebilir **sütunları**seçin **ad sunucuları** tıklatıp **Bitti**.

![DNS bölgelerini listeleme](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a>Bir DNS bölgesi Sil

Merhaba portal tooa DNS bölgesinde gidin. Merhaba üzerinde **DNS bölgesi** dikey penceresinde tıklatın **bölgeyi Sil**. İstendiğinde tooconfirm toodelete hello DNS bölgesi isteyen var. Bir DNS bölgesi silme hello bölgede bulunan tüm hello kayıtlarını siler.

## <a name="next-steps"></a>Sonraki adımlar

Bilgi nasıl DNS bölgesi ve kayıtları şu adresi ziyaret ederek toowork [Azure hello Azure portal kullanarak DNS ile çalışmaya başlama](dns-getstarted-portal.md).
