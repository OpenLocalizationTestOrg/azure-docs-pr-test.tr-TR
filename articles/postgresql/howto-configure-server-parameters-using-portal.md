---
title: "Sunucu parametreleri Azure veritabanı'nda PostgreSQL için Azure portalı üzerinden yapılandırma | Microsoft Docs"
description: "Bu makalede sunucu parametreleri Azure veritabanı'nda PostgreSQL için Azure portalı üzerinden nasıl yapılandırılacağını açıklar."
services: postgresql
author: rachel-msft
ms.author: raagyema
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 11/08/2017
ms.openlocfilehash: 9e8262fbfcde2e69a656e356a7ab241f2d5043ad
ms.sourcegitcommit: 93902ffcb7c8550dcb65a2a5e711919bd1d09df9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/09/2017
---
# <a name="configure-server-parameters-in-azure-portal"></a>Azure portalında sunucu parametreleri yapılandırın
Listesinde, Göster ve Azure portalı üzerinden PostgreSQL sunucu için bir Azure veritabanı için yapılandırma parametreleri güncelleştirin.

## <a name="prerequisites"></a>Ön koşullar
Nasıl yapılır bu kılavuzu adım gerekir:
- [Azure veritabanı PostgreSQL sunucu için](quickstart-create-server-database-portal.md)

## <a name="viewing-and-editing-parameters"></a>Görüntüleme ve parametreleri düzenleme
1. [Azure portalı](https://portal.azure.com) açın.

2. Azure veritabanınızı PostgreSQL sunucusu seçin.

3. Altında **ayarları** bölümünde, select **sunucu parametreleri**. Sayfa parametreleri, değerleri ve açıklamaları listesini gösterir.
![Parametreler için genel bakış sayfası](./media/howto-configure-server-parameters-in-portal/3-overview-of-parameters.png)

4. Seçin **açılan** client_min_messages gibi numaralandırılan türü parametreleri için olası değerler görmek için düğmesi.
![Aşağı açılan listeleme](./media/howto-configure-server-parameters-in-portal/4-enum-drop-down.png)

5. Seçin veya üzerine gelerek **ı** cpu_index_tuple_cost gibi sayısal parametreleri için olası değerler aralığını görmek için (bilgileri) düğmesini.
![bilgi düğmesi](./media/howto-configure-server-parameters-in-portal/4-information-button.png)

6. Gerekirse, kullanın **arama kutusu** belirli bir parametrenin Dar Aşağı için. Arama ad ve açıklama parametreleri olur.
![Arama sonuçları](./media/howto-configure-server-parameters-in-portal/5-search.png)

7. Ayarlamak istediğiniz parametre değerlerini değiştirin. Bir oturumda yaptığınız tüm değişiklikleri mor ile vurgulanır. Değerleri değişmiş sonra seçebileceğiniz **kaydetmek**. Veya **atmak** değişikliklerinizi.
![Kaydet veya değişiklikleri at](./media/howto-configure-server-parameters-in-portal/6-save-and-discard-buttons.png)

8. Yeni parametre değerlerini kaydettiyseniz, her zaman varsayılan değerleri dön her şeyi seçerek geri dönebilirsiniz **tümünü Varsayılana Sıfırla**.
![Tüm Varsayılana sıfırla](./media/howto-configure-server-parameters-in-portal/7-reset-to-default-button.png)

## <a name="next-steps"></a>Sonraki adımlar
Hakkında bilgi edinin:
- [Azure veritabanı PostgreSQL için sunucu parametrelerinde genel bakış](concepts-servers.md)
- [Azure CLI kullanarak parametrelerini yapılandırma](howto-configure-server-parameters-using-cli.md)
