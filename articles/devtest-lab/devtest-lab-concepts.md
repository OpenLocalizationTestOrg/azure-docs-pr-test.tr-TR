---
title: "aaaDevTest Labs kavramları | Microsoft Docs"
description: "DevTest Labs temel kavramlarını Hello öğrenin ve onu kolay toocreate yapabilirsiniz nasıl yönetmek ve Azure sanal makinelerini izlemek"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 105919e8-3617-4ce3-a29f-a289fa608fb2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: d9f1d948002c4d3121e5bdd4e65eb8b54cd91f9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="devtest-labs-concepts"></a>DevTest Labs kavramları
## <a name="overview"></a>Genel Bakış
liste aşağıdaki hello anahtar DevTest Labs kavramları ve tanımları içerir:

## <a name="labs"></a>Labs
Sınırları ve kotalar belirterek daha iyi olanak sağlayan sanal makineler (VM'ler), bu kaynakları yönetmek gibi bir laboratuvar kaynakları, bir grup kapsayan hello altyapısıdır.

## <a name="virtual-machine"></a>Sanal makine
Bir Azure VM çeşitli türlerde biri [isteğe bağlı, ölçeklenebilir bilgi işlem kaynakları](https://docs.microsoft.com/azure/app-service-web/choose-web-site-cloud-service-vm) Azure'un sunduğu. Sanallaştırma esnekliği toobuy gerek kalmadan hello ve hala toomaintain gerek olmasa da, çalıştıran fiziksel bir donanım hello korumak azure VM'ler verin, yapılandırma, düzeltme eki uygulama ve hello yazılım yükleme gibi belirli görevleri gerçekleştirerek VM hello Bu dosya üzerinde çalışır.

[Azure'da Windows sanal makineler genel bakış](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-overview) verir önce dikkate almanız gerekenler hakkında bilgi bir VM, nasıl oluşturduğunuz ve yönettiğiniz nasıl oluşturma.

## <a name="claimable-vm"></a>Claimable VM
Bir Azure Claimable VM izinlerine sahip herhangi bir laboratuvar kullanıcı tarafından kullanılabilir olan bir sanal makinedir. Laboratuvar Yönetim VM'ler belirli taban görüntüleri ve yapıları hazırlamak ve paylaşılan tooa havuzu kaydedebilirsiniz. Bu yapılandırmaya sahip bir gerektiğinde bir laboratuvar kullanıcı sonra çalışan bir VM hello havuzundan talep edebilir.

Claimable bir VM başlangıçta tooany belirli kullanıcı atanmamış, ancak her kullanıcının listesinde "Claimable sanal makineler" altında gösterilir. VM bir kullanıcı tarafından talep sonra "Benim sanal makineler" alanı tootheir taşınır ve artık herhangi bir kullanıcı tarafından claimable değil.

## <a name="environment"></a>Ortam
DevTest Labs'de bir ortamda bir laboratuvarda Azure kaynağı koleksiyonunu tooa ifade eder. [Bu blog gönderisine](https://blogs.msdn.microsoft.com/devtestlab/2016/11/16/connect-2016-news-for-azure-devtest-labs-azure-resource-manager-template-based-environments-vm-auto-shutdown-and-more/) anlatılmaktadır nasıl toocreate çoklu VM, Azure Resource Manager şablonlarınızı ortamlarından.

## <a name="base-images"></a>Taban görüntüleri
Taban görüntüleri VM görüntülerle tüm hello araçları ve ayarları önceden yüklenmiş olan ve yapılandırılmış tooquickly bir VM oluşturun. Bir VM test aracınızı var olan bir temel çekme ve bir yapı tooinstall ekleyerek sağlayabilirsiniz. Sonra hello sağladığınız VM böylece hello temel tooreinstall hello test aracısı her sağlama için gerek kalmadan kullanılabilmesi için bir taban hello gibi VM.

## <a name="artifacts"></a>Yapıtlar
Yapıları kullanılan toodeploy olan ve bir VM sağlandıktan sonra uygulamanızı yapılandırın. Yapıtlar şunlar olabilir:

* Aracılar, Fiddler ve Visual Studio gibi hello VM - üzerinde tooinstall istediğiniz araçları.
* Bir depoyu kopyalama gibi hello VM - üzerinde toorun istediğiniz eylemleri.
* Tootest istediğiniz uygulamalar.

Ürünleridir [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) yapılandırmayı uygulamak ve yönergeleri tooperform dağıtım içeren JSON dosyaları.

## <a name="artifact-repositories"></a>Yapı depoları
Yapı depoları yapıları burada iade git depoları ' dir. Yapı depoları, yeniden etkinleştirme ve paylaşımı, kuruluşunuzda toomultiple labs eklenebilir.

## <a name="formulas"></a>Formüller
Toplama toobase görüntülerinde formüller hızlı VM sağlama için bir mekanizma sağlar. DevTest Labs formülde varsayılan özellik değerleri kullanılan toocreate Laboratuvar VM listesidir.
Formül, aynı ayarlamak özelliklerinin - temel görüntü, VM boyutunu, sanal ağ ve yapıları - gibi hello olan VM'ler ile her zaman bu özellikleri toospecify gerek kalmadan oluşturulabilir. VM bir formülünden oluştururken, hello varsayılan değerler olarak kullanılamaz-olduğundan veya değiştirilemiyor.

## <a name="policies"></a>İlkeler
İlkeleri laboratuvarınızda maliyetini denetleme yardımcı olur. Örneğin, tanımlanmış bir zamanlamaya göre sanal makineleri kapatın ilke tooautomatically oluşturabilirsiniz.

## <a name="caps"></a>Büyük harfler
Büyük harf bir mekanizma toominimize atık laboratuvarınızda olur. Örneğin, kullanıcı başına veya bir laboratuvarda oluşturulan VM'ler cap toorestrict hello sayısını ayarlayabilirsiniz.

## <a name="security-levels"></a>Güvenlik düzeyleri
Güvenlik erişimi Azure rol tabanlı erişim denetimi (RBAC) tarafından belirlenir. toounderstand nasıl çalışır erişmek için onu toounderstand hello farklarını izin, bir rolü ve kapsamı RBAC tarafından tanımlandığı şekilde yardımcı olur.

* Tanımlanmış erişim tooa belirli bir eylemi (örneğin okuma erişimi tooall sanal makineler) izni - izni yok.
* Rol - bir rolü gruplandırılmış ve tooa kullanıcı atanan izinler kümesidir. Örneğin, hello *abonelik sahibi* rol bir abonelik içindeki tooall erişimine sahiptir.
* Kapsam - kapsamı, bir kaynak grubu, tek Laboratuvar veya aboneliğin tümü hello gibi bir Azure kaynağı hello hiyerarşisi içinde düzeydir.

DevTest Labs Hello kapsamında rolleri toodefine kullanıcı izinlerini iki tür vardır: Laboratuvar sahip ve Laboratuvar kullanıcı.

* Laboratuvar sahibi - bir laboratuvar sahibi hello Laboratuvar içinde tooany erişimine sahiptir. Bu nedenle, bir laboratuvar sahibi ilkeleri değiştirmek, okuma ve herhangi bir VM yazma, hello sanal ağı değiştirin ve benzeri.
* Laboratuvar kullanıcı - Laboratuvar kullanıcı VM'ler, ilkeleri ve sanal ağlar gibi tüm Laboratuvar kaynaklarını görüntüleyebilir ancak ilkeleri değiştiremez veya herhangi bir VM diğer kullanıcılar tarafından oluşturulan.

toosee toocreate özel DevTest Labs rollerinde başvurmak nasıl toohello makale [toospecific Laboratuvar ilkeleri kullanıcı izinleri](devtest-lab-grant-user-permissions-to-specific-lab-policies.md).

Kapsamları hiyerarşik olduğundan, bir kullanıcının belirli bir kapsamda izinleri olduğunda otomatik olarak çevrelenmiş her alt düzey kapsamındaki bu izinler verilir. Abonelik sahibi toohello rolü atanmış bir kullanıcı örneği için daha sonra bunlar tüm sanal makineler, tüm sanal ağları ve tüm labs dahil tooall kaynakları için bir abonelik varsa. Bu nedenle, abonelik sahibi, Laboratuvar sahibinin hello rolü otomatik olarak devralır. Ancak, hello ters doğru değil. Laboratuvar sahibi hello abonelik düzeyinden daha düşük bir kapsam erişim tooa laboratuvarı sahiptir. Bu nedenle, bir laboratuvar sahibi mümkün toosee sanal makine veya sanal ağlar ya da hello Laboratuvar dışında olan herhangi bir kaynağa olmaz.

## <a name="azure-resource-manager-templates"></a>Azure Resource Manager şablonları
Bu makalede açıklanan kavramları sağlayan Azure Resource Manager şablonları kullanarak yapılandırılabilir hello tümünün hello altyapı/yapılandırmasını Azure çözümünüzün tanımlayın ve art arda tutarlı bir durumda dağıtın.

[Merhaba yapısı ve Azure Resource Manager şablonları sözdizimini anlamanız](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates#template-format) hello farklı bir şablon bölümlerde kullanılabilir olan bir Azure Resource Manager şablonu ve özelliklerinin hello hello yapısını açıklar.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Sonraki adımlar
[DevTest Labs'de Laboratuvar oluşturma](devtest-lab-create-lab.md)
