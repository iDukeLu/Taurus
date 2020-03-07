# Linux/Mac 配置环境变量

## 配置环境变量的 3 种方式

Linux/Mac 均是 Unix 类型的系统，故它们配置环境变量的方式基本一致，通常环境变量有以下三种级别：

- 系统级环境变量：配置的环境变量，对所有用户生效
- 用户级环境变量：配置的环境变量，仅对当前用户生效
- 临时境变量：配置的环境变量，当前用户生效，退出后环境变量被清除

> 优先级：临时 > 用户级 > 系统级，优先级高的会覆盖优先级低的环境变量

### 1. 系统级环境变量

配置系统级环境变量，修改 `/etc/profile` 文件即可

- 编辑 `/etc/profile` 文件
  ```
  vi /etc/profile  
  ```
- 写入环境变量（这里以配置 Java 环境变量为例）
  ```
  # Java
  export JAVA_HOME=/opt/jdk/jdk1.8.0_241
  export PATH=$JAVA_HOME/bin:$PATH
  export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar  
  ```

- 使环境变量生效
  ```
  source /etc/profile  
  ```
  
### 2. 用户级环境变量
配置系统级环境变量，修改 `～/.bash_profile` 或 `～/.bashrc` 文件即可，`.bash_profile` 和 `.bashrc` 有什么不用可以参考这篇文章：[关于“.bash_profile”和“.bashrc”区别的总结](https://blog.csdn.net/sch0120/article/details/70256318)

- 编辑 `～/.bash_profile` 文件
  ```
  vi ～/.bash_profile
  ```
- 写入环境变量（这里以配置 Java 环境变量为例）
  ```
  # Java
  export JAVA_HOME=/opt/jdk/jdk1.8.0_241
  export PATH=$JAVA_HOME/bin:$PATH
  export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar  
  ```

- 使环境变量生效
  ```
  source ～/.bash_profile
  ```

### 3. 临时环境变量
配置临时环境变量，仅需使用 `export` 命令即可
```
export JAVA_HOME=/opt/jdk/jdk1.8.0_241
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar  
```
