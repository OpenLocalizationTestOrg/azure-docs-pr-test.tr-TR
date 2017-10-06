---
title: "aaaAdd ya da değişiklik Azure yönetici abonelik rolleri | Microsoft Docs"
description: "Açıklar nasıl tooadd Azure ortak yönetici, Hizmet Yöneticisi ve Hesap Yöneticisi veya değiştirme"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: 13a72d76-e043-4212-bcac-a35f4a27ee26
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: genli
ms.openlocfilehash: 14eaecf2dbfd7152775ac3552bf3a7ae3db596b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-change-azure-administrator-roles-that-manage-hello-subscription-or-services"></a>Ekleme veya değiştirme hello abonelik ya da hizmetleri yönetmek Azure yönetici rolleri
Değiştirebileceğiniz hello Azure aboneliğinize yönetir ve yöneten Azure yönetici hello aboneliğinizde kullanılan Azure Hizmetleri. tooview Azure faturalama bilgilerini ve Aboneliklerini yönetmek, toohello içinde oturum [hesap Merkezi'nde](https://account.windowsazure.com/Home/Index) Hesap Yöneticisi hello gibi. 

## <a name="add-an-admin-for-a-subscription"></a>Bir abonelik için bir yönetici ekleme
Hello Azure portal veya hello Klasik Azure portalı, Azure yönetici ekleyebilirsiniz.

**Azure portal**

tooadd birisi hello Azure portal'ın bir abonelik için yönetici olarak, bunları hello sahip rolünü size. Hello sahip rolünü yalnızca size atanan hello Abonelikteki hello kaynakları yönetebilir. Erişim ayrıcalık tooother abonelik yok. Merhaba hello eklediğiniz sahipleri [Azure portal](https://portal.azure.com) hello kaynağında yönetemez [Klasik Azure portalı](https://manage.windowsazure.com).

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba Hub menüsünde seçin **abonelik** > *hello hello yönetici tooaccess istediğiniz abonelik*.

    ![Seçili abonelik gösteren ekran görüntüsü](./media/billing-add-change-azure-subscription-administrator/newselectsub.png)

3. Merhaba abonelik dikey penceresinde, seçin **erişim denetimi (IAM)**.
4. Seçin **ekleme** > **rol** > **sahibi**. Select hello kullanıcı sahibi olarak tooadd istediğiniz ve ardından hello kullanıcı hello e-posta adresini yazın **kaydetmek**.

    ![Seçili hello sahip rolünü gösteren ekran görüntüsü](./media/billing-add-change-azure-subscription-administrator/add-role.png)

5. Merhaba, ortak yönetici olarak tooadd hello sahip hesabı istiyorsanız **erişim denetimi (IAM)** sayfasında hello kullanıcıyı sağ tıklatın ve ardından **ortak yönetici olarak Ekle**. Bu özellik artık kullanılabilir [Azure Önizleme portalı](https://preview.portal.azure.com/). 

     ![Ortak yönetici ekler ekran görüntüsü](./media/billing-add-change-azure-subscription-administrator/add-coadmin.png)

    >[!TIP]
    >Merhaba kullanıcının toomanage gerekirse tooadd hello "Sahip" kullanıcının ortak yönetici olarak gerekecek Azure hizmetlerinde hello [Klasik Azure portalı](https://manage.windowsazure.com/).

    tooremove hello ortak yönetici izni hello "ortak Yöneticisi" kullanıcı sağ tıklayın ve ardından **kaldırmak ortak yönetici**.

    ![Ortak yönetici kaldırır ekran görüntüsü](./media/billing-add-change-azure-subscription-administrator/remove-coadmin.png)


**Klasik Azure Portalı**

1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com/).
2. Merhaba Gezinti bölmesinde seçin **ayarları**> **Yöneticiler**> **Ekle**. </br>

    ![Nasıl tooget toohello Ekle düğmesini gösteren ekran görüntüsü](./media/billing-add-change-azure-subscription-administrator/addcoadmin.png)
3. Ortak yönetici ve ortak yönetici tooaccess hello istediğiniz seçip hello abonelik tooadd istediğiniz hello kişinin Hello e-posta adresini yazın.</br>

    ![Seçili abonelik gösteren ekran görüntüsü ](./media/billing-add-change-azure-subscription-administrator/addcoadmin2.png)</br>

e-posta adresi aşağıdaki hello bir ortak yönetici eklenebilir:

* **Microsoft Account** (eskiden Windows Live kimliği) </br>
  Bulut Outlook (Hotmail), Skype (MSN), OneDrive, Windows Phone ve Xbox LIVE gibi hizmetleri ve Microsoft Account toosign tooall tüketiciye yönelik Microsoft ürünlerinde kullanın.
* **Kurumsal hesap**</br>
  Bir kurumsal hesap Azure Active Directory altında oluşturulan hesaptır. Merhaba kuruluş hesabı adresi bu biçime sahiptir:

    Kullanıcı @&lt;etki alanınızın&gt;. onmicrosoft.com

## <a name="change-service-administrator-for-a-subscription"></a>Bir aboneliği için Hizmet Yöneticisi değiştirme
Yalnızca hello Hesap Yöneticisi, bir abonelik için Hizmet Yöneticisi hello değiştirebilirsiniz.

1. Çok oturum[Azure hesap Merkezi](https://account.windowsazure.com/subscriptions) hello Hesap Yöneticisi kullanarak.
2. Toochange hello aboneliği seçin.
3. Merhaba sağ tarafta seçin **Düzenle abonelik** ayrıntıları. </br>

    ![editsub](./media/billing-add-change-azure-subscription-administrator/editsub.png)
4. Merhaba, **Hizmet Yöneticisi** kutusuna, hello hello e-posta adresini girin yeni Hizmet Yöneticisi. </br>

    ![changeSA](./media/billing-add-change-azure-subscription-administrator/changeSA.png)

## <a name="change-hello-account-administrator"></a>Değişiklik hello Hesap Yöneticisi
hello Azure tooanother hesaba, tootransfer sahipliğini bkz [bir Azure aboneliği sahipliğini aktarma](billing-subscription-transfer.md).

Silmediğinizden veya hello Hesap yöneticisinin e-posta adresi yeniden adlandırmak, kesinlikle öneririz. Beklenmeyen ve istenmeyen davranışlar hello Azure hesabı ile görebilirsiniz. Düzgün mümkün tooAzure bu hesap ile oturum açma olması, toohello hesap değişiklik veya bu hesap ile kaynakları yönetme. 

## <a name="check-hello-account-administrator-of-hello-subscription"></a>Onay hello hello aboneliğin Hesap Yöneticisi
Aboneliğiniz için hello hesap yöneticisi olan emin değilseniz, aşağıdaki adımları toofind çıkışı hello kullanın.

  1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
  2. Merhaba Hub menüsünde seçin **abonelik**.
  3. Toocheck istediğiniz ve altında Ara hello aboneliği seçin **ayarları**.
  4. Seçin **özellikleri**. hello aboneliğin Hesap Yöneticisi Hello hello görüntülenen **Hesap Yöneticisi** kutusu.  

## <a name="types-of-azure-admin-accounts"></a>Azure Yönetici hesap türleri
 Hesap Yöneticisi, Hizmet Yöneticisi ve ortak yönetici hello üç Microsoft Azure yönetici rolleri türleridir. Merhaba aşağıdaki tabloda bu üç yönetici rolleri arasındaki hello fark açıklanmaktadır.

| Yönetim rolü | Sınır | Açıklama |
| --- | --- | --- |
| Hesap Yöneticisi (AA) |Azure hesabı başına 1 |Bu kaydolup veya Azure aboneliklerinin satın ve yetkili tooaccess hello hello kişidir [hesap Merkezi'nde](https://account.windowsazure.com/Home/Index) ve çeşitli yönetim görevlerini gerçekleştirebilirsiniz. Bu mümkün toocreate abonelikleri olan dahil, aboneliklerinizi iptal edin, bir abonelik için hello fatura değiştirmek ve hello Hizmet Yöneticisi değiştirin. |
| Hizmet Yöneticisi (SA) |Azure abonelik başına 1 |Merhaba yetkili toomanage Hizmetleri'nde bu rolüdür [Azure portal](https://portal.azure.com). Varsayılan olarak, yeni bir abonelik için hello Hesap Yöneticisi ayrıca hello Hizmet Yöneticisi ' dir. |
| Ortak yönetici (CA) hello [Klasik Azure portalı](https://manage.windowsazure.com) |Abonelik başına 200 |Bu rol hello sahip aynı erişim ayrıcalıkları hello Hizmet Yöneticisi, ancak abonelikleri tooAzure dizinleri hello ilişkisini değiştiremezsiniz. |

Azure Active Directory rol tabanlı erişim denetimi (RBAC) kullanıcıların sağlar toobe toomultiple rolleri eklendi. Daha fazla bilgi için bkz: [Azure Active Directory rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).

## <a name="limitations-and-restrictions-for-admin-accounts"></a>Sınırlamalar ve yönetici hesapları için kısıtlamalar
* Her abonelik, Azure AD dizini (olarak da bilinen varsayılan dizin hello) ile ilişkilidir. toofind hello varsayılan dizin hello abonelik gidin toohello ile ilişkili [Klasik Azure portalı](https://manage.windowsazure.com/)seçin **ayarları** > **abonelikleri**. Merhaba abonelik kimliği toofind hello varsayılan dizin denetleyin.
* Bir Microsoft Account oturum açtıysanız, ortak yönetici olarak diğer Microsoft Accounts veya kullanıcılar hello varsayılan dizin içinde yalnızca ekleyebilirsiniz.
* Bir kurumsal hesapla oturum açtıysanız, ortak yönetici olarak, kuruluşunuzdaki diğer Kurumsal hesaplar ekleyebilirsiniz. Örneğin, abby@contoso.com ekleyebilirsiniz bob@contoso.com Hizmet Yöneticisi veya ortak yönetici olarak ekleyemezsiniz, ancak john@notcontoso.com sürece john@notcontoso.com varsayılan dizindir. Kuruluş hesaplarıyla oturum imzalı kullanıcıları tooadd Microsoft Account kullanıcılar Hizmet Yöneticisi veya ortak yönetici olarak devam edebilir.
* Bir kurumsal hesap ile tooAzure içinde olası toosign olduğundan, hello değişiklikleri tooService yönetici ve ortak yönetici hesabı gereksinimleri şunlardır:

  | Yönteminde oturum | Microsoft Account veya kullanıcıların varsayılan dizin içindeki CA veya SA olarak eklensin mi? | Kurumsal hesap hello eklemek aynı kuruluş CA'yı veya SA olarak? | Farklı bir kuruluşta CA veya SA olarak kuruluş hesabı eklensin mi? |
  | --- | --- | --- | --- |
  |  Microsoft Hesabı |Evet |Hayır |Hayır |
  |  Kurumsal Hesap |Evet |Evet |Hayır |

## <a name="learn-more-about-resource-access-control-and-active-directory"></a>Kaynak erişim denetimi ve Active Directory hakkında daha fazla bilgi edinin
* Microsoft Azure'da kaynak erişiminin nasıl denetlendiğini hakkında daha fazla toolearn bkz [azure'da kaynak erişimini anlama](../active-directory/active-directory-understanding-resource-access.md).
* Azure Active Directory hakkında daha fazla bilgi için bkz: [Azure aboneliklerinin Azure Active Directory ile ilişkili](../active-directory/active-directory-how-subscriptions-associated-directory.md) ve [Azure Active Directory'de yönetici rolleri atama](../active-directory/active-directory-assign-admin-roles.md).

## <a name="need-help-contact-support"></a>Yardım mı gerekiyor? Desteğe başvurun.
Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) sorunu Çözümlendi hızla tooget.
