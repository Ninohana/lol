<div align="center">
  github.com/Ninohana/lcuClient<br/><hr/>
  一个封装完好的LCU API及SGP支持的Go Mod。
</div>

## 功能

 - 订阅客户端事件
 - 获取正在进行的对局信息
 - 获取召唤师信息（LCU/SGP）
 - 获取对局信息
 - 检查召唤师名称是否可用（有重复）
 - 通过puuid获取jwt
 - 观战
 - 获取回放文件

持续添加中……

## 快速开始

### 命令行方式

```shell
go get github.com/Ninohana/lcuClient
```

### 如果使用IDE

Go项目中使用`import`导入即可

```go
import "github.com/Ninohana/lcuClient"

// 或

import (
	"github.com/Ninohana/lcuClient"
)
```

大部分IDE会自动执行导入操作

### 使用示例

```go
// 创建LCU客户端
lcuClient := NewLcuClient("62529", BasicAuth{"riot", "JDJE18RKuT3fldK5yc2xuA"})

// 获取召唤师信息
summoner, _ := lcuClient.GetSummonerByName("我玉玉了#55165")
fmt.Println(summoner)

// 开启长连接
lcuClient.StartWebsocket(nil, nil)
// 监听事件
lcuClient.Subscribe("OnJsonApiEvent", func(data interface{}) {
		fmt.Println(data) // 直接输出
})

// 创建SGP客户端
sgpToken, _ := lcuClient.GetSgpToken() // 获取token
sgpClient := NewSgpClient(sgpToken.AccessToken, CQ100) // 班德尔城

// 获取正在发生的对局信息
gamingInfo, _ := sgpClient.GetGamingInfoByPuuid(summoner.Puuid)
fmt.Println(gamingInfo)
```

更详细的使用方法可以查看根目录下的测试类（以_test.go结尾的文件），例：[lcu_sgp_test.go](https://github.com/Ninohana/lol/blob/main/lcu_sgp_test.go)

## 社区共建

官方文档庞杂，个人能力渺小，需要社区的力量，欢迎Issue及PR，帮助改进、完善。如果该库能帮到你，还请不吝点个Star，感谢支持！

## 参考链接

LCU API官方文档

- https://riot-api-libraries.readthedocs.io/en/latest/lcuClient.html#lcuClient-explorer
- https://hextechdocs.dev/tag/lcuClient/
- https://developer.riotgames.com/docs/lol
- https://www.mingweisamuel.com/lcuClient-schema/tool/#/
