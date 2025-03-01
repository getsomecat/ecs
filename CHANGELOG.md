# CHANGELOG

# 主要变化

2023.10.03

- 修复sysbench安装过程中，原有镜像已失效的问题
- 优化sysbench安装过程，centos和redhat系先尝试使用yum安装然后尝试使用dnf安装，确保二者都尝试过
- 修复输入错误提示重新输入在之前插入参数模式后失效的问题

2023.09.29

- 参数模式下支持自定义路由回程的IP设置

2023.09.28

- 修复不生成分享链接的BUG

2023.09.22

- 支持使用参数预设需要执行的指令

2023.09.21

- 修复部分组件可能存在的报错显示问题

2023.09.18

- 自动裁剪的函数存在部分问题，有的东西未裁剪丢弃有的裁剪多了，目前已修复

2023.08.26

- 针对纯IPV6服务器，使用v6的目标地址进行路由测试
- 修复IPV4的地址检测判断，识别 RFC 6598 地址避免误判，特殊处理在纯IPV6的情况下无法检测IP类型的情况
- 优化自动替换Besttrace为Nexttrace的判断条件，自动替换兼容的情况更多了
- 优化路由检测的v6部分的判断
- 同步系统基础信息检测的lemonbench的上游更新，优化上游更新中依然存在的bug

2023.08.20

- besttrace的API由于平台可能时不时存在403问题，遇到403或查询失败将应自动替换为备用的nexttrace测试，即使精度有下降

2023.08.15

- 测速节点增加欧洲地区节点
- CPU检测区分受测机是物理还是虚拟以便使用物理核心数测试还是线程数测试
- ip234.in 测试网站已炸，更换为 ipwhois.io 查询

2023.07.29

- 增加主体脚本一键更新的选项，避免有些人主体脚本下了之后再也没更新过了，导致部分BUG实际修复了但未更新反馈有问题，实际没问题
- IP质量检测再次完全重构，支持10个数据库查询，又因为用了异步并发查询，新增数据源不会导致速度变慢，测试速度不变
- 更新仓库说明中的展示图为最新的脚本截图
- 单独的IP质量检测也支持分享链接了
- IP质量检测同样输出的数据将合并输出，只留下数据库编号

2023.07.27

- 迁移分享链接的地址

2023.07.23

- 修复纯IPV6的机器测试网速会为空，未对纯IPV6服务器的测速适配的问题，暂时识别到后部分分区自动跳过测试
- lxc或openvz架构由于部分测试项目可能输出了错误日志，导致命令行窗口虽然显示正常，但有部分机器上传上去的文件显示空缺部分内容，应该是正则匹配删东西删多了，尝试修复了一下，如若还有问题后续再尝试修复

2023.07.16

- 更新CPU性能检测的代码的核数判断部分，避免变量错配提示
- 更新CPU核数检测的主体代码，对接上游更新

2023.07.10

- 虚拟化检测修改判断条件，修复可能存在systemd-detect-virt但是wsl的情况
- 时区对准的ntpd矫正前，先检测123端口是否已被占用，如若被占用则证明有在校准中，无需再次矫准，跳过不进行矫正
- 部分系统信息的判断条件稍作修改，修复某些变量比较的类型错误的问题
- CPU测试的CPU核数修改使用的来源，避免部分检测核心数和检测的线程数不一致

2023.07.09

- 增加错误处理，增加速率限制识别，避免ASN的识别和邮箱可达性识别出问题
- 更新系统基础信息查询，使用两个原始脚本融合，更新lemonbench的部分
- 去除virt-what的依赖，对基础信息的查询减少了很多依赖项
- 增加对系统信息的非0非空判断，以判别使用哪个原始脚本的方法获取系统信息

2023.07.08

- IPV4和IPV6的查询增加本地查询选项，增加内外网IP检测，保证查询到的IP是外网IP
- 如果查询到是内网IP，再使用API进行外网IP查询
- 并发查询ASN和IPV4/IPV6，并发查询IP质量各项，减少脚本的运行时长大概5~10秒
- virt-what的检测修改为which的检测方式，避免某些特殊情况查询不到 

2023.07.05

- ASN查询与地址查询增加cloudflare的检测源，多源使用并行执行并发检测，提高了检测的成功率和准确性
- ASN查询删除重复查询，精简了代码，提高了检测速度
- 邮箱可达性检测增加错误代码处理，避免显示错误日志
- 删除部分无效函数代码归档，调整代码块顺序，集合同类型的代码块，方便未来维护

2023.07.04

- 增加IP质量检测分区检测源，新增25端口的邮箱可达性检测
- 更新纯测IP质量部分脚本，更新部分组件安装的流程
- 增加脚本运行次数的统计

