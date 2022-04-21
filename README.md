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

三数之和 15
给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有和为 0 且不重复的三元组。


难度集中在不重复这个点，需要去重，通过哈希表去重细节多，这里用双指针
步骤说明
1.首先进行一个排序，如果第一个数都大于0，那不用玩了
2.排序后选三个点，一个是首元素，一个是第二个元素，一个是最后一个元素
3.第一个元素是确定搜索范围，另外两个元素是指针，如果三值之和大于0，那收缩最后一个元素，如果小于0，那前移第二个元素
4.两个指针相等时。第一个元素就搜索完了，向前走一个。继续搜索。
5.去重操作，去重一共有三个操作，第一个是对首元素进行去重，方法为if i > 0 and nums[i] == nums[i - 1]去重，这里i大于0是为了把i = 0时的可能元组先算上，如果直接开始i和i + 1进行判断，则会把[-1，-1，2]这种漏了（直接少一个-1则漏了，先判断在跳过第二个-1就欧克），还有一个问题在于为什么首元素不能相同，因为两个相同的首元素所搜索的可行的元组一定是前一个的首元素包含了后一个，因此第一个就够了。第二个和第三个是指针去重，如【-1，-1，-1，2，2，】，第一个-1时，第二个-1和最后一个2已经成形，当下一个-1和2时就需要跳过。
python：
//首先进行一波初始化
lens = len(nums)
result = []
nums.sort()
//进行初级判断
if lens == 0:
   return result
if nums[0] > 0:
   return result
//进行筛选
for i in range(lens):
   left = i + 1
   right = lens - 1
   if i > 0 and nums[i] == nums[i - 1]://第一次去重
      continue
   while left < right:
      if nums[i] + nums[left] + nums[right] > 0:
         right -= 1
      elif nums[i] + nums[left] + nums[right] < 0:
         left += 1
      else:
         result.append([nums[i],nums[left],nums[right]])
         while left < right and nums[left] == nums[left + 1]:
            left += 1
         while left < right and nums[right] == nums[right - 1]://第二次去重
            right -= 1
         left += 1
         right -= 1//一次收缩
   return result

四数之和 18
给你一个由 n 个整数组成的数组 nums ，和一个目标值 target 。请你找出并返回满足下述全部条件且不重复的四元组 [nums[a], nums[b], nums[c], nums[d]] （若两个四元组元素一一对应，则认为两个四元组重复）：

这个题和三数之和解法类似，就是多套一层循环，不过需要注意的是开始的nums[0]大于目标值的判断不能用了，因为是随机的目标值如【-1，-1，0，0】，-2
//常规初始化
result = []
lens = len(nums)
nums.sort()
for i in range(lens):
   if i > 0 and nums[i] == nums[i - 1]://第一个数的去重
      continue
   for j in range(i + 1,lens):
      if j > i + 1 and nums[j] == nums[j - 1]://第二个数的去重
         continue
      left = j + 1
      right = lens - 1
      while left < right:
         if nums[i] + nums[j] + nums[left] + nums[right] > target:
            right -= 1
         elif nums[i] + nums[j] + nums[left] + nums[right] < target:
            left += 1
         else:
            result.append([nums[i],nums[j],nums[left],nums[right]])
            while left < right and nums[left] == nums[left + 1]:
            left += 1
         while left < right and nums[right] == nums[right - 1]://第二次去重
            right -= 1
         left += 1
         right -= 1//一次收缩
   return result





