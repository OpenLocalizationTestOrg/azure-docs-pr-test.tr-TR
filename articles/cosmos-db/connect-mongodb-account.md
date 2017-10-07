---
title: "bir Azure Cosmos DB hesaba aaaMongoDB bağlantı dizesini | Microsoft Docs"
description: "Tooconnect MongoDB uygulama tooan Azure Cosmos DB nasıl hesap MongoDB bağlantı dizesi kullanarak öğrenin."
keywords: "mongodb bağlantı dizesi"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: e36f7375-9329-403b-afd1-4ab49894f75e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.openlocfilehash: c0b81cb49a10e09e3f02411b91731c7f980ec47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-mongodb-application-tooazure-cosmos-db"></a>MongoDB uygulama tooAzure Cosmos DB Bağlan
Tooconnect MongoDB uygulama tooan Azure Cosmos DB nasıl hesap MongoDB bağlantı dizesi kullanarak öğrenin. Sonra Azure Cosmos DB veritabanı hello verileri olarak kullanabileceğiniz depolama MongoDB uygulamanız için. 

Bu öğretici tooretrieve bağlantı dizesi bilgilerini sağlayan iki yöntem sunar:

- [Merhaba Hızlı Başlangıç yöntemi](#QuickstartConnection), .NET, Node.js, MongoDB Kabuk, Java ve Python sürücüleri ile kullanmak için
- [Merhaba özel bir bağlantı dizesi yöntemi](#GetCustomConnection), diğer sürücülerin ile kullanmak için

## <a name="prerequisites"></a>Ön koşullar

- Bir Azure hesabı. Bir Azure hesabınız yoksa, oluşturma bir [ücretsiz Azure hesabı](https://azure.microsoft.com/free/) şimdi. 
- Bir Azure Cosmos DB hesabı. Yönergeler için bkz: [.NET ile MongoDB API web uygulaması oluşturma ve Azure portal hello](create-mongodb-dotnet.md).

## <a id="QuickstartConnection"></a>Merhaba Hızlı Başlangıç'ı kullanarak Hello MongoDB bağlantı dizesi alma
1. Bir Internet tarayıcısında toohello içinde oturum [Azure portal](https://portal.azure.com).
2. Merhaba, **Azure Cosmos DB** dikey penceresinde, select hello API MongoDB hesabı. 
3. Merhaba sol hello hesabı dikey bölmesinde **Hızlı Başlangıç**. 
4. Platformunuzu seçin (**.NET**, **Node.js**, **MongoDB Kabuk**, **Java**, **Python**). Sürücü veya listelenen, aracı endişelenmeyin--görmüyorsanız, biz sürekli olarak daha fazla bağlantı kod parçacıkları belge. Lütfen aşağıda ne istiyorsunuz üzerinde açıklama toosee. toolearn nasıl toocraft kendi bağlantısını oku [hello hesabın bağlantı dizesi bilgilerini al](#GetCustomConnection).
5. Kopyalayıp MongoDB uygulamanıza hello kod parçacığını yapıştırın.

    ![Hızlı Başlangıç dikey penceresi](./media/connect-mongodb-account/QuickStartBlade.png)

## <a id="GetCustomConnection"></a>Merhaba MongoDB bağlantı dizesi toocustomize Al
1. Bir Internet tarayıcısında toohello içinde oturum [Azure portal](https://portal.azure.com).
2. Merhaba, **Azure Cosmos DB** dikey penceresinde, select hello API MongoDB hesabı. 
3. Merhaba sol hello hesabı dikey bölmesinde **bağlantı dizesi**. 
4. Merhaba **bağlantı dizesi** dikey pencere açılır. Bu, tüm hello bilgiler gerekli tooconnect toohello hesabı preconstructed bağlantı dizesi dahil olmak üzere MongoDB için bir sürücü kullanarak sahip olur.

    ![Bağlantı dizesi dikey penceresi](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a>Bağlantı dizesi gereksinimleri
> [!Important]
> Azure Cosmos DB sıkı güvenlik gereksinimlerine ve standartları vardır. Azure Cosmos DB hesapların gerektirdiği kimlik doğrulaması ve güvenli iletişim aracılığıyla *SSL*. 
>
>

Azure Cosmos DB destekleyen hello standart MongoDB bağlantı dizesi URI biçimi, birkaç belirli gereksinimleri: Azure Cosmos DB hesapları, kimlik doğrulama ve SSL üzerinden güvenli iletişim gerektirir. Bu nedenle, hello bağlantı dizesi biçimi şöyledir:

    mongodb://username:password@host:port/[database]?ssl=true

Merhaba Bu dize değerleri hello kullanılabilir **bağlantı dizesi** daha önce gösterilen dikey penceresinde:

* Kullanıcı adı (gerekli): Azure Cosmos DB hesap adı.
* Parola (gerekli): Azure Cosmos DB hesap parolası.
* Ana bilgisayar (gerekli): hello Azure Cosmos DB hesabı'nın FQDN'si.
* Bağlantı noktası (gerekli): 10255 değerini bulur.
* Veritabanı (isteğe bağlı): bağlantı hello hello veritabanı kullanır. Hiçbir veritabanı sağladıysanız, "test" Merhaba varsayılan veritabanı.
* SSL = true (gerekli)

Örneğin, hello gösterilen hello hesap göz önünde bulundurun **bağlantı dizesi** dikey. Geçerli bir bağlantı dizesi şöyledir:

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[MongoChef kullanmak](mongodb-mongochef.md) Azure Cosmos DB API MongoDB hesabı ile.
* Hello Azure Cosmos DB API MongoDB için görüntüleyerek keşfedin [örnekleri](mongodb-samples.md).
