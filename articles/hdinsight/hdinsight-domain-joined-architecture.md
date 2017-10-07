---
title: "Azure Hdınsight mimarisi aaaDomain katılmış | Microsoft Docs"
description: "Nasıl tooplan etki alanı Hdınsight katılmış öğrenin."
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
ms.openlocfilehash: 1c3ecedf3739b4f8fa54160225be9c1d6e2ca6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-azure-domain-joined-hadoop-clusters-in-hdinsight"></a>HDInsight'ta Azure etki alanına katılmış Hadoop kümeleri planlama

Merhaba geleneksel Hadoop bir tek kullanıcı kümedir. Büyük veri iş yükleri oluşturan küçük uygulama ekiplerine sahip çoğu şirket için uygundur. Hadoop'un popülerliği arttıkça çoğu kurum, kümelerin BT ekipleri tarafından yönetildiği ve birden çok uygulama ekibinin ortak kümelerde çalıştığı bir modele geçiş yapıyor. Bu nedenle, ilgili çok kullanıcılı kümeleri arasında olan işlevler en istenen işlevlerin Azure Hdınsight hello.

Kendi çok kullanıcılı kimlik doğrulama ve yetkilendirme oluşturmak yerine, Hdınsight hello en popüler kimlik sağlayıcısı üzerinde--Active Directory (AD) kullanır. AD içinde Hello güçlü güvenlik işlev hdınsight'ta kullanılan toomanage çok kullanıcılı yetkilendirme olabilir. Hdınsight AD ile tümleştirme, AD kimlik bilgilerinizi kullanarak hello kümeleriyle iletişim kurabilir. Tüm Hdınsight üzerinde çalışan hizmetleri hello şekilde Hdınsight eşleşen bir AD tooa yerel Hadoop kullanıcı, (Ambari, sunucu, bırakabilmenizi, Spark thrift Hive sunucu ve diğerleri) hello kimliği doğrulanmış kullanıcı için sorunsuz bir şekilde çalışır.

## <a name="integrate-hdinsight-with-ad-and-ad-on-iaas-vm"></a>Hdınsight AD ve Iaas VM üzerinde AD ile tümleştirme

Hdınsight Azure AD veya Iaas VM üzerinde AD ile tümleştirerek, etki alanına katılmış tooa etki alanı hello Hdınsight küme düğümü olan. Hdınsight Hadoop Hizmetleri hello kümede çalışan hello için hizmet asıl adı oluşturur ve bunları belirtilen bir kuruluş birimi (OU) Azure AD veya Iaas VM üzerinde AD yerleştirir. Hdınsight de geriye doğru DNS eşlemelerini hello için hello etki alanındaki etki alanına katılmış toohello hello düğümleri IP adreslerini oluşturur.

Bu kuruluma birden fazla mimari kullanarak ulaşabilirsiniz. Mimariler aşağıdaki hello seçebilirsiniz.

**Azure Iaas üzerinde çalışan AD ile tümleşik Hdınsight**

Hdınsight Active Directory ile tümleştirme için hello basit mimarisi budur. Merhaba AD etki alanı denetleyicisi bir (veya birden çok) sanal makinelerle (VM) çalışır. Genellikle bu VM'ler bir sanal ağ içerisindedir. Merhaba Hdınsight kümesi için başka bir sanal ağ ayarlayın. Hdınsight toohave görüş tooActive Directory toopeer bu sanal ağlar kullanarak gereksinim duyduğunuz [VNet-VNet eşlemesi](../virtual-network/virtual-network-create-peering.md). Oluşturursanız, Active Directory hello oluşturabilirsiniz ve Hdınsight'ta hello aynı sanal ağı ARM, Active Directory'de hello ve toodo eşliği olması gerekmez. 

![HDInsight küme topolojisini etki alanına katma](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_1.png)

> [!NOTE]
> Bu mimaride, Azure Data Lake Store ile Merhaba Hdınsight kümesi kullanamazsınız.


Active Directory için Önkoşullar:

* Bir [kuruluş birimi](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) hangi yerleştirdiğiniz içinde oluşturulmalıdır Hdınsight küme VM'ler hello ve hello küme tarafından kullanılan hizmet asıl adı hello.
* [Hafif Dizin Erişim protokolleri](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md) (LDAPs) ayarlanmalıdır AD ile iletişim kurmak için. Merhaba kullanılan sertifika tooset LDAPS kurma (otomatik imzalı bir sertifika değil) gerçek bir sertifika olmalıdır.
* Geriye doğru DNS bölgeleri hello Hdınsight alt ağ (örneğin, 10.2.0.0/24 hello önceki resimdeki) başlangıç IP adresi aralığı için hello etki alanında oluşturulmalıdır.
* Hizmet hesabı veya kullanıcı hesabı gereklidir. Bu hesap toocreate hello Hdınsight kümesi kullanın. Bu hesabın hello aşağıdaki izinleri olması gerekir:

    - İzinleri toocreate hizmet asıl nesneleri ve makine nesnelerinde hello kuruluş birimi
    - İzinleri toocreate geriye doğru DNS proxy kuralları
    - İzinleri toojoin makineler toohello Active Directory etki alanı

**Yalnızca bulutta çalışan Azure AD ile tümleştirilmiş HDInsight**

Yalnızca bulutta çalışan Azure AD için bir etki alanı denetleyiciyi yapılandırarak HDInsight ile Azure AD'nin tümleştirilmesini sağlayın. Bu kullanılarak elde edilir [Azure Active Directory etki alanı Hizmetleri](../active-directory-domain-services/active-directory-ds-overview.md) (Azure AD DS). Azure AD DS etki alanı denetleyicisi makineler hello bulutta oluşturur ve bunları için IP adresleri sağlar. Yüksek kullanılabilirlik için iki etki alanı denetleyicisi oluşturur.

Şu anda Azure AD DS yalnızca klasik sanal ağlarda mevcuttur. Bunu yalnızca hello Klasik Azure portalı kullanılarak erişilebilir. Merhaba hello toobe gereken Azure portalında sanal ağ var. Hdınsight VNet-VNet eşlemesi kullanarak hello Klasik sanal ağ ile eşlenen.

> [!NOTE]
> Klasik sanal ağ ve sanal ağ gerektiren her iki sanal ağ içinde olan bir Azure Resource Manager arasında eşleme hello aynı bölgede ve altında hello aynı Azure aboneliği.

![HDInsight küme topolojisini etki alanına katma](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_2.png)

Azure AD önkoşulları:

* Bir [kuruluş birimi](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) hangi yerleştirdiğiniz içinde oluşturulmalıdır Hdınsight küme VM'ler hello ve hello küme tarafından kullanılan hizmet asıl adı hello.
* Azure AD DS'yi yapılandırırken [LDAPS](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md) kurulumu gerçekleştirmeniz gerekir. Merhaba kullanılan sertifika tooset LDAPS kurma (otomatik imzalı bir sertifika değil) gerçek bir sertifika olmalıdır.
* Geriye doğru DNS bölgeleri hello Hdınsight alt ağ (örneğin, 10.2.0.0/24 hello önceki resimdeki) başlangıç IP adresi aralığı için hello etki alanında oluşturulmalıdır.
* [Parola karmaları](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md) Azure AD tooAzure AD DS eşitlenen gerekir.
* Hizmet hesabı veya kullanıcı hesabı gereklidir. Bu hesap toocreate hello Hdınsight kümesi kullanın. Bu hesabın hello aşağıdaki izinleri olması gerekir:

    - İzinleri toocreate hizmet asıl nesneleri ve makine nesnelerinde hello kuruluş birimi
    - İzinleri toocreate geriye doğru DNS proxy kuralları
    - İzinleri toojoin makineler toohello Azure AD etki alanı

## <a name="next-steps"></a>Sonraki adımlar
* bir etki alanına katılmış Hdınsight kümesi tooconfigure bkz [etki alanına katılmış Hdınsight kümeleri yapılandırma](hdinsight-domain-joined-configure.md).
* bkz: toomanage etki alanına katılmış Hdınsight kümeleri [etki alanına katılmış Hdınsight kümelerini yönetme](hdinsight-domain-joined-manage.md).
* bkz: tooconfigure Hive ilkeleri ve çalışma Hive sorguları [etki alanına katılmış Hdınsight kümeleri için yapılandırma Hive ilkeleri](hdinsight-domain-joined-run-hive.md).
* etki alanına katılmış Hdınsight kümelerinde SSH kullanarak toorun Hive sorguları bkz [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).
