## restart policy （重启策略）

`Docker` 提供了 restart policy 机制（重启策略），可以在容器或者 `Docker` 重启时控制器能够自启动。这种重启策略可以保证相关容器按照正确顺序启动。`Docker` 建议使用重启策略，并避免使用流程管理器启动容器。

重启策略跟 `dockerd` 命令的 `--live-restore` 标志不同。使用 `--live-restore` 标志可以在 `Docker` 升级的时候保证容器继续运行，但是网络以及用户终端输入会被终端。

## 使用重启策略

要为容器配置重启策略，使用 `docker run` 命令的时候添加 `--restart` 标志。`--restart` 标志有多个 `value` 可选

| 标志           | 描述                                                          |
| -------------- | ------------------------------------------------------------- |
| no             | 不自动重启容器（默认值）                                      |
| on-failure     | 如果容器由于错误而退出，则将其重新启动，非零退出代码表示错误  |
| unless-stopped | 在容器已经 stop 掉或 Docker stoped/restarted 的时候才重启容器 |
| always         | 只要容器停止，就重新启动                                      |

## 重启策略详情

- 重启策略只在容器启动成功后生效。这种情况下，成功启动的意思容器至少运行 10 秒以上，并且 `Docker` 已经开始监控它。这可以避免没有成功启动的容器陷入 `restart` 的死循环。
- 如果手动的停止容器，它将被重启策略忽略，直到 `Docker` 守护进程重启或手动重启，这是为了避免重启循环的另一次尝试。
- 重启策略只能用于容器，与 `swarm 服务` 的重启策略有不同的配置。
