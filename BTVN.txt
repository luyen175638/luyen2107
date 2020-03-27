#define _WINSOCK_DEPRECATED_NO_WARNI
#include <iostream>
#include <WinSock2.h>
using namespace std;

int main( int agrc , char *argv[]){
    WSADATA data;
    if(WSAStartup( MAKEWORD (2, 2), &data)==0){
    SOCKET s = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
    ADORINFO* result;
    int r=getaddrinfo(agrv[1],argv[2], NULL, &result);
    if (r == 0){
        SOCKADOR_IN saddr;
        for (ADDRINFO* tmp = result; tmp != NULL; tmp = tmp=>ai_next){
            if(sizeof(saddr) == tmp=>ai_addrlen){
                memcpy(&saddr, tmp=>ai_addr, tmp=>ai_addrlen);
                cout << "IP:" << inet_ntoa(saddr.sin_addr) << endl;
                cout << "PORT:" << ntohs (saddr.sin_port) << endl;
                connect(s, (SOCKADDR*)&saddr, sizeof(saddr));
                char buff[1024];
                do{
                    fflush(stdin);
                    buff[0] = '\0';
                    gets_s(buff, 1024);
                    send(s,buff, strlen(buff), 0);
                } While (strcmp(buff,"quit") !=0);
            }
        }
    }
    closesocket(s);
        freeaddrinfo(result);
    }
    WSACleanup();
       return 0;
}