2023.06.27

- 增加IP质量检测分区检测源，新增黑名单网站数量检测，检测IP被多少个黑名单网站记录了
- 暂时放弃适配FreeBSD和Armbian系统，太难适配了，手头无相关测试机器
- 更新纯测IP质量部分脚本，去除jq依赖，缩短检测时长

2023.06.21

- 修复 Ubuntu18 系统在安装 virt-what 组件时，可能缺少universe的情况，自动添加universe记录

2023.06.19

- 修复部分组件的检测，避免检测的漏洞导致组件没被安装
- 修复硬盘的DD测试中IOPS的部分隐性BUG，优化写入计算的部分

2023.06.12

- 适配已正式发布的Debian12系统

2023.06.05

- 增加对FreeBSD系统的支持
- 去除了系统OS重复判断的部分函数，精简该部分代码
- 给分享链接的生成增加路径修正，避免有时候因为意外退出路径不对导致分享链接对应的文件处理失败
- 增加了systemctl还是rc.d支持的判断，避免部分系统无法使用相关的命令
- virt-what的检测通过which进行而不是写死对/usr/sbin/virt-what路径进行判断，普适性更高

2023.06.01 

- 修复部分机器被stun服务器和IP查询的API站点拉黑的问题，报错替换为中文显示而不是网页源码显示
- 修复astralinux系统的部分机器无法使用apt源下载sysbench时编译出错的问题，替换为debian模式进行编译

2023.05.31

- 优化dmidecode组件安装，尝试各种安装参数
- 适配Astra Linux CE系统
- 适配Debian11系统上的sysbench和virt-what安装，不再使用debian10的版本，预设了debian12的版本选项等待官方正式发布
- 修复sysbench在低版本系统安装时不存在events per second输出导致识别为空的问题，实测Debian8和9检测CPU时不再识别为空
- 增加了apt-get自动修复缺失公钥的功能
- 修改部分第三方分区描述，避免歧义

2023.05.29 

- 修改脚本使得systl优化仅在测试期间起效果，执行完毕后重置回默认的设置，避免影响原系统环境

2023.05.28 

- 测试支持了OracleLinux 8+系统，修复在偏门的系统上安装NAT类型检测工具包失效的问题

2023.05.24 

- 由于有上游仓库兼容了chatgpt的检测，故在融合怪中删除本人维护的版本的分区，同时删除易造成echo错误的检测代码

2023.05.22 

- 修复部分开发板的内存测试读测试异常大的问题
- 增加ntpd服务检测，避免存在ntpd时还使用chronyd同步时间
- 增加内核参数优化，优化tcp请求和内核资源限制
- 增加haveged以提供更优质的熵避免部分命令因此执行时间变长

2023.05.20 

- 修复.cn测速时延迟显示小数位过长约束为2位小数
- CPU类型检测有时候会出现一连串的空格，替换最多连续出现一个空格
- 适配stun，pystun，pystun3包进行NAT类型检测，避免单一包环境失效导致检测失败(centos系无stun包，python3无pystun包)，按顺序越往后检测越不精准
- 调整部分输出更美观

2023.05.19 

- 修复一些输出和pastebin的问题

2023.05.18

- speedtest.net 有时候移动节点列表会为空，应当此时切换至 speedtest.cn 的移动列表，已修复添加
- speedtest.net 的国际节点测速ID时常变换，待替换为自动更新的测速ID列表，已修复替换

2023.05.15 

- 更新io测试中yabs测试的部分使用GitHub的文件，不再使其依赖gitlab，适配使用cdn加速下载
- 硬件测试分区和原创区增加测试挂载的多个磁盘的IO(仅测试挂载盘)的单项
- 替换timedatectl使用chronyd同步时间，规避时区识别，仅作时间同步
- 修复部分系统缺少tar命令无法解压文件的问题
- 增加RockyLinux 8+系统的支持

2023.05.14 

- 增加NAT类型检测，使用stun工具查询，如果查询结果为开放型或支持回环，那么应该是独立外网IP的服务器，其他的看情况，大概率是无独立IP的共享IP的服务器
- 暂时去除新加坡日本洛杉矶的测速节点ID后续使用自动更新的源避免老是要手动更新这部分节点
- 因为三网回程测试基于ipip.net的程序，有时间准确度要求，为修正避免出现timestamp error的错误报告，增加时区检测，若本机系统时间偏差本机时区超过180秒自动修正后再执行检测

2023.05.13 

- 增加全国三网ping值测试的脚本，指定检测到中国IP时使用延迟检测替换路由检测，增加可用的CDN(自建白名单CDN)，增加中国IP检测的API(cip.cc)，增加第三方脚本添加三网Ping值测试脚本

