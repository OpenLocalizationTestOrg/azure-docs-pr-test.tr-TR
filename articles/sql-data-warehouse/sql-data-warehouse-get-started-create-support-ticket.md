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
# <a name="how-toocreate-a-support-ticket-for-sql-data-warehouse"></a><span data-ttu-id="b39d9-103">Nasıl toocreate bir destek bileti SQL Data Warehouse için</span><span class="sxs-lookup"><span data-stu-id="b39d9-103">How toocreate a support ticket for SQL Data Warehouse</span></span>
<span data-ttu-id="b39d9-104">SQL Veri Ambarı’nız ile ilgili herhangi bir sorun yaşıyorsanız lütfen mühendislik ekibimizin size yardımcı olabilmesi için bir destek bileti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b39d9-104">If you are having any issues with your SQL Data Warehouse, please create a support ticket so that our engineering team can assist you.</span></span>

> [!NOTE] 
> <span data-ttu-id="b39d9-105">12/20/2016 itibariyle hello kaynak sistem durumu denetimi hello Azure portal'ın doğru değil.</span><span class="sxs-lookup"><span data-stu-id="b39d9-105">As of 12/20/2016, hello resource health check in hello Azure portal is not accurate.</span></span> <span data-ttu-id="b39d9-106">Etkin olarak toofix bu sorunu çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="b39d9-106">We are actively working toofix this issue.</span></span> 


