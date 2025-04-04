# Ethernet 

Networking'in ilk yıllarında her üretici kendi interconnecting network cihazlarını ve networking protokollerini kullanıyordu. Bu yüzden, farklı üreticilerden ekipman alındığında, onların birlikte çalışabileceği garanti edilemiyordu. Networkler yaygınlaşmaya başladığında, farklı üreticileri aynı noktada birleştirmeye yarayan çeşitli kurallar tanımlanarak standartlar oluşturuldu.

Uzun bir süre boyuncu resmi bir şekilde kullanılan local area networking protokol standartı yoktu. Ancak zamanla ethernet diğerlerinden çok daha popüler hale geldi. Ethernet protokolleri, verinin nasıl biçimlendirileceğini ve wired network üzerinden nasıl iletileceğini tanımlar. Ayrıca ethernet standartları, OSI modelinin 1. ve 2. katmanlarını yönetir. Ethernet teknolojisi daha popüler hale gelmesiyle beraber artık bir standart haline gelmişti ve neredeyse tüm wired local area networklerinde ethernet kullanılıyordu.

The Institute of Electrical and Electronics Engineers, ya da IEEE, ethernet ve wireless standartlarının da dahil olduğu networking standartlarını yönetir. IEEE komiteleri, bağlantılar için standartları, medya gerekliliklerini ve iletişim protokollerini yönetmek ve onaylamakla yükümlüdür. Her standarta, hangi komitenin o standartı onaylayıp yönettiğini belli edecek şekilde bir sayı atanmıştır. Ethernet standartlarından sorumlu olan komite, 802.3'tür. 

Ethernetin 1973'te ortaya çıkmasından bu yana, zamanla bu teknolojiyi geliştirmek için çeşitli standartlar öne sürüldü. Ethernetin bu zamanla gelişebilme özelliği onu popüler yapan ana nedenlerden bir tanesidir. Ethernet'in her sürümünün kendine özgü bir standardı vardır. Örneğin 802.3 100BASE-T, twisted-pair kablo standartlarını kullanan 100 Megabit ethernet'i temsil eder. Buradaki "100 Mbps" ifadesi hızını, "BASE" ifadesi baseband iletimi kullanıldığını ve "T" ifadesi ise kablonun türünü yani buradaki ifadeye göre de twisted-pair olduğunu temsil eder.

Ethernetin ilk versiyonları maksimum 10 Mbps'a kadar desteklerken, günümüzde ise ethernetin saniyede 1.6TbE (Terabit Ethernet) desteklemesi için kullanılacak standartın da geliştirme aşamasında olduğunu söyleyelim. Bunun haricinde, günlük kullanımda 1GbE ve 10GbE yaygın olsa da, veri merkezleri ve büyük ağ altyapılarında 100GbE ve üzeri hızlar kullanılıyor.

# Ethernet Frames

Ethernet, wireless (WLAN) ile beraber günümüzde kullanılan 2 farklı LAN teknolojisinden biridir. Ethernet teknolojisi, twisted-pair, coaxial kablo ve fiber optik gibi kabloları kullanarak kablolu iletişime olanak tanır. Ethernet, data link layerda ve physical layerda çalışır. IEEE 802.2 ve 802.3 standartlarında tanımlanan bir ağ teknolojileri ailesidir.

## Data Link Sublayers

Ethernetin de dahil olduğu IEEE 802 LAN/MAN protokollerinin çalışabilmesi için yani data link layer'ın yönetilebilmesi için bu katman, "Logical Link Control (LLC)" ve "Media Access Control (MAC)" adı verilen iki farklı sublayer'e bölünmüştür.

### LLC Sublayer

IEEE 802.2 sublayer'ı, üst katmanlardaki ağ yazılımları ile alt katmanlardaki cihaz donanımları arasında iletişim kurar. Frame'in içine, hangi network layer protokolünün kullanıldığının bilgisini ekler. Bu bilgi, birden fazla Layer 3 protokolünün (IPv4 ve IPv6 gibi) aynı network interface ve media üzerinde çalışmasını sağlar.

### MAC Sublayer

Bu sublayer (örneğin IEEE 802.3, 802.11 veya 802.15) donanıma entegre edilmiştir ve veri encapsulation'ını ile media access control'ünü sağlar. Data link layer adreslemesini sağlar ve çeşitli physical layer teknolojileriyle (yani twisted-pairlar, fiber optik kablolar veya kablosuz iletim sağlayan bluetooth ve RFID, NFC gibi teknolojiler) entegre olarak çalışır.



