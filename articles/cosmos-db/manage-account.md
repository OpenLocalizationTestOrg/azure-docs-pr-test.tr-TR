---
title: "aaaManage hello Azure Portalı aracılığıyla Azure Cosmos DB hesap | Microsoft Docs"
description: "Nasıl toomanage Azure Cosmos DB hesap hello Azure Portal öğrenin. Hello Azure Portal tooview, kopyalama, silme ve erişimi hesaplarını kullanma hakkında bir kılavuz bulabilirsiniz."
keywords: Azure Portal, documentdb, azure, Microsoft azure
services: cosmos-db
documentationcenter: 
author: kirillg
manager: jhubbard
editor: cgronlun
ms.assetid: 00fc172f-f86c-44ca-8336-11998dcab45c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kirillg
ms.openlocfilehash: 77ad953cf558a519674be08ad913a12202f69496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-an-azure-cosmos-db-account"></a>Nasıl toomanage Azure Cosmos DB hesabı
Bilgi nasıl tooset genel tutarlılık, iş anahtarlarla ve hello Azure portalında Azure Cosmos DB hesabında silin.

## <a id="consistency"></a>Azure Cosmos DB tutarlılık ayarlarını yönet
Merhaba sağ tutarlılık düzeyi seçerek uygulamanızı hello semantiği bağlıdır. Azure Cosmos veritabanı hello kullanılabilir tutarlılık düzeylerini okuyarak öğrenmeniz [toomaximize kullanılabilirlik ve Azure Cosmos veritabanı performans düzeyleri tutarlılık kullanarak][consistency]. Azure Cosmos DB tutarlılık, kullanılabilirlik ve veritabanı hesabınız için kullanılabilir her tutarlılık düzeyinde performans garantileri sağlar. Güçlü tutarlılık düzeyi olan veritabanı hesabınızı yapılandırma verilerinizi yalıtılmış tooa tek Azure bölgesi olmasını gerektirir ve genel olarak kullanılabilir. Üzerinde diğer yandan Merhaba, gevşek tutarlılık düzeylerini - sınırlanmış eskime durumu, session veya son etkinleştir Merhaba, tooassociate veritabanı hesabınızı bilgileriyle Azure bölgelerinin herhangi bir sayı. şu basit adımları hello nasıl tooselect hello veritabanı hesabınız için varsayılan tutarlılık düzeyi gösterir. 

