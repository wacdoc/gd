# Tog am frithealaiche puist SMTP agad fhèin

## roimh-ràdh

Faodaidh SMTP seirbheisean a cheannach gu dìreach bho luchd-reic sgòthan, leithid:

* [Amazon SES SMTP](https://docs.aws.amazon.com/ses/latest/dg/send-email-smtp.html)
* [Puing post-d Ali Cloud](https://www.alibabacloud.com/help/directmail/latest/three-mail-sending-methods)

Faodaidh tu cuideachd am frithealaiche puist agad fhèin a thogail - cur air falbh gun chrìoch, cosgais iomlan ìosal.

Gu h-ìosal, bidh sinn a’ sealltainn ceum air cheum mar a thogas sinn am frithealaiche puist againn fhèin.

## Taghadh frithealaiche

Feumaidh am frithealaiche SMTP fèin-aoigheachd IP poblach le puirt 25, 456, agus 587 fosgailte.

Tha sgòthan poblach a chleachdar gu cumanta air na puirt sin a bhacadh gu bunaiteach, agus dh’ fhaodadh gum bi e comasach am fosgladh le bhith a’ toirt seachad òrdugh obrach, ach tha e gu math trioblaideach às deidh a h-uile càil.

Tha mi a 'moladh ceannach bho òstair aig a bheil na puirt sin fosgailte agus a' toirt taic do bhith a 'stèidheachadh ainmean fearainn air ais.

An seo, tha mi a’ moladh [Contabo](https://contabo.com) .

Tha Contabo na sholaraiche aoigheachd stèidhichte ann am Munich, a’ Ghearmailt, a chaidh a stèidheachadh ann an 2003 le prìsean gu math farpaiseach.

Ma roghnaicheas tu Euro mar airgead ceannach, bidh a’ phrìs nas saoire (bidh frithealaiche le cuimhne 8GB agus 4 CPUs a’ cosg timcheall air 529 yuan gach bliadhna, agus tha a’ chiad chìs stàlaidh an-asgaidh airson aon bhliadhna).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/UoAQkwY.webp)

Nuair a chuireas tu òrdugh, `prefer AMD` , agus bidh coileanadh nas fheàrr aig an fhrithealaiche le AMD CPU.

Anns na leanas, bheir mi VPS Contabo mar eisimpleir gus sealltainn mar a thogas tu am frithealaiche puist agad fhèin.

## Suidheachadh siostam Ubuntu

Is e an siostam obrachaidh an seo Ubuntu 22.04

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/smpIu1F.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/m7Mwjwr.webp)

Ma sheallas am frithealaiche air ssh `Welcome to TinyCore 13!` (mar a chithear san fhigear gu h-ìosal), tha e a’ ciallachadh nach deach an siostam a chuir a-steach fhathast. Feuch an dì-cheangail thu ssh agus fuirich beagan mhionaidean gus logadh a-steach a-rithist.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/-qKACz9.webp)

Nuair a nochdas `Welcome to Ubuntu 22.04.1 LTS` , tha an tòiseachadh deiseil, agus faodaidh tu leantainn air adhart leis na ceumannan a leanas.

### [Roghainneil] Tòisich an àrainneachd leasachaidh

Tha an ceum seo roghainneil.

