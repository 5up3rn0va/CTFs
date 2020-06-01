## GENERAL

### Welcome!
![welcome](https://user-images.githubusercontent.com/47029515/83407403-4ae20a00-a42e-11ea-9941-9a0147d0ad59.png)

You can get the flag by sending `!flag` to the bot. Unfortunately, the bot wasn't responding.  Got the flag by dming the author.
```
castorsCTF{welcome_player_good_luck_and_have_fun}
```


## CODING

### Arithmetics
![arithmetics](https://user-images.githubusercontent.com/47029515/83408550-6b12c880-a430-11ea-9faa-2b7bca57e580.png)

Connecting to `nc chals20.cybercastors.com 14429` we get a bot that gives a number of simple arithmetic expressions that need to be solved very quickly. 

![arithemtics1](https://user-images.githubusercontent.com/47029515/83409984-22a8da00-a433-11ea-93b6-8c299ad316bd.png)

Looking around I find a similar challenge in [Alex CTF 2017](https://0xd13a.github.io/ctfs/alexctf2017/math-bot/). 

```python
from pwn import *

r = remote('chals20.cybercastors.com', 14429)

r.recvline_contains('Hit <enter> when ready.')
r.sendline()
while True:
	s = r.recvline(False)
	print(s)
	if s.endswith(b'?'):
		ans = str(eval(s[8:-1]))
		print(ans)
		r.sendline(ans)
```
After a number of iterations the system starts using numerals.

![arithmetics2](https://user-images.githubusercontent.com/47029515/83410422-03f71300-a434-11ea-9b32-5fc32c2c36a4.png)

I tried assigning variables for the numbers

```python
from pwn import *

one, two, three, four, five, six, seven, eight, nine = 1,2,3,4,5,6,7,8,9

r = remote('chals20.cybercastors.com', 14429)

r.recvline_contains('Hit <enter> when ready.')
r.sendline()
while True:
	s = r.recvline(False)
	print(s)
	if s.endswith(b'?'):
		ans = str(eval(s[8:-1]))
		print(ans)
		r.sendline(ans)
```

After a while it starts using words for the operators as well.

![arithmetics3](https://user-images.githubusercontent.com/47029515/83411076-29385100-a435-11ea-95c6-e94d06c95cd0.png)

**Final code:**
```python
from pwn import *

d = {'one':'1', 'two':'2', 'three':'3', 'four':'4', 'five':'5', 'six':'6', 'seven':'7', 'eight':'8', 'nine':'9', 'divided-by': '//', 'multiplied-by':'*', 'plus':'+', 'minus':'-'}

def replace_all(text, dic):
	for i,j in dic.items():
		text = text.replace(i,j)
	return text

r = remote('chals20.cybercastors.com', 14429)

r.recvline_contains('Hit <enter> when ready.')
r.sendline()
while True:
	try:
		s = r.recvline(False)
		print(s)
		if s.endswith(b'?'):
			a = s[8:-1].decode("utf-8")
			a = replace_all(a, d)
			ans = str(eval(a))
			print(ans)
			r.sendline(ans)
	except:
		print(r.recvuntil('}'))
		break
```
![arithmetics4](https://user-images.githubusercontent.com/47029515/83411424-d612ce00-a435-11ea-8b84-24de6f373719.png)
