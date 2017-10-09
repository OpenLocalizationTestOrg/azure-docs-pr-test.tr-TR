
* Merhaba dönüştürme hello VM yeniden başlatılmasını gerektirir, bu nedenle Vm'leriniz hello geçiş önceden var olan bir bakım penceresi sırasında zamanlayın. 

* Merhaba dönüştürme ters çevrilebilir değil. 

* Tootest hello dönüştürme emin olun. Üretim hello geçişi gerçekleştirmeden önce bir sınama sanal makinesini geçirin.

* Merhaba dönüştürme sırasında hello VM serbest bırakma. Merhaba dönüştürmeden sonra başlatıldığında hello VM yeni bir IP adresi alır. Gerekirse, [statik IP adresi atamak](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md) toohello VM.

* Merhaba özgün VHD ve dönüştürmeden önce hello VM tarafından kullanılan hello depolama hesabı silinmez. Tooincur ücretleri devam eder. Bu yapıtların için fatura tooavoid hello dönüştürme tam olduğunu doğruladıktan sonra hello özgün VHD BLOB'ları silin.