Airson goireasachd, chuir mi stàladh agus rèiteachadh siostam bathar-bog ubuntu ann an [github.com/wactax/ops.os/tree/main/ubuntu](https://github.com/wactax/ops.os/tree/main/ubuntu) .

Ruith an àithne a leanas airson a stàladh le aon bhriogadh.

```
bash <(curl -s https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

Luchd-cleachdaidh Sìneach, feuch an cleachd thu an àithne a leanas na àite, agus thèid an cànan, sòn ùine, msaa a shuidheachadh gu fèin-ghluasadach.

```
CN=1 bash <(curl -s https://ghproxy.com/https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

### Tha Contabo a’ comasachadh IPV6

Dèan comas air IPV6 gus an urrainn do SMTP cuideachd puist-d a chuir le seòlaidhean IPV6.

deasaich `/etc/sysctl.conf`

Atharraich no cuir ris na loidhnichean a leanas

```
net.ipv6.conf.all.disable_ipv6 = 0
net.ipv6.conf.default.disable_ipv6 = 0
net.ipv6.conf.lo.disable_ipv6 = 0
```

Lean air adhart leis [an oideachadh contabo: A’ cur ceangal IPv6 ris an t-seirbheisiche agad](https://contabo.com/blog/adding-ipv6-connectivity-to-your-server/)

Deasaich `/etc/netplan/01-netcfg.yaml` , cuir beagan loidhnichean ris mar a chithear san fhigear gu h-ìosal (tha na loidhnichean sin aig faidhle rèiteachaidh bunaiteach Contabo VPS mu thràth, dìreach cuir às dhaibh).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/5MEi41I.webp)

An uairsin `netplan apply` gus an rèiteachadh atharraichte a thoirt gu buil.

Às deidh don rèiteachadh a bhith soirbheachail, faodaidh tu `curl 6.ipw.cn` a chleachdadh gus seòladh ipv6 den lìonra a-muigh agad fhaicinn.

## Dèan clon air na h-ops stòr rèiteachaidh

```
git clone https://github.com/wactax/ops.soft.git
```

## Cruthaich teisteanas SSL an-asgaidh airson an ainm fearainn agad

Gus post a chuir a-steach feumaidh teisteanas SSL airson crioptachadh agus soidhnigeadh.

Bidh sinn a’ cleachdadh [acme.sh](https://github.com/acmesh-official/acme.sh) gus teisteanasan a ghineadh.

Tha acme.sh na inneal soidhnidh teisteanais fèin-ghluasadach le còd fosgailte,

Cuir a-steach an taigh-bathair rèiteachaidh ops.soft, ruith `./ssl.sh` , agus thèid pasgan `conf` a chruthachadh anns **an eòlaire àrd** .

Lorg an solaraiche DNS agad bho [acme.sh dnsapi](https://github.com/acmesh-official/acme.sh/wiki/dnsapi) , deasaich `conf/conf.sh` .

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Qjq1C1i.webp)

An uairsin ruith `./ssl.sh 123.com` gus teisteanasan `123.com` agus `*.123.com` a ghineadh airson an ainm fearainn agad.

Cuiridh a’ chiad ruith [acme.sh](https://github.com/acmesh-official/acme.sh) an sàs gu fèin-obrachail agus cuiridh e gnìomh clàraichte airson ùrachadh fèin-ghluasadach. Chì thu `crontab -l` , tha loidhne mar a leanas ann.

```
52 0 * * * "/mnt/www/.acme.sh"/acme.sh --cron --home "/mnt/www/.acme.sh" > /dev/null
```

Tha an t-slighe airson an teisteanais a chaidh a chruthachadh rudeigin mar `/mnt/www/.acme.sh/123.com_ecc。`

Gairmidh ath-nuadhachadh teisteanais sgriobt `conf/reload/123.com.sh` , deasaich an sgriobt seo, faodaidh tu òrdughan leithid `nginx -s reload` a chuir ris gus an tasgadan teisteanais de thagraidhean co-cheangailte ùrachadh.

## Tog frithealaiche SMTP le chasquid

tha [chasquid](https://github.com/albertito/chasquid) na fhrithealaiche SMTP stòr fosgailte sgrìobhte ann an cànan Go.

Mar neach-ionaid airson seann phrògraman frithealaiche puist leithid Postfix agus Sendmail, tha chasquid nas sìmplidh agus nas fhasa a chleachdadh, agus tha e cuideachd nas fhasa airson leasachadh àrd-sgoile.

Thèid Run `./chasquid/init.sh 123.com` a chuir a-steach gu fèin-ghluasadach le aon bhriogadh (cuir an t-ainm fearainn agad an àite 123.com).

## Dèan rèiteachadh air ainm-sgrìobhte post-d DKIM

Tha DKIM air a chleachdadh gus ainmean post-d a chuir gus casg a chuir air litrichean bho bhith air an làimhseachadh mar spama.

Às deidh don àithne ruith gu soirbheachail, thèid iarraidh ort an clàr DKIM a shuidheachadh (mar a chithear gu h-ìosal).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/LJWGsmI.webp)

Dìreach cuir clàr TXT ris an DNS agad (mar a chithear gu h-ìosal).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/0szKWqV.webp)

## Thoir sùil air inbhe seirbheis & logaichean

 `systemctl status chasquid` Faic inbhe seirbheis.

Tha staid an obrachaidh àbhaisteach mar a chithear san dealbh gu h-ìosal

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/CAwyY4E.webp)

 `grep chasquid /var/log/syslog` no `journalctl -xeu chasquid` an loga mearachd fhaicinn.

## Cuir air ais rèiteachadh ainm fearainn

Tha an t-ainm àrainn cùil gus leigeil leis an t-seòladh IP a bhith air a rèiteachadh chun an ainm àrainn co-fhreagarrach.

Le bhith a’ suidheachadh ainm fearainn cùil faodaidh sin casg a chuir air puist-d bho bhith air an comharrachadh mar spama.

Nuair a gheibhear am post, nì am frithealaiche a tha a’ faighinn mion-sgrùdadh ainm fearainn air ais air seòladh IP an fhrithealaiche cur gus dearbhadh a bheil ainm fearainn cùil dligheach aig an t-seirbheisiche a tha a’ cur.

Mura h-eil ainm àrainn cùil aig an t-seirbheisiche a tha a’ cur a-steach no mura h-eil an t-ainm fearainn cùil a’ freagairt ri seòladh IP an fhrithealaiche cur, faodaidh am frithealaiche a gheibh am post-d aithneachadh mar spama no a dhiùltadh.

Tadhail air [https://my.contabo.com/rdns](https://my.contabo.com/rdns) agus rèiteachadh mar a chithear gu h-ìosal

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/IIPdBk_.webp)

Às deidh dhut an t-ainm àrainn cùil a shuidheachadh, cuimhnich gun cuir thu rèiteachadh air adhart an t-ainm àrainn ipv4 agus ipv6 chun t-seirbheisiche.

## Deasaich ainm òstair chasquid.conf

Atharraich `conf/chasquid/chasquid.conf` gu luach an ainm àrainn cùil.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/6Fw4SQi.webp)

An uairsin ruith `systemctl restart chasquid` gus an t-seirbheis ath-thòiseachadh.

## Cùl-taic conf gu stòr git

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Fier9uv.webp)