### <a name="toospecify-hello-default-consistency-for-an-azure-cosmos-db-account"></a>bir Azure Cosmos DB hesap toospecify hello varsayılan tutarlılık
1. Merhaba, [Azure portal](https://portal.azure.com/), Azure Cosmos DB hesabınıza erişemiyor.
2. Merhaba hesabı dikey penceresinde tıklayın **varsayılan tutarlılık**.
3. Merhaba, **varsayılan tutarlılık** dikey penceresinde, select hello yeni tutarlılık düzeyi ve tıklatın **kaydetmek**.
    ![Varsayılan tutarlılık oturumu][5]

## <a id="keys"></a>Görüntülemek, kopyalamak ve erişim anahtarlarını yeniden oluştur
Bir Azure Cosmos DB hesabı oluşturduğunuzda, hello hizmeti hello Azure Cosmos DB hesap erişildiğinde, kimlik doğrulaması için kullanılan iki ana erişim tuşu oluşturur. İki erişim tuşu sağlayarak Azure Cosmos DB tooregenerate hello herhangi kesinti tooyour Azure Cosmos DB hesap anahtarlarla sağlar. 

Merhaba, [Azure portal](https://portal.azure.com/), erişim hello **anahtarları** dikey penceresinde hello hello kaynak menüsünden **Azure Cosmos DB hesap** dikey tooview, kopyalama ve yeniden oluşturma hello erişim tuşları kullanılan tooaccess Azure Cosmos DB hesabınız var.

![Azure Portal ekran, anahtarlar dikey penceresinde](./media/manage-account/keys.png)

> [!NOTE]
> Merhaba **anahtarları** dikey penceresinde de içeren birincil ve kullanılan tooconnect tooyour olabilir ikincil bağlantı dizeleri hesap hello [veri geçiş aracı](import-data.md).
> 
> 

Salt okunur anahtarları de bu dikey pencerede kullanılabilir. Okuma ve salt okunur işlemler while, siler, oluşturur ve değiştirir değil sorgular.

### <a name="copy-an-access-key-in-hello-azure-portal"></a>Hello Azure portalına erişim tuşu kopyalama
Hello üzerinde **anahtarları** dikey penceresinde hello tıklatın **kopyalama** düğmesini toohello hello anahtar sağında toocopy istiyor.

![Görüntüleme ve hello Azure Portal, anahtarlar dikey penceresinde bir erişim tuşu kopyalama](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a>Erişim anahtarlarını yeniden oluştur
Merhaba erişim anahtarları tooyour Azure Cosmos DB hesabı değiştirmelisiniz düzenli aralıklarla toohelp tutmak bağlantılarınızı daha güvenlidir. İki erişim tuşu tooenable atanır, toomaintain bağlantıları toohello bir erişim anahtarı kullanırken, yeniden Azure Cosmos DB hesap hello diğer erişim anahtarı.

> [!WARNING]
> Erişim anahtarlarını yeniden hello geçerli anahtarı bağımlı olan tüm uygulamaları etkiler. Merhaba erişim anahtar tooaccess hello Azure Cosmos DB hesabı kullanan tüm istemciler güncelleştirilmiş toouse hello yeni anahtarı olması gerekir.
> 
> 

Uygulama veya hello Azure Cosmos DB hesabı kullanarak bulut Hizmetleri varsa, anahtarları, yeniden yüklerseniz anahtarları toplamazsanız hello bağlantıları kaybedeceksiniz. Merhaba aşağıdaki adımları hello süreci anahtarlarınızı çalışırken söz konusu ana hatlarıyla anlatılır.

1. Merhaba, uygulama kodu tooreference hello ikincil erişim tuşunu hello Azure Cosmos DB hesap erişim tuşu güncelleştirin.
2. Hello Azure Cosmos DB hesabınız için birincil erişim tuşunu yeniden oluşturun. Merhaba, [Azure Portal](https://portal.azure.com/), Azure Cosmos DB hesabınıza erişemiyor.
3. Merhaba, **Azure Cosmos DB hesabı** dikey penceresinde tıklatın **anahtarları**.
4. Merhaba üzerinde **anahtarları** dikey penceresinde hello üretme düğmesine tıklayın ve ardından **Tamam** tooconfirm toogenerate yeni bir anahtar istiyor.
    ![Erişim anahtarlarını yeniden oluştur](./media/manage-account/regenerate-keys.png)
5. Merhaba yeni anahtara kullanılabilir durumda doğruladıktan sonra (yaklaşık 5 dakika sonra yeniden üretme), uygulama kodu tooreference hello yeni birincil erişim anahtarınızı hello erişim tuşu güncelleştirin.
6. Merhaba ikincil erişim tuşunu yeniden oluşturun.
   
    ![Erişim anahtarlarını yeniden oluştur](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> Azure Cosmos DB hesabınızı, yeni oluşturulan anahtarı kullanılan tooaccess çalıştırılmadan önce birkaç dakika sürebilir.
> 
> 

## <a name="get-hello--connection-string"></a>Merhaba bağlantı dizesi Al
tooretrieve, bağlantı dizesi, aşağıdaki hello: 

1. Merhaba, [Azure portal](https://portal.azure.com), Azure Cosmos DB hesabınıza erişemiyor.
2. Merhaba kaynak menüye tıklayın **anahtarları**.
3. Merhaba tıklatın **kopyalama** düğmesine bir sonraki toohello **birincil bağlantı dizesi** veya **ikincil bağlantı dizesi** kutusu. 

Hello hello bağlantı dizesi kullanıyorsanız [Azure Cosmos DB veritabanı geçiş aracı](import-data.md), hello veritabanı adı toohello hello bağlantı dizesi sonuna ekleyin. `AccountEndpoint=< >;AccountKey=< >;Database=< >`.

## <a id="delete"></a>Bir Azure Cosmos DB hesabını silme
bir Azure Cosmos DB tooremove hesap hello Azure artık kullanıyorsanız, portalı hello hesap adını sağ tıklatın, ve tıklatın **hesabı Sil**.

![Azure portalı bir Azure Cosmos DB toodelete hesabına nasıl hello](./media/manage-account/deleteaccount.png)

1. Merhaba, [Azure portal](https://portal.azure.com/), erişim hello Azure Cosmos DB hesabı toodelete istiyor.
2. Merhaba üzerinde **Azure Cosmos DB hesabı** dikey penceresinde hello hesabını sağ tıklatın ve ardından **hesabı Sil**. 
3. Hello elde edilen onay dikey penceresinde hello Azure Cosmos DB hesap adı tooconfirm toodelete hello hesap istediğinizi yazın.
4. Merhaba tıklatın **silmek** düğmesi.

![Azure portalı bir Azure Cosmos DB toodelete hesabına nasıl hello](./media/manage-account/delete-account-confirm.png)

## <a id="next"></a>Sonraki adımlar
Nasıl çok öğrenin[Azure Cosmos DB hesabınız ile çalışmaya başlama](http://go.microsoft.com/fwlink/p/?LinkId=402364).

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
