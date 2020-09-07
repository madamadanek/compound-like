* 创建一个Comptroller 
**Comptroller.sol**
Comptroller()   ===> TErbQ6D7bQ9dxkEteKfjSmfyVpERq1sirG

* 创建一个CompToken(分发的token)              
**Comptroller.sol**  
Comp(TErbQ6D7bQ9dxkEteKfjSmfyVpERq1sirG)   => TRUSMbLN9Ma7BPiW1P3C1qUjheDiiTt33G

* 创建一个WhitePaperInterestRateModel          
**WhitePaperInterestRateModel.sol**
WhitePaperInterestRateModel(年利率 * 10^18, ?)
WhitePaperInterestRateModel(40000000000000000, 0) => TEhCWuZfvwxgHnua9zY7gGsb4bxeCvcxfK

* 基于当前的某一个ERC20 Token TJdViSYddZLmXZYKmMEUf21oZsAZEDA2cF

* 创建一个CErc20Token
**CErc20Immutable.sol**
CErc20Immutable(TJdViSYddZLmXZYKmMEUf21oZsAZEDA2cF, TErbQ6D7bQ9dxkEteKfjSmfyVpERq1sirG, TEhCWuZfvwxgHnua9zY7gGsb4bxeCvcxfK, 1000000000000000000, "name", "symbol", 18, TAiQSQ8YU4DLA9J7nh47XHhDTJHwuRvUDn) 
=> TKFkvYEF7QJqaW5sbWt89FAQHd4zqzVGuT

        (erc20token, comptroller, interestRateModel, initialExchangeRate, name, symbol, decimal, admin)

* 在原erc20 token上，授权新的CErc20 Token
   TJdViSYddZLmXZYKmMEUf21oZsAZEDA2cF.approve(TKFkvYEF7QJqaW5sbWt89FAQHd4zqzVGuT, xxxxx)

* 在comptroller合约里，先调整参数
  _setMaxAssets(10)   //更大也行

* 在comptroller合约里，注册新的CErc20Token
 _supportMarket(TKFkvYEF7QJqaW5sbWt89FAQHd4zqzVGuT)

* 每个用户使用前都需要注册该token
  enterMarkets(["TKFkvYEF7QJqaW5sbWt89FAQHd4zqzVGuT"])

* 创建一个测试priceOracle
**SimplePriceOracle.sol**
SimplePriceOracle() => TYZaQKWoaLhjddU9EaFQVsE2N15BESPPXq

* 设置一个测试价格
oracle.setUnderlyingPrice(TKFkvYEF7QJqaW5sbWt89FAQHd4zqzVGuT, 1000000000000000000)

* 更新oracle到comtroller
comptroller._setPriceOracle(TYZaQKWoaLhjddU9EaFQVsE2N15BESPPXq)

* 到这一步之后，应该可以mint和redeem（入金，出金）
 CErc20Token.mint/redeem 测试下

* 开启borrow
在comtroller里开启对应CErc20代币的借贷功能

* 设置资产抵押系数
_setCollateralFactor(TKFkvYEF7QJqaW5sbWt89FAQHd4zqzVGuT, 500000000000000000)