2023.05.11 

- 删除当识别为中国IP时仍然检测线路和回程路由的部分，准备替换为全国省会的Ping值检测

2023.05.06 

- 网站 ipinfo.io 的API有的机器因为代理原因或同段欺诈分过高原因，免费的额度耗尽，修复自动替换为其他接口查询，修复查询开发板的CPU型号时有换行符的问题

2023.05.05 

- 部分服务器在测试时使用speedtest-cli组件版本有要求，修复自动替换版本时部分服务器重复测试的问题

2023.05.04 

- 优化io测试中重复查询系统信息以及CPU检测时重复查询系统版本的函数，修改部分分区描述，修复在开发板上的本地设备检测不到CPU型号的问题

2023.05.03 

- 修复三网路由测试显示ASN时不显示AS号码的问题，删除无效的全国网络延迟测试

2023.05.02 

- 修复纯IPV6无法测试四网线路显示文件不存在的问题，修复纯IPV6网络查询到的ASN只显示了名字没显示AS号码的问题，修复IPV4的ASN查询可能出现的bug，增加两个数据来源网站

2023.05.01 

- 修复部分ARM机器识别CPU成功，但在甲骨文的新加坡的ARM上，即便使用yabs的CPU检测依然无法检测CPU类型的问题
- 修复显示ASN组织时使用ip.sb源时不显示AS号码的问题，删除上传的结果中yabs的IO测试部分出现的一些无效行
- 修复分区选择时可能错按选项导致菜单退出的问题，合并三网路由检测的函数简化代码

2023.04.29 

- 修复纯IPV6机器的IPV6测试中可能存在的一些BUG
- 修复纯IPV6机器的IPV6的ASN有时候识别失效的问题

2023.04.29 

- 修复部分机器查询内容的free命令不存在的问题
- 修复部分机器/proc/sys/vm/drop_caches是只读权限时，清除内存缓存会报无法写入的错误，增加sudo组件的检测和安装
- 修补有时候docker容器内的虚拟化架构检测误判为宿主机虚拟化架构的问题

2023.04.28 

- 第三方脚本区新增全球测速脚本，对应speedtest.cn的三网测速脚本
- 修复部分服务器组件安装需要交互的问题

2023.04.27 

- 修复单项测试多下载了io测试文件的问题
- 修复可能的非英文语言系统造成的部分信息识别失效的问题
- 修复screen挂起时语言模块缺少en_utf8语言包显示乱码的问题

2023.04.25 

- 更新修复国内服务器测三网路由时下载出错的问题

2023.04.24 

- 检测国内外IP增加两个判断，避免在国内还继续测流媒体等无用信息
- 修补使用CDN下载可能造成的重定向跟踪问题

2023.04.15 

