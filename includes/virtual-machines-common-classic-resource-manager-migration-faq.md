# <a name="frequently-asked-questions-about-classic-tooazure-resource-manager-migration"></a>Klasik tooAzure Kaynak Yöneticisi geçişini hakkında sık sorulan sorular

## <a name="does-this-migration-plan-affect-any-of-my-existing-services-or-applications-that-run-on-azure-virtual-machines"></a>Bu geçiş planı Azure sanal makinelerde çalışan mevcut hizmetlerimi ya da uygulamaların herhangi birini etkiliyor mu? 

Hayır. Merhaba VM'ler (Klasik), genel kullanılabilirlik tam olarak desteklenen hizmetleridir. Bu kaynaklar tooexpand toouse devam edebilmeniz için Microsoft Azure ayak.

## <a name="what-happens-toomy-vms-if-i-dont-plan-on-migrating-in-hello-near-future"></a>Yakın zaman hello geçiş planı yok toomy VM'ler ne olur? 

Biz hello varolan Klasik API'ler ve kaynak modeli onaysız kılınmadan değil. Toomake geçiş hello Resource Manager dağıtım modelinde kullanılabilen özellikleri Gelişmiş hello göz önünde bulundurularak kolay istiyoruz. Gözden geçirmenizi öneririz [hello geliştirmeleri bazıları](../articles/azure-resource-manager/resource-manager-deployment-model.md) Iaas Resource Manager altında bir parçası.

## <a name="what-does-this-migration-plan-mean-for-my-existing-tooling"></a>Bu geçiş planı, mevcut araçlarım için ne anlama geliyor? 

Araç toohello Resource Manager dağıtım modeli güncelleştirmek için tooaccount geçiş planlarınızı sahip hello en önemli değişikliklerden biri kullanılır.

## <a name="how-long-will-hello-management-plane-downtime-be"></a>Merhaba Yönetim düzeyi kapalı kalma süresini ne kadar olacak? 

Geçirilmekte olan kaynaklar hello sayısına bağlıdır. (VM'ler birkaç onlarca) daha küçük dağıtımlar için bir saatten az hello tüm geçiş almanız gerekir. (VM'ler yüzlerce) büyük ölçekli dağıtımlar için hello geçiş birkaç saat sürebilir.

## <a name="can-i-roll-back-after-my-migrating-resources-are-committed-in-resource-manager"></a>Geçiş kaynaklarım Kaynak Yöneticisi'ne işlendikten sonra işlemi geri alabilir miyim? 

Hello kaynakları hello durumu hazır olduğunuz sürece geçişinizi iptal edebilirsiniz. Merhaba kaynakları başarılı bir şekilde hello kaydetme işlemi geçirildikten sonra geri alma desteklenmiyor.

## <a name="can-i-roll-back-my-migration-if-hello-commit-operation-fails"></a>Merhaba kaydetme işlemi başarısız olursa ı my geçişi geri alma? 

Merhaba kaydetme işlemi başarısız olursa geçiş iptal edilemiyor. Merhaba kaydetme işlemi de dahil olmak üzere tüm geçiş işlemlerini ıdempotent ' dir. Bu nedenle hello işlemi kısa bir süre sonra yeniden deneyin öneririz. Hala hata yüz, destek bileti oluşturun veya bir forum gönderisi hello ClassicIaaSMigration etiketi oluşturmak bizim [VM Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows).

## <a name="do-i-have-toobuy-another-express-route-circuit-if-i-have-toouse-iaas-under-resource-manager"></a>Toouse Iaas altında Resource Manager varsa ı başka bir hızlı rota devresi toobuy var mı? 

Hayır. En son etkin [hello Klasik toohello Resource Manager dağıtım modelinden ExpressRoute bağlantı hatları taşıma](../articles/expressroute/expressroute-move.md). Zaten varsa yeni bir expressroute bağlantı hattı toobuy yok.

## <a name="what-if-i-had-configured-role-based-access-control-policies-for-my-classic-iaas-resources"></a>Klasik Iaas Kaynaklarım için Rol Tabanlı Erişim Denetimi yapılandırdıysam ne olur? 

Geçiş sırasında hello kaynaklara Klasik tooResource Yöneticisi dönüştürün. Bu nedenle geçişten sonra toohappen gerektiren hello RBAC İlkesi güncelleştirmeler planlamanızı öneririz.

## <a name="i-backed-up-my-classic-vms-in-a-backup-vault-can-i-migrate-my-vms-from-classic-mode-tooresource-manager-mode-and-protect-them-in-a-recovery-services-vault"></a>Klasik VM’lerimi bir Backup kasasına yedekledim. Miyim Vm'lerimin Klasik modda tooResource Yöneticisi modundan geçirmek ve bir kurtarma Hizmetleri kasasına koruyun? 

Klasik tooResource Yöneticisi modu hello VM taşıdığınızda bir yedekleme kasası Klasik VM kurtarma noktalarını otomatik olarak tooa kurtarma Hizmetleri kasası geçirme. Bu adımları tootransfer VM Yedeklemelerinizin izleyin:

