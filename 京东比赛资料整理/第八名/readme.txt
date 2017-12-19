逻辑说明
建立一个子模型, 本段交易定义为这段交易前后2次交易时间不超过20min, 如果最近2h内登录过不同设备或IP, 就加入数据集
建立一个主模型, 本段交易定义为这段交易前后2次交易时间不超过20min, 本次登录定义为最近一次登录结果不为31的登录, 就加入数据集
Data Leak: 根据Val集制定白样本过滤策略, 对于前两步生成的结果集, 如果某段交易的那次登录城市, 3天前以及3天后, 用户都登录过, 从结果集中去除
代码说明
1. Data
 对所有数据新增一列row_name, 要求全局唯一
2. Feature
 导入Feature内的Intellij工程
 运行com.jd.login.v14.Feature14A.java, com.jd.login.v14.Feature14C.java, 生成训练测试特征数据
 注意运行其他package内.java, 生成前置map文件
 运行com.jd.login.WhiteList.java, 打印结果b.csv
3. Jupyter Notebook
 运行part1.ipynb, 生成子模型结果集a.csv
 运行part2.ipynb, 生成主模型结果集c.csv
 合并a.csv和c.csv, 去重复, 去除b.csv中的row_name, 生成最后结果集d.csv