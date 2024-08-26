# ore-mine-pool


Ore-Mine-Pool是为OREV2实现的矿池，使矿工更容易挖矿。与 ore-cli 相比，它更易于使用且效率更高。


* ## 使用方法

```c
1. git clone https://github.com/orepool/ore-mine-pool.git
2. cd ore-mine-pool
3. chmod +x start.sh
4  screen -S ore-miner
5. ./start.sh wallet_address  // Linux启动启动方式
6. 指定solana钱包地址，用于接收ore，需要用户开启ore帐户（考虑私钥安全，所以用户自己创建）。
```


**PS**： 开户

只要钱包里面有ore就是已经开通了帐户，如果不确定是否开通可以上 [jup](https://jup.ag/swap/SOL-oreoU2P8bN6jkk3jbaiVxYnG1dCXcYxwhwyK9jSybcp)上兑换0.01ore，则会自动开通帐户。


* ## 工作原理


我们运行矿池服务器并使用多个钱包来获取挖矿任务。Miner 每 20 秒从服务器获取难度最低的当前任务，进行 20 秒的计算，并提交获得的最高难度答案。服务器记录难度最高的提交者的钱包。当任务需要在55秒内提交时，最高难度的答案将提交到区块链，并收取矿工费。


* ## 更高的计算效率


经过对市面上绝大多数矿池和官方 ore-cli 客户端的对比，我们发现官方客户端在多核设备上存在明显的局限性，通常需要多开多个实例才能将整个 CPU 的性能发挥到极致。而我们的客户端则无需进行多实例操作，只需运行一个程序即可。我们采用了多进程架构，并对核心进行了绑定，从而有效减少了调用开销，提升了整体算力和性能。


* ## 更好的公交选择


在矿石中，有 8 辆公共汽车（每辆都有 1/8 的奖励容量）。ore-cli 向随机选择的总线提交奖励，但总线之间存在不平衡。如果随机选择的公交车的奖励为零，则提交的奖励将为零。ore-miner选择最佳公交车进行提交（在链上查看最优公交车），确保全额奖励。效率的提高在这里没有量化。


* ## 双倍快乐


我们的矿池服务端已经实现ore+coal双挖功能，所以一次挖矿将会有两份奖励。


* ## 奖励领取原则


在使用我们的矿池时，您只需提供已开户的 ORE 钱包，即可实时领取奖励。与传统矿池不同的是，传统矿池虽然可以实时分配币，但打款到账时间通常需要两个小时以上，而我们的矿池通过合约提交的方式，在提交的同时即可将奖励直接领取到您的钱包，实现真正的实时到账。

由于采用了合约的方式，每一笔交易都可以在链上进行查询，包括我们的抽成比例，确保了绝对的透明化。


* ## 更易于维护


我们处理区块链交互，Miner只需要获取任务、计算和提交答案，无需处理复杂的区块链交互，使其更易于维护。我们在服务端使用帐户池的方式进行proof的请求和任务下发，用户无需自己维护多个私钥钱包。

只需要启动一个Miner者即可，钱包地址都是可以使用同一个，我们还提供多平台的Miner和相关脚本。


* ## 安全


只需要钱包公钥，没有私钥泄露的风险。


* ## 费用


在使用ore-cli提交奖励时，通常会产生 Gas 费用，这在许多情况下可能会消耗超过 50% 的奖励。相比之下，我们的矿池采用了创新的 ORE 抵扣 Gas 费用方案，大大减轻了用户的负担。

具体来说，当提交的难度较低时，如果 Gas 费用不足，由矿池会补足剩余部分。而在难度较高的情况下，系统会先从奖励中扣除 Gas 费用，剩余的奖励再按比例发放到用户账户。这种做法的主要优点包括：

1. **无需担心 Gas 费用问题**：用户不必为每次提交担心高额的 Gas 费用，因为矿池会处理这部分费用。
2. **防止被惩罚**：每笔提交都得到处理，确保提交不会因 Gas 费用问题而被惩罚。
3. **不影响未来奖励**：Gas 费用的处理不会影响后续提交的奖励，用户只有在实际盈利的情况下才需要承担 Gas 费用。

通过这种方案，我们确保了用户可以专注于挖矿，而无需过多关注 Gas 费用，提升了挖矿的整体体验和效率。


矿池费：抵扣gas后，进行15%分成(我们支付gas费、服务器维护费以及程序维护和更新费用）。

* ## 联系我们

[电报](t.me/minenodepool)
