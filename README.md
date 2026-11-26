# at&t家宽vps 怎么买不踩坑：SixtyNet 全套餐价格、CN2 回程与端口限制、2C4G 和 4C8G 的真实分界（附竞品价格对照）

at&t家宽vps 的价格带不算宽。人民币计价的国内商家，100Mbps 档 ¥149/月起，200Mbps 档 188 元/月上下；美元计价的海外商家，50Mbps 独享档 $35.99/月。带宽基本就 50、100、200Mbps 三档，配置从 2C2G 到 8C16G，差价主要来自带宽和 IP 属性。

SixtyNet 站在偏低价的一头：$20/月起，年付 $140 起，提供 AT&T Mobility 双 ISP 住宅 IP、10Gbps 端口、1Tbps 高防，2024 年的第三方测评记录其回程走 CN2 GIA。这套组合在同类里少见，代价后面会讲清楚：80/443 端口关闭、信用卡支付暂停、退款窗口只有 3 天。

> 多数人买 AT&T 家宽 VPS 只是为了一个干净的美国住宅 IP 环境，跑 API、反代、养号、看流媒体。这种情况选 SixtyNet 的 Residential-STARTER 就够：2 核 2G、40G NVMe、5TB 流量，年付 $140（标价 $180），月付约 $20 起。要装 Windows 或跑重一点的活，再往上看 4C4G 和 8C8G。
> 👉 [查看 SixtyNet 住宅套餐年付价与当前库存](https://sixtynet.net/aff.php?aff=39)

## SixtyNet 全套餐对比

官网当前把产品分成住宅、移动、LAX 机房、存储四条线。住宅系列才是带 AT&T 住宅 IP 的那批，也是搜 at&t家宽vps 的人该看的。全系 KVM 虚拟、AMD EPYC、DDR4 3200、NVMe，机房在洛杉矶 Coresite LA2。

| 套餐 | 配置 | 流量 | 价格（年付） | 购买 |
| --- | --- | --- | --- | --- |
| Residential-STARTER | 2 核 / 2G / 40G NVMe | 5TB | $140（标价 $180） | [开通](https://sixtynet.net/aff.php?aff=39&pid=25) |
| Residential-MICRO | 4 核 / 4G / 80G NVMe | 10TB | $340（标价 $420） | [开通](https://sixtynet.net/aff.php?aff=39&pid=26) |
| Residential-MEDIUM | 8 核 / 8G / 160G NVMe | 20TB | $740（标价 $900） | [开通](https://sixtynet.net/aff.php?aff=39&pid=28) |
| Residential-LARGE | 8 核 / 16G / 320G NVMe | 40TB | $1,540（标价 $1,860） | [开通](https://sixtynet.net/aff.php?aff=39&pid=27) |
| Mobile-STARTER | 2 核 / 2G / 40G NVMe | 50GB 移动流量 | $50 | [开通](https://sixtynet.net/aff.php?aff=39&pid=33) |
| Mobile-MICRO | 4 核 / 4G / 80G NVMe | 50GB 移动流量 | $100 | [开通](https://sixtynet.net/aff.php?aff=39&pid=34) |

住宅全系 10Gbps 端口、1Tbps DDoS 防御，年付比月付省 17%，住宅系列最高省 22%。Mobile 系列流量只有 50GB，是按移动网络流量计费的，别拿它当住宅套餐买。

LAX 系列走的是普通机房 IP，不带住宅属性，但 80/443 是开的，能建站：

| 套餐 | 配置 | 流量 | 价格（年付） | 购买 |
| --- | --- | --- | --- | --- |
| LAX-STARTER | 2 核 / 2G / 40G | 5TB | $200 | [开通](https://sixtynet.net/aff.php?aff=39&pid=21) |
| LAX-MICRO | 4 核 / 4G / 80G | 10TB | $400 | [开通](https://sixtynet.net/aff.php?aff=39&pid=22) |
| LAX-MEDIUM | 8 核 / 8G / 160G | 20TB | $800 | [开通](https://sixtynet.net/aff.php?aff=39&pid=23) |
| LAX-LARGE | 8 核 / 16G / 320G | 40TB | $1,600 | [开通](https://sixtynet.net/aff.php?aff=39&pid=24) |
| LAX-Storage-500G | 4 核 / 4G / 500G RAID10 | 10TB | $400 | [开通](https://sixtynet.net/aff.php?aff=39&pid=19) |
| LAX-Storage-1TB | 8 核 / 8G / 1TB RAID10 | 15TB | $700 | [开通](https://sixtynet.net/aff.php?aff=39&pid=20) |

以上价格来自公开测评整理的资料，月付价在早期测评里记为 $20/$40/$80/$160 起，与年付折算口径不同。下单前以结账页显示的实时价格为准，这类商家调价和改配置不算罕见。

## AT&T 家宽 VPS 到底慢在哪、快在哪

先说物理事实。AT&T 家宽的 IP 归属是真的，网络没有中国优化也是真的。公开的第三方体检报告里，AT&T 家宽到国内三网的大包延迟普遍在 160–200ms，北京电信 166ms、联通 183ms、移动 201ms，个别节点能到 280ms 甚至 425ms。闲时也有 5%–7% 丢包，晚高峰直连断流是常见现象。

回程路由能解释这件事。AT&T 家宽的典型回程是三段式：电信走 AT&T 接 163，联通走 AT&T 或 Verizon 接 4837，移动走 Arelion 接 CMI。全程没有 CN2、没有 CMI 专线，就是普通国际互联，所以延迟下不来。

SixtyNet 的差异在这里。2024 年第三方测评记录它的三网回程强制走 CN2 GIA 的 59.43 段，去程三网直连美国西海岸。如果现在还是这个路由，国内访问的稳定性会比纯落地型家宽好一截，不需要额外配中转。这一点必须自己确认：路由是会变的，两年前的测评不能当今天的保证。

纯落地型家宽就得配中转。机器在加州，洛杉矶线路机中转过去只要 3–5ms，50Mbps 能拉满。这时你的实际成本是家宽机器加一台洛杉矶线路机，不是标价那个数。

还有个容易略过的操作细节：别把带宽跑满。50Mbps 的机器限到 45Mbps，200Mbps 限到 190Mbps，重传能降到接近 0，传输质量明显不同。公开测评里无限速跑 200Mbps 时有 26 次重传，限到 190Mbps 后重传归零。这条对任何品牌的 AT&T 家宽都适用。

## 2C4G 和 4C8G 的分界线是装不装 Windows

这条判断在 ATTVPS 的测评里有直接依据：2C4G 能轻松跑大部分 API、反代、静态博客、轻量数据库；4C8G 起步才适合装 Windows。微软官方给的 Windows 最低硬件要求就是 2C4G，但那只是“能装进去”，跑起来会卡。

放到 SixtyNet 的档位上：Residential-STARTER 是 2C2G，比 2C4G 还低一档，跑 Linux 做环境、跑脚本、做反代都够，装 Windows 不建议。真要 Windows，从 Residential-MICRO 的 4C4G 起步，想舒服就上 8C8G。

按场景对应：

- 只跑 API、反代、静态博客、轻量数据库：Residential-STARTER 够用
- 要装 Windows：至少 Residential-MICRO，推荐 Residential-MEDIUM
- 要跑 200Mbps 级别的拉流：SixtyNet 住宅系列没有按带宽分档，10Gbps 端口是共享口径，实际能跑多少取决于路由和限速设置，这一点它不像干杯云那样明码标 200Mbps
- 只养号做环境：Residential-STARTER 最便宜，也最不容易浪费

## 三笔大多数人不会算的成本

**第一笔是年付风险。** SixtyNet 的退款窗口是 3 天，行业常见的是 30 天。3 天足够你开机、跑脚本、看路由和 IP 属性，不够你验证一个月的稳定性。公开测评对这类家宽产品的一致建议是先月付，跑稳了再续长期。家宽产品受真实线路和库存限制，售罄是常态，看到有货就冲动年付，退不了的时候很被动。

👉 [先用月付开一台 Residential-STARTER，3 天内可退](https://sixtynet.net/aff.php?aff=39&pid=25)

**第二笔是中转成本。** 如果你买的是不带中国优化的家宽（AaITR、NodeMach、干杯云、ATTVPS 都属于这类），实际总支出要加一台洛杉矶线路机，每月多出几十到上百元。SixtyNet 宣称 CN2 GIA 回程，这笔可能省掉，但省掉的前提是路由没变。

**第三笔是端口。** 25 端口在 AT&T 家宽产品上基本不通，批量发邮件这条路直接堵死，两篇独立测评都提到这一点。SixtyNet 的住宅系列还额外关了 80 和 443，意味着不能拿来跑对外网站。要建站得买 LAX 系列，那是机房 IP，没有住宅属性。

👉 [对照 SixtyNet 住宅与 LAX 两条产品线，确认端口和系统支持](https://sixtynet.net/aff.php?aff=39)

## 哪些人不需要 AT&T 家宽 VPS

直播推流直连不行，200ms 以上的延迟对推流稳定性影响太大，正确做法是用家宽机器做账号环境，推流走洛杉矶优化线路中转。高性能计算和大流量建站也不合适，同样的钱买普通 VPS 配置高得多。批量发邮件前面说过了，25 端口不通。

还有一类人容易买错：只需要一个美国 IP 看流媒体、临时测环境。这种情况 SixtyNet 的 Mobile 系列年付 $50 就够，或者 AaITR 的 ¥24/月动态 NAT，不用上住宅静态套餐。

## 竞品价格带对照

| 品牌 | 定位 | 配置 | 带宽 / 流量 | 公开测评列出的价格 |
| --- | --- | --- | --- | --- |
| NodeMach（原 VIRCS） | AT&T 静态独享家宽，支持 Windows | 4C / 8G / 50G NVMe | 50Mbps 独享 / 无限 | $35.99/月 |
| AaITR | AT&T / Frontier 静态家宽 | 2C / 2G / 25G SSD | 100Mbps / 2000GB 双向 | ¥149/月起 |
| AaITR 动态 NAT | 共享动态 IP，每日更换 | 1C / 512M / 8G | 100Mbps / 1000GB | ¥24/月起 |
| 干杯云 | AT&T 家宽 / 商宽，双栈 | 资料未列出 | 200Mbps / 无限 | 188 元/月 |
| ATTVPS | AT&T 家宽，纯落地定位 | 2C4G 起 | 50Mbps 独享 / 无限 | 资料未列出 |

NodeMach 胜在配置高、明确支持 Windows，$35.99/月买 4C8G 加无限流量，适合要跑重活的人。AaITR 的静态套餐 100Mbps、2000GB 双向，¥149/月起，年付八折折算约 ¥120/月，适合需要固定 IP 长期养号的场景。干杯云的 200Mbps 无限流量是这几家里带宽最高的，188 元/月对应的是拉流需求。ATTVPS 定位纯落地，50Mbps 独享无限流量，得自己配中转。

SixtyNet 的位置在它们中间偏下：价格最低，IP 属性是 AT&T Mobility 的双 ISP 住宅段，回程宣称 CN2 GIA，同时带高防。它的短板是端口限制和退款窗口，长板是价格和不用额外配中转（前提是路由成立）。

## 下单前确认这几件事

只要一个干净的美国住宅 IP 环境，跑 Linux、不建站、不发邮件，选 Residential-STARTER，年付 $140。要装 Windows 或跑多个服务，Residential-MICRO 起步。要建站，别买住宅系列，去看 LAX。只要一个临时美国 IP，Mobile 系列年付 $50。

下单前有四件事值得花两分钟确认：库存状态（住宅系列经常售罄）、IP 是否独享（SixtyNet 标的是独享住宅 IP，但结账页值得再看一眼）、3 天退款怎么算（从开通算还是从付款算）、当前支付方式（公开资料显示信用卡支付因风控暂停，结账页会列出可用选项，国内用户尤其要先看清楚）。路由是否仍走 CN2 GIA，可以开工单问，或者买最便宜的月付自己跑一遍 traceroute。

👉 [按这三档对照 SixtyNet 当前在售套餐与价格](https://sixtynet.net/aff.php?aff=39)
