---
title: "Azure Active Directory etki alanı Hizmetleri: RHEL VM tooa yönetilen etki alanına Katıl | Microsoft Docs"
description: "Red Hat Enterprise Linux sanal makine birleştirme tooAzure AD etki alanı Hizmetleri"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 87291c47-1280-43f8-8fb2-da1bd61a4942
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 41ca2aaf2eefbf9c403d2b834d61a1aa0943d950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-tooa-managed-domain"></a>Red Hat Enterprise Linux 7 sanal makine tooa yönetilen etki alanına Katıl
Bu makalede toojoin Red Hat Enterprise Linux (RHEL) 7 sanal makine tooan Azure AD etki alanı Hizmetleri etki alanı nasıl yönetileceğini gösterir.

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a>Red Hat Enterprise Linux sanal makine sağlama
Hello Azure portal kullanarak adımları tooprovision RHEL 7 sanal makine aşağıdaki hello gerçekleştirin.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).

    ![Azure portalı panosunun](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. Tıklatın **yeni** sol bölmesinde ve türü hello üzerinde **Red Hat** hello ekran aşağıdaki gösterildiği gibi hello arama çubuğunu içine. Red Hat Enterprise Linux girişleri hello arama sonuçlarında görünür. Tıklatın **Red Hat Enterprise Linux 7.2**.

    ![RHEL sonuçlarında seçin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. Merhaba arama sonuçları hello **her şeyi** bölmesinde hello Red Hat Enterprise Linux 7.2 görüntü listesinde. Tıklatın **Red Hat Enterprise Linux 7.2** tooview hello sanal makine görüntüsü hakkında daha fazla bilgi.

    ![RHEL sonuçlarında seçin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. Merhaba, **Red Hat Enterprise Linux 7.2** bölmesinde hello sanal makine görüntüsü hakkında daha fazla bilgi görmeniz gerekir. Merhaba, **dağıtım modeli seçin** açılan listesinde, select **Klasik**. Merhaba ardından **oluşturma** düğmesi.

    ![Görüntü ayrıntıları görüntüle](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. Merhaba, **Temelleri** hello sayfasının **sanal makine oluşturma** Sihirbazı'nı hello girin **ana bilgisayar adı** hello yeni sanal makine için. Ayrıca bir yerel yönetici kullanıcı adı hello belirtin **kullanıcı adı** alan ve **parola**. SSH anahtar tooauthenticate hello yerel yönetici kullanıcı toouse de seçebilirsiniz. Ayrıca bir **fiyatlandırma katmanı** hello sanal makine için.

    ![VM - temelleri sayfa oluşturma](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. Merhaba, **boyutu** hello sayfasının **sanal makine oluşturma** hello sanal makinenin seçin hello boyutu.

    ![VM - select boyutu oluşturun](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. Merhaba, **ayarları** hello sayfasının **sanal makine oluşturma** seçin hello hello sanal makinesi için depolama hesabı. Tıklatın **sanal ağ** tooselect hello sanal ağ toowhich hello Linux VM dağıtılmalıdır. Merhaba, **sanal ağ** dikey penceresinde, select hello sanal ağ içinde Azure AD etki alanı Hizmetleri kullanılabilir. Bu örnekte, hello 'MyPreviewVNet' sanal ağ seçin.

    ![VM oluşturma - sanal ağı seçin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. Merhaba üzerinde **Özet** hello sayfasının **sanal makine oluşturma** Sihirbazı, gözden geçirme ve tıklatın hello **Tamam** düğmesi.

    ![VM - seçilen sanal ağ oluşturma](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. Merhaba yeni sanal makine hello RHEL 7.2 görüntüyü temel alarak dağıtımını başlamanız gerekir.

    ![VM - Dağıtım başladı oluşturma](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. Birkaç dakika sonra hello sanal makine başarıyla dağıtılan ve kullanılmaya hazır olması gerekir.

    ![Dağıtılan VM - oluşturma](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-toohello-newly-provisioned-linux-virtual-machine"></a>Yeni sağlanan toohello Linux sanal makine uzaktan bağlanma
Azure'da Hello RHEL 7.2 sanal makine sağlandı. Merhaba sonraki görevdir tooconnect uzaktan toohello sanal makine.

**Toohello RHEL 7.2 sanal makineye bağlanmak** hello makalede hello yönergeleri izleyerek [nasıl toolog Linux çalıştıran tooa sanal makine üzerinde](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Merhaba adımları Hello kalan varsayalım hello PuTTY SSH istemcisini tooconnect toohello RHEL sanal makine kullanın. Daha fazla bilgi için bkz: Merhaba [PuTTY indirme sayfası](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

1. Açık hello PuTTY program.
2. Merhaba girin **ana bilgisayar adı** RHEL sanal makine yeni oluşturulan hello için. Bu örnekte, sanal makine hello ana bilgisayar adı 'contoso-rhel.cloudapp .net' sahiptir. Vm'nizin ana bilgisayar adı hello emin değilseniz, toohello VM hello Azure portal panosunda bakın.

    ![PuTTY Bağlan](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. Toohello sanal makineyi hello sanal makineyi oluşturduğunuzda belirttiğiniz hello yerel yönetici kimlik bilgilerini kullanarak oturum açın. Bu örnekte, "mahesh" Merhaba yerel yönetici hesabı kullanılır.

    ![PuTTY oturum açma](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-hello-linux-virtual-machine"></a>Gerekli paketler hello Linux sanal makineye yükleme
Bağlantı toohello sanal makine sonra hello sonraki tooinstall paketleri hello sanal makine üzerinde etki alanına katılma için gerekli bir görevdir. Merhaba aşağıdaki adımları gerçekleştirin:

1. **Realmd yükleyin:** hello realmd paket etki alanına katılma için kullanılır. PuTTY terminalinizde hello aşağıdaki komutu yazın:

    sudo yum yükleme realmd

    ![Realmd yükleyin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    Birkaç dakika sonra hello realmd paket hello sanal makinede yüklü.

    ![yüklü realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. **Sssd yükleyin:** hello realmd paket sssd tooperform etki alanına katılma işlemleri bağlıdır. PuTTY terminalinizde hello aşağıdaki komutu yazın:

    sudo yum yükleme sssd

    ![Sssd yükleyin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    Birkaç dakika sonra hello sssd paket hello sanal makinede yüklü.

    ![yüklü realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. **Kerberos yükleyin:** PuTTY terminalinizde hello aşağıdaki komutu yazın:

    sudo yum yükleme krb5 iş istasyonu krb5-kitaplıklar

    ![Kerberos yükleyin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    Birkaç dakika sonra hello realmd paket hello sanal makinede yüklü.

    ![Kerberos yüklü](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-hello-linux-virtual-machine-toohello-managed-domain"></a>Merhaba Linux sanal makine toohello yönetilen etki alanına katılma
Merhaba Linux sanal makinede yüklü gerekli hello paketlerini, hello sonraki görev toojoin hello sanal makine toohello yönetilen etki alanıdır.

1. Merhaba AAD etki alanı Hizmetleri yönetilen etki bulur. PuTTY terminalinizde hello aşağıdaki komutu yazın:

    sudo bölge CONTOSO100.COM Bul

    ![Bölge Bul](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    Varsa **bölge Bul** oluşturulamıyor toofind, yönetilen etki alanıdır hello etki hello sanal makineden (try ping) erişilebilir olduğundan emin olun. Ayrıca hello sanal makinede dağıtılan toohello gerçekten açıldı olun aynı sanal ağda hangi hello yönetilen etki alanı kullanılabilir.
2. Kerberos başlatır. PuTTY terminalinizde hello aşağıdaki komutu yazın. Toohello 'AAD DC Yöneticiler' grubuna üye olduğu bir kullanıcı belirttiğinizden emin olun. Yalnızca bu kullanıcılar, bilgisayarlar toohello yönetilen etki alanına eklenebilir.

    kinitbob@CONTOSO100.COM

    ![Kinit](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    Büyük harflerle hello etki alanı adı belirtin, başka kinit başarısız emin olun.
3. Merhaba makine toohello etki alanına katılın. PuTTY terminalinizde hello aşağıdaki komutu yazın. Merhaba belirtin aynı kullanıcı hello önceki adım ('kinit') belirtildi.

    sudo bölge birleştirme--ayrıntılı CONTOSO100.COM -U 'bob@CONTOSO100.COM'

    ![Bölge birleştirme](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

("Başarılı bir şekilde kaydedilen makine bölgedeki") bir ileti almalısınız hello makine başarıyla katıldı toohello yönetilen etki alanında olduğunda.

## <a name="verify-domain-join"></a>Etki alanına katılma doğrulayın
Hızlı bir şekilde hello makine başarıyla katıldı toohello yönetilen etki alanı olup olmadığını doğrulayın. Toohello bağlanmak yeni RHEL hello kullanıcı hesabının doğru şekilde giderilip giderilmediğini SSH ve bir etki alanı kullanıcı hesabı ve ardından onay toosee kullanarak VM etki alanına katıldı.

1. PuTTY içinde terminal, komut tooconnect toohello yeni aşağıdaki türü hello SSH kullanarak RHEL sanal makine etki alanına katıldı. Toohello yönetilen etki alanına ait bir etki alanı hesabı kullanın (örneğin, 'bob@CONTOSO100.COM' Bu durumda.)

    SSH -l bob@CONTOSO100.COM contoso rhel.cloudapp.net
2. PuTTY terminalinizde hello giriş dizini doğru başlatılmadı komutu toosee izlemeyi hello yazın.

    pwd
3. PuTTY terminalinizde hello grup üyeliklerini doğru çözüldüğünü komutu toosee izlemeyi hello yazın.

    id

Bu komutların örnek bir çıktı aşağıdaki gibidir:

![Etki alanına katılma doğrulayın](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a>Sorun giderme etki alanına katılma
Toohello başvuran [sorun giderme etki alanına katılma](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) makalesi.

## <a name="related-content"></a>İlgili İçerik
* [Azure AD etki alanı Hizmetleri - başlangıç kılavuzu](active-directory-ds-getting-started.md)
* [Windows Server sanal makine tooan Azure AD etki alanı Hizmetleri yönetilen etki alanına Katıl](active-directory-ds-admin-guide-join-windows-vm.md)
* [Nasıl toolog Linux çalıştıran tooa sanal makine üzerinde](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* [Kerberos yükleme](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [Red Hat Enterprise Linux 7 - Windows tümleştirme Kılavuzu](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