Mar eisimpleir, bidh mi a’ cumail suas am pasgan conf chun phròiseas github agam fhèin mar a leanas

Cruthaich taigh-bathair prìobhaideach an toiseach

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ZSCT1t1.webp)

Cuir a-steach an eòlaire conf agus cuir a-steach don taigh-bathair

```
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin git@github.com:wac-tax-key/conf.git
git push -u origin main
```

## Cuir ris an t-seoladair

ruith

```
chasquid-util user-add i@wac.tax
```

Faodar an neach a chuir ris

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/khHjLof.webp)

### Dèan cinnteach gu bheil am facal-faire air a shuidheachadh ceart

```
chasquid-util authenticate i@wac.tax --password=xxxxxxx
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/e92JHXq.webp)

Às deidh dhut an cleachdaiche a chuir ris, thèid `chasquid/domains/wac.tax/users` ùrachadh, cuimhnich gun cuir thu a-steach e chun taigh-bathair.

## DNS cuir clàr SPF ris

Tha SPF (Frèam Poileasaidh Luchd-cuiridh) na theicneòlas dearbhaidh post-d air a chleachdadh gus casg a chuir air foill post-d.

Bidh e a’ dearbhadh dearbh-aithne neach a chuir post le bhith a’ dèanamh cinnteach gu bheil seòladh IP an neach a chuir e a’ freagairt ri clàran DNS an ainm fearainn a tha e ag ràdh a tha, a’ cur casg air luchd-foill bho bhith a’ cur puist-d meallta.

Le bhith a’ cur clàran SPF a-steach faodaidh sin casg a chuir air puist-d bho bhith air an comharrachadh mar spama cho mòr ‘s as urrainn.

Mura h-eil am frithealaiche ainm fearainn agad a’ toirt taic do sheòrsa SPF, dìreach cuir clàr seòrsa TXT ris.

Mar eisimpleir, tha an SPF de `wac.tax` mar a leanas

`v=spf1 a mx include:_spf.wac.tax include:_spf.google.com ~all`

SPF airson `_spf.wac.tax`

`v=spf1 a:smtp.wac.tax ~all`

Thoir an aire gu bheil mi air a bhith `include:_spf.google.com` an seo, tha seo air sgàth gun rèiteachaidh mi `i@wac.tax` mar an seòladh cur ann am bogsa puist Google nas fhaide air adhart.

## rèiteachadh DNS DMARC

Is e DMARC an giorrachadh de (Dearbhadh Teachdaireachd stèidhichte air Fearann, Aithris & Co-chòrdadh).

Tha e air a chleachdadh gus breaban SPF a ghlacadh (is dòcha air adhbhrachadh le mearachdan rèiteachaidh, no gu bheil cuideigin eile a’ leigeil a-mach gur e thusa spam a chuir).

Cuir clàr TXT `_dmarc` ,

Tha an susbaint mar a leanas

```
v=DMARC1; p=quarantine; fo=1; ruf=mailto:ruf@wac.tax; rua=mailto:rua@wac.tax
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/k44P7O3.webp)

