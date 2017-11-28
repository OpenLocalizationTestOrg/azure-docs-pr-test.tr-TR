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
# <a name="get-started-with-sql-database-dynamic-data-masking-with-hello-azure-portal"></a><span data-ttu-id="a2d8b-103">SQL veritabanı dinamik veri maskeleme hello Azure Portal ile kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a2d8b-103">Get started with SQL Database dynamic data masking with hello Azure Portal</span></span>

<span data-ttu-id="a2d8b-104">Bu konu, nasıl gösterir tooimplement [dinamik veri maskeleme](sql-database-dynamic-data-masking-get-started.md) hello Azure portal ile.</span><span class="sxs-lookup"><span data-stu-id="a2d8b-104">This topic shows you how tooimplement [dynamic data masking](sql-database-dynamic-data-masking-get-started.md) with hello Azure portal.</span></span> <span data-ttu-id="a2d8b-105">Dinamik veri maskeleme kullanarak uygulayabileceğiniz [Azure SQL veritabanı cmdlet'leri](https://msdn.microsoft.com/library/azure/mt574084.aspx) veya hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2d8b-105">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>


## <a name="set-up-dynamic-data-masking-for-your-database-using-hello-azure-portal"></a><span data-ttu-id="a2d8b-106">Hello Azure Portal kullanarak veritabanınız için dinamik veri maskeleme ayarlama</span><span class="sxs-lookup"><span data-stu-id="a2d8b-106">Set up dynamic data masking for your database using hello Azure Portal</span></span>
1. <span data-ttu-id="a2d8b-107">Başlatma hello Azure portalında [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a2d8b-107">Launch hello Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a2d8b-108">Toohello ayarları dikey toomask istediğiniz hello hassas verileri içeren hello veritabanının gidin.</span><span class="sxs-lookup"><span data-stu-id="a2d8b-108">Navigate toohello settings blade of hello database that includes hello sensitive data you want toomask.</span></span>
3. <span data-ttu-id="a2d8b-109">Merhaba tıklatın **dinamik veri maskeleme** hello başlatan kutucuğa **dinamik veri maskeleme** yapılandırma dikey penceresi.</span><span class="sxs-lookup"><span data-stu-id="a2d8b-109">Click hello **Dynamic Data Masking** tile which launches hello **Dynamic Data Masking** configuration blade.</span></span>
   
   * <span data-ttu-id="a2d8b-110">Alternatif olarak, toohello kaydırabilirsiniz **Operations** 'ye tıklayın **dinamik veri maskeleme**.</span><span class="sxs-lookup"><span data-stu-id="a2d8b-110">Alternatively, you can scroll down toohello **Operations** section and click **Dynamic Data Masking**.</span></span>
     
     ![Gezinti Bölmesi](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. <span data-ttu-id="a2d8b-112">Merhaba, **dinamik veri maskeleme** bazı veritabanı sütunlarını karşılaşabileceğiniz yapılandırma dikey penceresinde hello önerileri altyapının işaretlenen maskeleme için.</span><span class="sxs-lookup"><span data-stu-id="a2d8b-112">In hello **Dynamic Data Masking** configuration blade you may see some database columns that hello recommendations engine has flagged for masking.</span></span> <span data-ttu-id="a2d8b-113">İçinde hello önerileri tooaccept sipariş, portalın **Maskesi Ekle** bir veya daha fazla sütun ve maskesi hello varsayılan türü bu sütun için temel alınarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a2d8b-113">In order tooaccept hello recommendations, just click **Add Mask** for one or more columns and a mask will be created based on hello default type for this column.</span></span> <span data-ttu-id="a2d8b-114">Merhaba maskeleme kuralı tıklayarak ve alan biçimi tooa farklı biçim tercih ettiğiniz maskeleme hello düzenleme maskeleme işlevi hello değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2d8b-114">You can change hello masking function by clicking on hello masking rule and editing hello masking field format tooa different format of your choice.</span></span> <span data-ttu-id="a2d8b-115">Emin tooclick olması **kaydetmek** toosave ayarlarınızı.</span><span class="sxs-lookup"><span data-stu-id="a2d8b-115">Be sure tooclick **Save** toosave your settings.</span></span>
   
    ![Gezinti Bölmesi](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. <span data-ttu-id="a2d8b-117">tooadd hello hello üstündeki veritabanınızda herhangi bir sütun için bir maskesi **dinamik veri maskeleme** yapılandırma dikey penceresinde **Maskesi Ekle** tooopen hello **maskeleme Kuralı Ekle** Yapılandırma dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="a2d8b-117">tooadd a mask for any column in your database, at hello top of hello **Dynamic Data Masking** configuration blade click **Add Mask** tooopen hello **Add Masking Rule** configuration blade</span></span>
   
    ![Gezinti Bölmesi](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. <span data-ttu-id="a2d8b-119">Select hello **şema**, **tablo** ve **sütun** toodefine hello maskeleneceğini alan atanmış.</span><span class="sxs-lookup"><span data-stu-id="a2d8b-119">Select hello **Schema**, **Table** and **Column** toodefine hello designated field that will be masked.</span></span>
7. <span data-ttu-id="a2d8b-120">Seçin bir **maskeleme alan biçimini** hassas verileri maskeleme kategorileri hello listesinden.</span><span class="sxs-lookup"><span data-stu-id="a2d8b-120">Choose a **Masking Field Format** from hello list of sensitive data masking categories.</span></span>
   
    ![Gezinti Bölmesi](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. <span data-ttu-id="a2d8b-122">Tıklatın **kaydetmek** hello dinamik veri maskeleme İlkesi kurallarında maskeleme kuralı dikey tooupdate hello kümesi maskeleme hello veri.</span><span class="sxs-lookup"><span data-stu-id="a2d8b-122">Click **Save** in hello data masking rule blade tooupdate hello set of masking rules in hello dynamic data masking policy.</span></span>
9. <span data-ttu-id="a2d8b-123">Türü hello SQL kullanıcılar veya maskeleme işlemi bırakılmalıdır ve erişim maskelenmeyen toohello hassas verileri AAD kimlikleri.</span><span class="sxs-lookup"><span data-stu-id="a2d8b-123">Type hello SQL users or AAD identities that should be excluded from masking, and have access toohello unmasked sensitive data.</span></span> <span data-ttu-id="a2d8b-124">Bu kullanıcılar noktalı virgülle ayrılmış bir listesi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a2d8b-124">This should be a semicolon-separated list of users.</span></span> <span data-ttu-id="a2d8b-125">Yönetici ayrıcalıklarına sahip kullanıcılar her zaman erişim toohello özgün maskelenmemiş veri gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a2d8b-125">Note that users with administrator privileges always have access toohello original unmasked data.</span></span>
   
    ![Gezinti Bölmesi](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > <span data-ttu-id="a2d8b-127">Bu nedenle hello uygulama katmanı toomake uygulama ayrıcalıklı kullanıcılar için hassas verileri görüntüleyin, hello SQL kullanıcı eklemek veya AAD kimlik Merhaba uygulaması tooquery hello veritabanı kullanır.</span><span class="sxs-lookup"><span data-stu-id="a2d8b-127">toomake it so hello application layer can display sensitive data for application privileged users, add hello SQL user or AAD identity hello application uses tooquery hello database.</span></span> <span data-ttu-id="a2d8b-128">Bu liste ayrıcalıklı kullanıcıların toominimize Etkilenme hello gizli verilerin en az bir sayı içermesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="a2d8b-128">It is highly recommended that this list contain a minimal number of privileged users toominimize exposure of hello sensitive data.</span></span>
   > 
   > 
10. <span data-ttu-id="a2d8b-129">Tıklatın **kaydetmek** yapılandırma dikey toosave hello yeni veya güncelleştirilmiş maskeleme ilkenin maskeleme hello veri.</span><span class="sxs-lookup"><span data-stu-id="a2d8b-129">Click **Save** in hello data masking configuration blade toosave hello new or updated masking policy.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a2d8b-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a2d8b-130">Next steps</span></span>

* <span data-ttu-id="a2d8b-131">Dinamik veri maskeleme genel bakış için bkz: [dinamik veri maskeleme](sql-database-dynamic-data-masking-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a2d8b-131">For an overview of dynamic data masking, see [dynamic data masking](sql-database-dynamic-data-masking-get-started.md).</span></span>
* <span data-ttu-id="a2d8b-132">Dinamik veri maskeleme kullanarak uygulayabileceğiniz [Azure SQL veritabanı cmdlet'leri](https://msdn.microsoft.com/library/azure/mt574084.aspx) veya hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2d8b-132">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>
