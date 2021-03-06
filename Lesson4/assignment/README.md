## 硅谷live以太坊智能合约 第四课作业
这里是同学提交作业的目录

### 第四课：课后作业
- 将第三课完成的payroll.sol程序导入truffle工程
- 在test文件夹中，写出对如下两个函数的单元测试：
- function addEmployee(address employeeId, uint salary) onlyOwner
``` js
  // test addEmployee
  it("...add emoloyee successfully.", function () {
      return PayRoll.deployed().then(function (instance) {
          payrollInstance = instance;
      }).then(function(){
        return payrollInstance.addFund({value: web3.toWei(50)});
      }).then(function(){
        return payrollInstance.addEmployee(accounts[1], 2);
      }).then(function(){
        return payrollInstance.employees.call(accounts[1]);
      }).then(function(employeeData){
        assert.equal(employeeData[1].valueOf(), web3.toWei(2), "This employee doesn't have salary as 2!");
      });
    });
```

- function removeEmployee(address employeeId) onlyOwner employeeExist(employeeId)
```js
  // test removeEmployee
  it("...remove employee successfully.", function() {
    return PayRoll.deployed().then(function (instance) {
      payrollInstance = instance;
    }).then(function() {
      return payrollInstance.addEmployee(accounts[2], 5);
    }).then(function() {
      return payrollInstance.removeEmployee(accounts[2]);
    }).then(function() {
      return payrollInstance.employees.call(accounts[2]);
    }).then(function(employeeData) {
      assert.equal(employeeData[0].valueOf(), 0x0, "This employee is not removed yet!")
    })
  });
```
- 思考一下我们如何能覆盖所有的测试路径，包括函数异常的捕捉
![](https://github.com/yanyangbaobeiIsEmma/guigulive-operation/blob/master/Lesson4/assignment/testResult.png)
- (加分题,选作）
- 写出对以下函数的基于solidity或javascript的单元测试 function getPaid() employeeExist(msg.sender)
- Hint：思考如何对timestamp进行修改，是否需要对所测试的合约进行修改来达到测试的目的？
