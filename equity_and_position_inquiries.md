###权益和持仓的查询
---

在策略中，可以通过调用AccountDataManager.GetSnapshots()方法获取所有providerID下的账户权益和持仓的明细，或GetSnapshot(byte providerId, byte route)获取指定providerID下的账户权益和持仓的明细，调用示例如下：

```

private void AccountInfo()
{
    System.Console.WriteLine("AccountInfo ... .. . ..  ");
    //查询所有providerID的账户
    AccountDataSnapshot[] ads = this.AccountDataManager.GetSnapshots();
    System.Console.WriteLine("ads.Length=" + ads.Length);    
    
    //AccountDataSnapshot ads_ctp = AccountDataManager.GetSnapshot(99,99); //查询CTP通道的账户
            
    foreach (AccountDataSnapshot item in ads)
    {
	AccountDataEntry[] ades = item.Entries;
	foreach (AccountDataEntry ade in ades)
	{					
            AccountDataFieldList fields = ade.Values.Fields;                                
            foreach (AccountDataField field in fields)
            {                
                Console.WriteLine("{0} = {1}" , field.Name, field.Value);
            }

            AccountData[] pos = ade.Positions;                              
            foreach (var po in pos)
            {
                Console.WriteLine("----------------------------------------");
                var ad = (AccountData)po;
                foreach (AccountDataField field in ad.Fields)
                {
                    Console.WriteLine("{0} = {1}", field.Name, field.Value);                            
                }                        
            }
        }
    }
}
```

查询结果如下：
![](/assets/equity_and_position_inquiries.png)


