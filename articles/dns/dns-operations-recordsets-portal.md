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
# <a name="manage-dns-records-and-record-sets-by-using-hello-azure-portal"></a>Hello Azure portal kullanarak DNS kayıtlarını ve kayıt kümelerini yönetme

> [!div class="op_single_selector"]
> * [Azure Portal](dns-operations-recordsets-portal.md)
> * [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

Bu makalede Azure portal toomanage kayıt kümelerini ve kayıtları kullanarak DNS bölgenizi için nasıl hello gösterilmektedir.

Bu önemli toounderstand hello DNS kayıt kümelerini ve DNS kayıtları tek tek arasındaki farktır. Kayıt kümesi türü aynı ad ve aynı hello olan hello sahip bir bölgedeki kayıtları koleksiyonudur. Daha fazla bilgi için bkz: [oluşturma DNS kayıt kümelerini ve kayıtları kullanarak hello Azure portal](dns-getstarted-create-recordset-portal.md).

## <a name="create-a-new-record-set-and-record"></a>Yeni kayıt kümesi ve kayıt oluşturma

toocreate kayıt hello Azure portal kümesi bkz [kullanarak oluşturmak DNS kayıtlarını hello Azure portal](dns-getstarted-create-recordset-portal.md).

## <a name="view-a-record-set"></a>Bir kayıt kümesini görüntüleme

1. Toohello Hello Azure portal, Git **DNS bölgesi** dikey.
2. Merhaba kayıt kümesi için arama yapın ve seçin. Merhaba kayıt kümesi özelliklerini açar.

    ![Kayıt kümesi arayın](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-tooa-record-set"></a>Yeni bir kayıt tooa kayıt kümesi Ekle

Too20 kayıtları tooany kayıt ayarlama ekleyebilirsiniz. Kayıt kümesi iki özdeş kaydı içeremez. Boş kaydı kümeleri (sıfır kayıtlarla) oluşturulabilir ancak hello Azure DNS ad sunucuları üzerinde görünmez. CNAME türündeki kayıt kümesi en fazla bir kayıt içerebilir.

1. Hello üzerinde **kayıt kümesinin özelliklerini** DNS bölgenizi dikey penceresinde hello kaydı tıklatın tooadd bir kaydetmek istediğiniz ayarlayın.

    ![Kayıt kümesi seçin](./media/dns-operations-recordsets-portal/selectset500.png)

2. Merhaba alanları doldurarak Hello kaydı özellikler kümesi belirtin.

    ![Kayıt ekleme](./media/dns-operations-recordsets-portal/addrecord500.png)

3. Tıklatın **kaydetmek** adresindeki ayarlarınızı hello dikey toosave üstündeki hello. Ardından hello dikey penceresini kapatın.
4. Merhaba köşede hello kayıt kaydediyor görürsünüz.

    ![Kayıt kümesi kaydediliyor](./media/dns-operations-recordsets-portal/saving150.png)

Merhaba kayıt kaydedildikten sonra hello hello değerlerine **DNS bölgesi** dikey penceresinde hello yeni kayıt yansıtacak.

## <a name="update-a-record"></a>Bir kaydı güncelleştirme

Varolan bir kayıt kümesini kaydında güncelleştirdiğinizde, güncelleştirebilirsiniz hello alanlar çalıştığınız hello kayıt türüne bağlıdır.

1. Merhaba üzerinde **kayıt kümesinin özelliklerini** dikey penceresinde hello kaydı arayın, kayıt kümesinin.
2. Merhaba kaydı değiştirin. Bir kayıt değiştirdiğinizde, hello kayıt hello kullanılabilir ayarlarını değiştirebilirsiniz. Aşağıdaki örneğine hello hello **IP adresi** alanı seçilmişse ve hello IP adresidir değiştirilen hello işlemi içinde.

    ![Bir kayıt değiştirme](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. Tıklatın **kaydetmek** adresindeki ayarlarınızı hello dikey toosave üstündeki hello. Merhaba sağ üst köşedeki, hello kayıt kaydedilmiş hello bildirim görürsünüz.

    ![Kayıt kümesi kaydedildi](./media/dns-operations-recordsets-portal/saved150.png)

Merhaba kayıt kaydedildikten sonra hello üzerinde hello kayıt hello değerlerini ayarlayın **DNS bölgesi** dikey penceresinde hello güncelleştirilmiş kayıt yansıtacak.

## <a name="remove-a-record-from-a-record-set"></a>Bir kayıt kümesinden bir kaydı kaldırma

Kayıt kümesi hello Azure portal tooremove kayıtları kullanabilirsiniz. Bir kayıt kümesinden Hello son kaydı kaldırma hello kayıt kümesi silmez unutmayın.

1. Merhaba üzerinde **kayıt kümesinin özelliklerini** dikey penceresinde hello kaydı arayın, kayıt kümesinin.
2. Tooremove istediğiniz hello kayıt'a tıklayın. Ardından **kaldırmak**.

    ![Bir kaydı kaldırma](./media/dns-operations-recordsets-portal/removerecord500.png)

3. Tıklatın **kaydetmek** adresindeki ayarlarınızı hello dikey toosave üstündeki hello.
4. Merhaba kaydı kaldırıldıktan sonra hello hello hello kaydını değerlerini **DNS bölgesi** dikey penceresinde hello kaldırma yansıtacak.

## <a name="delete"></a>Bir kayıt kümesini Sil

1. Merhaba üzerinde **kayıt kümesinin özelliklerini** kayıt kümeniz için dikey tıklayın **silmek**.

    ![Bir kayıt kümesini Sil](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. Toodelete hello kayıt kümesi istemediğinizi soran bir ileti görüntülenir.
3. Merhaba ad eşleşmeleri hello kaydı toodelete istediğiniz ve ardından doğrulayın **Evet**.
4. Merhaba üzerinde **DNS bölgesi** dikey penceresinde hello kayıt kümesi artık görünür olduğunu doğrulayın.

## <a name="work-with-ns-and-soa-records"></a>NS ve SOA kayıtları ile çalışma

Otomatik olarak oluşturulan NS ve SOA kayıtları diğer kayıt türünden farklı şekilde yönetilir.

### <a name="modify-soa-records"></a>SOA kayıtları değiştirme

Ekleme veya SOA kaydına hello bölgenin tepesinde Ayarla otomatik olarak oluşturulan hello kayıtları kaldırın (name = "@"). Ancak, hello SOA kaydı (dışında "ana bilgisayar") içinde hello parametrelerinden herhangi birini değiştirmek ve TTL hello kayıt ayarlayın.

### <a name="modify-ns-records-at-hello-zone-apex"></a>Merhaba bölge tepesinde NS kayıtları değiştirme

Merhaba NS kayıt Hello bölgenin tepesinde kümesi her DNS bölge ile otomatik olarak oluşturulur. Hello Azure DNS ad sunucuları atanan toohello bölgesi hello adlarını içerir.

Ek ad sunucuları toothis NS kayıt kümesi, etki alanları birden fazla DNS sağlayıcınız ile birlikte barındırma toosupport ekleyebilirsiniz. Merhaba TTL ve bu kayıt kümesi için meta verileri de değiştirebilirsiniz. Ancak, kaldırmak veya hello önceden doldurulmuş haldedir Azure DNS ad sunucuları değiştirin.

Bu yalnızca toohello NS kayıt kümesi hello bölge tepesinde en geçerli olduğunu unutmayın. Diğer NS kayıt kümelerinde bölgenizi (olarak kullanılan toodelegate alt bölgeler) kısıtlama değiştirilebilir.

### <a name="delete-soa-or-ns-record-sets"></a>SOA veya NS kayıt kümelerini Sil

Merhaba SOA ve NS kayıt kümelerini hello bölge tepesinde adresindeki silemezsiniz (name = "@"), otomatik olarak oluşturulur hello bölge oluşturulduğunda. Merhaba bölge sildiğinizde, bunlar otomatik olarak silinir.

## <a name="next-steps"></a>Sonraki adımlar

* Azure DNS hakkında daha fazla bilgi için bkz: Merhaba [Azure DNS'ye genel bakış](dns-overview.md).
* DNS otomatikleştirme hakkında daha fazla bilgi için bkz: [oluşturma DNS bölgeleri ve kayıt kümelerini kullanarak hello .NET SDK'sı](dns-sdk.md).
* Geriye doğru DNS kayıtları hakkında daha fazla bilgi için bkz: [geriye doğru DNS ve Azure desteği'na genel bakış](dns-reverse-dns-overview.md).
