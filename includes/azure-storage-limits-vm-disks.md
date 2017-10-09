Bir Azure sanal makinesi birkaç veri diskini eklemeyi destekler. En iyi performans için yüksek oranda kullanılan disk toolimit hello sayısı toohello sanal makine tooavoid olası azaltma bağlı isteyeceksiniz. Tüm diskleri yüksek oranda hello sırasında kullanılan değil, aynı anda hello depolama hesabı, daha büyük bir sayı diskleri destekleyebilir.

* **Azure yönetilen disklerin:** yönetilen diskleri sayısı sınırı Bölgesel ve ayrıca hello depolama türüne bağlıdır. Varsayılan hello ve ayrıca hello sınırı abonelik başına, bölge başına ve depolama türü başına 10.000. Örneğin, too10 oluşturabilirsiniz, 000 standart yönetilen disk ve ayrıca 10.000 premium diskler bir abonelikte ve bölgede yönetilen. 

    Yönetilen anlık görüntüler ve görüntüleri yönetilen diskleri sınırlamak hello karşı sayılır.

* **Standart depolama hesapları için:** Standart bir depolama hesabı en fazla toplam 20.000 IOPS istek oranına sahiptir. Hello tüm standart depolama hesabındaki bir sanal makine disklerinizi toplam IOPS bu sınırını aşmamalıdır.
  
    Yüksek oranda kullanılan disk hello istek hızı sınırı göre tek bir standart depolama hesabı tarafından desteklenen hello sayısı kabaca hesaplayabilirsiniz. Örneğin, temel katmana VM hello için en fazla yüksek oranda kullanılan diskleri olduğu hakkında 66 (disk başına 20.000/300 IOPS), ve bir standart katmanı VM için onu yaklaşık 40 (20.000/500 IOPS) disk başına hello aşağıdaki tabloda gösterildiği gibi. 
* **Premium depolama hesapları için:** Premium depolama hesabında en fazla aktarım hızı 50 Gbps’dir. Hello toplam verimlilik tüm VM disklerinizi bu sınırını aşmamalıdır.

