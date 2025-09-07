# datetime模块

## 问题137：如何获取当前时间？

**答：**
datetime模块提供了多种获取当前时间的方法：

```python
from datetime import datetime, date, time

# 获取当前日期和时间
now = datetime.now()
print(f"Current datetime: {now}")

# 获取当前日期
today = date.today()
print(f"Today: {today}")

# 获取当前时间
current_time = datetime.now().time()
print(f"Current time: {current_time}")

# 格式化输出
formatted = now.strftime("%Y-%m-%d %H:%M:%S")
print(f"Formatted: {formatted}")
```

---

## 问题138：如何格式化时间？

**答：**
使用strftime()方法可以格式化时间输出：

```python
from datetime import datetime

now = datetime.now()

# 常用格式化符号
formats = {
    "%Y": "四位数年份 (2023)",
    "%m": "月份 (01-12)",
    "%d": "日期 (01-31)",
    "%H": "小时 (00-23)",
    "%M": "分钟 (00-59)",
    "%S": "秒 (00-59)",
    "%A": "星期全名 (Monday)",
    "%B": "月份全名 (January)"
}

# 示例格式化
print(now.strftime("%Y-%m-%d"))           # 2023-12-25
print(now.strftime("%H:%M:%S"))           # 14:30:45
print(now.strftime("%A, %B %d, %Y"))      # Monday, December 25, 2023
```

---

## 问题139：如何进行时间计算？

**答：**
datetime模块支持时间计算操作：

```python
from datetime import datetime, timedelta

# 创建时间对象
start_time = datetime(2023, 1, 1)
end_time = datetime(2023, 12, 31)

# 计算时间差
duration = end_time - start_time
print(f"Duration: {duration.days} days")

# 时间加减
now = datetime.now()
tomorrow = now + timedelta(days=1)
next_week = now + timedelta(weeks=1)
next_hour = now + timedelta(hours=1)

# 计算两个时间的差值
time1 = datetime(2023, 1, 1, 10, 30)
time2 = datetime(2023, 1, 1, 14, 45)
diff = time2 - time1
print(f"Difference: {diff.total_seconds() / 3600} hours")
```
