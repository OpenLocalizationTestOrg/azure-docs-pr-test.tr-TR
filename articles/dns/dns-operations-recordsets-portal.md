---
title: "DNS kayıt kümelerini ve Azure DNS kayıtlarını yönetme | Microsoft Docs"
description: "Azure DNS etki alanınızı barındırmaya olduğunda DNS kayıt kümelerini ve kayıtları yönetme yeteneği sağlar."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ed44a1-7bfe-454f-964e-922ad978264a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 001b80ccba43beab44f6a598f820df65a85a345f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-the-azure-portal"></a><span data-ttu-id="0205a-103">DNS kayıtlarını yönetme ve Azure portalını kullanarak kayıt kümeleri</span><span class="sxs-lookup"><span data-stu-id="0205a-103">Manage DNS records and record sets by using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0205a-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0205a-104">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="0205a-105">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0205a-105">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="0205a-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0205a-106">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="0205a-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0205a-107">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="0205a-108">Bu makalede Azure portalını kullanarak kayıt kümeleri ve kayıtlar için DNS bölgenizi yönetme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="0205a-108">This article shows you how to manage record sets and records for your DNS zone by using the Azure portal.</span></span>

<span data-ttu-id="0205a-109">DNS kayıt kümelerini ve DNS kayıtları tek tek arasındaki farkı anlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="0205a-109">It's important to understand the difference between DNS record sets and individual DNS records.</span></span> <span data-ttu-id="0205a-110">Kayıt kümesi, aynı ada sahip ve aynı türde olan bir bölgedeki kayıtları koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="0205a-110">A record set is a collection of records in a zone that have the same name and are the same type.</span></span> <span data-ttu-id="0205a-111">Daha fazla bilgi için bkz: [oluşturma DNS kayıt kümelerini ve kayıtları Azure portalını kullanarak](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0205a-111">For more information, see [Create DNS record sets and records by using the Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="create-a-new-record-set-and-record"></a><span data-ttu-id="0205a-112">Yeni kayıt kümesi ve kayıt oluşturma</span><span class="sxs-lookup"><span data-stu-id="0205a-112">Create a new record set and record</span></span>

