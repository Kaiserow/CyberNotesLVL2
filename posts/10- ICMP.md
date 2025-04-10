# ICMPv4 and ICMPv6 Messages

IP'nin best-effort bir protokol olduğunu yani "ben elimden geleni yaparım ama garanti vermem" tarzında çalıştığını söylemiştik. Ama bununla beraber, bazen çeşitli hata ve bilgilendirme mesajlarıyla geri bildirimde bulunulması gerekebilir. Bu özelliği doğrudan IP'ye entegre etmek, onun best-effort özelliğine zarar vereceğinden ötürü ayrıca bir protokol olan "ICMP" kullanılır. Bu geri bildirimler IP'yi reliable bir protokol yapmaz, çünkü sadece geri bildirimde bulunulur, bununla beraber bir geri gönderim yapılmaz (yani TCP gibi çalışmaz). ICMP günümüzde çok sık kullanılmayıp, çeşitli firewall'lar tarafından güvenlik sebeplerinden ötürü genellikle engellense de bazen gerekli olabilir. ICMP mesajlarının gereklilik faktörleri kapsamlı olabilir. Biz şu anlık sadece 3 tanesine odaklanacağız;

• Host reachability

• Destination or Service Unreachable

• Time exceeded

## Host Reachability

ICMP echo mesajları adından da anlaşılabileceği üzere, networkte bulunan bir host'un ulaşılabilir olup olmadığını doğrulamak için kullanılır. Kaynak host hedefe bir "ICMP Echo Request" mesajı gönderir. Eğer karşıda gerçekten öyle bir host varsa ve ulaşılabilir durumdaysa, "ICMP Echo Reply" mesajı ile yanıt verir. Bu işlemi, daha önceden de aşina olabileceğiniz "ping" komutu ile sağlarız (Ping + Hedef IP/Domain name).

## Destination or Service Unreachable

Hedefe ulaştırılmak istenilen paket ulaştırılamadığında, kaynağı bilgilendirmek için "ICMP Destination Unreachable" mesajı gönderilir. Bu mesaj, paketin neden teslim edilmediğine dair bilgi veren kodları içerir. ICMPv4 için bu kodlar şu şekildedir;

0 -> Net unreachable

1 -> Host unreachable

2 -> Protocol unreachable

3 -> Port unreachable

ICMPv6 için de şu şekildedir;

0 -> No route to destination

1 -> Communication with the destination is administratively prohibited (Örneğin, firewall tarafından engellendiğinde)

2 -> Beyond scope of the source address

3 -> Address unreachable

4 -> Port unreachable

## Time Exceeded

ICMPv4 Time Exceeded mesajları router tarafından, paketin yönlendirilemediğini, çünkü "Time to Live (TTL)" süresinin 0'a ulaştığını kaynağa belirtmek için kullanılır. TTL alanını 0'a düşüren router, aldığı bu paketi atacak (discard) ve kaynağa bir "Time Exceeded" mesajı döndürecektir. ICMPv6'da da aynı işlem gerçekleşir, sadece tek fark TTL yerine Hop Limit olmasıdır.

Windows komut satırı üzerinden "tracert" komutu ile bir IP veya domain name vererek, kaynaktan hedefe gilidirken kaç tane "hop" noktasından geçildiğini görebilir ve eğer TTL 0'a ulaşırsa da "time exceeded" mesajını görüntüleyebilirsiniz.

# ICMPv6 Messages

Bu mesajlar çoğunlukla ICMPv4'e benzer fakat ICMPv4'te olmayan bir takım ek özellikler de sunar. Adından da görebileceğiniz üzere, ICMPv6 mesajları IPv6 paketine kapsüllenir (encapsulated).

ICMPv6, "Neighbor Discovery Protocol (ND ya da NDP)" nin bir parçası olarak 4 yeni protokol içerir.

Dinamik adres tahsisi (allocation) de dahil olmak üzere bir IPv6 routeri ile bir IPv6 cihazı arasındaki mesajlaşma aşağıdaki gibidir:

Router Solicitation (RS) message

Router Advertisement (RA) message

IPv6 cihazları arasındaki mesajlaşma, yinelenen adres tespiti (duplicate address detection) ve adres çözümlemesi (address resolution) dahil olmak üzere şu şekildedir:

Neighbor Solicitation (NS) message 

Neighbor Advertisement (NA) message

### RA Message

RA mesajları, IPv6 cihazlarına adresleme bilgisi sağlamak için, IPv6 etkinleştirilmiş her router tarafından genelde 200 saniyede bir gönderilir. Bu mesajlarda cihazlara, ağla ilgili adres bilgileri sağlanır:

• Prefix (örneğin 2001:db8::/64) -> Burada kastedilen şey bildiğimiz network adresi ya da bir IP adresinin network portionudur.

• Prefix length (yani o ağ bloğunun kaç bit olduğu, genelde /64)

• DNS adresi

• Domain adı (Bir domain name eksik yazılırsa, default olarak hangi domain ismine tamamlanacağını belirtir. Örneğin, ping www yazarsanız ve default olarak example.com adresine tamamlanması gerektiği söylenmişse, www.example.com adresine tamamlanır.)

Cihaz IPv6’de SLAAC (Stateless Address Autoconfiguration) kullanıyorsa, bu RA mesajıyla gelen prefix bilgisini alıp kendi IPv6 adresini üretir.
Ayrıca:

