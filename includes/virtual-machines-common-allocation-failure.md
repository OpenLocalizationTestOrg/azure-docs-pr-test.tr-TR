
Bu makalede Azure sorunu ele alınmamışsa hello ziyaret [MSDN ve yığın taşması Azure forumları](https://azure.microsoft.com/support/forums/). Bu forumlar sorununuzu nakledebilirsiniz veya too@AzureSupport Twitter'da. Ayrıca, size bir Azure destek isteği seçerek dosya **alma desteği** hello üzerinde [Azure Destek](https://azure.microsoft.com/support/options/) site.

## <a name="general-troubleshooting-steps"></a>Genel sorun giderme adımları
### <a name="troubleshoot-common-allocation-failures-in-hello-classic-deployment-model"></a>Merhaba Klasik dağıtım modelinde ortak ayırma hatalarını giderme
Bu adımlar, sanal makinelerde birçok ayırma hatalarını gidermek yardımcı olabilir:

* Merhaba VM tooa farklı bir VM boyutu yeniden boyutlandırın.<br>
    Tıklatın **tümüne Gözat** > **sanal makineleri (Klasik)** > sanal makineniz > **ayarları** > **boyutu**. Ayrıntılı adımlar için bkz: [hello sanal makine yeniden boyutlandırma](https://msdn.microsoft.com/library/dn168976.aspx).
* Merhaba bulut hizmetinden tüm sanal makineleri silin ve sanal makineleri yeniden oluşturun.<br>
    Tıklatın **tümüne Gözat** > **sanal makineleri (Klasik)** > sanal makineniz > **silmek**. Ardından **yeni** > **işlem** > [sanal makine görüntüsü].

### <a name="troubleshoot-common-allocation-failures-in-hello-azure-resource-manager-deployment-model"></a>Hello Azure Resource Manager dağıtım modelinde ortak ayırma hatalarını giderme
Bu adımlar, sanal makinelerde birçok ayırma hatalarını gidermek yardımcı olabilir:

* Durdur (deallocate) tüm sanal makineleri aynı kullanılabilirlik ayarlayın ve ardından her biri yeniden hello içinde.<br>
    toostop: tıklatın **kaynak grupları** > kaynak grubunuz > **kaynakları** > kullanılabilirlik kümesi > **sanal makineleri** > sanal makineniz >  **Durdur**.
  
    Tüm sanal makineleri durdurduktan sonra Seç hello ilk VM tıklatıp **Başlat**.

## <a name="background-information"></a>Arka plan bilgileri
### <a name="how-allocation-works"></a>Ayırma nasıl çalışır?
Azure veri merkezlerinde Hello sunucuları kümeler halinde bölümlenir. Normalde, bir ayırma isteği birden çok kümelerde çalıştı, ancak bazı kısıtlamalar hello ayırma istek hello Azure platformu tooattempt hello isteği yalnızca tek bir küme zorla mümkündür. Bu makalede, biz toothis "sabitlenmiş tooa küme olarak." başvurmak Aşağıda 1 diyagram birden çok kümelerde denenir normal bir ayırma hello durumunu gösterir. Diyagram 2 bir ayırma hello durumunun gösterir, bulut hizmeti CS_1 veya kullanılabilirlik kümesi varolan hello barındırıldığı olduğu için tooCluster 2 sabitlenmiş.
![Ayırma diyagramı](./media/virtual-machines-common-allocation-failure/Allocation1.png)

### <a name="why-allocation-failures-happen"></a>Ayırma hatalarının neden olması
Ayırma isteği sabitlenmiş tooa küme olduğunda hello kullanılabilir kaynak havuzu daha küçük olduğundan toofind boş kaynak başarısız bir yüksek ihtimalini yoktur. Merhaba küme kaynakları serbest bırakmak olsa bile, ayrıca, ayırma isteği sabitlenmiş tooa küme olmakla birlikte, istenen kaynak hello türü, küme tarafından desteklenmiyor, isteğiniz başarısız olur. Aşağıdaki diyagram 3 hello çalışması hello yalnızca adayı küme kaynakları serbest bırakmak olmadığından burada Sabitlenmiş ayırma başarısız gösterir. Diyagram 4 gösterir; burada Sabitlenmiş ayırma başarısız hello yalnızca adayı küme desteklemediğinden hello çalışması hello küme kaynakları serbest bırakmak olmasına rağmen hello istenen VM boyutu.

![Sabitlenmiş ayırma hatası](./media/virtual-machines-common-allocation-failure/Allocation2.png)

## <a name="detailed-troubleshoot-steps-specific-allocation-failure-scenarios-in-hello-classic-deployment-model"></a>Ayrıntılı adımları belirli ayırma hatası senaryoları hello Klasik dağıtım modelinde sorun giderme
Sabitlenmiş bir ayırma isteği toobe neden ortak ayırma senaryolar verilmiştir. Her senaryo bu makalenin sonraki bölümlerinde içine dalın.

* Bir VM'yi yeniden boyutlandırın veya sanal makineleri veya rol örneklerini tooan mevcut bulut hizmeti ekleyin
* Kısmen durduruldu (serbest bırakıldığında) sanal makineleri yeniden başlatın
* Tam olarak durduruldu (serbest bırakıldığında) sanal makineleri yeniden başlatın
* Hazırlama/üretim dağıtımları (yalnızca bir hizmet olarak platform)
* Benzeşim grubu (VM/hizmet yakınlık)
* Benzeşim grubu tabanlı sanal ağ

Ayırma hatası aldığınızda, açıklanan hello senaryoların herhangi biri tooyour hata geçerli değilse bakın. Hello Azure platformu tooidentify hello karşılık gelen senaryo tarafından döndürülen hello ayırma hatası kullanın. İsteğiniz sabitlenmiş, böylece hello fırsat ayırma başarı artırma isteği toomore kümeleriniz hello sabitleme kısıtlamaları tooopen bazılarını kaldırın.

"Hello istenen VM boyutu desteklenmiyor" Merhaba hata bildirmediği sürece, yeterli kaynağa atanmış olması gibi genel olarak, her zaman daha sonraki bir zamanda yeniden deneyebilirsiniz. isteğinizi hello küme tooaccommodate serbest. VM boyutu desteklenmiyor, hello istenen Hello sorunudur, farklı bir VM boyutu deneyin. Aksi takdirde hello tek kısıtlaması sabitleme tooremove hello seçenektir.

İki ortak hatası senaryoları ilgili tooaffinity gruplarıdır. Hello geçmiş, kullanılan tooprovide yakınında tooVMs/hizmet örneklerinin bir benzeşim grubu olan veya sanal ağ kullanılan tooenable hello oluşturma oldu. Bölgesel sanal ağlar Hello başlanmasıyla, benzeşim grupları artık gerekli toocreate bir sanal ağ değildir. İle Merhaba azaltma Azure altyapı, ağ gecikme hello öneri toouse benzeşim grupları için VM/hizmet yakınlık değişti.

Diyagram 5 aşağıdaki hello sınıflandırma (sabitlenmiş) hello ayırma senaryolar sunar.
![Sabitlenmiş ayırma sınıflandırma](./media/virtual-machines-common-allocation-failure/Allocation3.png)

> [!NOTE]
> Her bir ayırma senaryo listelenen hello hata kısa bir biçimidir. Toohello başvuran [hata dizesi arama](#Error string lookup) ayrıntılı hata dizeleri.
> 
> 

## <a name="allocation-scenario-resize-a-vm-or-add-vms-or-role-instances-tooan-existing-cloud-service"></a>Ayırma senaryo: bir VM'yi yeniden boyutlandırın veya sanal makineleri veya rol örnekleri tooan mevcut bulut hizmeti ekleyin
**Hata**

Upgrade_VMSizeNotSupported veya GeneralError

**Küme sabitleme nedeni**

A tooresize VM istek veya VM eklemek veya bir rol örneği tooan mevcut bulut hizmeti toobe hello olan bir bulut hizmetini barındıran hello özgün kümesine çalıştı. Yeni bir bulut hizmeti oluşturma hello Azure platformu toofind kaynakları serbest bırakmak veya istediğiniz hello VM boyutu destekleyen başka bir küme sağlar.

**Geçici çözüm**

Merhaba hata Upgrade_VMSizeNotSupported * varsa, farklı bir VM boyutu deneyin. Farklı bir VM boyutu kullanarak bir seçenek değildir, ancak kabul edilebilir toouse farklı bir sanal IP adresi (VIP) ise oluşturun, yeni bir bulut hizmeti toohost yeni VM hello ve burada hello var olan sanal makineleri çalıştıran hello yeni bulut hizmeti toohello bölgesel sanal ağ ekleyin. Mevcut bulut hizmetiniz bölgesel bir sanal ağ kullanmıyorsa hala hello yeni bulut hizmeti için yeni bir sanal ağ oluşturduğunuzda ve ardından bağlanmak, [var olan sanal ağ toohello yeni bir sanal ağ](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Daha fazla gördükleri hakkında [bölgesel sanal ağlar](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

Merhaba hata GeneralError * ise, kaynak (örneğin, belirli bir VM boyutu) hello türü hello küme tarafından desteklenir, ancak hello küme kaynakları serbest bırakmak hello şu anda yok olasıdır. Senaryo, yukarıda benzer toohello yeni bir bulut hizmeti (Merhaba yeni bulut hizmeti farklı bir VIP toouse sahip olduğuna dikkat edin) oluşturma aracılığıyla hello istenen işlem kaynak ekleyin ve bir bölgesel sanal ağ tooconnect bulut hizmetlerinizi kullanın.

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>Ayırma senaryo: yeniden başlatma kısmen durduruldu (serbest bırakıldığında) VM'ler
**Hata**

GeneralError *

**Küme sabitleme nedeni**

Kısmi ayırmayı kaldırma (serbest bırakıldığında) bir veya daha fazlasını ancak değil tüm VM'lerin bir bulut hizmetinde durduruldu anlamına gelir. Zaman durdurup (serbest bırakma) hello ilişkili bir VM kaynakları yayınladı. Bu durduruldu (serbest bırakıldığında) VM'yi yeniden başlatırken bu nedenle yeni ayırma isteğidir. Sanal makineleri yeniden başlatmayı kısmen deallocated bulut hizmetinde eşdeğer tooadding VM'ler tooan mevcut bulut hizmeti olur. Merhaba ayırma isteği hello olan bir bulut hizmetini barındıran hello özgün kümesine çalıştı toobe sahiptir. Farklı bir bulut hizmeti oluşturmak istediğiniz hello VM boyutu destekler veya ücretsiz kaynağa sahip başka bir küme hello Azure platformu toofind sağlar.

**Geçici çözüm**

Kabul edilebilir ise toouse delete hello farklı bir VIP durduruldu (serbest bırakıldığında) VM'ler (ancak Koru ilişkili hello diskleri) ve hello sanal makineleri farklı bir bulut hizmeti aracılığıyla geri ekleyin. Bölgesel sanal ağ tooconnect bulut hizmetlerinizi kullanın:

* Mevcut bulut hizmetiniz bölgesel bir sanal ağ kullanıyorsa, hello yeni bulut hizmeti toohello eklemeniz yeterlidir aynı sanal ağ.
* Mevcut bulut hizmetiniz bölgesel bir sanal ağ kullanmıyorsa hello yeni bulut hizmeti için yeni bir sanal ağ oluşturun ve ardından [var olan sanal ağ toohello yeni sanal ağınıza bağlamak](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Daha fazla gördükleri hakkında [bölgesel sanal ağlar](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

## <a name="allocation-scenario-restart-fully-stopped-deallocated-vms"></a>Ayırma senaryo: yeniden başlatma tam olarak durduruldu (serbest bırakıldığında) VM'ler
**Hata**

GeneralError *

**Küme sabitleme nedeni**

Durduruldu tam ayırmayı kaldırma anlamına gelir (tüm sanal makineler bir bulut hizmetinden serbest). Merhaba ayırma hello bulut hizmeti barındıran hello özgün kümesine çalıştı toobe bu VM'ye sahip toorestart ister. Yeni bir bulut hizmeti oluşturma hello Azure platformu toofind kaynakları serbest bırakmak veya istediğiniz hello VM boyutu destekleyen başka bir küme sağlar.

**Geçici çözüm**

Kabul edilebilir toouse farklı bir VIP ise, delete hello özgün durduruldu (serbest bırakıldığında) VM'ler (ancak Koru ilişkili hello diskleri) ve hello karşılık gelen bulut hizmetini ((serbest bırakıldığında) durduğunda kaynakları zaten yayımlanan ilişkili hello işlem silin Merhaba VM'ler için). Yeni bir bulut hizmeti tooadd hello VM'ler yeniden oluşturun.

## <a name="allocation-scenario-stagingproduction-deployments-platform-as-a-service-only"></a>Ayırma senaryo: hazırlama/üretim dağıtımları (yalnızca bir hizmet olarak platform)
**Hata**

New_General * veya New_VMSizeNotSupported *

**Küme sabitleme nedeni**

Hazırlama dağıtımı ve bir bulut hizmeti hello Üretim dağıtımı hello hello barındırılan aynı küme. Merhaba ikinci dağıtımı eklediğinizde, hello karşılık gelen ayırma isteği barındıran aynı küme hello ilk dağıtım hello denenir.

**Geçici çözüm**

Merhaba ilk dağıtım ve hello özgün bulut hizmetini silin ve hello bulut hizmeti yeniden dağıtın. Bu eylem, her iki dağıtım yeterli kaynakları serbest bırakmak toofit sahip bir küme veya istediğiniz hello VM boyutları destekleyen bir küme hello ilk dağıtım güden.

## <a name="allocation-scenario-affinity-group-vmservice-proximity"></a>Ayırma senaryo: benzeşim grubu (VM/hizmet yakınlık)
**Hata**

New_General * veya New_VMSizeNotSupported *

**Küme sabitleme nedeni**

Atanan tooan benzeşim grubunun herhangi bir işlem kaynağı tooone küme bağlıdır. Yeni işlem kaynak istekleri benzeşim grubundaki aynı hello mevcut kaynakları barındırıldığı küme hello denenir. Merhaba yeni kaynaklar var olan bir bulut hizmetini veya yeni bir bulut hizmeti aracılığıyla oluşturulan bu geçerlidir.

**Geçici çözüm**

Bir benzeşim grubu gerekli değilse, olmayan bir benzeşim grubu kullanın veya işlem kaynaklarınızı birden çok benzeşim gruplar halinde gruplandırabilirsiniz.

## <a name="allocation-scenario-affinity-group-based-virtual-network"></a>Ayırma senaryo: benzeşim grubuna bağlı sanal ağ
**Hata**

New_General * veya New_VMSizeNotSupported *

**Küme sabitleme nedeni**

Bölgesel sanal ağlar sunulmadan önce gerekli tooassociate benzeşim grubu ile bir sanal ağ yoktu. Sonuç olarak, bir benzeşim grubu yerleştirilen işlem kaynakları bağlı olan hello açıklandığı gibi hello aynı kısıtlamaları "ayırma senaryo: benzeşim grubu (VM/hizmet yakınlık)" Yukarıdaki bölümde. Merhaba işlem kaynakları bağlı tooone kümelerdir.

**Geçici çözüm**

Bir benzeşim grubu gerekmiyorsa ekleyeceğiniz, yeni kaynaklar hello için yeni bir bölgesel sanal ağ oluşturun ve ardından [var olan sanal ağ toohello yeni sanal ağınıza bağlamak](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Daha fazla gördükleri hakkında [bölgesel sanal ağlar](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

Alternatif olarak, [benzeşim grubuna bağlı sanal ağ tooa bölgesel sanal ağınızı geçirmek](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/)ve ardından istenen hello kaynakları yeniden ekleyin.

## <a name="detailed-troubleshooting-steps-specific-allocation-failure-scenarios-in-hello-azure-resource-manager-deployment-model"></a>Ayrıntılı adımları belirli ayırma hatası senaryoları hello Azure Resource Manager dağıtım modelinde sorun giderme
Sabitlenmiş bir ayırma isteği toobe neden ortak ayırma senaryolar verilmiştir. Her senaryo bu makalenin sonraki bölümlerinde içine dalın.

* Bir VM'yi yeniden boyutlandırın veya sanal makineleri veya rol örneklerini tooan mevcut bulut hizmeti ekleyin
* Kısmen durduruldu (serbest bırakıldığında) sanal makineleri yeniden başlatın
* Tam olarak durduruldu (serbest bırakıldığında) sanal makineleri yeniden başlatın

Ayırma hatası aldığınızda, açıklanan hello senaryoların herhangi biri tooyour hata geçerli değilse bakın. Hello Azure platformu tooidentify hello karşılık gelen senaryo tarafından döndürülen hello ayırma hatası kullanın. İsteğiniz sabitlenmiş tooan var olan küme ise, böylece hello fırsat ayırma başarı artırma isteği toomore kümeleriniz hello sabitleme kısıtlamaları tooopen bazılarını kaldırın.

"Hello istenen VM boyutu desteklenmiyor" Merhaba hata bildirmediği sürece, yeterli kaynağa atanmış olması gibi genel olarak, her zaman daha sonraki bir zamanda yeniden deneyebilirsiniz. isteğinizi hello küme tooaccommodate serbest. Aşağıda bu hello VM boyutu desteklenmiyor istenen Hello sorunun olup olmadığını için geçici çözümler konusuna bakın.

## <a name="allocation-scenario-resize-a-vm-or-add-vms-tooan-existing-availability-set"></a>Ayırma senaryo: bir VM'yi yeniden boyutlandırın veya VM'ler tooan varolan kullanılabilirlik kümesi ekleyin
**Hata**

Upgrade_VMSizeNotSupported * veya GeneralError *

**Küme sabitleme nedeni**

A tooresize VM istek veya kullanılabilirlik kümesi var olan bir VM tooan sahip hello varolan kullanılabilirlik kümesi barındıran hello özgün kümesine çalıştı toobe ekleyin. Yeni bir kullanılabilirlik kümesi oluşturmak istediğiniz hello VM boyutu destekler veya kaynakları serbest bırakmak sahip başka bir küme hello Azure platformu toofind sağlar.

**Geçici çözüm**

Merhaba hata Upgrade_VMSizeNotSupported * varsa, farklı bir VM boyutu deneyin. Farklı bir VM boyutu kullanarak bir seçenek değilse, tüm VM'ler hello kullanılabilirlik kümesindeki durdurun. İstenen VM boyutu değişiklik hello boyut hello destekleyen hello VM tooa küme ayırır hello sanal makinenin sonra kullanabilirsiniz.

Merhaba hata GeneralError * ise, kaynak (örneğin, belirli bir VM boyutu) hello türü hello küme tarafından desteklenir, ancak hello küme kaynakları serbest bırakmak hello şu anda yok olasıdır. Merhaba VM farklı bir kullanılabilirlik kümesinin bir parçası olabilir, farklı bir kullanılabilirlik kümesinde yeni bir VM oluşturun (Merhaba içinde aynı bölge). Bu yeni VM toohello sonra eklenebilir aynı sanal ağ.  

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>Ayırma senaryo: yeniden başlatma kısmen durduruldu (serbest bırakıldığında) VM'ler
**Hata**

GeneralError *

**Küme sabitleme nedeni**

Kısmi ayırmayı kaldırma (serbest bırakıldığında) bir veya daha fazla durduruldu ancak tümü, sanal makineleri bir kullanılabilirlik kümesi anlamına gelir. Zaman durdurup (serbest bırakma) hello ilişkili bir VM kaynakları yayınladı. Bu durduruldu (serbest bırakıldığında) VM'yi yeniden başlatırken bu nedenle yeni ayırma isteğidir. Kısmen deallocated kullanılabilirlik kümesindeki sanal makineleri yeniden başlatmayı eşdeğer tooadding VM'ler tooan varolan kullanılabilirlik ayarlanır. Merhaba ayırma isteği hello varolan kullanılabilirlik kümesi barındıran hello özgün kümesine çalıştı toobe sahiptir.

**Geçici çözüm**

Tüm sanal makineleri yeniden başlatmayı hello önce ilk hello kullanılabilirlik durdurun. Bu yeni bir ayırma girişimi çalıştırılır ve yeni bir küme kullanılabilir kapasiteye sahip seçilebilir emin olun.

## <a name="allocation-scenario-restart-fully-stopped-deallocated"></a>Ayırma senaryo: yeniden başlatma tam olarak durduruldu (serbest bırakıldığında)
**Hata**

GeneralError *

**Küme sabitleme nedeni**

Durduruldu tam ayırmayı kaldırma anlamına gelir (tüm sanal makineleri bir kullanılabilirlik kümesinde serbest). Bu sanal makineleri destekleyen tüm kümeleri hedeflediğini toorestart hello istenen boyuta hello ayırma isteği.

**Geçici çözüm**

Yeni bir VM boyutu tooallocate seçin. Bu işe yaramazsa, lütfen daha sonra yeniden deneyin.

## <a name="error-string-lookup"></a>Hata dizesi arama
**New_VMSizeNotSupported***

"hello VM boyutu (veya VM boyutları birleşimi) bu dağıtımın gerektirdiği toodeployment isteği kısıtlamaları sağlanamıyor. Mümkünse, tooa barındırılan hizmet başka bir dağıtım, sanal ağ bağlamaları gibi kısıtlamaları gevşetme deneyin ve tooa farklı benzeşim grubu ya da hiçbir benzeşim grubu veya deneyin ile dağıtma tooa farklı bir bölgeye. "

**New_General***

"Ayırma başarısız oldu; istekte oluşturulamıyor toosatisfy kısıtlamaları. Hello istenen yeni hizmet dağıtımı ilişkili tooan benzeşim grubu veya bir sanal ağ hedefler, veya var. Bu barındırılan hizmet altında varolan bir dağıtım. Bu koşulların herhangi biri kısıtlar hello yeni dağıtım toospecific Azure kaynakları. Lütfen daha sonra yeniden deneyin veya hello VM boyutu veya rol örneklerinin sayısını azaltmayı deneyin. Alternatif olarak, mümkünse, hello daha önce bahsedilen kısıtlamaları kaldırın veya tooa farklı bir bölgeye dağıtmayı deneyin."

**Upgrade_VMSizeNotSupported***

"Oluşturulamıyor tooupgrade hello dağıtımı. VM boyutu XXX hello mevcut dağıtımı destekleyen hello kaynaklarında kullanılamayabilir Hello istedi. Lütfen daha sonra yeniden deneyin, farklı bir VM boyutu veya daha az sayıda rol örneği ile deneyin veya yeni bir benzeşim grubu ya da benzeşim grubu bağlaması olmadan boş bir barındırılan hizmet altında dağıtım oluşturun."

**GeneralError***

"hello sunucu bir iç hatayla karşılaştı. Lütfen hello isteği yeniden deneyin." Veya "Başarısız tooproduce hello hizmeti için bir ayırma."

