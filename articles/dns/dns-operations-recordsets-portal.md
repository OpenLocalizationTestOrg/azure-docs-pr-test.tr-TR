---
title: "aaaManage DNS kayıt kümelerini ve Azure DNS kayıtları | Microsoft Docs"
description: "Azure DNS hello yetenek toomanage DNS kaydı ayarlar ve etki alanınızı barındırmaya zaman kayıtlarını sağlar."
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
ms.openlocfilehash: 2e62d017341589eaf8d1f8df2fe5db4b973381d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-hello-azure-portal"></a><span data-ttu-id="49359-103">Hello Azure portal kullanarak DNS kayıtlarını ve kayıt kümelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="49359-103">Manage DNS records and record sets by using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="49359-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="49359-104">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="49359-105">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="49359-105">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="49359-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="49359-106">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="49359-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="49359-107">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="49359-108">Bu makalede Azure portal toomanage kayıt kümelerini ve kayıtları kullanarak DNS bölgenizi için nasıl hello gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="49359-108">This article shows you how toomanage record sets and records for your DNS zone by using hello Azure portal.</span></span>

<span data-ttu-id="49359-109">Bu önemli toounderstand hello DNS kayıt kümelerini ve DNS kayıtları tek tek arasındaki farktır.</span><span class="sxs-lookup"><span data-stu-id="49359-109">It's important toounderstand hello difference between DNS record sets and individual DNS records.</span></span> <span data-ttu-id="49359-110">Kayıt kümesi türü aynı ad ve aynı hello olan hello sahip bir bölgedeki kayıtları koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="49359-110">A record set is a collection of records in a zone that have hello same name and are hello same type.</span></span> <span data-ttu-id="49359-111">Daha fazla bilgi için bkz: [oluşturma DNS kayıt kümelerini ve kayıtları kullanarak hello Azure portal](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="49359-111">For more information, see [Create DNS record sets and records by using hello Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="create-a-new-record-set-and-record"></a><span data-ttu-id="49359-112">Yeni kayıt kümesi ve kayıt oluşturma</span><span class="sxs-lookup"><span data-stu-id="49359-112">Create a new record set and record</span></span>

