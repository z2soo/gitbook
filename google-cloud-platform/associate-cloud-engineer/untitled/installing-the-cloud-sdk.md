# Installing the Cloud SDK

SDK?

set of tools that allows us to interact with different google.   
cloud service is all from the command line.

how to use sdk is important!

최신 구글 installation 문서를 찾아서 따라 하는 것을 권장

{% embed url="https://cloud.google.com/sdk/install" %}

\([https://jybaek.tistory.com/825](https://jybaek.tistory.com/825)\)

설치 후 cmd로 확인

```text
C:\Users\user>gcloud --version
Google Cloud SDK 301.0.0
bq 2.0.58
core 2020.07.10
gsutil 4.51
```

![](../../../.gitbook/assets/image%20%28102%29.png)

gcloud init

```text
C:\Users\user>gcloud init
Welcome! This command will take you through the configuration of gcloud.

Your current configuration has been set to: [default]

You can skip diagnostics next time by using the following flag:
  gcloud init --skip-diagnostics

Network diagnostic detects and fixes local network connection issues.
Checking network connection...done.
Reachability Check passed.
Network diagnostic passed (1/1 checks passed).

You must log in to continue. Would you like to log in (Y/n)?
```

![](../../../.gitbook/assets/image%20%28134%29.png)

y하면 로그인 창으로 이동

![](../../../.gitbook/assets/image%20%28127%29.png)

```text

Your browser has been opened to visit:

    https://accounts.google.com/o/oauth2/auth?client_id=32555940559.apps.googleusercontent.com&redirect_uri=http%3A%2F%2Flocalhost%3A8085%2F&scope=openid+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fuserinfo.email+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcloud-platform+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fappengine.admin+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcompute+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Faccounts.reauth&code_challenge=drT8a2yAzJdt7xhXrW3ZKoreZc2sOgQQ5i2nEv3Webc&code_challenge_method=S256&access_type=offline&response_type=code&prompt=select_account


You are logged in as: [dlawltn118@gmail.com].

Pick cloud project to use:
 [1] groovy-works-283005
 [2] organic-premise-283004
 [3] oval-surfer-283510
 [4] Create a new project
Please enter numeric choice or text value (must exactly match list
item):

```

확인

```text
C:\Users\user>gcloud config list
[core]
account = dlawltn118@gmail.com
disable_usage_reporting = True
project = oval-surfer-283510

Your active configuration is: [default]

C:\Users\user>
```