Tha brìgh gach paramadair mar a leanas

### p (Poileasaidh)

A’ nochdadh mar a làimhsicheas tu puist-d a dh’ fhàilnicheas dearbhadh SPF (Sender Policy Framework) no DKIM (DomainKeys Aithnichte Mail). Faodar am paramadair p a shuidheachadh gu aon de thrì luachan:

* gin: Chan eil gnìomh sam bith air a dhèanamh, chan eil ach an toradh dearbhaidh air a thoirt air ais don neach a chuir e tron ​​​​inneal aithris post-d.
* Cuarantine: Cuir am post nach deach seachad air an dearbhadh a-steach don phasgan spama, ach nach diùlt am post gu dìreach.
* diùlt: Diùlt gu dìreach puist-d a dh'fhàillig dearbhadh.

### fo (Roghainnean fàilligeadh)

A’ sònrachadh na tha de dh’fhiosrachadh air a thilleadh leis an inneal aithris. Faodar a shuidheachadh gu aon de na luachan a leanas:

* 0: Dèan aithris air toraidhean dearbhaidh airson a h-uile teachdaireachd
* 1: Na innis ach teachdaireachdan a dh'fhàillig an dearbhadh
* d: Na dèan aithris ach air fàilligidhean dearbhaidh ainm fearainn
* s: thoir cunntas air fàilligidhean dearbhaidh SPF a-mhàin
* l: Na dèan ach aithris air fàilligidhean dearbhaidh DKIM

### rua & ruf

* rua (Ag aithris URI airson aithisgean Iomlan): Seòladh post-d airson aithisgean iomlan fhaighinn
* ruf (Ag aithris URI airson aithisgean Foireansach): seòladh puist-d gus aithisgean mionaideach fhaighinn

## Cuir clàran MX ris gus puist-d a chuir air adhart gu Google Mail

Leis nach b’ urrainn dhomh bogsa-puist corporra an-asgaidh a lorg a bheir taic do sheòlaidhean uile-choitcheann (Catch-All, gheibh mi puist-d sam bith a chaidh a chuir chun ainm fearainn seo, gun chuingealachaidhean air ro-leasachain), chleachd mi chasquid airson a h-uile post-d a chuir air adhart chun bhogsa puist Gmail agam.

**Ma tha am bogsa puist gnìomhachais pàighte agad fhèin, feuch nach atharraich thu am MX agus leum air a’ cheum seo.**

