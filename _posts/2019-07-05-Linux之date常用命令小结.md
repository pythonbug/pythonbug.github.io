## 时间戳
```sh
date "+%s" # 1970年1月1号 0点0分0秒到当前时间的秒数，单位是秒
```

## 时间戳转换成日期格式
```sh
timestamp=`date "+%s"`

# 注意，这里的S是大写的表示“秒”，
#小写的s是时间戳，很长的一段数字，记住时，分，秒全部大写就可以了。
date -d @"$timestamp" "+%Y-%m-%d %H:%M:%S" 
```

## 日期转换成时间戳
```sh
time=$(date "+%Y-%m-%d")  # $()与``一样，都表示赋值
date -d "$time" "+%s"
```

## 前一天表示方法
```sh
date -d "1 days ago" "+%Y-%m-%d" # 这里的days写成day也可以
date -d -1days "+%Y-%m-%d" # 这里的days写成day也可以

# 37秒前
date -d "37 second ago" "+%Y-%m-%d %H:%M:%S"  # 注意这里的S是大写的，

# 明天怎么表示？
# 这里的days写成day也可以，一天之后的英语我试了 1 days later ，
# 1 days after好像都不行，有没有人知道的，可以留在评论中
date -d +1days "+%Y-%m-%d" 
```
## 小结
1、-d 后面接的是描述时间的字符串，可以是严格的日期格式，也可以非常拟人化的，比如 1 days ago ，nexrt Tuesday等等
2、时间格式前要加个 "+" 比如："+%s"、"+%Y%m%d"
3、%s表示时间戳 ，%S表示秒