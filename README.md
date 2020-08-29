# leetcode

## 环境搭建

由于使用 `Sphinx` 生成文档，所以需要安装 Python。

推荐使用 `virtualenvwrapper` 管理虚拟环境

- `pip install virtualenvwrapper`
- add below to ~/.zshrc or ~/.bash_profile

	`export WORKON_HOME=~/.virtualenvs`
	
	`source /usr/bin/virtualenvwrapper.sh` 需根据真实安装目录调整，可尝试 `pip uninstall virtualenvwrapper` 查看

- `mkvirtualenv leetcode`
- `workon leetcode`
- `pip install sphinx`
- `make html`