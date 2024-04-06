# Cloud-搭建
云端搭建&SSH
1. 默认选择Pytorch 并且cuda版本>12
2. 开机后首先安装transformers库
3.安装好后 查看huggingface-cli env
```sys
root@autodl-container-5df045955b-e04e1810:~# huggingface-cli env

Copy-and-paste the text below in your GitHub issue.

- huggingface_hub version: 0.22.2
- Platform: Linux-5.15.0-47-generic-x86_64-with-glibc2.35
- Python version: 3.10.8
- Running in iPython ?: No
- Running in notebook ?: No
- Running in Google Colab ?: No
- Token path ?: /root/.cache/huggingface/token
- Has saved token ?: False
- Configured git credential helpers: 
- FastAI: N/A
- Tensorflow: N/A
- Torch: 2.1.2+cu121
- Jinja2: 3.1.2
- Graphviz: N/A
- keras: N/A
- Pydot: N/A
- Pillow: 10.2.0
- hf_transfer: N/A
- gradio: N/A
- tensorboard: N/A
- numpy: 1.26.3
- pydantic: N/A
- aiohttp: N/A
- ENDPOINT: https://huggingface.co
- HF_HUB_CACHE: /root/.cache/huggingface/hub
- HF_ASSETS_CACHE: /root/.cache/huggingface/assets
- HF_TOKEN_PATH: /root/.cache/huggingface/token
- HF_HUB_OFFLINE: False
- HF_HUB_DISABLE_TELEMETRY: False
- HF_HUB_DISABLE_PROGRESS_BARS: None
- HF_HUB_DISABLE_SYMLINKS_WARNING: False
- HF_HUB_DISABLE_EXPERIMENTAL_WARNING: False
- HF_HUB_DISABLE_IMPLICIT_TOKEN: False
- HF_HUB_ENABLE_HF_TRANSFER: False
- HF_HUB_ETAG_TIMEOUT: 10
- HF_HUB_DOWNLOAD_TIMEOUT: 10
```
4. 把所有N/A的库通过pip安装
5. 将ENDPOINT设为国内镜像,这样就不用一直设置了
```sys
 echo 'export HF_ENDPOINT="https://hf-mirror.com"' >> ~/.bashrc
```
6.在云端中，系统盘很小，我们先转到存储盘创建文件夹并未后去huggingface模型存储做准备
```sys
root@autodl-container-5df045955b-e04e1810:~# cd /root/autodl-tmp/
root@autodl-container-5df045955b-e04e1810:~/autodl-tmp# mkdir huggingcache
root@autodl-container-5df045955b-e04e1810:~/autodl-tmp# cd h
hf/           huggingcache/ 
root@autodl-container-5df045955b-e04e1810:~/autodl-tmp# cd huggingcache/
```

