Модель|Состояние|Детали
---|---|---
**NVIDIA**
*pascal*
MSI GTX 1080 Ti gaming X, 11gb (черный матовый)|требует ремонта прогара и возврат элементов|получена в ремонт с прогаром под одним из плеч и сбитыми С1476 С156 R751 (под жжёной фазой) и сбитыми С1276 рядом с PCIE.
MSI GTX 1080 gaming X, 8gb (черный матовый)|починено и возвращено в октябре 2017|получена в ремонт с прогаром под одним из сдвоенных плеч. После вынимания плеча и чистки прогара - работает. Прогар заделан, фаза поставлена назад.
MSI GTX 1070 gaming X, 8gb (черный матовый)|почти не исследована|получена как донор для ремотна в состоянии "часто исчезает изображение, иногда просто сразу только включается монитор и ничего не показывает".
Asus GTX 1060 dual, 3gb (черный матовый)|отремонтировано в августе 2017|получена в ремонт с майнинга со сбитыми элеметами. Сбиты дорожки около вольтметра u19, он не даёт Power valid. Убрана эта проверка выпаиванием нулевого резистора к левому контакту правого диода 42t  - карта стартует, но при нагрузке даёт максимальные обороты вентиляторов. Под разъёмом отсутствует D6 с маркировкой WW1 (на тестпоинте - ближе к краю при нормальной работе - прямоугольные импульсы скважности 50%, частоты, зависящей от оборотов (порядка 40-100Гц), диапазона ~3v. На дальней от края - импульсы частоты порядка 50 КГц. На отдельном контакте - 3.3м. А также нет Q130 (SOT363, маркировка K6N D2), восстановлен диод - видеокарта управляет своими вентиляторами
Asus GTX 1060 dual, 3gb (черный матовый)|отремонтировано в августе 2017|получена в ремонт с майнинга, найден распаявшийся/повреждённый элемент с маркировкой 22G20 (и подчёркнуто). На другом экземпляре он маркирован как 21?24 (где ? - это палка то ли i то ли L). замена элемента помогла
Asus GTX 1050ti, 4gb (черный матовый)|исследовать поведение gpu на более высоких напряжениях|взята у перекупщика, состояние: следы флюса под gpu, перепаяная микросхема BIOS, сдвинут резистор, но похоже, что он на месте. при запуске карта читает биос, определяет свои основные параметры, но с драйвером nvidia - rminit adapter failed, с nouveau - таймаут при инициализации 3d,  вывод изображения работает нормально. невысокое напряжение на gpu - 0,77V. Для донорства снят EQ505 в корпусе SC59 с маркировкой 22G20| (и подчёркнуто). До снятия в процессе работы 12v, 12v, 4v, по идее можно заменить на шунт 2-х 12v.
Gigabyte P106, 6G, SN 03|возврат без ремонта, горелый чип|GPU 0.3 Ом,Память 43 Ом. при подключении даже без питания перестает работать весь pci e. Выпаян R713 - теперь PCIReset не заземляется, и осатльные устройства работают, но карта не определяется.
Gigabyte P106, 6G, SN 07|возврат без ремонта, горелый чип|GPU 0.4 Ом,Память 46 Ом, напряжение поднимаются, не определяется как pci -e уст ройство, но не висит и не вырубает
Gigabyte P106, 6G, SN 74|возврат без ремонта, горелый чип|GPU 0.2 Ом,Память 40 Ом, напряжение поднимаются, не определяется как pci -e уст ройство, но не висит и не вырубает
Gigabyte P106, 6G, SN 97|возврат без ремонта, горелый чип,последствия плохого втыкания в райзер|GPU 0.3 Ом,Память 43 Ом,Шарик рядом с U6, 5 Ом на клоке с PCIe
*Maxwell (750, 945-980), GM???*
Asus GTX 980, 4G (чёрный, Strix directCUII)|Предполагается научиться загружать BIOS через nvafakebios (взять дамп со второй карты)для родного драйвера.|Определяется PCIe-устройство, но не читается его BIOS в Winbond 25x20cln1g. При запуске nouveau с BIOS из файла появляется картинка, но артефачит красноватыми полосками во framebuffer. В dmesg - таймауты. Тестирование фреймбуфера показало присутствие проблем в одном из модулей памяти, по всей видимости M4 (или M3).  Выпаян 10кОм резистор между CE и VCC и микросхема BIOS - но CE всё равно 3.3v, только иногда маленькое подрагивание. После этой операции глюки M3 пропали, сколько-то даже работал Furmark на nouveau, но потом появились глюки на M6, а на M3 глюков нет(? м.б. не ошибка). Потом снова проблема на M4. Впаивание рабочей микросхемы BIOS ничего не дало. Исходная оказалась рабочей - работает впаянной на другую карту. При явном запросе чтения из prom через envytools - происходит обращение к ROM-микросхеме, однако в программу возвращается лишь мусор. Возможно, что можно подложить BIOS через nvafakebios и запустить с драйверами nvidia. Возможно, что проблемы с BIOS связаны с битой памятью. Замена модуля убрала проблемы памяти. Glxgears работает на nouveau. начинает искать биос по адресу fb300000 в 16мб pcie bar, но там нет нужной сигнатуры. замена микросхемы биос на родную не дало результатов на первый взгляд
Gainward GTX 980, 4GB (чёрно-коричневый)|Предполагается анализ зависимости проблем памяти от частоты gddr5 на основе maxwell reclocking in nouveau.|При инициализации драйверов nvidia подвисает (даже от nvidia-smi). Если до этого проводился тест памяти  - после инициализации драйвера некоторые буквы становтся белыми. При этом на nouveau показывает даже furmark, но медленно. При подключении x1 такая же ситуация. Обнаружен сколотый конденсатор на pcie. На в 10 раз сниженной частоте памяти работает. На 3ды пониженной частоте памяти ошибки памяти модуля M6. подготовлена под замену модуля М6, вздулись треврдотельные конденсаторы. Сопротивление GPU 4.6V (норма), на памяти окло 20 Ом. После замены M6 - ситуация не изменилась - при частоте памяти в 1728 и выше - вырубается модуль M6 при загрузке драйверв (Xid 62), а при 1080 - глючит модуль M8. С выпаянном BIOS не подаёт CE, но после принудительной загрузки nouveau - работает. Reclocking - уточнить по "fb/ram: Use Kepler implementation on Maxwell" 38a7c22. На повышенном напряжении процессора и пониженном всём остальном - работает до артефактов около часа.
Zotac GTX970 (чёрный матовый)|Починено в июле 2017, тестируется|Получено с симптомами "перестаёт работать в процессе игры через разное время". Обнаружен заклинивающий вентилтор. Была в пыли с сухой пастой, хотя температура нормальная. Разомкнут предохранитель системы охлаждения, поставлен внешний вентилятор. Предохранитель возвращён работает.
Gigabyte GTX 950 XTREME GAMING 2GB (чёрный)|Починено, продано с родным BIOS в июле 2017|По словам продавца - артефакты. На практике вообще чёрный экран. Обнаружена полная неработоспособность двух чипов памяти. Восстановлен сбитый резистор 1330 Ом между Vrefc памяти и землёй - исчезли проблемы памяти. Возвращён родной BIOS - больше нет чёрного экрана, всё работает. Временно для использование без UEFI 00 03 заменено на FF 04 в PCIR-структуре ROM для UEFI.
Asus 750ti 2Gb OC (черный глянцевый)|анализировать одинаковость clock, термотест памяти.|артефакты с nvidia одна четверть от всех модулей, с nouveau  - поврежден 1 из 4 байт, стоит неродной биос, высокое напряжение на памяти - 1,6V, стояла защита от перезаписи биос, bios перезаписан, но напряжения памяти  остались теми же, на gpu 0,96V. визуально артефакты выглядят как стандартный вылетевший модуль. Понижено напряжение памяти заменой резистора 2.5КОм на 4.7КОм в делителях обратной связи ШИМ памяти. Поведение памяти на 1.22v такое же. Глючит модуль M1. Все сопротивления cовпадают с модулем M3.
Msi 750 2GB (чёрный)|Снят GPU. На плате КЗ исчезло|Сопротивление менее 0.1 Ом как по линии питания памяти, так и по линии питания процессора. Проверено что на снятом GPU КЗ по линии питания памяти.
*Kepler (6??, 650-730, 7??), GK???*
Palit 780 SuperJetsream (чёрный, нет CO)|Артефакты, исследовать как 770|
MSI 780 Gaming (чёрный, TwinFrozr IV)||Получена с симптомами "стала выключаться, потом при 80 градусах вырубилась совсем", микросхема в углу повреждена деформироровалась APW7142, которая даёт питание логики DrMos. стартует редко и только если нет монитора. L6 - фаза нестабильна, L11 - фаза не работает нет контакта до pwm ?  большое сопротивление до земли. En шима обычно падает спустя несколько секунд, dr mos U8 U13 на tda21220 - 3d работает,  но 2 и 5 фаза неистово греется, есть пдозрение что не открывается нижнее плечо.
Gainward 770 4GB GDDR5(чёрный)|При частоте памяти 1200 работает очень стабильно.|По словам продавца - артефакты после установки драйверов. gpu-memtest не находит ошибок до попытки загрузить драйвер. Артефакты в BIOS если прошить новый (80.04.E6.00.0E) BIOS. На более старом 80.04.C3.00.BE Стабильно работает на 1200МГц памяти, на 1201 сразу вылетаетв артефакты. На nouveau вылетает на меньшей частоте.
Palit 770 2GB GDDR5 (чёрный, самая простая вариация от palit) |Ожидает возврата/горелдого конденсатора и предохранителя|получена с неясной предситорией с замыканием по входу. Пробитый конленстор устранён, показывает 3D.
MSI 770 2GB GDDR5(коричневый, без радиатора Twin Frozr)|Выключается|Была с повтороно выгоревшими нижними плечами по одной из фаз. После выпаивания - стартует, показывает 3d, но быстро вырубается.
Gigabyte 690 2x2GB GDDR5(чёрный)|отдана владельцу|Поступила в ремонт с симптомом "выкючается через случайное время под под любой нагрузкой" на практике выключается даже без 3Dпропадает питание на всем, кроме моста.Сопротивление обоих gpu - 12.8Ом. Сопротивление на памяти 80-84Ом, НА МОСТУ 12,2Ом. Проблема воспроизводится при попытке перевести вентилятор в ручной режим (даже если он не подключен). Без вентилятора 3d работает. Предположительно один из ШИМ гасит power good, что через ситсему обратной связи гасит оба ШИМ до reset по PCIe. При размыкании обратной свизи заземлением ключа q523, ШИМ U13 продолжает генерировать напряжение на GPU, но перестаёт давать power good. установлен новый шим, все драйвер мосфеты на пробленой цепи, после проверки ясно что L17 L14 не поднялись? pwm  на них есть. после перепайки этих фаз - работают нормально, проблема изначальная проблема не решена. без доп питания на разъемах 12v - 10,8v. 12v c pci-e 11v. vgpu1 - 0.984V(показывает), vgpu2 - 0.965v(не показывает), vmem1 1.375V(показывает), vmem2 1.5V(не показывает), en U523 2,69v стбильно(? не полностью уверены), непоказывающий gpu: импульсы на фазах частота 100кгерц,все фазы на нем работают, напряжение неровное, период напряжения 100кгерц, не греется  показывающий gpu: напряжение ровное, очень горячий. прошит биос, замеры  в ситуации, когда работает другой gpu - 1.05v, нерабочий - 0,981V. остальные замеры не изменились. выход работающего gpu  нестабилен, то ровный, то нет.
Gigabyte 690 2x2GB GDDR5(чёрный)|Починено питание на PEX-switch PEX8747|Поступила в ремонт после отказа во время прогона тестов после установки нового охлаждения при температуре порядка 100градусов. Не определяется. Есть питание на GPU, памяти, flash-памяти моста, но нет на самом мосту. Сопротивление по питанию моста - 2.2Ом. Сопротивление по ключу нижнего плеча Q15 - 1.5Ом - это мосфет M3006M размерами 2.8x2.9. Верхнее Q16 не в КЗ, mosfet AON7430. Спас выгоревший предохранитель R203. Выбранная замена - нижнее - IRFHM830DPBF, верхнее IRFHM831PbF. После замены всё работает. Ток для моста через предохранитель 12v - ~0.6А. Напряжение моста - 0.913v.
Evga 680 2GB GDDR5 (чёрный)|При запуске карты с подключённым дополнительным питанием появляется 0.89В на GPU, но отсуствуют другие системы питания|Пришла с прогаром транзистора по питанию памяти и ШИМом памяти RT8807BGQW с дыркой (по идее аналог APW7088). Также были отломаны некоторые ножки на gs7103 (low-dropout regulator, один из них снят, возможно аналогичен RT9018B, APL5920). После удаления транзистора, дросселей и конденсатора осталось 2Ом на входе PCIE 12в (сильно греется в районе прогара) м 0.03Ом на питании паямти. Поиск места КЗ указал на район C672, хотя он сам не виноват. Основное подозрение на чип паямти на обратной стороне от него. Снят чип памяти M5. Оказались пробиты как VDD (0.42 Ом), так и VDDQ (0.14 Ом). Сопротивление по питанию памяти незначительно увеличилось (0.042 Ом). M6, M2 сняты, сопротивления такого же порядка. M7 - снят, но повреждён не так сильно: сопротивление VVDQ 11 Ом. После этого сопротивление по питаню памяти составило 0.25 Ом. При подаче номинального напряжения памяти в 1.6v ток достиг 2А и термопара показал что температура M8 на 4 градуса выше остальных. После его снятия сопротивление составило порядка 10-1 Ом (при подаче 0.3-2v). Gри подаче 2v ток былнаибольший нагрев-на GPU ~ на 4 градуса. То есть течёт через какие-то сложные элементы и можно пытаться в таком виде запустить, так как перегрва при нормальном напряжении не происходит. Замыкание на PCIE устранено ковырянием в районе прогара с особым вниманием на ноки, соединяющие стороны платы.
Msi 680 2GB GDDR5 (чёрный)|тесты пройдены, работает полностью, подарена|После старта все напряжения есть, но даже при наличии интегрированного видео - 1 длинных 2 коротких. После этого иногда определялась в nvflash. BIOS был нулевого размера. Перепршит BIOS. После этого не пищит, как будто стартует. После запуска Xorg даже показывает изображение, но с уклоном в синий (нет красного). Бублик работал, но периодически вырубалась (изображение пропадает, вентиляторы крутятся быстрее). Иногда система не стартует, особенно если подключен монитор. при подключении  к другому монитору по dvi синевы нет, а вырубания просиходят в случайном месте, независимо от нагрузки. после вырубания напряжения нет ни на памяти, ни на gpu. БП не просаживается. Возле линии Analog red обнаружен повреждённый белый элемент, половина которого марирована чёрным. Имеет скол и в отличие от соседних не нулевое, а бесконченое сопротивление. обнаружен и заменен расколотый предохранитель на линии детектирования присутствия доп питания. теперь стартует с подключеным монитором. Для A79R-AX - поставлен старый BIOS. установлены нулевые элементы для решеня проблемы с vga разъемом.
Asus GTX760 2G GDDR5 DirectCU II Top (чёрный матовый)|Отремотировано в августе 2017, тестируется|Заменены закоротивший конденсатор и оборванный предохранитель
Palit GTX760 2G GDDR5 (тёмно-коричневый)|Фризы в 3d|Обрыв в предохранителе L2 с маркировкой X (8 Ампер). Вызван КЗ в верхнем плече микросхемы U16. Стоящие рядом аналогичные микросхемы отличаются, как будто их уже меняли. Сопротивления в норме, GPU ~12 Ом. После выпаивания пробитой фазы и установки предохранителя - стала включаться. Заменена фаза питания. Запускается, но при загрузке драйвера возникают подвисания и сообщение об ошибке Xid 8. BIOS был не родной. Прошит на обновлённую версию - подвисания отслись, но уже не при запуске awesome. Выяснилось что при низких напряениях (0.89) - подвисания и артефакиы в 2D, при высоких (1.25)- только остановки после начал работы 3d. 2D работает. Найдены сбитые элементы на обратной стороне, 3шт. Сопротивления на посадочных местах: 898  Ом (Вход 3.3), 8.5КОм  (по входу доп. питания), 24КОм (по входу другого доп. питания). Сбитые конденсаторы возвращены, проверено на другой мат-плате и на x1 - результат не изменился. Тест памяти прямой записью в PCIe BAR пройден. ocl_memtest выдаёт ошибку при запуске. Прямое чтение памяти во время подвисания работает, т.е. видеокарта отвечает на запросы. PGOOD основного ШИМа в норме, а PGOOD системы питания 1.05v присутствует, но имеет очень слабое подтягивание вверх, которое гасится осциллографом. Также возможен непропай 2-й ножки главного ШИМ. Но наибольшее подозрение - несоответствие напряжения установленному в VBIOS. Возможно виноват DrMOS U13 (последний не заменённый на SIC780), который не открывает нижнее плечо. Заменён, проблема осталась. На осциллографе подозрительно шумит выход системы питания PCI-E. Её вход - питание памяти порядка 1.4в, что подозрительно мало. ШИМ памяти - RT8809BZQW. Настраивается на выдачу пониженых 1.38V из-за подачи напряжения на VID, с не найденного источника 3.2v. Выпаян резистор 990Ом через который оно шло. напряжение на памяти 1.6V, ситуация не поменялась.
Gigabyte GTX760 OC|починено, возвращено|Поступила в ремонт, вообще не работала одна микросхема памяти: появлялись полоски даже в BIOS при его графическом режиме. Обнаружено отсутствие двух резисторов, поставлены.
Gigabyte GTX660 3G GK106-400-A1 (тёмно-коричневый)|Снят GPU КЗ, осталось КЗ в плече прогара|Имеет прогар в одной из фаз питания GPU. Однако сопротивление GPU по линии питания ~1.1Ом, что по идее меньше сопротивления  аналогичных карт. По питанию памяти и 3.3v с платы - сопортивление нулевое. Также КЗ на транзисторе стоящем на месте прогара. Поиск места кз не производился. Также вероятно сбит C79. 3.3v идут на как минимум на BIOS и на U508.
MSI GTX660 2G Twin Frozr Gaming (коричневый)|Сажать GPU назад|Не определяется, нет генерации (хотя напряжения на кварце есть). Ultra-low dropout U501 давал нестабильные 0.6v вместо 1.05v. После замены напряжение в норме, но ситуация не изменилась. На GPU 0.9v. Обнаружено замыкание между выходами кварца. Замыкание исчезло после снятия GPU, но и в самом GPU замыкания нет. Возможно замкнуло ранее, когда кто-то прогревал.<br/>U5 - Pm25LD020 - VBIOS<br/>U10 - NCP5901B - внешний ключ для 4-й фазы<br/>U11 - NCP5395G - основной ШИМ<br/>U507 - RT8101 - ШИМ памяти<br/>U508 - APL3516A - линейная система питания DisplayPort
Palit GTX650 1024M GDDR5 (тёмно-коричневый)|отремонтировано, продано|Замыкание по линии 12v с разъёма pcie, сопротивления порядка 0.1Ом. В питании GPU напряжение с pcie не используется, используется только для питания памяти. Более чем 2-лапых элементов немного, все не вызвали подозрений. Наибольшие подозрения вызвал бОльший конденсатор непосредственно в районе прихода 12v с платы. был обнаружен пробитый конденсатор на линии 12v c pcie (рядо с pcie), заменен на больший. 
ASUS GTX650Ti 1GBDDR5 (чёрный)|Артефакты в 3d (unexpected spikes)|. Дебаггинг показал что по всей видимости некорректно работают шейдеры на последнем по индексу ядре из 4х. Перепрошивка на K2100M из DOS оказалась нерабочей. Удалось вернуть закоротив CE на VCC при загрузке, и CE на GND перед прошивкой для обхода проверки.
Asus GT740 2GB GDDR5|подтвердить проблему gpu реболом и заменой шаров m3|Поступило в на вид не использовавшемся и не открывавшемся состоянии с артефактами. Сбоит каждый 4-й байт в одном из модулей, причём бит 0b00010000 из байта 0x1 немного чаще других. сбоит модуль M3. диагностический прогрев на модуль M3 убрал проблему на полчаса. samsung k4g41325fc-hc04. Замена M3 оставила проблему, но сделала её несколько плавающей - все подозрения на GPU (корректно проходит ZERO, ONE, 55 но не RAND, aa). Заменённый модуль или что вероятней его шары - также добавил ошибку 0b00000010 в байте 0x0 (не проходит ни ZERO ни ONE ни RAND, но проходит 55 и aa)
Gigabyte GT730 2GB GDDR5|Починено в июне 2017|Поступило в ремонт, возвращён сбитый конденсатор на PCIe и поставлен вентилятор.
*Fermi (420 - 625, 6??), GF???*
Gigabyte 590 2x1536MB GDDR5 (чёрный)|Получена от мастера, как донор памяти Samsung HC04, 1GBit (K4G10325FE-HC04)| Тестирование GPU, имеющего видеовыход, говорит об проблемном модуле памяти, соответсвующему clock-резистору, ближайшему к pci-e возле M611/M1. До памяти второго GPU достучаться не удалось. Падает в ядре при запросе nvidia-smi или при загрузке драйвера.
MSI N590GTX 2x1536MB GDDR5 (чёрный)|Отдано с 1м рабочим gpu|Получена с симпотомом "постоянно артефактит". При тесте с выключенной интегрированной работает 3d на основном GPU, Opencl - на обоих. MultiGPU приводит к отвалу карты. Очищен один BIOS прерыванием nvflash, после этого нормально заработала на windows на одном GPU. Такая прошивка не определялась на многих картах. Потом один чип заартефачил, он прошит в 580, оставлен только другой. Иногда даёт на windows ошибку 43. 
MSI N570GTX 1280MB GDDR5 (чёрный)|Очень быстро вырубается|Стартует, определяется драйвером, вырубается. Температуру показывала 50 градусов в простое. Потом стала просто менять скорость вращения вентиляторов при старте, нет картинки.
Gainward 570 1280MB GDDR5 NE5X570010DA-1100 (коричневая)|отремонтировано в августе 2017, продано сентябрь 2017|кз в верхнем плече первой фазы питания gpu. под транзистором прогар. транзистор снят. Причина КЗ - в MOSFET driver U2. Сопротивление GPU 0.5-0.6Ом - как оказалось рабочее. При поиске КЗ прожёгся элемент рядом с нераспаянной SU3 (чёрный маркирован 1-0). ДОбавляются оторванные конденсатры (6шт) и 1 КОм на памяти. При попытке включения кратковременная попытка подать напряжение на GPU. После замены верхнего плеча и его ключа - питание GPU есть, работает 3D, но активируется только одна фаза питания. OD1 - 5.2v, ODN - отсутствует, хотя PWM идёт на все ключи. Напряжение, генерируемое линейной системой AX1007 - 9.3V. После подачи 5v на ODN - заработали все ключи кроме U7 и U11. После замены этих ключей - все фазы работают.
Gainward 570 1280MB GDDR5 mHDMI (чёрный)|карта полностью рабочая, продано|В текстовом режиме некоторые символы мусорные. При загрузке драйвера сыпет ошибки и падает драйвер. Программный анализ показал, что взводится 2-й бит (пробелы превращаются в $) для многих байтов. Поочерёдный RESET модулей показал, что по всей видимости пролема в неполучении данных при работе с одной дорожки микросхемы памяти M3 (Samsung 037 K4G10325FE HС05). После качания M3 на шарах ситуация изменилась - теперь не взыодится второй, а опускается первый бит. Отпаяна совсем. После отпаивания симптомы мало изменились, даже запустился awesome, но больше артефактов и ошибок Xid. После замены чипа памяти проблемы исчезли: 3d запускается. Без родного охлаждения сильно греется. На стандартном BIOS через несколько десятков секунд работы Furmark появляется потрескивающий звук и через несколько секунд перезагрузка системы. Причина по всей видиомсти в том, что при пиковых нагрузках данная карта превышает лимиты питания (что "исправляется" в Windows-драйверах путём понижения параметров карты для Furmark). На benchnark "Piano" тоже приходит к перезагрузке, но несколько позже. Многие другие держит нормально. После подключения к двум БП (300+450) Furmark работает без проблем.
ASUS ENGTX560 (чёрный)|отдана|Был сбит 1 резистор 550Ом по VREFD у модуля памяти. Не работало 2 модуля. После установки - всё работает, Furmark греет до 74 градусов.
Zotac GTX560 (чёрный)|Работает, собрана без крышки и продана|Работает, но сильно греется даже при хорошем теплоотводе. Вероятно надо скальпировать. Скальпировано, собрано без крышки; теперь температура не превышает 75 (при запуске без корпуса).  скальпирована удачно.
Palit GTX560 OC 1GB GDDR5 (коричневый)|Работает. продана|Проблемы с одним из битов памяти в M6, XID 44 при загрузке драйвера. First address for 0b100000: 0x106. После замены этого чипа памяти работает, температура GPU в норме. Модель NE5X560THD02-1143F. Карточка требует устойчивого БП, более мощный основной подключался к боле требовательному крайнему 6-pin.
Palit GTX550Ti 1GB GDDR5 (коричневый)|Не определяется, донор элементов|Вначале были артефакты шрифтов в текстовом режиме. Но потом вообще перестала определяться: при старте запускается с интегрированным видео, хотя все напряжения есть. БЫло обнаружено, что сопротивление по 3.3v необычно низкое: 40Ом. При подаче 3.3v - ток ~0.3А, что даже меньше чем на рабочих картах. Так что на КЗ под GPU это не похоже.
Palit GTX 560Ti 2GB GDDR5 (красный)|Отремонтировано в марте 2017. после замены радиатора вернулись оплностью аналогичные симптомы, что и  до ремонта|При загрузке драйвера сыпет ошибки и тормозит драйвер, который с другой картой работает нормально. По словам продавца - проблемы под нагрузкой. Плата пратически идентична Palit GTX460 Sonic. Программа тестирования памяти находит проблемы при случайном тестировании с незагруженным драйвером. Проблема локализована в чипе паяти SM8 (SAMSUNG K4G10325FE-HC04), при помощи ZQ и RESET. После замены 3D с родным драйвером работает.
Zotac GTX470 1280MB GDDR5 (чёрный)|Прогар на плате|Получена из сервиса, где была донором с наклейкой GTX465. Есть пайка и снятые элементы, по крайней мере 3. КЗ по дополнительному питания 12v в одном из разъёмов. КЗ вызвано прогаром дорожек под транзистором. После устранения транзистора вместе со всеми дрожками под ним - осталось 3 фазы мз 4х, КЗ нет, но и старта gpu нет. Сопротивление на gpu 0.3Ом,1032510325 работоспособность gpu не ясна. Память 8 Hynix H5GQ1H24AFR-T0C
Gainward GTX470 (коричневый)|Заменён чип памяти, работает, продано. Через месяц симптомы вернулись, возвращено.|Не работала, из чипа памяти M1 всегда считывались единицы. Замеры сопротивлений до земли конденсаторов gddr5 не по питанию:<br/>VREFD - 2шт, 365 Ом. Соединены для пары, т.е. 4 параллельно.<br/>VREFC - 1шт, 365 Ом. Соединены для пары, т.е. 2 параллельно.<br/>Между парой 40Ом резисторов от CK_t/c 100КОм (обр. 12КОм). Отдельно от всего. Ёмкость 11.2nF. После возврата симпотмы идентичны исходным.<br/>
Gainward GTX465 (коричневый)|Работала без мелких конденсаторов, потом появились артефакты|Работает, но в редких случаях не инициализируется. на плате множество снятых конденсаторов, но работает. После лежания и кардинальной чистки - артефакты памяти. Со стороны GPU отсуствующих элементов не обнаружено, а с обратной:<br/> * 1 сдвинутый конденсатор на PCIe<br/> * 1 сколотый резистор между GPU и наклейкой  A100520002. На непохожем reference 470 он 10КОм, а на более похожем GTX570 - 321Ом. Без резистора - 0.3 - 2.0 МОм в зависимости от соседних измерений (видимо открываются транзисторы). Одна нога на земле, другая идёт в gpu.<br/> * 4 больших конденсатора в районе доп. питания.<br/> * 2 средних конденсатора по верхней линии памяти<br/> * 4 мелких конденсаторов в районе оборотной стороны M7, M8, из которых 2 далёких друг от друга НЕ по питанию памяти (до земли 114КОм, 368Ом).
???????(zotac?) GTX460 (черная, матовая)|прогревалась, гребенка в кз.|предположительно неисправна микросхема apw7145 - 7 м 8 контакт звонится друг на друга
Gainward GTX460 (красная)|починено, продано|Обуглились элементы с нулевым сопротивлением и обозначением SLB (видимо примерно в роли предохранителеей). Обнаружено КЗ всех лапок транзисторов соответстующей фазы. перепаяна соотвествующая фаза с заменой подозрительных элементов.
Palit GTX460 Sonic (красная)|донор элементов|До выпаяивания ШИМ. Разные симпотомы сменяли друг друга:питание gpu было несколько минут, потом исчезало. gpu был горячий. Все фазы работали нормально -> не было питания на gpu. До выпаивания gpu: -> замкнуто 3.3v видеоплаты, напрямую приходящие с PCIe, на одну ногу кварца, очень странно -> странный шум по вольтажу на 2-х управляющих ногах ШИМа. Ичтоник шума - дорожка идущая по верхней стороне платы и уходящая в плату -> Кварц рабочий, но не активировался. Проверялось при выпаянном ШИМ. Выпаян gpu. Замыкание на плате на кварц исчезло. На gpu найдены контакты, сопротивлени которых до ножки кварца ~4Ом. На карте жжёные дорожки под чипом
*Tesla (9300 - 405) G9?, GT???*
XFX GTX280 1GB GDDR3 (чёрный) G200-300-A2|Запустилась лишь однажды|Был красный светодиод, до выпаивания транзистора Q502, который по идее отвечает за детектирование наличия дополнительно питания. После этого светодиод стал зелёный, но не определялась: система загружается со встроенным видео. Но 1 раз за пустилсь и через пару секунд монитор погас. При измерении есть питание на GPU, видеопамяти и 5v DVI. Быстро становится тёплая в зоне основных транзисторов питания. Сопротивление на С198 (возле GPU в строну разъёмов доп. питания) - 22Ом, на L8 - 500Ом.
Asus GTX280 1GB GDDR3 (чёрный) G200-302-A2|артефакты памяти, периодичеки "плавающее" КЗ|Плата идентична XFX GTX280. Сткртует, артефакты в BIOS (точки, не те символы). При подключение pcie x1 артефактов стало как будто больше. Q502 на месте. При последующем включении - запах гари и появилось КЗ на 6-м дросселе L8 (который не по питанию GPU) а также на конденсаторе С198. Периодически КЗ становится не полным исчезает и есть картика одновременно с запахом гари.
Leadtek GTS260 896MB GDDR3 (чёрный)|оказалась рабочая, проверялась нами в 2016 и продана в начале 2017|Дорожки такие же как на 280. При длительном использовании проблем не выявлно кроме возможно редких зависаний, возможно не от неё.
Asus GTS250 1GB GDDR3 (cиний)|Продана в сентябре 2016 после замены предохранителя|При старте на памяти нет питания. Нет контакта на предохранителе на 8А рядом с разъёмом дополнительного питания. При замыкании предохранителя есть старт, идёт ток порядка 1А. Предположительно это была единственная проьлема. Дополнительное питание используется только для памяти. Подозрительно низкое сопортивление до земли с ключа транзистора - плеча, отвечающего за соединение с землёй. Но может с ним и всё впорядке, т.к. непосредственно рядом с ШИМ памяти UP6101BU8 находится резистора между LGATE и GND. предохрантель заменен на ВП1 с аналогичными параметрами. починено. Тест на MSI 9642 был нестабилен, предположительно из-за нехватки питания с разъёма от мат. платы. На нормальной плате с тем же БП проблем нет - работает стабильно. продана
Asus GTS250 1GB GDDR3 (cиний)|донор, возможно живой gpu|карта от знакомого. который снял с нее множество элементов, втч шим, твердотельные конденсаторы, транзисторы. все поставлено назад, кроме пробитых транзисторов. Отсутствует шим памяти, и непропай по ключам неокотрых плеч GPU - включение без него привело к предположительному выходу из строя нескольких пдеч.
Asus GTS250 512MB GDDR3 (cиний)|Основная гипотеза - КЗ в/под gpu|Получена из сервиса. КЗ по питанию после дросселей, причём как по питанию GPU, так и по питанию памяти. Большие чёрные элементы eS8, на обратной стороне gpu - конденсаторы, не выпаивались. Исследование падение напряжений при токе порядка 1А, поданного на замкнутые элементы указывает на то что область замыкания близка к конденсаторам на обратной стороне gpu. Причём касается это как линии питани gpu (проверилось на самых больших конденсаторах под gpu) так и линии питания памяти (проверилось на вторых по размеру конденсаторах под gpu). НА обратной стороне чипа 1 сбитый элемент. Ясно, что это не причина КЗ, но надо иметь ввиду.
Zotac GTS250 512MB GDDR3 (синий)|Основная гипотеза - КЗ в/под gpu|На второй-третий раз исследований внезапно вырубился БП по защите. Что до этого - неизвестно. При последующих включениях бывал сильный запах. Иcтоник не был найден, было найдено просаживание по 3.3v pcie. Выпаяна линейная система питания, потенциально проблемные конденсаторы. КЗ по питанию после линейной системы - осталось. Сопротивление ооочень маленькое, при подаче 2 ампер ничего не греется. Замеры падений напряжений по дорожкам указывают на дырку в плате с оратной стороны gpu, предположительно кз в шарах или подложке. Есть сколы, но небольшие. Ранее в районе gpu в термопасте была найдена мелкая странная крошка металла (или кремния).
PNY 9800 512MB GDDR3 (зелёный)|отдана с редкими артефактами, работает|Редко были замечены трудноразличимые артефакты в виде точек. Долго работала и продолжает работать. Из тестов артефакты можно увидеть только в LightMark. отдана.
**AMD/ATI**
*Arctic Islands GCN-4 RX-4?? RX-5??*
Sapphire RX 480 8GB Nitro+(чёрный матовый)|ожидает микросхем на замену питания памяти|получена в ремонт, обнаружены повреждённые/сбитые Infeneon IR3553, Anpec APW8722A, ONsemi NTMFS4C10N, s1ah (два транзистора, общего назначения sot 363), smd - предохранитель на 10A. На 21 ноге EN ШИМа IR3567B должно появляться 3.3v, но его там нет поскольку на gate Q2604 нет приходит питание памяти, которое должно видимо  активироваться первым. При подаче внешнего питания на память - начинает работать. 
Sapphire RX 480 4GB Nitro+(чёрный матовый)|исследовать причины погасания при повышения уровня производиетльности|получена в ремонт,по первому тесту карта нормально работает на наименьшем пресете производительности, но немедленно отключается при смене пресета на более быстрый. Найденый сбитый или снятый элемент в ограничении тока ШИМа памяти. Стали появляться артефакты в текстовом режиме, тест памяти указал на 1 проблемный бит. Потом стали глючить сразу 2 модуля - U2500 и U2400.First problem at: 0x400, дальше 0x200 не работает, 0x600 работает и так по очереди. в положении переключателя ближе к gpu сброшен через ^C после Flash type: M25P40/c
Sapphire RX 470 4GB (чёрный матовый)|залить прогар, поставить 2.2Ом и возможно конденсаторы по питанию, которое фильтрует 2.2Ом|получена как "неремонтируемый прогар в стандартном месте". Ключи CHL8510/IR3537
*Southern Islands GCN-1 HD7750 - HD7970, R9 270, R9 280, R7 240, R7 250*
Asus R9 280x Direct CU II|повреждение GPU по питанию памяти| Сопротивление по памяти порядка 0.1Ом, но система питания памяти справляется и даже не греется. Зато греются все модули памяти H5GQ2H24AFR R0C (3ГГц) - на некоторых через секунду после включения нельзя держать палец, на других через 5 секунд. Определяется прошивальщиком, считывает BIOS без мусора. GPU 4 Ом, VDDCI 40 Ом. После снятия всех модулей памяти - сопротивление по пмаяти - 8 Ом и греется gpu.
HIS 280x 3g (синий)|Нечем заменить ШИМ, отдано|память H5GQ2H24AFR R0C (3ГГц) 60 Ом, VDDCI 25 Ом. низкое сопротивление на pwm2 У chill8228g
Gigabyte 7970 OC 3g (синий)|Починено, отдано в ноябре 2017|Прогар верхнего плеча смежслойнвм замыканием в 1Ом до земли. GPU 2Ом, память 150 Ом. Устранён прогар, снижения частоты и максимальное потребление прошивкой BIOS.
Gigabyte 7970 OC 3g (синий)|Обслужено, отдано в декабре 2017|Вырубалась под нагрузкой, каким-то образом было плохо приложено охлаждение GPU, никаких проблем.
MSI 7970 (коричневый)|нечем заменить шим chill8228g, возвращено без ремонта|Получена с КЗ 12v на чип.VDDCI 10 Ом, память 60 Ом. Убраны повреждённый ключ 4й фазы и сгоревше верхнее плечо Q510, после этого запустиись 2 и3 фазы питания, но через полминуты сгорела 5-я. Шим ведёт себя нестабильно. После полной замены 3х первых фаз - показывает попытку начала подачи питания, но на этом всё. потенциально требовал замены токоизмеритель (закотачил только после тыкания щупом)одной фазы не было.
MSI R7950 3GDDR5/OC Twin Frozr III(коричневая)|нечем заменить шим chill8228g, GPU возможно рабочий|Получена с диагнозом "нет изображения". С обратной стороны сбиты C2317,C2322,C2315,C2910 - все VMEM, c28 - pexvdd. Gpu - 3Ом, память 54Ом, питание PEX - 160Ом. Пришла с положением переключателя BIOS в позиции 2. В этом состоянии - при всех подключенных доп. питаниях система зависает без писков. С закороченным BIOS определяется. Выяснилось что, отсуствует питание памяти (только корткий подъём).в процессе замеров проблема исчезла, референснные замеры после этого: EN2(chill8228g)3.25V, MOD(CHL8510)12.2V, BOOT(там же)5.75V(по мультимеру) (осциллографом - типичная форма выхода шим), на память 1.6V. Проблема снова появилась - EN2(chill8228g)3.3V, boot 4.4V, на память 0.3V. Предположительно виноват chill8228g, выпаян. Сопротивление на дорожке к mosfet driver памяти пришло к более типичному (от 6 к 7МОм). Однако с новым ШИМ питание на нём есть (3.3v), enable есть (3.3v), сопротивление GPU - в норме (2.9Ом) и внутренние 1.8V ШИМ тоже даёт. А напряжение на GPU - чистый ноль. Никаких попыток управления ключами через PWM - нет - смотрел осциллографом. ШИМ выдаёт на все PWM ровные 3.3v, что для установленных ключей CHL8510 обозначает "PWM Tri‐Level Hi Value" - то есть "закрыть оба плеча".
Sapphire HD 7950 3GDDR5(коричневая) - без охлаждения|нечем заменить шим chill8228g, был пробой верхнего плеча|Замыкание по 3.3v. Сгоревшие верхние плечи. В chill8228g было замыкание по pin 1.
Sapphire HD 7950 3GDDR5(коричневая)|Проблем нет, продано.|Получена с диагнозом "нет изображения, прогрев не помог". Есть следы от прогрева. На практике вырубалась из-за отсутствия термопасты. ocl_memtest стартует нестабильно, но это похоже на проблему opencl-драйверов. Других проблем не обнаружено - работает. Тестирует Женя. 
MSI R7 370 GAMING 2G (чёрный матовый)|Плата наверное рабочая, хотя паяны элементы, можно посадить новый чип|Получена с КЗ по чипу, чип снят.
???? R7870 2GDDR5(синий)|кз по питанию чипа, возвращено без ремонта|
PowerColor R7850 1GDDR5(красная)|Починено, продано в октябре 2017| Все напряжения есть, но Video Bios не читается при загрузке и не определяется PCIe-устройство. Обнаружено отсуствие POK на ULDropOut APL5932A и странные 0,8 V на выходе (аналог 1,8). После замены резистора-делителя - работает. Вентилятор не всегда стартовал, перестало проявляться после того как при попытке его вынуть он чуть чуть сдвинулся. Система из ШИМ и двойного транзистора выдаёт 0.955v.
Sapphire HD7770 1Gb gddr5 (синяя)|возвращено без ремонта(Зеленоград)|Все напряжения есть, но Video Bios не читается при загрузке и не определяется PCIe-устройство. ULDropOut gs7103 выдвет ожжиданемые 1,8V, но имеет маленькое сопротивление по выходу - 11Ом. Система из ШИМ и двойного транзистора выдаёт 0.96v (для PCIE судя по расположению, совпадает с аналогами). Ещё одно питание - 0.9v (контроллер памяти судя по расположению - на аналогах 0.85v-0.95v). возвращено без ремонта  - предварительный дигноз - низкое сопротивление одной системы питаня gpu

#### Northern Islands HD6450, HD6570, HD6670, HD6790 - HD6990, HD64xxM, HD67xxM, HD69xxM, HD7450 - HD7670
##### MSI R6850 1GDDR5(коричневая)
Получена с описанием "не работет поле того как подключили монитор на горячую". Стартует, показывает по VGA, но не определяет edid монитора. Проблема оказалась в драйвере fglrx. C radeon разрешение по VGA подхватывется. Так что карта полностью работает, никаких проблем нет. Продано.

#### sapphire R6850 1GDDR5(утрамарин)
не проходит тесты памяти, визуальные артефакты похожи на нерабочесть модуля, либо контроллера памяти. возвращено без ремонта
##### MSI AMD HD6870 1GDDR5(коричневая)
При попытке использовать ATI-драйвера - виснет через разное небольшое время. Обнаружен отвал конденсатора C304 рядом с микросхемой линейного стабилизатора uP7701u8, расположенного между VOUT и FB ногами. Замеры ёмкости - 0.6nF при 0.560 между щупами. 3d иногда запускается, но через некоторое время карта останавливается, исччезает напряжение на gpu, из-за того что перестаёт подаваться сигнал enable на основной ШИМ. Дальнейшие измерения показали что его исчезновение по всей видимости вызвано открытием транзистора Q210. Внезапно проблема перестала проявляться, карта работает, вероятно проблема в какой-то защитной схеме, которая выключает сигнал Enable. Тестировалась около 3-х месяцев, проблем не возникло. Однако после очередной замены системы охлаждения после запуска Furmark стали появляться проблемы с выводом картинки (сдвиг отобрааемой зоны и мусор). Unigine Heaven тоже начинает выдавать полосы на экран (драйвер radeon).

#### Evergreen HD5430 - HD5970, Some HD 6xxx
##### XFX HD6770 1GDDR5(чёрная)
Карта стартует нестабильно, обычно вырубается (исчезает напряжение на gpu и памяти) почти сразу после старта.  При запуске с закороченным BIOS на gpu стабильно 1.25v и можно прошить по сети. При запуске с незакороченным BIOS напряжение растёт до 1.3 (в это время карта работает) а потом падает в ноль. Перепрошивка BIOS на меньшее напряжение не дала результата

#### Radeon R700 HD4330 - HD5165, HD5xxV
##### HD 4870 1GB GDDR5 (красная)
Иногда один модуль памяти начинает выдавать мусор (pattern 0B10101010). Адрес при тестировании от начала - порядка 0x307, 0x308. Модули Hynix H5GQ1H24MJR T0C. Тыканием щупа включенного осциллографа на точку имеющую 1.6Ком  удалось вызвать помехи на модуле и локализовался модуль U4. замена на аналогичный сип с донора (470 с прогаром) не помогло, вызывая редкие артефакты. вернули снятый прежде чеп памяти, карта работает и отдана

#### Radeon R600 (HD 2xxx, HD 3xxx) Seriesse
##### HIS HD 3450 (синяя, мелкая)
Всегда работала и работает
