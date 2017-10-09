---
title: "aaaGet Azure hello Azure portal kullanarak DNS ile başlatılan | Microsoft Docs"
description: "Bilgi nasıl toocreate bir DNS bölgesi ve Azure DNS kaydında. Bu adım adım kılavuzu toocreate ve ilk DNS bölgesi ve kayıt hello Azure portalını kullanarak yönetin."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 5cea01d840d794001cccac64defed8b329d948db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-hello-azure-portal"></a>Azure hello Azure portal kullanarak DNS ile çalışmaya başlama

> [!div class="op_single_selector"]
> * [Azure portal](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Azure CLI 1.0](dns-getstarted-cli-nodejs.md)
> * [Azure CLI 2.0](dns-getstarted-cli.md)

Bu makalede, ilk DNS bölgesi ve hello Azure portal kullanarak kayıt hello adımları toocreate anlatılmaktadır. Ayrıca, Azure PowerShell kullanarak aşağıdaki adımları gerçekleştirin veya platformlar arası Azure CLI hello.

Bir DNS bölgesi belirli bir etki alanı için kullanılan toohost hello DNS kayıtlarını ' dir. Azure DNS, etki alanınızda barındırma toostart toocreate bir DNS bölgesi için o etki alanı adı gerekiyor. Ardından bu DNS bölgesinde etki alanınız için tüm DNS kayıtları oluşturulur. Son olarak, toopublish, DNS bölge toohello Internet tooconfigure hello ad sunucuları hello etki alanı için gerekir. Bu adımların her biri aşağıdaki adımları hello açıklanmıştır.

## <a name="create-a-dns-zone"></a>DNS bölgesi oluşturma

1. Toohello Azure portalında oturum açın
2. Hello Hub menüsünde ve tıklayın **yeni > Ağ iletişimi >** ve ardından **DNS bölgesi** tooopen hello oluşturmak DNS bölge dikey.

    ![DNS bölgesi](./media/dns-getstarted-portal/openzone650.png)

4. Merhaba üzerinde **oluşturma DNS bölgesi** dikey penceresinde hello aşağıdaki değerleri girin ve ardından **oluşturma**:


   | **Ayar** | **Değer** | **Ayrıntılar** |
   |---|---|---|
   |**Ad**|contoso.com|Merhaba DNS bölgesinin Hello adı|
   |**Abonelik**|[Aboneliğiniz]|Bir abonelik toocreate hello DNS bölgesini seçin.|
   |**Kaynak grubu**|**Yeni oluştur:** contosoDNSRG|Bir kaynak grubu oluşturun. Merhaba kaynak grubu adı, seçtiğiniz hello abonelik içinde benzersiz olmalıdır. Merhaba okuyun, kaynak grupları hakkında daha fazla toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) genel bakış makalesi.|
   |**Konum**|Batı ABD||

> [!NOTE]
> Merhaba kaynak grubu hello kaynak grubu toohello konumunu gösterir ve hello DNS bölgesi üzerinde hiçbir etkisi olmaz. Merhaba DNS bölgesi konumunu her zaman "Genel" ve gösterilmiyor.

## <a name="create-a-dns-record"></a>DNS kaydı oluşturma

Merhaba aşağıdaki örnek, yeni '' kayıt oluşturma hello sürecinde yardımcı olur. Diğer kayıt türleri ve toomodify mevcut kayıtları için bkz: [yönetmek DNS kayıtlarını ve kayıt kümelerini kullanarak hello Azure portal](dns-operations-recordsets-portal.md). 

1. Merhaba ile DNS bölgesi, hello Azure portalında oluşturulan **Sık Kullanılanlar** bölmesinde tıklatın **tüm kaynakları**. Merhaba tıklatın **contoso.com** DNS bölgesi hello tüm kaynak dikey. Merhaba aboneliği zaten içinde birçok kaynak varsa, girebilirsiniz **contoso.com** hello içinde **ada göre Filtrele...** tooeasily erişim hello DNS bölgesi kutusu.

1. Merhaba hello üstündeki **DNS bölgesi** dikey penceresinde, select **+ kayıt kümesine** tooopen hello **kayıt kümesi ekleme** dikey.