1. Toohello Hello yedekleme kasasına gidin **korunan öğeler** sekmesinde ve hello VM seçin. [Korumayı Durdur](../articles/backup/backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines)’a tıklayın. *İlişkili yedekleme verilerini sil* seçeneğini **işaretlenmemiş** olarak bırakın.
2. Merhaba yedekleme/anlık görüntü uzantısını VM hello silin.
3. Klasik mod tooResource Yöneticisi modundan Hello sanal makineyi geçirin. Karşılık gelen toohello sanal makine de hello depolama ve ağ bilgileri tooResource Yöneticisi modu geçirilen emin olun.
4. Kurtarma Hizmetleri kasası oluşturma ve yapılandırma hello üzerinde Yedekleme kullanarak sanal makine geçişi **yedekleme** kasa Panosu üzerinde eylem. Bir VM tooa kurtarma hizmetlerini yedekleme hakkında ayrıntılı bilgi için kasa, hello makalesine bakın [korumak Azure Vm'leri bir kurtarma Hizmetleri kasası ile](../articles/backup/backup-azure-vms-first-look-arm.md).

## <a name="can-i-validate-my-subscription-or-resources-toosee-if-theyre-capable-of-migration"></a>Geçiş özellikli ı my abonelik veya kaynak toosee doğrulayabilir? 

Evet. Merhaba platform desteklenen geçiş, geçiş için hazırlama hello ilk adımı hello kaynakları geçişini özellikli toovalidate seçenektir. Merhaba doğrulamak durumunda işlemi başarısız olursa, hello geçiş tamamlanamıyor tüm hello nedenlerle iletilerini alır.

## <a name="what-happens-if-i-run-into-a-quota-error-while-preparing-hello-iaas-resources-for-migration"></a>I hello Iaas kaynakları taşıma işlemine hazırlanırken bir kota hata çalıştırırsanız ne olur? 

Geçiş işleminizi iptal etmek ve ardından bir destek isteği tooincrease hello kotaları geçirme hello VM'ler nerede hello bölgede oturum öneririz. Merhaba kota istek onaylandıktan sonra hello geçiş adımları yeniden yürütme başlatabilirsiniz.

## <a name="how-do-i-report-an-issue"></a>Bir sorunu nasıl bildirebilirim? 

Sorunlar ve geçiş tooour hakkında sorular sonrası [VM Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows), hello anahtar sözcüğüyle ClassicIaaSMigration. Tüm sorularınızı bu foruma göndermenizi öneririz. Bir destek sözleşmesi varsa, Hoş Geldiniz toolog de bir destek bileti demektir.

## <a name="what-if-i-dont-like-hello-names-of-hello-resources-that-hello-platform-chose-during-migration"></a>Ne platform hello hello kaynakların hello adları istemeyiz, geçiş sırasında seçtiğiniz? 

Merhaba Klasik dağıtım modeli için adlarında açıkça sağladığınız tüm hello kaynaklar geçiş sırasında korunur. Bazı durumlarda yeni kaynaklar oluşturulur. Örneğin tüm VM’ler için ağ arabirimleri oluşturulur. Geçiş sırasında oluşturulan bu yeni kaynakların hello özelliği toocontrol hello adları şu anda desteklemiyoruz. Bu özellik için oyları hello üzerinde oturum [Azure geri bildirim Forumunda](http://feedback.azure.com).

## <a name="can-i-migrate-expressroute-circuits-used-across-subscriptions-with-authorization-links"></a>Yetkilendirme bağlantıları olan aboneliklerde kullanılan ExpressRoute devrelerini geçirebilir miyim? 

Çapraz abonelik yetkilendirme bağlantılar kullanan ExpressRoute devreleri kapalı kalma süresi olmadan otomatik olarak geçirilemez. Bunları elle nasıl geçirebileceğiniz hakkında yönergelerimiz vardır. Bkz: [geçirmek ExpressRoute bağlantı hattına ve hello Klasik toohello Resource Manager dağıtım modeli sanal ağlardan ilişkili](../articles/expressroute/expressroute-migration-classic-resource-manager.md) adımlar ve daha fazla bilgi için.

## <a name="i-got-a-message-vm-is-reporting-hello-overall-agent-status-as-not-ready-hence-hello-vm-cannot-be-migrated-ensure-that-hello-vm-agent-is-reporting-overall-agent-status-as-ready-or-vm-contains-extension-whose-status-is-not-being-reported-from-hello-vm-hence-this-vm-cannot-be-migrated-"></a>Bir ileti alındı *"VM hello raporlama genel aracı durumu olarak hazır değil. Bu nedenle, hello VM geçirilemez. Bu hello VM Aracısı hazır olarak genel aracı durumu raporlama olun"* veya *"VM uzantısı durumu bildirilmedi VM hello içerir. Bu nedenle bu VM geçirilemez.” *

Merhaba VM giden bağlantı toohello olmadığında bu ileti alındığında Internet. Merhaba VM Aracısı her beş dakikada hello aracı durumunu güncelleştirmek için giden bağlantı tooreach hello Azure depolama hesabı kullanır.