Deasaich `conf/chasquid/domains/wac.tax/aliases` , cuir am bogsa puist air adhart

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/OBDl2gw.webp)

`*` a’ comharrachadh a h-uile post-d, is `i` ro-leasachan seòladh puist-d an neach-cleachdaidh a chaidh a chruthachadh gu h-àrd. Gus post a chuir air adhart, feumaidh gach neach-cleachdaidh loidhne a chuir ris.

An uairsin cuir ris a ’chlàr MX (bidh mi a’ comharrachadh gu dìreach seòladh an ainm fearainn cùil an seo, mar a chithear sa chiad loidhne san fhigear gu h-ìosal).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/7__KrU8.webp)

Às deidh an rèiteachadh a bhith deiseil, faodaidh tu seòlaidhean puist-d eile a chleachdadh gus puist-d a chuir gu `i@wac.tax` agus `any123@wac.tax` gus faicinn am faigh thu puist-d ann an Gmail.

Mura h-eil, thoir sùil air log chasquid ( `grep chasquid /var/log/syslog` ).

## Cuir post-d gu i@wac.tax le Google Mail

Às deidh do Google Mail am post fhaighinn, bha mi gu nàdarrach an dòchas freagairt le `i@wac.tax` an àite i.wac.tax@gmail.com.

Tadhail air [https://mail.google.com/mail/u/1/#settings/accounts](https://mail.google.com/mail/u/1/#settings/accounts) agus briog air "Cuir seòladh puist-d eile ris".

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/PAvyE3C.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/_OgLsPT.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/XIUf6Dc.webp)

An uairsin, cuir a-steach an còd dearbhaidh a fhuaireadh tron ​​​​phost-d a chaidh a chuir air adhart.

Mu dheireadh, faodar a shuidheachadh mar an seòladh teachdaiche bunaiteach (còmhla ris an roghainn freagairt leis an aon sheòladh).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/a95dO60.webp)

San dòigh seo, tha sinn air crìoch a chuir air stèidheachadh frithealaiche puist SMTP agus aig an aon àm cleachdaidh sinn Google Mail gus puist-d a chuir agus fhaighinn.

## Cuir post-d deuchainn gus dèanamh cinnteach a bheil an rèiteachadh soirbheachail

Cuir a-steach `ops/chasquid`

Ruith `direnv allow` eisimeileachd a chuir a-steach (chaidh direnv a chuir a-steach sa phròiseas tòiseachaidh aon-iuchrach roimhe agus chaidh dubhan a chuir ris an t-slige)

ruith an uairsin

```
user=i@wac.tax pass=xxxx to=iuser.link@gmail.com ./sendmail.coffee
```

Tha brìgh nam paramadairean mar a leanas

* cleachdaiche: ainm-cleachdaidh SMTP
* pas: facal-faire SMTP
* gu: neach-faighinn

Faodaidh tu post-d deuchainn a chuir.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ae1iWyM.webp)

Thathas a’ moladh Gmail a chleachdadh gus puist-d deuchainn fhaighinn gus dèanamh cinnteach a bheil na rèiteachaidhean soirbheachail.

### crioptachadh àbhaisteach TLS

Mar a chithear san fhigear gu h-ìosal, tha a’ ghlas bheag seo ann, a tha a’ ciallachadh gun deach an teisteanas SSL a chomasachadh gu soirbheachail.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/SrdbAwh.webp)

An uairsin cliog air "Seall Post-d tùsail"

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/qQQsdxg.webp)

### DKIM

Mar a chithear san fhigear gu h-ìosal, tha duilleag puist tùsail Gmail a’ taisbeanadh DKIM, a tha a’ ciallachadh gu bheil an rèiteachadh DKIM soirbheachail.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/an6aXK6.webp)

Thoir sùil air an Fhuaras ann an ceann a’ phuist-d thùsail, agus chì thu gur e IPV6 an seòladh neach-cuiridh, a tha a’ ciallachadh gu bheil IPV6 cuideachd air a rèiteachadh gu soirbheachail.
