---
title: "aaaSecurity Azure SQL Server'da dikkate alınacak noktalar | Microsoft Docs"
description: "Bu konu, bir Azure sanal makinede çalışan SQL Server güvenliğini sağlamaya yönelik genel rehberlik sağlar."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: d710c296-e490-43e7-8ca9-8932586b71da
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/02/2017
ms.author: jroth
ms.openlocfilehash: 14c3d828fa87446da67beea6d28886de254afe15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-sql-server-in-azure-virtual-machines"></a>Azure Sanal Makineler'de SQL Server için Güvenlikle İlgili Dikkat Edilmesi Gerekenler

Bu konu, bir Azure sanal makine (VM) güvenli erişim tooSQL sunucu örnekleri sağlanmasına yardımcı genel güvenlik yönergeleri içerir.

Azure birkaç sektör düzenlemelerini ve bir sanal makinede çalışan SQL Server ile uyumlu bir çözüm toobuild etkinleştirebilirsiniz standartları karşılar. Azure ile Mevzuat uyumluluğu hakkında daha fazla bilgi için bkz: [Azure Güven Merkezi](https://azure.microsoft.com/support/trust-center/).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="control-access-toohello-sql-vm"></a>Denetim erişim toohello SQL VM

SQL Server sanal makine oluşturduğunuzda, toocarefully nasıl kontrol kimlerin erişimi toohello makine ve tooSQL sunucusu olduğunu göz önünde bulundurun. Genel olarak, yapmanız gerektiğini hello aşağıdaki:

- Erişim tooSQL sunucu tooonly hello uygulamaları ve ihtiyacınız olan istemciler kısıtlayın.
- Kullanıcı hesapları ve parolaları yönetmek için en iyi uygulamaları izleyin.

Aşağıdaki bölümlerde hello bu noktaları üzerinden düşünmeye önerileri sağlar.

## <a name="secure-connections"></a>Güvenli bağlantılar

Bir galeri görüntüsü ile bir SQL Server sanal makine oluşturduğunuzda, hello **SQL Server bağlantısı** seçeneğini tercih ettiğiniz hello verir **yerel (VM)**, **özel (sanal ağ dahilinde)** , veya **genel (Internet)**.

![SQL Server bağlantısı](./media/virtual-machines-windows-sql-security/sql-vm-connectivity-option.png)

Merhaba en iyi güvenlik için senaryonuza hello en kısıtlayıcı seçeneği belirleyin. SQL Server üzerinde erişen bir uygulama çalıştırıyorsanız, örneğin, aynı VM sonra hello **yerel** hello en güvenli seçenektir. Erişim toohello SQL Server'ı sonra gerektiren bir Azure uygulama çalıştırıyorsanız, **özel** yalnızca belirtilen hello içinde iletişim tooSQL sunucu güvenli hale getirdiği [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md). Gerektiriyorsa **ortak** (internest) erişim toohello SQL Server VM, ardından yapma emin toofollow saldırı yüzey alanınızı bu konuda tooreduce diğer en iyi yöntemler.

Merhaba seçilen seçenekleri hello Portalı'nda gelen güvenlik kuralları hello VM'ler üzerinde kullanmak [ağ güvenlik grubu](../../../virtual-network/virtual-networks-nsg.md) (NSG) tooallow veya ağ trafiğini tooyour sanal makine reddedin. Değiştirin veya yeni gelen NSG kuralları tooallow trafiği toohello SQL Server bağlantı noktası (varsayılan 1433) oluşturun. Bu bağlantı noktası üzerinden toocommunicate izin verilen belirli IP adreslerini de belirtebilirsiniz.

![Ağ güvenlik grubu kuralları](./media/virtual-machines-windows-sql-security/sql-vm-network-security-group-rules.png)

Ayrıca tooNSG toorestrict ağ trafiği kuralları, hello sanal makinede hello Windows Güvenlik Duvarı'nı da kullanabilirsiniz.

Uç noktaları hello Klasik dağıtım modeliyle kullanıyorsanız, bunları kullanmıyorsanız hello sanal makine üzerindeki tüm uç noktaları kaldırın. ACL'ler uç ile kullanma ile ilgili yönergeler için bkz: [uç noktada Yönet hello ACL](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint). Bu hello Kaynak Yöneticisi'ni kullanan VM'ler için gerekli değildir.

Son olarak, Azure sanal makinesinde SQL Server veritabanı altyapısı hello hello örneği için şifreli bağlantıları etkinleştirmeyi düşünün. SQL server örneği ile bir imzalı sertifika yapılandırın. Daha fazla bilgi için bkz: [şifreli bağlantıları etkinleştirmek toohello veritabanı altyapısı](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine) ve [bağlantı dizesi sözdizimi](https://msdn.microsoft.com/library/ms254500.aspx).

## <a name="use-a-non-default-port"></a>Varsayılan olmayan bağlantı noktası kullanma

Varsayılan olarak, SQL Server 1433 iyi bilinen bir bağlantı noktasında dinler. Daha yüksek güvenlik için SQL Server toolisten 1401 gibi varsayılan olmayan bir bağlantı noktası yapılandırın. Bir SQL Server galeri görüntüsü hello Azure portal'ın sağlarsanız, bu bağlantı noktası hello belirtebilirsiniz **SQL Server ayarları** dikey.

tooconfigure bu sağladıktan sonra iki seçeneğiniz vardır:

- Resource Manager VM'ler için seçtiğiniz **SQL Server yapılandırma** hello VM genel bakış dikey penceresinden. Bu bir seçenek toochange hello bağlantı noktası sağlar.

  ![TCP bağlantı noktası portalında değiştirin](./media/virtual-machines-windows-sql-security/sql-vm-change-tcp-port.png)

- Klasik sanal makineleri veya hello portal ile sağlanan olmayan SQL Server VM'ler için uzaktan toohello VM bağlanarak hello bağlantı noktasını el ile yapılandırabilirsiniz. Merhaba yapılandırma adımları için bkz: [belirli bir TCP bağlantı noktası üzerinde bir sunucu tooListen yapılandırma](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port). El ile bu yöntemi kullanırsanız, tooadd Windows Güvenlik duvarı kuralı tooallow gelen trafik, TCP bağlantı noktasını da gerekir.

> [!IMPORTANT]
> SQL Server bağlantı noktası açık toopublic Internet bağlantıları ise varsayılan olmayan bağlantı noktası belirterek iyi bir fikirdir.

SQL Server varsayılan olmayan bağlantı noktasında dinleme zaman bağladığınızda, başlangıç bağlantı noktası belirtmeniz gerekir. Örneğin, burada hello sunucusu IP adresi 13.55.255.255 ve SQL Server 1401 bağlantı noktasında dinleme bir senaryo düşünün. tooconnect tooSQL sunucu, belirtirsiniz `13.55.255.255,1401` hello bağlantı dizesinde.

## <a name="manage-accounts"></a>Hesapları yönetme

Saldırganlar tooeasily tahmin hesap adlarını veya parolaları istemezsiniz. Aşağıdaki ipuçları toohelp hello kullan:

- Yok adlı bir benzersiz yerel yönetici hesabı oluşturma **yönetici**.

- Karmaşık güçlü parolalar, tüm hesapları için kullanın. Hakkında daha fazla bilgi için bkz: toocreate güçlü bir parola [güçlü bir parola oluşturmak](https://support.microsoft.com/instantanswers/9bd5223b-efbe-aa95-b15a-2fb37bef637d/create-a-strong-password) makale.

- Varsayılan olarak, Azure SQL Server sanal makinesine Kurulum sırasında Windows kimlik doğrulaması seçer. Bu nedenle, hello **SA** oturum açma devre dışı bırakıldı ve bir parola Kurulumu tarafından atanır. Bu hello öneririz **SA** oturum açma bırakılamadı kullanılan veya etkinleştirilemedi. Bir SQL oturum açma görüntülenmesi gerekiyorsa, stratejileri aşağıdaki hello birini kullanın:

  - SQL hesabı olan benzersiz bir ad oluşturmak **sysadmin** üyeliği. Merhaba portalından etkinleştirerek bunu yapabilirsiniz **SQL kimlik doğrulaması** sağlama sırasında.

    > [!TIP] 
    > Sağlama işlemi sırasında SQL kimlik doğrulamasını etkinleştirmezseniz, el ile Merhaba kimlik doğrulama modu çok değiştirmelisiniz**SQL Server ve Windows kimlik doğrulama modu**. Daha fazla bilgi için bkz: [sunucu kimlik doğrulaması modunu değiştirme](https://docs.microsoft.com/sql/database-engine/configure-windows/change-server-authentication-mode).

  - Merhaba kullanmanız gerekiyorsa **SA** oturum açma, sağlama ve ata yeni güçlü bir parola sonra etkinleştir hello oturum açma.

## <a name="follow-on-premises-best-practices"></a>Şirket içi en iyi uygulamaları izleyin

Ayrıca toohello uygulamalar bu konuda açıklanan gözden geçirin ve uygun olan yerlerde hello geleneksel şirket içi güvenlik uygulamalarını uygulamak öneririz. Daha fazla bilgi için bkz: [bir SQL Server yüklemesi için güvenlik konuları](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation)

## <a name="next-steps"></a>Sonraki Adımlar

Ayrıca performans geçici en iyi yöntemler ilgilendiğiniz olup [Azure Virtual Machines'de SQL Server için performans en iyi uygulamaları](virtual-machines-windows-sql-performance.md).

Azure vm'lerinde SQL Server toorunning ilgili diğer konular için bkz: [Azure sanal makinelere genel bakış SQL Server'da](virtual-machines-windows-sql-server-iaas-overview.md).

