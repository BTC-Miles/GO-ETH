package main

import (
    "context"
    "fmt"
    "log"
    "math"
    "math/big"

    "github.com/ethereum/go-ethereum/common"
    "github.com/ethereum/go-ethereum/ethclient"
)

func main() {
    // 连接到以太坊节点，使用 Cloudflare 提供的公开节点
    client, err := ethclient.Dial("https://cloudflare-eth.com")
    if err != nil {
        log.Fatal(err) // 如果连接失败，输出错误信息并退出程序
    }

    // 指定以太坊账户地址，用于查询余额
    account := common.HexToAddress("0x71c7656ec7ab88b098defb751b7401b5f6d8976f")

    // 查询当前最新区块的账户余额
    balance, err := client.BalanceAt(context.Background(), account, nil)
    if err != nil {
        log.Fatal(err) // 如果查询余额失败，输出错误信息并退出程序
    }
    fmt.Println(balance) // 打印余额，单位为 wei (1 ETH = 10^18 wei)

    // 指定区块号，查询账户在该区块的余额
    blockNumber := big.NewInt(5532993)
    balanceAt, err := client.BalanceAt(context.Background(), account, blockNumber)
    if err != nil {
        log.Fatal(err) // 如果查询指定区块的余额失败，输出错误信息并退出程序
    }
    fmt.Println(balanceAt) // 打印在指定区块的余额，单位为 wei

    // 将余额从 wei 转换为以太币 (ETH)
    fbalance := new(big.Float)
    fbalance.SetString(balanceAt.String()) // 将余额转换为浮点数表示
    ethValue := new(big.Float).Quo(fbalance, big.NewFloat(math.Pow10(18))) // 除以 10^18 以得到 ETH 值
    fmt.Println(ethValue) // 打印余额的 ETH 值

    // 查询账户的待处理（未确认）交易的余额
    pendingBalance, err := client.PendingBalanceAt(context.Background(), account)
    if err != nil {
        log.Fatal(err) // 如果查询待处理余额失败，输出错误信息并退出程序
    }
    fmt.Println(pendingBalance) // 打印待处理余额，单位为 wei
}
