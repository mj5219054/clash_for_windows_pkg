# 去中心化存储格局

与主要目的是去信任价值转移的 Layer1 区块链（例如比特币和以太坊）不同，去中心化存储网络不仅需要记录交易（用于存储请求），还必须确保数据存储在特定的时间内，并克服与存储有关的其他挑战。因此，经常可以看到去中心化存储区块链应用多种共识机制，这些机制协同工作，以确保存储和检索的不同方面能够发挥作用。

在以下非详尽的去中心化存储项目列表中，我们可以瞥见去中心化存储的景观以及利基数据存储用例，如 P2P 文件共享和数据市场。

这项研究的重点是存储网络（基于 IPFS 和非 IPFS）。

* ![图片](https://user-images.githubusercontent.com/79394963/196874087-42b33aed-d6c6-4876-9387-178d0edbf81a.png)


图 1：去中心化存储协议概述（非详尽）

去中心化存储设计挑战

正如本文第一节所展示的，区块链不适合在链上存储大量的数据，因为相关的成本和对区块空间的影响。因此，去中心化的存储网络必须应用其他技术来确保去中心化。然而，如果网络想保持去中心化，不使用区块链作为主要的存储空间，会导致一长串其他挑战。

从本质上讲，一个去中心化的存储网络必须能够存储数据、检索数据和维护数据，同时确保网络内的所有行为者都能为他们所做的工作得到激励，同时也要坚持去中心化系统的无信任性质。

因此，从设计的角度来看，我们可以在以下说明性段落中总结出主要的挑战。

数据存储格式 Data Storage Format——首先，网络必须决定如何存储数据：数据是否应该被加密，数据应该被保存为一整套还是分成小块。

数据复制 Replication of Data——然后网络需要决定将数据存储在哪里：数据应该存储在多少个节点上，以及是否将所有数据复制到所有节点，或者每个节点是否应该获得不同的片段以进一步保护数据隐私。数据存储格式和数据的网络传播将决定数据在网络上可用的概率，即设备随时间发生故障（持久性）。

存储跟踪 Storage Tracking——从这里开始，网络需要一种机制来跟踪数据的存储位置。这很重要，因为网络需要知道询问哪些网络位置来检索特定数据。

数据存储证明 Proof of Data Stored——网络不仅需要知道数据的存储位置，而且存储节点还需要能够证明它们确实存储了它们打算存储的数据。

一段时间内的数据可用性 Data Availability over Time——网络还需要确保数据在它应该存在的时候就在它应该存在的地方。这意味着必须设计机制以确保节点不会随着时间的推移删除旧数据。

存储价格发现 Storage Price Discovery——节点期望为文件的持续存储付费。

持久数据冗余 Persistent Data Redundancy——虽然网络需要知道数据的位置，但由于公共开放网络的性质，节点会不断离开网络，新的节点会不断加入网络。因此，除了确保单个节点在它们应该存储的时候存储它们应该存储的东西之外，网络还需要确保当一个节点离开，它的数据消失时，整个网络上保持足够的数据或数据片段的副本。

数据传输 Data Transmission——然后，当网络连接到节点以检索（用户或数据维护工作负载）请求的数据时，存储数据的节点必须愿意传输数据，因为带宽也是有代价的。

网络代币经济学 Network Tokenomics——最后，除了确保数据驻留在网络内，网络必须确保网络本身将长期存在。如果网络消失了，它将会带走所有的数据 — 因此，强大的 tokenomics 是必要的，以确保网络的永久性，从而确保数据的长期可用性。

去中心化存储技术的最全分析

克服挑战数据去中心化

在本节中，我将比较和对比 IPFS、Filecoin、Crust Network、Arweave、Sia、Storj 和 Swarm 的去中心化存储网络设计的各个方面，以及它们如何克服上述挑战。这反映了成熟的以及新兴的去中心化存储网络，它们使用广泛的技术来实现去中心化。

下表总结了每个网络的技术方面和代币经济学，这将在本节中更详细地介绍，以及作者认为这些链遵循其各种设计元素的强大用例。

去中心化存储技术的最全分析

* ![图片](https://user-images.githubusercontent.com/79394963/196874158-f3fc6e92-b1bf-4b25-93f2-8188398e698a.png)

图 2：审查的存储网络的技术设计决策摘要

* ![图片](https://user-images.githubusercontent.com/79394963/196874231-de1f2739-0a1a-4dfc-b286-577bd2af1cb1.png)

去中心化存储技术的最全分析

* ![图片](https://user-images.githubusercontent.com/79394963/196874297-b596f54d-5e21-4af5-9dec-a907d94a70e6.png)

图 3：审查的存储网络的代币设计决策总结

去中心化存储技术的最全分析
* ![图片](https://user-images.githubusercontent.com/79394963/196874373-21cd60b8-11b6-42fb-b1cf-7cb60d97e461.png)

图 4：已审查存储网络的强大用例总结

由于许多概念在每个协议设计中密切相关，因此不可能清楚地划分每个挑战，因此各小节之间会有一些重叠。

* ![图片](https://user-images.githubusercontent.com/79394963/196874450-ead70385-0450-435d-997c-788bbba544c1.png)

数据存储格式和数据复制

数据格式和数据的复制是指数据如何存储在单个节点实例上，以及当用户或应用程序请求存储文件时，数据如何跨多个节点传播（以下将用户和应用程序统称为用户或应用程序）客户）。这是一个重要的区别，因为数据也可以作为网络或其他网络参与者发起的数据维护过程的结果存储在节点上。

在下表中，我们可以看到协议如何存储数据的简要概述：

去中心化存储技术的最全分析

图 5：审查存储网络的数据存储方法和数据复制

* ![图片](https://user-images.githubusercontent.com/79394963/196874539-72433868-c369-43f3-9686-0db50dcce3cf.png)



从上述项目来看，Filecoin 和 Crust 使用星际文件系统（IPFS）作为网络协调和通信层，用于在对等方之间传输文件并将文件存储在节点上。IPFS 和 Filecoin 都是由 Protocol Labs 开发的。

当新的数据要存储在 Filecoin 网络上时，存储用户必须通过 Filecoin 存储市场连接到一个存储供应商，并协商存储条款，然后再下一个存储订单。然后，用户必须决定使用哪种类型的擦除编码（EC）以及其中的复制因素。通过擦除编码，数据被分解成恒定大小的片段，每个片段都被扩展，并对冗余数据进行编码，因此，只有片段的一个子集才需要重建原始文件。复制因子指的是数据应该多长时间被复制到存储矿工的更多存储扇区。一旦存储矿工和用户就条款达成一致，数据就会被传送到存储矿工，并被存储在存储矿工的存储扇区。

去中心化存储技术的最全分析

* ![图片](https://user-images.githubusercontent.com/79394963/196874603-c1f92302-3ddd-42a5-af77-dfd424d7381b.png)

图 6：数据的数据复制和擦除编码

如果用户想要进一步增加冗余，他们需要与额外的存储供应商进行额外的存储交易，因为仍然存在一个存储矿工下线的风险，并且所有承诺的存储扇区都会随之下线。Filecoin 在 Filecoin 协议上构建的 NFT.Storage 和 Web3.Storage 等应用程序通过使用多个存储矿工存储文件来解决这个问题，但是在协议级别，用户必须手动与多个存储矿工互动。

相比之下，Crust 将数据复制到固定数量的节点：提交存储订单时，数据被加密并发送到至少 20 个 Crust IPFS 节点（节点数量可以调整）。在每个节点上，数据被分成许多较小的片段，这些片段被散列成 Merkle 树。每个节点保留构成完整文件的所有片段。虽然 Arweave 也使用完整文件的复制，但 Arweave 采用了一些不同的方法。交易提交到 Arweave 网络后，第一个单个节点会将数据作为块存储在 blockweave 上（Arweave 的区块链表现形式）。从那里开始，一种称为 Wildfire 的非常激进的算法确保数据在网络上快速复制，因为为了让任何节点挖掘下一个块，它们必须证明他们可以访问前一个块。

去中心化存储技术的最全分析

* ![图片](https://user-images.githubusercontent.com/79394963/196874670-2dc33893-b0fc-4184-be2d-b38413aff565.png)


图 7：数据存储格式将影响检索和重建

Sia、Storj 和 Swarm 使用纠删码 (EC) 来存储文件。通过 Crust 的实现，20 个完整的数据集存储在 20 个节点上。虽然这是非常冗余的，并且使数据非常耐用，但从带宽的角度来看，这是非常低效的。纠删码提供了一种更有效的实现冗余的方法，通过提高数据的持久性而不会产生大的带宽影响。

Sia 和 Storj 直接将 EC 分片传播到特定数量的节点，以满足一定的持久性要求。另一方面，Swarm 以更接近的节点形成邻域的方式管理节点，并且这些节点主动地在彼此之间共享数据块（Swarm 中使用的特定片段格式）。如果经常从网络中调用流行的数据，则会激励其他节点也存储流行的块——这称为机会缓存。因此，在 Swarm 中，网络中的数据片段数量可能远远多于被认为的最小“健康”数量。虽然这确实会影响带宽，但这可以被认为是通过减少与请求节点的距离来预先加载未来的检索请求。

存储跟踪

在将数据存储到一个或多个节点之后，网络需要知道数据的存储位置。这样，当用户请求检索他们的数据时，网络就知道去哪里找了。

去中心化存储技术的最全分析

* ![图片](https://user-images.githubusercontent.com/79394963/196874738-1ee0ac94-ede9-48e5-baf2-99efdc5d75d0.png)

图 8：审查存储网络的存储跟踪

Filecoin、Crust、Sia 和 Arweave 都使用区块链或区块链生命结构来管理存储订单并记录放置在网络上的每个存储请求。在 Filecoin 中，Crust 和 Sia 存储证明（即文件已被矿工存储的证明，存储在链上）。这使这些网络可以在任何时间点知道哪些数据位于何处。使用 Arweave，网络会激励所有节点存储尽可能多的数据，但是，节点不需要存储每条数据。由于 Arweave 将数据作为块存储在其区块链上，并且节点不需要存储所有数据，因此节点可能会丢失一些可以在以后检索的数据。因此，为什么 Arweave 的 blockweave 是「类似区块链」的结构。

在 Filecoin、Crust 和 Sia 上，存储节点都维护一个本地表，其中包含哪些存储节点存储哪些数据的详细信息。该数据通过彼此之间的闲聊在节点之间定期更新。然而，对于 Arweave，当请求内容时，节点是机会性地请求，而不是接触已知保存内容的特定节点。

Storj 和 Swarm 都没有自己的第 1 层区块链，因此以不同的方式跟踪存储。在 Storj 中，存储顺序管理和文件存储分为两种不同类型的节点，即卫星节点和存储节点。卫星，可以是单个服务器，也可以是冗余的服务器集合，只跟踪用户提交给他们存储的数据，并且只存储在与他们签订协议的存储节点上。存储节点可以与多颗卫星一起工作，并存储来自多颗卫星的数据。这种架构意味着在 Storj 中存储文件，不需要全网络的共识，这意味着效率更高，存储数据所需的计算资源更少。然而，这也意味着如果一颗卫星离线，该卫星管理的数据将无法访问。

在 Swarm 中，数据存储的地址直接记录在数据到块的转换过程中每个块的哈希中。由于块跨节点存储在同一地址空间（即邻域）中，因此文件的邻域可以简单地通过块哈希本身来标识。这意味着不需要单独跟踪文件存储位置的机制，因为存储位置由块本身隐含。

存储数据证明、随时间推移的可用性和存储价格发现

除了网络知道数据存储在哪里之外，网络还必须有一种方法来验证要存储在特定节点上的数据是否确实存储在该特定节点上。只有在验证发生之后，网络才能使用其他机制来确保数据随着时间的推移保持存储（即，存储节点不会在初始存储操作后删除数据）。此类机制包括证明数据在特定时间段内存储的算法、成功完成存储请求持续时间的财务激励以及对未完成请求的抑制等。这里应该注意的是，数据随时间的可用性并不等同于永久性，尽管永久存储是长期数据可用性的一种形式。最后，为了说明存储数据的证明以及随着时间的推移如何确保数据可用性，本节将介绍每个协议的完整存储过程。

去中心化存储技术的最全分析

* ![图片](https://user-images.githubusercontent.com/79394963/196874797-caaeb344-e8b1-48df-8e6e-85294a45a404.png)

图 9：存储的数据证明、随时间推移的可用性以及已审查存储网络的定价机制

Filecoin

在 Filecoin 上，存储矿工在收到任何存储请求之前，必须将抵押品存入网络，作为向网络提供存储的承诺。完成后，矿工可以在存储市场上提供存储并为其服务定价。想要在 Filecoin 上存储数据的用户可以设置他们的存储要求（例如，所需的存储空间、存储持续时间、冗余和复制因子）并提出询问。

然后存储市场匹配客户端和存储矿工。然后客户端将他们的数据发送给矿工，矿工将数据存储在一个扇区中。然后对该扇区进行密封，这是一个将数据转换为数据的唯一副本的过程，该副本称为与矿工的公钥相关联的副本。这种密封过程确保每个副本都是物理上唯一的副本，并构成 Filecoin 复制证明算法的基础。该算法使用副本的 Merkle 树根和原始数据的哈希来验证提供的存储证明的有效性。

随着时间的推移，存储矿工需要通过定期运行该算法来始终如一地证明他们对存储数据的所有权。但是，像这样的一致检查需要大量带宽。Filecoin 的新颖之处在于，为了证明数据随时间存储并减少带宽使用，矿工使用前一个证明的输出作为当前证明的输入，按顺序生成复制证明。这是通过多次迭代执行的，这些迭代表示数据要存储的持续时间。

Crust Network

在 Crust Network 中，节点还必须先存入抵押品，然后才能在网络上接受存储订单。节点提供给网络的存储空间量决定了抵押品的最大数量，该抵押品被质押并允许节点参与在网络上创建区块。这种算法被称为保证权益证明（Guaranteed Proof of Stake），它保证只有在网络中拥有权益的节点才能提供存储空间。

节点和用户会自动连接到去中心化存储市场 (DSM)，该市场会自动选择在哪些节点上存储用户的数据。存储价格是根据用户需求（例如存储持续时间 storage duration 、存储空间 storage space、复制因子 replication factor）和网络因素（例如拥塞 congestion）确定的。当用户提交存储订单时，数据将被发送到网络上的多个节点，这些节点使用机器的可信执行环境 (TEE：Trusted Execution Environment) 拆分数据并散列碎片。由于 TEE 是一个封闭的硬件组件，即使硬件所有者也无法访问，因此节点所有者无法自行重建文件。

文件存储在节点上后，包含文件哈希的工作报告与节点的剩余存储一起发布到 Crust 区块链。从这里确保数据随时间存储，网络定期请求随机数据检查：在 TEE 中，随机 Merkle 树哈希与相关文件片段一起被检索，该文件片段被解密并重新散列。然后将新散列与预期散列进行比较。这种存储证明的实现称为有意义的工作证明（MPoW：Meaningful Proof of Work）。

Sia

与 Filecoin 和 Crust 的情况一样，存储节点必须存入抵押品才能提供存储服务。在 Sia 上，节点必须决定发布多少抵押品：抵押品直接影响用户的存储价格，但同时发布低抵押品意味着如果它们从网络中消失，节点也没有任何损失。这些力量将节点推向平衡抵押品。

用户通过自动存储市场连接到存储节点，其功能类似于 Filecoin：节点设置存储价格，用户根据目标价格和预期存储时长设置预期价格。然后用户和节点会自动相互连接。

在用户和节点就存储合同达成一致后，资金被锁定在合同中，并使用擦除编码将数据分割成片段，每个片段使用不同的加密密钥进行单独散列，然后每个片段被复制到几个不同的节点上。记录在 Sia 区块链上的存储合同记录了协议条款以及数据的 Merkle 树哈希值。从那里，为了确保数据在预期的存储时间内被存储，存储证明会定期提交给网络。这些存储证明是基于随机选择的原始存储文件的一部分和记录在区块链上的文件的 Merkle 树的哈希值列表而创建。节点在一段时间内提交的每一个存储证明都会得到奖励，最后在合约完成时得到奖励。

在 Sia 上，存储合同最长可以持续 90 天。要存储超过 90 天的文件，用户必须使用 Sia 客户端软件手动连接到网络，以将合同再延长 90 天。Skynet 是 Sia 之上的另一层，类似于 Filecoins Web3.Storage 或 NFT.Storage 平台，通过让 Skynet 自己的客户端软件实例为用户执行合同续期，为用户自动完成这一过程。虽然这是一个变通办法，但它不是一个 Sia 协议级别的解决方案。

Arweave

与以前的解决方案相比，Arweave 使用非常不同的定价模型，因为 Arweave 不允许临时存储：在 Arweave 上，所有存储的数据都是永久的。在 Arweave 上，存储价格取决于在网络上存储数据 200 年的成本，假设这些成本每年减少 -0.5%。如果存储成本在一年内减少超过 -0.5%，则节省的费用用于在存储期限结束时追加额外的存储年限。在 Arweave 自己的估计中，每年 -0.5% 的存储成本降低是非常保守的。如果存储成本的降低永远大于 Arweave 的假设，那么存储持续时间将继续无限增长，从而使存储永久化。

在 Arweave 上存储文件的价格是由网络动态确定的，基于前面提到的 200 年存储成本估算和网络的难度。Arweave 是工作量证明 (PoW) 区块链，这意味着节点必须解决加密哈希难题才能挖掘下一个区块。如果更多的节点加入网络，解决哈希难题变得更加困难，因此需要更多的计算资源来解决这个难题。动态价格难度调整反映了额外计算能力的成本，以确保节点保持动力留在网络上挖掘新块。

如果用户接受在网络上存储文件的价格，节点就会接受数据并将其写入块中。这就是 Arweave 的访问证明算法发挥作用的地方。访问证明算法分两个阶段工作：首先，节点必须证明他们可以访问区块链中的前一个块，然后他们必须证明可以访问另一个随机选择的块，称为召回块。如果节点可以证明对这两个区块的访问权，它们就会进入 PoW 阶段。在 PoW 阶段，只有能够证明可以访问两个区块的矿工才开始尝试解决加密哈希难题。当矿工成功解决难题时，他们会将区块以及数据写入区块链。从这里开始，网络上的节点要能够挖掘下一个块，它们必须包括新挖掘的块。

矿工的奖励包括来自网络代币排放的数据和区块奖励。除交易费用外，用户支付的其余价格存储在捐赠基金中，随着时间的推移支付给持有数据的矿工。只有当网络认为交易费用和区块奖励不足以使挖矿业务盈利时，才会支付这笔费用。这会在捐赠基金中创建浮动代币，从而进一步延长 200 年的最短存储期限。

在 Arweave 的模型中，没有对存储位置的跟踪。因此，如果一个节点无权访问所请求的数据，它将向它在本地维护的对等列表中的节点询问块数据。

Storj

在 Storj 去中心化存储网络中，没有区块链或类似区块链的结构。没有区块链也意味着该网络对其状态没有全网共识。相反，跟踪数据存储位置由卫星节点处理，数据存储由存储节点处理。卫星节点可以决定使用哪些存储节点来存储数据，存储节点可以决定从哪些卫星节点接受存储请求。

除了处理跨存储节点的数据位置跟踪外，卫星还负责存储节点的存储和带宽使用的计费和支付。在这种安排下，存储节点设置自己的价格，只要用户愿意支付这些价格，卫星就会将它们相互连接起来。

当用户想要在 Storj 上存储数据时，用户必须选择一个卫星节点来连接并共享其特定的存储要求。卫星节点然后会挑选出满足存储需求的存储节点，并将存储节点与用户连接起来。然后用户直接将文件传输到存储节点，同时向卫星付款。然后，卫星每月为保存的文件和使用的带宽支付存储节点费用。

为了确保存储节点持续存储它们要存储的数据片段，卫星对存储节点进行定期审计。不存储任何数据的卫星在应用擦除编码之前随机选择文件片段，并要求所有存储擦除编码片段的节点验证数据。当有足够多的节点返回数据时，卫星可以识别出报告错误数据的节点。

为了防止节点消失和使数据脱机，并确保它们通过审计始终验证文件碎片，Storj 卫星扣留了大部分存储节点收入，这使得提早离开网络或未能通过审计在财务上不可行。随着节点在网络中停留的时间越长，扣留的收入比例就会被释放。只有当存储节点在运行至少 15 个月后确定他们想要离开网络，并且存储节点向网络发出他们想要离开网络允许网络移动所有数据时，网络才会返还剩余的扣留资金。

Swarm

虽然 Swarm 没有用于跟踪存储请求的第 1 层区块链，但在 Swarm 上存储文件是通过以太坊上的智能合约处理的。因此，可以跟踪包含有关文件的一些详细信息的存储订单。并且由于在 Swarm 中每个块的地址都包含在块中，因此块的邻域也可以被识别。因此，当请求数据时，邻域内的节点相互通信以返回用户请求的块。

通过客户端软件，Swarm 让用户可以确定数据量和数据存储在 Swarm 上的持续时间，并使用智能合约进行计算。当数据存储在 Swarm 上时，块会存储在一个节点上，然后复制到与上传节点相同的邻居中的其他节点。当数据存储在节点上时，它会被分割成块，这些块将数据映射到一个块树，该树构建一个 Merkle 树，树的根哈希是用于检索文件的地址。因此，树的根哈希证明文件已正确分块和存储。树中的每个块都进一步嵌入了包含证明，想要出售长期存储（也称为承诺存储）的节点必须在做出承诺时通过基于以太坊的智能合约验证并锁定股份——本质上是保证金。如果在承诺期间，节点未能证明他们承诺存储的数据的所有权，他们将失去全部保证金。

最后，为了进一步确保数据不会随着时间的推移而被删除，Swarm 采用了随机抽签方式，其中节点因持有通过 Swarm 的 RACE 抽签系统挑选的随机数据而获得奖励。

持久数据冗余

如果数据存储在一定数量的节点上，可以假设在长期内随着节点离开和加入网络，这些数据最终会消失。为了解决这个问题，节点必须确保以任何形式存储的数据定期复制，以在用户定义的存储期限内始终保持最低水平的冗余。

去中心化存储技术的最全分析

图 10：审查的存储网络的数据持久性机制

在 Filecoin 网络上开采的每个区块中，网络都会检查存储数据所需的证明是否存在以及它们是否有效。如果超过某个故障阈值，则网络认为存储矿工故障，将存储订单标记为失败，并在存储市场上重新引入相同数据的新订单。如果数据被认为不可恢复，则数据将丢失，用户将获得退款。

Curst Network 是在 2021 年 9 月发布主网的网络中最年轻的网络，它还没有随着时间的推移来补充文件冗余的机制，但这种机制目前正在开发中。

在 Sia 上，网络上可用的擦除编码片段的数量被转换为健康指标。随着节点和擦除编码片段随着时间的推移而消失，一段数据的健康状况会降低。为确保健康保持高水平，用户必须手动打开 Sia 客户端，该客户端会检查健康状态，如果不是 100%，客户端会将数据片段复制到网络上的其他节点。Sia 建议每月打开一次 Sia 客户端以运行此数据修复过程，以避免数据低于不可恢复的碎片阈值，并最终从网络中消失。

Storj 采用与 Sia 类似的方法，但不是让用户采取措施确保网络上有足够的擦除编码文件片段，而是由卫星节点接管这项工作。卫星节点定期对存储节点上存储的分片执行数据审计。如果审核返回有缺陷的片段，网络将重建文件，重新生成丢失的片段并将它们存储回网络。

对于 Arweave，一致的数据冗余是通过访问证明算法实现的，该算法需要节点存储旧数据才能挖掘新数据。这一要求意味着激励节点搜索并保留较旧和“稀有”的块，以增加他们被允许挖掘下一个块并获得挖掘奖励的机会。

最后，Swarm 通过邻域复制确保持久冗余，作为防止数据随时间消失的关键措施。Swam 需要一个节点的每组最近邻居来保存该节点数据块的副本。随着节点离开或加入网络，随着时间的推移，这些邻居会重新组织，并且每个节点的最近邻居都会更新，这要求它们重新同步其节点上的数据。这导致最终的数据一致性。这是一个持续进行的过程，完全在链下执行。

激励数据传输

去中心化存储技术的最全分析

图 11：促进审查存储网络数据传输的机制

用户在网络上存储数据后，当用户、另一个节点或网络进程请求访问数据时，数据也必须是可检索的。节点接收并存储数据后，必须愿意在请求时发送数据。

Filecoin 通过一种称为检索矿工的单独类型的矿工来实现这一点。检索矿工是专门提供数据片段的矿工，并因此获得 FIL 代币奖励。网络中的任何用户都可以成为检索矿工（包括存储节点），检索订单通过检索市场处理。当用户想要检索数据时，他们在检索市场下订单，检索节点为其提供服务。尽管 Filecoin 与 IPFS 建立在相同的底层堆栈上，但 Filecoin 不使用 IPFS 的 Bitswap 交换协议来传输用户数据。相反，Bitswap 协议用于请求和接收 Filecoin 区块链的块。

Crust 直接使用 IPFS 的 Bitswap 机制来检索数据并激励节点愿意传输数据。在 Bitswap 中，每个节点都维护与其通信的节点的信用和债务分数。仅请求数据的节点（例如，当用户提交数据检索请求时）最终会承担足够高的债务，以至于其他节点将停止对其检索请求做出反应，直到它自己也开始满足足够的检索请求。除此之外，在 Crust Network 中，可以为数据存储请求提供存储证明的前四个节点将由发起订单的用户授予一定比例的存储费用，这意味着节点受益于能够快速接收数据，这取决于他们在提供数据方面的积极程度。

因此，Swarm 的 SWAP 协议（Swarm Account Protocol）的工作方式与 IPFS 的 Bitswap 机制相同，并集成了额外的功能。这里节点还维护其他节点的带宽信用和债务的本地数据库，在节点之间创建服务对服务的关系。但是，SWAP 假设，有时某个节点不需要数据来在短期内重新平衡信贷与债务比率。为了解决这个问题，节点可以支付其他节点支票来偿还他们的债务。支票是节点承诺支付给另一个节点的链下凭证，可以通过以太坊区块链上的智能合约兑换 BZZ 代币。

去中心化存储技术的最全分析

图 12：群记帐协议。资料来源：Swarm 白皮书

在 Sia 和 Storj 中，用户为使用的带宽付费。在 Sia 中，上传、下载和修复带宽由用户支付，而在 Storj 中，上传所需的带宽由存储节点承担。在 Storj 中，这是为了阻止节点在收到数据后立即删除数据。由于这种设置，节点没有理由避免使用带宽，因为带宽是按照他们在接受存储订单之前规定的价格支付的。

最后，在 Arweave 中，节点根据对等节点共享事务和块的可靠性以及响应请求的可靠性来合理分配带宽。然后，该节点跟踪它与之交互的所有对等节点的这些因素，并且最好与得分较高的对等节点进行通信。这提高了节点传输数据和共享信息的意愿，因为以较慢的方式接收块意味着与其他节点相比，它们有更少的时间来解决 Arweave 的 PoA 共识算法的加密哈希难题。

代币经济学

最后，网络必须决定代币设计。虽然上述确保数据在应该可用时可用，但代币经济学设计确保网络将在未来存在。没有网络，用户和主机就没有底层数据可以与之交互。在这里，我们将仔细研究代币的用途以及影响代币供应的因素。

注意：虽然上述所有部分都会影响代币经济学设计，但这里我们主要关注代币效用和代币排放设计

去中心化存储技术的最全分析

图 13：经审查的存储网络的代币经济学设计决策

在 Filecoin 网络中，FIL 代币用于支付存储订单和检索带宽。Filecoin 网络有一个通货膨胀的代币排放模型，使用两种类型的铸币：简单铸币，它在 6 年减半的时间表（与比特币的 4 年相比）和基准铸币中产生额外的代币排放。网络达到总存储空间里程碑（见图 23）。这意味着网络上的存储矿工被激励为网络提供尽可能多的存储。

有两种方法可以减少市场上 FIL 的循环供应。如果矿工未能履行承诺，他们的抵押品将被烧毁并从网络中永久移除（在撰写本文时为 3050 万 FIL）。最后，时间锁定的存储订单会暂时将 FIL 从流通中移除，并随着时间的推移支付给矿工。这意味着使用的存储越多，短期内流通的代币就越少，从而对代币价值造成通货紧缩的价格压力。

去中心化存储技术的最全分析

图 14：存储挖掘和 Max Baseline Minting 的 Max 和 Min Minting。资料来源: https://filecoin.io/blog/filecoin-circulating-supply/

在 Crust Network 中，CRU 代币用于支付存储订单并用于质押，作为 Crust Network 保证权益证明 (GPoS) 共识机制的一部分。在这个模型中，网络代币的排放也是通货膨胀的，并被用作区块奖励。然而，Crust Network 没有代币上限——12 年的通货膨胀率同比下降，之后代币通货膨胀率持续保持在 2.8%。

在 Crust，验证人及其担保人锁定的股份也作为质押担保品。如果发现验证人有恶意行为或无法提供所需的证明，他们的股权将被砍掉并烧毁。最后，抵押品和时间锁定的存储订单会暂时从流通中移除代币。由于矿工网络存储容量决定了矿工的赌注限额，矿工被激励提供更多的存储容量，以使他们的赌注收入与其他矿工成比例地最大化。Staked 的代币和锁定在有时间限制的存储订单中的代币，对代币价值产生了通缩的价格压力。

去中心化存储技术的最全分析

图 15：Crust Network 代币排放。资料来源：Crust 经济白皮书

* ![图片](https://user-images.githubusercontent.com/79394963/196874917-df9fd68a-f78a-43ce-aecf-f25e07de6f13.png)

Sia 有两个用于网络的代币；一种是实用代币 Siacoin，另一种是名为 Siafunds 的创收代币。Siafunds 在网络刚上线时就向公众出售，主要由 Sia 基金会持有。Siafunds 赋予持有者在网络上放置的每个存储订单的一定百分比的收入。Siafunds 对 Sia 的代币经济学没有实质性影响，因此在此不再赘述。

Siacoin 有一个通胀代币排放模型，作为区块奖励，没有代币上限。区块奖励以每个区块的线性方式永久减少，直到区块高度 270,000（大约 5 年的运营；在 2020 年达到）。从那时起，每个区块都包含 30,000 SC 的固定区块奖励。2021 年，Sia 基金会对 Sia 网络进行硬分叉，每块额外提供 30,000 SC 补贴，以资助 Sia 基金会，这是一个旨在支持、发展和推广 Sia 网络的非营利实体。

去中心化存储技术的最全分析

图 16：Siacoin 供应和 Foundation 铸币的年度增长。资料来源：https ://siastats.info/macroeconomics

Sia 还使用燃烧证明机制，要求矿工燃烧 0.5-2.5% 的收入来证明网络上有合法节点。这给代币供应带来了下行压力，尽管每年的燃烧量仅反映大约 50 万 SC，而代币排放量为 31.4 亿 SC。最后，质押的抵押品和长期存储订单也暂时将代币从 Sia 的流通中移除。

Arweave 网络的原生代币是 AR 代币，用于支付 Arweave 网络上的永久和理论上的永久存储。Arweave 还使用通胀代币模型，最大供应上限为 6600 万个 AR 代币。在 Arweave，主要的通缩影响是由 Arweave 的捐赠驱动的，这是 Arweave 对长期存储合同的实施。当用户想要在 Arweave 上存储文件时，只有一小部分存储费会交给矿工——其余的会根据 Arweave 的高度保守假设存入至少 200 年存储时间的捐赠基金中。这意味着，任何下达的存储订单都会将代币锁定至少 200 年，并在这 200 年的期限内缓慢支付。

去中心化存储技术的最全分析
* ![图片](https://user-images.githubusercontent.com/79394963/196874973-2f533ebe-5c62-4d9f-98cb-3eac95d171e0.png)

图 17：AR 代币通胀和团队分配。资料来源：https://medium.com/amber-group/arweave-enabling-the-permaweb-870ade28998b

在 Storj 中，STORJ 代币用于支付存储和带宽费用。所有 4.25 亿个 STORJ 代币都被预先铸造为以太坊网络上的 ERC20 代币。以前使用的是基于比特币的 SJCX 代币，然而，在 2017 年，Storj Labs 将他们的代币转换为以太坊并将代码重命名为 STORJ。在 STORJ 代币中，目前有 1.908 亿个 STORJ 代币被锁定在 Storj Labs 托管的六个智能合约控制的批次中，而 2.341 亿个 STORJ 代币未解锁。每个季度都会解锁一个批次，当 Storj Labs 认为他们不需要资金来为运营提供资金时，他们会重新锁定一个批次。这意味着将近一半的 STORJ 供应由 Storj Labs 直接控制，但是，如果他们想兑现，他们将不得不等待 6 个季度，因为资金被锁定在智能合约后面。

去中心化存储技术的最全分析

* ![图片](https://user-images.githubusercontent.com/79394963/196875046-dd7bdff5-de0f-4b38-8fdf-637bf384223c.png)



图 18：批次重新锁定时间表。来源：https://www.storj.io/blog/using-timelocked-tokens-to-support-long-term-sustainability


最后，Swarm 使用 BZZ 代币作为实用代币来支付网络存储费用。Swarm 部署的代币经济学模型是一条联合曲线，它根据代币的供应量确定代币的价格。用户可以随时以当前市场价格将其代币卖回联合曲线。在 Swarm 中，长期存储订单需要以“承诺”的形式进行质押。与之前的网络类似，更多的存储使用意味着市场上可用的代币更少，这将对代币价格产生通缩压力，因为想要购买代币的用户必须从联合曲线购买，这将增加价格代币出售。

去中心化存储技术的最全分析

* ![图片](https://user-images.githubusercontent.com/79394963/196875141-916736cf-3383-494d-8cd3-469c38beb34f.png)

图 19：BZZ 键合曲线的形状。来源：https://medium.com/ethereum-swarm/swarm-and-its-bzzaar-bonding-curve-ac2fa9889914

讨论

不可能说一个网络在客观上比另一个网络更好。在设计去中心化存储网络时，必须考虑无数的权衡。虽然 Arweave 非常适合永久存储数据，但 Arweave 不一定适合将 Web2.0 行业参与者迁移到 Web3.0 – 并非所有数据都需要永久保存。但是，有一个强大的数据子领域确实需要永久性：NFT 和 DApp。

如果我们看看其他网络，我们会看到类似的权衡：Filecoin 正在激励 Web2.0 存储提供商将他们的存储迁移到 Web3.0，因此是采用去中心化的推动力。Filecoin 的时空证明算法计算量大，写入速度慢，这意味着它更适合不经常变化的高价值数据（比如他们的口号“存储人类最重要的数据”）。但是，许多应用程序需要不断更改其数据。Crust Network 通过提供计算强度较低的存储来填补这一空白。

看看这些项目如何存储数据，我们可以看到 Crust Network 和 Arweave 是唯一不使用纠删码的项目。很多人可能认为纠删编码是更好的选择，因为大多数项目都在使用它，但事实并非如此。Arweave 不需要擦除编码，因为与 Wildfire 机制相结合的访问证明共识机制可确保数据在整个网络中积极复制。在 Crust Network 上，数据被复制到至少 20 个节点，在许多情况下复制到 100 多个节点。虽然这确实具有更大的前期带宽，但能够同时从大量节点检索数据使得文件检索速度更快，并在发生故障或节点离开网络时增加了强大的冗余。Crust Network 需要这种高度的冗余，因为它还没有像其他链一样的数据补充或修复机制。在这里回顾的去中心化存储网络中，Crust Network 是最年轻的。

如果我们将任何项目与 Filecoin 进行比较，我们会看到其他链支持更高程度的存储去中心化，但可能在其他方面更加集中，例如单个卫星节点可以控制大型存储节点集群的 Storj。如果该卫星节点脱机，则对文件的所有访问都将丢失。然而，与 Sia 所需的手动维修过程相比，让卫星自主控制维修过程是一个巨大的升级。通过允许用户和卫星之间的任何形式的支付，Storj 还为 Web2.0 用户提供了更容易进入去中心化存储的第一步。

如果我们进一步将 Storj 的去中心化方法与其他项目的方法进行比较，我们会发现 Storj 缺乏系统范围内的共识确实是一个有目的的提高网络性能的设计决策，因为网络不需要等待共识才能继续满足存储请求。

Swarm 和 Storj 是唯一没有自己的 layer1 区块链网络的协议，而是依赖部署在以太坊网络上的 ERC20 代币。Swarm 直接集成在以太坊网络中，存储订单通过以太坊智能合约直接控制。由于邻近和相同环境的便利性，这使得 Swarm 成为以太坊原生 dApp 和存储基于以太坊的 NFT 元数据的有力选择。Storj 虽然也是基于以太坊的，但并未高度集成到以太坊生态系统中，但是，它也可以从智能合约中受益。

Sia 和 Filecoin 使用存储市场机制，存储供应商可以设置价格并与愿意根据特定要求支付这些价格的存储用户匹配，而在其他网络中，存储定价是基于网络特定因素的协议规定. 使用存储市场意味着用户可以在如何存储和保护他们的文件方面获得更多选择，但由网络设定价格可以降低复杂性并提供更轻松的用户体验。

结论

对于分散存储网络面临的各种挑战，没有单一的最佳方法。根据网络的目的和它试图解决的问题，它必须在网络设计的技术和代币经济学方面进行权衡。

去中心化存储技术的最全分析
* ![图片](https://user-images.githubusercontent.com/79394963/196875224-ad59fcb3-584e-4a61-88a8-aec1d2c20ee5.png)

图 20：已审查存储网络的强大用例总结

最后，网络的目的和它试图优化的特定用例将决定各种设计决策。

比较网络分析

以下是各种存储网络的总结概况，它们在下面定义的一组尺度上相互比较。使用的尺度反映了这些网络的比较维度，但应该注意的是，克服分散存储挑战的方法在许多情况下没有好坏之分，而只是反映了设计决策。

存储参数灵活性：用户控制文件存储参数的程度

存储持久性：文件存储在多大程度上可以通过网络实现理论上的持久性（即无需干预）

冗余持久性：网络通过补充或修复来保持数据冗余的能力

数据传输激励：网络确保节点慷慨传输数据的程度

存储跟踪的普遍性：节点之间对数据存储位置的共识程度

有保证的数据可访问性：网络确保存储过程中的单个参与者无法删除对网络上文件的访问的能力

Filecoin 的代币经济学支持增加整个网络的存储空间，用于以不可变的方式存储大量数据。此外，他们的存储算法更适用于不太可能随时间发生很大变化的数据（冷存储）。

去中心化存储技术的最全分析

* ![图片](https://user-images.githubusercontent.com/79394963/196875274-47b7e018-e898-4828-afdf-1f680f41811c.png)

图 21：Filecoin 总结概况

Crust 的代币经济学确保了超冗余和快速检索，使其适用于高流量 dApp 并适用于快速检索流行 NFT 的数据。

Crust 在存储持久性方面的得分较低，因为没有持久冗余，它提供永久存储的能力会受到严重影响。尽管如此，仍然可以通过手动设置极高的复制因子来实现持久性。

去中心化存储技术的最全分析

图 22：Crust 总结概况

* ![图片](https://user-images.githubusercontent.com/79394963/196875392-3079f23f-bbbd-4570-bdc8-bf4584ca0335.png)

Sia 是关于隐私的。之所以需要用户手动恢复，是因为节点不知道自己存储了哪些数据片段，以及这些片段属于哪些数据。只有数据所有者才能从网络中的分片中重建原始数据。

去中心化存储技术的最全分析

* ![图片](https://user-images.githubusercontent.com/79394963/196875447-50a58f72-42dd-44e5-83a5-63290388b80c.png)

图 23：Sia 总结概况
* ![图片](https://user-images.githubusercontent.com/79394963/196875678-b89ad132-8bb7-42dc-8cf6-6857214aa85b.png)

相比之下，Arweave 是关于持久性的。这也反映在它们的禀赋设计中，这使得存储成本更高，但也使它们成为 NFT 存储的极具吸引力的选择。

去中心化存储技术的最全分析
* ![图片](https://user-images.githubusercontent.com/79394963/196875502-2d5faf15-2cb9-45d6-b038-b870cc0b3fe8.png)

图 24：Arweave 的总结概况

* ![图片](https://user-images.githubusercontent.com/79394963/196875601-ce2ea864-5c7e-4e04-b867-0701010f9b07.png)

Storj 的商业模式似乎在很大程度上影响了他们的计费和支付方式：亚马逊 AWS S3 用户更熟悉按月计费。通过移除基于区块链的系统中常见的复杂支付和激励系统，Storj Labs 牺牲了一些去中心化，但显着降低了 AWS 用户关键目标群体的进入门槛。

去中心化存储技术的最全分析

图 25：Storj 总结概况

* ![图片](https://user-images.githubusercontent.com/79394963/196875544-c4b9facb-651e-48c4-aeff-61bcc9e57ae9.png)

Swarm 的联合曲线模型确保随着更多数据存储在网络上，存储成本保持相对较低的加班时间，并且它靠近以太坊区块链使其成为更复杂的基于以太坊的 dApp 的主要存储的有力竞争者。

去中心化存储技术的最全分析

图 26：Swarm 总结概况

下一个边界

回到 Web3 基础设施支柱（共识、存储、计算），我们看到去中心化存储空间拥有少数强大的参与者，他们已针对特定用例将自己定位在市场中。这并不排除新网络优化现有解决方案或占领新的利基市场，但这确实提出了一个问题：下一步是什么？

答案是：计算。实现真正去中心化互联网的下一个前沿是去中心化计算。目前，只有少数解决方案能够将去信任、去中心化计算的解决方案推向市场，这些解决方案可以为复杂的 dApp 提供支持，这些解决方案能够以远低于在区块链上执行智能合约的成本进行更复杂的计算。

互联网计算机 (ICP) 和 Holochain (HOLO) 是在撰写本文时在去中心化计算市场中占据强势地位的网络。尽管如此，计算空间并不像共识和存储空间那样拥挤。因此，强大的竞争对手迟早会进入市场并相应地定位自己。一个这样的竞争对手是Stratos (STOS)。Stratos 通过其分散式数据网格技术提供独特的网络设计，将区块链技术与分散式存储、分散式计算和分散式数据库相结合。

我们将去中心化计算，特别是 Stratos 网络的网络设计视为未来研究的领域。

参考文献

参考文献已按类别拆分，以便于查看。所有参考资料采用均在 2022 年 5 月 5 日至 31 日期间。

Arweave

Amber Group (2011) Arweave: Enabling the Permaweb. Available at: https://medium.com/amber-group/arweave-enabling-the-permaweb-870ade28998b



Arweave (2021) Storage Endowment. Available at: https://arwiki.wiki/#/en/storage-endowment (Accessed May 29th, 2022)

Arweave (2021) What is the Permaweb. Available at: https://arwiki.wiki/#/en/the-permaweb (Accessed May 29th, 2022)

Arweave (2022) Storage Price Stabilization. Available at: https://arwiki.wiki/#/en/Storage-Price-Stabilization (Accessed May 29th, 2022)

Arweave (n.d.) Technology. Available at: https://www.arweave.org/technology

Arweave Fees (2021) Arweave Fees. Available at: https://arweavefees.com/

Crypto Valley Journal (n.d.) Permaweb. Available at: https://cvj.ch/en/glossary/permaweb/

Gemini (2022) Arweave: A Permanent, Decentralized Internet. Available at: https://www.gemini.com/cryptopedia/arweave-token-ar-coin-permaweb

Gemini (n.d.) Glossary: Permaweb. Available at: https://www.gemini.com/cryptopedia/glossary#permaweb

Messari (n.d.) Arweave – Data Storage Protocol. Available at: https://messari.io/asset/arweave/profile/token-usage

Tom McWright (2019) How much does Arweave cost? https://observablehq.com/@tmcw/how-much-does-arweave-cost

Wayne Jones (n.d.) Can data really be stored forever? Available at: https://ardrive.io/can-data-really-be-stored-forever/

Crust

Crust Network (2020) Crust Technical White Paper v1.9.9. Available at: https://gw.crustapps.net/ipfs/QmP9WqDYhreSuv5KJWzWVKZXJ4hc7y9fUdwC4u23SmqL6t

Crust Network (2021) Crust Token Metrics & Economies. Available at: https://medium.com/crustnetwork/crust-token-metrics-economics-84592efc6d1f

Crust Network (2021) Economy Whitepaper. Available at: https://gw.crustapps.net/ipfs/QmRYJN6V5BzwnXp7A2Avcp5WXkgzyunQwqP3Es2Q789phF

Crust Network (n.d.) DSM. Available at: https://wiki.crust.network/docs/en/DSM

Crust Network Subscan (n.d.) Storage Price Calculator. Available at: https://crust.subscan.io/tools/storage_calculator

Filecoin

Coinlist (2017) Filecoin Token Sale Economies. Available at: https://coinlist.co/assets/index/filecoin_2017_index/Filecoin-Sale-Economics-e3f703f8cd5f644aecd7ae3860ce932064ce014dd60de115d67ff1e9047ffa8e.pdf

File.App (n.d.) Available at: https://file.app/

Filecoin (2020) Date Transfer in Filecoin. Available at: https://spec.filecoin.io/systems/filecoin_files/data_transfer/

Filecoin (2020) Storage Market in Filecoin. Available at: https://spec.Filecoin.io/systems/Filecoin_markets/storage_market/

Filecoin (2020) Understanding Filecoin Circulating Supply. Available at: https://filecoin.io/blog/filecoin-circulating-supply/

Filecoin (2020) What sets it apart: Filecoin’s proof system. Available at: https://filecoin.io/blog/posts/what-sets-us-apart-filecoin-s-proof-system/

Filecoin (2021) How storage and retrieval deals work on Filecoin. https://Filecoin.io/blog/posts/how-storage-and-retrieval-deals-work-on-Filecoin/

Filecoin (n.d.) IPFS and Filecoin. Available at: https://docs.Filecoin.io/about-Filecoin/ipfs-and-Filecoin/

Filecoin (n.d.) IPFS. Available at: https://spec.filecoin.io/#section-libraries.ipfs

James Duade (2021) FileCoin: Decentralized Cloud Storage Competitor To AWS, Microsoft Azure, And Google Cloud. Available at: https://seekingalpha.com/article/4419553-Filecoin-decentralized-cloud-storage-competitor-aws-microsoft-google

IPFS

Brave (2021) IPFS Support in Brave. Available at: https://brave.com/ipfs-support/

Hussein Nasser (2021) The IPFS Protocol Explained with Examples – Welcome to the Decentralized Web. Available at: https://www.youtube.com/watch?v=PlvMGpQnqOM

IPFS (n.d.) InterPlanetary Name System (IPNS). Available at: https://docs.ipfs.io/concepts/ipns/

James (2018) The technology behind IPFS. Available at: https://medium.com/coinmonks/the-technology-behind-ipfs-and-what-can-ipfs-do-c7009fe42bab

Sia

Cryptopedia Staff (2021) Sia: A Highly Decentralized Data Storage Solution. Available at: https://www.gemini.com/cryptopedia/siacoin-mining-sia-crypto-sc-coin-decentralized-storage#section-siacoin-sc-and-siafunds

Sia Docs (2022) Sia 101. Available at: https://docs.sia.tech/get-started-with-sia/sia101

Sia Wiki (2017) Hosting. Available at: https://siawiki.tech/host/hosting

Sia Wiki (2017). Using the UI for renting. Available at: https://siawiki.tech/renter/using_the_ui_for_renting

SiaStats.info (2018) “When coin burn?” Every day, and 400 000 SC so far. Available at: https://www.reddit.com/r/siacoin/comments/8te2e4/when_coin_burn_every_day_and_400_000_sc_so_far/

Taek (2015) [ANN] Sia – Decentralized Storage. Available at: https://bitcointalk.org/index.php?topic=1060294.msg11372055#msg11372055

Taek (n.d.) How Sia Works. Available at: https://web.archive.org/web/20171102065557/https:/forum.sia.tech/topic/108/how-sia-works

Vorick, D. and Champine, L. (2014) Sia: Simple Decentralized Storage. Available at: https://sia.tech/sia.pdf

Storj

Cryptopedia Staff (2021) Sia: A Highly Decentralized Data Storage Solution. Available at: https://www.gemini.com/cryptopedia/siacoin-mining-sia-crypto-sc-coin-decentralized-storage#section-siacoin-sc-and-siafunds

Sia Docs (2022) Sia 101. Available at: https://docs.sia.tech/get-started-with-sia/sia101

Sia Wiki (2017) Hosting. Available at: https://siawiki.tech/host/hosting

Sia Wiki (2017). Using the UI for renting. Available at: https://siawiki.tech/renter/using_the_ui_for_renting

SiaStats.info (2018) “When coin burn?” Every day, and 400 000 SC so far. Available at: https://www.reddit.com/r/siacoin/comments/8te2e4/when_coin_burn_every_day_and_400_000_sc_so_far/

Taek (2015) [ANN] Sia – Decentralized Storage. Available at: https://bitcointalk.org/index.php?topic=1060294.msg11372055#msg11372055

Taek (n.d.) How Sia Works. Available at: https://web.archive.org/web/20171102065557/https:/forum.sia.tech/topic/108/how-sia-works

Vorick, D. and Champine, L. (2014) Sia: Simple Decentralized Storage. Available at: https://sia.tech/sia.pdf

Swarm

Altcoin Disrupt (2021) What is Swarm? ICO Upcoming? Will Swarm 100X? Decentralized? $10K – $100K. Available at: https://www.youtube.com/watch?v=rxPlYf9Pe2A

Coding Bootcamps (n.d.) How to Work with Ethereum Swarm Storage. Available at: https://www.coding-bootcamps.com/blog/how-to-work-with-ethereum-swarm-storage.html

ETHDenver (2022) The State Of Ethereum Swarm – Angela Vitzthum. Available at: https://www.youtube.com/watch?v=22HfkeEmOK4

Ethereum Wiki (2020) Swarm Hash. Available at: https://eth.wiki/concepts/swarm-hash

Munair (2021) A Case for Swarming Medical History. Available at: https://munair.medium.com/a-case-for-swarming-medical-history-77baa5e40424

Swarm (n.d.) Swarm Docs. Available at: https://docs.ethswarm.org/docs/

Swarm Hive (2021) BZZ Tokenomics. Available at: https://medium.com/ethereum-swarm/swarm-tokenomics-91254cd5adf

Swarm Hive (2021) Swarm and its “Bzzaar” Bonding Curve. Available at: https://medium.com/ethereum-swarm/swarm-and-its-bzzaar-bonding-curve-ac2fa9889914

Swarm team (2021) SWARM: Storage and communication infrastructure for a self-sovereign digital society. Available at: https://www.ethswarm.org/swarm-whitepaper.pdf

Thebojda (2022) A Brief Introduction to Ethereum Swarm. Available at: https://hackernoon.com/a-brief-introduction-to-ethereum-swarm

Trón, V. (2021) The book of Swarm: storage and communication infrastructure for self-sovereign digital society back-end stack for the decentralised web. V1.0 pre-release 7. Available at: https://www.ethswarm.org/The-Book-of-Swarm.pdf

Miscellaneous

BitcoinFees.net (n.d.) Bitcoin Fees. Available at: https://bitcoinfees.net/ (Accessed May 15th, 2022)

BitcoinTalk Forum (2021) Some questions about OP_Return. Available at: https://bitcointalk.org/index.php?topic=5310671.0

Daniel, E. and Tschorsch, F. (2022) IPFS and Friends: A Qualitative Comparison of Next Generation Peer-to-Peer Data Networks. Available at: https://arxiv.org/pdf/2102.12737.pdf

Dfinity (n.d.) Blockchain’s future. Available at: https://dfinity.org/

Dr. Wood, G. (2016) Ethereum: A Secure Decentralized Generalised Transaction Ledger EIP-150 Revision. Available at: http://gavwood.com/paper.pdf

Ethereum Foundation (2022) Gas and Fees. Available at: https://ethereum.org/en/developers/docs/gas/

Ethereum Foundation (2022) Introduction to Dapps. Available at: https://ethereum.org/en/developers/docs/dapps/

Etherscan (2021) CryptopunksData Smart Contract. Available at: https://etherscan.io/address/0x16f5a35647d6f03d5d3da7b35409d65ba03af3b2#code

Fenbushi Capital (2021) Stratos: build “convenience store” network for decentralized storage. Available at: https://fenbushi.medium.com/stratos-build-convenience-store-network-for-decentralized-storage-7cd7dd0d2b49

Georgios Konstantopoulos & Leo Zhang (2021) Ethereum Blockspace – Who Gets What and Why. Available at: https://research.paradigm.xyz/ethereum-blockspace

Internet Computer (2022) Computation and Storage Costs. Available at: https://internetcomputer.org/docs/current/developer-docs/deploy/computation-and-storage-costs

Kofi Kufuor (2021) The State of NFT Data Storage. Available at: https://thecontrol.co/the-state-of-nft-data-storage-c471c1af58d5

Larva Labs (2021) On-chain Cryptopunks. Available at: https://www.larvalabs.com/blog/2021-8-18-18-0/on-chain-cryptopunks

SnapFingersEditor (2021) Decentral Storage for NFTs | SnapFingers Weekly #9. Available at: https://medium.com/snapfingers/decentral-storage-for-nfts-snapfingers-weekly-9-2d9315320847

Stackexchange Forum Bitcoin (2015) Explanation of what an OP_RETURN transaction looks like. Available at: https://bitcoin.stackexchange.com/questions/29554/explanation-of-what-an-op-return-transaction-looks-like (Accessed May 15th, 2022)

Stackexchange Forum Ethereum (2016) What is the cost to store 1KB, 10KB, 100KB worth of data into the ethereum blockchain? Available at: https://ethereum.stackexchange.com/questions/872/what-is-the-cost-to-store-1kb-10kb-100kb-worth-of-data-into-the-ethereum-block

Uniswap (2020) Uniswap Interface + IPFS. Available at: https://uniswap.org/blog/ipfs-uniswap-interface

Uniswap (2022) Uniswap Frontend Interface Release on Github. Available at: https://github.com/Uniswap/interface/blob/main/.github/workflows/release.yaml

Uniswap (2022) Uniswap Github Code Repository. Available at: https://github.com/Uniswap/interface

(来源:比推)


