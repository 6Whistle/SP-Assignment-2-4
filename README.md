# 시스템 프로그래밍 실습 2 - 4 과제

### 이름 : 이준휘

### 학번 : 2018202046

### 교수 : 최상호 교수님

### 강의 시간 : 화

### 실습 분반 : 목 7 , 8


## 1. Introduction

```
해당 과제는 기존에 2 - 3 에서 만든 결과에서 추가적으로 덧붙어서 만들어진다. Cache파일
의 유무를 파악한 뒤 miss 상태일 경우 web server과 연결하여 web server에 요청받은
request를 보낸다. 이후 response를 cache 파일에 저장하고 해당 데이터를 client에게 보
낸다. hit의 경우 web과 연결하지 않고 cache파일에 있는 데이터를 client에게 보낸다. 이
외의 부분은 기존과 동일하게 만들어진다.
```
## 2. Flow Chart

- proxy_cache.c




## 3. Pseudo Code

```
static void handler(){
pid_t pid;
int status;
Wait Any child with WNOHANG
```
}

static void AlarmHandler(){

print No Response and exit(0);

}


char *getIPAddr(char *addr){

struct hostent* hent;

char *haddr = NULL;

char temp[BUFFSIZE] = addr;

token = temp(delete [http://,](http://,) and tokenized with /;

if (gethostbyname(token) is exist)

haddr = inet_ntoa(hent’s h_addr_list[0]);

return haddr;

}

Make_Cache_Dir_Log_File(char* cache_dir, char* log_file){

getHomeDirectory();

cache_dir = ~/cache;

log_file = ~/logfile;

set umask 000;

make cache and log directory;

log_file += /logfile.txt;

}

```
Check_Exist_File(char *path, char *file_name, int is_exist_file){
if(directory isn’t exist)
return 0;
```
```
DIR *dir = Open path directory
While(struct dirent *d = Read path directory){
If(d->name == file name)
```

```
Close directory and return 1;
}
Close directory and return 0;
```
}

```
Void Write_Log_File(File *log_file, char *input_url,
char *hashed_url_dir, char* hashed_url_file, int is_exist_file){
time_t now;
struct tm *ltp;
```
```
ltp = current local time;
if(miss state)
Write miss, input_url, local time in log_file;
Else
Write hit, hashed dir/file, local time, input_url in log_file;
}
```
void Check_Cache_Print_Web(int client_fd, char *url, char *cache_dir, char *log_file, char *buf
int current_pid, int len, int *hit, int *miss){

```
char[60] hashed_url;
char[4] first_dir;
char *dir_div;
char[100] temp_dir;
char *haddr[BUFFSIZE;
int h_socket_fd, cache_fd, h_len;
int is_exist_file = 1;
```

struct sockaddr_in web_server_addr;

hashed_url = hashed url using sha1;

first_dir = { hashed_url[0~3], ‘\0’ };

dir_div = hashed_url + 3 address

temp_dir = ~/cache/first_dir;

if make temp_dir directory(permission = drwxrwxrwx)

is_exist_file = 0;

is_exist_file = hit or miss state;

Write state, url, dir/file name, time in logfile.txt;

temp_dir = ~/cache/first_dir/dir_div;

if(state == miss){

```
haddr = getIPAddr from url;
if (make socket fd failed)
print error and exit();
setting web_server_addr using haddr;
if (connection with web failed)
print error and exit();
SIGALRM signal handling.
alarm 2 0 sec;
write buf’s request to web server;
open temp_dir with write mode;
while(receive response){
alarm off;
write response at cache file;
```

```
write response to client_fd;
h_buf clear;
}
close h_socket_fd;
}
else{
open temp_dir with read mode;
while read data is exist in cache file{
write data to client_fd;
h_buf clear;
}
}
close fd;
return is_exist_file;
}
```
void Sub_Process_Work(int client_fd, struct sock_addr, char *buf, char *char_dir, FILE
*log_file){

```
char temp[BUFFSIZE] = { 0 };
char method[BUFFSIZE] = { 0 };
char url[BUFFSIZE] = { 0 };
char h_buf[BUFFSIZE];
char* haddr;
char *token = NULL;
int len, h_socket_fd;
int state, hit = 0, miss = 0;
```

```
struct sockaddr web_server_addr;
pid_t current_pid = Current process ID;
time_t start_process_time, end_process_time;
Save start process time;
print Connect success with client address and port;
while read data from client_fd to buf is exist{
print Request message;
method = Request message’s method;
if(method == GET){
url = Request message’s url
state = Ceck_Cache’s state(Hit or Miss);
}
}
```
check end time;

print terminate state, running time, hit or miss state in logfile.txt

print Terminate connection with client address and port;

return;

}

main(void){

```
Make Cache and log directory and store path’s information;
if open socket is failed, print error and return;
update server’s address information;
if binding socket and server’s address data is failed, print error and return;
```

```
Waiting Connection and Collect SIGCHID signal using handler;
while true{
if connection didn’t occur, print error and return;
if make child process failed, close file descriptor and socket and continue;
if child process, Do Sub_Process_Work() and exit;
close client file descriptor;
}
```
close socket file descriptor;

}

## 4. 결과 화면

```
해당 함수는 signal함수에서 handling을 위한 함수로 waitpid(WNOHANG)을 통해
child process의 종료를 확인시켜주는 역할을 수행한다.
```

AlarmHandler()에서는 SIGALRM 에러가 왔을 경우 No response를 출력하고 exit()을
동작시킴으로써 error를 handling한다. getIPAddr()함수에서는 url을 입력으로 받으며
url에서 [http://을](http://을) tokenize하고 /까지를 tokenize하여 순수한 주소를 가져온다. 이를
가지고 gethostbyname()함수를 통해 host의 정보를 가져와 IP를 추출한다.

해당 함수는 기존의 cache directory와 log directory를 생성하고 log_file과
cache_dir의 path를 저장하는 역할을 수행한다.


해당 함수는 기존의 Ceck_Cache 함수에서 추가된 내용을 포함하는 함수다. 이전과
같이 hit와 miss를 판별한 후 miss일 경우 이전 Sub_Process_Work에서 Web과 연
결한 부분을 수행한다. 이 때 alarm은 사진을 받는데 오래 걸리기 때문에 20 초로
설정하며 while문을 통해 반복적으로 response message를 받아 이를 cache file에
저장하고 client_fd에게 전달한다. miss일 경우 cache file을 읽고 해당 내용을
client_fd에게 전달한다.

해당 함수는 2 - 3 에서 만든 내용을 Ceck_Cache_Print_Web 함수로 옮겼기 때문에 내
용이 적어졌다. 단 이번의 함수에서는 반복문을 통해 Request가 있는 동안에는 지
속적으로 받는 것으로 변경되었다.


해당 그림은 server의 메인함수다. 해당 함수에서는 socket을 열고 binding을 통해
server의 정보를 묶는다. 그리고 listen을 통해 연결을 받는다. 연결을 accept할 경
우 child process를 생성하여 Sub_Process_Work 작업을 수행한다.

해당 파일은 Makefile이다. proxy_cache.c의 파일을 proxy_cache 실행파일로 만드는
역할을 수행한다.


해당 그림은 기존의 cache와 logfile이 없는 상태에서 시작한다.

proxy_cache를 실행 후 주어진 첫 URL을 입력하였을 때 해당 페이지가 보여졌다.


#### 두 번째 URL을 입력하였을 때에는 초기에는 사진을 가져오는데 시간이 오래 걸렸

#### 지만 정상적으로 사진을 가져온 모습을 확인할 수 있었다.


firefox를 닫고 다시 해당 URL을 입력했을 때에는 아까보다 빠르게 사진을 가져오
는 모습을 볼 수 있었다.



다른 페이지들도 사진이 있으면 비교적 오래 걸리긴 했지만 정상적으로 response
를 가져오는 모습을 보였다.

log_file을 보면 hit와 miss 모두 잘 받아지며, 한 번의 프로세스에서 html과 사진을
가져오는 경우에는 해당 숫자가 request를 요청한 만큼 뜬다.


```
cache file을 살펴보면 다음과 같이 파일 내에 response의 내용이 제대로 저장되어
있는 모습을 볼 수 있다. 이를 통해 해당 과제가 성공적으로 만들어졌음을 확인하
였다.
```
## 5. 고찰

```
해당 과제를 통해서 기존 과제에서 더욱 나아가 web으로부터 내용을 받아 이를 저장하
고 client에게 전송해주는 작업을 수행했다. 이를 통해 response가 한 번에 오지 않고 여
러 번에 걸쳐 오기 때문에 while문으로 받아주어야 한다는 사실을 알았으며, request 또한
한 번만 오는 것이 아니라 response를 받은 내용에 따라 다시 여러 번의 request를 보낸
다는 사실을 알게 되었다. 그리고 과제 중 처음에는 cache에 내용을 입력할 때 File 포인
터를 사용하였지만 파일이 정상적으로 써지지 않는 오류가 일어났다. 때문에 해당 부분의
원인을 찾아 이를 file descriptor를 통한 작성으로 변경하여 해당 문제를 해결하였다.
```
## 6. Reference

### 강의 자료만을 참고


