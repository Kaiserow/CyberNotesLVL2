# Ping - Test Connectivity

Ping, hostlar arasındaki bağlantıyı test etmek için ICMP echo request ve echo reply mesajlarını kullanan bir IPv4 ve IPv6 test yardımcı programıdır. Bir ağdaki başka bir host ile bağlantıyı test etmek için, ping komutu kullanılarak host adresine bir echo request gönderilir. Belirtilen adresteki host echo request alırsa, bir echo reply ile yanıt verir. Her echo reply alındığında, ping isteğin gönderildiği ve yanıtın alındığı zaman arasındaki süre hakkında geri bildirim sağlar. Bu, ağ performansının bir ölçüsü olabilir. Ping, reply için bir timeout değerine sahiptir. Timeout süresi içerisinde bir yanıt alınmazsa, mesajın alınmadığını belirten bir mesaj sağlar. Bu mesaj sayesinde bir problem olduğunu veya ICMP isteklerinin bir firewall tarafından yasaklandığını anlayabiliriz. Arka planda ARP veya ND süreci bir adres çözümlemesi için çalışıyor olabileceğinden, ilk isteğin timeout mesajıyla karşılık bulması doğal karşılanabilir. Adres ne zaman çözümlenirse ICMP echo request de o zaman gönderilecektir.

Aşağıdaki üç farklı tip bağlantı testini yakından inceleyelim:

• Pinging the local loopback

• Pinging the default gateway

• Pinging the remote host

## Ping the Loopback

Ping, local host'da IPv4 veya IPv6'in dahili yapılandırmasını test etmek için kullanılabilir. 

IPv4’te 127.0.0.1, IPv6’da ise ::1 adresinden gelen bir yanıt, IP protokolünün cihaza düzgün şekilde kurulduğunu gösterir.
Bu yanıt, OSI modelinin ağ katmanından (network layer) gelir.

Ancak bu durum, cihazdaki IP adresi, alt ağ maskesi ya da varsayılan ağ geçidi gibi ayarların doğru yapılandırıldığını göstermez.
Ayrıca bu test, ağ yığınının (network stack) alt katmanları hakkında da herhangi bir bilgi vermez.

Bu işlem sadece IP protokolünün ağ katmanına kadar düzgün çalıştığını test eder.
Eğer bu adrese ping atıldığında bir hata mesajı alınıyorsa, cihazda TCP/IP protokolü düzgün çalışmıyor demektir.

## Ping the Default Gateway

Ayrıca, bir hostun yerel ağda iletişim kurma yeteneğini test etmek için ping'i kullanabilirsiniz. Bu genellikle host'un default gateway'in IP adresine ping atılarak yapılır. Default gateway'e başarılı bir ping, host'un ve default gateway olarak hizmet veren router arayüzünün her ikisinin de yerel ağda çalışır durumda olduğunu gösterir.

## Ping a Remote Host

Ping, yerel host'un bir internet ağı üzerinden iletişim kurma yeteneğini test etmek için de kullanılabilir. Yerel host, uzak bir ağın işlevsel bir IPv4 host'una ping atabilir. Router, paketleri iletmek için IP routing tablosunu kullanır.

#### NOT: Birçok ağ yöneticisi ICMP mesajlarının kurumsal ağa girişini sınırlar veya yasaklar; bu nedenle, ping yanıtının olmaması güvenlik kısıtlamalarından kaynaklanıyor olabilir.

# Traceroute (tracert)

Ping komutu iki host arasındaki bağlantı testi için kullanılabilir ama iki host arasındaki cihazlar hakkında detay sağlamaz. Traceroute (tracert), yol boyunca başarılı olarak ulaştığı hop'ların listesini sunar. Yol boyunca ilerler ve takılı kalırsa, takılı kaldığı router (hop) bize sorunları çözmek için bilgiler sağlayabilir.

## Round Trip Time (RTT)

Traceroute kullanımı, yol boyunca her bir hop için round-trip süresi sağlar ve bir hop'un yanıt verip vermediğini belirtir. round-trip süresi, bir paketin uzak host'a ulaşması ve host'dan yanıtın geri dönmesi için geçen süredir (o yüzden gidiş-dönüş süresi diyebiliriz.) Kayıp veya yanıtlanmamış bir paketi belirtmek için bir yıldız işareti (*) kullanılır.


Bu bilgi, yoldaki sorunlu bir routerı bulmak için kullanılabilir veya routerın yanıt vermeyecek şekilde yapılandırıldığını gösterebilir. Ekranda belirli bir hop'tan yüksek yanıt süreleri veya veri kayıpları gösteriliyorsa, bu, router'ın kaynaklarının veya bağlantılarının zorlandığının bir göstergesidir.

Traceroute, hedefe giden yolu (hop'ları) bulmak için, IP paketlerinin TTL (Time To Live) değerini kademeli olarak artırarak çalışır. (IPv6 için de aynı adımlar geçerli sadece TTL, Hop Limit olarak değişiyor.)

1. İlk gönderilen paketin TTL değeri 1’dir.
→ Bu paket ilk router’da zaman aşımına uğrar
→ Router, ICMP Time Exceeded mesajı gönderir
→ Traceroute böylece ilk hop’un IP adresini öğrenir

2. Sonraki paketlerde TTL değeri 2, 3, 4... şeklinde arttırılır.
→ Her seferinde bir sonraki router’da zaman aşımına uğrayarak
→ O router’dan ICMP Time Exceeded mesajı alınır
→ Böylece her adımda bir sonraki hop adresi tespit edilir

3. TTL değeri artırılarak nihayet hedefe ulaşıldığında, artık zaman aşımı olmaz.
→ Bu kez hedef cihazdan ya:

ICMP Echo Reply (ping'e cevap)

ya da ICMP Port Unreachable (UDP portu kapalıysa) mesajı gelir.




