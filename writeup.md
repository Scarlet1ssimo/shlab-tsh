## 姿势

- 无论子进程是怎么停下来的（前提是用到WUNTRACED option），都会给父进程发送SIGCHLD，所以所有子进程回收都应该在`sigchld_handler`中处理。
- 相对的，SIGINT和SIGTSTP的handler只需要负责给前台进程发送信号就行了。
- Shell 应该要给所有fork出来的子进程换组：`setpgid(0, 0)`
- 

## 坑

- 给kill加负数用来杀死所有子进程（整个进程组）
- `strtol`要用尾指针判断错误情形

## 不足

- waitfg不知咋的就对了
- 没有完全的线程安全：
    - 信号堵塞
    - errno没有keep
    - 用的不全是安全的函数。
- 写了一下午加一晚上，挺菜的