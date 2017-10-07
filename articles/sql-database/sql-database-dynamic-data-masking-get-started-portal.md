---
title: "Azure portal: SQL veritabanı dinamik veri maskeleme | Microsoft Docs"
description: "Tooget SQL veritabanını dinamik veri maskeleme hello Azure Portal ile çalışmaya nasıl"
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: "2"
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: ronitr; ronmat
ms.openlocfilehash: 5c5f74682a15d42eceb78c3ca0705401e1ac0ae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-hello-azure-portal"></a>SQL veritabanı dinamik veri maskeleme hello Azure Portal ile kullanmaya başlama

Bu konu, nasıl gösterir tooimplement [dinamik veri maskeleme](sql-database-dynamic-data-masking-get-started.md) hello Azure portal ile. Dinamik veri maskeleme kullanarak uygulayabileceğiniz [Azure SQL veritabanı cmdlet'leri](https://msdn.microsoft.com/library/azure/mt574084.aspx) veya hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx).


## <a name="set-up-dynamic-data-masking-for-your-database-using-hello-azure-portal"></a>Hello Azure Portal kullanarak veritabanınız için dinamik veri maskeleme ayarlama
1. Başlatma hello Azure portalında [https://portal.azure.com](https://portal.azure.com).
2. Toohello ayarları dikey toomask istediğiniz hello hassas verileri içeren hello veritabanının gidin.
3. Merhaba tıklatın **dinamik veri maskeleme** hello başlatan kutucuğa **dinamik veri maskeleme** yapılandırma dikey penceresi.
   
   * Alternatif olarak, toohello kaydırabilirsiniz **Operations** 'ye tıklayın **dinamik veri maskeleme**.
     
     ![Gezinti Bölmesi](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. Merhaba, **dinamik veri maskeleme** bazı veritabanı sütunlarını karşılaşabileceğiniz yapılandırma dikey penceresinde hello önerileri altyapının işaretlenen maskeleme için. İçinde hello önerileri tooaccept sipariş, portalın **Maskesi Ekle** bir veya daha fazla sütun ve maskesi hello varsayılan türü bu sütun için temel alınarak oluşturulur. Merhaba maskeleme kuralı tıklayarak ve alan biçimi tooa farklı biçim tercih ettiğiniz maskeleme hello düzenleme maskeleme işlevi hello değiştirebilirsiniz. Emin tooclick olması **kaydetmek** toosave ayarlarınızı.
   
    ![Gezinti Bölmesi](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. tooadd hello hello üstündeki veritabanınızda herhangi bir sütun için bir maskesi **dinamik veri maskeleme** yapılandırma dikey penceresinde **Maskesi Ekle** tooopen hello **maskeleme Kuralı Ekle** Yapılandırma dikey penceresi
   
    ![Gezinti Bölmesi](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. Select hello **şema**, **tablo** ve **sütun** toodefine hello maskeleneceğini alan atanmış.
7. Seçin bir **maskeleme alan biçimini** hassas verileri maskeleme kategorileri hello listesinden.
   
    ![Gezinti Bölmesi](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. Tıklatın **kaydetmek** hello dinamik veri maskeleme İlkesi kurallarında maskeleme kuralı dikey tooupdate hello kümesi maskeleme hello veri.
9. Türü hello SQL kullanıcılar veya maskeleme işlemi bırakılmalıdır ve erişim maskelenmeyen toohello hassas verileri AAD kimlikleri. Bu kullanıcılar noktalı virgülle ayrılmış bir listesi olmalıdır. Yönetici ayrıcalıklarına sahip kullanıcılar her zaman erişim toohello özgün maskelenmemiş veri gerektiğini unutmayın.
   
    ![Gezinti Bölmesi](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > Bu nedenle hello uygulama katmanı toomake uygulama ayrıcalıklı kullanıcılar için hassas verileri görüntüleyin, hello SQL kullanıcı eklemek veya AAD kimlik Merhaba uygulaması tooquery hello veritabanı kullanır. Bu liste ayrıcalıklı kullanıcıların toominimize Etkilenme hello gizli verilerin en az bir sayı içermesi önerilir.
   > 
   > 
10. Tıklatın **kaydetmek** yapılandırma dikey toosave hello yeni veya güncelleştirilmiş maskeleme ilkenin maskeleme hello veri.


## <a name="next-steps"></a>Sonraki adımlar

* Dinamik veri maskeleme genel bakış için bkz: [dinamik veri maskeleme](sql-database-dynamic-data-masking-get-started.md).
* Dinamik veri maskeleme kullanarak uygulayabileceğiniz [Azure SQL veritabanı cmdlet'leri](https://msdn.microsoft.com/library/azure/mt574084.aspx) veya hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx).
