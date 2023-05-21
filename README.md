## 

<div align="center">  
    <h1> FullTClash</h1>  
    <p>🤖 A Telegram bot that operates based on the Clash core </p>  
    <p>English        <a href="https://github.com/AirportR/FullTclash/blob/dev/README_zh_CN.md">简体中文</a></p>   
    <a href="https://fulltclash.gitbook.io/fulltclash-doc"><img src="https://img.shields.io/static/v1?message=doc&color=blue&logo=micropython&label=FullTClash"></a> 
    <img src="https://img.shields.io/github/license/AirportR/FullTclash">  
    <a href="https://app.codacy.com/gh/AirportR/FullTclash/dashboard?utm_source=gh&utm_medium=referral&utm_content=&utm_campaign=Badge_grade"><img src="https://app.codacy.com/project/badge/Grade/389b2787eb7647dfad486ccaa70eabf4"></a>  
    <a href="https://github.com/AirportR/FullTclash/issues"><img src="https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat"></a>  
    <br>  
    <a href="https://github.com/AirportR/FullTclash/"><img src="https://img.shields.io/github/stars/AirportR/FullTclash?style=social"></a>  
   <a href = "https://t.me/FullTclash"><img src="https://img.shields.io/static/v1?style=social&logo=telegram&label=channel&message=channel" ></a>  
   <br>  
   <br>  
</div>

## Introduction

FullTclash bot is a Telegram bot (hereinafter referred to as "bot") that carries out its testing tasks. It currently supports batch connectivity testing using Clash configuration files and supports the following test items:

- Netflix
- Youtube
- DisneyPlus
- Bilibili
- Steam Currency
- OpenAI (ChatGPT)
- Landing IP risk (IP fraudulence)
- Wikipedia

As well as HTTP latency testing and network topology testing (inbound and outbound analysis).

## Preview

Media streaming test:

![test picture](https://upload.cc/i1/2023/03/30/xyTGRu.png)

![test picture](https://upload.cc/i1/2023/03/30/1gdtWf.png)

## Getting Started

### Preparation

To successfully run the project code, you first need to prepare the following information:

- Telegram's api_id and api_hash [Get it here](https://my.telegram.org/apps) (Google it if you don't know how to get it) (Some Telegram accounts have been blacklisted and cannot be used normally)

- Create a bot from [@BotFather](https://t.me/BotFather) and get the bot_token, which should look like:
  
  bot_token = "123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11"

### Pulling the source code

Method 1: Direct download (everyone knows where to download, right?)

Method 2: Use Git (recommended for Linux, convenient for updates). First, install Git, and then clone the repository. The following command is an example for the Ubuntu distribution, for Windows please solve it yourself.

```shell
apt install -y git && git clone https://github.com/AirportR/FullTclash.git && cd FullTclash
```

This method may require a proxy to speed up in mainland China, please solve it yourself.

### Preparing the environment

- Python 3.9 or above.
- And various related package dependencies.

You can use the following command to quickly install the environment in the current project directory:

> Windows:
> 
> ```shell
> pip install -r requirements.txt
> ```

> Linux:
> 
> ```shell
> pip3 install -r requirements.txt
> ```

### Configuring

The following are the minimum requirements to start the bot. If you are a beginner, it is recommended that you start with the minimum requirements to avoid unpredictable errors caused by making random changes to the configuration.

- Admin configuration

Create a file named config.yaml in the ./resources directory. The project has a template example named ./resources/config.yaml.example. Enter the following information in config.yaml:

```yaml
admin:
- 12345678 #change to your telegram uid
- 8765431 #this is the second line, indicating the second administrator. If there is no second administrator, delete this line.
```

- Bot configuration

```yaml
bot:
 api_id: 123456 #change to your api_id
 api_hash: 123456ABCDefg #change to your api_hash
 bot_token: 123456:ABCDefgh123455  # bot_token, obtained from @BotFather
 # If you are in mainland China, the program needs a proxy to connect to the Telegram server. Enter the following information:
 proxy: 127.0.0.1:7890 #replace with your proxy address and port
```

- Proxy configuration (optional)

If you are in mainland China, some subscription URLs may not be directly accessible. You can enter the following information in config.yaml:

```
# Use a proxy when obtaining subscriptions (optional)
proxy: 127.0.0.1:7890 #replace with your proxy address and port. Note that this configuration is separate from the one above.
```

Getting the session file (optional)

You need to place a logged-in .session file in the project file directory. This file is generated by the program and looks like this: my_bot.session

Method 1: You can directly configure it in the config.yaml file, and the program will automatically read the values in the configuration file to generate the session file (make sure it is correct).

```yaml
#example configuration file, make sure the indentations are correct
bot:
 api_id: 123456
 api_hash: 123456ABCDefg
 bot_token: 123456:ABCDefgh123455
```

Method 2: You can refer to this document to quickly obtain a .session file with the suffix.

Method 3: In the ./utils/tool/ directory of the project, there is a file named login.py, which can be run with the following command:

```
python .\login.py
```

After the program exits, a file named my_bot.session will be generated, which can be moved to the project root directory. When it runs, it will try to send a message to the target username you entered. When you receive the message "Hi, I'm working normally!", it means that the session file is valid; otherwise, it is invalid.

If the verification fails after starting, delete the generated mybot.session file. The file is corrupted and cannot be used. If you do not delete it, the program will continue to use the corrupted file and will not regenerate it.

Starting the bot

After configuring the bot, run the following command in the project directory:

> Windows:
> 
> ```shell
> python main.py
> ```

> Ubuntu(Linux):
> 
> ```shell
> python3 main.py
> ```

Wait for the initialization process. If you see the message "The program has started!"(Chinese version), it means that it is running.

To communicate with the bot, use the following commands:

> /clash start: start clash core. Otherwise, all test results will be N/A.

> /testurl <subscription URL> (in clash configuration format) to start testing.

> /help: view all command instructions.     

### Compiling Dynamic Link Libraries (Advanced)

The dynamic link libraries used in the project are stored in ./libs/. Among them:

> fulltclash.so is supported by Linux-amd64, and fulltclash.dll is supported by Windows-amd64.

No architecture specified?
If you don't have a dynamic link library file for your architecture, such as arm64, or if you are concerned about security issues with the repository-provided file, you can compile it yourself.

There is a source code file named fulltclash.go in ./libs/. You need to compile the file into a dynamic link library fulltclash.so using the Golang compiler.
The general process is as follows:

- Install the Golang compiler on your platform (the higher the version, the better)
  
  ```shell
  go mod init <path>
  ```
  
  ```shell
  go mod tidy
  ```
  
  Here is an example of compiling for the arm64 architecture:
  
  ```shell
  go build -buildmode=c-shared -o fulltclash.so fulltclash.go
  ```
  
    Cross-compiling:
  
  ```shell
  GOOS=linux GOARCH=arm64 GOARM=7 CGO_ENABLED=1 CC=aarch64-linux-gnu-gcc CXX=aarch64-linux-gnu-g++ AR=aarch64-linux-gnu-ar go build -buildmode=c-shared -o fulltclash.so fulltclash.go
  ```
  
  After the compilation is complete, overwrite the original file.
  If the operation is too difficult, you can initiate an issue for detailed discussion.

### Docker Startup

Tutorial documentation to be updated.

### Setting Process Guardianship for Programs (Linux)

Due to the characteristics of the Linux system, the foreground program will be closed after the SSH connection is closed. You need to set up process guardianship to run the program continuously in the background. The specific method can be found by searching on Google.

## Communication and Discussion

We welcome feedback from all parties:

- Raise an issue on the project page

## References

- [Streaming Unlocking Idea](https://github.com/lmc999/RegionRestrictionCheck)
- [Clash](https://github.com/Dreamacro/clash)
- [aiohttp](https://github.com/aio-libs/aiohttp)
- [pyrogram](https://github.com/pyrogram/pyrogram)
- [async-timeout](https://github.com/aio-libs/async-timeout)
- [Pillow](https://github.com/python-pillow/Pillow)
- [pilmoji](https://github.com/jay3332/pilmoji)
- [pyyaml](https://github.com/yaml/pyyaml)
- [requests](https://github.com/psf/requests)
