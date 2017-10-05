---
title: "Başka bir hesap için Azure aboneliği sahipliğini aktarma | Microsoft Docs"
description: "Başka bir kullanıcı ve süreci hakkında bazı sık sorulan sorular (SSS) için bir Azure aboneliği aktarım açıklar"
keywords: "Azure abonelik, azure aktarımı abonelik aktarımı, başka bir hesap, azure yeni abonelik sahibi azure aboneliği taşımak, azure aboneliği başka bir hesaba aktarın"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing,top-support-issue
ms.assetid: c8ecdc1e-c9c5-468c-a024-94ae41e64702
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8a856c39eb11546f35cb4e8c21e6bdcce98857a8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="transfer-ownership-of-an-azure-subscription-to-another-account"></a>Başka bir hesap için bir Azure aboneliği sahipliğini aktarma

Kullandıkça Öde, Visual Studio, eylem paketi ya da hesap Merkezi'nde BizSpark abonelik için aboneliğinizi başka bir kullanıcıya aktarabilir. Bu abonelik türleri için de Azure dış hizmetler aktarımını destekliyoruz. 

Varsa bir Azure aboneliği sahipliğini aktarma isteyebilirsiniz:

* Azure aboneliğinize başkası sahipliğini faturalama üzerinden elle gerekir.
* Azure için kaydolmak için kullandığınız hesap değiştirmek istiyorum. Belki de Microsoft Account kullanılan ancak çalışmanızı kullanma veya Okul hesabı yerine anlamına gelir.
* Azure aboneliğinizde bir dizinden taşımak istersiniz.
* Azure ve Office 365 farklı kiracılar varsa ve birleştirmek istiyorsanız.

Aboneliğinizi farklı bir teklif değiştirmek için bkz: [Azure aboneliğinizi başka bir teklife geç](billing-how-to-switch-azure-offer.md). 

