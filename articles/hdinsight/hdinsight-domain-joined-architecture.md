---
title: "Etki alanına katılmış Azure Hdınsight mimarisi | Microsoft Docs"
description: "Etki alanına katılmış HDInsight planlama hakkında bilgi edinin."
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7dc6847d-10d4-4b5c-9c83-cc513cf91965
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: saurinsh
ms.openlocfilehash: 7e34f47f09466a40993b4cc797ff1cad2bdaeafe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="plan-azure-domain-joined-hadoop-clusters-in-hdinsight"></a>HDInsight'ta Azure etki alanına katılmış Hadoop kümeleri planlama

Geleneksel Hadoop tek kullanıcılı bir kümedir. Büyük veri iş yükleri oluşturan küçük uygulama ekiplerine sahip çoğu şirket için uygundur. Hadoop'un popülerliği arttıkça çoğu kurum, kümelerin BT ekipleri tarafından yönetildiği ve birden çok uygulama ekibinin ortak kümelerde çalıştığı bir modele geçiş yapıyor. Bu nedenle çok kullanıcılı kümeler gibi işlevler, en çok talep gören Azure HDInsight işlevlerinden biri.

Kendi çok kullanıcılı kimlik doğrulama ve yetkilendirme oluşturmak yerine, Hdınsight en popüler kimlik sağlayıcısı--Active Directory (AD) kullanır. AD güçlü güvenlik işlevindeki hdınsight'ta çok kullanıcılı yetkilendirmeyi yönetmek için kullanılabilir. Hdınsight AD ile tümleştirme, AD kimlik bilgilerinizi kullanarak kümeleriyle iletişim kurabilir. Hdınsight Hdınsight üzerinde çalışan tüm hizmetleri yerel bir Hadoop kullanıcı için bir AD kullanıcısının eşler (Ambari, sunucu, bırakabilmenizi, Spark thrift Hive sunucu ve diğerleri) kimliği doğrulanmış kullanıcı için sorunsuz bir şekilde çalışır.

## <a name="integrate-hdinsight-with-ad-and-ad-on-iaas-vm"></a>Hdınsight AD ve Iaas VM üzerinde AD ile tümleştirme

Hdınsight Azure AD veya Iaas VM üzerinde AD ile tümleştirerek, Hdınsight küme düğümleri etki alanına bir etki alanına katılmış. Hdınsight küme üzerinde çalışan Hadoop Hizmetleri için hizmet asıl adı oluşturur ve bunları belirtilen bir kuruluş birimi (OU) Azure AD veya Iaas VM üzerinde AD yerleştirir. Hdınsight geriye doğru DNS eşlemelerini etki alanına katılan düğümlerin IP adresleri etki alanında da oluşturur.

Bu kuruluma birden fazla mimari kullanarak ulaşabilirsiniz. Aşağıdaki mimarilerin arasından seçim yapabilirsiniz.

**Azure Iaas üzerinde çalışan AD ile tümleşik Hdınsight**

