在 macOS 上安装和配置 dhtcrawler2，包括 Sphinx 和 Coreseek，可以按照以下步骤进行：

1. 安装依赖
安装 Erlang
使用 Homebrew 安装 Erlang：

bash

复制
brew install erlang
安装 MongoDB
通过 Homebrew 安装 MongoDB：

bash

复制
brew tap mongodb/brew
brew install mongodb-community
brew services start mongodb/brew/mongodb-community
2. 下载和配置 dhtcrawler2
克隆项目：

bash

复制
git clone https://github.com/btdig/dhtcrawler2.git
cd dhtcrawler2
3. 安装 Sphinx 和 Coreseek
安装 Sphinx
bash

复制
brew install sphinx
下载 Coreseek
前往 Coreseek 官方网站下载支持中文的版本。

4. 配置 Sphinx/Coreseek
创建 Sphinx 配置文件 在项目目录中创建 sphinx.conf：
plaintext

复制
source delta:xml
{
    type = xmlpipe2
    xmlpipe_command = cat /path/to/delta.xml
}
index delta:xml
{
    source = delta
    path = /path/to/data/delta
}
确保路径是绝对路径。
初始化 Sphinx 索引
bash

复制
indexer --config /path/to/sphinx.conf --all
5. 启动 Sphinx 服务
bash

复制
searchd --config /path/to/sphinx.conf
6. 配置 dhtcrawler2 使用 Sphinx
修改 priv/hash_reader.config 将 search_method 改为 sphinx。
修改 priv/httpd.config 同样，将 search_method 改为 sphinx。
7. 启动 dhtcrawler2
启动 Crawler
bash

复制
erl -pa ebin -s dhtcrawler start
启动 Hash Reader
bash

复制
erl -pa ebin -s hash_reader start
启动 HTTP 服务
bash

复制
erl -pa ebin -s httpd start
注意事项
确保所有路径正确，并且 Sphinx 和 Coreseek 的可执行文件在系统路径中。
根据需要调整配置文件中的参数以适应你的环境。