## <a name="transfer-ownership-of-an-azure-subscription"></a>Bir Azure aboneliği sahipliğini aktarma
> [!VIDEO https://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/Transfer-an-Azure-subscription/player]
>
>

1. Adresinde oturum açın <https://account.windowsazure.com/Subscriptions>. Sahiplik aktarımı gerçekleştirmek için hesap yöneticisi olmanız gerekir. Aboneliğin hesap yöneticisi kim olduğunu bulmak için bkz: [sık sorulan sorular](#faq).

2. Aktarılacak abonelik seçin.

3. Tıklatın **abonelik aktarımı** seçeneği. Bkz: [SSS](#no-button) düğmeyi görmüyorsanız.

   ![Azure hesabı abonelikleri sekmesi](./media/billing-subscription-transfer/image1.png)
4. Alıcıyı belirtin.

   ![Aktarım abonelik iletişim kutusu](./media/billing-subscription-transfer/image2.PNG)
5. Alıcı otomatik olarak, kabul bağlantısı içeren bir e-posta alır.

   ![Abonelik aktarımı alıcı'e-posta](./media/billing-subscription-transfer/image3.png)
6. Alıcı bağlantıya tıklar ve yönergeleri izler; bu arada ödeme bilgilerini de girer.

   ![İlk abonelik aktarımı web sayfası](./media/billing-subscription-transfer/image4.png)

   ![İkinci abonelik aktarımı web sayfası](./media/billing-subscription-transfer/image5.png)
7. Başarılı! Abonelik artık aktarılır.

## <a name="transfer-subscription-ownership-for-enterprise-agreement-ea-customers"></a>Kurumsal Anlaşma (Kurumsal Sözleşme) müşteriler için abonelik sahipliğini aktarma
Kuruluş Yöneticisi bir kayıt içinde abonelikleri sahipliğini aktarabilirsiniz. Başlamak için bkz: [hesap sahipliğini aktarma](https://ea.azure.com/helpdocs/changeAccountOwnerForASubscription) EA Portalı'nda.

## <a name="next-steps-after-accepting-ownership-of-a-subscription"></a>Bir aboneliğin sahipliğini kabul sonraki adımlar
1. Hesap Yöneticisi sunulmuştur. Gözden geçirin ve hizmet yöneticisini ve ortak Yöneticiler güncelleştirin. Admins yönetmek [Klasik Azure portalı](https://manage.windowsazure.com) ayarlarına giderek. [Yönetici rolleri hakkında daha fazla bilgi](billing-add-change-azure-subscription-administrator.md).

2. Rol tabanlı erişim denetimi (RBAC), aboneliğiniz ve hizmetleriniz için de kullanabilirsiniz. [Azure portalını](https://portal.azure.com) ziyaret edin. [RBAC hakkında daha fazla bilgi edinin](../active-directory/role-based-access-control-configure.md)

3. Dahil olmak üzere bu aboneliğin hizmetleriyle ilişkili kimlik bilgilerini güncelleştirin:
   
   * Kullanıcının yönetici hakları abonelik kaynaklarına yönetim sertifikaları. Daha fazla bilgi için bkz: [oluşturun ve bir yönetim sertifikası için Azure yükleyin](../cloud-services/cloud-services-certs-create.md)
   
   * Depolama Hizmetleri için erişim anahtarlarını ister. Daha fazla bilgi için bkz: [Azure storage hesapları hakkında](../storage/common/storage-create-storage-account.md)
   
   * Azure sanal makineleri Hizmetleri için uzaktan erişim kimlik bilgilerini ister. 

4. [Bu abonelik için faturalama uyarılarını güncelleştirin](billing-set-up-alerts.md) adresindeki [Azure hesap Merkezi](https://account.windowsazure.com/Subscriptions). 

5. Bir iş ortağı ile çalışıyorsanız, iş ortağı Kimliğini bu abonelikte güncelleştirmeyi deneyin. İş ortağı Kimliğini güncelleştirebilirsiniz [Azure hesap Merkezi](https://account.windowsazure.com/Subscriptions).

<a id="faq"></a>

## <a name="frequently-asked-questions-faq"></a>Sık sorulan sorular (SSS)
* <a name="whoisaa"></a>**Aboneliğin Hesap Yöneticisi kimdir?**

  Hesap Yöneticisi kaydolup veya Azure aboneliği satın kullanıcıdır. Bunlar erişim yetkiniz [hesap Merkezi'nde](https://account.windowsazure.com/Home/Index) ve abonelikleri oluşturma, aboneliklerinizi iptal edin, bir abonelik için faturalama değiştirmek veya Hizmet Yöneticisi değiştirme gibi çeşitli yönetim görevlerini gerçekleştirebilirsiniz. Bir abonelik için hesap yöneticinize olan emin değilseniz, öğrenmek için aşağıdaki adımları kullanın.

  1. [Azure Portal](https://portal.azure.com) oturum açın.
  2. Hub menüsünde seçin **abonelik**.
  3. Denetleyin ve altında aramak istediğiniz aboneliği seçin **ayarları**.
  4. Seçin **özellikleri**. Aboneliğin Hesap Yöneticisi görüntülenen **Hesap Yöneticisi** kutusu.  

* **Her şeyi aktarım mu? Kaynak grupları, VM'ler, diskleri ve diğer çalışan hizmetleri de dahil olmak üzere?**

  Evet, tüm kaynaklarınızı VM'ler, diskler ve Web siteleri aktarımı için yeni sahibin ister. Ancak, tüm [yönetici rolleri](billing-add-change-azure-subscription-administrator.md) ve [rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-configure.md) ayarladığınız ilkeleri farklı dizinlerde aktarım değil.

* <a id="no-button"></a>**Yok görmemin nedeni abonelik aktarımı düğmesi?**

  Görmüyorsanız, **aktarımı abonelik** düğmesi, sonra da teklifiniz için abonelik aktarımı desteklemiyoruz. [Desteğe başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

* **Abonelik aktarımı herhangi bir hizmet kesintisi yol mu?**

  Hizmet üzerinde etkisi yoktur. Aboneliğin aktarılması abonelik geçerli hesap yöneticisi altında iptal eder ve alıcının hesabı altında bir abonelik oluşturur. Yeni Abonelik için temel Azure Hizmetleri ilişkilidir. Abonelik kimliği aynı kalır.

* **Abonelik için dizini değiştirmek için bu işlemi nasıl kullanırım?**

  Bir Azure aboneliğiniz Hesap Yöneticisi ait dizinde oluşturulur. Dizini değiştirmek için hedef dizininde bir kullanıcı hesabı için abonelik aktarın. Bu kullanıcının aktarımı kabul etmek için adımları tamamlandığında, abonelik otomatik olarak hedef dizinine taşınır.

* **Fatura sahipliğini başka bir kuruluştan bir abonelik üzerinden izlerseniz Kaynaklarım erişiminiz devam eder?**

  Abonelik için başka bir kiracı aktardıysanız, önceki Kiracı ile ilişkilendirilen kullanıcılar abonelik erişimi kaybedersiniz. Bir kullanıcı bir Hizmet Yöneticisi veya ortak yönetici artık olsa bile, yine de dahil olmak üzere, başka bir güvenlik mekanizması abonelikle erişimleri:

  * Kullanıcının yönetici hakları abonelik kaynaklarına yönetim sertifikaları. Daha fazla bilgi için bkz: [oluşturun ve Azure için yönetim sertifikası karşıya](../cloud-services/cloud-services-certs-create.md).
  * Depolama Hizmetleri için erişim anahtarlarını ister. Daha fazla bilgi için bkz: [Azure storage hesapları hakkında](../storage/common/storage-create-storage-account.md).
  * Azure sanal makineleri Hizmetleri için uzaktan erişim kimlik bilgilerini ister.

 Alıcı kullanıcıların kaynaklara erişimini kısıtlamak gerekirse, hizmetle ilişkilendirilmiş gizli güncelleştirmeyi düşünmelisiniz. En fazla kaynak, aşağıdaki adımları kullanarak güncelleştirilebilir:

    1. [Azure Portal](https://portal.azure.com) gidin.
    2. Hub menüsünde seçin **tüm kaynakları**.
    3. Kaynak seçin. 
    4. Kaynak dikey penceresinde tıklayın **ayarları**. Burada görebilirsiniz ve var olan gizli güncelleştirin.

* **Abonelik faturalama döngüsü ortasında aktarırsanız, alıcı ödeme tüm faturalama döngüsü mu?**

  Gönderen, aktarım tamamlandıktan noktaya kadar bildirildi kullanım için ödeme sorumludur. Alıcı, sonraki sürümlerde aktarımı zamandan bildirilen kullanım sorumludur. Aktarım önce gerçekleşen ancak daha sonra bildirildi bazı kullanım olabilir. Kullanım alıcının fatura dahil edilir.

* **Alıcı, kullanım ve Fatura geçmişi erişimi var mı?**

  Bilgiler yalnızca alıcıya kullanılabilir son fatura miktarıdır veya ilk fatura başlatmasından önce abonelik aktarılan varsa geçerli bakiye oluşturulur. Kullanım ve fatura geçmişini geri kalanı abonelikle aktarılmaz.

* **Teklif aktarım sırasında değiştirilebilir mi?**

  Teklif aynı kalması gerekir. Teklifiniz değiştirmek için bkz: [Azure aboneliğinizi başka bir teklife geç](billing-how-to-switch-azure-offer.md).

* **Başka bir ülkede bir kullanıcı hesabı için bir abonelik aktarabilirim?**

  Hayır, başka bir ülkede kullanıcı hesabına bir aboneliğin aktarılması desteklenmiyor. Alıcının kullanıcı hesabının aynı ülkede olması gerekir.

* **Alıcı, farklı bir ödeme yöntemi kullanabilir miyim?**

  Evet. Ancak abonelik faturalama geçmişi iki hesap arasında bölünür.  

* **Bir Azure aboneliği transfer sonra ödeme yöntemini etkileniyor mu?**

  Abonelik aktarımı, kredi kartı veya benzer ödeme kabul etmek için yöntem abonelik için ödeme yapmak sağlanmalıdır. Örneğin, Bob bir abonelik için Jane aktarır ve Jane aktarımı kabul eder, Jane abonelik için ödeme yapmak için bir ödeme yöntemi sağlamanız gerekir. Transfer işlemi tamamlandıktan sonra Jane değil Bob abonelik için faturalandırılır.

* **Nasıl veri ve Hizmetleri Azure Aboneliğim için yeni abonelik geçişini miyim?**

  Abonelik sahipliği aktaramaz, kaynaklarınızın el ile geçirebilirsiniz. Bkz: [yeni kaynak grubu veya abonelik kaynaklarını taşıma](../azure-resource-manager/resource-group-move-resources.md).



## <a name="need-help-contact-support"></a>Yardım mı gerekiyor? Desteğe başvurun.
Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) hızla çözümlenen sorunu almak için. 


