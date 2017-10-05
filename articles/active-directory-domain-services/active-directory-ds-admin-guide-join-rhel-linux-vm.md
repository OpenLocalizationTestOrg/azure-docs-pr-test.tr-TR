---
title: "Azure Active Directory etki alanı Hizmetleri: RHEL VM yönetilen bir etki alanına katılın. | Microsoft Docs"
description: "Red Hat Enterprise Linux sanal makinesini Azure AD Etki Alanı Hizmetleri'ne ekleme"
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
ms.openlocfilehash: 69f1850bfed90392e9a4695e2443ffaa6bfc746d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-to-a-managed-domain"></a>Red Hat Enterprise Linux 7 sanal makinesini yönetilen bir etki alanına ekleme
Bu makalede bir Red Hat Enterprise Linux (RHEL) 7 sanal makine bir Azure AD etki alanı Hizmetleri yönetilen etki alanına katılma kullanmayı gösterir.

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a>Red Hat Enterprise Linux sanal makine sağlama
Azure Portalı'nı kullanarak bir RHEL 7 sanal makine sağlamak için aşağıdaki adımları gerçekleştirin.

1. [Azure Portal](https://portal.azure.com) oturum açın.

    ![Azure portalı panosunun](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. Tıklatın **yeni** türü ve sol bölmede **Red Hat** aşağıdaki ekran görüntüsünde gösterildiği gibi arama çubuğunu içine. Red Hat Enterprise Linux girişleri arama sonuçlarında görünür. Tıklatın **Red Hat Enterprise Linux 7.2**.

    ![RHEL sonuçlarında seçin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. Arama sonuçlarının **her şeyi** bölmesinde Red Hat Enterprise Linux 7.2 görüntü listesinde. Tıklatın **Red Hat Enterprise Linux 7.2** sanal makine görüntüsüne hakkında daha fazla bilgi görüntülemek için.

    ![RHEL sonuçlarında seçin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. İçinde **Red Hat Enterprise Linux 7.2** bölmesinde, sanal makine görüntüsüne hakkında daha fazla bilgi görmeniz gerekir. İçinde **dağıtım modeli seçin** açılan listesinde, select **Klasik**. Ardından **oluşturma** düğmesi.

    ![Görüntü ayrıntıları görüntüle](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. İçinde **Temelleri** sayfasında **sanal makine oluşturma** Sihirbazı'nı girin **ana bilgisayar adı** yeni bir sanal makine için. Ayrıca bir yerel yönetici kullanıcı adı belirtin **kullanıcı adı** alan ve **parola**. Yerel yönetici kullanıcının kimliğini doğrulamak için bir SSH anahtarı kullanmayı seçebilirsiniz. Ayrıca bir **fiyatlandırma katmanı** sanal makine için.

    ![VM - temelleri sayfa oluşturma](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. İçinde **boyutu** sayfasında **sanal makine oluşturma** Sihirbazı, sanal makine boyutunu seçin.

    ![VM - select boyutu oluşturun](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. İçinde **ayarları** sayfasında **sanal makine oluşturma** depolama hesabı için sanal makine Sihirbazı'nı seçin. Tıklatın **sanal ağ** için Linux VM dağıtılmalıdır sanal ağ seçmelisiniz. İçinde **sanal ağ** sanal ağ hangi Azure AD Etki Alanı Hizmetleri'nde kullanılabilir dikey penceresinde, seçin. Bu örnekte 'MyPreviewVNet' sanal ağı seçin.

    ![VM oluşturma - sanal ağı seçin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. Üzerinde **Özet** sayfasında **sanal makine oluşturma** Sihirbazı, gözden geçirme ve tıklatın **Tamam** düğmesi.

    ![VM - seçilen sanal ağ oluşturma](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. RHEL 7.2 görüntüyü temel alarak yeni bir sanal makine dağıtımı başlamanız gerekir.

    ![VM - Dağıtım başladı oluşturma](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. Birkaç dakika sonra sanal makine başarıyla ve hazır kullanılmak üzere dağıtılmalıdır.

    ![Dağıtılan VM - oluşturma](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-to-the-newly-provisioned-linux-virtual-machine"></a>Uzaktan yeni sağlandı Linux sanal makineye bağlanma
RHEL 7.2 sanal makine Azure'da sağlandı. Sonraki görev sanal makineye uzaktan bağlamaktır.

**RHEL 7.2 sanal makineye bağlanma** makalesindeki yönergeleri izleyin [Linux çalıştıran bir sanal makine için oturum açma](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Geri kalan adımlara varsayalım RHEL sanal makineye bağlanmak için PuTTY SSH istemcisini kullanın. Daha fazla bilgi için bkz: [PuTTY indirme sayfası](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

1. PuTTY programını açın.
2. Girin **ana bilgisayar adı** yeni oluşturulan RHEL sanal makine için. Bu örnekte, sanal makine ana bilgisayar adı 'contoso-rhel.cloudapp .net' sahiptir. VM ana bilgisayar adından emin değilseniz, Azure Portal'daki VM panoya bakın.

    ![PuTTY Bağlan](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. Sanal makineye sanal makinenin oluşturulduğu belirtilen yerel yönetici kimlik bilgilerini kullanarak oturum açın. Bu örnekte, "mahesh" yerel yönetici hesabı kullanılır.

    ![PuTTY oturum açma](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-the-linux-virtual-machine"></a>Gerekli paketler Linux sanal makineye yükleme
Sanal makineye bağlandıktan sonra sonraki görev sanal makinede etki alanına katılma için gerekli paketleri yüklemek için uygundur. Aşağıdaki adımları gerçekleştirin:

1. **Realmd yükleyin:** realmd paketi etki alanına katılma için kullanılır. PuTTY terminalinizde aşağıdaki komutu yazın:

    sudo yum yükleme realmd

    ![Realmd yükleyin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    Birkaç dakika sonra realmd paket sanal makinede yüklü.

    ![yüklü realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. **Sssd yükleyin:** realmd paket etki alanı birleştirme işlemleri gerçekleştirme sssd bağlıdır. PuTTY terminalinizde aşağıdaki komutu yazın:

    sudo yum yükleme sssd

    ![Sssd yükleyin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    Birkaç dakika sonra sssd paket sanal makinede yüklü.

    ![yüklü realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. **Kerberos yükleyin:** PuTTY terminalinizde aşağıdaki komutu yazın:

    sudo yum yükleme krb5 iş istasyonu krb5-kitaplıklar

    ![Kerberos yükleyin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    Birkaç dakika sonra realmd paket sanal makinede yüklü.

    ![Kerberos yüklü](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-the-linux-virtual-machine-to-the-managed-domain"></a>Linux sanal makinesini yönetilen bir etki alanına katılma
Gerekli paketleri Linux sanal makinede yüklü olan, sonraki görev sanal makineyi yönetilen etki alanına belirlemektir.

1. AAD etki alanı Hizmetleri yönetilen etki bulur. PuTTY terminalinizde aşağıdaki komutu yazın:

    sudo bölge CONTOSO100.COM Bul

    ![Bölge Bul](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    Varsa **bölge Bul** , yönetilen etki alanını bulmak, etki alanı sanal makine (try ping) erişilebilir olduğundan emin olun alamıyor. Ayrıca sanal makinenin yönetilen etki alanı kullanılamıyor aynı sanal ağa gerçekten dağıtılmış olduğundan emin olun.
2. Kerberos başlatır. PuTTY terminalinizde aşağıdaki komutu yazın. 'AAD DC Yöneticiler' grubuna ait bir kullanıcı belirttiğinizden emin olun. Yalnızca bu kullanıcıların bilgisayarları yönetilen etki alanına katılmasını sağlayabilir.

    kinitbob@CONTOSO100.COM

    ![Kinit](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    Büyük harflerle etki alanı adı belirtin, başka kinit başarısız emin olun.
3. Makine etki alanına katılın. PuTTY terminalinizde aşağıdaki komutu yazın. Önceki adımda ('kinit') belirtilen aynı kullanıcı belirtin.

    sudo bölge birleştirme--ayrıntılı CONTOSO100.COM -U 'bob@CONTOSO100.COM'

    ![Bölge birleştirme](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

("Başarılı bir şekilde kaydedilen makine bölgedeki") bir ileti almalısınız zaman makine başarıyla katılırsa yönetilen etki.

## <a name="verify-domain-join"></a>Etki alanına katılma doğrulayın
Hızlı bir şekilde makineyi yönetilen bir etki alanına başarıyla katıldı olup olmadığını doğrulayın. Bağlanmak yeni RHEL kullanıcı hesabının doğru şekilde giderilip giderilmediğini görmek için SSH ve bir etki alanı kullanıcı hesabı ve ardından onay kullanarak VM etki alanına katıldı.

1. PuTTY terminalinizde bağlanmak için aşağıdaki komutu yazın yeni SSH kullanarak RHEL sanal makine etki alanına katıldı. Yönetilen etki alanına ait bir etki alanı hesabı kullanın (örneğin, 'bob@CONTOSO100.COM' Bu durumda.)

    SSH -l bob@CONTOSO100.COM contoso rhel.cloudapp.net
2. PuTTY terminalinizde giriş dizini doğru başlatılmadı görmek için aşağıdaki komutu yazın.

    pwd
3. PuTTY terminalinizde grup üyeliklerini doğru çözüldüğünü olmadığını görmek için aşağıdaki komutu yazın.

    id

Bu komutların örnek bir çıktı aşağıdaki gibidir:

![Etki alanına katılma doğrulayın](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a>Sorun giderme etki alanına katılma
Başvurmak [sorun giderme etki alanına katılma](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) makalesi.

## <a name="related-content"></a>İlgili İçerik
* [Azure AD etki alanı Hizmetleri - başlangıç kılavuzu](active-directory-ds-getting-started.md)
* [Bir Windows Server sanal makine bir Azure AD etki alanı Hizmetleri yönetilen etki alanına katılma](active-directory-ds-admin-guide-join-windows-vm.md)
* [Linux çalıştıran bir sanal makine için oturum açma](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* [Kerberos yükleme](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [Red Hat Enterprise Linux 7 - Windows tümleştirme Kılavuzu](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
