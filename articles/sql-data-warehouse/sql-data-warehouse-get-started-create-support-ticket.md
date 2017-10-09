---
title: "aaaHow toocreate SQL Data Warehouse için destek bileti | Microsoft Docs"
description: "Nasıl toocreate bir destek bileti Azure SQL Data Warehouse'da."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: a91d1f53-03cb-464b-9d5b-4a9c1a194ed3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 72f7eac82112fb7f1bfb05abca4ce40aeb3c828c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-support-ticket-for-sql-data-warehouse"></a>Nasıl toocreate bir destek bileti SQL Data Warehouse için
SQL Veri Ambarı’nız ile ilgili herhangi bir sorun yaşıyorsanız lütfen mühendislik ekibimizin size yardımcı olabilmesi için bir destek bileti oluşturun.

> [!NOTE] 
> 12/20/2016 itibariyle hello kaynak sistem durumu denetimi hello Azure portal'ın doğru değil. Etkin olarak toofix bu sorunu çalışıyoruz. 


## <a name="create-a-support-ticket"></a>Destek bileti oluşturma
1. Açık hello [Azure portal][Azure portal].
2. Hello giriş ekranında hello tıklatın **Yardım + Destek** döşeme.
   
    ![Yardım + destek](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. Merhaba Yardım + destek dikey penceresinde üzerinde tıklatın **yeni destek isteği**.
   
    ![Yeni destek isteği](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. Select hello **istek türü**.
   
    ![İstek türü](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > Varsayılan olarak her SQL sunucusu (örn. myserver.database.windows.net) 45.000’lik **DTU Kotası**’na sahiptir. Bu kota yalnızca bir güvenlik sınırıdır. Bir destek bileti oluşturma ve seçerek kotayı artırabilir *kota* hello istek türü. gerekli için DTU Çarp toocalculate hello 7.5 hello toplam [DWU] [ DWU] gerekli. Örneğin, iki toohost istediğiniz bir SQL server, ardından üzerinde DW6000s 90,000 DTU kotası isteği.  Geçerli bir DTU tüketimi hello SQL server dikey penceresinden hello Portalı'nda görüntüleyebilirsiniz. Duraklatıldı ve duraklatılmamış veritabanları hello DTU kota doğru sayısı. 
   > 
   > 
5. Select hello **abonelik** ana veritabanı hello sorunu Raporlama ile Merhaba.
   
    ![Abonelik](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. Seçin **SQL Data Warehouse** kaynak hello gibi.
   
    ![Kaynak](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. [Azure destek planınızı][Azure support plan] seçin.
   
   * Tüm destek düzeylerinde **faturalama, kota ve abonelik yönetimi** desteği sunulmaktadır.
   * **Onarım** desteği [Geliştirici][Developer], [Standart][Standard], [Profesyonel Doğrudan][Professional Direct] veya [Premier][Premier] destek aracılığıyla sağlanır. Onarım sorunlardır müşteriler tarafından Azure'ı kullandığı sırada karşılaştıkları sorunlar bu neden Microsoft hello sorunu makul beklentiler olduğu.
   * **Geliştirici rehberliği** ve **Danışmanlık Hizmetleri** hello kullanılabilir [profesyonel doğrudan] [ Professional Direct] ve [Premier] [ Premier] destek düzeyleri. 
     
     Bir Premier Destek planınız varsa SQL Data Warehouse de rapor edebilirsiniz hello sorunlarıyla ilgili [Microsoft Premier çevrimiçi portalı][Microsoft Premier online portal].  Bkz: [Azure destek planları] [ Azure support plan] toolearn çeşitli destek planları, kapsam, yanıt süreleri ve fiyatlandırma dahil olmak üzere hello hakkında daha fazla vs.  Azure desteği ile ilgili sık sorulan sorular için bkz. [Azure desteği ile ilgili SSS][Azure support FAQs].  
     
     ![Destek planı](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. Select hello **sorun türü** ve **kategori**. Bu örnekte, biz "Araçlar" Merhaba sorun türü olarak ve "İstemci araçları" Merhaba kategori olarak seçtiniz. 
   
    ![Sorun türü kategori](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. Merhaba sorunu açıklayın ve iş etkisi hello düzeyini seçin.
   
    ![Sorun açıklaması](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. Bu destek bileti için **iletişim bilgileriniz** önceden doldurulur. Gerekli gördüğünüz halde bilgilerinizi güncelleştirin.
    
    ![İletişim bilgileri](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. Tıklatın **oluşturma** toosubmit hello destek isteği.

## <a name="monitor-a-support-ticket"></a>Destek biletini izleme
Merhaba destek isteğini gönderdikten sonra hello Azure destek ekibi sizinle iletişime geçer. toocheck isteği durumu ve ayrıntıları tıklatın **destek isteklerini yönetin** hello Panoda.

![Durumu kontrol etme](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a>Diğer Kaynaklar
Ayrıca, üzerinde hello ile SQL Data Warehouse topluluğuna bağlanabilirsiniz [yığın taşması] [ Stack Overflow] veya hello [Azure SQL Data Warehouse MSDN Forumu] [ Azure SQL Data Warehouse MSDN forum].

<!--Image references--> 

<!--Article references--> 
[DWU]: ./sql-data-warehouse-overview-what-is.md

<!--MSDN references--> 

<!--Other web references--> 
[Azure portal]: https://portal.azure.com/
[Azure support plan]: https://azure.microsoft.com/support/plans/?WT.mc_id=Support_Plan_510979/  
[Developer]: https://azure.microsoft.com/support/plans/developer/  
[Standard]: https://azure.microsoft.com/support/plans/standard/  
[Professional Direct]: https://azure.microsoft.com/support/plans/prodirect/  
[Premier]: https://azure.microsoft.com/support/plans/premier/  
[Azure support FAQs]: https://azure.microsoft.com/support/faq/
[Microsoft Premier online portal]: https://premier.microsoft.com/
[Stack Overflow]: https://stackoverflow.com/questions/tagged/azure-sqldw/
[Azure SQL Data Warehouse MSDN forum]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse/