1. Merhaba üzerinde **kayıt kümesi ekleme** dikey penceresinde hello değerleri aşağıdaki girin ve tıklayın **Tamam**. Bu örnekte, bir A kaydı oluşturuyorsunuz.

   |**Ayar** | **Değer** | **Ayrıntılar** |
   |---|---|---|
   |**Ad**|www|Merhaba kaydın adı|
   |**Tür**|A| Tür DNS kaydı toocreate A, kabul edilebilir değerlerdir AAAA, CNAME, MX, NS, SRV, TXT ve PTR.  Kayıt türleri hakkında daha fazla bilgi için, [DNS bölgelerine ve kayıtlarına genel bakış](dns-zones-records.md) bağlantısını ziyaret edin|
   |**TTL**|1|Time-to-live hello DNS isteği.|
   |**TTL birimi**|Saat|TTL değeri için zaman ölçümü.|
   |**IP adresi**|IP Adresi Değeri| Bu değer hello DNS kaydı çözümleyen hello IP adresidir.|

## <a name="view-records"></a>Kayıtları görüntüleme

Merhaba alt kısmında hello DNS bölgesine dikey penceresinde, hello DNS bölgesi için hello kayıtlarını görebilirsiniz. Her bölgede oluşturulan, hello varsayılan DNS ve SOA kayıtları, artı, oluşturduğunuz tüm yeni kayıtlar görmeniz gerekir.

![bölge](./media/dns-getstarted-portal/viewzone500.png)


## <a name="update-name-servers"></a>Ad sunucularını güncelleştirme

Sonra DNS bölgesi ve kayıtları doğru şekilde ayarlanan, tooconfigure gerek memnun, etki alanı adı toouse hello Azure DNS ad sunucuları. Bu DNS kayıtlarınızı hello Internet toofind üzerindeki diğer kullanıcılarla sağlar.

bölgenizin ad sunucuları Hello hello Azure portalında sunulur:

![bölge](./media/dns-getstarted-portal/viewzonens500.png)

Bu ad sunucuları hello etki alanı adı kayıt (Merhaba etki alanı adı satın aldığınız yerden) ile yapılandırılmalıdır. Kayıt hello seçeneği tooset hello ad sunucuları hello etki alanı için yukarı sunar. Daha fazla bilgi için bkz: [, etki alanı tooAzure DNS temsilci](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Tüm kaynakları silme

Bu makalede, aşağıdaki adımları tam hello oluşturulan tüm kaynakları toodelete:

1. Hello Azure portal'ın **Sık Kullanılanlar** bölmesinde tıklatın **tüm kaynakları**. Merhaba tıklatın **MyResourceGroup** kaynak tüm kaynaklar dikey penceresinde hello grubu. Merhaba aboneliği zaten içinde birçok kaynak varsa, girebilirsiniz **MyResourceGroup** hello içinde **ada göre Filtrele...** kutusunu tooeasily erişim hello kaynak grubu.
1. Merhaba, **MyResourceGroup** dikey penceresinde hello tıklatın **silmek** düğmesi.
1. Merhaba portal tootype hello toodelete istediğiniz hello kaynak grubu tooconfirm adını gerektirir. Tıklatın **silmek**, türü *MyResourceGroup* hello kaynak grubu adı için ardından **silmek**. Bu nedenle her zaman emin tooconfirm silmeden önce bir kaynak grubu Merhaba içeriğine olması, bir kaynak grubunu silme hello kaynak grubundaki tüm kaynakları siler. Merhaba portal hello kaynak grubu içinde bulunan tüm kaynakları siler ve sonra hello kaynak grubu kendisini siler. Bu işlem birkaç dakika sürer.


## <a name="next-steps"></a>Sonraki adımlar

Azure DNS hakkında daha fazla toolearn bkz [Azure DNS'ye genel bakış](dns-overview.md).

Azure DNS'de DNS kayıtlarını yönetme hakkında daha fazla toolearn bkz [yönetmek DNS kayıtlarını ve kayıt kümelerini kullanarak hello Azure portal](dns-operations-recordsets-portal.md).

