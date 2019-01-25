#### The Power Mechanism Of Etherzero

##### Understanding the power mechanism

##### 一, Preface
* Power is the Etherzero initialization token coin ，it is generated by PoS ，can not trading  on exchange ，and only used to as the gas .Any accounts with 0.01 above will increasing their power of value until reach the ceils 

* Find Your own power value in geth console:
```
eth.getPower("your address")
web3.fromWei(eth.getPower("your address"), "ether")
```
![avatar](../img/power-console.png)
#### 二,Two attributes:
* 1,The maximum of Power( related to the balance of account)

* 2,The speed of power increasing (related to the balance of account)

#### Mechanism Of Power  
* 1,The Power of Each account 
Power = Min(PowerMax, BlockGap * PowerSpeed)
```
CurrentBlock = current block height 
LastBlock = the block height of last transaction of account
BlockGap = CurrentBlock  - tLastBlock 
```
* 2,The consuming Power for each transaction
PowerSpend = Gas * GasPrice
```
eg: In one transaction, the Gas is 21000，and the GasPrice is 18Gwei

18Gwei = 0.000,000,018 ether

The consuming power = 21000 * 0.000000018 = 0.000378 ether
```
* 3,The ceiling  of power for every transaction 
```
PowerMaxPowerMax = (Math.exp(-1/(x*50)*10000)*10000000+200000)*0.000000018


 eg. an account is 0.01 etz, so the PowerMax is 0.0036 ether

if GasPrice=18 Gwei（0.000000018 ether,Then the Gas = 0.0036 / 0.000000018 = 200000

For under the condition that GasPrice is 18 Gwei, this account cannot send transaction which gas is larger than 20,0000

Also if GasPrice is 36 Gwei（0.000000036 ether），
Then the gas for this account is  Gas = 0.0036 / 0.000000036 = 100000

So , if GasPrice  is 36Gwei, this account cannot send transaction which gas  is larger than 10,0000
```

![avatar](../img/exp-001.png)
* 4,The PowerSpeed for one account regain 
PowerSpeed = (Math.exp(-1/(x*2)*1000)*200000+1000)*0.000000018
![avatar](../img/exp-002.png)
```

eg ,for one account which balance is 0, at block number 100, its balance become 0.01 etz

At 101 block number,Power = (101 - 100) * 0.000018 = 0.000018

At 102 block number,Power = (102 - 100) * 0.000018 = 0.000036

At 201 block number,Power = (201 - 100) * 0.000018 = 0.0018

At 301 block number,Power = (301 - 100) * 0.000018 = 0.0036

At 401 block number,Power = (401 - 100) * 0.000018 = 0.0036 （not increasing any more ）
```

* After block number 401，for 0.01 ETZ of this account ,it has reached the ceil for the power mechanism ，if need more Power, add the balance of this account .

![avatar](../img/goetz.png)

#### 四,Balance-Power Statistics list
![avatar](../img/statistics.png)
* You may find for  an account which is 0.01 etz，in the single transaction, the Gas will 360,0000(Assuming the GasPrice is 1 Gwei).