---
title: aaaUse Azure Cosmos DB Robomongo | Microsoft Docs
description: "Bilgi nasıl toouse bir Azure Cosmos DB ile Robomongo: API MongoDB hesabı"
keywords: robomongo
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 3018243e904015426dc69a69b26fb53421e1fe4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a>Bir Azure Cosmos DB ile Robomongo kullanın: API MongoDB hesabı
tooconnect tooan Azure Cosmos DB: API MongoDB hesabının Robomongo kullanarak, şunları yapmalısınız:

* İndirme ve yükleme [Robomongo](https://robomongo.org/)
* Azure Cosmos DB sahip: API MongoDB hesabı için [bağlantı dizesi](connect-mongodb-account.md) bilgileri

## <a name="connect-using-robomongo"></a>Robomongo kullanarak bağlan
tooadd Azure Cosmos DB: API MongoDB hesap toohello Robomongo MongoDB bağlantıları için hello aşağıdaki adımları gerçekleştirin.

1. Azure Cosmos DB almak: API MongoDB hesap bağlantı bilgilerini hello yönergeleri kullanarak [burada](connect-mongodb-account.md).

    ![Merhaba bağlantı dizesi dikey penceresi ekran görüntüsü](./media/mongodb-robomongo/connectionstringblade.png)
2. Çalıştırma *Robomongo.exe*

3. Merhaba bağlantı düğmesini altında **dosya** toomanage bağlantılarınızı. ' Ye tıklayın **oluşturma** hello içinde **MongoDB bağlantıları** hello açılır pencere **bağlantı ayarlarını** penceresi.

4. Merhaba, **bağlantı ayarlarını** penceresinde, bir ad seçin. Ardından, hello bulur **konak** ve **bağlantı noktası** adım 1, bağlantı bilgileri ve bunların içine girin **adresi** ve **bağlantı noktası**sırasıyla .

    ![Merhaba Robomongo bağlantılarını yönet ekran görüntüsü](./media/mongodb-robomongo/manageconnections.png)
5. Merhaba üzerinde **kimlik doğrulaması** sekmesini tıklatın, **gerçekleştirme kimlik doğrulama**. Ardından, veritabanınızın girin (varsayılan değer *yönetici*), **kullanıcı adı** ve **parola**.
Her ikisi de **kullanıcı adı** ve **parola** bağlantı bilgilerinizi adım 1'de bulunabilir.

    ![Merhaba Robomongo kimlik doğrulama sekmesi ekran görüntüsü](./media/mongodb-robomongo/authentication.png)
6. Merhaba üzerinde **SSL** sekmesi, onay **SSL kullan Protokolü**, hello değiştirme **kimlik doğrulama yöntemini** çok**otomatik olarak imzalanan sertifika**.

    ![Merhaba Robomongo SSL sekmesi ekran görüntüsü](./media/mongodb-robomongo/SSL.png)
7. Son olarak, tıklatın **Test** mümkün tooconnect sonra olduğunu tooverify **kaydetmek**.

## <a name="next-steps"></a>Sonraki adımlar
* Azure Cosmos DB keşfedin: API MongoDB için [örnekleri](mongodb-samples.md).
