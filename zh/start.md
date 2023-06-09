# 快速开始

> 贡献者：[@ImPerat0R\_](https://github.com/tssujt)、[@zhongjiajie](https://github.com/zhongjiajie)

安装是快速而直接的。

```bash
# airflow 需要 home 目录，默认是~/airflow，
# 但是如果你需要，放在其它位置也是可以的
# (可选)
export AIRFLOW_HOME=~/airflow

# 使用 pip 从 pypi 安装
pip install apache-airflow

# 初始化数据库
airflow initdb

# 启动 web 服务器，默认端口是 8080
airflow webserver -p 8080

# 启动定时器
airflow scheduler

# 在浏览器中浏览 localhost:8080，并在 home 页开启 example dag
```

运行这些命令后，Airflow 将创建`$AIRFLOW_HOME`文件夹，并放置一个`airflow.cfg`文件，其默认值可以让您快速上手。您可以通过查看`$AIRFLOW_HOME/airflow.cfg`文件或者在 UI 的`Admin->Configuration`菜单中检查相关配置。如果由 systemd 启动，则 webserver 的 PID 文件将存储在`$AIRFLOW_HOME/airflow-webserver.pid`或`/run/airflow/webserver.pid`。

开箱即用，Airflow 使用 sqlite 数据库，由于使用此数据库后端无法进行并行化，因此您应该迅速替换它。它与`SequentialExecutor`一起使用，但仅能按顺序运行任务实例。虽然这是非常有限的，但它允许您快速启动和运行并浏览 UI 和命令行实用程序。

以下是一些将触发一些任务实例的命令。在运行以下命令时，您应该能够在`example_bash_operator`DAG 中看到任务的状态发生变化。

```py
# 运行第一个任务实例
airflow run example_bash_operator runme_0 2015-01-01
# 运行两天的任务回填
airflow backfill example_bash_operator -s 2015-01-01 -e 2015-01-02
```

## 下一步是什么？

通过以上的学习，您可以前往[教程](zh/tutorial.md)部分获取更多示例，或者前往[操作指南](zh/howto/index.md)进行更进一步的实践。
