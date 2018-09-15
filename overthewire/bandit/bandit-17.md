The password is the only line that's been changed between the two files. We can
use "diff" for this.

bandit17@bandit:~$ ls
passwords.new  passwords.old
bandit17@bandit:~$ diff passwords.new passwords.old 
42c42
< kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
---
> 6vcSC74ROI95NqkKaeEC2ABVMDX9TyUr

When you try to log in to bandit18, you'll get a "Byebye !". This is related to
bandit18.