Varsayılan ağ geçidi (default gateway) olarak da
RA mesajını yollayan router’ın link-local IPv6 adresini (mesela fe80::1) kullanır.

Örneğin;

Router, "Merhaba IPv6 cihazları. Bir IPv6 global unicast address'ı oluşturmak için SLAAC kullanabilirsiniz. Prefix -> 2001:db8:acad:1::/64 şeklindedir. Bu arada default gateway'iniz olarak da benim link-local adresimi yani "fe80::1" adresini kullanabilirsiniz" diyerek bir RA mesajı gönderir.

### RS Message

IPv6 etkin bir router ayrıca bir RS mesajına yanıt olarak bir RA mesajı gönderecektir. Örneğin PC1, IPv6 adres bilgilerini dinamik olarak nasıl alacağını belirlemek için bir RS mesajı gönderir.

1. PC1, ağda herhangi bir IPv6 routerı olup olmadığını doğrulamak ve IPv6 adresleme bilgilerini nasıl alacağını öğrenmek için bir RS mesajı gönderir.

2. Router da RA mesajıyla yukarıda belirtildiği şekilde yanıt verir.

#### NOT: Hem router periyodik olarak RA mesajı yollar, hem de bir host RS (Router Solicitation) atarsa, router hemen özel olarak RA mesajı döndürür.

### NS Message

Bir cihaza global unicast IPv6 adresi ya da link-local unicast adresi atandığında, bu adresin benzersiz olup olmadığını doğrulamak için "Duplicate Address Detection (DAD)" gerçekleştirilebilir. (Farklı ağlarda bulunan cihazların link-local adresleri aynı denk gelebilir fakat yerel ağ içerisindeki iletişim için benzersiz olmalıdır ki karışıklık olmasın.)

Bu işlem için kaynak cihaz, kendi IPv6 adresini hedef olarak belirleyip bir "NS" mesajı gönderir. Eğer bu IPv6 adresine sahip başka bir cihaz ağda mevcut ise, "NA" mesajı ile yanıt verir. Bu NA mesajı, NS mesajını gönderen cihaza, bu IPv6 adresinin kullanıldığını bildirecektir. Eğer belirli bir zaman içerisinde NS mesajına, NA mesajı ile yanıt verilmezse, kullanılan IPv6 unicast adresinin benzersiz bir adres olduğu kabul edilir.

#### NOT: Global unicast IPv6 adresi ile link-local unicast adresi farklarını anlayabilmek için IPv4 üzerinden örneklendirelim; IPv6 sisteminde, router'ın local için kullandığı arayüzüne atanan adres link-local adresidir. Aynı IPv4'te local için, default gateway IPv4 adresinin kullanılmasına benzer. Global unicast adresi de, IPv4'te kullanılan ve router'a ISP tarafından atanan Public IP adresine benzer. İkisi de WAN (Wide Area Network) yani yerel ağın dışındaki arayüz için kullanılır. Tek fark, Global unicast adresi, router'ın LAN arayüzü kullanılarak, yerel ağdaki cihazlara dağıtılır.

#### NOT: DAD gerekli değildir ama RFC 4861 kullanılmasını önerir.

### NA Message

Address Resolution, LAN'daki bir cihaz bir hedefin IPv6 unicast adresini bildiğinde ancak Ethernet MAC adresini bilmediğinde kullanılır. Yani bizim bildiğimiz ARP sürecine oldukça benzerdir. Hedef için MAC adresini belirlemek istediğinde bir cihaz, solicited node adresine bir NS mesajı gönderecektir. Bu adres, hedefin IPv6 adresinden türetilen özel bir multicast adrestir. Normalde multicast adresleri bir grubu temsil eder ama buradaki adres grubuna genelde sadece hedef cihaz dahildir. Bu biraz garip gelebilir ama sonuç olarak bu adres, hedef MAC adresi bilinmediğinden bir unicast adresi olamaz. IPv4'da kullanılan ARP gibi tüm ağa broadcast atılması da çok verimli bir yöntem olmadığına göre en mantıklısı multicast kullanmak olacaktır. Gönderilen NS mesajı hedef IPv6 adresini içerir. Hedef bu IPv6 adresini kendi MAC'iyle karşılaştırıp doğruladıktan sonra kendi MAC adresini içeren "NA" mesajıyla yanıt verecektir.

-------------------------------------------------------------------------------------------------------------------------------

Neyin ne olduğu çok fazla karıştıysa, durumu şöyle özetleyelim:

Yukarıdaki mesaj türleri ICMPv6 protokolünün kullandığı mesajlardır. IPv6'in, IPv4'te olmayan bir çok fonksiyonu ek olarak desteklediğini önceden söylemiştik. Bu kapsamda da ICMPv6 mesajları ICMPv4'e göre çok daha işlevlidir. Bu mesajlar, ARP ve DHCP gibi protokollerin ayrı ayrı yaptığı işlemleri, onlara gerek kalmadan sadece ICMPv6 mesajları kullanılarak yapılmasına olanak tanıyarak ek yükü ortadan kaldırır.

#### NOT: ICMPv6 mesajları DHCP’yi tamamen ortadan kaldırmaz; bazı durumlarda DHCPv6 hala opsiyonel olarak kullanılabilir.