HDInsight’ı Active Directory ile tümleştirmek için kullanabileceğiniz en basit mimari budur. Bir (veya birden çok) sanal makinelerde (VM'ler) Azure AD etki alanı denetleyicisi çalışır. Genellikle bu VM'ler bir sanal ağ içerisindedir. HDInsight kümesi için başka bir sanal ağ kurarsınız. Active Directory için bir satır görüş sağlamak Hdınsight için kullanarak bu sanal ağlar eş gerek [VNet-VNet eşlemesi](../virtual-network/virtual-network-create-peering.md). ARM üzerinde Active Directory oluşturursanız, daha sonra Active Directory ve Hdınsight aynı Vnet'i oluşturabilirsiniz ve eşliği yapmanız gerekmez. 

![HDInsight küme topolojisini etki alanına katma](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_1.png)

> [!NOTE]
> Bu mimaride, Azure Data Lake Store'u HDInsight kümesi ile kullanamazsınız.


Active Directory için Önkoşullar:

* HDInsight kümesi VM'lerini ve küme tarafından kullanılan hizmet sorumlularını yerleştireceğiniz bir [kuruluş birimi](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) oluşturulmalıdır.
* [Hafif Dizin Erişim protokolleri](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md) (LDAPs) ayarlanmalıdır AD ile iletişim kurmak için. LDAPS kurulumu için kullanılan sertifika gerçek bir sertifika (otomatik olarak imzalanan sertifika değil) olmalıdır.
* HDInsight alt ağının IP adresi aralığı için etki alanında ters DNS bölgeleri oluşturulmalıdır (örneğin, bir önceki resimde 10.2.0.0/24).
* Hizmet hesabı veya kullanıcı hesabı gereklidir. Bu hesabı HDInsight kümesini oluşturmak için kullanın. Bu hesap aşağıdaki izinlere sahip olmalıdır:

    - Kuruluş birimi içerisinde hizmet sorumlusu nesneleri ve makine nesneleri oluşturma izinleri
    - Ters DNS proxy kuralları oluşturma izinleri
    - Makineleri Active Directory etki alanına katma izinleri

**Yalnızca bulutta çalışan Azure AD ile tümleştirilmiş HDInsight**

Yalnızca bulutta çalışan Azure AD için bir etki alanı denetleyiciyi yapılandırarak HDInsight ile Azure AD'nin tümleştirilmesini sağlayın. Bu kullanılarak elde edilir [Azure Active Directory etki alanı Hizmetleri](../active-directory-domain-services/active-directory-ds-overview.md) (Azure AD DS). Azure AD DS bulutta etki alanı denetleyici makinelerini oluşturur ve bunların IP adreslerini sağlar. Yüksek kullanılabilirlik için iki etki alanı denetleyicisi oluşturur.

Şu anda Azure AD DS yalnızca klasik sanal ağlarda mevcuttur. Yalnızca klasik Azure portalı kullanılarak erişilebilir. Azure portalında yer alan HDInsight sanal ağının sanal ağlar arası eşleme kullanılarak klasik sanal ağla eşlenmesi gerekir.

> [!NOTE]
> Klasik bir sanal ağ ile bir Azure Resource Manager sanal ağı arasında eşleme gerçekleştirilebilmesi için her iki sanal ağ da aynı bölgede ve aynı Azure aboneliği altında olmalıdır.

![HDInsight küme topolojisini etki alanına katma](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_2.png)

Azure AD önkoşulları:

* HDInsight kümesi VM'lerini ve küme tarafından kullanılan hizmet sorumlularını yerleştireceğiniz bir [kuruluş birimi](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) oluşturulmalıdır.
* Azure AD DS'yi yapılandırırken [LDAPS](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md) kurulumu gerçekleştirmeniz gerekir. LDAPS kurulumu için kullanılan sertifika gerçek bir sertifika (otomatik olarak imzalanan sertifika değil) olmalıdır.
* HDInsight alt ağının IP adresi aralığı için etki alanında ters DNS bölgeleri oluşturulmalıdır (örneğin, bir önceki resimde 10.2.0.0/24).
* [Parola karmalarının](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md) Azure AD'den Azure AD DS'ye eşitlenmesi gerekir.
* Hizmet hesabı veya kullanıcı hesabı gereklidir. Bu hesabı HDInsight kümesini oluşturmak için kullanın. Bu hesap aşağıdaki izinlere sahip olmalıdır:

    - Kuruluş birimi içerisinde hizmet sorumlusu nesneleri ve makine nesneleri oluşturma izinleri
    - Ters DNS proxy kuralları oluşturma izinleri
    - Makineleri Azure AD etki alanına katma izinleri

## <a name="next-steps"></a>Sonraki adımlar
* Etki alanına katılmış bir HDInsight kümesi yapılandırmak için bkz. [Etki alanına katılmış HDInsight kümelerini yapılandırma](hdinsight-domain-joined-configure.md).
* Etki alanına katılmış HDInsight kümelerini yönetmek için bkz. [Etki alanına katılmış HDInsight kümelerini yönetme](hdinsight-domain-joined-manage.md).
* Hive ilkelerini yapılandırmak ve Hive sorgularını çalıştırmak için bkz. [Etki alanına katılmış HDInsight kümeleri için Hive ilkelerini yapılandırma](hdinsight-domain-joined-run-hive.md).
* Etki alanına katılmış Hdınsight kümelerinde SSH kullanarak Hive sorguları çalıştırmak için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).