7. 将huggingface的缓存地址也就是倒数后几个全部更改，通过变更HF_HOME 即可
```sys
root@autodl-container-5df045955b-e04e1810:~/autodl-tmp/huggingcache# echo 'export HF_HOME=/root/autodl-tmp/huggingcache' >> ~/.bashrc
```
8.为了激活快速下载hf-transfer，将HF_HUB_ENABLE_HF_TRANSFER: False 改为True
```sys
echo 'export HF_HUB_ENABLE_HF_TRANSFER=1' >> ~/.bashrc
```
9. 通过source ~/.bashrc存储（刷新）
10. 查询huggingface-cli env
```sys
root@autodl-container-5df045955b-e04e1810:~/autodl-tmp/huggingcache# source ~/.bashrc 
+--------------------------------------------------AutoDL--------------------------------------------------------+
目录说明:
╔═════════════════╦════════╦════╦═════════════════════════════════════════════════════════════════════════╗
║目录             ║名称    ║速度║说明                                                                     ║
╠═════════════════╬════════╬════╬═════════════════════════════════════════════════════════════════════════╣
║/                ║系 统 盘║一般║实例关机数据不会丢失，可存放代码等。会随保存镜像一起保存。               ║
║/root/autodl-tmp ║数 据 盘║ 快 ║实例关机数据不会丢失，可存放读写IO要求高的数据。但不会随保存镜像一起保存 ║
╚═════════════════╩════════╩════╩═════════════════════════════════════════════════════════════════════════╝
CPU ：15 核心
内存：80 GB
GPU ：NVIDIA A40, 1
存储：
  系 统 盘/               ：4% 1.2G/30G
  数 据 盘/root/autodl-tmp：1% 40K/100G
+----------------------------------------------------------------------------------------------------------------+
*注意: 
1.系统盘较小请将大的数据存放于数据盘或网盘中，重置系统时数据盘和网盘中的数据不受影响
2.清理系统盘请参考：https://www.autodl.com/docs/qa/
root@autodl-container-5df045955b-e04e1810:~/autodl-tmp/huggingcache# huggingface-cli env

Copy-and-paste the text below in your GitHub issue.

- huggingface_hub version: 0.22.2
- Platform: Linux-5.15.0-47-generic-x86_64-with-glibc2.35
- Python version: 3.10.8
- Running in iPython ?: No
- Running in notebook ?: No
- Running in Google Colab ?: No
- Token path ?: /root/autodl-tmp/huggingcache/token
- Has saved token ?: False
- Configured git credential helpers: 
- FastAI: 2.7.14
- Tensorflow: N/A
- Torch: 2.1.2+cu121
- Jinja2: 3.1.2
- Graphviz: 0.20.3
- keras: N/A
- Pydot: 2.0.0
- Pillow: 10.2.0
- hf_transfer: 0.1.6
- gradio: N/A
- tensorboard: N/A
- numpy: 1.26.3
- pydantic: 2.6.4
- aiohttp: 3.9.3
- ENDPOINT: https://hf-mirror.com
- HF_HUB_CACHE: /root/autodl-tmp/huggingcache/hub
- HF_ASSETS_CACHE: /root/autodl-tmp/huggingcache/assets
- HF_TOKEN_PATH: /root/autodl-tmp/huggingcache/token
- HF_HUB_OFFLINE: False
- HF_HUB_DISABLE_TELEMETRY: False
- HF_HUB_DISABLE_PROGRESS_BARS: None
- HF_HUB_DISABLE_SYMLINKS_WARNING: False
- HF_HUB_DISABLE_EXPERIMENTAL_WARNING: False
- HF_HUB_DISABLE_IMPLICIT_TOKEN: False
- HF_HUB_ENABLE_HF_TRANSFER: True
- HF_HUB_ETAG_TIMEOUT: 10
- HF_HUB_DOWNLOAD_TIMEOUT: 10
```
11. 小模型下载我们可以通过huggingface-cli download --resume-download 模型名字 来下载，但是如果模型比较大，容易终端并且不好断点重新下载
12. 我们使用https://zhuanlan.zhihu.com/p/663712983 这个教程的方法，使用hfd下载最稳定
13. 安装hfd
14. 因为hdf需要git clone https://gist.github.com/padeoe/697678ab8e528b85a2a7bddafea1fa4f，但是服务器在国内，所以需要配置加速
```sys
source /etc/network_turbo
```
15. 下载后cd到该文件夹，对里面的hfd.sh进行提权操作，操作如下,同时我们对hfd.sh 做一个快捷方式处理，用hfd直接指代
```sys
root@autodl-container-5df045955b-e04e1810:~/autodl-tmp/tool# git clone https://gist.github.com/padeoe/697678ab8e528b85a2a7bddafea1fa4f
Cloning into '697678ab8e528b85a2a7bddafea1fa4f'...
remote: Enumerating objects: 87, done.
remote: Total 87 (delta 0), reused 0 (delta 0), pack-reused 87
Receiving objects: 100% (87/87), 22.59 KiB | 462.00 KiB/s, done.
Resolving deltas: 100% (33/33), done.
root@autodl-container-5df045955b-e04e1810:~/autodl-tmp/tool# cd 697678ab8e528b85a2a7bddafea1fa4f/
root@autodl-container-5df045955b-e04e1810:~/autodl-tmp/tool/697678ab8e528b85a2a7bddafea1fa4f# chmod a+x hfd.sh 
root@autodl-container-5df045955b-e04e1810:~/autodl-tmp/tool/697678ab8e528b85a2a7bddafea1fa4f# alias hfd="$PWD/hfd.sh"
```
16. 输入hfd后发现可以使用aria2，也是更推荐的方式，通过以下方式安装
```sys
sudo apt update
sudo apt install aria2
```
17. 再次输入hfd 发现需要git lfs
```sys
curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash
sudo apt-get install git-lfs
```
18. 现在输入hfd就可以正常使用了
```sys
root@autodl-container-5df045955b-e04e1810:~/autodl-tmp/tool# hfd
Usage:
  hfd <repo_id> [--include include_pattern] [--exclude exclude_pattern] [--hf_username username] [--hf_token token] [--tool aria2c|wget] [-x threads] [--dataset] [--local-dir path]    

Description:
  Downloads a model or dataset from Hugging Face using the provided repo ID.

Parameters:
  repo_id        The Hugging Face repo ID in the format 'org/repo_name'.
  --include       (Optional) Flag to specify a string pattern to include files for downloading.
  --exclude       (Optional) Flag to specify a string pattern to exclude files from downloading.
  include/exclude_pattern The pattern to match against filenames, supports wildcard characters. e.g., '--exclude *.safetensor', '--include vae/*'.
  --hf_username   (Optional) Hugging Face username for authentication. **NOT EMAIL**.
  --hf_token      (Optional) Hugging Face token for authentication.
  --tool          (Optional) Download tool to use. Can be aria2c (default) or wget.
  -x              (Optional) Number of download threads for aria2c. Defaults to 4.
  --dataset       (Optional) Flag to indicate downloading a dataset.
  --local-dir     (Optional) Local directory path where the model or dataset will be stored.

Example:
  hfd bigscience/bloom-560m --exclude *.safetensors
  hfd meta-llama/Llama-2-7b --hf_username myuser --hf_token mytoken -x 4
  hfd lavita/medical-qa-shared-task-v1-toy --dataset
```
19.我们用HuggingFaceH4/zephyr-7b-alpha来测试
20.先去到我们想存储的文件夹下，通过cd指令
21. 直接下载，推荐先关闭网络代理,下载时推荐用--hf_token 令牌登录
```sys
hfd HuggingFaceH4/zephyr-7b-alpha --tool aria2c -x 4 --hf_token 令牌
```
22. 在后续使用中，Model_path = 模型存储位置，传入from_pretrained(Model_path)即可正常使用

------
TO BE continue..

23. huggingface需要认证的模型用以下template：
```sys
root@autodl-container-5df045955b-e04e1810:~/autodl-tmp/huggingcache# hfd sentence-transformers/sentence-t5-base --hf_username 你的username不是显示的名字不加引号 --hf_token 你的token不要加引号 --tool aria2c -x 4 
```


