Azure sanal makineler için güncelleştirmeleri tooimprove hello güvenilirlik, performans ve güvenlik hello konak altyapısının düzenli olarak gerçekleştirir. Bu güncelleştirmeler aralığı hello barındırma ortamı (örneğin, işletim sistemi, hiper yönetici ve hello konakta dağıtılan çeşitli aracılar), yazılım bileşenleri düzeltme eki uygulama ağ bileşenleri yükseltme toohardware yetkisini alma. Bu güncelleştirmeler Hello çoğunluğu herhangi etkisi toohello barındırılan sanal makineler gerçekleştirilir. Ancak, güncelleştirmeler bir etkiye sahip olduğu durumlar vardır:

- Merhaba bakım yeniden başlatma gerektirmez, Azure hello konak güncelleştirilirken yerinde geçiş toopause hello VM kullanır.

- Bakım bir yeniden başlatma gerektirirse, planlı hello bakım bildiren bir duyuru alın. Bu durumlarda, ayrıca hello bakım kendiniz, uygun bir zaman başlayabileceğiniz bir zaman penceresi verilir.

Bu sayfa Microsoft Azure bakım her iki tür nasıl gerçekleştireceğini açıklar. Planlanmamış olaylar (kesintileri) hakkında daha fazla bilgi için sanal makinelerin kullanılabilirliğini yönetme hello [Windows] bakın (.. / articles/virtual-machines/windows/manage-availability.md) veya [Linux](../articles/virtual-machines/linux/manage-availability.md).

Bir sanal makinede çalışan uygulamalar için Azure meta veri hizmeti kullanarak gelecek güncelleştirmeleri hakkında bilgi toplama hello [Windows](../articles/virtual-machines/windows/instance-metadata-service.md) veya [Linux] (.. / articles/virtual-machines/linux/instance-metadata-service.md).

## <a name="in-place-vm-migration"></a>Yerinde VM geçiş

Güncelleştirmeleri tam bir yeniden başlatma gerektirmez, bir yerinde dinamik geçiş kullanılır. Merhaba güncelleştirme sırasında yaklaşık 30 RAM hello bellekte barındırma ortamı hello hello gerekli güncelleştirmeleri ve düzeltme eklerini uygularken koruma saniye, hello sanal makine duraklatıldı. Merhaba sanal makine sonra sürdürülür ve başlangıç saati hello sanal makinenin otomatik olarak eşitlenir.

Kullanılabilirlik kümelerinde VM'ler için güncelleştirilmiş birer birer güncelleştirme etki alanlarıdır. Bir güncelleştirme etki alanında (UD) tüm sanal makineleri duraklatıldı güncelleştirildi ve planlı bakım toohello üzerinde gitmeden önce sonra sürdürüldü sonraki UD.

Bazı uygulamalar, bu tür güncelleştirmeler tarafından etkilenebilir. Gerçek zamanlı Olay işleme, akış veya kod veya yüksek verimlilik senaryoları, ağ gibi gerçekleştiren uygulamaları tasarlanmış tootolerate 30 saniyelik duraklamalar olmayabilir. <!-- sooooo, what should they do? --> 


## <a name="maintenance-requiring-a-reboot"></a>Yeniden başlatma gerektiren bakım

Sanal makineleri planlı bakım için yeniden toobe gerektiğinde, önceden bildirilir. Planlı bakım iki aşaması vardır: Self Servis ve zamanlanmış bakım penceresinde hello.

Merhaba **Self Servis penceresi** hello bakım, sanal makineleri üzerinde başlatmak olanak tanır. Bu süre boyunca her VM toosee durumlarını sorgular ve Bakım isteğiniz hello sonucunu denetleyin.

Self Servis bakım başlattığınızda, VM zaten güncelleştirildi ve geri çalıştırır taşınan tooa düğümdür. Merhaba VM yeniden çünkü hello geçici disk kaybolur ve sanal ağ arabirimiyle ilişkilendirilmiş dinamik IP adreslerini güncelleştirilir.

Self Servis bakımını Başlat ve hello işlemi sırasında bir hata varsa hello işlemi durdurulursa, VM güncelleştirilmez hello ve ayrıca kaldırılır hello planlı bakım yinelemeden diğerine. Daha sonra yeni bir zamanlama ile temas ve olması yeni fırsat toodo bakım Self Servis sunulan. 

Merhaba Self Servis penceresi geçtiğinde hello **zamanlanmış bakım penceresi** başlar. Bu zaman penceresi sırasında hala hello bakım penceresi için sorgu, ancak artık mümkün toostart hello bakım kendiniz olabilir.

## <a name="availability-considerations-during-planned-maintenance"></a>Planlı bakım sırasında kullanılabilirlik konuları 

Bakım penceresi Hello planlanan kadar toowait karar verirseniz, VM'lerin hello yüksek availabilty korumak için birkaç şey tooconsider vardır. 

### <a name="paired-regions"></a>Eşleştirilmiş bölgeleri

Her Azure bölgesi hello içinde başka bir bölge ile eşleştirilmiş aynı coğrafi bölge, bölgesel çifti yaptıkları birlikte. Planlı bakım sırasında Azure yalnızca hello bölge çiftinin tek bir bölgedeki sanal makineleri güncelleştirir. Örneğin, hello Kuzey Orta ABD sanal makinelerinizde güncelleştirirken Azure tüm sanal makineler Orta Güney ABD hello güncelleştirmez aynı anda. Kuzey Avrupa bakım altında gibi ancak, diğer bölgeleriyle aynı hello Doğu ABD olarak zaman. Bölge çiftleri nasıl yardımcı olabilecek anlama bölgeler arasında daha iyi Vm'leriniz dağıtın. Daha fazla bilgi için bkz: [Azure bölgesi çiftleri](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

### <a name="availability-sets-and-scale-sets"></a>Kullanılabilirlik kümeleri ve ölçek kümeleri

Bir iş yükü Azure vm'lerinde dağıtırken, bir kullanılabilirlik kümesi tooprovide yüksek kullanılabilirlik tooyour uygulamadaki hello VM'ler oluşturabilirsiniz. Bu bir kesinti veya bakım olayları sırasında en az bir sanal makinenin kullanılabilir olmasını sağlar.

Bir kullanılabilirlik kümesi içinde tek tek sanal makineleri too20 güncelleştirme etki alanları (UDs) arasında yayılır. Planlı bakım sırasında herhangi bir anda yalnızca bir tek güncelleştirme etki alanı etkilenmez. Güncelleme etki alanına etkilenip Hello sırasını mutlaka sıralı olarak gerçekleşmez olduğunu unutmayın. 

Sanal makine ölçek kümesi sağlayan bir Azure işlem toodeploy kaynaktır ve aynı sanal makineleri bir küme tek bir kaynak olarak yönetebilirsiniz. Merhaba ölçek kümesi, bir kullanılabilirlik kümesindeki sanal makineleri gibi güncelleştirme etki alanları arasında otomatik olarak dağıtılır. Gibi kullanılabilirlik kümeleri ile ölçek kümeleri ile yalnızca bir tek güncelleştirme etki alanı herhangi bir zamanda etkilenmez.

Sanal makinelerinizin yüksek kullanılabilirlik için yapılandırma hakkında daha fazla bilgi için Windows için sanal makinelerin kullanılabilirliğini yönetme hello bakın (.. / articles/virtual-machines/windows/manage-availability.md) veya [Linux](../articles/virtual-machines/linux/manage-availability.md).