<span data-ttu-id="49359-113">toocreate kayıt hello Azure portal kümesi bkz [kullanarak oluşturmak DNS kayıtlarını hello Azure portal](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="49359-113">toocreate a record set in hello Azure portal, see [Create DNS records by using hello Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="view-a-record-set"></a><span data-ttu-id="49359-114">Bir kayıt kümesini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="49359-114">View a record set</span></span>

1. <span data-ttu-id="49359-115">Toohello Hello Azure portal, Git **DNS bölgesi** dikey.</span><span class="sxs-lookup"><span data-stu-id="49359-115">In hello Azure portal, go toohello **DNS zone** blade.</span></span>
2. <span data-ttu-id="49359-116">Merhaba kayıt kümesi için arama yapın ve seçin.</span><span class="sxs-lookup"><span data-stu-id="49359-116">Search for hello record set and select it.</span></span> <span data-ttu-id="49359-117">Merhaba kayıt kümesi özelliklerini açar.</span><span class="sxs-lookup"><span data-stu-id="49359-117">This opens hello record set properties.</span></span>

    ![Kayıt kümesi arayın](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-tooa-record-set"></a><span data-ttu-id="49359-119">Yeni bir kayıt tooa kayıt kümesi Ekle</span><span class="sxs-lookup"><span data-stu-id="49359-119">Add a new record tooa record set</span></span>

<span data-ttu-id="49359-120">Too20 kayıtları tooany kayıt ayarlama ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49359-120">You can add up too20 records tooany record set.</span></span> <span data-ttu-id="49359-121">Kayıt kümesi iki özdeş kaydı içeremez.</span><span class="sxs-lookup"><span data-stu-id="49359-121">A record set cannot contain two identical records.</span></span> <span data-ttu-id="49359-122">Boş kaydı kümeleri (sıfır kayıtlarla) oluşturulabilir ancak hello Azure DNS ad sunucuları üzerinde görünmez.</span><span class="sxs-lookup"><span data-stu-id="49359-122">Empty record sets (with zero records) can be created, but do not appear on hello Azure DNS name servers.</span></span> <span data-ttu-id="49359-123">CNAME türündeki kayıt kümesi en fazla bir kayıt içerebilir.</span><span class="sxs-lookup"><span data-stu-id="49359-123">Record sets of type CNAME can contain one record at most.</span></span>

1. <span data-ttu-id="49359-124">Hello üzerinde **kayıt kümesinin özelliklerini** DNS bölgenizi dikey penceresinde hello kaydı tıklatın tooadd bir kaydetmek istediğiniz ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="49359-124">On hello **Record set properties** blade for your DNS zone, click hello record set that you want tooadd a record to.</span></span>

    ![Kayıt kümesi seçin](./media/dns-operations-recordsets-portal/selectset500.png)

2. <span data-ttu-id="49359-126">Merhaba alanları doldurarak Hello kaydı özellikler kümesi belirtin.</span><span class="sxs-lookup"><span data-stu-id="49359-126">Specify hello record set properties by filling in hello fields.</span></span>

    ![Kayıt ekleme](./media/dns-operations-recordsets-portal/addrecord500.png)

3. <span data-ttu-id="49359-128">Tıklatın **kaydetmek** adresindeki ayarlarınızı hello dikey toosave üstündeki hello.</span><span class="sxs-lookup"><span data-stu-id="49359-128">Click **Save** at hello top of hello blade toosave your settings.</span></span> <span data-ttu-id="49359-129">Ardından hello dikey penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="49359-129">Then close hello blade.</span></span>
4. <span data-ttu-id="49359-130">Merhaba köşede hello kayıt kaydediyor görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="49359-130">In hello corner, you will see that hello record is saving.</span></span>

    ![Kayıt kümesi kaydediliyor](./media/dns-operations-recordsets-portal/saving150.png)

<span data-ttu-id="49359-132">Merhaba kayıt kaydedildikten sonra hello hello değerlerine **DNS bölgesi** dikey penceresinde hello yeni kayıt yansıtacak.</span><span class="sxs-lookup"><span data-stu-id="49359-132">After hello record has been saved, hello values on hello **DNS zone** blade will reflect hello new record.</span></span>

## <a name="update-a-record"></a><span data-ttu-id="49359-133">Bir kaydı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="49359-133">Update a record</span></span>

<span data-ttu-id="49359-134">Varolan bir kayıt kümesini kaydında güncelleştirdiğinizde, güncelleştirebilirsiniz hello alanlar çalıştığınız hello kayıt türüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="49359-134">When you update a record in an existing record set, hello fields you can update depend on hello type of record you're working with.</span></span>

1. <span data-ttu-id="49359-135">Merhaba üzerinde **kayıt kümesinin özelliklerini** dikey penceresinde hello kaydı arayın, kayıt kümesinin.</span><span class="sxs-lookup"><span data-stu-id="49359-135">On hello **Record set properties** blade for your record set, search for hello record.</span></span>
2. <span data-ttu-id="49359-136">Merhaba kaydı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="49359-136">Modify hello record.</span></span> <span data-ttu-id="49359-137">Bir kayıt değiştirdiğinizde, hello kayıt hello kullanılabilir ayarlarını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49359-137">When you modify a record, you can change hello available settings for hello record.</span></span> <span data-ttu-id="49359-138">Aşağıdaki örneğine hello hello **IP adresi** alanı seçilmişse ve hello IP adresidir değiştirilen hello işlemi içinde.</span><span class="sxs-lookup"><span data-stu-id="49359-138">In hello following example, hello **IP address** field is selected, and hello IP address is in hello process of being modified.</span></span>

    ![Bir kayıt değiştirme](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. <span data-ttu-id="49359-140">Tıklatın **kaydetmek** adresindeki ayarlarınızı hello dikey toosave üstündeki hello.</span><span class="sxs-lookup"><span data-stu-id="49359-140">Click **Save** at hello top of hello blade toosave your settings.</span></span> <span data-ttu-id="49359-141">Merhaba sağ üst köşedeki, hello kayıt kaydedilmiş hello bildirim görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="49359-141">In hello upper right corner, you'll see hello notification that hello record has been saved.</span></span>

    ![Kayıt kümesi kaydedildi](./media/dns-operations-recordsets-portal/saved150.png)

<span data-ttu-id="49359-143">Merhaba kayıt kaydedildikten sonra hello üzerinde hello kayıt hello değerlerini ayarlayın **DNS bölgesi** dikey penceresinde hello güncelleştirilmiş kayıt yansıtacak.</span><span class="sxs-lookup"><span data-stu-id="49359-143">After hello record has been saved, hello values for hello record set on hello **DNS zone** blade will reflect hello updated record.</span></span>

## <a name="remove-a-record-from-a-record-set"></a><span data-ttu-id="49359-144">Bir kayıt kümesinden bir kaydı kaldırma</span><span class="sxs-lookup"><span data-stu-id="49359-144">Remove a record from a record set</span></span>

<span data-ttu-id="49359-145">Kayıt kümesi hello Azure portal tooremove kayıtları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49359-145">You can use hello Azure portal tooremove records from a record set.</span></span> <span data-ttu-id="49359-146">Bir kayıt kümesinden Hello son kaydı kaldırma hello kayıt kümesi silmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="49359-146">Note that removing hello last record from a record set does not delete hello record set.</span></span>

1. <span data-ttu-id="49359-147">Merhaba üzerinde **kayıt kümesinin özelliklerini** dikey penceresinde hello kaydı arayın, kayıt kümesinin.</span><span class="sxs-lookup"><span data-stu-id="49359-147">On hello **Record set properties** blade for your record set, search for hello record.</span></span>
2. <span data-ttu-id="49359-148">Tooremove istediğiniz hello kayıt'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="49359-148">Click hello record that you want tooremove.</span></span> <span data-ttu-id="49359-149">Ardından **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="49359-149">Then select **Remove**.</span></span>

    ![Bir kaydı kaldırma](./media/dns-operations-recordsets-portal/removerecord500.png)

3. <span data-ttu-id="49359-151">Tıklatın **kaydetmek** adresindeki ayarlarınızı hello dikey toosave üstündeki hello.</span><span class="sxs-lookup"><span data-stu-id="49359-151">Click **Save** at hello top of hello blade toosave your settings.</span></span>
4. <span data-ttu-id="49359-152">Merhaba kaydı kaldırıldıktan sonra hello hello hello kaydını değerlerini **DNS bölgesi** dikey penceresinde hello kaldırma yansıtacak.</span><span class="sxs-lookup"><span data-stu-id="49359-152">After hello record has been removed, hello values for hello record on hello **DNS zone** blade will reflect hello removal.</span></span>

## <span data-ttu-id="49359-153"><a name="delete"></a>Bir kayıt kümesini Sil</span><span class="sxs-lookup"><span data-stu-id="49359-153"><a name="delete"></a>Delete a record set</span></span>

1. <span data-ttu-id="49359-154">Merhaba üzerinde **kayıt kümesinin özelliklerini** kayıt kümeniz için dikey tıklayın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="49359-154">On hello **Record set properties** blade for your record set, click **Delete**.</span></span>

    ![Bir kayıt kümesini Sil](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. <span data-ttu-id="49359-156">Toodelete hello kayıt kümesi istemediğinizi soran bir ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="49359-156">A message appears asking if you want toodelete hello record set.</span></span>
3. <span data-ttu-id="49359-157">Merhaba ad eşleşmeleri hello kaydı toodelete istediğiniz ve ardından doğrulayın **Evet**.</span><span class="sxs-lookup"><span data-stu-id="49359-157">Verify that hello name matches hello record set that you want toodelete, and then click **Yes**.</span></span>
4. <span data-ttu-id="49359-158">Merhaba üzerinde **DNS bölgesi** dikey penceresinde hello kayıt kümesi artık görünür olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="49359-158">On hello **DNS zone** blade, verify that hello record set is no longer visible.</span></span>

## <a name="work-with-ns-and-soa-records"></a><span data-ttu-id="49359-159">NS ve SOA kayıtları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="49359-159">Work with NS and SOA records</span></span>

<span data-ttu-id="49359-160">Otomatik olarak oluşturulan NS ve SOA kayıtları diğer kayıt türünden farklı şekilde yönetilir.</span><span class="sxs-lookup"><span data-stu-id="49359-160">NS and SOA records that are automatically created are managed differently from other record types.</span></span>

### <a name="modify-soa-records"></a><span data-ttu-id="49359-161">SOA kayıtları değiştirme</span><span class="sxs-lookup"><span data-stu-id="49359-161">Modify SOA records</span></span>

<span data-ttu-id="49359-162">Ekleme veya SOA kaydına hello bölgenin tepesinde Ayarla otomatik olarak oluşturulan hello kayıtları kaldırın (name = "@").</span><span class="sxs-lookup"><span data-stu-id="49359-162">You cannot add or remove records from hello automatically created SOA record set at hello zone apex (name = "@").</span></span> <span data-ttu-id="49359-163">Ancak, hello SOA kaydı (dışında "ana bilgisayar") içinde hello parametrelerinden herhangi birini değiştirmek ve TTL hello kayıt ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="49359-163">However, you can modify any of hello parameters within hello SOA record (except "Host") and hello record set TTL.</span></span>

### <a name="modify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="49359-164">Merhaba bölge tepesinde NS kayıtları değiştirme</span><span class="sxs-lookup"><span data-stu-id="49359-164">Modify NS records at hello zone apex</span></span>

<span data-ttu-id="49359-165">Merhaba NS kayıt Hello bölgenin tepesinde kümesi her DNS bölge ile otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="49359-165">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="49359-166">Hello Azure DNS ad sunucuları atanan toohello bölgesi hello adlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="49359-166">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="49359-167">Ek ad sunucuları toothis NS kayıt kümesi, etki alanları birden fazla DNS sağlayıcınız ile birlikte barındırma toosupport ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49359-167">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="49359-168">Merhaba TTL ve bu kayıt kümesi için meta verileri de değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49359-168">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="49359-169">Ancak, kaldırmak veya hello önceden doldurulmuş haldedir Azure DNS ad sunucuları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="49359-169">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="49359-170">Bu yalnızca toohello NS kayıt kümesi hello bölge tepesinde en geçerli olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="49359-170">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="49359-171">Diğer NS kayıt kümelerinde bölgenizi (olarak kullanılan toodelegate alt bölgeler) kısıtlama değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="49359-171">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

### <a name="delete-soa-or-ns-record-sets"></a><span data-ttu-id="49359-172">SOA veya NS kayıt kümelerini Sil</span><span class="sxs-lookup"><span data-stu-id="49359-172">Delete SOA or NS record sets</span></span>

<span data-ttu-id="49359-173">Merhaba SOA ve NS kayıt kümelerini hello bölge tepesinde adresindeki silemezsiniz (name = "@"), otomatik olarak oluşturulur hello bölge oluşturulduğunda.</span><span class="sxs-lookup"><span data-stu-id="49359-173">You cannot delete hello SOA and NS record sets at hello zone apex (name = "@") that are created automatically when hello zone is created.</span></span> <span data-ttu-id="49359-174">Merhaba bölge sildiğinizde, bunlar otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="49359-174">They are deleted automatically when you delete hello zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49359-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="49359-175">Next steps</span></span>

* <span data-ttu-id="49359-176">Azure DNS hakkında daha fazla bilgi için bkz: Merhaba [Azure DNS'ye genel bakış](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="49359-176">For more information about Azure DNS, see hello [Azure DNS overview](dns-overview.md).</span></span>
* <span data-ttu-id="49359-177">DNS otomatikleştirme hakkında daha fazla bilgi için bkz: [oluşturma DNS bölgeleri ve kayıt kümelerini kullanarak hello .NET SDK'sı](dns-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="49359-177">For more information about automating DNS, see [Creating DNS zones and record sets using hello .NET SDK](dns-sdk.md).</span></span>
* <span data-ttu-id="49359-178">Geriye doğru DNS kayıtları hakkında daha fazla bilgi için bkz: [geriye doğru DNS ve Azure desteği'na genel bakış](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="49359-178">For more information about reverse DNS records, see [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>