## <a name="create-a-support-ticket"></a><span data-ttu-id="b39d9-107">Destek bileti oluşturma</span><span class="sxs-lookup"><span data-stu-id="b39d9-107">Create a support ticket</span></span>
1. <span data-ttu-id="b39d9-108">Açık hello [Azure portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="b39d9-108">Open hello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="b39d9-109">Hello giriş ekranında hello tıklatın **Yardım + Destek** döşeme.</span><span class="sxs-lookup"><span data-stu-id="b39d9-109">On hello Home screen, click hello **Help + support** tile.</span></span>
   
    ![Yardım + destek](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. <span data-ttu-id="b39d9-111">Merhaba Yardım + destek dikey penceresinde üzerinde tıklatın **yeni destek isteği**.</span><span class="sxs-lookup"><span data-stu-id="b39d9-111">On hello Help + Support blade, click **Create support request**.</span></span>
   
    ![Yeni destek isteği](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. <span data-ttu-id="b39d9-113">Select hello **istek türü**.</span><span class="sxs-lookup"><span data-stu-id="b39d9-113">Select hello **Request Type**.</span></span>
   
    ![İstek türü](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > <span data-ttu-id="b39d9-115">Varsayılan olarak her SQL sunucusu (örn. myserver.database.windows.net) 45.000’lik **DTU Kotası**’na sahiptir.</span><span class="sxs-lookup"><span data-stu-id="b39d9-115">By default, each SQL server (e.g. myserver.database.windows.net) has a **DTU Quota** of 45,000.</span></span> <span data-ttu-id="b39d9-116">Bu kota yalnızca bir güvenlik sınırıdır.</span><span class="sxs-lookup"><span data-stu-id="b39d9-116">This quota is simply a safety limit.</span></span> <span data-ttu-id="b39d9-117">Bir destek bileti oluşturma ve seçerek kotayı artırabilir *kota* hello istek türü.</span><span class="sxs-lookup"><span data-stu-id="b39d9-117">You can increase your quota by creating a support ticket and selecting *Quota* as hello request type.</span></span> <span data-ttu-id="b39d9-118">gerekli için DTU Çarp toocalculate hello 7.5 hello toplam [DWU] [ DWU] gerekli.</span><span class="sxs-lookup"><span data-stu-id="b39d9-118">toocalculate your DTU needs, multiply hello 7.5 by hello total [DWU][DWU] needed.</span></span> <span data-ttu-id="b39d9-119">Örneğin, iki toohost istediğiniz bir SQL server, ardından üzerinde DW6000s 90,000 DTU kotası isteği.</span><span class="sxs-lookup"><span data-stu-id="b39d9-119">For example, you would like toohost two DW6000s on one SQL server, then you should request a DTU quota of 90,000.</span></span>  <span data-ttu-id="b39d9-120">Geçerli bir DTU tüketimi hello SQL server dikey penceresinden hello Portalı'nda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b39d9-120">You can view your current DTU consumption from hello SQL server blade in hello portal.</span></span> <span data-ttu-id="b39d9-121">Duraklatıldı ve duraklatılmamış veritabanları hello DTU kota doğru sayısı.</span><span class="sxs-lookup"><span data-stu-id="b39d9-121">Both paused and un-paused databases count toward hello DTU quota.</span></span> 
   > 
   > 
5. <span data-ttu-id="b39d9-122">Select hello **abonelik** ana veritabanı hello sorunu Raporlama ile Merhaba.</span><span class="sxs-lookup"><span data-stu-id="b39d9-122">Select hello **Subscription** that hosts hello database with hello problem you are reporting.</span></span>
   
    ![Abonelik](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. <span data-ttu-id="b39d9-124">Seçin **SQL Data Warehouse** kaynak hello gibi.</span><span class="sxs-lookup"><span data-stu-id="b39d9-124">Select **SQL Data Warehouse** as hello Resource.</span></span>
   
    ![Kaynak](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. <span data-ttu-id="b39d9-126">[Azure destek planınızı][Azure support plan] seçin.</span><span class="sxs-lookup"><span data-stu-id="b39d9-126">Select your [Azure support plan][Azure support plan].</span></span>
   
   * <span data-ttu-id="b39d9-127">Tüm destek düzeylerinde **faturalama, kota ve abonelik yönetimi** desteği sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b39d9-127">**Billing, quota and subscription management** support is available at all support levels.</span></span>
   * <span data-ttu-id="b39d9-128">**Onarım** desteği [Geliştirici][Developer], [Standart][Standard], [Profesyonel Doğrudan][Professional Direct] veya [Premier][Premier] destek aracılığıyla sağlanır.</span><span class="sxs-lookup"><span data-stu-id="b39d9-128">**Break-fix** support is provided through [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] or [Premier][Premier] support.</span></span> <span data-ttu-id="b39d9-129">Onarım sorunlardır müşteriler tarafından Azure'ı kullandığı sırada karşılaştıkları sorunlar bu neden Microsoft hello sorunu makul beklentiler olduğu.</span><span class="sxs-lookup"><span data-stu-id="b39d9-129">Break-fix issues are problems experienced by customers while using Azure where there is a reasonable expectation that Microsoft caused hello problem.</span></span>
   * <span data-ttu-id="b39d9-130">**Geliştirici rehberliği** ve **Danışmanlık Hizmetleri** hello kullanılabilir [profesyonel doğrudan] [ Professional Direct] ve [Premier] [ Premier] destek düzeyleri.</span><span class="sxs-lookup"><span data-stu-id="b39d9-130">**Developer mentoring** and **advisory services** are available at hello [Professional Direct][Professional Direct] and [Premier][Premier] support levels.</span></span> 
     
     <span data-ttu-id="b39d9-131">Bir Premier Destek planınız varsa SQL Data Warehouse de rapor edebilirsiniz hello sorunlarıyla ilgili [Microsoft Premier çevrimiçi portalı][Microsoft Premier online portal].</span><span class="sxs-lookup"><span data-stu-id="b39d9-131">If you have a Premier support plan, you can also report SQL Data Warehouse related issues on hello [Microsoft Premier online portal][Microsoft Premier online portal].</span></span>  <span data-ttu-id="b39d9-132">Bkz: [Azure destek planları] [ Azure support plan] toolearn çeşitli destek planları, kapsam, yanıt süreleri ve fiyatlandırma dahil olmak üzere hello hakkında daha fazla vs.  Azure desteği ile ilgili sık sorulan sorular için bkz. [Azure desteği ile ilgili SSS][Azure support FAQs].</span><span class="sxs-lookup"><span data-stu-id="b39d9-132">See [Azure support plans][Azure support plan] toolearn more about hello various support plans, including scope, response times, pricing, etc.  For frequently asked questions about Azure support, see [Azure support FAQs][Azure support FAQs].</span></span>  
     
     ![Destek planı](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. <span data-ttu-id="b39d9-134">Select hello **sorun türü** ve **kategori**.</span><span class="sxs-lookup"><span data-stu-id="b39d9-134">Select hello **Problem Type** and **Category**.</span></span> <span data-ttu-id="b39d9-135">Bu örnekte, biz "Araçlar" Merhaba sorun türü olarak ve "İstemci araçları" Merhaba kategori olarak seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="b39d9-135">In this example, we have chosen "Tools" as hello Problem type and "Client tools" as hello category.</span></span> 
   
    ![Sorun türü kategori](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. <span data-ttu-id="b39d9-137">Merhaba sorunu açıklayın ve iş etkisi hello düzeyini seçin.</span><span class="sxs-lookup"><span data-stu-id="b39d9-137">Describe hello problem and choose hello level of business impact.</span></span>
   
    ![Sorun açıklaması](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. <span data-ttu-id="b39d9-139">Bu destek bileti için **iletişim bilgileriniz** önceden doldurulur.</span><span class="sxs-lookup"><span data-stu-id="b39d9-139">Your **contact information** for this support ticket will be pre-filled.</span></span> <span data-ttu-id="b39d9-140">Gerekli gördüğünüz halde bilgilerinizi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="b39d9-140">Update this if necessary.</span></span>
    
    ![İletişim bilgileri](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. <span data-ttu-id="b39d9-142">Tıklatın **oluşturma** toosubmit hello destek isteği.</span><span class="sxs-lookup"><span data-stu-id="b39d9-142">Click **Create** toosubmit hello support request.</span></span>

## <a name="monitor-a-support-ticket"></a><span data-ttu-id="b39d9-143">Destek biletini izleme</span><span class="sxs-lookup"><span data-stu-id="b39d9-143">Monitor a support ticket</span></span>
<span data-ttu-id="b39d9-144">Merhaba destek isteğini gönderdikten sonra hello Azure destek ekibi sizinle iletişime geçer.</span><span class="sxs-lookup"><span data-stu-id="b39d9-144">After you have submitted hello support request, hello Azure support team will contact you.</span></span> <span data-ttu-id="b39d9-145">toocheck isteği durumu ve ayrıntıları tıklatın **destek isteklerini yönetin** hello Panoda.</span><span class="sxs-lookup"><span data-stu-id="b39d9-145">toocheck your request status and details, click **Manage support requests** on hello dashboard.</span></span>

![Durumu kontrol etme](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a><span data-ttu-id="b39d9-147">Diğer Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b39d9-147">Other Resources</span></span>
<span data-ttu-id="b39d9-148">Ayrıca, üzerinde hello ile SQL Data Warehouse topluluğuna bağlanabilirsiniz [yığın taşması] [ Stack Overflow] veya hello [Azure SQL Data Warehouse MSDN Forumu] [ Azure SQL Data Warehouse MSDN forum].</span><span class="sxs-lookup"><span data-stu-id="b39d9-148">Additionally, you can connect with hello SQL Data Warehouse community on [Stack Overflow][Stack Overflow] or on hello [Azure SQL Data Warehouse MSDN forum][Azure SQL Data Warehouse MSDN forum].</span></span>

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

