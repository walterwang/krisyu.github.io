#UITableViewController


####步骤一初始化：


- Single View Application
- 默认设置好，禁止rotate（我是多懒）
- 删除默认的场景，拖拽出Table View Controller
- 记得将新的TableViewController名字与.h文件对应起来同时设置为初始场景


####步骤二开始添加方法：

当然

```

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section{
     ... ;
 }


-(UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath{
    ....
    return cell;
}



```