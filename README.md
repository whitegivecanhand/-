哈希表
哈希表根据关键值直接访问数据的数据结构，通常用于快速判断一个元素是否在集合中
常用哈希表：数组、集合、映射
有效字母异位词 242
方法一：python通过创建字典进行快速查询
//首先通过长度判断是不是一致的
len1 = len(s)
len2 = len(t)
if len1 != len2:
   return False
//然后通过集合函数将两个字符串中不重复的字符收集起来
set1 = set(s)
set2 = set(t)
if set1 != set2:
  return False//如果元素不一样则直接返回
//创建字典进行查找
dict = {}
for i in set1:
  dict[i] = 0//创建的字典是建立了不重复的字符的映射
//通过字典进行查找
for i in range(len1):
  dict[s[i]] += 1//将两个字符串所有的字符在字典中体现
  dict[t[i]] -= 1//如果两者的字符种类和总量一致，最后字典所有值为0
  
//判断
for i in range(len1):
    if dicts[s[i]] != 0:
        return False
return True
方法二.C++通过ASCII码查找小写字符串
//首先创建一个空数组
int record[26] = 0;
//判断长度是否一致
if (s.length != t.length){
  return False;
}
//通过不同字符和a的ASCII码差别来定位数组位置
for (int i = 0;s[i] != '\n';i++){
  record[s[i] - 'a'] += 1;
  record[t[i] - 'a'] -= 1;
}
//判断是否为0
for(int i = 0;i < 26;i++){
  if(record[i] != 0){
    return False;
  }
}
return Ture 



两个数的交集349
//设置一个结果数组
result = []
//通过两个集合将不重复的数字提出来
s1 = set(s)
s2 = set(t)
//对两个集合进行遍历，找出一致的
for i in s1:
  if i in s2:
    result.append(i)
return result


两数之和 1
主要思路为判断目标数减去现有数组后的新数组与旧数组有没有交集
//建立一个字典，将现有数组存入，方便查询
hashmap = {}
//enumerate是枚举函数，会返回数值和数值下标
for ind,num in enumerate(nums): 
    hashmap[num] = ind//两个作用，记下数组同时标记数值位置,这里相对于初始化字典
for i,num in enumerate(nums):
    chazhiweizhi = hashmap[nums - target]//找寻差值在字典中是否存在，这里字典又相对于是新的数组
    if chazhiweizhi is not None and chazhiweizhi != i//如果差值存在于原字典，并且不是做差数值的坐标的话就输出
    return [i,j]
    
    
四数相加 454
主要思路是将前两个数搞成一组，通过字典将前两数的和进行一个归类
//初始化字典
dicts = collections.defaultdict(int)
n = len(nums1)
//将数组和整合到字典中
for i in range(n):
  for j in range(n):
    dicts[nums1[i] + nums2[j]] += 1//通过数值来表示这个和出现了多少次
count = 0 计数
for i in range(n):
  for j in range(n):
    if -(nums3[i] + nums4[j]) in dicts://判断后面两个值的负数是不是和前两个一致
      count = count + dicts[-(nums3[i] + nums4[j])]//这里需要注意的是需要找出所有的可能性，因此用字典来表示合理数值出现的次数
return count