<span data-ttu-id="0205a-113">Bir kayıt Azure portalında kümesi oluşturmak için bkz: [Azure portalını kullanarak oluşturmak DNS kayıtlarını](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0205a-113">To create a record set in the Azure portal, see [Create DNS records by using the Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="view-a-record-set"></a><span data-ttu-id="0205a-114">Bir kayıt kümesini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="0205a-114">View a record set</span></span>

1. <span data-ttu-id="0205a-115">Azure portalında Git **DNS bölgesi** dikey.</span><span class="sxs-lookup"><span data-stu-id="0205a-115">In the Azure portal, go to the **DNS zone** blade.</span></span>
2. <span data-ttu-id="0205a-116">Kayıt kümesi için arama yapın ve seçin.</span><span class="sxs-lookup"><span data-stu-id="0205a-116">Search for the record set and select it.</span></span> <span data-ttu-id="0205a-117">Bu kayıt kümesinin özelliklerini açar.</span><span class="sxs-lookup"><span data-stu-id="0205a-117">This opens the record set properties.</span></span>

    ![Kayıt kümesi arayın](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-to-a-record-set"></a><span data-ttu-id="0205a-119">Bir kayıt kümesine yeni bir kayıt ekleme</span><span class="sxs-lookup"><span data-stu-id="0205a-119">Add a new record to a record set</span></span>

<span data-ttu-id="0205a-120">Herhangi bir kayıt kümesi en fazla 20 kayıt ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0205a-120">You can add up to 20 records to any record set.</span></span> <span data-ttu-id="0205a-121">Kayıt kümesi iki özdeş kaydı içeremez.</span><span class="sxs-lookup"><span data-stu-id="0205a-121">A record set cannot contain two identical records.</span></span> <span data-ttu-id="0205a-122">Boş kaydı kümeleri (sıfır kayıtlarla) oluşturulabilir ancak Azure DNS ad sunucuları üzerinde görünmez.</span><span class="sxs-lookup"><span data-stu-id="0205a-122">Empty record sets (with zero records) can be created, but do not appear on the Azure DNS name servers.</span></span> <span data-ttu-id="0205a-123">CNAME türündeki kayıt kümesi en fazla bir kayıt içerebilir.</span><span class="sxs-lookup"><span data-stu-id="0205a-123">Record sets of type CNAME can contain one record at most.</span></span>

1. <span data-ttu-id="0205a-124">Üzerinde **kayıt kümesinin özelliklerini** DNS bölgenizi dikey penceresinde, bir kayıt eklemek istediğiniz kayıt kümesi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="0205a-124">On the **Record set properties** blade for your DNS zone, click the record set that you want to add a record to.</span></span>

    ![Kayıt kümesi seçin](./media/dns-operations-recordsets-portal/selectset500.png)

2. <span data-ttu-id="0205a-126">Alanları doldurarak kaydı özellikler kümesi belirtin.</span><span class="sxs-lookup"><span data-stu-id="0205a-126">Specify the record set properties by filling in the fields.</span></span>

    ![Kayıt ekleme](./media/dns-operations-recordsets-portal/addrecord500.png)

3. <span data-ttu-id="0205a-128">Tıklatın **kaydetmek** ayarlarınızı kaydetmek için dikey pencerenin üstündeki.</span><span class="sxs-lookup"><span data-stu-id="0205a-128">Click **Save** at the top of the blade to save your settings.</span></span> <span data-ttu-id="0205a-129">Ardından dikey penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="0205a-129">Then close the blade.</span></span>
4. <span data-ttu-id="0205a-130">Köşede kaydı kaydediyor görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="0205a-130">In the corner, you will see that the record is saving.</span></span>

    ![Kayıt kümesi kaydediliyor](./media/dns-operations-recordsets-portal/saving150.png)

<span data-ttu-id="0205a-132">Kayıt kaydedildi sonra değerleri **DNS bölgesi** dikey yeni kayıttaki yansıtacak.</span><span class="sxs-lookup"><span data-stu-id="0205a-132">After the record has been saved, the values on the **DNS zone** blade will reflect the new record.</span></span>

## <a name="update-a-record"></a><span data-ttu-id="0205a-133">Bir kaydı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="0205a-133">Update a record</span></span>

<span data-ttu-id="0205a-134">Varolan bir kayıt kümesini kaydında güncelleştirdiğinizde güncelleştirebilirsiniz alanları çalıştığınız kayıt türü bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="0205a-134">When you update a record in an existing record set, the fields you can update depend on the type of record you're working with.</span></span>

1. <span data-ttu-id="0205a-135">Üzerinde **kayıt kümesinin özelliklerini** dikey penceresinde, kayıt kümesi için arama kaydı için.</span><span class="sxs-lookup"><span data-stu-id="0205a-135">On the **Record set properties** blade for your record set, search for the record.</span></span>
2. <span data-ttu-id="0205a-136">Kayıt değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0205a-136">Modify the record.</span></span> <span data-ttu-id="0205a-137">Bir kayıt değiştirdiğinizde, kayıt için kullanılabilen ayarları değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0205a-137">When you modify a record, you can change the available settings for the record.</span></span> <span data-ttu-id="0205a-138">Aşağıdaki örnekte, **IP adresi** alanı seçilmişse ve değiştirilen sürecinde IP adresidir.</span><span class="sxs-lookup"><span data-stu-id="0205a-138">In the following example, the **IP address** field is selected, and the IP address is in the process of being modified.</span></span>

    ![Bir kayıt değiştirme](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. <span data-ttu-id="0205a-140">Tıklatın **kaydetmek** ayarlarınızı kaydetmek için dikey pencerenin üstündeki.</span><span class="sxs-lookup"><span data-stu-id="0205a-140">Click **Save** at the top of the blade to save your settings.</span></span> <span data-ttu-id="0205a-141">Sağ üst köşedeki kaydı kaydedilmiş bildirim görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="0205a-141">In the upper right corner, you'll see the notification that the record has been saved.</span></span>

    ![Kayıt kümesi kaydedildi](./media/dns-operations-recordsets-portal/saved150.png)

<span data-ttu-id="0205a-143">Kayıt kaydedildikten sonra kayıt için değerleri ayarlamak **DNS bölgesi** dikey penceresinde, güncelleştirilmiş kayıt yansıtacak.</span><span class="sxs-lookup"><span data-stu-id="0205a-143">After the record has been saved, the values for the record set on the **DNS zone** blade will reflect the updated record.</span></span>

## <a name="remove-a-record-from-a-record-set"></a><span data-ttu-id="0205a-144">Bir kayıt kümesinden bir kaydı kaldırma</span><span class="sxs-lookup"><span data-stu-id="0205a-144">Remove a record from a record set</span></span>

<span data-ttu-id="0205a-145">Azure portalı, kayıt kümesindeki kayıtları kaldırmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0205a-145">You can use the Azure portal to remove records from a record set.</span></span> <span data-ttu-id="0205a-146">Kayıt kümesindeki son kaydı kaldırma kayıt kümesi silmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0205a-146">Note that removing the last record from a record set does not delete the record set.</span></span>

1. <span data-ttu-id="0205a-147">Üzerinde **kayıt kümesinin özelliklerini** dikey penceresinde, kayıt kümesi için arama kaydı için.</span><span class="sxs-lookup"><span data-stu-id="0205a-147">On the **Record set properties** blade for your record set, search for the record.</span></span>
2. <span data-ttu-id="0205a-148">Kaldırmak istediğiniz kaydı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="0205a-148">Click the record that you want to remove.</span></span> <span data-ttu-id="0205a-149">Ardından **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="0205a-149">Then select **Remove**.</span></span>

    ![Bir kaydı kaldırma](./media/dns-operations-recordsets-portal/removerecord500.png)

3. <span data-ttu-id="0205a-151">Tıklatın **kaydetmek** ayarlarınızı kaydetmek için dikey pencerenin üstündeki.</span><span class="sxs-lookup"><span data-stu-id="0205a-151">Click **Save** at the top of the blade to save your settings.</span></span>
4. <span data-ttu-id="0205a-152">Kayıt kaldırıldıktan sonra kaydında değerlerini **DNS bölgesi** dikey kaldırma yansıtacak.</span><span class="sxs-lookup"><span data-stu-id="0205a-152">After the record has been removed, the values for the record on the **DNS zone** blade will reflect the removal.</span></span>

## <span data-ttu-id="0205a-153"><a name="delete"></a>Bir kayıt kümesini Sil</span><span class="sxs-lookup"><span data-stu-id="0205a-153"><a name="delete"></a>Delete a record set</span></span>

1. <span data-ttu-id="0205a-154">Üzerinde **kayıt kümesinin özelliklerini** kayıt kümeniz için dikey tıklayın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="0205a-154">On the **Record set properties** blade for your record set, click **Delete**.</span></span>

    ![Bir kayıt kümesini Sil](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. <span data-ttu-id="0205a-156">Kayıt kümesi silmek istiyorsanız soran bir ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="0205a-156">A message appears asking if you want to delete the record set.</span></span>
3. <span data-ttu-id="0205a-157">Ad, silme ve ardından istediğiniz kayıt kümesi ile eşleştiğini doğrulayın **Evet**.</span><span class="sxs-lookup"><span data-stu-id="0205a-157">Verify that the name matches the record set that you want to delete, and then click **Yes**.</span></span>
4. <span data-ttu-id="0205a-158">Üzerinde **DNS bölgesi** dikey penceresinde, kayıt kümesi artık görünür olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="0205a-158">On the **DNS zone** blade, verify that the record set is no longer visible.</span></span>

## <a name="work-with-ns-and-soa-records"></a><span data-ttu-id="0205a-159">NS ve SOA kayıtları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="0205a-159">Work with NS and SOA records</span></span>

<span data-ttu-id="0205a-160">Otomatik olarak oluşturulan NS ve SOA kayıtları diğer kayıt türünden farklı şekilde yönetilir.</span><span class="sxs-lookup"><span data-stu-id="0205a-160">NS and SOA records that are automatically created are managed differently from other record types.</span></span>

### <a name="modify-soa-records"></a><span data-ttu-id="0205a-161">SOA kayıtları değiştirme</span><span class="sxs-lookup"><span data-stu-id="0205a-161">Modify SOA records</span></span>

<span data-ttu-id="0205a-162">Ekleme veya kayıtları otomatik olarak oluşturulan SOA kayıt bölgenin tepesinde kümesi kaldırın (name = "@").</span><span class="sxs-lookup"><span data-stu-id="0205a-162">You cannot add or remove records from the automatically created SOA record set at the zone apex (name = "@").</span></span> <span data-ttu-id="0205a-163">Ancak, SOA kaydı (dışında "ana bilgisayar") içinde parametrelerinden herhangi birini değiştirmek ve TTL kaydı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0205a-163">However, you can modify any of the parameters within the SOA record (except "Host") and the record set TTL.</span></span>

### <a name="modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="0205a-164">Bölge tepesinde NS kayıtları değiştirme</span><span class="sxs-lookup"><span data-stu-id="0205a-164">Modify NS records at the zone apex</span></span>

<span data-ttu-id="0205a-165">NS kayıt bölgenin tepesinde kümesi her DNS bölge ile otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0205a-165">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="0205a-166">Bölgeye atanan Azure DNS ad sunucularının adlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="0205a-166">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="0205a-167">Birden fazla DNS sağlayıcınız ile birlikte barındırma etki alanlarını destekleyecek şekilde bu NS kaydının sunucularına ayarlayın ek ad ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0205a-167">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="0205a-168">Bu kayıt kümesi için meta verileri ve TTL de değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0205a-168">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="0205a-169">Ancak, kaldırmak veya önceden doldurulmuş haldedir Azure DNS ad sunucuları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0205a-169">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="0205a-170">Bu bölge tepesinde yalnızca NS kayıt kümesi için geçerli olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0205a-170">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="0205a-171">(Alt bölgelere temsilci seçmek için kullanıldığı şekilde), bu bölgedeki diğer NS kayıt kümelerini kısıtlama değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="0205a-171">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

### <a name="delete-soa-or-ns-record-sets"></a><span data-ttu-id="0205a-172">SOA veya NS kayıt kümelerini Sil</span><span class="sxs-lookup"><span data-stu-id="0205a-172">Delete SOA or NS record sets</span></span>

<span data-ttu-id="0205a-173">SOA silemezsiniz ve NS kayıt kümeleri bölgenin tepesinde (ad = "@"), otomatik olarak oluşturulur bölge oluşturulduğunda.</span><span class="sxs-lookup"><span data-stu-id="0205a-173">You cannot delete the SOA and NS record sets at the zone apex (name = "@") that are created automatically when the zone is created.</span></span> <span data-ttu-id="0205a-174">Bölge sildiğinizde, bunlar otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="0205a-174">They are deleted automatically when you delete the zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0205a-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0205a-175">Next steps</span></span>

* <span data-ttu-id="0205a-176">Azure DNS hakkında daha fazla bilgi için bkz: [Azure DNS'ye genel bakış](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0205a-176">For more information about Azure DNS, see the [Azure DNS overview](dns-overview.md).</span></span>
* <span data-ttu-id="0205a-177">DNS otomatikleştirme hakkında daha fazla bilgi için bkz: [oluşturma DNS bölgeleri ve .NET SDK kullanarak kayıt kümelerine](dns-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="0205a-177">For more information about automating DNS, see [Creating DNS zones and record sets using the .NET SDK](dns-sdk.md).</span></span>
* <span data-ttu-id="0205a-178">Geriye doğru DNS kayıtları hakkında daha fazla bilgi için bkz: [geriye doğru DNS ve Azure desteği'na genel bakış](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0205a-178">For more information about reverse DNS records, see [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>