使用[ecs-net](https://github.com/spiritLHLS/ecsspeed)自写测速脚本替代原有的脚本，修改：
- 三网测速每个运营商选择本机ping值最低的两个节点测速，节点列表大概每7天自动更新一次
- 支持国内服务器测试(有判断是否为国内机器)，在国内使用时使用CDN加速
- 当官方CLI安装失败(如罕见的架构或者官方网站访问失败时)自动使用 speedtest-go 作为替代品测速
- 同时修改了一个融合怪并发测试的版本，追求更短的测试时长，但前提要求是机器足够强劲

2023.04.14 

- 去除Python3的依赖，全套脚本只使用Shell语言
- IPV4的检测使用多个数据来源，保证IP质量检测能正常运行，不仅限于ip.sb来源
- 删除一个无效的IP数据库来源，去除jq组件和python组件的依赖，大幅度减少前期组件安装所需的时间

2023.04.13 

- 修复检测ARM时CPU识别不出来的BUG

2023.04.12 

- 修复如果测试有问题出现空测评的情况时会传空文件到pastebin的问题
- 增加Geekbench6测试选项在对应分区

2023.04.03 

- 修复sjlleo的nf查询不支持ARM架构机器查询的问题，但考虑到sjlleo不再维护流媒体检测的脚本，考虑替换别的作者的脚本检测

2023.04.02 

- 修复脚本openai脚本测试超时的问题，使用自维护的脚本，第三方流媒体检测方面脚本加入本人优化版本的选项，运行完毕自动上传结果到pastebin并给出分享链接

2023.03.30 

- 脚本运行还没选择就进行了部分组件的安装的逻辑问题已解决，组件只在选择完毕后进行安装
- 删除无效的ping0数据库，增加ip234数据库，优化了IP质量查询的函数减少了模块依赖，替换IP质量检测的V6检测平台，支持V6的地址进行检测
- 升级sysbench由1.0.17到1.0.20版本

2023.03.12 

- 更新修复适配中文系统支持，解决部分命令查询结果为中文不适配
- 更新了移动的测速节点ID

2023.03.04 

- 使用tmp文件优化缩减脚本执行时长，缩减了大概30秒执行时长

2023.02.28 

- 修复纯V6网络测试容易触发的某些错误

2023.02.20 

- 修复Fedora 23系统检测被redhat检测覆盖的问题
- 修复debian/ubuntu低版本需要验证才能下载virt-what, jq等工具包的问题

2023.02.11 

- 新增OpenAI检测，已加入融合怪套餐，修复删除部分流媒体检测空行的显示节省空间

2023.02.08 

- 解决almalinux部分版本安装不上sysbench部件的问题(epel-release的编译安装新增almalinux的判断)

2023.02.06 

- 解决almalinux不自带unzip的问题

2023.01.25 

- IP质量检测重构输出，增加两个数据库来源

2023.01.20 

- 三网路由测试收纳 nexttrace 作为第三方脚本选项和原创区脚本选项

2023.01.19 

- 修复自定义IP路由测试的一些显示bug

2023.01.17 

- 硬件测试合集添加对应硬件测试脚本，修改部分链接使用原始链接。

2023.01.16 

- 隐藏部分错误显示，优化了输出。

2023.01.15 

- 更新tiktok的检测，替换失效的函数

2023.01.14 

- 新增成都三网回程路由测试选项，改进测速部分的显示去除乱码
- 优化代码缩减了代码行数。

2023.01.11 

- 由于部分新服务器刚开机不自启动bbr，现脚本询问是否需要启动了bbr后再进行测试(前提是服务器自身已安装bbr但未启动，未安装则不询问，已启动也不询问)
- 第三方脚本重新分区并整合为合集，相同类型脚本在同合集中，自行选择
- 部分脚本描述细微更改

2023.01.07 

- 删除部分无效代码，三网回程路由优化使用ip.sb进行IP检测与ASN检测，再度优化缩减代码行数，merge了一个push以支持arch系统测试

2023.01.06 

- 修复IP质量检测的curl有的服务器会curl到V6去，而不是最基础的V4的bug，merge一个pull，脚本支持arch系统测试了

2023.01.03 

- 更改三网回程的环境文件下载方式，避免某些隐性bug

2023.01.02 

- 下载环境前预加载CDN加速轮询判断，如若无可用CDN才用原链接，解决国内服务器无法访问部分资源的问题，加速各种环境文件的下载，减少脚本环境准备时长。

2023.01.01 

- 修复脚本部分curl命令需要ssl验证的问题，已忽略校验
- 修复脚本OVZ运行时执行内核缓存清除报错显示的问题
- 修复python2版本不做IP质量检测以达到修复执行报错的问题
- 修复如果未设置TCP拥堵控制算法时显示为空的问题。

2022.12.28 

- 修复查询TCP加速方式时可能遇到的sysctl的路径不存在或者异常的问题
- 修复虚拟化架构只通过命令判断有可能失效导致查询结果为Dedicated的问题，增加检查系统文件的查询函数
- 简化部分函数判断，缩减脚本行数

2022.12.17 

- 删除一个无效数据库来源，又套了cf的5秒盾了，啧

2022.12.14 

- 非致命性bug后续很长一段时间内不再更新本脚本，所有致命性bug已修复
- 第三方脚本增加两个三网回程线路检测脚本
- 原创区新增自定义IP的IP质量检测脚本
- 融合怪的执行结果保存在```/root```下的test_result.txt中，运行完毕可用```cat test_result.txt```查看记录

2022.12.13 

- 流媒体检测部分远程调用最新脚本不再直接使用老脚本函数，检测准确度提升
- 替换部分github的raw链接使用cf的cdn链接加速下载，融合怪脚本所需运行时长缩减

2022.12.12 

- 新增两个IP类型数据库，IP检测已包含三个数据库
- 修复debian10系统apt源broken的问题，内置```apt --fix-broken install -y```
- 修复centos8的源失效问题，自动替换新源下载```AppStream```
- 新增支持Almalinux系统

2022.12.11 

- 不再使用ip.gs改用api.ipify.org进行IP识别

2022.11.04 

- 更新替换Tiktok检测脚本为superbench脚本，暂时移除端口检测
- 第三方脚本增加Geekbench选项，修改部分分区描述

2022.10.02 

- 重新划分测试区域，含借鉴脚本的原始脚本选项和原创脚本选项，如果本脚本不好用，可以试试原始脚本

2022.09.23 

- 增加全国网络延迟测试，新增两个原始版本的三网测速的选项

2022.08.31 

- 增加三网路由延迟，Tiktok解锁测试提速
